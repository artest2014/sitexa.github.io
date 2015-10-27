---
layout: post
title: Installing Sonatype Nexus on OS X 10.10 Yosemite
category: 'osx'
---

##1.下载

我们可以在nexus的官网上找到它的相关介绍，下载地址是http://www.sonatype.org/nexus/go，在这里可以找到最新的版本，如果需要以前的版本，在这里也可以找到下载地址。Nexus提供了两种安装方式，一种是内嵌Jetty的bundle，只要你有JRE就能直接运行。第二种方式是WAR，你只须简单的将其发布到web容器中即可使用。为了方便就直接选用bundle版本。我下载的是：nexus-2.11.4-01-bundle.tar.gz。

##2.安装

在指定的目录解压下载的文件。解压后会看到两个文件夹，分别是nexus-2.11.4-01和sonatype-work，前者包含了nexus的运行环境和应用程序，后者包含了你自己的配置和存储构件的地方。nexus-2.11.4-01/conf/nexus.properties中可以修改端口信息以及工作区的路径。

###2.1 command and directory:

     sudo mkdir -p /usr/local

     sudo mv ~/Downloads/nexus-2.11.4-01-bundle /usr/local

     sudo rm -f /Library/Nexus

     sudo ln -s /usr/local/nexus-2.11.4-01-bundle /Library/Nexus

     sudo chown -R /Library/Tomcat

##3.启动nexus

进入nexus-2.11.4-01/bin/jsw/目录，然后根据OS的版本进入相应的目录，在linux下，运行./nexus start即启动了服务，直接运行./nexus会看到提示信息，运行./nexus console 可以以控制台方式启动nexus，方便我们观察启动时的相关工作。neuxs默认监听端口是8081，此时在浏览器中运行访问http://127.0.0.1:8081/nexus或者http://localhost:8081/nexus或者http://0.0.0.0:8081/nexus应该可以看到nexus的界面。

##4配置nexus

新搭建的neuxs环境只是一个空的仓库，需要手动和远程中心库进行同步，nexus默认是关闭远程索引下载，最重要的一件事情就是开启远程索引下载。登陆nexus系统，默认用户名密码为admin/admin123。 点击左边Views/Repositories菜单下面的Repositories，找到右边仓库列表中的三个仓库Apache Snapshots，Codehaus Snapshots和Central，然后再没有仓库的Configuration下把Download Remote Indexes修改为true。然后在这三个仓库上分别右键，选择Repari Index，这样Nexus就会去下载远程的索引文件。

新建公司的内部仓库，步骤为Repositories –> Add –> Hosted Repository，在页面的下半部分输入框中填入Repository ID和Repository Name即可，比如分别填入myrepo和 my repository，另外把Deployment Policy设置为Allow Redeploy，点击save就创建完成了。

修改nexus仓库组

Nexus中仓库组的概念是Maven没有的，在Maven看来，不管你是hosted也好，proxy也好，或者group也好，对我都是一样的，我只管根据groupId，artifactId，version等信息向你要构件。为了方便Maven的配置，Nexus能够将多个仓库，hosted或者proxy合并成一个group，这样，Maven只需要依赖于一个group，便能使用所有该group包含的仓库的内容。

neuxs-2.11.4中默认自带了一个名为“Public Repositories”组，点击该组可以对他保护的仓库进行调整，把刚才建立的公司内部仓库加入其中，这样就不需要再在maven中明确指定内部仓库的地址了。同时创建一个Group ID为public-snapshots、Group Name为Public Snapshots Repositories的组，把Apache Snapshots、Codehaus Snapshots和Snapshots加入其中。

到这里neuxs的安装配置就完成了，下面介绍如何在mavne中使用自己的私服。

maven安装好默认是没有配置仓库信息，此时mavne都默认去远程的中心仓库下载所依赖的构件。既然使用了私服，就需要明确告诉maven去哪里下载构件，可以在三个地方进行配置，分别是是mavne的安装目录下的conf下的settings.xml文件，这个全局配置，再一个是在userprofile/.m2目录下的settings.xml,如果不存在该文件，可以复制conf下settings.xml，这个是针对当前用户的，还有一个是在pom.xml中指定，其只对该项目有效，三个文件的优先级是pom.xml大于.m2,.m2大于conf下。

