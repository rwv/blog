---
title: Docker 构建多架构镜像并上传至 Docker Hub
date: 2021-02-22T08:26:44+08:00
tags:
  - 技术
  - Docker
  - Docker Hub
aliases:
  - /2021/02/22/Docker-构建多架构镜像并上传至-Docker-Hub/
---

在更新 [seedgou/zerotier-moon](https://hub.docker.com/r/seedgou/zerotier-moon) 的时候，尝试了构建多架构的镜像并上传至 Docker Hub 上，记录一下。

<!--more-->

## 安装 QEMU

安装 QEMU 提供多架构 CPU 的模拟。

```bash
$ apt install -y qemu-user-static binfmt-support
```

运行 `docker buildx ls`，查看可用的架构:

```
$ docker buildx ls
NAME/NODE           DRIVER/ENDPOINT             STATUS  PLATFORMS
default             docker
  default           default                     running linux/amd64, linux/arm64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/arm/v7, linux/arm/v6
```

## 创建 buildx 实例

运行 `docker buildx create --use` 创建一个 builder。

## 构建并上传

运行构建命令并上传

```bash
$ docker buildx build -t seedgou/zerotier-moon:edge --platform=linux/amd64,linux/386,linux/ppc64le . --push
```

其中 `seedgou/zerotier-moon:edge` 为 Docker image 的 tag 名称， `linux/amd64,linux/386,linux/ppc64le` 为架构名称。

## 参考

[Leverage multi-CPU architecture support | Docker Documentation](https://docs.docker.com/docker-for-mac/multi-arch/)
