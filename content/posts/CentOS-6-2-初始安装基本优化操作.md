---
title: CentOS 初始安装基本优化操作
tags: 
  - Linux 
  - CentOS
categories:
  - Linux
  - CentOS
abbrlink: 54297
date: 2016-03-19 05:54:23
---

## CentOS 6.x 初始安装基本优化操作

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本文件是采用的模板是centos 6.x，相较于centos 5.x与centos 7.x系列有些区别，不能一概而论。

### 1. 测试环境

* MacBook Pro 15-inch i7 8GB
* VMware Fushion 8 Pro
* CentOS-6.7-x86_64-minimal.iso

### 2. 默认网卡开机未设定自启动
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;很多初学者，在安装系统的时候，碰到的第一个问题就是不能上网，所以有些同学就担心是不是需要去安装网卡驱动，其实这样想就把问题复杂化了，如果你在实体机安装Linux的系统时，可能会碰到网卡驱动不上导致无法上网的问题，这个时候是需要自行安装驱动的，但是我们使用的VMware的一款虚拟化工具，所以网卡驱动基本就不用考虑，原因是因为我们没有把网卡设置为开机自启动，下面讲如何开启网卡，并设定为开机自启动。

```
[root@vm02 ~]# ifup eth0

Determining IP information for eth0... done.
[root@vm02 ~]# 
[root@vm02 ~]# ifconfig eth0
eth0      Link encap:Ethernet  HWaddr 00:0C:29:B9:60:D8
          inet addr:172.16.102.129  Bcast:172.16.102.255  Mask:255.255.255.0
          inet6 addr: fe80::20c:29ff:feb9:60d8/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:127 errors:0 dropped:0 overruns:0 frame:0
          TX packets:85 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:14010 (13.6 KiB)  TX bytes:11410 (11.1 KiB)
          
[root@vm02 ~]# vi /etc/sysconfig/network-scripts/ifcfg-eth0
	DEVICE=eth0
	HWADDR=00:0C:29:B9:60:D8
	TYPE=Ethernet
	UUID=7ad636ff-78d9-4afa-9886-706b1de236a8
	ONBOOT=no		 // 默认是no，修改为yes
	NM_CONTROLLED=yes
	BOOTPROTO=dhcp

```

### 3. 增加第三方Yum源
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CentOS 系统内置的官方源软件更新较慢，而且缺少一些常用软件包，建议安装epel源，EPEL 是 Extra Packages for Enterprise Linux 的缩写（EPEL），是用于 Fedora-based Red Hat Enterprise Linux (RHEL) 的一个高质量软件源，所以同时也适用于 CentOS 或者 Scientific Linux 等发行版。

##### a. 因为我们使用的是minimal版本的ISO安装，所以系统默认没有wget，我们可以直接用yum安装：[wget是Linux常用的命令行下载工具]

```
[root@vm02 ~]# yum install -y wget
Loaded plugins: fastestmirror
Setting up Install Process
base                                                     | 3.7 kB     00:00
base/primary_db                                          | 4.6 MB     00:32
extras                                                   | 3.4 kB     00:00
extras/primary_db                                        |  34 kB     00:00
updates                                                  | 3.4 kB     00:00
updates/primary_db                                       | 4.0 MB     01:05
Resolving Dependencies
--> Running transaction check
---> Package wget.x86_64 0:1.12-5.el6_6.1 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package        Arch             Version                   Repository      Size
================================================================================
Installing:
 wget           x86_64           1.12-5.el6_6.1            base           483 k

Transaction Summary
================================================================================
Install       1 Package(s)

Total download size: 483 k
Installed size: 1.8 M
Downloading Packages:
wget-1.12-5.el6_6.1.x86_64.rpm                           | 483 kB     00:01
warning: rpmts_HdrFromFdno: Header V3 RSA/SHA1 Signature, key ID c105b9de: NOKEY
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
Importing GPG key 0xC105B9DE:
 Userid : CentOS-6 Key (CentOS 6 Official Signing Key) <centos-6-key@centos.org>
 Package: centos-release-6-7.el6.centos.12.3.x86_64 (@anaconda-CentOS-201508042137.x86_64/6.7)
 From   : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing : wget-1.12-5.el6_6.1.x86_64                                   1/1
  Verifying  : wget-1.12-5.el6_6.1.x86_64                                   1/1

Installed:
  wget.x86_64 0:1.12-5.el6_6.1

Complete!
[root@vm02 ~]#
```
##### b. 下载并安装epel源
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;不同CentOS版本的epel下载地址：

* CentOS 5 ： https://dl.fedoraproject.org/pub/epel/epel-release-latest-5.noarch.rpm
* CentOS 6 ： https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
* CentOS 7 ： https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本次试验用到的CentOS 6 所以我们下载epel-release-latest-6.noarch.rpm

