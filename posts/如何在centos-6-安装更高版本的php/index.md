# 如何在CentOS 6 安装更高版本的PHP


<p>
CentOS 6 默认安装的PHP 版本是5.3， 但现在很多应用对于LAMP中，PHP的版本最低5.4，所以本篇文章的主要内容是，如何升级PHP5.3到5.4以及更高版本
 </p>

## 实验环境：CentOS 6.4

解决办法是采用了remi源仓库已经适配的相应php版本

> 经过测试，该升级办法同样适用目前CentOS 6.x 所有版本

#### 1. 安装Remi源
```
# 因为remi依赖epel源仓库，所有我们要先安装它。
[root@visionet8 ~]# yum install -y epel-release

[root@visionet8 ~]# wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
[root@visionet8 ~]# rpm -Uvh remi-release-6.rpm
```

#### 2. 我们看下Remi的的yum配置文件
```
# Repository: http://rpms.remirepo.net/
# Blog:       http://blog.remirepo.net/
# Forum:      http://forum.remirepo.net/

[remi]
name=Remi's RPM repository for Enterprise Linux 6 - $basearch
baseurl=http://rpms.remirepo.net/enterprise/6/remi/$basearch/
#mirrorlist=http://rpms.remirepo.net/enterprise/6/remi/mirror
enabled=1
gpgcheck=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi

[remi-php55]
name=Remi's PHP 5.5 RPM repository for Enterprise Linux 6 - $basearch
#baseurl=http://rpms.remirepo.net/enterprise/6/php55/$basearch/
mirrorlist=http://rpms.remirepo.net/enterprise/6/php55/mirror
# NOTICE: common dependencies are in "remi-safe"
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi

[remi-php56]
name=Remi's PHP 5.6 RPM repository for Enterprise Linux 6 - $basearch
#baseurl=http://rpms.remirepo.net/enterprise/6/php56/$basearch/
mirrorlist=http://rpms.remirepo.net/enterprise/6/php56/mirror
# NOTICE: common dependencies are in "remi-safe"
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi
```

经过测试，启用remi源之后，默认情况下php版本为5.4,这时我们只需要升级php即可。

