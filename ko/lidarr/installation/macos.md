---
title: Lidarr MacOS 설치
description: Lidarr을 위한 MacOS 설치 가이드
published: true
date: 2023-07-28T11:16:00.388Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:53.957Z
---

# MacOS (OSX)

{#OSX}

> .NET 호환성 문제로 인해 Lidarr은 OSX 버전 10.15 (Catalina) 이상에서만 작동합니다.
{.is-warning}

1. [MacOS 앱](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) 또는 [MacOS M1 앱](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)을(를) 다운로드합니다. 시스템에 따라 선택하세요.
1. 압축 파일을 열고 Lidarr 아이콘을 응용 프로그램 폴더로 드래그합니다.
1. Lidarr을 자체 서명합니다. `codesign --force --deep -s - /Applications/Lidarr.app && xattr -rd com.apple.quarantine /Applications/Lidarr.app` 명령을 실행합니다.
1. Lidarr을 사용하기 위해 <http://localhost:8686>으로 이동합니다.