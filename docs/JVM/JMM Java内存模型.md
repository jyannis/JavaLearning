JMM（JAVA内存模型）是JVM基础知识中最容易被忽略的部分，但它对于我们加深对JVM总体的理解起到举足轻重的作用，同时也是大厂面试的一个重要考点。

<br/>

**目录**

- [基本概念](#基本概念)
  - [性质](#性质)
  - [目的](#目的)
  - [内容](#内容)
    - [规范变量访问](#规范变量访问)
    - [规范原子性](#规范原子性)
    - [规范可见性](#规范可见性)
    - [规范有序性](#规范有序性)
- [注意事项](#注意事项)
- [面试中如何回答](#面试中如何回答)

<br/>

<br/>

## 基本概念

JMM：JAVA Memory Model 也即**JAVA内存模型**

下面分四个方面来陈述：

- 性质：JMM本质上是一个什么东西。
- 目的：JMM之所以存在，是为了解决什么问题？
- 内容：JMM为了实现它的目的，要做些什么？
- 实现：利用什么技术真正实现它的目的？

<br/>

<br/>

### 性质

JMM是一种**规范**。

就好像HTTP是一种**交互协议**，[JAVA运行时数据区](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483776&idx=1&sn=25fbf98bb6dcda4e924675dc1e64997e&chksm=9ffc63e6a88beaf053d6036e5c4fff87af41df7d5a6e35329e115f9123b9b2d5c4363068f4c2&token=1776113537&lang=zh_CN#rd)是一种**内存结构**一样，JMM是对JAVA虚拟机作出**规范**，使它必须符合某些要求以满足某些目的。

<br/>

<br/>

### 目的

借助JMM规范，我们希望能够做到：

- 屏蔽硬件和操作系统的访问差异，让Java程序在各种平台下都能达到一致的内存访问效果；
- 解决多线程通过共享内存进行通信时，存在的原子性、可见性、有序性问题。

<br/>

<br/>

### 内容

#### 规范变量访问

JMM的首要目标是定义程序中各个变量的访问规则，即在虚拟机中**将变量存储到内存**和**从内存中取出变量**这样的底层细节。

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://gitee.com/jyannis/doc/raw/master/JavaLearning/JVM/JMM.png">
    <br>
    <div style="color:orange; border-bottom: 0px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">线程、主内存、工作内存三者的交互关系</div>
</center>

- JMM规定了所有的变量都存储在主内存（Main Memory）中
- 每个线程还有自己的工作内存（Work Memory），其中保存被该线程使用到的变量的主内存副本拷贝
- 线程对变量的所有操作（读取、赋值等）都必须在工作内存中进行，不能直接读写主内存
- 线程间变量值的传递需要通过主内存，不能访问其他线程的工作内存

<br/>

#### 规范原子性

JMM要求：

除了64位的数据类型（long和double），其他基本数据类型的访问读写都是必须具备原子性的。

不过现在的商用虚拟机都会把long和double数据类型也实现为原子操作。

另外，为了能够实现更大范围的原子性保证，JMM还提供了lock和unlock两个原子操作来满足这种需求，与它们相对应的更高层次的字节码也就是`monitorenter`和`moniterexit`，也就是synchronized的底层实现方式。还不是很了解synchronized？传送门：[Synchronizd关键字](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483769&idx=1&sn=bdb296488a0b2b30ae98287ecd7151cf&chksm=9ffc631fa88bea09aed92f62d1c2a8b6d469ec918586fa4e011b72c304bcb8ae5541465de9d3&token=1776113537&lang=zh_CN#rd)

<br/>

#### 规范可见性

可见性是指**当一个线程修改了共享变量的值，其他线程能够立即得知这个修改**。

 为了规范可见性，JMM引入了volatile关键字。volatile保证了：

1. 被volatile修饰的变量在被修改后立即同步到主内存
2. 被volatile修饰的变量在每次被使用之前都从主内存刷新

因此，可以使用volatile来保证多线程操作时变量的可见性。

而具体如何保证上面两条，**内存屏障**也起到至关重要的作用，篇幅原因这里就不详细展开了。如果想对volatile有更进一步了解，请移步[Volatile关键字](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483765&idx=1&sn=cf0c1b74985e2389719d6ae1f51f4258&chksm=9ffc6313a88bea05f7c77c45247a5a1ce251b77b13c71c0068a4b30cc2effee2e80e21e59988&token=1776113537&lang=zh_CN#rd)



除了volatile以外，还有两个关键字可以实现可见性：

- synchronized

  同步块的可见性是由“对一个变量执行unlock操作之前，必须先把此变量同步回主内存中（执行store、write操作）”这条规则获得的

- final

  被final修饰的字段在构造器中一旦初始化完成，并且构造器没有把“this”的引用传递出去（**this引用逃逸**是一件很危险的事情，其他线程有可能通过这个引用访问到“初始化了一半”的对象），那在其他线程中就能看见final修饰的值。

<br/>

#### 规范有序性

规范程序的有序性，也即让程序指令能够按照想要的顺序来执行。

这里的程序指令并不是一行行代码，而是应该理解为一个个原子的操作指令，它是比一行行代码更细化的粒度。

JMM中利用三点来规范有序性：

1. volatile关键字防止指令重排

   volatile是通过**内存屏障**来防止指令重排的，如果想对volatile有更进一步了解，请移步[Volatile关键字](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483765&idx=1&sn=cf0c1b74985e2389719d6ae1f51f4258&chksm=9ffc6313a88bea05f7c77c45247a5a1ce251b77b13c71c0068a4b30cc2effee2e80e21e59988&token=1776113537&lang=zh_CN#rd)

2. as-if-serial语义

   含义是：“在单线程下，无论指令怎样排序，最终结果都不能被改变。”

   有了as-if-serial语义，才使得synchronized也能够保证有序性。

3. happens-before"先行发生"原则

   “先行发生”原则定义两项操作之间的偏序关系。包括了“程序次序规则”、“线程启动规则”、“传递性”等等。具体如下（简单了解即可，无需记忆）：

   > 程序次序规则：同一个线程内，按照代码出现的顺序，前面的代码先行于后面的代码，准确的说是控制流顺序，因为要考虑到分支和循环结构。
   >
   >  
   >
   > 管程锁定规则：一个unlock操作先行发生于后面（时间上）对同一个锁的lock操作。
   >
   >  
   >
   > volatile变量规则：对一个volatile变量的写操作先行发生于后面（时间上）对这个变量的读操作。
   >
   >  
   >
   > 线程启动规则：Thread的start( )方法先行发生于这个线程的每一个操作。
   >
   >  
   >
   > 线程终止规则：线程的所有操作都先行于此线程的终止检测。可以通过Thread.join( )方法结束、Thread.isAlive( )的返回值等手段检测线程的终止。 
   >
   >  
   >
   > 线程中断规则：对线程interrupt( )方法的调用先行发生于被中断线程的代码检测到中断事件的发生，可以通过Thread.interrupt( )方法检测线程是否中断
   >
   >  
   >
   > 对象终结规则：一个对象的初始化完成先行于发生它的finalize（）方法的开始。
   >
   >  
   >
   > 传递性：如果操作A先行于操作B，操作B先行于操作C，那么操作A先行于操作C。

<br/>

<br/>

## 注意事项

经常有人把JAVA内存模型和运行时数据区搞混，也就是下面两张图：

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://gitee.com/jyannis/doc/raw/master/JavaLearning/JVM/JMM.png">
    <br>
    <div style="color:orange; border-bottom: 0px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">线程、主内存、工作内存三者的交互关系</div>
</center>

<br/>

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://gitee.com/jyannis/doc/raw/master/JavaLearning/JVM/%E8%BF%90%E8%A1%8C%E6%97%B6%E6%95%B0%E6%8D%AE%E5%8C%BA.jpeg">
    <br>
    <div style="color:orange; border-bottom: 0px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Java运行时数据区</div>
</center>

请千万不要再搞混了。

<br/>

<br/>

## 面试中如何回答

面试官：**JMM了解吗？简单讲讲？**



答：

JMM，JAVA内存模型，是一种用来屏蔽各种硬件和操作系统的内存访问差异的规范，目的是解决多线程通过主内存通信时，存在的原子性、可见性、有序性问题。

JMM首先规范了变量的访问。它要求所有变量都要存在主内存中，每个线程在自己工作内存中操作变量，然后同步回主内存；

其次JMM利用内存间原子性的交互操作规范了原子性，例如lock、unlock、read、store等等。通过这些操作，JMM保证了基本数据类型操作的原子性，并支持了synchronized；

JMM还利用volatile实现了可见性，它要求被volatile修饰的变量在使用时与主存及时同步；

最后JMM还保证了有序性，这是由volatile关键字的内存屏障、as-if-serial语义，以及happens-before“先行发生”原则一同支持的。

> 以上是概述性回答，然后根据面试官提的问题，可以再详细展开。例如：“面试官：‘volatile怎么保证可见性的？'”就可以再讲讲主内存与工作内存的及时性同步，还有内存屏障等等。

