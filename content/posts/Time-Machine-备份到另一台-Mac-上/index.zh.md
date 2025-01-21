---
title: Time Machine 备份到另一台 Mac 上
date: 2018-08-17T17:27:55+08:00
tags:
  - 技术
  - timemachine
  - Mac
aliases:
  - /2018/08/17/Time-Machine-备份到另一台-Mac-上/
---

Time Machine 可以很方便的备份系统，但是假如没有 Time Capsule 或者 NAS 时，也可以备份到另一台 Mac 的硬盘上。

<!--more-->

## 操作步骤

在 Time Machine 备份存放的目的地的电脑上打开`系统偏好设置`，选择`共享`并选择`文件共享`。添加你想要备份的目的地。

![Add Time Machine Folder](./Add_Time_Machine_Folder.png)

对目标文件夹右键，选择高级选项。勾选`作为 Time Machine 目的地共享`，同时可以设置备份最大容量。这样就可以将另一台 Mac 作为 Time Machine 的备份目的地了。

![Time Machine Advanced Settings](./Time_Machine_Advanced_Settings.png)
