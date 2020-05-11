框架是JAVA面试中比较重要的一个部分，而Spring是面试最爱问的框架之一。Spring中最重要的就是IOC和AOP这两大概念，本篇中对于AOP相关知识及面试题作一个总结。

<br/>

**目录**

- [基本概念](#基本概念)
  - [性质](#性质)
  - [目的](#目的)
  - [原理](#原理)
    - [AspectJ静态代理](#AspectJ静态代理)
    - [SpringAOP动态代理](#SpringAOP动态代理)
- [AOP关键词](#AOP关键词)
- [动态代理的两种实现](#动态代理的两种实现)
  - [JDK动态代理](#JDK动态代理])
  - [CGLIB动态代理](#CGLIB动态代理)
  - [其他一些核心问题](#其他一些核心问题)

<br/>

<br/>

## AOP基本概念

AOP：Aspect Oriented Programming 也即**面向切面编程**

下面分三个方面来陈述：

- 性质：AOP本质上是一个什么东西。
- 目的：AOP之所以存在，是为了解决什么问题？
- 原理：AOP背后是如何实现的？

<br/>

<br/>

### 性质

AOP是一种**设计思想**。

就像OOP是面向对象编程一样，AOP则是OOP的一种延伸，是针对切面进行编程。

那么什么叫**切面**呢？可以认为是一个可重用的模块，或是一系列公共行为和逻辑。

如果具体举例子来说，比如权限认证（用户在进入任何功能性接口之前都应该先完成鉴权）、日志打印（许多接口出现问题的时候都应该有相应的异常日志）等等。

<br/>

<br/>

### 目的

借助AOP，我们希望：

- 通过尽可能地复用代码，以降低编码复杂度
- 通过把切面提取出来，以降低模块间的耦合度
- 联系上面这两条，同时也就提升了系统的可维护性

<br/>

<br/>

### 原理

AOP实现的关键在于**代理模式**，AOP代理主要分为静态代理和动态代理。静态代理的代表为AspectJ；动态代理则以Spring AOP为代表。

#### AspectJ静态代理

AspectJ会在编译阶段生成AOP代理类，因此也称为编译时增强。

它会在编译阶段将Aspect（切面）织入到Java字节码中，运行的时候利用到的就是增强之后的AOP对象。

#### SpringAOP动态代理

Spring AOP不会像AspectJ那样在编译时增强，而是每次在运行时于内存中临时为方法生成一个AOP对象。

这个AOP对象包含了目标对象的全部方法，并且在特定的切点做了增强处理，并回调原对象的方法。

如果理解了动态代理，那么对Spring AOP动态代理也不会难以理解。希望对动态代理不是很熟悉的读者可以先自行查阅相关资料学习。

<br/>

<br/>

## AOP关键词

在Java AOP的世界里，有一些关键词是一定要明白的。

<br/>

**Aspect（切面）**

 Aspect 声明类似于 Java 中的类声明，在 Aspect 中会包含着一些 Pointcut 以及相应的 Advice。

**Joint point（连接点）**

表示在程序中明确定义的点，典型的包括方法调用，对类成员的访问以及异常处理程序块的执行等等，它自身还可以嵌套其它 joint point。

**Pointcut（切点）**

表示一组 joint point，这些 joint point 或是通过逻辑关系组合起来，或是通过通配、正则表达式等方式集中起来，它定义了相应的 Advice 将要发生的地方。

**Advice（增强）**

Advice 定义了在 Pointcut 里面定义的程序点具体要做的操作，它通过 before、after 和 around 来区别是在每个 joint point 之前、之后还是代替执行的代码。

**Advice执行顺序（很重要！！）**

环绕（@Around）开始阶段 → @Before → 执行切点方法 → 环绕结束阶段 → @After → @AfterReturning

**Target（目标对象）**

织入 Advice 的目标对象。

**Weaving（织入）**

将 Aspect 和其他对象连接起来, 并创建 Adviced object 的过程。

<br/>

<br/>

## 动态代理的两种实现

在上文的阅读中，我们知道Spring AOP是基于动态代理实现的。

它背后其实有两种实现方式：JDK动态代理和CGLIB动态代理。这也是非常重要的知识点，在下文中详细说明。

<br/>

### JDK动态代理

利用拦截器(拦截器必须实现InvocationHanlder)加上反射机制生成一个实现代理接口的匿名类，

在调用具体方法前调用InvokeHandler来处理。

https://blog.csdn.net/yhl_jxy/article/details/80586785

<br/>

### CGLIB动态代理

利用ASM开源包，修改代理对象类的class文件的字节码，生成子类，再加载class文件。

https://blog.csdn.net/yhl_jxy/article/details/80633194

<br/>

<br/>

### 其他一些核心问题

#### 何时使用JDK还是CGLIB？

- 如果目标对象实现了接口，默认情况下会采用JDK的动态代理实现AOP。

- 如果目标对象实现了接口，可以强制使用CGLIB实现AOP。

- 如果目标对象没有实现了接口，必须采用CGLIB库，Spring会自动在JDK动态代理和CGLIB之间转换。

<br/>

#### JDK动态代理和CGLIB字节码生成的区别？

- JDK动态代理只能对实现了接口的类生成代理，而不能针对类。

- CGLIB是针对类实现代理，主要是对指定的类生成一个子类，覆盖其中的方法，

​     并覆盖其中方法实现增强，但是因为采用的是继承，所以该类或方法最好不要声明成final，

​     对于final类或方法，是无法继承的。private也是一样。

<br/>

#### CGlib比JDK快？

- 使用CGLib实现动态代理，CGLib底层采用ASM字节码生成框架，使用字节码技术生成代理类，

在jdk6之前比使用Java反射效率要高。唯一需要注意的是，CGLib不能对声明为final的方法进行代

理，因为CGLib原理是动态生成被代理类的子类。

- 在jdk6、jdk7、jdk8逐步对JDK动态代理优化之后，在调用次数较少的情况下，JDK代理效率高于CGLIB代理效率，只有当进行大量调用的时候，jdk6和jdk7比CGLIB代理效率低一点，但是到jdk8的时候，jdk代理效率高于CGLIB代理，总之，每一次jdk版本升级，jdk代理效率都得到提升，而CGLIB代理消息确有点跟不上步伐。

<br/>

#### Spring如何选择用JDK还是CGLIB？

1）当Bean实现接口时，Spring就会用JDK的动态代理。

2）当Bean没有实现接口时，Spring使用CGlib实现。

3）可以强制使用CGlib（在spring配置中加入<aop:aspectj-autoproxy proxy-target-class="true"/>）。