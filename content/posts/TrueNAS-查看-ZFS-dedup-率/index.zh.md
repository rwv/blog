---
title: TrueNAS 查看 ZFS dedup 率
date: 2021-02-22T13:28:38+08:00
tags:
  - 技术
  - TrueNAS
aliases:
  - /2021/02/22/TrueNAS-查看-ZFS-dedup-率/
---

在 TrueNAS 中运行 `zpool list` 进行查看。

运行结果：

```
root@truenas[~]# zpool list
NAME        SIZE  ALLOC   FREE  CKPOINT  EXPANDSZ   FRAG    CAP  DEDUP    HEALTH  ALTROOT
Storage    14.5T  2.52T  12.0T        -         -    11%    17%  1.17x    ONLINE
```

其中的 `DEDUP` 即为 dedup 率。
