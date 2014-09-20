---
layout: post
title: 编译安装OpenSSL
description: OpenSSL安装，perl
category: blog
---
# 编译安装OpenSSL#
**（1）下载 ActivePerl。**选择版本5.18.2.1802-MSWin32-x86-64int-298023 地址[ActivePerl-5.18.2.1802-MSWin32-x86-64int-298023](ActivePerl-5.18.2.1802-MSWin32-x86-64int-298023)，安装时，一路点击下一步就行，注意选择勾选将其添加到系统环境变量path中。验证是否安装成功，并且bin目录已经在path环境变量中。perl -v 测试一下,如出现以下结果表明现在已经安装配置好。

	C:\openssl-1.0.1>perl -v
	This is perl 5, version 18, subversion 2 (v5.18.2) built for MSWin32-x86-multi-t
	hread-64int
	(with 1 registered patch, see perl -V for more detail)
	
	Copyright 1987-2013, Larry Wall
	
	Binary build 1802 [298023] provided by ActiveState http://www.ActiveState.com
	Built Apr 14 2014 15:40:28
	
	Perl may be copied only under the terms of either the Artistic License or the
	GNU General Public License, which may be found in the Perl 5 source kit.
	
	Complete documentation for Perl, including FAQ lists, should be found on
	this system using "man perl" or "perldoc perl".  If you have access to the
	Internet, point your browser at http://www.perl.org/, the Perl Home Page.

