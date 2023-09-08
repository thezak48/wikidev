---
title: ReadarrのPostgreSQLデータベースの設定
description: ReadarrをPostgresデータベースと設定する方法
published: true
date: 2022-12-04T23:00:38.482Z
tags: 
editor: markdown
dateCreated: 2022-07-25T22:49:56.668Z
---

# ReadarrとPostgres

このドキュメントでは、ReadarrでのPostgresサポートの移行と設定のキーポイントについて説明します。

> Readarr v0.1.1.1408以降が必要です
{.is-info}

このガイドは、素晴らしい[Roxedus](https://github.com/Roxedus)によって作成されました。

> ReadarrはPostgresデータベースをバックアップしません。バックアップはユーザーが実装および管理する必要があります
{.is-danger}

## Postgresのセットアップ

まず、Postgresのインスタンスが必要です。このガイドは、`postgres:14` Dockerイメージの使用方法について説明しています。

> `latest`タグを使用することは絶対に考えないでください！ {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=readarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## データベースの作成

Readarrには、次の3つのデータベースが必要です。

- `readarr-main`   これはすべての設定と履歴を保存するために使用されます
- `readarr-log`    これはログエントリを生成するイベントを保存するために使用されます
- `readarr-cache`    これはGoodReadsのキャッシュを保存するために使用されます

> Readarrはデータベースを自動的に作成しません。事前に作成してください{.is-warning}

上記のデータベースをお好みの方法で作成してください。たとえば、[pgAdmin](https://www.pgadmin.org/)や[Adminer](https://www.adminer.org/)などを使用することができます。

データベースには任意の名前を付けることができますが、`config.xml`ファイルに正しい名前が指定されていることを確認してください。詳細については、[スキーマの作成](/readarr/postgres-setup#schema-creation)を参照してください。

### スキーマの作成

ReadarrにPostgresを使用するように指示する必要があります。`config.xml`にはすでに必要なエントリが記入されているはずです。

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
<PostgresCacheDb>CacheDbName</PostgresCacheDb>
```

両方のデータベースを作成した**後にのみ**、SQLiteからPostgresへのReadarrの移行を開始できます。

## データの移行

> 既存のSQLiteデータベースをPostgresに移行したくない場合は、このガイドはすでに完了しています！ {.is-info}

データを移行するために、[PGLoader](https://github.com/dimitri/pgloader)を使用することができます。ただし、いくつかの注意点があります。

- デフォルトではトランザクションは大文字と小文字を区別しないため、`--with "quote identifiers"`を使用して大文字と小文字を区別するようにします。
- DebianとUbuntuのaptリポジトリにパッケージ化されたバージョンは、より新しいPostgresのバージョンでは古すぎます（Roxedusは他のディストリビューションのパッケージをテストしていません）。
  Roxedusは、このサポートを有効にするために[バイナリ](https://github.com/Roxedus/Pgloader-bin)をビルドしました（コードの変更は必要ありませんでしたが、更新された依存関係でビルドする必要がありました）。

> Postgresインスタンスのテーブルを削除しないでください {.is-danger}

移行を開始する前に、作成したPostgresデータベースでReadarrを**少なくとも1回**正常に実行したことを確認してください。次の手順で移行を開始します。

1. Readarrを停止します
1. 好みのデータベース管理ツールを開き、Postgresデータベースインスタンスに接続します
1. 次のコマンドを実行します。

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "MetadataProfiles";
```

1. 以下のいずれかのオプションを使用して移行を開始します。

    - ```bash
      pgloader --with "quote identifiers" --with "data only" readarr.db 'postgresql://qstick:qstick@localhost/readarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/readarr.db:/readarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /readarr.db "postgresql://qstick:qstick@localhost/readarr-main"
      ```

> pgloaderを使用してエラーが発生した場合は、DBが大きすぎるためかもしれません。この場合は、上記のコマンドに`--with "prefetch rows = 100" --with "batch size = 1MB"`を追加して解決してください。{.is-warning}

> これらの手順を実行した後は、`--with "data only"`を使用してスキーマを変更しないように指示するだけで、かなり簡単です。{.is-info}

1. Readarrを起動します