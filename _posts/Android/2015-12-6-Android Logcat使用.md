---
layout: post
author: Ericson
date: 2015-12-6 11:22
title: LogCat调试Android
category: Android
tag: [android,logcat,development]
---

在Android开发中，LogCat是一个非常重要的调试工具，可以输出很多信息。LogCat输出类型一般有五种：verbose, debug, info, warn, error。这些层次是向下兼容的。我们可以通过进程ID、项目包名、tag标签、text输出文本来限定输出范围。
主要通过定义Filter来实现。如下图所示：
![LogCat Filter](/public/img/android/logcatfilter.jpg)