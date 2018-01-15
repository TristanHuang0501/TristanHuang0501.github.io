---
layout:     post
title:      Java类加载及对象初始化分析
subtitle:   结合JVM探究初始化过程
date:       2017-11-23
author:     "Tristan"
header-img: "img/post-bg-irobot.png"
catalog:    true
tags:
- Java
- JVM
---

## Java类的初始化顺序

### 无父类初始化
对象在class文件加载完毕，以及为各成员在方法区开辟好内存空间之后，就开始初始化过程，对于无父类的情况，类中各成分的初始化顺序为：（静态变量、静态初始化块）>（变量、初始化块）>构造器。

```java
/**
 *以下示例的输出为：
 *    静态变量
 *    静态初始化块
 *    变量
 *    初始化块
 *    构造器
 */
public class InitialOrderTest {
    /* 静态变量 */
    public static String staticField = "静态变量";
    /* 变量 */
    public String field = "变量";
    /* 静态初始化块 */
    static {
        System.out.println( staticField );
        System.out.println( "静态初始化块" );
    }
    /* 初始化块 */
    {
        System.out.println( field );
        System.out.println( "初始化块" );
    }
    /* 构造器 */
    public InitialOrderTest(){
        System.out.println( "构造器" );
    }


    public static void main( String[] args ){
        new InitialOrderTest();
    }
}
```

总结：先初始化类变量然后赋值，再初始化实例变量然后赋值。

### 有父类初始化

在有父类的情况下，初始化的顺序为：
1. 父类静态代码块、父类静态成员字段（并列优先级，按代码中出现先后顺序顺序执行）（只在第一次加载类时执行）；
2. 子类静态代码块、子类静态成员字段（并列优先级，按代码...）（只在第一次加载类时执行）；
3. 父类普通代码块，父类普通成员字段（并列优先级，按代码...)
4. 父类构造器
5. 子类普通代码块，子类普通成员字段（并列优先级，按代码...)
6. 子类构造器

```java
/**
 *以下示例的输出为：
 *    父类--静态变量
 *    父类--静态初始化块
 *    子类--静态变量
 *    子类--静态初始化块
 *    子类main方法
 *    父类--变量
 *    父类--初始化块
 *    父类--构造器
 *    i=9, j=0
 *    子类--变量
 *    子类--初始化块
 *    子类--构造器
 *    i=9,j=20
 */
class Parent {
    /* 静态变量 */
    public static String p_StaticField = "父类--静态变量";
    /* 变量 */
    public String    p_Field = "父类--变量";
    protected int    i    = 9;
    protected int    j    = 0;
    /* 静态初始化块 */
    static {
        System.out.println( p_StaticField );
        System.out.println( "父类--静态初始化块" );
    }
    /* 初始化块 */
    {
        System.out.println( p_Field );
        System.out.println( "父类--初始化块" );
    }
    /* 构造器 */
    public Parent(){
        System.out.println( "父类--构造器" );
        System.out.println( "i=" + i + ", j=" + j );
        j = 20;
    }
}

public class SubClass extends Parent {
	/* 静态变量 */
    public static String s_StaticField = "子类--静态变量";
    /* 变量 */
    public String s_Field = "子类--变量";
	/* 静态初始化块 */
    static {
        System.out.println( s_StaticField );
        System.out.println( "子类--静态初始化块" );
    }
    /* 初始化块 */
    {
        System.out.println( s_Field );
        System.out.println( "子类--初始化块" );
    }
    /* 构造器 */
    public SubClass(){
        System.out.println( "子类--构造器" );
        System.out.println( "i=" + i + ",j=" + j );
    }

    /* 程序入口 */
    public static void main( String[] args ){
        System.out.println( "子类main方法" );
        new SubClass();
    }
}
```

总结：
- 父类优于子类，静态优于非静态，只有在第一次创建对象的时候才会初始化静态块和静态成员。
- 

同时注意到上面的例子中，main()方法在静态成员完成初始化后开始执行，这是因为main()方法是静态方法，当类成员准备完毕后已经有了运行类的静态方法的条件。JVM在按照上面总结的规则


## 可用的材料
当一个类使用new关键字来创建新的对象的时候，比如Person per = new Person();JVM根据Person()寻找匹配的类，然后找到这个类相匹配的构造方法，这里是无参构造，如果程序中没有给出任何构造方法，则JVM默认会给出一个无参构造。当创建一个对象的时候一定对调用该类的构造方法，构造方法就是为了对对象的数据进行初始化。JVM会对给这个对象分配内存空间，也就是对类的成员变量进行分配内存空间，如果类中在定义成员变量就赋值的话，就按初始值进行运算，如果只是声明没有赋初始值的话，JVM会按照规则自动进行初始化赋值。而成员方法是在对象调用这个方法的时候才会从方法区中加载到栈内存中，用完就立即释放内存空间。

###类变量的默认值问题
