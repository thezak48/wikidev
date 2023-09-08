---
title: Sonarr自定义脚本
description: 
published: true
date: 2022-06-13T15:52:03.477Z
tags: sonarr, 需要关注, 自定义脚本
editor: markdown
dateCreated: 2021-06-16T15:55:53.999Z
---

如果您想要触发一个自定义脚本，您可以在这里找到更多详细信息。通过[连接设置](/sonarr/settings#connections)，可以将脚本添加到Sonarr中。

# 概述

Sonarr可以在新导入或重命名剧集时执行自定义脚本。根据不同的操作，会提供不同的参数。参数通过环境变量传递给脚本。

## Sonarr日志

请注意，以下内容仅适用于自定义脚本：

- 脚本的`stdout`输出将作为`Debug`记录
- 脚本的`stderr`输出将作为`Info`记录
- 脚本的触发将在`Trace`中记录

# 环境变量

## 在抓取时

| 环境变量                              | 详情                                                                                      |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Grab`                                                                                       |
| `sonarr_series_id`                      | 系列的内部ID                                                                    |
| `sonarr_series_title`                   | 系列的标题                                                                          |
| `sonarr_series_tvdbid`                  | 系列的TVDB ID                                                                       |
| `sonarr_series_tvmazeid`                | 系列的TVMaze ID                                                                     |
| `sonarr_series_imdbid`                  | 系列的IMDB ID（如果未知则为空）                                                    |
| `sonarr_series_type`                    | 系列的类型（`Anime`，`Daily`或`Standard`）                                         |
| `sonarr_release_episodecount`           | 发布中的剧集数                                                            |
| `sonarr_release_seasonnumber`           | 发布中的季数                                                                   |
| `sonarr_release_episodenumbers`         | 逗号分隔的剧集编号列表                                                      |
| `sonarr_release_absoluteepisodenumbers` | 逗号分隔的绝对剧集编号列表                                             |
| `sonarr_release_episodeairdates`        | 逗号分隔的原始网络上的播出日期列表                                      |
| `sonarr_release_episodeairdatesutc`     | 逗号分隔的UTC时间的播出日期列表                                                     |
| `sonarr_release_episodetitles`          | 以`\|`分隔的剧集标题列表                                                        |
| `sonarr_release_title`                  | 种子/NZB的标题                                                                            |
| `sonarr_release_indexer`                | 抓取发布的索引器                                                   |
| `sonarr_release_size`                   | 发布的大小，由索引器报告                                              |
| `sonarr_release_quality`                | Sonarr检测到的发布的质量名称                                           |
| `sonarr_release_qualityversion`         | `1`是默认值，`2`用于正确版本，`3`+可用于动画版本             |
| `sonarr_release_releasegroup`           | 发布组（如果未知则为空）                                                             |
| `sonarr_download_client`                | 下载客户端                                                                              |
| `sonarr_download_id`                    | 种子/NZB文件的哈希值（用于在下载客户端中唯一标识下载） |

## 在导入/升级时

| 环境变量                               | 详情                                                                                       |
| -------------------------------------- | ------------------------------------------------------------------------------------------ |
| `sonarr_eventtype`                     | `Download`                                                                                  |
| `sonarr_isupgrade`                     | 当现有文件升级时为`True`，否则为`False`                                                      |
| `sonarr_series_id`                     | 系列的内部ID                                                                                |
| `sonarr_series_title`                  | 系列的标题                                                                                  |
| `sonarr_series_path`                   | 系列的完整路径                                                                              |
| `sonarr_series_tvdbid`                 | 系列的TVDB ID                                                                               |
| `sonarr_series_tvmazeid`               | 系列的TVMaze ID                                                                             |
| `sonarr_series_imdbid`                 | 系列的IMDB ID（如果未知则为空）                                                              |
| `sonarr_series_type`                   | 系列的类型（`Anime`、`Daily`或`Standard`）                                                   |
| `sonarr_episodefile_id`                | 剧集文件的内部ID                                                                            |
| `sonarr_episodefile_episodecount`      | 文件中的剧集数                                                                              |
| `sonarr_episodefile_relativepath`      | 剧集文件的路径，相对于系列路径                                                              |
| `sonarr_episodefile_path`              | 剧集文件的完整路径                                                                          |
| `sonarr_episodefile_episodeids`        | 剧集文件的内部ID（多个ID以逗号分隔）                                                         |
| `sonarr_episodefile_seasonnumber`      | 剧集文件的季数                                                                              |
| `sonarr_episodefile_episodenumbers`    | 剧集文件的剧集号（以逗号分隔的列表）                                                         |
| `sonarr_episodefile_episodeairdates`   | 剧集文件的原始网络上的播出日期（以逗号分隔的列表）                                           |
| `sonarr_episodefile_episodeairdatesutc`| 剧集文件的UTC时间上的播出日期（以逗号分隔的列表）                                             |
| `sonarr_episodefile_episodetitles`     | 剧集文件的剧集标题（以`\|`分隔的列表）                                                       |
| `sonarr_episodefile_quality`           | 剧集文件的质量名称，由Sonarr检测到                                                          |
| `sonarr_episodefile_qualityversion`    | `1`是默认值，`2`用于proper版本，`3`+可用于动画版本                                            |
| `sonarr_episodefile_releasegroup`      | 发布组（如果未知则为空）                                                                    |
| `sonarr_episodefile_scenename`         | 原始发布名称（如果未知则为空）                                                              |
| `sonarr_episodefile_sourcepath`        | 导入的剧集文件的完整路径                                                                    |
| `sonarr_episodefile_sourcefolder`      | 导入剧集文件的文件夹的完整路径                                                              |
| `sonarr_download_client`               | 下载客户端                                                                                  |
| `sonarr_download_id`                   | 种子/NZB文件的哈希值（用于在下载客户端中唯一标识下载）                                        |
| `sonarr_deletedrelativepaths`          | 导入此文件时删除的文件的路径（以`\|`分隔的列表）                                             |
| `sonarr_deletedpaths`                  | 导入此文件时删除的文件的完整路径（以`\|`分隔的列表）                                         |

## 重命名时

| 环境变量                          | 详情                                               |
| --------------------------------- | -------------------------------------------------- |
| `sonarr_eventtype`                | `Rename`                                           |
| `sonarr_series_id`                | 系列的内部ID                                       |
| `sonarr_series_title`             | 系列的标题                                         |
| `sonarr_series_path`              | 系列的完整路径                                     |
| `sonarr_series_tvdbid`            | 系列的TVDB ID                                      |
| `sonarr_series_tvmazeid`          | 系列的TVMaze ID                                    |
| `sonarr_series_imdbid`            | 系列的IMDB ID（如果未知则为空）                     |
| `sonarr_series_type`              | 系列的类型（`Anime`、`Daily`或`Standard`）          |

## 删除剧集文件时

| 环境变量                               | 详情                                                                          |
| --------------------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `EpisodeFileDelete`                                                              |
| `sonarr_series_id`                      | 系列的内部ID                                                                    |
| `sonarr_series_title`                   | 系列的标题                                                                      |
| `sonarr_series_path`                    | 系列的完整路径                                                                  |
| `sonarr_series_tvdbid`                  | 系列的TVDB ID                                                                   |
| `sonarr_series_tvmazeid`                | 系列的TVMaze ID                                                                 |
| `sonarr_series_imdbid`                  | 系列的IMDB ID（如果未知则为空）                                                  |
| `sonarr_series_type`                    | 系列的类型（`Anime`、`Daily`或`Standard`）                                       |
| `sonarr_episodefile_id`                 | 剧集文件的内部ID                                                                |
| `sonarr_episodefile_episodecount`       | 文件中的剧集数量                                                                |
| `sonarr_episodefile_relativepath`       | 剧集文件的路径，相对于系列路径                                                  |
| `sonarr_episodefile_path`               | 剧集文件的完整路径                                                              |
| `sonarr_episodefile_episodeids`         | 剧集文件的内部ID（多个ID用逗号分隔）                                             |
| `sonarr_episodefile_seasonnumber`       | 剧集文件的季数                                                                  |
| `sonarr_episodefile_episodenumbers`     | 剧集文件的剧集编号（用逗号分隔的列表）                                           |
| `sonarr_episodefile_episodeairdates`    | 剧集文件的原始网络上的播出日期（用逗号分隔的列表）                               |
| `sonarr_episodefile_episodeairdatesutc` | 剧集文件的UTC时间上的播出日期（用逗号分隔的列表）                                |
| `sonarr_episodefile_episodetitles`      | 剧集文件的剧集标题（用`\|`分隔的列表）                                           |
| `sonarr_episodefile_quality`            | 剧集文件的质量名称，由Sonarr检测到                                               |
| `sonarr_episodefile_qualityversion`     | `1`是默认值，`2`用于proper版本，`3`+可用于动画版本                                 |
| `sonarr_episodefile_releasegroup`       | 发布组（如果未知则为空）                                                        |
| `sonarr_episodefile_scenename`          | 原始发布名称（如果未知则为空）                                                  |

## 在删除系列时

| 环境变量                | 详情                                                                  |
| ----------------------- | --------------------------------------------------------------------- |
| `sonarr_eventtype`      | `SeriesDelete`                                                        |
| `sonarr_series_id`      | 系列的内部ID                                                          |
| `sonarr_series_title`   | 系列的标题                                                            |
| `sonarr_series_path`    | 系列的完整路径                                                        |
| `sonarr_series_tvdbid`  | 系列的TVDB ID                                                         |
| `sonarr_series_imdbid`  | 系列的IMDB ID（如果未知则为空）                                        |
| `sonarr_series_type`    | 系列的类型（`Anime`、`Daily`或`Standard`）                             |
| `sonarr_series_deletedfiles` | 当选择了删除文件选项时为`True`，否则为`False`                          |

## 在健康问题上

| 环境变量                   | 详情                                                      |
| -------------------------- | --------------------------------------------------------- |
| `sonarr_eventtype`         | `HealthIssue`                                             |
| `sonarr_health_issue_level` | 健康问题的类型（`Ok`、`Notice`、`Warning`或`Error`）       |
| `sonarr_health_issue_message` | 健康问题的消息                                           |
| `sonarr_health_issue_type` | 失败并触发健康问题的区域                                   |
| `sonarr_health_issue_wiki` | Wiki URL（如果不存在则为空）                              |

## 在应用程序更新时

| 环境变量                      | 详情                               |
| ----------------------------- | ---------------------------------- |
| `sonarr_eventtype`            | `ApplicationUpdate`                |
| `sonarr_update_message`       | 更新的消息                         |
| `sonarr_update_newversion`    | Sonarr更新到的版本（字符串）       |
| `sonarr_update_previousversion` | Sonarr更新自的版本（字符串）       |

## 在测试时

将脚本添加到Sonarr并点击“测试”时，将使用以下参数调用脚本。脚本应能够优雅地忽略任何不支持的事件类型。

| 环境变量             | 详情   |
| -------------------- | ------ |
| `sonarr_eventtype`   | `Test` |