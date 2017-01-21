---
author: liuadmin
comments: true
date: 2011-12-28 13:55:05+00:00
layout: post
slug: xendesktop-is-better-then-view-p1
title: '[zt] View和XenDesktop,到底谁更简单 -- Part I'
wordpress_id: 51558
categories:
- Virtualization
tags:
- Citrix
- Desktop
- RingCube
- Virtualization
- xen
- XenApp
- XenDesktop
---

桌面虚拟化最大的一个好处就是能简化管理。所以管理的复杂性往往成为企业用户在方案选型时的一个重要考量。但如何考察管理的复杂性呢？这个问题可并不简单！

先来看看最常犯的一个错误，那就是将“简化管理”与“简单化管理”等同起来。于是数一数不同厂商产品的安装步骤，组件数量以及控制台个数。OK，就开始下结论了。但是这个结论未免太草率。

对于IT管理员来讲，有些事情是只需要做一遍的，而有些事情则是需要天天做的。你其实更应该关注天天做的事情是不是真地变得简单了。

就拿操作系统的补丁来说吧，这是一个经常性的工作。为了简化补丁管理，VMware View和Citrix XenDesktop都采用了系统镜像的管理方式。虚拟桌面如果从镜像模板派生，那么一旦模板的补丁更新了，所有虚拟桌面的补丁就可以同步到最新。不过“承诺常常很像蝴蝶, 美丽地飞盘旋然后不见” 。还是让我们拿出放大镜， 看得更清楚一点。

虚拟桌面可简单分为两类，一类是个人专用桌面，这种桌面是一对一的；另一类是浮动分配桌面，这种桌面是一对N的，当上一个用户登出时，浮动桌面将回收并还原到与模板完全一致的状态。VMware View的补丁更新机制针对浮动分配桌面好使， 但是针对个人专用桌面就不灵了。如果你冒然对个人专用桌面做更新（recompose），桌面的补丁倒是与时俱进了，但桌面里所有用户自己安装的应用程序将会全部丢失！你能想象终端用户暴跳如雷的样子吗？ 事实上随着桌面虚拟化部署规模的扩大，你会发现个人专用桌面的占比越来越高。如果这类最大用户群体的桌面都照顾不好，又何谈简化管理呢？

其实VMware View的补丁机制和Citrix XenDesktop如出一辙，不适用的根本原因还是它下面的功夫没有做到。View没能真正实现OS与Application的完全分离。有童鞋可能会质疑说，View不是有差分盘吗？所有用户安装的程序都会写到差分盘上。话虽没错，不过别忘了差分盘是block-level的。如果作为参照物的母盘发生改变，block-level的差分数据（data delta）就都失效了。这就好比“刻舟求剑”，“母船”动了，“记号”也就失效了。

Citrix的做法是从File level来捕获data delta。在人可以理解和感知的文件系统和注册表级别来捕获差异。然后将差异保存到一个单独的Personal vDisk上。这样就实现了OS与Application的真正分离。

From [一周耀文](http://vdesk.blog.51cto.com/) : [http://vdesk.blog.51cto.com/2969473/744750](http://vdesk.blog.51cto.com/2969473/744750)
