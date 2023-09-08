# Lidarr FAQ

## Lidarr가 어떻게 작동하나요?

- Lidarr는 RSS 피드를 활용하여 새로운 릴리스와 이전에 릴리스된 릴리스를 자동으로 가져옵니다. RSS 피드는 사이트에서 최신 릴리스를 나타내며, 일반적으로 50개에서 100개의 릴리스를 포함하고 있습니다. RSS 피드에는 요청한 미디어를 팔로우하지 않는 미디어의 릴리스도 포함되어 있습니다. 디버그 로그를 확인하면 이러한 릴리스가 처리되는 것을 볼 수 있으며, 이는 완전히 정상적인 동작입니다.
- Lidarr는 RSS 동기화 간격에 대해 최소 10분, 최대 2시간을 요구합니다. 대부분의 인덱서에서는 15분을 권장하지만, 일부 인덱서는 더 낮은 간격을 허용하며 2시간은 Lidarr이 릴리스를 놓치지 않도록 충분히 자주 확인하도록 합니다(다른 인덱서에서 RSS 피드를 자주 요청하고 동일한 릴리스를 반복해서 처리하지 않도록 도와줍니다). 일부 인덱서는 10분보다 더 자주 RSS 동기화를 수행할 수 있도록 허용하며, 이러한 경우에는 Lidarr의 릴리스 푸시 API 엔드포인트를 사용하여 IRC 알림 채널과 함께 사용하여 릴리스를 Lidarr로 푸시하여 실시간으로 처리할 수 있으며, 인덱서와 Lidarr에 덜 부하를 주게 됩니다.

## Lidarr는 어떻게 릴리스를 찾나요?

- Lidarr는 주기적으로 누락된 앨범 파일이나 품질 목표를 충족하지 못한 앨범 파일을 검색하지 않습니다. 대신, 인덱서와 트래커에서 최근에 게시된 모든 릴리스를 자주 쿼리한 다음, 누락된 릴리스나 업그레이드해야 할 릴리스 목록과 비교합니다. 일치하는 항목은 다운로드됩니다. 이를 통해 Lidarr은 하루에 24-100개의 쿼리로 어떤 크기의 라이브러리든 커버할 수 있습니다(15-60분의 RSS 간격). 이를 이해하면, Lidarr은 오직 ''미래''만 커버한다는 것을 알 수 있습니다.
- 그렇다면 현재와 과거를 어떻게 처리해야 할까요? 앨범을 추가할 때는 올바른 경로, 프로필 및 모니터링 상태를 설정한 다음, 누락된 앨범 검색란을 선택하면 됩니다. 앨범이 아직 출시되지 않았다면 검색을 시작할 필요가 없습니다.
- 다른 말로 하면, Lidarr은 인덱서에 새로 업로드된 릴리스만 찾을 수 있습니다. 과거에 업로드된 원하는 릴리스를 찾으려고 노력하지는 않습니다.
- 이미 앨범을 추가했지만 이제 검색하려고 하는 경우 몇 가지 선택 사항이 있습니다. 앨범 페이지로 이동하여 검색 버튼을 사용하면 검색이 수행되고 자동으로 하나를 선택합니다. 검색 탭을 사용하여 ''모든'' 결과를 확인하고 원하는 결과를 수동으로 선택할 수도 있습니다. 또는 `Missing`, `Wanted`, 또는 `Cut-off Unmet` 필터를 사용할 수도 있습니다.
- Lidarr이 오랜 기간 동안 오프라인이었을 경우, Lidarr은 릴리스를 놓치지 않기 위해 마지막으로 처리한 릴리스를 찾기 위해 페이지를 뒤로 이동하려고 시도합니다. 인덱서가 페이징을 지원하고 너무 오랜 시간이 지나지 않았다면 Lidarr은 놓칠 수 있는 릴리스를 처리하고 누락된 릴리스를 검색할 필요가 없게 됩니다.

## 강제 인증

Lidarr의 UI에 외부 네트워크에서 액세스할 수 있도록 노출되어 있다면, UI에 액세스하기 위해 인증 방법을 사용해야 합니다. 이는 트래커와 인덱서에서 점점 더 필요해지고 있습니다.

Lidarr v2부터 인증은 필수입니다.

### 인증 방법

- `Basic` (브라우저 팝업) - 이 옵션은 Lidarr에 액세스할 때 작은 팝업이 표시되어 사용자 이름과 비밀번호를 입력할 수 있게 합니다.
- `Forms` (로그인 페이지) - 이 옵션은 다른 웹 사이트와 유사한 로그인 화면을 제공하여 Lidarr에 로그인할 수 있도록 합니다.
- `External` - 구성 파일을 통해 구성 가능
  - Authelia, Authetik, NGINX 기본 인증 등과 같은 **외부 인증**을 사용하는 경우, 앱을 종료한 다음 [구성 파일](/lidarr/appdata-directory)에서 `<AuthenticationMethod>External</AuthenticationMethod>`를 설정한 후 앱을 다시 시작하면 두 번의 인증이 필요하지 않도록 설정할 수 있습니다. **파일에 여러 개의 `AuthenticationMethod` 항목을 지정할 수 없으며, 파일에서 가장 위에 있는 값만 사용됩니다.**

