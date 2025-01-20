---
title: ZeroTier moon 设置教程
date: 2018-03-14T16:31:20+08:00
tags:
  - 技术
  - ZeroTier
aliases:
  - /2018/03/14/ZeroTier-moon-设置教程/
---

由于国内网络的复杂的情况， ZeroTier 的点与点连接很有可能建立失败。此时机器之间的连接就会绕道国外，造成较大的延迟和丢包率。在 ZeroTier 1.2.0 版本之后，一项新的功能被加入进来：“自定义根服务器”，又称 moon。通过自定义的服务器作为跳板加速内网机器之间的互相访问。本文简要介绍了 ZeroTier moon 的设置方法。

<!--more-->

---

**本文已更新，参见 [Docker 两键创建 ZeroTier moon 节点](/2018/05/13/Docker-两键创建-ZeroTier-moon-节点/)**

## 本文环境

### 机器 A (moon)

- 公网机器
- IP: `1.2.3.4`
- 系统: Ubuntu 16.04.1 LTS

### 机器 B

- 内网机器

### 机器 C

- 内网机器

## 设置教程

### 生成及修改 `moon.json`

首先登陆到机器 A 上，前往路径 `/var/lib/zerotier-one`。运行命令

```bash
zerotier-idtool initmoon identity.public >>moon.json
```

此命令会在当前目录下生成一个文件 `moon.json`，文件内容如下:

```json
{
  "id": "deadbeef00",
  "objtype": "world",
  "roots": [
    {
      "identity": "deadbeef00:0:34031483094...",
      "stableEndpoints": []
    }
  ],
  "signingKey": "b324d84cec708d1b51d5ac03e75afba501a12e2124705ec34a614bf8f9b2c800f44d9824ad3ab2e3da1ac52ecb39ac052ce3f54e58d8944b52632eb6d671d0e0",
  "signingKey_SECRET": "ffc5dd0b2baf1c9b220d1c9cb39633f9e2151cf350a6d0e67c913f8952bafaf3671d2226388e1406e7670dc645851bf7d3643da701fd4599fedb9914c3918db3",
  "updatesMustBeSignedBy": "b324d84cec708d1b51d5ac03e75afba501a12e2124705ec34a614bf8f9b2c800f44d9824ad3ab2e3da1ac52ecb39ac052ce3f54e58d8944b52632eb6d671d0e0",
  "worldType": "moon"
}
```

其中 `id` 为机器 A 在 ZeroTier 中的 id，本文为 `deadbeef00`。
修改 `"stableEndpoints"` 为机器 A 的公网的 ip。如：

```json
"stableEndpoints": [ "1.2.3.4/9993","2001:abcd:abcd::1/9993" ]
```

若公网机器没有 IPv6 地址，则将其修改为

```json
"stableEndpoints": [ "1.2.3.4/9993" ]
```

### 生成签名文件

修改完 `moon.json` 后，执行命令

```
zerotier-idtool genmoon moon.json
```

此命令会生成一个签名文件在当前目录下，文件名如 `000000deadbeef00.moon` （机器 A 的 id 为 `deadbeef00`)

### 将 moon 节点加入网络

在机器 A 中的 ZeroTier 目录中建立子文件夹 `moons.d`

不同系统下的 ZeroTier 目录位置：

- Windows: `C:\ProgramData\ZeroTier\One`
- Macintosh: `/Library/Application Support/ZeroTier/One` (在 Terminal 中应为 `/Library/Application\ Support/ZeroTier/One`)
- Linux: `/var/lib/zerotier-one`
- FreeBSD/OpenBSD: `/var/db/zerotier-one`

将在机器 A 生成的 `000000deadbeef00.moon` 拷贝进 `moons.d` 文件夹中，并重启 ZeroTier（此步好像有些许 bug，重启电脑为佳）

### 将内网机器连接上 moon 节点

#### 方法一

在机器 B、机器 C 中的 ZeroTier 目录中建立子文件夹 `moons.d`

不同系统下的 ZeroTier 目录位置：

- Windows: `C:\ProgramData\ZeroTier\One`
- Macintosh: `/Library/Application Support/ZeroTier/One` (在 Terminal 中应为 `/Library/Application\ Support/ZeroTier/One`)
- Linux: `/var/lib/zerotier-one`
- FreeBSD/OpenBSD: `/var/db/zerotier-one`

将在机器 A 生成的 `000000deadbeef00.moon` 拷贝进 `moons.d` 文件夹中，并重启 ZeroTier（此步好像有些许 bug，重启电脑为佳）

#### 方法二

在机器 B、机器 C 上执行

```bash
zerotier-cli orbit deadbeef00 deadbeef00
```

## 参考

[ZeroTier | Manual](https://www.zerotier.com/manual.shtml#4_4)
