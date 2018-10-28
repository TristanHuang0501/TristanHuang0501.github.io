---
layout:     post
title:      "我的博客搭建记"
subtitle:   Hello World, Hello Blog
date:       2017-01-24
author:     "Tristan"
header-img: "img/post-bg-unix-linux.jpg"
catalog:    true
tags:
- Blog
---

> 通过两天的摸索，终于能整出博客的大概样子出来了，总的来说并没有太过接触Jekyll框架底层的东西，只是在fork了hux大神的io项目之后做了调整和修改，熟悉了一下子Jekyll生成静态网页的原理、liquid模块语言、以及进一步熟悉了git和markdown。

### 1. 项目来源
- fork自[hux大神的io项目](https://github.com/Huxpro/huxpro.github.io)
- 同时参考了[Bebop对于hux的branch分支](https://github.com/chaosinmotion/chaosinmotion.github.io)

### 2. 参考的博文
- [阮一峰](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
- [使用Jekyll来写博客的一些心得](http://www.tuicool.com/articles/vENfq2)
- [使用java来自动初始化Jekyll的md文件](http://www.tuicool.com/articles/yu6vIfe)
- [jekyll+markdown+git+github](https://droidcat.bitbucket.io/2015/05/26/blog-or-wiki.html)

### 3. 本地搭建的最简单步骤
- 安装Ruby Installer
- 在cmd中输入`gem install jekyll`
- 在cmd中输入`gem install jekyll-paginate`
- cd到仓库中输入`jekyll server`
- 浏览器中输入`localhost:4000`即可本地调试

### 4. 记录值得注意的地方
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

### 5. GitHub Page的规定
尽管GitHub个人网站项目是免费的，但是却有一些限制。总体来说，完全够用，甚至太多了。
- 单个仓库大小不超过1GB，上传单个文件大小不能超过100MB，如果通过浏览器上传不能超过25MB
- 个人网站项目也不例外，最大空间1GB
- 个人网站项目每个月访问请求数不能超过10万次，总流量不能超过100GB
- 个人网站项目一小时创建数量不能超过10个

最新的规定在这里：[GitHub Page的规定](https://help.github.com/articles/what-is-github-pages/#recommended-limits)

### 6. 后续修改
根据需要我会时不时地对Blog做一些修改，会记录在下面：
#### 6.1 关于添加歌曲外链
~~找到了一个关于添加歌曲外链的好方法，而且应该很难会失效，是利用的QQ邮箱的附件收藏功能，具体的方法看[这里](https://zhidao.baidu.com/question/583100560403319365.html)~~

上面的方法已经失效，腾讯会改变链接地址，只能通过[好多歌](www.haoduoge.com)了：

测试一下，这里我放了一首羽泉的彩虹，会预先加载，循环播放，考虑到移动端的屏幕适配问题，宽度最好设置为300px：
<div>
  <audio controls loop preload style="width: 300px" src="http://mp3.haoduoge.com/s/2017-03-13/1489401430.mp3"></audio>
</div>

#### 6.2 emoji支持
Jekyll 本身不支持 emoji，不过有个插件可以使它支持 emoji 表情，那就是 jemoji(jekyll/jemoji)，显然这是官方提供的插件。
步骤：
- cmd安装gem包`gem install jemoji`
- '_config.yml'文件中添加
  ```
  gems:
      -jemoji
  ```
- 然后就可以使用`:smile:`来显示😄啦

参考博客:[Jekyll 的 emoji 插件](http://blog.fooleap.org/jemoji.html)

所有支持的表情：[EMOJI CHEAT SHEET](https://www.webpagefx.com/tools/emoji-cheat-sheet/)

#### 6.3 引入百度统计
2017/04/10： 引入了百度统计

#### 6.4 代码块显示优化
2018/01/18： 调整了行间距、语法高亮、滚动条美化等

##### 6.4.1 使用Rouge获取语法高亮样式表
之前的语法高亮用了一年，感觉不太好看，然后就寻思着换一下。我使用的代码高亮器是Rouge。Rouge是一个纯Ruby编写的代码高亮器，可用于60多种语言的高亮，其源代码托管在GitHub上，我们可以通过它来生成不同的样式表。

首先安装Rouge，然后生成对应主题的css文件
```bash
$ gem install rouge
$ rougify style monokai.sublime > assets/css/syntax.css
```
第二句的具体语法是这样的：
```bash
$ rougify style (theme_name) > (css_file.css)
```
其中：
- (theme_name) 表示要使用的主题名称，详细的主题列表可以通过 rougify help style 获得
- (css_file.css) 表示要导出的样式文件路径
获得css文件后，我们可以直接放到html中使用，或者复制粘贴到自己配置css的地方，如果需要修改代码块的背景颜色的话，修改syntax.css中的背景配色即可。Sublime的背景色为#272822，Atom的背景色为#282C34。
```css
pre[class='highlight'] {background-color:#272822;}
```

##### 6.4.2 bug修复记录
同时发现了一个以前没有发现的问题，就是在代码块中，我的方法注释如果是多行的话，在本地jekyll解释后是没问题的，但是上传到github上显示就会出现不换行的问题，分析网页的源文件，发现不知道为什么包着代码块的div中又多了一层div，所以我只能在css中用选择器使第二层的div设置了一下`white-space: pre`，然后就可以换行了。

##### 6.4.3 代码块滚动条优化
原来的滚动条太丑了，简直不能看，花了点功夫优化了一下，但是只能在webkit内核的浏览器上显示目前应该，没有做兼容性处理，主要增加了如下的css：
```css
/* 设置垂直滚动条的宽度和水平滚动条的高度 */
.highlight::-webkit-scrollbar{
    width: 8px;
    height: 8px;
}

/* 设置滚动条的滑轨 */
.highlight::-webkit-scrollbar-track {
      background-color: #ddd;
}

/* 滑块 */
.highlight::-webkit-scrollbar-thumb {
    background-color: rgba(0, 0, 0, 0.6);
    border-radius: 4px;
}

 /* 滑轨两头的监听按钮 */
.highlight::-webkit-scrollbar-button {
    background-color: #888;
    display: none;
}

/* 横向滚动条和纵向滚动条相交处尖角 */
.highlight::-webkit-scrollbar-corner {
    /*background-color: black;*/
}
```


### 7. 感言
快过年啦，在年前终于把自己的小阵地打造好了，虽然我只是做了一点点的小工作，但还是有收获的。
祝大家鸡年大吉......吧 :)


### 8. 下一步修改计划
行号问题：
: 代码块中行号的美化显示，看到stackoverflow上有讨论：[Enabling line numbers with rouge #4619](https://github.com/jekyll/jekyll/issues/4619)，但试了一下，发现巨丑，回头再解决一下看看。