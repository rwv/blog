---
title: OpenWrt HTTPS 支持
date: 2018-10-23T00:49:57+08:00
tags:
  - 技术
  - OpenWrt
aliases:
  - /2018/10/22/OpenWrt-HTTPS-支持/
---

在安装完 OpenWrt 后，官方固件并不支持 HTTPS，因此 `wget`, `curl` 甚至于 `opkg` 中都不能使用 HTTPS，因此安装 HTTPS 支持就很有必要了。

<!--more-->

## 安装步骤

```sh
opkg update
opkg install wget ca-certificates openssl-util ca-bundle
```

## curl 报错

在没有安装 `ca-bundle` 时，使用 `curl` 访问 HTTPS 链接会出现错误 `curl: (77) Error reading ca cert file /etc/ssl/certs/ca-certificates.crt - mbedTLS: (-0x3E00) PK - Read/write of file failed`

## 参考

- [Install oh-my-zsh on openwrt/lede-project](https://gist.github.com/fire1ce/65d3e370120750a5deb283abe1d74491)
