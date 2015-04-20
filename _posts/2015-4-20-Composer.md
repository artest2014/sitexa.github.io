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