---
title: hugo
weight: 5
pre: "<b>5. </b>"
disableToc: true
---



Hello and welcome!

This manual will show you how to run Hugo and Hugo server directly from your command line!

With the help of Hugo, you can create, view, enhance inputs for Knowledge Base and contribute to PIRL community.

## Overview

This guide will explain how to download, setup and run Hugo and Hugo server:

{{< imagesurlsheaders "cloud/Hugo.JPG" >}}

## Prerequisites

For granting the success of this operation, you will need these requirements:

* Internet connection
* [Download the latest version of Hugo binary (> 0.25) for your OS](https://github.com/gohugoio/hugo/releases)
* Download the pirl-docs repo from here: [Pirl-docs](https://git.pirl.io/community/pirl-docs)
* Web browser of your choice and some power of will

## Action!


### 1) Mac iOS
If you are a Mac user, install Hugo with one strong, simple command.

Command:
brew install Hugo

Follow installation guide [here](https://gohugo.io/getting-started/quick-start/)

### 2) Windows OS
* If you use a Windows as I do, simply download the latest version of [Hugo](https://github.com/gohugoio/hugo/releases) for Windows if you haven't done it yet.
* Download most recent [PIRL docs file depository](https://git.pirl.io/community/pirl-docs) if you haven't done it yet. Unzip/extract both of these two folders.
* Then go into Hugo folder and copy everything you will find there.
* Jump to the PIRL docs folder and past all HUGO files there and rewrite files if needed.
* Then press Search button nearby the main Windows start button in the left down corner (standardly it is here :) )
* Write a CMD in the empty line and hit Enter.
* Now you can see exactly what do I need to write every time I want to run Hugo server and write down some KnowledgeBase (KB) article.
* First I need to locate my destination (in this case it is a Disk D and some further folders). Then I will make my move toward the Hugo folder.

Commands in CMD:

1. C:\Users\YourComputername>D:
2. D:\>cd D:\PIRL\HUGO\pirl-docs-master\pirl-docs-master
3. Dir
4. Hugo.exe
5. Hugo.exe server
6. For shutting Hugo server down press: CTRL+C




### 3) Linux OS

I have created two possible ways for downloading, installation and running Hugo. Pick what is more OK for you.

#### a) Install by the package manager

* Type in the command:
```
wget https://github.com/gohugoio/hugo/releases/download/v0.49/hugo_0.49_Linux-32bit.deb
sudo dpkg -i hugo_0.49_Linux-32bit.deb
```

#### b) Alternatively, install via a shell script and then use another script for comfortable repetitive Startup
* Installation script

```
#!/bin/bash
wget https://github.com/gohugoio/hugo/releases/download/v0.49/hugo_0.49_Linux-64bit.tar.gz
tar -xf hugo_0.49_Linux-64bit.tar.gz
```
* Repetitive Startup script

```
#!/bin/bash
cd /path/to/hugo
ls -la
./hugo.sh &
pkill -f hugo.sh
./hugo.sh server
```
********************
## Checking in the Web browser

When your installation is done, start the web browser and type in:
```
http://localhost:1313
```
* Welcome in the Matrix. Now you can edit or create new index files and help us create another studding knowledge based articles.
* For doing so, pick the text editor which suit your needs. I prefer [Atom](https://atom.io/). Its really easy to use and its also GitLab user friendly.

--------

Author:
_[Mickey Maler](https://twitter.com/MickeyMaler)_

Contributor(s):
