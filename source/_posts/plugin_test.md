---
abbrlink: plugin_test
categories: []
cover: https://m.360buyimg.com/babel/jfs/t1/42857/33/21834/110982/6391d6a7E0f7e939b/f80ac21d616260e6.jpg
date: 2023/1/19 12:00
lang: zh-CN
tags:
- 测试
title: Hexo插件测试
toc: true
updated: 2023/1/19 12:00
---
一些插件的测试和模板

<!--more-->

### [APlayer](https://github.com/MoePlayer/hexo-tag-aplayer)

{% aplayer "Oz." "yama" "https://ed.tcea.top/d/ChaIndex/Space/tcea/Oz.%20-%20yama.mp3" "https://m.360buyimg.com/babel/jfs/t1/83885/8/23877/7843/6391dfb5E51955899/26e1ca62783eb937.jpg" "lrc:https://ed.tcea.top/d/ChaIndex/Space/tcea/Oz.%20-%20yama.lrc" %}

````
{% aplayer "Oz." "yama" "https://ed.tcea.top/d/ChaIndex/Space/tcea/Oz.%20-%20yama.mp3" "https://m.360buyimg.com/babel/jfs/t1/83885/8/23877/7843/6391dfb5E51955899/26e1ca62783eb937.jpg" "lrc:https://ed.tcea.top/d/ChaIndex/Space/tcea/Oz.%20-%20yama.lrc" %}
````

### [DPlayer](https://github.com/MoePlayer/hexo-tag-dplayer)

{% dplayer "url=https://files.catbox.moe/yiyosy.mp4"  "pic=https://m.360buyimg.com/babel/jfs/t1/73739/4/23911/130885/6391e09eE00866593/7102aa15077a6f07.jpg" "loop=yes" "theme=#FADFA3" "autoplay=false" %}

```
{% dplayer "url= https://files.catbox.moe/yiyosy.mp4"  "pic=https://m.360buyimg.com/babel/jfs/t1/73739/4/23911/130885/6391e09eE00866593/7102aa15077a6f07.jpg" "loop=yes" "theme=#FADFA3" "autoplay=false" %}
```

### MuiPlayer

<!-- 引入基础样式文件 mui-player.min.css -->

<link rel="stylesheet" type="text/css" href="https://muiplayer.js.org/css/mui-player.min.css" />

<!-- 引入基础脚本 mui-player.min.js -->

<script type="text/javascript" src="https://muiplayer.js.org/js/mui-player.min.js"></script>

<div id="mui-player"></div>
    <script>
        // 初始化 MuiPlayer 插件，MuiPlayer 方法传递一个对象，该对象包括所有插件的配置
        var mp = new MuiPlayer({
            container: '#mui-player',
            title: '视频标题',
            src: 'https://muiplayer.oss-cn-shanghai.aliyuncs.com/static/media/media.mp4',
        })
    </script>

