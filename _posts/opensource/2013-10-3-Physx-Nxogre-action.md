---
layout: post
title: 编译安装Physx + NxOgre 遇到的问题
category: coding
tags:physx NxOgre
keywords:
tagline: Supporting tagline
---

##（一）Setting the environmental variable for PhysX

   By setting up an environmental variable for PhysX it allows you to compile NxOgre without changing the paths in the linker and include settings. If you’ve installed Ogre from scratch you may of created an environmental variable for Ogre already.的，现在有了CSS3动画。

####步奏：
<ul>

<li>1. Click the Start button </li>
<li>2. Right Click on the “My Computer” text</li> 
<li>3. Click on the Properties menu item (XP/Vista) or Advanced System Settings link (7) </li>
<li>4. Click on the top tab (XP) or link (Vista/7) named “Advanced”. </li>
<li>5. Click on the “Environmental Variables” button </li>
<li>6. Press New in the User Variables for Username </li>
<li>7. Enter PHYSX_DIR for the Name </li>
<li>8. Enter the full path (minus the appending slash) of your PhysX SDK folder, i.e. C:/Dev/PhysX </li>
<li>9. Press Okay, and press okay again on the previous window. </li>
</ul>

##（二）编译 NxOgre 出错解决
LINK : fatal error LNK1104: cannot open file 'NxCooking.lib'
到安装目录下 查看：
E:/SDK/NVIDIA PhysX SDK/v2.8.1/SDKs/lib/Win32下
发现只有：
NxCharacter.lib
PhysXLoader.lib
PhysXCooking.lib
进而将进行一下改名：
rename the PhysXCooking to NxCooking


进而编译成功！

根据 Physx SDK 的版本不同 win32 下的库文件为：

Libraries listed in the file are:
NxCharacter.lib
NxCharacterCHECKED.lib
PhysXCooking.lib
PhysXCookingCHECKED.lib
PhysXCore.lib
PhysXLoader.lib
PhysXLoaderCHECKED.lib
