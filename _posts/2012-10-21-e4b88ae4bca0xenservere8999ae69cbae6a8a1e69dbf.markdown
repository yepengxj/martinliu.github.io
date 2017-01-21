---
author: liuadmin
comments: true
date: 2012-10-21 08:05:31+00:00
layout: post
slug: '%e4%b8%8a%e4%bc%a0xenserver%e8%99%9a%e6%9c%ba%e6%a8%a1%e6%9d%bf'
title: 上传XenServer虚机模板
wordpress_id: 52147
categories:
- CloudStack
tags:
- bz2
- cloudstack
- nfs
- tar
- vhd
- vhd.bz2
- xenserver
---

目标：在XenServer上生成CloudStack所需要的操作系统模板，转换成CloudStack所需要的格式，上传模板，测试使用模板创建的虚拟机。

在一个XenServer上安装目标操作系统，选择合适的版本，位数，安装xentools，安装需要的补丁，安装完毕之后关机待用。你建立的虚拟机是建在了NFS SR上的，那么就简单了，直接去NFS SR里面找到这个虚拟机的文件，文件应该是vhd文件，直接压缩为bz2格式的就ok了。如果虚拟机建立在了本地硬盘、iscsi或者FS等块存储上了，就稍微麻烦一点。一个最简单的方法，在www（如果是linux apache）下载服务器上建立一个nfs文件夹，用XenCenter建立一个新的SR，把这个nfs文件夹挂上。选择需要的模板虚拟机，选择Copy VM右键菜单，选择Full Copy，选中刚才建立的nfs SR；等待虚拟机复制完成，去nfs文件夹下面看看文件的大小是否正常，必要的话可以把这个copy出来的新虚拟机启动一下，看是否可以正常运行。

在nfs文件夹下面看到vhd文件后，就可以使用tar jcf命令压缩模板了，tar的压缩能力蛮强的，win2008 r2 sp1虚拟机vhd文件大小是8个多GB，压缩之后只有3个多GB。把压缩后的vhd.bz2文件放到合适的地方，在浏览器里面测试一下这个文件的下载地址是否正常。

登陆CloudStack，选择模板，选择注册新模板。这个过程一般可能10~20分钟和你的机器的速度有关，注册的过程是，先下载然后在辅助出差上解压模板的过程，在这个过程中，可以在辅助存储中的目录里面查看解压的过程，可以看到文件的大小从3。2GB的临时文件涨到8GB多的过程。等模板有变为vhd文件后，刷新模板的状态，最终状态为ready。

下面可以测试模板了，创建一个实例，选择该模板，看测试vm在CloudStack是否能够正常运行。

参考文章：

[How to upload a OVA or XVA template](http://docs.cloudstack.org/Knowledge_Base/How_to_upload_a_OVA_or_XVA_template)
[how to create and extract tar.gz and tar.bz2](http://linux.dsplabs.com.au/tar-how-to-create-and-extract-tar-gz-and-bz2-compressed-archives-under-linux-p39/)
