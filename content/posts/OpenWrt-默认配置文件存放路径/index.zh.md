---
title: OpenWrt 默认配置文件存放路径
date: 2018-10-23T00:37:26+08:00
tags:
  - 技术
  - OpenWrt
aliases:
  - /2018/10/22/OpenWrt-默认配置文件存放路径/
  - /2018/10/23/OpenWrt-默认配置文件存放路径/
---

在修改 OpenWrt 配置文件时不小心将路由器断电了，导致了配置文件的损坏，尝试了很多方法恢复 OpenWrt 却因为小米路由器 3G 的特殊性而失败，最后通过拷贝默认配置文件的方式而修复。

<!--more-->

## 具体路径

OpenWrt 是通过在 `/rom` 覆盖一层 overlay 层来实现快速恢复初始状态的，因我们可以前往 `/rom/etc/config` 中找到默认配置文件，并将其拷贝至 `/etc/config` 中

## 参考

- [OpenWrt Fourm - Is there a method for generating default config files?](https://forum.archive.openwrt.org/viewtopic.php?id=63573)
