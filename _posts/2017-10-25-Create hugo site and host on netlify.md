---
layout: post
title: Create hugo site and host on netlify
category: 'technology'
---

##  What is Hugo?

Hugo is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again.

##  Step 1: Install Hugo (MacOS)

    $ brew install hugo
    
Verify hugo version

    $ hugo version
    Hugo Static Site Generator v0.30.2 darwin/amd64 BuildDate: 2017-10-24T10:19:09+08:00
    
##  Step 2: Create a New Site

    $ hugo new site xex
    
    Congratulations! Your new Hugo site is created in /Users/open/WebstormProjects/xex.
    
    Just a few more steps and you're ready to go:
    
    1. Download a theme into the same-named folder.
       Choose a theme from https://themes.gohugo.io/, or
       create your own with the "hugo new theme <THEMENAME>" command.
    2. Perhaps you want to add some content. You can add single files
       with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
    3. Start the built-in live server via "hugo server".
    
    Visit https://gohugo.io/ for quickstart guide and full documentation.
    
##  Add version control (github)

    $ cd xex
    $ git init
    
##  Add theme: ananke

    $ git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
    $ echo 'theme = "ananke"' >> config.toml
    
##  Add some content

    $ cp -av themes/ananke/exampleSite/* .
    
    
##  Start hugo server with draft enabled

    $ hugo server -D
    
    Started building sites ...
    
    Built site for language en:
    1 of 1 draft rendered
    0 future content
    0 expired content
    1 regular pages created
    8 other pages created
    0 non-page files copied
    1 paginator pages created
    0 categories created
    0 tags created
    total in 12 ms
    Watching for changes in /Users/open/WebstormProjects/xex/{data,content,layouts,static,themes}
    Serving pages from memory
    Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
    Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
    Press Ctrl+C to stop
    
##  Customize the Theme

### Site Configuration

Open up config.toml in a text editor:

-   title = "南方 - 湘鄂西"
-   description = "神秘的湘鄂西，我的家乡."

Open up content/_index.md:

-   title: "湘鄂西：我的家乡"
-   description: "神秘，充满魅力，日本鬼子未曾进入过的地方！"

Open up content/contact.md:

-   title: "联系我"
-   formspree: action="https://formspree.io/xnpeng@163.com"

Make a new folder:

-   news
-   create _index.md

##  Upload to github

Use Webstorm to share project to github

##  Host on netlify

### Open app.netlify.com

-   create a new site
-   from github, select a repository: xex
-   select branch: master
-   build command: hugo
-   publish diretory: public
-   advanced setting, variable, HUGO_VERSION:0.30.2

### deploy

-   site name: xex.netlify.com
-   custom domain name: www.sitexa.cn

### Trigger deploy when github repository updated


Visit: [http://www.sitexa.cn](http://www.sitexa.cn)