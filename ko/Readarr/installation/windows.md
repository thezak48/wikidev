---
title: Readarr Windows 설치
description: Readarr을 위한 Windows 설치 가이드
published: true
date: 2023-07-04T15:23:25.114Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:03.495Z
---

# Windows

Readarr은 Windows에서 네이티브로 지원됩니다. Readarr은 Windows 서비스 또는 시스템 트레이 응용 프로그램으로 설치할 수 있습니다.
> Windows 버전은 Microsoft에서 현재 지원하는 버전에 대해서만 지원됩니다. 다른 버전은 작동할 수 있지만, 이는 지원되지 않는 구성입니다.
{.is-warning}

Windows 서비스는 사용자가 로그인하지 않은 상태에서도 실행됩니다. 그러나 특별한 구성 단계 없이 Windows 서비스는 네트워크 드라이브(X:\ 매핑된 드라이브 또는 \\\server\share UNC 경로)에 액세스할 수 없습니다.

또한 Windows 서비스는 'Local Service' 계정에서 실행되며, 기본적으로 이 계정은 **수동으로 사용자의 홈 디렉토리에 액세스할 수 있는 권한이 없습니다**. 이는 특히 홈 디렉토리로 다운로드를 구성한 다운로드 클라이언트를 사용할 때 중요합니다.

따라서 사용자가 로그인한 상태로 유지될 수 있다면 Readarr을 시스템 트레이 응용 프로그램으로 설치하는 것이 좋습니다. 이 옵션은 설치 프로그램에서 제공됩니다.

> 설치 후에 "관리자로 실행"을 한 번 실행해야 할 수도 있습니다. 예를 들어, 액세스 오류(예: 경로 `C:\ProgramData\Readarr\config.xml`에 대한 액세스가 거부됨)가 발생하거나 매핑된 네트워크 드라이브를 사용하는 경우입니다. 이렇게 하면 Readarr이 필요한 권한을 얻을 수 있습니다. 매번 관리자로 실행할 필요는 없어야 합니다.
{.is-warning}

> 경고: [PmsService](https://github.com/cjmurph/PmsService)를 통해 Plex를 서비스로 실행하는 경우, PMsService의 포트를 `8787`에서 변경하거나 `config.xml` 파일에서 Readarr이 실행되는 포트를 수정해야 합니다.
{.is-info}

1. 아래 링크된 아키텍처에 맞는 최신 버전의 Readarr을 다운로드합니다.
1. 설치 프로그램을 실행합니다.
1. <http://localhost:8787>로 이동하여 Readarr을 사용 시작합니다.

- [Windows x64 설치 프로그램](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 설치 프로그램](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> [x64 .zip 다운로드](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64)를 사용하여 Readarr을 수동으로 설치할 수도 있습니다. 그러나 이 경우 종속성, 설치 및 권한을 수동으로 처리해야 합니다.
{.is-info}