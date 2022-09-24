# 使用mosh代替ssh连接服务器


身为一名服务器运维人员，每天打交道最多的就是服务器了，最常用的连接服务器的工具就是SSH，因为SSH是一个不可持续的连接，当网络出现波动时，SSH断开会导致当前正在运行的服务中断，对工作产生非常大的影响，无意间看到了Mosh这个东西，安装使用下，发现网络波动这种事情不会导致服务器连接断开了，特意查了下，原来Mosh使用的是UDP方式传输：虽然也支持使用SSH配置进行认证登录，但是数据传输本身是使用UDP方式的，Mosh支持在会话中断时，不会立即退出，而是启用一个计时器，当网络恢复后会自动连接，同时会延续之前的会话，不会重新开启一个。

#### Mosh [主页](https://mosh.mit.edu/#getting)


#### 1. 安装配置
需要在服务端和客户端同时安装Mosh：
```
＃ 以centos 6.x 为例：
[user@host ~]$ sudo yum install -y epel-release
[user@host ~]$ sudo yum install -y mosh
```

#### 2. 采用SSH配置进行认证登录，只需要将ssh 替换为mosh即可
```
[user@host ~]$ mosh user@host

# 如何需要指定特定的ssh port或者使用ssh keyfile. 可以使用-ssh参数：
[user@host ~]$ mosh -ssh="ssh -i ~/.ssh/id_rsa -p 10002" user@host
```

#### 3. Other
另外Mosh还支持使用临时key的方式认证，需要服务器端创建临时key，然后客户端通过这个key进行登录，该key在会话结束的十分钟后自动失效。

```
# 创建临时key
[user@host ~]$ mosh-server
MOSH CONNECT 53371 asdAADfdse234LSDSdIbow
mosh-server (mosh 1.2.4)
Copyright 2012 Keith Winstein <mosh-devel@mit.edu>
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
[mosh-server detached, pid = 27290]

# 然后在client定义MOSH_KEY
[user@host ~]$ export MOSH_KEY=asdAADfdse234LSDSdIbow
# 注意mosh-client只能跟上具体的ip和临时端口，不支持主机名和域名方式

# 使用临时key连接服务器
[user@host ~]$ mosh-client 10.0.2.4 53371
```

