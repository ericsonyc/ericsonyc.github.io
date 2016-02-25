---
layout: post
author: Ericson
date: 2015-11-15
title: Hadoop源码编译
category: Hadoop
tag: [hadoop,source code]
---

下面针对Hadoop2.5.0源码讲解源码编译：

编译前的需求：
<ul>
	<li>Linux System</li>
	<li>JDK 1.6+</li>
	<li>Maven 3.0+</li>
	<li>Findbugs 1.3.9(if running findbugs)</li>
	<li>ProtocolBuffer 2.5.0</li>
	<li>CMake 2.6+(if compiling native code)</li>
	<li>Zlib devel(if compiling native code)</li>
	<li>openssl devel(if compiling native hadoop-pipes)</li>
	<li>Internet connection for first build(to fetch all Maven and Hadoop dependencies)</li>
</ul>

Maven main modules:
hadoop(Main Hadoop Project)
<ul>
	<li>hadoop-project(Parent POM for all Hadoop Maven modules)</li>
	<li>hadoop-project-dist(Parent POM for modules that generate distributions)</li>
	<li>hadoop-annotations(Generates the Hadoop doclet used to generated the Javadocs)</li>
	<li>hadoop-assembiles(Maven assembiles used by the different modules)</li>
	<li>hadoop-common-project(Hadoop Common)</li>
	<li>hadoop-hdfs-project(Hadoop HDFS)</li>
	<li>hadoop-mapreduce-project(Hadoop MapReduce)</li>
	<li>hadoop-tools(Hadoop tools like Streaming, Distcp, etc)</li>
	<li>hadoop-dist(Hadoop distributions assembler)</li>
</ul>

Maven build goals:<br/>
* Clean: mvn clean<br/>
* Compile: mvn compile [-Pnative]<br/>
* Run tests: mvn test [-Pnative]<br/>
* Create JAR: mvn package<br/>
* Run findbugs: mvn compile fingbugs:findbugs<br/>
* Run checkstyle: mvn compile checkstyle:checkstyle<br/>
* Install JAR in M2 cache: mvn install<br/>
* Deploy JAR to Maven repo: mvn deploy<br/>
* Run clover: mvn test -Pclover [-DcloverLicenseLocation=${use.name}/.clover.license]<br/>
* Run Rat: mvn apache-rat:check<br/>
* Build javadocs: mvn javadoc:javadoc<br/>
* Build distribution: mvn package [-Pdist][-Pdocs][-Psrc][-Pnative][-Dtar]<br/>
* Change Hadoop version: mvn version:set -DnewVersion=NEWVERSION

Build options:<br/>
* Use -Pnative to compile/bundle native code<br/>
* Use -Pdocs to generate & bundle the documentation in the distribution(using -Pdist)<br/>
* Use -Psrc to create a project source TAR.GZ<br/>
* Use -Dtar to create a TAR with the distribution(using -Pdist)