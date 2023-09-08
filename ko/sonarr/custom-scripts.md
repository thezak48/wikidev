# 개요

Sonarr은 에피소드가 새로 가져오거나 이름이 변경될 때 사용자 정의 스크립트를 실행할 수 있습니다. 동작에 따라 다른 매개변수가 제공됩니다. 매개변수는 환경 변수를 통해 스크립트로 전달됩니다.

## Sonarr 로그

다음은 사용자 정의 스크립트에 대해서만 로그에 기록됩니다:

- 스크립트의 `stdout` 출력은 `Debug`로 기록됩니다.
- 스크립트의 `stderr` 출력은 `Info`로 기록됩니다.
- 스크립트의 트리거는 `Trace`로 기록됩니다.

# 환경 변수

## 가져올 때

| 환경 변수                               | 세부 정보                                                                                     |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Grab`                                                                                       |
| `sonarr_series_id`                      | 시리즈의 내부 ID                                                                              |
| `sonarr_series_title`                   | 시리즈의 제목                                                                                |
| `sonarr_series_tvdbid`                  | 시리즈의 TVDB ID                                                                              |
| `sonarr_series_tvmazeid`                | 시리즈의 TVMaze ID                                                                            |
| `sonarr_series_imdbid`                  | 시리즈의 IMDB ID (알 수 없는 경우 비어 있음)                                                  |
| `sonarr_series_type`                    | 시리즈의 유형 (`Anime`, `Daily`, 또는 `Standard`)                                              |
| `sonarr_release_episodecount`           | 릴리스에 포함된 에피소드 수                                                                   |
| `sonarr_release_seasonnumber`           | 릴리스의 시즌 번호                                                                            |
| `sonarr_release_episodenumbers`         | 쉼표로 구분된 에피소드 번호 목록                                                             |
| `sonarr_release_absoluteepisodenumbers` | 쉼표로 구분된 절대 에피소드 번호 목록                                                        |
| `sonarr_release_episodeairdates`        | 원본 네트워크의 방영일자 목록(쉼표로 구분됨)                                                  |
| `sonarr_release_episodeairdatesutc`     | UTC에서의 방영일자 목록(쉼표로 구분됨)                                                        |
| `sonarr_release_episodetitles`          | 에피소드 제목의 `|`로 구분된 목록                                                            |
| `sonarr_release_title`                  | 토렌트/NZB 제목                                                                               |
| `sonarr_release_indexer`                | 릴리스를 가져온 인덱서                                                                         |
| `sonarr_release_size`                   | 인덱서에서 보고된 릴리스의 크기                                                                 |
| `sonarr_release_quality`                | Sonarr에서 감지된 릴리스의 품질 이름                                                           |
| `sonarr_release_qualityversion`         | `1`은 기본값, `2`는 적합한 값, `3`+는 애니메이션 버전에 사용될 수 있습니다.                  |
| `sonarr_release_releasegroup`           | 릴리스 그룹 (알 수 없는 경우 비어 있음)                                                       |
| `sonarr_download_client`                | 다운로드 클라이언트                                                                           |
| `sonarr_download_id`                    | 토렌트/NZB 파일의 해시(다운로드 클라이언트에서 다운로드를 고유하게 식별하는 데 사용됨)         |

## 가져오기/업그레이드할 때

| 환경 변수                               | 세부 정보                                                                                     |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Download`                                                                                   |
| `sonarr_isupgrade`                      | 기존 파일이 업그레이드되면 `True`, 그렇지 않으면 `False`                                      |
| `sonarr_series_id`                      | 시리즈의 내부 ID                                                                             |
| `sonarr_series_title`                   | 시리즈의 제목                                                                                |
| `sonarr_series_path`                    | 시리즈의 전체 경로                                                                           |
| `sonarr_series_tvdbid`                  | 시리즈의 TVDB ID                                                                             |
| `sonarr_series_tvmazeid`                | 시리즈의 TVMaze ID                                                                           |
| `sonarr_series_imdbid`                  | 시리즈의 IMDB ID (알 수 없는 경우 비어 있음)                                                 |
| `sonarr_series_type`                    | 시리즈의 유형 (`Anime`, `Daily`, 또는 `Standard`)                                             |
| `sonarr_episodefile_id`                 | 에피소드 파일의 내부 ID                                                                      |
| `sonarr_episodefile_episodecount`       | 파일에 포함된 에피소드 수                                                                    |
| `sonarr_episodefile_relativepath`       | 시리즈 경로를 기준으로 한 에피소드 파일의 상대 경로                                          |
| `sonarr_episodefile_path`               | 에피소드 파일의 전체 경로                                                                    |
| `sonarr_episodefile_episodeids`         | 에피소드 파일의 내부 ID(들)                                                                 |
| `sonarr_episodefile_seasonnumber`       | 에피소드 파일의 시즌 번호                                                                    |
| `sonarr_episodefile_episodenumbers`     | 쉼표로 구분된 에피소드 번호 목록                                                             |
| `sonarr_episodefile_episodeairdates`    | 원본 네트워크의 방영 날짜 목록(쉼표로 구분됨)                                                |
| `sonarr_episodefile_episodeairdatesutc` | UTC 기준의 방영 날짜 목록(쉼표로 구분됨)                                                      |
| `sonarr_episodefile_episodetitles`      | 에피소드 제목의 `|`로 구분된 목록                                                           |
| `sonarr_episodefile_quality`            | Sonarr가 감지한 에피소드 파일의 품질 이름                                                     |
| `sonarr_episodefile_qualityversion`     | `1`은 기본값, `2`는 적합한 품질, `3`+는 애니메이션 버전에 사용될 수 있음                      |
| `sonarr_episodefile_releasegroup`       | 릴리스 그룹 (알 수 없는 경우 비어 있음)                                                      |
| `sonarr_episodefile_scenename`          | 원본 릴리스 이름 (알 수 없는 경우 비어 있음)                                                 |
| `sonarr_episodefile_sourcepath`         | 가져온 에피소드 파일의 전체 경로                                                              |
| `sonarr_episodefile_sourcefolder`       | 에피소드 파일이 가져온 폴더의 전체 경로                                                      |
| `sonarr_download_client`                | 다운로드 클라이언트                                                                         |
| `sonarr_download_id`                    | 토렌트/NZB 파일의 해시 (다운로드 클라이언트에서 다운로드를 고유하게 식별하는 데 사용됨)     |
| `sonarr_deletedrelativepaths`           | 이 파일을 가져오기 위해 삭제된 파일의 `|`로 구분된 목록                                      |
| `sonarr_deletedpaths`                   | 이 파일을 가져오기 위해 삭제된 파일의 전체 경로의 `|`로 구분된 목록                            |

