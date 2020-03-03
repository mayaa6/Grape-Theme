---
layout: post
title: ICP备案支持的顶级域名
subtitle : ICP Supported Top Domains
tags: [Web]
category: blog
author: No Wonder
comments : True
redirect_from:
  - /beian-icp-top-domain-search/
---
众所周知，在中国大陆境内架设互联网服务，都是需要进行ICP备案的，否则都会被下线。正式的说法是这样的：

> 根据工信部《互联网信息服务管理办法》（国务院 292 号令），网站在未完成备案之前，不能指向大陆境内服务器开通访问。如果您的网站托管在中国大陆节点服务器，或者开通 CDN 服务，就必须申请 ICP（互联网内容提供商）备案。若网站服务器为非中国大陆节点，则不用申请备案。

关于ICP备案的权威解答，可以看[工信部ICP管理系统](http://www.miitbeian.gov.cn/)。如果不想阅读法律法规文件，也可以查看[阿里云的备案帮助](https://help.aliyun.com/knowledge_detail/36898.html)。

## 为什么要关心ICP备案

如果是个人用户，完全可以把网络服务部署在境外服务器上，这样可以免备案，比较方便。但是对于想做互联网生意的人，要在大陆靠互联网钱，就一定要有依照法律进行ICP备案。

常见的.com, .cn, .net顶级域名未注册资源资本已经枯竭，如果不想话高价收购，那么选择其他顶级域名是更具性价比的选择。于是对于域名投资者，能否进行ICP备案，也直接影响了域名的内在价值。

Google的母公司Alphabet公司网站域名是[abc.xyz](https://abc.xyz/)，其实这些域名在互联网从业者和年轻人中认可度已经比较高了。最大的阻碍是普通中老年大众，对他们来说网站就是.com。其实他们不知道，在.com之外还有一个很大的世界。

## 一个误解

不是所有顶级域名都可以进行ICP备案的，但是也绝对不止.com, .cn, .net, .org这几个。

有时也能看到一些老炮说出错误的信息，比如.la域名是不能进行ICP备案的。

阿里云上关于[域名备案的说明](https://help.aliyun.com/knowledge_detail/36904.html?spm=5176.doc59007.6.607.p3nHnh)，也并不准确：
> 市面上流通的域名后缀并非都可以备案。只有工信部收录的域名后缀才允许开放备案，目前工信部暂未收录 .pub/.rocks/.band/.market/software/.social/.lawyer/
> .engineer/.link/.click/.help/.gift/.pics/.photo/.news/
> .video/.win/.party/.date/.trade/.science/.online/
> .tech/.website/.space/.press/.wiki/.design/.live/
> .studio/.red/.loan/.bid/.mom/.lol/.work/.game/
> .store/.ltd 后缀的域名，故无法进行网站备案。

2017年12月14日的查询，上面提到的.tech, .online, .work, .ltd等定义域名都已经收录了， 可以进行ICP备案；.game， .lol等域名依然没有收录，不能进行ICP备案。

工信部收录的顶级域名并非是常年不变的：

根据百度知道上的[一个问答](https://zhidao.baidu.com/question/1049921757886904459.html)：
> 截止至2017年10月27日，管局可备案的域名一共是 467 个后缀。

而今天（2017年12月14日）的查询结果显示了439条记录。可以看出这个列表并不是常年不变的。

## 小工具

工信部的ICP管理系统的用户体验自然是非常差的。

主要的域名注册商也只发布和他们可以售卖的顶级域名相关的信息。比如常用的.me和.io域名，现在国内的域名注册商并没有售卖（可以直接从[godaddy.com](https://www.godaddy.com)上购买），也没有其消息。其实这两个域名都是可以进行ICP备案的，特别适合技术类产品。

做了下面这个小插件，方便查询。插件里面的数据每小时从工信部网站更新一次，基本可以保证及时准确。

<div id="domain_embed" style="height: 300px;"></div><script src=https://domain.nowonder.me/javascripts/embed.min.js async></script>

可以复制一下代码直接使用：

```html
<div id="domain_embed" style="height: 300px;"></div><script src=https://domain.nowonder.me/javascripts/embed.min.js async></script>
```

## 总结一下

还是有个小小的总结：

1. 如果在国内部署互联网服务，包括网站和小程序API等等，**一定要进行ICP备案和公安备案**；
2. 可以进行ICP备案的域名很多，而且也会增减更新；
3. 欢迎使用这个小插件查询可备案ICP顶级域名。
