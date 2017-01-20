---
author: liuadmin
comments: true
date: 2012-06-06 09:19:10+00:00
layout: post
slug: xenapp-mobility-pack-and-mobile-sdk-faq
title: XenApp Mobility Pack And Mobile SDK FAQ
wordpress_id: 51659
categories:
- Citrix
tags:
- Mobility
- SDK
- XenApp
---

今天听了Citrix Lab 老大Anil上的课，感觉对这两个东西豁然开朗了很多。至少解答了我的很多疑问，我感觉我的这些问题有可能会是常见问题，下面就列出一部分吧？

XenApp Mobility Pack 和 Mobile SDK 是安装在那的？
答：前者是安装在XenApp6.5服务器上的；后者是安装在开发环境中的，开发环境是指Windows开发环境，在次环境中去开发一个用来在XenApp服务器上发布的Windows应用程序，它能够通过Receiver调用移动设备的所有功能，后台能够连接企业应用完成业务操作。

XenApp Mobility Pack可以单独使用么？
答：是的。其实把他安装在XenApp6.5服务器上，你立刻就能得到几个新的用户策略，启用这些策略之后，就能够实现两个非常有用的功能：1）输入法在文本框的自动弹出；2）下拉框变成移动设备原生的选择菜单。这两个功能就能够极大的提高XenApp用户在移动设备上的体验。

XenApp Mobile App SDK可以单独使用么？
答：不能。它必须和XenApp服务器端的组建联合使用。它主要用做创新应用的开发。例如：一个主要在Windows平台上的软件开发商，它的客户说我们要求你们的应用能够支持所有的移动设备。可是这个ISV不想投人力在IOS和安卓上开发，因此他们利用Mobile SDK给用户做了Windows客户端程序的改造。

文档和演示程序在那里？
答：Citrix维护了很好的在线文档 [http://www.citrix.com/mobilitysdk/docs/index.html ](http://www.citrix.com/mobilitysdk/docs/index.html)
