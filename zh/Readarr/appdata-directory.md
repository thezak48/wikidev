---
title: Readarr 应用数据目录
description: 
published: true
date: 2021-11-24T19:24:45.782Z
tags: readarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:54:32.028Z
---

> 以下是应用数据目录的默认路径 {.is-info}

> 所有的 `$USER` 都是应用程序正在运行的用户的占位符 {.is-warning}

# Windows

`C:\ProgramData\Readarr`

# Linux

除非另有指定，否则 Readarr 将把其应用数据存储在用户 Readarr 正在运行的主文件夹中 `/home/$USER/.config/Readarr` 或 `~/.config/Readarr`

安装说明指定了 `/var/lib/readarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Readarr` 或 `~/.config/Readarr`

# Synology

`/usr/local/Readarr/var/.config/Readarr`

`/volume1/@appstore/Readarr/var/.config/Readarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Readarr`

`/share/CACHEDEV1_DATA/Readarr_CONFIG`

# Docker

`/config`

- 这将根据用户在主机系统上映射 `/config` 的位置而有所不同

# 参数

`-data=` 参数强制指定 AppData 文件夹的位置，因此您的启动命令可能会强制指定特定位置。当尝试运行多个实例时，这是必需的。在 Windows 上，这将是 `/data=`

`-nobrowser` 参数在启动时不启动/打开浏览器。在 Windows 上，这将是 `/nobrowser`