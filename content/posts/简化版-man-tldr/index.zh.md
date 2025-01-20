---
title: "简化版 man: tldr"
date: 2018-01-26T19:50:13+08:00
tags:
  - 技术
  - Terminal
aliases:
  - /2018/01/26/简化版-man-tldr/
---

tldr 全称 Too Long; Didn't Read. 指文本太长而使读者丧失了阅读的兴趣。本人在使用 `man` 命令查询某个命令的用法时也常因为冗长的文本而转向搜索引擎求助。对于一些不想读冗长的 man pages 的用户来说，可使用 `tldr` 命令来获取一些最简单的例子从而快速上手。

<!--more-->

## 例子

相比于又臭又长的 `man tar`

```
BSDTAR(1)                 BSD General Commands Manual                BSDTAR(1)

NAME
     tar -- manipulate tape archives

SYNOPSIS
     tar [bundled-flags <args>] [<file> | <pattern> ...]
     tar {-c} [options] [files | directories]
     tar {-r | -u} -f archive-file [options] [files | directories]
     tar {-t | -x} [options] [patterns]

DESCRIPTION
     tar creates and manipulates streaming archive files.  This implementation
     can extract from tar, pax, cpio, zip, jar, ar, and ISO 9660 cdrom images
     and can create tar, pax, cpio, ar, and shar archives.

     The first synopsis form shows a ``bundled'' option word.  This usage is
     provided for compatibility with historical implementations.  See COMPATI-
     BILITY below for details.

     The other synopsis forms show the preferred usage.  The first option to
     tar is a mode indicator from the following list:
     -c      Create a new archive containing the specified items.
```

`tldr tar` 则显得简洁很多，并且极易快速上手。

```
$ tldr tar

tar

Archiving utility.
Often combined with a compression method, such as gzip or bzip.

- Create an archive from files:
    tar cf target.tar file1 file2 file3

- Create a gzipped archive:
    tar czf target.tar.gz file1 file2 file3

- Extract an archive in a target folder:
    tar xf source.tar -C folder

- Extract a gzipped archive in the current directory:
    tar xzf source.tar.gz

- Extract a bzipped archive in the current directory:
    tar xjf source.tar.bz2

- Create a compressed archive, using archive suffix to determine the compression program:
    tar caf target.tar.xz file1 file2 file3

- List the contents of a tar file:
    tar tvf source.tar
```

## 安装

多种形式的 tldr 安装方式

- Homebrew: `brew install tldr`
- Node.js: `npm install -g tldr`
- Python: `pip install tldr`
- Ruby: `gem install tldrb`

更多安装方式可以参见 [TLDR pages](http://tldr.sh)

## 更新

tldr 安装完成后需要执行 `tldr --update` 来更新本地数据库。若更新失败：

```
$ tldr --update
Local data is older than two weeks, use --update to update it.

Error: Downloading File: https://github.com/tldr-pages/tldr/archive/master.zip
```

可以尝试添加代理 `export https_proxy=http://localhost:8080` 进行更新。

## 参考

[TLDR pages](http://tldr.sh)
