---
title: Lidarr カスタムスクリプト
description: 
published: true
date: 2023-04-09T23:23:38.475Z
tags: lidarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-11-24T19:22:09.331Z
---

カスタムスクリプトをトリガーする場合は、このページで詳細を確認できます。スクリプトは [接続設定](/lidarr/settings#connections) を介して Lidarr に追加されます。

# 概要

Lidarr は、エピソードが新しくインポートされたり名前が変更されたりしたときにカスタムスクリプトを実行できます。アクションによっては、異なるパラメータが提供されます。パラメータは環境変数を介してスクリプトに渡されます。

カスタムスクリプトは、Lidarr が実行されているユーザーによってアクセス可能な実行可能ファイルです。

## Lidarr ログ

以下の内容は、カスタムスクリプトの場合のみログに記録されます。

- スクリプトの `stdout` 出力は、`config/logs/Lidarr.debug.txt` に `Debug` としてログに記録されます。
- スクリプトの `stderr` 出力は、`config/logs/Lidarr.txt` に `Info` としてログに記録されます。
- スクリプトのトリガーは、`config/logs/Lidarr.trace.txt` に `Trace` としてログに記録されます。

# 環境変数

環境変数はイベントの種類によって異なります。以下のセクションでは、各イベントに対して利用可能な変数を示しています。

> [以下のセクションは整理、整頓、詳細の向上が必要です。ソースコードはこちらで確認できます](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Grab

| 環境変数                          | 詳細                                                                |
| --------------------------------- | ------------------------------------------------------------------- |
| `lidarr_eventtype`                | Grab                                                                |
| `lidarr_artist_id`                | `artist.Id`                                                         |
| `lidarr_artist_name`              | `artist.Metadata.Value.Name`                                        |
| `lidarr_artist_mbid`              | `artist.Metadata.Value.ForeignArtistId`                             |
| `lidarr_artist_type`              | `artist.Metadata.Value.Type`                                        |
| `lidarr_release_albumcount`       | `remoteAlbum.Albums.Count`                                          |
| `lidarr_release_albumreleasedates`| アルバムのリリース日のカンマ区切りのリスト                           |
| `lidarr_release_albumtitles`      | アルバムタイトルのパイプ区切りのリスト                               |
| `lidarr_release_albummbids`       | アルバムの外部サービス ID (例: MusicBrainz) のパイプ区切りのリスト   |
| `lidarr_release_title`            | `remoteAlbum.Release.Title`                                         |
| `lidarr_release_indexer`          | `remoteAlbum.Release.Indexer`                                       |
| `lidarr_release_size`             | `remoteAlbum.Release.Size`                                          |
| `lidarr_release_quality`          | `remoteAlbum.ParsedAlbumInfo.Quality.Quality.Name`                  |
| `lidarr_release_qualityversion`   | `remoteAlbum.ParsedAlbumInfo.Quality.Revision.Version`              |
| `lidarr_release_releasegroup`     | `releaseGroup`                                                      |
| `lidarr_download_client`          | `message.DownloadClient`                                            |
| `lidarr_download_id`              | `message.DownloadId`                                                |

## On Import / On Upgrade

| 環境変数                  | 詳細                                      |
| ------------------------- | ---------------------------------------- |
| `lidarr_eventtype`        | AlbumDownload                            |
| `lidarr_artist_id`        | `artist.Id`                              |
| `lidarr_artist_name`      | `artist.Metadata.Value.Name`             |
| `lidarr_artist_path`      | `artist.Path`                            |
| `lidarr_artist_mbid`      | `artist.Metadata.Value.ForeignArtistId`  |
| `lidarr_artist_type`      | `artist.Metadata.Value.Type`             |
| `lidarr_album_id`         | `album.Id`                               |
| `lidarr_album_title`      | `album.Title`                            |
| `lidarr_album_mbid`       | `album.ForeignAlbumId`                   |
| `lidarr_albumrelease_mbid`| `release.ForeignReleaseId`               |
| `lidarr_album_releasedate`| `album.ReleaseDate`                      |
| `lidarr_download_client`  | `message.DownloadClient`                 |
| `lidarr_download_id`      | `message.DownloadId`                     |
| `lidarr_addedtrackpaths`  | 追加されたトラックのパイプ区切りのリスト |
| `lidarr_deletedpaths`     | 削除されたファイルのパイプ区切りのリスト |

## Rename

| 環境変数                | 詳細                                     |
| ----------------------- | ---------------------------------------- |
| `lidarr_eventtype`      | Rename                                   |
| `lidarr_artist_id`      | `artist.Id`                              |
| `lidarr_artist_name`    | `artist.Metadata.Value.Name`             |
| `lidarr_artist_path`    | `artist.Path`                            |
| `lidarr_artist_mbid`    | `artist.Metadata.Value.ForeignArtistId`  |
| `lidarr_artist_type`    | `artist.Metadata.Value.Type`             |

## Track Retag

| 環境変数                         | 詳細                                     |
| -------------------------------- | ---------------------------------------- |
| `lidarr_eventtype`               | TrackRetag                               |
| `lidarr_artist_id`               | `artist.Id`                              |
| `lidarr_artist_name`             | `artist.Metadata.Value.Name`             |
| `lidarr_artist_path`             | `artist.Path`                            |
| `lidarr_artist_mbid`             | `artist.Metadata.Value.ForeignArtistId`  |
| `lidarr_artist_type`             | `artist.Metadata.Value.Type`             |
| `lidarr_album_id`                | `album.Id`                               |
| `lidarr_album_title`             | `album.Title`                            |
| `lidarr_album_mbid`              | `album.ForeignAlbumId`                   |
| `lidarr_albumrelease_mbid`       | `release.ForeignReleaseId`               |
| `lidarr_album_releasedate`       | `album.ReleaseDate`                      |
| `lidarr_trackfile_id`            | `trackFile.Id`                           |
| `lidarr_trackfile_trackcount`    | `trackFile.Tracks.Value.Count`           |
| `lidarr_trackfile_path`          | `trackFile.Path`                         |
| `lidarr_trackfile_tracknumbers`  | トラック番号のカンマ区切りのリスト        |
| `lidarr_trackfile_tracktitles`   | トラックタイトルのパイプ区切りのリスト    |
| `lidarr_trackfile_quality`       | `trackFile.Quality.Quality.Name`         |
| `lidarr_trackfile_qualityversion`| `trackFile.Quality.Revision.Version`     |
| `lidarr_trackfile_releasegroup`  | `trackFile.ReleaseGroup`                 |
| `lidarr_trackfile_scenename`     | `trackFile.SceneName`                    |
| `lidarr_tags_diff`               | `message.Diff.ToJson()`                  |
| `lidarr_tags_scrubbed`           | `message.Scrubbed`                       |

## Health Issue

| 環境変数                      | 詳細                                     |
| ----------------------------- | ---------------------------------------- |
| `lidarr_eventtype`            | HealthIssue                              |
| `lidarr_health_issue_level`   | `nameof(healthCheck.Type)`               |
| `lidarr_health_issue_message` | `healthCheck.Message`                    |
| `lidarr_health_issue_type`    | `healthCheck.Source.Name`                |
| `lidarr_health_issue_wiki`    | ヘルスイシューのヘルプページの Wiki URL   |

## On Test

Lidarr にスクリプトを追加し、「テスト」をクリックすると、以下のパラメータでスクリプトが呼び出されます。スクリプトは、サポートされていないイベントタイプを優雅に無視できるようにする必要があります。

| 環境変数 | 詳細 |
| ---------- | ---- |
| `lidarr_eventtype` | テスト |