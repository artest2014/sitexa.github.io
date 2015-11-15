---
layout: post
title: 使用Angular和Nodejs、socket.io搭建聊天室及多人聊天室
category: 'nodejs'
---

#一，利用Node搭建静态服务器

这个是这个项目的底层支撑部分。用来支持静态资源文件像html, css, gif, jpg, png, javascript, json, plain text等等静态资源的访问。这里面是有一个mime类型的文件映射。

mime.js:

    /**
     * mime类型的 map
     * @ author Cheng Liufeng
     * @ date 2014/8/30
     * 当请求静态服务器文件的类型 html, css, gif, jpg, png, javascript, json, plain text, 我们会在此文件进行映射
     */
    exports.types = {
     "css": "text/css",
     "gif": "image/gif",
     "html": "text/html",
     "ico": "image/x-icon",
     "jpeg": "image/jpeg",
     "jpg": "image/jpeg",
     "js": "text/javascript",
     "json": "application/json",
     "pdf": "application/pdf",
     "png": "image/png",
     "svg": "image/svg+xml",
     "swf": "application/x-shockwave-flash",
     "tiff": "image/tiff",
     "txt": "text/plain",
     "wav": "audio/x-wav",
     "wma": "audio/x-ms-wma",
     "wmv": "video/x-ms-wmv",
     "xml": "text/xml"
    };

这里面我先解释一下从输入网址到页面出现的过程。 当用户在浏览器地址栏里面输入一个url的时候。

接下来会发生一系列的过程。首先是DNS解析， 将域名转换成对应的IP地址，之后浏览器与远程Web服务器通过TCP三次握手协商来建立一个TCP/IP连接。该握手包括一个同步报文，开一个同步-应答报文和一个应答报文，这三个报文在浏览器和服务器之间传递。该握手首先由客户端尝试建立起通信，而后服务器应答并接受客户端的请求，最后由客户端发出该请求已经被接受的报文。一旦TCP/IP连接建立，浏览器会通过该连接向远程服务器发送HTTP的GET请求。

远程服务器找到资源并使用HTTP响应返回该资源，值为200的HTTP响应状态表示一个正确的响应。此时，Web服务器提供资源服务，客户端开始下载资源。下载的资源包括了html文件，css文件，javascript文件,image文件。然后开始构建一颗渲染树和一颗DOM树，期间会有css阻塞和js阻塞。所以底层是需要一个静态服务器支撑。这里面我原生构造一个静态服务器，不采用express框架。

事实上每一次资源文件请求的过程是一次次GET请求。下面我解释一下客户端（浏览器端或者采用linux下采用curl方式）的GET请求所对应的服务端处理过程。一次Get请求发送到服务端后，服务端可以根据GET请求对应一个资源文件的路径。知道了这个路径后，我们就可以采用文件读写的方式获取指定路径下的资源，然后返回给客户端。

我们知道Node里面的文件读写的API有readFile和readFileSync，但是更好的方式是采用流的方式去读取文件，采用流的方式的优点是可以采用缓存和gzip压缩。 

OK，那么如何实现缓存呢？通常情况下，客户端第一次去请求的时候，服务端会读取资源文件，返回给客户端。但是第二次再去请求同样的文件时，这个时候还是需要发送一次请求到服务端。服务端会根据Expires, cache-control, If-Modified-Since等Http头信息判断这个资源是否已经缓存过。如果有缓存，服务端则不会再次访问资源文件的实际路径。直接返回缓存的资源。

