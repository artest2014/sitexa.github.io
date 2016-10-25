---
layout: post
title: WebTorrent技术及其应用
category: 'technology'
---

## 1, 什么是WebTorrent?

WebTorrent是第一个在浏览器里使用的比特流(torrent)客户端。WebTorrent连接网端用户，形成分布式的、去中心化的网络，供用户之间传输文件。

##  2,神奇之处

设想YouTube这样的视频网站，设想用户帮助其存放视频内容。当这个网站支持WebTorrent技术时，访问的用户越多，下载的速度就越快。
浏览器与浏览器之间的通讯，消除了中间角色，让用户根据各自的需要相互通讯。没有服务器／客户端，只是点对点的对等网络。

##  3,WebTorrent有哪些使用案例？

最激动人心的使用案例是端点内容分发机制。当用户参与内容的存储和分发服务时，非盈利项目如维基(wiki)和网络档案(internet archive)可以减少带宽和主机成本。广泛使用的内容，通过浏览器到浏览器的服务机制，使成本更低，速度更快。使用较少的内容，则依赖原始服务器通过http提供服务。
还有激动人心的商业应用，比如内容加速(CDN)和应用(app)分发。

##  4,谁在使用WebTorrent？

-   WebTorrent Desktop - Open source streaming torrent client. For Mac, Windows, and Linux. (source code)
-   Instant.io – Streaming file transfer over WebTorrent (source code)
-   GitTorrent - Decentralized GitHub using BitTorrent and Bitcoin (source code)
-   PeerCloud - Serverless websites via WebTorrent (source code)
-   File.pizza - Free peer-to-peer file transfers in your browser (source code)
-   Webtorrentapp – Platform for launching web apps from torrents
-   Fastcast – Gallery site with some videos (source code)
-   Colored Coins - Open protocol for creating digital assets on the Blockchain (source code)
-   Tokenly Pockets - Digital token issuance with WebTorrent-based metadata (source code)
-   βTorrent - Fully-featured browser WebTorrent client (source code)
-   Seedshot - Peer to peer screenshot sharing from your browser (source code)
-   PeerWeb - Fetch and render a static website from a torrent
-   Niagara - Video player webtorrent with subtitles (zipped .srt(s))
-   Vique - Video player queue to share videos
-   YouShark - Web music player for WebTorrent (source code)
-   Peerify - Instant Web-seeded torrents for your files
-   Instant-Share - File sharing over WebTorrent
-   P2PDrop - Securely share files between peers (source code)
-   Twister - Decentralized microblogging service, using WebTorrent for media attachments (source code)
-   PeerTube - Prototype of a decentralized video streaming platform in the web browser (source code)
-   Cinematrix - Stream your favorite free content
-   webtorrent-cljs - Clojurescript wrapper for WebTorrent
-   Squidlink - Transfer files from A to B without the Cloud (source code)
-   Web2web - Server-less & domain-less websites updatable via torrents and bitcoin blockchain (source code)
-   Magnet Player - Stream video torrents directly from your browser (source code)
-   PeerFast - First P2P Internet Speed Test (source code)
-   TorrentMedia - Fully-featured desktop WebTorrent client
-   Your app here – Send a pull request with your URL!

##  5,WebTorrent是如何工作的？

WebTorrent协议与BitTorrent协议相似，只是WebTorrent使用WebRTC替代BitTorrent的TCP/UDP作为传输协议。
为了支持WebRTC的连接模型，我们对追踪协议进行了改变。因此，一个基于浏览器的WebTorrent客户端，或者叫“Web-peer”，只通跟支持WebTorrent/WebRTC协议的客户端连接。一但端点与端点(peer to peer)之间建立了连接，传输协议就跟通常的BitTorrent的传输协议完全一样。这样做的目的是为了让流行的BitTorrent客户端可以添加对WebTorrent的支持。

##  6,如何开始工作？

```
var client = new WebTorrent()

var torrentId = 'magnet:?xt=urn:btih:6a9759bffd5c0af65319979fb7832189f4f3c35d&dn=sintel.mp4&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&tr=wss%3A%2F%2Ftracker.webtorrent.io&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel-1024-surround.mp4'

client.add(torrentId, function (torrent) {
  var file = torrent.files[0]
  file.appendTo('body') // append the file to the DOM
})
```

##  7,什么是WebRTC?

WebRTC( Real-time-communication) 是W3C标，用来支持浏览器到浏览器之间的应用，如语音呼叫、视频聊天、文件传输，而不需要安装插件。WebRTC的RTCDataChannel API允许浏览器之间建立数据通道，传输数据。这与WebSocket和XMLHttpRequest不一样。

##  8,WebTorrent客户端能与BitTorrent客户端连接吗？

-   WebTorrent Desktop - Open source streaming torrent client. For Mac, Windows, and Linux.
-   Vuze - Powerful, full-featured torrent client
-   Playback - Open source JavaScript video player (super cool!)
-   webtorrent-hybrid - Node.js package (command line and API)
-   Instant.io - Simple WebTorrent client in a website
-   βTorrent - Fully-featured browser WebTorrent client (source code)
-   TorrentMedia - Desktop WebTorrent client
-   More coming soon – Send a PR to add your client to the list!

#   WebTorrent的应用领域

##  1,内容加速(CDN)

##  2,应用分发

##  3,销售单页

web2web 是p2p技术在网页上的实现方式。p2p(peer to peer)是一种点对点的传输技术，用在比特流上，就是广为人知的BitTorrent下载。BitTorrent由两部分配合完成大文件的传输：BitTorrent客户端，BitTorrent种子seed。种子通常可用客户端工具生成，保存为种子文件，以.torrent结尾。BitTorrent客户端打开种子文件，获得源媒体的服务地址，开始下载；同时，BitTorrent客户端必须提供上传服务，即把自己下载下来的媒体共享给别的用户以供下载。源媒体可以放在网络服务器上，也可以放在客户电脑上，但要求同时有一份完整的备份就能供客户使用。只要下载和分享的客户越来越多，下载的速度就会越来越快。web2web则是以网页浏览器为客户端，用它打开一个特制的网页，该网页用来打开种子网页，而种子网页中含有源媒体的种子。

web2web分享的步聚：

-   一，制作单网页。必须是单独一个网页。
-   二，生成种子。使用webtorrent创建网页的种子，并提供种源(seeding)。（此时可以保存为torrent文件分享出去。）
-   三，将上述种子的hash码提交到web2web-gateway上。
-   四，创建index.html文件，将上述网页的种子的hash码放进页面中，并把index.html放在网站上，供用户访问。
