---
layout: post
title: 在ternimal中简单提取字节
subtitle : Work With Bytes In macOS Terminal
tags: [macOS]
category: blog
author: No Wonder
comments : True
---

在给[youtube-dl](https://github.com/ytdl-org/youtube-dl)贡献了一个extractor，文档中要求提供视频文件前10241个字节的md5值，作为测试的依据。

```python
{
'md5': 'TODO: md5 sum of the first 10241 bytes of the video file (use --test)',
}
```

所以问题来了，在terminal中怎么对文件做简单的以字节为单位的处理？

## 查一下文件有几个字节

使用`wc`命令，`-c`数字节, '-n'数行数：

```bash
wc -c yourtargetfile.mp4
```

## 获取文件的某些字节

`head`从开头获取文件的内容，`tail`从结尾获取文件内容：

```bash
head -c 10241 yourtargetfile.mp4 | md5
tail -c 10241 yourtargetfile.mp4 | md5
```
