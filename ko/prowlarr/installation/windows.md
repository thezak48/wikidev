---
title: Prowlarr Windows 설치
description: Prowlarr을 위한 Windows 설치 가이드
published: true
date: 2023-08-28T19:43:08.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:39.779Z
---

# Windows

Prowlarr은 Windows에서 네이티브로 지원됩니다. Prowlarr은 Windows 서비스 또는 시스템 트레이 응용 프로그램으로 설치할 수 있습니다.
> Windows 버전은 현재 Microsoft에서 지원하는 버전에 대해서만 지원됩니다. 다른 버전은 작동할 수 있지만 이는 지원되지 않는 구성입니다.
{.is-warning}

Windows 서비스는 사용자가 로그인하지 않은 상태에서도 실행됩니다.
그렇지 않은 경우, 사용자가 로그인한 상태로 유지할 수 있다면 시스템 트레이 응용 프로그램을 사용할 수 있습니다. 설치 중에 해당 옵션이 제공됩니다.

> "C:\ProgramData\Prowlarr\config.xml" 경로에 대한 액세스 오류(예: 액세스가 거부됨)가 발생하는 경우 설치 후에 "관리자로 실행"으로 한 번 실행해야 할 수도 있습니다. 이렇게 하면 Prowlarr이 필요한 권한을 얻을 수 있습니다. 매번 관리자로 실행할 필요는 없어야 합니다.
{.is-warning}

1. 아래 링크에서 아키텍처에 맞는 최신 버전의 Prowlarr을 다운로드합니다.
1. 설치 프로그램을 실행합니다.
1. Prowlarr을 사용하기 위해 <http://localhost:9696>로 이동합니다.

- [Windows x64 설치 프로그램](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 설치 프로그램](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> [x64 .zip 다운로드](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64)를 사용하여 Prowlarr을 수동으로 설치할 수도 있습니다. 그러나 이 경우 종속성, 설치 및 권한을 수동으로 처리해야 합니다.
{.is-info}

> IIS의 LetsEncrypt 인증서 관리를 위해 [Certify The Web](https://docs.certifytheweb.com/docs/backgroundservice/)를 사용하고 동일한 컴퓨터에 Prowlarr을 설치하는 경우 백그라운드 서비스에서 포트 `9696`을 사용합니다. Prowlarr의 수신 포트를 `config.xml`에서 다른 포트로 변경하거나 Certify The Web 백그라운드 서비스의 포트를 변경해야 합니다.
{.is-info}