---
author: liuadmin
comments: true
date: 2012-05-13 16:31:45+00:00
layout: post
slug: edgesight-for-load-testing3-8-1user-guide
title: EdgeSight for Load Testing3.8.1中文教程
wordpress_id: 51651
categories:
- Citrix
tags:
- Edgesight
- load testing
- XenApp
- XenDesktop
- 中文
- 压力测试
- 手册
- 教程
- 虚拟应用
- 虚拟桌面
---

[![](http://cdn1.martinliu.cn/wp-content/uploads/2012/05/架构.png)](http://martinliu.cn/2012/05/edgesight-for-load-testing3-8-1user-guide.html/%e6%9e%b6%e6%9e%84)

点击此处下载本中文教程：[download id="10"] ； 本文件在XenApp6.5的安装光盘中有，用一个中文的操作系统找到“EDGESIGHT FOR LOAD TESTING.MSI” 安装完之后，就能在程序打开后按F1查看此文件了。

这个中文帮助文档写的非常详细，相信任何合作伙伴的工程师都能够学会用这个工具做XenApp或者是XenDesk的压力测试。下面来讲几点需要注意的事情。最好找一个物理的服务器去安装本工具，物理服务器能够具有比较强的处理能力，能模拟出足够多的用户并发的压力，从而达到测试的目的，而且有不会因为自身的资源使用影响其它任何其它。千万不要把这个压力生成器放到你的XenApp系统内的某个虚拟机里面。另外注意网络连接情况，最好摸清楚从压力生成服务器到XenApp所在服务器的每一跳所经过的网络设备，千万不要经过10M或者100M的低级交换机，测试前先ping下，看看延迟和丢包如何。最后到XenApp服务器这一端了，不要想任何系统默认安装的配置就能达到理想的性能压力测试效果，做压力测试前一定要做优化，性能优化文档查查KB。在录制脚本的时候，要选择最短，最简单操作路径，避免任何无用或者无意义的操作，脚本天生不是完美的，也需要优化，删除掉那些不必要的指令。在跑压力脚本前，先检查被测试系统当前的资源使用情况，在跑的过程中使用监控工具全面监控，及时识别出被测试系统的各个服务器上在网络、内存、CPU和I/O等这些关键点上，是否出现性能瓶颈。尽可能的和客户沟通这些瓶颈，做出及时的参数或者配置硬件配置调整。
