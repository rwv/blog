---
title: macOS 将 SSH key 加入到 Keychain
date: 2019-10-25T11:10:34+08:00
tags:
  - 技术
  - macOS
aliases:
  - /2019/10/25/macOS-将-SSH-key-加入到-Keychain/
---

将 SSH key 加入到 `ssh-agent` 中可以方便我们登陆其他服务器，但是在 macOS 中，使用了 `ssh-add` 添加后，重启即会失效。

<!--more-->

## 解决方法

首先使用 `ssh-add -K ~/.ssh/id_rsa` 来将 SSH key 加入到 Keychain 中。接着将下面的内容加入到 `~/.ssh/config` 中

```
Host *
  UseKeychain yes
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_rsa
```

## 参考

[How can I permanently add my SSH private key to Keychain so it is automatically available to ssh?](https://apple.stackexchange.com/questions/48502/how-can-i-permanently-add-my-ssh-private-key-to-keychain-so-it-is-automatically)
