---
layout: post
title: 总结Java8的HashMap
comments: true
author: "Yin Haomin"
tags:
    - HashMap
    - 总结
---

给自己挖一坑位，总结一下Java8的HashMap。<br>

#### 1.关于红黑树
关于红黑树的性质，网上那么多资料，讲一下我的理解。<br>
红黑树是一种二分查找树，之所以设计这种树，就是为了一方面要快速查找，一方面又不希望在新的数据插入删除的时候，浪费很多时间空间来保持树的好的查找性。<br>

#### 2.HashMap在1.7和1.8中的区别
20180826 Added<br>
1. Java 7使用hash表存储HashMap，存在的问题是，当很多数据发生哈希撞击，到同一个链表时，就会使查询效率退化为O(N);<br>
2. Java 8为了解决这个问题，当同一个hash值大于等于8的时候(不是7)，将不再使用链表存储；<br>
JDK7与JDK8中HashMap的实现：http://www.importnew.com/23164.html<br>

那么问题来了:<br>
1. hashCode默认是如何计算出来的呢？<br>
Redis和Java的哈希函数：https://www.jianshu.com/p/bb64cd7593ab<br>
(1).由此可见，java的Object的默认hashCode是通过Park-Miller算法计算出来的；<br>
(2).而Character、Integer、Long、Double的hashCode方法返回包装的基本类型;<br>
String的hashCode返回其值计算出来的信息；<br>
(3).如果重写了对象的hashCode()方法的话，则会更改对象在对象头中的MarkWord的hashCode部分的信息；<br>
2. What is the best way to implements the hashCode() function?<br>
视业务而定，但一般将所有的值都考虑进去；<br>
3. hashCode和equals的重写的逻辑关系？<br>
hashCode<br>
(1).对于同一个对象，多次调用，都返回同一个；<br>
(2).如果equals，则hashCode一定相等；<br>
(3).如果hashCode相等，但是equals不一定相等；<br>
equals几个特性；<br>
自反性，对称性，传递性，一致性；<br>

#### 3.HashMap的源码分析

#### 4.总结

#### 5.参考资料
1. [红黑树(一)之 原理和算法详细介绍](https://www.cnblogs.com/skywang12345/p/3245399.html)
2. [Java8系列之重新认识HashMap](http://www.importnew.com/20386.html)
3. [JDK7与JDK8中HashMap的实现](http://www.importnew.com/23164.html)
4. [Redis和Java的哈希函数](https://www.jianshu.com/p/bb64cd7593ab)
