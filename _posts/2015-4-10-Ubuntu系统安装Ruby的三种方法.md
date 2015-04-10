---
layout: post
title: Ubuntu系统安装Ruby的三种方法
---

Ruby是一个开源的动态编程语言，它有优美的语法，可用于构建可伸缩的Web应用程序。ruby gems可以很好地增强Ruby开发者的开发效率。
要在Ubuntu系统上安装Ruby，有几种方法，每种方法都只需几步就能搞定。

##方法一：使用apt-get安装##

可以直接使用两个命令完成Ruby的安装。

    $ sudo apt-get update
    $ sudo apt-get install ruby
或者

    $ sudo apt-get install ruby2.0

##方法二：使用brightbox ppa仓库安装##

    $ sudo apt-get install python-software-properties
    $ sudo apt-add-repository ppa:brightbox/ruby-ng
    $ sudo apt-get update
    $ sudo apt-get install ruby2.1 ruby2.1-dev

##方法三：使用RVM安装##

RVM是Ruby的版本管理器工具。
###1、安装RVM###
    $ sudo apt-get curl
    $ curl -L https://get.rvm.io | bash -s stable
    $ source ~/.rvm/scripts/rvm
###2、安装RVM的环境依赖###
    $ rvm requirements
###3、安装Ruby###
    $ rvm install ruby
如果想在Ubuntu上安装多个Ruby版本，那么可以使用下面的命令来指定使用rvm作为默认的Ruby版本管理。

    $ rvm use ruby --default
检查当前成功安装的Ruby版本

    $ ruby -v
安装gems

    $ gem list
    $ gem install [gem-name]
比如gem-name可以写sass
如果要从本地安装gems，命令如下：

    $ gem install --local [path of gem file]
可以使用命令更新已安装的gems，命令如下：

    $ gem update --system
或者

    $ gem update

##注：##

1，为了解决安装Jekyll过程中存在的问题，尝试过三种方法，最终是哪种方法起作用了，其实也不清楚。印象中，apt-get官方创库中，ruby的版本是1.9.3，不能满足jekyll的ruby版本（>=2.0)的要求，反复尝试三种安装方式安装ruby，都不能解决 “mkmf.rb can't find header files for ruby at /usr/lib/ruby/include/ruby.h”。也尝试了多种网上介绍的方法。

最终起作用的是：

    $ sudo apt-get install ruby2.2-dev

2, 上述方法完成后，安装jekyll, 顺利完成。

    $ bundle install
