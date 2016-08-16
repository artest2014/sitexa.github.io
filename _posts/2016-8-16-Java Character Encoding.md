---
layout: post
title: Java Character Set Encoding
category: 'technology'
---

-   Java stores characters internally as UTF-16
-   Java uses translation tables to map between external encodings and UTF-16.
    -   Map from external encoding to UTF-16 on input.
    -   Map from UTF-16 to external encoding on output.
-   These translations can be lossy.

-   Java only deals with UTF-16 internally.
-   Inbound characters are converted to UTF-16.
-   Outbound characters are converted from UTF-16 to whatever the output encoding is.
-   Unless you're reading and writing UTF-16, all character I/O requires conversion to and from Java's canonical UTF-16 encoding.
-   This is a perfectly reasonable and sound approach.

##  Scenario

-   Web-based user interface in windows
-   backed by Java servlets in linux
-   Support for Oracle or SQL Server in linux

![image](/images/encoding.jpg)



