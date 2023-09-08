---
title: Sonarr 문제 해결
description: 
published: true
date: 2023-07-24T19:54:54.368Z
tags: sonarr, 문제 해결
editor: markdown
dateCreated: 2021-06-20T19:13:01.108Z
---

# 목차

- [목차](#목차)
- [도움 요청하기](#도움-요청하기)
- [로그 및 로그 파일](#로그-및-로그-파일)
  - [표준 로그 위치](#표준-로그-위치)
  - [업데이트 로그 위치](#업데이트-로그-위치)
  - [로그 공유](#로그-공유)
  - [추적/디버그 로그](#추적디버그-로그)
  - [로그 지우기](#로그-지우기)
- [여러 개의 로그 파일](#여러-개의-로그-파일)
- [실패한 업데이트에서 복구하기](#실패한-업데이트에서-복구하기)
  - [문제 확인하기](#문제-확인하기)
    - [마이그레이션 문제](#마이그레이션-문제)
    - [권한 문제](#권한-문제)
  - [문제 해결하기](#문제-해결하기)
    - [권한 문제](#권한-문제)
    - [수동 업그레이드](#수동-업그레이드)
- [다운로드 및 가져오기](#다운로드-및-가져오기)
  - [다운로드 클라이언트 테스트](#다운로드-클라이언트-테스트)
  - [다운로드 테스트](#다운로드-테스트)
  - [가져오기 테스트](#가져오기-테스트)
  - [일반적인 문제](#일반적인-문제)
    - [릴리스에서 예상한 하나 이상의 에피소드가 가져오지 않거나 누락됨](#릴리스에서-예상한-하나-이상의-에피소드가-가져오지-않거나-누락됨)
    - [Sonarr v2 사용](#sonarr-v2-사용)
    - [다운로드 클라이언트의 웹 UI가 활성화되지 않음](#다운로드-클라이언트의-웹-ui가-활성화되지-않음)
    - [잘못 구성된 SSL 사용](#잘못-구성된-ssl-사용)
    - [Windows에서 공유 보이지 않음](#windows에서-공유-보이지-않음)
    - [매핑된 네트워크 드라이브가 신뢰할 수 없음](#매핑된-네트워크-드라이브가-신뢰할-수-없음)
    - [도커와 사용자, 그룹, 소유권, 권한 및 경로](#도커와-사용자-그룹-소유권-권한-및-경로)
    - [원격 경로 매핑](#원격-경로-매핑)
      - [원격 마운트 또는 원격 동기화 (Syncthing)](#원격-마운트-또는-원격-동기화-syncthing)
    - [라이브러리 폴더의 권한](#라이브러리-폴더의-권한)
    - [다운로드 폴더의 권한](#다운로드-폴더의-권한)
    - [다운로드 폴더와 라이브러리 폴더가 다른 폴더가 아님](#다운로드-폴더와-라이브러리-폴더가-다른-폴더가-아님)
    - [잘못된 카테고리](#잘못된-카테고리)
    - [압축된 토렌트](#압축된-토렌트)
    - [반복 다운로드](#반복-다운로드)
    - [유즈넷 다운로드가 가져오지 않음](#유즈넷-다운로드가-가져오지-않음)
    - [다운로드 클라이언트 항목 지우기](#다운로드-클라이언트-항목-지우기)
    - [다운로드를 라이브러리 항목에 매칭할 수 없음](#다운로드를-라이브러리-항목에-매칭할-수-없음)
      - [시리즈 ID로 시리즈가 매칭되었지만, 시리즈가 그랩 히스토리에 의해 매칭되었습니다. 자동 가져오기가 불가능합니다](#시리즈-id로-시리즈가-매칭되었지만-시리즈가-그랩-히스토리에-의해-매칭되었습니다-자동-가져오기가-불가능합니다)
    - [에피소드 이름이 TBA입니다](#에피소드-이름이-tba입니다)
    - [연결 시간 초과](#연결-시간-초과)
  - [목록에 없는 문제](#목록에-없는-문제)
- [검색 인덱서 및 트래커](#검색-인덱서-및-트래커)
  - [추적 로그를 켜기](#추적-로그를-켜기)
  - [인덱서 또는 트래커 테스트](#인덱서-또는-트래커-테스트)
  - [검색 테스트](#검색-테스트)
  - [일반적인 문제](#일반적인-문제-1)
    - [인덱서가 검색되지 않음](#인덱서가-검색되지-않음)
    - [잘못된 이름의 릴리스](#잘못된-이름의-릴리스)
    - [트래커에 RawSearch Caps가 필요함](#트래커에-rawsearch-caps가-필요함)
    - [시리즈에 별칭이 필요함](#시리즈에-별칭이-필요함)
    - [시리즈에 XEM 매핑이 필요함](#시리즈에-xem-매핑이-필요함)
    - [잘못된 시리즈 유형](#잘못된-시리즈-유형)
      - [일일](#일일)
      - [표준](#표준)
      - [애니메이션](#애니메이션)
    - [미디어가 모니터링되지 않음](#미디어가-모니터링되지-않음)
    - [쿼리 성공 - 결과가 반환되지 않음](#쿼리-성공-결과가-반환되지-않음)
    - [잘못된 카테고리](#잘못된-카테고리-1)
    - [잘못된 결과](#잘못된-결과)
    - [결과가 누락됨](#결과가-누락됨)
    - [인증서 유효성 검사](#인증서-유효성-검사)
    - [속도 제한에 도달](#속도-제한에-도달)
    - [IP 차단](#ip-차단)
    - [Jackett의 /all 엔드포인트 사용](#jackett의-all-엔드포인트-사용)
    - [NZBHydra2를 단일 항목으로 사용](#nzbhydra2를-단일-항목으로-사용)
    - [인덱서가 검색되지 않음](#인덱서가-검색되지-않음-1)
    - [Jackett 수동 검색으로 더 많은 결과 찾기](#jackett-수동-검색으로-더-많은-결과-찾기)
    - [릴리스 프로필이 적용되지 않음](#릴리스-프로필이-적용되지-않음)
    - [목록에 없는 문제](#목록에-없는-문제-1)
  - [오류](#오류)
    - [The underlying connection was closed: An unexpected error occurred on a send](#the-underlying-connection-was-closed-an-unexpected-error-occurred-on-a-send)
    - [The request timed out](#the-request-timed-out)
    - [목록에 없는 문제](#목록에-없는-문제-2)

# 도움 요청하기

도움이 필요하신가요? 괜찮습니다, 때로는 모두 도움이 필요합니다. 실시간으로 도움을 받으려면 다음 채팅을 통해 도움을 받을 수 있습니다.

- [<i class="fab fa-discord"></i>&emsp;Discord *공식 Sonarr Discord*](https://discord.sonarr.tv/)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *공식 Sonarr Subreddit*](https://reddit.com/r/sonarr)
{.links-list}

하지만 질문을 하기 전에 도움을 요청하는 방법을 최대한 잘 준비해야 합니다. 문제를 명확히 설명하고, OS/배포판, .net/Mono 버전, Sonarr 버전, 다운로드 클라이언트 및 해당 버전과 같은 설정 정보를 간단히 설명해야 합니다. **[Docker](https://www.docker.com/)를 사용하는 경우 [Docker 가이드](/docker-guide)를 먼저 실행하여 일반적이고 빈번한 경로/권한 문제를 해결하세요. 그렇지 않으면 [docker compose](/docker-guide#docker-compose)를 준비하세요. [Docker Compose 생성 방법](https://trash-guides.info/compose)** 이미 시도한 내용과 확인한 내용에 대해 알려주세요. 문제를 재현한 후 [로그 및 로그 파일 섹션](#로그-및-로그-파일)을 사용하여 로깅 수준을 추적으로 설정하고, 문제를 재현한 후 관련 컨텍스트를 pastebin에 업로드하고 링크를 게시글에 포함시켜주세요. 문제를 강조하기 위해 스크린샷도 포함시킬 수 있습니다.

우리가 알면 도움을 드리기가 더 쉽습니다.

# 로그 및 로그 파일

또한 일반적인 문제 해결 문제를 검토하는 것이 유용할 수 있습니다:
- [다운로드 및 가져오기 일반적인 문제](#일반적인-문제)
- [검색 인덱서 및 트래커 일반적인 문제](#일반적인-문제-1)
{.links-list}

디버그 로그가 요청되면 로그에는 `debug`가 포함되고, 추적 로그가 요청되면 로그에는 `trace`가 포함됩니다. 제공하는 로그에 `debug` 또는 `trace`가 포함되지 않는 경우 요청된 로그가 아닙니다.

- 요청되지 않은 한 로그 파일 전체를 공유하지 마세요.
- 로그를 직접 Discord에 업로드하거나 벽처럼 긴 텍스트로 붙여넣지 마세요. 요청되지 않은 경우에는 아래에 언급된 서비스를 통해 텍스트로 공유하세요.

공유할 좋은 로그를 제공하기 위해:

> RSS 새로 고침과 같은 스팸성 작업이 실행되지 않도록 확인하세요.
{.is-warning}

1. [추적으로 로깅 설정하기 (설정 => 일반 => 로그 수준 또는 구성 파일 편집)](#추적디버그-로그)
2. [로그 지우기 (시스템 => 로그 => 로그 지우기 또는 로그 폴더의 모든 로그 삭제)](#로그-지우기)
3. 문제 재현하기 (문제가 발생하는 작업을 다시 수행하세요)
4. UI나 로그 파일에서 추적 로그 파일(sonarr.trace.txt)을 열고 관련 컨텍스트를 찾으세요.
5. 문제가 발생하기 전에 큰 부분을 복사하고, 문제 자체를 복사하고, 문제가 발생한 후 큰 부분을 복사하세요.
6. [Gist](https://gist.github.com/), [0bin (**반드시 색상 지정 비활성화**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu의 Pastebin](https://pastebin.ubuntu.com/) 또는 유사한 사이트(아래에서 언급된 사이트는 제외)를 사용하여 위에서 복사한 로그를 공유하세요.

**주의사항:**
- **[pastebin.com](https://pastebin.com)은 로그를 차단하는 필터가 있으므로 사용하지 마세요.
- [pastebin.pl](https://pastebin.pl)은 사이트에 자주 접속할 수 없습니다.
- [JustPasteIt](https://justpaste.it/)은 로그 검토를 용이하게하지 않습니다.
- 로그를 파일로 업로드하지 마세요.
- 로그를 Google Drive, Dropbox 또는 기타 위에 언급되지 않은 사이트에 업로드하고 공유하지 마세요.
- 로그를 아카이브(zip, tar (tarball), 7zip 등)하지 마세요.
- 콘솔 출력, 도커 컨테이너 출력 또는 응용 프로그램 로그 이외의 내용을 공유하지 마세요.

**중요한 참고:**
- [0bin](https://0bin.net/)을 사용하는 경우 색상 지정을 비활성화하고 읽은 후에 삭제하지 않도록 주의하세요.

- 또는 특정 항목을 찾기 위해 이전 로그 파일 중 어떤 파일인지 확실하지 않은 경우 Notepad++을 사용할 수 있습니다. Notepad++의 "파일에서 찾기" 기능을 사용하여 필요한 경우 이전 로그 파일을 검색할 수 있습니다.
- **Unix 전용:** 특정 항목을 찾기 위해 이전 로그 파일 중 어떤 파일인지 확실하지 않은 경우 grep을 사용할 수 있습니다. 예를 들어, "Shooter"라는 영화/TV 프로그램/책/노래/인덱서에 대한 정보를 찾으려면 다음 명령을 실행할 수 있습니다. `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` [Appdata 디렉토리](/sonarr/appdata-directory)가 홈 폴더에 있는 경우 다음과 같이 실행할 수 있습니다. `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * 다음과 같은 플래그가 있습니다.
    * -i: 대소문자를 구분하지 않음
    * -n: 줄 번호 표시
    *  -r: 경로의 모든 파일을 재귀적으로 확인
    * -C: 찾은 줄 앞뒤로 표시할 줄 수를 지정
    * -e: 검색할 패턴

```

## 표준 로그 위치

로그 파일은 Sonarr의 [Appdata 디렉토리](/sonarr/appdata-directory) 내의 logs/ 폴더에 있습니다. 또한 UI에서 System => Logs => Files에서 로그 파일에 액세스할 수 있습니다.

> 참고: UI의 로그("이벤트") 테이블은 로그 파일과 동일하지 않으며 유용하지 않습니다. 로그가 요청되면 로그 파일에서 복사/붙여넣기를 해주세요.
{.is-info}

## 업데이트 로그 위치

업데이트 로그 파일은 Sonarr의 [Appdata 디렉토리](/sonarr/appdata-directory) 내의 UpdateLogs/ 폴더에 있습니다.

## 로그 공유

로그는 포럼이나 Reddit 게시물에서 길고 읽기 어려울 수 있으며 Discord에서 스팸이 될 수 있으므로 [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) 또는 유사한 pastebin 사이트를 사용하세요. 일반적으로 전체 파일이 필요하지 않으며, 문제/오류 전후의 충분한 컨텍스트만 필요합니다. RSS 동기화나 라이브러리 새로 고침과 같은 스팸성 작업이 완료될 때까지 기다리지 않도록 주의하세요.

## 추적/디버그 로그

로그 수준은 설정 => 일반 => 로깅에서 변경할 수 있습니다. Sonarr을 다시 시작할 필요는 없습니다. 이 변경은 로그 파일에만 영향을 미치며 로깅 데이터베이스에는 영향을 미치지 않습니다. 최신 디버그/추적 로그 파일의 이름은 각각 `sonarr.debug.txt` 및 `sonarr.trace.txt`입니다.

로그 수준을 설정할 수 없는 경우 UI에 액세스할 수 없는 경우 AppData 디렉토리의 config.xml을 편집하여 LogLevel 값을 Info 대신 Debug 또는 Trace로 설정할 수 있습니다.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## 로그 지우기

로그 파일과 로그 데이터베이스를 UI에서 직접 지울 수 있습니다. System => Logs => Files 및 System => Logs => Delete (휴지통 아이콘)를 사용하세요.

# 여러 개의 로그 파일

Sonarr은 각각 1MB로 제한된 롤링 로그 파일을 사용합니다. 현재 로그 파일은 항상 `sonarr.txt`이며, 다른 파일은 `sonarr.0.txt`가 다음으로 최신 파일입니다(숫자가 높을수록 오래된 파일입니다). 이 로그 파일에는 `fatal`, `error`, `warn`, `info` 항목이 포함됩니다.

디버그 로그 수준이 활성화되어 있는 경우 추가적인 `sonarr.debug.txt` 롤링 로그 파일이 있을 수 있습니다. 이 로그 파일에는 `fatal`, `error`, `warn`, `info`, `debug` 항목이 포함됩니다. 일반적으로 40시간 동안의 로그를 포함합니다.

추적 로그 수준이 활성화되어 있는 경우 추가적인 `sonarr.trace.txt` 롤링 로그 파일이 있을 수 있습니다. 이 로그 파일에는 `fatal`, `error`, `warn`, `info`, `debug`, `trace` 항목이 포함됩니다. 추적 로그의 상세성으로 인해 최대 몇 시간 동안의 로그만 포함됩니다.

# 실패한 업데이트에서 복구하기

업그레이드 시 문제가 발생하지 않도록 최선을 다하지만, 발생할 경우 설치를 복구하는 단계를 안내합니다.

## 문제 확인하기

업데이트 후 응용 프로그램이 시작되지 않을 때 가장 먼저 확인할 곳은 [업데이트 로그](#업데이트-로그-위치)를 검토하고 업데이트가 성공적으로 완료되었는지 확인하는 것입니다. 그래도 문제가 없다면 일반적인 응용 프로그램 로그 파일을 확인하기 전에 [로그](/sonarr/settings#logging) 및 [로그 파일](/sonarr/system#log-files)을 사용하여 로그 수준을 높이세요.

### 마이그레이션 문제

- 마이그레이션 오류는 동일하지 않을 수 있지만, 다음은 예시입니다:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### 권한 문제

- 권한 문제는 응용 프로그램이 관련 임시 폴더 및/또는 응용 프로그램 이진 파일 폴더에 액세스할 수 없는 경우 발생합니다. 응용 프로그램이 실행되는 사용자/그룹이 적절한 액세스 권한을 갖도록 권한을 수정하세요.

- Synology 사용자는 이 Synology 버그 `Access to the path '/proc/{some number}/maps is denied`를 경험할 수 있습니다.

- 특정 NAS에서 Synology 사용자는 `/tmp`의 공간이 부족한 문제에 직면할 수 있습니다. 앱을 위해 다른 `/tmp` 경로를 지정해야 합니다. 이에 대한 도움은 SynoCommunity나 다른 Synology 지원 채널을 참조하십시오.

## 문제 해결

이주 문제가 발생한 경우 즉시 할 수 있는 것은 많지 않습니다. 만약 이 문제가 특정한 경우이거나 (또는 아직 게시물이 없는 경우) [우리의 subreddit](https://reddit.com/r/sonarr)에 게시물을 작성하거나 [discord](https://discord.sonarr.tv/)에 참여하십시오. 동일한 문제를 겪는 다른 사람들이 있다면, 문제가 해결되도록 노력하고 있음을 확신할 수 있습니다.

> `develop`에서 안정 버전으로 데이터베이스를 사용하지 않았는지 확인하십시오. 브랜치 전환은 권장되지 않습니다.{.is-info}

### 권한 문제

- 권한을 수정하여 응용 프로그램이 `/tmp`와 응용 프로그램의 설치 디렉토리 모두에 액세스(읽기 및 쓰기)할 수 있도록 합니다.

- `/proc/###/maps`에 문제가 있는 Synology 사용자는 Sonarr 또는 다른 \*Arr 응용 프로그램을 중지하고 업데이트하는 것으로 이 문제를 해결할 수 있습니다. 이는 SynoCommunity 패키지의 문제입니다.

### 수동 업그레이드

웹사이트에서 최신 릴리스를 다운로드합니다.

업데이트(.exe)를 설치하거나 기존 설치에 내용을 추출(.zip)하고 일반적으로 Sonarr을 다시 실행합니다.

# 다운로드 및 가져오기

대부분의 사용자가 문제를 겪는 곳은 다운로드 및 가져오기입니다. 전반적으로, Sonarr은 다운로드 클라이언트와 통신하고 다운로드한 파일에 액세스할 수 있어야 합니다. 지원되는 다양한 다운로드 클라이언트와 더욱 다양한 설정이 있습니다. 이는 몇 가지 일반적인 설정이 있지만, 하나의 올바른 설정은 없으며 모든 설정은 조금씩 다를 수 있습니다.

> **첫 번째 단계는 로깅을 Trace로 설정하는 것입니다. 자세한 내용은 [로그 및 로그 파일](#logging-and-log-files)을 참조하십시오. 그런 다음 문제를 재현하고 해당 시간대의 추적 수준 로그를 사용하여 문제를 검토합니다.**
> 누군가가 도움을 주고 있다면, [pastebin](https://0bin.net), [Gist](https://gist.com) 또는 유사한 사이트에 이전/이후의 컨텍스트를 보여주는 내용을 게시하십시오.
> 전체 파일이 아니어도 되며, *오류만* 있는 것이 아니어야 합니다. 또한 로그 파일에 로그를 스팸하는 작업이 실행되지 않는 상태에서 문제를 재현해야 합니다.
{.is-danger}

도움을 요청할 때는 [도움 요청](#asking-for-help)을 읽어 필요한 세부 정보를 제공할 수 있도록 하십시오.

## 다운로드 클라이언트 테스트

다운로드 클라이언트가 실행 중인지 확인합니다. 먼저 다운로드 클라이언트를 테스트하고 작동하지 않으면 추적 수준 로그에서 자세한 정보를 확인할 수 있습니다. 브라우저에 입력할 수 있는 URL을 찾아서 작동하는지 확인하십시오. 연결 문제일 수 있으며, 잘못된 IP, 호스트 이름, 포트 또는 방화벽이 액세스를 차단할 수 있습니다. 사용자 이름, 비밀번호 또는 API 키를 잘못 입력한 인증 문제와 같이 명확한 문제일 수도 있습니다.

## 다운로드 테스트

이제 다운로드를 시도해 보겠습니다. 시리즈의 에피소드를 선택하고 수동 검색을 수행합니다. 그 파일 중 하나를 선택하고 다운로드를 시도합니다. 다운로드 클라이언트로 전송되는지 확인하십시오. 올바른 카테고리에 포함되는지 확인하십시오. 활동에 표시되는지 확인하십시오. **완료된 다운로드 확인** 작업(모니터링된 다운로드 새로 고침 및 처리된 다운로드 작업) 중에 추적 수준 로그에 표시되는지 확인하십시오. 해당 작업은 대략 매 분마다 실행됩니다. 해당 작업 중에 파일이 올바르게 구문 분석되는지 확인하십시오. 대기 중인 다운로드에 합리적인 이름이 있는지 확인하십시오. 일부 인덱서/트래커에서는 ID로 검색하기 때문에 인식할 수 없는 이름으로 대기 중인 다운로드를 큐에 넣을 수 있습니다.

## 가져오기 테스트

가져오기 문제는 대부분 활동에서 오렌지 아이콘이 표시되며 오류를 확인할 수 있습니다. 활동에 표시되지 않는 경우, 이것이 먼저 해결해야 할 문제입니다. 따라서 다시 돌아가서 이 문제를 해결하십시오. 대부분의 가져오기 오류는 *권한* 문제입니다. 가져오기 폴더에서 읽기 및 쓰기가 가능해야 합니다. 때로는 라이브러리 폴더의 권한도 문제가 될 수 있으므로 둘 다 확인하십시오.

경로 문제도 가능하지만, 일반적인 설정에서는 그렇게 흔하지 않습니다. 경로 문제를 이해하는 핵심은 다운로드 클라이언트로부터 다운로드 경로를 얻는다는 것입니다. 이는 다운로드 클라이언트가 다른 시스템(심지어 다른 운영 체제일 수도 있음)에서 실행될 때 문제가 될 수 있습니다. Docker 설정에서도 발생할 수 있으며, 볼륨이 잘 구성되지 않은 경우입니다. 원격 경로 매핑은 시드박스 설정과 같이 제어할 수 없는 경우에 좋은 해결책입니다. Docker 설정에서는 경로를 수정하는 것이 더 좋은 옵션입니다.

## 일반적인 문제

일부 일반적인 문제는 다음과 같습니다.

### 릴리스에 예상한 하나 이상의 에피소드가 가져오지 않거나 누락됨

- 모든 에피소드가 가져오기된 경우, 가장 일반적인 원인은 시즌 팩이 다운로드되었지만 시즌의 모든 에피소드를 포함하지 않습니다. `X`를 클릭하여 해당 릴리스를 제거하고 무시하십시오.
- 다른 모든 문제의 경우, 하나 이상의 에피소드가 가져오기되지 못했습니다. UI의 정보와 기타 일반적인 문제를 검토하십시오.

### Sonarr v2 사용

Sonarr v2는 2021년 3월부터 지원이 종료되었으며 더 이상 지원되지 않습니다. Sonarr v3로 업그레이드하십시오. qBittorrent v4.3.0 이상과 호환되지 않습니다.

### 다운로드 클라이언트의 웹 인터페이스가 비활성화됨

Sonarr은 다운로드 클라이언트와 API를 통해 통신하고 클라이언트의 웹 인터페이스를 통해 액세스합니다. 클라이언트의 웹 인터페이스가 활성화되어 있는지 확인하고 사용 중인 포트가 다른 클라이언트 포트 또는 시스템에서 사용 중인 포트와 충돌하지 않도록 해야 합니다.

### 잘못 구성된 SSL 사용

로컬 네트워크에서 인스턴스와 다운로드 클라이언트를 모두 사용하는 경우 SSL 암호화가 켜져 있지 않도록 확인하십시오. 자세한 내용은 [SSL FAQ 항목](/sonarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues)을 참조하십시오.

### Windows에서 공유가 보이지 않음

Windows 서비스의 기본 사용자는 일반적으로 공유에 액세스할 수 없는 `LocalService`입니다. 서비스를 편집하고 사용자로 실행하도록 설정하십시오. 자세한 내용은 FAQ 항목 [왜 원격 서버에서 파일을 볼 수 없을까요?](/sonarr/faq#why-cant-i-see-my-files-on-a-remote-server)를 참조하십시오.

### 매핑된 네트워크 드라이브는 신뢰할 수 없음

`X:\`와 같은 매핑된 네트워크 드라이브는 편리하지만, UNC 경로인 `\\server\share`만큼 신뢰할 수 없습니다. 또한 로그인하기 전에 사용할 수 없습니다. 필요한 경우 설정하고 다운로드 클라이언트를 사용하여 UNC 경로를 사용하도록 설정하십시오. 라이브러리가 공유에 있는 경우 루트 폴더가 UNC 경로를 사용하도록 설정해야 합니다. 다운로드 클라이언트가 공유로 전송하는 경우 다운로드 경로를 다운로드 클라이언트에서 가져오기 때문에 해당 경로를 구성해야 합니다. 매핑된 네트워크 드라이브를 개인적으로 사용하는 것은 괜찮지만, 자동화에는 사용하지 마십시오.

### Docker 및 사용자, 그룹, 소유권, 권한 및 경로

Docker는 잘못된 설정이 쉽게 발생할 수 있는 복잡성을 추가하지만, 여전히 기능이 있는 설정을 얻을 수 있습니다. 이 문서에서는 이러한 문제를 자세히 다루지 않고, 사용자, 그룹, 소유권, 권한 및 경로에 대해 설명하는 위키 문서 [for these automation software and Docker](/docker-guide)를 읽으십시오. 이 문서는 특정 Docker 시스템에 특정되지 않으며, 대신 고수준에서 다양한 주제를 다루므로 사용자의 환경에 구현할 수 있습니다.

### 원격 경로 매핑

Sonarr을 Docker에서 사용하고 다운로드 클라이언트를 Docker가 아닌 곳에서 사용하거나 두 프로그램을 다른 서버에 설치한 경우 원격 경로 매핑이 필요할 수 있습니다.

로그는 다음과 같이 보일 것입니다.

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/torrents/tv/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

따라서 `/volume3/data`는 Sonarr의 컨테이너 내에 존재하지 않거나 액세스할 수 없습니다.

- [설정 => 다운로드 클라이언트 => 원격 경로 매핑](/sonarr/settings#remote-path-mappings)
- 원격 경로 매핑은 다운로드 클라이언트가 다른 서버에 있는 경우나 \*Arr가 Windows에 있고 다운로드 클라이언트가 Linux에 있는 경우와 같이 완료된 데이터의 경로를 다루지 않는 경우에 사용됩니다.
- 일반적으로 원격 경로 매핑은 \*Arr가 Windows에 있고 다운로드 클라이언트가 Linux에 있는 경우 또는 그 반대인 경우에만 필요합니다. 원격 경로 매핑은 Docker 및 Native 클라이언트를 혼합하는 경우 또는 원격 서버를 사용하는 경우에도 필요할 수 있습니다.
- 원격 경로 매핑은 DUMB 검색/치환(원격 값이 발견되면 해당 호스트에 대한 LOCAL 값으로 대체)입니다.
- 잘못된 경로에 대한 오류 메시지에 REPLACED 값이 포함되어 있지 않은 경우, 경로 매핑이 예상대로 작동하지 않습니다. 일반적인 해결책은 매핑을 추가하고 제거하는 것입니다.
- [원격 경로 매핑에 대한 자세한 정보는 TRaSH의 튜토리얼을 참조하십시오](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> \*Arr 및 다운로드 클라이언트 모두 Docker 컨테이너인 경우 원격 경로 매핑이 필요한 경우는 드물지만, [Docker 가이드](/docker-guide)를 검토하거나 [TRaSH의 튜토리얼](https://trash-guides.info/hardlinks)을 따르는 것이 좋습니다.
{.is-info}

#### 원격 마운트 또는 원격 동기화 (Syncthing)

- 다운로드하는 동안 계속 동기화되도록 설정해야 합니다. 그리고 로컬 동기화 대상이 가져오기될 때 하드 링크가 가능하도록 해야 합니다. 즉, 동일한 파일 시스템에 있어야 하며 동일하게 보여야 합니다.
  - 미완료 및 완료된 파일이 모두 포함된 일반 폴더에서 동기화합니다.
  - 라이브러리와 로컬 파일 시스템이 동일한 위치에 있고 동일하게 보이도록 동기화합니다(Docker 및 네트워크 공유로 인해 잘못 구성될 수 있음).
  - 다운로드 파일이 복사, 하드 링크 또는 이동될 수 있도록 하기 위해 미리 동기화합니다. 사용자 또는 그룹이 읽기 및 쓰기를 할 수 있어야 합니다.
  - 동시에 다운로드하는 동안 동기화되므로 거의 다운로드가 완료된 상태로 선언됩니다. 그리고 아직 완전히 완료되지 않았더라도 하드링크가 가능하면 괜찮습니다.
  - (선택 사항 - 해당되는 경우 및/또는 필요한 경우(예: 원격 유즈넷 클라이언트)) 가져오기/다운로드/업그레이드 시에 원격 파일을 제거하기 위해 사용자 정의 스크립트를 구성합니다.
- 대안으로 원격 마운트는 원격 동기화 설정보다 훨씬 복잡하지 않지만, 일반적으로 느립니다.
  - sshfs 또는 다른 네트워크 파일 시스템 프로토콜을 사용하여 원격 저장소를 마운트합니다.
  - \*Arr가 실행되도록 구성된 사용자와 그룹이 읽기 또는 쓰기 액세스 권한을 갖도록 합니다.
  - 원격 경로 매핑을 구성하여 REMOTE 경로를 찾고 LOCAL과 동일한 경로로 대체합니다.

### 라이브러리 폴더의 권한

로그는 다음과 같이 보일 것입니다.

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/tv/The Orville/Season 03/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

목적지의 *권한*과 *소유권*을 확인하는 것을 잊지 마십시오. 다운로드의 소유권과 권한에 집중하기 쉽지만, 일반적으로 권한 관련 문제의 원인이 될 수 있지만, 목적지도 문제가 될 수 있습니다. 대상 폴더가 있는지 확인하십시오. 대상 *파일*이 이미 존재하거나 삭제되거나 휴지통으로 이동할 수 없는지 확인하십시오. 소유권과 권한이 다운로드한 파일을 복사, 하드 링크 또는 이동할 수 있도록 허용하는지 확인하십시오. 실행되는 사용자 또는 그룹은 루트 폴더를 읽고 쓸 수 있어야 합니다.

- Windows 사용자의 경우 서비스로 실행되는 경우:
  - Windows 서비스는 기본적으로 'Local Service' 계정에서 실행됩니다. 기본적으로 이 계정은 수동으로 권한을 할당하지 않는 한 사용자의 홈 디렉토리에 액세스할 수 없습니다. 이는 홈 디렉토리로 다운로드를 구성한 다운로드 클라이언트를 사용하는 경우 특히 관련이 있습니다.
  - 'Local Service'는 일반적으로 매우 제한된 권한을 갖습니다. 따라서 사용자가 로그인한 상태로 앱을 시스템 트레이 응용 프로그램으로 설치하는 것이 좋습니다. 설치 프로그램에서 이 옵션을 제공합니다. 서비스에서 트레이 응용 프로그램으로 전환하는 방법에 대해서는 FAQ를 참조하십시오.

- Synology 사용자는 [SynoCommunity 패키지에 대한 권한 관리](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)를 참조하십시오.

- Windows가 아닌 경우: NFS 마운트를 사용하는 경우 `nolock`이 활성화되어 있는지 확인하십시오.
- SMB 마운트를 사용하는 경우 `nobrl`이 활성화되어 있는지 확인하십시오.

### 다운로드 폴더의 권한

다음과 유사한 오류가 표시됩니다.

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES.1/a4187f6c3c4445f98e85da52b83c84e8.mkv. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

또는

```none
2022-02-03 10:40:41.8|Warn|Sabnzbd|[Resident.Alien.S02E02.720p.WEB.H264-CAKES] Error occurred while trying to delete data from '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES/'.
 
[v3.0.6.1342] System.UnauthorizedAccessException: Access to the path '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES' is denied.
```

*소스*의 *권한*과 *소유권*을 확인하는 것을 잊지 마십시오. 대상의 소유권과 권한에 집중하기 쉽지만, 일반적으로 소스가 원인입니다. 소스 폴더가 있는지 확인하십시오. 소유권과 권한이 다운로드한 파일을 복사/하드링크하거나 복사+삭제/이동할 수 있도록 허용하는지 확인하십시오. Sonarr가 실행되는 사용자 또는 그룹이 다운로드 파일을 읽고 쓸 수 있어야 합니다.

- Windows 사용자의 경우 서비스로 실행되는 경우:
  - Windows 서비스는 기본적으로 'Local Service' 계정에서 실행됩니다. 기본적으로 이 계정은 수동으로 권한을 할당하지 않는 한 사용자의 홈 디렉토리에 액세스할 수 없습니다. 이는 홈 디렉토리로 다운로드를 구성한 다운로드 클라이언트를 사용하는 경우 특히 관련이 있습니다.
  - 'Local Service'는 일반적으로 매우 제한된 권한을 갖습니다. 따라서 사용자가 로그인한 상태로 앱을 시스템 트레이 응용 프로그램으로 설치하는 것이 좋습니다. 설치 프로그램에서 이 옵션을 제공합니다. 서비스에서 트레이 응용 프로그램으로 전환하는 방법에 대해서는 FAQ를 참조하십시오.

- Synology 사용자는 [SynoCommunity 패키지에 대한 권한 관리](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)를 참조하십시오.

- Windows가 아닌 경우: NFS 마운트를 사용하는 경우 `nolock`이 활성화되어 있는지 확인하십시오.
- SMB 마운트를 사용하는 경우 `nobrl`이 활성화되어 있는지 확인하십시오.

### 다운로드 폴더와 라이브러리 폴더가 동일한 폴더가 아님

- 다운로드 클라이언트는 \*Arr에서 액세스할 수 있는 폴더에 다운로드해야 하며 루트/라이브러리 폴더가 아니어야 합니다. 다운로드 폴더와 루트 폴더는 분리되어야 합니다. 
- 루트 폴더에 직접 다운로드하지 마십시오. 또한 루트 폴더를 다운로드 클라이언트의 완료된 폴더나 미완료된 폴더로 사용하지 마십시오.
- [**이로 인해 시스템에서도 건강 점검이 실행됩니다**](/sonarr/system#downloading-into-root-folder)
- 응용 프로그램 내에서 루트 폴더는 구성된 미디어 라이브러리 폴더로 정의됩니다. 이는 마운트의 루트 폴더가 아닙니다. 다운로드 클라이언트가 미완료 또는 완료된 다운로드를 루트(라이브러리) 폴더로 이동하거나 이동하는 경우 문제가 발생할 수 있으며 권장되지 않습니다. 이를 수정하려면 다운로드 클라이언트를 변경하여 다운로드를 루트 폴더에 배치하지 않도록 설정하십시오. '배치'에는 다운로드 클라이언트 카테고리가 루트 폴더로 설정되어 있는 경우나 NZBGet/SABnzbd가 정렬이 가능하도록 설정되어 있고 루트 폴더로 정렬되는 경우도 포함됩니다. 이 체크는 현재 사용 중인 루트 폴더뿐만 아니라 추가된 모든 정의된 루트 폴더를 확인합니다. 즉, 다운로드 클라이언트가 다운로드하거나 완료된 다운로드를 이동하는 폴더는 \*Arr 응용 프로그램에서 루트/라이브러리/최종 미디어 대상 폴더로 구성된 폴더와 동일하지 않아야 합니다.
- 구성된 루트 폴더(라이브러리 폴더)는 [설정 => 미디어 관리 => 루트 폴더](/sonarr/settings/#root-folders)에서 찾을 수 있습니다.
- 예를 들어, 다운로드가 `\data\downloads`로 이동하는 경우 루트 폴더가 `\data\downloads`로 설정되어 있는 것입니다.
- 루트 폴더/라이브러리 폴더에는 `\data\media\`와 같은 경로를 사용하는 것이 좋습니다. 다운로드에는 `\data\downloads\`와 같은 경로를 사용하는 것이 좋습니다.

> 다운로드 폴더와 루트/라이브러리 폴더는 반드시 분리되어야 합니다.
{.is-warning}

### 잘못된 카테고리

Sonarr은 자체 다운로드만 처리하도록 카테고리를 설정해야 합니다. 일반적으로 올바른 카테고리 없이 추가된 토렌트는 거의 없지만, 발생할 수 있습니다. 수동으로 토렌트를 추가하고 처리하려면 올바른 카테고리가 있어야 합니다. 언제든지 설정할 수 있으며, 다운로드는 매 분마다 처리하려고 시도합니다.

### 압축된 토렌트

로그에는 다음과 같은 오류가 표시됩니다.

```none
No files found are eligible for import
```

토렌트가 `.rar` 파일로 압축되어 있는 경우 압축 해제를 설정해야 합니다. [Unpackerr](https://github.com/unpackerr/unpackerr)를 추천합니다. 이는 압축 해제를 올바르게 수행하여 손상된 부분적인 가져오기를 방지하고 가져온 파일을 정리합니다.

또한 해당 폴더에 유효한 미디어 파일이 없는 경우에도 이 오류가 발생할 수 있습니다.

### 반복 다운로드

반복 다운로드의 원인은 여러 가지가 있지만, 하나는 릴리스 프로필의 인덱서 제한과 관련이 있습니다. 인덱서는 데이터와 함께 저장되지 않으므로 라이브러리의 미디어에 대한 `preferred word` 점수는 0입니다. 그러나 "RSS" 및 검색 중에는 이 점수가 적용됩니다. 마찬가지로 `must contain` 또는 `must-not` 제한은 해당 인덱서에만 적용되며, 다른 것은 공정한 게임입니다. 이로 인해 항목을 반복해서 다운로드하게 되는데, 업그레이드처럼 보이다가 그렇지 않고 다시 나타나 업그레이드처럼 보이기 때문입니다. 릴리스 프로필을 인덱서에 제한하지 마십시오.

이는 다운로드가 실제로 가져오지 않고 큐에서 누락되어 새로운 다운로드가 계속해서 가져와지고 가져오지 않는 경우에도 발생할 수 있습니다. 이에 대한 자세한 문제 해결 단계는 다른 일반적인 문제 및 문제 해결 단계를 참조하십시오.

### 유즈넷 다운로드가 가져오지 못함

Sonarr은 SABnzbd 및 NZBGet에서 최근 60개의 다운로드만 확인합니다. 따라서 이력을 유지하는 경우 큰 큐에서 가져오기 문제가 발생할 수 있으며, 다운로드가 은폐되고 가져오지 않을 수 있습니다. 이를 방지하기 위해 이력을 유지하면서 아직 표시되는 항목을 확인할 수 있도록 하십시오. 이를 위해 완료 및 실패한 다운로드 핸들러에서 제거를 활성화하면 됩니다. NZBGet의 경우, 항목이 *숨겨진* 이력으로 이동됩니다. 불행히도, SABnzbd에는 유사한 기능이 없습니다. 거기서 할 수 있는 최선은 nzb 백업 폴더를 사용하는 것입니다.

### 다운로드 클라이언트에서 항목 제거

다운로드 클라이언트는 다운로드를 제거하지 않아야 합니다. 유즈넷 클라이언트는 이력에서 다운로드를 제거하지 않도록 설정해야 합니다. 토렌트 클라이언트는 시딩이 완료되면 토렌트를 제거하지 않고 일시 중지하거나 중지하도록 설정해야 합니다. 이는 Sonarr이 가져올 항목을 알기 위해 다운로드 클라이언트와 통신하기 때문입니다. 따라서 제거되면 가져올 항목이 없습니다. 파일이 들어있는 폴더가 있는 경우에도 마찬가지입니다.

SABnzbd의 경우, 이는 History Retention 설정으로 처리됩니다.

### 라이브러리 항목과 일치하지 않는 다운로드

다운로드가 가져온 후에는 다양한 이유로 릴리스를 구문 분석할 수 없습니다. Activity => Options => Show Unknown(최근 빌드에서는 기본적으로 활성화됨)를 사용하면 \*Arr의 다운로드 클라이언트 카테고리 내에서 무시되거나 이미 가져온 항목이 아닌 모든 항목이 표시됩니다. 이러한 항목은 일반적으로 수동으로 매핑하고 가져와야 합니다.

이는 또한 다운로드 클라이언트에는 있지만 응용 프로그램에는 해당 미디어 항목(영화/에피소드/도서/노래)이 없는 경우에도 발생할 수 있습니다.

#### 그랩 기록을 통해 일치하는 시리즈를 찾았지만, 시리즈가 시리즈 ID로 일치했습니다. 자동 가져오기가 불가능합니다.

- 이 가져오기 오류는 위와 같은 일치하지 않는 오류와 유사합니다.
- Sonarr은 인덱서 또는 트래커가 원하는 시리즈의 TVDb ID(또는 IMDb ID)를 가진 릴리스라고 보고한 경우 해당 릴리스를 가져왔습니다.
- 다운로드된 파일의 시리즈가 보고된 ID와 일치하지 않으므로 Sonarr은 파일을 가져오지 않습니다.
- 시리즈 제목과 릴리스 이름에 따라 - 릴리스가 해당 시리즈 ID와 연결된 올바른 경우 - Sonarr에 별칭을 추가해야 할 수도 있습니다. [이 FAQ 항목](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x)에서 자세한 정보를 확인할 수 있습니다.
- 또는 릴리스가 잘못 레이블되어 있고 보고된 시리즈 ID가 아닌 경우입니다. 이를 인덱서에 보고하여 수정 조치를 취해야 합니다.
- 이 오류를 처리하려면 다음 단계를 수행하십시오.
  1. 파일의 시리즈를 확인합니다.
  1. 별칭을 요청합니다(해당되는 경우).
  1. 파일을 수동으로 가져옵니다(활동 => 대기열에서 오른쪽에 있는 인간 아이콘) 또는 클라이언트의 대기열에서 `X`를 클릭하여 해당 릴리스를 무시하고 선택적으로 차단 목록에 추가하거나 선택적으로 클라이언트에서 제거합니다.

### 에피소드 이름이 TBA입니다.

TVDB에서 에피소드 이름이 알려지지 않은 경우 TBA로 제목이 지정되며 API에는 24시간 캐시가 있습니다. 일반적으로 TVDB 웹 사이트의 변경 사항은 TVDB 캐시, Skyhook 캐시 및 시리즈 새로 고침 간격으로 인해 Sonarr에 도달하는 데 24-48시간이 걸립니다.

Sonarr의 [에피소드 제목 필요](/sonarr/settings#importing) 설정은 제목이 TBA인 경우 가져오기 동작을 제어하지만, 에피소드의 방영일로부터 24시간이 지나면 제목이 여전히 TBA인 경우에도 릴리스가 가져와집니다. 또한 TBA 제목 파일의 자동 후속 이름 변경은 없습니다.

### 기본 연결이 닫혔습니다: 전송 중 예기치 않은 오류가 발생했습니다.

이는 현재 .NET 버전에서 지원되지 않는 SSL 프로토콜을 사용하는 인덱서에 의해 발생합니다. [Sonarr => 시스템 => 상태](/sonarr/system#status)에서 현재 .NET 버전을 확인할 수 있습니다.

### 요청 시간이 초과되었습니다.

Sonarr은 클라이언트로부터 응답을 받지 못하고 있습니다.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

이는 다음과 같은 원인으로도 발생할 수 있습니다.

- VPN이 잘못 구성되었거나 사용되는 경우
- 프록시가 잘못 구성되었거나 사용되는 경우
- 로컬 DNS 문제 - 다른 DNS 공급자로 변경해 보십시오.
- 로컬 IPv6 문제 - 일반적으로 IPv6는 활성화되어 있지만 기능이 없습니다.
- Privoxy의 사용 및 잘못된 구성

## 나열되지 않은 문제

일반적인 권한 및 네트워킹 문제 해결 명령에 대해 [가이드](/permissions-and-networking)에서 확인할 수도 있습니다. 그렇지 않으면 디스코드의 지원 팀과 상의하십시오. 이것이 일반적인 문제일 수 있는 경우 위키에 추가하도록 제안하십시오.

# 인덱서 및 트래커 검색

- [왜 Sonarr이 기대한 에피소드를 가져오지 않았을까요?](/sonarr/faq#why-didnt-sonarr-grab-an-episode-i-was-expecting) FAQ 항목도 도움이 될 수 있습니다.
- [Prowlarr](/prowlarr)를 사용하는 경우, [History](/prowlarr/history)에서 Prowlarr이 받은 모든 쿼리 및 해당 쿼리가 사이트로 전송된 방식을 볼 수 있습니다. Prowlarr History => Options에서 `Parameters`가 활성화되어 있는지 확인하십시오. (i) 아이콘을 클릭하면 추가 세부 정보가 표시됩니다.
- 문제 해결 단계는 아래에 나와 있습니다.

## 로깅을 추적 수준으로 설정

> **첫 번째 단계는 로깅을 추적 수준으로 설정하는 것입니다. 로깅 및 로그 파일에 대한 자세한 내용은 [로그 및 로그 파일](#logging-and-log-files)을 참조하십시오. 그런 다음 문제를 재현하고 해당 시간 범위의 추적 수준 로그를 사용하여 문제를 조사합니다.** 누군가가 도와주고 있다면, 전/후의 컨텍스트를 [pastebin](https://0bin.net), [Gist](https://gist.com) 또는 유사한 사이트에 올려서 보여줍니다. 전체 파일이어야 할 필요는 없으며 오류만 있는 것은 아닙니다. 또한 로그 파일에 로그 파일을 스팸으로 채우는 작업이 실행되지 않는 상태에서 문제를 재현해야 합니다.
{.is-danger}

## 인덱서 또는 트래커 테스트

인덱서 또는 트래커를 테스트할 때 디버그 또는 추적 로그에서 사용된 URL을 찾을 수 있습니다. 아래에 성공적인 테스트 예시가 나와 있습니다. 특정 URL과 매개변수를 사용하여 인덱서에 쿼리를 보내고 응답을 확인할 수 있습니다. 이 URL을 브라우저에서 테스트해 보세요. `apikey=(removed)`를 올바른 apikey인 `apikey=123`으로 바꿔서 테스트할 수 있습니다. 인덱서에서 오류가 발생하는 경우 매개변수를 실험해 보거나 연결성 문제가 있는지 확인할 수 있습니다. 자신의 브라우저에서 테스트한 후 시스템에서 실행 중인 시스템에서 테스트해야 합니다.

## 검색 테스트

인덱서/트래커 테스트와 마찬가지로 디버그 또는 추적 수준 로깅에서 검색을 트리거하면 로그 파일에서 사용된 URL을 얻을 수 있습니다. 테스트하는 동안 가능한 한 좁은 검색을 사용하는 것이 좋습니다. 단일 에피소드 또는 시즌에 대한 수동(대화식) 검색은 구체적이며 로그를 검사하는 동안 UI에서 결과를 확인할 수 있으므로 좋습니다. 수동(대화식) 검색은 시리즈로 이동하여 에피소드 또는 시즌에 대한 인간 아이콘을 클릭하여 트리거됩니다.

이 테스트에서는 명백한 오류를 찾고 몇 가지 간단한 테스트를 실행합니다. 검색에 사용된 URL을 로그 파일에서 확인할 수 있습니다. 특정 카테고리를 `cat=5030,5040,5045,5080`로 설정했으므로 예상한 결과를 보지 못하는 경우 이것이 한 가지 가능한 이유입니다. `tvdbid=354629`로 tvdbid로 검색했으므로 인덱서에서 에피소드가 올바르게 분류되지 않은 경우 수정해야 합니다. `season=1` 및 `ep=1`로 특정 시즌 및 에피소드로 검색했으므로 인덱서에서 이 정보가 올바르지 않으면 해당 결과를 볼 수 없습니다. 작동하는 쿼리의 출력 예시를 보려면 Manual Search XML Output을 참조하십시오.

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1" rel="self" type="application/rss+xml"/>
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
<newznab:response offset="0" total="2"/>
<item>
<title>The.Fix.S01E01.1080p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/358e0f946f953771c7688864b0334ba1
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=358e0f946f953771c7688864b0334ba1
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:32 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.1080p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)" length="3810861000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="3810861000"/>
<newznab:attr name="guid" value="358e0f946f953771c7688864b0334ba1"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="55"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:54:15 +0000"/>
</item>
<item>
<title>The.Fix.S01E01.720p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/f7e4ac2875b6a1ce45bae91ab19e9699
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=f7e4ac2875b6a1ce45bae91ab19e9699
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:33 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.720p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)" length="1195794000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="1195794000"/>
<newznab:attr name="guid" value="f7e4ac2875b6a1ce45bae91ab19e9699"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="14"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:51:45 +0000"/>
</item>
</channel>
</rss>
```

![searches-indexers-and-trackers1.png](/assets/sonarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/sonarr/searches-indexers-and-trackers2.png)

- 추적 로그 스니펫

```none
2021-03-20 13:15:23.6|Info|NzbSearchService|The Fix : S01E01에 대해 1개의 인덱서를 검색 중입니다.
2021-03-20 13:15:23.6|Debug|Newznab|피드 다운로드 중 https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
2021-03-20 13:15:23.6|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
```

- 검색의 전체 추적 로그

```none
2022-04-24 20:14:26.7|Info|NzbSearchService|Searching 1 indexers for [Fairy Tail : S02E91 (91)]
2022-04-24 20:14:26.7|Debug|Newznab|Downloading Feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=153021&season=2&ep=91
2022-04-24 20:14:26.7|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=153021&season=2&ep=91
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'proxyenabled' defaultValue:'False'
2022-04-24 20:14:27.3|Trace|HttpClient|Res: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=153021&season=2&ep=91: 200.OK (635 ms)
2022-04-24 20:14:27.3|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:27.3|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:27.3|Debug|NzbSearchService|Total of 2 reports were found for [Fairy Tail : S02E91 (91)] from 1 indexers
2022-04-24 20:14:27.3|Debug|NzbSearchService|Setting last search time to: 11/20/2019 20:14:27
2022-04-24 20:14:27.3|Info|DownloadDecisionMaker|Processing 2 releases
2022-04-24 20:14:27.3|Trace|DownloadDecisionMaker|Processing release 1/2
2022-04-24 20:14:27.3|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.1080p.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.3|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.1080p.WEB-DL'
2022-04-24 20:14:27.3|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.3|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.3|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.3|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:27.3|Debug|Parser|Quality parsed: WEBDL-1080p v1
2022-04-24 20:14:27.3|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.3|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.1080p.WEB-DL'
2022-04-24 20:14:27.3|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.1080p.WEB-DL': 0
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.1080p.WEB-DL, meets size constraints.
2022-04-24 20:14:27.3|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.3|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.3|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.3|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-1080p v1
2022-04-24 20:14:27.3|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:27.3|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.1080p.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.3|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.3|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.3|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.3|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.3|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] WEBDL-1080p is not wanted in profile
2022-04-24 20:14:27.3|Trace|DownloadDecisionMaker|Processing release 2/2
2022-04-24 20:14:27.3|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.720p.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.3|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.720p.WEB-DL'
2022-04-24 20:14:27.3|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.3|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.3|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.3|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:27.3|Debug|Parser|Quality parsed: WEBDL-720p v1
2022-04-24 20:14:27.3|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.3|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.720p.WEB-DL'
2022-04-24 20:14:27.3|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.720p.WEB-DL': 0
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.720p.WEB-DL, meets size constraints.
2022-04-24 20:14:27.3|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.3|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.3|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.3|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-720p v1
2022-04-24 20:14:27.3|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:27.3|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.720p.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.3|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.3|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.3|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.3|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'autounmonitorpreviouslydownloadedepisodes' defaultValue:'False'
2022-04-24 20:14:27.3|Debug|DownloadDecisionMaker|Release accepted
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'downloadpropersandrepacks' defaultValue:'PreferAndUpgrade'
2022-04-24 20:14:27.3|Trace|Http|Res: 66 [GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
2022-04-24 20:14:27.3|Debug|Api|[GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
```

## 일반적인 문제

아래는 대부분의 문제에 대한 해결책인 일반적인 문제입니다.

### 인덱서가 검색되지 않음

- 로그는 다음과 같이 보일 것입니다.

```none
2022-04-24 20:14:26.7|Info|ReleaseSearchService|Searching indexers for [Fairy Tail : S02E91 (91)]. 0 active indexers
2022-04-24 20:14:26.7|Debug|ReleaseSearchService|Total of 0 reports were found for [Fairy Tail : S02E91 (91)] from 0 indexers
2022-04-24 20:14:26.7|Info|DownloadDecisionMaker|No results found
```

- 위의 경우 검색되는 인덱서가 0개입니다. 이 숫자는 특정 설정에 따라 다를 수 있습니다. 설정한 인덱서의 수와 동일하지 않은 경우 다음과 같은 원인이 있을 수 있습니다.
  - [Health Checks (System => Status)](/sonarr/system#health)
    - [자동 검색이 활성화된 인덱서가 없습니다. Sonarr은 자동 검색 결과를 제공하지 않습니다.](/sonarr/system#no-indexers-available-with-automatic-search-enabled-sonarr-will-not-provide-any-automatic-search-results)
    - [활성화된 인덱서가 없습니다.](/sonarr/system#no-indexers-are-enabled)
    - [활성화된 인덱서가 검색을 지원하지 않습니다.](/sonarr/system#enabled-indexers-do-not-support-searching)
    - [대화식 검색이 활성화된 인덱서가 없습니다.](/sonarr/system#no-indexers-available-with-interactive-search-enabled)
    - [인덱서가 장애로 인해 사용할 수 없습니다.](/sonarr/system#indexers-are-unavailable-due-to-failures)
  - 애니메이션 시리즈 유형을 검색하고 트래커에 애니메이션 카테고리가 구성되어 있지 않은 경우. 인덱서에는 [두 가지 다른 구성 가능한 카테고리 유형](/sonarr/settings#indexers)이 있습니다.
  - 일일 또는 표준 시리즈 유형을 검색하고 트래커에 표준 (비 애니메이션) 카테고리가 구성되어 있지 않은 경우
    - 카테고리 - 기본 카테고리가 편집되지 않으면 기본 카테고리가 사용됩니다. 이 기본값은 최적화되지 않을 수 있습니다. 이 설정을 편집하면 Sonarr은 인덱서에 대한 사용 가능한 카테고리를 쿼리하고 선택 가능한 목록에서 표시합니다. 기본값은 카테고리를 토글하면 새로 고침됩니다.
  - 애니메이션 카테고리 - Sonarr이 애니메이션 검색에 사용할 카테고리입니다. 토글되지 않으면 카테고리가 사용되지 않습니다. 이 설정을 편집하면 Sonarr은 인덱서에 대한 사용 가능한 카테고리를 쿼리하고 선택 가능한 목록에서 표시합니다. 기본값은 카테고리를 토글하면 새로 고침됩니다.
  - 인덱서의 기능이 쿼리 유형 (시즌/에피소드 등)을 지원하지 않습니다.
    - Prowlarr에서 인덱서의 기능은 인덱서의 (I) 아이콘에서 찾을 수 있습니다.
    - Jackett은 UI에서 트래커의 기능을 표시하지 않습니다.
  - 추적 로그는 Sonarr을 ***다시 시작한 후*** 검색이 수행되면 인덱서가 무시되는 이유에 대한 정보를 표시합니다.

### 잘못된 이름의 릴리스

- 시리즈 팩은 지원되지 않습니다.
- 여러 시즌 팩은 지원되지 않습니다.
- 많은 경우에 Sonarr은 반환된 결과를 알려진 시리즈에 일치시키지 못합니다. 이러한 경우 로그는 다음과 같이 보일 것입니다. 이 경우에는 수동으로 가져와서 수동으로 가져와야 합니다. 로그에서 확인할 수 있는 핵심 구문은 `|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings`입니다.

```none
2022-02-23 14:11:09.7|Debug|Parser|Parsing string 'Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR'
2022-02-23 14:11:09.7|Trace|Parser|^(?<title>.+?)[-_. ]+?(?:S|Season|Saison|Series)[-_. ]?(?<season>\d{1,2}(?![-_. ]?\d+))(\W+|_|$)(?<extras>EXTRAS|SUBPACK)?(?!\\)
2022-02-23 14:11:09.7|Debug|Parser|Episode Parsed. Johnny Bravo 1997 Season 1 4 - Season 01 
2022-02-23 14:11:09.7|Debug|Parser|Language parsed: English
2022-02-23 14:11:09.7|Debug|QualityParser|Trying to parse quality for Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR
2022-02-23 14:11:09.7|Debug|Parser|Quality parsed: SDTV v1
2022-02-23 14:11:09.7|Debug|Parser|Release Group parsed: 
2022-02-23 14:11:09.8|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings
```

### 트래커에서 RawSearch Caps가 필요합니다.

- Sonarr은 `9 1 1`을 검색하지만 트래커에는 `9-1-1` 또는 `John s Show` 및 `John's Show`에 대한 결과만 있습니다.
- 이는 트래커가 표준화된 일반적인 검색을 지원하지 않기 때문입니다.
- 해결 방법은 트래커의 정의 검색 기능을 업데이트하여 `RawSearch`가 필요하고 지원됨을 나타내는 것입니다. ([여기](https://github.com/Sonarr/Sonarr/issues/1225#issuecomment-981153943) 참조)
- Jackett은 이 플래그를 지원하지만 기능을 추가하도록 Jackett에 기능 요청을 열어야 합니다.
- Prowlarr은 이 플래그를 지원하지만 기능을 추가하도록 Prowlarr에 기능 요청을 열어야 합니다.

### 시리즈에 별칭이 필요합니다.

릴리스는 `The Series Name`으로 업로드되었지만 TVDB에서는 `Series Name` 또는 유사한 이름 차이로 시리즈가 있습니다. [이 FAQ 항목](/sonarr/faq#why-cannot-sonarr-import-episode-files-for-series-x-why-cannot-sonarr-find-releases-for-series-x)을 참조하세요.

### 시리즈에 XEM 매핑이 필요합니다.

릴리스는 `Series Title S02E45` 또는 `Other Series Title S2022E42`로 업로드되었지만 TVDB에서는 이 에피소드를 `Series Title S03E01` 또는 `Other Series Title S03E42`로 가지고 있습니다. [이 FAQ 항목](/sonarr/faq#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)을 참조하세요.

### 잘못된 시리즈 유형

시리즈 유형은 Sonarr의 검색 방법에 영향을 미칩니다. 시리즈 유형은 인덱서에서 시리즈가 어떻게 릴리스되는지에 따라 선택되어야 합니다.
자세한 내용은 [이 FAQ 항목](/sonarr/faq#whats-the-different-series-types)을 참조하세요.

> **Anime** 시리즈 유형을 사용하는 경우, 표준 유형으로도 인덱서를 검색할 수 있습니다.
{.is-info}

#### 매일

로그에는 `Searching indexers for [The Witcher : 2021-12-20]`라는 메시지가 표시됩니다.

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### 표준

로그에는 `Searching indexers for [The Witcher : S01E09]`라는 메시지가 표시됩니다.

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### 애니메이션

로그에는 `Searching indexers for [The Witcher : S01E09 (09)]`라는 메시지가 표시됩니다.

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

### 미디어가 모니터링되지 않음

로그에는 다음과 유사한 내용이 표시됩니다.

```none
2022-03-30 13:46:03.0|Debug|MonitoredEpisodeSpecification|No episodes in the release are monitored. Rejecting
2022-03-30 13:46:03.0|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] One or more episodes is not monitored
```

시리즈/시즌/에피소드가 모니터링되지 않습니다. 시리즈, 시즌 및 에피소드의 모니터링 상태를 확인하세요.

> 시즌 팩은 모든 에피소드가 모니터링되고 시즌 팩이 모든 기존 에피소드를 업그레이드하거나 모든 에피소드가 누락된 경우에만 가져옵니다.
{.is-info}

### 쿼리 성공 - 결과 없음

`Query successful, but no results were returned from your indexer. This may be an issue with the indexer or your indexer category settings.`와 유사한 메시지를 받습니다.

이는 인덱서가 구성한 범주 내에 있는 결과를 반환하지 않는 경우에 발생합니다.

### 잘못된 범주

잘못된 범주는 인덱서/트래커의 수동 검색에서 결과가 표시되지만 \*Arr에는 표시되지 않는 가장 일반적인 원인입니다. 인덱서/트래커는 검색 결과에 범주를 표시해야 하므로 누락된 항목을 찾을 수 있습니다. Jackett 또는 Prowlarr를 사용하는 경우 각 트래커에는 특정 지원되는 범주 목록이 있습니다. Sonarr에서 항목을 편집하는 동안 이 목록을 브라우저 창에 표시하는 것이 도움이 될 수 있습니다.

> 인덱서 설정에서 `Anime Categories`를 비워 두면 인덱서는 Anime Series Type 검색에 사용되지 않습니다.
> 마찬가지로 인덱서 설정에서 `Categories`를 비워 두면 인덱서는 표준 및 매일 Series Type 검색에 사용되지 않습니다.
{.is-info}

### 잘못된 결과

인덱서가 완전히 관련 없는 결과를 반환할 수도 있습니다. Sonarr은 검색을 제한하기 위해 매개변수를 제공합니다. 때로는 완전히 관련 없는 결과가 반환됩니다. 또는 가끔은 대부분 관련이 있지만 일부 잘못된 결과가 반환됩니다. 첫 번째 경우는 일반적으로 인덱서의 문제이며 추적 로그에서 어떤 문제가 발생하는지 알 수 있습니다. 해당 인덱서를 비활성화하고 문제를 보고할 수 있습니다. 두 번째 경우는 일반적으로 범주화된 릴리스이며 인덱서/트래커에서 보고할 수 있습니다.

EZTV 및 기타 공개 트래커와 같은 특정 트래커는 쿼리하는 시리즈/시즌/에피소드와 정확히 일치하는 결과가 없는 경우 무작위 결과를 반환합니다. 이에 대한 해결책은 없습니다.

### 결과 누락

Sonarr에 표시되지 않지만 사이트에서 찾을 수 있는 결과가 있다면 다음과 같은 여러 가지 가능성 중 하나일 수 있습니다:

- [범주가 잘못되었습니다 - 위의 항목 참조](#wrong-categories)
- ID (IMDbId, TVDBId 등) 기반 검색이 수행되고 인덱서가 해당 릴리스를 올바르게 해당 ID에 매핑하지 않은 경우입니다. 이는 인덱서만 해결할 수 있는 문제입니다. 인덱서는 릴리스가 올바른 적용 가능한 ID에 매핑되도록 해야 합니다.
- Sonarr이 검색하는 방법과 일치하지 않는 방식으로 검색 중입니다. Sonarr이 쿼리하는 방식은 추적 로그에서 확인할 수 있습니다. 텍스트 기반 쿼리는 일반적으로 `q=words%20and%20things%20here`와 같은 형식으로 표시됩니다. 이 문자열은 HTTP 인코딩되어 있으며 온라인에서 HTML 디코딩/인코딩 도구를 사용하여 쉽게 디코딩할 수 있습니다.
- RSS 피드의 누락된 청크. 로그는 다음과 같이 표시되며 경고 이벤트가 표시됩니다.

```none
2022-02-22 08:03:38.7|Debug|Torznab|Downloading Feed http://jackett:9117/api/v2.0/indexers/torrentdownloads/results/torznab?t=tvsearch&cat=5000,100008&extended=1&apikey=(removed)&offset=2900&limit=100
2022-02-22 08:03:40.7|Warn|Torznab|Indexer TorrentDownloads rss sync didn't cover the period between 2/21/2022 8:32:06 PM and 2/21/2022 9:02:42 PM UTC. Search may be required.
```

### 인증서 유효성 검사

대부분의 인덱서/트래커에는 https를 통해 연결해야 하므로 시스템에서 제대로 작동해야 합니다. 이는 시스템의 시간대와 시간이 *정확히* 설정되어 있어야 함을 의미합니다. 또한 시스템 인증서가 최신 상태여야 합니다.

### 요청 시간 초과

Sonarr이 인덱서로부터 응답을 받지 못하고 있는 것입니다.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

이는 다음과 같은 이유로 발생할 수도 있습니다:

- VPN 또는 프록시를 사용하여 실행 중인 경우, 수백 명 또는 수천 명의 다른 사람들이 모두 , theXEM 및/또는 인덱서 및 트래커와 같은 서비스를 사용하려고 시도할 수 있습니다. 속도 제한 및 DDOS 보호는 주로 IP 주소별로 수행되며 VPN/프록시 출구 지점은 *하나*의 IP 주소입니다. 중국, 호주 또는 남아프리카와 같은 억압적인 국가가 아니라면 VPN/프록시를 사용할 필요가 없습니다.
- Rarbg는 API 내에서 일부 종류의 속도 제한을 가지고 있으며 결과가 없이 응답하는 것으로 나타납니다.

### IP 차단

비슷하게 속도 제한과 마찬가지로 일부 인덱서 - 예: Nyaa -는 IP 주소를 완전히 차단할 수 있습니다. 이는 일반적으로 반영구적이며 해결책은 ISP 또는 VPN 공급자에서 새 IP를 받는 것입니다.

### Jackett의 /all 엔드포인트 사용

Jackett의 `/all` 엔드포인트는 편리하지만 이것만의 이점입니다. 나머지는 잠재적인 문제입니다. 따라서 각 트래커를 개별적으로 추가해야 합니다. 또는 Jackett 및 NZBHydra2 대체 제품인 [Prowlarr](/prowlarr)을 확인할 수 있습니다.

[Jackett 자체도 /all을 피해야 하며 사용해서는 안 됩니다.](https://github.com/Jackett/Jackett#aggregate-indexers)

`/all` 엔드포인트를 사용하는 것은 이점이 없으며(관리 오버헤드만 감소됨), 다음과 같은 단점만 있습니다:

- 인덱서별 설정(범주, 검색 모드 등)을 제어할 수 없습니다.
- 검색 모드(IMDB, 쿼리 등)를 혼합하면 품질이 낮은 결과가 발생할 수 있습니다.
- 인덱서별 범주(\>= 100000)를 사용할 수 없습니다.
- 느린 인덱서는 전체 결과를 느리게 만듭니다.
- 총 결과는 1000개로 제한됩니다.
- 관련 없는 결과
- 누락된 결과

각 인덱서를 개별적으로 추가하면 인덱서별로 범주를 세밀하게 조정할 수 있으므로 `/all` 엔드포인트를 사용하는 경우 잘못된 범주가 일부 트래커에서 오류를 발생시킬 수 있는 문제가 발생할 수 있습니다. Sonarr에서 각 인덱서는 페이지네이션이 지원되는 경우 1000개의 결과 또는 그렇지 않은 경우 100개의 결과로 제한됩니다. 따라서 Jackett에 더 많은 트래커를 추가할수록 결과가 잘릴 가능성이 더 커집니다. 마지막으로 `/all`에서 *하나*의 트래커가 오류를 반환하면 해당 트래커가 비활성화되어 더 이상 결과를 얻을 수 없게 됩니다.

### NZBHydra2를 단일 항목으로 사용

여러 인덱서(즉, NZBHydra2에 많은 인덱서가 있는 경우)에 대해 Sonarr에 1개의 NZBHydra2 항목을 사용하는 것은 Jackett의 `/all` 엔드포인트와 동일한 문제가 있습니다.

### 인덱서가 검색되지 않음

- 인덱서가 검색되지 않는 경우, 인덱서가 쿼리 유형을 지원하지 않기 때문일 가능성이 높습니다. 가장 일반적인 경우는 Nyaa가 쿼리 검색만 지원하고 시즌/에피소드 검색을 지원하지 않습니다. 추적 로그는 재부팅 후 첫 번째 검색에서 인덱서가 가지거나 가지지 않는 기능을 나타냅니다.

### Jackett 수동 검색에서 더 많은 결과 찾기

- [이 FAQ 항목](/sonarr/faq#jackett-shows-more-results-than-sonarr-when-manually-searching)을 참조하세요.

### 릴리스 프로필이 존중되지 않음

프로필이 무시되는 것처럼 보일 수 있는 몇 가지 원인이 있습니다. 가장 일반적인 원인 중 하나는 릴리스 프로필의 인덱서 제한과 관련이 있습니다. 인덱서는 데이터와 함께 저장되지 않으므로 라이브러리의 미디어에 대한 `preferred word` 점수는 모두 0입니다. 그러나 "RSS" 및 검색 중에는 적용됩니다. `must contain` 또는 `must-not` contain 제한은 해당 인덱서에만 적용되며 다른 것은 공정한 게임입니다. 이로 인해 릴리스 프로필이 무시되거나 업그레이드 루프가 발생할 수 있습니다.

### 나열되지 않은 문제

일반적인 권한 및 네트워킹 문제 해결 명령에 대해서는 [가이드](/permissions-and-networking)를 참조하세요. 그렇지 않으면 Discord의 지원 팀과 상의하세요. 이것이 일반적인 문제일 수 있는 경우 위키에 추가하도록 제안하세요.

## 오류

인덱서를 추가할 때 발생할 수 있는 일부 일반적인 오류입니다.

### The underlying connection was closed: An unexpected error occurred on a send

이는 인덱서가 현재 .NET 버전에서 지원되지 않는 SSL 프로토콜을 사용하는 경우 발생합니다. [Sonarr => System => Status](/sonarr/system#status)에서 확인할 수 있습니다.

### The request timed out

Sonarr이 인덱서로부터 응답을 받지 못하고 있는 것입니다.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

이는 다음과 같은 이유로 발생할 수도 있습니다:

- VPN이 잘못 구성되었거나 사용 중인 경우
- 프록시가 잘못 구성되었거나 사용 중인 경우
- 로컬 DNS 문제 - 다른 DNS 공급자로 변경해 보세요.
- 로컬 IPv6 문제 - 일반적으로 IPv6는 활성화되어 있지만 기능하지 않습니다.
- Privoxy를 사용하고 잘못 구성된 경우

### 나열되지 않은 문제

일반적인 권한 및 네트워킹 문제 해결 명령에 대해서는 [가이드](/permissions-and-networking)를 참조하세요. 그렇지 않으면 Discord의 지원 팀과 상의하세요. 이것이 일반적인 문제일 수 있는 경우 위키에 추가하도록 제안하세요.