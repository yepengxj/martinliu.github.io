---
author: liuadmin
comments: true
date: 2012-03-05 14:24:50+00:00
layout: post
slug: '%e5%a6%82%e4%bd%95%e9%85%8d%e7%bd%aeandroid-emulator%e7%94%a8%e4%ba%8e%e8%b0%83%e8%af%95citrix-xenapp-6-5%e7%a7%bb%e5%8a%a8%e5%ba%94%e7%94%a8sdk'
title: 如何配置Android Emulator用于调试Citrix XenApp 6.5移动应用SDK
wordpress_id: 51628
categories:
- Citrix
tags:
- Android
- citrix receiver
- IOS
- Mobile
- SDK
- XenApp
---

[tip]本文转帖自国外的一个大拿，有余我朝是和谐社会，所以禁止访问该网站，特此转帖。 本文详细描述了如何配置一个XenApp 6.5 移动应用开发包的开发环境，写的非常使用。这个开发包是我每次交流必须讲的话题，往往是最后一个讲，可是每次都引起用户的强烈关注。从业务创新的角度讲，开发一个原生平板电脑界面的应用系统的诱惑力是在太大了，貌似我们无法阻挡程序猿去开发平板电脑业务应用；就像我们不能组织企业的老板们在iPad上使用移动办公系统一样。[/tip]


<blockquote>From [http://www.jasonconger.com/](http://www.jasonconger.com/)</blockquote>


One of the coolest SDKs I’ve seen come out in quite a while is the [Citrix XenApp 6.5 Mobile Application SDK](http://community.citrix.com/display/xa/XenApp+6.5+Mobile+Application+SDK). Citrix defines the XenApp 6.5 Mobile Application SDK as “… a rich tool kit for developers to write touch-friendly, mobilized applications that are hosted on Citrix XenApp and delivered to any device with Citrix Receiver. These mobilized applications are able to leverage a wide set of mobile device functionality including GPS, sensors, cameras, and device buttons in the same way that locally running, native applications do.”

As of this writing, only the Android version of the Citrix Receiver is supported (iOS is on the way).  Since I do not own any Android devices and I was anxious to get started, I had to set up an emulator and install the Citrix Receiver to get going with the SDK.  Here is how I did it.


## Install the Android SDK


Go to the Android SDK download page ([http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html)) and pick the correct installer for your platform. I’m using Windows, so I chose the .exe installer file.  After you run this .exe, you still do not have the emulator.  The reason for this is the Android SDK archive initially contains only the basic SDK tools. It does not contain an Android platform or any third-party libraries. You must install the Platform-tools and at least one version of the Android platform using the SDK Manager.

[singlepic id=1335 w=320 h=240 float=none]

I installed the Android SDK Platform-tools and all options for Android 4.0.3.

After the install completes, be sure to add **%ProgramFiles%\Android\android-sdk\platform-tools** to your PATH environment variable.  This will be handy later for installing the Citrix Receiver.


## Create an Android Virtual Device


After the installs complete, you can launch Android Virtual Device Manager (AVD Manager). This can be found in the Windows start menu under Android SDK Tools \ AVD Manager. AVD Manager is used to create various virtual devices running the Android OS.

![create-new-android-vd](http://martinliu.cn/wp-content/gallery/citrix/create-new-android-vd.png)
As you can see, I created an Android 4.0.3 device with 100 MiB of local storage. The more storage you add to your AVD, the longer it will take to boot. Since this AVD is only being used for XenApp 6.5 testing, I only allocated 100 MiB. The first boot of your AVD will take a little longer than subsequent boots.


## Download the Citrix Receiver for Android


Now that we have a functioning Android emulator, we need to get the Citrix Receiver installed. The first thing we need to do is download the .apk (Android Package) file. Normally, I would just go to [http://www.citrix.com/receiver](http://www.citrix.com/receiver) and choose “Android”. But, as of this writing, when you do that, you are redirected to the Android Marketplace. Unfortunately, Android Marketplace does not work on the Android Emulator. So, here is what you can do instead:
Go to [http://www.citrix.com/downloads](http://www.citrix.com/downloads) and choose “Receiver for Android” from the drop down list. From there, you can select the Android client and download the .apk.


## Install the Citrix Receiver for Android


Ok, so now we have a functioning Android emulator and the Citrix Receiver downloaded. The final step is to install the Citrix Receiver onto the emulator. Here’s how:



	
  1. Copy the .apk file to %ProgramFiles%\Android\android-sdk\tools

	
  2. Open a command prompt and change the directory to %ProgramFiles%\Android\android-sdk\tools

	
  3. With the AVD you created running, execute the following command:











<table >
<tbody >
<tr >

<td >`1
```

</td>

<td >`adb install <name of Citrix Receiver>.apk
```

</td>
</tr>
</tbody>
</table>
[singlepic id=1339 w=320 h=240 float=none]








 You now have a fully functional Citrix Receiver running on an Android emulator.  My next post shows you [how to set up a development environment to utilize the Mobile Application SDK and compile some of the examples](http://www.jasonconger.com/post/installing-and-using-the-citrix-xenapp-6-5-mobile-application-sdk/).
