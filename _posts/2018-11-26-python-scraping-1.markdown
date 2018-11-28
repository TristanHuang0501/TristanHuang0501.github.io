---
layout:     post
title:      Web Scraping with Python（1）
subtitle:   开爬前的必要准备
date:       2018-11-26
author:     "Tristan"
header-img: "img/post-bg-git.png"
catalog:    true
tags:
- Web Scraping
- Python
---

在深入讨论爬取一个网站之前，我们首先需要对目标站点的规模和结构进行一定程度的了解。网站自身的 robots.txt 和 sitemap 文件都可以为我们提供一定的帮助，此外还有一些能提供更详细信息的外部工具，比如 Google 搜索和 WHOIS。

### 1. 检查 robots.txt

> 浙江大学计算机学院院长庄越挺：互联网网站页面，如同广阔农村中的一个菜园，各有其主。一般而言，访客进去逛逛无可厚非，但是如果主人在边界立下界碑：未经允许不得入内，这就意味着主人的意愿成为外界是否获准入园参观的标准。Robots协议就是这样一块界碑，它虽然不具法律效应，但是人们都普遍遵循。未经允许入园就参观不仅违反了游戏规则，也有违道德标准。同样的道理，违反Robots协议，等同于违背了搜索引擎的行业规范，以这种方式获取资源是一种不道德的竞争。

#### 什么是 robots.txt ？

robots.txt（统一小写）是一种存放于网站根目录下的ASCII编码的文本文件，它通常告诉爬虫此网站中的哪些内容是不应被爬虫获取，哪些是可以被获取。大多数网站都会定义 robots.txt 文件，这样可以让爬虫了解爬取该网站时存在哪些限制。这些限制虽然仅仅作为建议给出，但是良好的网络公民都应当遵守这些限制。更多内容可以看 [wiki](https://zh.wikipedia.org/wiki/Robots.txt) 或者 [baidu](https://baike.baidu.com/item/robots协议)。

#### robots.txt 的作用？

1. 保护网站安全
2. 节省流量
3. 禁止搜索引擎收录部分页面
4. 引导蜘蛛爬网站地图


#### robots.txt 在哪里？

robots.txt文件存放在网站根目录下，并且文件名所有字母都必须小写。比如以下的几个：
- 百度：[https://www.baidu.com/robots.txt](https://www.baidu.com/robots.txt)
- 淘宝：[https://www.taobao.com/robots.txt](https://www.taobao.com/robots.txt) 
- 京东：[https://www.jd.com/robots.txt](https://www.jd.com/robots.txt)
- 阿里云：[https://www.aliyun.com/robots.txt](https://www.aliyun.com/robots.txt)
- 知乎：[https://www.zhihu.com/robots.txt](ttps://www.zhihu.com/robots.txt)

#### 怎样写自己的 robots.txt？

可以参考这里的语法，以后再具体补充：[网络营销师胡薇分享robots.txt的写法 - 小小不点酱的文章 - 知乎](https://zhuanlan.zhihu.com/p/23379013)

### 2. 检查 sitemap






