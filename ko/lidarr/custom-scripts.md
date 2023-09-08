---
title: Lidarr 사용자 정의 스크립트
description: 
published: true
date: 2023-04-09T23:23:38.475Z
tags: lidarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-11-24T19:22:09.331Z
---

사용자 정의 스크립트를 실행하려면 이 페이지에서 자세한 내용을 찾을 수 있습니다. 스크립트는 [연결 설정](/lidarr/settings#connections)을 통해 Lidarr에 추가됩니다.

# 개요

Lidarr는 에피소드가 새로 가져오거나 이름이 변경될 때 사용자 정의 스크립트를 실행할 수 있습니다. 동작에 따라 다른 매개변수가 제공됩니다. 매개변수는 환경 변수를 통해 스크립트로 전달됩니다.

사용자 정의 스크립트는 Lidarr가 실행 중인 사용자가 액세스할 수 있는 실행 가능한 파일일 수 있습니다.

## Lidarr 로그

다음은 사용자 정의 스크립트에 대해서만 로그가 기록됩니다.

- 스크립트의 `stdout` 출력은 `config/logs/Lidarr.debug.txt`에 `Debug`로 기록됩니다.
- 스크립트의 `stderr` 출력은 `config/logs/Lidarr.txt`에 `Info`로 기록됩니다.
- 스크립트의 트리거는 `config/logs/Lidarr.trace.txt`에 `Trace`로 기록됩니다.

# 환경 변수

환경 변수는 이벤트 유형에 따라 다릅니다. 아래 섹션에서 각 이벤트 유형에 대해 사용 가능한 변수를 보여줍니다.

> [아래 섹션은 정리, 구성 및 세부 정보를 개선해야 합니다. 여기에서 소스 코드를 확인하세요](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Grab

| 환경 변수                          | 세부 정보                                                           |
| ---------------------------------- | -------------------------------------------------------------------- |
| `lidarr_eventtype`                 | Grab                                                                 |
| `lidarr_artist_id`                 | `artist.Id`                                                          |
| `lidarr_artist_name`               | `artist.Metadata.Value.Name`                                         |
| `lidarr_artist_mbid`               | `artist.Metadata.Value.ForeignArtistId`                              |
| `lidarr_artist_type`               | `artist.Metadata.Value.Type`                                         |
| `lidarr_release_albumcount`        | `remoteAlbum.Albums.Count`                                           |
| `lidarr_release_albumreleasedates` | 앨범 출시 날짜의 쉼표로 구분된 목록                                 |
| `lidarr_release_albumtitles`       | 앨범 제목의 파이프로 구분된 목록                                     |
| `lidarr_release_albummbids`        | 앨범 외부 서비스 ID (예: MusicBrainz)의 파이프로 구분된 목록        |
| `lidarr_release_title`             | `remoteAlbum.Release.Title`                                          |
| `lidarr_release_indexer`           | `remoteAlbum.Release.Indexer`                                        |
| `lidarr_release_size`              | `remoteAlbum.Release.Size`                                           |
| `lidarr_release_quality`           | `remoteAlbum.ParsedAlbumInfo.Quality.Quality.Name`                   |
| `lidarr_release_qualityversion`    | `remoteAlbum.ParsedAlbumInfo.Quality.Revision.Version`               |
| `lidarr_release_releasegroup`      | `releaseGroup`                                                       |
| `lidarr_download_client`           | `message.DownloadClient`                                             |
| `lidarr_download_id`               | `message.DownloadId`                                                 |

## 가져오기 / 업그레이드

| 환경 변수               | 세부 정보                                  |
| -------------------------- | ---------------------------------------- |
| `lidarr_eventtype`         | AlbumDownload                            |
| `lidarr_artist_id`         | `artist.Id`                              |
| `lidarr_artist_name`       | `artist.Metadata.Value.Name`             |
| `lidarr_artist_path`       | `artist.Path`                            |
| `lidarr_artist_mbid`       | `artist.Metadata.Value.ForeignArtistId`  |
| `lidarr_artist_type`       | `artist.Metadata.Value.Type`             |
| `lidarr_album_id`          | `album.Id`                               |
| `lidarr_album_title`       | `album.Title`                            |
| `lidarr_album_mbid`        | `album.ForeignAlbumId`                   |
| `lidarr_albumrelease_mbid` | `release.ForeignReleaseId`               |
| `lidarr_album_releasedate` | `album.ReleaseDate`                      |
| `lidarr_download_client`   | `message.DownloadClient`                 |
| `lidarr_download_id`       | `message.DownloadId`                     |
| `lidarr_addedtrackpaths`   | 추가된 트랙 경로의 파이프로 구분된 목록 |
| `lidarr_deletedpaths`      | 삭제된 파일의 파이프로 구분된 목록     |

## 이름 바꾸기

| 환경 변수 | 세부 정보                                 |
| -------------------- | --------------------------------------- |
| `lidarr_eventtype`   | Rename                                  |
| `lidarr_artist_id`   | `artist.Id`                             |
| `lidarr_artist_name` | `artist.Metadata.Value.Name`            |
| `lidarr_artist_path` | `artist.Path`                           |
| `lidarr_artist_mbid` | `artist.Metadata.Value.ForeignArtistId` |
| `lidarr_artist_type` | `artist.Metadata.Value.Type`            |

## 트랙 재태그

| 환경 변수              | 세부 정보                                 |
| --------------------------------- | --------------------------------------- |
| `lidarr_eventtype`                | TrackRetag                              |
| `lidarr_artist_id`                | `artist.Id`                             |
| `lidarr_artist_name`              | `artist.Metadata.Value.Name`            |
| `lidarr_artist_path`              | `artist.Path`                           |
| `lidarr_artist_mbid`              | `artist.Metadata.Value.ForeignArtistId` |
| `lidarr_artist_type`              | `artist.Metadata.Value.Type`            |
| `lidarr_album_id`                 | `album.Id`                              |
| `lidarr_album_title`              | `album.Title`                           |
| `lidarr_album_mbid`               | `album.ForeignAlbumId`                  |
| `lidarr_albumrelease_mbid`        | `release.ForeignReleaseId`              |
| `lidarr_album_releasedate`        | `album.ReleaseDate`                     |
| `lidarr_trackfile_id`             | `trackFile.Id`                          |
| `lidarr_trackfile_trackcount`     | `trackFile.Tracks.Value.Count`          |
| `lidarr_trackfile_path`           | `trackFile.Path`                        |
| `lidarr_trackfile_tracknumbers`   | 쉼표로 구분된 트랙 번호의 목록   |
| `lidarr_trackfile_tracktitles`    | 파이프로 구분된 트랙 제목의 목록     |
| `lidarr_trackfile_quality`        | `trackFile.Quality.Quality.Name`        |
| `lidarr_trackfile_qualityversion` | `trackFile.Quality.Revision.Version`    |
| `lidarr_trackfile_releasegroup`   | `trackFile.ReleaseGroup`                |
| `lidarr_trackfile_scenename`      | `trackFile.SceneName`                   |
| `lidarr_tags_diff`                | `message.Diff.ToJson()`                 |
| `lidarr_tags_scrubbed`            | `message.Scrubbed`                      |

## 건강 문제

| 환경 변수          | 세부 정보                                 |
| ----------------------------- | --------------------------------------- |
| `lidarr_eventtype`            | HealthIssue                             |
| `lidarr_health_issue_level`   | `nameof(healthCheck.Type)`              |
| `lidarr_health_issue_message` | `healthCheck.Message`                   |
| `lidarr_health_issue_type`    | `healthCheck.Source.Name`               |
| `lidarr_health_issue_wiki`    | 건강 문제 도움말 페이지의 위키 URL |

## 테스트 중

Lidarr에 스크립트를 추가하고 '테스트'를 클릭하면 다음 매개변수로 스크립트가 호출됩니다. 스크립트는 지원되지 않는 이벤트 유형을 우아하게 무시할 수 있어야 합니다.

| 환경 변수 | 세부 정보 |
| ----------- | --------- |
| `lidarr_eventtype` | 테스트 |