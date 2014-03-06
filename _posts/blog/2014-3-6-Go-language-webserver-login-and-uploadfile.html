---
layout: post
title: Go语言实现web服务器，登陆和文件上传
description: 学习使用Go语言实现一个web服务器，编写登陆页面，上传文件页面，实现简单登陆验证和文件上传功能
category: blog
---

---
layout: post
title: Go语言实现web服务器，登陆和文件上传
description: 学习使用Go语言实现一个web服务器，编写登陆页面，上传文件页面，实现简单登陆验证和文件上传功能
category: blog
---


<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
<title>2014-3-6-Go-language-webserver-login-and-uploadfile</title>
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

<h1 id="go-web-">Go语言实现web服务器，登陆和文件上传</h1>
<p>学习使用Go语言实现一个web服务器，编写登陆页面，上传文件页面，实现简单登陆验证和文件上传功能</p>
<h2 id="web-">web服务器</h2>
<pre><code>func sayhelloName(w http.ResponseWriter, r *http.Request) {
    r.ParseForm()       //解析url传递的参数，对于POST则解析响应包的主体（request body）
    //注意:如果没有调用ParseForm方法，下面无法获取表单的数据
    fmt.Println(r.Form) //这些信息是输出到服务器端的打印信息
    fmt.Println(&quot;path&quot;, r.URL.Path)
    fmt.Println(&quot;scheme&quot;, r.URL.Scheme)
    fmt.Println(r.Form[&quot;url_long&quot;])
    for k, v := range r.Form {
        fmt.Println(&quot;key:&quot;, k)
        fmt.Println(&quot;val:&quot;, strings.Join(v, &quot;&quot;))
    }
    fmt.Fprintf(w, &quot;Hello swinghu!&quot;) //这个写入到w的是输出到客户端的
}</code></pre>
<p>启动该页面的处理函数</p>
<pre><code>    main（）{
          http.HandleFunc(&quot;/&quot;, sayhelloName)       //设置访问的路由
        err := http.ListenAndServe(&quot;:9090&quot;, nil) //设置监听的端口
        if err != nil {
            log.Fatal(&quot;ListenAndServe: &quot;, err)
        }
    }</code></pre>
