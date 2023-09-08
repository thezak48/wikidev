## 강제 인증

Prowlarr이 로컬 네트워크 외부에서 UI에 액세스할 수 있도록 노출되어 있다면, UI에 액세스하기 위해 인증 방법을 활성화해야 합니다. 이는 트래커와 인덱서에서 점점 더 필요로 되고 있습니다.

Prowlarr v1부터 인증은 필수입니다.

### 인증 방법

- `Basic` (브라우저 팝업) - 이 옵션은 Prowlarr에 액세스할 때 작은 팝업을 표시하여 사용자 이름과 비밀번호를 입력할 수 있게 합니다.
- `Forms` (로그인 페이지) - 이 옵션은 다른 웹사이트와 비슷한 로그인 화면을 제공하여 Prowlarr에 로그인할 수 있게 합니다.
- `External` - 구성 파일을 통해 구성 가능
  - Authelia, Authetik, NGINX 기본 인증 등과 같은 **외부 인증**을 사용하는 경우, 앱을 종료한 다음 [구성 파일](/prowlarr/appdata-directory)에서 `<AuthenticationMethod>External</AuthenticationMethod>`를 설정하고 앱을 다시 시작하여 이중 인증을 방지할 수 있습니다. **파일에 여러 개의 `AuthenticationMethod` 항목을 지정할 수 없으며, 최상위 값만 사용됩니다.**

### 인증 필요 여부

- 앱을 외부에 노출시키지 않거나 로컬(예: LAN) 액세스에 인증이 필요하지 않은 경우, 설정 => 일반 보안 => 인증 필요 항목을 `로컬 주소에 대해 비활성화`로 변경하십시오.
  - 이에 해당하는 구성 파일 항목은 `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`입니다.

{/*forced-authentication*/}

## 통계를 재설정하는 방법은 무엇인가요?

- 통계를 재설정하고 기록을 지우려면 다음 단계를 수행하십시오:

1. 기록 => 옵션
1. 기록 정리를 `1`로 설정합니다. 이렇게 하면 어제까지의 기록과 통계만 유지됩니다.
1. 시스템 => 작업으로 이동합니다.
1. "기록 정리" 작업을 실행합니다.
1. "정리" 작업을 실행합니다.
1. 기록 => 옵션으로 돌아갑니다.
1. 기록 및 통계의 보존 기간을 원하는 대로 설정합니다.

{/*how-do-i-reset-stats*/}

## 카테고리를 사용할 수 없거나 누락되었습니다.

- 사용자 정의/비표준 인덱서 특정 카테고리는 표준 카테고리로 매핑되므로, 표준 카테고리로 검색하면 모든 사용자 정의 카테고리가 포함됩니다. 자세한 내용은 특정 인덱서의 카테고리 매핑 정의를 확인하십시오.

{/*category-not-available-or-missing*/}

## 어떤 (일반적인) 토렌트 RSS 피드를 추가할 수 있나요?

네. "TorrentRSS"를 사용하십시오.

다음 속성은 필수입니다:

- guid
- title
- infohash
- enclosure 또는 link

다음 속성은 선택적이지만 권장됩니다:

- size
- pubDate

{/*can-i-add-any-generic-torrent-rss-feed*/}

## 어떤 (일반적인) Torznab 또는 Newznab 인덱서를 추가할 수 있나요?

- 네.
- `인덱서` => `인덱서 추가` (<kb>+</kb>) => `일반적인 Torznab` 또는 `일반적인 Newznab`로 이동합니다.

{/*can-i-add-any-generic-torznab-or-newznab-indexer*/}

## flaresolverr 인덱서를 사용할 수 있나요?

- 네.

