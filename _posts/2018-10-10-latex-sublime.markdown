---
layout:     post
title:      OS X 上配置 LaTeX 环境
subtitle:   配置过程中的经验总结
date:       2018-10-10
author:     "Tristan"
header-img: "img/post-bg-latex.jpg"
catalog:    true
tags:
- OS X
- LaTeX
- Sublime
---

在 Windows 平台上我们有 WinEdt 来完成 LaTeX 的写作，而在 Mac 平台上搭建 Latex 的写作环境也并不复杂，这里提供两种方法：

### MacTeX + TexPad

首先必须要有的就是 [MacTeX](http://www.tug.org/mactex/)，这个相当于一个生成的引擎，将我们写的文档按照格式的设定渲染成最终的 PDF 文档。在官网上可供选择的下载方式有两种，一种是完整的（大约 3G ，安装后 6G 左右），一种是basic（100M不到应该）。比较推荐的还是安装完整的，因为不然的话后面手工添加一些包还是挺麻烦的：

![mactex 下载](https://ws2.sinaimg.cn/large/006tNbRwgy1fw387ed6qdj30ka05p3yk.jpg)

TexPad 相当于一个编辑器，但是功能集成的很好，用起来比较清晰，安装过后它的界面是这样的：

![texpad 使用界面](https://ws4.sinaimg.cn/large/006tNbRwgy1fw38bv97fsj31kw0xitja.jpg)

可以看到论文的结构以及 PDF 文档分别分布在编辑框的左右，另外你在文章中所用到的所有的图片及表格等都会在左栏下方有列出。另外就是编辑时比较方便，比如我们在导入图片或者导包的时候会有自动提示。

但是我在用的时候会出现一个问题：明明是 UTF-8 编码格式打开的文档，但是在编译的时候却不能以 UTF-8 格式编码，提示我有不能转换的字符，但是真的找不出来，然后它就会按照默认的 ISO Latin 1 编码去编译文档，导致中文会乱码。当然在写英文论文的时候自然就不会有那么多的问题，总的来说还是挺好的工具。

### MacTex + Sublime + Skim

为了让毕业论文中的中文字符不至于乱码，只能换个思路，利用 Sublime 去搭建 LaTeX 环境，结果还挺惊喜的，因为整个过程并不复杂，且可拓展性比较高。

第一步还是装上我们的“引擎”， 然后就是装 [Sublime Text](https://www.sublimetext.com/)，还有就是装 PDF 阅读器 [skim](https://skim-app.sourceforge.io/) ，这个过程我就不多说了。然后我们需要给 Sublime 装一个插件，就是下图的 LaTexTools 了。

![sublime 插件](https://ws3.sinaimg.cn/large/006tNbRwgy1fw38njupylj30we0fq40c.jpg)

安装完这个其实我们按 ⌘+b 其实就可以对 tex 文档进行编译了。为了让 PDF 与 TeX 同步，我们还需要进 skim 中设置一下，在预设中选择 sublime 即可：

<img src="https://ws2.sinaimg.cn/large/006tNbRwgy1fw399a6ih4j30ns0i8wf7.jpg" alt="skim 设置" height="50%" width="50%">

上面也说道这种方式比较好的地方是具有可拓展性，比如说对 latex 公式的动态预览：

![latex 公式的动态预览](https://ws1.sinaimg.cn/large/006tNbRwgy1fw39ijq4d3j31fu0n4n1q.jpg)

这个功能以前是在插件 latex equation preview 中的，后来被集成到了上面的 LatexTools 中了（据 latex equation preview 这个包的原作者在知乎上说的），所以现在直接安装 LaTeXTools 再重启 Sublime 就能直接用该功能了，哦哦，还得装上 ImageMagic 包。

### Conclusion
总得来说，虽然 texpad 具有更佳的显示效果和封装，但是各种问题出现还是很麻烦的，而 sublime 配置起来其实也很方便，且各种插件具有可拓展性，所以建议大家直接围绕 sublime 搭建自己的论文写作环境。

### Issues
这里会记录环境搭建中出现的各种各样的问题。