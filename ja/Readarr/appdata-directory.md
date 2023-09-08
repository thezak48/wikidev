---
title: ReadarrのAppdataディレクトリ
description: 
published: true
date: 2021-11-24T19:24:45.782Z
tags: readarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:54:32.028Z
---

> 以下は、アプリケーションデータディレクトリのデフォルトパスです {.is-info}

> `$USER` というすべてのインスタンスは、アプリケーションが実行されているユーザーのプレースホルダーです {.is-warning}

# Windows

`C:\ProgramData\Readarr`

# Linux

それ以外が指定されていない限り、Readarrはユーザーのホームフォルダにアプリケーションデータを保存します `/home/$USER/.config/Readarr` または `~/.config/Readarr`

インストール手順では `/var/lib/readarr` が指定されています

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Readarr` または `~/.config/Readarr`

# Synology

`/usr/local/Readarr/var/.config/Readarr`

`/volume1/@appstore/Readarr/var/.config/Readarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Readarr`

`/share/CACHEDEV1_DATA/Readarr_CONFIG`

# Docker

`/config`

- これは、ユーザーがホストシステム上の `/config` にマップする場所によって異なります

# 引数

`-data=` 引数はAppDataフォルダの場所を強制します。したがって、起動コマンドでは特定の場所を強制する必要があります。複数のインスタンスを実行しようとする場合に必要です。Windowsでは、これは `/data=` になります

`-nobrowser` 引数は、起動時にブラウザを起動/開かないようにします。Windowsでは、これは `/nobrowser` になります