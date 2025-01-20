---
title: Windows Subsystem for Linux (WSL) 设置 zsh 为默认 shell
date: 2018-02-05T22:51:25+08:00
tags:
  - 技术
  - WSL
  - Windows Subsystem for Linux
  - zsh
aliases:
  - /2018/02/05/Windows-Subsystem-for-Linux-WSL-设置-zsh-为默认-shell/
---

在 Windows Subsystem for Linux 中，执行 `chsh -s /bin/zsh` 并不能成功地将默认 shell 修改为 zsh。在打开 WSL 时，默认 shell 仍然为 bash。通过一个简易的 workaround 可以使在打开 WSL 时同时打开 zsh。

<!--more-->

## 操作步骤

在 `~/.bashrc` 中添加

```bash
bash -c zsh
```

## 其他

出现这个问题的原因是 WSL 在启动时并没有执行 login 相关的组件，而这些组件和默认 shell 有关。Microsoft 已经知晓了这个问题，但并没有计划去解决。

参见：https://github.com/Microsoft/WSL/issues/477
