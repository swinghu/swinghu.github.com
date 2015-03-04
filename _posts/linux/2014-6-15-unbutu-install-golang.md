---
layout: post
title: Ubuntu 安装Go-lang
description: Ubuntu 安装Go-lang,以及配置相关文件
category: linux
---


#ubuntu下安装go-lang


1. 下载go-lang安装包
       
1. 解压缩文件并移动到指定目录/usr/local/go
	
	    tar -zxvf go1.2.1.linux-386.tar.gz
    	mov go /usr/local/go
1. 安装，修改配置文件
添加GOPATH,GOROOT,PATH,GOBIN路径
最后修改文件如下![](http://i.imgur.com/P9wQChr.png)

1. 验证配置是否成功，测试代码


    	package mainEEEEE
    	import "fmt"
    	func main(){
    
    		fmt.Printf("Hello World! \n")
    	
    	}
    

5.运行命令：go run hello.go
	

![](http://i.imgur.com/nRIUXWm.png)
    