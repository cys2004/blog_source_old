---
title: Fiddler实现自动化抓取视频 
cover: https://p1.meituan.net/csc/bf93452b878608f25722aec791601b9d21692.webp
lang: zh-CN
---
  有时我们会有大量抓取某个网站视频的需求。编写爬虫固然是一个不错的选择，但当我们遇到URL构造困难、服务器限制爬虫抓取的情况时，利用Fiddler Script实现批量保存m3u8就不失为一个好的方法。

<!--more-->

>  此方法参考了[小强Bug](https://www.cnblogs.com/zgq123456/articles/11067924.html)和[fall_hat](https://blog.csdn.net/fall_hat/article/details/103400755)两位大佬的文章，在此表达感谢。

   本次测试目标为某个Android短视频APP。首先在Fiddler上配置好HTTP代理，接着在安卓端设置代理后浏览器访问代理服务器IP:代理端口，下载并安装根证书。图略。

   值得注意的是，Android 7.0之后系统默认不再信任用户安装的证书，因此在有些情况下即使已经安装了证书，在抓包一些APP时也会出现SSL认证失败。此时可以尝试在平行空间中打开APP抓包或直接用Magisk等工具Root设备后手动移动证书文件到/system/etc/security/cacerts目录下。具体方法本文不再赘述。

  配置好Fiddler代理后，打开右侧的Fiddler Script选项卡。如果抓取的视频为mp4等格式，只需在OnBeforeResponse()方法末尾加入以下代码。
```
oSession.utilDecodeResponse();//防止保存的响应存在乱码
if (oSession.oResponse.headers.ExistsAndContains("Content-Type", "video/mp4")) { 
    oSession.SaveResponseBody("D:\\temp\\" + oSession.SuggestedFilename);//文件保存路径，可自定义
}
```
   如果需要抓取m3u8流媒体，则首先需要保存相应m3u8文件的URL。在Fiddler Script中定位至**OnBeforeRequest()**方法，在末尾加入以下代码。
```
if (oSession.fullUrl.Contains(".m3u8"))//过滤无关请求，只关注含有.m3u8的请求
{
    var fso;
    var file;
    fso = new ActiveXObject("Scripting.FileSystemObject");
    file = fso.OpenTextFile("D:\\FiddlerSessions\\m3u8.txt",8 ,true, true);//文件保存路径，可自定义
    file.writeLine(oSession.url);
    file.close();
}
```
  修改后如图所示
![][1]
  保存脚本后开始抓取，结果如图。
![][2]
  我们可以看到，由于APP多次请求m3u8，抓取结果中出现了大量重复URL，使用文本去重工具处理即可。最后得到无重复的URL列表。
![][3]
  打开N_m3u8Downloader_SimpleG，设置好保存目录后直接将URL列表文件拖入M3U8地址填写处，启动批量下载。
  结果如图。
![][4]


[1]: https://p0.meituan.net/csc/e4a34c3b3d2b1ff8ca62e7265660d80361027.png
[2]: https://p0.meituan.net/csc/dc12b377869d28b7c37da646abfec6c078141.png
[3]: https://p0.meituan.net/csc/8f0f5ec26b965e8ffafbf2c5855cd86478501.png
[4]: https://p1.meituan.net/csc/90280583dc1e9ae21a433bb73419290849589.png