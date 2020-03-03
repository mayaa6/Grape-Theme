---
layout: post
title: 如何替换掉macOS系统内置的Ruby
subtitle : How To Bypass MacOS System Ruby
tags: [Dev]
category: blog
author: No Wonder
comments : True
---

在Windows中安装Ruby只需要从官网下载安装包，重复点击下一步。安装结束后，系统中保留了一个最新版本的ruby，可以直接使用。

但是在macOS中就稍显麻烦：由于macOS内置了一套Ruby，安装在`/Library/Ruby`。在使用gem安装程序包的时候会遇到目录写入权限的问题，而且系统内置的ruby的版本也不是最新的。所以在macOS中做ruby相关的开发，还是需要先处理一下ruby的问题的。

## 三种处理方法

大致有三种方式解决：

1. 使用sudo安装gem
2. 使用版本管理器rvm
3. 使用brew安装独立版本的ruby

使用sudo，可以在`/Library/Ruby`目录里面安装gem。但是既然设置了写入权限，这个目录就是系统不希望用户去碰的，所以还是不去碰为好。

使用rvm，类似于nvm，可以安装多个版本的ruby。然而我不是做ruby开发，只是用一下Jekyll做一个静态网站，所以也不必费次周折。

所以选择brew方法，方便，省心，升级起来也方便。

## 使用brew安装ruby

`brew install ruby`之后，需要做一个环境变量的调整：

> GEM_PATH provides the locations (there may be several) where gems can be found.
GEM_HOME is where gems will be installed (by default).
(Therefore GEM_PATH should include GEM_HOME).

所以需要设置`RUBY_HOME`和`GEM_PATH`两个环境变量：

```bash
export RUBY_HOME=/usr/local/opt/ruby/bin
export GEM_PATH=~/.gem/ruby/2.7.0
export PATH=$RUBY_HOME:$GEM_PATH/bin:$PATH
```

同样macOS也内置了python和perl，进行python和perl开发的之前也要先处理一下python和perl的版本问题。简单的开发都可以用brew安装一个用户版本的python和perl，具体方法可以参考：[docs.brew.sh](https://docs.brew.sh/Gems,-Eggs-and-Perl-Modules)。

本文参考：

1. [Gems, Eggs and Perl Modules--Homebrew Documentation](https://docs.brew.sh/Gems,-Eggs-and-Perl-Modules)
2. [Developer Headaches on macOS Catalina: Xcode, Homebrew, Gems](https://medium.com/faun/macos-catalina-xcode-homebrew-gems-developer-headaches-cf7b1edf10b7)
