---
title: Sonarr MacOS 설치
description: Sonarr을 위한 MacOS 설치 가이드
published: true
date: 2023-07-28T11:15:29.588Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:29.890Z
---

# MacOS (OSX)

{#OSX}

> .NET 호환성 문제로 인해 Sonarr은 곧 OSX 버전 10.15 (Catalina) 이하에서 작동하지 않을 예정입니다.
{.is-warning}

1. [MacOS 앱](https://services.sonarr.tv/v1/download/main/latest?version=3&os=macos&installer=true)을 다운로드합니다.
1. 압축 파일을 열고 Sonarr 아이콘을 Application 폴더로 드래그합니다.
1. Sonarr을 자체 서명합니다. `codesign --force --deep -s - /Applications/Sonarr.app && xattr -rd com.apple.quarantine /Applications/Sonarr.app`
1. Sonarr을 사용하기 위해 <http://localhost:8989>로 이동합니다.