1. [설정 => 인덱서](/prowlarr/settings#indexer-proxies)에서 flaresolverr 인스턴스를 프록시로 추가합니다.
1. 생성된 flaresovlerr 프록시에 태그를 추가합니다.
1. [인덱서](/prowlarr/indexers)에 동일한 태그를 추가합니다.

> 태그는 일치해야 하며, Flaresolverr를 사용하려면 Cloudflare가 감지되어야 합니다. 태그가 사용되지 않으면 Flaresolverr 프록시는 비활성화됩니다.
{.is-warning}

> 자세한 내용은 TRaSH의 "Flaresolverr 설정 방법" 가이드를 참조하십시오.
{.is-info}

{/*can-i-use-flaresolverr-indexers*/}

## 다운되거나 작동하지 않는 인덱서를 추가하는 방법은 무엇인가요?

- 인덱서를 추가하는 표준 단계를 따르되, 다음 변경 사항을 주의하십시오.
- `활성화` 상자를 선택 해제(비활성화)합니다.
- `저장`을 누릅니다.
- 강제 저장을 위해 다시 `저장`을 누릅니다.
- 인덱서를 편집합니다(렌치 아이콘).
- `활성화` 상자를 선택(활성화)합니다.
- `저장`을 누릅니다.
- 강제 저장을 위해 다시 `저장`을 누릅니다.

{/*how-can-i-add-an-indexer-that-is-down-or-not-functional*/}

## Prowlarr이 Sonarr과 동기화되지 않습니다.

- Prowlarr은 Sonarr v3 이상만 지원합니다.
- Sonarr v2 (이전에는 nzbdrone이라고 함)은 Prowlarr에서 지원되지 않으며, 일반적으로 지원되지 않으며, 2021년 3월부터 지원이 종료되었습니다.

{/*prowlarr-will-not-sync-to-sonarr*/}

## Prowlarr이 X 인덱서를 앱에 동기화하지 않습니다.

- Prowlarr은 앱에 대한 추가 및 제거 또는 전체 동기화가 활성화된 경우에만 동기화됩니다.
- 앱과 인덱서가 일치하는 태그를 가지거나 태그가 전혀 없는 경우에만 인덱서가 앱에 동기화됩니다.
- 인덱서는 지원하는 기능/카테고리를 기반으로 동기화됩니다.
  - 인덱서가 TV 카테고리만 지원하는 경우 Lidarr, Radarr 및 Readarr에는 동기화되지 않습니다.
- 특정 앱에 대해 "지원되는" 카테고리를 선택할 수 있습니다.
- 인덱서는 설정 => 애플리케이션 => {앱} => 동기화 카테고리(고급 설정)에서 선택한 특정 카테고리가 지원되지 않으면 동기화를 시도하지 않으며 로그에 동기화 시도에 대한 표시가 표시되지 않습니다.
- 이러한 경우의 가장 일반적인 원인은 \*Arrs가 테스트 쿼리가 구성된 카테고리 중 하나 이상의 결과를 포함하는 결과를 반환하는 인덱서만 허용한다는 것입니다. 즉, 앱에 동기화하려는 경우 인덱서의 빈 쿼리가 앱에 구성된 카테고리 중 어떤 릴리스와도 결과를 반환하지 않으면 인덱서를 \*Arr에 추가할 수 없습니다.
- 구체적인 오류는 \*Arr에서 HTTP 400으로 `Query successful, but no results in the configured categories were returned from your indexer. This may be an issue with the indexer or your indexer category settings.`라고 나타납니다.
  - 해당 \*Arr에서 그 인덱서를 사용할 수 없을 수도 있습니다. 이는 Readarr 및 Lidarr에서 공개 트래커나 Usenet 인덱서를 사용하려고 시도하는 경우에 일반적입니다.
  - Prowlarr 내에서 \*Arr 애플리케이션의 고급 설정에서 동기화되는 카테고리를 조정합니다.
    - 일부 트래커(주로 "형편없는" 공개 트래커)는 `8000 - 기타` 카테고리를 선택하고 동기화해야 합니다. 이는 Prowlarr의 트래커 세부 정보에 자주(하지만 항상은 아님) 표시됩니다.
  - 나중에 다시 시도하십시오.
  - 문제가 지속되면 데이터베이스가 손상되었을 수 있습니다. 로그에서 `Database disk image is malformed` 또는 `Error creating main database`라는 메시지를 확인하십시오. 가능한 해결 방법에 대해서는 [이 항목](https://wiki.servarr.com/prowlarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)을 참조하십시오.

{/*prowlarr-will-not-sync-x-indexer-to-app*/}

## 어떤 \*Arr 인덱서 설정이 앱의 전체 동기화에 사용되나요?

- 앱/Prowlarr: 인덱서 이름
- 앱/Prowlarr: RSS 활성화/비활성화
- 앱/Prowlarr: 자동 검색 활성화/비활성화
- 앱/Prowlarr: 대화형 검색 활성화/비활성화
- 앱/Prowlarr: 인덱서 우선순위
- 앱/Prowlarr: API 키
- 앱/Prowlarr: URL
- 앱/Prowlarr: 기본 URL
- 앱/Prowlarr: 포트
- 앱/Prowlarr: 카테고리
- 앱/Prowlarr: 시드 비율 및 시드 시간
- 앱/Prowlarr: 최소 시더 수
- 앱/Prowlarr: *Prowlarr에서 구성 가능한/제어 가능한 다른 설정*
- Prowlarr: 구현 (예: YML 또는 C#)

전체 동기화가 활성화된 경우, 위의 항목 중 어느 하나라도 \*Arr 앱과 Prowlarr 간에 변경되면 인덱서가 \*Arr에 동기화되고 업데이트됩니다.

{/*what-arr-indexer-settings-are-compared-for-app-full-sync*/}

## Prowlarr을 어떻게 업데이트할 수 있나요?

- 설정으로 이동한 다음 일반 탭으로 이동하여 고급 설정을 표시합니다(저장 버튼 옆의 토글을 사용합니다).

1. 업데이트 섹션에서 브랜치 이름을 `master`, `develop` 또는 `nightly`로 변경합니다.
1. 저장

*이렇게 하면 해당 브랜치의 비트가 즉시 설치되지 않고, 다음 업데이트 중에 설치됩니다.*

- `master` - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) -    (기본/안정): 개발자와 다른 사용자들에 의해 develop 및 nightly 브랜치에서 테스트되었으며, 주요한 문제가 없는 것으로 알려져 있습니다. GitHub에서는 `master` 브랜치입니다.

- `develop` - ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) -  (베타): 테스트를 거친 후 nightly에서 릴리스되어 즉각적인 문제가 없음을 보장합니다. 새로운 기능과 버그 수정은 nightly 이후에 먼저 이곳에서 릴리스됩니다. 반 정도 안정적이지만 여전히 `베타`입니다.

> GitHub에서는 특정 시점에서 `develop` 브랜치의 스냅샷입니다.
{.is-warning}

- `nightly` - ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) -  (알파/불안정): 최신 코드가 커밋되고 모든 자동화된 테스트를 통과한 후 즉시 릴리스됩니다. 이 빌드는 아직 저희나 다른 사용자에 의해 사용된 적이 없을 수 있습니다. 경우에 따라 실행되지 않을 수도 있습니다. 이 브랜치는 고급 사용자에게만 권장됩니다. 이 브랜치에서는 문제가 발생하고 스스로 조사해야 합니다. ***이 브랜치는 오직 무엇을 하고 있는지 알고 있고, 실패한 업데이트를 복구하기 위해 손을 더럽힐 준비가 있는 경우에만 사용하세요.*** 이 버전은 즉시 업데이트됩니다.

> **경고: `develop`로 다시 전환할 수 없을 수도 있습니다.** GitHub에서는 `develop` 브랜치입니다.
{.is-danger}

- 참고: Docker를 통해 설치한 경우 컨테이너 태그 뒤에 `:latest`, `:testing`, `:develop` 또는 `:nightly`를 추가하십시오. 빌드를 제공하는 사람에 따라 다릅니다.

{/*how-do-i-update-prowlarr*/}

## `nightly`에서 `develop`로 다시 전환할 수 있나요?

