---
layout: post
title: Vim强制保存文件 
categories: linux
tags: linux tee sudo
keywords: linux,tee,sudo,命令
tagline: Supporting tagline
---
大家都知道vim下保存文件是w命令，但是如果文件编辑需要root权限，但是在打开文件的时候没有使用sudo命令，这样在编辑之后就会无法保存，因为没有权限，有时候改了很多行的文件就浪费了，下面这个命令可以帮助在这种情况下强制保存文件。
    
    w !sudo tee %

    sudo - 使用root权限进行操作
    tee - 从标准输入设备中读取，写入到标准输出设备，并保存在文件中
    % - 当前打开的文件

所以整条命令的意思就是将w的输出传给tee，通过sudo tee写入到当前文件中。 
