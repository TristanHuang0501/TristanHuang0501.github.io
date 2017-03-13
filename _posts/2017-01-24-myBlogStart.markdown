---
layout:     post
title:      "我的博客搭建记"
subtitle:   Hello World, Hello Blog
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

### 本地搭建的最简单步骤
- 安装Ruby Installer
- 在cmd中输入`gem install jekyll`
- 在cmd中输入`gem install jekyll-paginate`
- cd到仓库中输入`jekyll server`
- 浏览器中输入`localhost:4000`即可本地调试

### 记录值得注意的地方
- _post 文件夹中放用来发表的文章：
  - 文件名格式：`yyyy-mm-dd-post-name.md`或者`yyyy-mm-dd-post-name.markdown`
  - 在开始写具体内容前，必须填写yaml头信息，这样该文件才能被Jekyll进行处理。头信息必须在文件的开始部分，并且按照yaml的格式，如本篇文章：
  
  ```
  ---
  layout:     post
  title:      "我的博客搭建记"
  subtitle:   Hello World, Hello Blog
  date:       2017-01-24
  author:     "Tristan"
  header-img: "img/post-bg-unix-linux.jpg"
  catalog:    true
  tags:
  - 操作流
  - 日志
  ---
  ```


- 本地访问博客
  - 在终端中cd到博客主目录，输入`jekyll serve`，这样会在`_site`中生成一系列的网站的文件并且启动服务，这时在浏览器中访问`localhost:4000`就能本地访问自己博客。

### GitHub Page的规定
尽管GitHub个人网站项目是免费的，但是却有一些限制。总体来说，完全够用，甚至太多了。
- 单个仓库大小不超过1GB，上传单个文件大小不能超过100MB，如果通过浏览器上传不能超过25MB
- 个人网站项目也不例外，最大空间1GB
- 个人网站项目每个月访问请求数不能超过10万次，总流量不能超过100GB
- 个人网站项目一小时创建数量不能超过10个

最新的规定在这里：[GitHub Page的规定](https://help.github.com/articles/what-is-github-pages/#recommended-limits)

### 关于添加歌曲外链
~~找到了一个关于添加歌曲外链的好方法，而且应该很难会失效，是利用的QQ邮箱的附件收藏功能，具体的方法看[这里](https://zhidao.baidu.com/question/583100560403319365.html)~~

上面的方法已经失效，腾讯会改变链接地址，只能通过[好多歌](www.haoduoge.com)了：

测试一下，这里我放了一首羽泉的彩虹，会预先加载，循环播放，考虑到移动端的屏幕适配问题，宽度最好设置为300px：
<div>
  <audio controls loop preload style="width: 300px" src="http://mp3.haoduoge.com/s/2017-03-13/1489401430.mp3"></audio>
</div>

### 遗留和待改进
- 引入google统计或者百度统计


### 感言
快过年啦，在年前终于把自己的小阵地打造好了，虽然我只是做了一点点的小工作，但还是有收获的。
祝大家鸡年大吉......吧 :)


### 后记
我的天呐，本来以为搞定了，因为首页看起来没问题，但是当我点进我的第一篇文章，也就是本文的时候，竟然发现样！式！丢！了！，我的天，为啥啊？我以为我是误删了什么东西，把整个项目用git一步步退回去，拿头顶了三个小时愣是没发现问题在哪儿，最后拷贝别人(bebop)博客的源文件到我的\_post里发现能够正常显示，我就把文档一步步删，删到正文全没了才发现是yaml的头出了问题，`tags:`后面换下一行不要空格，这个容易出问题！！**mark**
