---
author: liuadmin
comments: true
date: 2012-07-27 04:37:42+00:00
layout: post
slug: '%e5%a6%82%e4%bd%95%e9%85%8d%e7%bd%aecloudstack%e7%9a%84iso%e4%b8%8b%e8%bd%bd%e7%ab%99%e7%82%b9'
title: 如何配置CloudStack的ISO下载站点
wordpress_id: 51817
categories:
- CloudStack
tags:
- Apache
- cloudstack
- IIS
- iso
- 下载
---

首先，需要安装和准备Web服务器，不管是iis还是apache，你需要增加一个MIME类型，需要把.iso作为一个正确的类型添加到配置中；如何添加，去google一下即可，这里不做描述。配置好了以后把ISO文件或者文件夹放到web站点相应的目录中。可以使用管理节点上的浏览器测试一下URL是否可以正常访问。
其次，配置CloudStack管理节点，告诉他允许下载的Web站点在那个网段。这个配置需要进入Global Settings，搜索secstorage关键字，找到一个叫做“secstorage.allowed.internal.sites”的配置参数。点击action下面的编辑按钮。我输入的是192.168.10.0/24，敲回车确认即可。这个参数是说，Web服务器的网段在192.168.10.0；然后到管理节点的命令行重启服务
[bash]
service cloud-management restart
[/bash]

最后，等服务起来之后，重新登陆管理界面，这下子就可以开始正常的iso模板添加操作了。否则应该会碰到connection refused的错误。
