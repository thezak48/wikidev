---
title: Sonarrのカスタムスクリプト
description: 
published: true
date: 2022-06-13T15:52:03.477Z
tags: sonarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:53.999Z
---

カスタムスクリプトをトリガーしたい場合は、[こちら](/sonarr/settings#connections)で詳細を確認できます。スクリプトはSonarrに[接続設定](/sonarr/settings#connections)を介して追加されます。

# 概要

Sonarrは、エピソードが新しくインポートされたりリネームされたりしたときにカスタムスクリプトを実行できます。アクションによっては、異なるパラメータが提供されます。パラメータは環境変数を介してスクリプトに渡されます。

## Sonarrログ

以下はカスタムスクリプトのみにログが記録されることに注意してください：

- スクリプトの`stdout`出力は`Debug`としてログに記録されます
- スクリプトの`stderr`出力は`Info`としてログに記録されます
- スクリプトのトリガーは`Trace`としてログに記録されます

# 環境変数

## Grab時

| 環境変数                                 | 詳細                                                                                          |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Grab`                                                                                       |
| `sonarr_series_id`                      | シリーズの内部ID                                                                              |
| `sonarr_series_title`                   | シリーズのタイトル                                                                            |
| `sonarr_series_tvdbid`                  | シリーズのTVDB ID                                                                             |
| `sonarr_series_tvmazeid`                | シリーズのTVMaze ID                                                                           |
| `sonarr_series_imdbid`                  | シリーズのIMDB ID（不明の場合は空）                                                            |
| `sonarr_series_type`                    | シリーズのタイプ（`Anime`、`Daily`、または`Standard`）                                         |
| `sonarr_release_episodecount`           | リリースのエピソード数                                                                        |
| `sonarr_release_seasonnumber`           | リリースのシーズン番号                                                                        |
| `sonarr_release_episodenumbers`         | カンマ区切りのエピソード番号のリスト                                                          |
| `sonarr_release_absoluteepisodenumbers` | カンマ区切りの絶対エピソード番号のリスト                                                      |
| `sonarr_release_episodeairdates`        | オリジナルネットワークからの放送日のカンマ区切りのリスト                                      |
| `sonarr_release_episodeairdatesutc`     | UTCでの放送日のカンマ区切りのリスト                                                            |
| `sonarr_release_episodetitles`          | エピソードタイトルの`\|`区切りのリスト                                                        |
| `sonarr_release_title`                  | トレント/NZBのタイトル                                                                        |
| `sonarr_release_indexer`                | リリースが取得されたインデクサー                                                               |
| `sonarr_release_size`                   | インデクサーによって報告されたリリースのサイズ                                                |
| `sonarr_release_quality`                | Sonarrによって検出されたリリースの品質名                                                      |
| `sonarr_release_qualityversion`         | `1`はデフォルト、`2`は正式版、`3`以上はアニメバージョンに使用できます                           |
| `sonarr_release_releasegroup`           | リリースグループ（不明の場合は空）                                                            |
| `sonarr_download_client`                | ダウンロードクライアント                                                                        |
| `sonarr_download_id`                    | トレント/NZBファイルのハッシュ（ダウンロードクライアントでダウンロードを一意に識別するために使用） |

## Import時/Upgrade時

| 環境変数                               | 詳細                                                                                        |
| -------------------------------------- | ------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                     | `Download`                                                                                  |
| `sonarr_isupgrade`                     | 既存のファイルがアップグレードされた場合は `True`、それ以外の場合は `False`                          |
| `sonarr_series_id`                     | シリーズの内部ID                                                                              |
| `sonarr_series_title`                  | シリーズのタイトル                                                                            |
| `sonarr_series_path`                   | シリーズのフルパス                                                                            |
| `sonarr_series_tvdbid`                 | シリーズのTVDB ID                                                                             |
| `sonarr_series_tvmazeid`               | シリーズのTVMaze ID                                                                           |
| `sonarr_series_imdbid`                 | シリーズのIMDB ID（不明の場合は空）                                                           |
| `sonarr_series_type`                   | シリーズのタイプ（`Anime`、`Daily`、または `Standard`）                                       |
| `sonarr_episodefile_id`                | エピソードファイルの内部ID                                                                    |
| `sonarr_episodefile_episodecount`      | ファイル内のエピソード数                                                                      |
| `sonarr_episodefile_relativepath`      | シリーズパスからのエピソードファイルのパス（相対パス）                                        |
| `sonarr_episodefile_path`              | エピソードファイルのフルパス                                                                  |
| `sonarr_episodefile_episodeids`        | エピソードファイルの内部ID（複数ある場合はカンマ区切り）                                      |
| `sonarr_episodefile_seasonnumber`      | エピソードファイルのシーズン番号                                                              |
| `sonarr_episodefile_episodenumbers`    | エピソード番号のカンマ区切りのリスト                                                          |
| `sonarr_episodefile_episodeairdates`   | オリジナルネットワークからの放送日のカンマ区切りのリスト                                      |
| `sonarr_episodefile_episodeairdatesutc`| UTCでの放送日のカンマ区切りのリスト                                                            |
| `sonarr_episodefile_episodetitles`     | エピソードタイトルの `|` 区切りのリスト                                                       |
| `sonarr_episodefile_quality`           | Sonarr によって検出されたエピソードファイルの品質名                                           |
| `sonarr_episodefile_qualityversion`    | `1` はデフォルト、`2` は正式版、`3` 以上はアニメ版に使用されることがあります                      |
| `sonarr_episodefile_releasegroup`      | リリースグループ（不明の場合は空）                                                            |
| `sonarr_episodefile_scenename`         | オリジナルのリリース名（不明の場合は空）                                                      |
| `sonarr_episodefile_sourcepath`        | インポートされたエピソードファイルのフルパス                                                  |
| `sonarr_episodefile_sourcefolder`      | エピソードファイルがインポートされたフォルダのフルパス                                        |
| `sonarr_download_client`               | ダウンロードクライアント                                                                       |
| `sonarr_download_id`                   | トレント/NZBファイルのハッシュ（ダウンロードクライアントでダウンロードを一意に識別するために使用） |
| `sonarr_deletedrelativepaths`          | このファイルをインポートするために削除されたファイルの `|` 区切りのリスト                       |
| `sonarr_deletedpaths`                  | このファイルをインポートするために削除されたファイルのフルパスの `|` 区切りのリスト             |

## リネーム時

| 環境変数                | 詳細                           |
| ----------------------- | ------------------------------ |
| `sonarr_eventtype`      | `Rename`                       |
| `sonarr_series_id`      | シリーズの内部ID               |
| `sonarr_series_title`   | シリーズのタイトル             |
| `sonarr_series_path`    | シリーズのフルパス             |
| `sonarr_series_tvdbid`  | シリーズのTVDB ID              |
| `sonarr_series_tvmazeid`| シリーズのTVMaze ID            |
| `sonarr_series_imdbid`  | シリーズのIMDB ID（不明の場合は空） |
| `sonarr_series_type`    | シリーズのタイプ（`Anime`、`Daily`、または `Standard`） |

## エピソードファイル削除時

| 環境変数                               | 詳細                                                                               |
| -------------------------------------- | ---------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `EpisodeFileDelete`                                                               |
| `sonarr_series_id`                      | シリーズの内部ID                                                                     |
| `sonarr_series_title`                   | シリーズのタイトル                                                                   |
| `sonarr_series_path`                    | シリーズのフルパス                                                                   |
| `sonarr_series_tvdbid`                  | シリーズのTVDB ID                                                                    |
| `sonarr_series_tvmazeid`                | シリーズのTVMaze ID                                                                  |
| `sonarr_series_imdbid`                  | シリーズのIMDB ID（不明の場合は空）                                                   |
| `sonarr_series_type`                    | シリーズのタイプ（`Anime`、`Daily`、または`Standard`）                                |
| `sonarr_episodefile_id`                 | エピソードファイルの内部ID                                                           |
| `sonarr_episodefile_episodecount`       | ファイル内のエピソード数                                                             |
| `sonarr_episodefile_relativepath`       | シリーズのパスからのエピソードファイルのパス                                           |
| `sonarr_episodefile_path`               | エピソードファイルのフルパス                                                         |
| `sonarr_episodefile_episodeids`         | エピソードファイルの内部ID（複数ある場合はカンマ区切り）                               |
| `sonarr_episodefile_seasonnumber`       | エピソードファイルのシーズン番号                                                     |
| `sonarr_episodefile_episodenumbers`     | エピソード番号のカンマ区切りリスト                                                   |
| `sonarr_episodefile_episodeairdates`    | オリジナルネットワークからの放送日のカンマ区切りリスト                                 |
| `sonarr_episodefile_episodeairdatesutc` | UTCでの放送日のカンマ区切りリスト                                                     |
| `sonarr_episodefile_episodetitles`      | エピソードタイトルの`\|`区切りリスト                                                 |
| `sonarr_episodefile_quality`            | Sonarrによって検出されたエピソードファイルの品質名                                     |
| `sonarr_episodefile_qualityversion`     | `1`はデフォルト、`2`は正式版、`3`以上はアニメバージョンに使用されることがあります       |
| `sonarr_episodefile_releasegroup`       | リリースグループ（不明の場合は空）                                                   |
| `sonarr_episodefile_scenename`          | オリジナルのリリース名（不明の場合は空）                                             |

## シリーズ削除時

| 環境変数                | 詳細                         |
| ----------------------- | ---------------------------- |
| `sonarr_eventtype`      | `SeriesDelete`               |
| `sonarr_series_id`      | シリーズの内部ID               |
| `sonarr_series_title`   | シリーズのタイトル             |
| `sonarr_series_path`    | シリーズのフルパス             |
| `sonarr_series_tvdbid`  | シリーズのTVDB ID              |
| `sonarr_series_imdbid`  | シリーズのIMDB ID（不明の場合は空） |
| `sonarr_series_type`    | シリーズのタイプ（`Anime`、`Daily`、または`Standard`） |

## ヘルスイシュー時

| 環境変数                     | 詳細                                                            |
| ---------------------------- | --------------------------------------------------------------- |
| `sonarr_eventtype`           | `HealthIssue`                                                   |
| `sonarr_health_issue_level`  | ヘルスイシューのタイプ（`Ok`、`Notice`、`Warning`、または`Error`） |
| `sonarr_health_issue_message`| ヘルスイシューからのメッセージ                                   |
| `sonarr_health_issue_type`   | 失敗したエリアとヘルスイシューをトリガしたエリア                   |
| `sonarr_health_issue_wiki`   | WikiのURL（存在しない場合は空）                                  |

## アプリケーションの更新時

| 環境変数                       | 詳細                                        |
| ------------------------------ | ------------------------------------------- |
| `sonarr_eventtype`             | `ApplicationUpdate`                         |
| `sonarr_update_message`        | 更新からのメッセージ                         |
| `sonarr_update_newversion`     | Sonarrが更新されたバージョン（文字列）       |
| `sonarr_update_previousversion`| Sonarrが更新される前のバージョン（文字列）   |

## テスト時

Sonarrにスクリプトを追加し、「テスト」をクリックすると、以下のパラメータでスクリプトが呼び出されます。スクリプトは、サポートされていないイベントタイプを優雅に無視できるようにする必要があります。

| 環境変数              | 詳細     |
| --------------------- | ------- |
| `sonarr_eventtype`    | `Test`  |