## 이름 변경 시

| 환경 변수                  | 세부 정보                                          |
| ------------------------ | ---------------------------------------------------- |
| `sonarr_eventtype`       | `Rename`                                             |
| `sonarr_series_id`       | 시리즈의 내부 ID                                    |
| `sonarr_series_title`    | 시리즈의 제목                                       |
| `sonarr_series_path`     | 시리즈의 전체 경로                                  |
| `sonarr_series_tvdbid`   | 시리즈의 TVDB ID                                    |
| `sonarr_series_tvmazeid` | 시리즈의 TVMaze ID                                  |
| `sonarr_series_imdbid`   | 시리즈의 IMDB ID (알 수 없는 경우 비어 있음)         |
| `sonarr_series_type`     | 시리즈의 유형 (`Anime`, `Daily`, 또는 `Standard`)      |

## 에피소드 파일 삭제 시

| 환경 변수                               | 세부 정보                                                                      |
| --------------------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `EpisodeFileDelete`                                                              |
| `sonarr_series_id`                      | 시리즈의 내부 ID                                                                 |
| `sonarr_series_title`                   | 시리즈의 제목                                                                   |
| `sonarr_series_path`                    | 시리즈의 전체 경로                                                              |
| `sonarr_series_tvdbid`                  | 시리즈의 TVDB ID                                                                |
| `sonarr_series_tvmazeid`                | 시리즈의 TVMaze ID                                                              |
| `sonarr_series_imdbid`                  | 시리즈의 IMDB ID (알 수 없는 경우 비어 있음)                                   |
| `sonarr_series_type`                    | 시리즈의 유형 (`Anime`, `Daily`, 또는 `Standard`)                                |
| `sonarr_episodefile_id`                 | 에피소드 파일의 내부 ID                                                         |
| `sonarr_episodefile_episodecount`       | 파일에 포함된 에피소드 수                                                       |
| `sonarr_episodefile_relativepath`       | 시리즈 경로를 기준으로 한 에피소드 파일의 상대 경로                               |
| `sonarr_episodefile_path`               | 에피소드 파일의 전체 경로                                                       |
| `sonarr_episodefile_episodeids`         | 에피소드 파일의 내부 ID(들)                                                    |
| `sonarr_episodefile_seasonnumber`       | 에피소드 파일의 시즌 번호                                                       |
| `sonarr_episodefile_episodenumbers`     | 쉼표로 구분된 에피소드 번호 목록                                                |
| `sonarr_episodefile_episodeairdates`    | 원본 네트워크의 방영 날짜 목록(쉼표로 구분)                                    |
| `sonarr_episodefile_episodeairdatesutc` | UTC 기준의 방영 날짜 목록(쉼표로 구분)                                          |
| `sonarr_episodefile_episodetitles`      | 에피소드 제목의 `|`로 구분된 목록                                               |
| `sonarr_episodefile_quality`            | Sonarr가 감지한 에피소드 파일의 품질 이름                                        |
| `sonarr_episodefile_qualityversion`     | `1`은 기본값, `2`는 적절한 품질, `3`+는 애니메이션 버전에 사용될 수 있음           |
| `sonarr_episodefile_releasegroup`       | 릴리스 그룹(알 수 없는 경우 비어 있음)                                          |
| `sonarr_episodefile_scenename`          | 원본 릴리스 이름(알 수 없는 경우 비어 있음)                                     |

