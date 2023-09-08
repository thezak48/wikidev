---
title: ProwlarrのAppdataディレクトリ
description: 
published: true
date: 2021-11-24T19:22:49.484Z
tags: prowlarr, appdata
editor: markdown
dateCreated: 2021-06-08T01:06:44.136Z
---

> 以下は、アプリケーションデータディレクトリのデフォルトパスです {.is-info}

> `$USER` という表記は、アプリケーションが実行されているユーザーのプレースホルダーです {.is-warning}

# Windows

`C:\ProgramData\Prowlarr`

# Linux

特に指定がない限り、Prowlarrはユーザーのホームフォルダにアプリケーションデータを保存します。パスは `/home/$USER/.config/Prowlarr` または `~/.config/Prowlarr` です。

インストール手順では `/var/lib/prowlarr` が指定されています。

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Prowlarr` または `~/.config/Prowlarr`

# Synology

`/usr/local/Prowlarr/var/.config/Prowlarr`

`/volume1/@appstore/Prowlarr/var/.config/Prowlarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Prowlarr`

`/share/CACHEDEV1_DATA/Prowlarr_CONFIG`

# Docker

`/config`

- ユーザーがホストシステム上の `/config` にマップする場所によって異なります

# 引数

`-data=` 引数はAppDataフォルダの場所を強制します。複数のインスタンスを実行しようとする場合に必要です。Windowsでは `/data=` となります。

`-nobrowser` 引数は起動時にブラウザを起動/開かないようにします。Windowsでは `/nobrowser` となります。