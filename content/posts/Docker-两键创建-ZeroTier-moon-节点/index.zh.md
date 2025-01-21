---
title: Docker 两键创建 ZeroTier moon 节点
date: 2018-05-13T19:46:00+08:00
tags:
  - 技术
  - 项目
  - ZeroTier
  - Docker
aliases:
  - /2018/05/13/Docker-两键创建-ZeroTier-moon-节点/
---

ZeroTier moon 节点的创建说不上特别繁琐但也绝对不是特别简单，因此写了一个 Docker 镜像方便 ZeroTier moon 节点的创建。

<!--more-->

## 搭建命令

一条命令创建 ZeroTier moon 节点：

```bash
$ docker run --name zerotier-moon -d -p 9993:9993 -p 9993:9993/udp seedgou/zerotier-moon -4 1.2.3.4
```

(将 `1.2.3.4` 替换为 moon 的 ip ）

另一条命令查看 moon id

```bash
$ docker logs zerotier-moon
```

**注意:** 当创建一个新的容器时，会生成新的 moon id。为了保持 moon id 不变，在容器停止运行时，使用 `docker start zerotier-moon` 重启容器。如果需要在创建新的容器时保持 moon id 不变，可以参考下面的**挂载配置文件夹**。

## 高阶用法

### 管理 ZeroTier

```bash
docker exec zerotier-moon /zerotier-cli
```

### 挂载配置文件夹

```bash
docker run --name zerotier-moon -d -p 9993:9993 -p 9993:9993/udp -v ~/somewhere:/var/lib/zerotier-one seedgou/zerotier-moon -4 1.2.3.4
```

这条命令将本机上的 `~/somewhere` 挂载到容器中的 `/var/lib/zerotier-one` 目录上，使得配置文件能够持久化。如果不挂载配置文件夹，新建容器则会生成新的 moon id.

### IPv6 支持

```bash
docker run --name zerotier-moon -d -p 9993:9993 -p 9993:9993/udp seedgou/zerotier-moon -4 1.2.3.4 -6 2001:abcd:abcd::1
```

将 `1.2.3.4`, `2001:abcd:abcd::1` 替换为 moon 的 ip. `-4` 选项可在纯 IPv6 环境中忽略。

### 自定义端口

```bash
docker run --name zerotier-moon -d -p 9994:9993 -p 9994:9993/udp seedgou/zerotier-moon -4 1.2.3.4 -p 9994
```

将 `9994` 替换为自定义端口。

## 项目地址

https://github.com/rwv/docker-zerotier-moon
