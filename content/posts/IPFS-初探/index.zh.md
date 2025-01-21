---
title: IPFS 初探
date: 2018-08-20T17:36:14+08:00
tags:
  - 技术
  - IPFS
  - P2P
  - 区块链
aliases:
  - /2018/08/20/IPFS-初探/
---

IPFS, InterPlanetary File System 是一个依靠 P2P 储存文件的系统。它的理念和机理和 BT 很像，不同的节点共同保存了一个文件，同时也都运用 DHT 来寻找文件。它还混合了时下最时髦的概念：区块链。通过 FileCoin 的应用来激励矿工们保存文件。这些理念看上去真的很美好，但是真的有想象中的那么好吗？

<!--more-->

## 为什么是 IPFS?

在 IPFS 的[官方网站](https://ipfs.io/)上，列出了 IPFS 的几个优势：

### P2P 效率高

p2p 技术的应用使得全球都可以快速的获得所需求的文件，不用担心国际网络之间连通性太差的问题。同时从多个服务器同时下载, 提升了下载速度。[在视频分发的应用中，节省了高达 60% 的带宽。](http://math.oregonstate.edu/~kovchegy/web/papers/p2p-vdn.pdf)

### 永久保存

在 web 中，文件经常会失效，时常会有 404 的情况出现，[一个网页的平均寿命只有 100 天](https://blogs.loc.gov/thesignal/2011/11/the-average-lifespan-of-a-webpage/)。而 IPFS 使得文件可以得到永久的保存，同时还提供了类 git 的历史版本回溯功能，使得文件更加安全。

### 去中心化

没有了中心的控制，每个用户都有机会发出自己的声音，使互联网恢复原本开放和扁平的样子。

### 稳定

非中心化使得文件不会被轻易的删除，屏蔽，修改。于此同时，在分布式的背景下，由于没有了没有单点失效的问题，一些如地震、火灾、停电等不可抗力事件将不会影响互联网的正常运行，文件仍然可以通过分布式网络结构分发至用户手中。

## 浅尝辄止

可通过 [Global Upload](https://globalupload.io) 将文件上传到 IPFS 网络之中，而不需要下载客户端至本地。

## 完整体验

前往 https://dist.ipfs.io/#go-ipfs 下载对应平台的 ipfs。安装过程具体参见 [Install IPFS - IPFS Documenation](https://docs.ipfs.io/introduction/install/)

下载安装完成后运行 `ipfs init` 进行初始化。

### 添加文件

```sh
$ ipfs add example.txt
added QmZ4tDuvesekSs4qM5ZBKpXiZGun7S2CYtEZRB3DYXkjGx
```

运行后会得到一串字符，这既是 IPFS HASH，通过 IPFS HASH 可以从 IPFS 网络中获取自己的文件。这和磁力链很相像，同样是通过一段 HASH 去访问 DHT 网络来取得文件。

### 打印文件

```sh
$ ipfs cat /ipfs/QmZ4tDuvesekSs4qM5ZBKpXiZGun7S2CYtEZRB3DYXkjGx
hello worlds
```

将 `QmZ4tDuvesekSs4qM5ZBKpXiZGun7S2CYtEZRB3DYXkjGx` 替换为对应的 IPFS HASH

### 下载文件

```sh
$ ipfs get /ipfs/QmZ4tDuvesekSs4qM5ZBKpXiZGun7S2CYtEZRB3DYXkjGx
```

### 开启网关

```sh
$ ipfs daemon
```

开启网关后，便可以通过访问 `http://localhost:8080/ipfs/QmYwAPJzv5CZsnA625s3Xf2nemtYgPpHdWEz79ojWnPbdG/readme` 的方式在浏览器中下载文件，而不需要与命令行打交道。

官方也提供了许多公共网关供其他人使用，如 `https://ipfs.work/ipfs/`

## IPFS 应用

IPFS 如今已经有了很多应用，如视频网站，图床，Wiki 等等

具体可参见 https://github.com/ipfs/awesome-ipfs

## 文件存活测试

对于 IPFS 来说，最不确定的是文件能否持续存在于 IPFS 网络之中。个人认为，文件在很长一段时间没有被访问后就会从 IPFS 网络中消失。要使得文件长久地存在于网络之中，就需要有人来 `pin` 这个文件，如今也有专门的服务来帮助用户 `pin` 住文件，如 [eternum](https://www.eternum.io)。但价格并不算友好，需要 $0.300/GB 每月。

还有一种方法便是常常去访问这个文件，使得这个文件一直存在于网络的各个节点之中。本人认为能被常常访问的最好方法便是发布至互联网上，在此本人将不同类型的文件上传至 IPFS 网络上，希望探寻出不同类型文件的存活时间。（本人预测图片的存活时间会最长，由于各种爬虫 🕷️ 的存在）

### 文档

PDF file: [pdf-sample.pdf](https://ipfs.io/ipfs/QmamSmjXAyyhqeQG7oEABwCDenuJuxTnW3553LfC42Mp6L/pdf-sample.pdf) (8 KB)

文件来源: [This is a test PDF file - UNEC](https://unec.edu.az/application/uploads/2014/12/pdf-sample.pdf)

### 图片

[Flat lay of healthy breakfast with bowls of fruit and oatmeal](https://ipfs.io/ipfs/QmPAwvkEpdshgYBiXXrLJyN56vZKTUs9emE1VCZvjsLEAQ/brooke-lark-289769-unsplash.jpg)

Breakfast JPEG 3.9MB 3717×5576

图片来源: [Breakfast by the Window photo by Brooke Lark (@brookelark) on Unsplash](https://unsplash.com/photos/W9OKrxBqiZA)

### 视频

<video controls autoplay src="https://ipfs.io/ipfs/QmPBkh5tWkfksJLQpgmu1F5xavVXcqUQmMidzCiX1Dn8ME/video.mp4" type="video/mp4"></video>

Video Of People Walking H.264 8.3MB 19sec 1920×1072

视频来源: [Pexels Video](https://videos.pexels.com/videos/video-of-people-walking-855564)
