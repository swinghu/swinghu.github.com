---
layout: post
title: Excel使用OFFSET和ROW进行隔行引用
categories: experience
tags: excel
keywords: excel,offset,row,命令,参数
tagline: Supporting tagline
---
今天在整理表格的时候突然遇到了一个小需求，当然用脚本语言或者其他都可以解决，但是感觉excel也可以搞定，于是弄了一下，查了好长时间......终于搞定了。

需求：excel表格自动填充引用时要有一定的间隔。

下面举例子把问题描述一下：

1. 在sheet 1中的A1-A10中有数字1-10，如果在B1-B10中需要和A1-A10同样的数字，可以在B1中填入"=A1"，然后把鼠标放在右下角，变为十字的时候向下拖住，自动填充。
2. 如果有10000行需要这么做该怎么办？可以先在B1中填入"=A1"，然后选中B1-B10000（这里当然要用shift），然后按ctrl+D即可自动填充。
3. 如果在sheet 2的A1-A10中需要同样的数字怎么办？可以在sheet 2的A1填入"=sheet 1!A1"，然后和上面的操作一样。
4. 现在的需求是如果我在sheet 2中的A1-A2中需要的是sheet 1中的A1和A6该怎么办？当然这是个简单的例子，如果是10000行的话，谁还会建议手动搞？查了好长时间，可能是搜索的词不太对，最后找到了一个解决方案，利用ROW()函数和OFFSET()函数。其中ROW()函数可以获得当前的行数，OFFSET()可以以某一个单元格或区域为base，以此为基础的偏移的数据。所以这个需求的解决方案就是在A1中填入：

    =sheet 1!(OFFSET(A1,(ROW()*5 - 4)),,,)

OFFSET函数原型为

    OFFSET(reference,rows,cols,height,width)

+ reference - base单元格或者区域，用A1:B2即可以表示A1A2B1B2这四个单元格
+ rows      - 表示reference左上角单元格为base，上下的偏移量（上为负，下为正）
+ cols      - 表示reference左上角单元格为base，左右的偏移量（右为正，左为负）
+ height    - 表示返回结果的行数（必须为正）
+ width     - 表示返回结果的列数（必须为正）

问题解决！
