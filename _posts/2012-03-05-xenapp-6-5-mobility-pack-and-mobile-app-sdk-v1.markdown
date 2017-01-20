---
author: liuadmin
comments: true
date: 2012-03-05 15:06:33+00:00
layout: post
slug: xenapp-6-5-mobility-pack-and-mobile-app-sdk-v1
title: 'XenApp 6.5 Mobility Pack and Mobile App SDK v1 '
wordpress_id: 51637
categories:
- Citrix
tags:
- Citrix
- Mobility
- SDK
- XenApp
- XenDesktop
---

XenApp 6.5 Mobility Pack 是可以安装在XenApp服务器上的一个扩展包，它能够使企业应用调用到移动终端设备上的原生功能，包括：GPS，摄像头，原生的界面控件。这个扩展包增加的策略能够和终端设备交互，控制相关传感器和功能。


XenApp 6.5 Mobile Application SDK 是一个开发包，程序猿可以使用一个微软Virtual Studio的开发环境，使用C或者C++语言来开发出运行在移动设备上的企业应用。

百闻不如一见，下面是一个实例程序。 [singlepic id=1333 w=320 h=240 float=none] 此程序是一个供水设施的巡检系统，中间部分是告警事件，按时间先后顺序显示了出现故障的GPS坐标，告警设备类型等信息。左边显示的是这些告警的地点在gogle map上的位置，下面是设备的图片。屏幕的右侧是事件处理区域，可以让巡查人员编辑和处理每一条告警事件，右下角是使用移动摄像头拍照记录的部分。这个应用是透过Citrix Receiver连接到虚拟应用发布服务器上使用的，虚拟应用发布服务器上发布了此应用的客户端，次客户端在和后台的应用服务器交互，做信息的存储和处理等业务逻辑操作。以上是我对改应用的理解。原帖见：[http://blogs.citrix.com/2011/10/25/announcing-the-xenapp-6-5-mobile-application-sdk-mobility-pack/](http://blogs.citrix.com/2011/10/25/announcing-the-xenapp-6-5-mobile-application-sdk-mobility-pack/)

下面在举一个例子：对比一下使用了移动应用开发包优化过后的XenDesktop虚拟桌面和为优化的差异，细节下差异一目了然。

 For example, with this pack, XenApp can intelligently recognize an Android or iOS tablet as the endpoint and render Tablet Optimized Desktops, making the experience much more natural for the user.  From this:

 [![](http://cdn.ws.citrix.com/wp-content/uploads/2011/12/prev-start-menu-300x225.png)](http://martinliu.cn/?attachment_id=174177488)

to this:

 [![](http://cdn.ws.citrix.com/wp-content/uploads/2011/12/pack-start-menu-300x225.png)](http://martinliu.cn/?attachment_id=174177489)

No more pinching and zooming to navigate windows intended for a full desktop interface! // from [http://blogs.citrix.com/2011/12/19/mobilize-your-enterprise-with-the-xenapp-6-5-mobility-pack/](http://blogs.citrix.com/2011/12/19/mobilize-your-enterprise-with-the-xenapp-6-5-mobility-pack/)

[box]Citrix 移动应用开发包能为我们做什么：The Citrix Mobile Application SDK provides over 50 specific mobile API’s that can be used from any enterprise Windows development environment.  These APIs allow developers to create touch enabled UI’s for new and existing enterprise applications.  With these new APIs the applications can leverage the unique capabilities of smartphones and tablets, allowing full access to device sensors and capabilities such as GPS, camera, and accelerometer.  This sensor information can then be relayed back to and used by an enterprise application hosted on XenApp in the data center. This capability is novel and innovative as up till now it has not been possible for Windows applications in the datacentre to access these new device capabilities.[/box]

从那里能够的到Citrix 移动应用开发包：[http://community.citrix.com/display/xa/XenApp+6.5+Mobile+Application+SDK](http://community.citrix.com/display/xa/XenApp+6.5+Mobile+Application+SDK) 下载SDK需要注册免费的mycitrix账号，登陆后下载。

本文的参考文章：



	
  * [http://blogs.citrix.com/2011/10/25/announcing-the-xenapp-6-5-mobile-application-sdk-mobility-pack/](http://blogs.citrix.com/2011/10/25/announcing-the-xenapp-6-5-mobile-application-sdk-mobility-pack/)

	
  * [http://blogs.citrix.com/2011/12/19/mobility-pack-and-mobile-app-sdk-v1-released/](http://blogs.citrix.com/2011/12/19/mobility-pack-and-mobile-app-sdk-v1-released/)

	
  * [http://blogs.citrix.com/2011/12/19/mobilize-your-enterprise-with-the-xenapp-6-5-mobility-pack/](http://blogs.citrix.com/2011/12/19/mobilize-your-enterprise-with-the-xenapp-6-5-mobility-pack/)



