---
title: python pyenv virturalenv 安装、设置与使用
date: 2018-02-01T03:53:29+08:00
tags:
  - 技术
  - Python
  - pyenv
  - virtualenv
  - Linux
aliases:
  - /2018/01/31/python-pyenv-virturalenv-安装、设置与使用/
---

Python 的版本兼容性一直都是个大问题，做好版本之间的隔离就显得格外重要。pyenv 可以很好地管理不同的 Python 版本并且切换自如。本文简略介绍了 pyenv 和 virturalenv 的安装、设置与使用。

<!--more-->

## 安装 pyenv

### 安装依赖

- Ubuntu/Debian:

```bash
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev
```

- Fedora/CentOS/RHEL:

```bash
dnf install zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel xz xz-devel
```

- openSUSE:

```
zypper in zlib-devel bzip2 libbz2-devel readline-devel sqlite3 sqlite3-devel libopenssl-devel xz xz-devel
```

- macOS:

```bash
brew install readline xz
```

### 安装 pyenv

```bash
$ curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
```

zsh 用户修改 `~/.zshrc`，bash 用户修改 `~/.bashrc`，在底部加入

```
export PATH="~/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

## 设置 pyenv

### 安装 Python

```bash
$ pyenv install --list #列出可用的 Python 版本
$ pyenv install 2.7.9 #安装 Python 2.7.9
$ pyenv install 3.6.4 #安装 Python 3.6.4
$ pyenv install anaconda3-5.0.1 #安装 Anaconda3 5.0.1
```

### 创建 virtualenv

```bash
$ pyenv virtualenv 3.6.4 venv36
$ pyenv virtualenv 2.7.9 venv27
```

### 修改默认环境

修改 `~/.pyenv/version`，使得 Python2 和 Python3 共存。

```
venv36
venv27
```

## pyenv 下 pip 修改源

在 pyenv 中，先 activate 想要修改的 pip 源，如：

```
$ pyenv activate venv36
```

然后修改 `$VIRTUAL_ENV/pip.conf` 文件，以中科大源为例：

```
[global]
index-url = https://mirrors.ustc.edu.cn/pypi/web/simple
format = columns
```

## 其他命令

```bash
$ pyenv commands    #列出所有可用的命令
$ pyenv versions    #列出所有可用的 Python 版本
$ pyenv install 2.7.10   #安装某一 Python 版本
$ pyenv uninstall 2.7.10    #卸载某一 Python 版本
$ pyenv global 2.7.10   #设置某一版本为全局 Python 版本
$ pyenv local 2.7.10    #设置某一版本为当前文件夹 Python 版本
$ pyenv activate venv2     #进入某一环境
$ pyenv deactivate venv2     #退出某一环境
```

## 参考

- https://github.com/pyenv/pyenv/wiki/Common-build-problems
- https://pip.pypa.io/en/stable/user_guide/#configuration
