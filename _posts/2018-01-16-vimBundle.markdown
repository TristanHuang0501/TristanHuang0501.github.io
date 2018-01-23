---
layout:     post
title:      Vim编辑器Windows配置(一)
subtitle:   有一种信仰叫做vim
date:       2018-01-17
author:     "Tristan"
header-img: "img/post-bg-vim.png"
catalog:    true
tags:
- vim 
---



### 1. 前提准备
注意：安装vundle前提需要先安装git和配置curl

#### 1.1 安装GVIM

#### 1.2 安装git客户端：msysgit
msysgit只提供了git的核心功能，而且是基于命令行的
 1. 下载[msysgit](https://github.com/git-for-windows/git/releases/download/v2.15.1.windows.2/Git-2.15.1.2-64-bit.exe)，版本为2.15.1
 2. 安装过程中注意在PATH环境选择（Adjusting your PATH environment）界面，我们选择第二个"run git from the Windows Command Prompt"
 3. 安装完成，打开cmd，运行指令 git --version 检查git版本号

#### 1.3 配置curl
在Windows下安装curl与msysgit结合非常简单，只需要在git的cmd目录创建文件curl.cmd即可，文件内容如下：

```
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

### 2. 安装插件管理工具Vundle
1. 打开cmd或者git bash，运行以下命令，即可将vundle安装到Vim\vimfiles目录下（这里假设vim安装在c盘路径下，具体情况需修改）：
```
git clone https://github.com/gmarik/Vundle.vim.git  
          C:\Program Files (x86)\Vim\vimfiles\bundle\Vundle.vim
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


### 3. 具体插件安装
具体的插件安装就是在配置文件中添加，然后打开gvim在命令模式下运行 `:BundleInstall`即可
#### 3.1 文件管理插件 NERDTree 和共享插件 vim-nerdtree-tabs
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
NERDTree关于切换工作台和目录的快捷键：
```
ctrl + w + h    光标 focus 左侧树形目录
ctrl + w + l    光标 focus 右侧文件显示窗口
ctrl + w + w    光标自动在左右侧窗口切换
ctrl + w + r    移动当前窗口的布局位置
```

```
o       在已有窗口中打开文件、目录或书签，并跳到该窗口
go      在已有窗口 中打开文件、目录或书签，但不跳到该窗口
t       在新 Tab 中打开选中文件/书签，并跳到新 Tab
T       在新 Tab 中打开选中文件/书签，但不跳到新 Tab
i       split 一个新窗口打开选中文件，并跳到该窗口
gi      split 一个新窗口打开选中文件，但不跳到该窗口
s       vsplit 一个新窗口打开选中文件，并跳到该窗口
gs      vsplit 一个新 窗口打开选中文件，但不跳到该窗口

e:      以文件管理的方式打开选中的目录
i:      执行当前文件
D:      删除书签

P:      跳到根结点 
p:      跳到父节点
K:      跳到当前目录下同级的第一个结点
J:      跳到当前目录下同级的最后一个结点 

C       将选中目录或选中文件的父目录设为根结点
u       将当前根结点的父目录设为根目录，并变成合拢原根结点
U       将当前根结点的父目录设为根目录，但保持展开原根结点
r       递归刷新选中目录
R       递归iii<F8>刷新根结点
cd      将 CWD 设为选中目录

I       切换是否显示隐藏文件
f       切换是否使用文件过滤器
F       切换是否显示文件
B       切换是否显示书签

q       关闭 NerdTree 窗口
A       全屏显示NERDTree，或者关闭全屏
?       切换是否显示 Quick Help

:NERDTree Z:\    切换NERDTree的盘符到Z盘
```
切换标签页指令：
```
:tabnew [++opt选项] ［＋cmd］ 文件      建立对指定文件新的tab
:tabc   关闭当前的 tab
:tabo   关闭所有其他的 tab
:tabs   查看所有打开的 tab
:tabp   前一个 tab
:tabn   后一个 tab

标准模式下：
gT      前一个 tab
gt      后一个 tab
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

" 按下 F2 调出/隐藏 NERDTree
map  :silent! NERDTreeToggle

" 将 NERDTree 的窗口设置在 vim 窗口的右侧（默认为左侧）
let NERDTreeWinPos="right"

" 显示书签列表
let NERDTreeShowBookmarks=1
```

更多详细的配置可以参考：[Vim之NERDTree帮助](http://www.cnblogs.com/mo-beifeng/archive/2011/09/08/2171018.html)

#### 3.2 搜索定位打开文件插件 CtrlP
在配置文件中添加 `Plugin 'kien/ctrlp.vim'` ，然后安装即可，效果如图所示
![CtrlP插件效果图](http://www.huangdc.com/wp-content/uploads/2016/06/ctrlp-vim-demo.gif)

#### 3.3 状态栏插件 vim-airline
在`_vimrc`文件中添加如下两句即可：
```
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'
```
此时是有很多内置的主题的，可以直接使用，方法是在配置文件中写
```
let g:airline_theme="solarized"
```
其中"solarized"指定了主题，也可以在vim中输入指令`:AirlineTheme solarized"即可马上更改，但是是一次性的，关闭vim后就恢复原状了。

#### 3.4 导航插件 tagbar
Tagbar和Taglist很相似，都是展示当前文件Symbol的插件，但是两者的关注点不同，总得来说Tagbar对面向对象的支持更好，它会自动根据文件修改的时间来重新排列Symbol的列表。

网上大部分的博文都是在nuix系统下的安装，我这里整理一份windows下安装的步骤：

##### 3.4.1 安装 Exuberant ctags
tagbar 正常工作依赖于 vim 和 [Exuberant ctags](http://ctags.sourceforge.net/)。下载后将`ctags.exe`文件放在一个在PATH环境变量的文件夹里，或者直接就新加一个路径。

##### 3.4.2 安装 tagbar
在配置文件中加入：
```
"文件侦查启动,用以检测文件的后缀  
filetyp on  
"安装tagbar插件  
Plugin 'majutsushi/tagbar'  
"设置tagbar使用的ctags的插件,必须要设置对  
let g:tagbar_ctags_bin='XXX_youpath/ctags'  
"设置tagbar的窗口宽度  
let g:tagbar_width=30  
"设置tagbar的窗口显示的位置,为左边  
let g:tagbar_left=1  
" autofocus on tagbar open
let g:tagbar_autofocus=1
"映射tagbar的快捷键  
map <F8> :TagbarToggle<CR>  
"打开文件自动 打开tagbar  
autocmd BufReadPost *.java call tagbar#autoopen()  
```

### 4. Vim配色colorscheme
在vim安装目录下有个colors文件夹，里面存放的就是各种colorscheme，选择好相应的主题后，到`_vimrc`文件中设置，比如说选择 desert 主题，只需添加如下一句：
```
colorscheme desert
```

当系统默认的主题已经无法满足你的时候，可以google比较好的配色方案放到colors文件夹下同时修改配置，这里推荐一个非常棒的网站：[A ColorScheme Editor for Vim](http://bytefluent.com/vivify/)，这个网站不仅提供了很多的配色方案，还能对方案进行编辑（比如变亮或变暗）后再下载，选择困难还可以随机配色，酷毙了简直！

实在想作还可以自己写，也不复杂，也就几个参数调教一下就好了，不过我还没折腾。reddit 上也有一个关于创建 Colorscheme 的讨论：[Creating Your Lovely Color Scheme](https://www.reddit.com/r/vim/comments/7auw18/creating_your_lovely_color_scheme_vimconf2017/)

### 5. 可能出现的问题
1. 输入 `:BundleInstall` 指令后报错："unknown function: vundle#installer#new"，可以参考这里 [vim插件vundle/bundle安装错误小结](https://segmentfault.com/a/1190000003795535)

### 6. 参考资料：
- [全世界最好的编辑器VIM之Windows配置篇](http://www.huangdc.com/421)
- [改变vim配色：安装colorscheme](http://blog.csdn.net/simple_the_best/article/details/51901361)
