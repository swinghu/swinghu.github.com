---
layout: post
title: CEGUI + Ogre 安装设置详解
category: coding
tags:netstat CEGUI Ogre
keywords:
tagline: Supporting tagline
---

这是《OGRE 3D 1.7 Beginner's Guide》学习笔记，再加一点自己的认识。推荐学习ogre的新手此书

- 英文版：[《OGRE 3D 1.7 Beginner's Guide》][RCEN]


##ogre 1.7.0的下载、配置和编译指南

<ul>
<li>1. ogre 1.7.0的下载地址：https://sourceforge.net/projects/ogre/files/ogre/1.7/ogre-v1-7-0.zip/download</li>

<li>2. ogre 1.7.0依赖库的下载地址（不定期更新，请关注该贴）：http://www.ogre3d.org/forums/viewtopic.php?f=1&t=54533</li>

<li>3. 将ogre解压，建议将解压后生成的ogre目录改名为对应的版本号，例如：F:/SDK/ogre-v1-7-0，以区分各个版本</li>

<li>4. 将依赖库解压到ogre的目录中，例如：F:/SDK/ogre-v1-7-0/Dependencies</li>

<li>5. 根据自己的VC版本打开F:/SDK/ogre-v1-7-0/Dependencies/src目录中对应的工程VS20XX.sln</li>

<li>6. 编译出依赖库的debug和release</li>

<li>7. 下载最新版本的cmake：http://www.cmake.org/cmake/resources/software.html</li>

<li>8. 解压cmake到任意目录，例如：F:/Tools/cmake-2.8.0-win32-x86</li>

<li>9. 运行F:/Tools/cmake-2.8.0-win32-x86/bin/cmake-gui.exe</li>

<li>10. 在"Where is the source code"和"Where to build the binaries"中分别设置ogre的解压路径，例如：F:/SDK/ogre-v1-7-0</li>

<li>11. 点击configure，选择好VC的版本</li>

<li>12. 点击Generate后将生成OGRE.sln</li>

<li>13. 编译出ogre的debug和release</li>

<li>14. 如果不需要运行samples，那么只需要编译OgreMain、RenderSystem_Direct3D9（或其他）和所需的Plugin即可 </li>
</ul>


##cegui 0.7.1的下载、配置和编译指南


<ul>
<li>1. cegui 0.7.1的下载地址：http://prdownloads.sourceforge.net/crayzedsgui/CEGUI-0.7.1.zip?download</li>

<li>2. cegui 0.7.1依赖库的下载地址：http://prdownloads.sourceforge.net/crayzedsgui/CEGUI-DEPS-0.7.x-r1-vc9.zip?download</li>

<li>3. 将cegui解压，建议将解压后生成的cegui目录改名为对应的版本号，例如：F:/SDK/cegui-v0-7-1，以区分各个版本</li>

<li>4. 将依赖库解压到cegui的目录中，例如：F:/SDK/cegui-v0-7-1/Dependencies</li>

<li>5. 进入目录F:/SDK/cegui-v0-7-1/projects/premake</li>

<li>6. 用记事本打开目录下的config.lua，找到两个变量：OGRE_PATHS和OIS_PATHS</li>

<li>7. 将其修改成对应的ogre和ois的路径，例如：</li>

	OGRE_PATHS = { "F:/SDK/ogre-v1-7-0", "OgreMain/include", "lib" }
	OIS_PATHS = { "F:/SDK/ogre-v1-7-0/Dependencies/include/OIS/", "", "lib" }

<li>8. 找到CEGUI_OLD_OIS_API变量，设置为false</li>

<li>9. 找到OGRE_RENDERER变量，设置为true</li>

<li>10. 找到SAMPLES_OGRE变量，设置为true</li>

<li>11. 进入目录F:/SDK/cegui-v0-7-1/projects/premake，运行build_vs2008.bat（或对应的其他版本），你将看到CEGUI.sln</li>

<li>12. 继续运行build_samples_vs2008.bat（或对应的其他版本），你将看到CEGUISamples.sln</li>

<li>13. 在编译CEGUI.sln和CEGUISamples.sln时，如果依然存在找不到h或是link错误，请打开工程属性，修改Additional Include Directories和Additional Library Directories中对应的ogre和ois相关的路径</li>

<li>14. 请注意ogre 1.7.0的lib是生成在debug和release子目录中，记得修改为正确的link路径</li>

<li>15. 运行sample前，记得先复制F:/SDK/cegui-v0-7-1/dependencies/bin下的所有dll到F:/SDK/cegui-v0-7-1/bin下面，这样就不会报错提示缺少dll了</li>
</ul>

- 英文版：[《OGRE 3D 1.7 Beginner's Guide》][RCEN]


[RCEN]: http://book.douban.com/subject/5949822/ "OGRE 3D 1.7 Beginner's Guide"

