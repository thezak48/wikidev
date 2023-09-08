---
title: RadarrのAppdataディレクトリ
description: 
published: true
date: 2023-05-09T17:51:34.896Z
tags: radarr, appdata
editor: markdown
dateCreated: 2021-05-25T02:34:50.549Z
---

> 以下は、アプリケーションデータディレクトリのデフォルトパスです {.is-info}

> `$USER` のすべてのインスタンスは、アプリケーションが実行されているユーザーのプレースホルダーです {.is-warning}

# Windows

`C:\ProgramData\Radarr`

# Linux

特に指定がない場合、Radarrはユーザーのホームフォルダにアプリケーションデータを保存します `/home/$USER/.config/Radarr` または `~/.config/Radarr`

インストール手順では `/var/lib/radarr` が指定されています

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Radarr` または `~/.config/Radarr`

# Synology

`/usr/local/Radarr/var/.config/Radarr`

`/volume1/@appstore/Radarr/var/.config/Radarr'

'/volume1/@appdata/radarr/.config/Radarr'

# QNAP

`/share/MD0_DATA/homes/admin/.config/Radarr`

`/share/CACHEDEV1_DATA/Radarr_CONFIG`

# Docker

`/config`

- これは、ユーザーがホストシステム上の `/config` にマップする場所によって異なります

# 引数

`-data=` 引数はAppDataフォルダの場所を強制します。したがって、起動コマンドは特定の場所を強制する必要があります。複数のインスタンスを実行しようとする場合に必要です。Windowsでは、これは `/data=` になります

`-nobrowser` 引数は、起動時にブラウザを起動/開かないようにします。Windowsでは、これは `/nobrowser` になります