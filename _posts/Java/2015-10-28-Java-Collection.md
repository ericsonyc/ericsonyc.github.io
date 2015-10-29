---
layout: post
author: Ericson
date: 2015-10-28 23:44
title: Java Collections
category: Java
---

Java集合类是一个特别有用的工具类，可以用于存储数量不等的多个对象，并可实现常用的数据结构。<br/>
Java集合大致可以分为：Set、List、Map三种体系:
<ul>
	<li>Set：代表无序、不可重复的集合</li>
	<li>List：代表有序、可重合的集合</li>
	<li>Map：代表具有映射关系的集合</li>
</ul>
Java集合类主要由两个接口派生而来：Collection和Map，Collection和Map是java集合框架的根接口。Collection接口的继承树如下图所示：<br/>
![Collection](/public/img/java/collection.png)
Map接口继承树如下图所示：<br/>
![Map](/public/img/java/map.png)
使用Iterator接口可以遍历集合元素，Iterator本身并不提供盛装对象的能力。<font color="red">当使用Iterator对集合里的元素进行迭代时，Iterator并不是把集合本身传递给迭代变量，而是把集合元素的值传给迭代变量，所以修改迭代变量的值对集合元素本身没有任何影响，但可以删除。</font><br/>
[Java Code]
{% highlight java %}
public void iterator(){
        Collection books=new ArrayList();
        books.add("a");
        books.add("b");
        books.add("c");
        Iterator it=books.iterator();
        while(it.hasNext()){
            String book=(String)it.next();
            book="d";
        }
        System.out.println(books.toString());
    }
{% endhighlight %}
>输出a,b,c

Iterator是fail-fast机制，一旦在迭代过程中检测到该集合已经被修改过，程序立即引发ConcurrentModificationException异常。Iterator方法的工作原理如下图所示：
![Iterator](/public/img/java/iterator.jpg)

Set集合：判断两个对象相同不是用==运算符，而是用equals方法。因此可以修改equals方法来添加相同的元素。

HashSet类：不是同步的，允许null值，HashSet底层实际上是一个HashMap，把<key,value>值封装成一个Map.Entry类，通过Entry类中的key来比较添加的值。HashSet判断两个对象相等的标准是通过equals方法比较相等，并且hashCode方法返回一样的值。当hashCode相同，当equals不同，元素会以链式存储，影响性能。<font color="red">如果修改一个HashSet中的值可能会出现混乱，因为hashCode可能会根据对象的值计算，当改掉该值时，该对象依然存储在原来的hashCode上，但是再次访问它计算hashCode就不是原来的位置了。</font>

LinkedHashSet类：维护元素的插入顺序，因此性能略低于HashSet，但在迭代访问Set里的全部元素时将有很好的性能，因为它以链表来维护内部顺序。该类底层实现是LinkedHashMap类，维护了一个双重链接列表。此链接列表定义了迭代顺序，该类不是同步的。

TreeSet类：是SortedSet接口的实现类，可以确保集合元素处于排序状态。TreeSet是通过比较元素大小来排序，而不是插入顺序，所以要求元素直接必须要是可比较的，如果把一个对象添加到TreeSet中，则该对象的类必须实现Comparable接口，否则程序会抛出异常。TreeSet使用两种排序方法：自然排序和定制排序。
<ul>
	<li>自然排序：调用元素的compareTo方法，按元素的升序排序。编程时要尽量确保equals方法和compareTo方法保持一致性。<font color="red">如果TreeSet中包含了可变对象，当可变对象的Field被修改时，TreeSet在处理这些对象时将会非常复杂，而且容易出错。</font></li>
	<li>定制排序：通过Comparator接口来重写compareTo方法。</li>
</ul>
TreeSet类是线程非安全的，源码中是用TreeMap来实现的，而TreeMap采用红黑树的结构来存储数据，是一种自平衡的排序二叉树，TreeSet把<key,value>值封装成Entry类来表示红黑树的一个节点。

EnumSet类：