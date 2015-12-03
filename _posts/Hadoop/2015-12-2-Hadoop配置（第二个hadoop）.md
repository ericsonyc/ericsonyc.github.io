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

<div style="width:auto; height:auto; overflow:auto">
<table>
    <tr>
        <td>参数</td>
        <td>描述</td>
        <td>默认</td>
        <td>配置文件</td>
        <td>例子值</td>
    </tr>
    <tr>
        <td>fs.defaultFS</td>
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

MapReduce端口如下：

<div style="width:auto; height:auto; overflow:auto">
<table>
    <tr>
        <td>参数</td>
        <td>描述</td>
        <td>默认</td>
        <td>配置文件</td>
        <td>例子值</td>
    </tr>
    <tr>
        <td>mapred.job.trackerjob</td>
        <td>tracker交互端口</td>
        <td>8021</td>
        <td>mapred-site.xml</td>
        <td>hdfs://master:8021</td>
        <td>mapred.job.trackerjob</td>
    </tr>
    <tr>
        <td>mapred.job.tracker.http.address</td>
        <td>jobtracker的web管理端口</td>
        <td>50030</td>
        <td>mapred-site.xml</td>
        <td>0.0.0.0:50030</td>
    </tr>
    <tr>
        <td>mapred.task.tracker.http.address</td>
        <td>tasktracker的HTTP端口</td>
        <td>50060</td>
        <td>mapred-site.xml</td>
        <td>0.0.0.0:50060</td>
    </tr>
</table>
</div>
其他端口：

<div style="width:auto; height:auto; overflow:auto">
    <table>
        <tr>
            <td>参数</td>
            <td>描述</td>
            <td>默认</td>
            <td>配置文件</td>
            <td>例子值</td>
        </tr>
        <tr>
            <td>dfs.namenode.secondary.http-address</td>
            <td>secondary Namenode web管理端口</td>
            <td>50090</td>
            <td>hdfs-site.xml</td>
            <td>0.0.0.50090</td>
        </tr>
    </table>
</div>
以上有些配置是hadoop1.x的，2.x的配置请参考[官方文档](http://hadoop.apache.org/docs/)，大概修改上面几个端口以及目录就可以配置多个hadoop。目录配置也可以参考官方文档进行相应的修改。

Hadoop的目录配置看下图：

<div style="width:auto; height:auto; overflow:auto">
    <img src="/public/img/hadoop/directory_configuration.jpg">
</div>