settings.xml的配置如下：

在profiles段增加一个profile

      <profile>
           <id>nexus</id>
           <repositories>
             <repository>
                 <id>nexus</id>
                 <name>local private nexus</name>
                 <url>http://192.168.1.68:8081/nexus/content/groups/public</url>
                 <releases><enabled>true</enabled></releases>
                 <snapshots><enabled>false</enabled></snapshots>
             </repository>
             <repository>
                 <id>nexus-snapshots</id>
                 <name>local private nexus</name>
                 <url>http://192.168.1.68:8081/nexus/content/groups/public-snapshots</url>
                 <releases><enabled>false</enabled></releases>
                 <snapshots><enabled>true</enabled></snapshots>
             </repository>
           </repositories>
           <pluginRepositories>
             <pluginRepository>
                 <id>nexus</id>
                 <name>local private nexus</name>
                 <url>http://192.168.1.68:8081/nexus/content/groups/public</url>
                 <releases><enabled>true</enabled></releases>
                 <snapshots><enabled>false</enabled></snapshots>
             </pluginRepository>
             <pluginRepository>
                 <id>nexus-snapshots</id>
                 <name>local private nexus</name>
                 <url>http://192.168.1.68:8081/nexus/content/groups/public-snapshots</url>
                 <releases><enabled>false</enabled></releases>
                 <snapshots><enabled>true</enabled></snapshots>
             </pluginRepository>
            </pluginRepositories>
         </profile>
         

上述的id，name可以根据自己的喜好来定义，保证多个repository的id不重复即可，主要是url的配置，可以在nexus的repositories列表中找到对应的url，就是repositories的Repository Path，刚才我们已经在neuxs中定于了仓库组，这里就取对应组的Repository Path信息即可。

另外，仓库是两种主要构件的家。第一种构件被用作其它构件的依赖。这是中央仓库中存储的大部分构件类型。另外一种构件类型是插件。如果不配置pluginRepositories，那么执行maven动作时，还是会看到去远程中心库下载需要的插件构件，所以这里一定要加上这个。

在settings.xml中配置了profile还不行，需要激活它，在activeProfiles段，增加如下配置:

    <span style="font-size: 14px;"><activeProfile>nexus</activeProfile><br></span>
    
此处activeProfile中的内容就上面定义profile的id。

pom.xml配置如下：

    <repositories>
            <repository>
                <id>nexus</id>
                <name>local private nexus</name>
                <url>http://192.168.1.68:8081/nexus/content/groups/public</url>
                <releases>
                    <enabled>true</enabled>
                </releases>
                <snapshots>
                    <enabled>false</enabled>
                </snapshots>
            </repository>
            <repository>
                <id>nexus-snapshots</id>
                <name>local private nexus</name>
                <url>http://192.168.1.68:8081/nexus/content/groups/public-snapshots</url>
                <releases>
                    <enabled>false</enabled>
                </releases>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
        </repositories>
        <pluginRepositories>
            <pluginRepository>
                <id>nexus</id>
                <name>local private nexus</name>
                <url>http://192.168.1.68:8081/nexus/content/groups/public</url>
                <releases>
                    <enabled>true</enabled>
                </releases>
                <snapshots>
                    <enabled>false</enabled>
                </snapshots>
            </pluginRepository>
            <pluginRepository>
                <id>nexus-snapshots</id>
                <name>local private nexus</name>
                <url>http://192.168.1.68:8081/nexus/content/groups/public-snapshots</url>
                <releases>
                    <enabled>false</enabled>
                </releases>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </pluginRepository>
        </pluginRepositories>
        
其中id，name都无所谓，关键不能把url弄错。

有了上述配置，当在项目执行maven操作时，如果本地库中没有依赖的构件，maven会去私服下载，如果私服也没有，私服会去远程中心库下载，同时会在私服的本地缓存，这样如果第二个人再要用到这个构件，私服就直接提供下载。
    
<img src="/images/nexus.png">