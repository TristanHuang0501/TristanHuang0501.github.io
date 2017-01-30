---
layout:     post
title:      "Android札记"
subtitle:    重新认识android
date:       2017-01-30
author:     "Tristan"
header-img: "img/post-bg-android.jpg"
catalog:    true
tags:
- Android 
---

 **虚拟机：**ART是趋势，DalVik已经慢慢在被淘汰
 
 > ART，即Android Runtime。ART 的机制与 Dalvik 不同。在Dalvik下，应用每次运行的时候，字节码都需要通过即时编译器（just in time ，JIT）转换为机器码，这会拖慢应用的运行效率，而在ART 环境中，应用在第一次安装的时候，字节码就会预先编译成机器码，使其成为真正的本地应用。这个过程叫做预编译（AOT,Ahead-Of-Time）。这样的话，应用的启动(首次)和执行都会变得更加快速。

参考: [Android 中的Dalvik和ART是什么，有啥区别？](http://www.jianshu.com/p/58f817d176b7)

**开发环境：**

- eclipse+adt

- android studio

**辅助资源：**

- [google开发者网站](https://developer.android.com/index.html)

- [Android中文api](www.android-doc.com)

- [App code](http://appxcode.com)：有很多好的轮子

**项目组织文件：**

manifeast中的package是android分辨应用的唯一标识，和gen目录下的包名相同，与src目录下的不同

**真机调试时eclipse的file explorer打不开data文件夹：**

当用真机开发Android时，连接了Eclipse后，默认在File Explorer下是达不开我们手机的data文件夹的，这里打不开是因为权限不足。以下有个小技巧可以解决这问题。

首先，测试机先root，然后在手机上安装上Root Explorer 管理器（或类似软件），再将/data/data及其子文件夹下的访问权限都修改为可读可写可执行即可。这时候再使用eclipse的File Explorer就可以展开了，这时候就可以查看应用下的SQLite数据库了。

实验室手机[Nexus5快速root工具](http://www.shuame.com/faq/root-tutorial/2613-google-nexus5.html)

**DDMS：**Dalvik Debug monitor service

**ADB：**Android Debug Bridge

直接使用需要在cmd中cd到sdk的目录下使用`adb start-server`指令，在此之前需要将该目录添加到系统环境的path下。本质是个socket。
相关的指令：

- `adb start-server`其实任何一条adb指令都可以重启adb

- `adb kill-server`杀死进程

- `adb install  apk的路径`安装apk

- `adb uninstall com.tristan.something`这里是写的包名

- `adb devices`显示所有连接的android设备

- `adb shell`进入android系统的命令行（linux）

**当你的手机助手占用的系统的adb的端口（5037）怎么办？**

首先通过`adb devices`查看端口，然后在windows下cmd使用`netstat -ano`查看当前系统各个端口被什么进程所占用

**一些遗漏知识点：**

- 单纯线性布局永远不会发生组件的重叠

- URI和URL的[区别](https://www.zhihu.com/question/21950864)

  ```
  //举例，拨号逻辑
  public void onclick(View v){
      EditText et = (EditText) findViewById(R.id.et);
      String phone = et.getText().toString();
      Intent intent = new Intent();
	  intent.setAction(Intent.ACTION_CALL);
	  intent.setData(Uri.parse("tel:" + phone));
  }
  ```

- 当应用涉及到用户权限时，需要到manifesat中去添加权限(可以通过可视化操作)