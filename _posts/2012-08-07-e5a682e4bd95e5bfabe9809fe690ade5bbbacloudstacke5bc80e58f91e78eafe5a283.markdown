---
author: liuadmin
comments: false
date: 2012-08-07 15:45:50+00:00
layout: post
slug: '%e5%a6%82%e4%bd%95%e5%bf%ab%e9%80%9f%e6%90%ad%e5%bb%bacloudstack%e5%bc%80%e5%8f%91%e7%8e%af%e5%a2%83'
title: 如何快速搭建CloudStack开发环境
wordpress_id: 51841
categories:
- CloudStack
tags:
- ant
- Apache
- Citrix
- cloud
- Cloud Computing
- cloudstack
- iaas
- VirtualBox
---

本文转自 cloudstack-dev@incubator.apache.org 邮件组：





	
  1. download and Install VirtualBox,

	
  2. download DevCloud image from [http://download.cloud.com/templates/devcloud/DevCloud.ova](http://download.cloud.com/templates/devcloud/DevCloud.ova),

	
  3. import DevCloud image into VB,

	
  4. checkout CloudStack code from Apache git repo into my machine,

	
  5. execute commands "ant clean-all build-all", "ant rdeploy -Drhost=172.168.56.1 -Dport=2222",  "ant rdeploydb -Drhost=172.168.56.1 -Dport=2222",  "ant rdebug -Drhost=172.168.56.1-Dport=2222"   all seems success

	
  6. on browser [http://192.168.56.1:8080/client/](http://192.168.56.1:8080/client/), login as admin/password, continue with basic installation, use exactly the same

	
  7. data for creating Zone, pod, cluster, etc that here [http://wiki.cloudstack.org/display/comm/DevCloud](http://wiki.cloudstack.org/display/comm/DevCloud) - step8/f(Access CloudStack web UI: [http://ip-address-of-your-machine:8080/client](http://ip-address-of-your-machine:8080/client), create a new zone, add pod/cluster/host etc). Following install guide after add host I should add Primary storage (there is no that step on the Devcloud manual), so I set similar to the Secondary storage (path:/opt/storage/primary, server: 10.0.2.15), I don't know if it makes a sense.

	
  8. On the latest step I click "Launch" button


转帖自学一下。如果你是Windows的桌面机
