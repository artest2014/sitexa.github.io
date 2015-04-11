---
layout: post
title: 配置ubuntu的telnet服务
category: 'other'
---

##1.安装xinetd 以及telnetd

    $ sudo apt-get install xinetd telnetd

##2.配置文件

###A. /etc/inetd.conf

    $ cat /etc/inetd.conf （如果存在就不需要了）

显示telnet stream tcp nowait telnetd /usr/sbin/tcpd /usr/sbin/in.telnetd

###B. 修改/etc/xinetd.conf

    $ sudo gedit /etc/xinetd.conf

    # Simple configuration file for xinetd
    # Some defaults, and include /etc/xinetd.d/

    defaults
    {

        # Please note that you need a log_type line to be able to use log_on_success
        # and log_on_failure. The default is the following :
        # log_type = SYSLOG daemon info(插入红色部分）
        instances = 60
        log_type = SYSLOG authpriv
        log_on_success = HOST PID
        log_on_failure = HOST
        cps = 25 30
    }

    includedir /etc/xinetd.d

###C.修改/etc/xinetd.d/telnet

    $ sudo gedit /etc/xinetd.d/telnet

并加入以下内容：

    # default: on
    # description: The telnet server serves telnet sessions; it uses \
    # unencrypted username/password pairs for authentication.
    service telnet
    {
        disable = no
        flags = REUSE
        socket_type = stream
        wait = no
        user = root
        server = /usr/sbin/in.telnetd
        log_on_failure += USERID
    }

##3. 重启机器或重启网络服务##

    $ sudo /etc/init.d/xinetd restart

##4. 使用TELNET客户端远程登录；ifconfig -a显示本机地址##