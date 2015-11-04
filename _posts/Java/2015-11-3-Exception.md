---
layout: post
author: Ericson
date: 2015-11-3 16:28
title: Java异常处理
category: [Java,异常处理]
tag: [java,异常处理]
---

Java将异常分为两种，Checked异常和Runtime异常，Java认为Checked异常都是可以在编译阶段被处理的异常，所以它强制程序处理所有的Checked异常；而Runtime异常则无须处理。

Java的异常处理机制可以让程序具有极好的容错性，让程序更加健壮。当程序运行出现意外情形时，系统会自动生成一个Exception对象来通知程序，从而实现将“业务功能实现代码”和“错误处理代码”分离，提供更好的可读性。异常类的继承关系如下图所示：
<div align="center">
<img src="/public/img/algorithm/exception.jpeg" width="350" height="550">
</div>
粉红色的代表Checked Exception，其必须被try-catch语句块所捕获；绿色的异常是运行时异常，是Unchecked Exception，不需要捕获。Java把所有的非正常情况分为两种：异常和错误，它们都继承Throwable父类。Error错误，一般是指与虚拟机相关的问题，如系统崩溃、虚拟机错误、动态链接失败等。finally语句块中负责处理一些资源释放，如果finally里含有return语句，则try里的return语句将会失效。