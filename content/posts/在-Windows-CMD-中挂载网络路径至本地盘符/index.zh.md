---
title: 在 Windows CMD 中挂载网络路径至本地盘符
date: 2019-04-26T13:40:17+08:00
tags:
- 技术
- Windows
- CMD
- UNC
aliases:
  - /2019/04/26/在-Windows-CMD-中挂载网络路径至本地盘符/ 
---

在 Windows CMD 中挂载网络路径 UNC 至本地盘符主要有两个办法，主流的是使用 `pushd` 进行挂载，但这个办法有个致命的缺点。

<!--more-->

## 主流方法 `pushd`

``` batch
set unc_path=\\Host\a\b\c
pushd
:: insert your code here
popd
```

但使用此方法时，`pushd` 会将 `\\Host\a` 挂载至可用盘符（假设为 `Y:`），并将工作目录更改至 `Y:\b\c`。但是这个方法致命的缺点为：当用户有 `\\Host\a\b\c` 的权限却没有 `\\Host\a` 的权限时，所有在此目录下的命令都会报错 `Access is denied`

## 另一种方法 `net use`

``` batch
set unc_path=\\Host\a\b\c

:: mount unc_path to available drive
net use * %unc_path%

:: get the drive letter and set variable drive_letter
for /f "tokens=2,3" %%i in ('net use') do if '%%j=='%unc_path% set drive_letter==%%i

:: switch to drive directory
%drive_letter%

:: insert your code here

:: unmount drive
net use %drive_letter% /delete /y
```

此命令首选查找可用盘符进行挂载，然后获取挂载盘符的位置。与 `pushd` 主要的不同是 `net use` 挂载子目录而不是根目录，因此不会遇到之前所说的权限问题。

注意：当在命令行中运行时 `%%i`, `%%j` 需要改成 `%i`, `%j`

