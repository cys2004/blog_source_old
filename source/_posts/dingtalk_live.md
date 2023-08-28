---
title: 钉钉直播串流测试
cover: 
lang: zh-CN
toc: true
---

 利用vConsole获取钉钉直播的真实flv地址后使用flv.js和DPlayer实现网页端播放。

<!--more-->

<script src="https://fastly.jsdelivr.net/npm/flv.js@1.5.0/dist/flv.min.js"></script>
{% dplayer "url=https://dtlive-sz.dingtalk.com/live_hp/ae579b61-04dd-4023-923c-4ce343ccfc97.flv?app_type=win&auth_key=1676333091-0-0-7f28498fae5a82da7d2f3fcc1afac8dc&token=5146e66f86fe105eba7a2e528c075951DJZlp5DFIDZYDQDSQN3YCMRKlMCwZYu76yvd35kJdETiTFvZYfr5dZvXQPxZcEkI7b0AmrbbDXsLcuKWEOjfK8IOa1qLwgr3kfYNTAFS-tE=&version=7.0.0-Release.1109109"  "pic=" "loop=yes" "theme=#FADFA3" "autoplay=false" %}

```
<script src="https://fastly.jsdelivr.net/npm/flv.js@1.5.0/dist/flv.min.js"></script>
{% dplayer "url=https://dtlive-sz.dingtalk.com/live_hp/fcddd800-a59b-4aa0-905e-76b7b5f545db.flv?app_type=win&auth_key=1674175799-0-0-678d189ba4ebfd436425c5517438e872&token=b7b8d23d280cba27a7dddffad53691dccFCIt3w8E6XZuZZ0ws6q7ZiYZu0l5fzx60NjCkHSKzobROpU5h4kpJTCmB6mpOd8woj5rZiVGFAqKpMhM5buuKmTLmCbMrY_MSQl5O-l2ZY=&version=6.5.50-Release.11089104"  "pic=" "loop=yes" "theme=#FADFA3" "autoplay=false" %}
```

