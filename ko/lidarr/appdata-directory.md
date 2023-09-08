---
title: Lidarr Appdata 디렉토리
description: 
published: true
date: 2021-11-24T19:22:06.078Z
tags: lidarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:53:13.142Z
---

> 아래는 응용 프로그램 데이터 디렉토리의 기본 경로입니다 {.is-info}

> `$USER`라는 모든 인스턴스는 응용 프로그램이 실행 중인 사용자를 나타냅니다 {.is-warning}

# Windows

`C:\ProgramData\Lidarr`

# Linux

그렇지 않은 경우, Lidarr은 사용자의 홈 폴더에 응용 프로그램 데이터를 저장합니다. `/home/$USER/.config/Lidarr` 또는 `~/.config/Lidarr`

설치 지침에서는 `/var/lib/lidarr`를 지정합니다.

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Lidarr` 또는 `~/.config/Lidarr`

# Synology

`/usr/local/Lidarr/var/.config/Lidarr`

`/volume1/@appstore/Lidarr/var/.config/Lidarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Lidarr`

`/share/CACHEDEV1_DATA/Lidarr_CONFIG`

# Docker

`/config`

- 이는 사용자가 호스트 시스템에서 `/config`에 매핑하는 위치에 따라 다를 수 있습니다.

# Arguments

`-data=` 인수는 AppData 폴더의 위치를 강제로 지정하므로 시작 명령에 특정 위치를 강제로 지정해야 합니다. 여러 인스턴스를 실행하려는 경우 필요합니다. Windows에서는 `/data=`가 됩니다.

`-nobrowser` 인수는 시작 시 브라우저를 실행/열지 않도록 합니다. Windows에서는 `/nobrowser`가 됩니다.