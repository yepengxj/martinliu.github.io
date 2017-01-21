---
author: liuadmin
comments: true
date: 2012-08-16 15:25:19+00:00
layout: post
slug: xenserver-san-boot%e5%ae%89%e8%a3%85
title: XenServer SAN Boot安装
wordpress_id: 51895
categories:
- XenServer
tags:
- boot
- cx480
- emc
- HP BL680 G7
- lun
- san
- xenserver
- 光纤存储
- 安装
---

**环境：**服务器--HP BL680 G7刀片服务器   存储--EMC CX480

**故障描述：**
从存储方面为主机分配作为San Boot引导Lun 60GB空间，作为HA独立Lun 40GB，用来存放虚拟机数据Lun
安装过程中选择60GB的Lun并且在安装之前高级设置中打开了multipath开关。
安装完成后，显示如下：attempling boot from hard drive (C:)
![attemting-boot-from-hard-driver-c](http://martinliu.cn/wp-content/gallery/citrix/attemting-boot-from-hard-driver-c.png)
**解决办法：**
需要说明的是在EMC CX480存储在分配Lun空间时，会为Lun分配Lun ID和Host ID（这2个ID均可以进行修改）
一般HBA默认Host ID为0的Lun作为San Boot的引导lun。因此，在实际生产中，如果之前Host ID 0的lun已经被其他Lun所使用，引导lun使用为其他Host ID时，需要在HBA卡设置中明确设置由该Host ID Lun引导。

如：本项目中，主机的引导Lun Host ID为 1，我们就需要在HBA卡中设置Host ID1的Lun作为引导Lun。
![select-adapter](http://martinliu.cn/wp-content/gallery/citrix/select-adapter.png)
开启HBA的San Boot功能
![qlogic-fast-util](http://martinliu.cn/wp-content/gallery/citrix/qlogic-fast-util.png)
选择正确的作为引导的lun作为引导lun使用。完成后保存设置重启后故障解决

**注意：**这里所看到的lun ID都是存储上面的Host ID，一定不要忽视。

致谢：投稿人 王文博（北京网智瑞通信息技术服务有限公司）
欢迎投稿，请发邮件到 liuzh66@gmail.com

