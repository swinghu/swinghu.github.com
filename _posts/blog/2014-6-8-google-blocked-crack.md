---
layout: post
title: google block  之终极解决方式[持续更新]
description: google blocked 解决方案(本文章持续更新，如果有新的解决方案，请对此博文进行评论留言【点击查看评论】。)
category: blog
---


#google block  之终极解决方式  #

首先声明 该方法来自互联网，方法1，方法2简单，用户可以尝试，我亲测第一种方法可以用，方法2，3没有	亲测。

方法1 修改hosts文件
----
将

    203.208.41.144 www.google.com.hk
    203.208.41.145 www.google.com.hk

添加至：* C:\Windows\System32\drivers\etc\hosts*文件中


#### 2014/6/9 18:59:34 更新 ###

另网友提供新的可用ip，感谢[过往记忆](http://www.iteblog.com/archives/1039)

详细见原文地址：http://www.iteblog.com/archives/1039

目前google只有北京段的IP有用，之前的

	74.125.128.94、
	74.125.235.191、
	74.125.224.212、
	74.125.131.105、
	173.194.70.100

google北京的IP地址范围是203.208.32.0 – 203.208.63.255，经过我测试IP范围在203.208.46.[128-223]之间都可以用，下面的一些IP也可以用：

	203.208.37.18
	203.208.37.16
	203.208.37.20
	203.208.37.17
	203.208.37.19


方法2 修改Chrome 浏览器
----
在 Chrome 浏览器中打开「实验性功能」页面（chrome://flags/），启用「实验性 QUIC 协议」和「经由实验性 QUIC 协议发出的 HTTPS 请求」，重启浏览器后可以正常登陆 Google 相关服务。// 我就是手抖


方法3 修改host （请保持耐心看完）
----
谷歌google搜索打不开、谷歌gmail邮箱及相关服务无法登录的解决办法

谷歌打不开, 谷歌打不开怎么办, google打不开, google打不开怎么办, 谷歌

谷歌打不开 google打不开，与中国大陆封杀有关，但是主要是因为最近google服务器在全球范围内重新进行了布局调整。

解决办法是只要修改用户本地计算机hosts文件就可以了。

###一、Windows系统修改hosts文件的方法

windows系统hosts文件在本地电脑C盘，路径是：*C:\Windows\System32\drivers\etc *

用记事本txt文件打开hosts文件。

（如果提示没有管理权限的话，可把hosts文件复制，粘贴到电脑的桌面。在电脑桌面上双击hosts文件，用记事本打开，添加代码修改，保存，再把桌面上这个hosts文件复制，粘贴到*C:\Windows\System32\Drivers\etc* 文件夹里，电脑提示“是否替换”，点击“是”，替换原来的hosts文件。)

（如果没找到hosts文件，可在本帖末尾下载一个新hosts，复制到*C:\Windows\System32\Drivers\etc* 文件夹里。）


