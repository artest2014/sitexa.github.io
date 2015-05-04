---
layout: post
title: OpenCart V2.0
category: 'ecommerce'
---

##1,Install OpenCart
###(1) Upload all of the files and folders to your server from the "Upload" folder, place them in a folder under your web root;
###(2) Rename config-dist.php to config.php and admin/config-dist.php to admin/config.php;
###(3) For Linux/Unix make sure the following folders and files are writeable.

    		chmod 0755 or 0777 system/cache/
    		chmod 0755 or 0777 system/logs/
    		chmod 0755 or 0777 system/download/
    		chmod 0755 or 0777 system/upload/
    		chmod 0755 or 0777 image/
    		chmod 0755 or 0777 image/cache/
    		chmod 0755 or 0777 image/catalog/
    		chmod 0755 or 0777 config.php
    		chmod 0755 or 0777 admin/config.php

    		If 0755 does not work try 0777.
###(4) Make sure you have installed a MySQL Database which has a user assigned to it
DO NOT USE YOUR ROOT USERNAME AND ROOT PASSWORD
###(5) Visit the store homepage e.g. http://www.example.com or http://www.example.com/opencart/
###(6) You should be taken to the installer page. Follow the on screen instructions.
###(7) After successful install, delete the /install/ directory from ftp.

##2,Basic Security Practices

<img src="/images/opencart.png">