- 아니요. `nightly` 브랜치로 전환한 후에는 `develop`로 다시 전환할 수 없습니다. `develop` 브랜치로 전환하려면 Prowlarr을 완전히 삭제하고 `develop` 브랜치에서 새로 설치해야 합니다.

{/*can-i-switch-from-nightly-back-to-develop*/}

## 브랜치 간에 전환할 수 있나요?

- 네. 설정에서 일반 탭으로 이동한 다음 고급 설정을 표시하십시오(저장 버튼 옆의 토글을 사용).

1. 브랜치 이름을 `master`, `develop` 또는 `nightly`로 변경합니다.
1. 저장

*이렇게 하면 해당 브랜치의 비트가 즉시 설치되지 않고, 다음 업데이트 중에 설치됩니다.*

{/*can-i-switch-between-branches*/}

## 도움이 필요합니다. Mac에서 Prowlarr을 열 수 없다는 팝업이 나타납니다.

- Mac에서 Prowlarr을 열려고 할 때 "개발자가 확인되지 않았으므로 Prowlarr을(를) 열 수 없습니다"라는 팝업이 나타날 수 있습니다. 이는 Mac의 보안 설정으로 인해 발생하는 문제입니다.

- 다음 단계를 따라 문제를 해결할 수 있습니다:

1. 시스템 환경 설정을 엽니다.
1. 보안 및 개인 정보 보호를 클릭합니다.
1. 일반 탭으로 이동합니다.
1. "이 앱은 개발자가 확인되지 않았으므로 열 수 없습니다"라는 메시지가 나타나면 "여전히 열기"를 클릭합니다.

{/*help-my-mac-says-prowlarr-cannot-be-opened-because-the-developer-cannot-be-verified*/}

## 도움이 필요합니다. Mac에서 Prowlarr.app이 손상되었으며 열 수 없습니다.

- Mac에서 Prowlarr을 열려고 할 때 "Prowlarr.app이(가) 손상되었으며 열 수 없습니다"라는 메시지가 나타날 수 있습니다. 이는 Mac의 보안 설정으로 인해 발생하는 문제입니다.

- 다음 단계를 따라 문제를 해결할 수 있습니다:

1. Finder에서 Prowlarr.app을 찾습니다.
1. 마우스 오른쪽 버튼을 클릭하고 "이 앱을 열 수 없습니다"를 선택합니다.
1. "열기"를 클릭합니다.

{/*help-my-mac-says-prowlarrapp-is-damaged-and-cant-be-opened*/}

## Prowlarr에 기능을 요청하려면 어떻게 해야 하나요?

