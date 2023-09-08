---
title: Radarr 문제 해결
description: Radarr의 문제 해결에 대한 내용입니다. 로그 파일 가져오기, 검색 문제 해결 및 일반적인 문제, 다운로드/가져오기 문제 해결 및 일반적인 문제에 대해 설명합니다.
published: true
date: 2023-08-12T09:40:45.369Z
tags: radarr, 문제 해결
editor: markdown
dateCreated: 2021-08-03T21:05:52.988Z
---

# 목차

- [목차](#목차)
- [도움 요청하기](#도움-요청하기)
- [로그 및 로그 파일](#로그-및-로그-파일)
  - [표준 로그 위치](#표준-로그-위치)
  - [업데이트 로그 위치](#업데이트-로그-위치)
  - [로그 공유하기](#로그-공유하기)
  - [추적/디버그 로그](#추적디버그-로그)
  - [로그 지우기](#로그-지우기)
- [여러 개의 로그 파일](#여러-개의-로그-파일)
- [실패한 업데이트에서 복구하기](#실패한-업데이트에서-복구하기)
  - [문제 확인하기](#문제-확인하기)
    - [데이터베이스 디스크 이미지가 손상되었습니다](#데이터베이스-디스크-이미지가-손상되었습니다)
    - [마이그레이션 문제](#마이그레이션-문제)
    - [UI 마이그레이션 문제](#UI-마이그레이션-문제)
    - [권한 문제](#권한-문제)
  - [문제 해결하기](#문제-해결하기)
    - [마이그레이션 문제](#마이그레이션-문제-1)
    - [권한 문제](#권한-문제-1)
    - [수동 업그레이드](#수동-업그레이드)
- [다운로드 및 가져오기](#다운로드-및-가져오기)
  - [다운로드 클라이언트 테스트](#다운로드-클라이언트-테스트)
  - [다운로드 테스트](#다운로드-테스트)
  - [가져오기 테스트](#가져오기-테스트)
  - [일반적인 문제](#일반적인-문제)
    - [다운로드 클라이언트의 웹 사용자 인터페이스가 비활성화되어 있습니다](#다운로드-클라이언트의-웹-사용자-인터페이스가-비활성화되어-있습니다)
    - [잘못 구성된 SSL 사용](#잘못-구성된-SSL-사용)
    - [Windows에서 공유를 볼 수 없습니다](#Windows에서-공유를-볼-수-없습니다)
    - [매핑된 네트워크 드라이브는 신뢰할 수 없습니다](#매핑된-네트워크-드라이브는-신뢰할-수-없습니다)
    - [도커와 사용자, 그룹, 소유권, 권한 및 경로](#도커와-사용자-그룹-소유권-권한-및-경로)
    - [원격 경로 매핑](#원격-경로-매핑)
      - [원격 마운트 또는 원격 동기화 (Syncthing)](#원격-마운트-또는-원격-동기화-syncthing)
    - [라이브러리 폴더의 권한](#라이브러리-폴더의-권한)
    - [다운로드 폴더의 권한](#다운로드-폴더의-권한)
    - [다운로드 폴더와 라이브러리 폴더가 다른 폴더가 아닙니다](#다운로드-폴더와-라이브러리-폴더가-다른-폴더가-아닙니다)
    - [잘못된 카테고리](#잘못된-카테고리)
    - [압축된 토렌트](#압축된-토렌트)
    - [반복 다운로드](#반복-다운로드)
    - [Usenet 다운로드가 가져오기를 놓칩니다](#Usenet-다운로드가-가져오기를-놓칩니다)
    - [다운로드 클라이언트 항목 지우기](#다운로드-클라이언트-항목-지우기)
    - [다운로드를 라이브러리 항목에 매칭할 수 없습니다](#다운로드를-라이브러리-항목에-매칭할-수-없습니다)
    - [연결 시간 초과](#연결-시간-초과)
  - [목록에 없는 문제](#목록에-없는-문제)
- [검색, 인덱서 및 트래커](#검색-인덱서-및-트래커)
  - [로그 레벨을 추적으로 변경](#로그-레벨을-추적으로-변경)
  - [인덱서 또는 트래커 테스트](#인덱서-또는-트래커-테스트)
  - [검색 테스트](#검색-테스트)
  - [일반적인 문제](#일반적인-문제-1)
    - [트래커에 RawSearch Caps가 필요합니다](#트래커에-RawSearch-Caps가-필요합니다)
    - [미디어가 모니터링되지 않습니다](#미디어가-모니터링되지-않습니다)
    - [잘못된 카테고리](#잘못된-카테고리-1)
    - [쿼리 성공 - 결과가 반환되지 않았습니다](#쿼리-성공---결과가-반환되지-않았습니다)
    - [잘못된 결과](#잘못된-결과)
    - [결과가 누락되었습니다](#결과가-누락되었습니다)
    - [인증서 유효성 검사](#인증서-유효성-검사)
    - [요청 속도 제한 초과](#요청-속도-제한-초과)
    - [IP 차단](#IP-차단)
    - [연도가 일치하지 않습니다](#연도가-일치하지-않습니다)
    - [연도가 누락되었습니다](#연도가-누락되었습니다)
    - [Jackett의 /all 엔드포인트 사용](#Jackett의-all-엔드포인트-사용)
    - [NZBHydra2를 단일 항목으로 사용](#NZBHydra2를-단일-항목으로-사용)
    - [목록에 없는 문제](#목록에-없는-문제-1)
  - [오류](#오류)
    - [기본 연결이 닫혔습니다: 전송 중 예기치 않은 오류가 발생했습니다](#기본-연결이-닫혔습니다-전송-중-예기치-않은-오류가-발생했습니다)
    - [요청 시간이 초과되었습니다](#요청-시간이-초과되었습니다)
    - [목록에 없는 문제](#목록에-없는-문제-2)

# 도움 요청하기

도움이 필요하신가요? 괜찮습니다. 때로는 모두 도움이 필요합니다. 다음 채팅을 통해 실시간 도움을 받을 수 있습니다.

- [<i class="fab fa-discord"></i>&emsp;Discord *Radarr 공식 Discord*](https://radarr.video/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Radarr 공식 서브레딧*](https://reddit.com/r/radarr)
{.links-list}

하지만 질문을 하기 전에 도움을 요청하는 방법을 최대한 잘 준비해야 합니다. 문제를 명확히 설명하고 OS/배포판, .NET 버전, Radarr 버전, 다운로드 클라이언트 및 해당 버전과 같은 설정과 함께 시스템 구성에 대해 간단히 설명해야 합니다. **[Docker](https://www.docker.com/)를 사용하는 경우 [Docker 가이드](/docker-guide)를 먼저 따르십시오. 이는 일반적이고 빈번한 경로/권한 문제를 해결해 줄 것입니다. 그렇지 않으면 [docker compose](/docker-guide#docker-compose)를 준비해 주세요. [Docker Compose 생성 방법](https://trash-guides.info/compose)** 이미 시도해 본 내용과 살펴본 내용에 대해 알려주세요. 문제를 재현하고 로깅을 추적 수준으로 설정한 다음 문제를 재현하고 관련 컨텍스트를 Pastebin에 업로드하고 해당 링크를 게시에 포함시키세요. 문제를 강조하기 위해 스크린샷도 첨부할 수 있습니다.

우리가 알면 도움을 드리기가 더 쉽습니다.

# 로그 및 로그 파일

일반적인 문제 해결 문제도 검토하는 것이 좋습니다:
- [다운로드 및 가져오기 일반적인 문제](#일반적인-문제)
- [인덱서 및 트래커 검색 일반적인 문제](#일반적인-문제-1)
{.links-list}

디버그 로그를 요청받으면 로그에는 `debug`가 포함되고 추적 로그를 요청받으면 로그에는 `trace`가 포함됩니다. 제공하는 로그에 둘 다 포함되어 있지 않은 경우 요청받은 로그가 아닙니다.

- 요청되지 않은 경우 전체 로그 파일을 공유하지 마세요.
- 요청되지 않은 경우 Discord에 로그를 직접 업로드하거나 텍스트 벽으로 붙여넣지 마세요.
- 로그를 첨부 파일, zip 아카이브 또는 기타 텍스트 이외의 형식으로 공유하지 마세요.

유용한 로그를 제공하기 위해 다음을 수행하세요:

> 스팸 같은 작업(예: RSS 새로 고침)이 실행되고 있지 않은지 확인하세요.
{.is-warning}

1. [추적으로 로깅 설정하기 (설정 => 일반 => 로그 레벨 또는 구성 파일 편집)](#추적디버그-로그)
2. [로그 지우기 (시스템 => 로그 => 로그 지우기 또는 로그 폴더의 모든 로그 삭제)](#로그-지우기)
3. 문제 재현하기 (문제가 발생하는 작업을 다시 수행하세요)
4. UI 또는 로그 파일에서 문제와 관련된 컨텍스트를 찾아보세요. ([표준 로그 위치](#표준-로그-위치) 참조)
5. 문제가 발생하기 전의 큰 부분, 문제 자체 및 문제가 발생한 후의 큰 부분을 복사하세요.
6. [Gist](https://gist.github.com/), [0bin (**색상화 비활성화 필수**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu의 Pastebin](https://pastebin.ubuntu.com/) 또는 유사한 사이트(아래에서 제외된 사이트는 제외)를 사용하여 위에서 복사한 로그를 공유하세요.

**주의 사항:**
- **[pastebin.com](https://pastebin.com)은 로그를 차단하는 필터가 있으므로 사용하지 마세요.
- [pastebin.pl](https://pastebin.pl)은 사이트에 자주 접속할 수 없으므로 사용하지 마세요.
- [JustPasteIt](https://justpaste.it/)은 로그 검토를 지원하지 않으므로 사용하지 마세요.
- 로그를 파일로 업로드하지 마세요.
- 로그를 Google Drive, Dropbox 또는 기타 위에서 언급하지 않은 사이트를 통해 업로드하고 공유하지 마세요.
- 로그를 아카이브(zip, tar (tarball), 7zip 등)하지 마세요.
- 콘솔 출력, 도커 컨테이너 출력 또는 응용 프로그램 로그 이외의 내용을 공유하지 마세요.

**중요한 참고 사항:**
- [0bin](https://0bin.net/)을 사용하는 경우 색상화를 비활성화하고 읽은 후에 삭제하지 않도록 주의하세요.

- 또는 특정 항목을 찾으려면 N++을 사용할 수 있습니다. Notepad++의 "파일에서 찾기" 기능을 사용하여 필요한 이전 로그 파일을 검색할 수 있습니다.
- **Unix 전용:** 특정 항목을 찾으려면 grep을 사용할 수 있습니다. 예를 들어 "Shooter"라는 영화/TV 프로그램/도서/노래/인덱서에 대한 정보를 찾으려면 다음 명령을 실행할 수 있습니다. `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` [Appdata 디렉토리](/radarr/appdata-directory)가 홈 폴더에 있는 경우 다음과 같이 실행합니다. `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * 각 플래그의 기능은 다음과 같습니다.
    * -i: 대소문자를 구분하지 않음
    * -n: 줄 번호 표시
    * -r: 경로 내의 모든 파일을 재귀적으로 확인
    * -C: 찾은 줄의 이전 및 이후 줄 수 제공
    * -e: 검색할 패턴

```

## 표준 로그 위치

로그 파일은 Radarr의 [Appdata 디렉토리](/radarr/appdata-directory)의 logs/ 폴더에 있습니다. 또한 UI에서 System => Logs => Files에서 로그 파일에 액세스할 수 있습니다.

> 참고: UI의 로그("이벤트") 테이블은 로그 파일과 동일하지 않으며 유용하지 않습니다. 로그를 요청받은 경우 로그 파일에서 복사/붙여넣기를 해주세요.
{.is-info}

## 업데이트 로그 위치

업데이트 로그 파일은 Radarr의 [Appdata 디렉토리](/radarr/appdata-directory)의 UpdateLogs/ 폴더에 있습니다.

## 로그 공유하기

로그는 포럼이나 Reddit 게시물에서 길고 읽기 어려울 수 있으며 Discord에서 스팸이 될 수 있으므로 [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) 또는 유사한 pastebin 사이트를 사용하세요. 일반적으로 전체 파일이 필요하지 않으며, 문제/오류 전후의 적절한 컨텍스트만 필요합니다. 스팸 같은 작업(예: RSS 동기화 또는 라이브러리 새로 고침)이 완료될 때까지 기다리지 않도록 주의하세요.

## 추적/디버그 로그

로그 레벨은 설정 => 일반 => 로깅에서 변경할 수 있습니다. 변경 사항은 로그 파일에만 영향을 미치며 로깅 데이터베이스에는 영향을 미치지 않습니다. 최신 디버그/추적 로그 파일은 각각 `radarr.debug.txt` 및 `radarr.trace.txt`로 이름이 지정됩니다.

로그 레벨을 설정하는 UI에 액세스할 수 없는 경우 AppData 디렉토리의 config.xml을 편집하여 LogLevel 값을 Info 대신 Debug 또는 Trace로 설정할 수 있습니다.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## 로그 지우기

로그 파일과 로그 데이터베이스를 UI에서 직접 지울 수 있습니다. System => Logs => Files 및 System => Logs => Delete (휴지통 아이콘)을 참조하세요.

# 여러 개의 로그 파일

Radarr는 각각 1MB로 제한된 롤링 로그 파일을 사용합니다. 현재 로그 파일은 항상 `radarr.txt`이며 다른 파일은 `radarr.0.txt`가 다음으로 최신 파일입니다(숫자가 높을수록 오래된 파일입니다). 이 로그 파일에는 `fatal`, `error`, `warn`, `info` 항목이 포함됩니다.

디버그 로그 레벨이 활성화되어 있는 경우 추가적인 `radarr.debug.txt` 롤링 로그 파일이 있을 수 있습니다. 이 로그 파일에는 `fatal`, `error`, `warn`, `info`, `debug` 항목이 포함됩니다. 일반적으로 40시간 동안의 로그를 포함합니다.

추적 로그 레벨이 활성화되어 있는 경우 추가적인 `radarr.trace.txt` 롤링 로그 파일이 있을 수 있습니다. 이 로그 파일에는 `fatal`, `error`, `warn`, `info`, `debug`, `trace` 항목이 포함됩니다. 추적 로그는 대부분의 경우 최대 몇 시간 동안만 유지됩니다.

# 실패한 업데이트에서 복구하기

- 업그레이드 시 문제가 발생하지 않도록 최선을 다하지만, 발생하는 경우 설치를 복구하는 단계를 안내합니다.
- 이 섹션은 일반적인 업데이트 후 문제도 다룹니다.

## 문제 확인하기

- 업데이트 후 애플리케이션이 시작되지 않는 경우 가장 먼저 [업데이트 로그](#업데이트-로그-위치)를 검토하고 업데이트가 성공적으로 완료되었는지 확인하세요. 문제가 없는 경우 일반적인 애플리케이션 로그 파일을 살펴보기 전에 시작을 다시 시도하기 전에 [로그](/radarr/settings#logging) 및 [로그 파일](/radarr/system#log-files)을 사용하여 로그 파일을 찾고 로그 레벨을 높이세요.
- 가장 자주 발생하는 문제는 앱이 설치된 시스템이 업그레이드 중에 `/tmp` 디렉토리를 수정하고 중요한 \*Arr 파일을 삭제하여 업그레이드와 롤백 모두 실패하는 경우입니다. 이 경우 기존 손상된 설치 위에 재설치하면 됩니다.

### 데이터베이스 디스크 이미지가 손상되었습니다

- [FAQ 항목](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)을 참조하세요.

### 마이그레이션 문제

- 마이그레이션 오류는 동일하지 않을 수 있지만, 다음은 예시입니다:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### UI 마이그레이션 문제

- [지원되지 않는 버전/브랜치](/radarr/faq#can-i-switch-between-branches) 간 전환하는 경우 다음과 같은 마이그레이션 문제가 발생할 수 있습니다. 이 경우 [이전 버전 또는 더 높은 버전으로 돌아가세요](/radarr/faq#how-do-i-update-radarr) 또는 현재 버전에 대한 [백업을 복원하세요](/radarr/faq#how-do-i-backuprestore-radarr).

![radarr-migration-error-ui.png](/assets/radarr/radarr-migration-error-ui.png)

### 권한 문제

- 권한 문제는 애플리케이션이 관련 임시 폴더 및/또는 앱 바이너리 폴더에 액세스할 수 없기 때문에 발생합니다. 애플리케이션이 실행되는 사용자/그룹이 적절한 액세스 권한을 갖도록 권한을 수정하세요.

- Synology 사용자는 Synology 버그 `Access to the path '/proc/{some number}/maps is denied`를 마주칠 수 있습니다.

- 특정 NAS에서 `/tmp` 공간이 부족한 문제가 발생할 수도 있습니다. 앱을 위해 다른 `/tmp` 경로를 지정해야 합니다. 이에 대한 도움은 SynoCommunity나 다른 Synology 지원 채널을 참조하십시오.

## 문제 해결

### 마이그레이션 문제

마이그레이션 문제가 발생한 경우 즉시 해결할 수 있는 방법은 많지 않습니다. 만약 이 문제가 특정한 경우이거나 (또는 아직 게시물이 없는 경우) [our subreddit](https://reddit.com/r/radarr)에 게시물을 작성하거나 [discord](https://radarr.video/discord)에 참여하십시오. 동일한 문제를 겪는 다른 사용자가 있다면, 문제가 해결되도록 노력하고 있음을 확신할 수 있습니다.

> `nightly`에서 안정 버전으로 데이터베이스를 사용하려고 시도하지 않았는지 확인하십시오. 브랜치를 자주 변경하는 것은 권장되지 않습니다.{.is-info}

### 권한 문제

- `/tmp` 및 애플리케이션의 설치 디렉토리 양쪽에 대한 액세스(읽기 및 쓰기)를 애플리케이션이 실행되는 사용자/그룹이 보장하도록 권한을 수정하십시오.

- `/proc/###/maps`에 문제가 있는 Synology 사용자는 Sonarr 또는 다른 \*Arr 애플리케이션을 중지하고 업데이트해야 합니다. 이는 SynoCommunity 패키지의 문제입니다.

### 수동 업그레이드

웹사이트에서 최신 릴리스를 다운로드하십시오.

업데이트(.exe)를 설치하거나 기존 설치에 내용을 추출(.zip)하고 Radarr을 일반적으로 실행하십시오.

# 다운로드 및 가져오기

대부분의 사용자가 문제를 겪는 곳은 다운로드 및 가져오기입니다. 높은 수준에서 말하면, Radarr은 다운로드 클라이언트와 통신하고 다운로드한 파일에 액세스해야 합니다. 지원되는 다양한 다운로드 클라이언트와 다양한 설정이 있기 때문에, 몇 가지 일반적인 설정이 있지만 하나의 올바른 설정은 없으며 모든 사용자의 설정은 조금씩 다를 수 있습니다.

> **첫 번째 단계는 로깅을 Trace 수준으로 설정하는 것입니다. 자세한 내용은 [Logging and Log Files](#logging-and-log-files)를 참조하십시오. 그런 다음 문제를 재현하고 해당 시간대의 Trace 수준 로그를 사용하여 문제를 조사합니다.** 누군가가 도와주고 있다면, 문제가 발생하기 전/후의 컨텍스트를 [pastebin](https://0bin.net), [Gist](https://gist.com) 또는 유사한 사이트에 올려서 보여줍니다. 전체 파일이 아니어도 되며, 오류만 있는 것이 아니어야 합니다. 또한 로그 파일에 로그를 스팸하는 작업이 실행되지 않는 상태에서 문제를 재현해야 합니다.
{.is-danger}

도움을 요청할 때는 [도움 요청하기](#asking-for-help)를 읽어서 필요한 세부 정보를 제공할 수 있도록 해야 합니다.

## 다운로드 클라이언트 테스트

다운로드 클라이언트가 실행 중인지 확인하십시오. 먼저 다운로드 클라이언트를 테스트하고 작동하지 않으면 Trace 수준 로그에서 자세한 정보를 확인할 수 있습니다. 브라우저에 입력할 수 있는 URL을 찾아서 작동하는지 확인하십시오. 연결 문제일 수 있으며, 잘못된 IP, 호스트 이름, 포트 또는 방화벽이 액세스를 차단할 수도 있습니다. 사용자 이름, 비밀번호 또는 API 키를 잘못 입력한 인증 문제와 같이 명확한 문제일 수도 있습니다. 일부 시드박스는 다운로드 클라이언트의 실제 포트 대신 https, 포트 443 및 URL 기본값(고급 옵션)을 사용해야 할 수도 있습니다.

## 다운로드 테스트

이제 다운로드를 시도해 보겠습니다. 영화를 선택하고 수동 검색을 수행합니다. 이 파일 중 하나를 선택하고 다운로드를 시도해 보십시오. 다운로드 클라이언트로 전송되는지 확인하십시오. 올바른 카테고리에 있는지 확인하십시오. 활동에 표시되는지 확인하십시오. **완료된 다운로드 확인** 작업(모니터링된 다운로드 새로 고침 및 처리 작업) 중에 Trace 수준 로그에 표시되는지 확인하십시오. 해당 작업은 대략 매 분마다 실행됩니다. 해당 작업 중에 파일이 올바르게 구문 분석되는지 확인하십시오. 대기 중인 다운로드에 합리적인 이름이 있는지 확인하십시오. 일부 인덱서/트래커에서는 ID로 검색하기 때문에 인식할 수 없는 이름으로 대기열에 추가될 수 있습니다.

## 가져오기 테스트

가져오기 문제는 대부분 활동에 오류가 표시되는 오렌지 아이콘으로 나타납니다. 활동에 표시되지 않는 경우, 이 문제에 우선적으로 집중해야 합니다. 대부분의 가져오기 오류는 *권한* 문제입니다. 가져오기 폴더에서 읽기 및 쓰기가 가능하도록 권한을 설정해야 합니다. 때로는 라이브러리 폴더의 권한도 문제가 될 수 있으므로 둘 다 확인해야 합니다.

경로 문제도 가능하지만, 일반적인 설정에서는 그렇게 흔하지 않습니다. 경로 문제를 이해하는 핵심은 다운로드 클라이언트로부터 다운로드 경로를 가져온다는 것입니다. 이는 다운로드 클라이언트가 다른 시스템(심지어 다른 운영 체제일 수도 있음)에서 실행되는 경우에 문제가 될 수 있습니다. Docker 설정에서도 발생할 수 있으며, 볼륨이 잘 구성되지 않은 경우입니다. 원격 경로 매핑은 시스템에 제어권이 없는 시드박스 설정과 같은 경우에 좋은 해결책입니다. Docker 설정에서는 경로를 수정하는 것이 더 좋은 옵션입니다.

## 일반적인 문제

일부 일반적인 문제는 다음과 같습니다.

### 다운로드 클라이언트의 웹 사용자 인터페이스가 비활성화되어 있음

Radarr은 다운로드 클라이언트와 API를 통해 통신하고 클라이언트의 웹 사용자 인터페이스를 통해 액세스합니다. 클라이언트의 웹 사용자 인터페이스가 활성화되어 있는지 확인하고 사용 중인 다른 클라이언트 포트나 시스템에서 사용 중인 포트와 충돌하지 않는지 확인해야 합니다.

### 잘못된 SSL 구성

로컬 네트워크에서 인스턴스와 다운로드 클라이언트를 모두 사용하는 경우 SSL 암호화가 켜져 있지 않도록 확인하십시오. 자세한 내용은 [the SSL FAQ entry](/radarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues)를 참조하십시오.

### Windows에서 공유가 보이지 않음

Windows 서비스의 기본 사용자는 일반적으로 공유에 액세스할 수 없는 `LocalService`입니다. 서비스를 편집하고 사용자로 실행하도록 설정하십시오. 자세한 내용은 FAQ 항목 [why can’t see my files on a remote server](/radarr/faq#why-cant-i-see-my-files-on-a-remote-server)를 참조하십시오.

### 매핑된 네트워크 드라이브가 신뢰할 수 없음

`X:\`와 같은 매핑된 네트워크 드라이브는 편리하지만, UNC 경로인 `\\server\share`보다 신뢰성이 떨어집니다. 또한 로그인하기 전에 사용할 수 없습니다. 필요한 경우 설정하고 다운로드 클라이언트를 사용하여 UNC 경로를 사용하도록 설정하십시오. 라이브러리가 공유에 있는 경우 루트 폴더가 UNC 경로를 사용하도록 설정해야 합니다. 다운로드 클라이언트가 공유로 전송하는 경우, 다운로드 경로를 다운로드 클라이언트에서 가져오기 때문에 UNC 경로를 구성해야 합니다. 매핑된 네트워크 드라이브를 개인적으로 사용하는 것은 괜찮지만, 자동화에는 사용하지 마십시오.

### Docker 및 사용자, 그룹, 소유권, 권한 및 경로

Docker는 잘못 설정하기 쉬운 복잡성을 추가하지만, 여전히 기능이 있는 설정을 얻을 수 있습니다. 이 문서에서는 여기서 다루지 않고 고수준으로 설명하는 [for these automation software and Docker](/docker-guide)라는 위키 문서를 읽으십시오. 이 문서는 특정 Docker 시스템에 특정되지 않고, 대신 사용자의 환경에 구현할 수 있도록 고수준으로 설명합니다.

### 원격 경로 매핑

Radarr을 Docker에서 사용하고 다운로드 클라이언트를 비-Docker에서 사용하는 경우(또는 그 반대로) 또는 프로그램을 다른 서버에 설치한 경우 원격 경로 매핑이 필요할 수 있습니다.

로그에는 다음과 유사한 내용이 표시됩니다.

```none
2022-02-03 14:03:54.3|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /volume3/data/torrents/movies/The.Orville.2022.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

따라서 `/volume3/data`는 Radarr의 컨테이너 내에 존재하지 않거나 액세스할 수 없습니다.

- [Settings => Download Clients => Remote Path Mappings](/radarr/settings#remote-path-mappings)
- 원격 경로 매핑은 다운로드 클라이언트가 다른 서버에 있는 경우나 \*Arr가 Windows에 있고 다운로드 클라이언트가 Linux에 있는 경우와 같이 \*Arr이 해당 폴더에 대한 주소를 알지 못하는 경우에 사용됩니다.
- 일반적으로 원격 경로 매핑은 \*Arr가 Windows에 있고 다운로드 클라이언트가 Linux에 있는 경우나 그 반대인 경우에만 필요합니다. 원격 경로 매핑은 Docker 및 Native 클라이언트를 혼합하거나 원격 서버를 사용하는 경우에도 필요할 수 있습니다.
- 원격 경로 매핑은 DUMB 검색/치환(원격 값 찾기, 지정된 호스트에 대한 로컬 값으로 치환)입니다.
- 잘못된 경로에 대한 오류 메시지에 REPLACED 값이 포함되어 있지 않은 경우, 경로 매핑이 예상대로 작동하지 않습니다. 일반적인 해결책은 매핑을 추가하고 제거하는 것입니다.
- [원격 경로 매핑에 대한 TRaSH의 자습서를 참조하여 추가 정보를 얻을 수 있습니다](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> \*Arr 및 다운로드 클라이언트 모두 Docker 컨테이너인 경우 원격 경로 매핑이 필요한 경우는 드물습니다. [Docker 가이드](/docker-guide)를 검토하거나 [TRaSH의 자습서](https://trash-guides.info/hardlinks)를 따르는 것이 좋습니다.
{.is-info}

#### 원격 마운트 또는 원격 동기화(Syncthing)

- 다운로드하는 동안 계속 동기화되도록 설정해야 합니다. 그리고 로컬 동기화 대상이 가져올 때 하드 링크를 할 수 있도록 해야 합니다. 즉, 동일한 파일 시스템이어야 하며, 동일한 모습이어야 합니다.
  - 미완료 및 완료된 파일이 모두 포함된 일반 폴더에서 동기화합니다.
  - 라이브러리와 로컬 파일 시스템이 동일한 위치에 있도록 동기화합니다. (Docker 및 네트워크 공유는 구성하기 쉽게 만듭니다.)
  - 미완료 및 완료된 파일을 동기화하여 토렌트 클라이언트가 이동할 때 로컬에서 반영되고 모든 파일이 이미 "있는" 상태가 되도록 합니다(아직 다운로드 중인 경우에도). 그런 다음 하드 링크를 사용하려면 가져오기가 완료되기 전에 가져오면 됩니다.
  - 이렇게 하면 다운로드하는 동안 계속 동기화되며, 토렌트 클라이언트가 tv 하위 폴더로 이동하고 동기화가 반영됩니다. 이렇게 하면 다운로드가 대부분 완료된 상태로 선언됩니다. 그리고 아직 완전히 완료되지 않았더라도 하드링크가 가능하면 괜찮습니다.
  - (선택 사항 - 해당되는 경우 및/또는 필요한 경우(예: 원격 유즈넷 클라이언트)) 가져오기/다운로드/업그레이드 시 사용자 정의 스크립트를 구성하여 원격 파일을 제거합니다.
- 원격 동기화 대신 원격 마운트를 사용하는 경우 구성하기가 훨씬 덜 복잡하지만 일반적으로 속도가 느립니다.
  - sshfs 또는 다른 네트워크 파일 시스템 프로토콜을 사용하여 원격 저장소를 마운트합니다.
  - \*Arr이 실행되도록 구성된 사용자 및 그룹이 읽기 또는 쓰기 액세스 권한을 갖도록 설정합니다.
  - 원격 경로 매핑을 구성하여 REMOTE 경로를 찾아서 LOCAL 값으로 대체합니다.

### 라이브러리 폴더의 권한

로그는 다음과 같이 표시됩니다.

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/media/Movie Name (2010). Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

*대상*의 권한과 소유권을 확인하는 것을 잊지 마십시오. 다운로드의 소유권과 권한에 집중하기 쉽고, 일반적으로 권한 관련 문제의 원인이지만, 대상도 가능한 원인입니다. 대상 폴더가 존재하는지 확인하십시오. 대상 *파일*이 이미 존재하거나 삭제되거나 휴지통으로 이동할 수 없는지 확인하십시오. 소유권과 권한이 다운로드한 파일을 복사하거나 하드 링크하거나 이동할 수 있도록 허용하는지 확인하십시오. 실행하는 사용자 또는 그룹은 루트 폴더를 읽고 쓸 수 있어야 합니다.

- Windows 사용자의 경우 서비스로 실행 중인 경우:
  - Windows 서비스는 기본적으로 'Local Service' 계정에서 실행됩니다. 기본적으로 이 계정은 수동으로 권한을 할당하지 않는 한 사용자의 홈 디렉토리에 액세스할 수 없습니다. 이는 홈 디렉토리로 다운로드하는 다운로드 클라이언트를 사용할 때 특히 관련이 있습니다.
  - 'Local Service'는 일반적으로 매우 제한된 권한을 갖습니다. 따라서 사용자가 로그인한 상태로 앱을 시스템 트레이 애플리케이션으로 설치하는 것이 좋습니다. 설치 프로그램에서 이 옵션을 제공합니다. 서비스를 트레이 앱으로 변환하는 방법에 대해서는 FAQ를 참조하십시오.

- Synology 사용자는 [SynoCommunity 패키지의 권한 관리](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)를 참조하십시오.

- Windows가 아닌 경우: NFS 마운트를 사용하는 경우 `nolock`이 활성화되어 있는지 확인하십시오.
- SMB 마운트를 사용하는 경우 `nobrl`이 활성화되어 있는지 확인하십시오.

### 다운로드 폴더의 권한

로그는 다음과 같이 표시됩니다.

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/downloads/The.Movie. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

*소스*의 권한과 소유권을 확인하는 것을 잊지 마십시오. 대상의 소유권과 권한에 집중하기 쉽고, 권한 관련 문제의 가능한 원인이지만, 일반적으로 소스입니다. 소스 폴더가 존재하는지 확인하십시오. 소유권과 권한이 다운로드한 파일을 복사/하드링크하거나 복사+삭제/이동할 수 있도록 허용하는지 확인하십시오. 실행하는 사용자 또는 그룹은 다운로드 폴더를 읽고 쓸 수 있어야 합니다.

- Windows 사용자의 경우 서비스로 실행 중인 경우:
  - Windows 서비스는 기본적으로 'Local Service' 계정에서 실행됩니다. 기본적으로 이 계정은 수동으로 권한을 할당하지 않는 한 사용자의 홈 디렉토리에 액세스할 수 없습니다. 이는 홈 디렉토리로 다운로드하는 다운로드 클라이언트를 사용할 때 특히 관련이 있습니다.
  - 'Local Service'는 일반적으로 매우 제한된 권한을 갖습니다. 따라서 사용자가 로그인한 상태로 앱을 시스템 트레이 애플리케이션으로 설치하는 것이 좋습니다. 설치 프로그램에서 이 옵션을 제공합니다. 서비스를 트레이 앱으로 변환하는 방법에 대해서는 FAQ를 참조하십시오.

- Synology 사용자는 [SynoCommunity 패키지의 권한 관리](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)를 참조하십시오.

- Windows가 아닌 경우: NFS 마운트를 사용하는 경우 `nolock`이 활성화되어 있는지 확인하십시오.
- SMB 마운트를 사용하는 경우 `nobrl`이 활성화되어 있는지 확인하십시오.

### 다운로드 폴더와 라이브러리 폴더가 동일한 폴더가 아님

다운로드 클라이언트는 \*Arr에서 액세스할 수 있는 폴더에 다운로드해야 하며, 루트/라이브러리 폴더와 다른 폴더여야 합니다. 별도의 다운로드 폴더에서 가져온 파일을 라이브러리 폴더로 가져와야 합니다.

루트 폴더로 직접 다운로드해서는 안 됩니다. 또한 루트 폴더를 다운로드 클라이언트의 완료된 폴더나 미완료된 폴더로 사용해서도 안 됩니다.

> 다운로드 폴더와 루트/라이브러리 폴더는 반드시 별도로 설정해야 합니다.
{.is-warning}

### 잘못된 카테고리

Radarr은 자체 다운로드만 처리하도록 카테고리를 설정해야 합니다. 제대로된 카테고리가 없이 추가된 토렌트는 드물지만 추가될 수 있습니다. 수동으로 토렌트를 추가하고 처리하려면 올바른 카테고리를 설정해야 합니다. 다운로드 클라이언트가 카테고리를 설정할 수 있으므로 언제든지 설정할 수 있습니다.는 다운로드를 매 분마다 처리하려고 시도합니다.

### 압축된 토렌트

로그에는 다음과 유사한 오류가 표시됩니다.

```none
No files found are eligible for import
```

토렌트가 `.rar` 파일로 압축되어 있는 경우 추출 설정을 해야 합니다. [Unpackerr](https://github.com/unpackerr/unpackerr)를 추천합니다. 이는 올바른 추출을 수행하여 손상된 부분적인 가져오기를 방지하고 가져온 파일을 가져온 후 정리합니다.

또한 폴더에 유효한 미디어 파일이 없는 경우에도 이 오류가 발생할 수 있습니다.

### 반복 다운로드

반복 다운로드의 원인 중 하나는 사용자 정의 형식과 관련이 있습니다. 릴리스 이름이 사용자 정의 형식과 일치하지만 다운로드 파일은 일치하지 않을 수 있습니다. 이로 인해 업그레이드처럼 보이지만 실제로는 아닌 항목을 반복해서 다운로드하게 됩니다. 사용자 정의 형식을 다운로드 이름 변경 스키마에 포함시켜 이 문제를 해결할 수 있습니다. (사용자 정의 형식을 이름 변경에 포함시키도록 설정하고, 이름 변경 스키마에 사용자 정의 형식을 추가하세요)

이는 다운로드가 실제로 가져오지 않고 대기열에서 누락되어 새로운 다운로드가 계속해서 가져오고 가져오지 않는 경우에도 발생할 수 있습니다. 이에 대한 해결 방법은 다양한 일반적인 문제 및 문제 해결 단계를 참조하십시오.

### 유즈넷 다운로드가 가져오지 못함

Radarr은 SABnzbd 및 NZBGet에서 최근 60개의 다운로드만 확인합니다. 따라서 가져오기 문제가 있는 대량 대기열에서는 다운로드가 음성으로 누락되고 가져오지 않을 수 있습니다. 이를 방지하기 위해 계속해서 나타나는 항목을 확인하기 위해 기록을 유지하는 것이 가장 좋습니다. 완료 및 실패한 다운로드 핸들러에서 제거를 활성화하여 이를 달성할 수 있습니다. NZBGet에서는 항목을 *숨겨진* 기록으로 이동시킵니다. 불행히도 SABnzbd에는 유사한 기능이 없습니다. 거기서 달성할 수 있는 최선은 nzb 백업 폴더를 사용하는 것입니다.

### 다운로드 클라이언트에서 항목 지우기

다운로드 클라이언트는 다운로드를 제거하지 않아야 합니다. 유즈넷 클라이언트는 기록에서 다운로드를 제거하지 않도록 설정해야 합니다. 토렌트 클라이언트는 시딩이 완료되면 토렌트를 제거하지 않고 일시 중지하거나 중지해야 합니다. 이는 Radarr이 가져올 내용을 다운로드 클라이언트와 통신하기 때문에 제거되면 가져올 내용이 없습니다... 파일이 들어있는 폴더가 있더라도요.

SABnzbd의 경우 이는 History Retention 설정으로 처리됩니다.

### 라이브러리 항목과 일치하지 않는 다운로드

다양한 이유로 다운로드를 가져온 후에는 릴리스를 구문 분석할 수 없을 수 있습니다. Activity => Options => Show Unknown(이제 최근 빌드에서 기본적으로 활성화됨)를 사용하면 \*Arr의 다운로드 클라이언트 범주 내에서 무시되지 않거나 이미 가져온 항목이 아닌 모든 항목이 표시됩니다. 이러한 항목은 일반적으로 수동으로 매핑하고 가져와야 합니다.

이유는 다음과 같습니다.
- 영화 이름에는 TMDb에는 `:`가 있지만 `-` 또는 `:`를 대체하는 `-` 또는 ` `가 있는 대체 제목이 없습니다.
- 파일 이름에는 필요한 연도가 누락되어 있습니다.
- AKA 또는 이상한 다중 이름; Radarr은 이러한 것들에 대해 제한된 지원을 제공합니다.
- 파일 이름이 여러 영화와 일치합니다.
- 인덱서의 릴리스 이름 또는 릴리스 ID가 파일 이름과 일치하지 않습니다.

이는 다운로드 클라이언트에 다운로드가 있지만 해당 미디어 항목(영화/에피소드/도서/노래)이 응용 프로그램에 존재하지 않는 경우에도 발생할 수 있습니다.

### 기본 연결이 닫혔습니다: 전송 중 예기치 않은 오류가 발생했습니다

이는 현재 .NET 버전에서 지원되지 않는 SSL 프로토콜을 사용하는 인덱서로 인해 발생합니다. [Radarr => System => Status](/radarr/system#status)에서 현재 .NET 버전을 찾을 수 있습니다.

### 요청 시간이 초과되었습니다

Radarr이 클라이언트로부터 응답을 받지 못하고 있습니다.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

이는 다음과 같은 원인으로 인해 발생할 수도 있습니다.

- 잘못 구성된 VPN 또는 VPN 사용
- 잘못 구성된 프록시 또는 프록시 사용
- 로컬 DNS 문제 - 다른 DNS 공급자로 변경해 보세요.
- 로컬 IPv6 문제 - 일반적으로 IPv6는 활성화되어 있지만 기능이 없습니다.
- Privoxy 사용 및 잘못된 구성

## 목록에 없는 문제

[가이드](/permissions-and-networking)에서 일반적인 권한 및 네트워킹 문제 해결 명령을 검토할 수도 있습니다. 그렇지 않으면 디스코드의 지원 팀과 상의하십시오. 이것이 일반적인 문제일 수 있는 경우 위키에 추가하도록 제안하십시오.

# 검색 인덱서 및 트래커

- [Prowlarr](/prowlarr)을 사용하는 경우, Prowlarr이 받은 모든 쿼리의 [History](/prowlarr/history) 및 해당 쿼리가 사이트로 전송된 방식을 볼 수 있습니다. Prowlarr History => Options에서 `Parameters`가 활성화되어 있는지 확인하세요. (i) 아이콘을 클릭하면 추가 세부 정보를 볼 수 있습니다.

## 로깅 레벨을 Trace로 설정

> **첫 번째 단계는 로깅 레벨을 Trace로 설정하는 것입니다. 로깅 및 로그 파일에 대한 자세한 내용은 [Logging and Log Files](#logging-and-log-files)를 참조하세요. 그런 다음 문제를 재현하고 해당 시간대의 Trace 레벨 로그를 사용하여 문제를 조사합니다.** 누군가가 도와주고 있다면, 이전/이후의 컨텍스트를 [pastebin](https://0bin.net), [Gist](https://gist.com) 또는 유사한 사이트에 올려서 보여줍니다. 전체 파일이어야 할 필요는 없으며 오류만 있으면 안 됩니다. 또한 로그 파일에 로그 파일을 스팸하는 작업이 실행되지 않도록 문제를 재현해야 합니다.
{.is-danger}

## 인덱서 또는 트래커 테스트

인덱서 또는 트래커를 테스트할 때 디버그 또는 추적 로그에서 사용된 URL을 찾을 수 있습니다. 성공적인 테스트 예시는 아래에 나와 있으며, 특정 URL과 매개변수를 사용하여 인덱서에 쿼리를 보내고 응답을 확인할 수 있습니다. 이 URL을 브라우저에서 테스트해 보세요. `apikey=(removed)`를 올바른 apikey(예: `apikey=123`)로 바꿔서 매개변수를 실험해 볼 수도 있습니다. 인덱서에서 오류가 발생하는 경우 연결성 문제가 있는지 확인할 수도 있습니다. 자신의 브라우저에서 테스트한 후 시스템에서 실행 중인 시스템에서 테스트해야 합니다.

## 검색 테스트

앞서 언급한 인덱서/트래커 테스트와 마찬가지로 디버그 또는 추적 수준 로깅에서 검색을 트리거하면 로그 파일에서 사용된 URL을 얻을 수 있습니다. 테스트 중에는 가능한 한 좁은 검색을 사용하는 것이 좋습니다. 수동 검색은 구체적이며 로그를 검사하는 동안 UI에서 결과를 볼 수 있기 때문에 좋습니다.

이 테스트에서는 명백한 오류를 찾고 몇 가지 간단한 테스트를 실행합니다. 검색에 사용된 URL인 `https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(removed)&q=O+Brother+Where+Art+Thou`를 볼 수 있습니다. 이 URL을 해당 인덱서의 올바른 apikey로 `(removed)`를 바꾼 후 브라우저에서 테스트해 보세요. 작동하나요? 예상한 결과가 표시되나요? 이 URL에서 특정 카테고리를 2000으로 설정했으므로 예상한 결과가 표시되지 않는 경우 이것이 하나의 가능한 이유입니다. 영화가 인덱서에서 올바르게 분류되지 않은 경우 수정해야 합니다. 작동하는 쿼리의 출력 예시를 보려면 Manual Search XML Output을 참조하세요.

- Manual Search XML Output

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(removed)&q=O+Brother+Where+Art+Thou" rel="self" type="application/rss+xml"/>
<title>api.nzbgeek.info</title>
<description>NZBgeek API</description>
<link>http://api.nzbgeek.info/</link>
<language>en-gb</language>
<webMaster>info@nzbgeek.info (NZBgeek)</webMaster>
<category/>
<image>
<url>https://api.nzbgeek.info/covers/nzbgeek.png</url>
<title>api.nzbgeek.info</title>
<link>http://api.nzbgeek.info/</link>
<description>NZBgeek</description>
</image>
<newznab:response offset="0" total="17"/>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=e83b7ae75bca71e92367fab29b036731&apikey=(removed)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(removed)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=e83b7ae75bca71e92367fab29b036731</comments>
<pubDate>Sat, 10 Jul 2021 08:33:22 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(removed)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="e83b7ae75bca71e92367fab29b036731"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=c00a92567863801ab1a4901458ae31ba&apikey=(removed)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(removed)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=c00a92567863801ab1a4901458ae31ba</comments>
<pubDate>Sun, 28 Mar 2021 10:50:38 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(removed)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="c00a92567863801ab1a4901458ae31ba"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=75f5be8b4cd573c2359b638350689f73&apikey=(removed)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(removed)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=75f5be8b4cd573c2359b638350689f73</comments>
<pubDate>Sun, 28 Jul 2019 00:46:00 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(removed)" length="936738000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="936738000"/>
<newznab:attr name="guid" value="75f5be8b4cd573c2359b638350689f73"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(removed)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(removed)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=a0fe801d9ba0a703db7d2164e996aa1f</comments>
<pubDate>Mon, 14 Aug 2017 15:34:36 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(removed)" length="9746182000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="9746182000"/>
<newznab:attr name="guid" value="a0fe801d9ba0a703db7d2164e996aa1f"/>
</item>
</channel>
</rss>
```

***이미지 필요***

![searches-indexers-and-trackers1.png](/assets/radarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/radarr/searches-indexers-and-trackers2.png)

- 추적 로그 스니펫

```none
필요한 수동 검색 추적 로그 스니펫
```

- 검색의 전체 추적 로그

```none
필요한 수동 검색의 전체 추적 로그 섹션
```

## 일반적인 문제

일반적인 문제는 다음과 같습니다.

### 트래커에서 RawSearch Caps가 필요함

- Radarr이 `Kikis Delivery Service`를 검색하지만 트래커에는 `Kiki's Delivery Service`의 결과만 있습니다.
- 이는 트래커가 일반적인 표준화된 검색을 지원하지 않기 때문입니다.
- 해결 방법은 트래커의 정의에서 검색 기능을 업데이트하여 `RawSearch`를 [요구하고 지원한다는 것을 나타내는 것입니다](https://github.com/Radarr/Radarr/issues/4502#issuecomment-981143905).
- Jackett은 이 플래그를 지원하지만 기능을 추가하려면 Jackett에서 인덱서별로 기능을 업데이트해야 합니다. Jackett에 기능 요청을 제출하세요.
- Prowlarr은 이 플래그를 지원하지만 기능을 추가하려면 Prowlarr에서 인덱서별로 기능을 업데이트해야 합니다. Prowlarr에 기능 요청을 제출하세요.

### 미디어가 모니터링되지 않음

영화(들)가 모니터링되지 않습니다.

### 잘못된 카테고리



잘못된 카테고리는 인덱서/트래커의 수동 검색 결과에 표시되지 않는 가장 일반적인 원인입니다. 인덱서/트래커는 검색 결과에 카테고리를 표시해야 하므로 누락된 부분을 파악하는 데 도움이 됩니다. Jackett이나 Prowlarr을 사용하는 경우 각 트래커에는 지원되는 특정 카테고리 목록이 있습니다. 카테고리를 사용할 때 올바른 카테고리를 사용하는지 확인하십시오. 많은 사람들은 카테고리 목록을 하나의 브라우저 창에 표시하고 수정하는 동안 편리하게 사용합니다.

### 쿼리 성공 - 결과 없음

인덱서에서 `쿼리 성공했지만 인덱서에서 결과가 반환되지 않았습니다. 이는 인덱서나 인덱서 카테고리 설정과 관련된 문제일 수 있습니다.`와 유사한 메시지를 받습니다.

이는 인덱서가 구성된 카테고리 내에서 결과를 반환하지 않아 발생하는 문제입니다.

### 잘못된 결과

가끔씩 인덱서는 전혀 관련 없는 결과를 반환할 수 있습니다. Radarr은 검색을 제한하기 위해 매개변수를 제공하지만 반환된 결과는 전혀 관련이 없을 수 있습니다. 또는 때로는 몇 가지 잘못된 결과와 대부분 관련된 결과가 반환될 수 있습니다. 첫 번째 경우 일반적으로 인덱서의 문제이며 추적 로그에서 원인을 알 수 있습니다. 해당 인덱서를 비활성화하고 문제를 보고할 수 있습니다. 두 번째 경우 일반적으로 카테고리가 잘못 지정된 릴리스입니다. 이러한 경우 인덱서/트래커에서 신고할 수 있습니다.

### 결과 누락

Radarr에서 표시되지 않는 사이트에서 찾을 수 있는 결과가 있다면 다음과 같은 여러 가능성 중 하나일 수 있습니다:

- [카테고리가 잘못되었습니다 - 위에서 확인하세요](#wrong-categories)
- ID (IMDbId, TMDbId 등) 기반 검색이 수행되고 인덱서가 해당 ID에 올바르게 매핑되지 않은 경우입니다. 이는 인덱서만 해결할 수 있는 문제입니다. 인덱서는 릴리스가 올바른 적용 가능한 ID에 매핑되도록 해야 합니다.
- Radarr이 검색하는 방식과 일치하지 않는 검색을 수행하는 경우입니다. 인덱서에서 검색하는 용어가 Radarr이 쿼리하는 방식과 매우 다를 수 있습니다. 추적 로그에서 Radarr이 어떻게 쿼리하는지 확인할 수 있습니다. 텍스트 기반 쿼리는 일반적으로 `q=words%20and%20things%20here`와 같은 형식으로 표시됩니다. 이 문자열은 HTTP 인코딩되어 있으며 온라인 HTML 디코딩/인코딩 도구를 사용하여 쉽게 디코딩할 수 있습니다.
- [외국 영화 제목이 처리되는 방법 및 Radarr이 언제 검색하는지 FAQ를 참조하세요](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

### 인증서 유효성 검사

대부분의 인덱서/트래커에는 https를 통해 연결해야 하므로 시스템에서 정상적으로 작동해야 합니다. 즉, 시간대와 시간이 올바르게 설정되어 있어야 합니다. 또한 시스템 인증서가 최신 상태여야 합니다.

### 요청 속도 제한

VPN이나 프록시를 통해 실행하는 경우, 다른 사람들과 함께 서비스를 사용하려는 수십, 수백 또는 수천 명과 경쟁할 수 있습니다. , theXEM 및/또는 인덱서 및 트래커와 같은 서비스를 사용하려는 경우 속도 제한 및 DDOS 보호가 IP 주소별로 자주 적용됩니다. VPN/프록시 출구 지점은 *하나의* IP 주소입니다. 중국, 호주 또는 남아프리카와 같은 억압적인 국가가 아닌 경우 VPN/프록시를 사용할 필요가 없습니다.

Rarbg는 API 내에서 일부 요청 속도 제한을 가지고 있으며 결과가 없이 응답하는 것으로 나타납니다.

### IP 차단

비슷하게, Nyaa와 같은 특정 인덱서는 IP 주소를 완전히 차단할 수 있습니다. 이는 일반적으로 반영구적이며 해결 방법은 ISP 또는 VPN 공급자로부터 새 IP를 받는 것입니다.

### 연도가 일치하지 않음

- [이 FAQ 항목을 참조하세요](/radarr/faq#how-does-radarr-determine-the-year-of-a-movie)
  - Radarr은 TMDb에서 메타데이터를 가져옵니다.
  - Radarr은 가장 오래된 **극장 개봉일** 및 가장 오래된 **프리미어** 날짜의 연도를 사용하여 일치시킵니다.
- 일부 경우에는 영화가 변경되거나 이동되어 릴리스 그룹에서 사용하는 연도가 가장 오래된 프리미어 날짜 연도나 가장 오래된 극장 개봉일 연도와 일치하지 않을 수 있습니다. 이러한 경우 수동으로 가져와서 가져와야 합니다.

### 연도가 누락됨

릴리스 이름에 연도가 포함되지 않은 경우 Radarr은 해당 릴리스를 가져오지 않습니다. 이는 잘못된 릴리스이며 수동으로만 가져올 수 있습니다. 영화가 예상대로 가져와지지 않는 이유를 파악하려고 할 때 이러한 사항을 간과하는 경우가 많습니다.

### Jackett의 /all 엔드포인트 사용

Jackett의 `/all` 엔드포인트는 편리하지만 그것만의 이점이 있습니다. 그 외의 모든 것은 잠재적인 문제입니다. 따라서 각 트래커를 개별적으로 추가해야 합니다. 또는 Jackett 및 NZBHydra2 대체제인 [Prowlarr](/prowlarr)를 확인할 수도 있습니다.

[Jackett 자체도 /all을 피하고 사용하지 말아야 한다고 말합니다.](https://github.com/Jackett/Jackett#aggregate-indexers)

all 엔드포인트 사용의 이점은 없으며(관리 오버헤드만 감소됨), 다음과 같은 단점이 있습니다:

- 인덱서별 설정(카테고리, 검색 모드 등)을 제어할 수 없습니다.
- 검색 모드(IMDB, 쿼리 등)를 혼합하면 품질이 낮은 결과가 발생할 수 있습니다.
- 인덱서별 카테고리(100000 이상)를 사용할 수 없습니다.
- 느린 인덱서는 전체 결과 속도를 늦출 수 있습니다.
- 총 결과는 1000개로 제한됩니다.

각 인덱서를 개별적으로 추가하면 인덱서별로 카테고리를 세밀하게 조정할 수 있으며, 잘못된 카테고리를 사용하면 일부 트래커에서 오류가 발생할 수 있는 `/all` 엔드포인트와는 다른 문제가 발생할 수 있습니다. 에서는 페이지네이션을 지원하는 경우 각 인덱서가 1000개의 결과로 제한되며, 페이지네이션을 지원하지 않는 경우 100개로 제한됩니다. 이는 Jackett에 더 많은 트래커를 추가할수록 결과가 잘려나갈 가능성이 더 커진다는 것을 의미합니다. 마지막으로 `/all`에서 *하나의* 트래커가 오류를 반환하면 해당 트래커가 비활성화되어 결과를 얻을 수 없게 됩니다.

### NZBHydra2를 단일 항목으로 사용

NZBHydra2를 단일 인덱서 항목으로 사용하는 경우 (즉, NZBHydra2에 많은 인덱서가 있는 경우 Radarr에는 1개의 NZBHydra2 항목이 있고 NZBHydra2에는 많은 인덱서가 있는 경우) Jackett의 `/all` 엔드포인트와 동일한 문제가 발생합니다.

### 나열되지 않은 문제

일반적인 권한 및 네트워킹 문제 해결 명령에 대해 [가이드](/permissions-and-networking)를 참조할 수도 있습니다. 그렇지 않으면 디스코드의 지원 팀과 상의하십시오. 이것이 일반적인 문제일 수 있는 경우 위키에 추가하도록 제안하십시오.

## 오류

인덱서를 추가할 때 볼 수 있는 일반적인 오류 중 일부입니다.

### 기본 연결이 닫혔습니다: 전송 중 예기치 않은 오류가 발생했습니다

이는 인덱서가 현재 [Radarr => 시스템 => 상태](/radarr/system#status)에서 찾은 .NET 버전에서 지원되지 않는 SSL 프로토콜을 사용하는 경우입니다.

### 요청 시간이 초과되었습니다

Radarr이 인덱서로부터 응답을 받지 못하고 있습니다.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

이는 다음과 같은 경우에도 발생할 수 있습니다:

- 잘못 구성된 VPN 또는 VPN 사용
- 잘못 구성된 프록시 또는 프록시 사용
- 로컬 DNS 문제 - 다른 DNS 공급자로 변경해 보세요.
- 로컬 IPv6 문제 - 일반적으로 IPv6는 활성화되어 있지만 기능하지 않습니다.
- Privoxy 사용 및 잘못 구성

### 나열되지 않은 문제

일반적인 권한 및 네트워킹 문제 해결 명령에 대해 [가이드](/permissions-and-networking)를 참조할 수도 있습니다. 그렇지 않으면 디스코드의 지원 팀과 상의하십시오. 이것이 일반적인 문제일 수 있는 경우 위키에 추가하도록 제안하십시오.