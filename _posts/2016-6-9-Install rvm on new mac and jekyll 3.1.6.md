---
layout: post
title: install rvm on new mac -- to install jekyll 3.1.6
category: 'technology'
---

Jekyll is a simple, blog-aware, static site generator. It takes a template directory containing raw text files in various formats, runs it through a converter (like Markdown) and our Liquid renderer, and spits out a complete, ready-to-publish static website suitable for serving with your favorite web server. Jekyll also happens to be the engine behind GitHub Pages, which means you can use Jekyll to host your project’s page, blog, or website from GitHub’s servers for free.

##  1,xcode-select --install

##  2,\curl -sSL https://get.rvm.io | bash -s stable

##  3,rvm requirements

##  4,brew doctor

##  5,rvm install 2.1.2

![image](/images/rvm-jekyll.png)

##  6,gem install jekyll

```
pengxunans-MacBook-Pro:~ open$ gem install jekyll
Fetching: colorator-0.1.gem (100%)
Successfully installed colorator-0.1
Fetching: sass-3.4.22.gem (100%)
Successfully installed sass-3.4.22
Fetching: jekyll-sass-converter-1.4.0.gem (100%)
Successfully installed jekyll-sass-converter-1.4.0
Fetching: rb-fsevent-0.9.7.gem (100%)
Successfully installed rb-fsevent-0.9.7
Fetching: ffi-1.9.10.gem (100%)
Building native extensions. This could take a while...
Successfully installed ffi-1.9.10
Fetching: rb-inotify-0.9.7.gem (100%)
Successfully installed rb-inotify-0.9.7
Fetching: listen-3.0.8.gem (100%)
Successfully installed listen-3.0.8
Fetching: jekyll-watch-1.4.0.gem (100%)
Successfully installed jekyll-watch-1.4.0
Fetching: kramdown-1.11.1.gem (100%)
Successfully installed kramdown-1.11.1
Fetching: liquid-3.0.6.gem (100%)Fetching: liquid-3.0.6.gem
Successfully installed liquid-3.0.6
Fetching: mercenary-0.3.6.gem (100%)
Successfully installed mercenary-0.3.6
Fetching: rouge-1.11.0.gem (100%)
Successfully installed rouge-1.11.0
Fetching: safe_yaml-1.0.4.gem (100%)
Successfully installed safe_yaml-1.0.4
Fetching: jekyll-3.1.6.gem (100%)
Successfully installed jekyll-3.1.6
Parsing documentation for colorator-0.1
Installing ri documentation for colorator-0.1
Parsing documentation for sass-3.4.22
Installing ri documentation for sass-3.4.22
Parsing documentation for jekyll-sass-converter-1.4.0
Installing ri documentation for jekyll-sass-converter-1.4.0
Parsing documentation for rb-fsevent-0.9.7
Installing ri documentation for rb-fsevent-0.9.7
Parsing documentation for ffi-1.9.10
Installing ri documentation for ffi-1.9.10
Parsing documentation for rb-inotify-0.9.7
Installing ri documentation for rb-inotify-0.9.7
Parsing documentation for listen-3.0.8
Installing ri documentation for listen-3.0.8
Parsing documentation for jekyll-watch-1.4.0
Installing ri documentation for jekyll-watch-1.4.0
Parsing documentation for kramdown-1.11.1
Installing ri documentation for kramdown-1.11.1
Parsing documentation for liquid-3.0.6
Installing ri documentation for liquid-3.0.6
Parsing documentation for mercenary-0.3.6
Installing ri documentation for mercenary-0.3.6
Parsing documentation for rouge-1.11.0
Installing ri documentation for rouge-1.11.0
Parsing documentation for safe_yaml-1.0.4
Installing ri documentation for safe_yaml-1.0.4
Parsing documentation for jekyll-3.1.6
Installing ri documentation for jekyll-3.1.6
Done installing documentation for colorator, sass, jekyll-sass-converter, rb-fsevent, ffi, rb-inotify, listen, jekyll-watch, kramdown, liquid, mercenary, rouge, safe_yaml, jekyll after 14 seconds
14 gems installed
```
