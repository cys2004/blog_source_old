---
title: 辞旧迎新——荣耀畅玩7X（BND-AL10）刷机手记
cover: https://m.360buyimg.com/babel/jfs/t1/221156/11/14683/669884/63c69b14Fb5763414/3d20dbd73169c90d.jpg
lang: zh-CN
toc: true
---

由于系统崩坏等一系列原因，我在春节前夕彻底告别了伴随我两年之久的旧系统。本文简单记录了我的刷机过程。如有疑问，欢迎评论区交流。

<!--more-->

{% aplayer "扬旗鸣鼓【bilibili音乐·2022虚拟歌手贺岁纪单品】" "祈Inory, 多多poi" "https://files.catbox.moe/e2zsup.mp3" "https://m.360buyimg.com/babel/jfs/t1/213202/5/25123/120697/63c652d7F0fb332e3/02f2c40e431492b5.jpg" "lrc:https://files.catbox.moe/6pecu1.lrc" %}

## 刷入原厂固件

### 备份数据

**数据无价，备份数据是刷机前的首要准备工作。**

值得一提的是，在备份Via浏览器的书签时，我发现Via的开发者迫于服务器压力取消了云同步书签的功能。

所以说，Via浏览器还是很受欢迎的嘛。

### 获取固件和TWRP Recovery

{% raw %}<article class="message is-warning"><div class="message-header">{% endraw %}
注意
{% raw %}</div><div class="message-body">{% endraw %}
如无必要，**强烈不建议使用奇兔刷机等刷机工具提供的固件以及一键刷机服务。**
{% raw %}</div></article>{% endraw %}

如果想继续使用国行版系统的话，可以通过华为手机助手的升级或降级操作下载原厂固件。其下载的固件一般存储在`C:\Users\用户名\Documents\HiSuite\ROM`目录下。

但我此次想要尝鲜国际版固件，因此需要手动寻找匹配的固件。

