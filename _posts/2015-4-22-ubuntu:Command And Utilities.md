---
layout: post
title: Ubuntu 14.04 Command And Utilities
category: 'ubuntu'
---

##1,将应用程序锁定到启动栏[Launcher]
在/usr/share/applications/文件夹中建立jetbrains-idea.desktop:

    [Desktop Entry]
    Version=1.0
    Type=Application
    Name=IntelliJ IDEA
    Icon=/opt/idea-IU/bin/idea.png
    Exec="/opt/idea-IU/bin/idea.sh" %f
    Comment=Develop with pleasure!
    Categories=Development;IDE;
    Terminal=false
    StartupWMClass=jetbrains-idea

###(1),将启动项拖动到启动栏
###(2),或者，启动应用程序后，图标出现在启动栏上，点击鼠标右键菜单->锁定到启动栏