<p>浏览器输入127.0.0.1,查看结果：<br><img src="http://i.imgur.com/WIRrOcq.png" alt=""></p>
<h2 id="-">登陆页面设计</h2>
<p>Notepad++ 编写html文件并保存为login.gptl(以下github自动将html转换为网页显示)<br>    <html><br>    <head><br>    <title></title><br>    </head><br>    <body><br>        <table weith="1024" heigth="400"><br>        <input type="checkbox" name = "interest" value = "football">足球<br>        <input type="checkbox" name = "interest" value= "basketball">篮球<br>        <input type="checkbox" name = "interest" value ="tennis">网球<br>        <form action="/login" method="post"><br>            用户名:<input type="text" name="username"><br>            密码:<input type="password" name="password"><br>            <input type = "hidden" name = "token" value = "{{.}}"><br>            <input type="submit" value="登陆"><br>        </form><br>        <select name = "fruit"><br>        <option value = "apple">apple</option><br>        <option value = "pear"> pear</option><br>        <option value = "banana">banana</option><br>        </select><br>    </body><br>    </html></p>
<p>注意将保存文件的格式设为UTF-8无BOM格式，否则可能由于编码问题，导致出错（直接显示页面HTML文件的内容）。<br>编写服务器端登陆处理代码：<br>    func login(w http.ResponseWriter, r *http.Request) {<br>        fmt.Println(&quot;method:&quot;, r.Method) //获取请求的方法<br>        if r.Method == &quot;GET&quot; {<br>            crutime := time.Now().Unix()<br>            h := md5.New()<br>            io.WriteString(h,strconv.FormatInt(crutime,10))<br>            token := fmt.Sprintf(&quot;%x&quot;,h.Sum(nil))</p>
<pre><code>        t, _ := template.ParseFiles(&quot;login.gtpl&quot;)
        w.Header().Set(&quot;Content-Type&quot;, &quot;text/html; charset=utf-8&quot;)// fix the the return html file
        t.Execute(w, token)//增加 token：将nil 改为token            
        } else {
        //请求的是登陆数据，那么执行登陆的逻辑判断
        r.ParseForm()//默认handler 不对form进行解析   
        token := r.Form.Get(&quot;token&quot;)
        if token != &quot;&quot; {
            fmt.Println(&quot;token is :&quot;, template.HTMLEscapeString(r.Form.Get(&quot;token&quot;)))
        } else {
            fmt.Println(&quot;token  errer&quot;)
        }

        fmt.Println(&quot;username:&quot;, template.HTMLEscapeString(r.Form.Get(&quot;username&quot;)))
        fmt.Println(&quot;password:&quot;, template.HTMLEscapeString(r.Form.Get(&quot;password&quot;)))
        fmt.Println(&quot;fruit:&quot;,template.HTMLEscapeString(r.Form.Get(&quot;fruit&quot;)))

        if len(r.Form.Get(&quot;password&quot;)) == 0 {
            //template.HTMLEscape(w,[]byte(&quot;password is null&quot;))
            t, _ := template.ParseFiles(&quot;login.gtpl&quot;)
               w.Header().Set(&quot;Content-Type&quot;, &quot;text/html; charset=utf-8&quot;)
               t.Execute(w, nil)
        }else {
            t, _ := template.ParseFiles(&quot;upload.gtpl&quot;)//实现登陆后跳转到upload页面
            w.Header().Set(&quot;Content-Type&quot;, &quot;text/html; charset=utf-8&quot;)
               t.Execute(w, nil)
            template.HTMLEscape(w,[]byte(&quot;Hello &quot;+r.Form.Get(&quot;username&quot;)+&quot;,you have loginning,the web token is &quot;+template.HTMLEscapeString(r.Form.Get(&quot;token&quot;))))
        }
    }
}</code></pre>
<p>启动该页面的处理函数：<br>    func main() {<br>    .............<br>    http.HandleFunc(&quot;/login&quot;, login)         //设置访问的路由<br>    .............<br>    err := http.ListenAndServe(&quot;:9090&quot;, nil) //设置监听的端口<br>    if err != nil {<br>        log.Fatal(&quot;ListenAndServe: &quot;, err)<br>    }</p>
<p>浏览器输入127.0.0.1:9090,查看结果：<br><img src="http://i.imgur.com/LFJRDb4.png" alt=""></p>
<h2 id="-">文档上传</h2>
<p>Notepad++ 编写html文件并保存问upload.gtpl(以下github自动将html转换为网页显示)<br>    <html><br>    <head><br>    <title>upload file</title><br>    </head><br>    <body><br>        <form enctype ="multipart/form-data" action ="http://127.0.0.1:9090/upload" method = "post"><br>            <input type = "file" name ="uploadfile"/><br>            <input type = "hidden" name = "token" value ="{{.}}"/><br>            <input type = "submit" value = "upload" /><br>            <input type = "hidden" name = "token" value = "{{.}}"><br>        </form><br>    </body><br>    </html><br>注意将保存文件的格式设为UTF-8无BOM格式，否则可能由于编码问题，导致出错（直接显示页面HTML文件的内容）。<br>编写服务器端登陆处理代码：</p>
<pre><code>func upload (w http.ResponseWriter, r *http.Request) {//上传文件处理
    fmt.Println(&quot;method&quot;,r.Method)
    if r.Method == &quot;GET&quot; {
        crutime := time.Now().Unix()
        h := md5.New()
        io.WriteString(h,strconv.FormatInt(crutime,10))
        token := fmt.Sprintf(&quot;%x&quot;,h.Sum(nil))
        t, _ := template.ParseFiles(&quot;upload.gtpl&quot;)
        t.Execute(w,token)
    }else {
        r.ParseMultipartForm(32&lt;&lt;20)
        file, handler ,err := r.FormFile(&quot;uploadfile&quot;)        
        if err != nil {
            fmt.Println(err)
            return
        }

        defer file.Close()
        fmt.Fprintf(w,&quot;%v&quot;,handler.Header)

        f, err := os.OpenFile(&quot;./test/&quot;+handler.Filename,os.O_WRONLY|os.O_CREATE,0666)
        if err != nil {
            fmt.Println(err)
            return
        } else {
            fmt.Println(&quot;File:&quot;+handler.Filename+&quot; upload successfully&quot;)
        }
        defer f.Close()
        io.Copy(f,file)
    }
}</code></pre>
<p>启动该页面的处理函数：</p>
<pre><code>    func main() {
        .............   
        http.HandleFunc(&quot;/login&quot;, login)         //设置访问的路由
        .............
        http.HandleFunc(&quot;/upload&quot;,upload)//设置上传文件的访问路由
        err := http.ListenAndServe(&quot;:9090&quot;, nil) //设置监听的端口

        if err != nil {
            log.Fatal(&quot;ListenAndServe: &quot;, err)
        }</code></pre>
<p>浏览器输入127.0.0.1:9090,输入用户名，密码（密码不能为空）登陆后，页面跳转到upload 页面，选择本地文件点击上传，查看结果：<br><img src="http://i.imgur.com/oGM7gin.png" alt=""><br><img src="http://i.imgur.com/dW2Z3Rp.png" alt=""></p>
<p>整个执行过程服务端输出为：</p>
<pre><code>method: POST
token is : c405a0c1f62eaa856394b21462fafb2c
username: gouser
password: dkjssdfsdf
fruit: 
map[]
path /favicon.ico
scheme 
[]
method POST
File:Server.go upload successfully
map[]
path /favicon.ico
scheme 
[]</code></pre>
<p>源码获取：<img src="http://i.imgur.com/t4ps3Uh.png" alt=""><br><a href="https://github.com/swinghu/gowebserver.git" title="Go webserver"><a href="https://github.com/swinghu/gowebserver.git">https://github.com/swinghu/gowebserver.git</a></a></p>


<!-- This document was created with MarkdownPad, the Markdown editor for Windows (http://markdownpad.com) -->