**（2）下载OpenSSL。**选择版本 openssl-1.0.1i.tar.gz [下载地址](ftp://ftp.openssl.org/source/openssl-1.0.1i.tar.gz)。这里在选择版本的时候要注意，版本尽量选择最新版本（最新版为1.0.2 处于beta阶段）初学不要选用snapshot版本的。要不然和我一样会出现很多诡异的问题，如。

	tmp32dll/sha512-586.asm(288) : error A2008:  : mm
	tmp32dll/sha512-586.asm(289) : error A2008:  : mm
	tmp32dll/sha512-586.asm(290) : error A2008:  : mm
	tmp32dll/sha512-586.asm(291) : error A2008:  : mm
	tmp32dll/sha512-586.asm(292) : error A2008:  : mm
	tmp32dll/sha512-586.asm(293) : error A2008:  : mm
	tmp32dll/sha512-586.asm(294) : error A2008:  : mm
	tmp32dll/sha512-586.asm(295) : error A2008:  : mm
	NMAKE : fatal error U1077: 'ml' : return code '0x1'
	Stop.

遇到"NMAKE : fatal error U1077: 'ml' : return code '0x1'
Stop." 问题后，不管怎么搜教程，我都都没有解决掉。最后选择了其他版本。下载后解压（7zip）,解压到：C:\openssl-1.0.1。
**（3）编译OpenSSL。**
cd到解压目录C:\openssl-1.0.1，运行：

	per Configure VC-WIN32
显示配置信息：

	Configuring for VC-WIN32
    no-ec_nistp_64_gcc_128 [default]  OPENSSL_NO_EC_NISTP_64_GCC_128 (skip dir)
    no-gmp          [default]  OPENSSL_NO_GMP (skip dir)
    no-jpake        [experimental] OPENSSL_NO_JPAKE (skip dir)
    no-krb5         [krb5-flavor not specified] OPENSSL_NO_KRB5
    no-md2          [default]  OPENSSL_NO_MD2 (skip dir)
    no-rc5          [default]  OPENSSL_NO_RC5 (skip dir)
    no-rfc3779      [default]  OPENSSL_NO_RFC3779 (skip dir)
    no-sctp         [default]  OPENSSL_NO_SCTP (skip dir)
    no-shared       [default]
    no-store        [experimental] OPENSSL_NO_STORE (skip dir)
    no-unit-test    [default]  OPENSSL_NO_UNIT_TEST (skip dir)
    no-zlib         [default]
    no-zlib-dynamic [default]
	IsMK1MF=1
	CC            =cl
	：：：：：：：：：：：：：：：：：：：：：：：：：：：：：：：：
	：：：：：：：：：：：：：：：：：：：：：：：：：：：：：：：：
	：：：：：：：：：：：：：：：：：：：：：：：：：：：：：：：：
	ENGINES_OBJ   =
	PROCESSOR     =
	RANLIB        =true
	ARFLAGS       =
	PERL          =perl
	THIRTY_TWO_BIT mode
	BN_LLONG mode
	RC4_INDEX mode
	RC4_CHUNK is undefined
	
	Configured for VC-WIN32.x


 选择[开始]->[microsoft visual studio 2013]选择visual studio tools,选择后将会打开发者工具开文件夹，选择：VS2013 x86 本机工具命令提示。点击进入命令提示行dos界面。进入vc/bin 目录中运行命令，设置环境变量：

	vcvars32.bat
控制台出现停顿一会，进入下一行，标识已经配置好。
通过VS2013 x86 本机工具命令提示 的命令工具 cd到OpenSSL目录中，创建makefile文件，输入命令：

	ms\do_ms
虽然有其他命令，例如，如果使用MASM，接着输入：ms\do_masm
如果使用NASM，接着输入：ms\do_nasm，但是需要安装相应其他软件，本人没有试用，这里就不在介绍。
运行改命令后：

	C:\openssl-1.0.1>ms\do_ms
	C:\openssl-1.0.1>perl util\mkfiles.pl  1>MINFO
	
	C:\openssl-1.0.1>perl util\mk1mf.pl no-asm VC-WIN32  1>ms\nt.mak
	
	C:\openssl-1.0.1>perl util\mk1mf.pl dll no-asm VC-WIN32  1>ms\ntdll.mak
	
	C:\openssl-1.0.1>if x == x goto skipce
	
	C:\openssl-1.0.1>perl util\mkdef.pl 32 libeay  1>ms\libeay32.def
	
	C:\openssl-1.0.1>perl util\mkdef.pl 32 ssleay  1>ms\ssleay32.def

接上，接上条命令，还是在VS2013 x86 本机工具命令提示工具下，运行：
	
	nmake -f ms\ntdll.mak

如果不出错就是漫长的等待，等待其编译。编译的时候，会在OpenSSL目录下的文件夹tmp32dll生成编译等obj文件。最后dll，lib文件将会在outdll文件中找到。至此，编译完成。


（4）测试OpenSSL，一旦能够成功编译，就可以测试是否编译成功。运行命令：

	
	C:\openssl-1.0.1>nmake -f ms\ntdll.mak install
运行该命令，显示系列的测试，加ok字样。

（5）安装OpenSSL，一旦能够成功编译，安装就很简单。运行命令：
	
	C:\openssl-1.0.1>nmake -f ms\ntdll.mak install
	Microsoft (R) 程序维护实用工具 12.00.21005.1 版
	版权所有 (C) Microsoft Corporation。  保留所有权利。

	Building OpenSSL
	
	perl util/mkdir-p.pl "\usr\local\ssl"
	created directory `/usr'
	created directory `/usr/local'
	created directory `/usr/local/ssl'
	        perl util/mkdir-p.pl "\usr\local\ssl\bin"
	created directory `/usr/local/ssl/bin'
	        perl util/mkdir-p.pl "\usr\local\ssl\include"
	created directory `/usr/local/ssl/include'
	        perl util/mkdir-p.pl "\usr\local\ssl\include\openssl"
	created directory `/usr/local/ssl/include/openssl'
	        perl util/mkdir-p.pl "\usr\local\ssl\lib"
	created directory `/usr/local/ssl/lib'
	        perl util/copy.pl "inc32\openssl\*.[ch]" "\usr\local\ssl\include\openss
	"
	Copying: inc32/openssl/aes.h to /usr/local/ssl/include/openssl/aes.h
	Copying: inc32/openssl/applink.c to /usr/local/ssl/include/openssl/applink.c
	Copying: inc32/openssl/asn1.h to /usr/local/ssl/include/openssl/asn1.h
	Copying: inc32/openssl/asn1_mac.h to /usr/local/ssl/include/openssl/asn1_mac.h
	Copying: inc32/openssl/asn1t.h to /usr/local/ssl/include/openssl/asn1t.h
	Copying: inc32/openssl/bio.h to /usr/local/ssl/include/openssl/bio.h
	Copying: inc32/openssl/blowfish.h to /usr/local/ssl/include/openssl/blowfish.h
	Copying: inc32/openssl/bn.h to /usr/local/ssl/include/openssl/bn.h
	Copying: inc32/openssl/buffer.h to /usr/local/ssl/include/openssl/buffer.h
	Copying: inc32/openssl/camellia.h to /usr/local/ssl/include/openssl/camellia.h
	Copying: inc32/openssl/cast.h to /usr/local/ssl/include/openssl/cast.h
	Copying: inc32/openssl/cmac.h to /usr/local/ssl/include/openssl/cmac.h
	Copying: inc32/openssl/cms.h to /usr/local/ssl/include/openssl/cms.h
	Copying: inc32/openssl/comp.h to /usr/local/ssl/include/openssl/comp.h
	Copying: inc32/openssl/conf.h to /usr/local/ssl/include/openssl/conf.h
	Copying: inc32/openssl/conf_api.h to /usr/local/ssl/include/openssl/conf_api.h
	Copying: inc32/openssl/crypto.h to /usr/local/ssl/include/openssl/crypto.h
	Copying: inc32/openssl/des.h to /usr/local/ssl/include/openssl/des.h
	Copying: inc32/openssl/des_old.h to /usr/local/ssl/include/openssl/des_old.h

至此OpenSSL安装完毕

