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

screenshot

![image](/images/wasabi.jpg)

##ktor

Web backend framework for Kotlin

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
    
    