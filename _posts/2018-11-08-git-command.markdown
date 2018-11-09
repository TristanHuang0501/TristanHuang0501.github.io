---
layout:     post
title:      Git - 理解Ta，爱Ta（2）
subtitle:   常用命令速查
date:       2018-10-28
author:     "Tristan"
header-img: "img/post-bg-git.png"
catalog:    true
tags:
- Git
---

Git 的四个组成部分：

![](https://ws3.sinaimg.cn/large/006tNbRwly1fx0k8koyaaj30j0049dfv.jpg)

### 1. 初始化仓库
```bash
git init
```

### 2. 将修改添加到暂存区
```bash
git add 文件名 # 将工作区的某个文件添加到暂存区
git add -u #添加所有被 tracked 文件中被修改或删除的文件信息到暂存区，不处理 untracked 的文件
git add -A #添加所有被 tracked 文件中被修改或删除的文件信息到暂存区，包括 untracked 的文件
```