server.js:

    /**
    * 聊天室服务端
    * 功能：实现了Node版的静态服务器
    * 实现了缓存，gzip压缩等
    * @ author Cheng Liufeng
    * @ date 2014/8/30
    */
    // 设置端口号
    var PORT = 3000;
    // 引入模块
    var http = require('http');
    var url = require('url');
    var fs = require('fs');
    var path = require('path');
    var zlib = require('zlib');
    // 引入文件
    var mime = require('./mime').types;
    var config = require('./config');
    var chatServer = require('./utils/chat_server');
    var server = http.createServer(function (req, res) {
    res.setHeader("Server","Node/V8");
    // 获取文件路径
    var pathName = url.parse(req.url).pathname;
    if(pathName.slice(-1) === "/"){
    pathName = pathName + "index.html"; //默认取当前默认下的index.html
    }
    // 安全处理（当使用Linux 的 curl命令访问时，存在安全隐患）
    var realPath = path.join("client", path.normalize(pathName.replace(/\.\./g, "")));
    // 检查文件路径是否存在
    path.exists(realPath, function(exists) {
    // 当文件不存在时的情况， 输出一个404错误
    if (!exists) {
    res.writeHead(404, "Not Found", {'Content-Type': 'text/plain'});
    res.write("The request url" + pathName +" is not found!");
    res.end();
    } else {   // 当文件存在时的处理逻辑
    fs.stat(realPath, function(err, stat) {
      // 获取文件扩展名
    var ext = path.extname(realPath);
    ext = ext ? ext.slice(1) : "unknown";
    var contentType = mime[ext] || "text/plain";
    // 设置 Content-Type
    res.setHeader("Content-Type", contentType);
    var lastModified = stat.mtime.toUTCString();
    var ifModifiedSince = "If-Modified-Since".toLowerCase();
    res.setHeader("Last-Modified", lastModified);
    if (ext.match(config.Expires.fileMatch)) {
     var expires = new Date();
     expires.setTime(expires.getTime() + config.Expires.maxAge * 1000);
     res.setHeader("Expires", expires.toUTCString());
     res.setHeader("Cache-Control", "max-age=" + config.Expires.maxAge);
    }
    if (req.headers[ifModifiedSince] && lastModified == req.headers[ifModifiedSince]) {
     res.writeHead(304, "Not Modified");
     res.end();
    } else {
    // 使用流的方式去读取文件
    var raw = fs.createReadStream(realPath);
    var acceptEncoding = req.headers['accept-encoding'] || "";
    var matched = ext.match(config.Compress.match);
    if (matched && acceptEncoding.match(/\bgzip\b/)) {
    res.writeHead(200, "Ok", {'Content-Encoding': 'gzip'});
    raw.pipe(zlib.createGzip()).pipe(res);
    } else if (matched && acceptEncoding.match(/\bdeflate\b/)) {
    res.writeHead(200, "Ok", {'Content-Encoding': 'deflate'});
    raw.pipe(zlib.createDeflate()).pipe(res);
    } else {
    res.writeHead(200, "Ok");
    raw.pipe(res);
    }

//下面是普通的读取文件的方式，不推荐

    //   fs.readFile(realPath, "binary", function(err, data) {
    //   if(err) {
    //    // file exists, but have some error while read
    //    res.writeHead(500, {'Content-Type': 'text/plain'});
    //    res.end(err);
    //   } else {
    //    // file exists, can success return
    //    res.writeHead(200, {'Content-Type': contentType});
    //    res.write(data, "binary");
    //    res.end();
    //   }
    //   });
      }
      });
     }
     });
    });
    
//监听3000端口
    
    server.listen(PORT, function() {
     console.log("Server is listening on port " + PORT + "!");
    });
    
// 让socket.io服务器和http服务器共享一个端口
    
    chatServer.listen(server);
    
#二，服务端利用WebSocket构建聊天室服务端
##为什么采用websocket?

我们知道现在主流的聊天室还是采用ajax去实现客户端和服务端的通信。采用的是一种轮询的机制。所谓轮询，就是客户端每隔一段时间就去发送一次请求，询问服务端，看看服务端有没有新的聊天数据，如果有新的数据，就返回给客户端。 

Websocket则完全不同。 websocket是基于长链接。就是客户端和服务端一旦建立链接之后，这个链接就会一直存在。 是一种全双工的通信。 这个时候的机制有点类似发布-订阅模式。 客户端会订阅一些事件，一旦服务端有新的数据出现，会主动推送给客户端。