- Prowlarr에 새로운 기능을 요청하려면 [Prowlarr GitHub 저장소](https://github.com/Prowlarr/Prowlarr)에서 이슈를 만들어야 합니다. 이슈를 만들 때 다음 사항을 고려하십시오:

  - 요청하는 기능에 대한 명확하고 간결한 설명을 제공합니다.
  - 기능 요청이 이미 제출되었는지 먼저 확인합니다. 중복된 요청은 관리자들에게 추가 작업을 요구하게 됩니다.
  - 가능한 경우, 기능 요청에 대한 예시나 사용 사례를 제공합니다.
  - 요청한 기능이 다른 앱과의 호환성에 영향을 미칠 수 있는지 확인합니다.

{/*how-do-i-request-a-feature-for-prowlarr*/}

## 오류가 발생했습니다: 데이터베이스 디스크 이미지가 손상되었습니다.

- 이 오류는 Prowlarr 데이터베이스가 손상되었을 때 발생할 수 있습니다. 이 문제를 해결하기 위해 다음 단계를 수행할 수 있습니다:

1. Prowlarr을 종료합니다.
1. Prowlarr 데이터베이스 파일을 찾습니다. 기본적으로 데이터베이스 파일은 Prowlarr 앱 데이터 디렉토리에 있습니다.
1. 데이터베이스 파일을 백업하고 복사합니다.
1. 데이터베이스 파일을 삭제합니다.
1. Prowlarr을 다시 시작합니다.

- 이 단계를 수행하면 Prowlarr이 새로운 데이터베이스 파일을 생성하고 오류가 해결될 수 있습니다.

{/*i-am-getting-an-error-database-disk-image-is-malformed*/}

## Mac에서 Prowlarr을 사용하다가 갑자기 작동이 중지되었습니다. 무슨 일이 일어난 걸까요?

- Mac에서 Prowlarr을 사용하다가 갑자기 작동이 중지된 경우 다음 단계를 수행하여 문제를 해결할 수 있습니다:

1. Prowlarr을 종료합니다.
1. Finder에서 Prowlarr.app을 찾습니다.
1. 마우스 오른쪽 버튼을 클릭하고 "이 앱을 열 수 없습니다"를 선택합니다.
1. "열기"를 클릭합니다.
1. Prowlarr이 다시 시작됩니다.

- 이 단계를 수행하면 Prowlarr이 정상적으로 작동할 수 있습니다.

{/*i-use-prowlarr-on-a-mac-and-it-suddenly-stopped-working-what-happened*/}

## Windows 서비스에서 트레이 앱으로 변경하는 방법은 무엇인가요?

- Windows에서 Prowlarr을 서비스로 실행 중이지만 트레이 앱으로 변경하려면 다음 단계를 수행할 수 있습니다:

1. Prowlarr을 종료합니다.
1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
1. `nssm.exe` 파일을 찾습니다. 이 파일은 Prowlarr 설치 디렉토리에 있습니다.
1. 명령 프롬프트를 열고 다음 명령을 실행합니다: `nssm remove Prowlarr`
1. Prowlarr을 다시 시작합니다.

- 이 단계를 수행하면 Prowlarr이 서비스에서 트레이 앱으로 변경됩니다.

{/*how-do-i-change-from-the-windows-service-to-a-tray-app*/}

## Prowlarr을 백업/복원하는 방법은 무엇인가요?

- Prowlarr을 백업하고 복원하는 방법은 다음과 같습니다:

### Prowlarr 백업

- 내장된 백업을 사용하는 방법:

  1. Prowlarr을 종료합니다.
  1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
  1. `backup` 폴더를 찾습니다.
  1. `backup` 폴더를 백업하고 원하는 위치에 저장합니다.

- 파일 시스템을 직접 사용하는 방법:

  1. Prowlarr을 종료합니다.
  1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
  1. 모든 파일과 폴더를 백업하고 원하는 위치에 저장합니다.

### 백업에서 복원

- zip 백업을 사용하는 방법:

  1. Prowlarr을 종료합니다.
  1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
  1. 백업 파일을 압축 해제하고 모든 파일과 폴더를 복원합니다.

- 파일 시스템 백업을 사용하는 방법:

  1. Prowlarr을 종료합니다.
  1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
  1. 백업한 파일과 폴더를 복원합니다.

### Synology NAS에서 파일 시스템 복원

- Synology NAS에서 파일 시스템 복원을 수행하는 방법은 다음과 같습니다:

  1. Prowlarr을 종료합니다.
  1. Synology NAS의 파일 탐색기를 엽니다.
  1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `/volume1/Prowlarr`에 있습니다.
  1. 백업한 파일과 폴더를 복원합니다.

{/*how-do-i-backuprestore-prowlarr*/}

## Windows에서 웹 UI가 로컬호스트에서만 로드됩니다.

- Windows에서 Prowlarr의 웹 UI가 로컬호스트에서만 로드되는 경우 다음 단계를 수행하여 문제를 해결할 수 있습니다:

1. Prowlarr을 종료합니다.
1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
1. `config.xml` 파일을 찾습니다.
1. `config.xml` 파일을 텍스트 편집기로 엽니다.
1. `<UrlBase>` 요소를 찾습니다.
1. `<UrlBase>` 요소의 값을 비워 둡니다.
1. `config.xml` 파일을 저장하고 닫습니다.
1. Prowlarr을 다시 시작합니다.

- 이 단계를 수행하면 Prowlarr의 웹 UI가 로컬 네트워크의 IP 주소로부터 액세스할 수 있게 됩니다.

{/*webui-only-loads-at-localhost-on-windows*/}

## 쿠키를 찾는 방법은 무엇인가요?

- Prowlarr에서 쿠키를 찾는 방법은 다음과 같습니다:

1. Prowlarr을 실행합니다.
1. 웹 브라우저에서 Prowlarr에 로그인합니다.
1. 개발자 도구를 엽니다. 대부분의 브라우저에서는 F12 키를 누르거나 오른쪽 클릭 메뉴에서 "검사" 또는 "개발자 도구"를 선택하여 개발자 도구를 열 수 있습니다.
1. 개발자 도구의 "Application" 탭으로 이동합니다.
1. 왼쪽 창에서 "Storage"를 확장합니다.
1. "Cookies"를 선택합니다.
1. "localhost" 아래에서 Prowlarr 도메인을 찾습니다.
1. 해당 도메인을 확장하고 "Name" 열에서 쿠키 이름을 확인합니다.

- 이 단계를 수행하면 Prowlarr에서 사용되는 쿠키를 확인할 수 있습니다.

{/*finding-cookies*/}

## uTorrent이 더 이상 작동하지 않습니다.

- uTorrent이 더 이상 작동하지 않는 경우 다음 단계를 수행하여 문제를 해결할 수 있습니다:

1. Prowlarr을 종료합니다.
1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
1. `config.xml` 파일을 찾습니다.
1. `config.xml` 파일을 텍스트 편집기로 엽니다.
1. `<TorrentDownloadClient>` 요소를 찾습니다.
1. `<TorrentDownloadClient>` 요소의 값을 다음과 같이 변경합니다:

   ```xml
   <TorrentDownloadClient>uTorrent</TorrentDownloadClient>
   ```

1. `config.xml` 파일을 저장하고 닫습니다.
1. Prowlarr을 다시 시작합니다.

- 이 단계를 수행하면 uTorrent이 다시 작동할 수 있습니다.

{/*utorrent-is-no-longer-working*/}

## config.xml이 손상되었다는 팝업이 나타났습니다. 어떻게 해야 하나요?

- "config.xml이 손상되었습니다"라는 팝업이 나타난 경우 다음 단계를 수행하여 문제를 해결할 수 있습니다:

1. Prowlarr을 종료합니다.
1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
1. `config.xml` 파일을 찾습니다.
1. `config.xml` 파일을 텍스트 편집기로 엽니다.
1. 파일 내용을 확인하고 손상된 부분을 수정합니다.
1. `config.xml` 파일을 저장하고 닫습니다.
1. Prowlarr을 다시 시작합니다.

- 이 단계를 수행하면 손상된 `config.xml` 파일을 수정하여 Prowlarr이 다시 정상적으로 작동할 수 있습니다.

{/*i-got-a-pop-up-that-said-configxml-was-corrupt-what-now*/}

## 잘못된 인증서 및 기타 HTTPS 또는 SSL 문제

- 잘못된 인증서 및 기타 HTTPS 또는 SSL 문제가 발생하는 경우 다음 단계를 수행하여 문제를 해결할 수 있습니다:

1. Prowlarr을 종료합니다.
1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
1. `config.xml` 파일을 찾습니다.
1. `config.xml` 파일을 텍스트 편집기로 엽니다.
1. `<EnableSsl>` 요소를 찾습니다.
1. `<EnableSsl>` 요소의 값을 `false`로 변경합니다.
1. `config.xml` 파일을 저장하고 닫습니다.
1. Prowlarr을 다시 시작합니다.

- 이 단계를 수행하면 Prowlarr이 SSL을 사용하지 않도록 설정되어 HTTPS 또는 SSL 문제를 해결할 수 있습니다.

{/*invalid-certificate-and-other-https-or-ssl-issues*/}

## 도움이 필요합니다. 자물쇠가 걸렸습니다.

- Prowlarr에 잠겨서 로그인할 수 없는 경우 다음 단계를 수행하여 문제를 해결할 수 있습니다:

1. Prowlarr을 종료합니다.
1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
1. `config.xml` 파일을 찾습니다.
1. `config.xml` 파일을 텍스트 편집기로 엽니다.
1. `<Authentication>` 요소를 찾습니다.
1. `<Authentication>` 요소의 값을 `false`로 변경합니다.
1. `config.xml` 파일을 저장하고 닫습니다.
1. Prowlarr을 다시 시작합니다.

- 이 단계를 수행하면 Prowlarr이 잠금 해제되어 로그인할 수 있게 됩니다.

{/*help-i-have-locked-myself-out*/}

## 이상한 UI 문제

- Prowlarr의 UI에 이상한 문제가 발생하는 경우 다음 단계를 수행하여 문제를 해결할 수 있습니다:

1. Prowlarr을 종료합니다.
1. Prowlarr 데이터 디렉토리로 이동합니다. 기본적으로 데이터 디렉토리는 `C:\ProgramData\Prowlarr`에 있습니다.
1. `config.xml` 파일을 찾습니다.
1. `config.xml` 파일을 텍스트 편집기로 엽니다.
1. 파일 내용을 확인하고 이상한 부분을 수정합니다.
1. `config.xml` 파일을 저장하고 닫습니다.
1. Prowlarr을 다시 시작합니다.

- 이 단계를 수행하면 Prowlarr의 UI 문제가 해결될 수 있습니다.

{/*weird-ui-issues*/}

## VPN, Prowlarr 및 \*ARRs

- VPN을 사용하여 Prowlarr과 \*ARRs를 함께 사용하는 경우 다음 사항을 고려하십시오:

  - VPN을 사용하면 인터넷 트래픽이 암호화되어 보호됩니다. 그러나 VPN을 사용하면 일부 인덱서와 트래커에 액세스할 수 없을 수 있습니다.
  - VPN을 사용하면 인터넷 연결이 느려질 수 있습니다. 이는 Prowlarr과 \*ARRs의 성능에 영향을 줄 수 있습니다.
  - VPN을 사용하면 지리적으로 제한된 콘텐츠에 액세스할 수 있습니다. 이는 Prowlarr과 \*ARRs를 사용하여 해당 콘텐츠를 다운로드하는 데 도움이 될 수 있습니다.

- VPN을 사용하는 경우 Prowlarr과 \*ARRs를 함께 사용할 때 발생할 수 있는 문제를 해결하기 위해 다음 단계를 수행할 수 있습니다:

  1. VPN을 사용하여 인터넷에 연결합니다.
  1. Prowlarr과 \*ARRs를 실행합니다.
  1. Prowlarr과 \*ARRs에서 VPN을 사용하지 않는 인덱서와 트래커를 설정합니다.
  1. Prowlarr과 \*ARRs를 사용하여 원하는 콘텐츠를 다운로드합니다.

- 이 단계를 수행하면 VPN을 사용하여 Prowlarr과 \*ARRs를 함께 사용할 수 있습니다.

{/*vpns-jackett-and-the-arrs*/}

## 시작 시 브라우저가 자동으로 실행되는 것을 멈추는 방법은 무엇인가요?

- Prowlarr이 시작될 때 브라우저가 자동으로 실행되는 것을 멈추려면 다음 단계를 수행할 수 있습니다:

1. Prowlarr을 실행합니다.
1. 웹 브라우저에서 Prowlarr에 로그인합니다.
1. 설정으로 이동합니다.
1. 일반 탭으로 이동합니다.
1. "브라우저에서 시작 시 열기" 옵션을 비활성화합니다.
1. 설정을 저장합니다.

- 이 단계를 수행하면 Prowlarr이 시작될 때 브라우저가 자동으로 실행되지 않습니다.

{/*how-do-i-stop-the-browser-from-launching-on-startup*/}

## 한 번에 모든 인덱서를 쉽게 추가할 수 있나요?

- 네, 한 번에 모든 인덱서를 쉽게 추가할 수 있습니다. 다음 단계를 수행하십시오:

1. Prowlarr을 실행합니다.
1. 설정으로 이동합니다.
1. 인덱서 탭으로 이동합니다.
1. "인덱서 추가" 버튼을 클릭합니다.
1. "Torznab" 또는 "Newznab"을 선택합니다.
1. "Torznab 인덱서 추가" 또는 "Newznab 인덱서 추가" 대화 상자가 표시됩니다.
1. "Enable RSS Sync" 옵션을 선택합니다.
1. "Enable Search" 옵션을 선택합니다.
1. "Save" 버튼을 클릭합니다.

- 이 단계를 수행하면 모든 인덱서가 쉽게 추가됩니다.

{/*can-i-easily-add-all-indexers-at-once*/}

|                                                                      | `master` (stable) ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) | `nightly` (unstable) ![Current Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/prowlarr)                       | `latest`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-prowlarr) | `latest`                                                                                                                                                                                                             | `develop`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |

