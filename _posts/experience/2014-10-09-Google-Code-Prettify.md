---
layout: post
title: Google Code Prettify代码高亮 
categories: experience
tags: linux google code
keywords: linux,google,code,命令,参数
tagline: Supporting tagline
---
代码高亮在网页显示中比较重要，Google Code Prettify几乎满足了所有需求：

+ 支持大部分语言
+ 文件小，加载速度快
+ 显示美观

下面介绍下如何将Google Code Prettify加入到自己的网页中。

Step 1. 下载文件。解压将pretty.css和pretty.js放到网站服务器的资源位置。

    https://code.google.com/p/google-code-prettify/downloads/list

Step 2. 引用文件。将如下代码放入到网页中：

    <link href="prettify.css" type="text/css" rel="stylesheet" />
    <script src="prettify.js" type="text/javascript"></script>

Step 3. 加载方法。在<body>标签中加入如下代码：

    <body onload="prettyPrint()">

Step 4. 修改代码标签。在<pre>标签中加入如下代码：

    <pre class="prettyprint">...</pre>

这样就可以显示带高亮的代码了。

这里如果大家嫌麻烦不想每次写代码的时候都加上class="prettyprint"的话，可以通过js来实现。

+ 优点：每次和以前一样，不需要写多余的代码
+ 缺点：每次页面刷新的时候，开始的时候都是没有高亮的，之后js执行的时候会变为高亮。

具体方法也很简单：

将Step 3的操作改为如下操作，Step 4取消即可。

引用js文件：

    <script src="/assets/js/jquery-1.11.1.min.js" type="text/javascript"></script>

加入js代码：

    <script>
        $(window).load(function(){
            $("pre").addClass("prettyprint");
            prettyPrint();
        })
    </script>

完毕！
