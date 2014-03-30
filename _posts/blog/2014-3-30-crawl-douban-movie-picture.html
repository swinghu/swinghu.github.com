---
layout: post
title:爬取douban(18000+)影视海报图片
category: blog
description: golang语言， mongodb数据库
---


<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
<title>2014-3-30-crawl-douban-movie-picture</title>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<style type="text/css">
/* GitHub stylesheet for MarkdownPad (http://markdownpad.com) */
/* Author: Nicolas Hery - http://nicolashery.com */
/* Version: b13fe65ca28d2e568c6ed5d7f06581183df8f2ff */
/* Source: https://github.com/nicolahery/markdownpad-github */

/* RESET
=============================================================================*/

html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, embed, figure, figcaption, footer, header, hgroup, menu, nav, output, ruby, section, summary, time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
}

/* BODY
=============================================================================*/

body {
  font-family: Helvetica, arial, freesans, clean, sans-serif;
  font-size: 14px;
  line-height: 1.6;
  color: #333;
  background-color: #fff;
  padding: 20px;
  max-width: 960px;
  margin: 0 auto;
}

body>*:first-child {
  margin-top: 0 !important;
}

body>*:last-child {
  margin-bottom: 0 !important;
}

/* BLOCKS
=============================================================================*/

p, blockquote, ul, ol, dl, table, pre {
  margin: 15px 0;
}

/* HEADERS
=============================================================================*/

h1, h2, h3, h4, h5, h6 {
  margin: 20px 0 10px;
  padding: 0;
  font-weight: bold;
  -webkit-font-smoothing: antialiased;
}

h1 tt, h1 code, h2 tt, h2 code, h3 tt, h3 code, h4 tt, h4 code, h5 tt, h5 code, h6 tt, h6 code {
  font-size: inherit;
}

h1 {
  font-size: 28px;
  color: #000;
}

h2 {
  font-size: 24px;
  border-bottom: 1px solid #ccc;
  color: #000;
}

h3 {
  font-size: 18px;
}

h4 {
  font-size: 16px;
}

h5 {
  font-size: 14px;
}

h6 {
  color: #777;
  font-size: 14px;
}

body>h2:first-child, body>h1:first-child, body>h1:first-child+h2, body>h3:first-child, body>h4:first-child, body>h5:first-child, body>h6:first-child {
  margin-top: 0;
  padding-top: 0;
}

a:first-child h1, a:first-child h2, a:first-child h3, a:first-child h4, a:first-child h5, a:first-child h6 {
  margin-top: 0;
  padding-top: 0;
}

h1+p, h2+p, h3+p, h4+p, h5+p, h6+p {
  margin-top: 10px;
}

/* LINKS
=============================================================================*/