在Google上以“BND-AL10 firmware stock”为关键字搜索，成功找到[所需固件](https://firmwarefile.com/honor-7x-bnd-al10)。

`Honor_7X_BND-AL10_9.1.0.140_C675E2R1P1T8_Firmware_9.0.0_R3_EMUI9.1.0_05015DEE_Dload.zip`

由文件名可知该固件为原厂固件，系统版本为EMUI9.1（Android9.0），国家地区代码为C675，[查表](https://onfix.cn/course/3836)后确认为印度版固件，自带完整的Google服务。

在[XDA论坛](https://forum.xda-developers.com/)上以“BND-AL10 TWRP”为关键字搜索得到[该机型的TWRP Recovery文件](https://forum.xda-developers.com/t/compilation-firmware-flash-emui-8-0-0-honor-7x-all-models.3833875/)。

{% raw %}<article class="message is-warning"><div class="message-header">{% endraw %}
注意
{% raw %}</div><div class="message-body">{% endraw %}
**该Recovery仅适配Honor 7X的出厂系统EMUI 8.0.0，如果后续通过OTA升级到EMUI 9.0/9.1，需要先通过华为手机助手降级到EMUI 8.0.0，然后再刷入TWRP Recovery。**
{% raw %}</div></article>{% endraw %}


### 解锁Bootloader
鉴于华为早在2018年就关闭了官方获取Bootloader解锁码的通道，现在只能通过非官方途径解锁Bootloader。此处建议通过淘宝等平台远程租用猎人加密狗等工具进行解锁。如果对自己没有信心，也可以直接购买第三方解锁服务，但价格会高出不少。

我的设备已经解锁了Bootloader，因此本次刷机无需进行这一步。

{% raw %}<article class="message is-warning"><div class="message-header">{% endraw %}
注意
{% raw %}</div><div class="message-body">{% endraw %}
**解锁Bootloader会清除个人数据，务必做好备份工作！**
{% raw %}</div></article>{% endraw %}

### 刷入TWRP Recovery

1. 在设备的开发者选项中启用USB调试，连接电脑后在手机弹出的对话框中授权USB调试。
2. 打开adb命令行，确认设备连接状态。
   `adb devices`
3. 通过adb重启设备到fastboot模式
   `adb reboot fastboot`
4. 刷入TWRP
   `fastboot flash recovery [TWRP Recovery的位置]`
5. 重启设备
   `fastboot reboot`
### 刷入固件

1. 解压出固件中的卡刷包`/Firmware/dload/update_sd.zip`。
2. 通过adb推送刷机包到设备存储。
   `adb push [卡刷包的完整路径] /sdcard`
3. 通过adb重启设备到TWRP Recovery
   `adb reboot recovery`
4. 在TWRP中进入“安装”界面，选中刚才推送的卡刷包，勾选“完成后重启”，滑动滑块确认安装。
5. 等待安装结束后设备重启进入新系统。

## 刷入Magisk

### 修补RAMDISK

1. 解压出卡刷包`update_sd.zip`中的`UPDATE.APP`文件

2. 下载HuaweiUpdateExtractor并打开，在`Settings`选项卡中取消勾选`Verify header checksum`。

3. 将刚才解压得到的`UPDATE.APP`文件拖动到程序窗口中，找到`RECOVERY_RAMDIS.img`，右键导出。

4. 使用adb将刚才导出的文件推送到设备存储。
   `adb push [RECOVERY_RAMDIS.img的位置] /sdcard`

5. 在设备上安装`Magisk Manager`，点击“安装”——“安装到Recovery”——“选择并修补一个文件”，然后选择刚才推送到设备存储中的`RECOVERY_RAMDIS.img`，等待文件修补完成。

6. 文件修补完成后，将设备存储Downloads目录下生成的以`magisk_patched`为文件名开头的文件复制到电脑上。
### 刷入修补后的RAMDISK

1. 使用adb重启到fastboot模式。
   `adb reboot fastboot`

2. 在fastboot模式下刷入修补过的ramdisk文件。
   `fastboot flash recovery_ramdisk [magisk_patched-xxx.img文件的位置]`

3. 刷入完成后重启手机到正常系统。
   `fastboot reboot`

4. 在正常系统中通过adb重启到Recovery。
    `adb reboot recovery`

    **此时的Recovery分区已经刷入了Magisk，执行此命令后将进入带有Magisk环境的系统，而不是先前的TWRP Recovery。**

5. 进入系统后，打开Magisk Manager，点击“安装”——“安装到Recovery”——“直接安装（推荐）”，等待Magisk安装完成后重启手机，自动进入带有Magisk的系统。

{% raw %}<article class="message is-warning"><div class="message-header">{% endraw %}
注意
{% raw %}</div><div class="message-body">{% endraw %}
以这种方式安装的Magisk位于Recovery分区内，需要从Recovery分区引导启动系统。由于 Magisk和Recovery都在同一个分区，因此进入系统或Recovery取决于开机时按下音量键时间的长短。即：

正常开机——进入到不含Magisk的系统；

同时按下音量+键和电源键开机——第一屏出现——放开所有按键——进入到启用Magisk的系统；

同时按下音量+键和电源键开机——第一屏出现——继续按音量+键——进入 Recovery。

但是，由于Magisk App此时已经了解设备的状态，因此可以直接在Magisk App中普通重启到启用Magisk的系统。
{% raw %}</div></article>{% endraw %}

## 刷入LSPosed

1. 在Magisk Manager的设置中启用Zygisk并重启。
2. 从LSPosed的[官方仓库](https://github.com/LSPosed/LSPosed/releases)中下载基于Zygisk的LSPosed模块压缩包（LSPosed-xxx-xxxx-zygisk-release.zip）。
3. 在Magisk中安装模块并重启后即可使用LSPosed。

## 参考文章

[[新手必看]华为刷机你一定要知道的 - 某贼](https://zhuanlan.zhihu.com/p/416456337)

[华为EMUI、HarmonyOS 系统ROOT安装Magisk(面具) - 东山海岛](https://www.bilibili.com/read/cv16261842)

[Magisk 安装说明 - 锦夏挽秋（译）](https://blog.csdn.net/qq1337715208/article/details/115922514)

<a class="tag is-dark is-medium" href="https://novelai.net/" target="_blank">
<span class="icon"><i class="fas fa-camera"></i></span>&nbsp;&nbsp;文章头图由NovelAI生成 </a>