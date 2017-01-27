---
author: liuadmin
comments: true
date: 2011-05-18 15:25:39+00:00
layout: post
slug: how-to-deploy-mid-tier-to-tomcat-7
title: How to deploy mid-tier to tomcat 7
wordpress_id: 51067
categories:
- BMC
tags:
- 7.6.04
- ARS
- deploy
- install
- java
- Mid-tier
- remedy
- Tomcat
- 安装
- 性能
---

![tomcat 7](http://tomcat.apache.org/images/tomcat.gif)Since Apache Tomcat 7.0.14 came out, I have not reason why I am not checking this out. And this is  the first time I deopy a .war file into tomcat instance.

I am runing Remedy ITSM 7.6.04 in VMWare workstation on my laptop. It's a Dell e6400 with 8GB RAM. When I startup arsystem, that vm is just running out of 5GB RAM. I almost got no RAM for running tomcat on laptop(Win7 64bit). I used to run a mid-tier that was installed from Remedy ARS installer package with Tomcat 6.0. I had to limit Tomcat max memory pool size to 512 BM_. _If not, I could not open any windows for testing Remedy. But the overall performance is not acceptable.

So I decided to test this combination out, MidTier.war + Tomcat 7.0.14. There is a quick note below.



	
  1. Download [Apache Tomcat 7.0.14 ](http://apache.etoak.com/tomcat/tomcat-7/v7.0.14/bin/apache-tomcat-7.0.14.exe)and install it

	
  2. Copy MidTier.war to C:\Apache Software Foundation\Tomcat 7.0\webapps , rename it to arsys.war

	
  3. restart tomcat 7 service, you will see .war file is unzip to a new folder

	
  4. Open a new firefox widnow or tab, access to http://localhost:8080/arsys/shared/config/config.jsp

	
  5. Add your ars server in service list

	
  6. Login Remedy Mid-tier from http://localhost:8080/arsys/


Now I got a new issue, CPU usage is hight, tomcat7 process take 40~50% :) I  am thinking I need a new more powerful laptop to play around this product. This testing is not finished yet. Stay tune, I may came up with a workaround. And it should works better then tomcat6.

![apache](http://www.apache.org/images/asf-logo.gif)
