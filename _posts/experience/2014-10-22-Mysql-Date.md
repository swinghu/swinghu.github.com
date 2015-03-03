---
layout: post
title: Mysql中使用date_add和adddate操作date
categories: experience
tags: mysql date
keywords: mysql,date,命令,参数
tagline: Supporting tagline
---
今天在写mysql查询日期比当前天多一天的sql，本来以为是很简单的用curdate() + 1就可以了，结果试了半天发现不行，才发现了一个完全没听过的方法：

    date_add(date, interval expr type)
    adddate(date, interval expr type)
    adddate(date, days)

其中前两种是同义语句，这样就可以完成此需求了。

    select date_add('2014-10-22', interval 1 day); --> '2014-10-23'
    select adddate('2014-10-22', 1); --> '2014-10-23'

那么自然可以想到如果减少的话会有对应的如下方法：

    date_sub(date, interval expr type)
    subdate(date, interval expr type)
    subdate(date, days)

问题解决！
