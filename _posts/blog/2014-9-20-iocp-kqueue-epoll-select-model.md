---
layout: post
title: IOCP,kqueue,epoll 概述
description: IOCP,kqueue,epoll,select模型，阻塞/非阻塞，同步/异步
category: blog
---
服务器都是跨平台的，window下面用iocp,linux下用epoll,或者poll+多线程。 

**epoll 与 IOCP**
相同点
+ 	（1）异步，高效
+ 	（2）都可以通过指针携带应用层数据，IOCP通过单句柄和单IO数据与IOCP底层通信，epoll通过epoll_data里的“void *ptr”来传递
+ 	（3）不仅在事件到来时，告诉你发生了什么，而且同时告诉你这次事件所操作的数据是哪些。

不同点
+ （1）epoll工作原理：如果你想进行IO操作，先向epoll查询是否可以读写，处于可以读写状态后，epoll会通过epoll_wait函数通知你。
+ （2）IOCP工作原理：IOCP是在IO完成后，才通过get函数返回这个完成通知，epoll则不是在IO操作完成后通知你。
+ （3）epoll仅仅是一个异步事件通知机制，本身不做任何IO操作，与IO之间彼此独立。
+ （4）IOCP不仅完成之后的事件通知，同时自己还封装了部分IO控制逻辑


//Todo
**windows下的四种模型 IOCP，select,event....**