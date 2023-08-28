---
title: Hexo插件测试
cover: https://m.360buyimg.com/babel/jfs/t1/42857/33/21834/110982/6391d6a7E0f7e939b/f80ac21d616260e6.jpg
lang: zh-CN
toc: true
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

### [yzmplayer](https://github.com/cairs00/yzmplayer)

<style type="text/css">
.video-container { display: block; position: relative; width: 100%; height: 0; overflow: hidden; box-sizing: border-box } .video-container iframe, .video-container video { position: absolute; top: 0; left: 0; border: none; width: 100%; height: 100% } .video-ratio-16by9 { padding-bottom: 56.25% /* 9/16 */ } .video-ratio-4by3 { padding-bottom: 75% /* 3/4 */ }
</style>

<div class="video-container video-ratio-16by9">
<iframe src="https://jx.777jiexi.com/player/?url=https://ed.tcea.top/d/ChaIndex/Space/cys/%E6%BB%A1%E8%B6%B3%E4%BD%A0%E5%AF%B9%E8%B5%9B%E5%8D%9A%E6%AD%8C%E5%A7%AC%E7%9A%84%E5%85%A8%E9%83%A8%E5%B9%BB%E6%83%B3%E3%80%8AI%20Really%20Want%20to%20Stay%20At%20Your%20House%E3%80%8B%E6%98%9F%E5%B0%98Infinity%E7%BF%BB%E5%94%B1/%E6%BB%A1%E8%B6%B3%E4%BD%A0%E5%AF%B9%E8%B5%9B%E5%8D%9A%E6%AD%8C%E5%A7%AC%E7%9A%84%E5%85%A8%E9%83%A8%E5%B9%BB%E6%83%B3%E3%80%8AI%20Really%20Want%20to%20Stay%20At%20Your%20House%E3%80%8B%E6%98%9F%E5%B0%98Infinity%E7%BF%BB%E5%94%B1_%E9%AB%98%E6%B8%85%201080P.mp4" allowfullscreen="" mozallowfullscreen="" msallowfullscreen="" oallowfullscreen="" webkitallowfullscreen="" frameborder="0"></iframe>
</div>

````
<style type="text/css">
.video-container { display: block; position: relative; width: 100%; height: 0; overflow: hidden; box-sizing: border-box } .video-container iframe, .video-container video { position: absolute; top: 0; left: 0; border: none; width: 100%; height: 100% } .video-ratio-16by9 { padding-bottom: 56.25% /* 9/16 */ } .video-ratio-4by3 { padding-bottom: 75% /* 3/4 */ }
</style>
            
<div class="video-container video-ratio-16by9">
<iframe src="https://jx.777jiexi.com/player/?url=https://ed.tcea.top/d/ChaIndex/Space/cys/%E6%BB%A1%E8%B6%B3%E4%BD%A0%E5%AF%B9%E8%B5%9B%E5%8D%9A%E6%AD%8C%E5%A7%AC%E7%9A%84%E5%85%A8%E9%83%A8%E5%B9%BB%E6%83%B3%E3%80%8AI%20Really%20Want%20to%20Stay%20At%20Your%20House%E3%80%8B%E6%98%9F%E5%B0%98Infinity%E7%BF%BB%E5%94%B1/%E6%BB%A1%E8%B6%B3%E4%BD%A0%E5%AF%B9%E8%B5%9B%E5%8D%9A%E6%AD%8C%E5%A7%AC%E7%9A%84%E5%85%A8%E9%83%A8%E5%B9%BB%E6%83%B3%E3%80%8AI%20Really%20Want%20to%20Stay%20At%20Your%20House%E3%80%8B%E6%98%9F%E5%B0%98Infinity%E7%BF%BB%E5%94%B1_%E9%AB%98%E6%B8%85%201080P.mp4" allowfullscreen="" mozallowfullscreen="" msallowfullscreen="" oallowfullscreen="" webkitallowfullscreen="" frameborder="0"></iframe>
</div>
````

### ArtPlayer

<div class="artplayer-app"></div>

<script src="https://cdn.jsdelivr.net/npm/artplayer/dist/artplayer.js"></script>

<script>
var art = new Artplayer({
container: '.artplayer-app',
url: 'https://files.catbox.moe/yiyosy.mp4',
});
</script>


```
<div class="artplayer-app"></div>

<script src="https://cdn.jsdelivr.net/npm/artplayer/dist/artplayer.js"></script>

<script>
var art = new Artplayer({
container: '.artplayer-app',
url: 'https://files.catbox.moe/yiyosy.mp4',
});
</script>
```

### MuiPlayer
<link rel="stylesheet" type="text/css" href="css/mui-player.min.css"/>
<script type="text/javascript" src="js/mui-player.min.js"></script>
<div id="mui-player"></div>
