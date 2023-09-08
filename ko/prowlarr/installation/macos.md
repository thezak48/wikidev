---
title: Prowlarr MacOS 설치
description: Prowlarr을 위한 MacOS 설치 가이드
published: true
date: 2023-07-28T11:17:40.904Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:30.382Z
---

# MacOS (OSX)

{#OSX}
  
> .NET 호환성 문제로 인해 Prowlarr은 OSX 버전 10.15 (Catalina) 이상에서만 작동합니다.
{.is-warning}

1. [MacOS 앱](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) 또는 [MacOS M1 앱](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)을 다운로드합니다. 시스템에 따라 선택하세요.
1. 압축 파일을 열고 Prowlarr 아이콘을 Application 폴더로 드래그합니다.
1. Prowlarr에 자체 서명을 추가합니다. `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine /Applications/Prowlarr.app` 명령을 실행합니다.
1. Prowlarr을 사용하기 위해 <http://localhost:9696>으로 이동합니다.