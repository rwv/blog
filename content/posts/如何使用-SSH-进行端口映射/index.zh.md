---
title: 如何使用 SSH 进行端口映射
date: 2017-11-28T19:58:56+08:00
tags:
  - 技术
  - SSH
  - Linux
toc: true
aliases:
  - /2017/11/28/如何使用-SSH-进行端口映射/
---

如何将内网环境下的机器映射到外网 ip 上已经有许多解决方案了，如：[ngrok](https://ngrok.com/), [花生壳 🥜](https://hsk.oray.com), [frp](https://github.com/fatedier/frp) 等。这些都需要特定软件的支持，本文介绍如何使用 SSH tunnel 进行简单的内网端口映射。

<!--more-->

## 配置公网 ip 机器

首先修改 `/etc/ssh/sshd_config` 中的 `GatewayPorts` 选项，在文件尾部添加

```
GatewayPorts yes
```

并重启 `sshd`

注：macOS 用户重启 `sshd` 请在 Terminal 中运行：

```bash
sudo launchctl stop com.openssh.sshd
sudo launchctl start com.openssh.sshd
```

## 配置内网 ip 机器

在内网机器中运行

```bash
ssh -N -R  0.0.0.0:8080:localhost:80 user@example.host -p 22
```

此条命令为将内网机器的 `80` 端口映射到 `user@example.host:22` 的 `8080` 端口。

## ssh 保持运行

### 生成 ssh 公钥 🔑 进行免密码连接

#### 检查现有的 ssh 公钥

在内网机器中运行 `ls -al ~/.ssh` 来查看是否有已存在的 ssh 密钥

```bash
ls -al ~/.ssh
# Lists the files in your .ssh directory, if they exist
```

若有已生成的公钥，请直接跳转到"添加公钥至远程服务器"

#### 生成 ssh 公钥

在内网机器中使用 `ssh-keygen` 来生成新的密钥

```bash
ssh-keygen -t ecdsa -b 521 -C "$(whoami)@$(hostname)-$(date -I)"
```

（对于新手来说对于提示可以一路回车下去。🌚）

#### 添加公钥至远程服务器

在内网机器中使用 `ssh-copy-id` 来将公钥至添加远程服务器

```bash
ssh-copy-id user@example.host
```

### 使用 `autossh` 进行连接

在安装完 `autossh` 后，执行

#### 若内网机器用户为 `root`

```bash
autossh -M 5680 -NR 0.0.0.0:8080:localhost:80 user@example.host -p 22 -f
```

#### 若内网机器用户不为 `root`

```bash
/bin/su -c '/usr/bin/autossh -M 5680 -NR 0.0.0.0:8080:localhost:80 user@example.host -f' - username
```

其中 `username` 为内网机器的用户名

## 参考资料

1. [Restart SSH/sshd in Mac OS X – VIVO の PUB](http://vivo.pub/2409)
2. [SSH Tunnel 解决无公网 IP 80 被封等问题](https://blog.bbzhh.com/index.php/archives/60.html)
3. [Connecting to GitHub with SSH - User Documentation - GitHub Help](https://help.github.com/articles/connecting-to-github-with-ssh/)
4. [SSH keys - ArchWiki](https://wiki.archlinux.org/index.php/SSH_keys)