### 도커 컨테이너 내에서 Prowlarr을 업데이트할 수 있을까요?

- *기술적으로 가능합니다.* **하지만 절대로 하지 마십시오.** 이것은 도커의 주요 철학입니다. 가장 최신의 `nightly`로 설치를 업그레이드한 다음 도커 컨테이너 자체를 업데이트하면(오래된 버전으로 다운그레이드할 수도 있음) 데이터베이스 문제가 발생할 수 있습니다.

### 더 최신 버전 설치하기

#### Native

1. 시스템으로 이동한 다음 업데이트 탭으로 이동합니다.
1. 아직 설치되지 않은 더 최신 버전은 옆에 업데이트 버튼이 표시됩니다. 해당 버튼을 클릭하여 업데이트를 설치합니다.

#### Docker

1. 태그를 다시 가져오고 컨테이너를 업데이트합니다.

## `nightly`에서 `develop`로 변경할 수 있을까요?

## 브랜치 간에 전환할 수 있을까요?

- 버전이 동일한 경우 전환할 수 있지만, 그렇지 않은 경우 `nightly`에서 `develop`로 전환하거나 `develop`에서 `nightly`로 전환할 수 있는지 개발팀과 확인하십시오.
- 이 지침을 따르지 않으면 Prowlarr이 사용할 수 없거나 오류가 발생할 수 있습니다. 경고합니다.
  - 가장 일반적인 오류는 누락된 열 또는 테이블과 관련된 데이터베이스 오류입니다.

