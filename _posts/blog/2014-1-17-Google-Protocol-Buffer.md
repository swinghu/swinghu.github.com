---
layout: post
title: Google Protocol Buffer Java学习
description: Google Protocol Buffer,Java
category: blog
---

##Google Protocol Buffer 

>### What Are Protocol Buffers? ----[Developer Guide][develop_guide]
>    `Protocol buffers are Google's language-neutral, platform-neutral, extensible mechanism for serializing structured data – think XML, but smaller, faster, and simpler. You define how you want your data to be structured once, then you can use special generated source code to easily write and read your structured data to and from a variety of data streams and using a variety of languages – Java, C++, or Python.
>The `[download][pb_download] `provides the complete source code for the protocol buffer compiler and all the classes your generated code needs, together with building and installation instructions.`
###How do I start?
>`Download and install the package.
>Read the overview.
>Try the tutorial for your favourite language.
>`

##一个简单的例子
###安装 Google Protocol Buffer
本文开发平台为windows7操作系统，直接下载网站发布的windows binary版本。
在[网站][web_site]上可以下载 Protobuf ,例如选择这个版本`“protoc-2.5.0-win32.zip	 Protocol Buffers 2.5.0 compiler -- Windows binary   Featured”`。当然你也可以选择其他版本，如linux,在Linux中编译源码安装`Protocol Buffer`。

###关于简单例子的描述
我打算使用 Protobuf 和 Java 开发一个十分简单的例子程序。
该程序由两部分组成。这两个部分共同完成一个类似于电话簿的程序，实现向电话簿中添加信息，和读取信息。第一部分被称为 `AddPerson`，第二部分叫做` ListPeople`。
`AddPerson`  负责将一些结构化的数据写入一个磁盘文件，如本例中的文件 23 
`ListPeople` 则负责从该磁盘文件中读取结构化数据并打印到屏幕上。
准备用于演示的结构化数据是 `addressbook.proto`，它包含两个基本数据：
<ul>
<li>name，为一个string数据类型</li>
<li>id，这是int32</li>
<li>email，字符串数据类型</li>
</ul>
清单 `addressbook.proto`文件

    package tutorial;

    option java_package = "com.example.tutorial";
    option java_outer_classname = "AddressBookProtos";

    message Person {
      required string name = 1;
      required int32 id = 2;
      optional string email = 3;

      enum PhoneType {
        MOBILE = 0;
        HOME = 1;
        WORK = 2;
      }

    message PhoneNumber {
        required string number = 1;
        optional PhoneType type = 2 [default = HOME];
      }

      repeated PhoneNumber phone = 4;
    }
    message AddressBook {
      repeated Person person = 1;
    }
在上例中，package 名字叫做 `tutorial`，定义了三个消息`Person,PhoneNumber,AddressBook`，三个所定义的数据类型可以见上面的清单
 `addressbook.proto`文件，清单
`addressbook.proto`文件已经清楚的给出。该文件编译后，生成的java文件所在的包为：`java_package=com.example.tutorial`，这条代码的意思就是所生成的java类文件名为`AddressBookProtos.java `所在的包应该是`com.example.tutorial`,所生成的java类文件名为`AddressBookProtos`(就是最后生成一个AddressBookProtos.java文件)
###编译 .proto 文件
写好`proto`文件之后就可以用 `Protobuf `编译器将该文件编译成目标语言了。本例中我们将使用Java语言。

1.将`protoc.exe`文件拷贝到 `C:/Windows`目录下
各文件目录结构如下：
![synchronizes-with](/images/protocolbuffer/dir_of_protobuf_file.png) 
其中`addressbook.proto`文件在`message`文件夹内

2.执行编译命令

    D:\Twisted\java> protoc -I=D:/Twisted/java/message --java_out=D:/Twisted/java/src "D:/Twisted/java/message/addressbook.proto"    
![synchronizes-with](/images/protocolbuffer/compiler_prot_file.png)
如果没有错误，那么就会在本地磁盘目录`D:/Twisted/java/src`中找到一个为com的子文件夹，依次打开子文件夹(路径为：`D:\Twisted\java\src\com\example\tutorial`)就可以找到`AddressBookProtos.java`这个文件，该文件就是`protobuffer`为我们生成的，就是我们需要的`java`文件

###编写 `AddPerson`和`ListPeople`
如前所述， `AddPerson` 将把一个结构化数据写入磁盘，以便其他人来读取。
`ListPeople`将读从本地文件中读取结构化数据，并将其打印出来。
两个Java文件具体的代码如下.

