---
layout: post
title: briefcase - topics of these days
category: 'technology'
---

##Umbraco CMS

Umbraco is a free open source Content Management System built on the ASP.NET platform.

For the first time on the Microsoft platform, there is a free user and developer friendly CMS that makes it quick and easy to create websites - or a breeze to build complex web applications. Umbraco has award-winning integration capabilities and supports ASP.NET MVC or Web Forms, including User and Custom Controls, out of the box. It's a developer's dream and your users will love it too.

Used by more than 350,000 active websites including http://daviscup.com, http://heinz.com, http://peugeot.com, http://www.hersheys.com/ and The Official ASP.NET and IIS.NET website from Microsoft (http://asp.net / http://iis.net), you can be sure that the technology is proven, stable and scales.

##Wasabi HTTP framework

An HTTP Framework built with Kotlin for the JVM.

Wasabi combines the conciseness and expressiveness of Kotlin, the power of Netty and the simplicity of Express.js (and other Sinatra-inspired web frameworks) to provide an easy to use HTTP framework.

###start script

build.gradle

    buildscript {
        project.ext.kotlin_version = '1.0.1-2'
        project.ext.wasabi_version = '0.1.182'
        repositories {
            mavenCentral()
            maven {
                url "https://oss.sonatype.org/content/repositories/snapshots"
            }
        }
        dependencies {
            classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        }
    }
    
    apply plugin: 'kotlin'
    apply plugin: 'application'
    
    mainClassName = 'com.sitexa.app.ServerKt'
    
    repositories {
        mavenCentral()
        maven {
            url "https://oss.sonatype.org/content/repositories/snapshots"
        }
        maven {
            url "http://repository.jetbrains.com/all"
        }
    }
    
    dependencies {
        compile "org.wasabi:wasabi:$wasabi_version"
        compile "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
    }
    
    sourceSets {
        src {
            main {
                kotlin
            }
        }
        test {
            main {
                kotlin
            }
        }
        main.java.srcDirs += 'src/main/kotlin'
    }
    
    task wrapper(type: Wrapper) {
        gradleVersion = '2.8'
    }

Each Wasabi application is composed of a single AppServer on which you define route handlers. A route handler can respond to any of the HTTP verbs: GET, POST, PUT, DELETE, OPTIONS, HEAD. A normal application consists of a section where you define a series of parameters for the application, followed by your handlers (i.e. your routing table).

screenshot

![image](/images/wasabi.jpg)

##ktor

Web backend framework for Kotlin.

    <repository>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
        <id>bintray-kotlin-ktor</id>
        <name>bintray</name>
        <url>http://dl.bintray.com/kotlin/ktor</url>
    </repository>
    
    <dependency>
        <groupId>org.jetbrains</groupId>
        <artifactId>ktor-core</artifactId>
        <version>LATEST</version>
    </dependency>
    
##netty

>Netty is an asynchronous event-driven network application framework 
>for rapid development of maintainable high performance protocol servers & clients.

Netty is a NIO client server framework which enables quick and easy development of network applications such as protocol servers and clients. It greatly simplifies and streamlines network programming such as TCP and UDP socket server.

'Quick and easy' doesn't mean that a resulting application will suffer from a maintainability or a performance issue. Netty has been designed carefully with the experiences earned from the implementation of a lot of protocols such as FTP, SMTP, HTTP, and various binary and text-based legacy protocols. As a result, Netty has succeeded to find a way to achieve ease of development, performance, stability, and flexibility without a compromise.

  discard-client          discard-server
  echo-client             echo-server
  factorial-client        factorial-server
  file-server             http-cors-server
  http-file-server        http-helloworld-server
  http-snoop-client       http-snoop-server
  http-upload-client      http-upload-server
  websocket-client        websocket-server
  http2-client            http2-server
  http2-tiles             http2-multiplex-server
  spdy-client             spdy-server
  worldclock-client       worldclock-server
  objectecho-client       objectecho-server
  quote-client            quote-server
  securechat-client       securechat-server
  telnet-client           telnet-server
  proxy-server            socksproxy-server
  memcache-binary-client  stomp-client
  uptime-client           sctpecho-client
  sctpecho-server         localecho
  
reference

[http://netty.io/](http://netty.io/)

[https://github.com/netty/netty](https://github.com/netty/netty)

##web.py

web.py is a web framework for Python that is as simple as it is powerful. web.py is in the public domain; you can use it for whatever purpose with absolutely no restrictions.

web.py was originally published while Aaron Swartz worked at reddit.com, where the site used it as it grew to become one of the top 1000 sites according to Alexa and served millions of daily page views. "It's the anti-framework framework. web.py doesn't get in your way," explained founder Steve Huffman.

###The web.py Philosophy

The web.py slogan is: "Think about the ideal way to write a web app. Write the code to make it happen."

This is literally how I developed web.py. I wrote a web application in Python just imagining how I wanted the API to be. It started with import web, of course, and then had a place to define URLs, simple functions for GET and POST, a thing to deal with input variables and so on. Once the code looked right to me, I did whatever it took to make it execute without changing the application code -- the result was web.py.

In response to someone complaining about web.py having "yet another template language", I wrote a bit more about my philosophy:

-   You don't have to use it -- each part of web.py is completely separate from the others. But you're right, it is "yet another template language". And I'm not going to apologize for it.

-   The goal of web.py is to build the ideal way to make web apps. If reinventing old things with only small differences were necessary to achieve this goal, I would defend reinventing them. The difference between the ideal way and the almost-ideal way is, as Mark Twain suggested, the difference between the lightning and the lightning bug.

-   But these aren't just small differences. Instead of exposing Python objects, web.py allows you to build HTTP responses. Instead of trying to make the database look like an object, web.py makes the database easier to use. And instead of coming up with yet another way to write HTML, the web.py template system tries to bring Python into HTML. Not many other people are really trying to do that.

-   You can disagree that these ways are better and say why. But simply criticizing them for being different is a waste of time. Yes, they are different. That's the whole point.

