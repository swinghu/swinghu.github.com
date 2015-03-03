---
layout: post
title: Ubuntu 12.04安装Jekyll调试环境 
categories: linux
tags: linux ubuntu jekyll git
keywords: linux,ubuntu,jeykll,git,命令,参数
tagline: Supporting tagline
---
最近安装了Ubuntu，自然而然要把git马上安装上，其实主要是为了我的这个网站啊，就是github pages，但是突然发现我在Windows安装了调试环境，在Ubuntu上还没有安装，下面就开始安装，步骤比较简单。

Step 1：执行命令

    sudo apt-get install rubygems1.8 rake

Step 2：执行命令

    sudo gem install jekyll

Trouble Shooting：在安装的时候出现了如下信息
    Fetching: liquid-2.6.1.gem (100%)
    Fetching: kramdown-1.4.2.gem (100%)
    Fetching: mercenary-0.3.4.gem (100%)
    Fetching: safe_yaml-1.0.3.gem (100%)
    Fetching: colorator-0.1.gem (100%)
    Fetching: yajl-ruby-1.1.0.gem (100%)
    Building native extensions.  This could take a while...
    Fetching: posix-spawn-0.3.9.gem (100%)
    Building native extensions.  This could take a while...
    Fetching: pygments.rb-0.6.0.gem (100%)
    Fetching: redcarpet-3.1.2.gem (100%)
    ERROR:  Error installing jekyll:
	    redcarpet requires Ruby version >= 1.9.2.
解决方法，通过

    ruby -v

知道当前Ruby版本是1.8，更新Ruby版本即可解决问题。执行命令

    sudo apt-get update
    sudo apt-get install ruby1.9.3
    sudo update-alternatives --install /usr/bin/ruby ruby /usr/bin/ruby1.9.3 400 \
            --slave   /usr/share/man/man1/ruby.1.gz ruby.1.gz \
                            /usr/share/man/man1/ruby1.9.3.1.gz \
            --slave   /usr/bin/ri ri /usr/bin/ri1.9.3 \
            --slave   /usr/bin/irb irb /usr/bin/irb1.9.3 \
            --slave   /usr/bin/rdoc rdoc /usr/bin/rdoc1.9.3
    sudo update-alternatives --config ruby

再次执行

    ruby -v

发现版本已经变成了1.9.3。

Trouble Shooting：执行命令jekyll时候出现了如下信息：
    /var/lib/gems/1.9.1/gems/execjs-2.2.1/lib/execjs/runtimes.rb:51:in `autodetect': Could not find a JavaScript runtime. See https://github.com/sstephenson/execjs for a list of available runtimes. (ExecJS::RuntimeUnavailable)
......

这是因为没有安装javascript运行时环境，执行命令

    sudo apt-get install nodejs

之后进入github pages的根目录，执行命令

    jekyll serve --watch

安装完成！
