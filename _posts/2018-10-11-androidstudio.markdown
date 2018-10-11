---
layout:     post
title:      Android Studio 构建项目
subtitle:   对遇到的一些问题的记录
date:       2018-10-11
author:     "Tristan"
header-img: "img/post-bg-androidstudio.jpg"
catalog:    true
tags:
- Android
- Android Studio
---

## issue:Could not find com.android.tools.build:aapt2:3.2.0-4818971
和 Stack Overflow 上的别人出现的问题一样的，但是上面提供的答案对我电脑并没有效果，有效的解决方法是修改 buil.gradle 的内容：主要是增加了jcenter(){url 'http://jcenter/bintray.com/'} 
```gradle
// Top-level build file where you can add configuration options common to all sub-projects/modules.
 
buildscript {
    repositories {
        jcenter(){ url 'http://jcenter.bintray.com/'}
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.0.0'
 
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
 
allprojects {
    repositories {
        jcenter(){url 'http://jcenter.bintray.com/'}
    }
}
 
task clean(type: Delete) {
    delete rootProject.buildDir
}
```


## 其他东西，后面补充
init.gradle文件其实是Gradle的初始化脚本(Initialization Scripts)，也是运行时的全局配置。