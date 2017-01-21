---
author: liuadmin
comments: true
date: 2011-11-27 14:56:56+00:00
layout: post
slug: hypervisor-is-not-operationl-for-pc
title: 当Hypervisor成为服务器的标配
wordpress_id: 51530
categories:
- Cloud Computing
tags:
- Citrix
- Hypervisor
- xen
- xenserver
---

先声明一下，本文属于偷懒行为，意在证明本blog还没有关张大吉，只是在经历了一段时间的紧张学习之后，终于有时间发布文章了。这是一个开始相信后续又更多内容会陆续发表。
最近搭建产品测试和学习环境都是用XenServer，在此虚拟化平台之上，导入若干个操作系统的模版后，其他的产品测试和学习工作就可以轻松地展开了。XenCenter集中地管理访问这些虚拟机也非常方便。用了一段时间后发现：免费版本对于没有什么特殊要求的软件测试和开发人员来说是完全够用，且非常简单易用，更不没有盗版的风险。




![](http://xen.org/images/globals/xen_logo.gif)这次主要是推荐XenServer，它是我认为在开源和商业软件之间平衡的最好的软件。它起源于Xen.org的开源软件，现在用户可以使用到的基于Xen的主要版本又三个。1）Xen Source 4.1.2，这个版本为纯开放版本，是目前全球装机量做大的Hypervisor，可以说没有它就没有现在百花齐放的云世界；2）XenServer免费版本，是商业版本的入门级别，它的可执行文件和最高级收费版本的XenServer没有任何差别，只是少了很多高级功能（详见：[http://shenhj.blog.51cto.com/829152/420500](http://shenhj.blog.51cto.com/829152/420500)）即便如此，国内用户也非常多！但是往往用了免费版本的人都会发现，它的功能实惠，量又足!! 3）第三种当然是付费版本了，它也有几个档次的价位供你选择，能够随着你需求的升级，在过渡到高阶功能版本，最爽的是它是按照服务器硬件的台数计价，不在单独对CPU和内存的使用收钱；提醒各位看官，请尽量避免以下情况出现：有一天你从市场买了几头猪，拿回家后，姓卫的虚拟化厨师说，想吃右后腿的话，比必须给我另外在支付三千大洋；这里请一定想清楚到底猪是谁的。

网上的学习资料太多了，我只选取部分我认为不错的视频学习材料与大家共享：
[tip]
[ 视频: Citrix 8步演示如何虚拟化服务器之一　XenServer 简介](http://v.youku.com/v_show/id_XMzAyMTg2NTky.html)
[ 视频: Citrix 8步演示如何虚拟化服务器之二　安装XenServer](http://v.youku.com/v_show/id_XMzAyMTg5NTIw.html)
[ 视频: Citrix 8步演示如何虚拟化服务器之三　安装XenCenter](http://v.youku.com/v_show/id_XMzAyMTkwMDE2.html)
[ 视频: Citrix 8步演示如何虚拟化服务器之四　创建资源池](http://v.youku.com/v_show/id_XMzAyMTkwNTg0.html)
[ 视频: Citrix 8步演示如何虚拟化服务器之五　连接共享存储](http://v.youku.com/v_show/id_XMzAyMTkxMjk2.html)
[ 视频: Citrix 8步演示如何虚拟化服务器之六　新建虚拟机](http://v.youku.com/v_show/id_XMzAyMTk0NDg0.html)
[ 视频: Citrix 8步演示如何虚拟化服务器之七　导入虚拟机](http://v.youku.com/v_show/id_XMzAyMTkzMjg4.html)
[ 视频: Citrix 8步演示如何虚拟化服务器之八　迁移虚拟机](http://v.youku.com/v_show/id_XMzAyMTk0Nzcy.html)

[/tip]

