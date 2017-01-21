---
author: liuadmin
comments: true
date: 2012-06-18 04:28:33+00:00
layout: post
slug: xendesktop-multi-monitor
title: XenDesktop多屏幕显示
wordpress_id: 51665
categories:
- XenDesktop
tags:
- Citrix
- monitor
- WI
- XenDesktop
---

[转帖] 说明：当客户端使用多个显示器时，连接XenDesktop默认只会使用主屏幕，不会使用扩展屏。如何使用扩展屏？

A.首先将Client端连接好多个显示器，并设置好是扩展屏还是Mirror方式1-手动实现：连接到XenDesktop桌面，退出全屏显示切换成窗口式，将调整XenDesktop窗口大小至多个屏幕中（通过鼠标拉窗口大小来完成），在点击全屏即可。方式2-自动实现：修改WI上的default.ica文件， default.ica文件位于C:\Inetpub\wwwroot\Citrix\DesktopWeb\conf for Web Interface clientC:\Inetpub\wwwroot\Citrix\PNAgent\conf for Program Neighborhood Agent。在[Application] 中添加 ConnectionBar=0
BTW：如何限制Multi-monitor的数量？通过Display memory Limit来控制。

目前我在一个项目中测试的效果如下，使用WYSE的瘦客户机，同时连接4个显示器。扩展显示桌面。

[![img_0805](http://martinliu.cn/wp-content/gallery/citrix/thumbs/thumbs_img_0805.jpg)](http://martinliu.cn/wp-content/gallery/citrix/img_0805.jpg)

[![img_0806](http://martinliu.cn/wp-content/gallery/citrix/thumbs/thumbs_img_0806.jpg)](http://martinliu.cn/wp-content/gallery/citrix/img_0806.jpg)