在hosts文件中把鼠标光标移到最下面那行代码末尾，回车换行，再添加进如下代码（代码前面不加 # ）：

    
    203.208.46.176 0-focus-opensocial.googleusercontent.com
    
    203.208.46.176 3hdrrlnlknhi77nrmsjnjr152ueo3soc-a-calendar-opensocial.googleusercontent.com
    
    203.208.46.176 accounts.google.com
    
    203.208.46.176 ajax.googleapis.com
    
    203.208.46.176 android.l.google.com
    
    203.208.46.176 a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 apis.google.com
    
    203.208.46.176 appengine.google.com
    
    203.208.46.176 bks0.books.google.com
    
    203.208.46.176 bks1.books.google.com
    
    203.208.46.176 bks2.books.google.com
    
    203.208.46.176 bks3.books.google.com
    
    203.208.46.176 bks4.books.google.com
    
    203.208.46.176 bks5.books.google.com
    
    203.208.46.176 bks6.books.google.com
    
    203.208.46.176 bks7.books.google.com
    
    203.208.46.176 bks8.books.google.com
    
    203.208.46.176 bks9.books.google.com
    
    203.208.46.176 blogsearch.google.cn
    
    203.208.46.176 blogsearch.google.com.hk
    
    203.208.46.176 books.google.com
    
    203.208.46.176 browserchannel-docs.l.google.com
    
    203.208.46.176 browserchannel-spreadsheets.l.google.com
    
    203.208.46.176 browsersync.google.com
    
    203.208.46.176 cache.pack.google.com
    
    203.208.46.176 calendar.google.com
    
    203.208.46.176 chatenabled.mail.google.com
    
    203.208.46.176 checkout.google.com
    
    203.208.46.176 chrome.google.com
    
    203.208.46.176 clients1.google.com
    
    203.208.46.176 clients1.googleusercontent.com
    
    203.208.46.176 clients2.google.com
    
    203.208.46.176 clients2.googleusercontent.com
    
    203.208.46.176 clients3.google.com
    
    203.208.46.176 clients3.googleusercontent.com
    
    203.208.46.176 clients4.google.com
    
    203.208.46.176 clients4.googleusercontent.com
    
    203.208.46.176 clients5.google.com
    
    203.208.46.176 clients5.googleusercontent.com
    
    203.208.46.176 clients6.google.com
    
    203.208.46.176 clients6.googleusercontent.com
    
    203.208.46.176 clients7.google.com
    
    203.208.46.176 clients7.googleusercontent.com
    
    203.208.46.176 code.google.com
    
    203.208.46.176 csi.gstatic.com
    
    203.208.46.176 desktop.google.com
    
    203.208.46.176 desktop2.google.com
    
    203.208.46.176 ditu.google.cn
    
    203.208.46.176 ditu.google.com
    
    203.208.46.176 dl.google.com
    
    203.208.46.176 docs.google.com
    
    203.208.46.176 earth.google.com
    
    203.208.46.176 encrypted.google.com
    
    203.208.46.176 encrypted.google.com.hk
    
    203.208.46.176 encrypted-tbn0.google.com
    
    203.208.46.176 encrypted-tbn1.google.com
    
    203.208.46.176 encrypted-tbn2.google.com
    
    203.208.46.176 encrypted-tbn3.google.com
    
    203.208.46.176 feedback.googleusercontent.com
    
    203.208.46.176 finance.google.com
    
    203.208.46.176 fonts.googleapis.com
    
    203.208.46.176 g0.gstatic.com
    
    203.208.46.176 gg.google.com
    
    203.208.46.176 ghs.google.com
    
    203.208.46.176 ghs.l.google.com
    
    203.208.46.176 google.com
    
    203.208.46.176 google.com.hk
    
    203.208.46.176 googlecl.googlecode.com
    
    203.208.46.176 googlehosted.l.googleusercontent.com
    
    203.208.46.176 id.google.cn
    
    203.208.46.176 id.google.com
    
    203.208.46.176 id.google.com.hk
    
    203.208.46.176 images.google.com
    
    203.208.46.176 images.google.com.hk
    
    203.208.46.176 images0-focus-opensocial.googleusercontent.com
    
    203.208.46.176 images1-focus-opensocial.googleusercontent.com
    
    203.208.46.176 images2-focus-opensocial.googleusercontent.com
    
    203.208.46.176 images3-focus-opensocial.googleusercontent.com
    
    203.208.46.176 images4-focus-opensocial.googleusercontent.com
    
    203.208.46.176 images5-focus-opensocial.googleusercontent.com
    
    203.208.46.176 images6-focus-opensocial.googleusercontent.com
    
    203.208.46.176 images-lso-opensocial.googleusercontent.com
    
    203.208.46.176 images-oz-opensocial.googleusercontent.com
    
    203.208.46.176 images-pos-opensocial.googleusercontent.com
    
    203.208.46.176 investor.google.com
    
    203.208.46.176 khms0.google.com
    
    203.208.46.176 khms1.google.com
    
    203.208.46.176 labs.google.com
    
    203.208.46.176 large-uploads.l.google.com
    
    203.208.46.176 lh1.ggpht.com
    
    203.208.46.176 lh1.googleusercontent.com
    
    203.208.46.176 lh2.ggpht.com
    
    203.208.46.176 lh2.googleusercontent.com
    
    203.208.46.176 lh3.ggpht.com
    
    203.208.46.176 lh3.googleusercontent.com
    
    203.208.46.176 lh4.ggpht.com
    
    203.208.46.176 lh4.googleusercontent.com
    
    203.208.46.176 lh5.ggpht.com
    
    203.208.46.176 lh5.googleusercontent.com
    
    203.208.46.176 lh6.ggpht.com
    
    203.208.46.176 lh6.googleusercontent.com
    
    203.208.46.176 m.google.com
    
    203.208.46.176 mail.google.com
    
    203.208.46.176 mail-attachment.googleusercontent.com
    
    203.208.46.176 maps.google.cn
    
    203.208.46.176 maps.google.com
    
    203.208.46.176 maps.gstatic.cn
    
    203.208.46.176 maps.gstatic.com
    
    203.208.46.176 maps-api-ssl.google.com
    
    203.208.46.176 mt0.google.cn
    
    203.208.46.176 mt0.google.com
    
    203.208.46.176 mt1.google.cn
    
    203.208.46.176 mt1.google.com
    
    203.208.46.176 mt2.google.cn
    
    203.208.46.176 mt2.google.com
    
    203.208.46.176 mt3.google.cn
    
    203.208.46.176 mt3.google.com
    
    203.208.46.176 mts0.google.com
    
    203.208.46.176 mts1.google.com
    
    203.208.46.176 music.google.com
    
    203.208.46.176 music.googleusercontent.com
    
    203.208.46.176 music-streaming.l.google.com
    
    203.208.46.176 mw2.google.com
    
    203.208.46.176 news.google.cn
    
    203.208.46.176 news.google.com
    
    203.208.46.176 news.google.com.hk
    
    203.208.46.176 newsfeed-dot-latest-dot-rovio-ad-engine.appspot.com
    
    203.208.46.176 nt0.ggpht.com
    
    203.208.46.176 nt1.ggpht.com
    
    203.208.46.176 nt2.ggpht.com
    
    203.208.46.176 nt3.ggpht.com
    
    203.208.46.176 oauth.googleusercontent.com
    
    203.208.46.176 ode25pfjgmvpquh3b1oqo31ti5ibg5fr-a-calendar-opensocial.googleusercontent.com
    
    203.208.46.176 pack.google.cn
    
    203.208.46.176 pack.google.com
    
    203.208.46.176 picasa.google.com
    
    203.208.46.176 picasaweb.google.com
    
    203.208.46.176 picasaweb.google.com.hk
    
    203.208.46.176 places.google.com
    
    203.208.45.200plus.google.com
    
    203.208.46.176 plus.google.com.hk
    
    203.208.46.176 plusone.google.com
    
    203.208.46.176 pop.gmail.com
    
    203.208.46.176 profiles.google.com
    
    203.208.46.176 project-slingshot-gp.appspot.com
    
    203.208.46.176 r3269-dot-latest-dot-project-slingshot-gp.appspot.com
    
    203.208.46.176 s1.googleusercontent.com
    
    203.208.46.176 s2.googleusercontent.com
    
    203.208.46.176 s3.googleusercontent.com
    
    203.208.46.176 s4.googleusercontent.com
    
    203.208.46.176 s5.googleusercontent.com
    
    203.208.46.176 s6.googleusercontent.com
    
    203.208.46.176 safebrowsing.clients.google.com
    
    203.208.46.176 safebrowsing-cache.google.com
    
    203.208.46.176 sandbox.google.com
    
    203.208.46.176 scholar.google.cn
    
    203.208.46.176 scholar.google.com
    
    203.208.46.176 scholar.google.com.hk
    
    203.208.46.176 scholar.l.google.com
    
    203.208.46.176 services.google.com
    
    203.208.46.176 sites.google.com
    
    203.208.46.176 sketchup.google.com
    
    203.208.46.176 spreadsheets.google.com
    
    203.208.46.176 ssl.google-analytics.com
    
    203.208.46.176 ssl.gstatic.com
    
    203.208.46.176 suggestqueries.google.com
    
    203.208.46.176 t.doc-0-0-sj.sj.googleusercontent.com
    
    203.208.46.176 t0.gstatic.com
    
    203.208.46.176 t1.gstatic.com
    
    203.208.46.176 t2.gstatic.com
    
    203.208.46.176 t3.gstatic.com
    
    203.208.46.176 talkgadget.google.com
    
    203.208.46.176 talkx.l.google.com
    
    203.208.46.176 themes.googleusercontent.com
    
    203.208.46.176 toolbar.google.com
    
    203.208.46.176 toolbar.google.com.hk
    
    203.208.46.176 toolbarqueries.clients.google.com
    
    203.208.46.176 toolbarqueries.google.com.hk
    
    203.208.46.176 tools.google.com
    
    203.208.46.176 translate.google.cn
    
    203.208.46.176 translate.google.com
    
    203.208.46.176 translate.google.com.hk
    
    203.208.46.176 translate.googleapis.com
    
    203.208.46.176 uploadsj.clients.google.com
    
    203.208.46.176 v8mq9slfbk1dglresapkg0i5f8pm64lc-a-calendar-opensocial.googleusercontent.com
    
    203.208.46.176 video.google.cn
    
    203.208.46.176 video.google.com
    
    203.208.46.176 video.google.com.hk
    
    203.208.46.176 voice.google.com
    
    203.208.46.176 wave.google.com
    
    203.208.46.176 webcache.googleusercontent.com
    
    203.208.46.176 wenda.google.com.hk
    
    203.208.46.176 www.gmail.com
    
    203.208.46.180 www.google.com
    
    203.208.46.176 www.google.com.hk
    
    203.208.46.176 www.googleadservices.com
    
    203.208.46.176 www.google-analytics.com
    
    203.208.46.176 www.googleapis.com
    
    203.208.46.176 www.googlelabs.com
    
    203.208.46.176 www.gstatic.com
    
    203.208.46.176 www-calendar-opensocial.googleusercontent.com
    
    203.208.46.176 www-opensocial.googleusercontent.com
    
    203.208.46.176 www-oz-opensocial.googleusercontent.com
    
    203.208.46.176 bt26mravu2qpe56n8gnmjnpv2inl84bf-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 rbjhe237k979f79d87gmenp3gejfonu9-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 k6v18tjr24doa89b55o3na41kn4v73eb-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 8kubpeu8314p2efdd7jlv09an9i2ljdo-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 adstvca8k2ooaknjjmv89j22n9t676ve-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 ob7f2qc0i50kbjnc81vkhgmb5hsv7a8l-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 53rd6p0catml6vat6qra84rs0del836d-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 u807isd5egseeabjccgcns005p2miucq-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 r70rmsn4s0rhk6cehcbbcbfbs31pu0va-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 59cbv4l9s05pbaks9v77vc3mengeqors-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 i8brh95qor6r54nkl52hidj2ggcs4jgm-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 upt14k1i2veesusrda9nfotcrbp9d7p5-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 debh8vg7vd93bco3prdajidmm7dhql3f-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 4fjvqid3r3oq66t548clrdj52df15coc-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 hsco54a20sh11q9jkmb51ad2n3hmkmrg-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 qhie5b8u979rnch1q0hqbrmbkn9estf7-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 e6ha3snmi09c57cs4h4dnoa006cgfjfu-a-oz-opensocial.googleusercontent.com
    
    203.208.46.176 66fl6oqbdsqf5fjl032t5iulimtqjhpa-a-oz-opensocial.googleusercontent.com


