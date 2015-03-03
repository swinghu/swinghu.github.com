---
layout: post
title: Ubuntu 12.04安装Eclipse 
categories: linux
tags: linux ubuntu eclipse
keywords: linux,ubuntu,eclipse,命令,参数
tagline: Supporting tagline
---
在Ubuntu 12.04上安装Eclipse，有2中方法：

方法1：直接使用apt-get自动安装
+ 优点：操作简单
+ 缺点：版本限制
执行命令

    sudo apt-get install eclipse-platform

这样就可以直接使用Eclipse，不过Eclipse和JDK的版本和源有关系。

方法2：从官网下载安装包手动安装
+ 优点：安装简洁，版本目录可控
+ 缺点：相对麻烦
Step 1：访问Eclipse官网下载需要的版本，例如eclipse-jee-luna-SR1-linux-gtk.tar.gz。

Step 2：执行命令

    sudo tar -zxf eclipse-jee-luna-SR1-linux-gtk.tar.gz -C /opt

将压缩文件解压到/opt目录下面，现在到/opt/eclipse/eclipse就可以直接运行Eclipse了。

Step 3：将Eclipse添加到程序启动图标。在/usr/share/applications目录下面创建eclipse.desktop，输入如下内容。

    [Desktop Entry]
    Comment=Java IDE
    Name=Eclipse
    Exec=/opt/eclipse/eclipse
    Encoding=UTF-8
    Terminal=false
    Type=Application
    Categories=Application;Development;
    Icon=/opt/eclipse/icon.xpm

现在就可以看到Eclipse在应用程序里面了。

安装结束！
