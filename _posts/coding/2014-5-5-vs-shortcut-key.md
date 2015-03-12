---
layout: post
title: vs 快捷键(转)
category: coding
tags:vs 快捷键
keywords:vs 快捷键
tagline: Supporting tagline
---

# vs 快捷键(转) #

  在进行代码开发的时候，我们往往会频繁的使用键盘、鼠标进行协作，但是切换使用两种工具会影响到我们的开发速度，如果所有的操作都可以只用键盘来完成，那开发效率将得到大幅度的提升。因此，灵活地应用 Visual Studio 的键盘快捷键，就可以起到事半功倍的地步。

　　为了便于日后查看，我根据使用的效果分成这么几块：代码编辑、查找与替换、代码美化、代码导航、Visual Studio 窗口和调试，并在最后提供修改默认快捷键的方法。同时，在参考了资源[2]的文章后，发现使用动画演示不仅直观而且更方便于日后回忆，因此也尝试用 Gif 录制软件为快捷键配上了动画演示。

 

　　本文所介绍的快捷方式适用于 C#。对于其它语言的使用者，请酌情参考。

代码编辑

　　快速选中引号之间的东东

　　将光标放在左引号的左侧，然后双击。如果使用了@符号或者字符串有换行，则只能放在@左侧。![](http://images.cnitblog.com/i/30991/201405/011322190805760.gif)

区块选择、编辑

　　按住 Alt 键，然后用鼠标选择某一区块，就可以对这一区块进行复制、粘贴、编辑等操作。
![](http://images.cnitblog.com/i/30991/201405/011322357052873.gif)
　
删除光标所在行

　　Ctrl + Shift + L

　　因为只需要将光标放置在某一行中，即可删除该行，从而节约了选中一行代码所产生的开销。
![](http://images.cnitblog.com/i/30991/201405/011322574701888.gif)

剪切光标所在行

　　Ctrl + X 或 Ctrl + L
![](http://images.cnitblog.com/i/30991/201405/011323550333275.gif)

在光标上下插入空行

　　光标之上 Ctrl + Enter

　　光标之下 Ctrl + Shift + Enter

![](http://images.cnitblog.com/i/30991/201405/011324190952192.gif)

重命名

　　F2

　　很强大的重命名，可以帮助我们把所有引用到该对象的地方都进行修改，从而减少因忘记修改而导致的错误。
![](http://images.cnitblog.com/i/30991/201405/011324416274309.gif)

　强迫智能感知

　　Ctrl + J
![](http://images.cnitblog.com/i/30991/201405/011325165483078.gif)

强迫显示方法重载参数

　　Ctrl + Shift + Space

![](http://images.cnitblog.com/i/30991/201405/011325445337127.gif)

注释代码

　　Ctrl + E, Ctrl + Ｃ
![](http://images.cnitblog.com/i/30991/201405/011326049083386.gif)

反注释代码

　　Ctrl + E, Ctrl + Ｕ

![](http://images.cnitblog.com/i/30991/201405/011326211735454.gif)


　将当前行下移

　　Alt + Shift + T
![](http://images.cnitblog.com/i/30991/201405/011326387058710.gif)

打开智能标记

　　Shift + Alt + F10 或者  Ctrl + . (点)

　　感谢 @Bce 的补充，差点遗忘了这个很有用的快捷键。

　　当你在编辑器中输入的内容发生改变或出现问题的时候，你会看到这些内容下面出现了一个小短横，当鼠标移动当小短横上后，就可以展开这个标记，这是 VS 在提示你当前可以执行的操作，比如当你修改一个变量名的时候，它会提示你是否要替换所有引用到的地方，又比如你添加的某一个类的名称空间没有引用进来，那它会提示你是否要把这个名称空间引用进来。
![](http://images.cnitblog.com/i/30991/201405/012047176894003.gif)


## 查找与替换 ##

　　在当前文档内进行查找

　　Ctrl + F
![](http://images.cnitblog.com/i/30991/201405/011326584393840.gif)

在当前文档内，直接使用上次搜索的关键字进行查找

　　向下查找 F3
![](http://images.cnitblog.com/i/30991/201405/011327216429627.gif)

　向上查找 Shift + F3

![](http://images.cnitblog.com/i/30991/201405/011327380808683.gif)

　在当前文档内进行替换

　　Ctrl + H

## 代码美化 ##

　　格式化代码片段

　　Ctrl + E, Ctrl + F
![](http://images.cnitblog.com/i/30991/201405/011328060643733.gif)

格式化整个文档

　　Ctrl + E, Ctrl + D
![](http://images.cnitblog.com/i/30991/201405/011328220029001.gif)

## 代码导航 ##

　　折叠/展开代码块

　　Ctrl + M, Ctrl + M
![](http://images.cnitblog.com/i/30991/201405/011328418146388.gif)

转到定义

　　F12

　　可以快速帮我们把光标定位到变量定义或类型定义的地方
![](http://images.cnitblog.com/i/30991/201405/011329288924036.gif)

查找引用

　　Shift +　F12

　　可以快速找到所有使用了该对象的地方
![](http://images.cnitblog.com/i/30991/201405/011330011891805.gif)

定位到

　　Ctrl + ,

　　使用场景示例，项目结构复杂，类型数量庞大，突然想看一下某个自定义的枚举的成员，但在当前打开的文件中无法快速找到哪里使用了此枚举，这个时候可以通过Ctrl + , 快速定位到定义此枚举的文件。
![](http://images.cnitblog.com/i/30991/201405/011330221275933.gif)

定位到某一行

　　Ctrl + G
![](http://images.cnitblog.com/i/30991/201405/011330433614321.gif)

　定位到下一个括号

　　Ctrl + ]

　　当某一括号（{}、（）、[]）中的内容很长，导致无法在迅速定位到另一端的时候，可以使用该快捷键。使用时，需要先将光标放在其中一侧括号的一旁（左、右都可）。
![](http://images.cnitblog.com/i/30991/201405/011331119869499.gif)

　定位到文档头、尾

　　Ctrl + Home | Ctrl + End

![](http://images.cnitblog.com/i/30991/201405/011331304861685.gif)

定位到上、下一次编辑的位置

　　上一次位置 Ctrl + -

　　下一次位置 Ctrl + Shift + -

![](http://images.cnitblog.com/i/30991/201405/011331473612341.gif)


定位到上一个高亮的引用

　　Ctrl + Shift + 上、下箭头

　　当你光标定位在某一个单词的时候，Visual Studio 会智能把所有该单词出现的地方都高亮起来，这个时候你可以使用如下快捷键在这几个高亮的单词间进行跳转。

![](http://images.cnitblog.com/i/30991/201405/011332111115929.gif)

## Visual Stuido 窗口 ##

　　切换选项卡

　　Ctrl + Tab
![](http://images.cnitblog.com/i/30991/201405/011332337832089.gif)

关闭当前选项卡

　　Ctrl + F4
![](http://images.cnitblog.com/i/30991/201405/011332538301547.gif)

## 调试 ##

　　编译整个解决方案

　　F6 

 

　　编译并运行

　　F5

 

　　设置或取消断点

　　F9

 

## 修改快捷键 ##

　　如果觉得预设的快捷键不好用，可以通过 工具 / 选项 / 键盘 进行调整。

 

　　1. 找到想要修改的快捷键，并移除原来的快捷键设置。
　　 ![](http://images.cnitblog.com/i/30991/201405/011333366894908.jpg)
　　 ![](http://images.cnitblog.com/i/30991/201405/011334006584796.jpg)
  2. 填入自己想要的快捷键，点击 “分配”。
   ![](http://images.cnitblog.com/i/30991/201405/011334134559505.jpg)
   Gif 动画演示
   ![](http://images.cnitblog.com/i/30991/201405/011334318451191.gif)

参考资源

    [1]. 预定义键盘快捷键

    [2]. Visual Studio 常用快捷键

 

　　本文来源于 《[Visaul Studio 常用快捷键的动画演示](http://blog.chenxu.me/post/detail?id=0543017f-1c98-4bd6-b87c-8bd19b4d752c)》

  作者：[stg609](http://blog.chenxu.me/)