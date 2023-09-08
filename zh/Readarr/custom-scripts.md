---
title: Readarr自定义脚本
description: 
published: true
date: 2022-05-02T03:36:38.595Z
tags: readarr, 需要关注, 自定义脚本
editor: markdown
dateCreated: 2021-06-23T06:41:11.792Z
---

如果您想要触发一个自定义脚本，您可以在这里找到更多详细信息。通过[连接设置](/readarr/settings#connections)，可以将脚本添加到Readarr中。

# 概述

当图书被新导入或重命名时，Readarr可以执行自定义脚本。根据不同的操作，会提供不同的参数。参数通过环境变量传递给脚本。

## Readarr日志

请注意，以下内容仅适用于自定义脚本的日志记录：

- 脚本的`stdout`输出将作为`Debug`记录
- 脚本的`stderr`输出将作为`Info`记录
- 脚本的触发将作为`Trace`记录

# 环境变量

## 在抓取时

| 环境变量                          | 详情                                           |
| --------------------------------- | ---------------------------------------------- |
| `readarr_eventtype`               | `Grab`                                         |
| `readarr_author_id`               | 作者的内部ID                                    |
| `readarr_author_name`             | 作者的名称                                     |
| `readarr_author_grid`             | 作者的Goodreads ID                              |
| `readarr_release_bookcount`       | 发布中的图书数量                               |
| `readarr_release_bookreleasedates`| 图书的发布日期                                 |
| `readarr_release_booktitles`      | 发布中的图书标题                               |
| `readarr_release_bookids`         | 图书的ID                                       |
| `readarr_release_grids`           | 发布中的图书的Goodreads ID                      |
| `readarr_release_title`           | 图书的标题                                     |
| `readarr_release_indexer`         | 从中抓取发布的索引器                           |
| `readarr_release_size`            | 发布的大小                                     |
| `readarr_release_quality`         | 发布的质量                                     |
| `readarr_release_qualityVersion`  | 发布的质量版本                                 |
| `readarr_release_releasegroup`    | 发布的发布组（如果未知则为空）                   |
| `readarr_download_client`         | 用于下载发布的下载客户端                        |
| `readarr_download_id`             | 下载的ID                                       |

## 在导入/升级时

| 环境变量                  | 详情                                           |
| ------------------------- | ---------------------------------------------- |
| `readarr_eventtype`       | `Download`                                     |
| `readarr_author_id`       | 作者的内部ID                                    |
| `readarr_author_name`     | 作者的名称                                     |
| `readarr_author_path`     | 作者的路径                                     |
| `readarr_author_grid`     | 作者的Goodreads ID                              |
| `readarr_book_id`         | 图书的ID                                       |
| `readarr_book_title`      | 图书的标题                                     |
| `readarr_book_grid`       | 图书的Goodreads ID                              |
| `readarr_book_releasedate`| 图书的发布日期                                 |
| `readarr_download_client` | 用于下载发布的下载客户端                        |
| `readarr_download_id`     | 下载的ID                                       |

## 在重命名时

| 环境变量             | 详情                                           |
| -------------------- | ---------------------------------------------- |
| `readarr_eventtype`  | `Rename`                                       |
| `readarr_author_id`  | 作者的内部ID                                    |
| `readarr_author_name`| 作者的名称                                     |
| `readarr_author_path`| 作者的路径                                     |
| `readarr_author_grid`| 作者的Goodreads ID                              |

## 在图书重新标记时

| 环境变量                          | 详情                                           |
| --------------------------------- | ---------------------------------------------- |
| `readarr_eventtype`               | `TrackRetag`                                   |
| `readarr_author_id`               | 作者的内部ID                                    |
| `readarr_author_name`             | 作者的名称                                     |
| `readarr_author_path`             | 作者的路径                                     |
| `readarr_author_grid`             | 作者的Goodreads ID                              |
| `readarr_book_id`                 | 图书的ID                                       |
| `readarr_book_title`              | 图书的标题                                     |
| `readarr_book_grid`               | 图书的Goodreads ID                              |
| `readarr_book_releasedate`        | 图书的发布日期                                 |
| `readarr_bookfile_id`             | 图书文件的ID                                   |
| `readarr_bookfile_path`           | 图书的路径                                     |
| `readarr_bookfile_quality`        | 图书文件的质量                                 |
| `readarr_bookfile_qualityversion` | 图书文件的质量版本                             |
| `readarr_bookfile_releasegroup`   | 图书的发布组                                   |
| `readarr_bookfile_scenename`      | 图书的场景名称                                 |
| `readarr_tags_diff`               | 标签的差异                                     |
| `readarr_tags_scrubbed`           | 清理后的标签                                   |

## 在健康问题上

| 环境变量                        | 详情                                                       |
| ------------------------------- | ---------------------------------------------------------- |
| `readarr_eventtype`             | `HealthIssue`                                              |
| `readarr_health_issue_level`    | 健康问题的类型（`Ok`、`Notice`、`Warning`或`Error`）        |
| `readarr_health_issue_message`  | 健康问题的消息                                             |
| `readarr_health_issue_type`     | 失败并触发健康问题的区域                                   |
| `readarr_health_issue_wiki`     | Wiki的URL（如果不存在则为空）                              |

## 在测试时

当将脚本添加到Readarr并点击“测试”时，将使用以下参数调用脚本。脚本应该能够优雅地忽略任何不支持的事件类型。

| 环境变量             | 详情    |
| -------------------- | ------- |
| `readarr_eventtype`  | `Test`  |