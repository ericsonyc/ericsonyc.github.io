---
layout: post
author: Ericson
date: 2015-11-15
title: Hadoop safemode详解
category: Hadoop
tag: [hadoop,safemode]
---

Hadoop在NameNode启动时会先进入Safemode安全模式。在安全模式下，只允许对元数据的访问操作。默认情况下，NameNode在重启时，DataNode需要向NameNode发送块的信息，NameNode只有获取到整个文件系统中99.9%（这可以配置）的块满足最小副本才会自动退出安全模式。百分比可以通过dfs.namenode.safemode.threshold-pct来设置，这个值小于0表示无须等待直接退出安全模式；这个值大于1表示永远处于安全模式。

Hadoop safemode主要从4个配置中读取，然后决定是不是安全模式。配置如下：
<ul>
	<li>dfs.namenode.replication.min:这个配置表示块满足的最小的备份数</li>
	<li>dfs.namenode.safemode.threshold-pct:这个配置表示共需有多少百分比的块满足上面备份要求，才能退出安全模式，如果这个百分比大于1，则会永久处于安全模式</li>
	<li>dfs.namenode.safemode.min.datanodes:表示在NameNode退出安全模式之前活着的datanode的数量，当这个数量大于集群datanode数量时，表示永久位于安全模式</li>
	<li>dfs.namenode.safemode.extension:这个配置表示在满足第二个条件时，NameNode还需要处于安全模式的时间，单位是秒</li>
</ul>
Hadoop safemode的主要命令：
<ul>
	<li>进入：hadoop dfsadmin -safemode enter</li>
	<li>获取：hadoop dfsadmin -safemode get</li>
	<li>离开：hadoop dfsadmin -safemode leave</li>
</ul>
<font color="red">实际遇到问题：当NameNode所在节点的资源不够，即使使用命令离开安全模式，也会自动进入安全模式，所以配置Hadoop时要注意这个问题。</font>