---
author: liuadmin
comments: true
date: 2011-06-16 17:16:14+00:00
layout: post
slug: addm-8-2-ssh-key-deploy
title: ADDM 8.2 ssh key 生成和部署
wordpress_id: 51137
categories:
- BMC
tags:
- ADDM
- BMC
- cmdb
- keploy
- key
- ssh
---

## 生产密钥


用tideway用户登录ADDM服务器，运行下面的命令
[bash]
[tideway@localhost .ssh]$ ls
[tideway@localhost .ssh]$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/usr/tideway/.ssh/id_rsa):  “敲回车”
Enter passphrase (empty for no passphrase):  “敲回车”
Enter same passphrase again:  “敲回车”
Your identification has been saved in /usr/tideway/.ssh/id_rsa.
Your public key has been saved in /usr/tideway/.ssh/id_rsa.pub.
The key fingerprint is:
27:20:55:fc:f9:9a:41:35:11:ef:6d:b7:6c:4e:78:00 tideway@localhost.localdomain
[tideway@localhost .ssh]$ ls
id_rsa  id_rsa.pub
[tideway@localhost .ssh]$
[/bash]



## 下载和安装key文件部署工具


http://code.google.com/p/keploy/downloads/list
下载 keploy-0.5.tgz 
上传到ADDM服务器的/usr/tideway/.ssh目录中
[bash]
[tideway@localhost .ssh]$ ls
id_rsa  id_rsa.pub  keploy-0.5.tgz
[tideway@localhost .ssh]$ tar zxvf keploy-0.5.tgz
keploy-0.5/
keploy-0.5/keploy
keploy-0.5/LICENSE
keploy-0.5/README
keploy-0.5/INSTALL
keploy-0.5/CHANGELOG
[tideway@localhost .ssh]$ ls
id_rsa  id_rsa.pub  keploy-0.5  keploy-0.5.tgz
[tideway@localhost .ssh]$ cd keploy-0.5
[tideway@localhost keploy-0.5]$ ls
CHANGELOG  INSTALL  keploy  LICENSE  README
[tideway@localhost keploy-0.5]$ ./keploy -v

NOTICE: You may be prompted for you password,
NOTICE: this is directly from the ssh client, not keploy

Preparing to deploy ssh key...
ERROR: No targets defined.
[tideway@localhost keploy-0.5]$ ./keploy -h
Usage: keploy [options] [hosts]

Options:
  -i ID_FILE            specifies identity file
  -l USERID, --login=USERID
                        define userid for remote connections
  -f TARGET_FILE, --file=TARGET_FILE
                        read list of targets from file
  -k, --use-known       read list of targets from known_hosts files
  -r, --remove          remove primary identity from remote(s)
  -c OLD_ID_FILE, --change=OLD_ID_FILE
                        replace old identity with new one on remote(s)
  -A                    enable/disable agent forwarding on remote
  -v                    give verbose output
  -q, --quiet           quiet the output
  --version             show program's version number and exit
  -h, --help            show this help message and exit
[tideway@localhost keploy-0.5]$
[/bash]
在keploy-0.5生成一个文件hostlist，里面每一行放一台机器的IP，回头让工具自动读取该文件



## Linux被采集帐号准备


建议直接把ADDM采集机的key文件部署到root用户上，如果用户觉得这个做法不安全的话，我们可以建立一个不普通用户，把特权命令用sudo处理一下，下面是具体的做法


### 运行ssh的证书认证


用root登录被采集机，修改/etc/ssh/sshd_config文件，将如下参数的注释符号（#）去掉，以启用这些参数：
RSAAuthentication          yes
PubkeyAuthentication     yes
AuthorizedKeysFile         .ssh/authorized_keys
重启sshd服务
#/etc/init.d/sshd restart



### 配置sudo


Linux平台对采集账户需要配置sudo。以root用户登录被管服务器，修改/etc/sudoers文件，在文件末尾追加一行：
tideway  ALL=(root) NOPASSWD:/usr/sbin/dmidecode,/usr/sbin/hwinfo, /usr/sbin/hbanyware/hbacmd,/usr/sbin/lsof,/sbin/ethtool,/sbin/mii-tool



### 增加采集帐号tideway


操作步骤如下（以root用户登录服务器）：
[root@ars home]# useradd tideway
[root@ars home]# passwd tideway
Changing password for user tideway.
New UNIX password: “使用tideway做密码，采集成功后可以修改掉”
BAD PASSWORD: it is based on a dictionary word
Retype new UNIX password: “使用tideway做密码，采集成功后可以修改掉”
passwd: all authentication tokens updated successfully.
[root@ars home]#



## 部署ADDM ssh 密钥到被采集机




### 部署


在采集机部署前，查看/home/tideway 目录
[bash]
[root@ars home]# cd tideway/
[root@ars tideway]# pwd
/home/tideway
[root@ars tideway]# ls -la
total 36
drwx------ 3 tideway tideway 4096 Jun 17 00:55 .
drwxr-xr-x 4 root    root    4096 Jun 17 00:55 ..
-rw-r--r-- 1 tideway tideway   33 Jun 17 00:55 .bash_logout
-rw-r--r-- 1 tideway tideway  176 Jun 17 00:55 .bash_profile
-rw-r--r-- 1 tideway tideway  124 Jun 17 00:55 .bashrc
-rw-r--r-- 1 tideway tideway  515 Jun 17 00:55 .emacs
drwxr-xr-x 4 tideway tideway 4096 Jun 17 00:55 .mozilla
-rw-r--r-- 1 tideway tideway  658 Jun 17 00:55 .zshrc
[root@ars tideway]#
[/bash]
注意这里没有.ssh目录
开始使用我们下载的工具部署，登录到ADDM采集机上
[bash]
[tideway@localhost keploy-0.5]$ vi hostlist
[tideway@localhost keploy-0.5]$ cat hostlist
192.168.189.154
[tideway@localhost keploy-0.5]$ ./keploy -f hostlist

NOTICE: You may be prompted for you password,
NOTICE: this is directly from the ssh client, not keploy

Preparing to deploy ssh key...
Using user-defined host list from file: hostlist
./keploy:164: DeprecationWarning: os.popen3 is deprecated.  Use the subprocess module.
  si, so, se = os.popen3(execute)
        Found host(s):
                192.168.189.154
        Found identity:
                /usr/tideway/.ssh/id_rsa.pub
        Working on host: 192.168.189.154
The authenticity of host '192.168.189.154 (192.168.189.154)' can't be established.
RSA key fingerprint is de:4e:f0:c8:9b:86:ee:25:af:a9:1c:19:8f:20:90:ad.
Are you sure you want to continue connecting (yes/no)? yes
tideway@192.168.189.154's password:  "输入目标机上tideway用户的密码，我用的是tideway"
                Public Identity Key: deployed
[tideway@localhost keploy-0.5]$
[/bash]
可以到被采集机的/home/tideway/.ssh下面看看传过去的正式文件，这种方式极大的避免了，手工创建.ssh目录，设置它和key文件权限的工作量


### 验证


在采集机上，使用tideway用户登录被采集服务器。
[bash]
[tideway@localhost keploy-0.5]$ ssh 192.168.189.154
Last login: Fri Jun 17 01:08:21 2011 from 192.168.189.147
[tideway@ars ~]$
[/bash]
