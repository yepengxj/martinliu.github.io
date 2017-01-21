---
author: liuadmin
comments: true
date: 2012-07-05 16:49:31+00:00
layout: post
slug: zt-reference-architectures-that-scale-citrix-xendesktop-on-flexpod-with-microsoft-private-cloud
title: '[ZT] Reference Architectures that Scale: Citrix XenDesktop on FlexPod with
  Microsoft Private Cloud'
wordpress_id: 51773
categories:
- XenDesktop
tags:
- cisco
- Citrix
- Hyper-V
- Microsoft
- XenDesktop
- xenserver
---

今天学习了一篇很有意义的帖子，特别是它的结论对我特别有帮助。帖子的原文地址：[Reference Architectures that Scale: Citrix XenDesktop on FlexPod with Microsoft Private Cloud](http://blogs.citrix.com/2012/07/03/reference-architectures-that-scale-citrix-xendesktop-on-flexpod-with-microsoft-private-cloud/)

下面是硬件的测试架构，使用的服务器是UCS 14刀，NatApp存储，Hyper-V，加载XenDesktop 5.6

[![](http://cdn.ws.citrix.com/wp-content/uploads/2012/07/1-CVD-SolutionsOverview-1024x743.png)](http://cdn.ws.citrix.com/wp-content/uploads/2012/07/1-CVD-SolutionsOverview.png)

**_Test Results_**





The reference implementation achieved impressive results in our test runs, especially in comparison to previous testing with earlier generation Cisco blades. As a matter of fact, the tested configuration reduced the rack space needed to support 2000 users, decreasing it from 30 Rack Units (RUs) to 12 RUs. This density can help to lower power use, which directly translates into energy savings.










The results specifically showed that the Cisco UCS B230 M2 half-width blade (featuring dual-socket, 10-core processors and 256GB of memory) can support medium workloads up to 145 users per blade. A single FlexPod VDI design containing two Cisco UCS chassis units with 14 such blades can support at least 2000 virtual desktop workloads while maintaining acceptable response times. The results clearly demonstrated linear scalability of desktop workloads for this reference architecture.  Detailed metrics are given below.







14片在12U的空间上，轻松的支撑了2000个Normal型工作负载的Win7虚拟桌面（1.5GB/8~12IOPS；所有虚拟机开机启动时间为半个小时。平均每个刀片上能够支持145个用户，而且维持了比较合理的用户相应速度。在这个架构中，证明了XenDeskTop可以实现横向扩展的特性。







微软和思科的详细测试报告下载：




[download id="13" format="1"]




[download id="12" format="1"]





## 微软测试报告中的主要结论：


Microsoft, Citrix, Cisco, and NetApp successfully validated XenDesktop streaming 2,000 concurrent Windows 7 desktops to virtual machines hosted with Hyper-V. The deployment was built on a 16-node FlexPod with Microsoft Private Cloud infrastructure that comprises the hardware requirements in the Microsoft Private Cloud Fast Track program. The hardware, in conjunction with Windows Server 2008 R2 Enterprise SP1, Hyper-V, System Center 2012, and Citrix XenDesktop 5.6:


<blockquote>

> 
> 
	
>   * Validated that a single instance of Virtual Machine Manager and a single instance of the XenDesktop delivery controller successfully hosted 2,000 VDI workloads.
> 
	
>   * Verified single-server scalability: 143 Windows 7 desktops with 512 MB of dynamic memory (expandable to 2 GB) running knowledge worker load on a single Cisco UCS B230 M2 Blade Server with 20 cores and 256 GB of random access memory (RAM).
> 
	
>   * Validated a fully virtualized environment where all VDI components (such as Active Directory Domain Services, Microsoft SQL Server, VMM, XenDesktop, and Provisioning Server) were run in virtual machines.
> 
	
>   * _**Observed an 80 percent storage savings in comparison to a similar VDI environment without NetApp storage efficiencies.**_
> 

</blockquote>