a {
  color: #4183C4;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

/* LISTS
=============================================================================*/

ul, ol {
  padding-left: 30px;
}

ul li > :first-child, 
ol li > :first-child, 
ul li ul:first-of-type, 
ol li ol:first-of-type, 
ul li ol:first-of-type, 
ol li ul:first-of-type {
  margin-top: 0px;
}

ul ul, ul ol, ol ol, ol ul {
  margin-bottom: 0;
}

dl {
  padding: 0;
}

dl dt {
  font-size: 14px;
  font-weight: bold;
  font-style: italic;
  padding: 0;
  margin: 15px 0 5px;
}

dl dt:first-child {
  padding: 0;
}

dl dt>:first-child {
  margin-top: 0px;
}

dl dt>:last-child {
  margin-bottom: 0px;
}

dl dd {
  margin: 0 0 15px;
  padding: 0 15px;
}

dl dd>:first-child {
  margin-top: 0px;
}

dl dd>:last-child {
  margin-bottom: 0px;
}

/* CODE
=============================================================================*/

pre, code, tt {
  font-size: 12px;
  font-family: Consolas, "Liberation Mono", Courier, monospace;
}

code, tt {
  margin: 0 0px;
  padding: 0px 0px;
  white-space: nowrap;
  border: 1px solid #eaeaea;
  background-color: #f8f8f8;
  border-radius: 3px;
}

pre>code {
  margin: 0;
  padding: 0;
  white-space: pre;
  border: none;
  background: transparent;
}

pre {
  background-color: #f8f8f8;
  border: 1px solid #ccc;
  font-size: 13px;
  line-height: 19px;
  overflow: auto;
  padding: 6px 10px;
  border-radius: 3px;
}

pre code, pre tt {
  background-color: transparent;
  border: none;
}

kbd {
    -moz-border-bottom-colors: none;
    -moz-border-left-colors: none;
    -moz-border-right-colors: none;
    -moz-border-top-colors: none;
    background-color: #DDDDDD;
    background-image: linear-gradient(#F1F1F1, #DDDDDD);
    background-repeat: repeat-x;
    border-color: #DDDDDD #CCCCCC #CCCCCC #DDDDDD;
    border-image: none;
    border-radius: 2px 2px 2px 2px;
    border-style: solid;
    border-width: 1px;
    font-family: "Helvetica Neue",Helvetica,Arial,sans-serif;
    line-height: 10px;
    padding: 1px 4px;
}

/* QUOTES
=============================================================================*/

blockquote {
  border-left: 4px solid #DDD;
  padding: 0 15px;
  color: #777;
}

blockquote>:first-child {
  margin-top: 0px;
}

blockquote>:last-child {
  margin-bottom: 0px;
}

/* HORIZONTAL RULES
=============================================================================*/

hr {
  clear: both;
  margin: 15px 0;
  height: 0px;
  overflow: hidden;
  border: none;
  background: transparent;
  border-bottom: 4px solid #ddd;
  padding: 0;
}

/* TABLES
=============================================================================*/

table th {
  font-weight: bold;
}

table th, table td {
  border: 1px solid #ccc;
  padding: 6px 13px;
}

table tr {
  border-top: 1px solid #ccc;
  background-color: #fff;
}

table tr:nth-child(2n) {
  background-color: #f8f8f8;
}

/* IMAGES
=============================================================================*/

img {
  max-width: 100%
}
</style>
</head>
<body>
<h1 id="-douban-18000-">爬取douban(18000+)影视海报图片</h1>
<p>使用golang爬取douban上18000+影视海报图片,涉及到操作golang网络包，以及mongodb 的基本操作。代码如下</p>
<pre><code>package main

import (
    &quot;bytes&quot;
    &quot;fmt&quot;
    &quot;io&quot;
    &quot;io/ioutil&quot;
    &quot;net/http&quot;
    &quot;os&quot;
    &quot;strings&quot;
    &quot;labix.org/v2/mgo&quot;
    &quot;labix.org/v2/mgo/bson&quot;
    &quot;time&quot;
    &quot;strconv&quot;
)

type movie struct{
    Id_  bson.ObjectId  `bson:&quot;_id&quot;`
    Alt string            `bson:&quot;alt&quot;`
    Casts []string        `bson:&quot;casts&quot;`
    Countries []string    `bson:&quot;countries&quot;`
    Cb_id string        `bson:&quot;db_id&quot;`
    Directors []string    `bson:&quot;directors&quot;`
    Download []string    `bson:&quot;download&quot;`
    Genres []string        `bson:&quot;genres&quot;`
    Id int64            `bson:&quot;id&quot;`
    Image string        `bson:&quot;image&quot;`     //imgurl字段
    Iscrawled bool         `bson:&quot;iscrawled`
    Rating string        `bson:&quot;rating&quot;`
    Summary string        `bson:&quot;summar&quot;`
    Title string        `bson:&quot;title&quot;`
    Year time.Time        `bson:&quot;year&quot;`
}


func main() {
        //连接数据库，获取picture的url
        session, err := mgo.Dial(&quot;127.0.0.1&quot;)
        if err != nil {
                panic(err)
        }
        defer session.Close()

        // Optional. Switch the session to a monotonic behavior.
        session.SetMode(mgo.Monotonic, true)

        c := session.DB(&quot;movie&quot;).C(&quot;movieclip&quot;)    创建对话
        count := 0
        count,err  = c.Count()
        if err != nil{
            panic(err)
        }
        fmt.Println(&quot;cout&quot;,count) 

        // 取出picurl

        mv := []movie{}

        err = c.Find(nil).All(&amp;mv)
        for i, m := range mv {
            if m.Iscrawled == false { 
                //去掉&quot;http: //&quot;中“http:”与“//”之间的空格，否者调用getImg失败
                newurl := strings.Replace(m.Image,&quot; //&quot;,&quot;//&quot;,1)
                fmt.Println(&quot;crawl url: &quot;+strconv.Itoa(i)+&quot;  &quot;+newurl)            
                getImg(newurl)
                //iscrawled = true，设置为“已经下载该图片”
                c.Update(bson.M{&quot;_id&quot;:m.Id_},
                    bson.M{&quot;$set&quot;:bson.M{&quot;iscrawled&quot;:true}})                    
            }else{
                   continue
               }

        }
}

func getImg(url string) (n int64, err error) {//获取图片
    path := strings.Split(url, &quot;/&quot;)             //分割字符串
    var name string
    if len(path) &gt; 1 {
        name = path[len(path)-1]
    }
    fmt.Println(name)
    out, err := os.Create(name)
    defer out.Close()
    resp, err := http.Get(url)                 //调用网络模块包：http,使用Get方式请求
    defer resp.Body.Close()                     //获取请求后响应
    pix, err := ioutil.ReadAll(resp.Body)
    n, err = io.Copy(out, bytes.NewReader(pix))    //写入到本地文件中
    return

}</code></pre>
<h2 id="golang-mongodb">golang连接mongodb</h2>
<ol>
<li><p>导入包<br>mgo目前虽然不是mongodb的golang的官方驱动包，目前很有可能成为golang，mongodb驱动的标准。</p>
<pre><code> &quot;labix.org/v2/mgo&quot;
 &quot;labix.org/v2/mgo/bson&quot;</code></pre>
</li>
<li><p>创建回话Dial</p>
<p> session, err := mgo.Dial(&quot;127.0.0.1&quot;)</p>
<pre><code>     if err != nil {
             panic(err)
     }
     defer session.Close()

     // Optional. Switch the session to a monotonic behavior.
     session.SetMode(mgo.Monotonic, true)//是否开启一致性会话模式。</code></pre>
</li>
<li><p>创建回话，连接到db，获取到文档集,    </p>
<pre><code> c := session.DB(&quot;test&quot;).C(&quot;people&quot;)    创建对话
 count := 0
 count,err  = c.Count()
 if err != nil{
     panic(err)
     }</code></pre>
</li>
<li><p>取出文档集movie中的url字段</p>
<pre><code> // 取出picurl
 mv := []movie{}       
 err = c.Find(nil).All(&amp;mv)
 newurl := strings.Replace(m.Image,&quot; //&quot;,&quot;//&quot;,1)</code></pre>
</li>
</ol>
<h2 id="mongo-">mongo操作</h2>
<ol>
<li><p>mongodb增加iscrawled字段<br>在爬取图片的时候，首先设置一个是否爬取得标记，对全部文档进行添加字段iscrawled，在控制台命令提示符中进行设置</p>
<pre><code>  use movie        //确保操作是在movi
  db.movie.update({},{$set:{&quot;iscrawled&quot;:&quot;0&quot;}},false,true)</code></pre>
<p>下载更新之后设置为已经下载：</p>
<pre><code>  c.Update(bson.M{&quot;_id&quot;:m.Id_},
              bson.M{&quot;$set&quot;:bson.M{&quot;iscrawled&quot;:true}})    </code></pre>
</li>
<li><p>相关mongodb命令 </p>
</li>
</ol>
<ul>
<li><p>增加删除字段    </p>
<pre><code>db.people.update({},{$set:{&quot;iscrawled&quot;:&quot;0&quot;}},false,true)
db.people.update({},{$unset:{&quot;iscrawled&quot;:&quot;0&quot;}},false,true)
db.people.update({},{$set:{&quot;iscrawled&quot;:false}},false,true)</code></pre>
</li>
<li>导入数据(json格式文件)<br><code>E:\installsoft\mongodb\bin&gt;mongoimport -d test -c people --file E:\installsoft\mongodb\data\db\movie.json</code></li>
</ul>
<ul>
<li><p>mongodb意外掉电，不能重新开启服务！</p>
<p>  Fri Mar 28 12:49:19.924 [initandlisten] CreateFileW for E:\installsoft\mongodb\d<br>  ata\db\bastogne.ns failed with errno:5 拒绝访问。 (file size is 16777216) in Mem<br>  oryMappedFile::map<br>  Fri Mar 28 12:49:19.926 [initandlisten] error couldn&#39;t open file E:\installsoft\<br>  mongodb\data\db\bastogne.ns terminating</p>
</li>
</ul>
<pre><code>E:\installsoft\mongodb\bin&gt;mongod --repair --dbpath=E:\installsoft\mongodb\data</code></pre>
<h2 id="-">参考文献：</h2>
<ol>
<li>mgo Guide 0.1 (中文) 》<a href="http://jimmykuu.sinaapp.com/static/books/mgo_guide/">http://jimmykuu.sinaapp.com/static/books/mgo_guide/</a></li>
<li>mgo doc v2：<a href="http://godoc.org/labix.org/v2/mgo">http://godoc.org/labix.org/v2/mgo</a></li>
<li>mgo项目主页：<a href="http://labix.org/mgo">http://labix.org/mgo</a></li>
</ol>

</body>
</html>
<!-- This document was created with MarkdownPad, the Markdown editor for Windows (http://markdownpad.com) -->
