---
layout: post
title: IM Framework based on WebSocket - SparkJava and NodeJs
category: 'technology'
---

## Node.js and WebSocket

server:

    var app = require('express')();
    var http = require('http').Server(app);
    var io = require('socket.io')(http);
    
    app.get('/', function(req, res){
    	res.send('<h1>Welcome Realtime Server</h1>');
    });
    
    //在线用户
    var onlineUsers = {};
    //当前在线人数
    var onlineCount = 0;
    
    io.on('connection', function(socket){
    	console.log('a user connected');
    	
    	//监听新用户加入
    	socket.on('login', function(obj){
    		//将新加入用户的唯一标识当作socket的名称，后面退出的时候会用到
    		socket.name = obj.userid;
    		
    		//检查在线列表，如果不在里面就加入
    		if(!onlineUsers.hasOwnProperty(obj.userid)) {
    			onlineUsers[obj.userid] = obj.username;
    			//在线人数+1
    			onlineCount++;
    		}
    		
    		//向所有客户端广播用户加入
    		io.emit('login', {onlineUsers:onlineUsers, onlineCount:onlineCount, user:obj});
    		console.log(obj.username+'加入了聊天室');
    	});
    	
    	//监听用户退出
    	socket.on('disconnect', function(){
    		//将退出的用户从在线列表中删除
    		if(onlineUsers.hasOwnProperty(socket.name)) {
    			//退出用户的信息
    			var obj = {userid:socket.name, username:onlineUsers[socket.name]};
    			
    			//删除
    			delete onlineUsers[socket.name];
    			//在线人数-1
    			onlineCount--;
    			
    			//向所有客户端广播用户退出
    			io.emit('logout', {onlineUsers:onlineUsers, onlineCount:onlineCount, user:obj});
    			console.log(obj.username+'退出了聊天室');
    		}
    	});
    	
    	//监听用户发布聊天内容
    	socket.on('message', function(obj){
    		//向所有客户端广播发布的消息
    		io.emit('message', obj);
    		console.log(obj.username+'说：'+obj.content);
    	});
      
    });
    
    http.listen(3000, function(){
    	console.log('listening on *:3000');
    });

client/html:

    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8">
            <meta name="format-detection" content="telephone=no"/>
            <meta name="format-detection" content="email=no"/>
    <meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=0" name="viewport">
            <title>多人聊天室</title>
            <link rel="stylesheet" type="text/css" href="./style.css" />
            <!--[if lt IE 8]><script src="./json3.min.js"></script><![endif]-->
            <script src="http://realtime.plhwin.com:3000/socket.io/socket.io.js"></script>
        </head>
        <body>
            <div id="loginbox">
                <div style="width:260px;margin:200px auto;">
                    请先输入你在聊天室的昵称
                    <br/>
                    <br/>
                    <input type="text" style="width:180px;" placeholder="请输入用户名" id="username" name="username" />
    				<input type="button" style="width:50px;" value="提交" onclick="CHAT.usernameSubmit();"/>
                </div>
            </div>
            <div id="chatbox" style="display:none;">
                <div style="background:#3d3d3d;height: 28px; width: 100%;font-size:12px;">
                    <div style="line-height: 28px;color:#fff;">
                        <span style="text-align:left;margin-left:10px;">Websocket多人聊天室</span>
                        <span style="float:right; margin-right:10px;"><span id="showusername"></span> | 
    					<a href="javascript:;" onclick="CHAT.logout()" style="color:#fff;">退出</a></span>
                    </div>
                </div>
                <div id="doc">
                    <div id="chat">
                        <div id="message" class="message">
    <div id="onlinecount" style="background:#EFEFF4; font-size:12px; margin-top:10px; margin-left:10px; color:#666;">
    </div>
                        </div>
                        <div class="input-box">
                            <div class="input">
    <input type="text" maxlength="140" placeholder="请输入聊天内容，按Ctrl提交" id="content" name="content">
                            </div>
                            <div class="action">
                                <button type="button" id="mjr_send" onclick="CHAT.submit();">提交</button>
                            </div>
                            
                            <div style="font-size: 12px;float:left;position: absolute;width:100%;top:45px;left:10px">
    						<p>如果这个Demo对你有帮助，<a href="https://github.com/plhwin" target="_blank">请到Github关注我</a></p>
    						<p>教程：<a href="http://www.plhwin.com/2014/05/28/nodejs-socketio/" target="_blank">http://www.plhwin.com/2014/05/28/nodejs-socketio/</a></p>
                            	<p>源码：<a href="https://github.com/plhwin/nodejs-socketio-chat" target="_blank">https://github.com/plhwin/nodejs-socketio-chat</a></p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <script type="text/javascript" src="./client.js"></script>
        </body>
    </html>