```
[root@vm02 ~]# wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
--2016-03-18 11:47:17--  https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
Resolving dl.fedoraproject.org... 209.132.181.26, 209.132.181.23, 209.132.181.24, ...
Connecting to dl.fedoraproject.org|209.132.181.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 14540 (14K) [application/x-rpm]
Saving to: “epel-release-latest-6.noarch.rpm”

100%[======================================>] 14,540      69.5K/s   in 0.2s

2016-03-18 11:47:25 (69.5 KB/s) - “epel-release-latest-6.noarch.rpm” saved [14540/14540]

[root@vm02 ~]# ls
anaconda-ks.cfg                   install.log
epel-release-latest-6.noarch.rpm  install.log.syslog
```

### 4. 安装vim：Linux使用最广泛的文件编辑工具
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;与我们长久使用Win环境不同的是，在Linux之中，我们接触最多的是command line，所以熟练一款命令行下的文本编辑工具是一项必备技能，我这里推荐大家：vim。

```
[root@vm02 ~]# yum install -y vim
Loaded plugins: fastestmirror
Setting up Install Process
Determining fastest mirrors
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
Resolving Dependencies
--> Running transaction check
---> Package vim-enhanced.x86_64 2:7.4.629-5.el6 will be installed
--> Processing Dependency: vim-common = 2:7.4.629-5.el6 for package: 2:vim-enhanced-7.4.629-5.el6.x86_64
--> Processing Dependency: perl(:MODULE_COMPAT_5.10.1) for package: 2:vim-enhanced-7.4.629-5.el6.x86_64
--> Processing Dependency: libperl.so()(64bit) for package: 2:vim-enhanced-7.4.629-5.el6.x86_64
--> Processing Dependency: libgpm.so.2()(64bit) for package: 2:vim-enhanced-7.4.629-5.el6.x86_64
--> Running transaction check
---> Package gpm-libs.x86_64 0:1.20.6-12.el6 will be installed
---> Package perl.x86_64 4:5.10.1-141.el6_7.1 will be installed
--> Processing Dependency: perl(version) for package: 4:perl-5.10.1-141.el6_7.1.x86_64
--> Processing Dependency: perl(Pod::Simple) for package: 4:perl-5.10.1-141.el6_7.1.x86_64
--> Processing Dependency: perl(Module::Pluggable) for package: 4:perl-5.10.1-141.el6_7.1.x86_64
---> Package perl-libs.x86_64 4:5.10.1-141.el6_7.1 will be installed
---> Package vim-common.x86_64 2:7.4.629-5.el6 will be installed
--> Processing Dependency: vim-filesystem for package: 2:vim-common-7.4.629-5.el6.x86_64
--> Running transaction check
---> Package perl-Module-Pluggable.x86_64 1:3.90-141.el6_7.1 will be installed
---> Package perl-Pod-Simple.x86_64 1:3.13-141.el6_7.1 will be installed
--> Processing Dependency: perl(Pod::Escapes) >= 1.04 for package: 1:perl-Pod-Simple-3.13-141.el6_7.1.x86_64
---> Package perl-version.x86_64 3:0.77-141.el6_7.1 will be installed
---> Package vim-filesystem.x86_64 2:7.4.629-5.el6 will be installed
--> Running transaction check
---> Package perl-Pod-Escapes.x86_64 1:1.04-141.el6_7.1 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=============================================================================================================================================================================
 Package                                          Arch                              Version                                         Repository                          Size
=============================================================================================================================================================================
Installing:
 vim-enhanced                                     x86_64                            2:7.4.629-5.el6                                 base                               1.0 M
Installing for dependencies:
 gpm-libs                                         x86_64                            1.20.6-12.el6                                   base                                28 k
 perl                                             x86_64                            4:5.10.1-141.el6_7.1                            updates                             10 M
 perl-Module-Pluggable                            x86_64                            1:3.90-141.el6_7.1                              updates                             40 k
 perl-Pod-Escapes                                 x86_64                            1:1.04-141.el6_7.1                              updates                             33 k
 perl-Pod-Simple                                  x86_64                            1:3.13-141.el6_7.1                              updates                            213 k
 perl-libs                                        x86_64                            4:5.10.1-141.el6_7.1                            updates                            579 k
 perl-version                                     x86_64                            3:0.77-141.el6_7.1                              updates                             52 k
 vim-common                                       x86_64                            2:7.4.629-5.el6                                 base                               6.7 M
 vim-filesystem                                   x86_64                            2:7.4.629-5.el6                                 base                                15 k

Transaction Summary
=============================================================================================================================================================================
Install      10 Package(s)

Total download size: 19 M
Installed size: 59 M
Downloading Packages:
(1/10): gpm-libs-1.20.6-12.el6.x86_64.rpm                                                                                                             |  28 kB     00:00
(2/10): perl-5.10.1-141.el6_7.1.x86_64.rpm                                                                                                            |  10 MB     00:10
(3/10): perl-Module-Pluggable-3.90-141.el6_7.1.x86_64.rpm                                                                                             |  40 kB     00:00
(4/10): perl-Pod-Escapes-1.04-141.el6_7.1.x86_64.rpm                                                                                                  |  33 kB     00:00
(5/10): perl-Pod-Simple-3.13-141.el6_7.1.x86_64.rpm                                                                                                   | 213 kB     00:00
(6/10): perl-libs-5.10.1-141.el6_7.1.x86_64.rpm                                                                                                       | 579 kB     00:00
(7/10): perl-version-0.77-141.el6_7.1.x86_64.rpm                                                                                                      |  52 kB     00:00
(8/10): vim-common-7.4.629-5.el6.x86_64.rpm                                                                                                           | 6.7 MB     00:07
(9/10): vim-enhanced-7.4.629-5.el6.x86_64.rpm                                                                                                         | 1.0 MB     00:01
(10/10): vim-filesystem-7.4.629-5.el6.x86_64.rpm                                                                                                      |  15 kB     00:00
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                        980 kB/s |  19 MB     00:19
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing : 1:perl-Pod-Escapes-1.04-141.el6_7.1.x86_64                                                                                                               1/10
  Installing : 1:perl-Module-Pluggable-3.90-141.el6_7.1.x86_64                                                                                                          2/10
  Installing : 3:perl-version-0.77-141.el6_7.1.x86_64                                                                                                                   3/10
  Installing : 4:perl-libs-5.10.1-141.el6_7.1.x86_64                                                                                                                    4/10
  Installing : 1:perl-Pod-Simple-3.13-141.el6_7.1.x86_64                                                                                                                5/10
  Installing : 4:perl-5.10.1-141.el6_7.1.x86_64                                                                                                                         6/10
  Installing : 2:vim-filesystem-7.4.629-5.el6.x86_64                                                                                                                    7/10
  Installing : 2:vim-common-7.4.629-5.el6.x86_64                                                                                                                        8/10
  Installing : gpm-libs-1.20.6-12.el6.x86_64                                                                                                                            9/10
  Installing : 2:vim-enhanced-7.4.629-5.el6.x86_64                                                                                                                     10/10
  Verifying  : 1:perl-Pod-Simple-3.13-141.el6_7.1.x86_64                                                                                                                1/10
  Verifying  : 1:perl-Pod-Escapes-1.04-141.el6_7.1.x86_64                                                                                                               2/10
  Verifying  : gpm-libs-1.20.6-12.el6.x86_64                                                                                                                            3/10
  Verifying  : 2:vim-enhanced-7.4.629-5.el6.x86_64                                                                                                                      4/10
  Verifying  : 2:vim-filesystem-7.4.629-5.el6.x86_64                                                                                                                    5/10
  Verifying  : 1:perl-Module-Pluggable-3.90-141.el6_7.1.x86_64                                                                                                          6/10
  Verifying  : 2:vim-common-7.4.629-5.el6.x86_64                                                                                                                        7/10
  Verifying  : 3:perl-version-0.77-141.el6_7.1.x86_64                                                                                                                   8/10
  Verifying  : 4:perl-libs-5.10.1-141.el6_7.1.x86_64                                                                                                                    9/10
  Verifying  : 4:perl-5.10.1-141.el6_7.1.x86_64                                                                                                                        10/10

Installed:
  vim-enhanced.x86_64 2:7.4.629-5.el6

Dependency Installed:
  gpm-libs.x86_64 0:1.20.6-12.el6           perl.x86_64 4:5.10.1-141.el6_7.1      perl-Module-Pluggable.x86_64 1:3.90-141.el6_7.1 perl-Pod-Escapes.x86_64 1:1.04-141.el6_7.1
  perl-Pod-Simple.x86_64 1:3.13-141.el6_7.1 perl-libs.x86_64 4:5.10.1-141.el6_7.1 perl-version.x86_64 3:0.77-141.el6_7.1          vim-common.x86_64 2:7.4.629-5.el6
  vim-filesystem.x86_64 2:7.4.629-5.el6

Complete!
[root@vm02 ~]#

```

