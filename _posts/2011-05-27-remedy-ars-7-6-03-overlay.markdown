---
author: liuadmin
comments: true
date: 2011-05-27 16:50:16+00:00
layout: post
slug: remedy-ars-7-6-03-overlay
title: Remedy ARS 7.6.03 overlay
wordpress_id: 51090
categories:
- BMC
tags:
- 7.6.04
- ARS
- BMC
- ITIL
- ITSM
- remedy
- 定制
- 实施
- 开发
- 汉化
- 项目
---

[![Remedy-ARS-7.6.04-Overlay](http://cdn1.martinliu.cn/wp-content/uploads/2011/05/Remedy-ARS-7.6.04-Overlay.png)](http://martinliu.cn/2011/05/remedy-ars-7-6-03-overlay.html/remedy-ars-7-6-04-overlay)一个Remedy产品史上较大的新功能正在被大多数人忽视和绕过，实在是不吐不快，也希望所有的Remedy开发人员能够关注一下这个功能，因为他可能真的对你的项目非常重要。

上图显示了Overloay对象的地位和功用，我们都是工作在BMC原厂的开箱即用的程序对象层面上，所有安装程序首次安装到系统上的应用的所有对象都是Base对象。在这个基础之上我们做定制和开发，定制和开发出来的对象有两种，一种是Overlay对象，中文翻译为叠加对象，这种叠加对象并不会对原有的Base对象进行修改，而是覆盖在其之上的，两者是和谐共存的。另外一种对象就是纯客户化的对象，即以前没有，开发人员新加入的对象，这种对象和其他两种对象是没有冲突的。

Overlay可以是Base对象保持原状有什么意义？最重要的一点就是对升级有好处，以前我们开发的所有Remedy应用系统，大家都不敢做升级，当客户或者BMC的support要求要升级的时候，我们都会抵制或反对，这里的原因相信大家心里都知道。那么以后大家就不必这样了，只要在开发定制的过程中合理的使用Overlay对象做定制开发，方能保证定制后的系统对补丁和升级来者不拒。

那么如何使用到Overlay对象呢？在Dev Studio中选中需要修改的对象，点右键选择create overlay，你就能在原厂的对象上做一个叠加对象了。这里提出一个7.6.04 Dev Studio的错误做法：默认登录到Dev Studio以后，你可能会发现在默认的最佳实践模式下，你不能向以前一样任意修改东西，发现在切换到另外一个模式（好像是经典模式）之后又什么都能修改了，所以你就认为找到了修改的方法，其实这种操作恰恰是绕过了Overlay功能。在这种模式等于在以前旧版本产品的模式下开发做。


<blockquote>老外如是说：What the overlay feature does is to simply allow you to do the following:

1) Add new items that are identified as custom items you have added.  They are flagged as custom items in the displays.  You can easily sort by and get a list of custom items.  And it is COMPLETE.  You don't have to worry if you are missing one or if you forgot about something you added.
2) Update existing items by leaving the original definition there and updating a copy of that definition with your changes.
a) all the benefits of #1 are present AND your changes have the exact same name/identification as the original
b) you can at any time see your version vs. the original to see exactly what has changed from out of the box
c) Not have to deal with "ripple changes".  By this I mean that if in the past you copied a filter to a new name (to avoid overwrite at upgrade), you had to copy any guide that included it and then any workflow that called the guide to use the new name.   The fact that the items are the SAME ITEM means that there is no need to change other things.
d) When an upgrade occurs, the definitions in the base layer are changed but NOTHING about the items you have overlaid (or added custom) are changed. So, your changes are not overwritten.  In fact, your changes continue to be the overlay and continue to sit on top of and override the definition that was newly imported with the same name/id.
e) After the upgrade, you can again compare your overlay with the new out of the box definition to see if there is anything that should change.  Maybe the out of the box does the right thing now and you should remove your overlay or maybe there is an extended set of actions and you need to pick up one or more of the new actions in your overlay.

The key is that it provides an automatic and inherent layer that is YOUR layer that sits over the out of the box definition and allows you to safely, clearly, and cleanly adjust or augment the defintions if needed for your environment.

This is a feature that allows you to gain further and tighter control over your environment.  It is something that provides you with the ability to better understand what is stock and what is custom and what is changed about the solution.  It is one that preserves all changes you have made across upgrades with a layer of independence and yet links so that changes stay tied into the solution without the change you have made being updated by the upgrade itself.</blockquote>


突然想讲这样的一个故事，如果曾经发生在你身上，就当是个笑话吧。Remedy ITSM套件就好比是一个精装别墅，BMC一般会告诉客户，那里面有世界上最豪华的设施和装修，直接拿着行李入住就行了，事实如此！不过客户往往没有先看进屋看个究竟（其实往往用户没有这个机会，因素复杂，我不说你懂得），就找来施工队，提出我是有这样那样生活习惯和品位的，这都是对此房子的期望和需求，我的上帝客户啊！东西你都买了为啥就不先试住一下呢？尝试新鲜事物的精神您有木有？接着施工队的工人（也就是我们的Remedy程序开发人员）被工头（项目经理）带着就进屋了，说我们就是专业干这个的，能保证按时上线，您就等好吧！客户在院子里站着，瞧着施工队拿着需求分析书和开发工具进进出出，在屋里叮叮当当紧着忙活，几个月之后，项目经理过来说，我们可以做上线培训了（或者试运行/或者UAT测试了），这下客户才真的走进屋，客户开始纳闷了，心里直嘀咕，这真的是别墅么？好像有点糙啊！项目经理说，我们正式按照您的指示，已经把它做成中式风格了，老美的东西怕您用不惯。就这样客户茫然的也就入住了，其实客户可能只也住在了别墅某一层的一间屋里。通往其它房间的门都被封了，并且贴上了壁纸，或者被新打的大衣柜给挡住了，每次回家都是从窗台爬梯子上去。

对任何项目而言，在原厂产品上的定制开发是必须的，但是往往是项目的无底洞，那么如何规避这种风险？怎样让Remedy ITSM产品开箱即用的功能发挥到最大化？无疑对产品已有能力的挖潜和利用也要花时间精力成本去研究，这个时间和开发定制的工作时间是冲突矛盾的。那么：让客户先试住，在逐步装修，可能才是平衡矛盾的关键。客户也应该把项目实施和开发的资金做一个规划，切勿在前期投入太大，项目的前期，应该是学习产品和适应最佳实践的过程。实施方应该想方设法的让客户先进屋看清楚，和客户一起住一段时间，之后在去开工装修，这个过程应该是项目美好的蜜月期。
