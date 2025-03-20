+++
date = '2025-03-18T10:07:03+08:00'
draft = false
title = 'Linux Server Initialization Checklist'
summary = 'This memo documents various initialization operations performed on a Linux server, primarily to rapidly configure the server for subsequent development and maintenance. Dotbot could also manage these configurations, but this serves as a personal record.'
description = 'This memo documents various initialization operations performed on a Linux server, primarily to rapidly configure the server for subsequent development and maintenance. Dotbot could also manage these configurations, but this serves as a personal record.'
ShowToc = true
TocOpen = true
+++

## APT Configuration

Change sources to HTTPS, upgrade the system, and install commonly used tools:

```bash
sed -i 's/http:/https:/g' /etc/apt/sources.list
apt update && apt upgrade -y
apt install -y curl wget git screen htop zsh sudo rsync nano nload
```

## Configure SSH

Set up SSH key-based login:

```bash
mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys
```

Disable password login and enforce SSH key authentication:

```bash
sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart sshd
```

## Install oh-my-zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
nano ~/.zshrc
source ~/.zshrc
```

## Install Docker

```bash
curl -fsSL https://get.docker.com | sh
```

## Configure Automatic Updates

```bash
apt-get install -y unattended-upgrades apt-listchanges
dpkg-reconfigure unattended-upgrades
```

## Enable ZRAM

```bash
apt install -y zram-tools
echo -e "ALGO=zstd\nPERCENT=60" | tee -a /etc/default/zramswap
service zramswap reload
```

## Enable BBR Network Optimization

```bash
# Check if BBR is enabled
sysctl net.ipv4.tcp_congestion_control

echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
```

## Configure Time Synchronization (Chrony)

```bash
apt install -y chrony
nano /etc/chrony/chrony.conf
# Add the following time servers:
# pool time.cloudflare.com iburst nts
# pool time.google.com iburst
systemctl restart chrony
```

## Configure DNS Service (systemd-resolved)

```bash
apt install -y systemd-resolved
systemctl enable --now systemd-resolved
nano /etc/systemd/resolved.conf
# TODO: Use sed to configure Cloudflare DNS and fallback DNS
# DNS=1.1.1.1#cloudflare-dns.com 1.0.0.1#cloudflare-dns.com
# FallbackDNS=8.8.8.8#dns.google 8.8.4.4#dns.google
# DNSOverTLS=yes
systemctl restart systemd-resolved
```

After completing these steps, the server is ready for use.
