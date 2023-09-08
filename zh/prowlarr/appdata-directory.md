---
title: Prowlarr应用数据目录
description: 
published: true
date: 2021-11-24T19:22:49.484Z
tags: prowlarr, appdata
editor: markdown
dateCreated: 2021-06-08T01:06:44.136Z
---

> 以下是应用数据目录的默认路径 {.is-info}

> 所有的`$USER`都是占位符，代表应用程序正在运行的用户 {.is-warning}

# Windows

`C:\ProgramData\Prowlarr`

# Linux

除非另有指定，Prowlarr将其应用数据存储在用户Prowlarr正在运行的主目录下 `/home/$USER/.config/Prowlarr` 或 `~/.config/Prowlarr`

安装说明指定了 `/var/lib/prowlarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Prowlarr` 或 `~/.config/Prowlarr`

# Synology

`/usr/local/Prowlarr/var/.config/Prowlarr`

`/volume1/@appstore/Prowlarr/var/.config/Prowlarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Prowlarr`

`/share/CACHEDEV1_DATA/Prowlarr_CONFIG`

# Docker

`/config`

- 这将根据用户在主机系统上映射`/config`的位置而有所不同

# 参数

`-data=`参数强制指定AppData文件夹的位置，因此您的启动命令可能会强制指定特定位置。当尝试运行多个实例时，这是必需的。在Windows上，这将是`/data=`

`-nobrowser`参数在启动时不启动/打开浏览器。在Windows上，这将是`/nobrowser`