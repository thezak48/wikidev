---
title: Radarrカスタムスクリプト
description: 
published: true
date: 2022-05-02T03:36:09.625Z
tags: radarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:44.765Z
---

カスタムスクリプトをトリガーする場合は、[こちら](/radarr/settings#connections)で詳細を確認できます。スクリプトは、Radarrの[接続設定](/radarr/settings#connections)を介して追加されます。

# 概要

Radarrは、映画がインポートまたはリネームされたときにカスタムスクリプトを実行できます。アクションに応じて、異なるパラメータが提供されます。パラメータは環境変数を介してスクリプトに渡されます。

## Radarrログ

以下は、カスタムスクリプトのみがログに記録されることに注意してください：

- スクリプトの`stdout`出力は`Debug`としてログに記録されます
- スクリプトの`stderr`出力は`Info`としてログに記録されます
- スクリプトのトリガーは`Trace`でログに記録されます

# 環境変数

## Grab時

| 環境変数                          | 詳細                                                                                          |
| --------------------------------- | ----------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                | `Grab`                                                                                         |
| `radarr_download_client`          | ダウンロードクライアント（不明の場合は空）                                                     |
| `radarr_download_id`              | トレント/NZBファイルのハッシュ（ダウンロードクライアントでダウンロードを一意に識別するために使用） |
| `radarr_movie_id`                 | 映画の内部ID                                                                                  |
| `radarr_movie_imdbid`             | 映画のIMDb ID（不明の場合は空）                                                                |
| `radarr_movie_in_cinemas_date`    | 映画の公開日（不明の場合は空）                                                                |
| `radarr_movie_physical_release_date` | 映画の物理リリース日（不明の場合は空）                                                      |
| `radarr_movie_title`              | 映画のタイトル                                                                                |
| `radarr_movie_tmdbid`             | 映画のTMDb ID                                                                                 |
| `radarr_movie_year`               | 映画のリリース年                                                                              |
| `radarr_release_indexer`          | リリースが取得されたインデクサー                                                               |
| `radarr_release_quality`          | Radarrによって検出されたリリースの品質名                                                       |
| `radarr_release_qualityversion`   | `1`はデフォルト、`2`は正式版、`3`以上はアニメバージョンに使用できます                           |
| `radarr_release_releasegroup`     | リリースグループ（不明の場合は空）                                                             |
| `radarr_release_size`             | インデクサーによって報告されたリリースのサイズ                                                 |
| `radarr_release_title`            | トレント/NZBのタイトル                                                                        |

## Import時/Upgrade時

| 環境変数                          | 詳細                                                                                          |
| --------------------------------- | ----------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                | `Download`                                                                                     |
| `radarr_download_id`              | トレント/NZBファイルのハッシュ（ダウンロードクライアントでダウンロードを一意に識別するために使用） |
| `radarr_download_client`          | ダウンロードクライアント                                                                        |
| `radarr_isupgrade`                | 既存のファイルがアップグレードされた場合は`True`、それ以外の場合は`False`                         |
| `radarr_movie_id`                 | 映画の内部ID                                                                                  |
| `radarr_movie_imdbid`             | 映画のIMDb ID（不明の場合は空）                                                                |
| `radarr_movie_in_cinemas_date`    | 映画の公開日（不明の場合は空）                                                                |
| `radarr_movie_path`               | 映画のフルパス                                                                                |
| `radarr_movie_physical_release_date` | 映画の物理リリース日（不明の場合は空）                                                      |
| `radarr_movie_title`              | 映画のタイトル                                                                                |
| `radarr_movie_tmdbid`             | 映画のTMDb ID                                                                                 |
| `radarr_movie_year`               | 映画のリリース年                                                                              |
| `radarr_moviefile_id`             | 映画ファイルの内部ID                                                                          |
| `radarr_moviefile_relativepath`   | 映画ファイルのパス（映画パスを基準とした相対パス）                                             |
| `radarr_moviefile_path`           | 映画ファイルのフルパス                                                                        |
| `radarr_moviefile_quality`        | Radarrによって検出されたリリースの品質名                                                       |
| `radarr_moviefile_qualityversion` | `1`はデフォルト、`2`は正式版、`3`以上はアニメバージョンに使用できます                           |
| `radarr_moviefile_releasegroup`   | リリースグループ（不明の場合は空）                                                             |
| `radarr_moviefile_scenename`      | オリジナルのリリース名（不明の場合は空）                                                       |
| `radarr_moviefile_sourcepath`     | インポートされた映画ファイルのフルパス                                                         |
| `radarr_moviefile_sourcefolder`   | 映画ファイルがインポートされたフォルダのフルパス                                               |
| `radarr_deletedrelativepaths`     | このファイルをインポートするために削除されたファイルの`|`で区切られたリスト                       |
| `radarr_deletedpaths`             | このファイルをインポートするために削除されたファイルのフルパスの`|`で区切られたリスト                 |

## Rename時

| 環境変数                                 | 詳細                                             |
| ---------------------------------------- | ----------------------------------------------- |
| `radarr_eventtype`                       | `Rename`                                        |
| `radarr_movie_id`                        | 映画の内部ID                                     |
| `radarr_movie_title`                     | 映画のタイトル                                   |
| `radarr_movie_year`                      | 映画のリリース年                                 |
| `radarr_movie_path`                      | 映画のフルパス                                   |
| `radarr_movie_imdbid`                    | 映画のIMDb ID（不明の場合は空）                  |
| `radarr_movie_tmdbid`                    | 映画のTMDb ID                                   |
| `radarr_movie_in_cinemas_date`           | 映画の劇場公開日（不明の場合は空）                |
| `radarr_movie_physical_release_date`     | 映画の物理/ウェブリリース日（不明の場合は空）    |
| `radarr_moviefile_ids`                   | ファイルIDの`,`区切りのリスト                    |
| `radarr_moviefile_relativepaths`         | 相対パスの`|`区切りのリスト                       |
| `radarr_moviefile_paths`                 | パスの`|`区切りのリスト                           |
| `radarr_moviefile_previousrelativepaths` | 以前の相対パスの`|`区切りのリスト                 |
| `radarr_moviefile_previouspaths`         | 以前のパスの`|`区切りのリスト                       |

## ヘルスチェック時

| 環境変数                      | 詳細                                                      |
| ----------------------------- | ------------------------------------------------------------ |
| `radarr_eventtype`            | `HealthIssue`                                                |
| `radarr_health_issue_level`   | ヘルスチェックの種類（`Ok`、`Notice`、`Warning`、または`Error`） |
| `radarr_health_issue_message` | ヘルスチェックのメッセージ                                   |
| `radarr_health_issue_type`    | 失敗したエリアとヘルスチェックをトリガーしたエリア           |
| `radarr_health_issue_wiki`    | WikiのURL（存在しない場合は空）                               |

## アプリケーションの更新時

| 環境変数                      | 詳細                               |
| ----------------------------- | ---------------------------------- |
| `radarr_eventtype`            | `ApplicationUpdate`                |
| `radarr_update_message`       | 更新のメッセージ                    |
| `radarr_update_newversion`    | Radarrが更新されたバージョン（文字列） |
| `radarr_update_previousversion` | Radarrが更新される前のバージョン（文字列） |

## テスト時

Radarrにスクリプトを追加し、「テスト」をクリックすると、以下のパラメータでスクリプトが呼び出されます。スクリプトは、サポートされていないイベントタイプを優雅に無視できる必要があります。

| 環境変数              | 詳細   |
| -------------------- | ------- |
| `radarr_eventtype`   | `Test`  |