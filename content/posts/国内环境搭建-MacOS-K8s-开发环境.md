---
title: 国内环境搭建 MacOS K8s 开发环境
toc: true
tags:
  - K8s
abbrlink: 15266
date: 2022-05-17 10:09:02
categories:
---

## Minikube

在 Mac 上搭建开发环境，这里主要使用了 Kubernetes 官方推荐的 minikube 和 docker-for-desktop 环境

```sh
minikube start --image-mirror-country cn \
    --registry-mirror=https://vbj8usl3.mirror.aliyuncs.com
```