```
[root@visionet8 html]# yum update -y php*
Failed to set locale, defaulting to C
Loaded plugins: fastestmirror, refresh-packagekit, security
Loading mirror speeds from cached hostfile
 * base: mirrors.163.com
 * epel: mirrors.ustc.edu.cn
 * extras: mirrors.aliyun.com
 * remi-safe: mirrors.tuna.tsinghua.edu.cn
 * updates: mirrors.cn99.com
remi                                                                               | 2.9 kB     00:00
remi/primary_db                                                                    | 1.6 MB     00:05
Setting up Update Process
Resolving Dependencies
--> Running transaction check
---> Package php.x86_64 0:5.3.3-48.el6_8 will be updated
---> Package php.x86_64 0:5.4.45-12.el6.remi will be an update
---> Package php-cli.x86_64 0:5.3.3-48.el6_8 will be updated
---> Package php-cli.x86_64 0:5.4.45-12.el6.remi will be an update
---> Package php-common.x86_64 0:5.3.3-48.el6_8 will be updated
---> Package php-common.x86_64 0:5.4.45-12.el6.remi will be an update
---> Package php-gd.x86_64 0:5.3.3-48.el6_8 will be updated
---> Package php-gd.x86_64 0:5.4.45-12.el6.remi will be an update
--> Processing Dependency: libt1.so.5()(64bit) for package: php-gd-5.4.45-12.el6.remi.x86_64
---> Package php-mcrypt.x86_64 0:5.3.3-4.el6 will be updated
---> Package php-mcrypt.x86_64 0:5.4.45-12.el6.remi will be an update
---> Package php-mysql.x86_64 0:5.3.3-48.el6_8 will be updated
---> Package php-mysql.x86_64 0:5.4.45-12.el6.remi will be an update
---> Package php-pdo.x86_64 0:5.3.3-48.el6_8 will be updated
---> Package php-pdo.x86_64 0:5.4.45-12.el6.remi will be an update
--> Running transaction check
---> Package t1lib.x86_64 0:5.1.2-6.el6_2.1 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

==========================================================================================================
 Package                  Arch                 Version                           Repository          Size
==========================================================================================================
Updating:
 php                      x86_64               5.4.45-12.el6.remi                remi               2.8 M
 php-cli                  x86_64               5.4.45-12.el6.remi                remi               4.1 M
 php-common               x86_64               5.4.45-12.el6.remi                remi               968 k
 php-gd                   x86_64               5.4.45-12.el6.remi                remi               152 k
 php-mcrypt               x86_64               5.4.45-12.el6.remi                remi                60 k
 php-mysql                x86_64               5.4.45-12.el6.remi                remi               145 k
 php-pdo                  x86_64               5.4.45-12.el6.remi                remi               129 k
Installing for dependencies:
 t1lib                    x86_64               5.1.2-6.el6_2.1                   base               160 k

Transaction Summary
==========================================================================================================
Install       1 Package(s)
Upgrade       7 Package(s)

Total download size: 8.5 M
Downloading Packages:
(1/8): php-5.4.45-12.el6.remi.x86_64.rpm                                           | 2.8 MB     00:07
(2/8): php-cli-5.4.45-12.el6.remi.x86_64.rpm                                       | 4.1 MB     00:06
(3/8): php-common-5.4.45-12.el6.remi.x86_64.rpm                                    | 968 kB     00:02
(4/8): php-gd-5.4.45-12.el6.remi.x86_64.rpm                                        | 152 kB     00:01
(5/8): php-mcrypt-5.4.45-12.el6.remi.x86_64.rpm                                    |  60 kB     00:00
(6/8): php-mysql-5.4.45-12.el6.remi.x86_64.rpm                                     | 145 kB     00:00
(7/8): php-pdo-5.4.45-12.el6.remi.x86_64.rpm                                       | 129 kB     00:01
(8/8): t1lib-5.1.2-6.el6_2.1.x86_64.rpm                                            | 160 kB     00:00
----------------------------------------------------------------------------------------------------------
Total                                                                     338 kB/s | 8.5 MB     00:25
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
Warning: RPMDB altered outside of yum.
  Updating   : php-common-5.4.45-12.el6.remi.x86_64                                                  1/15
  Updating   : php-cli-5.4.45-12.el6.remi.x86_64                                                     2/15
  Updating   : php-pdo-5.4.45-12.el6.remi.x86_64                                                     3/15
  Installing : t1lib-5.1.2-6.el6_2.1.x86_64                                                          4/15
  Updating   : php-gd-5.4.45-12.el6.remi.x86_64                                                      5/15
  Updating   : php-mysql-5.4.45-12.el6.remi.x86_64                                                   6/15
  Updating   : php-5.4.45-12.el6.remi.x86_64                                                         7/15
  Updating   : php-mcrypt-5.4.45-12.el6.remi.x86_64                                                  8/15
  Cleanup    : php-5.3.3-48.el6_8.x86_64                                                             9/15
  Cleanup    : php-mysql-5.3.3-48.el6_8.x86_64                                                      10/15
  Cleanup    : php-pdo-5.3.3-48.el6_8.x86_64                                                        11/15
  Cleanup    : php-cli-5.3.3-48.el6_8.x86_64                                                        12/15
  Cleanup    : php-gd-5.3.3-48.el6_8.x86_64                                                         13/15
  Cleanup    : php-mcrypt-5.3.3-4.el6.x86_64                                                        14/15
  Cleanup    : php-common-5.3.3-48.el6_8.x86_64                                                     15/15
  Verifying  : php-mcrypt-5.4.45-12.el6.remi.x86_64                                                  1/15
  Verifying  : t1lib-5.1.2-6.el6_2.1.x86_64                                                          2/15
  Verifying  : php-common-5.4.45-12.el6.remi.x86_64                                                  3/15
  Verifying  : php-gd-5.4.45-12.el6.remi.x86_64                                                      4/15
  Verifying  : php-cli-5.4.45-12.el6.remi.x86_64                                                     5/15
  Verifying  : php-pdo-5.4.45-12.el6.remi.x86_64                                                     6/15
  Verifying  : php-mysql-5.4.45-12.el6.remi.x86_64                                                   7/15
  Verifying  : php-5.4.45-12.el6.remi.x86_64                                                         8/15
  Verifying  : php-5.3.3-48.el6_8.x86_64                                                             9/15
  Verifying  : php-gd-5.3.3-48.el6_8.x86_64                                                         10/15
  Verifying  : php-cli-5.3.3-48.el6_8.x86_64                                                        11/15
  Verifying  : php-pdo-5.3.3-48.el6_8.x86_64                                                        12/15
  Verifying  : php-common-5.3.3-48.el6_8.x86_64                                                     13/15
  Verifying  : php-mysql-5.3.3-48.el6_8.x86_64                                                      14/15
  Verifying  : php-mcrypt-5.3.3-4.el6.x86_64                                                        15/15

Dependency Installed:
  t1lib.x86_64 0:5.1.2-6.el6_2.1

Updated:
  php.x86_64 0:5.4.45-12.el6.remi                      php-cli.x86_64 0:5.4.45-12.el6.remi
  php-common.x86_64 0:5.4.45-12.el6.remi               php-gd.x86_64 0:5.4.45-12.el6.remi
  php-mcrypt.x86_64 0:5.4.45-12.el6.remi               php-mysql.x86_64 0:5.4.45-12.el6.remi
  php-pdo.x86_64 0:5.4.45-12.el6.remi

Complete!
```

#### 3. 测试：
```
[root@visionet8 html]# php -v
PHP 5.4.45 (cli) (built: Sep 19 2016 15:31:07)
Copyright (c) 1997-2014 The PHP Group
Zend Engine v2.4.0, Copyright (c) 1998-2014 Zend Technologies
```

#### 4. php 5.5 和php5.6

>  若要升级到5.5 或 5.6，根据remi源的配置文件，将php5.5的enable参数设置为1，并将默认enable修改为0,然后<code>yum update php*</code>即可。
<hr/>


#### 5. php 7
> 安装完成之后发现, 在安装remi源之后，在<code>/etc/yum.repos.d</code>除了<code>remi.repo</code>之外，还有<code>remi-php70.repo</code>和<code>remi-php71.repo</code>，测试下，如果要升级到php7，可以打开相应源仓库的配置文件，之后升级即可。

<br>

> <b>以上功能在升级时，要考虑其他组件的版本兼容性，不要盲目升级。</b>

