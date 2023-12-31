---
title: Radarr 라이브러리
description: 
published: true
date: 2022-11-14T15:04:06.364Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:24:18.386Z
---

# 영화

## 라이브러리 보기

- 모두 업데이트 - 모든 영화의 메타데이터를 업데이트하고 포스터를 새로 고치며 영화 폴더와 파일을 다시 스캔합니다(활성화된 경우).
- 새로 고치고 스캔 - 현재 보고 있는 영화의 메타데이터를 새로 고치고 해당 폴더를 다시 스캔합니다.
- RSS 동기화 - 인덱서에서 RSS 피드를 새로 고치고 새로 게시된 항목을 확인합니다.
- 모두 검색 / 필터링된 항목 검색 / 선택된 항목 검색 - 현재 보기에서 모든 영화 또는 선택된 영화를 검색합니다.
- 수동 가져오기 (영화 인덱스) - Radarr에 추가한 영화의 파일을 Radarr이 액세스할 수 있는 모든 폴더에서 수동으로 가져옵니다.
  - 자동 이동 - 파일을 Radarr의 영화와 일치시키려고 자동으로 시도하고 이동하여 가져옵니다.
  - 대화식 가져오기 - 경로 내의 모든 파일을 검토하고 Radarr의 영화와 일치시키려고 시도하여 결과를 검토할 수 있습니다. 하단 왼쪽 모서리에서 이동 또는 복사/하드링크를 선택할 수 있습니다.
- 수동 가져오기 (영화) - Radarr에 추가한 영화의 폴더에서 영화 파일을 수동으로 가져옵니다.
  - 자동 이동 - 파일을 Radarr의 영화와 일치시키려고 자동으로 시도하고 이동하여 가져옵니다.
  - 대화식 가져오기 - 경로 내의 모든 파일을 검토하고 Radarr의 영화와 일치시키려고 시도하여 결과를 검토할 수 있습니다. 하단 왼쪽 모서리에서 이동 또는 복사/하드링크를 선택할 수 있습니다.
- 영화 편집기 / 영화 인덱스 - 대량 편집기 모드와 영화 인덱스(라이브러리) 모드 사이를 전환합니다.
- 옵션 - 표시 옵션 변경
- 보기 - 보기 유형 전환
  - 테이블 - 표 형식 보기(목록 보기)
  - 포스터 - 포스터 표시(Plex와 유사)
  - 개요 - 개요 정보와 포스터 표시(자세한 보기)
- 정렬 - 현재 보기 정렬

### 필터

- 필터 - 현재 보기 필터링
  - 모니터링 중인 것만 - 업데이트를 모니터링하는 제목.
  - 모니터링 중이 아닌 것 - 업데이트를 모니터링하지 않는 제목.
  - 누락됨 - 데이터베이스에 있으며 모니터링 중이지만 파일 시스템에 없는 제목.
  - 원하는 - 데이터베이스에 있으며 모니터링 중이며 누락되었지만 가용성 설정에 따라 사용 가능해야 하는 제목
  - 컷오프 미달 - 파일 시스템에 있는 제목이지만 원하는 품질을 모니터링 중인 경우.
  - 사용자 정의 필터
    - 모니터링(부울)
    - 사용 가능한 것으로 간주(부울)
    - 최소 가용성(열거형)
      - 발표 예정
      - 상영 중
      - 개봉
    - 제목 \[포함\] (문자열)
    - 출시 상태(열거형)
      - TBA
      - 발표 예정
      - 상영 중
      - 개봉
      - 삭제됨
        - TMDb에서 삭제됨
    - 스튜디오(열거형 스튜디오)
    - 컬렉션(열거형 컬렉션)
    - 품질 프로필(열거형 품질 프로필)
    - 추가됨(정적 날짜 및 시간, 상대적 시간 간격)
    - 연도(정수)
    - 상영 중(정적 날짜 및 시간, 상대적 시간 간격)
    - 물리적 출시(정적 날짜 및 시간, 상대적 시간 간격)
    - 디지털 출시(정적 날짜 및 시간, 상대적 시간 간격)
    - 상영 시간(정수)
    - 경로 \[포함\] (문자열)
    - 디스크 크기(정수)
    - 장르 \[포함\] (열거형 장르)
    - TMDB 평점(부동소수점)
    - TMDB 투표(정수)
    - IMDb 평점
    - 토마토 평점
    - IMDb 투표
    - 인증(등급 열거형(PG-13, R 등))
    - 태그 \[포함\] (열거형 태그)

# 새로 추가

![radarr-add-new-empty.png](/assets/radarr/radarr-add-new-empty.png)

- 새로운 영화를 추가하려면 이 페이지에서 작업을 수행해야 합니다.
  - 자세한 내용은 [빠른 시작 가이드](/radarr/quick-start-guide)에서 확인할 수 있습니다.
