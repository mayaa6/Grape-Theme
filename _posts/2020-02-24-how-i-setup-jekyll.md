---
layout: post
title: 使用Jekyll重建我的博客
subtitle : How I Setup Jekyll for My Blog
tags: [Dev]
category: blog
author: No Wonder
comments : True
---

本文记录一下研究博客系统，并选用Jekyll搭建、部署本网站的过程。

## 起因

2017年的时候，使用ghost搭建了一个这个博客。在这个博客里面零星记录了点东西，就没有再维护。

如今做的事情越来越多，也越来越杂，经常要在不同工作状态中切换。所以就继续一个地方可以快速记录点东西，也方便快速查找。于是决定把这个blog重新建立起来。

## 博客系统的选择

之前用的ghost，因为那时候正在写node，所以没有怎么选择，就用了当时最热的node开源博客项目ghost。

首先看看ghost，版本已经更新了很多。看官方文档来看，ghost是按照付费阅读的路子发展的，__*更适合KOL建立自己的付费阅读平台*__。优点是有客户端，主题也比较丰富，缺点是除了blog，其他方便比较单一。

于是考虑使用静态站生成器。[staticgen.com](https://www.staticgen.com/)里面是一个非常全面的静态生成器的汇总，关于静态站的优势[jamstack.org](https://jamstack.org/)有一个不错的总结。

其中比较有名的项目有：

1. 基于node的Hexo
2. 基于Ruby的Jekyll
3. 基于Golang的Hugo
4. 基于react的Gatsby

因为没有用过golang，所以首先排除Hugo。React稍显复杂，也排除。剩下的Hexo和Jekyll都是比较丰富的生态。

看这两个的官方案例，Hexo国人用的很多，showcase和theme里面大量的中文资源，而Jekyll里面中国资源比较少。但是hexo的站点大多的单一的blog，而Jekyll则有大量的其他类型的站点：

1. 文档站点：[cssreference.io](https://cssreference.io/) 和 [htmlreference.io](https://htmlreference.io/)
2. 政府网站：[plainlanguage.gov](https://plainlanguage.gov/) [www.isomer.gov.sg](https://www.isomer.gov.sg/)

所以考虑这个站点以后还会添加一些静态页面小工具之类的东西，还是选择使用更灵活的Jekyll。

## Ruby基础知识

首先安装ruby环境，不要用macOS自带的ruby，要用brew安装一个用户版本的ruby。详见这篇文章：[如何替换掉macOS系统内置的Ruby]({% link _posts/2020-2-21-how-to-bypass-macos-system-ruby.md %})。

Gem是ruby的包管理器，是ruby的一部分，安装程序包使用`gem install`。

其他gem命令：

```bash
gem list
gem info
gem uninstall
gem cleanup
```

bundler独立于Gem，要单独安装`gem install bundler`。bundler与项目内管理依赖，包括读取Gemfile和生成Gemfile.lock。相当于ruby把node里面的npm的功能拆分成了gem和bundler两个部分。

## 主题选择

Jekyll的博客主题不如Hexo的丰富，可能是因为Jekyll的使用者并不局限于blog吧，都是在自己设计站点。

特别喜欢css-tricks和codepen那种暗色大字号的主题，发现有国人做了一个类似css-tricks的hexo主题：[三·钻](https://tridiamond.me/)，效果非常好，但是不能放在Jekyll里面用。从主题库里面选择了一款韩国人的主题[grape-theme](https://grape-theme.netlify.com/)进行修改，将原来白色系的主题改成了黑色系，效果大致也可以。

## 本地Jekyll开发

有三种方式新建Jekyll项目：

```bash
jekyll new myblog #新建使用默认主题的Jekyll，可以直接跑起来
jekyll new-theme #新建主题，包含空的Jekyll框架
bundle init #生成一个Gemfile
git clone ...  # 直接clone喜欢的jekyll主题拿来修改
```

Jekyll默认使用sass，如果需要使用更复杂一点的css构建方式，可以参考[cssreference.io](https://cssreference.io/)的方法，单独用gulp或者grunt处理css。

的比较神奇的是，Jekyll作为纯静态站，也可以实现文章搜索，使用的是[`jekyll_pages_api_search`](https://github.com/18F/jekyll_pages_api_search)。

对于中文站点，如果需要对文字进行截断，需要使用`truncatewords`代替`truncate`，`truncate`只适用于西方文字，详见[github](https://github.com/Shopify/liquid/issues/166)。

## Jekyll部署

可以直接将生成的静态文件上传服务器/pages服务/OSS，但是博客更新起来会比较麻烦。

如果想实现持续集成，也有四种方法：

1. 部署在github pages上：简单方便，在国内的访问速度不佳，也不会被百度收录，代码简单修改
2. 部署在netlify上：简单方便，访问速度不佳
3. 部署在国内的coding.net上：自己配置Jenkins
4. 部署在vps上：需要自行配置git hook来进行Jekyll编译

Jekyll的Jenkins配置可以参考[sketchingdev](https://sketchingdev.co.uk/blog/continuous-deployment-of-jekyll-website-with-jenkins.html)和[github](https://github.com/gravitee-io/gravitee-docs/blob/master/Jenkinsfile)。

选择了最省事儿的方法，使用部署在netlify上。配合cloudflare做前端，最终的在国内的速度还是可以接受的。

## 博客主题参考

下面是一些不错的博客主题：

### Hexo主题

* [iguan7u](https://iguan7u.cn/)
* [clover](https://esappear.github.io/clover/)
* [LITREILY](https://www.litreily.top/)
* [Solar Blog](https://tzvetkov75.github.io/demo_blog/public/): 暗色系带头部动画
* [cactus](https://probberechts.github.io/hexo-theme-cactus/cactus-dark/public/): 暗色主题
* [三·钻](https://tridiamond.me/)：模仿css-tricks
* [artifact](https://artifact.me/)
* Fluid： [Fluid](https://zkqiang.cn/) [rook1e](https://rook1e.com/) ：国产原创精品，亮点是头部cover图的打字效果

### Gatsby主题

* [ly你个c](https://www.lyyourc.com/)

### Jekyll主题

* [Next](https://simpleyyt.com/jekyll-theme-next/)
* [grape-theme](https://grape-theme.netlify.com/)：韩国人做的
* [jekflix](https://jekflix.rossener.com/):模仿netflix
* [MASSIVELY](https://iwiedenm.github.io/jekyll-theme-massively/)
* [Samarjeet Singh](https://thelehhman.com/)
* [dark reader](https://sharadcodes.github.io/jekyll-theme-dark-reader/)
* [Joon](http://vormwald.github.io/joon/)

## 总结

折腾下来的结果还算基本满意，接下来就是平时多补充内容了。

顺便发现了一些让人眼前一亮的音乐站点：[www.mailta.pe](https://www.mailta.pe/)，里面邀请了很多人来分享自己喜欢的音乐。

以后一年修改一次主题，保持新年新气象。
