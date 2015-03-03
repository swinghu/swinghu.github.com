---
layout: post
title: Ubuntu 12.04使用Goagent和Chrome插件SwitchySharp翻墙 
categories: linux
tags: linux ubuntu goagent chrome
keywords: linux,ubuntu,goagent,chrome,命令,参数
tagline: Supporting tagline
---
首先你要保证你要已经有Google App Engine帐号，申请很简单，传送门猫理会goagent教程

    [http://maolihui.com/goagent-detail.html](http://maolihui.com/goagent-detail.html)

这里已经有了Windows上安装的方法，下面简单介绍下在Ubuntu上安装的方法。基本步骤极为类似：
访问

    [https://code.google.com/p/goagent/](https://code.google.com/p/goagent/)

下载goagent的zip文件，执行命令

    unzip google_appengine.zip
    sudo mv goagent-goagent-0f39b33/ /opt/goagent

进入/opt/goagent/server文件夹，执行命令

    sudo python uploader.py

然后俺步骤输入appid，gmail和password，等待安装成功。

进入/opt/goagent/local文件夹，执行命令，修改proxy.ini文件中[gae]下面的appid为你申请的appid，保存后退出。

执行命令

    sudo ./goagent-gtk.py

提示要安装python-vte，执行命令

    sudo apt-get install python-vte

之后即可启动脚本。注意！在/opt/goagent/local文件夹下面有SwitchySharp.crx和SwitchyOptions.bak，这个就是Chrome的插件和配置文件。

在Chrome中安装后导入配置即可。

安装完成！
