---
layout: post
title: tar命令常用参数 
categories: linux
tags: linux tar
keywords: linux,tar,命令,参数
tagline: Supporting tagline
---
    tar -[c|x|t|u|r][z|j][v]f <打包文件> 文件 [-C <路径>]

    -c 创建文档
    -x 解压文档
    -t 查看文档
    -u 更新文档
    -r 添加文档

    -z 使用gz压缩格式
    -j 使用bz2压缩（压缩率高，耗时长）

    -v 显示执行过程

    -f 后面直接跟要执行的文件名称

    -C 将压缩文件解压到指定目录
