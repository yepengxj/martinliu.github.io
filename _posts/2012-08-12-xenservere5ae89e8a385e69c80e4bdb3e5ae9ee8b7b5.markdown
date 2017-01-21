---
author: liuadmin
comments: true
date: 2012-08-12 15:16:53+00:00
excerpt: 以上是XenServer的部分实施经验之总结，有不完整，或者不妥之处，请扶正。我想其实把XenServer经常遇到的安装错误和解决方法都整理一下也很好。如果你有类似的经验，请回帖记录一下。多谢观赏本文。
layout: post
slug: xenserver%e5%ae%89%e8%a3%85%e6%9c%80%e4%bd%b3%e5%ae%9e%e8%b7%b5
title: XenServer安装最佳实践
wordpress_id: 51856
categories:
- XenServer
tags:
- bios
- Citrix
- console
- free
- ibm
- RAM
- remote
- scrubbing
- Server
- x3850
- xen
- XenSrever
---

首先来看一个安装异常的情况，XenServer6.0.201在IBM x3850 X5型号的服务器上卡在下面这个屏幕的情况。

这个是由于在Bios中有一个设置没有开启，如下图所示：

Remote Console = Enable ; 没错都是这个参数惹得货；为什么会这样的？原因是我在安装的时候图快，怀着侥幸的心理，这个参数没有找到，就想忽略了，没成想，XenServer的安装程序可是没有放过我。就这个参数轻松的断送了我几乎一个上午，浪费掉的时间真可惜!关于处理器部分的参数还是有些的，下面我就把我的截屏贴出来，供后人参考。另外我这次的安装中还出现了一个错误，XenServer装完后，提示找不到系统磁盘，顿时就抓狂，后来在BIOS里面一查看，原理第一块硬盘居然不在系统启动清单中，把他加回来之后正常启动。这个排错的过程又浪费了我半个多小时，怪就怪IBM服务器重启自检一次的时间太长了，哈哈！

那么安装Citrix的最佳实践还有那些参数或者过程是不能错过的呢？下面是一个清单，你如果按照这么做了，成功并且平稳运行的几率是95%以上，如果不这么做，回头请不要埋怨这个产品不灵。关键看实施过程的耐心和细心，这就直接反映出了你的专业程度。


<blockquote>Restore default BIOS setup</blockquote>


开机进入BIOS之后，先把BIOS的设置回复的出厂模式，避免前人给你留下的遗患，这是正确配置的起点。


<blockquote>Enable VT or AMD/V</blockquote>


启用VT或者AMD/T；如果没有这个选项怎么办，换一张Win或者Linux的操作系统盘开装，这是你唯一的选择。其实这是服务器虚拟化的前提条件，装之前就要问清楚服务器的处理器支不支持虚拟化技术。其实查询一下XenServer的HCL比这个更重要。


<blockquote>disable C-state
Disable executive lock bit
Enable remote console(if IBM server)</blockquote>


Remote Console在IBM的服务器上面才有，其它厂商的服务器忽略，另外两个参数是普通存在的，不同厂商的服务器有可能名称不太相同。


<blockquote>Disable Multi-thread if possible</blockquote>


根据经验，如果你的服务器打开超线程之后虚拟核数大于48核，请在XenServer安装的过程中关闭这个选项。总虚拟核数=服务器路数*CPU核数*2；例如2路，6核的服务器，开超线程后的总核数=2*6*2=24核；那么还是打开这个配置即可。如果超过了48个核，那么请关闭超线程。等XenSrever成功装完之后，然后在回到这里把它启用，从而让XenServer获得最大的动力。


<blockquote>本地磁盘设置成RAID1或RAID 1/0
如果磁盘以前安装过 KVM,VMware 或其它 OS, 重新初始化 RAID 10</blockquote>


一般进入磁盘RAID设置的界面后，首先要做的是清除当前的所有RAID配置，保存结果后，在创建新的配置。本地硬盘配置为RAID10是推荐配置。照做即可。另外如果此服务器如果是做XenDesktop只用，在安装XenServer的过程中还要勾选优化XenDesktop的选项，这样本地磁盘就可以做智能缓存功能了，可以极大提升XenDesk系统的性能。在说个题外话，如果有钱的话把本地磁盘变成SSD那么XenDesktop跑起来就更爽了，道理你懂的。


<blockquote>BIOS Power Regulator for Maximum Performance</blockquote>


有些服务器的电源设置，默认为省电模式，那么它意味着CPU会自己降频使用自己，从而达到节电的目的，这个不是XenServer想看到的，请把节电相关的配置都去掉，都设置为最大性能优先。


<blockquote>Dom0的手动调优</blockquote>


参照 CTX124259, 将 Dom0 的内存上限扩展到2940M，这个参数对跑高密度虚拟机的XenServer服务器是必要的；如果服务器不支持UEFI和GPT分区, 安装XS6.0是可参照如下附件使用MBR分区安装，并根据业务需要将Dom0的文件系统扩展 到10G或20G，默认Dom0是4个GB，本来也够用了，但是这样就可以存储更多的log，比较方便后期的排错。


<blockquote>XenServer 安装之后打补丁</blockquote>


XenServer是一个快速成长的产品，一定要查询好最新的补丁清单，下载到XenCenter这个机器上，把该打的补丁都打上，这个没有什么说的。打补丁的过程中，需要有选择的看下，一些驱动补丁如果和你的硬件不相干，就不需要打了。相关的一定不要错过。[http://support.citrix.com/product/xens/v6.0/](http://support.citrix.com/product/xens/v6.0/ ) 这里是查询XenServer6补丁的网页。所有同一个规格的服务器都要打全了相同的补丁集。打完补丁之后，全部重启服务器。对于正经的项目实施来说，还需要做日志的收集和分析。在XenCenter中把XenServer的日志全部都出成压缩文件，每个服务器导出一个文件。Citrix提供了分析工具，可以免费使用，工具的网址：[https://taas.citrix.com](https://taas.citrix.com)，上传日志到这个工具网站中后，在这个网址上可以看到每个机器的分析结果，如果提示有错误的话，请提前想招解决，一定不要给项目流下遗患。


<blockquote>创建资源池相关操作</blockquote>


在建池之前，一定别忘了把每台XenServer的MetaDate 备份一下，命令如下：
[bash]xe pool-dump-database file-name=/root/xenserver001[/bash]
看到了，这个路径在root下面，备份了之后一定去查看一下，活要见人，死要见尸。这个主要是给XenServer留个后路，免得服务器退出池，或者把池推到重来的时候，每个服务器还是可以有个干净的基础配置的还原点。之后开始建资源池。这里一定要遵守三网分离的原则，即“管理网”，“生产网”和“存储网”要隔离开。推荐的最佳配置为使用6块网卡，两两绑定，来实现各自的功能。如果是FC或者ISCSI的存储，需要检查存储设备那端所支持的多路径的类型，然后在XenServer这端也配置相当的多路径功能。

以上是XenServer的部分实施经验之总结，有不完整，或者不妥之处，请扶正。我想其实把XenServer经常遇到的安装错误和解决方法都整理一下也很好。如果你有类似的经验，请回帖记录一下。多谢观赏本文。
