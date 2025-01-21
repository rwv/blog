---
title: macOS 设置应用默认语言
date: 2019-10-24T17:24:19+08:00
tags:
  - 技术
  - macOS
aliases:
  - /2019/10/24/macOS-设置应用默认语言/
---

不同应用会有不同的语言要求，例如之前 VSCode 默认中文的设置就让一些人感到不大习惯，macOS 提供了设置应用默认语言的方法。

<!--more-->

## 操作方法

### 获取应用的 `kMDItemCFBundleIdentifier`

运行以下命令获取应用的 `kMDItemCFBundleIdentifier` （以系统地图应用为例）

```bash
mdls -name kMDItemCFBundleIdentifier /System/Applications/Maps.app
```

得到

```
kMDItemCFBundleIdentifier = "com.apple.Maps"
```

### 修改应用默认语言

运行

```bash
defaults write com.apple.Maps  AppleLanguages '(zh-CN)'
```

语言代码表: http://www.lingoes.net/zh/translator/langcode.htm

## 更好的教程

本文只是个小笔记，请参见 [如何临时修改 macOS 应用的界面语言 - 少数派](https://sspai.com/post/44536)
