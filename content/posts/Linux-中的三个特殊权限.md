---
title: Linux 中的三个特殊权限
tags: 
    - Linux
categories: 
    - Linux
abbrlink: 21394
date: 2016-03-29 07:50:36
---



```
Linux中除了普通权限之外，还有三个特殊权限。
SUID:：以文件的所属用户执行，而非执行文件的用户，多用于可执行文件，设置suid后，在权限位中，所属用户的  最后一个权
限为变为s，添加SUID权限可用“+s”表示。
例如：passwd
[adam@ultraera  ~]$  which  passwd
/usr/bin/passwd
[adam@ultraera  ~]$  ls  -l  /usr/bin/passwd
-rwsr-xr-x.  1  root  root  25980  Feb  22  2012  /usr/bin/passwd
[adam@ultraera  ~]$
SGID：主要针对文件夹，在设置了SGID的文件夹中创建任何新文件都继承该文件的所属组，设置sgid后，在权限位中，所属
组的最后一个权限位变为s，添加SGID权限可用“+s”表示。
例如：
[adam@ultraera  ~]$  mkdir  ultraera
[adam@ultraera  ~]$  ls  -l
total  4
drwxrwxr-x  2  adam  adam  4096  Nov  27  21:09  ultraera
[adam@ultraera  ~]$  chmod  g+s  ultraera/
[adam@ultraera  ~]$  ls  -l
total  4
drwxrwsr-x  2  adam  adam  4096  Nov  27  21:09  ultraera
[adam@ultraera  ~]$  su
Password:
[root@ultraera  adam]#  mkdir  -p  ultraera/test
[root@ultraera  adam]#  ls  -l  ultraera/
total  4
drwxr-sr-x  2  root  adam  4096  Nov  27  21:09  test
[root@ultraera  adam]#
sticky：针对文件夹，对目录拥有写权限的用户，仅可以删除其所拥有的文件，无法删除其他用户所拥有的文件，设置了sticky
之后，在权限位，other的最后一个权限位变为t,添加SGID权限可用“+t”表示。
例如：
[root@ultraera  tmp]#  mkdir  ultraera
[root@ultraera  tmp]#  chmod  a=rwx,o+t  ultraera/
[root@ultraera  tmp]#  ls  -ld  ultraera/
drwxrwxrwt  2  root  root  4096  Nov  27  21:29  ultraera/
[root@ultraera  tmp]#  useradd  user1
[root@ultraera  tmp]#  useradd  user2
[root@ultraera  tmp]#  su  user1
[user1@ultraera  tmp]$  touch  ./ultraera/test
[user1@ultraera  tmp]$  ls  -l  ultraera/
total  0
-rw-rw-r--  1  user1  user1  0  Nov  27  21:31  test
[user1@ultraera  tmp]$  exit
exit
[root@ultraera  tmp]#  su  user2
[user2@ultraera  tmp]$  rm  -f  ./ultraera/test
rm:  cannot  remove  `./ultraera/test':  Operation  not  permitted
[user2@ultraera  tmp]$


同样使用chmod来设定特殊权限，与普通权限一样，特殊权限也可以用数字表示：
suid  ：  4
sgid  ：  2
sticky ：  1
chmod  4644  filename	#设置文件suid权限
chmod  2755  flodername	#设置文件夹sgid权限
chmod  1755  flodername	#设置文件夹sticky权限

```
