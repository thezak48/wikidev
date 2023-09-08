---
title: Prowlarr Appdata 디렉토리
description: 
published: true
date: 2021-11-24T19:22:49.484Z
tags: prowlarr, appdata
editor: markdown
dateCreated: 2021-06-08T01:06:44.136Z
---

> 아래는 애플리케이션 데이터 디렉토리의 기본 경로입니다 {.is-info}

> `$USER`는 애플리케이션이 실행 중인 사용자를 나타내는 자리 표시자입니다 {.is-warning}

# Windows

`C:\ProgramData\Prowlarr`

# Linux

Prowlarr은 기본적으로 사용자의 홈 폴더에 애플리케이션 데이터를 저장합니다. 경로는 `/home/$USER/.config/Prowlarr` 또는 `~/.config/Prowlarr`입니다.

설치 지침에서는 `/var/lib/prowlarr`을 지정합니다.

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Prowlarr` 또는 `~/.config/Prowlarr`

# Synology

`/usr/local/Prowlarr/var/.config/Prowlarr`

`/volume1/@appstore/Prowlarr/var/.config/Prowlarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Prowlarr`

`/share/CACHEDEV1_DATA/Prowlarr_CONFIG`

# Docker

`/config`

- 이는 사용자가 호스트 시스템에서 `/config`를 매핑한 위치에 따라 다를 수 있습니다.

# Arguments

`-data=` 인수는 AppData 폴더의 위치를 강제로 지정하므로 시작 명령에 특정 위치를 강제로 지정할 수 있습니다. 여러 인스턴스를 실행하려는 경우 필요합니다. Windows에서는 `/data=`가 됩니다.

`-nobrowser` 인수는 시작 시 브라우저를 열지 않도록 합니다. Windows에서는 `/nobrowser`가 됩니다.