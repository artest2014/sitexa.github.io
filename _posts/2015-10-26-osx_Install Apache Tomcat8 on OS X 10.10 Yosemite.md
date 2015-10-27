---
layout: post
title: Installing Tomcat 8 on OS X 10.10 Yosemite
category: 'osx'
---

###1,Download a binary distribution of the core module: apache-tomcat-8.0.28.tar.gz from here. I picked the tar.gz in Binary Distributions / Core section.

###2,Opening/unarchiving the archive will create a folder structure in your Downloads folder: (btw, this free Unarchiver app is perfect for all kinds of compressed files and superior to the built-in Archive Utility.app)
~/Downloads/apache-tomcat-8.0.28

###3,Open to Terminal app to move the unarchived distribution to /usr/local
sudo mkdir -p /usr/local
sudo mv ~/Downloads/apache-tomcat-8.0.28 /usr/local

###4,To make it easy to replace this release with future releases, we are going to create a symbolic link that we are going to use when referring to Tomcat (after removing the old link, you might have from installing a previous version):
sudo rm -f /Library/Tomcat
sudo ln -s /usr/local/apache-tomcat-8.0.28 /Library/Tomcat

###5,Change ownership of the /Library/Tomcat folder hierarchy:
sudo chown -R <your_username> /Library/Tomcat

###6,Make all scripts executable:
sudo chmod +x /Library/Tomcat/bin/*.sh

<img src="/images/tomcat8.png">

###7,Deploy webapp on tomcat8

####(1) ln -s /Users/[myname]/IdeaProjects/sitexa-openapi/target/sitexa-openapi /Library/Tomcat/webapps/sitexa-api
####(2) /Library/Tomcat/bin/startup.sh

<img src="/images/sitexa-api.png">