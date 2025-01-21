---
title: 安装 fbprophet 遇到 command clang failed with exit status 1 错误
date: 2019-10-24T17:20:02+08:00
tags:
  - 技术
  - Python
  - fbprophet
aliases:
  - /2019/10/24/安装-fbprophet-遇到-command-clang-failed-with-exit-status-1-错误/
---

在安装 fbprophet 的时候遇到了 `command clang failed with exit status 1` 的问题，在经过一番研究后发现是 pystan 的问题。

<!--more-->

## 解决方案

长话短说，pystan 目前无法在 Python 3.7+ 中运行，测试在 3.6.6 中可以成功运行。

## 参考资料

[PyStan 2.18.0.0 compilation failure on macOS in Anaconda environment. #521](https://github.com/stan-dev/pystan/issues/521)
