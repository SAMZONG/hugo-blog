---
title: HowTo Install Python3 on CentOS 6.x
tags: 
    - Python
    - CentOS
categories: 
    - Python
abbrlink: 36731
date: 2016-12-08 20:12:37
---

接触过Python2.x与Python3.x的应该知道，它们二者的区别也是蛮大的，而随着Python3.x的盛行，越来越多的应用运行与Python3.x的环境之上，但是我们的CentOS的系列，目前都默认安装时Python2.x（CentOS 7.x也是），所以不得不我们需要自己行动手安装Python 3.x的环境。

Mirosoft平台与Mac平台，不在考虑范围，他们都有相应的软件包与图形化安装工具，可以很好的解决这个问题，所以今天我们的环境是在CentOS 6.x系列上进行。

> Demo ：CentOS 6.8

#### Method 1. Build & Install From Source-File

1. Python3.x 源码文件下载，请选择适合的版本。 [下载页面](https://www.python.org/ftp/python/)
2. 我这里使用版本 Python 3.5
```
[cent@demo ~]$ wget https://www.python.org/ftp/python/3.5.0/Python-3.5.0.tgz
```
3. 安装系统基本工具：
```
# yum-utils
[cent@demo ~]$ sudo yum install -y yum-utils

# 构建python 编译环境
[cent@demo ~]$ sudo yum-builddep python
```
4. 开始编译 & 安装
并且源码安装的同时，会将pip3与setuptools一同安装.
```
[cent@demo ~]$ tar xf Python-3.5.0.tgz
[cent@demo ~]$ cd Python-3.5.0
[cent@demo ~]$ ./configure
[cent@demo ~]$ make
[cent@demo ~]$ sudo make install
```
5. 检查版本
```
[cent@demo ~]$ python3 -V
Python 3.5.0

# 如果希望系统默认为Python3
[cent@demo ~]$ alias python='usr/bin/python3.5'
```

#### Method 2. Install From EPEL repos
也许有的同学会说，编译安装，那是上古时期的做法了，yum在线安装才是王道，当然这种说法也有可取之处，所以接下来讲下如何使用yum安装，需要注意的是yum安装是需要时间测试和增加到相应的源仓库，一般会稍慢于源码安装的方式，这里采用EPEL源，这是一个非常棒的第三方源仓库，之前的文章中也多次提到，这里就不做过多描述，请看下面的命令：
```
[cent@demo ~]$ sudo yum install -y epel-release
[cent@demo ~]$ sudo yum install -y python34

# 因为yum安装时没能同时安装pip与setuptools，所以我们要手动安装，这里采用拿第三方包解决问题

[cent@demo ~]$ curl -O https://bootstrap.pypa.io/get-pip.py
[cent@demo ~]$ sudo python3 get-pip.py

[cent@demo ~]$  python3 -V
Python 3.4.3
```
