---
layout:     post
title:      打造适合自己的 IDE
subtitle:   记录 IDEA 上我喜欢的 plugin
date:       2018-10-12
author:     "Tristan"
header-img: "img/post-bg-androidstudio.jpg"
catalog:    true
tags:
- IDEA
- Plugin
---

### 编辑类

#### IdeaVim + IdeaVimExtension
习惯了 vim 的操作（连 chrome 都装了 vim 的插件），不想再去慢慢熟悉 IntelliJ Platform 上的一系列编辑类的快捷键了，就装上 IdeaVim这个插件，这样就可以用自己喜欢的 `dd`，`cw`, `ggVG` 这些命令了。

IdeaVimExtension 为 IdeaVim 插件增加了自动切换为英文输入法的功能，通过以下命令来开启：
```
:set keep-english-in-normal
```
命令名字简洁明了，就是在 normal 模式时换为英文输入法，方便我们键入各种命令，当然如果你有需要回到 insert 模式时恢复输入法，用一下命令：
```
:set keep-english-in-normal-and-restore-in-insert
```
但是目前这个插件仅支持 macOS，这个插件实在是太好用了，记得以前经常在切换状态的时候还要切换输入法，想想还是挺烦人的，现在就没有这个烦恼啦，Oh yeah~

### 代码规范类

#### Alibaba Java Coding Guidelines