清单 `AddPerson.java`文件

    package com.example.tutorial;
    import com.example.tutorial.AddressBookProtos.AddressBook;
    import com.example.tutorial.AddressBookProtos.Person; 
    import java.io.BufferedReader;
    import java.io.FileInputStream;
    import java.io.FileNotFoundException;
    import java.io.FileOutputStream; 
    import java.io.InputStreamReader;  
    import java.io.IOException;  
    import java.io.PrintStream;    
    class AddPerson{    
        // This function fills in a Person message based on user input.    
        static Person PromptForAddress(BufferedReader stdin,PrintStream stdout)throws IOException{      
            Person.Builder person = Person.newBuilder();
            stdout.print("Enter person ID: ");      
            person.setId(Integer.valueOf(stdin.readLine())); //设置ID号码    
            stdout.print("Enter name: ");      
            person.setName(stdin.readLine()); //添加名字
            stdout.print("Enter email address (blank for none): ");      
            String email = stdin.readLine();     //email地址
            if (email.length() > 0){        
                person.setEmail(email);     
            }       
            while (true){        
                stdout.print("Enter a phone number (or leave blank to finish): ");
                String number = stdin.readLine();        
                if (number.length() == 0){          
                    break;        
                }          
                Person.PhoneNumber.Builder phoneNumber = Person.PhoneNumber.newBuilder().setNumber(number);
                stdout.print("Is this a mobile, home, or work phone? ");        
                String type = stdin.readLine();        
                if (type.equals("mobile")){          
                    phoneNumber.setType(Person.PhoneType.MOBILE);    
                } else if (type.equals("home")) {          
                    phoneNumber.setType(Person.PhoneType.HOME);        
                } else if (type.equals("work")) {         
                    phoneNumber.setType(Person.PhoneType.WORK);        
                } else {          
                    stdout.println("Unknown phone type.  Using default.");        
                }          
                person.addPhone(phoneNumber);      
            }        
            return person.build();    
        }      
        // Main function: Reads the entire address book from a file,  adds one person based on user input, 
        //then writes it back out to the same file.    
        public static void main(String[] args) throws Exception{      
            if (args.length != 1) {        
                System.err.println("Usage:  AddPerson ADDRESS_BOOK_FILE");        
                System.exit(-1);      
            }        
            AddressBook.Builder addressBook = AddressBook.newBuilder();        
            // Read the existing address book.      
            try {        
                addressBook.mergeFrom(new FileInputStream(args[0]));      
            } catch (FileNotFoundException e) {        
                System.out.println(args[0] + ": File not found.  Creating a new file.");      
            }        
            // Add an address.      
            addressBook.addPerson(        
                PromptForAddress(new BufferedReader(new InputStreamReader(System.in)), System.out));        
            // Write the new address book back to disk.      
            FileOutputStream output = new FileOutputStream(args[0]);      
            addressBook.build().writeTo(output);     
            output.close();    
        } 
    }

清单 `ListPerson.java`文件

    package com.example.tutorial;
    
    import com.example.tutorial.AddressBookProtos.AddressBook;
    import com.example.tutorial.AddressBookProtos.Person;
    import java.io.FileInputStream;      
        public class ListPeople {    
            // Iterates though all people in the AddressBook and prints info about them.    
            static void Print(AddressBook addressBook) {      
                for (Person person: addressBook.getPersonList()) {        
                    System.out.println("Person ID: " + person.getId());        
                    System.out.println("  Name: " + person.getName());        
                    if (person.hasEmail()) {          
                        System.out.println("  E-mail address: " + person.getEmail());        
                    }          
                    for (Person.PhoneNumber phoneNumber : person.getPhoneList()) {          
                        switch (phoneNumber.getType()) {            
                            case MOBILE:              
                                System.out.print("  Mobile phone #: ");              
                                break;            
                            case HOME:              
                                System.out.print("  Home phone #: ");              
                                break;            
                            case WORK:              
                                System.out.print("  Work phone #: ");              
                            break;          
                        }          
                        System.out.println(phoneNumber.getNumber());        
                    }      
                }    
            }      
            // Main function:  Reads the entire address book from a file and prints all  the information inside.    
            /**
             * @param args
             * @throws Exception
             */
            public static void main(String[] args) throws Exception {      
                if (args.length != 1) {        
                    System.err.println("Usage:  ListPeople ADDRESS_BOOK_FILE");        
                    System.exit(-1);      
                }        
                // Read the existing address book.      
                AddressBook addressBook = AddressBook.parseFrom(new FileInputStream(args[0]));
                //AddressBook addressBook = AddressBook.parseFrom(new FileInputStream("./23"));
                Print(addressBook);    
            }  
    }
###建立`eclipse java`项目
建立一个java项目添加以上文件到工程中，整个工程的文件，包如下所示：
![synchronizes-with](/images/protocolbuffer/projlist.png)
注意添加所需jar包文件：protobuf-java-2.5.0.jar,可点击此处[下载][protobuf_jar]

选运行`AddPerson.java`文件进行添加
![synchronizes-with](/images/protocolbuffer/inputprofile.png)

再运行`ListPerson.java`文件进行内容的显示
![synchronizes-with](/images/protocolbuffer/listprofile.png)
##Protocol Buffer为我们做了什么事情
想了解`Protocol Buffer`为我们做了什么事情，就要看`AddressBookProtos.java`这个文件，在`eclipse`中查看该文件的`Outline`

如下图所示：
![synchronizes-with](/images/protocolbuffer/addressbookoutline.png)
![synchronizes-with](/images/protocolbuffer/addressbookoutline2.png)
从上图可知pb主要为我们生成了一些get方法，方便我们进行操作,整个文件代码长度2000多行。

##Relate reading
<li>一篇介绍Protocol Buffers, Avro, Thrift & MessagePack区别文[文章][pb_thrift].</li>
<li>介绍Thrift vs. Protocol Buffers之间的的[区别][thrift_pb_diff].</li>
<li>介绍使用pb,thrift,MessagePack,Avro构建RPC的[site][pb_rpc].</li>

[develop_guide]: https://developers.google.com/protocol-buffers/docs/overview?hl=zh-CN
[pb_download]: http://code.google.com/p/protobuf/downloads/
[web_site]:http://code.google.com/p/protobuf/downloads/list
[protobuf_jar]:http://grepcode.com/project/repo1.maven.org/maven2/com.google.protobuf/protobuf-java/
[pb_thrift]:http://www.igvita.com/2011/08/01/protocol-buffers-avro-thrift-messagepack/
[thrift_pb_diff]:http://stuartsierra.com/2008/07/10/thrift-vs-protocol-buffers
[pb_rpc]:http://blog.jeoygin.org/2011/09/rpc-framework-protocol-buffers.html
