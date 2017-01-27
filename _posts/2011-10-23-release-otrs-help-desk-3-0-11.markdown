---
author: liuadmin
comments: true
date: 2011-10-23 15:52:27+00:00
layout: post
slug: release-otrs-help-desk-3-0-11
title: 'Release: OTRS Help Desk 3.0.11'
wordpress_id: 51517
categories:
- CMS/CMDB
- ITIL/ITSM
tags:
- cmdb
- ITIL
- ITSM
- open source
- oss
- 服务台
---

* * *


[success]这是一个补丁修补版本。我的名字也第一次出现，感谢Michael的帮忙，没有你我可能迟迟发不上去这个翻译。完整的release notes见 [http://otrs.org/releases/3.0.11](http://otrs.org/releases/3.0.11)[/success]
<table cellpadding="0" >
<tbody >
<tr >

<td >








































+++++++++++++++++++++++++ Release Note ++++++++++++++++++++++++

Release:            OTRS Help Desk 3.0.11
Status:             stable
Code Name:          Cancún Beach, México

We are proud to announce that the latest patch level release of OTRS 3.0
(codename: Cancún Beach, México) has been released.

Important for Upgrading
=======================
* From OTRS 3.0.x: Make sure you run bin/[otrs.RebuildConfig.pl](http://otrs.RebuildConfig.pl/) after
the upgrade so that the configuration is refreshed. Otherwise the
system may not work.

* From OTRS 2.4.x: Please read the UPGRADING and INSTALL files for
detailed instructions.

Warning
=======
OTRS versions from 3.0.beta1 up to 3.0.2 were affected by a bug in the
GenericAgent which could cause the "Ticket Delete" flag to be active
by default for new GenericAgent jobs, depending on the locale. If you
used one of the affected versions and have created new GenericAgent
jobs with them, please review them to check if the "Ticket Delete"
flag indeed has the correct value. Otherwise unwanted data loss might
occur.

Improvements
============
* Updated Simplified Chinese Translation, thanks to Martin Liu!
* Updated Danish translation, thanks to Lars Jørgensen!
<table cellpadding="0" >
<tbody >
<tr >

<td >






































Software Download
=================* [ [http://otrs.org/downloads/](http://otrs.org/downloads/) ] (Germany/Hamburg)
* [ [ftp://ftp.otrs.org/pub/otrs/](ftp://ftp.otrs.org/pub/otrs/) ] (Germany/Hamburg)

A complete list of all download mirrors is available at
[ [http://otrs.org/downloads/](http://otrs.org/downloads/) ].







































</td>
</tr>
</tbody>
</table>






































</td>
</tr>
</tbody>
</table>
