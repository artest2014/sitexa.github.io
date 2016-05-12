---
layout: post
title: Homebrew:the OSX package manager
category: 'osx'
---

Using the brew command you can easily add powerful functionality to your mac.

## 1,install homebrew
    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

## 2,check version:
    $ brew --version

## 3,verification:
    $ brew doctor

## 4,update:
    $ brew update

## 5,link
    $ brew link --overwrite autoconf
    $ brew link --overwrite automake

## 6, install ruby:
    $ rvm install ruby --head
