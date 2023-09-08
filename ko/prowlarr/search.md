---
title: Prowlarr 검색
description: 
published: true
date: 2022-01-02T23:05:56.758Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:31:53.221Z
---

이 페이지에서는 Prowlarr에서 검색하는 방법을 안내합니다. 일반적으로 검색은 앱을 통해 이루어지지만, Prowlarr에서 직접 검색할 수도 있습니다.

# 검색 수행하기

검색을 시작하려면 왼쪽 메뉴에서 `Search`를 클릭하십시오. 화면 하단에 일부 옵션이 있는 대부분 공백으로 된 페이지가 표시됩니다.

![search_1_searchscreen.png](/assets/prowlarr/search_1_searchscreen.png)

- Query - 검색어를 Query 필드에 입력하십시오.
  - 검색 유형을 변경하려면 돋보기 아이콘을 클릭하십시오. 사용 가능한 옵션은 다음과 같습니다:
    - 기본 검색 - 기본 텍스트 쿼리
    - TV 검색 - TV 매개변수를 사용한 검색 (TVDbId, IMDbId, TMDbID 등) 및 시즌/에피소드 검색
    - 영화 검색 - 영화 매개변수를 사용한 검색 (TMDbId, IMDbId, 장르 등)
    - 오디오 검색 - 음악 매개변수를 사용한 검색 (아티스트, 앨범, 레이블, 장르 등)
    - 책 검색 - 책 매개변수를 사용한 검색 (작가, 제목 등)

> 이들은 일반적으로 `{VariableName:SearchValue}` 형식으로 표시됩니다. 예를 들어 The Simpsons Season 32의 TV 검색의 경우 검색 입력은 `{TvdbId:71663} {Season:32}`가 됩니다.
{.is-info}

> 모든 인덱서가 모든 쿼리 유형을 지원하지 않을 수 있습니다.
{.is-info}

- Indexers - Indexers 드롭다운에서 원하는 인덱서를 선택하십시오. "Usenet" 또는 "Torrents"를 선택하여 해당 카테고리의 모든 인덱서를 자동으로 선택하거나, 검색에 대해 특정 인덱서를 선택할 수도 있습니다.
- Category - 드롭다운에서 인덱서에서 검색할 카테고리를 선택하십시오. 상위 카테고리 (TV, 영화 등)를 선택하여 하위 카테고리를 자동으로 선택하거나, 그룹 중에서 특정 카테고리를 선택할 수도 있습니다.

그런 다음 `Search` 버튼을 클릭하십시오. 결과가 나타나기까지 몇 초가 걸릴 수 있습니다. 결과가 나타나면 `Options` 버튼을 사용하여 열을 추가하거나 제거할 수 있으며, 열 머리글을 클릭하거나 `Filter` 버튼을 사용하여 결과를 정렬하고 필터링할 수 있습니다.

결과를 다운로드하려면 결과 오른쪽의 다운로드 아이콘을 클릭하십시오. 이렇게 하면 구성된 적절한 다운로드 클라이언트로 전송됩니다.

왼쪽에서 선택란을 선택하고 `Grab Releases` 버튼을 클릭하여 한 번에 여러 결과를 일괄로 가져올 수 있습니다.

> 다운로드된 항목은 Prowlarr에서 설정한 카테고리 할당을 갖게 됩니다. 이는 앱 프로그램에서 비표준 디렉토리로부터 수동으로 가져와야 할 수도 있습니다!
{.is-info}

# API 엔드포인트

## RSS 호환 - 단일 인덱서 피드

- 표준 Newznab/Torznab 호환 엔드포인트/매개변수입니다. 정의된 표준에 따라 필요에 따라 쿼리를 조정할 수 있습니다.

> 다중 인덱서 엔드포인트는 해당 기능의 중요한 단점으로 인해 추가되지 않을 것입니다.
{.is-info}

### 쿼리에서 API 키 사용

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - 예: `http://192.168.1.100:9696/11/api?t=search&q=mike&apikey={yourkey}&cat=5000,2000`

### 헤더에서 API 키 사용

> 헤더로 API 키를 전달할 때 `X-Api-Key`를 반드시 포함해야 합니다.
{.is-info}

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - 예: `http://192.168.1.100:9696/{indexerid}/api?t=search&q=mike&cat=5000,2000`

## 검색 피드

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/api/v1/search?query={encoded term}&indexerIds={comma separated list}&categories={comma separated list}&type={searchtype}`
  - 예: `http://192.168.1.100/prowlarr/api/v1/search?query=black%20hawk%20down&indexerIds=-1&categories=2000&type=search`
  - 예: `http://192.168.1.100/prowlarr/api/v1/search?query=%7BTvdbId%3A71663%7D%20%7BSeason%3A32%7D&categories=5000&type=tvsearch`

매개변수

- `query` - URL 인코딩된 검색 문자열
- `indexerIds` - 쉼표로 구분된 인덱서 ID 목록
  - 모든 인덱서를 위한 매개변수를 생략하려면 매개변수를 URL에서 제거하십시오.
  - `-2`는 모든 토렌트를 의미합니다.
  - `-1`은 모든 유즈넷을 의미합니다.
  - 인덱서 ID
- `categories` - 사용할 카테고리의 쉼표로 구분된 목록
  - 모든 카테고리를 위한 매개변수를 생략하십시오.
- `type` - 수행할 검색 유형
  - `search` - 기본 텍스트 쿼리
  - `tvsearch` - TV 쿼리 - TV 매개변수 지원
  - `moviesearch` - 영화 쿼리 - 영화 매개변수 지원
  - `audiosearch` - 오디오/음악 쿼리 - 음악 매개변수 지원
  - `booksearch` - 책 쿼리 - 책 매개변수 지원