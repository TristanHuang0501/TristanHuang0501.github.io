---
layout:     post
title:      "我的博客搭建记"
subtitle:   "Hello World, Hello Blog"
date:       2017-01-24
author:     "Tristan"
header-img: "img/post-bg-unix-linux.jpg"
catalog:    true
tags:
- 操作流
- 日志
---

> 通过两天的摸索，终于能整出博客的大概样子出来了，总的来说并没有太过接触Jekyll框架底层的东西，只是在fork了hux大神的io项目之后做了调整和修改，熟悉了一下子Jekyll生成静态网页的原理、liquid模块语言、以及进一步熟悉了git和markdown。

### 项目来源
- fork自[hux大神的io项目](https://github.com/Huxpro/huxpro.github.io)
- 同时参考了[Bebop对于hux的branch分支](https://github.com/chaosinmotion/chaosinmotion.github.io)

### 参考的博文
- [阮一峰](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
- [使用Jekyll来写博客的一些心得](http://www.tuicool.com/articles/vENfq2)
- [使用java来自动初始化Jekyll的md文件](http://www.tuicool.com/articles/yu6vIfe)
- [jekyll+markdown+git+github](https://droidcat.bitbucket.io/2015/05/26/blog-or-wiki.html)

### 记录值得注意的地方
- _post 文件夹中放用来发表的文章：
  - 文件名格式：`yyyy-mm-dd-post-name.md`或者`yyyy-mm-dd-post-name.markdown`
  - 在开始写具体内容前，必须填写yaml头信息，这样该文件才能被Jekyll进行处理。头信息必须在文件的开始部分，并且按照yaml的格式，如本篇文章：
  
  ```
  ---
  layout:     post
  title:      "我的博客搭建记(Github+Jekyll)"
  subtitle:   " \"Hello World, Hello Blog\""
  date:       2017-01-23 22:26:00
  author:     "Tristan"
  header-img: "img/post-bg-unix-linux.jpg"
  catalog: true
  tags:
  - 操作流
  - 日志
  ---
  ```


- 本地访问博客
  - 在终端中cd到博客主目录，输入`jekyll serve`，这样会在`_site`中生成一系列的网站的文件并且启动服务，这时在浏览器中访问`localhost:4000`就能本地访问自己博客。


### 遗留和待改进
- 评论区的添加问题
- 网页的icon更换
- 设计合理的标签
- footer和侧边的facebook和豆瓣等标签的添加
- 域名绑定有问题，51tristan.top还是会跳到以前的主页上


### 感言
快过年啦，在年前终于把自己的小阵地打造好了，虽然我只是做了一点点的小工作，但还是有收获的。
祝大家鸡年大吉......吧 :)


### 后记
我的天呐，本来以为搞定了，因为首页看起来没问题，但是当我点进我的第一篇文章，也就是本文的时候，竟然发现样！式！丢！了！，我的天，为啥啊？我以为我是误删了什么东西，把整个项目用git一步步退回去，拿头顶了三个小时愣是没发现问题在哪儿，最后拷贝别人(bebop)博客的源文件到我的\_post里发现能够正常显示，我就把文档一步步删，删到正文全没了才发现是yaml的头出了问题，`tags:`后面换下一行不要空格，这个容易出问题！！**mark**
