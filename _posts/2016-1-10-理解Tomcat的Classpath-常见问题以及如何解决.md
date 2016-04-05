---
layout: post
title: 理解Tomcat的Classpath-常见问题以及如何解决
category: 'technology'
---

##问题：我的应用程序依赖一个外部的仓库，我不能引用它。

让Tomcat知道一个外部的仓库，在catalina.properties文件的shared loader位置，使用正确的语法，声明这个仓库。语法基于你要配置的文件或仓库的类型：
-   1、增加一个文件夹作为类仓库，使用“path/to/foldername”
-   2、增加一个文件夹下的所有jar文件作为类仓库，使用"path/to/foldername/*.jar"
-   3、增加单个jar文件作为类仓库，使用"file://path/to/foldername/jarname.jar"
-   4、调用环境变量，使用${}格式，例如${VARIABLE_NAME}
-   5、声明多个资源，用逗号分隔开
-   6、所有的路径相对于CATALINA_BASE或CATALINA_HOME，或者是绝对路径

##问题：我想多个应用程序共享一个jar文件，这个jar文件在Tomcat里面。

除了一些常见的第三方库（比如JDBC drivers），最好不要在$CATALINA_HOME/lib目录下包含额外的库，即使这样在一些情况下是可行的。应该重新创建比如/shared/lib和/shared/classes目录，然后在catalina.properties配置shared.loader属性：
"shared/classes,shared/lib/*.jar"