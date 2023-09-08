---
title: Radarr应用数据目录
description: 
published: true
date: 2023-05-09T17:51:34.896Z
tags: radarr, appdata
editor: markdown
dateCreated: 2021-05-25T02:34:50.549Z
---

> 以下是应用数据目录的默认路径 {.is-info}

> 所有的`$USER`都是占位符，代表应用程序正在运行的用户 {.is-warning}

# Windows

`C:\ProgramData\Radarr`

# Linux

除非另有指定，否则Radarr将其应用数据存储在用户Radarr正在运行的主目录下的`/home/$USER/.config/Radarr`或`~/.config/Radarr`

安装说明指定为`/var/lib/radarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Radarr`或`~/.config/Radarr`

# Synology

`/usr/local/Radarr/var/.config/Radarr`

`/volume1/@appstore/Radarr/var/.config/Radarr'

`/volume1/@appdata/radarr/.config/Radarr'

# QNAP

`/share/MD0_DATA/homes/admin/.config/Radarr`

`/share/CACHEDEV1_DATA/Radarr_CONFIG`

# Docker

`/config`

- 这将根据用户在主机系统上映射`/config`的位置而有所不同

# 参数

`-data=`参数强制指定AppData文件夹的位置，因此您的启动命令可能会强制指定特定位置。在Windows上，这将是`/data=`

`-nobrowser`参数在启动时不启动/打开浏览器。在Windows上，这将是`/nobrowser`