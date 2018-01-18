---
layout:     post
title:      Vim编辑器Windows配置
subtitle:   有一种信仰叫做vim
date:       2018-01-17
author:     "Tristan"
header-img: "img/post-bg-vim.png"
catalog:    true
tags:
- vim 
---



### 前提准备
注意：安装vundle前提需要先安装git和配置curl

#### 安装GVIM

#### 安装git客户端：msysgit
msysgit只提供了git的核心功能，而且是基于命令行的
 1. 下载[msysgit](https://github.com/git-for-windows/git/releases/download/v2.15.1.windows.2/Git-2.15.1.2-64-bit.exe)，版本为2.15.1
 2. 安装过程中注意在PATH环境选择（Adjusting your PATH environment）界面，我们选择第二个"run git from the Windows Command Prompt"
 3. 安装完成，打开cmd，运行指令 git --version 检查git版本号

#### 配置curl
在Windows下安装curl与msysgit结合非常简单，只需要在git的cmd目录创建文件curl.cmd即可，文件内容如下：

```bash
@rem Do not use "echo off" to not affect any child calls.
@setlocal

@rem Get the abolute path to the parent directory, which is assumed to be the
@rem Git installation root.
@for /F "delims=" %%I in ("%~dp0..") do @set git_install_root=%%~fI
@set PATH=%git_install_root%\bin;%git_install_root%\mingw\bin;%git_install_root%\mingw64\bin;%PATH%
@rem !!!!!!! For 64bit msysgit, replace 'mingw' above with 'mingw64' !!!!!!!

@if not exist "%HOME%" @set HOME=%HOMEDRIVE%%HOMEPATH%
@if not exist "%HOME%" @set HOME=%USERPROFILE%

@curl.exe %*
```

配置好后打开cmd，运行命令 curl --version 检查 curl 版本号，然后下面就进入安装 vundle 阶段了

### 安装插件管理工具Vundle
1. 打开cmd或者git bash，运行以下命令，即可将vundle安装到Vim\vimfiles目录下（这里假设vim安装在c盘路径下，具体情况需修改）：
```
git clone https://github.com/gmarik/Vundle.vim.git  C:\Program Files (x86)\Vim\vimfiles\bundle\Vundle.vim
```
2. 添加一个gvim目录的环境变量 `$VIM` ，值比如说为 `C:\Program Files (86)\Vim`
3. 在vim安装目录下的启动设定文件 `_vimrc` 中添加 bundle 配置，内容如下：

```
"插件管理
set rtp+=$VIM/vimfiles/bundle/Vundle.vim/
call vundle#begin()
"let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
"my bundle plugin

call vundle#end()
filetype plugin indent on
```


### 具体插件安装
具体的插件安装就是在配置文件中添加，然后打开gvim在命令模式下运行 `:BundleInstall`即可
#### 1. 文件管理插件 NERDTree 和共享插件 vim-nerdtree-tabs
在`_vimrc`文件中添加两行：
```
"插件管理
set rtp+=$VIM\vimfiles\bundle\Vundle.vim\
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
Plugin 'scrooloose/nerdtree'        "这两行
Plugin 'jistr/vim-nerdtree-tabs'
Plugin 'kien/ctrlp.vim'
call vundle#end()
```
NERDTree的一些基本操作快捷键：
```
?: 快速帮助文档
o: 打开一个目录或者打开文件，创建的是buffer，也可以用来打开书签
go: 打开一个文件，但是光标仍然留在NERDTree，创建的是buffer
t: 打开一个文件，创建的是Tab，对书签同样生效
T: 打开一个文件，但是光标仍然留在NERDTree，创建的是Tab，对书签同样生效
i: 水平分割创建文件的窗口，创建的是buffer
gi: 水平分割创建文件的窗口，但是光标仍然留在NERDTree
s: 垂直分割创建文件的窗口，创建的是buffer
gs: 和gi，go类似
x: 收起当前打开的目录
X: 收起所有打开的目录
e: 以文件管理的方式打开选中的目录
D: 删除书签
P: 大写，跳转到当前根路径
p: 小写，跳转到光标所在的上一级路径
K: 跳转到第一个子路径
J: 跳转到最后一个子路径
<C-j>和<C-k>: 在同级目录和文件间移动，忽略子目录和子文件
C: 将根路径设置为光标所在的目录
u: 设置上级目录为根路径
U: 设置上级目录为跟路径，但是维持原来目录打开的状态
r: 刷新光标所在的目录
R: 刷新当前根路径
I: 显示或者不显示隐藏文件
f: 打开和关闭文件过滤器
q: 关闭NERDTree
A: 全屏显示NERDTree，或者关闭全屏
```

可以在`_vimrc`文件中添加NERDTree的配置，比如说：
```
" 关闭NERDTree快捷键
map <leader>t :NERDTreeToggle<CR>
" 显示行号
let NERDTreeShowLineNumbers=1
let NERDTreeAutoCenter=1
" 是否显示隐藏文件
let NERDTreeShowHidden=1
" 设置宽度
let NERDTreeWinSize=21
" 在终端启动vim时，共享NERDTree
let g:nerdtree_tabs_open_on_console_startup=1
" 忽略一下文件的显示
let NERDTreeIgnore=['\.pyc','\~$','\.swp']
" 显示书签列表
let NERDTreeShowBookmarks=1
```

更多详细的配置可以参考：[Vim之NERDTree帮助](http://www.cnblogs.com/mo-beifeng/archive/2011/09/08/2171018.html)

#### 2. 搜索定位打开文件插件CtrlP
在配置文件中添加 `Plugin 'kien/ctrlp.vim'` ，然后安装即可，效果如图所示
![CtrlP插件效果图](http://www.huangdc.com/wp-content/uploads/2016/06/ctrlp-vim-demo.gif)

#### 3. 配色插件colorscheme
在vim安装目录下有个colors文件夹，里面存放的就是各种colorscheme，选择好相应的主题后，到`_vimrc`文件中设置，比如说选择 desert 主题，只需添加如下一句：
```
colorscheme desert
```

当系统默认的主题已经无法满足你的时候，可以google比较好的配色方案放到colors文件夹下同时修改配置，这里推荐一个非常棒的网站：[A ColorScheme Editor for Vim](http://bytefluent.com/vivify/)，这个网站不仅提供了很多的配色方案，还能对方案进行编辑（比如变亮或变暗）后再下载，选择困难还可以随机配色，酷毙了简直！

实在想作还可以自己写，也不复杂，也就几个参数调教一下就好了，不过我还没折腾。reddit 上也有一个关于创建 Colorscheme 的讨论：[Creating Your Lovely Color Scheme](https://www.reddit.com/r/vim/comments/7auw18/creating_your_lovely_color_scheme_vimconf2017/)

### 可能出现的问题
1. 输入 `:BundleInstall` 指令后报错："unknown function: vundle#installer#new"，可以参考这里 [vim插件vundle/bundle安装错误小结](https://segmentfault.com/a/1190000003795535)

### 参考资料：
- [全世界最好的编辑器VIM之Windows配置篇](http://www.huangdc.com/421)
- [改变vim配色：安装colorscheme](http://blog.csdn.net/simple_the_best/article/details/51901361)
