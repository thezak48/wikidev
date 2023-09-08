---
title: Readarr Appdata 디렉토리
description: 
published: true
date: 2021-11-24T19:24:45.782Z
tags: readarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:54:32.028Z
---

> 아래는 응용 프로그램 데이터 디렉토리의 기본 경로입니다. {.is-info}

> `$USER`는 응용 프로그램이 실행 중인 사용자를 나타내는 자리 표시자입니다. {.is-warning}

# Windows

`C:\ProgramData\Readarr`

# Linux

Readarr은 별도로 지정하지 않는 한 사용자의 홈 폴더인 `/home/$USER/.config/Readarr` 또는 `~/.config/Readarr`에 응용 프로그램 데이터를 저장합니다.

설치 지침에서는 `/var/lib/readarr`을 지정합니다.

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Readarr` 또는 `~/.config/Readarr`

# Synology

`/usr/local/Readarr/var/.config/Readarr`

`/volume1/@appstore/Readarr/var/.config/Readarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Readarr`

`/share/CACHEDEV1_DATA/Readarr_CONFIG`

# Docker

`/config`

- 이는 사용자가 호스트 시스템에서 `/config`에 매핑하는 위치에 따라 다를 수 있습니다.

# Arguments

`-data=` 인수는 AppData 폴더의 위치를 강제로 지정하므로 시작 명령에 특정 위치를 강제로 지정할 수 있습니다. 여러 인스턴스를 실행하려는 경우 이것이 필요합니다. Windows에서는 `/data=`가 됩니다.

`-nobrowser` 인수는 시작 시 브라우저를 열지 않도록 합니다. Windows에서는 `/nobrowser`가 됩니다.