websocket采用的是ws协议，不是http协议或者https协议。另外采用websocket的另一个好处就是可以减少很多数据流量。文章开头，我已经介绍了传统的一次资源请求过程，需要三次握手协议，而且每次请求头所占空间比较大，这样会很费流量。而Websocket里面的互相沟通的Header是很小的-大概只有 2 Bytes。    

    /**
     * 聊天服务。
     */
    var socketio = require('socket.io');
    var io;
    var guestNumber = 1;   //初始用户名编号
    var nickNames = {};   // 昵称列表
    var namesUsed = [];   //使用过的用户名
    var currentRoom = {};   //当前聊天室
    function assignGuestName(socket, guestNumber, nickNames, namesUsed) {
     var name = 'Guest' + guestNumber;
     nickNames[socket.id] = name;
     socket.emit('nameResult', {
     success: true,
     name: name
     });
     namesUsed.push(name);
     return guestNumber + 1;
    }
    function joinRoom(socket, room) {
     socket.join(room);
     currentRoom[socket.id] = room;
     socket.emit('joinResult', {room: room});
     socket.broadcast.to(room).emit('message', {
     text: nickNames[socket.id] + 'has joined ' + room + '.'
     });
    }
    function handleMessageBroadcasting(socket) {
     socket.on('message', function(message) {
     socket.broadcast.to(message.room).emit('message', {
      text: nickNames[socket.id] + ':' + message.text
     });
     });
    }
    exports.listen = function(server) {
     io = socketio.listen(server);
     io.set('log level', 1);
     // 定义每个用户的连接处理
     io.sockets.on('connection', function(socket) {
     // 分配一个用户名
     guestNumber = assignGuestName(socket, guestNumber, nickNames, namesUsed);
     // 将用户加入聊天室Lobby里
     joinRoom(socket, 'Lobby');
     //处理聊天信息
     handleMessageBroadcasting(socket, nickNames);
     //handleNameChangeAttempts(socket, nickNames, namesUsed);
     //handleRoomJoining(socket);
     //handleClientDisconnection(socket, nickNames, namesUsed);
     });
    };
    
#三，利用Angular搭建聊天室客户端

##为什么使用Angular?

作为一款前端MVC框架，Angular.js无疑是引人注目的。模块化，双向数据绑定，指令系统，依赖注入。而且Angular内置jquerylite，这让熟悉jQuery语法的同学很容易上手。

当然，个人认为， angular在构建一个单页应用和crud项目方面有很大的优势。 我们这个聊天室就是基于SPA（single page application）的目的。

index.html    

    <!DOCTYPE html>
    <html ng-app="chatApp">
    <head>
     <meta name="viewport" content="width=device-width, user-scalable=no">
    </head>
    <body ng-controller="InitCtrl">
     <div ng-view></div>
     <script src="lib/angular.js"></script>
     <script src="lib/angular-route.js"></script>
     <script src="lib/socket.io.js"></script>
     <script src="app.js"></script>
     <script src="controllers/InitCtrl.js"></script>
    </body>
    </html>
    
##怎样构建一个单页应用？单页应用的原理？

先谈谈单页应用的原理。所谓单页，并不是整个页面无刷新。当你审查一下google chrome的console控制台的时候，你会发现，angular内部还是采用了ajax去异步请求资源。所以只是局部刷新。但是这种方式相对于以前的DOM节点的删除和修改已经有很大的进步了。

构建单页应用，我们需要借助于angular-route.js。这个angular子项目可以帮助我们定义路由和对应的逻辑处理控制器。利用它，我们可以实现一个单页应用。
         
app.js:

    /**
     * 客户端（目前只支持浏览器，将来会扩展到移动端）程序入口文件
     * 创建一个模块，并且命名为chatApp
     * 配置路由，实现单页应用(single page application)
     */
     var chatApp = angular.module("chatApp", ['ngRoute']);
     // 路由配置
     chatApp.config(function($routeProvider) {
     $routeProvider.when('/', {
      templateUrl : 'views/init.html',
      controller: 'InitCtrl'
     })
     .when('/init', {
      templateUrl : 'views/init.html',
      controller: 'InitCtrl'
     });
     });
     
客户端聊天界面的代码逻辑如下.
     
