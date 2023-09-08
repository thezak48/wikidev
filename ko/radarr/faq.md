## 모든 영화 파일을 하나의 폴더에 저장할 수 있나요?

- 네, Radarr은 모든 영화 파일을 하나의 폴더에 저장할 수 있습니다. 이를 위해 다음 단계를 따르세요:

1. Radarr 웹 인터페이스에서 `Settings`로 이동합니다.
2. `Media Management` 탭을 선택합니다.
3. `File Management` 섹션에서 `Enable`을 선택합니다.
4. `Movies` 폴더 경로를 지정합니다. 모든 영화 파일이 이 폴더에 저장됩니다.
5. 변경 사항을 저장합니다.

이제 Radarr은 모든 영화 파일을 지정한 폴더에 저장합니다.

- 아니오, 그 이유는 Radarr가 [Sonarr](/sonarr)의 포크이기 때문입니다. Sonarr에서는 각 쇼마다 폴더가 있습니다. 이 제한은 많은 사용자들에게 고통스러운 문제로 알려져 있으며, 앞으로의 버전에서 개선될 수도 있습니다. 이것은 단순한 변경이 아니며, 백엔드 전체를 다시 작성해야 합니다.
- [Custom Folder GitHub Issue](https://github.com/Radarr/Radarr/issues/153)는 기술적으로 이 요청을 다루지만, 해당 시기에 모든 영화 파일을 하나의 폴더에 구현할 것을 보장하지는 않습니다.
- 아래에는 약간의 해킹적인 해결책이 설명되어 있습니다. Radarr에서 리스캔을 트리거하지 않도록 주의하십시오. 그렇지 않으면 영화가 누락된 것으로 표시되고 영화가 업그레이드되지 않을 것입니다.
  - 사용자 정의 스크립트 사용
    - 스크립트는 가져올 때 트리거되어야 합니다.
    - 원하는 시기에 파일을 이동하도록 설계되어야 합니다.
    - 그런 다음 Radarr API를 호출하여 영화를 모니터링하지 않도록 변경해야 합니다.
- 모든 영화를 하나의 폴더로 이동하려는 경우 [팁 및 트릭 섹션 => 각 영화에 대한 폴더 만들기](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) 문서를 확인하십시오.

## 내 라이브러리의 모든 영화를 하나의 폴더에 넣을 수 있나요?

- 아니요, 위에서 설명한 대로입니다.

## Radarr를 어떻게 업데이트할 수 있나요?

- 설정으로 이동한 다음 일반 탭으로 이동하고 고급 설정을 표시합니다 (저장 버튼 옆의 토글을 사용합니다).

1. 업데이트 섹션에서 브랜치 이름을 `master` 또는 `develop`로 변경합니다.
1. 저장합니다.

*이렇게 하면 해당 브랜치의 비트가 즉시 설치되지는 않으며, 다음 업데이트 중에 설치됩니다.*

- ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (기본/안정): 개발 및 매일 빌드 브랜치에서 사용자들에 의해 테스트되었으며, 주요한 문제가 없는 것으로 알려져 있습니다. 이 버전은 대략 한 달에 한 번 업데이트를 받습니다. GitHub에서는 `master` 브랜치입니다.

- ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (베타): 이것은 테스트 엣지입니다. 매일 빌드에서 테스트된 후 릴리스됩니다. 매일 빌드 이후에 새로운 기능과 버그 수정이 여기에서 먼저 릴리스됩니다. 상대적으로 안정적이지만 여전히 `베타`입니다. 이 버전은 개발에 따라 주간 또는 격주로 업데이트를 받습니다.

> **경고: `develop` 브랜치로 전환한 후에는 `master`로 돌아갈 수 없을 수도 있습니다.** GitHub에서는 특정 시점에서 `develop` 브랜치의 스냅샷입니다.
{.is-warning}

- ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (알파/불안정): 이것은 최신 개발 버전입니다. 코드가 커밋되고 모든 자동화된 테스트를 통과한 즉시 릴리스됩니다. 이 빌드는 아직 저희나 다른 사용자들에 의해 사용된 적이 없을 수 있습니다. 경우에 따라 실행되지 않을 수도 있습니다. 이 브랜치는 고급 사용자에게만 권장됩니다. 이 브랜치에서는 문제가 발생하고 자체 조사가 예상됩니다.  ***이 브랜치는 실패한 업데이트를 복구하기 위해 손을 더럽힐 준비가 되어 있는 경우에만 사용하십시오.*** 이 버전은 즉시 업데이트됩니다.

> **경고: `develop` 브랜치로 전환한 후에는 `master`로 돌아갈 수 없을 수도 있습니다.** GitHub에서는 `develop` 브랜치입니다.
{.is-danger}

- 참고: Docker를 통해 설치한 경우 컨테이너 태그 끝에 `:release`, `:latest`, `:testing` 또는 `:develop`를 추가하십시오. 빌드를 제공하는 사람에 따라 다릅니다.

|                                                                    | ![Current Master/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Current Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Docker 컨테이너 내에서 Radarr를 업데이트할 수 있나요?

- *기술적으로는 가능합니다.* **하지만 절대로 하지 마십시오.** 이것은 Docker의 주요 철학입니다. 가장 최신의 `nightly`로 설치를 업그레이드하고 Docker 컨테이너 자체를 업데이트하면 (이전 버전으로 다운그레이드할 수도 있음) 데이터베이스 문제가 발생할 수 있습니다.

### 더 최신 버전 설치하기

#### Native

1. 시스템으로 이동한 다음 업데이트 탭으로 이동합니다.
1. 아직 설치되지 않은 더 최신 버전에는 옆에 업데이트 버튼이 표시됩니다. 해당 버튼을 클릭하여 업데이트를 설치합니다.

#### Docker

1. 태그를 다시 가져오고 컨테이너를 업데이트합니다.

## `nightly`에서 `develop`로 전환할 수 있나요?

## 브랜치 간에 전환할 수 있나요?

- 버전이 동일한 경우 전환할 수 있습니다. 그렇지 않으면 해당 빌드에 대해 `nightly`에서 `master`로 전환할 수 있는지, `nightly`에서 `develop`로 전환할 수 있는지, 또는 `develop`에서 `master`로 전환할 수 있는지 개발 팀과 확인하십시오.
- 이 지침을 따르지 않으면 Radarr가 사용할 수 없거나 오류가 발생할 수 있습니다. 아래와 같은 오류가 발생하면 새로운 데이터베이스를 사용하여 이전 버전의 \*Arr을 사용하는 것이 지원되지 않습니다. 이전 버전의 \*Arr으로 업그레이드하거나 그 이상의 버전으로 업그레이드하십시오.
  - 예시 오류 메시지:
    - `Error parsing column 45 (Language=31 - Int64)`
    - `The DataMapper was unable to load the following field: 'Languages' value`
    - `ID does not match a known language Parameter name: id`
    - 기타 유사한 열이나 테이블이 누락된 데이터베이스 오류입니다.

## Radarr를 백업/복원하는 방법은 무엇인가요?

### Radarr 백업하기

#### 내장된 백업 사용

- Radarr UI에서 시스템 => 백업으로 이동합니다.
- 백업 버튼을 클릭합니다.
- 백업이 생성된 후 zip 파일을 다운로드하여 안전한 위치에 보관합니다.

#### 파일 시스템 직접 사용

- Radarr의 AppData 디렉토리 위치를 찾습니다.
  - Radarr UI에서 시스템 => 정보로 이동합니다.
  - [Radarr Appdata 디렉토리](/radarr/appdata-directory)
- Radarr를 중지합니다. - 데이터베이스가 손상되는 것을 방지합니다.
- 내용을 안전한 위치로 복사합니다.

### 백업에서 복원하기

> 서로 다른 경로를 사용하는 OS로 복원하는 것은 작동하지 않습니다 (Windows에서 Linux로, Linux에서 Windows로, Windows에서 OS X로 또는 OS X에서 Windows로). OS X와 Linux 간의 이동은 가능할 수 있지만, Windows에서 사용하는 `\` 대신 `/`를 포함하는 경로를 사용하기 때문에 지원되지 않습니다. 데이터베이스의 모든 경로를 수동으로 편집하거나 [Toolbarr](https://github.com/Notifiarr/toolbarr)를 사용해야 합니다.
{.is-warning}

#### zip 백업 사용

- Radarr를 다시 설치합니다 (해당되는 경우/이미 설치되어 있지 않은 경우).
- Radarr를 실행합니다.
- 시스템 => 백업으로 이동합니다.
- 백업 복원을 선택합니다.
- 파일 선택을 선택합니다.
- 백업 zip 파일을 선택합니다.
- 복원을 선택합니다.

#### 파일 시스템 백업 사용

- Radarr를 다시 설치합니다 (해당되는 경우/이미 설치되어 있지 않은 경우).
- Radarr의 AppData 디렉토리 위치를 찾습니다.
  - Radarr를 한 번 실행하고 UI에서 시스템 => 정보로 이동합니다.
  - [Radarr Appdata 디렉토리](/radarr/appdata-directory)
- Radarr를 중지합니다.
- AppData 디렉토리의 내용을 삭제합니다. **(.db-wal/.db-journal 파일이 있는 경우 포함)**
- 백업에서 복원합니다.
- Radarr를 시작합니다.
- 경로가 동일한 경우 모든 것이 이전 상태에서 계속됩니다.

#### Synology NAS에서 파일 시스템 복원

> 주의: Synology에서 복원하려면 Linux에 대한 지식과 Synology 장치에 대한 루트 SSH 액세스가 필요합니다.
{.is-warning}

- Radarr를 다시 설치합니다 (해당되는 경우/이미 설치되어 있지 않은 경우).
- Radarr의 AppData 디렉토리 위치를 찾습니다.
  - Radarr를 한 번 실행하고 UI에서 시스템 => 정보로 이동합니다.
  - [Radarr Appdata 디렉토리](/radarr/appdata-directory)
- Radarr를 중지합니다.
- SSH를 통해 Synology NAS에 연결하고 root로 로그인합니다.

> 일부 설치에서 사용자가 아래 명령과 다른 경우가 있습니다: `chown -R sc-Radarr:Radarr *` {.is-info}

- 다음 명령을 실행합니다:

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- 파일의 권한을 업데이트합니다:

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- Radarr를 시작합니다.

# Radarr 일반적인 문제

## 작업이 취소되었습니다

- Radarr가 요청을 보낸 서버로부터 100초 동안 응답이 없었습니다.
- 로그에는 `System.Threading.Tasks.TaskCanceledException: A task was canceled.`가 포함됩니다.
- 이는 일반적으로 다음과 같은 이유로 발생합니다:
  - 잘못 구성된 VPN의 사용 또는 구성
  - 잘못 구성된 프록시의 사용 또는 구성
  - 로컬 DNS 문제 - 다른 DNS 공급자로 변경해 보십시오.
  - 로컬 IPv6 문제 - *가장 일반적인 경우* - 일반적으로 호스트 시스템에서 IPv6가 활성화되어 있지만 기능하지 않습니다.
  - Privoxy의 사용 및 잘못된 구성
  - PiHole [Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit) 요청
- DNS를 사용하여 문제 해결할 수 있습니다. `nslookup <추적 로그에서의 도메인.tld>` 및 ipv6를 사용하여 `curl -sv -6 "<추적 로그에서의 URL>"` 또는 다른 연결을 사용하여 `curl -sv -4 "<추적 로그에서의 URL>"`을 사용하여 ipv6를 사용하여 문제를 해결할 수 있습니다.

## 경로가 이미 기존 영화에 구성되어 있습니다

![existing-movie.png](/assets/radarr/existing-movie.png)

- 라이브러리 가져오기에서 "기존"이 표시되거나 "경로가 기존 영화에 구성되어 있음" 오류가 발생합니다.
- 이는 이미 다른 영화에 할당된 경로를 추가하거나 기존 영화의 경로를 편집하려고 할 때 발생합니다.
- 아마도 사용자가 라이브러리를 가져올 때 올바르지 않은 영화를 수정하지 않았기 때문입니다.
- 이미 그 경로에 할당된 영화를 찾아서 수정하십시오.
  - 영화 인덱스
  - 테이블 보기
  - 옵션 => 열로 경로 추가
  - 정렬하여 해당 문제가 있는 경로에 있는 영화를 찾습니다.
- 또는 Radarr에서 해당 경로를 사용하는 영화를 삭제합니다.

## 영화 폴더 이름을 어떻게 변경할 수 있나요?

{#rename-folders}

> 동일한 절차가 영화 경로를 이동/변경하는 데도 적용됩니다. Radarr에서 경로를 업데이트하고 파일을 이동할 필요가 없는 경우 단계 5에서 "예, 파일 이동"을 선택하지 마십시오.
{.is-info}

1. 영화
1. 영화 편집기
1. 폴더 이름을 바꿀 영화 선택
1. 루트 폴더를 현재 영화가 있는 루트 폴더로 변경
1. "예, 파일 이동" 선택

> Plex를 사용하는 경우 이로 인해 인트로, 썸네일, 챕터 및 미리보기 메타데이터가 다시 감지됩니다.
{.is-warning}

## 영화 파일 및 폴더 이름 지정

- 현재 Radarr는 각 영화가 적어도 `영화 제목 (연도)/` 형식의 폴더에 있어야 한다고 요구합니다. 선택적으로 `_` 또는 `.`는 유효한 구분자입니다. 가져오기 중 올바른 품질 및 해상도 식별을 용이하게 하기 위해 `영화 제목 (연도) [품질-해상도].ext`와 같은 파일 이름이 가장 좋습니다. 다시 말하지만 `_` 또는 `.`는 유효한 구분자입니다.

  - 이러한 변경을 수행하는 데 유용한 도구는 [filebot](http://www.filebot.net/#download)입니다. Apple 및 Windows 스토어에서 유료 버전을 사용할 수 있지만 이전 [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download) 사이트에서 무료로 찾을 수 있습니다. GUI 및 CLI 모두를 갖추고 있으므로 편한 대로 사용할 수 있습니다. 위의 예에서 `{ny}`는 `이름 (연도)`로 확장되고 `{vf}`는 `1080p`와 같은 해상도를 제공합니다. 품질을 추론할 내용이 없으므로 `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`를 사용하여 720p보다 낮은 모든 것을 `[DVD-572p]`로 이름을 지정하고 720p 이상을 `[Bluray-1080p]`와 같이 지정할 수 있습니다.

- 자세한 내용은 [팁 및 트릭 섹션 => 각 영화에 대한 폴더 만들기](/radarr/faq)를 참조하십시오.

## 영화 폴더 이름이 잘못되었습니다

- 영화 폴더 이름은 영화가 추가된 시점의 메타데이터(이름/연도)를 기반으로 합니다. 영화가 출시되기 전에 영화를 추가한 경우 영화 폴더 이름을 업데이트하여 새로운 현재 데이터를 반영해야 할 수도 있습니다.
- 영화가 이미 폴더에 있는 경우에도 폴더 이름이 올바르지 않을 수 있습니다. 폴더 이름은 `영화 제목 (연도)`여야 하며, 제목과 연도가 폴더 이름에 포함되는 것이 현재 중요합니다.

  - 잘 작동하는 예:
    - `/mnt/Movies/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Kid Movies/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - 작동하지만 수동 관리가 필요한 예:
    - 글자별: `/mnt/Movies/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - 등급별: `/mnt/Movies/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - 장르별: `/mnt/Movies/Crime, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - 이러한 예는 영화가 추가될 때 수동 관리가 필요합니다. 각 예제에는 `A-D` 및 `E-G`와 같은 첫 글자 예제, 등급 예제에는 `R` 및 `PG-13`, 장르 폴더의 다양성을 추측할 수 있습니다. 새로운 영화를 추가할 때 이 형식이 작동하려면 올바른 기본 폴더를 선택해야 합니다.
  - 작동하지 않는 예:
    - 단일 폴더: `/mnt/Kid Movies/Frozen (2013) [Bluray-1080p].mkv`
      - 현재 영화는 단순히 영화 이름으로 된 폴더에 있어야 합니다. 이 기능을 추가하기 위해 개발 작업이 완료될 때까지 이를 우회할 방법은 없습니다.
    - v3에서 작동하지 않는 v0.2의 **영화** 폴더 이름 형식은 **파일** 속성을 **영화 폴더** 이름에 포함하는 것입니다. ``{Movie.Title}.{Release Year}.{Quality.Full}-{MediaInfo.Simple}{`Release.Group}``와 같은 형식은 v3에서 작동하지 않습니다.
      - 폴더는 영화와 관련이 있으며 파일과 독립적입니다. 또한 이는 계획된 영화 당 여러 파일 지원과 호환되지 않습니다.
      - 제거된 다른 이유는 이로 인해 빈번한 혼동, 데이터베이스 손상 및 일반적으로 완전히 완성되지 않았습니다.
  - [팁 및 트릭 섹션 => 각 영화에 대한 폴더 만들기](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)는 파일 및 폴더 구조가 잘 작동하는지 확인하는 데 좋은 소스입니다.

## 영화 새로 고침 작업을 비활성화할 수 있나요?

- 아니요, SQL 조작을 통해 비활성화해서는 안 됩니다. 새로 고침 영화 작업은 상위 Servarr 프록시를 쿼리하고 각 영화의 메타데이터(식별자, 캐스트, 요약, 등급, 번역, 대체 제목 등)가 Radarr에 현재 저장된 정보와 비교하여 업데이트해야 하는지 확인합니다. 필요한 경우 해당 영화를 업데이트합니다.
- 새로 고침 작업이 I/O 사용량이 많아지는 것이 일반적인 불만입니다.
- 주요 설정은 "새로 고침 후 영화 폴더 다시 스캔"입니다. 새로 고침 중 디스크 I/O 사용량이 급증하는 경우 스캔 설정을 `수동`으로 변경해야 합니다.
  - 이 설정을 `절대로` `하지 않도록` 변경하십시오. 라이브러리에 대한 모든 변경(새로운 영화, 업그레이드, 삭제 등)이 Radarr를 통해 이루어지는 경우에만 `하지 않도록` 설정하십시오.
  - 영화 파일을 수동으로 삭제하거나 Plex 또는 다른 타사 프로그램을 통해 삭제하는 경우에는 `하지 않도록` 설정하지 마십시오.
- 변경할 수 있는 다른 설정은 "비디오 파일 분석"입니다. 이 설정은 tdarr을 사용하거나 파일을 외부적으로 수정하는 경우에 활성화하는 것이 좋습니다. 그렇지 않은 경우 "비디오 파일 분석"을 비활성화하여 일부 I/O를 줄일 수 있습니다.

## Radarr에 기능을 요청하는 방법은?

- 이것은 쉬운 질문입니다. [여기를 클릭하십시오](https://github.com/Radarr/Radarr/issues)

## 도움이 필요합니다. Mac에서 Radarr를 열 수 없습니다. 개발자가 확인되지 않았으므로 열 수 없습니다.

- 이것은 간단합니다. 자세한 내용은 [여기](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)를 참조하십시오. ![개발자가 확인되지 않음](developer-cannot-be-verified.png "개발자가 확인되지 않음")
- 또는 Radarr를 자체 서명해야 할 수도 있습니다. `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`를 실행해야 할 수도 있습니다.

## 도움이 필요합니다. Mac에서 Radarr.app이 손상되어 열 수 없습니다.

- 이는 손상된 다운로드로 인한 것이거나 [보안 문제](#help-my-mac-says-radarr-cannot-be-opened-because-the-developer-cannot-be-verified)로 인한 것입니다. 자세한 내용은 관련 FAQ 항목을 참조하십시오.

## 오류가 발생했습니다: 데이터베이스 디스크 이미지가 손상되었습니다

> \* v4.X 버전으로 업그레이드한 후 이 문제가 발생하는 Radarr 사용자를 위한 내용입니다. v4 버전은 여러 가지 원인으로 인해 이전에 Radarr에서 감지할 수 없었던 데이터베이스의 손상이 발생할 수 있습니다. 마이그레이션은 실패하고 Radarr가 시작되지 않게 됩니다. 아마도 모든 백업이 손상되었으므로 해당 백업을 복원하는 것만으로는 문제를 해결할 수 없을 것입니다.
> \* 마이그레이션 후 데이터베이스를 열거나 복구할 수 없는 경우 최근 백업에서 데이터베이스의 사본을 만들고 해당 파일에 데이터베이스 복구 프로세스를 적용한 다음 복구된 백업 파일로 Radarr를 시작해 보십시오. 그러면 문제없이 마이그레이션이 수행될 것입니다.
{.is-warning}

- **`로그 데이터베이스 생성 오류`는 로그.db에 문제가 있는 것을 나타냅니다.**
  - 이는 데이터베이스 이름을 변경하거나 제거하여 빠르게 해결할 수 있습니다. 로그 데이터베이스에는 명령 기록 및 업데이트 설치 기록, 정보, 경고 및 오류 항목이 포함되어 있습니다.
- **`메인 데이터베이스 생성 오류` 또는 지정된 데이터베이스가 없는 일반적인 `데이터베이스 디스크 이미지가 손상되었습니다` 오류는 radarr.db에 문제가 있는 것을 나타냅니다.**
  - 아래에 나열된 단계를 계속 진행하십시오.
- 이는 대부분 Radarr의 대부분 정보를 저장하는 SQLite 데이터베이스가 손상되었음을 의미합니다. 기존 데이터베이스를 복구하려고 시도하거나 백업을 복구하려고 시도하거나, 그렇지 않으면 새로운 깨끗한 데이터베이스로 다시 시작해야 합니다.
- 이 오류는 데이터베이스 파일이 \*Arr가 실행 중인 사용자/그룹에 의해 쓰기 가능하지 않을 때 발생할 수 있습니다. 권한이 원인인 경우 새로 설치된 경우, 새 서버로 마이그레이션된 경우, 최근에 appdata 디렉토리 권한을 수정한 경우 또는 \*Arr가 실행되는 사용자 및 그룹을 변경한 경우에만 문제가 발생할 수 있습니다.
- 가장 좋은 첫 번째 옵션은 [백업에서 복원을 시도](#how-do-i-backuprestore-my-radarr)하는 것입니다. 그러나 v4로 업그레이드한 후 이 오류를 받은 사용자의 경우 백업 자체가 작동할 가능성이 매우 낮으며, 언급된 다른 복구 방법을 시도해야 합니다.
- 데이터베이스를 복구해 볼 수도 있습니다. 이 문제가 업데이트 후 발생한 경우에는 일반적으로 유일한 옵션입니다. [sqlite3 `.recover` 명령](/useful-tools#recovering-a-corrupt-db)을 시도해 보십시오.
  - sqlite에 `.recover`가 없거나 더 GUI(예: Windows) 친화적인 방법을 원하는 경우 [이 위키의 지침](/useful-tools#recovering-a-corrupt-db-ui)을 따르십시오.
- 데이터베이스 오류의 다른 가능한 원인은 데이터베이스를 네트워크 드라이브(nfs 또는 smb 또는 로컬이 아닌 다른 것)에 배치한 경우입니다. **SQLite는 데이터와 응용 프로그램이 동일한 컴퓨터에 공존하는 상황을 위해 설계되었습니다.** 따라서 \*Arr AppData 폴더(/config 도커 마운트)는 로컬 저장소에 있어야 합니다. [SQLite와 네트워크 드라이브는 함께 작동하지 않으며 결국 데이터베이스가 손상될 수 있습니다](https://www.sqlite.org/draft/useovernet.html).
- mergerFS를 사용하는 경우 SQLite가 mmap을 사용하므로 `direct_io`를 제거해야 합니다. mergerFS [문서](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)에서 설명한대로 `direct_io`는 mmap을 지원하지 않습니다.

## Mac에서 Radarr를 사용하고 갑자기 작동하지 않습니다. 무슨 일이 일어났나요?

- 대부분 이는 MacOS 버그로 인해 하나의 데이터베이스가 손상되었기 때문입니다.
- 위의 데이터베이스가 손상되었습니다 항목을 참조하십시오.
- 그런 다음 시작을 시도하고 작동하는지 확인하십시오. 작동하지 않으면 추가 지원이 필요합니다. [서브레딧 /r/radarr](http://reddit.com/r/radarr)에 게시하거나 [Discord](https://radarr.video/discord)에 참여하여 도움을 받으십시오.

## 원격 서버에서 파일을 Radarr이 볼 수 없는 이유는 무엇인가요?

- 모든 OS에서 \*Arr을 실행하는 사용자/그룹이 마운트된 드라이브에 대한 읽기 및 쓰기 액세스 권한이 있는지 확인하십시오.
- Linux의 경우 다음을 확인하십시오.
  - NFS 마운트를 사용하는 경우 마운트에 `nolock`이 활성화되어 있는지 확인하십시오.
  - SMB 마운트를 사용하는 경우 마운트에 `nobrl`이 활성화되어 있는지 확인하십시오.
- Windows의 경우: 간단히 말해서, \*Arr이 실행되는 사용자(서비스인 경우) 또는 하위 앱(트레이 앱인 경우)은 원격 서버의 파일 경로에 액세스할 수 없습니다. 이는 다양한 이유로 발생할 수 있지만 가장 일반적인 경우는 \*Arr이 서비스로 실행되어 발생하는 문제입니다.

### 기본적으로 Radarr은 보호된 원격 파일 공유에 액세스할 수 없는 LocalService 계정 아래에서 실행됩니다.

- 해당 공유에 액세스할 수 있는 다른 사용자로 Radarr 서비스를 실행합니다.
- Windows 서버에서 관리 도구 \> 서비스 창을 엽니다.
- Radarr 서비스를 중지합니다.
- 속성 \> 로그온 대화상자를 엽니다.
- 서비스 사용자 계정을 대상 사용자 계정으로 변경합니다.
- 시작 프로그램 폴더에서 Radarr.exe를 실행합니다.

### 매핑된 네트워크 드라이브를 사용하는 경우(UNC 경로가 아닌 경우)

- 경로를 UNC 경로(`\\서버\공유`)로 변경하십시오.
- 시작 프로그램 폴더에서 Radarr.exe를 실행합니다.

## Windows 서비스에서 트레이 앱으로 변경하는 방법은?

1. Radarr을 종료합니다.
1. Radarr 디렉토리에 있는 serviceuninstall.exe를 실행합니다.
1. 한 번 관리자 권한으로 Radarr.exe를 실행하여 적절한 권한을 부여하고 방화벽을 엽니다. 완료되면 닫고 일반적으로 실행하십시오.
1. (선택 사항) .exe에 대한 바로 가기를 시작 폴더에 놓아 부팅 시 자동으로 시작하도록 설정할 수 있습니다.

## 도움이 필요합니다. 자물쇠를 걸었습니다

{#help-i-have-forgotten-my-password}

인증을 비활성화하려면(잊어버린 사용자 이름이나 비밀번호를 재설정하려면) [Radarr Appdata 디렉토리](/radarr/appdata-directory) 내에 있는 `config.xml`을 편집해야 합니다.

1. 텍스트 편집기에서 config.xml을 엽니다.
1. 인증 방법 줄을 찾습니다. `<AuthenticationMethod>Basic</AuthenticationMethod>` 또는 `<AuthenticationMethod>Forms</AuthenticationMethod>`일 것입니다.
1. `AuthenticationMethod` 줄을 `<AuthenticationMethod>None</AuthenticationMethod>`로 변경합니다.
1. Radarr을 다시 시작합니다.
1. 이제 비밀번호 없이 Radarr에 액세스할 수 있으며, UI에서 `설정: 일반`으로 이동하여 사용자 이름과 비밀번호를 설정해야 합니다.

## 시작 시 브라우저가 열리지 않도록하는 방법은?

운영 체제에 따라 여러 가지 방법이 있습니다.

- 일부 운영 체제에서는 `설정` => `일반`에서 시작 시 브라우저를 열지 여부에 대한 확인란이 있습니다.
- Radarr을 호출할 때 인수에 `-nobrowser`(*nix) 또는 `/nobrowser`(Windows)를 추가할 수 있습니다.
- Radarr을 중지하고 config.xml 파일을 편집하여 `<LaunchBrowser>True</LaunchBrowser>`를 `<LaunchBrowser>False</LaunchBrowser>`로 변경합니다.

## 이상한 UI 문제

- 라이브러리 페이지가 아무것도 표시되지 않거나 특정 보기나 정렬이 작동하지 않는 등 이상한 UI 문제가 발생하는 경우, Chrome 은신 모드 또는 Firefox 은신 창에서 확인해 보십시오. 그곳에서 정상적으로 작동하는 경우 특정 IP/도메인에 대한 브라우저 캐시와 쿠키를 지우십시오. 자세한 내용은 [캐시 및 쿠키 지우기](/useful-tools#clearing-cookies-and-local-storage) 위키 문서를 참조하십시오.

## 웹 인터페이스가 Windows에서 localhost에서만 로드됩니다.

- 웹 인터페이스에 <http://localhost:7878/> 또는 <http://127.0.0.1:7878/>에서만 액세스할 수 있는 경우 최소한 한 번은 관리자로 실행해야 합니다.

## 권한

- Radarr은 다운로더가 파일을 넣은 위치에서 최종 위치로 파일을 이동해야 하므로 소스 및 대상 디렉토리 및 파일을 읽고 쓸 수 있어야 합니다.
- Linux에서는 서비스가 자체 사용자로 실행되는 것이 모범 사례이므로 공유 그룹을 사용하고 다운로더 및 .에서 폴더 권한을 `775`로 설정하고 파일을 `664`로 설정하는 것이 좋습니다. umask 표기법으로는 `002`입니다.

## 시스템 및 로그가 영원히 로드됩니다

- 이는 easy-privacy 블록 목록 때문입니다. 이들은 /api/log?를 포함하는 모든 URL을 차단합니다. 목록을 검토하고 해당 목록에서 모든 URL을 차단하는 것이 합리적인지 판단하십시오. 여기에는 사이트를 깨뜨릴 수 있는 수십 개의 URL이 포함되어 있습니다. 이를 선택한 것입니다. 쉬운 해결책은 Radarr이 실행 중인 도메인을 화이트리스트에 추가하는 것입니다. 그러나 목록을 확인하는 것을 권장합니다.

## 토렌트 압축 해제

- 대부분의 토렌트 클라이언트는 유넷과 달리 자동으로 압축된 아카이브를 처리하지 않습니다. [unpackerr](https://github.com/unpackerr/unpackerr)를 추천합니다.

## uTorrent이 더 이상 작동하지 않습니다

- 웹 UI가 활성화되어 있는지 확인하십시오.
- Alt Listening Port(고급 => 웹 UI)가 Listening Port(연결)와 동일하지 않은지 확인하십시오.
- 연결에 대한 포트 포워딩을 방해하지 않도록 웹 UI Alt Listening Port를 변경하는 것이 좋습니다.

## 팝업이 나타나서 config.xml이 손상되었다고 했습니다. 이제 어떻게 해야 하나요?

- Radarr은 시작 시 구성 파일을 읽을 수 없어서 구성 파일이 어떤 방식으로든 손상되었습니다. 온라인으로 돌아가려면 [appdata-directory](/radarr/appdata-directory)에서 `.xml`을 삭제해야 합니다. 삭제한 후에 시작하면 기본 포트(7878)에서 시작하게 됩니다. 이제 일반 설정 페이지에서 구성한 설정을 다시 구성해야 합니다.

## 잘못된 인증서 및 기타 HTTPS 또는 SSL 문제



- 다운로드 클라이언트가 작동을 멈추고 `Localhost is an invalid certificate`와 같은 오류가 발생합니까?
  - Radarr은 SSL 인증서를 유효성 검사합니다. 다운로드 클라이언트에 SSL 인증서가 설정되어 있지 않거나 자체 서명된 https 인증서를 사용하고 로컬 인증서 저장소에 CA 인증서가 추가되지 않은 경우 연결을 거부합니다. 무료로 올바르게 서명된 인증서는 [let's encrypt](https://letsencrypt.org/)에서 사용할 수 있습니다.
  - 다운로드 클라이언트와 동일한 컴퓨터에 있다면 HTTPS를 사용할 필요가 없으므로 가장 쉬운 해결책은 연결에 대해 SSL을 비활성화하는 것입니다. 대부분의 경우 로컬 네트워크에서도 필요하지 않다는 것에 동의할 것입니다. 보안이 취약한 SSL 설정을 유지하려면 고급 설정에서 인증서 유효성 검사를 비활성화할 수 있습니다.

## VPN, Jackett 및 \*ARRs

- 중국, 호주 또는 남아프리카와 같은 억압적인 국가가 아닌 경우 토렌트 클라이언트는 일반적으로 VPN 뒤에 있어야 할 유일한 것입니다. VPN 종단점은 많은 사용자가 공유하기 때문에 각 소프트웨어가 사용하는 다양한 서비스에서는 속도 제한, DDOS 보호 및 IP 차단을 경험할 수 있습니다.
- 다른 말로, VPN을 사용하여 \*Arrs (Lidarr, Prowlarr, Radarr, Readarr 및 Lidarr)를 VPN 뒤에 두면 일부 경우에는 서비스에 액세스할 수 없으므로 응용 프로그램을 사용할 수 없게 됩니다.

> **VPN이 \*Arrs와 문제를 일으킬지 여부는 문제가 아니라 언제 일어날지에 대한 문제입니다. 이미지 제공자는 차단하고 대부분의 \*Arr 서버 (업데이트, 메타데이터 등) 앞에는 Cloudflare가 있으며 이 역시 차단할 수 있습니다.**
{.is-warning}

- **많은 개인 트래커는 VPN을 사용하거나 액세스하는 것 (예: Jackett 또는 Prowlarr 사용)을 금지합니다.**

### VPN 사용

- Docker를 사용하는 경우 VPN이 필요하면 Hotio 또는 Binhex의 Download Client + VPN 컨테이너를 사용하는 것이 좋습니다.
- Docker를 사용하지 않는 경우 VPN 클라이언트는 VPN 뒤에 있는 필요한 (다운로드 클라이언트) 앱만 지원하는 분할 터널링을 지원해야 합니다.
- 트래커에 액세스하는 데 문제가 있는 경우 ISP의 DNS 서버 대신 Google 또는 Cloudflare의 DNS 서버를 사용하여 문제를 해결할 수 있습니다.
- 일부 경우 (예: 영국 ISP) 토렌트 다운로드 클라이언트를 VPN 뒤에 두고 Jackett/Prowlarr를 다음과 같이 설정해야 할 수 있습니다:
  - Jackett을 VPN 뒤에 두고 분할 터널링이 로컬 액세스를 허용하는지 확인합니다.
  - Prowlarr의 경우 VPN 클라이언트를 구성하여 프록시를 제공하고 설정 => 인덱서에 프록시를 추가합니다. 프록시에 태그를 지정하고 해당 태그를 사용해야 하는 인덱서를 추가합니다.
    - VPN에서 프록시를 생성하는 방법을 제공하지 않는 경우에만 필요한 경우 Prowlarr을 VPN 뒤에 두고 분할 터널링이 로컬 액세스를 허용하는지 확인합니다.

# Radarr 검색 및 다운로드 일반적인 문제

## 왜 새 영화를 Radarr에 추가할 수 없을까요?

{#why-cant-i-add-a-new-movie-to-radarr}

- Radarr은 영화 정보 및 팬아트, 배너 및 배경과 같은 이미지를 위해 [The Movie Database (TMDb)](http://themoviedb.org)를 사용합니다. 일반적으로 영화를 추가할 수 없는 몇 가지 이유가 있습니다:
  - TMDb는 (Radarr에서 사용하는) API를 통해 영화를 검색할 때 특수 문자 사용을 허용하지 않습니다. 따라서 번역된 이름으로 검색하거나 특수 문자 없이 검색해 보세요.
  - TMDb ID 또는 TMDb에 있는 경우 IMDb ID로도 추가할 수 있습니다.
  - 해당 영화가 아직 TMDb에 추가되지 않았을 수 있으므로 [가이드](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006)를 따라 추가해야 합니다.

## Jackett에서 수동 검색할 때보다 더 많은 결과가 표시됩니다.

- 이는 Jackett을 다른 방식으로 검색하기 때문입니다. 자세한 내용은 [문제 해결 문서](/radarr/troubleshooting)를 참조하십시오.

## Radarr은 영화의 연도를 어떻게 결정합니까?

- Radarr은 [TMDb](https://www.themoviedb.org/)에서 메타데이터를 가져옵니다.
- Radarr은 가장 오래된 **극장 개봉일** 및 가장 오래된 **프리미어** 날짜의 연도를 사용하여 일치시킵니다.
  - 극장 개봉일이 없는 경우 로직은 가장 오래된 물리적 또는 디지털 출시일로 대체됩니다.
- 영화에 디지털, 물리적, 극장 또는 프리미어 출시일이 없는 경우 TMDb를 업데이트해야 합니다.
- [TMDb의 기여 가이드](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013)에서 출시 유형에 대해 다음과 같이 설명합니다.
  - **프리미어** - 프리미어 상영은 영화제 상영 (예: TIFF) 또는 주요 도시 (예: LA, 런던, 토론토)에서 캐스트와 스태프가 참석하는 프리미어 이벤트와 같은 형태를 취할 수 있습니다.
  - **극장** - 원래 개봉 및 이후의 모든 공식적인 개봉에 사용될 수 있습니다. 넓은 배급 또는 포화 배급에 사용됩니다. 미국에서 600-1,999개의 스크린은 넓은 배급으로 간주되며 2000개 이상은 포화 배급으로 간주됩니다.
  - **극장 (제한)** - 제한된 극장 개봉은 주요 대도시 시장에서 몇 개의 극장에서 새 영화를 개봉하는 영화 배급 전략입니다. 미국에서 극장 수는 600개 미만입니다.
  - **물리적** - 모든 VHS, DVD 및 Blu-ray 출시를 포함합니다.
  - **디지털** - 스트리밍 플랫폼, VOD 대여 또는 구매를 포함한 모든 관련 출시를 추가할 수 있습니다. 온라인 영화제 및 가상 영화관 개봉을 포함한 디지털 상영도 디지털 출시로 간주됩니다.

## Radarr은 외국 영화 또는 외국 제목을 어떻게 처리합니까?

> [TRaSH의 사용자 정의 형식 언어 가이드](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats)는 원하는 언어로 영화를 가져오는 데 도움이 될 수 있습니다.{.is-info}

> 2023-02-12부터 Radarr의 메타데이터 캐시는 TMDb에서 영화의 원래 언어를 TMDb의 말하기 언어로 간주합니다. 단, TMDb에서 영화에 대해 말하기 언어가 하나만 있는 경우에만 해당됩니다. 그렇지 않으면 영화의 원래 TMDb 언어가 사용됩니다.
{.is-warning}

## ID 검색

- **ID 기반 검색을 지원하는 인덱서** - ID (TMDbId, IMDbId 등) 기반 검색을 지원하는 인덱서 및 트래커에서 검색 - 많은 Usenet 인덱서 및 많은 개인 토런트 트래커와 같은 경우 - 결과가 ID 기반 검색에 반환되면 텍스트 쿼리는 사용되지 않습니다. 결과가 반환되면 이름/텍스트 검색으로 대체되지 않습니다. 인덱서에서 결과가 누락된 경우 이는 잘못된 영화 ID와 연결된 릴리스 때문입니다.
  - 릴리스의 언어는 제공된 경우 이름에서 파싱하는 대신 인덱서나 트래커의 릴리스 언어에서 파생될 수도 있습니다.

## 텍스트 검색

- **ID 기반 검색이 지원되지 않거나 ID 기반 검색 결과가 없는 인덱서** - 사용자가 선호하는 언어로 영화의 원래 제목, 영어 제목 및 번역 제목을 사용하여 검색합니다. 이는 영화의 품질 프로필과 품질 프로필에서 점수가 0보다 큰 사용자 정의 형식에도 적용됩니다.
- 파싱(즉, 가져오기)은 모든 번역 및 대체 제목에서 일치하는 항목을 찾습니다.
  - 릴리스의 언어는 제공된 경우 이름에서 파싱하는 대신 인덱서나 트래커의 릴리스 언어에서 파생될 수도 있습니다.

## 외국 영화 가져오기

- 외국어로 된 영화를 가져오려면 영화의 품질 프로필 언어를 원래 언어 (영화의 원래 언어\*), 해당 프로필의 특정 언어 또는 `Any`로 설정하고, 어떤 언어를 가져올지 결정하기 위해 품질 프로필에서 0보다 큰 점수를 가진 사용자 정의 형식을 만들어야 합니다.
- 이는 인덱서 설정에서 구성된 인덱서 언어를 포함하지 않습니다.
  - [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c)부터는 `multi`가 더 이상 영어를 포함한다고 가정하지 않습니다.
  - 사용자는 인덱서당 설정을 조정하여 `multi`가 어떤 언어를 나타내는지 정의할 수 있습니다.

## Radarr에서 이름에 "multi"가 있는 경우 어떻게 처리합니까?

- Radarr v4.1+에서는 Radarr이
`multi`가 이제 영화의 언어이고 이전 버전과 달리 영어가 아니라고 가정합니다.
  - 사용자는 인덱서당 설정을 조정하여 `multi`가 어떤 언어를 나타내는지 정의할 수 있습니다.
- "multi" 정의는 릴리스 파싱에만 도움이 되며 외국 제목이나 영화 검색에는 도움이 되지 않습니다.

## 도움이 필요합니다. 영화가 추가되었지만 검색되지 않습니다.

- Radarr은 누락된 영화를 *자동으로* 검색하지 않습니다. 대신, 모든 RSS에 구성된 모든 인덱서에 대해 주기적으로 새 게시물을 쿼리합니다. 그 목록에 원하는 영화나 컷오프 미달 영화가 나타나면 다운로드됩니다. 즉, 영화가 게시되기 전(또는 재게시되기 전)까지 다운로드되지 않습니다.
- 즉시 원하는 영화를 추가하는 경우 가장 좋은 옵션은 *영화 추가* (**1**) 버튼 왼쪽에 있는 "누락된 영화를 검색 시작"란을 확인하는 것입니다. 또는 추가한 영화의 페이지로 이동하여 돋보기 "검색" (**2**) 버튼을 클릭하거나 원하는 영화를 검색하기 위해 원하는 보기를 사용할 수도 있습니다.

  - 영화 추가 시 영화 추가 및 검색
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - 기존 영화 검색
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jackett의 /all 엔드포인트

{#jackett-all-endpoint}

- Jackett의 `/all` 엔드포인트는 편리하지만 그것만의 이점입니다. 그 외의 모든 것은 잠재적인 문제입니다. 따라서 각 트래커를 개별적으로 추가해야 합니다. 또는 Jackett 및 NZBHydra2 대체제인 [Prowlarr](/prowlarr)을 확인할 수도 있습니다.

- **2022년 1월 1일 업데이트: Jackett의 `/all` 엔드포인트는 더 이상 지원되지 않습니다(예: 경고가 발생) 4.0.0.5730부터 문제만 야기합니다.**

- Jackett의 /all 엔드포인트는 편리하지만 그것만의 이점입니다. 그 외의 모든 것은 잠재적인 문제이므로 이제 각 트래커를 개별적으로 추가해야 합니다.
- [Jackett의 개발자들도 피해야 하고 사용해서는 안 된다고 말합니다.](https://github.com/Jackett/Jackett#aggregate-indexers)
- /all 엔드포인트를 사용하는 것은 이점이 없으며 다음과 같은 단점만 있습니다:
  - 인덱서별 설정(카테고리, 검색 모드 등)을 제어할 수 없습니다.
  - 검색 모드(IMDB, 쿼리 등)를 혼합하면 품질이 낮은 결과가 발생할 수 있습니다.
  - 인덱서별 카테고리(100000 이상)를 사용할 수 없습니다.
  - 느린 인덱서는 전체 결과의 속도를 늦출 수 있습니다.
  - 총 결과는 1000개로 제한됩니다.
  - /all에서 하나의 트래커가 오류를 반환하면 \*Arr은 해당 트래커를 비활성화하고 결과를 얻지 못하게 됩니다.

### Jackett /All 해결책

- Jackett에서 각 트래커를 수동으로 인덱서로 추가합니다.
- [Prowlarr](/prowlarr)을 확인하십시오. 이는 Lidarr/Radarr/Readarr 개발 팀에서 제공하는 인덱서를 \*Arr에 동기화할 수 있습니다.
- [NZBHydra2](https://github.com/theotherp/nzbhydra2)를 확인하십시오. 이는 인덱서를 \*Arr에 동기화할 수 있습니다. 그러나 단일 집계 엔드포인트를 사용하지 마시고 동기화를 사용할 경우 `multi`를 사용하십시오.

## 왜 두 개의 파일이 있는 건가요? | 왜 다운로드 폴더에 파일이 남아 있는 건가요?

이는 정상적인 동작입니다. 하드링크를 지원하는 설정을 사용하면 공간을 두 배로 사용하지 않습니다. 아래는 토렌트 프로세스가 작동하는 방식입니다.

1. Radarr은 다운로드 요청을 클라이언트에 보내고, 해당 요청을 다운로드 클라이언트 설정에서 구성한 레이블 또는 카테고리 이름과 연결합니다. 예: 영화, TV, 시리즈, 음악 등.
1. Radarr은 해당 카테고리 이름을 사용하여 다운로드 클라이언트에서 활성 다운로드를 모니터링합니다. 이 모니터링은 다운로드 클라이언트의 API를 통해 수행됩니다.
1. 완료된 파일은 시드를 유지하기 위해 원래 위치에 남겨집니다(비율이나 시간은 다운로드 클라이언트 또는 특정 다운로드 클라이언트에서 조정할 수 있습니다). 파일이 미디어 폴더로 가져올 때 하드링크를 지원하는 경우 하드링크를 만들고, 하드링크를 지원하지 않는 경우 파일을 복사합니다.
1. Radarr의 설정에서 "완료된 다운로드 처리 - 완료된 항목 제거" 옵션이 활성화된 경우, Radarr은 다운로드 클라이언트에서 시딩이 완료되고 토렌트가 중지(일시 중지)된 것을 보고 원래 파일과 토렌트를 삭제합니다. 최적으로 다운로드 클라이언트를 구성하는 방법은 [TRaSH의 다운로드 클라이언트 가이드](https://trash-guides.info/Downloaders/)를 참조하십시오.

> 하드링크는 기본적으로 활성화되어 있습니다. [하드링크를 사용하면 추가 디스크 공간을 사용하지 않습니다.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) 완료된 다운로드 디렉토리와 미디어 라이브러리의 파일 시스템과 마운트는 동일해야 합니다. 하드링크 생성이 실패하거나 하드링크를 지원하지 않는 경우 파일을 복사합니다.
{.is-info}

## 왜 Radarr는 리버스 프록시 뒤에서 작동하지 않을까요?

- v3부터 Radarr는 .NET과 새 웹 서버를 사용합니다. SignalR이 작동하려면 UI 버튼이 작동하고 데이터베이스 변경이 적용되고 기타 항목이 필요합니다. 이를 위해 Radarr의 위치 블록에 다음을 추가해야 합니다.

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- nginx 문서에서 제안하는대로 `proxy_set_header Connection "Upgrade";`를 포함하지 않도록 주의하십시오. **이는 작동하지 않습니다.**
- [ASP.NET Core 문제](https://github.com/aspnet/AspNetCore/issues/17081)를 참조하십시오.
- Cloudflare와 같은 CDN을 사용하는 경우 웹소켓 연결을 허용하도록 웹소켓이 활성화되어 있는지 확인하십시오.
- 예기치 않은 리디렉션을 방지하려면 호스트 헤더가 전달되도록 확인하십시오.