client/js:

    (function () {
    	var d = document,
    	w = window,
    	p = parseInt,
    	dd = d.documentElement,
    	db = d.body,
    	dc = d.compatMode == 'CSS1Compat',
    	dx = dc ? dd: db,
    	ec = encodeURIComponent;
    	
    	
    	w.CHAT = {
    		msgObj:d.getElementById("message"),
    		screenheight:w.innerHeight ? w.innerHeight : dx.clientHeight,
    		username:null,
    		userid:null,
    		socket:null,
    		//让浏览器滚动条保持在最低部
    		scrollToBottom:function(){
    			w.scrollTo(0, this.msgObj.clientHeight);
    		},
    		//退出，本例只是一个简单的刷新
    		logout:function(){
    			//this.socket.disconnect();
    			location.reload();
    		},
    		//提交聊天消息内容
    		submit:function(){
    			var content = d.getElementById("content").value;
    			if(content != ''){
    				var obj = {
    					userid: this.userid,
    					username: this.username,
    					content: content
    				};
    				this.socket.emit('message', obj);
    				d.getElementById("content").value = '';
    			}
    			return false;
    		},
    		genUid:function(){
    			return new Date().getTime()+""+Math.floor(Math.random()*899+100);
    		},
    		//更新系统消息，本例中在用户加入、退出的时候调用
    		updateSysMsg:function(o, action){
    			//当前在线用户列表
    			var onlineUsers = o.onlineUsers;
    			//当前在线人数
    			var onlineCount = o.onlineCount;
    			//新加入用户的信息
    			var user = o.user;
    				
    			//更新在线人数
    			var userhtml = '';
    			var separator = '';
    			for(key in onlineUsers) {
    		        if(onlineUsers.hasOwnProperty(key)){
    					userhtml += separator+onlineUsers[key];
    					separator = '、';
    				}
    		    }
    			d.getElementById("onlinecount").innerHTML = '当前共有 '+onlineCount+' 人在线，在线列表：'+userhtml;
    			
    			//添加系统消息
    			var html = '';
    			html += '<div class="msg-system">';
    			html += user.username;
    			html += (action == 'login') ? ' 加入了聊天室' : ' 退出了聊天室';
    			html += '</div>';
    			var section = d.createElement('section');
    			section.className = 'system J-mjrlinkWrap J-cutMsg';
    			section.innerHTML = html;
    			this.msgObj.appendChild(section);	
    			this.scrollToBottom();
    		},
    		//第一个界面用户提交用户名
    		usernameSubmit:function(){
    			var username = d.getElementById("username").value;
    			if(username != ""){
    				d.getElementById("username").value = '';
    				d.getElementById("loginbox").style.display = 'none';
    				d.getElementById("chatbox").style.display = 'block';
    				this.init(username);
    			}
    			return false;
    		},
    		init:function(username){
    			/*
    			客户端根据时间和随机数生成uid,这样使得聊天室用户名称可以重复。
    			实际项目中，如果是需要用户登录，那么直接采用用户的uid来做标识就可以
    			*/
    			this.userid = this.genUid();
    			this.username = username;
    			
    			d.getElementById("showusername").innerHTML = this.username;
    			//this.msgObj.style.minHeight = (this.screenheight - db.clientHeight + this.msgObj.clientHeight) + "px";
    			this.scrollToBottom();
    			
    			//连接websocket后端服务器
    			this.socket = io.connect('ws://realtime.plhwin.com:3000');
    			
    			//告诉服务器端有用户登录
    			this.socket.emit('login', {userid:this.userid, username:this.username});
    			
    			//监听新用户登录
    			this.socket.on('login', function(o){
    				CHAT.updateSysMsg(o, 'login');	
    			});
    			
    			//监听用户退出
    			this.socket.on('logout', function(o){
    				CHAT.updateSysMsg(o, 'logout');
    			});
    			
    			//监听消息发送
    			this.socket.on('message', function(obj){
    				var isme = (obj.userid == CHAT.userid) ? true : false;
    				var contentDiv = '<div>'+obj.content+'</div>';
    				var usernameDiv = '<span>'+obj.username+'</span>';
    				
    				var section = d.createElement('section');
    				if(isme){
    					section.className = 'user';
    					section.innerHTML = contentDiv + usernameDiv;
    				} else {
    					section.className = 'service';
    					section.innerHTML = usernameDiv + contentDiv;
    				}
    				CHAT.msgObj.appendChild(section);
    				CHAT.scrollToBottom();	
    			});
    
    		}
    	};
    	//通过“回车”提交用户名
    	d.getElementById("username").onkeydown = function(e) {
    		e = e || event;
    		if (e.keyCode === 13) {
    			CHAT.usernameSubmit();
    		}
    	};
    	//通过“回车”提交信息
    	d.getElementById("content").onkeydown = function(e) {
    		e = e || event;
    		if (e.keyCode === 13) {
    			CHAT.submit();
    		}
    	};
    })();

