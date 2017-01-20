---
author: liuadmin
comments: true
date: 2012-02-08 08:05:35+00:00
layout: post
slug: xendesktop-is-better-then-view-p2
title: 【ZT】 View和XenDesktop到底谁更简单 Part II
wordpress_id: 51606
categories:
- Virtualization
tags:
- Citrix
- View
- VMWare
- XenDesktop
---

FROM ： [http://vdesk.blog.51cto.com/2969473/774669](http://vdesk.blog.51cto.com/2969473/774669)

望着这个标题发了半小时呆后，我就想抽自己！真的没法写，这两个东西丫的没一个简单的！如果你唯一目标就是奔着“简单”去的。So sorry，您找错对象了。

        View和XenDesktop其实都是为大企业客户设计的解决方案，仅从版本命名上就可见一斑。View最低版本叫Enterprise Edition，高阶版叫Premier Edition。XenDesktop相似，叫做Enterprise Edition和Platinum Edition。

       知道啥叫Enterprise吗？Enterprise就是大企业客户。大企业客户在生意对话中属于强势的一方，他们会定义自己的标准和架构，然后要求厂商的产品去支持和与之集成。另外大企业内用户众多，应用场景复杂，也要求桌面的方案足够灵活，能够定制不同策略以适应不同的标准和要求。因此为大企业客户设计的解决方案它压根就简单不了！

在比较企业级的解决方案时，通常关注点不会放在“简单”上面。而是比较谁对大企业的要求适应性更强。国外有一个叫Burton Group的组织（now part of Gartner），花了5个多月时间做了一个桌面虚拟化的评估标准。标准覆盖甚广：

-User experience
-Service advertising and connection brokerage
-Business continuity
-Network
-Storage
-Back-end virtual infrastructure
-Management
-Security
-Guest OS support
-Licensing
-Product support
-Third-party vendor support

这个标准今天被看作是桌面虚拟化领域的权威定义。国内巨头企业在桌面虚拟化选型时，无一例外都会参考这个标准。这个标准将产品功能分成三级： Must to have，Need to have和Nice to have。随后Burton group对XenDesktop 4和View4.5按这个标准做了一个完整评估，评估结论如下：

[![](http://cdn1.martinliu.cn/wp-content/uploads/2012/02/124434949.png)](http://martinliu.cn/2012/02/xendesktop-is-better-then-view-p2.html/attachment/124434949)

从上面的图表，你会发现View刚刚走完Must to have的开发阶段。与XenDesktop相比，在Need to have 和Nice to have的二，三级功能元上差距还很大。不要小看这些差距，它们对后期管理和运维至关重要。

我举一个管理的例子，大家就明白了。如果有用户向你抱怨虚拟桌面很慢，你该怎么办？“慢”纯粹属于主观感受，每个人对“慢”的感受和容忍度是不一样的。用View，你可能就要去猜了，因为它的控制台不能提供重要度量数据的可视性，你需要借助第三方的工具去收集数据来验证自己的猜测。而使用XenDesktop，它的EdgeSight组件就可以帮你看见这个慢的原因在哪里。是不是真的慢了？具体慢了多少？是慢在网络上，还是服务器端，还是客户端？如果是客户端登录环节慢了，它又可以将登录过程分解成10几个步骤，看看你是慢在验证，还是慢在用户档案加载，还是慢在运行脚本上…….

       简而言之，对于大企业而言，桌面虚拟化可不是简单发布出一个桌面就OK了。毕竟后期运维人员70%~80%的时间都要与这个虚拟化平台打交道，所以一些更灵活、更高阶的配置、管理、维护功能也同等重要。而能达到这个要求，您的方案就不可能“简单”！

       中小企业的方案更倾向于“简单”。那么对于中小企业来讲，View和XenDesktop谁更适用呢？答案是都不适用。因为中小企业对桌面虚拟化的要求截然不同。中小企业没有足够的IT人员，没有足够的专业技能，没有足够的后端基础设施，也没有足够的IT预算。所以，无论是View还是XenDesktop对他们而言，都太复杂了，太昂贵了。

中小企业期望的桌面虚拟化解决方案要比PC更便宜，比PC更易安装和管理，有着与PC相接近的用户体验，同时还能少花钱多办事，在重要的功能上没有缺失（如高可用， 随需扩展和动态负载均衡）。天啦！天下有这么便宜的事吗?


       VMware目前肯定是没有的。而Citrix针对中小企业市场，特别推出了一款产品，叫做VDI-in-a-Box， 大家可以去下载体验一下。这个产品在1个小时内就可以安装完毕，零培训就可以上手。与传统企业级VDI方案相比，它削减掉超过60%的基础设施， 使得每个虚拟桌面的成本比新购PC还低。即使今后扩容，也仅需要简单的增加服务器，不需要重新设计和重新架构，没有任何隐形的成本。想要了解更多有关VDI-in-a-Box的信息，可以参考链接中的文档：[https://citrix.sharefile.com/d-s7824ca9d0dd47479](https://citrix.sharefile.com/d-s7824ca9d0dd47479)
