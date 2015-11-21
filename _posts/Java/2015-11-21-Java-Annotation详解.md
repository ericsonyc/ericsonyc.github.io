---
layout: post
author: Ericson
date: 2015-11-21 16:12
title: Java Annotation（注释）详解
category: java
tag: [java,annotation]
---

Annotation其实是代码里的特殊标记，这些标记可以在编译、类加载、运行时被读取，并执行相应的处理。通过使用Annotation，程序开发人员可以在不改变原有逻辑的情况下，在源文件中嵌入一些补充的信息。代码分析工具、开发工具和部署工具可以通过这些补充信息进行验证或者进行部署。

Annotation提供了一种为程序元素设置元数据的方法，从某些方面来看，Annotation就像修饰符一样，可用于修饰包、类、构造器、方法、成员变量、参数、局部变量的声明，这些信息被存储在Annotation的“name=value”对中。

Annotation必须使用工具APT（Annotation Processing Tool）来处理，工具负责提前Annotation里包含的元数据，工具还会根据这些元数据增加额外的功能。

Java提供了4个基本的Annotation：
* @Override
* @Deprecated
* @Suppress Warnings
* @SafeWarargs
