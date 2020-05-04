> 本仓库适用对象：
>
> 1. 想要实践Java后台开发的新手
> 2. 想要拿offer到手软的应届生、低工龄社会人



更多原创内容和干货分享：

1. [公众号—Jyannis](#公众号) ： 每日面试题分享 + 第一手热乎乎面经及面试故事

   

<p align="center">
  <a href="#联系我"><img src="https://img.shields.io/badge/weChat-微信群-blue.svg" alt="微信群"></a>
  <a href="#公众号"><img src="https://img.shields.io/badge/%E5%85%AC%E4%BC%97%E5%8F%B7-Jyannis-lightgrey" alt="公众号"></a>
  <a href="https://me.csdn.net/m0_46311226"><img src="https://img.shields.io/badge/csdn-CSDN-red.svg" alt="投稿"></a>
  <a href="https://www.zhihu.com/people/jie-ci-82-51"><img src="https://img.shields.io/badge/zhihu-知乎-yellow" alt="投稿"></a>
</p>




## 目录

- [我是零基础，怎么上手Java后台开发（SpringBoot）？](https://zhuanlan.zhihu.com/p/97958284)
- [我刚学明白SpringBoot，怎么开展学习微服务？](https://github.com/jyannis/SpringCloud-Alibaba-Learning)
- [Java技术栈学习书籍推荐](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483774&idx=1&sn=76f898602aa9af5913f4c9ea82fc0d20&chksm=9ffc6318a88bea0ed50d39255bc27366391c62d84b3bbda79772ba11cb740070e91dd7b50bec&token=1776113537&lang=zh_CN#rd)
- Java
    - 常见Java基础面试题
    - 容器（集合框架）
- JVM
    - [运行时数据区](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483776&idx=1&sn=25fbf98bb6dcda4e924675dc1e64997e&chksm=9ffc63e6a88beaf053d6036e5c4fff87af41df7d5a6e35329e115f9123b9b2d5c4363068f4c2&token=1776113537&lang=zh_CN#rd)
    - [垃圾回收](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483779&idx=1&sn=6ae9053df60475e7033ed6f17615b7e4&chksm=9ffc63e5a88beaf3f717c04274c087f7b38b8cdcb65ac20d165ee301a3c1dc28d10260b3cca1&token=1776113537&lang=zh_CN#rd)
        - [Java四种引用类型](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483783&idx=1&sn=c04e4ff81c62e1048f56931fb60eb845&chksm=9ffc63e1a88beaf763aa90e484fae5b9506c5c68224b657ab46d29aa51316f72ee71ba823ddf&token=1776113537&lang=zh_CN#rd)
    - [类加载机制](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483777&idx=1&sn=f330cb56e1bf6e0863792c6160299416&chksm=9ffc63e7a88beaf16eeb8a05a6081dfa0baf2306779d2761c480e65262eee776bb2f8c88de9d&token=1776113537&lang=zh_CN#rd)
    - [调优命令行工具](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483719&idx=1&sn=fc747d2e5b9b1928f312f1cb9a643f3b&chksm=9ffc6321a88bea37aacff8850cd60b9b4e7b1540850daf97dfe853d1d1a3b07d30fe6d3ed250&token=1776113537&lang=zh_CN#rd)
    - [Volatile关键字](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483765&idx=1&sn=cf0c1b74985e2389719d6ae1f51f4258&chksm=9ffc6313a88bea05f7c77c45247a5a1ce251b77b13c71c0068a4b30cc2effee2e80e21e59988&token=1776113537&lang=zh_CN#rd)
    - [JMM](https://github.com/jyannis/JavaLearning/blob/master/docs/JVM/JMM%20Java%E5%86%85%E5%AD%98%E6%A8%A1%E5%9E%8B.md)
    - [JVM问题排查实战](#JVM问题排查实战)
- 并发
    - Java与线程的基础知识
    - [Synchornized关键字](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483769&idx=1&sn=bdb296488a0b2b30ae98287ecd7151cf&chksm=9ffc631fa88bea09aed92f62d1c2a8b6d469ec918586fa4e011b72c304bcb8ae5541465de9d3&token=1776113537&lang=zh_CN#rd)
    - 锁优化
    - [同步组件](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483773&idx=1&sn=53c49298fae09a9e8bc089bf2cc0f046&chksm=9ffc631ba88bea0de0e26906c1bfb2e7234aafb8044a8d3d798c01457be77a57d57c0858c2cb&token=1776113537&lang=zh_CN#rd)
    - [线程池](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483763&idx=1&sn=73501f177d4882a23401e614b7a06b5d&chksm=9ffc6315a88bea030635a6fc138fe4d41b10a2801c04f7eefdbe642b0317d5a9de98e627edef&token=1776113537&lang=zh_CN#rd)
    - 并发容器
    - [ThreadLocal](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483891&idx=1&sn=7a6f3790a5fccd9cd378141215941a18&chksm=9ffc6395a88bea831a9b7c03fa50abefba84574f16f2c7c7186ce1e8097bf8f199847d041943&token=1533871073&lang=zh_CN#rd)
- MySQL
    - [索引](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483844&idx=1&sn=d49ea52feb5efefc6f62fdb27bb2bc39&chksm=9ffc63a2a88beab497fc893b09657dd76bfe8135275cd01bca1e9ca5589c3b99de5f28a9f2ba&token=1776113537&lang=zh_CN#rd)
    - [锁](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483775&idx=1&sn=a9f52d630f191aa1afcf71e38e595800&chksm=9ffc6319a88bea0f8c37b39d1b9aeabb03b7f403e832729c4172115d30db91325bcf3ce57535&token=1776113537&lang=zh_CN#rd)
    - [Explain执行计划分析](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483863&idx=1&sn=9a25e58d37ee017688805fee46f59bb1&chksm=9ffc63b1a88beaa79269295884f3f4a275edd3879c3131784bd32255fe21e022e9470f986b9d&token=1776113537&lang=zh_CN#rd)
    - 分区
    - [InnoDB存储引擎体系结构](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483864&idx=1&sn=04ffd18b14d868acc72865bec6dd5e24&chksm=9ffc63bea88beaa8780b77edf6fed1bb72bc12c06d8919ffc5a6223f14dcd3e48665b59173f8&token=1776113537&lang=zh_CN#rd)
    - 文件
    - 查询处理流程
- Redis
    - [概述](https://github.com/jyannis/JavaLearning/blob/master/docs/redis/概述.md)
    - [数据结构](https://github.com/jyannis/JavaLearning/blob/master/docs/redis/数据结构.md)
    - [持久化](https://github.com/jyannis/JavaLearning/blob/master/docs/redis/持久化.md)
    - [常见缓存问题及其解决](https://github.com/jyannis/JavaLearning/blob/master/docs/redis/常见缓存问题及其解决.md)
    - [常用命令](https://github.com/jyannis/JavaLearning/blob/master/docs/redis/常用命令.md)
- Spring
    - IOC
    - AOP
    - 事务
- [网络](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483809&idx=1&sn=ddf5933cf18ed6f5ba4e30a634f18da3&chksm=9ffc63c7a88bead1a8c91fa846a7ba7bacbf8faff04b6ec4d3f99909331a0a369de75d036006&token=1776113537&lang=zh_CN#rd)
- 操作系统
- 设计模式
    - [装饰者Decorator](https://github.com/jyannis/design-patterns/tree/master/Decorator)
    - [观察者Observer](https://github.com/jyannis/design-patterns/tree/master/Observer)
    - [策略Strategy](https://github.com/jyannis/design-patterns/tree/master/Strategy)
- 算法
- IO
    - [一文读懂BIO、NIO、AIO](https://github.com/jyannis/JavaLearning/blob/master/docs/IO/%E4%B8%80%E6%96%87%E8%AF%BB%E6%87%82BIO%E3%80%81NIO%E3%80%81AIO.md)
- [各种面经与面试故事](#面经与面试故事)
- 面试技巧
    - [如何进行知识积累](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#如何进行知识积累)
      - [如何把握实践与理论的天平](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#如何把握实践与理论的天平)
      - [我应该如何整理笔记](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#我应该如何整理笔记)
      - [怎么复习才不会忘](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#怎么复习才不会忘)
    - [面试前](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#面试前)
      - [怎么写出让人眼前一亮的简历](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#怎么写出让人眼前一亮的简历)
      - [如何突击面试](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#如何突击面试)
      - [面试前焦虑该怎么办](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#面试前焦虑该怎么办)
    - [面试开始](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#面试开始)
      - [自我介绍到底要怎么说](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#自我介绍到底要怎么说)
    - [面试中](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#面试中)
      - [技术面试的时候应该注意些什么](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#技术面试的时候应该注意些什么)
      - [面试尬场怎么办](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#面试尬场怎么办)
      - [如何学会埋坑](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#如何学会埋坑)
    - [面试结束](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#面试结束)
      - [面试官：“你有什么想问我的吗”，该说什么？](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#面试官："你有什么想问我的吗"，该说什么？)
      - [我怎样才能知道我是否通过了](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md#我怎样才能知道我是否通过了)
- 技术人生
    - [今天我收到了蚂蚁金服实习offer](https://github.com/jyannis/JavaLearning/blob/master/docs/tech-life/今天我收到了蚂蚁金服实习offer.md)





## JVM问题排查实战

- [发生死锁如何排查](https://blog.csdn.net/m0_46311226/article/details/104970857)
- [CPU过高如何排查](https://blog.csdn.net/m0_46311226/article/details/105010210)
- [发生OOM如何排查](https://blog.csdn.net/m0_46311226/article/details/104996664)





## 面经与面试故事

面经：由jyannis一个字一个字地整理答案，供读者自测与复习。

- 阿里
  - [阿里云一面 2020-03-11](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483795&idx=1&sn=68b8a8607863a8b57de367bfbafd325c&chksm=9ffc63f5a88beae3bf9026fb77174edd9814906a9330149b379ca5919a2f9d22a283ecaa17c6&token=1776113537&lang=zh_CN#rd)
  - [淘系部门一面 2020-03-14](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483850&idx=1&sn=b2323dc0690791f2efb8b7287d3d3218&chksm=9ffc63aca88beabae428a6682c84b9fc8861b89aeef3ccfa97474508a3f52fff68d59bdcc698&token=1776113537&lang=zh_CN#rd)
  - [淘系部门一面 2020-03-15](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483859&idx=1&sn=03f4b1b3a66a8d6ab671ac15d837109a&chksm=9ffc63b5a88beaa3ed51cd7da9e6ae74309ebc9d89a94ee733f4e63e7cbbec1ab4f608cc3f07&token=1776113537&lang=zh_CN#rd)



面试故事：jyannis身边的同学真实的面试经历

- 阿里
  - [淘系部门三面](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483816&idx=1&sn=a0f040286dc5a54f7139421e802a8705&chksm=9ffc63cea88bead8974be27ed3fdb828d9439c5626f8bbb291d4aa2270329f5dd27a33ced115&token=1776113537&lang=zh_CN#rd)
- 字节跳动
  - [中台部门一面](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483835&idx=1&sn=0e1e8f8f52e98e6fd84552ff168c6d2e&chksm=9ffc63dda88beacb563e078874f87c0c79cf6922d7eb36e3282cc426bd1a60e295b6674f4972&token=1776113537&lang=zh_CN#rd)
  - [中台部门二面](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483831&idx=1&sn=68ddf105230922302e3d7b051efe7c8a&chksm=9ffc63d1a88beac7facb9f1e1880075c45bc5e8764e6951ac8cb2eb2e0f15b7183d24610bf5a&token=1776113537&lang=zh_CN#rd)
- 携程
  - [后台日常实习](https://mp.weixin.qq.com/s?__biz=MzA4Mjk5OTA0OQ==&mid=2247483836&idx=1&sn=3f47d42abb1a9ad074acf8b22f4145ca&chksm=9ffc63daa88beacce39f45211b36de0badf00c143d7f0d125ee61f0a025facc6d8f419142799&token=1776113537&lang=zh_CN#rd)





## 说明

开源项目在于大家的参与，这才使得它得以进步。点一下watch是对我最大的支持。



### 作者介绍

​	我是来自华东师范大学软件工程专业的2017级本科生。

​	于高三毕业（2017年7月）开始学习Java语言，在今年（2020，大三）先后斩获携程（1月）、字节跳动（三月）、蚂蚁金服（四月）实习生offer，并拿到最高的双A评级（本部门P9评A + 交叉面P9评A），大概率转正。

​	作为一名踩过荆棘走过弯路的Java学习者，希望借助这篇开源文档对后来者提供一些帮助。



### 关于转载

如果你需要转载本仓库的一些文章到自己的博客的话，记得注明原文地址就可以了。

### 如何对该开源文档进行贡献

1. 笔记内容大多是手敲，所以难免会有笔误，你可以帮我找错别字。
2. 很多知识点我可能没有涉及到，所以你可以对其他知识点进行补充。
3. 现有的知识点难免存在不完善或者错误，所以你可以对已有知识点进行修改/补充。





### 联系我

疫情阶段，jyannis最近闲得慌，欢迎大家来打扰：



微信：

<img src="https://gitee.com/jyannis/JavaLearning/raw/master/docs/%E5%BE%AE%E4%BF%A1.png" alt="微信" style="zoom: 50%;" />





扣扣：

<img src="https://gitee.com/jyannis/JavaLearning/raw/master/docs/qrcode_1586150172794.jpg" alt="qq" style="zoom:50%;" />





### 公众号

欢迎关注jyannis，不定期分享第一手笔经面经，及最热最潮的技术知识。

你的每一次点击和在看都是对我最大的支持！

![Jyannis](https://gitee.com/jyannis/JavaLearning/raw/master/docs/Jyannis.jpg)

