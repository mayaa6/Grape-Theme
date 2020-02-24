---
short_name: macos
title: MacOS
image: macos.jpg
comments : True
---

## 命令行工具

Who's listening on specific port in Mac

```bash
lsof -nP -i4TCP:$PORT | grep LISTEN
```

Install developer tools

```bash
xcode-select --install
```

Cannot partition external drive

参考[apple discussions](https://discussions.apple.com/thread/7338380)

```bash
diskutil erasedisk hfs+ External GPT /dev/disk2
```

List directory size

```bash
du -hs *
```
