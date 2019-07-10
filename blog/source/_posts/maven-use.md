---
title: maven使用说明
date: 2016-05-18 22:35:34
tags:
- java
categories: java
---

参考教程：

http://www.yiibai.com/maven/maven_environment_setup.html

下载maven:

http://maven.apache.org/download.cgi

创建web项目：

mvn archetype:generate -DgroupId=com.starsmark -DartifactId=AAway -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false

编译-打包：mvn clean package

eclipse:

cd AAway

mvn eclipse:eclipse -Dwtpversion=2.0