## 도움이 필요합니다. Mac에서 개발자가 확인되지 않아 Prowlarr을 열 수 없다는 메시지가 표시됩니다.

- 이것은 간단한 문제입니다. 자세한 내용은 [여기](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)를 참조하십시오.
- 또는 Prowlarr을 자체로 서명해야 할 수도 있습니다. `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine`

![faq_1_mac.png](/assets/general/faq_1_mac.png)

## 도움이 필요합니다. Mac에서 Prowlarr.app이 손상되어 열 수 없습니다.

이는 손상된 다운로드(다시 시도) 또는 이전에 언급한 보안 문제로 인한 것입니다.

## Prowlarr에 기능을 요청하는 방법은 무엇인가요?

Prowlarr에 기능을 요청하려면 먼저 GitHub에서 유사한 요청이 있는지 확인한 다음 [여기를 클릭하여 요청을 추가하십시오](https://github.com/Prowlarr/Prowlarr/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=).

## 오류가 발생합니다: 데이터베이스 디스크 이미지가 손상되었습니다

- **`Error creating log database` 오류는 logs.db에 문제가 있는 것을 나타냅니다.**
  - 이는 데이터베이스를 이름을 변경하거나 제거하여 빠르게 해결할 수 있습니다. 로그 데이터베이스에는 명령 기록 및 업데이트 설치 기록, 그리고 Info, Warn 및 Error 항목이 포함되어 있습니다.
- **`Error creating main database` 또는 지정된 데이터베이스가 없는 일반적인 `database disk image is malformed` 오류는 prowlarr.db에 문제가 있는 것을 나타냅니다.**
  - 아래에 나열된 단계를 따르십시오.
- 이는 Prowlarr의 대부분의 정보를 저장하는 SQLite 데이터베이스가 손상되었음을 의미합니다. 기존 데이터베이스를 복구하려고 시도하거나 백업을 복구하려고 시도하거나, 그 외에 모든 것이 실패하면 새로운 데이터베이스로 다시 시작하는 옵션이 있습니다.
- 이 오류는 데이터베이스 파일이 \*Arr이 실행되는 사용자/그룹에 의해 쓰기 가능하지 않을 때 발생할 수 있습니다. 권한 문제는 일반적으로 새로 설치한 경우, 새 서버로 이전한 경우, 최근에 appdata 디렉토리 권한을 수정한 경우 또는 \*Arr이 실행되는 사용자와 그룹을 변경한 경우에만 문제가 될 수 있습니다.
- 가장 좋은 옵션은 [백업에서 복원을 시도하는 것입니다](#how-do-i-backuprestore-my-prowlarr).
- 데이터베이스를 복구해 볼 수도 있습니다. 이 문제가 업데이트 후에 발생한 경우에는 일반적으로 유일한 옵션입니다. [sqlite3의 `.recover` 명령](/useful-tools#recovering-a-corrupt-db)을 시도해 보십시오.
  - sqlite에 `.recover`가 없거나 더 GUI(예: Windows) 친화적인 방법을 원하는 경우 [이 위키의 지침](/useful-tools#recovering-a-corrupt-db-ui)을 따르십시오.
- 데이터베이스 오류의 또 다른 가능한 원인은 데이터베이스를 네트워크 드라이브(nfs 또는 smb 또는 기타 로컬이 아닌 것)에 배치한 경우입니다. **SQLite는 데이터와 응용 프로그램이 동일한 컴퓨터에 공존하는 상황을 위해 설계되었습니다.** 따라서 \*Arr AppData 폴더(/config 도커 마운트)는 로컬 스토리지에 있어야 합니다. [SQLite와 네트워크 드라이브는 함께 작동하지 않으며 결국 손상된 데이터베이스를 야기할 수 있습니다](https://www.sqlite.org/draft/useovernet.html).
- mergerFS를 사용하는 경우 SQLite가 mmap을 사용하기 때문에 `direct_io`를 제거해야 합니다. `direct_io`는 mmap을 지원하지 않기 때문에 SQLite와 함께 작동하지 않습니다. mergerFS [문서 여기](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)에서 자세히 설명되어 있습니다.

## Mac에서 Prowlarr을 사용하다가 갑자기 작동이 중지되었습니다. 무슨 일이 일어난 걸까요?

대부분 이는 MacOS 버그로 인해 Prowlarr 데이터베이스가 손상되었기 때문입니다. 손상된 데이터베이스를 복원하는 방법에 대한 FAQ 항목을 확인하십시오.

## Windows 서비스에서 트레이 앱으로 변경하는 방법은 무엇인가요?

- Prowlarr을 종료합니다.
- Prowlarr 디렉토리에 있는 serviceuninstall.exe를 실행합니다.
- Prowlarr.exe를 관리자 권한으로 한 번 실행하여 적절한 권한을 부여하고 방화벽을 엽니다. 완료되면 종료하고 일반적으로 실행하십시오.
- (선택 사항) 부팅 시 자동으로 시작하도록 Prowlarr.exe에 대한 바로 가기를 시작 프로그램 폴더에 놓습니다.

## Prowlarr을 백업/복원하는 방법은 무엇인가요?

### Prowlarr 백업하기

#### 내장된 백업 사용

- Prowlarr UI에서 System => Backup으로 이동합니다.
- 백업 버튼을 클릭합니다.
- 백업이 생성된 후 zip 파일을 다운로드하여 안전한 위치에 보관합니다.

#### 파일 시스템 직접 사용

- Prowlarr의 AppData 디렉토리 위치를 찾습니다.
  - Prowlarr UI에서 System => About으로 이동합니다.
  - [Prowlarr Appdata 디렉토리](/prowlarr/appdata-directory)
- Prowlarr을 중지합니다. 이렇게 하면 데이터베이스가 손상되지 않습니다.
- 내용을 안전한 위치로 복사합니다.

### 백업에서 복원하기

> 서로 다른 경로를 사용하는 OS로 복원하는 것은 작동하지 않습니다(Windows에서 Linux로, Linux에서 Windows로, Windows에서 macOS로 또는 macOS에서 Windows로). macOS와 Linux 간의 이동은 `/`를 사용하는 경로를 사용하기 때문에 작동할 수 있지만, 지원되지 않습니다. 데이터베이스의 모든 경로를 수동으로 편집해야 합니다.
{.is-warning}

#### zip 백업 사용

- Prowlarr을 다시 설치합니다(해당되는 경우/이미 설치되지 않은 경우).
- Prowlarr을 실행합니다.
- System => Backup으로 이동합니다.
- Restore Backup을 선택합니다.
- Choose File을 선택합니다.
- 백업 zip 파일을 선택합니다.
- Restore를 선택합니다.

#### 파일 시스템 백업 사용

- Prowlarr을 다시 설치합니다(해당되는 경우/이미 설치되지 않은 경우).
- Prowlarr의 AppData 디렉토리 위치를 찾습니다.
  - Prowlarr을 한 번 실행하고 UI에서 System => About으로 이동합니다.
  - [Prowlarr Appdata 디렉토리](/prowlarr/appdata-directory)
- Prowlarr을 중지합니다.
- AppData 디렉토리의 내용을 삭제합니다. **(.db-wal/.db-journal 파일이 있는 경우 포함)**
- 백업에서 복원합니다.
- Prowlarr을 시작합니다.
- 경로가 동일한 경우 모든 것이 이전 상태에서 계속됩니다.

#### Synology NAS에서 파일 시스템 복원

> 주의: Synology에서 복원하는 경우 Linux에 대한 지식과 Synology 장치에 대한 루트 SSH 액세스가 필요합니다.
{.is-warning}

- Prowlarr을 다시 설치합니다(해당되는 경우/이미 설치되지 않은 경우).
- Prowlarr의 AppData 디렉토리 위치를 찾습니다.
  - Prowlarr을 한 번 실행하고 UI에서 System => About으로 이동합니다.
  - [Prowlarr Appdata 디렉토리](/prowlarr/appdata-directory)
- Prowlarr을 중지합니다.
- SSH를 통해 Synology NAS에 연결하고 root로 로그인합니다.

> 일부 설치에서 사용자가 아래 명령과 다른 경우가 있습니다: `chown -R sc-Prowlarr:Prowlarr *` {.is-info}

- 다음 명령을 실행합니다:

    ```shell
        rm -r /usr/local/Prowlarr/var/.config/Prowlarr/Prowlarr.db
        cp -f /tmp/Prowlarr_backup/* /usr/local/Prowlarr/var/.config/Prowlarr/
    ```

- 파일의 권한을 업데이트합니다:

    ```shell
        cd /usr/local/Prowlarr/var/.config/Prowlarr/
        chown -R Prowlarr:users *
        chmod -R 0644 *
    ```

- Prowlarr을 시작합니다.

## 웹 인터페이스가 Windows에서만 localhost에서 로드됩니다.

웹 인터페이스에 `http://localhost:9696/` 또는 `http://127.0.0.1:9696`로만 접근할 수 있는 경우, Prowlarr을 최소한 한 번은 관리자 권한으로 실행해야 합니다.

## 쿠키 찾기

일부 사이트는 자동으로 로그인할 수 없으며 Prowlarr에서 작동하려면 수동으로 로그인한 다음 쿠키를 제공해야 합니다. [자세한 내용은 이 문서를 참조하십시오.](/useful-tools#finding-cookies)

## uTorrent이 더 이상 작동하지 않습니다

- 웹 인터페이스가 활성화되어 있는지 확인합니다.

![faq_4_utorrent.png](/assets/general/faq_4_utorrent.png)

- 웹 인터페이스를 켭니다.

![faq_5_utorrent.png](/assets/general/faq_5_utorrent.png)

- Alt Listening Port(Advanced => Web UI)가 Listening Port(Connections)와 다른지 확인합니다. 연결을 위한 포트 포워딩에 영향을 주지 않도록 Web UI Alt Listening Port를 변경하는 것이 좋습니다.

![faq_6_utorrent.png](/assets/general/faq_6_utorrent.png)

## config.xml이 손상되었다는 팝업이 떴습니다. 어떻게 해야 하나요?

Prowlarr은 시작 시 config 파일을 읽을 수 없게 되어 손상되었습니다. Prowlarr을 다시 온라인으로 돌리려면 AppData 폴더에서 `.xml` 파일을 삭제한 후 Prowlarr을 시작하면 기본 포트(9696)에서 시작됩니다. 그리고 일반 설정 페이지에서 구성한 설정을 다시 구성해야 합니다.

## 잘못된 인증서 및 기타 HTTPS 또는 SSL 문제

다운로드 클라이언트가 작동을 멈추고 `Localhost is an invalid certificate`와 같은 오류가 발생하는 경우가 있나요?

Prowlarr은 SSL 인증서를 확인합니다. 다운로드 클라이언트에 SSL 인증서가 설정되어 있지 않거나 로컬 인증서 저장소에 CA 인증서가 추가되지 않은 자체 서명 HTTPS 인증서를 사용하는 경우 Prowlarr은 연결을 거부합니다. 무료로 올바르게 서명된 인증서는 let's encrypt에서 제공됩니다.

다운로드 클라이언트와 Prowlarr이 동일한 기기에 있는 경우 HTTPS를 사용할 필요가 없으므로 가장 쉬운 해결책은 연결에 대한 SSL을 비활성화하는 것입니다. 대부분의 경우 로컬 네트워크에서는 필요하지 않다고 생각합니다. 보안이 취약한 SSL 설정을 유지하려면 고급 설정에서 인증서 유효성 검사를 비활성화할 수 있습니다.

## 도움이 필요합니다. 자물쇠를 걸었습니다.

{#help-i-have-forgotten-my-password}

인증을 비활성화하려면 (잊어버린 사용자 이름이나 비밀번호를 재설정하려면) [Prowlarr Appdata Directory](/prowlarr/appdata-directory)에 있는 `config.xml`을 편집해야 합니다.

1. 텍스트 편집기에서 config.xml을 엽니다.
2. 인증 방법 라인을 찾습니다. `<AuthenticationMethod>Basic</AuthenticationMethod>` 또는 `<AuthenticationMethod>Forms</AuthenticationMethod>`일 것입니다.
3. `AuthenticationMethod` 라인을 `<AuthenticationMethod>None</AuthenticationMethod>`로 변경합니다.
4. Prowlarr을 다시 시작합니다.
5. 이제 Prowlarr에는 비밀번호 없이 액세스할 수 있으며, UI에서 `Settings: General`로 이동하여 사용자 이름과 비밀번호를 설정해야 합니다.

## 이상한 UI 문제

- 이상한 UI 문제가 발생하거나 특정 뷰나 정렬이 작동하지 않는 경우, Chrome의 시크릿 창이나 Firefox의 프라이빗 창에서 확인해 보세요. 그곳에서 잘 작동한다면 특정 IP/도메인에 대한 브라우저 캐시와 쿠키를 지우세요. 자세한 내용은 [캐시, 쿠키 및 로컬 스토리지 지우기](/useful-tools#clearing-cookies-and-local-storage) 위키 문서를 참조하세요.

## VPN, Jackett 및 \*ARRs

- 중국, 호주 또는 남아프리카와 같은 억압적인 국가가 아닌 경우, 토렌트 클라이언트는 일반적으로 VPN 뒤에 있어야 하는 유일한 것입니다. VPN 엔드포인트는 여러 사용자와 공유되기 때문에 각 소프트웨어가 사용하는 다양한 서비스에서 속도 제한, DDOS 보호 및 IP 차단을 경험할 수 있습니다.
- 다른 말로, \*Arrs (Lidarr, Prowlarr, Radarr, Readarr 및 Lidarr)을 VPN 뒤에 두면 일부 경우에는 애플리케이션을 사용할 수 없게 만들 수 있습니다.

> **명확하게 말하자면 VPN이 \*Arrs와 문제를 일으킬지 아닌지가 문제가 아니라 언제 문제가 발생할 것입니다: 이미지 제공자는 차단할 것이고 클라우드플레어는 \*Arr 서버(업데이트, 메타데이터 등) 앞에 있으며 차단될 수 있습니다.**
{.is-warning}

- **많은 비공개 트래커는 VPN을 사용하거나 액세스하는 것(예: Jackett 또는 Prowlarr 사용)을 금지할 수 있습니다.**

### VPN 사용

- VPN이 필요하고 Docker를 사용하는 경우 Hotio 또는 Binhex의 Download Client + VPN 컨테이너를 사용하는 것이 좋습니다.
- VPN이 필요하지만 Docker를 사용하지 않는 경우 VPN 클라이언트는 반드시 분할 터널링을 지원해야 합니다. 이렇게 하면 필요한 (다운로드 클라이언트) 앱만 VPN 뒤에 있게 됩니다.
- 트래커에 액세스하는 데 문제가 있는 경우 ISP의 DNS 서버 대신 Google이나 Cloudflare의 DNS 서버를 사용하여 해결할 수 있습니다.
- 일부 경우(예: 영국 ISP) 토렌트 다운로드 클라이언트를 VPN 뒤에 두고 Jackett/Prowlarr을 다음과 같이 설정해야 할 수도 있습니다:
  - Jackett을 VPN 뒤에 두고 분할 터널링이 로컬 액세스를 허용하도록 설정합니다.
  - Prowlarr의 경우 VPN 클라이언트를 구성하여 프록시를 제공하고 설정 => 인덱서에 프록시를 추가합니다. 프록시에 태그를 지정하고 해당 태그를 사용해야 하는 인덱서를 추가합니다.
    - 절대 필요한 경우 VPN에서 프록시를 생성하는 방법을 제공하지 않는 경우 Prowlarr을 VPN 뒤에 두고 분할 터널링이 로컬 액세스를 허용하도록 설정합니다.

## 브라우저가 시작할 때 실행되지 않도록 할 수 있나요?

운영 체제에 따라 여러 가지 방법이 있습니다.

- 일부 운영 체제에서는 `Settings` => `General`에서 브라우저를 시작할 때 실행하는 확인란이 있습니다.
- Prowlarr을 호출할 때 인수에 `-nobrowser`(*nix) 또는 `/nobrowser`(Windows)를 추가할 수 있습니다.
- Prowlarr을 중지하고 config.xml 파일을 편집하고 `<LaunchBrowser>True</LaunchBrowser>`를 `<LaunchBrowser>False</LaunchBrowser>`로 변경합니다.

## 모든 인덱서를 한 번에 쉽게 추가할 수 있나요?

아니요. 이렇게 하는 것은 좋은 방법이 아니며 이 기능은 추가되지 않을 것입니다. 인덱서를 신중하게 선택하고 너무 느리거나 검색 결과를 생성하지 않는 인덱서를 제거하는 것이 훨씬 좋습니다. 인덱서를 적절하게 가지고 유지 관리하면 전반적으로 훨씬 좋은 결과와 빠른 검색 결과를 얻을 수 있습니다.