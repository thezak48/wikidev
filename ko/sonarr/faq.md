# Sonarr 기본 사항

## Sonarr은 에피소드를 어떻게 찾나요?

- Sonarr은 누락된 에피소드나 품질 목표를 충족하지 못한 에피소드를 정기적으로 검색하지 않습니다. 대신, Sonarr은 새로 게시된 에피소드/릴리스를 모두 쿼리한 다음, 누락된 에피소드나 업그레이드가 필요한 에피소드 목록과 비교합니다. 일치하는 항목은 다운로드됩니다. 이를 통해 Sonarr은 하루에 24-100개의 쿼리(15-60분의 RSS 간격)로 *어떤 크기의 라이브러리든* 커버할 수 있습니다. 이를 이해하면, Sonarr은 *미래*만 커버한다는 것을 알 수 있습니다.
- 그렇다면 현재와 과거는 어떻게 처리하나요? 쇼를 추가할 때 올바른 경로, 프로필 및 모니터링 상태를 설정한 다음, 누락된 검색란을 선택하면 됩니다. 쇼에 에피소드가 없고 아직 출시되지 않은 경우 검색을 시작할 필요가 없습니다.
- 다시 말해, Sonarr은 인덱서에 새로 업로드된 릴리스만 찾을 수 있습니다. 과거에 업로드된 릴리스를 찾으려고 노력하지는 않습니다.
- 이미 쇼를 추가했지만 이제 검색하려는 경우 몇 가지 선택 사항이 있습니다. 쇼 페이지로 이동하여 검색 버튼을 사용하면 검색을 수행한 다음 자동으로 에피소드를 선택합니다. 개별 에피소드나 시즌을 자동으로 또는 수동으로 검색할 수 있습니다. 또는 [Wanted](/sonarr/wanted) 탭으로 이동하여 검색할 수 있습니다.
- Sonarr이 오랜 기간 동안 오프라인이었을 경우, Sonarr은 놓친 릴리스를 피하기 위해 마지막으로 처리한 릴리스를 찾기 위해 페이지를 되감으려고 시도합니다. 인덱서가 페이징을 지원하고 너무 오래되지 않았다면 Sonarr은 놓친 에피소드를 검색하지 않고 처리할 수 있습니다.

### 자동 검색이 발생하는 경우

자동 검색(인덱서의 API를 통한)은 다음 상황에서만 수행됩니다. 일반적인 규칙이 적용되는 것에 유의하세요: 시리즈 + 에피소드는 모니터링되어야 하며, 에피소드에 방영일이 없으면 건너뜁니다.

- 트리거된 자동 또는 수동 검색
  - 사용자 또는 API가 트리거한 검색. 일반적으로 특정 에피소드, 시즌 또는 시리즈의 자동 또는 수동 검색 버튼을 클릭하여 실행됩니다.
- "추가 및 검색" 버튼을 사용하여 쇼를 추가하는 경우
- "Wanted => Missing" 또는 "Wanted => Cutoff Unmet"를 사용하여 하나 이상의 검색을 수행하는 경우
- 방영 후 추가된 최신 에피소드
  - Sonarr에 새로운 에피소드가 추가되고, 해당 에피소드가 지난 14일 이내에 방영되었거나 미래 1일 이내에 방영될 경우(조금 일찍 릴리스되는 에피소드를 커버하기 위해), Sonarr은 해당 에피소드를 검색합니다. 단, 시리즈 폴더가 다시 스캔된 후에 검색이 수행됩니다(Sonarr 외부에서 가져온 항목을 포함하기 위해).

## 가능한 다운로드는 어떻게 비교되나요?

