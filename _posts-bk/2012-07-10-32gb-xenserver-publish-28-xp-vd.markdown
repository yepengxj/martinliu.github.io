---
author: liuadmin
comments: true
date: 2012-07-10 16:27:14+00:00
layout: post
slug: 32gb-xenserver-publish-28-xp-vd
title: 32GB测试笔记本电脑成功发布28个XP虚拟桌面
wordpress_id: 51798
categories:
- XenDesktop
tags:
- Citrix
- XenDesktop
- xenserver
---

一直想搞清楚，这台强悍的测试机到底能够撑得住多少个虚拟桌面。今天终于测了一下，稍微满足了一下子好奇心。
底层装的是最新版的XenServer6.02，模板机XP做了一些优化，调整为动态内存到1024~2048，其实可以调整到更小，如512~1024，下次在测试一下这个方案，不过那样可能登录速度和登陆后桌面点击的反应会有一定的折扣；本次不考虑那么多，只是想看看这个本本到底能够跑多少虚拟机。存储使用的是NAS存储，桌面是发布的专有模式桌面。有图有真相，下面的截屏供参考：

[nggallery id=15]
