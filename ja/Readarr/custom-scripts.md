---
title: Readarrカスタムスクリプト
description: 
published: true
date: 2022-05-02T03:36:38.595Z
tags: readarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-23T06:41:11.792Z
---

カスタムスクリプトをトリガーしたい場合は、詳細はこちらをご覧ください。スクリプトは、[接続設定](/readarr/settings#connections)を介してReadarrに追加されます。

# 概要

Readarrは、本が新しくインポートされたり名前が変更されたりしたときにカスタムスクリプトを実行できます。アクションによっては、異なるパラメータが提供されます。パラメータは環境変数を介してスクリプトに渡されます。

## Readarrログ

以下は、カスタムスクリプトの場合にのみログに記録されます。

- スクリプトの`stdout`出力は`Debug`としてログに記録されます。
- スクリプトの`stderr`出力は`Info`としてログに記録されます。
- スクリプトのトリガーは`Trace`としてログに記録されます。

# 環境変数

## Grab時

| 環境変数                          | 詳細                                             |
| --------------------------------- | ------------------------------------------------ |
| `readarr_eventtype`               | `Grab`                                           |
| `readarr_author_id`               | 著者の内部ID                                     |
| `readarr_author_name`             | 著者の名前                                       |
| `readarr_author_grid`             | 著者のGoodreads ID                               |
| `readarr_release_bookcount`       | リリースの中の本の数                             |
| `readarr_release_bookreleasedates`| 本のリリース日                                   |
| `readarr_release_booktitles`      | リリースの本のタイトル                           |
| `readarr_release_bookids`         | 本のID                                           |
| `readarr_release_grids`           | リリースのGoodreads ID                           |
| `readarr_release_title`           | 本のタイトル                                     |
| `readarr_release_indexer`         | リリースが取得されたインデクサ                   |
| `readarr_release_size`            | リリースのサイズ                                 |
| `readarr_release_quality`         | リリースの品質                                   |
| `readarr_release_qualityVersion`  | リリースの品質バージョン                         |
| `readarr_release_releasegroup`    | リリースグループ（不明の場合は空）               |
| `readarr_download_client`         | リリースをダウンロードするために使用されるクライアント |
| `readarr_download_id`             | ダウンロードのID                                 |

## Import/Upgrade時

| 環境変数                 | 詳細                                             |
| ------------------------ | ------------------------------------------------ |
| `readarr_eventtype`      | `Download`                                       |
| `readarr_author_id`      | 著者の内部ID                                     |
| `readarr_author_name`    | 著者の名前                                       |
| `readarr_author_path`    | 著者のパス                                       |
| `readarr_author_grid`    | 著者のGoodreads ID                               |
| `readarr_book_id`        | 本のID                                           |
| `readarr_book_title`     | 本のタイトル                                     |
| `readarr_book_grid`      | 本のGoodreads ID                                 |
| `readarr_book_releasedate`| 本のリリース日                                   |
| `readarr_download_client`| リリースをダウンロードするために使用されるクライアント |
| `readarr_download_id`    | ダウンロードのID                                 |

## Rename時

| 環境変数             | 詳細                       |
| -------------------- | ------------------------- |
| `readarr_eventtype`  | `Rename`                  |
| `readarr_author_id`  | 著者の内部ID               |
| `readarr_author_name`| 著者の名前                 |
| `readarr_author_path`| 著者のパス                 |
| `readarr_author_grid`| 著者のGoodreads ID         |

## Book Retag時

| 環境変数                          | 詳細                       |
| --------------------------------- | ------------------------- |
| `readarr_eventtype`               | `TrackRetag`              |
| `readarr_author_id`               | 著者の内部ID               |
| `readarr_author_name`             | 著者の名前                 |
| `readarr_author_path`             | 著者のパス                 |
| `readarr_author_grid`             | 著者のGoodreads ID         |
| `readarr_book_id`                 | 本のID                     |
| `readarr_book_title`              | 本のタイトル               |
| `readarr_book_grid`               | 本のGoodreads ID           |
| `readarr_book_releasedate`        | 本のリリース日             |
| `readarr_bookfile_id`             | 本ファイルのID             |
| `readarr_bookfile_path`           | 本のパス                   |
| `readarr_bookfile_quality`        | 本ファイルの品質           |
| `readarr_bookfile_qualityversion` | 本ファイルの品質バージョン |
| `readarr_bookfile_releasegroup`   | 本のリリースグループ       |
| `readarr_bookfile_scenename`      | 本のシーン名               |
| `readarr_tags_diff`               | タグの差分                 |
| `readarr_tags_scrubbed`           | タグのスクラブ             |

## Health Issue時

| 環境変数                          | 詳細                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| `readarr_eventtype`               | `HealthIssue`                                                |
| `readarr_health_issue_level`      | ヘルスイシューのタイプ（`Ok`、`Notice`、`Warning`、または`Error`） |
| `readarr_health_issue_message`    | ヘルスイシューからのメッセージ                               |
| `readarr_health_issue_type`       | 失敗したエリアとヘルスイシューをトリガしたもの                 |
| `readarr_health_issue_wiki`       | WikiのURL（存在しない場合は空）                               |

## テスト時

Readarrにスクリプトを追加し、「テスト」をクリックすると、以下のパラメータでスクリプトが呼び出されます。スクリプトは、サポートされていないイベントタイプを優雅に無視できるようにする必要があります。

| 環境変数             | 詳細   |
| -------------------- | ------- |
| `readarr_eventtype`  | `Test`  |