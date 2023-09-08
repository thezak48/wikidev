---
title: Readarr MacOS 설치
description: Readarr을 위한 MacOS 설치 가이드
published: true
date: 2023-07-28T11:16:36.367Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:47.465Z
---

# MacOS (OSX)

{#OSX}

> .NET 호환성 문제로 인해 Readarr은 OSX 버전 10.15 (Catalina) 이상에서만 작동합니다.
{.is-warning}

1. 시스템에 따라 [MacOS 앱](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) 또는 [MacOS M1 앱](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)을 다운로드합니다.
1. 압축 파일을 열고 Readarr 아이콘을 애플리케이션 폴더로 드래그합니다.
1. Readarr을 자체 서명합니다. `codesign --force --deep -s - /Applications/Readarr.app && xattr -rd com.apple.quarantine /Applications/Readarr.app`
1. Readarr을 사용하기 위해 <http://localhost:8787>로 이동합니다.