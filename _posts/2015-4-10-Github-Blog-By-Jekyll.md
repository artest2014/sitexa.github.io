---
layout: post
title: GitHub Repository website and Project blog on github.io
---

使用github托管用户博客(Repository)和项目博客(Project)

1, 用户博客，repository website for you or your organization.
    每个github帐号只有一个，且为：sitexa.github.io形式的项目blog。其地址为：http://sitexa.github.io

2, 项目博客，project blog.
    每个项目只有一个，且为：sitexa.github.io/sns。其地址为：http://sitexa.github.io/sns

3, 域名映射
   （1）在sitexa.github.io的master目录下建立CNAME, 内容为：www.sitexa.org
   （2）在sitexa.org的域名服务器上建立别名：www.sitexa.org CNAME sitexa.github.io
访问:http://sitexa.github.io --> http://www.sitexa.org

4，使用Ruby编程语言；

5，使用Jekyll建站工具。