---
layout:     post
title:      Singleton单例模式探讨
subtitle:   我，独一无二
date:       2017-10-27
author:     "Tristan"
header-img: "img/post-bg-irobot.png"
catalog:    true
tags:
- 设计模式
- Java
---

> 单件模式某种意义上来讲，可能是所有模式中最“单纯”的，因为她的类图只有一个类！尽管从类设计的角度来说很简单，但在实现上还是会遇到相当多的波折。 


在开发时，有一些对象其实我们只需要一个，比方说：线程池（threadpool）、缓存（cache)、对话框、处理偏好设置和注册表（registry）的对象、日志对象、充当打印机、显卡等设备的驱动程序的对象。事实上，这类对象只能有一个实例，如果制造出多个，就会导致许多的问题，例如：程序的行为异常、资源使用过量，或者是不一致的结果。

使用单例模式可以很好地解决这个问题，除了保持对象的唯一性外，还能提供全局访问点，并且根据实现的方式的不同而具有如延迟实例化、改善多线程

先来看下单件模式的简单定义：
> 单件模式确保一个类只有一个实例，并提供一个全局访问点。



### 写法

#### 1. 最简单的实现

```java
public class Singleton{
	private Singleton(){}  //私有构造函数
	private static Singleton instance = null; //单例对象
	
	public static Singleton getInstance(){
		if(instance == null){
			instance = new Singleton();
		}
		return instance;
	} 
} 
```

分析：

* 要想一个类只能构造一个对象，自然不能随便去做new操作，因此Singleton类的构造方法是私有的。
* 单例的初始值是null，还未构建时，调用getInstance()方法会构建单例对象并返回，这个写法属于懒加载模式（lazy initialization），即延迟实例化。
* 但是延迟实例化带来的隐患就是带来“先检查后执行”的竞态条件，即基于一种可能失效的观察结果（`if(instance == null`）来做出判断或者执行某个计算（`instance = new Singleton()`）。


#### 2. 用饿汉模式保证线程安全

```java
public class Singleton{
	private Singleton(){}  //私有构造函数
	private static Singleton instance = new Singleton(); //类加载时就初始化
	
	public static Singleton getInstance(){
		return instance;
	} 
} 
```

分析：

* 编程时，我们必须认定所有的程序都是多线程的，否则线程会由于无法预料的数据变化而发生错误。当多个线程同时访问和修改相同的变量时，将会在串行编程模型中引入非串行因素，而这种非串行性是很难分析的。
* 饿汉模式，即“急切地”创建实例，而不是延迟实例化。利用这个做法，我们依赖JVM在加载这个类时马上创建此唯一的单例实例，即使客户端没有调用`getInstance()`方法。
* 缺点也恰恰是其是饿汉模式，而不是懒加载，这导致它在一些场景中将无法使用：譬如Singleton实例的创建是依赖参数或者配置文件的，在`getInstance()`之前必须调用某个方法设置参数给它，这样这种单例写法就无法使用了。

#### 3. synchronized关键字同步getInstance()

```java
public class Singleton{
	private Singleton(){}  //私有构造函数
	private static Singleton instance = null; //单例对象
	
	public static synchronized Singleton getInstance(){
		if(instance == null){
			instance = new Singleton();
		}
		return instance;
	} 
} 
```

分析：

* 使用synchronized关键字，通过该内置锁对整个方法进行同步，是一种简单且粗粒度线程安全实现方式。
* 此时我们面对的就是一个性能问题，而不是线程安全问题：同步会降低性能。实际上，只有第一次执行此方法时，才真正需要同步，换句话说，多线程能够安全并发地执行除了第一次调用外的所有调用。此时，因为synchronized关键字，我们为该方法的每一次调用都要付出昂贵的同步代价，这就造成性能的很大下滑，是一种不良并发（Poor Concurrency）。
* 同步的代价在不同的JVM中是不同的。在早期，代价相当高，随着更高级的JVM的出现，同步代价降低了，但出入synchronized方法或块仍然有性能损失。

#### 4. 双重检查加锁（DCL）

双重检查加锁（Double checked locking，DCL）是一种使用同步块加锁的方法，之所以称其为双重检查锁，是因为会有两次检查`instance == null`，一次在同步块外，一次在同步块内。

由上面的第一类最简单实现可知，懒汉模式下，问题就出在用了可能失效的观测结果来决定下一步的动作。既然如此，我们只要保证在第一次执行时只有一个线程能进入第二个`if`检查语句即可，第一次检查是否已有实例有可能会产生误会，但是第二次检查我们保证了只有一个线程拿到内置锁，这样就保证了第一次执行的正确性，而后面就不需要同步了，这样就从理论角度很好地解决了上面的同步代价问题。

同时我们还要注意到这是个静态方法，所以是以Class对象作为锁，而不是调用该方法的具体对象。

```java
public class Singleton{
	private Singleton(){}
	private static Singleton instance = null;

	public static Singleton getInstance(){
		if(instance == null){
			synchronized(Singleton.class){
				if(instance == null){
					instance = new Singleton();
				}
			}
		}
		return instance;
	}
}
```
    
