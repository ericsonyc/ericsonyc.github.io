---
layout: post
author: Ericson
date: 2015-10-29 15:25
title: Java Collections <二>
category: Java
tag: [java,collection]
---

Map用于保存具有映射关系的数据，<key,value>。Map接口和Set接口很像，Set接口下的实现类在Map中都有对应的类，Set中的一个元素是Map中对应键值对的封装。

HashMap和Hashtable的关系类似于ArrayList和Vector的关系，Hashtable是线程安全的，而HashMap是线程不安全的，HashMap中可以保存null值（key和value都可以），而Hashtable中不能保存null。与HashSet类似，尽量不要使用可变对象作为HashMap和Hashtable的key，尽量不要修改元素的key值，会引起混乱。

LinkedHashMap用一个双向链表来维护key-value的次序，性能略低于HashMap，因为要维护一个链表。Properties类继承Hashtable，该对象在处理属性文件时特别方便，该类可以把Map对象和属性文件关联起来。

SortedMap接口的实现类是TreeMap类，TreeMap就是一个红黑树数据结构，每个<key,value>对就是一个红黑树的节点，根据key来进行排序。

WeakHashMap与HashMap的用法基本相似，区别在于，HashMap的key保留了对实际对象的强引用，这意味着只要该HashMap对象不被销毁，该HashMap的所有key所引用的对象就不会被垃圾回收，HashMap也不会自动删除这些key所对应的键值对；但WeakHashMap的key只保留了对实际对象的弱引用，这意味着如果WeakHashMap对象的key所引用的对象没有被其他强引用变量所引用，则这些key所引用的对象可能被垃圾回收，WeakHashMap也可能自动删除这些key所对应的键值对。<br/>
[Java Code]
{% highlight java %}
public void weak() {
        WeakHashMap whm = new WeakHashMap();
        whm.put(new String("a"), new String("a"));
        whm.put(new String("b"), new String("b"));
        whm.put(new String("c"), new String("c"));
        whm.put("java", new String("love"));
        System.out.println(whm);
        System.gc();//garbage collection
        System.runFinalization();//run finalize method
        System.out.println(whm);
    }
{% endhighlight %}
>第二个输出只输出“java”键值对，其他abc被释放掉，因为是匿名对象，属于弱引用，“java” key被保存到了常量池。

IdentityHashMap类：该类实现机制和HashMap基本相似，但它在处理两个key相等时比较独特，在IdentityHashMap中，当且仅当两个key严格相等（内存地址也要一样）时，IdentityHashMap才认为两个key相等（对于HashMap，只要equals和hashCode一样就行）。

EnumMap类是一个与枚举一起使用的Map实现，EnumMap中的所有key都必须是单个枚举类的枚举值，在内部以数组形式保存，不允许key为null，但允许value为null。

Enumeration接口是Iterator迭代器的老版本，是线程安全的。