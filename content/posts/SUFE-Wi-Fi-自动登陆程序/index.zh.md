---
title: SUFE Wi-Fi 自动登陆程序
date: 2017-11-30T15:51:05+08:00
tags:
  - 项目
  - SUFE
aliases:
  - /2017/11/30/SUFE-Wi-Fi-自动登陆程序/
---

此程序可以实现自动登录上海财经大学无线网络的功能。
该程序分为 [Connector](https://github.com/rwv/sufe-wifi-connector) 和 [Dashboard](https://github.com/rwv/sufe-wifi-dashboard) 两部分，分别为自动登录程序和后台管理程序。
ENJOY IT! 🤯

---

**这是个免费开源程序，希望能到 [GitHub](https://github.com/rwv/sufe-wifi-connector) 给个 STAR! 🌟**

---

**国内下载地址**：

- [Windows 版本](http://sufewifi-1253151332.cossh.myqcloud.com/Windows.SUFE.Wi-Fi.zip)
- [macOS 版本](http://sufewifi-1253151332.cossh.myqcloud.com/macOS.SUFE.Wi-Fi.dmg)

<!--more-->

## 已知问题

1. macOS 版 Connector 程序运行后在 Dock 栏上显示未响应（实际上仍在运行）。且电脑关机时此未响应会阻止电脑关机，只能手动结束 Connector 程序才能使电脑继续关机。
2. macOS 和 Windows 版本均没有代码签名，所以第一次运行时可能系统可能会警告来自未知的开发者。Windows 用户请直接按照提示打开运行，macOS 用户请在应用程序文件夹中对两个程序按住 `option ⌥` 后右键打开运行。
3. Windows 可能会出现 Dashboard 管理程序获取不到信息的情况，目前尚不清楚发生原因。

## 支持列表

|         | 电信 | 联通 | 移动 |
| :-----: | :--: | :--: | :--: |
| Windows |  √   |  √   |  √   |
|  macOS  |  √   |  √   |  √   |
|  Linux  |  √   |  √   |  √   |

注：

1. 联通在 macOS 10.13, Windows 10 上经过测试成功
2. Linux 未测试
3. 移动未测试（似乎登陆逻辑和联通一样 🤔）
4. 电信初步测试成功，未经大范围测试

## 使用方法

国内下载地址：
[Windows 版本](http://sufewifi-1253151332.cossh.myqcloud.com/Windows.SUFE.Wi-Fi.zip)
[macOS 版本](http://sufewifi-1253151332.cossh.myqcloud.com/macOS.SUFE.Wi-Fi.dmg)

请前往 [GitHub Releases](https://github.com/rwv/sufe-wifi-connector/releases) / 国内下载地址 进行程序下载, 程序内附使用方法。

## Contact me

如果有任何问题，请前往 [GitHub](https://github.com/rwv/sufe-wifi-connector) 提出 Issue 或发邮件至 i@zczc.cz

## Contribute

- Use It
- Open Issue
- Send Pull Request

## TODO

- [ ] Travis-CI 和 Coveralls
- [ ] docstring
- [x] Windows
- [x] Linux
- [x] 电信
- [x] 移动
- [x] Log
- [x] 跨平台生成可执行文件, Using pyinstaller
- [x] RPC & Web Frontend
