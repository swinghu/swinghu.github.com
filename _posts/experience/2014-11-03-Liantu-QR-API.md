---
layout: post
title: 使用联图 QR API 生成当前网站的二维码
categories: experience
tags: api 二维码
keywords: 联图,liantu,api,二维码,命令,参数
tagline: Supporting tagline
---
为了不影响大部分用户看二维码，我决定暂时抛弃Google API，使用另一个API——联图二维码API，貌似功能还更强大一些，可以改颜色。

Google QR API：

    http://qr.liantu.com/api.php?text=<data>

    text=<data> - 二维码图形的源数据
	bg=<颜色代码> - 背景颜色
	fg=<颜色代码> - 前景颜色
	gc=<颜色代码> - 渐变颜色
	el=<h|q|m|l> - 纠错等级
	w=<size> - 尺寸大小（像素）
	m=<size> - 外边界（像素）
	logo=<img url> - logo图片地址

例如我的首页的网站就是可以这样获得

	http://qr.liantu.com/api.php?&bg=ffffff&fg=33cccc&gc=cc00cc&w=200&text=http://dongyuxi.github.io

![Simple Blog - 董玉玺的个人博客](http://qr.liantu.com/api.php?&bg=ffffff&fg=33cccc&gc=cc00cc&w=200&text=http://dongyuxi.github.io)

这回貌似应该可以了！那么我的每个页面都加上它吧！
