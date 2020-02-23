---
short_name: video
title: Video
image: video.jpg
---
## FFMPEG 代码参考
### 合并多个mp3文件
```
ffmpeg -i "concat:file1.mp3|file2.mp3" -acodec copy output.mp3
```

### 合并文件夹内的所有mp4文件
```
ffmpeg -f concat -safe 0 -i <(for f in ./*.mp4; do echo "file '$PWD/$f'"; done) output.mp4
```

```
ffmpeg -f concat -safe 0 -i <(for f in ./*.mp4; do echo "file '$PWD/$f'"; done) -filter:v scale=608:1080 output.mp4
```

```
ffmpeg -f concat -safe 0 -i <(for f in ./*.mp4; do echo "file '$PWD/$f'"; done) -c copy output.mp4
```

### images to time lapse
```
// 1080P video
ffmpeg -r 25 -pattern_type glob -i '*.JPG' -vcodec libx264 -tune stillimage -filter_complex "[0]scale=1920:-1,crop=1920:1080" -b:v 20000k output.mp4

// 4K video
ffmpeg -r 25 -pattern_type glob -i '*.JPG' -vcodec libx264 -tune stillimage -filter_complex "[0]scale=3840:-1,crop=3840:2160" -b:v 20000k output.mp4
```

### 压制字幕
[ffmpeg.org:HowToBurnSubtitlesIntoVideo](https://trac.ffmpeg.org/wiki/HowToBurnSubtitlesIntoVideo)
[ffmpeg.org:filter documents](http://ffmpeg.org/ffmpeg-filters.html#subtitles-1)
[yaosansi's blog](https://www.yaosansi.com/post/ffmpeg-burn-subtitles-into-video/)

```
ffmpeg -i video.avi -vf subtitles=subtitle.srt out.avi
```

```
ffmpeg -i test.mov -vf subtitles=audio.srt:fontsdir=/Library/Fonts/:force_style='FontName=STIXSizTwoSymReg' out.mp4
```

```
ffmpeg -i video.avi -vf "ass=subtitle.ass" out.avi
```

### 静态图片和mp3合成视频
```
ffmpeg -loop 1 -y -i  image.jpg -i audio.mp3 -shortest -acodec copy -vcodec libx264 -tune stillimage -filter_complex "[0]scale=1920:-1,crop=1920:1080" -r 30 -b:v 2000k output.mp4
```

## Apple Motion 5教程

Motion5的教程不多，下面是一些制作比较精品的

* [AV-Ultra YouTube Channel](https://www.youtube.com/channel/UC0N-iKBpHZlhSFu6BqLsHWQ)
* [Simon Ubsdell Youtube Channel](https://www.youtube.com/channel/UC7c46tWEb2grLQ95OGLxBJQ)


## 国内的在线视频制作网站

喵影工厂桌面版
https://www.shencut.com/

来画视频（手绘风格视频）
https://www.laihua.com/

传影
https://www.chuanying520.com/

影大师
http://www.yingdashi.cn/

右糖
https://mv.lightmake.cn/

## fcpx/motion素材购买
[macsoft淘宝店](https://macsoft.taobao.com/)，这里都是写二手国外付费资源。