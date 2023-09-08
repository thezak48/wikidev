---
title: LIdarrのPostgreSQLデータベースの設定
description: Postgresデータベースを使用してLidarrを設定する方法
published: true
date: 2023-09-03T17:21:21.279Z
tags: 
editor: markdown
dateCreated: 2022-11-25T01:35:56.796Z
---

# LidarrとPostgres

このドキュメントでは、LidarrでのPostgresサポートの移行と設定の主要なポイントについて説明します。

> Lidarr v1.1.2.2890以降が必要です
{.is-info}

このガイドは、素晴らしい[Roxedus](https://github.com/Roxedus)によって作成されました。

> LidarrはPostgresデータベースをバックアップしません。バックアップはユーザーが実装および管理する必要があります
{.is-danger}

## Postgresの設定

まず、Postgresインスタンスが必要です。このガイドは、`postgres:14` Dockerイメージの使用方法について説明しています。

> `latest`タグを使用することは絶対に考えないでください！ {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=lidarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## データベースの作成

Lidarrには2つのデータベースが必要です。これらのデフォルトの名前は次のとおりです。

- `lidarr-main`   これはすべての設定と履歴を保存するために使用されます
- `lidarr-log`    これはログエントリを生成するイベントを保存するために使用されます

> Lidarrはデータベースを自動的に作成しません。事前に作成してください{.is-warning}

上記で言及されたデータベースを、お好みの方法で作成してください。たとえば、[pgAdmin](https://www.pgadmin.org/)や[Adminer](https://www.adminer.org/)を使用することができます。

データベースには任意の名前を付けることができますが、`config.xml`ファイルに正しい名前が指定されていることを確認してください。詳細については、[スキーマの作成](/lidarr/postgres-setup#schema-creation)を参照してください。

### スキーマの作成

LidarrにPostgresを使用するように指示する必要があります。`config.xml`には、すでに必要なエントリが入力されているはずです。

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

データベース名を指定する場合は、次の設定も含める必要があります。

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

両方のデータベースを**作成した後にのみ**、SQLiteからPostgresへのLidarrの移行を開始できます。

## データの移行

> 既存のSQLiteデータベースをPostgresに移行したくない場合は、このガイドはすでに完了しています！ {.is-info}

データを移行するために、[PGLoader](https://github.com/dimitri/pgloader)を使用することができます。ただし、いくつかの注意点があります。

- デフォルトではトランザクションは大文字と小文字を区別しないため、`--with "quote identifiers"`を使用して大文字と小文字を区別するようにします。
- DebianとUbuntuのaptリポジトリにパッケージ化されたバージョンは、より新しいPostgresのバージョンでは古すぎます（Roxedusは他のディストリビューションのパッケージをテストしていません）。
  Roxedusは、このサポートを有効にするために[バイナリ](https://github.com/Roxedus/Pgloader-bin)をビルドしました（コードの変更は必要ありませんでしたが、更新された依存関係でビルドする必要がありました）。

> Postgresインスタンスのテーブルを削除しないでください {.is-danger}

移行を開始する前に、作成したPostgresデータベースでLidarrを**少なくとも1回**正常に実行したことを確認してください。次の手順で移行を開始します。

1. Lidarrを停止します
2. 好みのデータベース管理ツールを開き、Postgresデータベースインスタンスに接続します
3. 次のコマンドを実行します：

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
DELETE FROM "MetadataProfiles";
```

4. 以下のいずれかのオプションを使用して移行を開始します：

    - ```bash
      pgloader --with "quote identifiers" --with "data only" lidarr.db 'postgresql://qstick:qstick@localhost/lidarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/lidarr.db:/lidarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /lidarr.db "postgresql://qstick:qstick@localhost/lidarr-main"
      ```

  > pgloaderを使用してエラーが発生した場合は、DBが大きすぎるためかもしれません。この場合は、上記のコマンドに`--with "prefetch rows = 100" --with "batch size = 1MB"`を追加して解決してください
  {.is-warning}
  
  > これらの手順を実行すると、`--with "data only"`を使用してスキーマを変更しないように指示した後は、かなり簡単です
  {.is-info}

5. Lidarrを起動します
6. データベースで以下のクエリを実行します。`Npgsql.PostgresException (0x80004005): 23505: duplicate key value violates unique constraint`のようなエラーが発生した場合は、次のクエリを実行してください。
```sql
select setval('public."AlbumReleases_Id_seq"',(SELECT MAX("Id")+1 FROM "AlbumReleases"));
select setval('public."Albums_Id_seq"',(SELECT MAX("Id")+1 FROM "Albums"));
select setval('public."ArtistMetadata_Id_seq"',(SELECT MAX("Id")+1 FROM "ArtistMetadata"));
select setval('public."Artists_Id_seq"',(SELECT MAX("Id")+1 FROM "Artists"));
select setval('public."Blacklist_Id_seq"',(SELECT MAX("Id")+1 FROM "Blocklist"));
select setval('public."Commands_Id_seq"',(SELECT MAX("Id")+1 FROM "Commands"));
select setval('public."Config_Id_seq"',(SELECT MAX("Id")+1 FROM "Config"));
select setval('public."CustomFilters_Id_seq"',(SELECT MAX("Id")+1 FROM "CustomFilters"));
select setval('public."CustomFormats_Id_seq"',(SELECT MAX("Id")+1 FROM "CustomFormats"));
select setval('public."DelayProfiles_Id_seq"',(SELECT MAX("Id")+1 FROM "DelayProfiles"));
select setval('public."DownloadClientStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "DownloadClientStatus"));
select setval('public."DownloadClients_Id_seq"',(SELECT MAX("Id")+1 FROM "DownloadClients"));
select setval('public."DownloadHistory_Id_seq"',(SELECT MAX("Id")+1 FROM "DownloadHistory"));
select setval('public."ExtraFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "ExtraFiles"));
select setval('public."History_Id_seq"',(SELECT MAX("Id")+1 FROM "History"));
select setval('public."ImportListExclusions_Id_seq"',(SELECT MAX("Id")+1 FROM "ImportListExclusions"));
select setval('public."ImportListStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "ImportListStatus"));
select setval('public."ImportLists_Id_seq"',(SELECT MAX("Id")+1 FROM "ImportLists"));
select setval('public."IndexerStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "IndexerStatus"));
select setval('public."Indexers_Id_seq"',(SELECT MAX("Id")+1 FROM "Indexers"));
select setval('public."LyricFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "LyricFiles"));
select setval('public."MetadataFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "MetadataFiles"));
select setval('public."MetadataProfiles_Id_seq"',(SELECT MAX("Id")+1 FROM "MetadataProfiles"));
select setval('public."Metadata_Id_seq"',(SELECT MAX("Id")+1 FROM "Metadata"));
select setval('public."NamingConfig_Id_seq"',(SELECT MAX("Id")+1 FROM "NamingConfig"));
select setval('public."NotificationStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "NotificationStatus"));
select setval('public."Notifications_Id_seq"',(SELECT MAX("Id")+1 FROM "Notifications"));
select setval('public."PendingReleases_Id_seq"',(SELECT MAX("Id")+1 FROM "PendingReleases"));
-- select setval('public."Profiles_Id_seq"',(SELECT MAX("Id")+1 FROM "Profiles"));
select setval('public."QualityDefinitions_Id_seq"',(SELECT MAX("Id")+1 FROM "QualityDefinitions"));
select setval('public."RemotePathMappings_Id_seq"',(SELECT MAX("Id")+1 FROM "RemotePathMappings"));
-- select setval('public."Restrictions_Id_seq"',(SELECT MAX("Id")+1 FROM "Restrictions"));
select setval('public."RootFolders_Id_seq"',(SELECT MAX("Id")+1 FROM "RootFolders"));
select setval('public."ScheduledTasks_Id_seq"',(SELECT MAX("Id")+1 FROM "ScheduledTasks"));
select setval('public."Tags_Id_seq"',(SELECT MAX("Id")+1 FROM "Tags"));
select setval('public."TrackFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "TrackFiles"));
select setval('public."Tracks_Id_seq"',(SELECT MAX("Id")+1 FROM "Tracks"));
select setval('public."Users_Id_seq"',(SELECT MAX("Id")+1 FROM "Users"));
```
注：2つのクエリはコメントアウトされていますが、シーケンスの「ソース」テーブルが見つからなかったためです。