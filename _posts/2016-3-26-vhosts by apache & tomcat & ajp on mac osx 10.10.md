---
layout: post
title: vhosts by apache & tomcat & ajp on mac osx 10.10
category: 'technology'
---

##  1,/etc/apache2/httpd.conf
   
    Include /private/etc/apache2/extra/httpd-vhosts.conf

##  2,/etc/apache2/extra/httpd-vhosts.conf

    <VirtualHost *:80>
        ServerAdmin webmaster@dev.sitexa.com
        DocumentRoot "/Users/xnpeng/Sites/dev"
        ServerName dev.sitexa.com
        ErrorLog "/private/var/log/apache2/dev.sitexa.com-error_log"
        CustomLog "/private/var/log/apache2/dev.sitexa.com-access_log" common
    </VirtualHost>
    
    <Directory "/Users/xnpeng/Sites/dev">
        Options FollowSymLinks Multiviews
        MultiviewsMatch Any
        AllowOverride None
        Require all granted
    </Directory>
    
    <VirtualHost *:80>
        ServerAdmin webmastart@wiki.sitexa.com
        ServerName wiki.sitexa.com
    
        ProxyRequests On
        ProxyPreserveHost On
    
        <Proxy *>
            Order deny,allow
            Allow from all
        </Proxy>
         
        #jetty server
        ProxyPass / http://localhost:8888/
    
        ErrorLog "/private/var/log/apache2/wiki-error_log"
        CustomLog "/private/var/log/apache2/wiki-access_log" common
    </VirtualHost>
    
    <VirtualHost *:80>
        ServerAdmin webmaster@api.sitexa.com
        ServerName api.sitexa.com
    
        ProxyRequests On
        ProxyPreserveHost On
    
        <Proxy *>
            Order deny,allow
            Allow from all
        </Proxy>
        
        #Tomcat server
        ProxyPass / ajp://localhost:8209/
        ProxyPassReverse / ajp://localhost:8209/
    
        ErrorLog "/private/var/log/apache2/api-error_log"
        CustomLog "/private/var/log/apache2/api-access_log" common
    </VirtualHost>


##  3,/etc/hosts
  
    127.0.0.1       localhost home.sitexa.com dev.sitexa.com wiki.sitexa.com
