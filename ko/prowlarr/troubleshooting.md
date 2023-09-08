# 문제 해결하기

도움이 필요하신가요? 괜찮아요, 때로는 모두가 도움이 필요합니다. 실시간 도움을 받으려면 다음 채팅을 통해 도움을 받을 수 있습니다.

- [<i class="fab fa-discord"></i>&emsp;Discord *공식 Prowlarr Discord*](https://prowlarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *공식 Prowlarr Subreddit*](https://reddit.com/r/prowlarr)
{.links-list}

하지만 질문을 하기 전에 도움을 요청하는 방법이 최선인지 확인해주세요. 문제를 명확하게 설명하고 OS/배포판, .NET 버전, Prowlarr 버전, 다운로드 클라이언트 및 해당 버전과 같은 설정과 함께 설정에 대해 간단히 설명해주세요. **[Docker](https://www.docker.com/)를 사용하는 경우 [Docker 가이드](/docker-guide)를 먼저 실행하여 일반적이고 빈번한 경로/권한 문제를 해결하세요. 그렇지 않으면 [docker compose](/docker-guide#docker-compose)를 준비해주세요. [Docker Compose 생성 방법](https://trash-guides.info/compose)** 이미 시도한 것, 살펴본 것에 대해 알려주세요. 문제를 재현하고 로깅을 추적 수준으로 높이고, 문제를 재현한 후에 관련된 컨텍스트를 pastebin에 올리고 해당 링크를 게시물에 포함시켜주세요. 문제를 강조하기 위해 스크린샷도 포함시킬 수 있습니다.

우리가 알면 도움을 드리기가 더 쉽습니다.

# 로깅 및 로그 파일

[Indexer, Application 및 Download Client 문제 일반적인 문제](#indexer-application-and-download-client-issues)도 검토하는 것이 좋습니다.

> 개발이나 디버깅을 위해 인덱서 응답을 제공하라는 요청이 있을 경우 이 파란색 섹션을 계속 읽으세요. 그렇지 않으면 아래 단계로 이동하세요. 인덱서 응답을 디버깅하기 위해서는 Prowlarr의 `settings/development` (숨겨진 페이지)으로 이동하여 개선된 인덱서 로깅을 일시적으로 활성화하는 것이 도움이 될 수 있습니다. 항상 켜두지는 마세요.
{.is-info}

디버그 로그를 요청받으면 로그에 `debug`가 포함되어 있고 추적 로그를 요청받으면 로그에 `trace`가 포함되어 있습니다. 제공하는 로그에 이러한 단어가 포함되어 있지 않으면 요청받은 로그가 아닙니다.

- 요청받지 않은 한 로그 파일 전체를 공유하지 마세요.
- 로그를 직접 Discord에 업로드하거나 텍스트 벽으로 붙여넣지 마세요. 요청되지 않은 경우에는 아래에 나열된 서비스를 통해 텍스트로 공유하세요.

좋은 로그를 제공하기 위한 팁:

> RSS 새로 고침과 같은 스팸이 많은 작업이 실행되고 있지 않은지 확인하세요.
{.is-warning}

1. [로그 추적 수준을 Trace로 변경하세요 (설정 => 일반 => 로그 수준 또는 구성 파일 편집)](#tracedebug-logs)
2. [로그 지우기 (시스템 => 로그 => 로그 지우기 또는 로그 폴더의 모든 로그 삭제)](#clearing-logs)
3. 문제 재현하기 (문제가 발생하는 작업을 다시 수행하세요)
4. UI나 로그 파일의 [trace 로그 파일 (Lidarr.trace.txt)](#standard-logs-location)에서 관련 컨텍스트를 찾으세요.
5. 문제가 발생하기 전과 후의 큰 청크를 복사하세요.
6. [Gist](https://gist.github.com/), [0bin (**반드시 색상 지정 비활성화**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu의 Pastebin](https://pastebin.ubuntu.com/) 또는 유사한 사이트(아래에서 제외된 사이트는 제외)를 사용하여 위에서 복사한 로그를 공유하세요.

**경고:**
- **[pastebin.com](https://pastebin.com)은 로그를 차단하는 필터가 있으므로 사용하지 마세요.
- [pastebin.pl](https://pastebin.pl)은 사이트에 자주 접속할 수 없습니다.
- [JustPasteIt](https://justpaste.it/)은 로그 검토를 지원하지 않는 사이트입니다.
- 로그를 파일로 업로드하지 마세요.
- 로그를 Google Drive, Dropbox 또는 기타 사이트에 업로드하고 공유하지 마세요.
- 로그를 아카이브(압축, tar (tarball), 7zip 등)하지 마세요.
- 콘솔 출력, 도커 컨테이너 출력 또는 응용 프로그램 로그가 아닌 다른 것을 공유하지 마세요.

**중요한 참고 사항:**
- [0bin](https://0bin.net/)을 사용할 때 색상 지정을 비활성화하고 읽은 후에도 삭제하지 마세요.

- 또는 이전 로그 파일에서 특정 항목을 찾으려면 N++을 사용할 수 있습니다. Notepad++의 "파일에서 찾기" 기능을 사용하여 필요한 이전 로그 파일을 검색할 수 있습니다.
- **Unix 전용:** 특정 항목을 찾으려면 grep을 사용할 수도 있습니다. 예를 들어 영화/TV 프로그램/도서/노래/인덱서 "Shooter"에 대한 정보를 찾으려면 다음 명령을 실행할 수 있습니다. `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` [Appdata 디렉토리](/prowlarr/appdata-directory)가 홈 폴더에 있는 경우 다음과 같이 실행할 수 있습니다. `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * 각 플래그의 기능은 다음과 같습니다.
    * -i: 대소문자 구분 안 함
    * -n: 줄 번호 표시
    *  -r: 경로의 모든 파일을 재귀적으로 확인
    * -C: 찾은 줄 앞과 뒤의 줄 수 제공
    * -e: 검색할 패턴

```

## 표준 로그 위치

로그 파일은 Prowlarr의 [Appdata 디렉토리](/prowlarr/appdata-directory)의 logs/ 폴더에 있습니다. 또한 UI에서 System => Logs => Files에서 로그 파일에 액세스할 수도 있습니다.

> 참고: UI의 로그("이벤트") 테이블은 로그 파일과 동일하지 않으며 유용하지 않습니다. 로그를 요청받은 경우 로그 파일에서 복사/붙여넣기를 해주세요.
{.is-info}

## 업데이트 로그 위치

업데이트 로그 파일은 Prowlarr의 [Appdata 디렉토리](/prowlarr/appdata-directory)의 UpdateLogs/ 폴더에 있습니다.

## 로그 공유

로그는 포럼이나 Reddit 게시물의 일부로는 길고 읽기 어려울 수 있으며 Discord에서는 스팸으로 처리되므로 [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) 또는 유사한 pastebin 사이트를 사용해주세요. 일반적으로 전체 파일이 필요하지 않고, 문제/오류 전후의 적절한 컨텍스트만 필요합니다. RSS 동기화나 라이브러리 새로 고침과 같은 스팸이 많은 작업이 완료될 때까지 기다리는 것을 잊지 마세요.

## 추적/디버그 로그

로그 수준은 Settings => General => Logging에서 변경할 수 있습니다. Prowlarr를 다시 시작할 필요는 없습니다. 이 변경은 로그 파일에만 영향을 미치며 로깅 데이터베이스에는 영향을 미치지 않습니다. 최신 디버그/추적 로그 파일의 이름은 각각 `prowlarr.debug.txt` 및 `prowlarr.trace.txt`입니다.

UI에서 로깅 수준을 설정할 수 없는 경우 AppData 디렉토리의 config.xml을 편집하여 LogLevel 값을 Info 대신 Debug 또는 Trace로 설정할 수 있습니다.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## 로그 지우기

UI에서 로그 파일과 로그 데이터베이스를 직접 지울 수 있습니다. `System` => `Logs` => `Files` 및 `System` => `Logs` => `Delete` (휴지통 아이콘)에서 지울 수 있습니다.

# 여러 개의 로그 파일

Prowlarr는 각각 1MB로 제한된 롤링 로그 파일을 사용합니다. 현재 로그 파일은 항상 Prowlarr.txt이며, 다른 파일 중 Prowlarr.0.txt가 다음으로 최신 파일입니다(숫자가 높을수록 오래된 파일입니다). 이 로그 파일에는 `fatal`, `error`, `warn`, `info` 항목이 포함됩니다.

디버그 로그 수준이 활성화되어 있는 경우 추가적인 `prowlarr.debug.txt` 롤링 로그 파일이 있을 수 있습니다. 이 로그 파일에는 `fatal`, `error`, `warn`, `info`, `debug` 항목이 포함됩니다. 일반적으로 40시간 동안의 내용을 포함합니다.

추적 로그 수준이 활성화되어 있는 경우 추가적인 `prowlarr.trace.txt` 롤링 로그 파일이 있을 수 있습니다. 이 로그 파일에는 `fatal`, `error`, `warn`, `info`, `debug`, `trace` 항목이 포함됩니다. 추적 로그는 대부분 몇 시간 이내에만, 때로는 몇 분 이내에만 유효합니다.

# 실패한 업데이트에서 복구하기

업그레이드할 때 문제가 발생하지 않도록 최선을 다하지만, 발생한 경우 이 가이드를 따라 설치를 복구할 수 있습니다.

## 문제 확인하기

- 업데이트 후 애플리케이션이 시작되지 않는 경우 가장 먼저 확인해야 할 곳은 [업데이트 로그](#update-logs-location)를 검토하고 업데이트가 성공적으로 완료되었는지 확인하는 것입니다. 그래도 문제가 없다면 다음 단계로 넘어가기 전에 일반적인 애플리케이션 로그 파일을 살펴보세요. [Logging](/prowlarr/settings#logging) 및 [Log Files](/prowlarr/system#log-files)를 사용하여 로그 파일을 찾고 로그 수준을 높이세요.
- 가장 자주 발생하는 문제는 앱이 설치된 시스템이 업그레이드 중에 `/tmp` 디렉토리를 조작하고 업그레이드 중에 중요한 \*Arr 파일을 삭제하여 업그레이드와 롤백 모두 실패하는 경우입니다. 이 경우, 기존에 손상된 설치에 덮어쓰기로 다시 설치하면 됩니다.

### 마이그레이션 문제

- 마이그레이션 오류는 동일하지 않을 수 있지만, 다음은 예시입니다:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### 권한 문제

- 권한 문제는 애플리케이션이 관련 임시 폴더와/또는 앱 바이너리 폴더에 액세스할 수 없을 때 발생합니다. 애플리케이션이 실행되는 사용자/그룹이 적절한 액세스 권한을 갖도록 권한을 수정하세요.

- Synology 사용자는 Synology 버그 `Access to the path '/proc/{some number}/maps is denied`에 직면할 수 있습니다.

- Synology 사용자는 특정 NAS에서 `/tmp`에 공간이 부족한 경우가 있습니다. 앱을 위한 다른 `/tmp` 경로를 지정해야 합니다. 이에 대한 도움은 SynoCommunity나 다른 Synology 지원 채널에서 받을 수 있습니다.

## 문제 해결하기

마이그레이션 문제의 경우 즉시 할 수 있는 것은 많지 않습니다. 문제가 특정한 경우(또는 아직 게시물이 없는 경우) [reddit](https://reddit.com/r/prowlarr)에 게시하거나 [discord](https://prowlarr.com/discord)에 참여하세요. 동일한 문제가 있는 경우 안심하세요. 우리는 이 문제에 대해 작업 중입니다.

> 안정 버전에서 `nightly`의 데이터베이스를 사용하지 않도록 주의하세요. 브랜치 변경은 권장되지 않습니다.{.is-info}

### 권한 문제

- 권한을 수정하여 애플리케이션이 `/tmp`와 애플리케이션의 설치 디렉토리에 액세스(읽기 및 쓰기)할 수 있도록 하세요.

- Synology 사용자는 `/proc/###/maps`로 인해 Sonarr이나 다른 \*Arr 애플리케이션을 중지하고 업데이트해야 할 수 있습니다. 이는 SynoCommunity 패키지의 문제입니다.

### 수동 업그레이드

웹사이트에서 최신 릴리스를 다운로드하세요.

업데이트(.exe)를 설치하거나 내용을 추출(.zip)하여 기존 설치 위에 덮어쓰고 일반적으로 Prowlarr를 실행하세요.

# NGINX 오류

Prowlarr 설정에서 다음 줄이 필요합니다.

`proxy_set_header Host $host;`

다른 `proxy_set_header`가 있는 경우 위의 줄로 대체해야 합니다.

# 인덱서, 애플리케이션 및 다운로드 클라이언트 문제

- 기본적으로 Prowlarr는 인덱서와 통신할 수 있어야 합니다.
- 애플리케이션 동기화를 사용하는 경우 Prowlarr는 애플리케이션과 통신할 수 있어야 하며, 애플리케이션은 Prowlarr와 통신할 수 있어야 합니다.
- Prowlarr에 수동으로 다운로드할 다운로드 클라이언트가 있는 경우 Prowlarr는 해당 다운로드 클라이언트와 통신할 수 있어야 합니다.

> 인덱서 ID 0을 쿼리하는 로그: 0 ID는 인덱서가 작동하지 않아도 Prowlarr에 다시 호출하고 연결할 수 있는 일반 테스트 엔드포인트입니다.
{.is-info}

일반적인 원인은 다음과 같습니다.

## 프레임 크기를 결정할 수 없거나 손상된 프레임을 수신했습니다

`Cannot determine the frame size or a corrupted frame was received.`

Prowlarr가 사이트에 연결하는 데 보안 문제가 발생했습니다.

일반적으로 다음과 같은 이유로 발생합니다.

- 로컬 DNS 문제 - 다른 DNS 공급자로 변경해보세요.

## 연결 시간 초과

`The request timed out`

Prowlarr가 클라이언트로부터 응답을 받지 못하고 있습니다. [일반적인 네트워크 및 권한 문제 해결 가이드](/permissions-and-networking)를 참조하세요.

일반적으로 다음과 같은 이유로 발생합니다.

- 잘못 구성된 VPN 또는 VPN 사용
- 잘못 구성된 프록시 또는 프록시 사용
- 로컬 DNS 문제 - 다른 DNS 공급자로 변경해보세요.
- 로컬 IPv6 문제 - 일반적으로 IPv6는 활성화되어 있지만 기능하지 않습니다.
- Privoxy 사용

## Sonarr HTTP 404 오류

- 이는 Sonarr의 종료 지원 (EOL) 버전에서 v3 API 엔드포인트가 없어서 발생하는 경우입니다.
- Prowlarr는 Sonarr v2를 지원하지 않습니다.
- Prowlarr는 Sonarr v3만 지원합니다.

## \*Arr HTTP 400 오류

- 이 FAQ 항목을 참조하세요: [Prowlarr가 X 인덱서를 앱에 동기화하지 않음](/prowlarr/faq#prowlarr-will-not-sync-x-indexer-to-app)

## 503 HTTP Service Unavailable

- 이는 트래커가 Cloudflare를 통해 차단되어 있고 [FlareSolverr](https://github.com/FlareSolverr/FlareSolverr)가 필요한 경우입니다.

## 잘못된 토렌트

- URL과 Prowlarr이 사용한 변수를 통해 링크를 다운로드해 보세요.
- Prowlarr을 통해 프록시된 토렌트를 다운로드해 보세요 (즉, 파일을 가져온 앱이 사용한 prowlarr 링크를 사용하세요).
- 인덱서에 대한 쿠키나 기타 자격 증명이 만료되지 않았고 유효한지 확인하세요.
- 만약 문제가 Prowlarr에서 발생한 것이라면 버그 보고서를 제출해 주세요.

## 인덱서와 트래커 검색

- [Lidarr 검색 및 인덱서](/lidarr/troubleshooting#searches-indexers-and-trackers)
- [Radarr 검색 및 인덱서](/radarr/troubleshooting#searches-indexers-and-trackers)
- [Readarr 검색 및 인덱서](/readarr/troubleshooting#searches-indexers-and-trackers)
- [Sonarr 검색 및 인덱서](/sonarr/troubleshooting#searches-indexers-and-trackers)
{.links-list}