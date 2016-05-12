---
layout: page
title: Bazel,a blaze for software build!
category: 'life'
---

## What is Bazel
Correct, reproducible, fast builds for everyone

Build software of any size, quickly and reliably, just as engineers do at Google.

Bazel is Google's own build tool, now publicly available in Beta. Bazel has built-in support for building both client and server software, including client applications for both Android and iOS platforms. It also provides an extensible framework that you can use to develop your own build rules.

## Installing Bazel

### System Requirements

####  Supported platforms:

Ubuntu Linux (Utopic 14.10 and Trusty 14.04 LTS)
Mac OS X

####  Java:

Java JDK 8 or later (JDK 7 is still supported but deprecated).

####  Install dependencies

Ubuntu

1. Install JDK 8

Ubuntu Trusty (14.04 LTS). OpenJDK 8 is not available on Trusty. To install Oracle JDK 8:

    $ sudo add-apt-repository ppa:webupd8team/java
    $ sudo apt-get update
    $ sudo apt-get install oracle-java8-installer

Ubuntu Utopic (14.10). To install OpenJDK 8:

    $ sudo apt-get install openjdk-8-jdk openjdk-8-source

2. Install required packages

Type command:

    $ sudo apt-get install pkg-config zip g++ zlib1g-dev unzip

Mac OS X

1. Install JDK 8

JDK 8 can be downloaded from Oracle's JDK Page. Look for "Mac OS X x64" under "Java SE Development Kit". This will download a DMG image with an install wizard.

2. Install XCode command line tools

Xcode can be downloaded from the Apple Developer Site, which will redirect to the App Store.

For objc_* and ios_* rule support, you must have Xcode 6.1 or later with iOS SDK 8.1 installed on your system.

Once XCode is installed you can trigger the license signature with the following command:

    $ sudo gcc --version

### Download Bazel

Download the Bazel installer for your operating system.

####  Run the installer

Run the installer:

    $ chmod +x install-version-os.sh
    $ ./install-version-os.sh --user

The --user flag installs Bazel to the $HOME/bin directory on your system and sets the .bazelrc path to $HOME/.bazelrc. Use the --help command to see additional installation options.

####  Set up your environment

If you ran the Bazel installer with the --user flag as above, the Bazel executable is installed in your $HOME/bin directory. It's a good idea to add this directory to your default paths, as follows:

    $ export PATH="$PATH:$HOME/bin"

You can also add this command to your ~/.bashrc file.


## Getting start

###  project root and workspace

<img src="/images/my-project-1.png"/>

###  java source file

<img src="/images/my-project-2.png"/>

###  BUILD file

<img src="/images/my-project-3.png"/>

###  run build

<img src="/images/my-project-4.png"/>

###  run

<img src="/images/my-project-5.png"/>


<h1> Bazel Tutorial </h1>

<a href="http://bazel.io/docs/tutorial/index.html">Tutorial</a>