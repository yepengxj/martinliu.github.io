---
author: liuadmin
comments: true
date: 2012-10-28 15:40:01+00:00
layout: post
slug: xenapp-xendesktop-receiver-3-3%e5%ba%94%e7%94%a8%e5%95%86%e5%ba%97%e6%9c%80%e4%bd%b3%e5%ae%9e%e8%b7%b5
title: Receiver 3.3+应用商店最佳实践
wordpress_id: 52156
categories:
- XenApp
- XenDesktop
tags:
- Access Gateway
- Ag
- AppControler
- Netscaler
- receiver
- StoreFront
- xen
- XenApp
- XenDesktop
---

前一篇博客“[让用户畅游在云的大同世界里”](http://martinliu.cn/2012/09/让用户畅游在云的大同世界里.html)提到了提到了Receiver 3.3以及我所期望用到的最主要功能：同时连接并登陆多个虚拟化站点，让所有用户使用的虚拟应用（桌面）都汇聚（聚合）到用户终端上。这样做的需求源于：很多客户都有多个网络隔离的，多个地域隔离；用户的移动性决定了，做应用发布汇聚的必要性，这样也就奠定了CloudGateway的需求的根本。<!-- more -->
[![](http://cdn1.martinliu.cn/wp-content/uploads/2012/09/cg-architecture-inpg_v2.png)](http://cdn1.martinliu.cn/wp-content/uploads/2012/09/cg-architecture-inpg_v2.png)

在Reciever 3.3让用户犹如登陆了自己的iTune，可以浏览已经购买的应用，这些应用的图标就在界面的首页上，如果需要使用按个常用应用可以随时点击启动它；对于那些还没有使用过的应用，可以点击左侧的分类，浏览添加，当然也可以使用应用商店的搜索，找到自己需要的应用。那么这些应用是哪里来的？它们的来源有两个：1）StoreFront 应用商店；2）AppControler 应用控制中心；StoreFront负责会不和对外发布XenDesktop和XenApp群集中的应用；AppControler主要负责发布SaaS和移动应用；这样用户从Receiver 3.3（电脑和各种移动设备）端，完整的获得企业要提供给用户的所有种类的应用服务，包括：XenDesk/XenApp后端的各种业务应用、SaaS应用、移动设备应用（IOS和Andriod app）和传统业务应用和内容。注意这是一种全新的应用交付方式，它新在：用户和IT的人都完全不用关心任何一个应用在客户端上的安装、需求、升级、补丁和支持的问题，这些问题全都交给了数据中IT团队在虚拟应用和桌面交付平台上统一管理。任何一种应用访问，对于用户来说就是一种IT服务，用户只需通过Receiver使用这种服务，而不需要对这个服务的数据安全、软件维护等任何技术问题操心。

到此为止，我已经说道了本文要讲的主线：Reciever 3.3 -> AG -> StoreFront -> XenDesktop/XenApp ；在这条路径上AG运行在NetScaler上是前端和后台的分水岭，AG外侧是用户，AG内侧是数据中心内部。那么，老的Receiver，或者说叫做Online Plugin和非老的已存在的XenDesktop和XenApp到哪里去了，看下下面的图，你就明白了。

![receiver33](http://martinliu.cn/wp-content/gallery/citrix/receiver33.png)

如上图所示，老的Receiver或者online plugin不能通过AG连接到应用商店里面，只能走以前的老路，那么也就不能享受到我上面所的所有的好处。New Receiver只的就是我所说的Reciever 3.3。但是它不能通过AG连接WI。说道这里不得不说，我上周在用户现场测试的辛苦经历。我要的其实只是New Receiver对应的这条路径。但是，没有向导Storefont是必须的，因此倒是吧上面的路径配通了，而迟迟无法实现Receiver 3.3所能达到的理想的状态。

上面全都是正确的废话，下面开始分享对工程师有用的干货。下面我按照上图的五个层次依次总结一下，我上周在一个政府项目实施案例中的经验和教训：

[tab label="Receiver" first="yes"]
Receiver的选择，能做到多账户同时登陆，聚合多个账户中后台系统虚拟资源的版本目前只有Receiver for windows 3.3 版本（Mac版和其它版本，我还没有测过）；而不是其它任何版本，如果你是初次玩Receiver的话，进到下载里面，一定会被搞晕掉，它不是：Receiver for windows的任何版本，包括3.2、 3.1 。也不是所有Online Plugin联机插件的各个版本，它们属于Existing Receiver这一类。 [box color="orange" icon="flag"]
分析一下你的实际需求，然后再决定该使用那个版本；这是一个重要的决定，它确定了你是否需要部署Storefront和AppControler这两个服务。
[/box]
[/tab]

[tab label="Access Gateway"]
AG的选择，如果涉及Receiver 3.3的话，AG上有两几个关键点。首先AG的系统最好是NS10的，很多文档和POC手册都是和10相关的，而且和StoreFront搭配起来都算是同期产品版本，应该会比较好一些。下面是我们在实施现场的一些AG配置总结：
[list icon="check"]



	
  * StoreFront的地址用IP而不是DNS

	
  * STA在AG中还是要配置

	
  * 用HTTP和StoreFront关联而不是HTTPS

	
  * 继续使用ICA proxy（这个一定要用，不然只能用Smartaccess模式了）

	
  * 去除了Clientless相关策略，不用AppController，不需要这个配置


[/list]
从这些配置方式来看，还有StoreFont服务，在不使用AppControler的情况下，AG的配置策略以前的AG传统的配置方法区别不大；但是如果有AppController 和第三方SaaS应用就不一样了，那样的话还是要参考[KB **CTX131908**](http://support.citrix.com/article/CTX131908)中的策略来配，不过这个KB没有谈到以上的那些要点，我要不是受到NS大师的指导，几乎就被带到沟里去了。
[/tab]

[tab label="StoreFront WI" ]
这里只说下StoreFront，这就是我说的应用商店，有了它你就可以保持所有用户的应用订购信息。从发展的眼光看，它应该是WI的一个替换，但是在一段时间内，肯定需要和WI并存。它的安装文件在CloudGateway产品中可以下载，是一个103兆的安装包，可以装在win2008 R2 64bit的系统上，需要MS SQL数据库的支持。可以做多节点的群集，那样就需要想WI一样在前面放负载均衡器。它其实能够让Receiver和Online Plugin同时使用。这里稍微介绍一点它的结构，它里面有两个重要部件：Receiver 商店站点，这是让Receiver直连的；Receiver for Web 商店站点，这个是为了照顾老版本的Online Plugin而设计的，老版本的用户也可以访问应用商店，但是它们只能通过Web的方式登陆，登陆后能看到和Native Win32版的Receiver for Windows 3.3相同样式的深绿色界面，和应用商店内容。点击应用后，ICA连接还是可以通过Online Plugin 正常建立。

[/tab]

[tab label="应用和桌面" last="yes"]
XenDesktop和XenApp这里就不在多说，由于目前我也没有实际测试AppControler的实施经验所以，经验配置部分的内容待续。

不过AppControler应该十个很好的东西，有了它才能企业内部的IT管理人员把应用发布服务的面辐射到每个角落，才能让更方便地为用户管理SaaS应用，才能让Receiver端可以正常使用Share File这样的网盘数据服务。
[/tab]

参考链接：
[list icon="star"]




  * [Receiver for Windows 3.3 中文在线帮助文档](http://support.citrix.com/proddocs/topic/receiver-windows-33/nl/zh/cn/receiver-windows-wrapper.html?locale=cn)


  * [StoreFront 1.2 中文在线帮助文档](http://support.citrix.com/proddocs/topic/dws-storefront-12/nl/zh/cn/dws-version-wrapper.html?locale=cn)


  * [Access Gateway 10 集成说明](http://support.citrix.com/proddocs/topic/access-gateway/nl/zh/access-gateway-10/agee-xa-xd-integration-edocs-landing.html)


  * [How to Configure Access to Citrix Receiver StoreFront through Access Gateway Enterprise Edition](http://support.citrix.com/article/CTX131908)


[/list]
