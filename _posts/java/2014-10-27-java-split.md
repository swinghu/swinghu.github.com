---
layout: post
title: Java使用split("|")分割竖线的问题
categories: Java
tags: java split
keywords: mysql,date,命令,参数
tagline: Supporting tagline
---
今天在处理log文件的时候偶然发现了一个小问题，就是java的String调用split的时候直接用竖线分割会导致每个字母都分开，举个具体的例子：

	String line = "abcd|efgh";
	String[] arr = line.split("|");
	//arr的结果就是"a", "b", "c", "d", "|", "e", "f", "g", "h"

当然不是我们想要的。

其实仔细看一下split的函数原型

	split(String regex);
	split(String regex, int limit);

就神马都懂了，里面是正则表达式，所以如果想使用竖线，那么就要转义，而java中又要二次转义，即

	String[] arr = line.split("\\|");

就可以进行正确的操作了。

这里稍微解释下竖线的意思，就是或的意思嘛，因为2侧神马都木有，所以把每个字母都分开了。
