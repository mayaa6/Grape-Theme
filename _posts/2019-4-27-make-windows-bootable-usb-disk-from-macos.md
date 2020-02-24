---
layout: post
title: 在macOS中制作Windows系统启动盘
subtitle : Make A Windows Bootable USB Disk From MacOS
tags: [macos, windows]
category: blog
author: No Wonder
comments : True
---

用macOS以后，避免了给自己电脑重装系统的麻烦，但是免不了给别人重装Windows系统。

说实话，经常需要给电脑重装系统还是个人使用习惯的问题。我之前的Windows电脑，一台2013年购买的zenbook超级本，一直用到现在都没有重装过系统。从一开始预装的Windows8，后来系统内升级到Windows10，到现在一切正常。

制作Windows启动优盘，在Windows里面一般使用ultraISO或者微软官方出品的[Windows USB/DVD Download Tool](https://www.microsoft.com/en-us/download/windows-usb-dvd-download-tool)。在macOS中，没有官方的工具，也不需要花时间去找第三方的ISO工具，直接用命令行就可以搞定。

## 制作启动优盘步骤

下载完成Windows的ISO镜像之后，插入优盘，使用`diskutil list`获取优盘的设备地址。

然后使用`diskutil eraseDisk`将优盘格式化，并设置分区表。

启动Windows需要的文件系统一般是`FAT32`，安装Windows XP等老系统的时候，也可能用到`MS-DOS`。

启动Windows用到的分区表一般是`MBR`或者`GPT`。其中`MBR`是很有年头的分区表格式，大部分系统都支持。`GPT`是新一代的分区表格式，目的是取代`MBR`。

一般用`FAT32`和`GPT`的组合不会错。但是如果遇到比较老的电脑或操作系统，不妨把文件系统和分区表排列组合一下，应该能得应付的过去：

```bash
#Usage:  diskutil eraseDisk format name [APM[Format]|MBR[Format]|GPT[Format]] 
#        MountPoint|DiskIdentifier|DeviceNode
 diskutil eraseDisk MS-DOS "WIN10" MBR /dev/disk2
 diskutil eraseDisk FAT32 "WINXP" MBR /dev/disk2
 diskutil eraseDisk MS-DOS "WINXP" GPT /dev/disk2
 diskutil eraseDisk FAT32 "WIN10" GPT /dev/disk2
```

本文参考：

1. [How Make a Windows 10 USB Using Your Mac - Build a Bootable ISO From Your Mac's Terminal](https://www.freecodecamp.org/news/how-make-a-windows-10-usb-using-your-mac-build-a-bootable-iso-from-your-macs-terminal/)
2. [What’s the Difference Between GPT and MBR When Partitioning a Drive?](https://www.howtogeek.com/193669/whats-the-difference-between-gpt-and-mbr-when-partitioning-a-drive/)