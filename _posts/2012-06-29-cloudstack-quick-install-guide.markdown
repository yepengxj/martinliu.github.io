---
author: liuadmin
comments: true
date: 2012-06-29 15:18:04+00:00
layout: post
slug: cloudstack-quick-install-guide
title: CloudStack Quick install guide (中文精编版)
wordpress_id: 51710
categories:
- CloudStack
tags:
- Citrix
- cloudstack
- xenserver
---

This post has a English version,[ click here](http://martinliu.cn/2012/08/cloudstack-quick-install-guide-english-mini-version.html)
测试环境描述：
两台硬件配置足够高的笔记本电脑，链接在一个交换机上，都能够上网。

[![](http://cdn1.martinliu.cn/wp-content/uploads/2012/06/IMG_0841.jpg)](http://martinliu.cn/2012/06/cloudstack-quick-install-guide.html/img_0841)

安装过程：第一步安装RHEL6管理服务器操作系统；第二部安装CloudStack软件；第三步安装Xenserver；第四步：初始化配置CloudStack

安装RHEL6 64bit操作系统的注意事项：



	
  1. 使用全域名作为主机名，例如 ：cloudstack.xen.cn； 安装完后 hostname --fqdn 查一下

	
  2. 使用ntp服务器 0~3.xenserver.pool.ntp.org

	
  3. 选择桌面类型安装，同时安装Mysql server/client

	
  4. 配置为静态ip地址，网关和DNS还要保证装完之后，能够上互联网

	
  5. 关闭防火墙，这样可以省去安装文档中iptables相关的端口设置，加速安装过程


安装Cladestack的时候需要同时安装系统的几个依赖的软件包，所以要把本地的DVD设置为yum的源挂载DVD到/media目录，之前必须安装几个依赖的包
[shell]
mount /dev/cdrom /media
yum install deltarpm-3.5-0.5.20090913git.el6.x86_64.rpm
yum install python-deltarpm-3.5-0.5.20090913git.el6.x86_64.rpm
yum install createrepo-0.9.8-4.el6.noarch.rpm
[/shell]

首先生成一个yum源的文件，如下所示：
[shell]
[root@cloudstack 1] cat /etc/yum.repos.d/rhel6.repo
[rhel6]
name=rhel6
baseurl=file:///media/
enabled=1
gpgcheck=0
[/shell]

用 yum list 检查一下dvd源是否正常。

现在既可以进入CloudStack的安装过程了，下载并解压缩安装包
[shell]
tar xzvf CloudStack-oss-3.0.2-1-rhel6.2.tar.gz
./install #运行安装命令
选择 m
选择 y
[/shell]

安装脚本使用yum安装所有的文件，它能够查出系统上还差那些包，依赖的包会通过yum一次性安装，安装过程如下所示：

[shell]
tomcat6-lib                          noarch          6.0.24-33.el6               rhel6               2.9 M
tomcat6-servlet-2.5-api              noarch          6.0.24-33.el6               rhel6                93 k
ws-commons-util                      noarch          1.0.1-13.el6                rhel6                37 k
wsdl4j                               noarch          1.5.2-7.8.el6               rhel6               157 k
xml-commons-apis                     x86_64          1.3.04-3.6.el6              rhel6               439 k
xml-commons-resolver                 x86_64          1.1-4.18.el6                rhel6               145 k

Transaction Summary
============================================================================================================
Install      38 Package(s)

Total download size: 91 M
Installed size: 172 M
Is this ok [y/N]: y
Downloading Packages:
------------------------------------------------------------------------------------------------------------
Total                                                                       115 MB/s |  91 MB     00:00
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
Installing : libgcj-4.4.6-3.el6.x86_64                                                               1/38
Installing : jakarta-commons-logging-1.0.4-10.el6.noarch                                             2/38
Installing : cloud-deps-3.0.2-1.el6.x86_64                                                           3/38
Installing : cloud-utils-3.0.2-1.el6.x86_64                                                          4/38

Installed:
cloud-client.x86_64 0:3.0.2-1.el6

Dependency Installed:
axis.noarch 0:1.2.1-7.2.el6                            bcel.x86_64 0:5.2-7.2.el6
classpathx-jaf.x86_64 0:1.0-15.4.el6                   classpathx-mail.noarch 0:1.1.1-9.4.el6
cloud-agent-scripts.x86_64 0:3.0.2-1.el6               cloud-client-ui.x86_64 0:3.0.2-1.el6
cloud-core.x86_64 0:3.0.2-1.el6                        cloud-deps.x86_64 0:3.0.2-1.el6
cloud-python.x86_64 0:3.0.2-1.el6                      cloud-server.x86_64 0:3.0.2-1.el6
cloud-setup.x86_64 0:3.0.2-1.el6                       cloud-utils.x86_64 0:3.0.2-1.el6
ecj.x86_64 1:3.4.2-6.el6                               ipmitool.x86_64 0:1.8.11-12.el6
jakarta-commons-collections.noarch 0:3.2.1-3.4.el6     jakarta-commons-daemon.x86_64 1:1.0.1-8.9.el6
jakarta-commons-dbcp.noarch 0:1.2.1-13.8.el6           jakarta-commons-discovery.noarch 1:0.4-5.4.el6
jakarta-commons-httpclient.x86_64 1:3.1-0.6.el6        jakarta-commons-logging.noarch 0:1.0.4-10.el6
jakarta-commons-pool.x86_64 0:1.3-12.7.el6             java-1.5.0-gcj.x86_64 0:1.5.0.0-29.1.el6
java_cup.x86_64 1:0.10k-5.el6                          libgcj.x86_64 0:4.4.6-3.el6
log4j.x86_64 0:1.2.14-6.4.el6                          mx4j.noarch 1:3.0.1-9.13.el6
regexp.x86_64 0:1.5-4.4.el6                            sinjdoc.x86_64 0:0.5-9.1.el6
tomcat6.noarch 0:6.0.24-33.el6                         tomcat6-el-2.1-api.noarch 0:6.0.24-33.el6
tomcat6-jsp-2.1-api.noarch 0:6.0.24-33.el6             tomcat6-lib.noarch 0:6.0.24-33.el6
tomcat6-servlet-2.5-api.noarch 0:6.0.24-33.el6         ws-commons-util.noarch 0:1.0.1-13.el6
wsdl4j.noarch 0:1.5.2-7.8.el6                          xml-commons-apis.x86_64 0:1.3.04-3.6.el6
xml-commons-resolver.x86_64 0:1.1-4.18.el6

Complete!
Done
[/shell]
以上的命令表示管理服务器组件正常安装成功。

下面需要安装数据库部分，再次运行安装脚本：
[shell]
./install
> 选择 d
Installing the MySQL server...
Loaded plugins: product-id, refresh-packagekit, security, subscription-manager
Updating certificate-based repositories.
cloud-temp                                                                          | 2.6 kB     00:00 ...
rhel6                                                                               | 4.0 kB     00:00 ...
Setting up Install Process
Package mysql-server-5.1.52-1.el6_0.1.x86_64 already installed and latest version
Nothing to do
Starting the MySQL server...
初始化 MySQL 数据库： Installing MySQL system tables...
OK
Filling help tables...
OK

To start mysqld at boot time you have to copy
support-files/mysql.server to the right place for your system

PLEASE REMEMBER TO SET A PASSWORD FOR THE MySQL root USER !
To do so, start the server, then issue the following commands:

/usr/bin/mysqladmin -u root password 'new-password'
/usr/bin/mysqladmin -u root -h cloudstack.xen.cn password 'new-password'

Alternatively you can run:
/usr/bin/mysql_secure_installation

which will also give you the option of removing the test
databases and anonymous user created by default.  This is
strongly recommended for production servers.

See the manual for more instructions.

You can start the MySQL daemon with:
cd /usr ; /usr/bin/mysqld_safe &

You can test the MySQL daemon with mysql-test-run.pl
cd /usr/mysql-test ; perl mysql-test-run.pl

Please report any problems with the /usr/bin/mysqlbug script!

[确定]
正在启动 mysqld：                                          [确定]
Done
[/shell]

以上表明数据库部分安装成功，还需要把mysql的几个参数调整一下，编辑配置文件，实例文件如下

[shell]
cat /etc/my.cfn
[mysqld]
datadir=/var/lib/mysql
#加入的部分
innodb_rollback_on_timeout=1
innodb_lock_wait_timeout=600
max_connections=350
log-bin=mysql-bin
binlog-format = 'ROW'
#加入的部分
socket=/var/lib/mysql/mysql.sock
user=mysql
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0

[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
[/shell]
重启动mysql让参数生效：
[shell]
[root@cloudstack CloudStack-oss-3.0.2-1-rhel6.2] service mysqld restart
停止 mysqld：                                              [确定]
正在启动 mysqld：                                          [确定]
[/shell]
给mysql的root用户设置密码
[shell]
[root@cloudstack home] mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.1.52-log Source distribution

Copyright (c) 2000, 2010, Oracle and/or its affiliates. All rights reserved.
This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL v2 license

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> set password = password('citrix');
Query OK, 0 rows affected (0.00 sec)

mysql> exit
Bye
[/shell]
初始化Cloudtack管理服务器的数据库
[shell]
[root@cloudstack home] cloud-setup-databases cloud:citrix@localhost --deploy-as=root:citrix
Mysql user name:cloud                                                           [ OK ]
Mysql user password:citrix                                                      [ OK ]
Mysql server ip:localhost                                                       [ OK ]
Mysql server port:3306                                                          [ OK ]
Mysql root user name:root                                                       [ OK ]
Mysql root user password:citrix                                                 [ OK ]
Checking Cloud database files ...                                               [ OK ]
Checking local machine hostname ...                                             [ OK ]
Checking SELinux setup ...                                                      [ OK ]
Detected local IP address as 192.168.10.15, will use as cluster management server node IP[ OK ]
Preparing /etc/cloud/management/db.properties                                   [ OK ]
Applying /usr/share/cloud/setup/create-database.sql                             [ OK ]
Applying /usr/share/cloud/setup/create-schema.sql                               [ OK ]
Applying /usr/share/cloud/setup/create-database-premium.sql                     [ OK ]
Applying /usr/share/cloud/setup/create-schema-premium.sql                       [ OK ]
Applying /usr/share/cloud/setup/server-setup.sql                                [ OK ]
Applying /usr/share/cloud/setup/templates.sql                                   [ OK ]
Applying /usr/share/cloud/setup/create-index-fk.sql                             [ OK ]
Processing encryption ...                                                       [ OK ]
Finalizing setup ...                                                            [ OK ]

CloudStack has successfully initialized database, you can check your database configuration in /etc/cloud/management/db.properties
[/shell]
数据库初始化完毕，下面需要运行管理服务器初始化命令。
[shell]
[root@cloudstack home] cloud-setup-management
Starting to configure CloudStack Management Server:
Configure sudoers ...         [OK]
Configure Firewall ...        [OK]
Configure CloudStack Management Server ...[OK]
CloudStack Management Server setup is Done!
[/shell]

以上管理节点的部分安装完毕。安装文档的需求，管理服务器需要挂一个16TB大小的NFS存储，如果环境中没有这个大的存储建议，使用足够大的硬盘做一个NFS的share用来测试，下面是相关的命令
[shell]
[root@cloudstack ~] service rpcbind start
[root@cloudstack ~] service nfs start
启动 NFS 服务：                                            [确定]
关掉 NFS 配额：                                            [确定]
启动 NFS 守护进程：                                        [确定]
启动 NFS mountd：                                          [确定]
[root@cloudstack ~] chkconfig nfs on
[root@cloudstack ~] chkconfig rpcbind on
[root@cloudstack home] cd /home
[root@cloudstack home] mkdir primary
[root@cloudstack home] mkdir secondary
[root@cloudstack home] vi /etc/exports   #编辑nfs路径
[root@cloudstack home] cat /etc/exports  #实例如下
/home    *(rw,async,no_root_squash)
[root@cloudstack home] exportfs -a    #检查nfs共享目录的结果
[root@cloudstack home] exportfs
/home             <world>
[/shell]

编辑 /etc/sysconfig/nfs 配置文件，保证它包含一下这些参数
[shell]
MOUNTD_NFS_V3="yes"
LOCKD_TCPPORT=32803
LOCKD_UDPPORT=32769
MOUNTD_PORT=892
RQUOTAD_PORT=875
STATD_PORT=662
STATD_OUTGOING_PORT=2020
[/shell]
重新启动nfs服务，在一个已经安装好的XenServer上做一下测试。保证Xenerver能够正常读写这个目录，相关命令如下：
[shell]
[root@xs root]mkdir test
[root@xs root]mount 192.168.10.15:/home  /root/test
[root@xs root]ls test
[root@xs root]touch testfile   #这个文件应该在两边的都能ls到
[/shell]

在保证管理服务器能上网的情况下，运行如下命令，为管理服务器从网上下载相关的模板文件
[shell]
/usr/lib64/cloud/agent/scripts/storage/secondary/cloud-install-sys-tmplt -m /home/secondary -u http://download.cloud.com/templates/acton/acton-systemvm-02062012.vhd.bz2 -h xenserver -F
正在解析主机 download.cloud.com... 207.171.189.81
正在连接 download.cloud.com|207.171.189.81|:80... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：140616708 (134M) [binary/octet-stream]

99% [===================================================================================================> ] 140,512,160  149K/s eta(英国中部时
99% [===================================================================================================> ] 140,551,600  145K/s eta(英国中部时
100%[====================================================================================================>] 140,616,708  155K/s   in 11m 27s
2012-06-29 20:03:57 (200 KB/s) - 已保存 “/usr/lib64/cloud/agent/scripts/storage/secondary/a5fc3577-c5e7-49ff-8fbf-ed88dc8aaff5.vhd” [140616708/140616708])

Uncompressing to /usr/lib64/cloud/agent/scripts/storage/secondary/a5fc3577-c5e7-49ff-8fbf-ed88dc8aaff5.vhd.tmp (type bz2)...could take a long time
Moving to /home/secondary/template/tmpl/1/1///a5fc3577-c5e7-49ff-8fbf-ed88dc8aaff5.vhd...could take a while
Successfully installed system VM template  to /home/secondary/template/tmpl/1/1/
[/shell]
到下载的路径下面ls一下，确认下载成功。

下面选择一台配置好的服务器来安装XenServer，这台服务器最好也能上网，和管理节点的服务器在一个网段里。
安装注意事项：

	
  1. 下载最新版的6.0.201安装盘，最新版的cloudstack必须要这个版本以上的xenserver

	
  2. 网络配置为能上网的设置，方便下载东西

	
  3. 用ntp服务器 0~3.xenserver.pool.ntp.org


安装后从管理服务器上ssh到xenServer命令行，需要下载cloudstack相关的安装包。执行如下命令：
[shell]
[root@cloudstack .ssh]# ssh 192.168.10.10   #这是xenserver的地址
The authenticity of host '192.168.10.10 (192.168.10.10)' can't be established.
RSA key fingerprint is ae:5b:8a:dc:2a:c8:6c:56:f6:7a:48:02:e6:db:78:dd.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.10.10' (RSA) to the list of known hosts.
root@192.168.10.10's password:
Type "xsconsole" for access to the management console.
[root@hpxs1 ~] pwd
/root
[root@hpxs1 ~] mkdir tmp
[root@hpxs1 ~] cd tmp
[root@hpxs1 tmp] wget http://download.cloud.com/releases/3.0.1/XS-6.0.2/xenserver-cloud-supp.tgz
--2012-06-29 21:55:08--  http://download.cloud.com/releases/3.0.1/XS-6.0.2/xenserver-cloud-supp.tgz
Resolving download.cloud.com... 207.171.185.201
Connecting to download.cloud.com|207.171.185.201|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3342001 (3.2M) [application/x-tar]
Saving to: `xenserver-cloud-supp.tgz'

100%[================================================================>] 3,342,001    217K/s   in 15s

2012-06-29 21:55:49 (214 KB/s) - `xenserver-cloud-supp.tgz' saved [3342001/3342001]
[root@hpxs1 tmp] tar xf xenserver-cloud-supp.tgz
[root@hpxs1 tmp] ls
example-answerfile   post-install.sh  src                       xenserver-cloud-supp.tgz
packages.cloud-supp  README           xenserver-cloud-supp.iso
[root@hpxs1 tmp] xe-install-supplemental-pack xenserver-cloud-supp.iso
Installing 'XenServer Cloud Supp Pack'...

Preparing...                ########################################### [100%]
1:iptables               ########################################### [ 10%]
2:iptables-ipv6          ########################################### [ 20%]
3:arptables              ########################################### [ 30%]
4:iptables-debuginfo     ########################################### [ 40%]
5:ipset-modules-kdump-2.6########################################### [ 50%]
6:ipset-modules-xen-2.6.3########################################### [ 60%]
7:csp-pack               ########################################### [ 70%]
8:ebtables               ########################################### [ 80%]
9:ipset                  ########################################### [ 90%]
10:iptables-devel         ########################################### [100%]
Update sysctl to enable *tables checking
Memory required by all installed packages: 894697472
Truncating to static-max: 789839872
Setting VM.memory_target: 789839872
Pack installation successful.
[root@hpxs1 tmp]
[root@hpxs1 tmp] xe-switch-network-backend bridge
Cleaning up old ifcfg files
Remove... ifcfg-xenbr0
Disabling openvswitch daemon
Configure system for bridge networking
You *MUST* now reboot your system
[root@hpxs1 tmp] reboot
[/shell]
测试xenserver是否能够正常链接管理服务器的nfs目录
[shell]
[root@hpxs1 ~] mkdir nfs
[root@hpxs1 ~] mount 192.168.10.15:/home/primary /root/nfs
[root@hpxs1 ~] cd nfs
[root@hpxs1 nfs] touch testfile
[root@hpxs1 nfs] ls
testfile   #到管理服务器端查看是否有该文件存在
[/shell]
下面进入图形界面的初始化屏幕。进入之后的配置向导如下图集所示。
[nggallery id=14]
