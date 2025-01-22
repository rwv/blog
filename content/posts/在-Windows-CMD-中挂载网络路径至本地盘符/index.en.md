---
title: Mounting Network UNC Paths to Drive Letters in Windows CMD
date: 2019-04-26T13:40:17+08:00
tags:
  - Technology
  - Windows
  - CMD
  - UNC
slug: mounting-network-unc-paths-to-drive-letters-in-windows-cmd
---

There are two methods to mount a network UNC (Universal Naming Convention) path to a local drive letter in Windows Command Prompt. While `pushd` is commonly used, it has a significant limitation that may affect certain scenarios.

<!--more-->

## Common Method: Using `pushd`

```batch
set unc_path=\\Host\a\b\c
pushd %unc_path%
:: Your commands here
popd
```

When using `pushd`, Windows automatically mounts `\\Host\a` to the first available drive letter (for example, `Y:`), then changes the working directory to `Y:\b\c`. However, this approach has a critical limitation: if the user has permissions for `\\Host\a\b\c` but lacks access to `\\Host\a`, all commands in this directory will fail with an `Access is denied` error.

## Alternative Method: Using `net use`

```batch
set unc_path=\\Host\a\b\c

:: Mount the UNC path to an available drive letter
net use * %unc_path%

:: Extract the assigned drive letter
for /f "tokens=2,3" %%i in ('net use') do if '%%j=='%unc_path% set drive_letter=%%i

:: Change to the mounted drive
%drive_letter%

:: Your commands here

:: Clean up: unmount the drive
net use %drive_letter% /delete /y
```

This alternative approach first assigns an available drive letter to the path using `net use`, then retrieves the assigned drive letter. The key advantage over `pushd` is that `net use` mounts the specific subdirectory rather than the root directory, thereby avoiding the permission issues mentioned above.

Note: When executing these commands directly in the command prompt (rather than in a batch file), replace `%%i` and `%%j` with `%i` and `%j` respectively.
