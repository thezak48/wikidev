---
title: Sonarr应用数据目录
description: 
published: true
date: 2021-11-24T19:25:42.806Z
tags: 
editor: markdown
dateCreated: 2021-06-09T15:53:57.860Z
---

> 以下是应用数据目录的默认路径 {.is-info}

> 所有的`$USER`都是应用程序正在运行的用户的占位符 {.is-warning}

# Windows

`C:\ProgramData\Sonarr`

# Linux

除非另有说明，Sonarr将把其应用数据存储在用户Sonarr正在运行的主目录下的`/home/$USER/.config/Sonarr`或`~/.config/Sonarr`

> 对于基于apt仓库的安装，默认为`/var/lib/Sonarr`
{.is-info}

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Sonarr`或`~/.config/Sonarr`

# Synology

如果您正在使用SynoCommunity软件包安装Sonarr，则应在此处找到您的应用数据。如果您在Synology NAS上使用Docker，请查看下面的Docker部分。

## DSM 7及以上版本

`/volume1/@appdata/nzbdrone/.config/Sonarr`

## DSM 6及以下版本

`/volume1/@appstore/nzbdrone/.config/Sonarr`

> SynoCommunity仍然使用原始软件包名称`nzbdrone`作为底层软件包名称 {.is-info}

# QNAP

`/share/MD0_DATA/homes/admin/.config/Sonarr`

`/share/CACHEDEV1_DATA/Sonarr_CONFIG`

# Docker

`/config`

- 这将根据用户在主机系统上映射`/config`的位置而有所不同

# 参数

`-data=`参数强制指定AppData文件夹的位置，因此您的启动命令可能会强制指定特定位置。在Windows上，这将是`/data=`

`-nobrowser`参数在启动时不启动/打开浏览器。在Windows上，这将是`/nobrowser`