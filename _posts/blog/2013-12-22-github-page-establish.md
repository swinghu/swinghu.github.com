---
layout: post
title: github 个人网站搭建
description: 使用github搭建个人主页,GitExtensions,RailInstaller。
category: blog
---
写这篇文章主要是总结自己学习搭建web page的过程，以免下次，总结搭建过程中遇到的问题，
也是帮助没有使用过github和Jekyll的童鞋可以快速掌握搭建过程，快速体验。

如果你对ruby完全没有了解，仅仅对html有初步的了解，这都没有关系，只要你懂一点点linux命令就行
例如ls,cd,mkdir,cp,ssh命令等(不懂也没有关系),不懂请用到时Google。一切软件的下载见后面的软件汇总，具体步骤如下：

1，安装Git
在windows下安装git，我选择的是GitExtensions233SetupComplete.msi默认安装就行。

2，安装ruby环境
安装RailInstaller，在学习的过程中，在网上找资料发现大多数推荐安装Ruby2.0.0或者其他版本，其实经过试验后
或多或少存在一些问题(有些问题是由于软件更新导致，有些由于写的不够详细而产生)，下载rubyinstaller-1.9.3-p448.exe
选择默认安装(尽量安装路径不要出现空格或中文)，为什么选择？以为其集成了Ruby、Rails、Bundler、Git、Sqlite、TinyTDS、SQL Server support和DevKit等软件
(包含主要使用的的Devkit)，并且RailInstaller的好处接下来就会体现。

3，配置Git
在RailInstaller安装完成界面(程序安装的最后一步)，提示是否进行Git环境的配置，默认情况是选择是，选择“确定”就行。
如果你之前配置好了git，这边会自动检测到你的相关信息，如git帐号，邮箱，key，以及会显示一些软件信息如：ruby，git版本之类的
并且自动cd到目录 /c/Sites下面，今后你只要将博客放在该目录下就行。
在开始菜单里找到RailsInstaller –> Git Bash，执行它，就打开了下面的命令窗口，以后的配置操作都是在这个窗口下进行的
首先测试是否git可以正常连接，如果不能，请回到第一步进行Git的配置(该命令在运行，开始->程序->RailsInstaller –> Git Bash 控制台下执行(该控制台我主要是为配置环境用))。
	ssh -T git@github.com
提示以下信息表示连接成功：

	$  ssh -T git@github.com
	Hi user_name! You've successfully authenticated, but GitHub does not provide shell
	access.
	
4，安装Jekyll和相关包
首先更改一个镜像文件的地址：

	gem sources --remove http://rubygems.org/
	gem sources -a http://ruby.taobao.org/
	
然后用gem sources -l看看现在源列表(我的电脑上添加了多次，所以有多个项)
	
	$ gem sources -l
	*** CURRENT SOURCES ***
	http://ruby.taobao.org/
	http://ruby.taobao.org/
	http://ruby.taobao.org/
	http://ruby.taobao.org/
	http://ruby.taobao.org/

安装jekyll

	gem install jekyll
	
安装附加项，Jekyll需要用到directory_watcher、liquid、open4、maruku和classifier这几个包，
用上面的命令可以自动安装。Jekyll默认用maruku来解析markdown语言，你也可以用别的程序来解析，
比如rdiscount或kramdown

	gem install rdiscount kramdown

5，建立github pages
在github.com上创建代码库，登录到自己的Github账户，选择New repository,比如新建一个名如：name.github.com的代码库
然后在代码库页，选择右侧的下拉列表框：Settings，就会对该项目进行修改，找到Github Pages一栏，点击右侧Automatic Page Generator按钮
生成网页，稍等片刻系统就会将网页生成好。待生成好后，克隆自己的代码库
	git clone git@github.com:user_name/dkd.git
执行以后，git会把存放在github上的代码库文件下载到本地的，生成名为dkd的目录。删掉.git目录，并且将网站文件放置在该文件夹下

6，写博文，发博客(请打开：开始->程序->RailsInstaller –> Command Prompt with Ruby and Rails控制台应用程序，今后我们的博文推送都将会通过这个控制台进行)
编辑博客，并以文件后缀.md命名，博文开头格式如下

	---
	layout: post
	title: MathJax编程
	category: blog
	description: Shell是用户与Linux操作系统沟通的桥梁，是每一个Linux用户的必修功课之一。
	---

文件命名方式如下:
	2013-12-8-Linux-Shell.md
请确保你的文件被保存为不含 BOM 的 UTF-8(若不是将会出错，可以使用notepad++ 来进行格式转换) 
使用git命令推送到git服务器上，先加入本地库中
	git add .
	git commit -m"备注修改信息“
	git push
如果你在其他机器上修改过，那么先要执行 git pull否则会提示： non-fast-forward错误

	C:\Sites\username.github.com>git push
	To git@github.com:username/username.github.com.git
	! [rejected]        master -> master (non-fast-forward)
	error: failed to push some refs to 'git@github.com:username/username.github.com.git'
	To prevent you from losing history, non-fast-forward updates were rejected
	Merge the remote changes (e.g. 'git pull') before pushing again.  See the
	'Note about fast-forwards' section of 'git push --help' for details.
7，浏览器打开浏览username.github.io
稍等片刻，github就会为你生成网页。用浏览器打开网址：username.github.com


软件汇总：
- msygit链接：[msygit][msygit]
- RailInstall下载链接：[RailInstall-1.9.3-p448][rail]

[msygit]: http://code.google.com/p/msysgit/downloads/list
[rail]: http://inwake.com/ypchen/files/upload/railsinstaller-2.0.1.exe
