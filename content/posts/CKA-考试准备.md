---
title: CKA 考试准备
toc: true
author: samzong.lu
author_id: defaultAuthorId
language: en
tags:
  - Docker
  - K8s
categories:
  - 闲聊
  - 学习
abbrlink: 4344
date: 2022-04-18 06:00:00
---
## 汇总

本来预计 4 月 10 号左右，可以开始准备 CKA 的考试了，因为疫情在家办公，再加上报名去做志愿者，所以这个时间耽搁到了现在才开始


### 时间成本

在这里记录下整个学习过程，也给大家预估下，不走培训机构，自学大概需要多久的时间

| 时间 | 事项 | 耗费时间 |
|---|---|---|
| 2022-04-16 | 了解什么是 CKA 和考试内容,捡起来 Docker 的知识, 个人项目转为 Docker Image 并推送到 dockerhub |  1d |
| 2022-04-17 | 在个人电脑上成功运行起来 K8s 的环境，并完成个人项目部署 | 1d |


### 体会

- 有段时间没回过头来弄代码了，平时写比较多是项目上的小脚本，系统化把一个项目改造为 Docker image，再来了一遍，整个优化过程的感觉还是很舒服的


## 学习资料

### 培训机构的大纲

大致培训时间是 3 天，给自己预估的学习时间大概是 一周左右的时间

- CKA最新考纲解读与Kubernetes入门（Day 1/上午）
   - CKA考试大纲解读
   - Kubernetes基本概念与应用场景
   - Kubernetes主要功能特性、集群架构与组件
   - 使用kubeadm安装集群与版本升级
   - etcd数据备份与还原
   - kubectl使用、shell自动补
- Kubernetes工作负载、调度与Helm（Day 1/下午）
   - Pod基本操作、生命周期、回调与探针
   - 初始化与临时容器
   - 使用Deployment部署自修复无状态服务
   - 使用Deployment滚动更新/回滚/扩缩无状态服务
   - 使用StatefulSet部署有状态服务
   - 使用DaemonSet部署守护进程
   - 深入理解控制器工作原理
   - 使用ConfigMaps和Secrets配置应用程序
   - Kubernetes调度策略实践
   - 资源限制如何影响Pod调度
   - 理解调度器工作原理
   - 各种调度策略使用场景总结
   - 使用Helm部署/升级/回滚/下线服务
   - Helm回调与Chart编写
- Kubernetes服务与网络（Day 2/上午）
   - 定义Service与Endpoint
   - Service Iptables与IPVS代理模式
   - 通过Service名称与ClusterIP集群内互访
   - 通过NodePort、Ingress、LoadBalancer集群外访问
   - CoreDNS原理介绍
   - 配置和使用CoreDNS
   - 同Pod/同Node/跨Node/跨集群互通性
   - 常见网络接口插件工作原理与适用场景
   - 常见网络故障排查
- Kubernetes存储与安全（Day 2/下午）
   - Volume、PV、PVC、StorageClass
   - 卷模式、访问模式和卷回收策略
   - 理解持久容量声明原语
   - 了解如何配置具有持久性存储的应用程序
   - 认证、授权与鉴权
   - 管理基于角色的访问控制（RBAC）
   - Pod和容器操作权限安全策略
   - Network Policy
- Kubernetes监控日志、故障排查（Day 3/上午）
   - 如何监控一个Kubenetes应用
   - 查看与管理集群和节点日志
   - 管理容器标准输出和标准错误日志
   - 如何解决应用程序故障
   - 对群集组件故障进行故障排除
   - Kubernetes其他常见问题定位
- CKA考试注意事项与模拟演练（Day 3/下午）
   - CKA真题演练与解析【重点】
   - CKA考试注意事项及应试答疑