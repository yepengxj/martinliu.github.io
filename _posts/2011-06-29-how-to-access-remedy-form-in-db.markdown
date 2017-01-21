---
author: liuadmin
comments: true
date: 2011-06-29 14:09:22+00:00
layout: post
slug: how-to-access-remedy-form-in-db
title: 如何读取Remedy中的数据
wordpress_id: 51303
categories:
- CMS/CMDB
tags:
- ARS
- arschema
- BMC
- oracle
- remedy
---

Remedy系统几乎是一个绿色软件，它的几乎所有业务数据、配置数据和工作流都是存储在数据库中，也就是说：只要能够保留一份完整的数据库备份，即可高枕无忧，需要的时候就可以把系统还原出来。业务数据在Remedy中大多存储在regular form中。多数的业务数据都是通过Join form进行访问和存取。在Remedy中的各种form构成了Remedy系统的所有数据结构和界面，有些类型的form是只做界面而创建的。

如何从数据库层面直接读取Remedy ARS系统中的业务数据？首先你需要在Remedy User中查询和确认你需要读取的form的名称，之后在用Remedy develop studio中确认你需要读取字段在数据库中的database ID，然后使用SQLPLUS 查询出form的数据库视图名称，最后编写一条sqlplus语句验证查询的结果。确认了表和字段在数据库中的ID之后，你就可以使用任何数据库客户端直接绕过Remedy应用系统来读取业务数据了。这样做比API的调用开发难度要小些。

