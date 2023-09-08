---
title: Radarr Appdata 디렉토리
description: 
published: true
date: 2023-05-09T17:51:34.896Z
tags: radarr, appdata
editor: markdown
dateCreated: 2021-05-25T02:34:50.549Z
---

> 아래는 응용 프로그램 데이터 디렉토리의 기본 경로입니다 {.is-info}

> `$USER`라는 모든 인스턴스는 응용 프로그램이 실행 중인 사용자를 나타냅니다 {.is-warning}

# Windows

`C:\ProgramData\Radarr`

# Linux

Radarr의 응용 프로그램 데이터는 기본적으로 사용자 Radarr이 실행 중인 홈 폴더에 저장됩니다. `/home/$USER/.config/Radarr` 또는 `~/.config/Radarr`로 지정됩니다.

설치 지침에서는 `/var/lib/radarr`를 지정합니다.

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Radarr` 또는 `~/.config/Radarr`

# Synology

`/usr/local/Radarr/var/.config/Radarr`

`/volume1/@appstore/Radarr/var/.config/Radarr'

'/volume1/@appdata/radarr/.config/Radarr'

# QNAP

`/share/MD0_DATA/homes/admin/.config/Radarr`

`/share/CACHEDEV1_DATA/Radarr_CONFIG`

# Docker

`/config`

- 이는 사용자가 호스트 시스템에서 `/config`를 매핑하는 위치에 따라 다를 수 있습니다.

# Arguments

`-data=` 인수는 AppData 폴더의 위치를 강제로 지정하므로 시작 명령에 특정 위치를 강제로 지정해야 합니다. 여러 인스턴스를 실행하려는 경우 이것은 필수입니다. Windows에서는 `/data=`가 됩니다.

`-nobrowser` 인수는 시작 시 브라우저를 열지 않도록 합니다. Windows에서는 `/nobrowser`가 됩니다.