---
author: liuadmin
comments: true
date: 2014-11-18 15:16:50+00:00
layout: post
slug: '%e7%a1%ac%e4%bb%b6%e5%b0%b1%e7%bb%aa%e5%8f%af%e5%bc%80%e5%b7%a5%e4%ba%86'
title: 硬件就绪可开工了
wordpress_id: 53177
categories:
- life
tags:
- lab
---

昨天晚上折腾了很晚，结果扩展的8GB内存条死活和系统不兼容，导致ESXi安装卡在内存检查哪里。在京东上直接退货，然后订货HP专用内存条。今天下午新条子火速送达。装上后系统在也卡了。ESXi安装顺利完成。下载了vClient后，导入了几个常用ISO，安装好了RHEL6和7的模板机。接下来可以开始方案的研究了。由于这台服务器有着巨大的折腾的空间，未来的硬件升级whish list包括：

[su_list icon="icon: heart-o"]



	
  * 增加SSD磁盘，加速IO密集的虚拟机

	
  * 增加到16GB内存，可惜不能上32GB，短板，相当的短

	
  * 增加新的硬盘，当前的1TB用完后，还有三个盘位

	
  * 升级CPU到Xeon e1256l v2，据说性能可以提升三倍，逻辑CPU数可以到8颗


[/su_list]

开源的东西还好，基本上都是结构简洁的居多，我可能从配置管理相关的技术开始搞起来，如Formen，Puppet；再到Ceph&gluster等存储应用，再到OpenStack这样较复杂的应用。
