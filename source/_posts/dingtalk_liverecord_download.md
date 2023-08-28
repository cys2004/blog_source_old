---
title: 利用vConsole下载钉钉直播回放
cover: 
lang: zh-CN
toc: true
---

不出所料，我在学校集中隔离时被检出新冠阳性，因而不得不居家学习。于是，就有了这一次的旧活重整。

<!--more-->

{% aplayer "赴梦" "音阙诗听,小魂" "https://files.catbox.moe/c8rv2w.mp3" "https://p0.meituan.net/csc/c10add4ff3630ebd70af582681006680147805.jpg" "lrc:https://files.catbox.moe/2p1gtn.lrc" %}

### 配置代理

#### 配置Fiddler

在Fiddler里启用解密HTTPS流量并安装好根证书（不了解根证书的话勾选“解密HTTPS流量”后在弹出的窗口里一路点“是”即可），同时确保Fiddler为系统默认代理。

![](https://p0.meituan.net/csc/732ddebc7a986453f3819b63c5bd57ff15397.png)

#### 修改钉钉代理

在钉钉登陆界面右上角找到设置代理页面，改为Fiddler使用的代理地址和端口。

(代理地址通常为本机地址127.0.0.1，端口默认为8888)

提示：新版钉钉会自动使用本机浏览器代理，因此使用新版钉钉时配置好Fiddler后无需单独设置钉钉代理。

### 引入vConsole.js

在Fiddler的自定义脚本（FiddlerScript）界面找到**OnBeforeResponse**函数，并添加以下代码。

```
var sToInsert = "<script src='https://fastly.jsdelivr.net/gh/Tencent/vConsole@3.8.1/dist/vconsole.min.js'></script><script>var vConsole = new VConsole();</script>";
        oSession.utilDecodeResponse();
        oSession.utilReplaceOnceInResponse('</head>', sToInsert + '</head>', 0);
```

![](https://p1.meituan.net/csc/c66279c888bb9e138fe793234b5aa4c459422.png)

注意：一些较老的教程给出的引入vConsole的代码中直接使用了vConsole在jsdeliver中的地址，但由于[jsdeliver在国内无法使用](https://luotianyi.vc/6295.html)会导致引用失败。只需将代码中的```http://cdn.jsdelivr.net```替换为```http://fastly.jsdelivr.net```即可。

