---
layout: post
title: Docker 是什么？
description: Docker科普，详细介绍Docker
category: blog
---


WHAT IS DOCKER AND WHEN TO USE IT
=================================

![](http://i.imgur.com/dAuXOTh.png)
Heard of Docker, but still having trouble understanding it? Don’t worry, you are not alone. Today, I want to try to explain Docker in a few different ways.

###WHAT ISN’T DOCKER?###


Before we talk about what Docker is, I will talk about what it isn’t. What is the negation of Docker? What are its limits? What can’t Docker do?

Docker is NOT a Linux Container technology (like LXC)
Docker is NOT limited to just LXC anymore (can theoretically manage VMs in the future)
Docker is NOT a Configuration Manager replacement (like Chef, Puppet, SaltStack, etc)
Docker is NOT a PaaS
Docker is NOT good at linking across separate servers or VMs (yet,[ see ambassadors](http://www.centurylinklabs.com/deploying-multi-server-docker-apps-with-ambassadors/))
Docker is NOT good at isolating Linux Containers from each other (shared kernel)
### WHAT IS DOCKER? ###

So then what is Docker good at?

Docker is **great at building and sharing disk images** with others through the Docker [Index](https://index.docker.io/)
Docker is a** manager for infrastructure** (today’s bindings are for Linux Containers, but future bindings including KVM, Hyper-V, Xen, etc.)
Docker is** a great image distribution model** for server templates built with Configuration Managers (like Chef, Puppet, SaltStack, etc)
Docker uses btrfs (a copy-on-write filesystem) to keep track of **filesystem diff’s** which can be committed and collaborated on with other users (like git)
Docker has a **central repository of disk images** (public and private) that allow you to easily run different operating systems (Ubuntu, Centos, Fedora, even Gentoo)
### WHEN TO USE DOCKER? ###

Docker is a basic tool, like git or java, that you should start incorporating into your daily development and ops practices.

Use Docker as **version control system** for your entire app’s operating system
Use Docker **when you want to distribute/collaborate **on your app’s operating system with a team
Use Docker to **run your code on your laptop **in the same environment as you have on your server (try the [building](https://github.com/centurylinklabs/building) tool)
Use Docker whenever your **app needs to go through multiple phases of development** (dev/test/qa/prod, try [Drone](https://drone.io/) or [Shippable](http://shippable.com/), both do Docker CI/CD)
Use Docker with your[ Chef Cookbooks ](http://tech.paulcz.net/2013/09/creating-immutable-servers-with-chef-and-docker-dot-io.html)and [Puppet Manifests](http://puppetlabs.com/blog/building-puppet-based-applications-inside-docker) (remember, Docker doesn’t do configuration management)
### WHAT ALTERNATIVES ARE THERE TO DOCKER? ###

The [Amazon AMI Marketplace](https://aws.amazon.com/marketplace/ref=mkt_ste_amis_redirect?b_k=291) is the closest thing to the [Docker Index](https://index.docker.io/) that you will find. With AMIs, you can only run them on Amazon. With Docker, you can run the images on any Linux server that runs Docker.
The [Warden](https://github.com/cloudfoundry/warden) project is a LXC manager written for Cloud Foundry without any of the social features of Docker like sharing images with other people on the Docker Index

### HOW DOCKER IS LIKE JAVA ###

Java’s promise: Write Once. Run Anywhere.

Docker has the same promise. Except instead of code, you can configure your servers exactly the way you want them (pick the OS, tune the config files, install binaries, etc.) and you can be certain that your server template will run exactly the same on any host that runs a Docker server.

For example, in Java, you write some code:

	 class HelloWorldApp {
	    	public static void main(String[] args) {
	        	System.out.println("Hello World!");
	    		}
	 }

Then run javac `HelloWorld.java`. The resulting `HelloWorld.class` can be run on any machine with a JVM.

In Docker, you write a `Dockerfile`:

	
>	FROM ubuntu:13.10
	
>	ENV DEBIAN_FRONTEND noninteractive
	RUN apt-get update -qq -y && \
	    apt-get install curl -qq -y && \
	    apt-get clean
	
>	RUN curl -sSL https://get.rvm.io | bash -s stable --ruby=2.1.1

Then run `docker build -t my/ruby `. and the resulting container, `my/ruby `can be run on any machine with a Docker server.

The Docker server is like a JVM for systems. It lets you get around the leaky abstraction of Virtual Machines by giving you an abstraction that runs just above virtualization (or even bare metal).

### HOW DOCKER IS LIKE GIT ###

Git’s promise: Tiny footprint with lightning fast performance.

Docker has the same promise. Except instead of for tracking changes in code, you can track changes in systems. Git outclasses SCM tools like Subversion, CVS, Perforce, and ClearCase with features like cheap local branching, convenient staging areas, and multiple workflows. Docker outclasses other tools with features like ultra-fast container startup times (microseconds, not minutes), convenient [image building tools](https://github.com/centurylinklabs/building), and collaboration workflows.

For example, in Git you make some change and can see changes with git status:



	$ git init .
	$ touch README.md
	$ git add .
	$ git status
	On branch master
	
	Initial commit
	
	Changes to be committed:
	  (use "git rm --cached ..." to unstage)
	
		new file:   README.md
	$ git commit -am "Adding README.md"
	[master (root-commit) 78184aa] Adding README.md
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 README.md
	$ git push
	Counting objects: 49, done.
	Delta compression using up to 4 threads.
	Compressing objects: 100% (39/39), done.
	Writing objects: 100% (49/49), 4.29 KiB | 0 bytes/s, done.
	Total 49 (delta 13), reused 0 (delta 0)
	To git@github.com:my/repo.git
	 * [new branch]      master -> master
	Branch master set up to track remote branch master from origin.
	$ git pull
	remote: Counting objects: 4, done.
	remote: Compressing objects: 100% (3/3), done.
	remote: Total 3 (delta 0), reused 0 (delta 0)
	Unpacking objects: 100% (3/3), done.
	From github.com:cardmagic/docker-ruby
	   f98f3ac..4578f21  master     -> origin/master
	Updating f98f3ac..4578f21
	Fast-forward
	 README.md | 3 +++
	 1 file changed, 3 insertions(+)
	 create mode 100644 README.md
	$ git whatchanged
	commit 78184aa2a04b4a9fefb13d534d157ef4ac7e81b9
	Author: Lucas Carlson <lucas@rufy.com>
	Date:   Mon Apr 21 16:46:34 2014 -0700
	
	    Adding README.md
	
	:000000 100644 0000000... e69de29... A  README.md

In Docker, you can track changes throughout your entire system:


	$ MY_DOCKER=$(docker run -d ubuntu bash -c 'touch README.md; sleep 10000')
	$ docker diff $MY_DOCKER
	A /README.md
	C /dev
	C /dev/core
	C /dev/fd
	C /dev/ptmx
	C /dev/stderr
	C /dev/stdin
	C /dev/stdout
	$ docker commit -m "Adding README.md" $MY_DOCKER my/ubuntu
	4d46072299621b8e5409cbc5d325d5ce825f788517101fe63f5bda448c9954da
	$ docker push my/ubuntu
	The push refers to a repository [my/ubuntu] (len: 1)
	Sending image list
	Pushing repository my/ubuntu (1 tags)
	511136ea3c5a: Image already pushed, skipping 
	Image 6170bb7b0ad1 already pushed, skipping
	Image 9cd978db300e already pushed, skipping
	de2fdfc8f7d8: Image successfully pushed 
	Pushing tag for rev [de2fdfc8f7d8] on {https://registry-1.docker.io/v1/repositories/my/ubuntu/tags/latest}
	$ docker pull my/ubuntu
	Pulling repository my/ubuntu
	de2fdfc8f7d8: Download complete 
	511136ea3c5a: Download complete 
	6170bb7b0ad1: Download complete 
	9cd978db300e: Download complete 
	$ docker history my/ubuntu
	IMAGE               CREATED             CREATED BY                                      SIZE
	de2fdfc8f7d8        3 minutes ago       bash -c touch README.md; sleep 10000            77 B
	9cd978db300e        11 weeks ago        /bin/sh -c #(nop) ADD precise.tar.xz in /       204.4 MB
	6170bb7b0ad1        11 weeks ago        /bin/sh -c #(nop) MAINTAINER Tianon Gravi 

### CONCLUSIONS ###

These collaboration features (docker push and docker pull) are one of the most disruptive parts of Docker. The fact that any Docker image can run on any machine running Docker is amazing. But The Docker pull/push are the first time developers and ops guys have ever been able to easily collaborate quickly on building infrastructure together. The app guys can focus on building perfect app servers and the ops guys can focus on building perfect service containers. The app guys can share app containers with ops guys and the ops guys can share MySQL and PosgreSQL and Redis servers with app guys.
**
This is the game changer with Docker. That is why Docker is changing the face of development for our generation.** The Docker community is already curating and cultivating generic service containers that anyone can use as starting points. The fact that you can use these Docker containers on any system that runs the Docker server is an incredible feat of engineering.

To learn more about how to incorporate Docker into your daily life, follow along on this blog. [Here is a good starting point.](http://www.centurylinklabs.com/about/)

- From [centurylinklabs](http://www.centurylinklabs.com/what-is-docker-and-when-to-use-it/) 
- on April 22, 2014	
- by Lucas Carlson 