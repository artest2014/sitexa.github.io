---
layout: post
title: Redis build & install & play
category: 'technology'
---

Redis is an open source (BSD licensed), in-memory data structure store, used as database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries. Redis has built-in replication, Lua scripting, LRU eviction, transactions and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster.

## 1,make;
## 2,make test;
## 3,run redis:

    $ cd src
    $ ./redis-server

![image](/images/redis-1.png)

## 4, install into /usr/local/bin

    $ make install

## 5, start redis

    $ redis-server

## 6, connect to redis-server

    $ redis-cli

![image](/images/redis-cli-2.png)

## 7, uninstall redis

    $ cd /usr/local/bin
    $ ls -l redis*
    $ sudo rm redis*

![image](/images/redis-3.png)


## 8, brew install redis

![image](/images/redis-4.png)

## 9, how to start redis-server?

    $which redis-server
    /Users/xnpeng/anaconda/bin/redis-server
    $redis-server /usr/local/etc/redis.conf

![image](/images/redis-5.png)

    $ /usr/local/bin/redis-server /usr/local/etc/redis.conf

![image](/images/redis-6.png)
