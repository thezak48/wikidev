---
title: 유용한 도구
description: 
published: true
date: 2023-08-28T09:19:27.683Z
tags: useful-tools
editor: markdown
dateCreated: 2021-06-05T20:51:53.183Z
---

# 목차

- [목차](#목차)
- [손상된 DB 복구](#손상된-db-복구)
  - [손상된 DB 복구 (UI) (Windows)](#손상된-db-복구-ui-windows)
  - [명령 줄 DB 복구](#명령-줄-db-복구)
- [쿠키 찾기](#쿠키-찾기)
  - [Chrome](#chrome)
  - [Firefox](#firefox)
- [쿠키 및 로컬 스토리지 지우기](#쿠키-및-로컬-스토리지-지우기)
  - [Chrome](#chrome-1)
  - [Firefox](#firefox-1)
  - [Microsoft Edge (Chromium)](#microsoft-edge-chromium)
  {.links-list}
- [기타 프로젝트 및 프로그램 - 요청 앱 \*Arrs](#기타-프로젝트-및-프로그램-요청-앱-arrs)
  - [Notifiarr](#notifiarr-fka-discord-notifier)
  - [Ombi](#ombi)
  - [Overseerr](#overseerr)
  - [Petio](#petio)
  {.links-list}
- [기타 프로젝트 및 프로그램 - \*Arr 관련](#기타-프로젝트-및-프로그램-arr-관련)
  - [원격 제어](#원격-제어)
    - [LunaSea](#lunasea)
    - [Radarr & Sonarr Companion - Android 앱](#radarr-sonarr-companion-android-앱)
    - [nzb360 - Android 앱](#nzb360-android-앱)
    {.links-list}
  - [Lidarr](#lidarr)
    - [AMD](#amd)
    - [AMVD](#amvd)
  - [Radarr](#radarr)
    - [AMTD](#amtd)
  - [자막](#자막)
    - [Bazarr](#bazarr)
- [기타 프로젝트 및 프로그램 - 토렌트/다운로드](#기타-프로젝트-및-프로그램-토렌트다운로드)
  - [Cross-Seed](#cross-seed)
  - [Unpackerr](#unpackerr)
  - [qBit Management](#qbit-management)
- [기타 프로젝트 및 프로그램](#기타-프로젝트-및-프로그램)
  - [Filebot](#filebot)
  - [JDupes](#jdupes)
  - [Just A Bunch Of Starr Scripts](#just-a-bunch-of-starr-scripts)
  - [Just A Bunch Of Plex Scripts (JBOPS)](#just-a-bunch-of-plex-scripts)
  - [Plex Meta Manager](#plex-meta-manager)
  - [Tautulli](#tautulli)
  - [Tdarr](#tdarr)
  - [tdarr_inform](#tdarr_inform)
  {.links-list}
- [Twitter 연결 지침](#twitter-연결-지침)

다음 앱들은 \*Arr 애플리케이션 스위트 또는 미디어 저장과 관련된 도구입니다. 이러한 도구들은 \*Arr 개발팀에 의해 유지, 개발 또는 지원되지 않습니다. 특정 지원 질문은 해당 애플리케이션 개발팀에 문의하십시오.

# 손상된 DB 복구

애플리케이션의 데이터베이스는 아래에 연결된 애플리케이션 데이터 디렉토리에서 찾을 수 있습니다. 디렉토리는 datadir 인수로 전달될 수도 있습니다.

- [Lidarr 앱 데이터 디렉토리](/lidarr/appdata-directory)
- [Prowlarr 앱 데이터 디렉토리](/prowlarr/appdata-directory)
- [Radarr 앱 데이터 디렉토리](/radarr/appdata-directory)
- [Readarr 앱 데이터 디렉토리](/readarr/appdata-directory)
- [Sonarr 앱 데이터 디렉토리](/sonarr/appdata-directory)
{.links-list}

> 아래에 나열된 두 가지 옵션으로 데이터베이스를 복구할 수 있습니다.{.is-info}

- [DB Browser for SQLite를 사용하여 UI로 복구](#손상된-db-복구-ui)
- [Sqlite의 `.recover` 함수를 사용하여 명령 줄 DB 복구](#명령-줄-db-복구)
{.links-list}

## 손상된 DB 복구 (UI) (Windows)

{#windows}
{#손상된-db-복구-ui}

> 이는 Sqlite v3.29 | [`.recover` 명령에 대한 자세한 내용은 Sqlite 문서를 참조하십시오](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database)와 동일한 작업을 수행합니다. 아래에 수행 방법이 연결되어 있습니다.{.is-info}

> [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/)는 SQLite와 호환되는 데이터베이스 파일을 생성, 설계 및 편집하기 위한 고품질 시각적 오픈 소스 도구입니다. DB4S는 데이터베이스를 생성, 검색 및 편집하려는 사용자와 개발자를 위한 것입니다. DB4S는 익숙한 스프레드시트와 유사한 인터페이스를 사용하며, 복잡한 SQL 명령을 배울 필요가 없습니다.
{.is-info}

1. 애플리케이션을 중지합니다.
1. 손상된 데이터베이스 (`.db`)의 사본을 만들고 `.shm` 및 `.wal` 파일을 함께 복사합니다.
1. [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/)에서 손상된 데이터베이스를 엽니다.
1. 파일 => 내보내기 => SQL 파일로 데이터베이스 내보내기
1. 모든 테이블 선택
1. "INSERT INTO에 열 이름 유지" 확인/활성화
1. 모두 내보내기
1. 이전 스키마 덮어쓰기
1. 저장
1. 데이터베이스 닫기
1. 새 데이터베이스 => 파일 => 가져오기 => 이전 내보내기 단계에서의 파일 가져오기
1. 가져오기 오류 또는 제약 조건 문제가 있는 경우, 가능한 경우 문제가 있는 삽입 문을 정리하거나 삭제합니다.
1. 다음 SQL을 실행합니다: `VACUUM;`
1. 프롬프트가 나타나면 데이터베이스를 저장합니다.
1. 도구 => 무결성 확인; 결과는 OK라고 표시되어야 합니다.
1. 데이터베이스 닫기
1. 구성 폴더에서 모든 `wal`, `shm`, `db` 파일을 제거합니다.
1. (또는 \*Arr이 DB4S와 동일한 시스템에 없는 경우 복사) 구성 폴더에 새 데이터베이스를 저장하고 애플리케이션에 대상을 지정합니다. 모든 \*Arr은 데이터베이스를 `<appname>.db`로 이름 지정합니다. 예: `radarr.db`
1. 복구된 데이터베이스에 필요한 권한을 올바르게 설정합니다. 소유자는 \*Arr이 구성된 사용자 및 그룹이어야 합니다.
1. 애플리케이션을 시작합니다.

`VACUUM;` 명령은 gif에 포함되어 있지 않음을 참고하세요.

![dbrecover.gif](/dbrecover.gif)

## 명령 줄 DB 복구

{#nix}

아래 지침은 \*Nix 운영 체제를 위한 것이지만 Windows 명령 줄에서도 유사한 개념이 적용됩니다.

> 이는 [sqlite3 `.recover` 명령](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database)을 사용하는 것이 이상적입니다. 이는 Sqlite 3.29+를 필요로 합니다.
{.is-info}

> \*Arrs에서 sqlite3가 필요하므로 시스템에 sqlite3가 설치되어 있다고 가정합니다.
{.is-info}

1. 애플리케이션을 중지합니다.
1. 상자에 SSH를 입력하거나 셸을 엽니다.
1. `sqlite3 <bad database 경로> ".recover" | sqlite3 <복구된 데이터베이스의 출력 경로>`를 입력합니다.
1. 복구된 데이터베이스에 필요한 권한을 올바르게 설정합니다. 소유자는 \*Arr이 구성된 사용자 및 그룹이어야 합니다.
1. 이전 손상된 데이터베이스와 폴더 내의 모든 `wal` 또는 `shm`을 제거하거나 이동/이름을 변경합니다.
1. 복구된 데이터베이스의 이름을 변경합니다. 모든 \*Arr은 데이터베이스를 `<appname>.db`로 이름 지정합니다. 예: `radarr.db`
1. 애플리케이션을 시작합니다.

# 쿠키 찾기

- 일부 사이트는 자동으로 로그인할 수 없으며 수동으로 로그인한 다음 쿠키를 제공해야 작동합니다. 아래 페이지에서 해당 작업을 수행하는 방법에 대해 설명합니다.

## 일반 지침

1. Prowlarr 인덱서 구성에서 사용할 사이트 링크 주소를 사용하여 브라우저에서 웹 사이트에 로그인합니다.
1. F12 키를 눌러 개발 도구 패널을 엽니다.
1. 네트워크 탭을 선택합니다.
1. Doc 버튼 (Chrome 브라우저) 또는 HTML 버튼 (Firefox 브라우저)을 클릭합니다.
1. F5 키를 눌러 페이지를 새로 고칩니다.
1. 첫 번째 행 항목을 클릭합니다.
1. 오른쪽 패널에서 헤더 탭을 선택합니다.
1. 요청 헤더 섹션에서 'cookie:'를 찾습니다. 트래커에 대한 UI의 도움말 텍스트를 참조하세요.
1. 전체 쿠키 문자열 (cookie: 이후의 모든 것)을 선택하고 복사합니다.
1. Prowlarr 인덱서 구성 쿠키 상자에 이미 있는 내용을 삭제합니다.
1. 복사한 쿠키 문자열을 해당 상자에 붙여넣습니다.
1. 저장을 클릭합니다.

> 트래커에 사용자 에이전트가 필요한 경우 요청 헤더에서 찾을 수 있습니다.
{.is-info}

### 참고 사항

- 쿠키는 거의 다른 플랫폼에서 작동하지 않으므로 Prowlarr을 실행하는 동일한 컴퓨터에서 브라우저를 사용해야 합니다.
- 웹 사이트의 로그인 페이지에서 세션을 한 IP 주소로 제한하거나 짧은 시간 후에 로그아웃하는 옵션을 선택하지 마십시오. "기억하기" 옵션이 있는 경우 사용하십시오.
- 쿠키를 사용한 후에도 사이트의 토런트 검색 페이지에 액세스할 수 있는지 확인하십시오. 사이트가 이를 방지하기 위해 수행하는 작업(알림, 읽지 않은 알림 또는 읽지 않은 개인 메시지 또는 낮은 비율 경고)은 쿠키를 사용한 후에 Prowlarr이 성공적인 테스트를 할 수 없게 합니다.

## Chrome

- 토렌트 트래커 웹 사이트로 이동하여 로그인합니다.

- F12 키를 누릅니다.

- 상단에 있는 Application 탭에서 왼쪽에 "Storage"가 있습니다. "Cookies" 하위 섹션 아래에 트래커의 URL이 표시됩니다. 해당 URL을 클릭합니다.

- 해당 탭에서 "Pass" 또는 유사한 항목을 클릭하면 "Cookie Value"라는 상자가 나타나며, 약 25-30자 정도의 문자열이 표시됩니다. 해당 문자열을 복사하여 필요한 애플리케이션에 붙여넣습니다.

  - 문자열이 `cid=cid-that-you-got-from-the-browser; sid=sid-that-you-got-from-the-browser`와 유사한 경우 전체 항목을 사용해야 합니다.

![cookie_chrome.png](/assets/prowlarr/cookie_chrome.png)

- Chrome 문서 [Chrome cookies](https://developer.chrome.com/docs/devtools/storage/cookies/)도 참조할 수 있습니다.

## Firefox

- [Mozilla 문서를 참조하세요](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Cookies)

![faq_3_cookies.png](/assets/general/faq_3_cookies.png)

# 쿠키 및 로컬 스토리지 지우기

## Chrome

1. `chrome://settings/siteData`로 이동합니다.
1. 지우려는 사이트(또는 앱) 이름을 입력합니다.
1. 사이트 옆의 휴지통 아이콘을 클릭합니다.

## Firefox

- [Mozilla 도움말 문서](https://support.mozilla.org/en-US/kb/clear-cookies-and-site-data-firefox)를 참조하세요.

## Microsoft Edge (Chromium)

1. `edge://settings/siteData`로 이동합니다.
1. 지우려는 사이트(또는 앱) 이름을 입력합니다.
1. 사이트 옆의 화살표를 클릭합니다.
1. 사이트 옆의 휴지통 아이콘을 클릭합니다.

# 기타 프로젝트 및 프로그램 - 요청 앱 \*Arrs

## Notifiarr (fka Discord Notifier)

[Notifiarr](https://notifiarr.com/)는 \*Arr 개발자 중 한 명이 자세한 디스코드 알림을 제공하기 위해 만든 도구입니다. 선택한 트리거에 기반한 알림(반응 포함)을 구성할 수 있는 구성 가능한 방법을 제공합니다. 웹 사이트에서 알림에 표시할 내용을 선택할 수 있는 UI를 제공합니다. Grab, Import, Upgrade, Health 및 Failed 알림을 비롯한 다양한 알림을 지원합니다.

[위키](https://notifiarr.wiki/)

주요 기능

- 애플리케이션 상태
- 요청 및 승인 (\~Ombi)
- 사용자 정의 *ARR 애플리케이션 알림
- 승인을 위한 요청 시스템
- 사용자가 시리즈 또는 영화를 모니터링하고 알림을 받을 수 있는 팔로우 시스템 (@멘션을 통해)
- 서버 상태
- 새로운 기능 빈도

## Ombi

[Ombi](https://github.com/tidusjar/Ombi/)는 사용자가 영화, TV 프로그램(시리즈, 시즌 또는 단일 에피소드) 및 음악 앨범을 요청할 수 있는 기능을 제공합니다.

## Overseerr

[Overseerr](https://overseerr.dev/)는 기존 Plex 생태계와 함께 작동하는 요청 관리 및 미디어 탐색 도구입니다.

## Petio

[Petio](https://petio.tv/)는 Plex 서버 소유자에게 제공되는 타사 동반 앱으로, 사용자가 콘텐츠를 요청, 검토 및 발견할 수 있도록 합니다.

이 앱은 가장 기술에 대해 친숙하고 직관적인 사용자에게 즉각적으로 익숙한 인터페이스를 제공합니다. Petio는 사용자의 요청을 관리하고, Sonarr 및 Radarr과 같은 타사 앱에 연결하며, 콘텐츠를 사용 가능할 때 사용자에게 알림을 보내고 요청 진행 상황을 추적합니다. Petio는 사용자가 서버 내부 및 외부에서 미디어를 발견하고, 관련 콘텐츠를 빠르고 쉽게 찾고, 다른 사용자를 위해 의견을 남기기 위해 리뷰할 수 있도록 합니다.

# 기타 프로젝트 및 프로그램 - \*Arr 관련

## 원격 제어

### LunaSea

[LunaSea](https://www.lunasea.app/)는 완전한 기능을 갖춘 오픈 소스 자체 호스팅 컨트롤러입니다! 자체 호스팅 미디어 소프트웨어 간에 원활한 경험을 제공하는 데 중점을 둡니다.

### Radarr & Sonarr Companion - Android 앱

휴대폰으로 쉽게 새로운 영화/TV 프로그램을 시스템에 추가할 수 있습니다. 앱은 [Google Play](https://play.google.com/store/apps/details?id=easy.radarr)에서 사용할 수 있습니다.

### nzb360 - Android 앱

nzb360은 Sonarr, Radarr, Lidarr, 토렌트, usenet 및 기타 서비스를 관리합니다. 앱은 [Google Play](https://play.google.com/store/apps/details?id=com.kevinforeman.nzb360)에서 사용할 수 있습니다. 자세한 정보는 [공식 웹사이트](https://nzb360.com/)를 확인하세요.

## Lidarr

### AMD

[자동 음악 다운로더](https://github.com/RandomNinjaAtk/docker-amd) RandomNinjaAtk/amd는 Lidarr 동반 스크립트로 Lidarr를 위해 음악을 자동으로 다운로드합니다.

### AMVD

[자동 음악 비디오 다운로더](https://github.com/RandomNinjaAtk/docker-amvd) RandomNinjaAtk/amvd는 Lidarr 동반 스크립트로 음악 비디오를 자동으로 다운로드하고 태그를 지정하여 다른 비디오 애플리케이션(plex/kodi/jellyfin/emby)에서 사용할 수 있도록 합니다.

## Radarr

## AMTD

[자동 영화 예고편 다운로더](https://github.com/RandomNinjaAtk/docker-amtd) RandomNinjaAtk/amtd는 Radarr 동반 스크립트로 영화 예고편과 추가 콘텐츠를 자동으로 다운로드하여 다른 비디오 애플리케이션(plex/kodi/jellyfin/emby)에서 사용할 수 있도록 합니다.

## 자막

## Bazarr

[Bazarr](https://github.com/morpheus65535/bazarr)는 Sonarr 및 Radarr와 함께 작동하여 요구 사항에 따라 자막을 관리하고 다운로드합니다.

# 기타 프로젝트 및 프로그램 - 토렌트/다운로드

## Cross-Seed

[Cross-Seed](https://github.com/mmgoodnow/cross-seed)는 기존 토렌트에 근거하여 교차 시드할 수 있는 토렌트를 다운로드하는 데 도움을 주는 앱입니다. 수동 개입을 최소화하기 위해 보수적으로 일치하도록 설계되었습니다. 현재 Jackett 및 Qbittorrent/rTorrent을 지원합니다.

## Toolbarr

[Toolbarr](https://github.com/Notifiarr/toolbarr)는 Starr 애플리케이션의 문제를 해결하기 위한 일련의 유틸리티를 제공합니다. Toolbarr를 사용하면 Starr 앱 및 SQLite3 데이터베이스에 대해 다양한 작업을 수행할 수 있습니다.

## Unpackerr

[Unpackerr](https://github.com/unpackerr/unpackerr)은 다운로드 호스트에서 데몬으로 실행되는 애플리케이션입니다. 완료된 다운로드를 확인하고 \*Arr이 가져올 수 있도록 압축을 해제합니다.

완료된 다운로드를 추출하고 가져온 후에 파일을 삭제하는 옵션은 여러 가지가 있습니다. Captain은 그 중 어느 것도 마음에 들지 않아 직접 작성했습니다. 합리적인 로깅을 갖춘 작은 단일 이진 파일로, 다운로드된 아카이브를 추출하고 가져온 후에 남은 잔해를 청소할 수 있습니다.

## qBit Management

[qBit Management 또는 "qbit_manage"](https://github.com/StuffAnThings/qbit_manage)은 qBittorrent 인스턴스를 관리하는 데 사용되는 프로그램입니다. 다음과 같은 작업을 수행할 수 있습니다:



- 트래커 URL에 기반하여 토렌트에 태그를 추가합니다 (태그가 없는 토렌트에만 태그를 추가합니다).
- 저장 디렉토리에 기반하여 카테고리를 업데이트합니다.
- 등록되지 않은 토렌트를 제거합니다 (데이터 및 토렌트를 삭제합니다. 크로스 시딩 중이지 않은 경우에만 삭제합니다).
- 일시 중지된 상태에서 크로스 시딩 토렌트를 자동으로 추가합니다 (크로스 시딩 스크립트와 함께 사용됩니다).
- 완료된 경우 가장 작은 크기로 정렬된 일시 중지된 토렌트를 다시 확인하고 재개합니다.
- qBittorrent에서 참조되지 않는 루트 디렉토리의 고아 파일을 제거합니다.
- 하드 링크가 없는 토렌트를 태그하고, 최대 비율 및/또는 시딩 시간에 기반하여 이러한 토렌트와 내용을 선택적으로 정리하는 옵션을 제공합니다.

# 다른 프로젝트 및 프로그램

## Filebot

[FileBot](https://www.filebot.net/)은 영화, TV 프로그램 및 애니메이션을 정리하고 이름을 바꾸는 데 사용되는 최고의 도구입니다. 또한 자막과 아트워크를 가져올 수 있습니다. 똑똑하고 간편하게 작동합니다.

## JDupes

[Jdupes](https://github.com/jbruchon/jdupes)는 중복 파일을 식별하고 조치를 취하는 프로그램입니다.

> TRaSH에도 가이드가 있습니다 {.is-info} (https://trash-guides.info/jdupes)

- `jdupes -M -r "/data/tv/" "/data/tv/.torrents/"` <= 이 명령은 중복 파일을 확인하고 결과를 요약해서 출력합니다.

- `jdupes -L -r "/data/tv/" "/data/tv/.torrents/"` <= 이 명령은 중복 파일을 하드 링크로 다시 생성하여 중복 공간을 줄입니다.

## Just A Bunch Of Starr Scripts

- [Just A Bunch Of Starr Scripts](https://github.com/angrycuban13/Just-A-Bunch-Of-Starr-Scripts)
- [Upgradinatorr](https://github.com/angrycuban13/Scripts/blob/main/Upgradinatorr/README.md)는 Radarr/Sonarr 미디어 라이브러리에서 특정 태그가 지정되지 않은 n개의 항목을 수동으로 검색하는 PowerShell 스크립트입니다. n은 이 스크립트가 검색할 항목의 수입니다. 이렇게 하면 인덱서에 과부하를 주지 않고 밴되지 않을 수 있습니다 :)

## Just A Bunch Of Plex Scripts

- [Just A Bunch Of Plex Scripts (JBOPS)](https://github.com/blacktwin/JBOPS)
- [TRaSH Guides JBOPS 4K Transcode Stopping with Tautulli](https://trash-guides.info/Plex/Tips/4k-transcoding/)

## Plex Meta Manager

[Plex Meta Manager (PMM)](https://github.com/meisnate12/Plex-Meta-Manager)는 영화, TV 프로그램 및 컬렉션의 메타데이터 정보를 업데이트하고 컬렉션을 자동으로 작성하는 Python 스크립트입니다.

## Tautulli

[Tautulli](https://tautulli.com/)는 Plex 미디어 서버와 함께 실행할 수 있는 타사 애플리케이션으로, 활동을 모니터링하고 다양한 통계를 추적할 수 있습니다. 가장 중요한 것은 시청한 콘텐츠, 시청한 사용자, 시청한 날짜와 장소, 시청 방법 등의 통계 정보를 제공합니다. "왜 시청했는지"에 대한 정보는 제공되지 않지만, 당신이 '겨울왕국'을 42번 재생한 이유를 의문지을 필요는 없습니다. 모든 통계 정보는 깔끔하고 편리한 인터페이스에서 테이블과 그래프로 제공되어 다른 사람들에게 서버에 대해 자랑할 수 있도록 도와줍니다.

## Tdarr

[Tdarr](https://tdarr.io)는 미디어 라이브러리의 트랜스코드/리뮤크 관리를 자동화하고 파일을 필요한 대로 코덱/스트림/컨테이너 등으로 정확하게 조정하는 닫힌 소스의 자체 호스팅 웹 앱입니다. [Sonarr](/sonarr)/[Radarr](/radarr)와 함께 작동하도록 설계되었으며 모듈화, 병렬화 및 확장성을 목표로 구축되었습니다. 추가하는 각 라이브러리는 자체 트랜스코드 설정, 필터 및 일정을 가지고 있습니다. 필요에 따라 워커를 시작하고 종료할 수 있으며, '일반', '트랜스코드' 및 '건강 점검' 세 가지 유형으로 분할됩니다. 워커 제한은 스케줄러와 수동으로 관리할 수 있습니다.

## tdarr_inform

[tdarr_inform](https://github.com/deathbybandaid/tdarr_inform)는 파일 시스템 이벤트나 빈번한 디스크 스캐닝에 의존하지 않고 Sonarr 및 Radarr에게 새로운/변경된/삭제된 파일에 대한 정보를 전달하기 위한 사용자 정의 스크립트입니다.

## Deleterr

[Deleterr](https://github.com/rfsbraz/deleterr)는 Plex/Sonarr/Radarr에서 사용하지 않는 미디어를 삭제하는 도구입니다. Overseerr/Ombi를 통해 사용자가 쇼를 요청할 수 있지만 사용 가능한 디스크 공간을 수동으로 모니터링하고 싶지 않을 때 제한된 공간을 관리하는 데 도움이 됩니다. 정의한 기준을 충족하는 미디어만 삭제하도록 구성할 수 있습니다.

## Twitter Connect

<https://apps.twitter.com/>에서 Twitter 애플리케이션을 생성합니다 (아직 생성하지 않았다면).

필수 필드와 콜백 URL을 입력합니다. 콜백 URL은 공개적으로 사용 가능한 URL(localhost가 아닌)로 설정해야 합니다. 실제로 존재할 필요는 없지만 설정되어야 합니다. <https://sonarr.tv/twitter> 또는 <https://radarr.video>를 사용하면 충분합니다.