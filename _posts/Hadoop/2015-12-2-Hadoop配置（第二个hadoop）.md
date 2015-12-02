---
layout: post
author: Ericson
date: 2015-12-2
title: Hadoop配置（集群部署第二个Hadoop）
category: Hadoop
tag: [hadoop,configuration]
---

场景：一个集群有多人使用，假设有两个人，一个人已经在他的用户下配置了一个Hadoop集群，并且一直在跑程序，另一个同学有自己的用户，他对Hadoop做了一些源码更改，想自己搭建一个Hadoop集群（或者他和前一个人不熟，想用自己搭建的Hadoop），这就需要集群上有两个Hadoop，如果配置不好会出现端口冲突的问题，使得两个人配置的Hadoop不能使用。

Hadoop本身也就是由一组Java程序组成，通过Socket绑定到网络端口上进行RPC，因此只要保证以下两点就可以：
<ul>
    <li>Hadoop在OS上的本地存储路径不冲突</li>
    <li>Hadoop在OS上的网络端口不冲突</li>
</ul>
1.路径问题：<br>
只需要把hadoop.tmp.dir设置到用户目录下即可
2.端口问题：<br>
Hadoop常用的端口：<br>
HDFS端口如下：

<div align="center">
<table border="1">
    <tr>
        <td>参数</td>
        <td>描述</td>
        <td>默认</td>
        <td>配置文件</td>
        <td>例子值</td>
    </tr>
    <tr>
        <td>fs.default.name</td>
        <td>namenode RPC交互端口</td>
        <td>8020</td>
        <td>core-site.xml</td>
        <td>hdfs://Master:8020</td>
    </tr>
    <tr>
        <td>dfs.http.address</td>
        <td>namenode web管理端口</td>
        <td>50070</td>
        <td>hdfs-site.xml</td>
        <td>0.0.0.0:50070</td>
    </tr>
    <tr>
        <td>dfs.datanode.address</td>
        <td>datanode控制端口</td>
        <td>50010</td>
        <td>hdfs-site.xml</td>
        <td>0.0.0.0:50010</td>
    </tr>
    <tr>
        <td>dfs.datanode.ipc.address</td>
        <td>datanode的RPC服务器地址和端口</td>
        <td>50020</td>
        <td>hdfs-site.xml</td>
        <td>0.0.0.0:50020</td>
    </tr>
    <tr>
        <td>dfs.datanode.http.address</td>
        <td>datanode的HTTP服务器和端口</td>
        <td>50075</td>
        <td>hdfs-site.xml</td>
        <td>0.0.0.0:50075</td>
    </tr>
</table>
</div>