---
title: Readarr 사용자 정의 스크립트
description: 
published: true
date: 2022-05-02T03:36:38.595Z
tags: readarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-23T06:41:11.792Z
---

사용자 정의 스크립트를 실행하려면 [여기](/readarr/settings#connections)에서 자세한 내용을 찾을 수 있습니다. 스크립트는 Readarr에 [연결 설정](/readarr/settings#connections)을 통해 추가됩니다.

# 개요

Readarr는 책을 새로 가져오거나 이름을 바꿀 때 사용자 정의 스크립트를 실행할 수 있습니다. 동작에 따라 다른 매개변수가 제공됩니다. 매개변수는 환경 변수를 통해 스크립트로 전달됩니다.

## Readarr 로그

다음은 사용자 정의 스크립트에 대해서만 로그에 기록됩니다:

- 스크립트의 `stdout` 출력은 `Debug`로 기록됩니다.
- 스크립트의 `stderr` 출력은 `Info`로 기록됩니다.
- 스크립트의 트리거는 `Trace`로 기록됩니다.

# 환경 변수

## 가져올 때

| 환경 변수                         | 세부 정보                                 |
| ---------------------------------- | ------------------------------------------- |
| `readarr_eventtype`                | `Grab`                                      |
| `readarr_author_id`                | 작가의 내부 ID                              |
| `readarr_author_name`              | 작가의 이름                                |
| `readarr_author_grid`              | 작가의 Goodreads ID                         |
| `readarr_release_bookcount`        | 릴리스에 포함된 책의 수                     |
| `readarr_release_bookreleasedates` | 책의 릴리스 날짜                           |
| `readarr_release_booktitles`       | 릴리스의 책 제목                            |
| `readarr_release_bookids`          | 책의 ID                                     |
| `readarr_release_grids`            | 릴리스의 Goodreads ID                       |
| `readarr_release_title`            | 책의 제목                                  |
| `readarr_release_indexer`          | 릴리스를 가져온 인덱서                      |
| `readarr_release_size`             | 릴리스 크기                                |
| `readarr_release_quality`          | 릴리스 품질                                |
| `readarr_release_qualityVersion`   | 릴리스 품질 버전                           |
| `readarr_release_releasegroup`     | 릴리스 그룹 (알 수 없는 경우 비어 있음)    |
| `readarr_download_client`          | 릴리스를 다운로드하는 데 사용된 클라이언트 |
| `readarr_download_id`              | 다운로드 ID                                |

## 가져오거나 업그레이드할 때

| 환경 변수                   | 세부 정보                                 |
| -------------------------- | ------------------------------------------- |
| `readarr_eventtype`        | `Download`                                  |
| `readarr_author_id`        | 작가의 내부 ID                              |
| `readarr_author_name`      | 작가의 이름                                |
| `readarr_author_path`      | 작가의 경로                                |
| `readarr_author_grid`      | 작가의 Goodreads ID                         |
| `readarr_book_id`          | 책의 ID                                     |
| `readarr_book_title`       | 책의 제목                                  |
| `readarr_book_grid`        | 책의 Goodreads ID                           |
| `readarr_book_releasedate` | 책의 릴리스 날짜                           |
| `readarr_download_client`  | 릴리스를 다운로드하는 데 사용된 클라이언트 |
| `readarr_download_id`      | 다운로드 ID                                |

## 이름을 바꿀 때

| 환경 변수          | 세부 정보                   |
| ----------------- | ------------------------- |
| `readarr_eventtype`   | `Rename`                  |
| `readarr_author_id`   | 작가의 내부 ID |
| `readarr_author_name` | 작가의 이름        |
| `readarr_author_path` | 작가의 경로        |
| `readarr_author_grid` | 작가의 Goodreads ID       |

## 책의 태그를 다시 지정할 때

| 환경 변수              | 세부 정보                   |
| --------------------- | ------------------------- |
| `readarr_eventtype`               | `TrackRetag`              |
| `readarr_author_id`               | 작가의 내부 ID |
| `readarr_author_name`             | 작가의 이름        |
| `readarr_author_path`             | 작가의 경로        |
| `readarr_author_grid`             | 작가의 Goodreads ID       |
| `readarr_book_id`                 | 책의 ID                 |
| `readarr_book_title`              | 책의 제목              |
| `readarr_book_grid`               | 책의 Goodreads ID       |
| `readarr_book_releasedate`        | 책의 릴리스 날짜  |
| `readarr_bookfile_id`             | 책 파일의 ID              |
| `readarr_bookfile_path`           | 책의 경로          |
| `readarr_bookfile_quality`        | 책 파일의 품질         |
| `readarr_bookfile_qualityversion` | 책 파일의 품질 버전 |
| `readarr_bookfile_releasegroup`   | 책의 릴리스 그룹 |
| `readarr_bookfile_scenename`      | 책의 Scene 이름    |
| `readarr_tags_diff`               | 태그의 차이          |
| `readarr_tags_scrubbed`           | 정리된 태그             |

## 건강 문제가 발생했을 때

| 환경 변수           | 세부 정보                                                      |
| ------------------------------ | ------------------------------------------------------------ |
| `readarr_eventtype`            | `HealthIssue`                                                |
| `readarr_health_issue_level`   | 건강 문제의 유형 (`Ok`, `Notice`, `Warning`, 또는 `Error`) |
| `readarr_health_issue_message` | 건강 문제의 메시지                                |
| `readarr_health_issue_type`    | 실패한 영역 및 건강 문제를 트리거한 유형              |
| `readarr_health_issue_wiki`    | 위키 URL (존재하지 않는 경우 비어 있음)                           |

## 테스트할 때

Readarr에 스크립트를 추가하고 '테스트'를 클릭하면 다음과 같은 매개변수로 스크립트가 호출됩니다. 스크립트는 지원되지 않는 이벤트 유형을 우아하게 무시할 수 있어야 합니다.

| 환경 변수 | 세부 정보 |
| -------------------- | ------- |
| `readarr_eventtype`  | `Test`  |