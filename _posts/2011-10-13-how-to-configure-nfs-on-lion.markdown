---
author: liuadmin
comments: true
date: 2011-10-13 16:30:50+00:00
layout: post
slug: how-to-configure-nfs-on-lion
title: 苹果Lion系统做NFS文件夹共享
wordpress_id: 51510
categories:
- Apple
tags:
- appple
- iso
- linux
- lion
- mac
- nfs
- xen
- xenserver
---

苹果系统和其它Unix系统之间使用其内置的NFS的方式共享文件应该是最容易配置的，下面是相关步骤。
1. 编辑一个文件：编辑/etc/exports文件，加入目标需要导出的文件夹路径，例如：/Users/liumartin/Documents/Simon -alldirs -ro
2. 使用一个命令：启用nfsd： sudo nfsd enable
3. 测试一下结果
[bash]
liumartin@ showmount -e
Exports list on localhost
/Users/liumartin/Documents/Simon    Everyone
[/bash]
4. 文件夹已经使用NFS协议发布到局域网里了，可以使用其它任意NFS客户端来挂这个目录，以及这个目录中的子目录，下面的例子，使用XenCenter来为XenServer挂载Lion系统上的NFS共享文件夹，并读取其中的ISO文件
[![mac-nfs](http://martinliu.cn/wp-content/gallery/citrix/mac-nfs.jpg)](http://martinliu.cn/wp-content/gallery/citrix/mac-nfs.jpg)
