---
layout: post
title: Nginx学习手记（二）
category: coding
tags:  nginx
keywords: nginx
tagline: Supporting tagline
---

ubuntu下安装Tengine
1、下载：

	http://tengine.taobao.org/download/tengine-1.4.2.tar.gz

2、解压：

代码:
	tar -xvf tengine-1.4.2.tar.gz

3、安装依赖：
代码:
	sudo apt-get install libpcre++-dev libssl-dev zlib1g-dev

注：pcre依赖是rewrite模块必选；ssl是https访问的模块；zlib是启用网页gzip压缩用，必选。

4、编译安装：
代码:

	cd tengine-1.4.2
	./configure --prefix=/usr --conf-path=/etc/nginx/nginx.conf --pid-path=/var/run/nginx.pid --lock-path=/var/lock/nginx.lock --http-client-body-temp-path=/var/tmp/nginx/client --http-proxy-temp-path=/var/tmp/nginx/proxy --http-fastcgi-temp-path=/var/tmp/nginx/fastcgi --http-scgi-temp-path=/var/tmp/nginx/scgi --http-uwsgi-temp-path=/var/tmp/nginx/uwsgi
	make
	sudo make install
	mkdir /var/tmp/nginx

注：没有直接使用默认配置，按照ubuntu下apt-get安装nginx的规范来配置的。
另：如果无法make，则需要安装gcc、make包：
代码:
	sudo apt-get install gcc make

5、配置文件及启动：
	配置文件：/etc/nginx/nginx.conf
	程序启动、停止：/usr/sbin/nginx -s {start/stop/reload}
	版本信息（nginx -v）：Tengine version: Tengine/1.4.2 (nginx/1.2.5)
