---
layout: post
title: Actor Messaging platform
category: 'technology'
---

Actor is a platform for instant messaging. Actor provides features like:

-   large group chats;
-   unlimited history storage;
-   file sharing;
-   phone and email authentication via one time passwords;
-   easy integration with external services.

Actor has one of the best IM apps for Android, iOS, and Web. Thay are designed to handle poor connectivity, support offline messaging experience and file storage in applications, and also build contact lists automatically!

The Actor Platform is good for improving enterprise communications, building a message-oriented startup, or building a country-wide national messenger.

##Architecture

![image](/images/ActorArchitecture.png)

Actor is not based on any other protocol or other messaging solutions. Platform uses in-house developed protocol for communication between server and clients that was inspired by Telegram's MTProto and named after it: MTProto v2.

Actor Server is implemented on top of high-performance framework Akka Streams and use PostgreSQL for persistence. In actor's roadmap there is milestone for removing dependency from PostgreSQL and allow use any SQL database.

Actor Applications implementation is separated to the core and UI. Core is a single codebase written on Java 6 without reflection and then converted to various languages. UI is implemented with native tools for each platform. 

