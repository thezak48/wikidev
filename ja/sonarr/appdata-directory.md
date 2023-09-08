---
title: SonarrのAppdataディレクトリ
description: 
published: true
date: 2021-11-24T19:25:42.806Z
tags: 
editor: markdown
dateCreated: 2021-06-09T15:53:57.860Z
---

> 以下はアプリケーションデータディレクトリのデフォルトパスです {.is-info}

> `$USER` のすべてのインスタンスは、アプリケーションが実行されているユーザーのプレースホルダーです {.is-warning}

# Windows

`C:\ProgramData\Sonarr`

# Linux

特に指定がない限り、Sonarrはユーザーのホームフォルダにアプリケーションデータを保存します `/home/$USER/.config/Sonarr` または `~/.config/Sonarr`

> aptリポジトリベースのインストールでは、デフォルトで `/var/lib/Sonarr` になります
{.is-info}

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Sonarr` または `~/.config/Sonarr`

# Synology

SynoCommunityパッケージを使用している場合、アプリデータはここに保存されます。Synology NASでDockerを使用している場合は、Dockerセクションを参照してください。

## DSM 7以降

`/volume1/@appdata/nzbdrone/.config/Sonarr`

## DSM 6以前

`/volume1/@appstore/nzbdrone/.config/Sonarr`

> SynoCommunityは、基礎となるパッケージ名に対して `nzbdrone` の元のパッケージ名を使用しています {.is-info}

# QNAP

`/share/MD0_DATA/homes/admin/.config/Sonarr`

`/share/CACHEDEV1_DATA/Sonarr_CONFIG`

# Docker

`/config`

- これは、ユーザーがホストシステム上の `/config` にマップする場所によって異なります

# 引数

`-data=` 引数はAppDataフォルダの場所を強制します。したがって、起動コマンドは特定の場所を強制する必要があります。複数のインスタンスを実行しようとする場合に必要です。Windowsでは、`/data=` になります

`-nobrowser` 引数は、起動時にブラウザを起動/開かないようにします。Windowsでは、`/nobrowser` になります