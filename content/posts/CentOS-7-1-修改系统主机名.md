---
title: CentOS 修改系统主机名
tags: 
    - CentOS
categories: 
    - Linux
    - CentOS
abbrlink: 45128
date: 2016-05-05 05:41:39
---

## CentOS 7 修改主机名

### 方法1: <code> hostname 主机名</code>

这种方式，只能修改临时的主机名，当重启机器后，主机名称又变回来了。


### 方法2: <code> hostnamectl set-hostname <主机名>  </code>

使用这种方式修改，可以永久性的修改主机名称！
