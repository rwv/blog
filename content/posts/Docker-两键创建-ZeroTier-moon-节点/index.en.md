---
title: Create a ZeroTier Moon Node with Docker in Two Commands
date: 2018-05-13T19:46:00+08:00
tags:
  - Technology
  - Projects
  - ZeroTier
  - Docker
url: /en/posts/create-a-zerotier-moon-node-with-docker-in-two-commands/
---

While creating a ZeroTier moon node isn't overly complex, it does involve several steps. To simplify this process, I've created a Docker image that lets you set up a moon node with just two commands.

<!--more-->

## Basic Setup

First, create the ZeroTier moon node:

```bash
docker run --name zerotier-moon -d -p 9993:9993 -p 9993:9993/udp seedgou/zerotier-moon -4 1.2.3.4
```

(Replace `1.2.3.4` with your moon node's public IP address)

Then, retrieve your moon ID:

```bash
docker logs zerotier-moon
```

**Note:** Each new container generates a new moon ID. To preserve your moon ID after container restarts, use `docker start zerotier-moon` instead of creating a new container. For persistent moon ID storage across new container creations, see the **Mounting Configuration Directory** section below.

## Advanced Usage

### ZeroTier Management

```bash
docker exec zerotier-moon /zerotier-cli
```

### Mounting Configuration Directory

```bash
docker run --name zerotier-moon -d -p 9993:9993 -p 9993:9993/udp -v ~/somewhere:/var/lib/zerotier-one seedgou/zerotier-moon -4 1.2.3.4
```

This command mounts a local directory (`~/somewhere`) to the container's `/var/lib/zerotier-one` directory, enabling configuration persistence. Without this mount, each new container will generate a fresh moon ID.

### IPv6 Support

```bash
docker run --name zerotier-moon -d -p 9993:9993 -p 9993:9993/udp seedgou/zerotier-moon -4 1.2.3.4 -6 2001:abcd:abcd::1
```

Replace both `1.2.3.4` and `2001:abcd:abcd::1` with your moon node's IPv4 and IPv6 addresses respectively. In IPv6-only environments, you can omit the `-4` option.

### Custom Port

```bash
docker run --name zerotier-moon -d -p 9994:9993 -p 9994:9993/udp seedgou/zerotier-moon -4 1.2.3.4 -p 9994
```

Replace `9994` with your desired port number.

## Source Code

https://github.com/rwv/docker-zerotier-moon
