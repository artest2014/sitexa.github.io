---
layout: post
title: Docker -- birthday-3-Architecture
category: 'technology'
---

## 1,description

-   A Python webapp: which lets you vote between several options
-   A Redis queue: which collects new votes
-   A Java worker: which consumes votes and stores them in A Postgres database: backed by a Docker volume
-   A Node.js webapp: which shows the results of the voting in real time

## 2,big picture

![image](/images/bd3-architecture.png)


ref:

[https://github.com/docker/docker-birthday-3](https://github.com/docker/docker-birthday-3)