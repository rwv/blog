---
title: Windows CMD echo 不添加新行/不换行
date: 2019-04-26T14:07:15+08:00
tags:
  - 技术
  - Windows
  - CMD
aliases:
  - /2019/04/26/Windows-CMD-echo-不添加新行-不换行/
---

当使用 `echo` 时，Windows 会在文本后面添加新行。而有时我们需要不添加新行。

<!--more-->

## 添加新行

``` batch
echo Test
```

## 不添加新行

``` batch
echo|set /p="Test"
```
