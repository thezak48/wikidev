---
title: Lidarr Windows 설치
description: Lidarr을 위한 Windows 설치 가이드
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Windows

Lidarr은 Windows에서 네이티브로 지원됩니다. Lidarr은 Windows 서비스 또는 시스템 트레이 응용 프로그램으로 설치할 수 있습니다.
> Windows 버전은 현재 Microsoft에서 지원하는 버전에 한정되며, 다른 버전도 작동할 수 있지만 이는 지원되지 않는 구성입니다.
{.is-warning}

Windows 서비스는 사용자가 로그인하지 않은 상태에서도 실행됩니다. 그러나 특별한 구성 단계 없이 Windows 서비스는 네트워크 드라이브(X:\ 매핑된 드라이브 또는 \\\server\share UNC 경로)에 액세스할 수 없습니다.

또한 Windows 서비스는 'Local Service' 계정에서 실행되며, 기본적으로 이 계정은 **사용자의 홈 디렉토리에 액세스할 수 있는 권한이 수동으로 할당되지 않은 경우에는 액세스할 수 없습니다**. 이는 특히 홈 디렉토리로 다운로드 클라이언트를 구성한 경우에 관련이 있습니다.

따라서 사용자가 로그인한 상태로 유지될 수 있다면 Lidarr을 시스템 트레이 응용 프로그램으로 설치하는 것이 좋습니다. 설치 도중 이 옵션을 선택할 수 있습니다.

> 트레이 모드로 설치한 후 "관리자로 실행"을 한 번 실행해야 할 수도 있습니다. 액세스 오류(예: 경로 `C:\ProgramData\Lidarr\config.xml`에 액세스가 거부됨)가 발생하는 경우나 매핑된 네트워크 드라이브를 사용하는 경우입니다. 이렇게 하면 Lidarr이 필요한 권한을 얻을 수 있습니다. 매번 관리자로 실행할 필요는 없어야 합니다.
{.is-warning}

1. 아래 링크에서 아키텍처에 맞는 최신 버전의 Lidarr을 다운로드합니다.
1. 설치 프로그램을 실행합니다.
1. Lidarr을 사용하기 위해 <http://localhost:8686>로 이동합니다.

- [Windows x64 설치 프로그램](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 설치 프로그램](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> [x64 .zip 다운로드](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64)를 사용하여 Lidarr을 수동으로 설치할 수도 있습니다. 그러나 이 경우 종속성, 설치 및 권한을 수동으로 처리해야 합니다.
{.is-info}