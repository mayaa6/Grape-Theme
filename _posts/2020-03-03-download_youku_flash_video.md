---
layout: post
title: 下载优酷flash播放器视频
subtitle : Download Youku Flash Player Video
tags: [macOS]
category: blog
author: No Wonder
comments : True
---

一些很古老的网站上还能找到flash格式的优酷网的播放器，这对于macOS用户是相当痛苦的。macOS默认是不支持flash的，所以这种老视频是完全看不到的。

怎么看到这些视频内容呢？方法如下：

## 第一步，获取视频ID

使用开发者工具获取flash player的url，如下：

```
http://player.youku.com/player.php/sid/XNzMxMDk1OTEy/v.swf
```

URL中`sid`之后，`v.swf`之前的部分就是次视频的id了，这个id在整个视频的生命周期中一般是不会改变的。

## 第二部，替换得到视频URL

随便打开是个优酷视频，观察到新版本优酷网的视频url如下：

```
https://v.youku.com/v_show/id_XNDU2Mzc2MDAwOA==.html
```

很明显`id_`之后接的部分就是视频ID，替换为之前得到的所需视频ID，得到所需视频的新版url:
```
https://v.youku.com/v_show/id_XNzMxMDk1OTEy.html
```

接下来的下载优酷视频，就很随意了。
