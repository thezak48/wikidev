---
title: ProwlarrのPostgreSQLデータベースの設定
description: PostgreSQLデータベースを使用してProwlarrを設定する方法について説明します。
published: true
date: 2022-11-29T13:19:38.953Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:38:53.538Z
---

# ProwlarrとPostgres

このドキュメントでは、ProwlarrでのPostgresサポートの移行と設定の主要なポイントについて説明します。

このガイドは、素晴らしい[Roxedus](https://github.com/Roxedus)によって作成されました。

> PostgresデータベースはProwlarrによってバックアップされません。バックアップはユーザーによって実装および管理する必要があります
{.is-danger}

## Postgresの設定

まず、Postgresのインスタンスが必要です。このガイドは、`postgres:14` Dockerイメージの使用方法について説明しています。

> `latest`タグを使用することは絶対に考えないでください！ {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=prowlarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## データベースの作成

Prowlarrには2つのデータベースが必要です。これらのデフォルトの名前は次のとおりです：

- `prowlarr-main`   これはすべての設定と履歴を保存するために使用されます
- `prowlarr-log`    これはログエントリを生成するイベントを保存するために使用されます

> Prowlarrはデータベースを自動的に作成しません。事前にこれらのデータベースを作成してください{.is-warning}

上記で言及されたデータベースを、お好みの方法で作成してください。たとえば、[pgAdmin](https://www.pgadmin.org/)や[Adminer](https://www.adminer.org/)を使用することができます。

> `Housekeeping`タスクを実行するためには、このユーザーがスーパーユーザーである必要があります。なぜなら、それはvacuumタスクを実行するためだからです{.is-info}

データベースには任意の名前を付けることができますが、`config.xml`ファイルに正しい名前が設定されていることを確認してください。詳細については、[スキーマの作成](/prowlarr/postgres-setup#schema-creation)を参照してください。

### スキーマの作成

ProwlarrにPostgresを使用するように設定する必要があります。`config.xml`にはすでに必要なエントリが入力されているはずです：

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

データベース名を指定する場合は、次の設定も含める必要があります：

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

両方のデータベースを作成した**後にのみ**、SQLiteからPostgresへのProwlarrの移行を開始できます。

## データの移行

> 既存のSQLiteデータベースをPostgresに移行したくない場合は、このガイドはすでに完了しています！ {.is-info}

データを移行するために、[PGLoader](https://github.com/dimitri/pgloader)を使用することができます。ただし、いくつかの注意点があります：

- デフォルトではトランザクションは大文字と小文字を区別しないため、`--with "quote identifiers"`を使用して大文字と小文字を区別するようにします。
- DebianおよびUbuntuのaptリポジトリにパッケージ化されたバージョンは、より新しいPostgresのバージョンでは古すぎます（Roxedusは他のディストリビューションのパッケージをテストしていません）。
  Roxedusは、このサポートを有効にするためにバイナリをビルドしました（コードの変更は必要ありませんでしたが、更新された依存関係でビルドする必要がありました）。

> Postgresインスタンスのテーブルを削除しないでください {.is-danger}

移行を開始する前に、作成したPostgresデータベースでProwlarrを**少なくとも1回正常に実行**したことを確認してください。次の手順で移行を開始します：

1. Prowlarrを停止します
1. 好みのデータベース管理ツールを開き、Postgresデータベースインスタンスに接続します
1. 次のいずれかのオプションを使用して移行を開始します：

    - ```bash
      pgloader --with "quote identifiers" --with "data only" prowlarr.db 'postgresql://qstick:qstick@localhost/prowlarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/prowlarr.db:/prowlarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /prowlarr.db "postgresql://qstick:qstick@localhost/prowlarr-main"
      ```

  > pgloaderを使用してエラーが発生した場合は、DBが大きすぎるためかもしれません。この場合は、上記のコマンドに`--with "prefetch rows = 100" --with "batch size = 1MB"`を追加して解決してください
  {.is-warning}

  > これらの処理が完了したら、`--with "data only"`を使用してスキーマを変更しないように指示するだけで、非常に簡単です
  {.is-info}

1. Prowlarrを起動します