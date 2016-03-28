---
layout: post
title: 基于xmpp协议的openfire+smack+spark实现即时通信解决方案
category: 'technology'
---

##定义

XMPP（可扩展消息处理现场协议）是基于可扩展标记语言（XML）的协议，它用于即时消息（IM）以及在线现场探测。

XMPP中定义了三个角色，客户端，服务器，网关。通信能够在这三者的任意两个之间双向发生。服务器同时承担了客户端信息记录，连接管理和信息的路由功能。网关承担着与异构即时通信系统的互联互通。基本的网络形式是单客户端通过TCP/IP连接到单服务器，然后在之上传输XML。

[http://xmpp.org/](http://xmpp.org/)

##openfire 

openfire是基于XMPP 协议的即时通信的服务器端的一个实现，如果你要实现一个简单的点对点通信或是简单的群聊，你完全可以使用该服务openfire本身提供的服务而不需要编写一行服务端的代码，非常方便。同时openfire还支持插件的扩展，如果你需要丰富增加服务端的功能，你可以基于openfire进行插件二次开发，或者直接修改openfire的源码实现。
Openfire (formerly Wildfire) is a cross-platform real-time collaboration server based on the XMPP (Jabber) protocol.

##smack

smack是XMPP传输协议的Java实现，提供了一套API接口(类似于JDK中的HttpUrlConnection提供Http连接请求)，它是连接openfire服务、发送通信信息的桥梁。
Easy to use Java XMPP client library.

##spark

spark是基于smack实现的一个XMPP即时通信客户端.
Cross-platform real-time collaboration client optimized for business and organizations.

##sparkweb
Cross-platform web-based collaboration client optimized for business and organizations.

##Openfire的安装

下载地址：http://www.igniterealtime.org/downloads/index.jsp

版本：Openfire 4.0.2 for mac

![image](/images/openfire.jpg)

安装路径：/usr/local/openfire

###解决Openfire无法启动的问题

修改/usr/local/openfire/bin/openfire.sh

在脚本上面加入：export JAVA_HOME=`/usr/libexec/java_home`

修改权限：sudo chmod -R 777 /usr/local/openfire/bin

###解决admin console 无法登录问题

如果是采用外部数据库，原始用户与密码都是admin,打开数据表可以看见，是明文保存。如果设置了密码，则是加密保存。

##Spark安装后，登录时闪退