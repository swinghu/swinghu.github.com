---
layout: post
title: 查看windows端口占用信息
category: life
tags:netstat windows 端口
keywords:windows port
tagline: Supporting tagline
---


netstat命令来自linux定义：
> netstat - Print network connections, routing tables, interface statistics, masquerade connections, and multicast memberships
|命令参数|注释|
|-a	| Displays all active connections and the TCP and UDP ports on which the computer is listening.|
|-b (Windows)|	Displays the binary (executable) program's name involved in creating each connection or listening port. (Windows XP, 2003 Server and newer Windows operating systems; not Microsoft Windows 2000 or older).|
|-b (OS X, NetBSD)|	Causes -i to report the total number of bytes of traffic.|
|-e|	Displays ethernet statistics, such as the number of bytes and packets sent and received. This parameter can be combined with -s.|
|-f (Windows)|	Displays fully qualified domain names <FQDN> for foreign addresses (only available on Windows Vista and newer operating systems).|
|-f Address Family (FreeBSD) |	Limits display to a particular socket address family, unix, inet, inet6|
|-g|	Displays multicast group membership information for both IPv4 and IPv6 (may only be available on newer operating systems)|
|-i|	Displays network interfaces and their statistics (not available under Windows)|
|-m|	Displays the memory statistics for the networking code (STREAMS statistics on Solaris).|
|-n|	Displays active TCP connections, however, addresses and port numbers are expressed numerically and no attempt is made to determine names.|
|-o (Windows)|	Displays active TCP connections and includes the process ID (PID) for each connection. You can find the application based on the PID on the Processes tab in Windows Task Manager. This parameter can be combined with -a, -n, and -p. This parameter is available on Microsoft Windows XP, 2003 Server (and Windows 2000 if a hotfix is applied).[6]|
|-p protocol (Windows and BSD)|	Shows connections for the protocol specified by protocol. In this case, protocol can be tcp, udp, tcpv6, or udpv6. If this parameter is used with -s to display statistics by protocol, protocol can be tcp, udp, icmp, ip, tcpv6, udpv6, icmpv6, or ipv6.|
|-p (Linux)	|Show which processes are using which sockets (similar to -b under Windows) (you must be root to do this)|
|-P protocol (Solaris)|	Shows connections for the protocol specified by protocol. In this case, protocol can be ip, ipv6, icmp, icmpv6, igmp, udp, tcp, or rawip.|

|-r	|Displays the contents of the IP routing table. (This is equivalent to the route print command under Windows.)|

|-s	|Displays statistics by protocol. By default, statistics are shown for the TCP, UDP, ICMP, and IP protocols. If the IPv6 protocol for Windows XP is installed, statistics are shown for the TCP over IPv6, UDP over IPv6, ICMPv6, and IPv6 protocols. The |-p |parameter can be used to specify a set of protocols.|
|-t (Linux)	| Display only TCP connections.|
|-W (FreeBSD)|	Display wide output - doesn't truncate hostnames or IPv6 addresses|
|-v (Windows)|	When used in conjunction with -b it will display the sequence of components involved in creating the connection or listening port for all executables.|
Interval	Redisplays the selected information every Interval seconds. Press CTRL+C to stop the redisplay. If this parameter is omitted, netstat prints the selected information only once.|
|-h (unix)
/? (windows)|	Displays help at the command prompt.|

常用命令

netstat -a 列出所有端口
netstat -at 列出所有tcp端口
netstat -au 列出所有udp端口
netstat -l 只显示监听端口
netstat -lt 列出所有监听tcp端口
netstat -lu 列出所有监听udp端口
netstat -p 同时显示pid和进程名称
netstat -ano查看端口占用列表

netstat -ap | grep ssh 找出程序运行的端口
netstat -ano|findstr "443"         //搜索443端口占用情况，并找到进程ID

tasklist查看该端口对应任务名称
tasklist|findstr "3084"                     //查找PID为720对应的进程名


例如，某次在安装WMware的时候提示443端口被占用，怎样找出那个应用程序占用？

首先运行：netstat -ano|findstr "443"

	C:\Users\swinghu-pc>netstat -ano|findstr "443"
	  TCP    0.0.0.0:443            0.0.0.0:0              LISTENING       3084
	  TCP    192.168.10.113:1931    74.125.26.84:443       SYN_SENT        6584
	  TCP    192.168.10.113:1932    74.125.26.84:443       SYN_SENT        6584
	  TCP    192.168.10.113:1934    64.233.189.31:443      SYN_SENT        6584
	  TCP    192.168.10.113:1936    64.233.189.31:443      SYN_SENT        6584
	  TCP    [::]:443               [::]:0                 LISTENING       3084

然后运行：tasklist|findstr "3084"

	C:\Users\swinghu-pc>tasklist|findstr "3084"
	VisualSVNServer.exe           3084 Services                   0      8,724 K


参考
netstat(8) - Linux man page   http://linux.die.net/man/8/netstat
netstat                       http://en.wikipedia.org/wiki/Netstat
