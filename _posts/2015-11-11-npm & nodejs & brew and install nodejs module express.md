---
layout: post
title: npm & nodejs & brew and install nodejs module express
category: 'nodejs'
---

##1,安装nodejs
    $ brew install nodejs

    /usr/local/etc/bash_completion.d
    /usr/local/Cellar/node/5.0.0:2824 files,36M

##2,下载npm
    $ git clone --recursive git://github.com/isaacs/npm.git

##3, 进到npm目录下，运行下面的命令安装：
    $ node cli.js install npm -gf  

    /usr/local/Cellar/node/5.0.0/bin/npm -> /usr/local/Cellar/node/5.0.0/lib/node_modules/npm/bin/npm-cli.js
    /usr/local/Cellar/node/5.0.0/lib
    └── npm@3.3.12

##4，安装express模块：
    $ npm install express -gf

    /usr/local/lib
    └─┬ express@4.13.3
    ├─┬ accepts@1.2.13
    │ ├─┬ mime-types@2.1.7
    │ │ └── mime-db@1.19.0
    │ └── negotiator@0.5.3
    ├── array-flatten@1.1.1
    ├── content-disposition@0.5.0
    ├── content-type@1.0.1
    ├── cookie@0.1.3
    ├── cookie-signature@1.0.6
    ├─┬ debug@2.2.0
    │ └── ms@0.7.1
    ├── depd@1.0.1
    ├── escape-html@1.0.2
    ├── etag@1.7.0
    ├─┬ finalhandler@0.4.0
    │ └── unpipe@1.0.0
    ├── fresh@0.3.0
    ├── merge-descriptors@1.0.0
    ├── methods@1.1.1
    ├─┬ on-finished@2.3.0
    │ └── ee-first@1.1.1
    ├── parseurl@1.3.0
    ├── path-to-regexp@0.1.7
    ├─┬ proxy-addr@1.0.8
    │ ├── forwarded@0.1.0
    │ └── ipaddr.js@1.0.1
    ├── qs@4.0.0
    ├── range-parser@1.0.3
    ├─┬ send@0.13.0
    │ ├── destroy@1.0.3
    │ ├─┬ http-errors@1.3.1
    │ │ └── inherits@2.0.1
    │ ├── mime@1.3.4
    │ └── statuses@1.2.1
    ├── serve-static@1.10.0
    ├─┬ type-is@1.6.9
    │ └── media-typer@0.3.0
    ├── utils-merge@1.0.0
    └── vary@1.0.1

