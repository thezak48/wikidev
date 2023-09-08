---
title: Lidarr自定义脚本
description: 
published: true
date: 2023-04-09T23:23:38.475Z
tags: lidarr, 需要关注, 自定义脚本
editor: markdown
dateCreated: 2021-11-24T19:22:09.331Z
---

如果您想要触发一个自定义脚本，您可以在此页面找到更多详细信息。通过[Lidarr连接设置](/lidarr/settings#connections)，可以将脚本添加到Lidarr中。

# 概述

当导入或重命名一个剧集时，Lidarr可以执行一个自定义脚本。根据不同的操作，会提供不同的参数。参数通过环境变量传递给脚本。

自定义脚本可以是用户Lidarr运行的任何可执行文件。

## Lidarr日志

请注意，以下内容仅适用于自定义脚本：

- 脚本的`stdout`输出将记录在`config/logs/Lidarr.debug.txt`中的`Debug`日志中
- 脚本的`stderr`输出将记录在`config/logs/Lidarr.txt`中的`Info`日志中
- 脚本的触发将记录在`config/logs/Lidarr.trace.txt`中的`Trace`日志中

# 环境变量

环境变量根据事件类型而异。下面的部分指示了每个事件类型可用的变量。

> [下面的部分需要整理、组织和增强细节。在此处查看源代码](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## 抓取

| 环境变量                          | 详情                                                           |
| --------------------------------- | -------------------------------------------------------------- |
| `lidarr_eventtype`                | 抓取                                                           |
| `lidarr_artist_id`                | `artist.Id`                                                    |
| `lidarr_artist_name`              | `artist.Metadata.Value.Name`                                   |
| `lidarr_artist_mbid`              | `artist.Metadata.Value.ForeignArtistId`                        |
| `lidarr_artist_type`              | `artist.Metadata.Value.Type`                                   |
| `lidarr_release_albumcount`       | `remoteAlbum.Albums.Count`                                     |
| `lidarr_release_albumreleasedates`| 以逗号分隔的专辑发布日期列表                                   |
| `lidarr_release_albumtitles`      | 以竖线分隔的专辑标题列表                                       |
| `lidarr_release_albummbids`       | 以竖线分隔的专辑外部服务ID列表（例如MusicBrainz）               |
| `lidarr_release_title`            | `remoteAlbum.Release.Title`                                    |
| `lidarr_release_indexer`          | `remoteAlbum.Release.Indexer`                                  |
| `lidarr_release_size`             | `remoteAlbum.Release.Size`                                     |
| `lidarr_release_quality`          | `remoteAlbum.ParsedAlbumInfo.Quality.Quality.Name`              |
| `lidarr_release_qualityversion`   | `remoteAlbum.ParsedAlbumInfo.Quality.Revision.Version`          |
| `lidarr_release_releasegroup`     | `releaseGroup`                                                  |
| `lidarr_download_client`          | `message.DownloadClient`                                        |
| `lidarr_download_id`              | `message.DownloadId`                                            |

## 导入/升级

| 环境变量                    | 详情                                   |
| -------------------------- | -------------------------------------- |
| `lidarr_eventtype`         | AlbumDownload                          |
| `lidarr_artist_id`         | `artist.Id`                            |
| `lidarr_artist_name`       | `artist.Metadata.Value.Name`           |
| `lidarr_artist_path`       | `artist.Path`                          |
| `lidarr_artist_mbid`       | `artist.Metadata.Value.ForeignArtistId`|
| `lidarr_artist_type`       | `artist.Metadata.Value.Type`           |
| `lidarr_album_id`          | `album.Id`                             |
| `lidarr_album_title`       | `album.Title`                          |
| `lidarr_album_mbid`        | `album.ForeignAlbumId`                 |
| `lidarr_albumrelease_mbid` | `release.ForeignReleaseId`             |
| `lidarr_album_releasedate` | `album.ReleaseDate`                    |
| `lidarr_download_client`   | `message.DownloadClient`               |
| `lidarr_download_id`       | `message.DownloadId`                   |
| `lidarr_addedtrackpaths`   | 以竖线分隔的已添加的曲目路径列表       |
| `lidarr_deletedpaths`      | 以竖线分隔的已删除的文件列表           |

## 重命名

| 环境变量              | 详情                                   |
| -------------------- | -------------------------------------- |
| `lidarr_eventtype`   | 重命名                                 |
| `lidarr_artist_id`   | `artist.Id`                            |
| `lidarr_artist_name` | `artist.Metadata.Value.Name`           |
| `lidarr_artist_path` | `artist.Path`                          |
| `lidarr_artist_mbid` | `artist.Metadata.Value.ForeignArtistId`|
| `lidarr_artist_type` | `artist.Metadata.Value.Type`           |

## 曲目重新标记

| 环境变量                          | 详情                                   |
| --------------------------------- | -------------------------------------- |
| `lidarr_eventtype`                | TrackRetag                             |
| `lidarr_artist_id`                | `artist.Id`                            |
| `lidarr_artist_name`              | `artist.Metadata.Value.Name`           |
| `lidarr_artist_path`              | `artist.Path`                          |
| `lidarr_artist_mbid`              | `artist.Metadata.Value.ForeignArtistId`|
| `lidarr_artist_type`              | `artist.Metadata.Value.Type`           |
| `lidarr_album_id`                 | `album.Id`                             |
| `lidarr_album_title`              | `album.Title`                          |
| `lidarr_album_mbid`               | `album.ForeignAlbumId`                 |
| `lidarr_albumrelease_mbid`        | `release.ForeignReleaseId`             |
| `lidarr_album_releasedate`        | `album.ReleaseDate`                    |
| `lidarr_trackfile_id`             | `trackFile.Id`                         |
| `lidarr_trackfile_trackcount`     | `trackFile.Tracks.Value.Count`         |
| `lidarr_trackfile_path`           | `trackFile.Path`                       |
| `lidarr_trackfile_tracknumbers`   | 以逗号分隔的曲目编号列表               |
| `lidarr_trackfile_tracktitles`    | 以竖线分隔的曲目标题列表               |
| `lidarr_trackfile_quality`        | `trackFile.Quality.Quality.Name`       |
| `lidarr_trackfile_qualityversion` | `trackFile.Quality.Revision.Version`   |
| `lidarr_trackfile_releasegroup`   | `trackFile.ReleaseGroup`               |
| `lidarr_trackfile_scenename`      | `trackFile.SceneName`                  |
| `lidarr_tags_diff`                | `message.Diff.ToJson()`                |
| `lidarr_tags_scrubbed`            | `message.Scrubbed`                     |

## 健康问题

| 环境变量                    | 详情                                   |
| --------------------------- | -------------------------------------- |
| `lidarr_eventtype`          | HealthIssue                            |
| `lidarr_health_issue_level` | `nameof(healthCheck.Type)`              |
| `lidarr_health_issue_message`| `healthCheck.Message`                   |
| `lidarr_health_issue_type`   | `healthCheck.Source.Name`               |
| `lidarr_health_issue_wiki`   | 健康问题帮助页面的Wiki URL              |

## 测试

当将脚本添加到Lidarr并点击“测试”时，将使用以下参数调用脚本。脚本应能够优雅地忽略任何不支持的事件类型。

| 环境变量            | 详情     |
| ------------------- | -------- |
| `lidarr_eventtype`  | 测试     |