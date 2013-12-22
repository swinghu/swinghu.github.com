---
layout: post
title: Linux Shell编程
category: blog
description: Shell是用户与Linux操作系统沟通的桥梁，是每一个Linux用户的必修功课之一。
---

##1、 Linux 脚本编写基础

##1.1	基本语法介绍

###1.1.1	开头

Shell程序必须以下面的行开始(首行)
	
	$ #!/bin/sh
例如：命令vi test.sh进入vi编辑页面输入
	
	$ #!/bin/sh
	$ echo“hello world"
编辑好后，进入vi的命令模式(按ESC键)，按下wq保存退出，此时还不能运行该shell命令，因为该文件还没有执行权限，要使得
该脚本可以执行运行
	
	$ chmod +x test.sh		//添加可执行权限

###1.1.2	注释
进行shell编程时，shell中的注释以#开头，直到该行末尾

###1.1.3	变量

shell可以不先声明变量，就可以使用，例如
	
	$ csv =".csv"
	$ echo $csv
	$ for((i=0; i<10;i++))
	
###1.1.4	常用shell命令(重点grep，awk，sed)

	$ echo "some text": 将文字内容打印在屏幕上
	$ ls: 文件列表
	$ wc –l filewc -w filewc -c file: 计算文件行数计算文件中的单词数计算文件中的字符数
	$ cp sourcefile destfile: 文件拷贝
	$ mv oldname newname : 重命名文件或移动文件
	$ rm file: 删除文件
	$ grep 'pattern' file: 在文件内搜索字符串比如：grep 'searchstring' file.txt
	$ cut -b colnum file: 指定欲显示的文件内容范围，并将它们输出到标准输出设备比如：输出每行第5个到第9个字符cut -b5-9 file.txt千万不要和cat命令混淆(注意如果要输出某行中的某个字段(例如字符串"16，14，mfa，-0.159"，求mfa)
	$ cat dataout.txt: 输出文件内容到标准输出设备（屏幕）上
	$ file somefile: 得到文件类型
	$ read var: 提示用户输入，并将输入赋值给变量(从控制台输入)
	$ sort file.txt: 对file.txt文件中的行进行排序(好强大)
	$ uniq: 删除文本文件中出现的行列比如： sort dataout.txt | uniq
	
	$ expr: 进行数学运算Example: add 2 and 3 expr 2 "+" 3
	$ find: 搜索文件比如：根据文件名搜索find . -name filename -print
	$ tee: 将数据输出到标准输出设备(屏幕) 和文件比如：somecommand | tee outfile(有点与符号“>"类似)
	$ basename file: 返回不包含路径的文件名比如：basename /home/swinghu/txtfile 将返回 txtfile
	$ dirname file: 返回文件所在路径比如：dirname /home/swinghu/txtfile 将返回 /home/swinghu
	$ tail file : 打印文本文件末尾几行
	$ sed: Sed是一个基本的查找替换程序。可以从标准输入（比如命令管道）读入文本，并将结果输出到标准输出（屏幕）。该命令采用正则表达式（见参考）进行搜索。
	$ awk: awk 用来从文本文件中提取字段。缺省地，字段分割符是空格，可以使用-F指定其他分割符。cat file.txt | awk -F, '{print $1 "," $3 }'这里我们使用，作为字段分割符，同时打印第一个和第三个字段。如果该文件内容如下： Adam Bor, 34, IndiaKerry Miller, 22, USA命令输出结果为：Adam Bor, IndiaKerry Miller, USA
	
###1.1.5	管道 重定向 backtick

(1)管道(|)可以用来将一个命令的输出作为另一个命令的输入，或者输出该命令执行结果到指定文件，如:
	
	$ ./shell_program_name -i [value] -n [value] -d [value] | dataout.txt
	$ grep "hadoop" hadoop.config |wc -l  //在hadoop.config文件中搜索”hadoop“，并且grep输出作为wc命令的输入，最后统计出现行数
	
(2)重定向(>)可以将命令的结果输出到文件，而不是标准输出(控制台)
	
	$ ./shell_program_name -i [value] -n [value] -d [value] > dataout.txt
	$ ./mrmr -i 2.csv -t 0.5 >outputfile.txt
	
###1.1.6	控制流程语句
(1)字符串的比较(注意字符串之间的空格)
	
	if(str1 = str2)		当两个串有相同内容、长度时为真   
	if(str1 != str2)	当串str1和str2不等时为真    
	if(-n str1)	  		当串的长度大于0时为真(串非空)    
	if(-z str1)  		当串的长度为0时为真(空串)    
	if(str1)			当串str1为非空时为真
    
(2)整数之间的比较

	int1 -eq int2　　　　两数相等为真
	int1 -ne int2　　　　两数不等为真   
	int1 -gt int2　　　　int1大于int2为真   
	int1 -ge int2　　　　int1大于等于int2为真    
	int1 -lt int2　　　　int1小于int2为真    
	int1 -le int2　　　　int1小于等于int2为真 
   
(3)逻辑组合条件测试(and 、or 、not)

	-a     与    
	-o     或    
	!      非 
(4)嵌套if语句

	if command 
		then 
			command 
		else 
			if command 
			then 
				command 
			else 
			if command 
				then 
					command 
			fi 
		fi 
	fi

(4)case语句

	case value in    
		pattem 1)    
			command    
		command;;    
		pattem 2)    
			command    
		command;;    
		....    
		pattem)    
			command;    
	esac

(4)for语句的各种写法
第一种写法

	for 变量名 in 列表  
	do  
		命令1  
		命令2…  
	done  
	
例如：

	for I in {1..100}; 
	do 
		if [ $[$I%2] -eq 0 ]; then 
			let sum1+=$I 
		else 
			let sum2+=$I 
		fi 
	done 

遍历目录下的文件：

	#!/bin/bash
	for x in /var/log/*
	do
        #echo "$x is a file living in /var/log"
        echo $(basename $x) is a file living in /var/log
	done
	
第二种写法

	for (( count=0; count < 100; count++ ))
		do
		...
	done
	注意”((“与count有空格
	
例如

	for (( i=1; i<=5; i++ ))
		do
			echo "i=$i"
	done
	
(5)while语句
	while true
		do
		语句
	done
	
例如

	#!/bin/sh
	var=1
	while (( $var <= 3 ))
	do
		echo $var
		var=$(($var + 1))
	done

下文待续
	
