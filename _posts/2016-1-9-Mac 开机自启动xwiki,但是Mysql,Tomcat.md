---
layout: post
title: Mac OSX 开机自启动xwiki,但是Mysql,Tomcat
category: 'technology'
---

在OSX上配置开机自启动xwiki，笔记本环境是OSX10.10,xwiki+mysql+tomcat, 台式机环境是OSX10.11,xwiki+h2+jetty。根据如下方式配置，台式机成功，笔记本失败。

## auto start xwiki----under jetty
     $ vi /Library/LuanchDaemons/start_xwiki.plist
     <?xml version="1.0" encoding="UTF-8"?>
     <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
     <plist version="1.0">
         <dict>
             <key>UserName</key>
             <string>root</string>
             <key>KeepAlive</key>
             <false/>
             <key>Label</key>
             <string>xwiki</string>
             <key>RunAtLoad</key>
             <true/>
             <key>ProgramArguments</key>
             <array>
                <string>/Applications/XWikiEnterprise74/start_xwiki.sh</string>
             </array>
             </dict>
     </plist>


## Mysql开机自启动
    
    $sudo vi /Library/LaunchDaemons/com.mysql.mysql.plist
    
    <!--?xml version="1.0" encoding="UTF-8"?-->
    <plist version="1.0">
      <dict>
        <key>KeepAlive</key>
        <true />
        <key>Label</key>
        <string>com.mysql.mysqld</string>
        <key>ProgramArguments</key>
        <array>
          <string>/usr/local/mysql/bin/mysqld_safe</string>
          <string>--user=mysql</string>
        </array>        
      </dict>
    </plist>


$sudo chown root:wheel /Library/LaunchDaemons/com.mysql.mysql.plist
$sudo chmod 644 /Library/LaunchDaemons/com.mysql.mysql.plist

start it:
$sudo launchctl load -w /Library/LaunchDaemons/com.mysql.mysql.plist

stop it :
$sudo launchctl unload -w 
/Library/LaunchDaemons/com.mysql.mysql.plist


##auto start tomcat

    $sudo vi /Library/LaunchDaemons/org.apache.tomcat.plist
    <!--?xml version="1.0" encoding="UTF-8"?-->
    <plist version="1.0">
        <dict>
            <key>Disabled</key>
            <false />
            <key>Label</key>
            <string>org.apache.tomcat</string>
            <key>ProgramArguments</key>
            <array>
                <string>/usr/local/apache-tomcat-8.0.30/bin/catalina.sh</string>
                <string>run</string>
                </array>
            <key>RunAtLoad</key>
            <true/>
        </dict>
    </plist>
     
