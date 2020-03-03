---
layout: post
title: 奇怪的jade-lang!
subtitle : Obsolete Jade Language and Pug Language
tags: [Dev]
category: blog
author: No Wonder
comments : True
redirect_from:
  - /old-jade-project/
---
## 起因
这几天写一个项目，使用express-cli初始化项目，看了一眼express-cli的配置参数：

![express doc screenshot](http://cdn1.zenocean.cn/201712/jietu20171210-192535.jpg)

express中提供了jade和pug的支持，默认设置为jade。
大概一年前，由于商标问题，jade项目已经改名为pug（[官网](https://pugjs.org/api/migration-v2.html)、[知乎讨论](https://www.zhihu.com/question/46418330/answer/101389532)）:
> Due to a trademark issue, the project name has been changed from “**Jade**” to “**Pug**” in conjunction with the release of Pug 2. This also means that we have changed the official supported file extension from `.jade` to `.pug`. Although `.jade` is still supported, it is deprecated. All users are encouraged to transition to `.pug` immediately.

那么express默认支持jade，而不是pug又是什么情况呢？

## 疑惑
先找到jade的网站[jade-lang.com](http://jade-lang.com)看看:

![jade_website_new](http://cdn1.zenocean.cn/201712/jietu20171212-170441.jpg)

和以前的不一样，之前的官网是这样：

![jade_website_old](http://cdn1.zenocean.cn/201712/jade_website_old.jpg)

### jade网站改版了

jade项目的官网已经进行的改版，页面底部显示了2017年。内容方面，jade新网站去掉了github和change log等代码信息，只保留了基础的文档。但是新版网站没有跳转到pug项目网站的链接，也没有任何明显的表明和pug项目关系的文字，好像和pug项目没什么关系似的。但是[官方关于更名的声明](https://github.com/pugjs/pug/issues/2184)可不是这样说的：
> The new website will be at www.pugjs.org (which I have registered). Once that website is built, http://jade-lang.com/ will be updated to redirect to www.pugjs.org

### jade网站的内容
新jade站的内容和pug站的文档部分大致相同，但是仔细比较，也有不少文字内容上的不一致。不一致之处几乎都是无关键要的语言表达方式的不同，比如：

pug网站关于attribute的[文档](https://pugjs.org/language/attributes.html)：
> Tag attributes look similar to HTML (with optional commas), but their values are just regular JavaScript.


jade网站关于attribute的[文档](http://jade-lang.com/reference/attributes)：
> Tag attributes look similar to html, however their values are just regular JavaScript.

### wordpress
[在线检查](https://www.isitwp.com)，jade新站点使用了wordpress。一个美国开源项目文档站点使用了wordpress，确实有点罕见。
![jade website is wordpress](http://cdn1.zenocean.cn/201712/jietu20171212-161206.jpg)

对比一下，pug的站点就是用node+express+react开发的（[github](https://github.com/pugjs/pug-www)）。


## 调查
jade网站是不是还是pug的团队在维护着呢？

### 网站信息

分别查一下pug项目和jade项目的网站信息：

```bash
Non-authoritative answer:
Name:	pugjs.org
Address: 104.27.174.55
```

```bash
Non-authoritative answer:
Name:	jade-lang.com
Address: 178.62.122.47
```

![pasted-graphic-4](http://cdn1.zenocean.cn/201712/pasted-graphic-4.jpg)

![pasted-graphic-5](http://cdn1.zenocean.cn/201712/pasted-graphic-5.jpg)

pug项目网站指向 [cloudflare](https://www.cloudflare.com) ，jade项目的网站指向 [digital ocean](https://m.do.co/c/1784f959c124) 英国区的服务器。看上去好像也并不是一家。

### github和npm

再看一下express-cli的[代码](https://github.com/expressjs/generator/blob/master/bin/express-cli.js)：
```javascript
switch (program.view) {
  case 'dust':
    pkg.dependencies.adaro = '~1.0.4'
    break
  case 'jade':
    pkg.dependencies['jade'] = '~1.11.0'
    break
  case 'ejs':
    pkg.dependencies['ejs'] = '~2.5.7'
    break
  case 'hjs':
    pkg.dependencies['hjs'] = '~0.0.6'
    break
  case 'hbs':
    pkg.dependencies['hbs'] = '~4.0.1'
    break
  case 'pug':
    pkg.dependencies['pug'] = '2.0.0-beta11'
    break
  case 'twig':
    pkg.dependencies['twig'] = '~0.10.3'
    break
  case 'vash':
    pkg.dependencies['vash'] = '~0.12.2'
    break
}
```

可以看出，express使用的jade版本为~1.11.0，就是[npm](https://www.npmjs.com/package/jade)上发布的jade的最后一版。npm上面提供的github链接为[https://github.com/jadejs/jade](https://github.com/jadejs/jade), 会自动跳转到新的[https://github.com/pugjs/pug](https://github.com/pugjs/pug)。

同时看到jadejs的github组已经清空：
![jade github repository](http://cdn1.zenocean.cn/201712/jietu20171212-173128.jpg)

比较npm上统计的jade项目下载数目：

|                             | pug     | jade      |
|-----------------------------|---------|-----------|
| downloads in the last day   | 27,456  | 101,910   |
| downloads in the last week  | 158,098 | 658,194   |
| downloads in the last month | 660,485 | 2,738,285 |

jade的下载量总体为pug的4倍左右，看来大部分开发者还是认jade这个名字。

## 总结
全部的情况是这样的：
- jade网站没有按照官方的解释跳转到pug网站，也没有任何指向pug项目的信息；
- jade网站经过了重新的设计和开发，文档内容基本和pug保持一致；
- 从域名和服务器信息来看，jade网站和pug网站两个站点并没有直接联系。

猜测：
- 仍在使用老版本jade的同志还很多，所以临时用wordpress建站，继续维护着jade的项目网站

疑问：
- 为什么不在jade网站上把用户导入pug呢？难道因为jade的下载量，开发者已经放弃治疗了吗？

这么一点点小事儿，其实也没什么大不了的，只是觉得有点意思。