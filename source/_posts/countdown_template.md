---
title: 高考倒计时控件测试
cover: 
lang: zh-CN
toc: true
---
<div class="box" >
{% raw %}<article class="message is-info"><div class="message-header">{% endraw %}
2023高考倒计时
{% raw %}</div><div class="message-body">{% endraw %}
<div class="gn_box">      <h3>距2023年高考还有</h3><center> <div id="CountMsg" class="HotDate"><span id="t_d">165 天</span><span id="t_h">3 时</span><span id="t_m">26 分</span><span id="t_s">46 秒</span></div></center> <script type="text/javascript">  function getRTime() {        var EndTime = new Date('2023/06/7 00:09:00');       var NowTime = new Date();       var t = EndTime.getTime() - NowTime.getTime();              var d = Math.floor(t / 1000 / 60 / 60 / 24);              var h = Math.floor(t / 1000 / 60 / 60 % 24);              var m = Math.floor(t / 1000 / 60 % 60);              var s = Math.floor(t / 1000 % 60);      var day = document.getElementById("t_d");     if (day != null) {         day.innerHTML = d + " 天";        }     var hour = document.getElementById("t_h");     if (hour != null) {         hour.innerHTML = h + " 时";       }     var min = document.getElementById("t_m");     if (min != null) {         min.innerHTML = m + " 分";        }     var sec = document.getElementById("t_s");     if (sec != null) {         sec.innerHTML = s + " 秒";     } }      setInterval(getRTime, 1000);      </script> </div>
{% raw %}</div></article>{% endraw %}
</div>
<!--more-->

```
<div class="box" >
{% raw %}<article class="message is-info"><div class="message-header">{% endraw %}
2023高考倒计时
{% raw %}</div><div class="message-body">{% endraw %}
<div class="gn_box">      <h3>距2023年高考还有</h3><center> <div id="CountMsg" class="HotDate"><span id="t_d">165 天</span><span id="t_h">3 时</span><span id="t_m">26 分</span><span id="t_s">46 秒</span></div></center> <script type="text/javascript">  function getRTime() {        var EndTime = new Date('2023/06/7 00:09:00');       var NowTime = new Date();       var t = EndTime.getTime() - NowTime.getTime();              var d = Math.floor(t / 1000 / 60 / 60 / 24);              var h = Math.floor(t / 1000 / 60 / 60 % 24);              var m = Math.floor(t / 1000 / 60 % 60);              var s = Math.floor(t / 1000 % 60);      var day = document.getElementById("t_d");     if (day != null) {         day.innerHTML = d + " 天";        }     var hour = document.getElementById("t_h");     if (hour != null) {         hour.innerHTML = h + " 时";       }     var min = document.getElementById("t_m");     if (min != null) {         min.innerHTML = m + " 分";        }     var sec = document.getElementById("t_s");     if (sec != null) {         sec.innerHTML = s + " 秒";     } }      setInterval(getRTime, 1000);      </script> </div>
{% raw %}</div></article>{% endraw %}
</div>
```