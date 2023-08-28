---
title: Cloudflare Argo Tunnel实现零成本内网穿透 
cover: https://p0.meituan.net/csc/fc0a2fe1b9fcae273668faa89cde579a15465.png
lang: zh-CN
---

**Cloudflare Argo Tunnel 内网穿透演示站：[猹盘](https://ed.tcea.top/)**

众所周知，国内的运营商早在十多年前便封锁了家用宽带的80、443等端口，因此使用家宽建站需要改用其他端口。这样一来，用户在访问自建网络服务时就必须带端口号访问，不仅会使URL繁琐难看，而且有暴露源站引来攻击的风险。使用Frp等传统的内网穿透服务是常用的解决方案，但由于政策原因，国内的内网穿透服务只能绑定备案过的域名，况且长期购买稳定的内网穿透服务会是一笔不小的开支。此时，老牌云服务商Cloudflare免费提供的Argo Tunnel内网穿透服务就不失为一个好的选择。

<!--more-->
> 本文部分内容参考了[Hajeekn](https://blog.slqwq.cn/2021/posts/fktz6u/index.html)和[杰森](https://johnrosen1.com/2022/04/19/cloudflare/)两位大佬的文章，在此表达感谢。
## 优点

- 完全免费的内网穿透服务
- 无需备案便可绑定域名
- 可免费申请和部署HTTPS
- 良好的网络攻击防御能力
- 速度尚可，能满足一般中小型网站的需求

## 缺点

- 暂时不支持UDP协议
- 服务器位于海外，访问延迟稍高
- 带宽有限，不能满足大流量、高并发的应用场景

## 准备

- 一台具有网络连接的Linux服务器（即需要内网穿透的服务所在的宿主机。Windows系统请参阅[Hajeekn](https://blog.slqwq.cn/2021/posts/fktz6u/index.html)大佬的教程）
- 一个托管于Cloudflare的域名。如果域名托管在国内云服务商（如DNSPod、万网等），则需要修改NS记录指向Cloudflare分配的名称服务器以使用Cloudflare进行DNS解析。相关教程请参阅[Cloudflare Docs](https://developers.cloudflare.com/fundamentals/get-started/setup/)

## 流程

### 安装Cloudflared

用于运行Argo Tunnel服务的[Cloudflared](https://github.com/cloudflare/cloudflared/)开源于Github，可在[Releases](https://github.com/cloudflare/cloudflared/releases)处找到对应平台的安装文件。

Linux下使用以下命令来安装Cloudflared：

```bash
curl -LO https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
dpkg -i cloudflared-linux-amd64.deb
```

### 登录 Cloudflared
```bash
cloudflared tunnel login
```

执行命令后会显示一个URL，用浏览器打开，登录Cloudflare账号，然后选择用于内网穿透的域名。

成功后会自动生成证书，存放于`~/cloudflared/cert.pem`中。

### 新建隧道

下方命令里的<Tunnel-NAME>为隧道名称，可以随意起。

```bash
cloudflared tunnel create <Tunnel-NAME>
```

成功后会显示隧道的UUID，同时提示相关凭证已放置于`~/.cloudflared/<Tunnel-UUID>.json`中。

### 新建 Tunnel 对应的 DNS 记录

`<SUBDOMAIN>`填你想用来做内网穿透的域名，可以使用二级域名（example.com）或三级域名（www.example.com） 等。

```bash
cloudflared tunnel route dns <Tunnel-NAME> <SUBDOMAIN>
```

成功后会自动在选定域名下创建指向Argo Tunnel内网穿透服务器的CNAME记录。

### 建立配置文件

新建Cloudflared配置文件

```bash
vim ~/.cloudflared/config.yml
```

写入以下内容并保存

```yaml
tunnel: <Tunnel-UUID>
credentials-file: /root/.cloudflared/<Tunnel-UUID>.json
protocol: h2mux
originRequest:
  connectTimeout: 30s
  noTLSVerify: false
ingress:
  - hostname: <SUBDOMAIN>
    service: http://localhost:80
  - service: http_status:404
```

受限于国内网络环境，无法使用默认的`quic`协议建立隧道，因此需指定协议为`http2`或`h2mux`,以及本地服务地址`http://localhost:80`

### 配置Cloudflared服务

在systemd内新建Cloudflared服务文件

`vim /etc/systemd/system/cloudflared.service`

写入以下内容并保存

```bash
[Unit]
Description=cloudflared
After=network.target

[Service]
TimeoutStartSec=0
Type=notify
ExecStart=/usr/bin/cloudflared --loglevel debug --transport-loglevel warn --config /root/.cloudflared/config.yml tunnel run <Tunnel-NAME>
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

### 启动Cloudflared服务
```bash
systemctl enable cloudflared --now
```

等待一两分钟，然后通过刚才配置好的域名`https://<SUBDOMAIN>`访问你的服务即可。

## 参考资料

1. [Cloudflare 隧道内网穿透搭建记录](https://johnrosen1.com/2022/04/19/cloudflare/)

1. [Cloudflare 的 Argo Tunnel 使用](https://blog.slqwq.cn/2021/posts/fktz6u/index.html)

1. [Cloudflare Docs](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/)

1.  [Many services, one cloudflared](https://blog.cloudflare.com/many-services-one-cloudflared/)
