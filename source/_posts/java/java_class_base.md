title: Java反射基础
comments: true
date: 2016-07-28 10:30:12
updated: 2016-07-28 10:30:12
tags:
  - java_base
  - knowledge
categories:
  - java
---

# Java 反射
在运行中，可以使程序创建和控制任何类的对象。

##  缺点
1. 性能: 对类的逻辑结构信息获取后，然后对这些类进行操作（所以相对于源码方式速度较低）
1. 模糊程序内部处理逻辑等

## Java reflection
使类和数据结构按名称动态检索相关的信息并可以操作这些信息。

java.lang.reflect.*(Field,Method,Constructor)
java.lang.Class

## 反射的实现方式
1. 通过对象的getClass()，例如：String.getClass
1. 通过对象实例方法获取，例如：String.classs
1. 通过Class.forName("java.lang.String"),加载时，会将对应的静态方法加载
