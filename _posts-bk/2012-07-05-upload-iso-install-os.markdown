---
author: liuadmin
comments: true
date: 2012-07-05 08:38:37+00:00
layout: post
slug: upload-iso-install-os
title: 在CloudStack上如何上传ISO和安装系统
wordpress_id: 51766
categories:
- CloudStack
tags:
- Citrix
- cloudstack
---

上传操作系统ISO到CloudStack服务器上，是一个简单的过程。为了图省事，我在管理服务器上搭了iso下载服务器。首先保证本机安装了httpd服务，这个apache的安装包，通常是操作系统自带的，没有的话yum install httpd 一下；之后 service httpd restart一下，保证http服务正常。之后要修改一下/etc/mime.types文件加入一行：
[shell]
# MIME type                                     Extensions
none/none                                       iso
[/shell]
再次重启httpd服务。
复制ISO文件到apache服务的默认路径下面/var/www/html/
在浏览器里面测试一下看看上传的iso文件是否能够下载http://192.168.10.15/MS_zh-hans_windows_xp_professional_with_service_pack_3_x86_cd_x14-80404.iso
CloudStack支持HTTP共享目录的方式复制ISO文件，ISO文件被管理服务器下载到它的secondary存储中。
登录CloudStack界面，使用模板管理，添加一个ISO。如下图所示
[![add a iso](http://martinliu.cn/wp-content/gallery/cloudstack/thumbs/thumbs_screenshot-6.png)](http://martinliu.cn/wp-content/gallery/cloudstack/screenshot-6.png)
上传iso文件成功之后，就可以使用实例管理，增加一个实例，开始安装操作系统了。安装操作系统的过程忽略。当看到你建立的实例为运行状态后，点击控制台图标， 在新弹出的console窗口中，我们就可以看到windows的安装画面了。
