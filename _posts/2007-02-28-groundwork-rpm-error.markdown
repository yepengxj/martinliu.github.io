---
author: liuadmin
comments: true
date: 2007-02-28 09:14:00+00:00
layout: post
slug: groundwork-rpm-error
title: GroundWork rpm 安装会导致原系统的一些改变
wordpress_id: 49144
categories:
- NSM
tags:
- GroundWork
- rpm
---

GroundWork rpm安装对系统造成的改变有：<br />

<br />	
  1. /etc/init.d/apache2 被改名为 apache2-save 导致，以前的Apache不能启动
<br />	
  2. 会在/etc/ld.so.conf中加入一行/usr/local/groundwork/lib ；不知道为什么这会导致一下系统的服务不能正常运行，如：PostgreSQL和snmpd。修复方法是注释掉这一行，然后运ldconfig命令。还不知道GroundWork在没有这一行的情况下有什么问题，注释掉之后好像它还是能正常运行的。
<br />
