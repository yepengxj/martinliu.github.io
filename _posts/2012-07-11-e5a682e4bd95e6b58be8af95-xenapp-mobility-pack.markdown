---
author: liuadmin
comments: true
date: 2012-07-11 17:04:22+00:00
layout: post
slug: '%e5%a6%82%e4%bd%95%e6%b5%8b%e8%af%95-xenapp-mobility-pack'
title: 如何测试 XenApp Mobility Pack
wordpress_id: 51803
categories:
- XenApp
tags:
- '6.5'
- Android
- Citrix
- IOS
- Mobility
- XenApp
---

安装XenApp6.5，下载XenApp6_5MobilityPack1_0.zip；解压缩之后是三个文件，我习惯于先打那个补丁包，然后在安装CitrixGroupPolicyManagement_x64.msi文件（我的测试系统是64位的）。

安装完之后，XenApp里面多了什么？多了两个自动运行的服务。如下图所示：

[![](http://cdn1.martinliu.cn/wp-content/uploads/2012/07/mp-services.png)](http://cdn1.martinliu.cn/wp-content/uploads/2012/07/mp-services.png)

XenApp的管理策略里面多了什么？如下图所示：

[![](http://cdn1.martinliu.cn/wp-content/uploads/2012/07/3-functions.png)](http://cdn1.martinliu.cn/wp-content/uploads/2012/07/3-functions.png)

这些策略怎么测试？先启用这些策略，再使用Pad设备或者其它移动设备测试即可。



	
  * 启动触控优化桌面：发布一个Xenapp的共享桌面，pad连上后，可以看到右上角有个半透明的块，点击它既可以在优化和普通桌面直接切换，切换之后，世界一下子变得特别美好，enjoy！

	
  * 远程控制组合框：发布一个界面或者页面上有下拉框的程序，用移动设备连上后，在点击这些页面的下拉框，看看这世界变得和以前有何不同。

	
  * 自动显示键盘：发布一个界面或者页面上有文本输入框的程序，用移动设备连上后，点击文本框，让它获得焦点，接着输入字符，接着点击别的地方，让它失去焦点。想想你以前类似的过程是怎么操作的，是不是发现以前的日子有点点苦逼了吧？




还能够做什么绚丽的演示？




可以在http://www.citrix.com/mobilitysdk/docs/downloads.html 网站下载官方的演示程序，[点此处下载](http://www.citrix.com/mobilitysdk/docs/downloads/CMP.NET%20MobilitySDK%20%23318504.3.zip)。这个程序既包含源代码有包含编译好的可执行文件，把它们都copy到xenapp服务器上，发布一下那里面的可执行程序，用pad或者手机连上，看看有什么新发现，是否感觉这简直就是一个原生的ios或者安卓程序呢？