Run and browse:

![image](/images/websocket.jpg)


### Video streaming over websockets using JavaScript

What is the fastest way to stream live video using JavaScript? Is WebSockets over TCP a fast enough protocol to stream a video of, say, 30fps?

Yes.. it is, take a look at this [project](http://www.youtube.com/watch?v=WcwnQW_AnC8). Websockets can easily handle HD videostreaming.. However, you should go for Adaptive Streaming. I explain [here](http://stackoverflow.com/questions/4242081/chopping-media-stream-in-html5-websocket-server-for-webbased-chat-video-conferenc) how you could implement it.

Currently we're working on a webbased instant messaging application with chat, filesharing and video/webcam support. With some bits and tricks we got streaming media through websockets (used HTML5 Media Capture to get the stream from our webcams).

You need to build a stream API and a Media Stream Transceiver to control the related media processing and transport.

[Video streaming over websockets using JavaScript](http://stackoverflow.com/questions/4241992/video-streaming-over-websockets-using-javascript)


### How do we split our audio/video data in chunks with Python?
We are currently working on a chat + (file sharing +) video conference application using HTML5 websockets. To make our application more accessible we want to implement Adaptive Streaming, using the following sequence:

-   Raw audio/video data client goes to server
-   Stream is split into 1 second chunks
-   Encode stream into varying bandwidths
-   Client receives manifest file describing available segments
-   Downloads one segment using normal HTTP
-   Bandwidth next segment chosen on performance of previous one
-   Client may select from a number of different alternate streams at a variety of data rates

So.. How do we split our audio/video data in chunks with Python?

[Chopping media stream in HTML5 websocket server for webbased chat/video conference application](http://stackoverflow.com/questions/4242081/chopping-media-stream-in-html5-websocket-server-for-webbased-chat-video-conferenc)


## Spark and WebSocket

Server:

	public class Chat {
    
        static Map<Session, String> userUsernameMap = new HashMap<>();
        static int nextUserNumber = 1; //Assign to username for next connecting user
    
        public static void main(String[] args) {
            staticFileLocation("public"); //index.html is served at localhost:4567 (default port)
            webSocket("/chat", ChatWebSocketHandler.class);
            init();
        }
    
        //Sends a message from one user to all users, along with a list of current usernames
        public static void broadcastMessage(String sender, String message) {
            userUsernameMap.keySet().stream().filter(Session::isOpen).forEach(session -> {
                try {
                    session.getRemote().sendString(String.valueOf(new JSONObject()
                        .put("userMessage", createHtmlMessageFromSender(sender, message))
                        .put("userlist", userUsernameMap.values())
                    ));
                } catch (Exception e) {
                    e.printStackTrace();
                }
            });
        }
    
        //Builds a HTML element with a sender-name, a message, and a timestamp,
        private static String createHtmlMessageFromSender(String sender, String message) {
            return article().with(
                    b(sender + " says:"),
                    p(message),
                    span().withClass("timestamp").withText(new SimpleDateFormat("HH:mm:ss").format(new Date()))
            ).render();
        }
    
    }
    
Handler:
	
	@WebSocket
	public class ChatWebSocketHandler {
	
		private String sender, msg;
	
		@OnWebSocketConnect
		public void onConnect(Session user) throws Exception {
			String username = "User" + Chat.nextUserNumber++;
			Chat.userUsernameMap.put(user, username);
			Chat.broadcastMessage(sender = "Server", msg = (username + " joined the chat"));
		}
	
		@OnWebSocketClose
		public void onClose(Session user, int statusCode, String reason) {
			String username = Chat.userUsernameMap.get(user);
			Chat.userUsernameMap.remove(user);
			Chat.broadcastMessage(sender = "Server", msg = (username + " left the chat"));
		}
	
		@OnWebSocketMessage
		public void onMessage(Session user, String message) {
			Chat.broadcastMessage(sender = Chat.userUsernameMap.get(user), msg = message);
		}
	}

Html:

	<!DOCTYPE html>
    <html>
    <head>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>WebsSockets</title>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <div id="chatControls">
            <input id="message" placeholder="Type your message">
            <button id="send">Send</button>
        </div>
        <ul id="userlist"> <!-- Built by JS --> </ul>
        <div id="chat">    <!-- Built by JS --> </div>
        <script src="websocketDemo.js"></script>
    </body>
    </html>

JS:

	//Establish the WebSocket connection and set up event handlers
    var webSocket = new WebSocket("ws://" + location.hostname + ":" + location.port + "/chat/");
    webSocket.onmessage = function (msg) { updateChat(msg); };
    webSocket.onclose = function () { alert("WebSocket connection closed") };
    
    //Send message if "Send" is clicked
    id("send").addEventListener("click", function () {
        sendMessage(id("message").value);
    });
    
    //Send message if enter is pressed in the input field
    id("message").addEventListener("keypress", function (e) {
        if (e.keyCode === 13) { sendMessage(e.target.value); }
    });
    
    //Send a message if it's not empty, then clear the input field
    function sendMessage(message) {
        if (message !== "") {
            webSocket.send(message);
            id("message").value = "";
        }
    }
    
    //Update the chat-panel, and the list of connected users
    function updateChat(msg) {
        var data = JSON.parse(msg.data);
        insert("chat", data.userMessage);
        id("userlist").innerHTML = "";
        data.userlist.forEach(function (user) {
            insert("userlist", "<li>" + user + "</li>");
        });
    }
    
    //Helper function for inserting HTML as the first child of an element
    function insert(targetId, message) {
        id(targetId).insertAdjacentHTML("afterbegin", message);
    }
    
    //Helper function for selecting element by id
    function id(id) {
        return document.getElementById(id);
    }

Run and browse:

![image](/images/spark-websocket.jpg)

### How to stream audio/video data over websocket using javascript?

Use java-ffmpeg wrapper, or simply use java runtime to execute ffmpeg?

todo...problem to solve