- 검색 필드 아래에는 기존 영화 가져오기 버튼도 있습니다. 해당 경우에 대한 유용한 정보는 [빠른 시작 가이드](/radarr/quick-start-guide)에서 찾을 수 있습니다.
- "경로가 이미 구성되었습니다"라는 오류가 발생하는 경우, [이 FAQ 항목](/radarr/faq#path-is-already-configured-for-an-existing-movie)을 참조하세요.

# 라이브러리 가져오기

라이브러리 가져오기를 사용하면 기존에 정리된 영화와 각 영화의 파일을 경로 디렉토리의 기존 파일을 통해 가져올 수 있습니다. 이 기능은 새로운 Radarr 인스턴스를 만들고 기존 영화를 유지하려는 경우에 특히 유용합니다.

- 라이브러리 가져오기는 Radarr에 기존에 정리된 영화 라이브러리를 추가하고 가져오는 데 사용됩니다.
- 라이브러리 가져오기는 다음과 같은 용도로 사용할 수 없습니다.
  - 다운로드 폴더에서 파일 가져오기
  - 올바르게 이름이 지정되고 자체 영화 폴더 내에서 조직된 하나 이상의 파일 추가 또는 가져오기
  - 라이브러리 가져오기에 입력된 루트(라이브러리) 폴더에서 영화와 해당 파일을 추가하는 것이 아닌 다른 용도
- "경로가 이미 구성되었습니다"라는 오류가 발생하는 경우, [이 FAQ 항목](/radarr/faq#path-is-already-configured-for-an-existing-movie)을 참조하세요.
  
> 가져올 영화 폴더와 파일에는 이름에 연도가 포함되어 있어야 합니다.{.is-warning}

> \* Windows가 아닌 경우: NFS 마운트를 사용하는 경우 `nolock`이 활성화되어 있는지 확인하세요.
> \* SMB 마운트를 사용하는 경우 `nobrl`이 활성화되어 있는지 확인하세요.
{.is-warning}

> **Radarr을 실행하도록 구성한 사용자 및 그룹은이 위치에 대한 읽기 및 쓰기 액세스 권한이 있어야 합니다.**
{.is-info}

> 다운로드 클라이언트는 다운로드 폴더에 다운로드하고 Radarr은 미디어 서버가 사용하는 미디어 폴더(최종 목적지)로 가져옵니다.
{.is-info}

> **다운로드 폴더와 미디어 폴더는 동일한 위치일 수 없습니다.**
{.is-danger}

# 컬렉션

이 위키는 커뮤니티에 의해 개발 및 유지되고 있습니다.
이 섹션에는 Radarr의 컬렉션 페이지를 반영하고 설명하는 기여가 없습니다.

# 탐색

탐색은 추천 영화를 보여줍니다.

- 목록이 없는 경우, 라이브러리의 영화에 대한 TMDb에서 추천하는 영화 중 상위 90개와 가장 최근 추가된 10개의 추천 영화를 보여줍니다.

> 팁: `옵션`에서 Radarr 추천 영화를 비활성화하고 목록에서만 영화를 볼 수 있습니다.
{.is-info}

- 목록이 있는 경우, 위에서 언급한 추천 사항과 목록의 항목을 표시합니다.

> 팁: `필터`를 `새로운 제외`로 변경하여 라이브러리에 없는 영화만 표시할 수 있습니다.
{.is-info}

![radarr-discover-empty.png](/assets/radarr/radarr-discover-empty.png)

- 영화가 적거나 전혀 없는 새로운 설치인 경우, 탐색 추천이 제한적일 수 있습니다. 추천 방향을 제공하기 위해 라이브러리 콘텐츠를 추가해야 합니다. 다음과 같은 옵션이 있습니다:
  1. [새로운 영화 추가](/radarr/library#add-new) 버튼을 클릭하여 수동으로 영화를 추가합니다.
  1. [기존 라이브러리 가져오기](/radarr/library#library-import) 버튼을 클릭하여 기존 라이브러리를 가져옵니다.
  1. [목록 추가](/radarr/settings#lists) 버튼을 클릭하여 목록을 Radarr에 추가합니다. 이 섹션의 [추가 정보(지원)](/radarr/faq#what-are-lists-and-what-can-they-do-for-me) 페이지에서 목록에 대한 자세한 정보를 찾을 수 있습니다.

![radarr-discover-add-new-movies.png](/assets/radarr/radarr-discover-add-new-movies.png)

- 위에서 나열한 세 가지 옵션 중 하나로 영화를 추가한 후, 다른 영화를 찾을 수 있습니다.
    1. 여기에서 라이브러리에 추가할 영화를 선택할 수 있습니다.
    1. 이 목록에 있는 모든 영화를 선택할 수 있습니다.
    1. 가져온 후 이 영화가 이동할 루트 경로를 선택합니다.
    1. 가져오기 전에 영화가 가져야 할 가용성을 선택합니다.
    1. 이미 작성한 품질 프로필을 선택합니다([자세한 정보](/radarr/settings#quality-profiles)).
    1. Radarr이 이 영화를 품질 업그레이드를 모니터링해야 할까요?
    1. 영화를 추가한 후 Radarr이 이 영화를 자동으로 검색해야 할까요?
    1. 가져온 목록에서 이 영화를 제외할까요? ([자세한 정보](/radarr/settings#list-exclusion))
    1. 마지막으로, 영화를 라이브러리에 추가합니다.