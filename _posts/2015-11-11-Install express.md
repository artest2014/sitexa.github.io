---
layout: post
title: npm & nodejs & brew and install nodejs module express
category: 'nodejs'
---

##1,首先假定你已经安装了 Node.js，接下来为你的应用创建一个目录，然后进入此目录并将其作为当前工作目录。
    $ mkdir myapp
    $ cd myapp

##2,通过 npm init 命令为你的应用创建一个 package.json 文件。 欲了解 package.json 是如何起作用的，请参考 Specifics of npm’s package.json handling。
    $ npm init

##3,接下来安装 Express 并将其保存到依赖列表中：
    $ npm install express --save

##4,进入 myapp 目录，创建一个名为 app.js 的文件，然后将下列代码复制进去：

    var express = require('express');
    var app = express();

    app.get('/', function (req, res) {
        res.send('Hello World!');
    });
    
    var server = app.listen(3000, function () {
      var host = server.address().address;
      var port = server.address().port;
    
      console.log('Example app listening at http://%s:%s', host, port);
    });

##5,通过如下命令启动此应用：
    $ node app.js

##6,然后在浏览器中打开 http://localhost:3000/ 并查看输出结果。

<img src="/images/nodejs-helloworld.png"/>

##7,通过应用生成器工具 express 可以快速创建一个应用的骨架。
###(1)通过如下命令安装express-generator
    $ npm install express-generator -g
###(2)在当前工作目录下创建一个命名为 myapp1 的应用:
    $ express myapp1
       create : myapp1
       create : myapp1/package.json
       create : myapp1/app.js
       create : myapp1/public
       create : myapp1/public/javascripts
       create : myapp1/public/images
       create : myapp1/routes
       create : myapp1/routes/index.js
       create : myapp1/routes/users.js
       create : myapp1/public/stylesheets
       create : myapp1/public/stylesheets/style.css
       create : myapp1/views
       create : myapp1/views/index.jade
       create : myapp1/views/layout.jade
       create : myapp1/views/error.jade
       create : myapp1/bin
       create : myapp1/bin/www
###(3)然后安装所有依赖包：
    $ cd myapp1 
    $ npm install
###(4)启动这个应用（MacOS 或 Linux 平台）：
    $ DEBUG=myapp1 npm start
###(5)在浏览器中打开 http://localhost:3000/
<img src="/images/nodejs-express-generator.png"/>