+++
date = '2025-03-18T10:07:03+08:00'
draft = false
title = 'Linux 服务器初始化备忘'
summary = '本备忘录记录了在 Linux 服务器上初始化的一些操作。主要是用来快速配置服务器，方便后续的开发和维护。其实也可以用 Dotbot 来管理，但是还是想记录一下。'
description = '本备忘录记录了在 Linux 服务器上初始化的一些操作。主要是用来快速配置服务器，方便后续的开发和维护。其实也可以用 Dotbot 来管理，但是还是想记录一下。'
ShowToc = true
TocOpen = true
+++

## APT 配置

更改为 https 源，升级系统并安装常用工具

```bash
sed -i 's/http:/https:/g' /etc/apt/sources.list
apt update && apt upgrade -y
apt install -y curl wget git screen htop zsh sudo rsync nano nload
```

## 配置 SSH

配置 SSH 密钥登陆

```bash
mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys
```

禁用密码登录，改用 SSH Key

```bash
sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart sshd
```

## 安装 oh-my-zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
nano ~/.zshrc
source ~/.zshrc
```

## 安装 Docker

```bash
curl -fsSL https://get.docker.com | sh
```

## 配置自动更新

```bash
apt-get install -y unattended-upgrades apt-listchanges
dpkg-reconfigure unattended-upgrades
```

## 启用 ZRAM

```bash
apt install -y zram-tools
echo -e "ALGO=zstd\nPERCENT=60" | tee -a /etc/default/zramswap
service zramswap reload
```

## 启用 BBR 网络优化

```bash
# check if bbr is enabled
sysctl net.ipv4.tcp_congestion_control

echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
```

## 配置时间同步（Chrony）

```bash
apt install -y chrony
nano /etc/chrony/chrony.conf
# 添加以下时间服务器
# server time.google.com iburst
# server time.cloudflare.com iburst
systemctl restart chrony
```

## 配置 DNS 服务（systemd-resolved）

```bash
apt install -y systemd-resolved
systemctl enable --now systemd-resolved
nano /etc/systemd/resolved.conf
# TODO: 使用 sed 配置 Cloudflare DNS 和备用 DNS
# DNS=1.1.1.1#cloudflare-dns.com 1.0.0.1#cloudflare-dns.com
# FallbackDNS=8.8.8.8#dns.google 8.8.4.4#dns.google
# DNSOverTLS=yes
systemctl restart systemd-resolved
```

以上步骤完成后，服务器即可投入使用。
