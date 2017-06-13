---
layout: post
title: Hugo blog by GO
category: 'technology'
---

Hugo works flexibly with many formats, and is ideal for blogs, docs, portfolios and much more. Hugo’s speed fosters creativity—it makes building a website fun again.
 
Hugo is designed for speed and performance. Great care has been taken to ensure build time with Hugo is as short as possible. We’re talking milliseconds to build your entire site—for most setups!
 
Hugo is designed to work the way you do. Organize your content however you want with any URL structure. Group your content using your own indexes and categories. Define your own metadata in any format: YAML, TOML or JSON. Best of all, Hugo handles all these variations with virtually no configuration. Hugo just works.

## Install git



##  Install GO

### download go tools from golang.org

-   go1.8.3.darwin-amd64.tar.gz for MacOS
-   go1.8.3.linux-amd64.tar.gz for linux

```
tar -C /usr/local -xzf go1.8.3.darwin-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
export GOROOT=$HOME/go1.X
export PATH=$PATH:$GOROOT/bin
export GOPATH=$HOME/go
```

## Install govendor

```$ go get github.com/kardianos/govendor```


##  Install Hugo 

-   hugo_0.22_macOS-64bit.tar.gz for macOS
-   hugo_0.22_Linux-64bit.tar.gz for linux

## Install denpendencies 

```govendor get github.com/spf13/hugo```

## Using hugo

```
hugo build
hugo install
hugo server
```
