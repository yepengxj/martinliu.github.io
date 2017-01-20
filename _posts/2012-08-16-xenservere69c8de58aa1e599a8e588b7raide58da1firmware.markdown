---
author: liuadmin
comments: true
date: 2012-08-16 14:43:23+00:00
layout: post
slug: xenserver%e6%9c%8d%e5%8a%a1%e5%99%a8%e5%88%b7raid%e5%8d%a1firmware
title: XenServer服务器刷RAID卡firmware
wordpress_id: 51890
categories:
- XenServer
post_format:
- Status
tags:
- 1068E
- Integrated Raid模式
- IR模式
- lsi
- MegaRaid
- raid
- xenserver
- 浪潮
---

最近安装浪潮服务器，发现找不到本地硬盘的错误。这是RAID卡不兼容，导致不能够读取硬盘造成的。
此主板上板载lsi 1068E raid芯片默认使用的是SoftWare Raid模式(MegaRaid)，这种模式不为xenserver所兼容，所以需要更改主板跳线，并刷新板载Raid芯片的firmware，更改raid模式为IR模式（Integrated Raid模式）使xenserver可以兼容。NF560D2更新后，可以顺利安装Xenserver。
还有一台服务器的RAID卡在主板上控制死了工作模式，没有刷机的可能，这种情况下，只能使用DDK编译该RAID卡的驱动，在安装的过程中，进入高级模式，加载附加的驱动，之后就可以正常安装了。如何做DDK编译附加的设备驱动程序，待续。
