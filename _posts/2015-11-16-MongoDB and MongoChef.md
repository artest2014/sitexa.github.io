---
layout: post
title: MongoDB and MongoChef
category: 'technology'
---

MongoDB allows Foursquare to seamlessly process and store all user check-ins, with hundreds of thousands of input/output operations per second.

##1,brew install mongodb;
==> Downloading https://homebrew.bintray.com/bottles/mongodb-3.0.7.yosemite.bott
######################################################################## 100.0%
==> Pouring mongodb-3.0.7.yosemite.bottle.tar.gz
==> Caveats
To have launchd start mongodb at login:
ln -sfv /usr/local/opt/mongodb/*.plist ~/Library/LaunchAgents
Then to load mongodb now:
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
Or, if you don't want/need launchctl, you can just run:
mongod --config /usr/local/etc/mongod.conf
==> Summary
/usr/local/Cellar/mongodb/3.0.7: 17 files, 158M

##2, start mongodb:
$ mongod --config /usr/local/etc/mongod.conf
通过：http://localhost:27017查看是否已经成功启动。

##3,connect to mongodb:
$ mongo
MongoDB shell version: 3.0.7
connecting to: test
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
http://docs.mongodb.org/
Questions? Try the support group
http://groups.google.com/group/mongodb-user
Server has startup warnings:
2015-11-15T09:49:48.338+0800 I CONTROL [initandlisten]
2015-11-15T09:49:48.338+0800 I CONTROL [initandlisten] ** WARNING: soft rlimits too low. Number of files is 256, should be at least 1000


##4,MongoChef - MongoDB GUI tool

MongoChef is the best tool to work with MongoDB. Whether you’re exploring your local database or working with shards and replica sets, MongoChef is here to help and make working with MongoDB a pleasure.

![image](/images/mongodb1.png)