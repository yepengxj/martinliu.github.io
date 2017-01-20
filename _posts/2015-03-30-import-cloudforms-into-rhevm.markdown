---
author: liuadmin
comments: true
date: 2015-03-30 03:13:47+00:00
excerpt: 下载CloudForms最新版本的rhev的虚拟机，导入到rhevm的nfs export存储中。从模板生成虚拟机。运行和配置CloudForms虚拟机，这样它就可以管理这个rhevm的环境了。
layout: post
slug: import-cloudforms-into-rhevm
title: Import CloudForms  into rhevm
wordpress_id: 53659
categories:
- CloudForms
tags:
- cfme
---

[bash]
[root@rhevm03 export]# cat /etc/exports
/var/lib/exports/iso *(rw)
/export/rhev_import_export_disk *(rw,sync,no_subtree_check,all_squash,anonuid=36,anongid=36)
/export/template *(rw,sync,no_subtree_check,all_squash,anonuid=36,anongid=36)
# [root@rhevm03 export]# engine-image-uploader -N cfme5351 -e export-nfs-rhevm -v -m upload /tmp/cfme-rhevm-5.3-51.x86_64.rhevm.ova
[/bash]

然后从Web Console上导入这个模板，创建一个目标规格的虚拟机。