### 인증 필요 여부

- 앱을 외부에 노출하지 않거나 로컬(예: LAN) 액세스에 대해 인증이 필요하지 않으려면 설정 => 일반 보안 => 인증 필요에서 `Disabled For Local Addresses`로 변경하십시오.
  - 이에 해당하는 구성 파일은 `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`입니다.

## 가능한 다운로드는 어떻게 비교되나요?

> 일반적으로 품질이 우선합니다. 품질을 주요 우선 순위로 설정하지 않으려면 품질을 병합할 수 있습니다. [TRaSH의 가이드](https://trash-guides.info/merge-quality)를 참조하세요.***
{.is-info}

- 현재 로직은 [여기에서 찾을 수 있습니다](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs).

- 2022-01-23 기준 로직은 다음과 같습니다:

1. 품질
1. 우선 순위 단어 점수
1. 프로토콜 (해당 지연 프로필에서 구성된대로)
1. 인덱서 우선 순위
1. 시드/피어 (토렌트인 경우)
1. 앨범 수
1. 연령 (유즈넷인 경우)
1. 크기

## Ubuntu 22.04로 업데이트한 후 Lidarr가 작동하지 않습니다.

- Lidarr v0.8은 Ubuntu 22.04와 호환되지 않으며 지원되지 않습니다.
- Ubuntu 22.04는 Lidarr v1만 지원합니다.
- [브랜치와 버전에 대한 FAQ 항목을 참조하세요](#how-do-i-update-lidarr).

## 새로운 릴리스나 아티스트를 Lidarr에 추가할 수 없는 이유는 무엇인가요?

- 해당 릴리스가 MusicBrainz에서 `unknown` 유형일 가능성이 높습니다.

## 다양한 아티스트 앨범을 추가할 수 없는 이유는 무엇인가요?

- Musicbrainz의 Various Artists 및 기타 메타 아티스트는 제공하는 항목의 수 때문입니다.

## Lidarr는 스튜디오 앨범만 표시하고 싱글이나 EP를 어떻게 찾을 수 있나요?

- Lidarr는 기본적으로 각 아티스트의 스튜디오 앨범만 가져옵니다. 그러나 Metadata 프로필을 사용하여 아티스트별로 또는 전체 라이브러리별로 앨범 유형을 확장할 수 있습니다.

## 앨범만 추가할 수 있나요?

- 현재는 불가능합니다.

## 개별 트랙을 다운로드할 수 있나요?

- Lidarr은 전체 릴리스를 검색하고 다운로드하는 방식으로 작동하기 때문에 개별 트랙은 아티스트가 싱글로 발매한 경우에만 다운로드할 수 있습니다.

## 왜 아티스트 X가 검색에 나타나지 않나요?

- 검색은 아직 진행 중인 작업입니다. 검색에 나타나지 않는 아티스트는 `lidarr:mbid`를 검색하여 아티스트의 Musicbrainz ID를 찾아 추가할 수 있습니다.

## Lidarr가 트랙이 너무 많은 앨범을 매칭했습니다. 앨범을 올바른 릴리스로 변경할 수 있나요?

- 앨범 세부 정보 페이지를 열고 상단 탐색에서 편집 아이콘을 선택하면 해당 앨범과 연결된 모든 릴리스의 드롭다운 목록을 찾을 수 있습니다.

## Lidarr에서 릴리스를 찾을 수 없지만 MusicBrainz에는 있는 경우

- 이는 릴리스가 `unknown` 릴리스 상태를 가지고 있기 때문일 가능성이 높습니다. MusicBrainz를 업데이트하세요.

## Lidarr와 MusicBrainz 데이터베이스는 얼마나 자주 동기화되나요?

- 매 시간 정각 5분마다 동기화됩니다.

## 누락된 아티스트 이미지를 어떻게 추가할 수 있나요?

- fanart.tv에 이미지를 추가하고 캐시를 통해 약 7일 이상 기다린 다음 메타데이터를 새로 고침하세요.

## 누락된 앨범 이미지(커버 아트)를 어떻게 얻을 수 있나요?

- musicbrainz에 커버 아트를 추가하고 약 1시간 이상 기다린 다음 캐시를 통해 새로 고침하세요.

## 아티스트를 가져오는 중에 문제가 발생했습니다. 원인은 무엇일까요?

- 아티스트 가져오기 프로세스는 아티스트 이름과 경로 위치만 가져오며, 이는 데이터베이스에 저장되어 메타데이터를 검색하고 다운로드된 콘텐츠를 동일한 위치에 저장할 수 있도록 합니다. 이를 위해 Lidarr이 실행되는 사용자 계정은 데이터 디렉토리에 대한 읽기 및 쓰기 권한이 필요합니다.

## 아티스트 폴더 이름을 어떻게 변경할 수 있나요?

{#rename-folders}

> 아티스트 경로를 이동/변경하는 경우에도 동일한 절차가 적용됩니다.
{.is-info}

1. 라이브러리
1. 대량 편집기
1. 폴더 이름을 변경하려는 아티스트 선택
1. 루트 폴더를 현재 아티스트가 있는 루트 폴더로 변경
1. "예, 파일 이동" 선택

## 원하는 목록에서 아티스트를 대량으로 삭제하는 방법은 무엇인가요?

- 대량 편집기를 사용하여 삭제하려는 아티스트를 선택한 다음 삭제하세요.

## Lidarr이 리버스 프록시 뒤에서 작동하지 않는 이유는 무엇인가요?

- Lidarr은 .NET과 새로운 웹 서버를 사용합니다. SignalR이 작동하려면 UI 버튼이 작동하고 데이터베이스 변경이 적용되며 기타 항목이 필요합니다. Lidarr에 다음과 같은 추가가 필요합니다:
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;

- nginx 문서에서 제안하는대로 `proxy_set_header Connection "Upgrade";`를 포함하지 않도록 주의하세요. `이는 작동하지 않습니다`
- [ASP.NET Core 문제를 참조하세요](https://github.com/aspnet/AspNetCore/issues/17081)
- Cloudflare와 같은 CDN을 사용하는 경우 웹소켓이 활성화되어 웹소켓 연결을 허용해야 합니다.

## Lidarr을 어떻게 업데이트할 수 있나요?

- 설정으로 이동한 다음 일반 탭으로 이동하여 고급 설정을 표시하세요(저장 버튼 옆의 토글을 사용하세요).

1. 업데이트 섹션에서 브랜치 이름을 `master` 또는 `develop`로 변경하세요.
1. 저장

*이렇게 하면 해당 브랜치의 비트가 즉시 설치되지는 않으며, 다음 업데이트 중에 설치됩니다.*

- `master` - ![현재 마스터/안정 버전](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) - (기본/안정): 개발 및 nightly 브랜치에서 사용자들에 의해 테스트되었으며 주요한 문제가 없는 것으로 알려져 있습니다. 이 버전은 대략 한 달에 한 번 업데이트를 받습니다. GitHub에서 이것은 `master` 브랜치입니다.

- `develop` - ![현재 개발/베타 버전](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) - (베타): 이것은 테스트 엣지입니다. nightly에서 테스트된 후 즉시 릴리스되어 즉각적인 문제가 없음을 보장합니다. 새로운 기능과 버그 수정은 nightly 이후에 먼저 여기에서 릴리스됩니다. 이 버전은 반정도 안정적이지만 여전히 `베타`입니다. 이 버전은 주간 또는 2주에 한 번 업데이트를 받습니다.

> **경고: `develop` 브랜치로 전환한 후에는 `master`로 돌아갈 수 없을 수도 있습니다.** GitHub에서 이것은 특정 시점에서 `develop` 브랜치의 스냅샷입니다.
{.is-warning}

- `nightly` - ![현재 nightly/불안정 버전](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) - (알파/불안정): 이것은 최신 버전입니다. 코드가 커밋되고 모든 자동화된 테스트를 통과한 즉시 릴리스됩니다. 이 빌드는 아직 저희나 다른 사용자들에 의해 사용된 적이 없을 수도 있습니다. 경우에 따라 실행되지 않을 수도 있습니다. 이 브랜치는 고급 사용자에게만 권장됩니다. 이 브랜치에서는 문제와 자체 조사가 예상됩니다. ***이 브랜치는 실패한 업데이트를 복구하기 위해 손을 더럽힐 준비가 되어 있는지 알고 있는 경우에만 사용하십시오.*** 이 버전은 즉시 업데이트됩니다.

> **경고: `nightly`로 전환한 후에는 `master`로 돌아갈 수 없을 수도 있습니다.** GitHub에서 이것은 `develop` 브랜치입니다.
{.is-danger}

- 참고: Docker를 통해 설치한 경우 컨테이너 태그 끝에 `:release`, `:latest`, `:testing` 또는 `:develop`를 추가하십시오. `nightly` 브랜치는 명시적으로 나열되지 않습니다.

|                                                                    | `master` (안정) ![현재 마스터/최신](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) | `develop` (베타) ![현재 개발/베타](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) | `nightly` (알파) ![현재 nightly/알파](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/lidarr)                       | `release`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-lidarr) | `latest`                                                                                                                                                                                                              | `develop`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |

### Docker 컨테이너 내에서 Lidarr를 업데이트할 수 있나요?

- *기술적으로는 가능합니다.* **하지만 절대로 하지 말아야 합니다.** 이것은 Docker의 주요 철학입니다. 최신 `nightly`로 설치를 업그레이드하고 Docker 컨테이너 자체를 업데이트하면(이전 버전으로 다운그레이드될 수도 있음) 데이터베이스 문제가 발생할 수 있습니다.

### 더 최신 버전 설치하기

#### Native

1. 시스템으로 이동한 다음 업데이트 탭으로 이동합니다.
1. 아직 설치되지 않은 더 최신 버전은 옆에 업데이트 버튼이 표시됩니다. 해당 버튼을 클릭하여 업데이트를 설치합니다.

#### Docker

1. 태그를 다시 가져오고 컨테이너를 업데이트합니다.

## `nightly`에서 `develop`로 전환할 수 있나요?

## 브랜치 간에 전환할 수 있나요?

- 버전이 동일한 경우 전환할 수 있지만, 그렇지 않은 경우 해당 빌드에 대해 `nightly`에서 `master`로, `nightly`에서 `develop`로 또는 `develop`에서 `master`로 전환할 수 있는지 개발 팀과 확인하십시오.
- 이 지침을 따르지 않으면 Lidarr가 사용할 수 없거나 오류가 발생할 수 있습니다. 경고했습니다.
  - 가장 일반적인 오류는 `Error parsing column 45 (Language=31 - Int64)` 또는 누락된 열 또는 테이블에 대한 기타 유사한 데이터베이스 오류입니다.

## 오류가 발생했습니다: 데이터베이스 디스크 이미지가 손상되었습니다

- **`Error creating log database` 오류는 logs.db에 문제가 있는 것을 나타냅니다.**
  - 이는 데이터베이스 이름이 logs.db이며, 명령 기록 및 업데이트 설치 기록, 그리고 Info, Warn 및 Error 항목과 같은 중요하지 않은 정보를 포함합니다.
- **`Error creating main database` 또는 특정 데이터베이스가 지정되지 않은 일반적인 `database disk image is malformed` 오류는 lidarr.db에 문제가 있는 것을 나타냅니다.**
  - 아래의 단계를 계속 진행하십시오.
- 이는 Lidarr의 대부분의 정보를 저장하는 SQLite 데이터베이스가 손상되었음을 의미합니다. 기존 데이터베이스를 복구하려고 시도하거나 백업을 복구하려고 시도하거나, 모든 것이 실패하면 새로운 데이터베이스로 처음부터 시작해야 합니다.
- 이 오류는 데이터베이스 파일이 \*Arr가 실행되는 사용자/그룹에 의해 쓰기 가능하지 않을 때 발생할 수 있습니다. 이러한 권한 문제는 새로 설치한 경우, 새 서버로 마이그레이션한 경우, 최근에 appdata 디렉토리 권한을 수정한 경우 또는 \*Arr가 실행되는 사용자와 그룹을 변경한 경우에만 문제가 될 수 있습니다.
- 가장 좋은 옵션은 [백업에서 복원을 시도하는 것입니다](#lidarr을-백업/복원하는-방법은-무엇인가요)
- 데이터베이스를 복구해 볼 수도 있습니다. 이 문제가 업데이트 후에 발생한 경우에는 일반적으로 유일한 옵션입니다. [sqlite3 `.recover` 명령](/useful-tools#recovering-a-corrupt-db)을 시도해 보십시오.
  - sqlite에 `.recover`가 없거나 GUI(예: Windows) 친화적인 방법을 원하는 경우 [이 위키의 지침](/useful-tools#recovering-a-corrupt-db-ui)을 따르십시오.
- 데이터베이스 오류의 또 다른 가능한 원인은 데이터베이스를 네트워크 드라이브(nfs 또는 smb 또는 기타 로컬이 아닌 드라이브)에 위치시키는 경우입니다. **SQLite는 데이터와 응용 프로그램이 동일한 컴퓨터에 공존하는 상황을 위해 설계되었습니다.** 따라서 \*Arr AppData 폴더(/config mount for docker)는 로컬 스토리지에 있어야 합니다. [SQLite와 네트워크 드라이브는 함께 작동하지 않으며 일부 경우에는 손상된 데이터베이스를 야기할 수 있습니다](https://www.sqlite.org/draft/useovernet.html).
- mergerFS를 사용하는 경우 SQLite가 mmap을 사용하므로 `direct_io`를 제거해야 합니다. 이에 대한 자세한 내용은 mergerFS [문서](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)를 참조하십시오.

## Lidarr를 백업/복원하는 방법은 무엇인가요?

### Lidarr 백업

#### 내장된 백업 사용

- Lidarr UI에서 System => Backup으로 이동합니다.
- Backup 버튼을 클릭합니다.
- 백업이 생성된 후 zip 파일을 다운로드하여 안전한 위치에 보관합니다.

#### 파일 시스템 직접 사용

- Lidarr의 AppData 디렉토리 위치를 찾습니다.
  - Lidarr UI에서 System => About으로 이동합니다.
  - [Lidarr Appdata 디렉토리](/lidarr/appdata-directory)
- Lidarr을 중지합니다. 이렇게 하면 데이터베이스가 손상되지 않습니다.
- 내용물을 안전한 위치로 복사합니다.

### 백업에서 복원

> 서로 다른 경로를 사용하는 OS로 복원하는 것은 작동하지 않습니다(Windows에서 Linux로, Linux에서 Windows로, Windows에서 OS X로 또는 OS X에서 Windows로). OS X와 Linux 간의 이동은 `/`를 포함하는 경로를 사용하기 때문에 작동할 수 있지만, 지원되지 않습니다. 데이터베이스의 모든 경로를 수동으로 편집해야 합니다.
{.is-warning}

#### zip 백업 사용

- Lidarr을 다시 설치합니다(해당 사항이 있는 경우/이미 설치되어 있지 않은 경우).
- Lidarr을 실행합니다.
- System => Backup으로 이동합니다.
- Restore Backup을 선택합니다.
- Choose File을 선택합니다.
- 백업 zip 파일을 선택합니다.
- Restore를 선택합니다.

#### 파일 시스템 백업 사용

- Lidarr을 다시 설치합니다(해당 사항이 있는 경우/이미 설치되어 있지 않은 경우).
- Lidarr의 AppData 디렉토리 위치를 찾습니다.
  - Lidarr을 한 번 실행하고 UI에서 System => About으로 이동합니다.
  - [Lidarr Appdata 디렉토리](/lidarr/appdata-directory)
- Lidarr을 중지합니다.
- AppData 디렉토리의 내용물을 삭제합니다. **(.db-wal/.db-journal 파일이 있는 경우 포함)**
- 백업에서 복원합니다.
- Lidarr을 시작합니다.
- 경로가 동일한 경우 모든 것이 이전 상태에서 계속됩니다.

#### Synology NAS에서 파일 시스템 복원

> 주의: Synology에서 복원하려면 Linux에 대한 지식과 Synology 장치에 대한 루트 SSH 액세스가 필요합니다.
{.is-warning}

- Lidarr을 다시 설치합니다(해당 사항이 있는 경우/이미 설치되어 있지 않은 경우).
- Lidarr의 AppData 디렉토리 위치를 찾습니다.
  - Lidarr을 한 번 실행하고 UI에서 System => About으로 이동합니다.
  - [Lidarr Appdata 디렉토리](/lidarr/appdata-directory)
- Lidarr을 중지합니다.
- SSH를 통해 Synology NAS에 연결하고 root로 로그인합니다.

> 일부 설치에서 사용자가 아래 명령과 다를 수 있습니다: `chown -R sc-Lidarr:Lidarr *` {.is-info}

- 다음 명령을 실행합니다:

```shell
rm -r /usr/local/Lidarr/var/.config/Lidarr/Lidarr.db
cp -f /tmp/Lidarr_backup/* /usr/local/Lidarr/var/.config/Lidarr/
```

- 파일의 권한을 업데이트합니다:

 ```shell
cd /usr/local/Lidarr/var/.config/Lidarr/
chown -R Lidarr:users *
chmod -R 0644 *
```

- Lidarr을 시작합니다.

## Mac에서 Lidarr를 사용하다가 갑자기 작동하지 않습니다. 무슨 일이 일어난 걸까요?

- 아마도 이는 MacOS 버그로 인해 데이터베이스 중 하나가 손상되었기 때문입니다.

- 위의 데이터베이스가 손상되었습니다 항목을 참조하십시오.

- 그런 다음 실행을 시도하고 작동하는지 확인합니다. 작동하지 않으면 추가 지원이 필요합니다. [subreddit /r/lidarr](http://reddit.com/r/lidarr)에 게시하거나 [our discord](https://lidarr.audio/discord)에 참여하여 도움을 받으십시오.

## Pi와 Raspbian에서 Lidarr를 실행할 수 없습니다.

Raspbian은 Ubuntu 20.04를 기반으로 한 도커 컨테이너 실행을 지원하지 않는 너무 오래된 libseccomp2 버전을 가지고 있습니다. hotio와 LinuxServer는 둘 다 Ubuntu 20.04를 기반으로 사용합니다. `--privileged`를 사용하거나 Ubuntu에서 libseccomp2를 업데이트하거나 더 좋은 OS를 사용해야 합니다(우리는 Ubuntu 20.04 arm64를 추천합니다).

**가능한 해결 방법:**

Debian 저장소에서 백포트를 설치하여 문제를 해결했습니다. 일반적으로 백포트를 일괄 업그레이드 모드로 사용하는 것은 권장되지 않습니다. 하나의 패키지를 설치하는 것은 괜찮을 수 있지만 문제가 발생할 수도 있습니다. 따라서 무엇을 하는지 이해해야 합니다.

문제 해결 단계:

먼저 Raspbian buster를 실행 중인지 확인하십시오. `lsb_release -a`를 사용하여 확인할 수 있습니다.

> Distributor ID: Raspbian
> Description: Raspbian GNU/Linux 10 (buster)
> Release: 10
> Codename: buster

- buster를 사용하는 경우:
  - 다음 명령을 실행하여 백포트를 소스에 추가합니다.

  ```shell
   echo "deb <http://deb.debian.org/debian> buster-backports main" | sudo tee /etc/apt/sources.list.d/buster-backports.list
   ```

  - libseccomp2의 백포트를 설치합니다.

  ```shell
  sudo apt update && sudo apt-get -t buster-backports install libseccomp2
  ```

## 왜 목록 동기화 시간이 너무 오래 걸리고 변경할 수 있을까요?

목록은 "지금 추가"가 아니라 "언젠가 추가"되기를 원하는 도구입니다.

목록을 수동으로 새로 고칠 수 있으며, 스크립트를 작성하여 API를 통해 트리거하거나 Lidarr에 직접 릴리스를 추가할 수 있습니다.

이 변경은 사람들이 10분마다 목록을 업데이트하여 서버가 중단되지 않도록 하기 위한 것입니다.

## 릴리스 갱신 작업을 비활성화할 수 있을까요?

아니요, SQL 조작을 통해 비활성화해서도 안 됩니다. 릴리스 갱신 작업은 상위 Servarr 프록시를 쿼리하고 각 릴리스의 메타데이터(식별자, 캐스트, 요약, 평점, 번역, 대체 제목 등)가 Lidarr에 현재 저장된 내용과 비교하여 업데이트해야 하는지 확인합니다. 필요한 경우 해당 릴리스를 업데이트합니다.

릴리스 갱신 작업이 I/O 사용량이 많은 문제를 일으키는 것이 일반적인 불만입니다. 문제를 일으킬 수 있는 설정 중 하나는 "갱신 후 아티스트 폴더 다시 스캔"입니다. 갱신 중 디스크 I/O 사용량이 급증하는 경우 스캔 설정을 `수동`으로 변경하는 것이 좋습니다. 이 설정을 `절대로` `안 함`으로 변경하지 마십시오. 릴리스 파일을 수동으로 삭제하거나 타사 프로그램을 사용하는 경우에는 이 설정을 `안 함`으로 설정하지 마십시오.

## 왜 Lidarr가 원격 서버의 파일을 볼 수 없을까요?

- 모든 OS에서 \*Arr을 실행하는 사용자/그룹이 마운트된 드라이브에 대한 읽기 및 쓰기 액세스 권한을 갖고 있는지 확인하십시오.
- Linux의 경우:
  - NFS 마운트를 사용하는 경우 마운트에 `nolock`이 활성화되어 있는지 확인하십시오.
  - SMB 마운트를 사용하는 경우 마운트에 `nobrl`이 활성화되어 있는지 확인하십시오.
- Windows의 경우: 간단히 말해서, \*Arr이 실행 중인 사용자(서비스인 경우) 또는 해당 사용자가 액세스할 수 없는 파일 경로에 있습니다. 이는 다양한 이유로 발생할 수 있지만 가장 일반적인 이유는 \*Arr이 서비스로 실행되기 때문입니다. 아래에 설명된 문제가 발생합니다.

### Lidarr은 기본적으로 LocalService 계정에서 실행되며, 이 계정은 보호된 원격 파일 공유에 액세스할 수 없습니다.

- Lidarr 서비스를 해당 공유에 액세스할 수 있는 대상 사용자로 실행합니다.
- Windows 서버에서 관리 도구 \> 서비스 창을 엽니다.
- Lidarr 서비스를 중지합니다.
- 속성 \> 로그온 대화상자를 엽니다.
- 서비스 사용자 계정을 대상 사용자 계정으로 변경합니다.
- 시작 프로그램 폴더에서 Lidarr.exe를 실행합니다.

### 매핑된 네트워크 드라이브를 사용하는 경우(UNC 경로가 아닌 경우)

- 경로를 UNC 경로(`\\서버\공유`)로 변경합니다.
- 시작 프로그램 폴더에서 Lidarr.exe를 실행합니다.

## 도움이 필요합니다. 저는 접근할 수 없게 되었습니다.

{#help-i-have-forgotten-my-password}

인증을 비활성화하려면(잊어버린 사용자 이름이나 비밀번호를 재설정하려면) [Lidarr Appdata 디렉토리](/lidarr/appdata-directory) 내부에 있는 `config.xml`을 편집해야 합니다.

1. 텍스트 편집기에서 config.xml을 엽니다.
1. 인증 방법 라인을 찾습니다. `<AuthenticationMethod>Basic</AuthenticationMethod>` 또는 `<AuthenticationMethod>Forms</AuthenticationMethod>`일 것입니다.
1. `AuthenticationMethod` 라인을 `<AuthenticationMethod>None</AuthenticationMethod>`로 변경합니다.
1. Lidarr을 다시 시작합니다.
1. 이제 Lidarr에는 비밀번호 없이 액세스할 수 있으며, UI에서 `Settings: General`로 이동하여 사용자 이름과 비밀번호를 설정해야 합니다.

## 시작 시 브라우저가 자동으로 실행되는 것을 어떻게 멈출 수 있나요?

OS에 따라 여러 가지 방법이 있습니다.

- 일부 OS의 `Settings` => `General`에서 시작 시 브라우저를 실행하는 확인란이 있습니다.
- Lidarr을 호출할 때 인수에 `-nobrowser`(*nix) 또는 `/nobrowser`(Windows)를 추가할 수 있습니다.
- Lidarr을 중지하고 config.xml 파일을 편집하여 `<LaunchBrowser>True</LaunchBrowser>`를 `<LaunchBrowser>False</LaunchBrowser>`로 변경합니다.

## 이상한 UI 문제가 발생합니다.

- 라이브러리 페이지에 아무 내용도 나타나지 않거나 특정 보기나 정렬이 작동하지 않는 등 이상한 UI 문제가 발생하는 경우, Chrome 은 익명 창 또는 Firefox는 개인 창에서 확인해 보십시오. 그곳에서 정상적으로 작동하는 경우 특정 IP/도메인에 대한 브라우저 캐시와 쿠키를 지워 보십시오. 자세한 내용은 [캐시 및 쿠키 지우기](/useful-tools#clearing-cookies-and-local-storage) 위키 문서를 참조하십시오.

## VPN, Jackett 및 \*ARRs

- 중국, 호주 또는 남아프리카와 같은 억압적인 국가가 아닌 경우 토런트 클라이언트만 VPN 뒤에 있으면 됩니다. VPN 엔드포인트는 여러 사용자가 공유하기 때문에 각 소프트웨어가 사용하는 다양한 서비스에서 속도 제한, DDOS 보호 및 IP 차단을 경험할 수 있습니다.
- 다른 말로 하면, \*Arr(Lidarr, Prowlarr, Radarr, Readarr 및 Lidarr)을 VPN 뒤에 두면 해당 애플리케이션을 사용할 수 없는 경우가 있습니다.

> **분명히 말하자면 VPN이 \*Arr에 문제를 일으킬지 않을 때가 아니라 언제든지 문제를 일으킵니다: 이미지 제공자는 차단하고 대부분의 \*Arr 서버(업데이트, 메타데이터 등) 앞에는 클라우드플레어가 있으며, 클라우드플레어도 차단할 수 있습니다.**
{.is-warning}

- **많은 개인 트래커에서 VPN 사용 또는 액세스(예: Jackett 또는 Prowlarr 사용)로 인해 차단될 수 있습니다.**

### VPN 사용

- VPN이 필요하고 Docker를 사용하는 경우 Hotio 또는 Binhex의 Download Client + VPN 컨테이너를 사용하는 것이 좋습니다.
- VPN이 필요하지만 Docker를 사용하지 않는 경우 VPN 클라이언트는 ***반드시*** 분할 터널링을 지원해야 합니다. 이렇게 하면 필요한(다운로드 클라이언트) 앱만 VPN 뒤에 있게 됩니다.
- 트래커에 액세스하는 데 문제가 있는 경우 ISP의 DNS 서버 대신 Google이나 Cloudflare의 DNS 서버를 사용하면 해결될 수 있습니다.
- 일부 경우(예: 영국 ISP) 토런트 다운로드 클라이언트를 VPN 뒤에 두고 Jackett/Prowlarr을 다음과 같이 설정해야 할 수 있습니다:
  - Jackett을 VPN 뒤에 두고 분할 터널링이 로컬 액세스를 허용하도록 설정합니다.
  - Prowlarr의 경우 VPN 클라이언트를 구성하여 프록시를 제공하고 설정 => 인덱서에 프록시를 추가합니다. 프록시에 태그를 지정하고 해당 태그를 사용해야 하는 인덱서를 추가합니다.
    - 절대 필요하고 VPN에서 프록시를 생성하는 방법을 제공하지 않는 경우 Prowlarr을 VPN 뒤에 두고 분할 터널링이 로컬 액세스를 허용하도록 설정합니다.

## Jackett의 /all 엔드포인트

{#jackett-all-endpoint}

- Jackett의 `/all` 엔드포인트는 편리하지만 그것만의 이점이 있습니다. 그 외의 모든 것은 잠재적인 문제입니다. 따라서 각 트래커를 개별적으로 추가해야 합니다. 또는 Jackett 및 NZBHydra2 대체제인 [Prowlarr](/prowlarr)을 확인해 볼 수 있습니다.
- **2022년 4월 업데이트: jackett `/all`에 대한 \*Arr 지원이 제거되었습니다. 이는 문제만 야기하기 때문입니다.**
- Jackett의 /all 엔드포인트는 편리하지만 그것만의 이점이 있습니다. 그 외의 모든 것은 잠재적인 문제입니다. 따라서 이제는 각 트래커를 개별적으로 추가해야 합니다.
- [Jackett의 개발자들도 이를 피하고 사용하지 말아야 한다고 말하고 있습니다.](https://github.com/Jackett/Jackett#aggregate-indexers)
- /all 엔드포인트를 사용하는 것은 장점이 없으며, 다음과 같은 단점이 있습니다:
  - 인덱서별 설정(카테고리, 검색 모드 등)을 제어할 수 없습니다.
  - 검색 모드(IMDB, 쿼리 등)를 혼합하면 품질이 낮은 결과가 발생할 수 있습니다.
  - 인덱서별 카테고리(100000 이상)를 사용할 수 없습니다.
  - 느린 인덱서는 전체 결과를 느리게 만듭니다.
  - 총 결과는 1000개로 제한됩니다.
  - /all의 트래커 중 하나가 오류를 반환하면 \*Arr은 해당 트래커를 비활성화하고 결과를 얻을 수 없게 됩니다.

### Jackett /All 해결 방법

- Jackett에서 각 트래커를 수동으로 인덱서로 추가합니다.
- \*Arr에 인덱서를 동기화할 수 있는 [Prowlarr](/prowlarr)을 확인합니다. 이는 Lidarr/Radarr/Readarr 개발 팀에서 제공합니다.
- \*Arr에 인덱서를 동기화할 수 있는 [NZBHydra2](https://github.com/theotherp/nzbhydra2)를 확인합니다. 그러나 단일 집계 엔드포인트를 사용하지 말고 동기화에 `multi`를 사용하십시오.

## 왜 두 개의 파일이 있는 건가요? | 왜 다운로드 폴더에 파일이 남아 있는 건가요?

이는 정상적인 동작입니다. 하드링크를 지원하는 설정에서는 공간을 두 배로 사용하지 않습니다. 아래는 토런트 프로세스의 작동 방식입니다.

1. Lidarr은 클라이언트에게 다운로드 요청을 보내고, 구성된 다운로드 클라이언트 설정에서 설정한 레이블 또는 카테고리 이름과 연결합니다. 예: 영화, TV, 시리즈, 음악 등.
1. Lidarr은 해당 카테고리 이름을 사용하는 다운로드 클라이언트의 활성 다운로드를 모니터링합니다. 이 모니터링은 다운로드 클라이언트의 API를 통해 수행됩니다.
1. 완료된 파일은 원래 위치에 남아 있어 파일을 시딩할 수 있도록 합니다(비율이나 시간은 다운로드 클라이언트나 특정 다운로드 클라이언트에서 조정할 수 있습니다). 파일이 미디어 폴더로 가져오면 하드링크를 지원하는 경우 하드링크를 만들고, 지원하지 않는 경우 파일을 복사합니다.
1. Lidarr의 설정에서 "완료된 다운로드 처리 - 완료된 항목 제거" 옵션이 활성화된 경우, Lidarr은 원본 파일과 토런트를 다운로드 클라이언트에서 삭제합니다. 다운로드 클라이언트가 시딩이 완료되고 토런트가 중지된 것을 보고할 때에만 삭제됩니다. 최적으로 다운로드 클라이언트를 구성하는 방법은 [TRaSH의 Download Client Guides](https://trash-guides.info/Downloaders/)를 참조하십시오.

> 하드링크는 기본적으로 활성화되어 있습니다. [하드링크를 사용하면 추가 디스크 공간을 사용하지 않습니다.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) 완료된 다운로드 디렉토리와 미디어 라이브러리의 파일 시스템과 마운트는 동일해야 합니다. 하드링크 생성이 실패하거나 설정이 하드링크를 지원하지 않는 경우 파일을 복사합니다.
{.is-info}

## 클라우드 스토리지에서 API 제한에 대한 경고가 계속 나타납니다.

Lidarr은 다른 Arrs와 다릅니다. Lidarr은 파일 이름 대신 태그를 사용합니다. 클라우드 스토리지에 Lidarr 파일을 저장하면 태그를 읽기 위해 파일을 다운로드해야 합니다. 이로 인해 스토리지 제공업체의 API 제한을 빠르게 초과할 수 있습니다. Lidarr 라이브러리를 클라우드 스토리지 제공업체에 저장하는 것을 강력히 권장하지 않으며, 문제가 발생하는 경우 해당 설정 때문일 가능성이 높습니다.