## 시리즈 삭제 시

| 환경 변수                | 세부 정보                               |
| ----------------------- | --------------------------------------- |
| `sonarr_eventtype`      | `SeriesDelete`                          |
| `sonarr_series_id`      | 시리즈의 내부 ID                         |
| `sonarr_series_title`   | 시리즈의 제목                           |
| `sonarr_series_path`    | 시리즈의 전체 경로                      |
| `sonarr_series_tvdbid`  | 시리즈의 TVDB ID                        |
| `sonarr_series_imdbid`  | 시리즈의 IMDB ID (알 수 없는 경우 비어 있음) |
| `sonarr_series_type`    | 시리즈의 유형 (`Anime`, `Daily`, 또는 `Standard`) |

## 건강 문제 발생 시

| 환경 변수                     | 세부 정보                                                         |
| ---------------------------- | ----------------------------------------------------------------- |
| `sonarr_eventtype`           | `HealthIssue`                                                     |
| `sonarr_health_issue_level`  | 건강 문제의 유형 (`Ok`, `Notice`, `Warning`, 또는 `Error`)          |
| `sonarr_health_issue_message`| 건강 문제의 메시지                                                |
| `sonarr_health_issue_type`   | 실패한 영역 및 건강 문제를 트리거한 유형                           |
| `sonarr_health_issue_wiki`   | 위키 URL (존재하지 않는 경우 비어 있음)                           |

## 애플리케이션 업데이트 시

| 환경 변수                      | 세부 정보                              |
| ----------------------------- | -------------------------------------- |
| `sonarr_eventtype`            | `ApplicationUpdate`                    |
| `sonarr_update_message`       | 업데이트에서의 메시지                   |
| `sonarr_update_newversion`    | Sonarr이 업데이트된 버전 (문자열)       |
| `sonarr_update_previousversion`| Sonarr이 업데이트되기 전 버전 (문자열) |

## 테스트 시

Sonarr에 스크립트를 추가하고 '테스트'를 클릭하면 스크립트가 다음 매개변수와 함께 호출됩니다. 스크립트는 지원되지 않는 이벤트 유형을 우아하게 무시할 수 있어야 합니다.

| 환경 변수              | 세부 정보 |
| --------------------- | --------- |
| `sonarr_eventtype`    | `Test`    |