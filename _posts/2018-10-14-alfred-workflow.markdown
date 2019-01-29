---
layout:     post
title:      打造你的 Alfred 神器（1）
subtitle:   我喜欢的 workflow 整理 
date:       2018-10-13
author:     "Tristan"
header-img: "img/post-bg-alfred.jpg"
catalog:    true
tags:
- Alfred
- workflow
---

使用 Mac 作为主力生产工具的应该都有了解过 Alfred 这个神器，简介内容这里就不介绍了，大家可以看 [Alfred 神器使用手册](https://sspai.com/post/44624)，作者从 what, how, why 整个解释地非常好了我觉得。

Alfred 提供了很多的功能，在购买了 powerpack 之后又具备了 workflow 的功能，这个东西简直就是用上了就离不开了，在这里我会持续收集我上手一段时间，然后又非常喜欢的 workflow，作为大家的使用参考，同时我也会尽量附上每个 workflow 的下载链接，省去大家寻找的麻烦。

最近也在研究自己写一些符合我自身使用习惯的 workflow，可能会写一篇关于怎样写 workflow 的文章。

### 工具类（搜索、打开方向）

#### Search*(v1.0)* ~ [Download](https://github.com/Louiszhai/alfred-workflows/blob/master/workflows/Search.alfredworkflow?raw=true)

程序员都离不开搜索, 每天耗费在搜索上的时间更是不计其数. 实际上, 搜索的操作步骤是可以被优化的. Search 正是一款这样的workflow. 基于它, 您可以任何区域选中文本, 按下绑定好的快捷键 (最多两次按键, 建议绑定快捷键为Option+W), 便可直接在默认浏览器打开搜索结果页, 省心省力. 目前搜索引擎支持 谷歌, 百度, 雅虎, 维基百科等.

#### Sublime Text*(v1.1.0)* ~ [Download](https://github.com/zenorocha/alfred-workflows/raw/master/sublime-text/sublime-text.alfredworkflow)

![sublime text](https://ws4.sinaimg.cn/large/006tNbRwly1fw6lrdo69cj30x0092wep.jpg)

#### Terminal → Finder*(v1.6.0)* ~ [Download](https://github.com/zenorocha/alfred-workflows/raw/master/terminal-finder/terminal-finder.alfredworkflow)

Open current Finder (or Path Finder) window in Terminal (or iTerm) and vice versa.

![ft](https://ws4.sinaimg.cn/large/006tNbRwly1fw6lv239ekj30x00b8q35.jpg)

![tf](https://ws2.sinaimg.cn/large/006tNbRwly1fw6lv5660mj30x00920st.jpg)

#### localhost

打开默认浏览器的 localhost:xxxx 

--------------------------------------------------

### 工具类（系统设置方向）

#### [alfred-figlet](https://github.com/importre/alfred-figlet)
将英文字母变为 ASCII 码艺术字。

You need [Node.js 4+](https://nodejs.org/) and Alfred 3 with the paid Powerpack upgrade.

执行下面的命令安装，有可能


在执行上面的命令安装 alfred-dark-mode 的时候，提示没有写权限：
```zsh
npm WARN checkPermissions Missing write access to /usr/local/lib/node_modules
```
这个时候在指令前面加上 sudo 即可，但是我出现了这个问题：[ISSUE: Alfred preferences plist not resolving correctly #2](https://github.com/importre/alfred-slack-status/issues/2)，还是没有搞定，以后再弄吧。

有需求可以先用这个替代品：[TAAG: Text to ASCII Art Generator](http://patorjk.com/software/taag/)，可以用来生成 ASCII 艺术字呢，比如说下面这个星战风格的：
```
.___________..______       __       _______.___________.    ___      .__   __. 
|           ||   _  \     |  |     /       |           |   /   \     |  \ |  | 
`---|  |----`|  |_)  |    |  |    |   (----`---|  |----`  /  ^  \    |   \|  | 
    |  |     |      /     |  |     \   \       |  |      /  /_\  \   |  . `  | 
    |  |     |  |\  \----.|  | .----)   |      |  |     /  _____  \  |  |\   | 
    |__|     | _| `._____||__| |_______/       |__|    /__/     \__\ |__| \__| 
                                                                               
```

```
████████╗██████╗ ██╗███████╗████████╗ █████╗ ███╗   ██╗
╚══██╔══╝██╔══██╗██║██╔════╝╚══██╔══╝██╔══██╗████╗  ██║
   ██║   ██████╔╝██║███████╗   ██║   ███████║██╔██╗ ██║
   ██║   ██╔══██╗██║╚════██║   ██║   ██╔══██║██║╚██╗██║
   ██║   ██║  ██║██║███████║   ██║   ██║  ██║██║ ╚████║
   ╚═╝   ╚═╝  ╚═╝╚═╝╚══════╝   ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═══╝                                      
```

#### IP Address*(v1.2.0)* ~ [Download](https://github.com/zenorocha/alfred-workflows/raw/master/ip-address/ip-address.alfredworkflow)

![IP Address](https://ws3.sinaimg.cn/large/006tNbRwly1fw6lcs4ky3j30x00dejrv.jpg)

#### Kill Process*(v1.2.0)* ~ [Download](https://github.com/zenorocha/alfred-workflows/raw/master/kill-process/kill-process.alfredworkflow)

![](https://ws1.sinaimg.cn/large/006tNbRwly1fw6li0ynswj30x00det95.jpg)

--------------------------------------------------

### 生活类

#### [Loved or Unloved Music](https://github.com/robotsandcake/alfred-love-loved-music-workflow) ~ [Download](https://github.com/robotsandcake/alfred-love-loved-music-workflow/blob/master/love-unloved-music.alfredworkflow?raw=true)

This Alfred.app workflow for macOS makes it easy for the user to set the currently playing song to "Loved" or "Unloved", which when coupled with an iTunes Smart Playlist means you can avoid the Barry Manilow and love the Orbital.

#### [有道翻译](https://github.com/wensonsmith/YoudaoTranslate) ~ [Download](https://github.com/wensonsmith/YoudaoTranslate/releases)

挺好用的，可以弃掉欧路词典的全局快捷键了感觉，哈哈，实在不行才 alfred 打开欧路好了。这个 workflow 是用的有道智云的 NLP 应用，需要注册一下，不过也挺简单的。好用。

#### [印象笔记/evernote](https://www.zhihu.com/question/28011717/answer/140638646)

获取你的印象账号所对应的 [Dev Tokens](http://dev.evernote.com/doc/articles/dev_tokens.php)，然后键入 es-token ，完成配置，然后就可以正常使用这个 workflow 了。

![](https://ws4.sinaimg.cn/large/006tNbRwly1fwzyokrccdj30vo0fmjw4.jpg)

现在 Dev Token 国际版是可以正常开启的，但是国内印象笔记被关闭了，如果你点开上面的网站会显示这样的结果：

![](https://ws1.sinaimg.cn/large/006tNbRwly1fwwf11gqfsj31fo0pmdib.jpg)

包括一些同学用 sublime 去访问印象笔记也由于 token 失效会无法用，此时需要我们手动去申请，按照[创建页面失效的解决办法](http://www.biliyu.com/article/1799.html)提供的方法，印象笔记会立刻给你发送邮件的，然后会给你开启获取 token 的权限：

![](https://ws2.sinaimg.cn/large/006tNbRwly1fwwf42oiwdj314i0c6aaw.jpg)



--------------------------------------------------



### 资源
- [Louiszhai/alfred-workflows](https://github.com/Louiszhai/alfred-workflows)
- [zenorocha/alfred-workflows](https://github.com/zenorocha/alfred-workflows#ip-address-v120--download)

- [AlfredWorkflow.com](http://alfredworkflow.com) - List of Alfred Workflows.
- [Ctwise Alfred Workflows](https://github.com/ctwise/alfred-workflows) - Workflows from the Github user "ctwise".
- [Packal](http://www.packal.org/) - The biggest place to find Workflows.
- [Vítor Galvão’s Alfred Workflows](https://github.com/vitorgalvao/alfred-workflows/) - Workflows from the Github user "vitorgalvao".
