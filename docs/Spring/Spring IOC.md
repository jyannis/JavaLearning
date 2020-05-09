框架是JAVA面试中比较重要的一个部分，而Spring是面试最爱问的框架之一。Spring中最重要的就是IOC和AOP这两大概念，本篇中对于IOC相关知识及面试题作一个总结。

<br/>

**目录**

- [基本概念](#基本概念)
  - [性质](#性质)
  - [目的](#目的)
  - [内容](#内容)
    - [没有引入IOC的软件系统](#没有引入IOC的软件系统)
    - [引入IOC的软件系统](#引入IOC的软件系统)
    - [引入IOC的效果](#引入IOC的效果)
- [常见面试题](#常见面试题)
  - [Bean作用域](#（1）Bean作用域)
  - [Bean生命周期](#（2）Bean生命周期)
  - [BeanFactory和ApplicationContext的区别](#（3）BeanFactory和ApplicationContext的区别)
- [核心源码梳理](#核心源码梳理)
  - [Bean解析](#（1）Bean解析)
  - [Bean注册](#（2）Bean注册)
  - [Bean加载](#（3）Bean加载)

<br/>

<br/>

## IOC基本概念

IOC：Inverse of Control 也即**控制反转**

下面分四个方面来陈述：

- 性质：IOC本质上是一个什么东西。
- 目的：IOC之所以存在，是为了解决什么问题？
- 内容：IOC为了实现它的目的，要做些什么？

<br/>

<br/>

### 性质

IOC是一种**设计思想**。

它不是一种具体的技术，虽然我们经常把IOC和Spring联系在一起，但其实它也完全可以体现在其他的框架和语言中。

<br/>

<br/>

### 目的

借助IOC设计思想，我们希望能够做到**互相依赖的对象之间的解耦**。

<br/>

<br/>

### 内容

#### 没有引入IOC的软件系统

软件系统内部肯定有若干个对象存在，其中部分与部分对象之间存在着互相调用或依赖的关系，导致对象之间耦合度较高，如下图：

![耦合的对象](https://gitee.com/jyannis/doc/raw/master/JavaLearning/Spring/%E8%80%A6%E5%90%88%E7%9A%84%E5%AF%B9%E8%B1%A1.png)

我们可以把对象比喻成齿轮。如果几个耦合的对象中有一个对象不动了（无法正常工作），那么其他的对象也无法正常工作。导致“牵一发而动全身”的情况。

<br/>

#### 引入IOC的软件系统

在引入IOC容器后，我们再来看一下这个软件系统：

![容器托管后的对象](https://gitee.com/jyannis/doc/raw/master/JavaLearning/Spring/%E5%AE%B9%E5%99%A8%E6%89%98%E7%AE%A1%E5%90%8E%E7%9A%84%E5%AF%B9%E8%B1%A1.png)

齿轮之间的转动交给了“第三方”——也就是IOC容器。

由IOC容器来对各个对象进行统一的管理，当某个对象B需要对象A来帮助它完成什么功能时，就由IOC容器来把容器管理的A“借给”（专业术语叫“注入”）B来使用。

<br/>

#### 引入IOC的效果

对于这一点，我们不妨来看一下去掉IOC容器后的这张图：

![去除容器的状态](https://gitee.com/jyannis/doc/raw/master/JavaLearning/Spring/%E5%8E%BB%E9%99%A4%E5%AE%B9%E5%99%A8%E7%9A%84%E7%8A%B6%E6%80%81.png)

可以发现对象与对象之间不再紧密贴合。

这样的话，在我们编码实现A的时候，就无需考虑B、C和D了。

也即达到了我们想要的“**互相依赖的对象之间的解耦**”。

<br/>

<br/>

## 常见面试题

对于Spring IOC容器，最核心的两点就是：

- 容器本身
- 容器里的元素，或者说对象（bean）

围绕这两点，我们可以整理出下面三个非常重要的面试题。

<br/>

### （1）Bean作用域

Spring容器中的bean可以分为5个作用域：

- singleton：默认，容器中只有一个bean的实例，由BeanFactory自身来维护。

- prototype：为每一个bean请求提供一个实例。

- request：为每一个网络请求创建一个实例，在请求完成以后，bean会失效并被垃圾回收器回收。

- session：与request范围类似，确保每个session中有一个bean的实例，在session过期后，bean会随之失效。

- global-session：全局作用域，global-session和Portlet应用相关。当你的应用部署在Portlet容器中工作时，它包含很多portlet。如果你想要声明让所有的portlet共用全局的存储变量的话，那么这全局变量需要存储在global-session中。全局作用域与Servlet中的session作用域效果相同。

<br/>

### （2）Bean生命周期

bean从出生到消亡，经历了哪些过程？

1. 实例化Bean：

   对于BeanFactory容器，当客户向容器请求一个尚未初始化的bean时，或初始化bean的时候需要注入另一个尚未初始化的依赖时，容器就会调用createBean进行实例化。对于ApplicationContext容器，当容器启动结束后，通过获取BeanDefinition对象中的信息，实例化所有的bean。

2. 设置对象属性（依赖注入）：

   实例化后的对象被封装在BeanWrapper对象中，紧接着，Spring根据BeanDefinition中的信息 以及 通过BeanWrapper提供的设置属性的接口完成依赖注入。

3. 处理Aware接口：

   接着，Spring会检测该对象是否实现了xxxAware接口，并将相关的xxxAware实例注入给Bean：
   1. 如果这个Bean已经实现了BeanNameAware接口，会调用它实现的setBeanName(String beanId)方法，此处传递的就是Spring配置文件中Bean的id值；
   2. 如果这个Bean已经实现了BeanFactoryAware接口，会调用它实现的setBeanFactory()方法，传递的是Spring工厂自身。
   3. 如果这个Bean已经实现了ApplicationContextAware接口，会调用setApplicationContext(ApplicationContext)方法，传入Spring上下文；

4. BeanPostProcessor：

   如果想对Bean进行一些自定义的处理，那么可以让Bean实现了BeanPostProcessor接口，那将会调用postProcessBeforeInitialization(Object obj, String s)方法。

5. InitializingBean 与 init-method：

   如果Bean在Spring配置文件中配置了 init-method 属性，则会自动调用其配置的初始化方法。

6. BeanPostProcessor

   如果这个Bean实现了BeanPostProcessor接口，将会调用postProcessAfterInitialization(Object obj, String s)方法；由于这个方法是在Bean初始化结束时调用的，所以可以被应用于内存或缓存技术；

> 以上几个步骤完成后，Bean就已经被正确创建了，之后就可以使用这个Bean了。

7. DisposableBean：

   当Bean不再需要时，会经过清理阶段，如果Bean实现了DisposableBean这个接口，会调用其实现的destroy()方法；

8. destroy-method：

   最后，如果这个Bean的Spring配置中配置了destroy-method属性，会自动调用其配置的销毁方法。

<br/>

### （3）BeanFactory和ApplicationContext的区别

BeanFactory和ApplicationContext是Spring的两大核心接口，都可以当做Spring的容器。其中ApplicationContext是BeanFactory的子接口。

- BeanFactory：是Spring里面最底层的接口，包含了各种Bean的定义，读取bean配置文档，管理bean的加载、实例化，控制bean的生命周期，维护bean之间的依赖关系。ApplicationContext接口作为BeanFactory的派生，除了提供BeanFactory所具有的功能外，还提供了更完整的框架功能：
  - 继承MessageSource，因此支持国际化。
  - 统一的资源文件访问方式。
  - 提供在监听器中注册bean的事件。
  - 同时加载多个配置文件。
  - 载入多个（有继承关系）上下文 ，使得每一个上下文都专注于一个特定的层次，比如应用的web层。

<br/>

其他的一些不同处：

先列个表格，然后下面详细说明。

|                                      | BeanFactory | ApplicationContext   |
| ------------------------------------ | ----------- | -------------------- |
| **加载方式**                         | 惰性加载    | 预先加载             |
| **启动速度**                         | 较快        | 较慢（加载Bean过多） |
| **创建方式**                         | 编程式      | 编程式或声明式       |
| **Bean(Factory)PostProcessor扩展点** | 手动注册    | 自动注册             |

<br/>

- 加载方式

  BeanFactroy采用的是惰性加载形式来注入Bean的，即只有在使用到某个Bean时(调用getBean())，才对该Bean进行加载实例化。这样，我们就不能发现一些存在的Spring的配置问题。如果Bean的某一个属性没有注入，BeanFacotry加载后，直至第一次使用调用getBean方法才会抛出异常。

​        ApplicationContext是在容器启动时，一次性创建了所有的Bean。这样，在容器启动时，我们就可以发现Spring中存在的配置错误，这样有利于检查所依赖属性是否注入。 ApplicationContext启动后预载入所有的单实例Bean，通过预载入单实例bean ,确保当你需要的时候，你就不用等待，因为它们已经创建好了。

- 启动速度

  相对于基本的BeanFactory，ApplicationContext 唯一的不足是占用内存空间。当应用程序配置Bean较多时，程序启动较慢。

- 创建方式

  BeanFactory通常以编程的方式被创建，ApplicationContext还能以声明的方式创建，如使用ContextLoader。

- 扩展点的注册

  BeanFactory和ApplicationContext都支持BeanPostProcessor、BeanFactoryPostProcessor的使用，但两者之间的区别是：BeanFactory需要手动注册，而ApplicationContext则是自动注册。

<br/>

<br/>

## 核心源码梳理

在Spring IOC方面，最核心的源码也就是这三步：

1. bean解析
2. bean注册
3. bean加载

限于篇幅，这里仅对三段源码的核心逻辑做一个整理，这也是在我看来比较有用，但网上又很少有人去写的。

而至于真正要去深读源码的话，建议在网上找一些大牛的博客，或者阅读《Spring源码深度解析》这本书。

<br/>

### （1）Bean解析

主要流程：

1. Spring载入Bean的XML配置文件

2. 把XML文件解析为Resource对象

   Resource接口抽象了所有Spring内部使用到的底层资源，例如File、URL、Classpath等等。

3. 加载XML得到对应的Document

4. 根据Document注册Bean

   XmlBeanDefinitionReader的registerBeanDefinitions方法 → DefaultBeanDefinitionDocumentReader的parseBeanDefinitions方法，其间有各种标签解析。有兴趣的读者可以去看看这一段的源码，是解析阶段里相对比较重要的源码

5. 解析并注册

   解析完成的bean以BeanDefinition的形式注册到BeanDefinitionRegistry（就是我们的IOC容器）中，以map形式保存。

<br/>

其中**BeanDefinition**是一个关键的点，需要注意一下：

BeanDefinition是一个接口，在Spring中存在三种实现：RootBeanDefinition、ChildBeanDefinition以及GenericBeanDefinition。其中GenericBeanDefinition是xml中读到的bean信息第一步存储的形式，之后会转为RootBeanDefinition。

- 父bean用RootBeanDefinition表示，

- 子bean用ChildBeanDefinition表示，

- 没有父bean的bean用RootBeanDefinition表示。

- GenericBeanDefinition是一站式服务类。

什么叫一站式服务类？可以理解为就是过渡用的类，最后还是要转为RootBeanDefinition和ChildBeanDefinition的。

<br/>

### （2）Bean注册

将beanDefinition直接放到map中，使用beanName作为key。

不过在真正注册之前，要做一些准备工作（了解即可）：

1. 校验AbstractBeanDefinition的methodOverrides属性
2. 对beanName已经注册的情况处理（如果不允许beanName覆盖就抛出异常）
3. 加入map缓存
4. 清除解析之前留下的对应beanName的缓存

<br/>

### （3）Bean加载

在AbstractBeanFactory的`doGetBean(final String name, @Nullable final Class<T> requiredType,@Nullable final Object[] args, boolean typeCheckOnly)`中加载

1. 转换对应beanName为真实的beanName（转换别名为真正的beanName，如果是FactoryBean就去除开头的&符号）

   - 之所以如果是FactoryBean就要做处理，是因为bean的class属性实现类是FactoryBean时，通过getBean返回的不是FactoryBean本身，而是FactoryBean的getObject方法返回的对象

   - FactoryBean是为了隐藏实例化一些复杂bean的细节，给上层应用带来便利。FactoryBean使用了工厂模式

2. 尝试从缓存中加载单例

   1. 进入方法`getSingleton(String beanName, boolean allowEarlyRefe rence)`且allowEarlyReference为true
      1. 优先在**singletonObjects**找
      2. 没有就在**earlySingletonObjects**找
      3. 再没有就取出对应的**singletonFactories**.get(beanName).getObject()，并存到**earlySingletonObjects**里

   2. 如果缓存中能找到
      1. bean的实例化（对缓存中取出的原始状态bean进行加工）
   3. 如果缓存中找不到
      1. prototype模式的依赖检查（有循环依赖就抛出异常，只有单例情况才会尝试解决循环依赖）
      2. 如果当前beanFactory中没有相应beanName，就尝试从parentFactory里检测、取出beanName对应bean
      3. 将GenericBeanDefinition转换为RootBeanDefinition（这是因为之后对于bean的所有后续处理都是针对RootBeanDefinition进行的）
      4. 寻找依赖，如果存在依赖就递归初始化依赖的bean
      5. 针对不同的scope进行bean创建
      6. 类型转换（例如返回的bean是个String，但requiredType传Integer）


<br/>

其中2.1需要利用三级缓存解决循环依赖问题：

（在DefaultSingletonBeanRegistry的`getSingleton(String beanName, boolean allowEarlyReference)`方法中）

涉及到的重点缓存map：

**singletonObjects**：存放初始化好的bean（beanName → bean实例）

**earlySingletonObjects**：存放刚实例化好的，但是还未配置属性和初始化的bean（提前曝光的单例对象）

**singletonFactories**：存放beanName和创建bean的工厂之间的关系（beanName → ObjectFactory）

举例：

例如循环依赖A → B → A

1. 尝试getSingleton("A",true)

   singletonObjects里找不到，并且A并不在创建状态（`isSingletonCurrentlyInCreation(beanName)`为false），直接返回空（也就是缓存取不到）

   缓存取不到就开始直接尝试加载，加载时要递归加载依赖的bean，所以接下来尝试加载B

2. 尝试getSingleton("B",true)

   singletonObjects里找不到，并且B并不在创建状态，直接返回空

   开始尝试加载B依赖的bean，也就是A

3. 尝试getSingleton("A",true)

   singletonObjects里找不到，并且A在创建状态，所以去earlySingletonObjects里找

   发现earlySingletonObjects里也没有，就从singletonFactories里拿，提前曝光到earlySingletonObjects里

   A成为一个还未初始化完全，但是可以被依赖的bean

4. B成功初始化
5. A成功初始化

