---
layout: post
title: Jetty
category: 'other'
---

##1,下载安装jetty
jetty主页：http://www.eclipse.org/jetty
目前的最新稳定版本：jetty-distribution-9.2.10.v20150310.tar.gz
下载解压后拷贝到 /opt/jetty/目录下。

##2,启动jetty

    cd /opt/jetty
    java -jar start.jar

<img src="/images/jetty-home.png"/>

or

    cd /opt/jetty/demo-base
    java -jar ../start.jar

<img src="/images/jetty-demo-base.png"/>


##3,Create a new jetty base

    mkdir /tmp/mybase
    cd /tmp/mybase
    java -jar /opt/jetty/start.jar

##4,Change the jetty port

    java -jar start.jar -jetty.port=8081

##5,Starting https

    java -jar start.jar --add-to-startd=https
    java -jar start.jar