InitCtrl.js:     

    /**
     * # InitCtrl
     */
    angular.module('chatApp').controller('InitCtrl', function($scope) {
     var socket = io.connect('http://127.0.0.1:3000');
     socket.on('nameResult', function(result) {
     var message;
     if (result.success) {
      message = 'you are now known as ' + result.name + '.'; 
      console.log('message=', message);
      document.getElementById('guestname').innerHTML = message;
     } else {
      message = result.message;
     }
     });
     socket.on('joinResult', function(result) {
     document.getElementById('room').innerHTML = result.room;
     });
     $scope.sendMessage = function() {
     var message = {
      room: 'Lobby',
      text: document.getElementById('user_input').value
     };
     socket.emit('message', message);
     };
     socket.on('message', function(message) {
     var p = document.createElement('p');
     p.innerHTML = message.text;
     document.getElementById('message').appendChild(p);
     });
    });
    
#基于node.js和socket.io搭建多人聊天室
刚学node.js，想着做点东西练练手。网上的东西多而杂，走了不少弯路，花了一天时间在调代码上。参考网上的一篇文章，重写了部分代码，原来的是基于基于node-websocket-server框架的，我没用框架，单单是socket.io。

#一、基本功能
##1、用户随意输入一个昵称即可登录
##2、登录成功后
-  1) 对正在登录用户来说，罗列所有在线用户列表，罗列最近的历史聊天记录
-  2) 对已登录的用户来说，通知有新用户进入房间，更新在线用户列表

##3、退出登录
-  1)支持直接退出
-  2) 当有用户退出，其他所有在线用户会收到信息，通知又用户退出房间，同时更新在线用户列表

##4、聊天
-   1) 聊天就是广播，把信息广播给所有连接在线的用户

##5、一些出错处理
-   1) 暂时简单处理了系统逻辑错误、网络出错等特殊情况的出错提示

问题：功能不完善，有bug(退出后，新用户重新登录，还是原来的用户) 。抽空完善吧

#二、技术介绍
socket.io(官网：http://socket.io/)是一个跨平台，多种连接方式自动切换，做即时通讯方面的开发很方便，而且能和expressjs提供的传统请求方式很好的结合，即可以在同一个域名，同一个端口提供两种连接方式：request/response, websocket(flashsocket,ajax…)。

这篇文章对socket.io的使用做了详细介绍：<http://www.jb51.net/article/71361.htm>

《用node.js和Websocket做个多人聊天室吧》 <http://www.html5china.com/HTML5features/WebSocket/20111206_3096.html>

#三、注意事项    

##（1）客户端这样引用socket.io.js：

    <script src="/socket.io/socket.io.js"></script>

可能会加载失败（我在这里耗了不少时间）

可以改为：

    <script src="http://ip:port/socket.io/socket.io.js"></script>
    
(对应服务器的ip地址和端口号，比如说localhost和80端口)
    
##（2）实现广播的时候，参考官网的写法，竟然不起作用，如：
    
    var io = require('socket.io').listen(80);
     
    io.sockets.on('connection', function (socket) {
     socket.broadcast.emit('user connected');
     socket.broadcast.json.send({ a: 'message' });
    });
    
后来看了这个：<http://stackoverflow.com/questions/7352164/update-all-clients-using-socket-io>

改为以下才起作用：
    
    io.sockets.emit('users_count', clients);
    
#四、效果图

<img src="/images/chatroom-1.png">
<img src="/images/chatroom-2.png">
<img src="/images/chatroom-3.png">
<img src="/images/chatroom-4.png">

#五、源码下载

Nodejs多人聊天室（[点击此处下载源码](http://xiazai.jb51.net/201508/yuanma/chat.rar)）

ps:

##1、在命令行运行
    
    node main.js

然后在浏览器中打开index.html,如果浏览器（ff、Chrome）不支持，请升级到支持WebSocket的版本.

##2、推荐node.js的IDE WebStorm

以上内容就是本文基于Angular和Nodejs搭建聊天室及多人聊天室的实现，希望大家喜欢。


source: <http://www.jb51.net/article/71356.htm>