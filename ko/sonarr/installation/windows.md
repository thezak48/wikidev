---
title: Sonarr Windows 설치
description: Sonarr을 위한 Windows 설치 가이드
published: true
date: 2023-07-04T15:22:44.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:54.851Z
---

# Windows

Sonarr은 Windows에서 네이티브로 지원됩니다. Sonarr은 Windows 서비스 또는 시스템 트레이 응용 프로그램으로 설치할 수 있습니다.

> Windows 버전은 현재 Microsoft에서 지원하는 버전에 대해서만 지원됩니다. 다른 버전도 작동할 수 있지만, 이는 지원되지 않는 구성입니다.
{.is-warning}

Windows 서비스는 사용자가 로그인하지 않은 상태에서도 실행됩니다. 그러나 특별한 구성 단계 없이 Windows 서비스는 네트워크 드라이브(X:\ 매핑된 드라이브 또는 \\\server\share UNC 경로)에 액세스할 수 없습니다.

또한 Windows 서비스는 기본적으로 'Local Service' 계정에서 실행됩니다. 이 계정은 기본적으로 사용자의 홈 디렉토리에 액세스할 수 있는 권한이 없습니다. 이는 특히 홈 디렉토리로 다운로드하는 설정이 구성된 다운로드 클라이언트를 사용할 때 중요합니다.

따라서 사용자가 로그인한 상태로 유지될 수 있다면 Sonarr을 시스템 트레이 응용 프로그램으로 설치하는 것이 좋습니다. 설치 도중에 이 옵션을 선택할 수 있습니다.

> 설치 후에 "관리자로 실행"을 한 번 실행해야 할 수도 있습니다. 예를 들어, 액세스 오류가 발생하는 경우 - 예: 경로 `C:\ProgramData\Sonarr\config.xml`에 액세스가 거부됨 - 또는 매핑된 네트워크 드라이브를 사용하는 경우입니다. 이렇게 하면 Sonarr이 필요한 권한을 얻을 수 있습니다. 매번 관리자로 실행할 필요는 없어야 합니다.
{.is-warning}

1. 아래 링크에서 아키텍처에 맞는 최신 버전의 Sonarr을 다운로드합니다.
1. 설치 프로그램을 실행합니다.
1. Sonarr을 사용하기 위해 <http://localhost:8989>로 이동합니다.

- [Windows x32 설치 프로그램](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows&installer=true)
{.links-list}

> [x32 .zip 다운로드](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows)를 사용하여 Sonarr을 수동으로 설치할 수도 있습니다. 그러나 이 경우 종속성, 설치 및 권한을 수동으로 처리해야 합니다.
{.is-info}