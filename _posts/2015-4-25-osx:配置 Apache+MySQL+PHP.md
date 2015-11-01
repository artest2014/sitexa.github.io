---
layout: post
title: Mac OS X 配置 Apache+MySQL+PHP
category: 'osx'
---

###1,OS X 10.10 Yosemite自带apache(2.4)和php(5.5.20):
(1)apache2配置文件: /etc/apache2/httpd.conf

(2)apache2默认网站根目录:/Library/WebServer/Documents

(3)php配置文件:/etc/php.ini

参考文章:<a href="http://getgrav.org/blog/mac-os-x-apache-setup-multiple-php-versions">http://getgrav.org/blog/mac-os-x-apache-setup-multiple-php-versions</a>

###2,php安装路径:
/usr/local/etc/php/5.4/

/usr/local/etc/php/5.5/ 

/usr/local/etc/php/5.6/

###3,安装php扩展mcrypt费劲,参考文章:
<a href="http://www.bubuko.com/infodetail-420234.html">http://www.bubuko.com/infodetail-420234.html</a>

###4,启动/停止/重启apache服务
    sudo apachectl start/stop/restart
        

###注: 
编译生成mcrypt.so时,php源码编译环境(包含mcrypt源码)的版本,一定要与运行环境的php版本一致,否则加载不起来.

(1),OS X 自带php版本号为:5.5.20,如果用5.5.24的源码生成mcrypt.so,是不行的;

(2),使用brew install php56, 安装的是5.6.7版,而不是php.net下载的最新版5.6.8版;

(3),phpize在两个位置的版本不同:/usr/local/bin/phpize, /usr/bin/phpize, 使用的时候注意保持一致.


###5，autoconf
###6，automake
###7，Xcode command line

###8,忘了MySQL是如何安装的.启动方法如下:
+   (1)
You can then start the MySQL server from the System Preferences or via the command line or if restarted it has to be command line
+   (2)
Command line start MySQL: sudo /usr/local/mysql/support-files/mysql.server start

refs:
<a href="http://coolestguidesontheplanet.com/get-apache-mysql-php-phpmyadmin-working-osx-10-10-yosemite/">http://coolestguidesontheplanet.com/get-apache-mysql-php-phpmyadmin-working-osx-10-10-yosemite</a>