下面是一个例子：用Remedy默认的用户名密码登录，查询BMC.CORE:BMC_ComputerSystem form在数据库中视图的名称为T517，在BMC Remedy Developer Studio中查询字段的ID[（点击查看大图）](http://cdn1.martinliu.cn/wp-content/uploads/2011/06/ars-forms.jpg)在此视图中查询CI名称里含有test-fc关键字的CI，并返回所有CI的name, inc id 和TotalPhysicMemory属性值。

[oracle@ars ~]$ sqlplus ARAdmin/AR#Admin#@remedy
SQL*Plus: Release 11.2.0.1.0 Production on Wed Jun 29 21:51:39 2011
Copyright (c) 1982, 2009, Oracle.  All rights reserved.
Connected to:
Oracle Database 11g Release 11.2.0.1.0 - 64bit Production
[sql]
SQL>
SQL> select schemaid from arschema where name='BMC.CORE:BMC_ComputerSystem';
  SCHEMAID
----------
       517
SQL>
SQL> desc T517;
 Name                                      Null?    Type
 ----------------------------------------- -------- ----------------------------
 C1                                                 VARCHAR2(31)
 C2                                                 VARCHAR2(254)
 C3                                        NOT NULL NUMBER(15)
 C4                                                 VARCHAR2(254)
 C5                                        NOT NULL VARCHAR2(254)
 C6                                        NOT NULL NUMBER(15)
 C7                                        NOT NULL NUMBER(15)
 C8                                        NOT NULL VARCHAR2(254)
 C112                                               VARCHAR2(255)
 C179                                               VARCHAR2(38)
 C60513                                             VARCHAR2(255)
 C200000001                                         VARCHAR2(254)
 C200000003                                         VARCHAR2(60)
 C200000004                                         VARCHAR2(60)
 C200000005                                         VARCHAR2(60)
 C200000020                                         VARCHAR2(254)
 C200000021                                         NUMBER(28)
 C200000022                                         NUMBER(28)
 C200000023                                         VARCHAR2(30)
 C200000025                                         VARCHAR2(254)
 C200000026                                         VARCHAR2(254)
 C200000028                                         VARCHAR2(254)
 C200000029                                         VARCHAR2(254)
 C200000032                                         VARCHAR2(60)
 C200000033                                         VARCHAR2(30)
 C200000034                                         VARCHAR2(30)
 C200000035                                         VARCHAR2(30)
 C200003000                                         CLOB
 C240000007                                         VARCHAR2(254)
 C240000008                                         CLOB
 C240001002                                         VARCHAR2(254)
 C240001003                                         VARCHAR2(254)
 C240001005                                         VARCHAR2(254)
 C260100002                                         NUMBER(15)
 C260140117                                         VARCHAR2(254)
 C260400001                                         NUMBER(28)
 C260400002                                         NUMBER(28)
 C300927600                                         NUMBER(15)
 C301002800                                         VARCHAR2(254)
 C301002900                                         VARCHAR2(254)
 C301003400                                         VARCHAR2(255)
 C301016000                                         VARCHAR2(254)
 C301016100                                         CLOB
 C301016200                                         NUMBER(15)
 C301016700                                         NUMBER(15)
 C301016800                                         NUMBER(15)
 C301016900                                         NUMBER(15)
 C301017000                                         NUMBER(15)
 C301017100                                         NUMBER(15)
 C301017200                                         NUMBER(28)
 C301017300                                         NUMBER(28)
 C301019500                                         NUMBER(15)
 C301019600                                         VARCHAR2(254)
 C301019800                                         VARCHAR2(254)
 C301019900                                         VARCHAR2(30)
 C301089100                                         VARCHAR2(80)
 C301118000                                         NUMBER(15)
 C301172600                                         NUMBER(15)
 C301182000                                         NUMBER(15)
 C301186800                                         VARCHAR2(254)
 C400079600                                         VARCHAR2(38)
 C400124500                                         NUMBER(15)
 C400127400                                         VARCHAR2(127)
 C400129100                                         NUMBER(15)
 C400129200                                         VARCHAR2(38)
 C400131200                                         VARCHAR2(255)
 C400131300                                         VARCHAR2(255)
 C490001289                                         VARCHAR2(127)
 C530010100                                         VARCHAR2(254)
 C530010200                                         VARCHAR2(254)
 C530010600                                         NUMBER(15)
 C530014300                                         NUMBER(15)
 C530014400                                         NUMBER(15)
 C530014500                                         NUMBER(15)
 C530019500                                         CLOB
 C530031600                                         NUMBER(15)
 C530032500                                         NUMBER(15)
 C530034500                                         VARCHAR2(255)
 C530035200                                         VARCHAR2(255)
 C530041601                                         NUMBER(15)
 C530043901                                         VARCHAR2(255)
 C530054200                                         NUMBER(15)
 C530058400                                         VARCHAR2(254)
 C530058500                                         VARCHAR2(254)
 C530059800                                         VARCHAR2(255)
 C530060100                                         NUMBER(15)
 C530060200                                         VARCHAR2(255)
 C530060300                                         NUMBER(15)
 C530062400                                         VARCHAR2(254)
 C530067430                                         NUMBER(15)
 C530067920                                         NUMBER(15)
 C530067930                                         VARCHAR2(127)
 E0                                        NOT NULL VARCHAR2(15)
 E1                                        NOT NULL VARCHAR2(15)

SQL>
SQL>  select C200000020,C179,C200000022 from T517 where  C200000020 like 'test-fc%';
C200000020
--------------------------------------------------------------------------------
C179                                   C200000022
-------------------------------------- ----------
test-fc-2.testlab.bigcorp.com
OI-48A6276C70E411E0A984000C29455AB9           448

test-fc-5.testlab.bigcorp.com
OI-4CCD50C270E411E0AA53000C29455AB9           320

test-fc-4.testlab.bigcorp.com
OI-4D1B433670E411E0AA57000C29455AB9           160

C200000020
--------------------------------------------------------------------------------
C179                                   C200000022
-------------------------------------- ----------
test-fc-6.testlab.bigcorp.com
OI-4E9E37C270E411E0AA69000C29455AB9           256
SQL>
[/sql]

[tip]鸣谢 [炮灰向钱冲](http://weibo.com/xuj0)和我对以上技术细节的讨论。[/tip]
