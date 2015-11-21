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
<ul>
<li>@Override：可以强制一个子类必须覆盖父类的方法，该标记只能用作方法，不能用作其他内容</li>
<li>@Deprecated：表示已过时，程序调用已过时的东西会导致编译警告</li>
<li>@SuppressWarnings：抑制编译器警告</li>
<li>@SafeVarargs：是Java7专门为抑制“堆污染”编译警告，</li>
</ul>
除了java.lang下的4个基本Annotation外，在java.lang.annotation包下还提供了4个Meta Annotation，这4个Meta Annotation都用于修饰其他Annotation定义。

@Retention只能用于修饰一个Annotation定义，用于指定被修饰的Annotation可以保留多长时间。@Retention包含一个RetentionPolicy类型的成员变量，所以使用时需赋值。有三个值：
<ul>
	<li>RetentionPolicy.CLASS:编译器将Annotation保持在class文件中，当运行时，JVM不再保留Annotation</li>
	<li>RetentionPolicy.RUNTIME:编译器将Annotation保存在class文件中，当运行java程序时，JVM会保留Annotation</li>
	<li>RetentionPolicy.SOURCE:Annotation只保留在源代码中，编译器直接丢弃Annotation</li>
</ul>
示例：
{%highlight java%}
@Retention(RetentionPolicy.CLASS) or
@Retention(RetentionPolicy.RUNTIME)
{%endhighlight%}

@Target也只能修饰一个Annotation定义，它用于指定被修饰的Annotation能用于哪些程序单元。@Target也有一个成员变量，变量如下所示：
<ul>
	<li>ElementType.ANNOTATION_TYPE:指定该策略的Annotation只能修饰Annotation</li>
	<li>ElementType.CONSTRUCTOR:指定该策略的Annotation只能修饰构造器</li>
	<li>ElementType.FIELD:指定该策略Annotation只能修饰成员变量</li>
	<li>ElementType.LOCAL_VARIABLE:指定该策略Annotation只能修饰局部变量</li>
	<li>略(网上查)</li>
</ul>

@Documented用于指定被该Meta Annotation修饰的Annotation类将被javadoc工具提取成文档，如果定义Annotation类时使用了@Documented修饰，则所有使用该Annotation修饰的程序元素的API文档中将会包含该Annotation说明。

@Inherited指定被它修饰的Annotation将具有继承性——如果某个类使用了@Annotation修饰，则其子类将自动被@Annotation修饰。

自定义Annotation，使用@interface来自定义新的Annotation，代码如下：
{%highlight java%}
public @interface Test{
	
}
{%endhighlight%}
自定义Annotation中还可以声明成员变量，Annotation中的成员变量是用无参数的方法来声明的，示例如下：
{%highlight java%}
public @interface Test{
	String name() default "ericson";
	int age() default 25;
}
{%endhighlight%}