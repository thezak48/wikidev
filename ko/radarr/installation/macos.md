---
title: Radarr MacOS 설치
description: Radarr을 위한 MacOS 설치 안내서
published: true
date: 2023-07-28T09:08:51.541Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:05.036Z
---

# MacOS (OSX)

{#OSX}

> .NET 호환성 문제로 인해 Radarr은 OSX 버전 10.15 (Catalina) 이상에서만 작동합니다.
{.is-warning}

1. 시스템에 따라 [MacOS 앱](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) 또는 [MacOS M1 앱](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)을 다운로드합니다.
1. 압축 파일을 열고 Radarr 아이콘을 Application 폴더로 드래그합니다.
1. Radarr을 자체 서명합니다. `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine /Applications/Radarr.app`
1. Radarr을 사용하기 위해 <http://localhost:7878>로 이동합니다.

> Radarr은 미디어 파일 분석을 위해 번들 버전의 ffprobe를 사용하며, 시스템에 ffprobe 또는 ffmpeg를 설치할 필요가 없습니다. Radarr에서 Ffprobe를 찾을 수 없다는 메시지가 표시되면 일반적으로 다시 설치하여 해결할 수 있습니다.
{.is-info}