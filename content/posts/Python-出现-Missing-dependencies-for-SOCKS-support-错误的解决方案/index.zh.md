---
title: Python 出现 Missing dependencies for SOCKS support 错误的解决方案
date: 2018-07-31T02:45:34+08:00
tags:
  - 技术
  - Python
aliases:
  - /2018/07/30/Python-出现-Missing-dependencies-for-SOCKS-support-错误的解决方案/
---

最近在创建新的 Python Virtualenv 时出现了 `Missing dependencies for SOCKS support` 的错误，经检查后发现为 Python 本身在没有安装 pysocks 时并不支持 socks5 代理，而环境变量中则设置了 socks5 的代理。

<!--more-->

## 解决方案

```bash
$ unset all_proxy && unset ALL_PROXY # 取消所有 socks 代理
$ pip install pysocks
```

## 参考

[Python's requests “Missing dependencies for SOCKS support” when using SOCKS5 from Terminal - Stack Overflow](https://stackoverflow.com/questions/38794015/pythons-requests-missing-dependencies-for-socks-support-when-using-socks5-fro)
