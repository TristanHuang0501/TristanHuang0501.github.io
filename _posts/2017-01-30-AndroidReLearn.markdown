---
layout:     post
title:      "Android知识整理"
subtitle:    重新认识android
date:       2017-02-15
author:     "Tristan"
header-img: "img/post-bg-android.jpg"
catalog:    true
tags:
- Android 
---


### 1. 虚拟机
 **认知：**ART是趋势，DalVik已经慢慢在被淘汰
 
 > ART，即Android Runtime。ART 的机制与 Dalvik 不同。在Dalvik下，应用每次运行的时候，字节码都需要通过即时编译器（just in time ，JIT）转换为机器码，这会拖慢应用的运行效率，而在ART 环境中，应用在第一次安装的时候，字节码就会预先编译成机器码，使其成为真正的本地应用。这个过程叫做预编译（AOT,Ahead-Of-Time）。这样的话，应用的启动(首次)和执行都会变得更加快速。

参考: [Android 中的Dalvik和ART是什么，有啥区别？](http://www.jianshu.com/p/58f817d176b7)

------------

### 2. 相关资源
- [google开发者网站](https://developer.android.com/index.html)
- [Android中文api](www.android-doc.com)
- [App code](http://appxcode.com)：有很多好的轮子

------------

### 3. 组件

#### 3.1 Button

##### 3.1.1 Button点击事件触发的两种方法：
1. 在activity中`bt.setOnClickListener(new onClickListener())`
2. 在layout中，bt设置一个属性`android:onClick = "something"`，然后在activity中定义一个同名的方法`public void something(View v){}`这个方法所接收的参数为一个View对象，当按钮被按下时，系统会调用这个`something()`方法

> 注意，在onClick方法中传入的View对象是被点击的button对象，<u>所以多个button可以共用一个点击监听，只要在监听里面用`bt.getId()`来最终区分出来是哪个button就可以分别处理而不干扰。<u>

有一个疑问就是：共用监听or单独监听（每个button一个内部类）or在layout中设置`onClick`这几种方式在消耗内存上有啥区别？

##### 3.1.2 设置半透明度
- 在xml文件中：
    - 半透明：`<Button android:background="#e0000000" ... /> `
    - 透明：`<Button android:background="#00000000" ... />`

- 在java代码中：
    - `btn.getBackground().setAlpha(100)` //0~255透明度
- 数值量：
  - 颜色和不透明度 (alpha) 值以十六进制表示法表示。任何一种颜色的值范围都是 0 到 255（00 到 ff）。
  - 对于 alpha，00 表示完全透明，ff 表示完全不透明。
  - 表达式顺序是`“aabbggrr”`，其中“aa=alpha”（00 到 ff）；“bb=blue”（00 到 ff）；“gg=green”（00 到 ff)；“rr=red”（00 到 ff）。
  - 例如，如果您希望对某叠加层应用不透明度为 50% 的蓝色，则应指定以下值：7fff0000


-------------

### 4. 布局
开发中用的最多的是`linearlayout`和`relativelayout`

#### 4.1 LinearLayout

> 单纯线性布局永远不会发生组件的重叠

*LinearLayout中的layout_weight属性：*
`layout_weight`属性用于分配`LinearLayout`中的的额外空间(extra space)。

如果View不想拉伸的话，`layout_weight`值设置为0。否则的话这些像素会按比例分配到weight值大于0的所有View。

换句话说，也就是`android:layout_weight`属性告知`LinearLayout`如何进行子组件的布置安排。

参考：
[LinearLayout的layout_weight属性](http://www.cnblogs.com/JohnTsai/p/4077183.html)

#### 4.2 RelativeLayout
在`relativelayout`中默认的对齐方式是左对齐和顶部对齐，可以通过设置`android:layout_align*="true"("id")`或者`layout_above="id"`或者`layout_toLeftOf="@id/*"`等属性来改变，而居中等可以通过`android:centerIn*`来设置

假设有两个对象（id分别为tv1和tv2）第二个对象设置了两个属性`alignRight="@id/tv1"`、`alignLeft="@id/tv1"`，那么第二个对象就会和第一个对象**等宽**


#### 4.3 FrameLayout
> 帧布局是五大布局中最简单的布局方式，在需要布局中有空间重叠的情况下才使用。
> `frameLayout`中的所有视图都已以层叠的方式展现的。第一个添加到布局中的视图显示在最底层，最后一个被放在最顶层。上一层的视图会覆盖下一层的视图，因此该布局类似于堆栈布局。

- 在`framelayout`中子视图默认的对齐方式也是左对齐和顶部对齐，可以通过设置`android:layout_gravity="left|buttom"`等属性来改变


- 在`framelayout`中，空间的`layout_margin`属性需要依赖`layout_gravity`属性，否则设置无效。`layout_margin`所示的边缘值是相对于控件的`layout_gravity`所定义的参考点而言的。

- 如果以图片作为`linearLayout`的背景，那么将无法控制布局的高和宽，其尺寸会不受控制地适应图片的大小，因此采用`frameLayout`配合`imageView`添加可大小可控的背景


#### 4.4 TableLayout

```xml
<TableLayout>
<!--tableRow中有几个子标签就有几列-->
  <TableRow> </TableRow>
  <TavleRow> </TableRow>
</TableLayout>
```

**宽高：**
在表格布局中每个`tableRow`的宽高是有个默认值的，默认的宽是`match_parent`默认的高是`wrap_content`，同时宽高也是不可更改的，改了也无效
可以在`TableLayout`中设置`stretchColumns="*"`设置拉伸列

**分割线：**
如果想在表格中插入一个分割线，可以在`<TableLayout>`中加入一个直接子标签`<TextView>`，将其高度设为1个dp，设置下颜色就好了

**两个独有的属性：**
可以通过`layout_column=""`直接设置某个元素在第几列，这样就可以不必从第0列开始
可以通过`layout_span=""`来设置某一个元素占几列


-------------

### 5. 读写文件
> 存储空间包括内部存储空间和外部存储空间

#### 5.1 内部存储空间(ROM)
内部存储读写文件不需要权限，因为只能写自己包内的文件，其他包不能动，除非有root权限
##### 5.1.1 绝对路径
```
File file = new File("data/data/com.example.*/file");
FileOutputStream fos = new FileOutStream(file);
fos.write(string.getBytes());
```
##### 5.1.2 使用路径api
可以通过`getFilesDir()`来获得`data/data/com.example.*/file`文件夹的路径.，所以可以这样写：

  File file = new File(getFilesDir(),"name.txt");

而通过`getCacheDir()`可以获得
`data/data/com.example.*/cache`文件夹的路径

从源码看，两者的区别是：当rom空间不够的时候，cache文件夹中的东西有可能会被系统删除，但是不能指望系统去删除，应该自己设置一个阈值
在设置中点击存储，选择相应的应用，可以选择**清除缓存**和**清除数据**，前者会清空cache文件夹中的所有文件，而后者会删除包内所有的用户文件

#### 5.2 外部存储读写（sd卡）
外部存储写数据需要权限`WRITE_EXTERNAL_STORAGE`，而读数据则不一定，要看开发者选项里面是否勾选了sd卡读写保护
##### 5.2.1 绝对路径
各个厂商的sd卡的路径差不多都不一样，要注意

    File file = new File("sdcard/file.*")

##### 5.2.2 使用路径api
这个api名字突出一个长啊，使用之前先判断sd卡是否可用

    if(Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED)){
      File file = new File(Environment.getExternalStorageDirectory(),"name");
    }

其中，sd卡的状态可以有：

|状态|说明|
|:--- | :---|
|`REMOVE`|没有插sd卡|
|`UNMOUNT`|sd卡已插，但是没有挂载|
|`CHECKING`|sd卡正在被系统遍历|
|`MOUNTED`|sd卡准备就绪，可以读写|
|`MOUNTED_READ_ONLY`|sd卡可用，但是只读|

##### 5.2.3 获取sd卡的剩余空间
可以参看**设置**系统应用的源码，放在`package/apps/Settings`中，具体用的时候可以google找轮子
  
    sd卡存储空间 = 可用的区块数量*区块大小（blockSize）


#### 5.3 文件访问权限

> **权限的表现形式：**
> `d rwx rwx rwx`        一共十位

- 在Android中，每一个应用都是一个独立的用户
- `d`：代表文件夹，文件是-
- 第一个`rwx`：决定owner用户对此文件的权限
  - r：读
  - w：写
  - x：执行(execute)

![文件访问权限](https://github.com/TristanHuang0501/TristanHuang0501.github.io/raw/master/img/in-post/post-android-permission.jpg)


具体编程时，当我们需要在应用中写入一个一定权限的文件的时候：

```java
public void bt_click(View v){
  //此api会把文件写到data/data/com.xxx.xxx/files文件夹下
  try{
    FileOutputStream fos = openFileOutput("example.txt", MODE_WORLD_READABLE);
    fos.write("哈哈".getBytes());
    fos.close();
  }catch(Exception e){
    e.printStackTrace();
  }
}
```

其中要说明的是openFileOutput是Context提供的一个很要用的方法，但是只能写到本应用对应的文件夹下：

![@openFileOutput方法](https://github.com/TristanHuang0501/TristanHuang0501.github.io/raw/master/img/in-post/post-android-openFileOutput.png)

#### 5.4 使用Shared Preference存取简单数据

> SharedPreferences的使用非常简单，能够轻松的存放数据和读取数据。SharedPreferences只能保存简单类型的数据，例如，String、int等。一般会将复杂类型的数据转换成Base64编码，然后将转换后的数据以字符串的形式保存在 XML文件中，再用SharedPreferences保存。

具体的方法参看博文：
[Android SharedPreferences使用以及原理详解](http://blog.csdn.net/wxyyxc1992/article/details/17222841)
**注意：**要使用Activity类的getSharedPreferences方法获得SharedPreferences对象，而不要new一个新的对象，否则效率不高


-----------


### 6. 调试时的小技巧
1. **真机调试时eclipse的file explorer打不开data文件夹：**
当用真机开发Android时，连接了Eclipse后，默认在File Explorer下是达不开我们手机的data文件夹的，这里打不开是因为权限不足。以下有个小技巧可以解决这问题。
首先，测试机先root，然后在手机上安装上Root Explorer 管理器（或类似软件），再将/data/data及其子文件夹下的访问权限都修改为可读可写可执行即可。这时候再使用eclipse的File Explorer就可以展开了，这时候就可以查看应用下的SQLite数据库了。

2. **当devices中的设备显示不出来的时候：**
直接使用需要在cmd中cd到sdk的目录下使用`adb start-server`指令，也可以将该目录直接加入到系统变量的path中，这样直接就在cmd任意位置输入指令即可。本质是个socket。
相关的指令：
- `adb start-server`其实任何一条adb指令都可以重启adb
- `adb kill-server`杀死进程<br>
- `adb install  apk的路径`安装apk
- `adb uninstall com.tristan.something`这里是写的包名
- `adb devices`显示所有连接的android设备
- `adb shell`进入android系统的命令行（linux）

3. **当你的手机助手占用的系统的adb的端口（5037）怎么办？**
首先通过`adb devices`查看端口，然后在windows下cmd使用`netstat -ano`查看当前系统各个端口被什么进程所占用

4. **项目组织文件：**
manifeast中的package是android分辨应用的唯一标识，和gen目录下的包名相同，与src目录下的不同
当应用涉及到**用户权限**时，需要到manifesat中去添加权限(可以通过可视化操作)

5. **root工具：**
实验室手机[Nexus5快速root工具](http://www.shuame.com/faq/root-tutorial/2613-google-nexus5.html)

6. **查看日志：**
在logcat中设置过滤器的时候最好根据`Tag`来过滤（比如`System.out`输出的日志的tag就是`System.out`，级别为`Info`），而不要用`Application`来过滤
logcat语句：
  
      Log.e(tag,string)
      Log.i(tag,string)
      ...

7. **URI和URL的[区别]()**
```java
//举例，拨号逻辑
public void onclick(View v){
    EditText et = (EditText) findViewById(R.id.et);
    String phone = et.getText().toString();
    Intent intent = new Intent();
  intent.setAction(Intent.ACTION_CALL);
  intent.setData(Uri.parse("tel:" + phone));
}
```
8. **Eclipse查看sdk或者jdk源码：**
[解决使用Eclipse中调用javadoc的问题](http://blog.163.com/logowx@126/blog/static/6256726420096259420870/)



[区别]:https://www.zhihu.com/question/21950864