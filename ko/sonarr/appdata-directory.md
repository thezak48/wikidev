---
title: Sonarr Appdata 디렉토리
description: 
published: true
date: 2021-11-24T19:25:42.806Z
tags: 
editor: markdown
dateCreated: 2021-06-09T15:53:57.860Z
---

> 아래는 응용 프로그램 데이터 디렉토리의 기본 경로입니다 {.is-info}

> `$USER`라는 모든 인스턴스는 응용 프로그램이 실행 중인 사용자를 나타냅니다 {.is-warning}

# Windows

`C:\ProgramData\Sonarr`

# Linux

그렇지 않은 경우 Sonarr는 사용자 Sonarr이 실행 중인 홈 폴더에 응용 프로그램 데이터를 저장합니다. `/home/$USER/.config/Sonarr` 또는 `~/.config/Sonarr`

> apt 저장소 기반 설치의 경우, 기본값은 `/var/lib/Sonarr`입니다
{.is-info}

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Sonarr` 또는 `~/.config/Sonarr`

# Synology

Sonarr에 대한 SynoCommunity 패키지를 사용하는 경우, 여기에서 앱 데이터를 찾을 수 있습니다. Synology NAS에서 Docker를 사용하는 경우 Docker 섹션 아래를 참조하십시오.

## DSM 7 이상

`/volume1/@appdata/nzbdrone/.config/Sonarr`

## DSM 6 이하

`/volume1/@appstore/nzbdrone/.config/Sonarr`

> SynoCommunity는 여전히 기본 패키지 이름 `nzbdrone`을 사용합니다 {.is-info}

# QNAP

`/share/MD0_DATA/homes/admin/.config/Sonarr`

`/share/CACHEDEV1_DATA/Sonarr_CONFIG`

# Docker

`/config`

- 이는 사용자가 호스트 시스템에서 `/config`를 매핑하는 위치에 따라 다를 수 있습니다.

# Arguments

`-data=` 인수는 AppData 폴더의 위치를 강제로 지정하므로 시작 명령에 특정 위치를 강제로 지정해야 합니다. 여러 인스턴스를 실행하려는 경우 이것이 필요합니다. Windows에서는 `/data=`가 됩니다.

`-nobrowser` 인수는 시작 시 브라우저를 실행/열지 않도록 합니다. Windows에서는 `/nobrowser`가 됩니다.