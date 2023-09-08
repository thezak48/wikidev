---
title: RadarrのPostgreSQLデータベースの設定
description: PostgreSQLデータベースを使用してRadarrを設定する方法
published: true
date: 2023-08-09T19:29:31.472Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:42:34.178Z
---

# RadarrとPostgreSQL

このドキュメントでは、RadarrでのPostgreSQLサポートの移行と設定の主要なポイントについて説明します。

> Radarr v4.1.0.6133以降が必要です
{.is-info}

このガイドは、素晴らしい[Roxedus](https://github.com/Roxedus)によって作成されました。

> RadarrはPostgreSQLデータベースをバックアップしません。バックアップはユーザーが実装および管理する必要があります
{.is-danger}

## PostgreSQLの設定

まず、PostgreSQLインスタンスが必要です。このガイドは、`postgres:14` Dockerイメージの使用方法について説明しています。

> `latest`タグを使用することは絶対に考えないでください！ {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=radarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## データベースの作成

Radarrには2つのデータベースが必要です。これらのデフォルトの名前は次のとおりです。

- `radarr-main`   これはすべての設定と履歴を保存するために使用されます
- `radarr-log`    これはログエントリを生成するイベントを保存するために使用されます

> Radarrはデータベースを自動的に作成しません。事前にこれらのデータベースを作成してください{.is-warning}

上記で言及されたデータベースを、お好みの方法で作成してください。たとえば、[pgAdmin](https://www.pgadmin.org/)や[Adminer](https://www.adminer.org/)を使用することができます。

データベースには任意の名前を付けることができますが、`config.xml`ファイルに正しい名前が記載されていることを確認してください。詳細については、[スキーマの作成](/radarr/postgres-setup#schema-creation)を参照してください。

### スキーマの作成

RadarrにPostgreSQLを使用するように指示する必要があります。`config.xml`には、すでに必要なエントリが記載されているはずです。

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

両方のデータベースを**作成した後にのみ**、SQLiteからPostgreSQLへのRadarrの移行を開始できます。

## データの移行

> 既存のSQLiteデータベースをPostgreSQLに移行したくない場合は、このガイドはすでに完了しています！ {.is-info}

データを移行するために、[PGLoader](https://github.com/dimitri/pgloader)を使用することができます。ただし、いくつかの注意点があります。

- デフォルトではトランザクションは大文字と小文字を区別しないため、`--with "quote identifiers"`を使用して大文字と小文字を区別するようにします。
- DebianとUbuntuのaptリポジトリにパッケージ化されたバージョンは、より新しいPostgreSQLのバージョンでは古すぎます（Roxedusは他のディストリビューションのパッケージをテストしていません）。
  Roxedusは、このサポートを有効にするために[バイナリ](https://github.com/Roxedus/Pgloader-bin)をビルドしました（コードの変更は必要ありませんでしたが、更新された依存関係でビルドする必要がありました）。

> Postgresインスタンスのテーブルを削除しないでください {.is-danger}

移行を開始する前に、Radarrを作成したPostgresデータベースに対して**少なくとも1回は正常に実行**したことを確認してください。次の手順で移行を開始します。

1. Radarrを停止します
1. 好みのデータベース管理ツールを開き、Postgresデータベースインスタンスに接続します
1. 次のコマンドを実行します:

```SQL
DELETE FROM "Profiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. 以下のいずれかのオプションを使用して、移行を開始します:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" radarr.db 'postgresql://qstick:qstick@localhost/radarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/radarr.db:/radarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /radarr.db "postgresql://qstick:qstick@localhost/radarr-main"
      ```

  > pgloaderを使用してエラーが発生した場合は、DBが大きすぎるためかもしれません。この場合は、上記のコマンドに`--with "prefetch rows = 100" --with "batch size = 1MB"`を追加して解決してください
  {.is-warning}

  > これらの設定を行った後は、`--with "data only"`を使用してスキーマを変更しないようにするだけで、かなり簡単です
  {.is-info}


2. Radarrを起動します

3. SQLiteからの移行後に映画を追加する際に問題が発生する場合は、次のコマンドを実行します:
```SQL
select setval('public."MovieFiles_Id_seq"', (SELECT MAX("Id")+1 FROM "MovieFiles"));
select setval('public."AlternativeTitles_Id_seq"', (SELECT MAX("Id")+1 FROM "AlternativeTitles"));
select setval('public."Blacklist_Id_seq"', (SELECT MAX("Id")+1 FROM "Blocklist"));
select setval('public."Collections_Id_seq"', (SELECT MAX("Id")+1 FROM "Collections"));
select setval('public."Commands_Id_seq"', (SELECT MAX("Id")+1 FROM "Commands"));
select setval('public."Config_Id_seq"', (SELECT MAX("Id")+1 FROM "Config"));
select setval('public."Credits_Id_seq"', (SELECT MAX("Id")+1 FROM "Credits"));
select setval('public."CustomFilters_Id_seq"', (SELECT MAX("Id")+1 FROM "CustomFilters"));
select setval('public."CustomFormats_Id_seq"', (SELECT MAX("Id")+1 FROM "CustomFormats"));
select setval('public."DelayProfiles_Id_seq"', (SELECT MAX("Id")+1 FROM "DelayProfiles"));
select setval('public."DownloadClientStatus_Id_seq"', (SELECT MAX("Id")+1 FROM "DownloadClientStatus"));
select setval('public."DownloadClients_Id_seq"', (SELECT MAX("Id")+1 FROM "DownloadClients"));
select setval('public."DownloadHistory_Id_seq"', (SELECT MAX("Id")+1 FROM "DownloadHistory"));
select setval('public."ExtraFiles_Id_seq"', (SELECT MAX("Id")+1 FROM "ExtraFiles"));
select setval('public."History_Id_seq"', (SELECT MAX("Id")+1 FROM "History"));
select setval('public."ImportExclusions_Id_seq"', (SELECT MAX("Id")+1 FROM "ImportExclusions"));
select setval('public."ImportListMovies_Id_seq"', (SELECT MAX("Id")+1 FROM "ImportListMovies"));
select setval('public."IndexerStatus_Id_seq"', (SELECT MAX("Id")+1 FROM "IndexerStatus"));
select setval('public."Indexers_Id_seq"', (SELECT MAX("Id")+1 FROM "Indexers"));
select setval('public."MetadataFiles_Id_seq"', (SELECT MAX("Id")+1 FROM "MetadataFiles"));
select setval('public."Metadata_Id_seq"', (SELECT MAX("Id")+1 FROM "Metadata"));
select setval('public."MovieFiles_Id_seq"', (SELECT MAX("Id")+1 FROM "MovieFiles"));
select setval('public."MovieMetadata_Id_seq"', (SELECT MAX("Id")+1 FROM "MovieMetadata"));
select setval('public."MovieTranslations_Id_seq"', (SELECT MAX("Id")+1 FROM "MovieTranslations"));
select setval('public."Movies_Id_seq"', (SELECT MAX("Id")+1 FROM "Movies"));
select setval('public."NamingConfig_Id_seq"', (SELECT MAX("Id")+1 FROM "NamingConfig"));
select setval('public."Notifications_Id_seq"', (SELECT MAX("Id")+1 FROM "Notifications"));
select setval('public."PendingReleases_Id_seq"', (SELECT MAX("Id")+1 FROM "PendingReleases"));
select setval('public."Profiles_Id_seq"', (SELECT MAX("Id")+1 FROM "Profiles"));
select setval('public."QualityDefinitions_Id_seq"', (SELECT MAX("Id")+1 FROM "QualityDefinitions"));
select setval('public."Restrictions_Id_seq"', (SELECT MAX("Id")+1 FROM "Restrictions"));
select setval('public."RootFolders_Id_seq"', (SELECT MAX("Id")+1 FROM "RootFolders"));
select setval('public."ScheduledTasks_Id_seq"', (SELECT MAX("Id")+1 FROM "ScheduledTasks"));
select setval('public."SubtitleFiles_Id_seq"', (SELECT MAX("Id")+1 FROM "SubtitleFiles"));
select setval('public."Tags_Id_seq"', (SELECT MAX("Id")+1 FROM "Tags"));
select setval('public."Users_Id_seq"', (SELECT MAX("Id")+1 FROM "Users"));
```