### 4. 关闭SELinux
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELinux主要由美国国家安全局开发，并于2000年12月22日发行给开放源代码的开发社区。SELinux旨在加强访问控制架构以对付入侵的威胁或任何企图略过安全架构的应用程序，并且从2.6版的Linux核心就开始集成SELinux；但是SELinux严格的权限控制对于初学者来说并不是非常必要，所以我们建议关闭SELinux，[其实由于SELinux的复杂性，很多运维人员都是选择关闭它，熟悉阿里云ECS的同学可能知道，它是默认关闭SELinux的，但是我们不建议在生产环境关闭SELinux。]

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELinux的配置文件主要由两个：/etc/sysconfig/selinux、 /etc/selinux/config，其实第一个是第二个路径的软链接。

```
[root@vm02 ~]# vim /etc/selinux/config
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=enforcing
# SELINUXTYPE= can take one of these two values:
#     targeted - Targeted processes are protected,
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted

```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELinux 的状态模式：

* enforcing : 强制启用SELinux
* permissive : 只显示警告讯息以替代强制启用SELinux
* disabled : 停用SELinux

>Tips: SELinux的参数只能在重启后生效。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELinux 常用的两个命令：getenforce setenforce :

* getenforce 获得SELinux 当前的状态，返回值为如上三种；
* setenforce 临时改变SELinux的状态，参数为布尔值，0是关闭，1是开启。

> Tips: 状态已经为disabled时，无法使用setenforce 1 启用。


### 5. 

### 6.
 
### 7.

### 8.