---
title: Radarr 빠른 시작 가이드
description: 
published: true
date: 2023-08-27T22:14:05.687Z
tags: radarr, quickstart
editor: markdown
dateCreated: 2021-06-20T20:05:44.814Z
---

# 목차

- [목차](#목차)
- [빠른 시작 설정 가이드](#빠른-시작-설정-가이드)
- [시작](#시작)
- [미디어 관리](#미디어-관리)
  - [영화 명명](#영화-명명)
  - [가져오기](#가져오기)
  - [파일 관리](#파일-관리)
  - [루트 폴더](#루트-폴더)
- [프로필](#프로필)
- [품질](#품질)
- [인덱서](#인덱서)
- [다운로드 클라이언트](#다운로드-클라이언트)
  - [{.tabset}](#tabset)
    - [유즈넷](#유즈넷)
    - [비트토렌트](#비트토렌트)
- [기존 정리된 미디어 라이브러리 가져오는 방법](#기존-정리된-미디어-라이브러리-가져오는-방법)
  - [영화 가져오기](#영화-가져오기)
  - [기존 미디어 가져오기](#기존-미디어-가져오기)
    - [일치하는 항목 없음](#일치하는-항목-없음)
    - [가져온 후 잘못된 폴더 이름 수정](#가져온-후-잘못된-폴더-이름-수정)
  - [영화 추가하는 방법](#영화-추가하는-방법)

# 빠른 시작 설정 가이드

> 이 페이지는 아직 작성 중이며 완성되지 않았습니다. 기여는 환영합니다.

> 모든 설정에 대한 자세한 설명은 [Radarr => 설정](/radarr/settings)을 참조하세요.
{.is-info}

이 가이드에서는 Radarr을 시작하기 위해 수행해야 할 기본 설정을 설명하려고 합니다. 화면에서 볼 수 있는 일부 옵션은 건너뛰겠습니다. 더 자세한 내용은 FAQ 및 문서의 해당 페이지를 참조하세요.

> 스크린샷 및 GUI 설정에서 `주황색`으로 표시된 것은 고급 옵션입니다. 이를 볼 수 있도록 페이지 상단의 `고급 표시`를 클릭해야 합니다.
{.is-warning}

# 시작

설치 및 시작 후 브라우저를 열고 `http://{your_ip_here}:7878`로 이동합니다.

![Radarr-start.png](/assets/radarr/Radarr-start.png)

# 미디어 관리

먼저 `미디어 관리` 설정을 살펴보겠습니다. 여기에서 선호하는 명명 및 파일 관리 설정을 설정할 수 있습니다.

`설정` => `미디어 관리`

![Radarr-settings-mm.png](/assets/radarr/Radarr-settings-mm.png)

## 영화 명명

![Radarr-settings-mm-movie-naming.png](/assets/radarr/Radarr-settings-mm-movie-naming.png)

1. 영화 이름 변경 사용/비사용(현재 이름이나 다운로드 시의 이름을 그대로 둘지 또는 변경할지 여부).
2. 불법 문자를 대체하거나 제거할지 여부 (`\ / : * ? " < > | ~ # % & + { }`).
3. 이 설정은 Radarr이 영화 파일 내의 콜론을 처리하는 방법을 지정합니다.
4. 여기에서 실제 영화 파일의 명명 규칙을 선택합니다.
5. *(고급 옵션) 비디오 파일을 포함하는 폴더의 명명 규칙을 설정하는 곳입니다.*

> 권장되는 명명 규칙과 예제는 [TRaSH의 권장 명명 규칙](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/)을 참조하세요.
{.is-info}

## 가져오기

![Radarr-settings-mm-importing.png](/assets/radarr/Radarr-settings-mm-importing.png)

1. *(고급 옵션) `복사 대신 하드링크 사용` 자세한 내용은 [TRaSH의 하드링크 가이드](https://trash-guides.info/hardlinks)를 참조하세요.
1. *(고급 옵션) 파일 가져온 후 일치하는 추가 파일(자막, nfo 등) 가져오기.*

## 파일 관리

![Radarr-settings-mm-fm.png](/assets/radarr/Radarr-settings-mm-fm.png)

1. 디스크에서 삭제된 영화는 자동으로 Radarr에서 모니터링이 해제됩니다.
    - 영화를 삭제하고 Radarr에서 해당 영화를 다시 다운로드하지 않으려는 경우 이 옵션을 사용합니다.
1. *(고급 옵션) 삭제된 파일이 삭제되기 전에 이동할 위치를 지정합니다(휴지통을 비우기 전에 복구할 수 있도록).
1. *(고급 옵션) 파일이 영구적으로 삭제되기 전에 경과해야 하는 기간입니다.

## 루트 폴더

![Radarr-settings-mm-root-folder.png](/assets/radarr/Radarr-settings-mm-root-folder.png)

여기에서 Radarr이 기존 정리된 미디어 라이브러리를 가져올 루트 폴더를 추가하고 다운로드 클라이언트가 다운로드한 미디어를 가져올 위치를 설정합니다(복사/하드링크/이동).

> \* Windows가 아닌 경우: NFS 마운트를 사용하는 경우 `nolock`이 활성화되어 있는지 확인하세요.
> \* SMB 마운트를 사용하는 경우 `nobrl`이 활성화되어 있는지 확인하세요.
{.is-warning}

> **Radarr을 실행하도록 구성한 사용자 및 그룹은이 위치에 대한 읽기 및 쓰기 액세스 권한이 있어야 합니다.** {.is-info}

> 다운로드 클라이언트는 다운로드 폴더로 다운로드하고 Radarr은 미디어 폴더(최종 목적지)로 가져옵니다. 미디어 서버에서 사용하는 폴더입니다.
{.is-info}

> **다운로드 폴더와 미디어(라이브러리/루트) 폴더는 동일한 위치일 수 없습니다.**
{.is-danger}

변경 사항을 저장하는 것을 잊지 마세요.

# 프로필

`설정` => `프로필`

![Radarr-settings-profiles.png](/assets/radarr/Radarr-settings-profiles.png)

여기에서 품질, 선호하는 언어 및 사용자 정의 형식 점수에 대한 프로필을 구성할 수 있습니다.

품질 소스 및 언어를 실제로 원하는 것만 선택하여 자체 프로필을 만드는 것이 좋습니다.

외국어 제목 및 언어에 대한 자세한 내용은 [이 FAQ 항목](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)을 참조하세요.

많은 사용자가 [TRaSH의 사용자 정의 형식 언어 가이드](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats)를 사용하여 원하는 언어를 지정하는 데 도움을 받습니다.

프로필은 사용자 정의 형식 점수가 구성되는 곳입니다. 원하지 않는 다운로드를 피하기 위해 [TRaSH의 가이드](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)에서 아래의 사용자 정의 형식을 추가하는 것이 강력히 권장됩니다. 자세한 내용은 연결된 TRaSH 가이드 사용자 정의 형식 문서 및 컬렉션 사용자 정의 형식 페이지 상단의 3개의 TRaSH 사용자 정의 형식 가이드를 참조하세요.

- [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl)는 Dolby Vision (DV)을 지원하지 않는 경우 녹색 색조가 있는 DV 릴리스를 가져오지 않습니다.
- [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk)는 BR-DISK 품질 파싱과 일치하지 않는 잘못된 이름의 BR-DISK를 가져오지 않습니다.

> 자세한 내용은 [설정 => 프로필](/radarr/settings#profiles)을 참조하세요.
> 품질 소스 간의 차이점은 [품질 정의](/radarr/settings#qualities-defined)를 참조하세요.
{.is-info}

# 품질

`설정` => `품질`

![Radarr-settings-quality.png](/assets/radarr/Radarr-settings-quality.png)

여기에서 원하는 미디어 파일의 최소 및 최대 크기를 변경/조정할 수 있습니다(유즈넷을 사용하는 경우 RAR/PAR2 파일을 고려하세요).

> 품질 설정에 대한 도움이 필요한 경우 테스트된 예제인 [TRaSH의 크기 권장 사항](https://trash-guides.info/Radarr/Radarr-Quality-Settings-File-Size/)을 확인하세요.
{.is-info}

# 인덱서

`설정` => `인덱서`

![Radarr-settings-indexers.png](/assets/radarr/Radarr-settings-indexers.png)

여기에서 파일을 실제로 다운로드할 인덱서/트래커를 추가합니다.

새 인덱서를 추가하려면 <kb>+</kb> 버튼을 클릭하면 다양한 옵션을 포함한 새 창이 표시됩니다. 이 위키에서는 Radarr이 유즈넷 인덱서와 토런트 트래커를 모두 "인덱서"로 간주합니다.

여기에는 유즈넷과 토런트 두 가지 섹션이 있습니다. 사용할 다운로드 클라이언트에 따라 선택할 인덱서 유형을 선택해야 합니다.

토런트 트래커의 경우 거의 모두 [Prowlarr](/prowlarr) 또는 [Jackett](https://github.com/Jackett/Jackett)의 사용을 요구합니다.

# 다운로드 클라이언트

`설정` => `다운로드 클라이언트`

![Radarr-settings-download-clients.png](/assets/radarr/Radarr-settings-download-clients.png)

다운로드 및 가져오기는 대부분의 사용자가 문제를 겪는 부분입니다. 소프트웨어는 다운로드 클라이언트와 통신할 수 있어야 하며, 클라이언트가 파일을 다운로드하는 위치에 대한 읽기 및 쓰기 액세스 권한이 있어야 합니다. 지원되는 다운로드 클라이언트가 많고 설정의 다양성도 많습니다. 일반적인 설정이 있지만 하나의 올바른 설정은 없으며 모든 설정은 약간 다를 수 있습니다. 그러나 잘못된 설정은 많습니다.

> 자세한 내용은 [설정 페이지](/radarr/settings#download-clients), 이 섹션의 [자세한 정보(지원)](/radarr/supported#download-clients) 페이지 및 [TRaSH의 다운로드 클라이언트 가이드](https://trash-guides.info/Downloaders/)를 참조하세요.
{.is-info}

## 다운로드 프로토콜 {.tabset}

### 유즈넷

{#usenet}

- Radarr은 클라이언트에 다운로드 요청을 보내고, 다운로드 클라이언트 설정에서 구성한 레이블 또는 카테고리 이름과 연결합니다.
  - 예: 영화, TV, 시리즈, 음악 등.
- Radarr은 해당 카테고리 이름을 사용하는 다운로드 클라이언트의 활성 다운로드를 모니터링합니다. 이는 다운로드 클라이언트의 API를 통해 모니터링됩니다.
- 다운로드가 완료되면 Radarr은 다운로드 클라이언트가 보고한 최종 파일 위치를 알게 됩니다. 이 파일 위치는 미디어 폴더와 별도로 어디에든지 위치할 수 있습니다. Radarr이 액세스할 수 있어야 합니다.
- Radarr은 완료된 파일 위치에서 Radarr이 사용할 수 있는 파일을 스캔합니다. 파일 이름을 구문 분석하여 요청한 미디어와 일치하는지 확인합니다. 그렇게 할 수 있다면 지정된 규칙에 따라 파일 이름을 변경하고 지정된 미디어 위치로 이동합니다.
- 원자적 이동(즉시 이동)은 기본적으로 활성화되어 있습니다. 파일 시스템과 마운트는 완료된 다운로드 디렉토리와 미디어 라이브러리에 대해 동일해야 합니다. 원자적 이동이 실패하거나 설정이 하드링크와 원자적 이동을 지원하지 않는 경우 Radarr은 파일을 복사한 다음 원본에서 삭제합니다. 이는 IO가 많이 발생합니다.
- Radarr의 설정에서 "완료된 다운로드 처리 - 삭제" 옵션이 활성화된 경우 다운로드에서 남은 파일은 요청을 통해 휴지통이나 재활용으로 보내집니다.

### 비트토렌트

{#bittorrent}

- Radarr은 클라이언트에 다운로드 요청을 보내고, 다운로드 클라이언트 설정에서 구성한 레이블 또는 카테고리 이름과 연결합니다.
  - 예: 영화, TV, 시리즈, 음악 등.
- Radarr은 해당 카테고리 이름을 사용하는 다운로드 클라이언트의 활성 다운로드를 모니터링합니다. 이 모니터링은 다운로드 클라이언트의 API를 통해 수행됩니다.
- 아직 시딩 중인 완료된 다운로드는 파일을 원래 위치에 남겨두어 파일을 시딩할 수 있도록 합니다(비율이나 시간은 다운로드 클라이언트나 Radarr에서 조정할 수 있습니다). 미디어 폴더로 가져올 때 Radarr은 하드링크를 지원하는 경우 하드링크를 만들고, 그렇지 않은 경우 파일을 복사합니다. 하드링크는 기본적으로 활성화되어 있습니다. [하드링크를 사용하면 추가 디스크 공간을 사용하지 않습니다.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) 파일 시스템과 마운트는 완료된 다운로드 디렉토리와 미디어 라이브러리에 대해 동일해야 합니다. 하드링크 생성이 실패하거나 설정이 하드링크를 지원하지 않는 경우 Radarr은 파일을 복사합니다.
- Radarr의 설정에서 "완료된 다운로드 처리 - 삭제" 옵션이 활성화된 경우 Radarr은 클라이언트에서 토렌트를 삭제하고 토렌트 데이터를 삭제하도록 클라이언트에 요청합니다. 다만 클라이언트가 시딩이 완료되고 토렌트가 중지된 것을 보고할 때에만 이 작업이 수행됩니다.

# 기존 정리된 미디어 라이브러리 가져오는 방법

> Radarr은 정기적으로 영화를 검색하지 않습니다. Radarr이 작동하는 방식에 대한 자세한 내용은 [Radarr 작동 방식](/radarr/faq#how-does-radarr-work) FAQ 항목을 참조하세요.
{.is-info}

프로필/품질 크기를 설정하고 인덱서 및 다운로드 클라이언트를 추가한 후 기존 정리된 미디어 라이브러리를 가져오는 시간입니다.

`영화`

![Radarr-movies.png](/assets/radarr/Radarr-movies.png)

`기존 영화 가져오기`를 선택하거나 사이드바에서 `가져오기`를 선택합니다.

## 영화 가져오기

![Radarr-movies-import.png](/assets/radarr/Radarr-movies-import.png)

이전에 [루트 폴더 섹션](#루트-폴더)에서 추가한 루트 경로를 선택합니다.

## 기존 미디어 가져오기

![Radarr-importing-existing.png](/assets/radarr/Radarr-importing-existing.png)

기존 영화 폴더의 이름이 잘 지정되어 있다면 Radarr은 해당 영화와 일치하려고 시도합니다. 5번에서 볼 수 있듯이 모든 영화가 단일 디렉토리에 있는 경우 [이 가이드](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)를 따르세요.

1. 영화 폴더 이름입니다.
1. 모니터링 - 영화를 Radarr에 추가하는 방법입니다.

- 없음 - 영화나 컬렉션을 새로운 릴리스로 모니터링하지 않습니다.
- 영화만 - 영화를 새로운 릴리스로만 모니터링합니다.
- 영화 및 컬렉션 - 영화를 새로운 릴리스로 모니터링하고, 영화의 컬렉션에 있는 모든 영화를 추가하고 모니터링합니다(컬렉션이 있는 경우).

1. 가용성 - Radarr이 영화를 사용 가능하다고 간주하는 시점입니다.

- **공지**: Radarr은 영화가 Radarr에 추가되자마자 사용 가능하다고 간주합니다. 이 설정은 품질이 좋고 가짜가 없는 좋은 개인 트래커를 사용하는 경우 *권장*됩니다.
- **상영 중**: Radarr은 영화가 영화관에 출시되는 즉시 사용 가능하다고 간주합니다. 이 옵션은 *권장되지 않습니다*.
- **출시**: Radarr은 블루레이가 출시되는 즉시 사용 가능하다고 간주합니다. 이 옵션은 인덱서에 자주 가짜가 포함된 경우 *권장*됩니다.

1. 품질 프로필 - 사용할 기본 프로필을 선택합니다.
1. 영화 - Radarr이 일치하는 영화로 간주하는 영화입니다. 이를 검토하고 일치하지 않는 경우 수정 또는 검색해야 합니다. 잘못된 일치는 잘못된 폴더 이름으로 인해 발생하는 경우가 많습니다.
1. 일괄적으로 모니터링 상태 선택.
1. 일괄적으로 최소 가용성 선택.
1. 일괄적으로 품질 프로필 선택.
1. 기존 미디어 라이브러리를 가져오기 시작합니다.

영화가 Radarr에 추가되면 Radarr은 영화의 폴더를 스캔하고 폴더 내의 비디오 파일을 영화와 일치시키려고 합니다. Radarr이 파일과 영화를 일치시키지 못하고 영화의 Radarr 상태가 누락된 상태인 경우 가장 일반적인 원인은 파일 이름에 연도가 포함되어 있지 않기 때문입니다. Radarr은 구문 분석 가능하도록 파일 이름에 연도가 포함되어야 합니다.  

### 일치하는 항목 없음

다음과 같은 오류가 발생하는 경우

![Radarr-importing-existing-no-match.png](/assets/radarr/Radarr-importing-existing-no-match.png)

영화 폴더 이름을 잘못 지정한 것 같습니다.

다음과 같이 문제를 해결할 수 있습니다.

오류 메시지를 확장합니다.

![Radarr-importing-existing-no-match-expand.png](/assets/radarr/Radarr-importing-existing-no-match-expand.png)

그리고 [themoviedb](https://www.themoviedb.org/)에서 연도나 제목이 일치하는지 확인합니다. 이 예제에서는 연도가 잘못되었음을 알 수 있으며, 연도를 변경하고 새로 고침 아이콘을 클릭하여 수정할 수 있습니다.

![radarr-importing-existing-no-match-expand-refresh.png](/assets/radarr/radarr-importing-existing-no-match-expand-refresh.png)

또는 tmdb:id 또는 imdb:id(만약 tmdb가 imdb에 연결되어 있는 경우)를 사용하고 일치하는 영화를 선택할 수도 있습니다.

![Radarr-importing-existing-no-match-expand-tmdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-tmdb.png)

![Radarr-importing-existing-no-match-expand-imdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-imdb.png)

### 가져온 후 잘못된 폴더 이름 수정하기

![Radarr-wrong-folder-name.png](/assets/radarr/Radarr-wrong-folder-name.png)

가져온 후 수정한 것을 확인할 수 있습니다. 폴더 이름에 여전히 잘못된 연도가 포함되어 있습니다. 이를 수정하기 위해 약간의 마법을 사용해 보겠습니다.

영화 개요로 이동하세요.

`영화`

상단에서 `영화 편집기`를 클릭하세요.

![Radarr-movie-editor.png](/assets/radarr/Radarr-movie-editor.png)

활성화한 후 폴더 이름을 변경하려는 영화를 선택하세요.

![Radarr-movie-editor-select.png](/assets/radarr/Radarr-movie-editor-select.png)

1. 폴더 이름을 이전에 설정한 폴더 이름 규칙으로 변경하려면 모든 영화 폴더의 이름을 설정하세요 [영화 이름 지정 섹션](#영화-이름-지정).
2. 폴더 이름을 변경하려는 영화를 선택하세요.
3. 동일한 `루트 폴더`를 선택하세요.

새로운 팝업이 표시됩니다.

![Radarr-movie-editor-move-files-yes.png](/assets/radarr/Radarr-movie-editor-move-files-yes.png)

`예, 파일 이동`을 선택하세요.

그럼 마법이 일어납니다.

![Radarr-correct-folder-name.png](/assets/radarr/Radarr-correct-folder-name.png)

올바른 연도를 따르는 폴더 이름으로 변경된 것을 확인할 수 있습니다.

## 영화 추가 방법

기존에 정리된 미디어 라이브러리를 가져온 후 원하는 영화를 추가하는 시간입니다.

`영화` => `새로 추가`

![Radarr-add-new.png](/assets/radarr/Radarr-add-new.png)

상자에 원하는 영화 이름을 입력하거나 tmdb:id 또는 imdb:id를 사용하세요.

영화 이름을 입력하는 동안 결과가 표시될 것입니다.

![Radarr-movie-search.png](/assets/radarr/Radarr-movie-search.png)

원하는 영화를 보면 클릭하세요.

![Radarr-movie-add.png](/assets/radarr/Radarr-movie-add.png)

1. 루트 폴더 - Radarr는 영화를 설정한 루트 폴더에 추가합니다 [루트 폴더 섹션](#루트-폴더).
2. 모니터링 - 영화를 Radarr에 추가하는 방법입니다.

- 영화만 = Radarr는 라이브러리에 없는 영화를 RSS 피드에서 모니터링하거나 기존 영화를 더 좋은 품질로 업그레이드합니다.
- 영화 및 컬렉션 = Radarr는 라이브러리에 없는 영화를 RSS 피드에서 모니터링하거나 기존 영화를 더 좋은 품질로 업그레이드합니다. 또한 이 영화의 컬렉션에 속한 모든 영화를 선택한 설정으로 추가합니다.
- 없음 = Radarr는 RSS 피드를 모니터링하지 않으며 업그레이드나 새로운 영화는 무시되며 수동으로 수행해야 합니다. 모니터링되지 않은 영화에 대한 모든 검색은 수동으로 트리거되거나 대화식 검색을 수행해야 합니다.

1. 이용 가능 여부 - Radarr가 영화를 이용 가능하다고 간주하는 시점을 설정합니다.

> 아래 이용 가능성에 영향을 주는 TMDB의 날짜에 대한 자세한 정보는 [Radarr가 영화의 연도를 어떻게 결정하는가](#Radarr가-영화의-연도를-어떻게-결정하는가)를 참조하세요.
{.is-info}

- **발표 예정**: Radarr는 영화가 Radarr에 추가되는 즉시 이용 가능하다고 간주합니다. 이 설정은 가짜가 없는 좋은 개인 트래커(또는 정말 좋은 공개 트래커, 예: rarbg.to)를 사용하는 경우에 권장됩니다.
- **극장 개봉**: Radarr는 영화가 극장에서 상영되는 즉시 이용 가능하다고 간주합니다 (TMDb의 극장 개봉일). 이 옵션은 권장되지 않습니다.
- **출시**: Radarr는 블루레이 또는 스트리밍 버전이 출시되는 즉시 영화를 이용 가능하다고 간주합니다 (TMDb의 디지털 및 물리적 출시일). 이 옵션은 권장되며, `-14` 또는 `-21`일의 이용 가능 지연과 함께 사용하는 것이 좋습니다.
  - TMDb에 날짜가 없는 경우, 극장 개봉일로부터 90일 후에 웹 또는 물리적 서비스에서 영화가 이용 가능하다고 가정합니다.

1. 품질 프로필 - 이 영화에 사용할 프로필을 선택하세요.
1. 태그 - 고급 사용을 위해 특정 태그를 추가할 수 있습니다.
1. 추가 시 검색 - Radarr가 Radarr에 추가된 영화가 누락된 경우 검색하도록 이 기능을 활성화하세요 [자세한 정보](/radarr/faq#Radarr가-영화를-찾는-방법)
1. `영화 추가`를 클릭하여 영화를 Radarr에 추가하세요.

- "경로가 이미 구성되어 있음" 오류가 발생하는 경우 [이 FAQ 항목](/radarr/faq#기존-영화에-대한-경로가-이미-구성되어-있음)을 참조하세요.