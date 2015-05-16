---
layout: post
title: Nginx学习手记（一）
category: coding
tags:  nginx
keywords: nginx
tagline: Supporting tagline
---



##(1)Http相关知识：http  method ，请求报文，响应报文格式，状态码
![synchronizes-with](/images/githubpages/1http_method.png)
##(2)web 响应多个用户的四种模型，以及四种IO模型的特点
![synchronizes-with](/images/githubpages/2web_response_model.png)
##(3)异步阻塞模型：select模型，epoll； Apache prefork/worker模式
![synchronizes-with](/images/githubpages/3select_epoll.png)
##(4)高并发实现模式
![synchronizes-with](/images/githubpages/4high_concurency.png)
##(5)Nginx 基于事件，支持边缘触发，mmap，AIO的一种轻量级web服务器的含义？
![synchronizes-with](/images/githubpages/5nginx_base_event_mmap.png)
##(6)Nginx 用作反向代理，以及使用同步机制会带来的缺陷
![synchronizes-with](/images/githubpages/6reverse_proxy.png)
##(7)异步机制，文件断点续传；Nginx模块架构图
![synchronizes-with](/images/githubpages/7nginx_module.png)
##(8) Nginx 与Apache，PHP通信机制
![synchronizes-with](/images/githubpages/8nginx_apache_php_message.png)
##(9)Nginx 源码编译，参数详解以及配置文件nginx.conf文件
![synchronizes-with](/images/githubpages/9nginx_compile_conf_file.png)
##(10)Nginx与PHP协同处理请求分工
![synchronizes-with](/images/githubpages/10ngix_static_php_dinamic.png)
##（11）如何验证你的nginx 的配置是否正确，你可以运行
<li>1.sudo /opt/nginx/sbin/nginx –t</li>
	如 ：root@swinghu ~# /usr/local/nginx/sbin/nginx -t

<li>2.Nginx 重新启动reload ：</li>

	/usr/local/nginx/sbin/nginx 启动
	/usr/local/nginx/sbin/nginx -s reload 重启
	/usr/local/nginx/sbin/nginx -s stop 关闭
	如：root@swinghu ~# usr/local/nginx/sbin/nginx/ -s reload
	
<li>3.Nginx查看连接信息：</li>
编辑nginx.conf 文件：加入

	localtion/nginx_status {
	stub_status on;
	access_log off;
	}
	
在浏览器中输入：127.0.0.1./nginx_status   