代码有点长，直接复制就可以。然后重新打开谷歌google搜索、Gmail邮箱或谷歌相关服务，看看是不是速度飞快呢？！

使用goagent翻墙的同学，建议下载最新版goagent3.1.17，把203.208.46.176 添加到Goagent/Local/proxy.ini 文件里面的 iplist 列表里“google_cn = ”后面，并修改proxy.ini 里的appid，再上传*goagent/server/uploader.bat*，上传完毕就ok了。


###二、苹果Mac系统修改hosts文件的方法

第一种方法：在应用程序里面打开终端（terminal），输入 sudo vi /etc/hosts 回车进入。如果提示输入密码，就输入锁屏密码。hosts文件就自动打开了。
接着输入英文状态下的“ i ”，进入编辑模式，将上面的代码（和上面Windows系统的代码一样）拷贝进去，编辑完成之后，按 esc退出，输入 :wq 保存。

第二种方法：启动root帐户直接改。打开终端，输入: sudo open /Applications/TextEdit.app/Contents/MacOS/TextEdit /etc/hosts  就可以用文本编辑来直观修改hosts了。 


###三、Android手机手动修改HOSTS文件的方法

　　Android手机是和Google帐号紧密联系的，很多时候Google帐号无法登录，导致Android无法使用。

　　在电脑上我们通过修改Hosts方法可以解决Google的登录问题，在Android手机上也可以使用这个方法。

具体操作方法是：

　　1、先通过各种方法让Android手机获取Root权限，之后运行Root Explorer管理器，进入可写状态，找到/system/etc/hosts的文件，将其权限修改为可写。

　　2、打开Terminal Emulator，输入su，进入root模式，输入 vi /system/etc/hosts 命令，按i进入编辑模式，之后将需要添加的代码加入hosts文件中。

　　3、Android虚拟终端下当vi在编辑模式时，按下“确定”键（Trackball），再按下虚拟键盘上的“1”，就可以退出编辑模式了（CTRL+[），这个时候使用 :wq 就可以保存退出了。

　　4、之后重启手机即可。