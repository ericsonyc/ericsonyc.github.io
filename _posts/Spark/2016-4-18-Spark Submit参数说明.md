---
layout: post
author: 吴超
date: 2016-4-18 10:57
title: Spark Submit参数说明
category: Spark
tag: [spark,parameters]
---

参数|说明
-|-
--master|可以是spark://host:port,mesos://host:port,yarn,yarn-cluster,yarn-client,local
--deploy-mode|client或cluster
--class|主类名称，带包名
--name|Application名称
--jars|Driver依赖的第三方jar
--py-files|python应用程序文件列表“，”逗号隔开
--files|用逗号隔开放置在executor工作目录的文件列表
--properties-file|设置应用程序属性的文件路径，默认是conf/spark-defaults.conf
--driver-memory|设置driver的内存大小
--driver-library-path|driver库的路径
--executor-memory|每个executor内存大小，默认1G
--driver-cores|driver程序使用的cpu个数
--supervise|失败后是否重启driver，仅限于alone模式
--total-executor-cores|executor使用cores的总数
--executor-cores|每个executor使用的cores数目
--queue|提交应用程序到Yarn的队列，默认是default队列，仅限于Yarn模式
--num-executors|启动executor数量，默认是2个，仅限于Yarn模式
--archives|仅限于Yarn模式，表示添加的归档文件
