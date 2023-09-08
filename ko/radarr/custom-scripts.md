# Radarr 사용자 지정 스크립트
---
title: Radarr 사용자 지정 스크립트
description: 
published: true
date: 2022-05-02T03:36:09.625Z
tags: radarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:44.765Z
---

사용자 정의 스크립트를 실행하려면 여기에서 자세한 내용을 찾을 수 있습니다. 스크립트는 [연결 설정](/radarr/settings#connections)을 통해 Radarr에 추가됩니다.

# 개요

Radarr는 영화를 가져오거나 이름을 바꿀 때 사용자 정의 스크립트를 실행할 수 있습니다. 동작에 따라 다른 매개변수가 제공됩니다. 매개변수는 환경 변수를 통해 스크립트로 전달됩니다.

## Radarr 로그

다음은 사용자 정의 스크립트에 대해서만 로그에 기록됩니다:

- 스크립트의 `stdout` 출력은 `Debug`로 기록됩니다.
- 스크립트의 `stderr` 출력은 `Info`로 기록됩니다.
- 스크립트의 트리거는 `Trace`로 기록됩니다.

# 환경 변수

## 가져오기 시

| 환경 변수                           | 세부 정보                                                                                   |
| ------------------------------------ | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                   | `Grab`                                                                                       |
| `radarr_download_client`             | 다운로드 클라이언트 (알 수 없는 경우 비어 있음)                                                           |
| `radarr_download_id`                 | 토렌트/NZB 파일의 해시 (다운로드 클라이언트에서 다운로드를 고유하게 식별하는 데 사용됨) |
| `radarr_movie_id`                    | 영화의 내부 ID                                                                             |
| `radarr_movie_imdbid`                | 영화의 IMDb ID (알 수 없는 경우 비어 있음)                                                     |
| `radarr_movie_in_cinemas_date`       | 영화의 개봉일 (알 수 없는 경우 비어 있음)                                                       |
| `radarr_movie_physical_release_date` | 영화의 실제 출시일 (알 수 없는 경우 비어 있음)                                                     |
| `radarr_movie_title`                 | 영화의 제목                                                                           |
| `radarr_movie_tmdbid`                | 영화의 TMDb ID                                                                        |
| `radarr_movie_year`                  | 영화의 개봉 연도                                                                    |
| `radarr_release_indexer`             | 릴리스가 가져온 인덱서                                                   |
| `radarr_release_quality`             | Radarr에서 감지한 릴리스의 품질 이름                                           |
| `radarr_release_qualityversion`      | `1`은 기본값, `2`는 적합한 값이며, `3`+는 애니메이션 버전에 사용될 수 있습니다             |
| `radarr_release_releasegroup`        | 릴리스 그룹 (알 수 없는 경우 비어 있음)                                                             |
| `radarr_release_size`                | 인덱서가 보고한 릴리스의 크기                                              |
| `radarr_release_title`               | 토렌트/NZB 제목                                                                            |

## 가져오기/업그레이드 시

| 환경 변수                           | 세부 정보                                                                                   |
| ------------------------------------ | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                   | `Download`                                                                                   |
| `radarr_download_id`                 | 토렌트/NZB 파일의 해시 (다운로드 클라이언트에서 다운로드를 고유하게 식별하는 데 사용됨) |
| `radarr_download_client`             | 다운로드 클라이언트                                                                              |
| `radarr_isupgrade`                   | 기존 파일이 업그레이드되었을 때 `True`, 그렇지 않으면 `False`                                  |
| `radarr_movie_id`                    | 영화의 내부 ID                                                                             |
| `radarr_movie_imdbid`                | 영화의 IMDb ID (알 수 없는 경우 비어 있음)                                                     |
| `radarr_movie_in_cinemas_date`       | 영화의 개봉일 (알 수 없는 경우 비어 있음)                                                       |
| `radarr_movie_path`                  | 영화의 전체 경로                                                                       |
| `radarr_movie_physical_release_date` | 영화의 실제 출시일 (알 수 없는 경우 비어 있음)                                                     |
| `radarr_movie_title`                 | 영화의 제목                                                                           |
| `radarr_movie_tmdbid`                | 영화의 TMDb ID                                                                        |
| `radarr_movie_year`                  | 영화의 개봉 연도                                                                    |
| `radarr_moviefile_id`                | 영화 파일의 내부 ID                                                                |
| `radarr_moviefile_relativepath`      | 영화 파일의 경로, 영화 경로를 기준으로 상대적인 경로                                           |
| `radarr_moviefile_path`              | 영화 파일의 전체 경로                                                                  |
| `radarr_moviefile_quality`           | Radarr에서 감지한 릴리스의 품질 이름                                           |
| `radarr_moviefile_qualityversion`    | `1`은 기본값, `2`는 적합한 값이며, `3`+는 애니메이션 버전에 사용될 수 있습니다             |
| `radarr_moviefile_releasegroup`      | 릴리스 그룹 (알 수 없는 경우 비어 있음)                                                             |
| `radarr_moviefile_scenename`         | 원래 릴리스 이름 (알 수 없는 경우 비어 있음)                                                     |
| `radarr_moviefile_sourcepath`        | 가져온 영화 파일의 전체 경로                                                         |
| `radarr_moviefile_sourcefolder`      | 영화 파일이 가져온 폴더의 전체 경로                                     |
| `radarr_deletedrelativepaths`        | 이 파일을 가져오기 위해 삭제된 파일의 `|`로 구분된 목록                            |
| `radarr_deletedpaths`                | 이 파일을 가져오기 위해 삭제된 파일의 전체 경로의 `|`로 구분된 목록              |

## 이름 변경 시

| 환경 변수                                | 세부 정보                                       |
| ---------------------------------------- | ----------------------------------------------- |
| `radarr_eventtype`                       | `Rename`                                        |
| `radarr_movie_id`                        | 영화의 내부 ID                                  |
| `radarr_movie_title`                     | 영화의 제목                                    |
| `radarr_movie_year`                      | 영화의 개봉 연도                               |
| `radarr_movie_path`                      | 영화의 전체 경로                               |
| `radarr_movie_imdbid`                    | 영화의 IMDb ID (알 수 없는 경우 비어 있음)     |
| `radarr_movie_tmdbid`                    | 영화의 TMDb ID                                 |
| `radarr_movie_in_cinemas_date`           | 영화의 개봉일 (알 수 없는 경우 비어 있음)      |
| `radarr_movie_physical_release_date`     | 영화의 실제/웹 배포일 (알 수 없는 경우 비어 있음) |
| `radarr_moviefile_ids`                   | 파일 ID의 `,`로 구분된 목록                     |
| `radarr_moviefile_relativepaths`         | 상대 경로의 `|`로 구분된 목록                   |
| `radarr_moviefile_paths`                 | 경로의 `|`로 구분된 목록                        |
| `radarr_moviefile_previousrelativepaths` | 이전 상대 경로의 `|`로 구분된 목록              |
| `radarr_moviefile_previouspaths`         | 이전 경로의 `|`로 구분된 목록                   |

## 건강 상태 확인 시

| 환경 변수                       | 세부 정보                                                         |
| ----------------------------- | ----------------------------------------------------------------- |
| `radarr_eventtype`            | `HealthIssue`                                                     |
| `radarr_health_issue_level`   | 건강 문제의 유형 (`Ok`, `Notice`, `Warning` 또는 `Error`)            |
| `radarr_health_issue_message` | 건강 문제에서의 메시지                                            |
| `radarr_health_issue_type`    | 실패한 영역 및 건강 문제를 트리거한 영역                            |
| `radarr_health_issue_wiki`    | 위키 URL (존재하지 않는 경우 비어 있음)                            |

## 애플리케이션 업데이트 시

| 환경 변수                        | 세부 정보                               |
|--------------------------------- |-------------------------------------- |
| `radarr_eventtype`               | `ApplicationUpdate`                   |
| `radarr_update_message`          | 업데이트에서의 메시지                   |
| `radarr_update_newversion`       | Radarr이 업데이트된 버전 (문자열)       |
| `radarr_update_previousversion`  | Radarr이 업데이트되기 전 버전 (문자열)  |

## 테스트 시

Radarr에 스크립트를 추가하고 '테스트'를 클릭하면 다음 매개변수와 함께 스크립트가 호출됩니다. 스크립트는 지원되지 않는 이벤트 유형을 우아하게 무시할 수 있어야 합니다.

| 환경 변수             | 세부 정보 |
| -------------------- | ------- |
| `radarr_eventtype`   | `Test`  |