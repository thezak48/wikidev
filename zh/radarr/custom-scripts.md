---
title: Radarr自定义脚本
description: 
published: true
date: 2022-05-02T03:36:09.625Z
tags: radarr, 需要关注, 自定义脚本
editor: markdown
dateCreated: 2021-06-16T15:55:44.765Z
---

如果您想要触发一个自定义脚本，您可以在这里找到更多详细信息。通过[连接设置](/radarr/settings#connections)，可以将脚本添加到Radarr中。

# 概述

Radarr可以在电影导入或重命名时执行自定义脚本。根据不同的操作，会提供不同的参数。参数通过环境变量传递给脚本。

## Radarr日志

请注意，以下内容仅适用于自定义脚本：

- 脚本的`stdout`输出将作为`Debug`记录
- 脚本的`stderr`输出将作为`Info`记录
- 脚本的触发将作为`Trace`记录

# 环境变量

## 在抓取时

| 环境变量                            | 详情                                                                                         |
| ----------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                  | `Grab`                                                                                       |
| `radarr_download_client`            | 下载客户端（如果未知则为空）                                                                 |
| `radarr_download_id`                | 种子/NZB文件的哈希（用于在下载客户端中唯一标识下载）                                          |
| `radarr_movie_id`                   | 电影的内部ID                                                                                 |
| `radarr_movie_imdbid`               | 电影的IMDb ID（如果未知则为空）                                                              |
| `radarr_movie_in_cinemas_date`      | 影院上映日期（如果未知则为空）                                                               |
| `radarr_movie_physical_release_date`| 实体发布日期（如果未知则为空）                                                               |
| `radarr_movie_title`                | 电影的标题                                                                                   |
| `radarr_movie_tmdbid`               | 电影的TMDb ID                                                                                |
| `radarr_movie_year`                 | 电影的发行年份                                                                               |
| `radarr_release_indexer`            | 从中抓取发布的索引器                                                                          |
| `radarr_release_quality`            | Radarr检测到的发布的质量名称                                                                  |
| `radarr_release_qualityversion`     | `1`是默认值，`2`用于正确版本，`3`+可用于动画版本                                             |
| `radarr_release_releasegroup`       | 发布组（如果未知则为空）                                                                     |
| `radarr_release_size`               | 发布的大小，由索引器报告                                                                     |
| `radarr_release_title`              | 种子/NZB的标题                                                                               |

## 在导入/升级时

| 环境变量                            | 详情                                                                                         |
| ----------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                  | `Download`                                                                                   |
| `radarr_download_id`                | 种子/NZB文件的哈希（用于在下载客户端中唯一标识下载）                                          |
| `radarr_download_client`            | 下载客户端                                                                                   |
| `radarr_isupgrade`                  | 当现有文件升级时为`True`，否则为`False`                                                      |
| `radarr_movie_id`                   | 电影的内部ID                                                                                 |
| `radarr_movie_imdbid`               | 电影的IMDb ID（如果未知则为空）                                                              |
| `radarr_movie_in_cinemas_date`      | 影院上映日期（如果未知则为空）                                                               |
| `radarr_movie_path`                 | 电影的完整路径                                                                               |
| `radarr_movie_physical_release_date`| 实体发布日期（如果未知则为空）                                                               |
| `radarr_movie_title`                | 电影的标题                                                                                   |
| `radarr_movie_tmdbid`               | 电影的TMDb ID                                                                                |
| `radarr_movie_year`                 | 电影的发行年份                                                                               |
| `radarr_moviefile_id`               | 电影文件的内部ID                                                                             |
| `radarr_moviefile_relativepath`     | 电影文件的路径，相对于电影路径                                                               |
| `radarr_moviefile_path`             | 电影文件的完整路径                                                                           |
| `radarr_moviefile_quality`          | Radarr检测到的发布的质量名称                                                                  |
| `radarr_moviefile_qualityversion`   | `1`是默认值，`2`用于正确版本，`3`+可用于动画版本                                             |
| `radarr_moviefile_releasegroup`     | 发布组（如果未知则为空）                                                                     |
| `radarr_moviefile_scenename`        | 原始发布名称（如果未知则为空）                                                               |
| `radarr_moviefile_sourcepath`       | 导入的电影文件的完整路径                                                                     |
| `radarr_moviefile_sourcefolder`     | 导入电影文件的文件夹的完整路径                                                               |
| `radarr_deletedrelativepaths`       | 以`|`分隔的已删除文件的列表，用于导入此文件                                                   |
| `radarr_deletedpaths`               | 以`|`分隔的已删除文件的完整路径列表，用于导入此文件                                             |

## 重命名时

| 环境变量                                 | 详情                                               |
| ---------------------------------------- | -------------------------------------------------- |
| `radarr_eventtype`                       | `Rename`                                           |
| `radarr_movie_id`                        | 电影的内部ID                                       |
| `radarr_movie_title`                     | 电影的标题                                         |
| `radarr_movie_year`                      | 电影的发行年份                                     |
| `radarr_movie_path`                      | 电影的完整路径                                     |
| `radarr_movie_imdbid`                    | 电影的IMDb ID（如果未知则为空）                     |
| `radarr_movie_tmdbid`                    | 电影的TMDb ID                                      |
| `radarr_movie_in_cinemas_date`           | 电影的院线上映日期（如果未知则为空）                 |
| `radarr_movie_physical_release_date`     | 电影的实体/网络发行日期（如果未知则为空）             |
| `radarr_moviefile_ids`                   | 逗号分隔的文件ID列表                               |
| `radarr_moviefile_relativepaths`         | 竖线分隔的相对路径列表                             |
| `radarr_moviefile_paths`                 | 竖线分隔的路径列表                                 |
| `radarr_moviefile_previousrelativepaths` | 竖线分隔的先前相对路径列表                         |
| `radarr_moviefile_previouspaths`         | 竖线分隔的先前路径列表                             |

## 关于健康检查

| 环境变量                      | 详情                                                        |
| ----------------------------- | ----------------------------------------------------------- |
| `radarr_eventtype`            | `HealthIssue`                                               |
| `radarr_health_issue_level`   | 健康问题的类型（`Ok`、`Notice`、`Warning`或`Error`）         |
| `radarr_health_issue_message` | 健康问题的消息                                              |
| `radarr_health_issue_type`    | 失败并触发健康问题的区域                                    |
| `radarr_health_issue_wiki`    | Wiki链接（如果不存在则为空）                                |

## 关于应用程序更新

| 环境变量                      | 详情                                     |
| ----------------------------- | ---------------------------------------- |
| `radarr_eventtype`            | `ApplicationUpdate`                      |
| `radarr_update_message`       | 更新的消息                               |
| `radarr_update_newversion`    | Radarr更新到的版本（字符串）              |
| `radarr_update_previousversion` | Radarr更新前的版本（字符串）             |

## 关于测试

将脚本添加到Radarr并点击“测试”时，将使用以下参数调用脚本。脚本应能够优雅地忽略任何不支持的事件类型。

| 环境变量               | 详情    |
| ---------------------- | ------- |
| `radarr_eventtype`     | `Test`  |