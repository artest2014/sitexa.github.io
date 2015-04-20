---
layout: post
title: Composer
category: 'laravel'
---

##1,Install Composer
$ curl -sS https://getcomposer.org/installer | php
$ sudo mv composer.phar /usr/local/bin/composer

##2, Use Composer
###(1)pacagist.org
Packagist is the main Composer repository. It aggregates all sorts of PHP packages that are installable with Composer.
Browse packages or submit your own.
###(2)create a project dir
    mkdir tmp
    cd tmp
###(3)download phpspec
    composer require phpspec/phpspec
<img src="/images/require-phpspec.png">

##3,Create a project[learning-laravel-5] branch[dev-develop] based on laravel framework
    composer create-project laravel/laravel learning-laravel-5 dev-develop
run project:

    php -S localhost:8888 -t public

<img src="/images/wrong-with-run.png">

##3,Install laravel
###(1)Via laravel installer
    composer global require "laravel/installer=~1.1"

这个命令将laravel安装到~/.composer目录中。将目录添加到路径中：

    export PATH=$HOME/.composer/vendor/bin
使用laravel创建新项目：

    laravel new blog
    cd blog
    php -S localhost:8888 -t public
open http://localhost:8888 with browser,shows: Laravel 5

###(2)Via Composer Create Project
    composer create-project laravel/laravel myblog --prefer-dist
    cd myblog
    php -S localhost:8888 -t public

###(3)Scaffolding
Laravel ships with scaffolding for user registration and authentication. If y would like to remove this scaffolding, use the fresh Artisan command:

    php artisan fresh


