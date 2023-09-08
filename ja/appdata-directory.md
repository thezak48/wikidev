---
title: LidarrのAppdataディレクトリ
description: 
published: true
date: 2021-11-24T19:22:06.078Z
tags: lidarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:53:13.142Z
---

> 以下は、アプリケーションデータディレクトリのデフォルトパスです {.is-info}

> `$USER` のすべてのインスタンスは、アプリケーションが実行されているユーザーのプレースホルダーです {.is-warning}

# Windows

`C:\ProgramData\Lidarr`

# Linux

特に指定がない限り、Lidarrはユーザーのホームフォルダにアプリケーションデータを保存します `/home/$USER/.config/Lidarr` または `~/.config/Lidarr`

インストール手順では `/var/lib/lidarr` が指定されています

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Lidarr` または `~/.config/Lidarr`

# Synology

`/usr/local/Lidarr/var/.config/Lidarr`

`/volume1/@appstore/Lidarr/var/.config/Lidarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Lidarr`

`/share/CACHEDEV1_DATA/Lidarr_CONFIG`

# Docker

`/config`

- これは、ユーザーがホストシステム上の `/config` にマップする場所によって異なります

# 引数

`-data=` 引数はAppDataフォルダの場所を強制します。したがって、起動コマンドは特定の場所を強制する必要があります。複数のインスタンスを実行しようとする場合に必要です。Windowsでは、`/data=` になります

`-nobrowser` 引数は、起動時にブラウザを起動/開かないようにします。Windowsでは、`/nobrowser` になります