> 일반적으로 품질이 우선합니다. 품질을 주요 우선 순위로 설정하지 않으려면 품질을 병합할 수 있습니다. [TRaSH의 가이드](https://trash-guides.info/merge-quality)를 참조하세요.
{.is-info}

- 현재 로직은 [여기에서 항상 찾을 수 있습니다](https://github.com/Sonarr/Sonarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs#L31-L40s).

- 2022-01-23 기준 로직은 다음과 같습니다:

1. 품질
1. 언어
1. 우선 단어 점수\*
1. 프로토콜(해당 지연 프로필에서 구성한 대로)
1. 에피소드 수\*
1. 에피소드 번호
1. 인덱서 우선순위
1. 시드/피어(토렌트인 경우)
1. 나이(유즈넷인 경우)
1. 크기

> REPACKS 및 PROPER는 품질의 v2이며, 동일한 품질의 non-repack보다 우선합니다. [미디어 관리 => 파일 관리 `Download Proper & Repacks`를 "Do Not Prefer"로 설정](/sonarr/settings#file-management)하고, [TRaSH의 가이드](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#p2p-groups-repackproper)에서 제안하는 긍정적인 점수와 함께 `/\b(repack|proper)\b/i`와 같은 우선 단어 정규식을 사용하세요.
{.is-warning}

> \* 우선 단어는 품질 및/또는 언어 커트오프가 충족되었더라도 항상 릴리스를 업그레이드합니다. 이는 프로필에서 업그레이드가 비활성화된 경우에도 해당됩니다.
> \* 우선 단어는 표준 시즌 팩 기본 설정을 무시합니다. 이는 [Sonarr Github 이슈 #3562](https://github.com/Sonarr/Sonarr/issues/3562)입니다. 우선 단어를 사용할 때 시즌 팩을 선호하려면 [시즌 팩 기본 설정을 추가해야 합니다](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs).
{.is-info}

## 우선 단어 FAQ

- 디스크 파일의 점수에 대한 설명: 파일의 기존 이름과 릴리스의 "원래 씬 이름"은 우선 단어를 평가하는 데 사용됩니다. 두 값 중 더 높은 점수가 적용됩니다.

- 이름 변경에 우선 단어가 어떻게 포함되나요?

  - Sonarr에서는 이름 변경 체계에서 `{Preferred Words}` 토큰을 사용하고 릴리스 프로필에서 `Include Preferred when Renaming`을 활성화할 수 있습니다. Sonarr에 대한 권장 이름 변경 체계 예제를 보려면 [TRaSH의 권장 이름 변경 체계](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/)를 참조하세요. 이름 변경 체계에서 토큰을 사용하면 다운로드 루프 문제를 해결하는 데 도움이 될 수 있습니다.

- v3.0.7부터는 릴리스 프로필 기반으로 우선 단어를 포함할 수도 있습니다. `{Preferred Words:<릴리스 프로필 이름>}`

- 우선 단어는 품질 및/또는 언어 커트오프가 충족되었더라도 항상 릴리스를 업그레이드합니다. 이는 프로필에서 `Upgrades`가 비활성화된 경우에도 해당됩니다.

> 우선 단어는 표준 시즌 팩 기본 설정을 무시합니다. 이는 [Sonarr Github 이슈 #3562](https://github.com/Sonarr/Sonarr/issues/3562)입니다. 우선 단어를 사용할 때 시즌 팩을 선호하려면 [시즌 팩 기본 설정을 추가해야 합니다](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs).
{.is-info}

- 태그는 어떤 시리즈에 릴리스 프로필이 적용되는지 제어하는 데 사용할 수 있습니다. 자세한 내용은 릴리스 프로필에 대한 설정 항목을 참조하세요.

- 우선 단어 및 릴리스 프로필에 대한 추가 정보는 [설정 페이지](/sonarr/settings#release-profiles)를 참조하세요.

## Windows 서비스에서 트레이 앱으로 변경하는 방법은 무엇인가요?

1. Sonarr를 종료합니다.
1. Sonarr 디렉토리에 있는 serviceuninstall.exe를 실행합니다.
1. 관리자 권한으로 Sonarr.exe를 한 번 실행하여 적절한 권한과 방화벽을 엽니다. 완료되면 Sonarr를 닫고 정상적으로 실행할 수 있습니다.
1. (선택 사항) 부팅 시 자동으로 시작하도록 Sonarr.exe에 바로 가기를 만듭니다.

## Sonarr를 백업/복원하는 방법은 무엇인가요?

### Sonarr를 백업하는 방법

#### 내장된 백업 기능 사용

- Sonarr UI에서 System => Backup으로 이동합니다.
- Backup 버튼을 클릭합니다.
- 백업이 생성된 후 zip 파일을 다운로드하여 안전한 위치에 보관합니다.

#### 파일 시스템 직접 사용

- Sonarr의 AppData 디렉토리 위치를 찾습니다.
  - Sonarr UI에서 System => About로 이동합니다.
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Sonarr를 중지합니다. 이렇게 하면 데이터베이스가 손상되는 것을 방지할 수 있습니다.
- 내용을 안전한 위치로 복사합니다.

### 백업에서 복원하는 방법

> 서로 다른 경로를 사용하는 운영 체제로 복원하는 것은 작동하지 않습니다(Windows에서 Linux로, Linux에서 Windows로, Windows에서 macOS로 또는 macOS에서 Windows로). macOS와 Linux 간의 이동은 `/` 대신 `\`를 사용하는 Windows와 달리 동작할 수 있지만 지원되지 않습니다. 데이터베이스의 모든 경로를 수동으로 편집하거나 [Toolbarr](https://github.com/Notifiarr/toolbarr)를 사용해야 합니다.
{.is-warning}

#### zip 백업 사용

- Sonarr를 다시 설치합니다(해당 사항이 없거나 이미 설치된 경우).
- Sonarr를 실행합니다.
- System => Backup으로 이동합니다.
- Restore Backup을 선택합니다.
- Choose File을 선택합니다.
- 백업 zip 파일을 선택합니다.
- Restore를 선택합니다.

#### 파일 시스템 백업 사용

- Sonarr를 다시 설치합니다(해당 사항이 없거나 이미 설치된 경우).
- Sonarr의 AppData 디렉토리 위치를 찾습니다.
  - Sonarr를 한 번 실행하고 UI에서 System => About로 이동합니다.
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Sonarr를 중지합니다.
- AppData 디렉토리의 내용(.db-wal/.db-journal 파일이 있는 경우 포함)을 삭제합니다.
- 백업에서 복원합니다.
- Sonarr를 시작합니다.
- 경로가 동일한 경우 모든 것이 이전 상태에서 계속됩니다.

#### Synology NAS에서 파일 시스템 복원

> 주의: Synology에서 복원하려면 Linux에 대한 지식과 Synology 장치에 대한 루트 SSH 액세스가 필요합니다.
{.is-warning}

- Sonarr를 다시 설치합니다(해당 사항이 없거나 이미 설치된 경우).
- Sonarr의 AppData 디렉토리 위치를 찾습니다.
  - Sonarr를 한 번 실행하고 UI에서 System => About로 이동합니다.
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Sonarr를 중지합니다.
- SSH를 통해 Synology NAS에 연결하고 root로 로그인합니다.

> 일부 설치에서 사용자가 아래 명령과 다를 수 있습니다: `chown -R sc-Sonarr:Sonarr *` {.is-info}

- 다음 명령을 실행합니다:

```shell
rm -r /usr/local/Sonarr/var/.config/Sonarr/Sonarr.db
cp -f /tmp/Sonarr_backup/* /usr/local/Sonarr/var/.config/Sonarr/
```

- 파일의 권한을 업데이트합니다:

 ```shell
cd /usr/local/Sonarr/var/.config/Sonarr/
chown -R Sonarr:users *
chmod -R 0644 *
```

- Sonarr를 시작합니다.

## 도움이 필요하여 자물쇠를 걸었습니다

{#help-i-have-forgotten-my-password}

> Sonarr의 v4에서는 `AuthenticationMethod` 타입 `None`은 더 이상 유효하지 않습니다. 비밀번호를 잊어버린 경우 [FAQ](/sonarr/faq-v4)를 참조하십시오.
{.is-info}

인증을 비활성화하려면 (잊어버린 사용자 이름이나 비밀번호를 재설정하려면) `config.xml`을 텍스트 편집기에서 열고 다음 단계를 수행해야 합니다.

1. `config.xml`을 텍스트 편집기에서 엽니다.
1. 인증 방법 라인을 찾습니다.
`<AuthenticationMethod>Basic</AuthenticationMethod>` 또는 `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. `AuthenticationMethod` 라인을 `<AuthenticationMethod>None</AuthenticationMethod>`로 변경합니다.
1. Sonarr를 재시작합니다.
1. 이제 Sonarr에 비밀번호 없이 액세스할 수 있으며, UI의 `Settings: General`로 이동하여 사용자 이름과 비밀번호를 설정해야 합니다.

## 왜 두 개의 파일이 있는 건가요? \| 왜 다운로드 폴더에 파일이 남아 있는 건가요?

이것은 정상입니다. [하드링크](https://trash-guides.info/hardlinks)를 지원하는 설정에서는 두 번의 공간을 사용하지 않습니다. 아래는 토렌트 프로세스의 작동 방식입니다.

1. Sonarr가 클라이언트에 다운로드 요청을 보내고, 해당 요청을 다운로드 클라이언트 설정에서 구성한 레이블 또는 카테고리 이름과 연결합니다. 예: 영화, TV, 시리즈, 음악 등.
1. Sonarr는 해당 카테고리 이름을 사용하여 다운로드 클라이언트의 활성 다운로드를 모니터링합니다. 이 모니터링은 다운로드 클라이언트의 API를 통해 수행됩니다.
1. 완료된 파일은 원래 위치에 남아 있어 파일을 시딩할 수 있도록 합니다(시딩 비율이나 시간은 다운로드 클라이언트나 특정 다운로드 클라이언트 아래에서 조정할 수 있습니다). 파일이 미디어 폴더로 가져오면 하드링크를 지원하는 경우 파일을 하드링크로 만들고, 그렇지 않은 경우 파일을 복사합니다.
1. Sonarr의 설정에서 "Completed Download Handling - Remove Completed" 옵션이 활성화된 경우, Sonarr는 다운로드 클라이언트에서 시딩이 완료되고 토렌트가 중지(일시 중지)된 경우에만 원본 파일과 토렌트를 삭제합니다. 다운로드 클라이언트가 완료된 시딩을 보고하는 경우에만 삭제됩니다. 다운로드 클라이언트를 최적으로 구성하는 방법은 [TRaSH의 Download Client Guides](https://trash-guides.info/Downloaders/)를 참조하십시오.

> 하드링크는 기본적으로 활성화되어 있습니다. [하드링크는 추가 디스크 공간을 사용하지 않습니다](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/). 완료된 다운로드 디렉토리와 미디어 라이브러리의 파일 시스템과 마운트는 동일해야 합니다. 하드링크 생성이 실패하거나 설정이 하드링크를 지원하지 않는 경우 파일이 복사됩니다.{.is-info}

## 기능/버그 X가 수정되었는데 왜 보이지 않을까요?

Sonarr는 `main`과 `develop` 두 가지 주요 코드 브랜치로 구성됩니다.

- `main`은 `develop` 브랜치가 안정적인 경우에 주기적으로 릴리스됩니다.
- `develop`은 사전 릴리스 테스트 및 고객이 사용할 수 있는 최신 버전입니다. 기능이 `develop`에 표시된 경우 해당 기능은 `develop` 브랜치를 실행하는 사용자에게만 사용할 수 있으며, `main`으로 이동한 후에 공식적으로 릴리스됩니다.

## 에피소드 진행 상황은 어떻게 계산되나요?

- 에피소드 수(Episode Count)와 파일이 있는 에피소드 수(Episode File Count)로 에피소드 수를 계산하는 두 가지 요소가 있습니다. 각각은 시리즈 또는 시즌의 전반적인 진행 상황을 제공하기 위해 약간 다른 로직을 사용합니다.

  - 에피소드 수 => 에피소드가 이미 방영되었고 모니터링 중이거나 - 에피소드에 파일이 있음
  - 파일이 있는 에피소드 수 => 에피소드에 파일이 있음

- 시리즈에 10개의 에피소드가 모두 방영되었고 파일이 없는 경우 0/10 에피소드가 표시됩니다. 해당 시리즈의 모든 에피소드를 모니터링 해제한 경우 0/0이 표시되며, 해당 시리즈의 모든 에피소드를 가져온 경우 모니터링 여부와 관계없이 10/10 에피소드가 표시됩니다.

## 다른 컴퓨터에서 Sonarr에 어떻게 접속할 수 있나요?

- 기본적으로 Sonarr는 모든 시스템에서의 요청을 수신하지 않습니다(관리자로 실행하지 않은 경우), 로컬호스트에서만 요청을 수신합니다. 이는 Sonarr가 Windows와 통합되는 방식에 따라 발생하는 것입니다(현재 대체 방법에도 동일하게 적용됩니다). Sonarr를 관리자로 실행하면 Windows에 올바르게 등록되고 방화벽 포트가 열리므로 네트워크의 다른 시스템에서 접근할 수 있습니다. 관리자로 실행하는 것은 한 번만 필요합니다(포트를 변경하는 경우 다시 실행해야 함).

## 왜 Sonarr가 시리즈 정보를 자주 새로 고치나요?

- Sonarr는 시리즈 및 에피소드 정보를 12시간마다 새로 고칩니다. 이는 공격적으로 보일 수 있지만 매우 중요한 프로세스입니다. TVDb 프록시에서 데이터를 새로 고치는 것은 새로운 에피소드 정보(방영일, 에피소드 수, 상태(계속/종료))를 동기화하기 위함입니다. 방영되지 않는 프로그램도 새로운 정보로 업데이트됩니다.
- 디스크 스캔은 덜 중요하지만 Sonarr가 정렬하지 않은 새로운 파일을 확인하고 삭제된 파일을 감지하는 데 사용됩니다.
- 가장 시간이 많이 소요되는 부분은 정보 새로 고침입니다(합리적인 디스크 액세스 속도를 가정할 때). 에피소드 수가 많은 경우 처리해야 할 에피소드 수가 많아져 시간이 더 걸립니다.

> 이 작업을 비활성화할 수는 없습니다. 이 작업이 오래 실행되어 문제가 있다고 생각되는 경우, 이 작업을 중지하는 대신 해결해야 할 다른 문제가 있는 것입니다.
{.is-warning}

## Activity 옆에 숫자가 있는 이유는 무엇인가요?

이 숫자는 다운로드 클라이언트의 대기열에 있는 에피소드 수와 이력에서 아직 가져오지 않은 마지막 60개 항목을 나타냅니다. 숫자가 파란색이면 정상적으로 작동하며 에피소드가 완료되면 가져옵니다. 노란색은 에피소드에 경고가 있는 경우를 의미합니다. 빨간색은 오류가 발생한 경우를 의미합니다. 노란색(경고) 및 빨간색(오류)의 경우 문제를 확인하려면 Activity에서 대기열을 확인해야 합니다(아이콘 위로 마우스를 올려서 자세한 내용을 확인할 수 있음).
다운로드 클라이언트의 대기열이나 이력에서 해당 항목을 제거해야 Sonarr의 대기열에서 제거할 수 있습니다.

## 시리즈 유형에는 어떤 종류가 있나요?

- 시리즈 유형은 Sonarr가 시리즈를 검색하는 방식에 영향을 미칩니다. 시리즈 유형은 인덱서에서 시리즈가 어떻게 발표되는지를 기반으로 하며, 실제로 시리즈의 '유형'은 아닙니다.
- 대부분의 프로그램은 `Standard`여야 합니다. 일일 프로그램은 일반적으로 날짜와 함께 발표되므로 `Daily`를 사용해야 합니다. 마지막으로 애니메이션은 일반적으로 `Anime`를 사용하지만 때로는 `Standard`가 더 잘 작동할 수 있으므로 문제가 발생하면 *다른* 유형을 시도해 보세요.
- 주의: 시리즈 유형이 애니메이션으로 설정되어 있고 활성화된 인덱서 중에 애니메이션 카테고리가 구성되지 않은 경우 해당 인덱서는 건너뛰게 되며 검색되지 않는 것처럼 보일 수 있습니다.
- 주의: 애니메이션 유형은 시즌 팩이나 시즌에 대한 개념이 없으며, 각 에피소드를 개별적으로 검색합니다.
- 주의: 모든 인덱서가 시즌/에피소드(표준) 검색을 지원하지는 않습니다.
- 시리즈 유형은 Mass Editor 또는 시리즈 보기에서 수정할 수 있습니다. 시리즈 유형은 가져올 때 선택할 수 있습니다.

- **Anime** - 절대 에피소드 번호를 사용하여 발표된 에피소드
- **Daily** - 매일 또는 그 이상의 간격으로 발표된 에피소드(yyyy-mm-dd 형식)
- **Standard** - SxxEyy 패턴으로 발표된 에피소드

### 시리즈 유형 예시

아래는 각 유형의 예시 발표 이름입니다. 구별되는 부분은 굵게 표시되어 있습니다.

> **Anime** 시리즈 유형을 사용하는 경우 [표준 유형으로도 인덱서를 검색할 수 있습니다.](/sonarr/settings#indexers)
{.is-info}

#### Daily

로그에는 `Searching indexers for [The Witcher : 2021-12-20]`가 표시됩니다.

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

로그에는 `Searching indexers for [The Witcher : S01E09]`가 표시됩니다.

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

로그에는 `Searching indexers for [The Witcher : S01E09 (09)]`가 표시됩니다.

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

## 시리즈 폴더 이름을 어떻게 변경할 수 있나요?

{#rename-folders}

> 동일한 프로세스가 시리즈 경로를 이동/변경하는 데도 적용됩니다.{.is-info}

Sonarr가 이미 일부 시리즈 폴더를 생성한 후에 시리즈 이름 형식을 조정한 경우 Sonarr는 기존 폴더의 이름을 자동으로 변경하지 않습니다. 이러한 폴더의 이름을 변경하려면 다음 단계를 수행해야 합니다.

1. Series
1. Mass Editor
1. 폴더 이름을 변경해야 하는 시리즈 선택
1. Root Folder를 현재 시리즈가 있는 동일한 Root Folder로 변경합니다.
1. "Yes move files"를 선택하여

> Plex 또는 Emby를 사용하는 경우 이렇게 하면 동영상 소개, 썸네일, 챕터 및 미리보기 메타데이터가 다시 감지됩니다.
{.is-warning}

## Sonarr를 어떻게 업데이트할 수 있나요?

- 설정으로 이동한 다음 일반 탭으로 이동하고 고급 설정을 표시합니다(저장 버튼 옆의 토글을 사용하여 표시).

1. 업데이트 섹션에서 브랜치 이름을 `main` 또는 `develop`로 변경합니다.
1. 저장합니다.

*이렇게 하면 해당 브랜치의 비트가 즉시 설치되지 않으며, 다음 업데이트 중에 설치됩니다.*

- main - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (기본/안정): 이 버전은 사용자가 nightly(`develop`) 브랜치에서 테스트한 후에는 알려진 중대한 문제가 없습니다. 이 브랜치는 대부분의 사용자에게 사용되어야 합니다. GitHub에서는 `main` 브랜치입니다.
- develop - ![Current Develop/Nightly](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (알파/불안정): 이 버전은 비공식적으로 릴리스되었으며, 일부 사용자가 사용하고 있습니다. GitHub에서는 `develop` 브랜치입니다.

> ~~**경고: `main`으로 전환한 후에는 다시 `main`으로 돌아갈 수 없습니다.** GitHub에서는 `develop` 브랜치입니다.~~
{.is-danger}

- v4 develop - ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (알파/불안정): **비-Docker 사용자의 경우 브랜치는 v4을 설치한 후에 `develop`입니다. Docker 사용자의 경우 이것은 `develop` 태그일 가능성이 높습니다.** 이것은 Sonarr v4 베타 버전의 최신 버전입니다. 코드가 커밋되고 모든 자동화된 테스트를 통과한 후에 즉시 릴리스됩니다. 이 빌드는 아직 사용자 또는 다른 사용자에 의해 사용되지 않았을 수 있습니다. 어떤 경우에는 실행되지 않을 수도 있습니다. 이 브랜치는 고급 사용자에게만 권장됩니다. 이 브랜치에서는 문제가 발생할 수 있으며, 문제 해결을 위해 스스로 조사해야 합니다. GitHub에서는 `develop` 브랜치입니다.

> **경고: v3(non-Docker) 설치는 직접 v4로 업그레이드할 수 없으며, Sonarr v4를 설치해야 합니다.**
{.is-info}

- 참고: Docker를 통해 설치한 경우 컨테이너 태그 뒤에 `:release`, `:latest`, `:nightly` 또는 `:develop`를 추가하십시오. 빌드를 제공하는 사람에 따라 다릅니다.

|                                                                    | `main` (stable) ![Current Main/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v3) (beta) ![Current v3 Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v4) (v4 beta) ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) |
|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [hotio](https://hotio.dev/containers/sonarr)                       | `release`                                                                                                                                                                                             | `nightly`                                                                                                                                                                                                   | `v4`                                                                                                                                                                                                            |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-sonarr) | `latest`                                                                                                                                                                                              | `3.0.10`                                                                                                                                                                                                     | `develop`                                                                                                                                                                                                       |

### 더 최신 버전 설치하기

#### Native

1. 시스템으로 이동한 다음 업데이트 탭으로 이동합니다.
2. 아직 설치되지 않은 더 최신 버전은 옆에 업데이트 버튼이 표시됩니다. 해당 버튼을 클릭하여 업데이트를 설치합니다.

> v3는 베타 v4로 업데이트할 수 없으며 수동으로 설치해야 합니다. [v4 베타 공지](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)를 참조하세요.
{.is-info}

#### Docker

1. 태그를 다시 가져오고 컨테이너를 업데이트합니다.

## `develop`에서 `main`으로 전환할 수 있나요?

- 아래 항목을 참조하세요.

## 브랜치 간에 전환할 수 있나요?

> (거의) 항상 위험을 증가시킬 수 있습니다.{.is-info}

- `main`에서 `develop`로 전환할 수 있습니다.
- 아래를 참조하거나 해당 빌드에 대해 `develop`에서 `main`으로 전환할 수 있는지 개발 팀과 확인하세요.
- 이 지침을 따르지 않으면 Sonarr이 사용할 수 없거나 오류가 발생할 수 있습니다. 아래와 같은 오류가 발생하면 이전 \*Arr 버전과 호환되지 않는 더 최신 데이터베이스를 사용하고 있습니다. 이전 버전과 동일한 버전 이상으로 \*Arr을 업그레이드하세요.
  - 예시 오류 메시지:
    - `Error parsing column 45 (Language=31 - Int64)`
    - `The DataMapper was unable to load the following field: 'Languages' value`
    - `ID does not match a known language Parameter name: id`
    - 기타 누락된 열이나 테이블과 관련된 유사한 데이터베이스 오류
- **2022년 8월 7일 업데이트**
  - `3.0.9.1549`가 main/stable로 출시되었습니다.
  - develop에서 `3.0.9.1549` 이하 버전을 사용하는 경우 main으로 안전하게 다운그레이드할 수 있습니다.
  - 더 최신 버전을 사용하는 경우 nightly/develop에 갇힐 수 있습니다. 이전 버전 이상으로 업그레이드하기 전에 백업을 만들고 복원할 수 있습니다. 안전하게 다운그레이드할 수 있는지 개발 팀과 확인하세요.

# Sonarr 및 시리즈 문제 + 메타데이터

## Sonarr은 씬 번호 매핑 문제를 어떻게 처리하나요 (American Dad! 등)?

### Sonarr이 씬 번호 매핑 문제를 처리하는 방법

- Sonarr은 사용자가 쇼 (파일을 게시하는 사람들)와 TheTVDb (일반적으로 네트워크의 번호 매기기를 따르는) 간의 매핑을 생성할 수 있는 커뮤니티 기반 사이트인 [TheXEM](http://thexem.info/)을 활용합니다. 이미 많은 쇼가 등록되어 있으며, 일반적으로 변경 사항은 몇 일 내에 승인됩니다 (정확한 경우). TheXEM은 에피소드 번호 매기기의 차이 (에피소드가 특별한 것인지 아닌지에 대한 불일치) 및 시즌 번호의 차이를 수정하는 데 사용됩니다. 예를 들어, 에피소드가 S10E01로 출시되었지만 TheTVDb에서는 동일한 에피소드를 S2017E01로 나열합니다.
- XEM은 일반적으로 씬의 번호 매기기와 TVDb의 번호 매기기가 일치하지 않을 때 문제를 해결하므로 Sonarr이 작동하지 않습니다. [XEM](http://thexem.info)이 Sonarr이 참조할 수 있는 맵을 생성합니다.
- 릴리스 그룹은 방송 방식에 따라 두 개의 에피소드를 하나의 파일로 묶지만 TVDb는 각 에피소드를 개별적으로 표시합니다.
- 릴리스 그룹은 시즌을 S2010으로 사용하고 TVDb는 S01을 사용합니다.
- [XEM](http://thexem.info)은 대부분의 경우에 작동하며 문제없이 유지됩니다. 그러나 대부분의 경우 문제가 발생할 수 있습니다.
- 특정 인덱서나 릴리스 그룹이 `Scene` (즉, XEM) 대신 TVDb를 따를 수 있습니다. 이를 관찰한 경우 씬 매핑 양식을 통해 제출하세요.
{.is-info}

- [서비스 요청된 매핑 *이미 요청되거나 추가된 별칭과 릴리스를 검토하고 확인하세요*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [서비스 씬 매핑 요청 양식 *별칭에 대한 새 요청을 만드세요. 양식을 완전히 작성하세요*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

### 문제가 있는 쇼

> 이 목록은 씬 매핑에 알려진 문제가 있는 쇼의 전체 목록이 아닙니다. 그러나 이 목록에는 일반적인 쇼가 포함되어 있습니다.
{.is-info}

- 알려진 쇼 및 문제점에 대한 불완전한 목록입니다:
- American Dad {#problemshow-americandad}
  - 네트워크 시즌 변경으로 인해 American Dad는 일반적으로 릴리스와 TVDb 사이에 1 시즌 차이가 있습니다. 자세한 내용은 XEM 맵을 참조하세요.
  - [American Dad](https://thexem.info/xem/show/4948)는 현재 TVDb 기준으로 S19 또는 Scene 기준으로 S18입니다. 따라서 Sonarr에서 시즌 19를 검색하면 XEM 맵 때문에 **오직** 시즌 18 결과만 반환됩니다.
  - 시즌 19 에피소드가 있는 인덱서 / 릴리스 그룹이 있는 경우 씬 매핑 양식을 통해 제출하고 이미 요청되지 않았는지 확인하세요.
    - [서비스 요청된 매핑 *이미 요청되거나 추가된 별칭과 릴리스를 검토하고 확인하세요*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [서비스 씬 매핑 요청 양식 *별칭에 대한 새 요청을 만드세요. 양식을 완전히 작성하세요*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- Paw Patrol {#problemshow-pawpatrol}
  - 더블 에피소드 파일 대 단일 에피소드 TVDb, 그리고 모든 에피소드가 더블이 아니기 때문에 맵이 잘못 추가될 수 있습니다.
- Pokémon {#problemshow-pokemon}
  - [Pokemon](http://thexem.info/xem/show/4638)은 TheXem에서 *더빙된* 에피소드를 추적합니다. 따라서 자막이 있는 에피소드를 원하는 경우 행운을 빕니다. 특정 릴리스 그룹이 TVDb를 따르고 XEM 매핑을 따르지 않는 경우 씬 매핑 양식을 통해 제출하고 이미 요청되지 않았는지 확인하세요.
    - [서비스 요청된 매핑 *이미 요청되거나 추가된 별칭과 릴리스를 검토하고 확인하세요*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [서비스 씬 매핑 요청 양식 *별칭에 대한 새 요청을 만드세요. 양식을 완전히 작성하세요*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- La Casa de Papel / Money Heist  {#problemshow-moneyheist}
  - TVDb에는 스페인 네트워크의 원래 방영 순서가 있지만 Netflix가 권리를 구매하여 시리즈를 다른 에피소드 수로 재편집했습니다. 이로 인해 "시즌 5"가 기존 "시즌 3" 에피소드 위에 가져와집니다. [추가 정보는 이 Reddit 스레드에서 확인할 수 있습니다](https://old.reddit.com/r/sonarr/comments/pdrr6l/money_heist_mess/).
- Kamen Rider {#problemshow-kamenrider}
  - 이 쇼는 앤솔로지 항목 ([TVDb ID 74096](https://thetvdb.com/series/kamen-rider))을 사용해야 Sonarr에서 자동화할 수 있습니다. 이 쇼는 앤솔로지 항목 (모든 시즌을 수집)과 TVDb에서 개별 시즌으로 별도의 항목으로 나열됩니다. [TheXEM](https://thexem.info/xem/show/5376)에서 앤솔로지 항목에 개별 시즌 이름 매핑이 있기 때문에 수동으로 다운로드하고 가져온 릴리스를 Sonarr에 추가할 수 없습니다.
- Bleach: Thousand-Year Blood War {#problemshow-bleach}
  - Bleach: Thousand-Year Blood War의 최신 시즌은 다양한 이름 매핑으로 출시되어 자동화하기 어렵고 기존 에피소드 중 일부를 덮어쓸 수 있습니다. 다음 중 하나에 해당하는 경우에만 자동화할 수 있습니다:
    - 에피소드를 S17Exx 번호로 출시하는 경우 또는
    - 올바른 Season 2 시리즈 제목으로 (여기에서 찾을 수 있음 <https://thexem.info/xem/show/5476>) 이 새로운 아크를 절대 에피소드 번호 1부터 시작하는 경우.
- Great Asian Railway Journeys {#problemshow-greatasianrail}
  - Great Asian Railway Journeys는 처음에 20개의 작은 에피소드로 방영되었지만 나중에 10개의 긴 에피소드로 재방영되었습니다. 이러한 긴 결합 에피소드는 특별 에피소드로 추가되어야 하며, 이에 따라 이름이 지정되어야 합니다. (S00E01 등)
- Horizon {#problemshow-horizon}
  - 1964년 이후로 가끔 에피소드를 방영하는 쇼입니다. 이로 인해 매핑이 특히 어려워집니다. [TheXEM](https://thexem.info/xem/show/5495)에서 확인할 수 있습니다. 관심이 있는 경우 Sonarr 디스코드에서 원래 토론을 찾을 수 있습니다. [여기](https://discord.com/channels/383686866005917708/649018968559845376/1046898050909622312).
- Kaleidoscope (2023) {#problemshow-kaleidoscope}
  - Kaleidoscope (2023)은 Netflix에서 비선형 쇼로 출시되었으며, 각 사용자가 시리즈를 시청할 때마다 다른 순서로 표시됩니다. 이로 인해 Sonarr에 문제가 발생하며, 릴리스 그룹에는 쇼에 대해 다른 에피소드 순서가 있습니다. 에피소드 매핑이 잘못되는 것을 방지하기 위해 Sonarr은 자동으로 에피소드를 가져오지 않으며, 에피소드를 수동으로 가져와서 가져와야 합니다. 에피소드 제목을 기준으로 일치시키거나 첫 몇 초를 미리보기하여 에피소드 '색상'이 제목과 일치하는지 확인할 수 있습니다.

다른 일반적인 문제가 발생하는 몇 가지 예시는 다음과 같습니다: Arrested Development, Kitchen Nightmares (US), Mythbusters, Pawn Stars.

## 왜 Sonarr이 X 시리즈의 에피소드 파일을 가져오지 못하거나 찾지 못할까요? / 왜 Sonarr이 X 시리즈의 릴리스를 찾지 못할까요?

특정 시리즈의 에피소드를 찾거나 가져오지 못하는 이유는 여러 가지가 있을 수 있습니다.

> Sonarr은 TVDb에서 별칭이나 번역(즉, 외국어 제목)을 사용하지 않습니다.
{.is-warning}

> **ID 기반 검색을 지원하는 인덱서의 경우**, 시리즈 TVDbID 또는 IMDbID를 사용하여 검색합니다. ID 기반 검색이 결과를 반환하지 않는 경우에만 시리즈 제목과 별칭이 사용됩니다.
{.is-info}

- Sonarr은 제목을 일치시킬 수 있도록 의존합니다. 종종 업로더는 다른 제목으로 에피소드를 게시합니다. 예를 들어, `CSI: Crime Scene Investigation`은 `CSI`로 게시됩니다. 따라서 Sonarr은 도움이 없이는 이름을 일치시킬 수 없습니다. 이러한 경우 Sonarr 팀이 유지 관리하는 Scene Mapping으로 처리됩니다.
- [문제가 있는 프로그램 및 릴리스 그룹 대 TVDb 번호 문제에 대한 FAQ 항목](#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)를 검토해보세요.

> **모든 일본 애니메이션의 경우, [thexem.info](https://thexem.info)에 별칭을 추가해야 합니다**. 새 매핑을 요청하려면 아래 단계를 따르세요. 추가 정보는 Sonarr Discord의 #XEM 채널에서 XEM 멤버들과 함께 찾을 수 있습니다.
{.is-danger}

- [서비스 요청 매핑 *별칭과 릴리스가 이미 요청되거나 추가되지 않았는지 확인하고 검토하세요*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [서비스 Scene Mapping 요청 양식 *별칭에 대한 새 요청을 작성하세요. 양식을 모두 작성하세요*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

> 일반적으로 서비스 요청은 1-5일 이내에 추가됩니다.
{.is-info}

> 다시 한 번 말하지만, 일본 애니메이션에 대해서는 매핑을 요청하지 마세요. XEM을 사용하세요.
> 추가 정보는 [\#XEM discord 채널](https://discord.gg/Z3D6u5hBJb)에서 XEM 멤버들과 함께 찾을 수 있습니다.
{.is-danger}

> 일본 애니메이션이 아닌 시리즈가 시즌 매핑을 필요로 하는 경우 (예: S25E26로 출시되었지만 TVDB는 S26E2로 표시되는 경우) XEM 매핑이 필요합니다. 이는 서비스 매핑으로 수행할 수 없습니다.
{.is-info}

> TVDb에는 "Helt Perfekt"라는 시리즈가 있으며, TVDb ID가 `343189` 및 `252077`입니다. 이 시리즈는 TVDb에서 동일한 이름을 가지고 있어 TVDb의 규칙을 위반합니다. 시리즈에 대한 첫 번째 항목이 이름을 얻습니다. 시리즈에 대한 이후 항목은 시리즈 이름에 연도를 포함해야 합니다. 그러나 씬 예외가 추가되어 (대소문자 구분 매핑) Helt Perfekt 릴리스에는 `NORWEGIAN`이 포함된 경우 -\> `252077` 및 `SWEDISH`가 포함된 경우 -\> `343189`로 매핑됩니다.
{.is-info}

## TVDb가 업데이트되었는데 Sonarr이 업데이트되지 않는 이유는 무엇인가요?

{#tvdb}

- TVDb는 API에 24시간 캐시를 사용합니다.
- TVDb의 API는 몇 시간이 걸리는 CDN 캐시를 통해 채워집니다.
- Sonarr의 Skyhook은 이를 위해 몇 시간 동안 작은 캐시를 가지고 있습니다.
- 게다가, Sonarr은 Refresh Series 작업을 매 12시간마다 실행합니다. 이 작업은 시스템 => 작업에서 수동으로 실행할 수 있습니다. 시리즈 인덱스에서 "모두 업데이트"를 선택하거나 해당 시리즈의 페이지에서 특정 시리즈를 수동으로 실행할 수도 있습니다.

- 따라서 TVDb의 변경 사항이 Sonarr에 자동으로 반영되려면 일반적으로 36~48시간(24 + ~3 + ~3 + 12)이 소요됩니다.

- TVDb에 시리즈 또는 에피소드가 누락된 경우, 추가된 시간부터 36~48시간이 소요됩니다.

{#missing-episodes}

- TVDb 업데이트가 48시간 이상 전에 이루어졌다고 알고 있다면, [Discord](https://discord.sonarr.tv/)에서 토론해주세요.

## 왜 시리즈를 추가할 수 없을까요?

{#why-can-i-not-add-a-new-series}

- TheTVDb가 사용 불가능한 경우 Sonarr은 검색 결과를 가져올 수 없으며 검색을 통해 새로운 시리즈를 추가할 수 없습니다. TVDbID를 알고 있다면 해당 ID로 시리즈를 추가하는 방법에 대해 UI에서 설명합니다.
- Sonarr은 영어 제목이 없는 시리즈를 추가할 수 없습니다. TVDb ID를 사용하여 시리즈를 추가하려고 하면 영어 제목이 없는 시리즈가 찾을 수 없습니다. TheTVDb에 해당 시리즈에 대한 영어 제목이 없는 경우, 해당 시리즈를 추가한 다음 [TVDb의 캐시가 지워질 때까지 기다려야 합니다](#tvdb).
- 해당 시리즈는 TV 시리즈여야 하며, 영화가 아니어야 합니다. TVDb에 존재해야 합니다. IMDB, TMDB 또는 다른 곳에 있지만 TVDb에 없는 경우 해당 시리즈를 추가할 수 없습니다.
- 해당 시리즈는 TVDb에 존재해야 합니다.
- 일부 시리즈는 사실상 주 시리즈의 연속이거나 시즌으로 간주될 수 있습니다.
  - 알려진 일부 시리즈/시즌은 다음과 같습니다:
  - [Dexter New Blood는 Season 9였지만 이제 [자체 시리즈](https://thetvdb.com/series/dexter-new-blood)입니다](https://thetvdb.com/series/dexter/seasons/official/9).

## TVDb ID를 알고 있는데 시리즈를 추가할 수 없는 이유는 무엇인가요?

{#why-cant-i-add-a-new-series-when-i-know-the-tvdb-id}

- Sonarr은 영어 제목이 없는 시리즈를 추가할 수 없습니다. TVDb ID를 사용하여 시리즈를 추가하려고 하면 영어 제목이 없는 시리즈가 찾을 수 없습니다. TheTVDb에 해당 시리즈에 대한 영어 제목이 없는 경우 (사용 가능한 경우) 해당 시리즈를 추가해야 합니다.
- URL 또는 시리즈를 확인하세요 - Sonarr은 영화를 지원하지 않습니다. 영화는 [Radarr](/radarr)를 사용하세요.

## Title Slug가 사용 중입니다

- 이 오류의 주요 원인은 다음과 같습니다.

## 중복된 이름이 있고 연도가 없습니다

- 이 오류는 TheTVDB에서 두 개의 시리즈가 동일한 제목으로 지정된 경우에 자주 발생합니다. 이 경우 두 번째 시리즈에는 시리즈 제목에 연도가 추가되어야 합니다.
  - Series A
  - Series A (2021)
- 이를 해결하려면 TVDb를 최종적으로 (아마도) 업데이트할 때까지 기다리세요. 또는 직접 TVDb를 업데이트하세요. **TVDb의 모더레이터가 승인한 후에만** Sonarr에서 수정된 제목을 사용하려면 업데이트 후 30시간 이상 기다려야 합니다.

## 중복된 이름이 있고 구두점이 다릅니다

- 구두점으로만 차이가 나는 두 개의 유사한 이름을 가진 시리즈의 경우, [Sonarr Discord](https://discord.sonarr.tv/)에서 이를 보고하세요.
  - Joe's Show (2022)
  - Joes Show (2022)

## 에피소드에 절대 번호가 없습니다

- TVDb의 에피소드에는 절대 번호가 지정되어 있지 않습니다. 필요한 경우 TVDb에서 시리즈를 업데이트하고 업데이트가 TVDb의 내부 캐시에서 지워질 때까지 36~48시간을 기다리세요.

## 에피소드 방영 시간

- Sonarr에서 브라우저에 표시되는 에피소드 방영 날짜와 시간은 클라이언트의 시간/시간대를 기준으로 합니다. 모든 시간은 Sonarr에서 브라우저로 UTC 시간(ISO-8601 형식)으로 전송됩니다.
- TVDb는 스트리밍 서비스에 대한 예외를 제외하고, 방영 네트워크의 로컬 시간을 기준으로 방영 시간과 날짜를 정의합니다. [자세한 내용은 TVDb의 FAQ 항목을 참조하세요](https://support.thetvdb.com/kb/faq.php?id=29).
- TVDb의 에피소드 방영 날짜와 방영 시간은 UTC로 변환되며, Sonarr 팀이 네트워크에 대해 Skyhook에서 매핑한 Sonarr의 시간대를 사용합니다.
  - 네트워크가 매핑되지 않은 경우 TVDb의 시간은 미국 동부 표준시 (UTC-5)로 가정됩니다.
  - 방영 시간이 네트워크의 로컬 시간대에서 브라우저의 시간대로 변환될 때 일치하지 않는 경우, 네트워크의 시간대를 Skyhook에 매핑하는 데 지원이 필요합니다. [개발 팀에 문의하여 네트워크의 시간대를 업데이트하는 데 도움을 받으세요](https://discord.sonarr.tv/).

# Sonarr 일반적인 문제

## 경로가 기존 시리즈에 이미 구성되어 있습니다

- 라이브러리 가져오기에서 "기존"이 표시되거나 "경로가 기존 시리즈에 구성되어 있습니다"라는 오류가 발생합니다.
- 이는 이미 다른 시리즈에 할당된 경로를 추가하거나 기존 시리즈의 경로를 편집하려고 할 때 발생합니다.
- 이는 사용자가 라이브러리를 가져올 때 일치하지 않는 시리즈를 수정하지 않은 것이 원인입니다.
- 해당 시리즈의 경로에 이미 할당된 영화를 찾아서 수정하세요.
  - 시리즈 인덱스
  - 테이블 보기
  - 옵션 => 열로 경로 추가
  - 정렬하여 문제가 있는 경로에 해당하는 영화 찾기
- 또는 기존 경로를 사용하여 Sonarr에서 시리즈를 삭제하세요.

## 시스템 및 로그가 영원히 로드됩니다

- 이는 easy-privacy 블록 목록 때문입니다. 이 목록은 /api/log?을 포함하는 모든 URL을 차단합니다. 목록을 검토하고 해당 목록의 모든 URL을 차단하는 것이 합리적인지 판단하세요. 여기에는 여러 사이트를 망가뜨릴 수 있는 수십 개의 URL이 포함되어 있습니다. 이를 귀하의 광고 차단기에서 선택한 것입니다. 가장 쉬운 해결책은 Sonarr이 실행 중인 도메인을 화이트리스트에 추가하는 것입니다. 그러나 목록을 확인하는 것을 권장합니다.

## 이상한 UI 문제

- 라이브러리 페이지가 아무 것도 표시하지 않거나 특정 보기나 정렬이 작동하지 않는 등 이상한 UI 문제가 발생하는 경우, Chrome 은닉 창이나 Firefox 개인 창에서 확인해보세요. 거기에서 정상적으로 작동한다면, 특정 IP/도메인에 대한 브라우저 캐시와 쿠키를 지우세요. 자세한 내용은 [캐시, 쿠키 및 로컬 스토리지 지우기](/useful-tools#clearing-cookies-and-local-storage) 위키 문서를 참조하세요.

## 웹 인터페이스가 Windows에서만 localhost에서 로드됩니다

- 웹 인터페이스에 <http://localhost:8989/> 또는 <http://127.0.0.1:8989>로만 접근할 수 있는 경우, 최소한 한 번은 관리자 권한으로 Sonarr을 실행해야 합니다.

## 팝업이 나타나 "config.xml이 손상되었으므로 열 수 없습니다"라는 메시지가 표시되었습니다. 이제 어떻게 해야 하나요?

- Sonarr은 구성 파일을 시작할 때 구성 파일을 읽을 수 없어서 이 오류가 발생합니다. Sonarr을 다시 온라인으로 만들려면 [AppData 폴더](/sonarr/appdata-directory)에서 `.xml`을 삭제한 다음 Sonarr을 시작하면 기본 포트(8989)에서 시작됩니다. 이제 일반 설정 페이지에서 구성한 설정을 다시 구성해야 합니다.

## 잘못된 인증서 및 기타 HTTPS 또는 SSL 문제

- Windows가 아닌 경우, 대부분의 경우 mono의 인증서가 오래되어 동기화되어야 합니다. [설치 문서의 mono ssl에 대한 섹션을 참조하세요](/sonarr/installation#mono-ssl-issues)
- 다운로드 클라이언트가 작동하지 않고 "Localhost는 잘못된 인증서입니다"와 같은 오류가 발생합니까?
  - Sonarr은 이제 SSL 인증서를 확인합니다. 다운로드 클라이언트에 SSL 인증서가 설정되어 있지 않거나 로컬 인증서 저장소에 CA 인증서가 추가되지 않은 자체 서명 HTTPS 인증서를 사용하는 경우 Sonarr은 연결을 거부합니다. 무료로 올바르게 서명된 인증서는 [let's encrypt](https://letsencrypt.org/)에서 제공됩니다.
  - 다운로드 클라이언트와 Sonarr이 동일한 컴퓨터에 있는 경우 HTTPS를 사용할 필요가 없으므로 가장 쉬운 해결책은 연결에 대해 SSL을 비활성화하는 것입니다. 대부분의 경우 로컬 네트워크에서도 필요하지 않습니다. 보안이 취약한 SSL 설정을 유지하려면 고급 설정에서 인증서 유효성 검사를 비활성화할 수 있습니다.

## 브라우저가 시작할 때마다 어떻게 브라우저를 중지할 수 있나요?

사용하는 운영체제에 따라 여러 가지 방법이 있습니다.

- 일부 운영체제의 `설정` => `일반`에서 시작할 때 브라우저를 실행하는 확인란이 있습니다.
- Sonarr을 호출할 때 인수에 `-nobrowser`(*nix) 또는 `/nobrowser`(Windows)를 추가할 수 있습니다.
- Sonarr을 중지하고 config.xml 파일을 편집하여 `<LaunchBrowser>True</LaunchBrowser>`를 `<LaunchBrowser>False</LaunchBrowser>`로 변경하세요.

## VPN, Jackett 및 \*ARRs

- 중국, 호주 또는 남아프리카와 같은 억압적인 국가가 아닌 경우, 토런트 클라이언트는 일반적으로 VPN 뒤에 있어야 하는 유일한 것입니다. VPN 종단점은 여러 사용자가 공유하기 때문에 각 소프트웨어가 사용하는 다양한 서비스에서 속도 제한, DDOS 보호 및 IP 차단을 경험할 수 있습니다.
- 즉, \*Arrs(Lidarr, Prowlarr, Radarr, Readarr 및 Lidarr)를 VPN 뒤에 두면 서비스에 액세스할 수 없어서 응용 프로그램을 사용할 수 없는 경우가 발생할 수 있습니다.

> **VPN이 \*Arrs와 충돌을 일으킬지 여부가 문제가 아니라, 언제 일어날지에 대한 문제입니다: 이미지 제공자는 차단될 것이고, 대부분의 \*Arr 서버(업데이트, 메타데이터 등) 앞에는 클라우드플레어가 있으며, 여기에서도 차단될 수 있습니다**
{.is-warning}

- **많은 개인 트래커에서 VPN 사용 또는 액세스(예: Jackett 또는 Prowlarr 사용)로 인해 금지될 수 있습니다.**

### VPN 사용

- VPN이 필요하고 Docker를 사용하는 경우 Hotio 또는 Binhex의 Download Client + VPN 컨테이너를 사용하는 것이 좋습니다.
- VPN이 필요하고 Docker를 사용하지 않는 경우 VPN 클라이언트가 필요한 앱만 VPN 뒤에 있도록 분할 터널링을 지원해야 합니다.
- 트래커에 액세스하는 데 문제가 있는 경우 ISP의 DNS 서버 대신 Google 또는 Cloudflare의 DNS 서버를 사용하여 문제를 해결할 수 있습니다.
- 일부 경우(예: 영국 ISP) 토런트 다운로드 클라이언트를 VPN 뒤에 두고 Jackett/Prowlarr를 다음과 같이 구성해야 할 수 있습니다:
  - Jackett을 VPN 뒤에 두고 분할 터널링이 로컬 액세스를 허용하도록 설정하세요.
  - Prowlarr의 경우 VPN 클라이언트를 구성하여 프록시를 제공하고 설정 => 인덱서에 프록시를 추가하세요. 프록시에 태그를 지정하고 해당 태그를 사용하는 인덱서를 동일한 태그로 지정하세요.
    - 필요한 경우 VPN에서 프록시를 생성하는 방법을 제공하지 않는 경우 Prowlarr을 VPN 뒤에 두고 분할 터널링이 로컬 액세스를 허용하도록 설정하세요.

## 내가 가지고 있지 않거나 원하지 않는 쇼에 대한 로그 메시지가 표시됩니다

- 이러한 메시지는 Sonarr이 에피소드를 원하는지 확인하기 위해 RSS 피드에서 가져오는 것이 완전히 정상적입니다. 일반적으로 이러한 메시지는 디버그/추적 로깅에서만 표시되지만, 항목 처리에 문제가 발생한 경우 경고 또는 오류가 표시될 수도 있습니다. 원하지 않는 쇼에 대한 경고/오류는 무시해도 안전하며, 원하는 쇼에 대한 경우 포럼에서 지원 스레드를 열어주세요.

## 시딩 중인 토런트가 자동으로 삭제되지 않습니다

- 아직 시딩 중인 토렌트가 가져오면, 토렌트 클라이언트가 계속 시딩할 수 있도록 복사하거나 하드 링크(활성화되어 있고 *가능한 경우*)됩니다. 이상적인 설정에서는 토렌트 다운로드 폴더와 라이브러리 폴더가 동일한 파일 시스템에 있으며, 하드 링크가 가능하고 낭비되는 공간을 최소화합니다.
- 또한 Sonarr에서 시드 시간/비율 목표를 구성하고 다운로드 클라이언트에서 해당 목표가 충족되면 일시 중지 또는 중지하도록 설정하고 완료 및 실패한 다운로드 핸들러 아래에서 제거를 활성화할 수 있습니다. 이렇게 하면 시딩이 완료된 토렌트가 Sonarr에 의해 다운로드 클라이언트에서 제거됩니다.

## 도움, 내 Mac에서 "개발자가 확인할 수 없으므로 Sonarr을 열 수 없습니다"라는 팝업이 나타납니다

- 이것은 간단한 문제입니다. 자세한 내용은 [여기](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)를 참조하세요.
[![개발자가 확인할 수 없음](/assets/general/faq_1_mac.png)]

## 도움, 내 Mac에서 Sonarr.app이 손상되었으므로 열 수 없습니다

- 이는 손상된 다운로드로 인한 것이므로 다시 시도하거나 [관련 FAQ 항목을 참조하세요](#help-my-mac-says-sonarr-cannot-be-opened-because-the-developer-cannot-be-verified).

## 오류: 데이터베이스 디스크 이미지가 손상되었습니다

> sqlite3를 3.41로 업그레이드한 후에 이 오류가 발생할 수 있습니다. Sonarr v3.0.9는 sqlite3 3.41을 지원하지 않습니다. 기본적인 변경 사항 때문에. [문제에 대한 자세한 내용은 Sonarr GHI #5464에서 확인할 수 있습니다](https://github.com/Sonarr/Sonarr/issues/5464)
> 이 문제는 Sonarr v3.0.10으로 해결되었으며 사용자는 Sonarr을 해당 버전으로 업그레이드해야 합니다.
{.is-warning}

- **`Error creating log database` 오류는 logs.db와 관련된 문제를 나타냅니다.**
  - 데이터베이스의 이름을 변경하거나 삭제하여 빠르게 해결할 수 있습니다. 로그 데이터베이스에는 명령 기록, 업데이트 설치 기록, 그리고 Info, Warn, Error 항목이 포함되어 있습니다.
- **`Error creating main database` 또는 일반적인 `database disk image is malformed` 오류는 sonarr.db와 관련된 문제를 나타냅니다.**
  - 아래에 나열된 단계를 따라 진행하세요.
- 이는 Sonarr의 대부분의 정보를 저장하는 SQLite 데이터베이스가 손상되었음을 의미합니다. 가능한 옵션은 (a) 백업을 시도하거나, 기존 데이터베이스를 복구하거나, 백업을 복구하거나, 모든 것이 실패한 경우 새로운 데이터베이스로 다시 시작하는 것입니다.
- 이 오류는 데이터베이스 파일이 \*Arr가 실행되는 사용자/그룹에 의해 쓰기 가능하지 않을 때 발생할 수 있습니다. 권한 문제는 일반적으로 새로 설치한 경우, 새 서버로 마이그레이션한 경우, 최근에 appdata 디렉토리 권한을 수정한 경우, 또는 \*Arr가 실행되는 사용자와 그룹을 변경한 경우에만 문제가 될 수 있습니다.
- 가장 좋고 첫 번째 옵션은 [백업에서 복원을 시도하는 것입니다](#how-do-i-backuprestore-my-sonarr).
- 데이터베이스를 복구하는 것도 시도해볼 수 있습니다. 이 문제가 업데이트 후에 발생한 경우에는 일반적으로 유일한 옵션입니다. [sqlite3 `.recover` 명령](/useful-tools#recovering-a-corrupt-db)을 시도해보세요.
  - 만약 sqlite에 `.recover`가 없거나 더 GUI(예: Windows) 친화적인 방법을 원한다면 [이 위키의 지침을 따르세요](/useful-tools#recovering-a-corrupt-db-ui).
- 데이터베이스 오류의 또 다른 가능한 원인은 데이터베이스를 네트워크 드라이브(nfs 또는 smb 또는 다른 로컬이 아닌 드라이브)에 위치시키는 것입니다. **SQLite는 데이터와 응용 프로그램이 동일한 컴퓨터에 함께 있는 상황을 위해 설계되었습니다.** 따라서 \*Arr AppData 폴더(/config 도커 마운트)는 로컬 스토리지에 있어야 합니다. [SQLite와 네트워크 드라이브는 함께 사용할 수 없으며 결국 손상된 데이터베이스를 일으킬 수 있습니다](https://www.sqlite.org/draft/useovernet.html).
- 만약 mergerFS를 사용 중이라면 SQLite가 mmap을 사용하기 때문에 `direct_io`를 제거해야 합니다. 이에 대한 자세한 내용은 mergerFS [문서](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)를 참조하세요.

## 나는 Mac에서 Sonarr을 사용하고 갑자기 작동이 멈췄습니다. 무슨 일이 있었나요?

- 아마도 이는 MacOS 버그로 인해 Sonarr 데이터베이스 중 하나가 손상되었기 때문입니다.
- [다음 단계를 따라 해결하세요](#i-am-getting-an-error-database-disk-image-is-malformed).
- 그런 다음 Sonarr을 실행해보고 작동하는지 확인하세요. 작동하지 않는 경우 추가 지원이 필요합니다. [reddit](http://reddit.com/r/Sonarr)에 게시하거나 [discord](https://discord.sonarr.tv/)에서 도움을 받으세요.

## 왜 Sonarr이 원격 서버의 파일을 볼 수 없을까요?

- 모든 OS에서 \*Arr로 실행 중인 사용자/그룹이 마운트된 드라이브에 대한 읽기 및 쓰기 권한을 갖고 있는지 확인하세요.
- Linux의 경우 다음을 확인하세요:
  - NFS 마운트를 사용하는 경우 마운트에 `nolock`이 활성화되어 있는지 확인하세요.
  - SMB 마운트를 사용하는 경우 마운트에 `nobrl`이 활성화되어 있는지 확인하세요.
- Windows의 경우: 간단히 말해서, \*Arr가 실행 중인 사용자(서비스인 경우) 또는 하위에서 파일 경로에 액세스할 수 없습니다. 이는 다양한 이유로 발생할 수 있지만 가장 일반적인 이유는 \*Arr가 서비스로 실행되기 때문에 아래에 설명된 문제가 발생하는 것입니다.

### Sonarr은 기본적으로 LocalService 계정에서 실행되며 보호된 원격 파일 공유에 액세스할 수 없습니다.

- Sonarr 서비스를 해당 공유에 액세스할 수 있는 다른 사용자로 실행합니다.
- Windows 서버에서 관리 도구 \> 서비스 창을 엽니다.
- Sonarr 서비스를 중지합니다.
- 속성 \> 로그온 대화상자를 엽니다.
- 서비스 사용자 계정을 대상 사용자 계정으로 변경합니다.
- 시작 프로그램 폴더에서 Sonarr.exe를 실행합니다.

### 매핑된 네트워크 드라이브를 사용 중입니다 (UNC 경로가 아님)

- 경로를 UNC 경로(`\\서버\공유`)로 변경하세요.
- 시작 프로그램 폴더에서 Sonarr.exe를 실행합니다.

## 매핑된 네트워크 드라이브 대 UNC 경로

- 매핑된 네트워크 드라이브를 사용하는 것은 일반적으로 잘 작동하지 않습니다, 특히 Sonarr이 서비스로 구성된 경우입니다. 공유를 설정하는 더 좋은 방법은 UNC 경로를 사용하는 것입니다. 따라서 `X:\TV` 대신 `\\서버\TV`를 사용하세요.

- 기억해야 할 중요한 점은 Sonarr이 경로 정보를 다운로더에서 가져온다는 것입니다. 따라서 NZBGet, SABNzbd 또는 기타 다운로더도 UNC 경로를 사용하도록 설정해야 합니다.

## Sonarr은 Big Sur에서 작동하지 않습니다

다음을 실행하세요.

```shell
chmod +x /Applications/Sonarr.app/Contents/MacOS/Sonarr
```

## v2에서 업그레이드한 후 내 사용자 지정 스크립트가 작동하지 않습니다

- 아마도 연결에 인수를 전달하고 있는 것 같습니다. 이는 지원되지 않습니다.
- 다음을 수행하여 이를 수정하세요:
  1. 인수를 경로로 변경하세요.
  1. 스크립트의 shebang이 pwsh 경로에 매핑되도록 확인하세요 (shebang 정의가 없는 경우 추가하세요).
  1. pwsh 스크립트가 실행 가능한지 확인하세요.

# Sonarr 검색 및 다운로드 일반 문제

## 쿼리 성공 - 결과가 반환되지 않음

- [다음 문제 해결 항목을 참조하세요](/sonarr/troubleshooting#query-successful-no-results-returned)

## Sonarr이 기대한 에피소드를 다운로드하지 않은 이유는 무엇인가요?

먼저, ["Sonarr은 에피소드를 어떻게 찾나요?"](#how-does-sonarr-find-episodes)라는 섹션을 읽고 이해했는지 확인하세요. 그런 다음 적어도 하나의 인덱서가 기대한 에피소드를 가지고 있는지 확인하세요.

1. Sonarr에서 에피소드 목록 옆에 있는 '수동 검색' 아이콘을 클릭하세요. 결과가 있는지 확인하세요. 결과가 없다면 Sonarr이 인덱서와 통신하는 데 문제가 있거나 인덱서에 해당 에피소드가 없거나, 에피소드가 잘못된 이름/분류로 인덱서에 등록되어 있을 수 있습니다.
1. **2단계에서 결과가 있다면**, 해당 결과 옆에 붉은 느낌표 아이콘을 확인하세요. 아이콘 위로 마우스를 올려놓으면 해당 릴리스가 자동 다운로드 후보로 선정되지 않은 이유를 확인할 수 있습니다. 모든 결과에 아이콘이 있는 경우 자동 다운로드가 발생하지 않습니다.
1. **2단계에서 적어도 하나의 유효한 수동 검색 결과가 있다면**, 자동 다운로드가 발생해야 합니다. 그렇지 않은 경우 RSS 동기화를 방해하는 일시적인 통신 문제가 가장 가능성이 높습니다. 최상의 결과를 얻기 위해 여러 인덱서를 설정하는 것이 좋습니다.
1. **특정 쇼에 대한 수동 결과가 없지만 인덱서 웹 사이트에서 찾을 수 있다면** - 이는 다양한 이유로 발생할 수 있습니다. 예를 들어, 인덱서에서 제대로 태그가 지정되지 않은 경우에는 자동 검색 결과로 Sonarr에 반환되지 않을 수 있습니다. 이 [문제 해결 항목](/sonarr/troubleshooting#searches-indexers-and-trackers)에서 원인을 확인하는 데 도움이 되는 팁을 제공합니다. 여러 인덱서를 활성화하면 동일한 콘텐츠에 대해 더 많은 소스를 제공하여 이 문제를 해결하는 데 도움이 될 수 있습니다.

## 일치하는 시리즈를 찾았지만 릴리스가 ID로 시리즈와 일치되어 자동 가져오기가 불가능합니다

- [다음 문제 해결 항목을 참조하세요](/sonarr/troubleshooting#found-matching-series-via-grab-history-but-series-was-matched-by-series-id-automatic-import-is-not-possible)

- TVDb에서 에피소드 이름이 알려지지 않은 경우 TBA로 제목이 지정되며 TVDb API에는 24시간 캐시가 있습니다. 일반적으로 TVDb 웹 사이트의 변경 사항은 TVDb 캐시(24시간), skyhook 캐시(몇 시간) 및 시리즈 새로 고침 간격(12시간마다)으로 인해 Sonarr에 도달하는 데 24-48시간이 걸립니다. [에피소드 제목 필수 설정](/sonarr/settings#importing)은 제목이 TBA인 경우 가져오기 동작을 제어하지만, 시리즈 방영 후 48시간이 지나면 제목이 여전히 TBA인 경우에도 릴리스가 가져와집니다. 또한 TBA로 제목이 지정된 파일의 자동 이름 변경은 없습니다. TBA 타이머는 에피소드 방영 날짜와 시간에서 계산되며, 다운로드한 시간이나 업로드 시간에서 계산되지 않습니다.

## Sonarr이 검색 또는 가져오기에서 알 수 없는 시리즈로 표시됩니다

- [다음 항목을 참조하세요](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x)

## Jackett의 /all 엔드포인트

{#jackett-all-endpoint}

- Jackett의 `/all` 엔드포인트는 편리하지만 그것이 유일한 이점입니다. 그 외의 모든 것은 잠재적인 문제입니다. 따라서 각 트래커를 개별적으로 추가해야 합니다. 또는 Jackett 및 NZBHydra2 대체제인 [Prowlarr](/prowlarr)을 확인해볼 수 있습니다.

- **2022년 2월 5일 업데이트: jackett `\all` 엔드포인트에 대한 \*Arr 지원이 중단되었습니다. v3.0.6.1457부터 Jackett /all 엔드포인트는 더 이상 지원되지 않습니다(경고가 발생합니다) 이는 문제만 야기하기 때문입니다.**

- Jackett의 `/all` 엔드포인트는 편리하지만 그것이 유일한 이점입니다. 그 외의 모든 것은 잠재적인 문제입니다. 따라서 이제는 각 트래커를 개별적으로 추가해야 합니다.
- [Jackett 개발자도 사용을 피하고 사용하지 말아야 한다고 말하고 있습니다](https://github.com/Jackett/Jackett#aggregate-indexers).
- `/all` 엔드포인트를 사용하는 것은 이점이 없으며 다음과 같은 단점이 있습니다:
  - 인덱서별 설정(카테고리, 검색 모드 등)을 제어할 수 없습니다.
  - 검색 모드(IMDB, 쿼리 등)를 혼합하면 품질이 낮은 결과가 발생할 수 있습니다.
  - 인덱서별 카테고리(100000 이상)를 사용할 수 없습니다.
  - 느린 인덱서는 전체 결과 속도를 늦출 수 있습니다.
  - 총 결과는 1000개로 제한됩니다.
  - `/all`의 트래커 중 하나가 오류를 반환하면 \*Arr은 해당 트래커를 비활성화하고 결과를 얻을 수 없게 됩니다.

### Jackett /All 해결 방법

- Jackett에서 각 트래커를 수동으로 인덱서로 추가하세요.
- \*Arr에 인덱서를 동기화할 수 있는 [Prowlarr](/prowlarr)을 확인하세요. 이는 Lidarr/Radarr/Readarr 개발팀에서 제공합니다.
- 인덱서를 \*Arr에 동기화할 수 있는 [NZBHydra2](https://github.com/theotherp/nzbhydra2)를 확인하세요. 그러나 단일 집계 엔드포인트를 사용하지 마세요. 대신 동기화에 `multi`를 사용하세요.

## Jackett의 수동 검색에서 Sonarr보다 더 많은 결과가 표시됩니다

- Sonarr에서 구성된 트래커의 카테고리를 확인하세요.
- 이는 Sonarr이 Jackett에서 수동 검색을 다르게 수행하기 때문입니다. [자세한 내용은 이 문제 해결 기사를 참조하세요](/sonarr/troubleshooting#searches-indexers-and-trackers).

## 쿠키 찾기

- 일부 사이트는 자동으로 로그인할 수 없으며 쿠키를 수동으로 로그인한 후 Sonarr에 제공해야 작동합니다. [자세한 내용은 이 문서를 참조하세요](/useful-tools#finding-cookies).

## 토렌트 압축 해제

- 대부분의 토렌트 클라이언트는 유넷과 달리 자동으로 압축된 아카이브를 처리하지 않습니다. [unpackerr](https://github.com/unpackerr/unpackerr)를 추천합니다.

## 권한

- Sonarr은 다운로더가 파일을 넣은 위치에서 최종 위치로 파일을 이동해야 하므로 Sonarr은 소스 및 대상 디렉토리 및 파일에 대해 읽기/쓰기 권한이 필요합니다.
- 서비스가 자체 사용자로 실행되는 Linux에서는 공유 그룹을 사용하고 다운로더와 Sonarr 모두에서 폴더 권한을 `775`로, 파일 권한을 `664`로 설정해야 합니다. umask 표기법으로는 `002`입니다.

## 강제 인증

- Sonarr v4 (베타)에서는 인증이 필수입니다. 자세한 내용은 [Sonarr v4 FAQ - 강제 인증](/sonarr/faq-v4#forced-authentication)을 참조하세요.