然而上面的代码在实际的多线程环境中却很有可能失效，指令重排造成了这一切。直接的原因是在初始化一个对象并使一个对象引用指向他的整个过程不是原子的，导致了可能会出现引用指向对象并未初始化好的那块堆内存，详细解释一下，以`instance = new Singleton();`为例，这个操作可以拆分为：

```
//1. 栈内存开辟空间给instance引用
//2. 堆内存开辟空间准备初始化对象
//3. 调用Singleton的构造器初始化对象
//4. 栈中引用指向这个堆内存空间地址（执行完这步instance就是非null的了）
```

真实的指令的粒度比上述过程更小，但是已经能够说明问题。由于操作非原子性，给了JVM重排序的机会。JVM重排序的原则是：在单线程中，不管怎么排，保证最终结果一致。然而，多线程下的指令重排序就给程序带来了很多问题。

在上述过程中，假设程序刚开始运行在Thread1，如果第4步抢先执行了，此时 instance 非 null ，然后被 Thread2 抢占，此时`getInstance()`方法直接返回instance引用，然后使用，然后顺理成章地就报错了。

为了解决这个问题，我们用`volatile`来修饰instance变量声明，这是Java语言提供的一种稍弱的同步机制，用来确保将变量的更新操作通知到其他线程。

> 加锁机制既可以保证可见性又可以确保原子性，而volatile变量只能确保可见性。




当把变量声明为`volatile`类型后，编译器与运行时都会注意到这个变量是共享额，因此不会将该变量上的操作与其他内存操作一起重排序。`volatile`变量不会被缓存在寄存器或者对其他处理器不可见的地方，因此在读取`volatile`类型的变量时总返回最新写入的值。总计起来，就是：

* 保证可见性：使用该变量必须重新去主内存读取，修改了该变量必须立刻刷新主内存。
* 防止重排序：通过插入内存屏障，加入`volatile`之后查看汇编代码可以发现多了一句`lock addl $0x0,(%esp)`。

所以我们加上`volatile`再写一遍：

```java
public class Singleton{
	private Singleton(){}
	private volatile static Singleton instance = null;

	public static Singleton getInstance(){
		if(instance == null){
			synchronized(Singleton.class){
				if(instance == null){
					instance = new Singleton();
				}
			}
		}
		return instance;
	}
}
```

其实在 Java 5 以前的版本使用了`volatile`的双检锁还是有问题的。其原因是 Java 5 以前的 JMM （Java 内存模型）是存在缺陷的，即使将变量声明成`volatile`也不能完全避免重排序，主要是 volatile 变量前后的代码仍然存在重排序问题。这个 volatile 屏蔽重排序的问题在 Java 5 中才得以修复，所以在这之后才可以放心使用 volatile。


#### 5. 静态内部类

使用静态内部类这种方法也是《Effective Java》上所推荐的：

```java 
public class Singleton {  
    private Singleton (){} 

    private static class SingletonHolder {  
        private static final Singleton INSTANCE = new Singleton();  
    }  
     
    public static final Singleton getInstance() {  
        return SingletonHolder.INSTANCE; 
    }  
}
```

这种写法仍然使用JVM本身机制保证了线程安全问题；由于 SingletonHolder 是私有的，除了 getInstance() 之外没有办法访问它，因此它是懒汉式的；同时读取实例的时候不会进行同步，没有性能缺陷；也不依赖 JDK 版本。

#### 6. 枚举Enum

简单是用枚举写单例的最大优点：

```java
public enum EasySingleton{
    INSTANCE;
}
```

我们可以通过EasySingleton.INSTANCE来访问实例，这比调用`getInstance()`方法简单多了。创建枚举默认就是线程安全的，所以不需要担心DCL，而且还能防止反序列化导致重新创建新的对象。但是还是很少看到有人这样写，可能是因为不太熟悉吧。

### 实际运用

一般来说，单例模式有五种写法：懒汉、饿汉、双重检验锁、静态内部类、枚举。上述所说都是线程安全的实现，文章开头给出的第一种方法不算正确的写法。

一般情况下直接使用饿汉式就好了，如果明确要求要懒加载（lazy initialization）可以于使用静态内部类，如果涉及到反序列化创建对象时可以使用枚举的方式来实现单例。

### 疑问

- 类的单件和对象的单件有什么区别？
- 全局变量比起单件模式来有哪些不足的地方？
- 既然单件模式的构造器是私有的，那么是否还能够设计出她的子类，继承单件类？
- 多个类加载器如何导致单件失效而产生多个实例？
- 静态内部类有什么性质？

### 参考资料：

- [漫画：什么是单例设计模式](http://mp.weixin.qq.com/s?__biz=MzIxMjE5MTE1Nw==&mid=2653192169&idx=1&sn=9c7c8c269b44443b5c4c6136529367c4&chksm=8c990d33bbee8425731a0ae76bd656a78e4fc9dddbe6c62ee77fc5686b35d001f9ced0980a3a&mpshare=1&scene=1&srcid=1127ZSP9IcnzmWHyT9d4jYxh#rd)
- [如何正确地写出单例模式](http://wuchong.me/blog/2014/08/28/how-to-correctly-write-singleton-pattern/)


### 可以参考的写作素材

- 《我，机器人》独一无二
- One一个 app