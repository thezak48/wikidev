---
title: Radarr 配置 PostgreSQL 数据库
description: 使用 PostgreSQL 配置 Radarr
published: true
date: 2023-08-09T19:29:31.472Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:42:34.178Z
---

# Radarr 和 PostgreSQL

本文档将介绍在 Radarr 中迁移和设置 PostgreSQL 支持的关键要点。

> 需要 Radarr v4.1.0.6133 或更新版本
{.is-info}

此指南由了不起的 [Roxedus](https://github.com/Roxedus) 创建。

> Radarr 不会备份 PostgreSQL 数据库，任何备份必须由用户自行实施和维护
{.is-danger}

## 设置 PostgreSQL

首先，我们需要一个 PostgreSQL 实例。本指南是针对使用 `postgres:14` Docker 镜像的情况编写的。

> 切勿考虑使用 `latest` 标签！{.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=radarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## 创建数据库

Radarr 需要两个数据库，它们的默认名称如下：

- `radarr-main`：用于存储所有配置和历史记录
- `radarr-log`：用于存储生成日志条目的事件

> Radarr 不会为您创建这些数据库。请确保提前创建它们{.is-warning}

使用您喜欢的方法（例如 [pgAdmin](https://www.pgadmin.org/) 或 [Adminer](https://www.adminer.org/)）创建上述数据库。

您可以为数据库指定任何名称，但请确保 `config.xml` 文件中有正确的名称。有关更多信息，请参阅[模式创建](/radarr/postgres-setup#schema-creation)。

### 模式创建

我们需要告诉 Radarr 使用 PostgreSQL。`config.xml` 应该已经填充了我们需要的条目：

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

如果您想指定数据库名称，还应包括以下配置：

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

只有在创建了这两个数据库之后，您才可以开始从 SQLite 迁移到 PostgreSQL 的 Radarr 迁移。

## 迁移数据

> 如果您不想将现有的 SQLite 数据库迁移到 PostgreSQL，则此指南已经完成！{.is-info}

要迁移数据，我们可以使用 [PGLoader](https://github.com/dimitri/pgloader)。但是，它有一些注意事项：

- 默认情况下，事务是不区分大小写的，我们使用 `--with "quote identifiers"` 使其区分大小写。
- Debian 和 Ubuntu 的 apt 存储库中打包的版本对于较新版本的 PostgreSQL 来说太旧（Roxedus 尚未在其他发行版中测试过软件包）。
  Roxedus [构建了一个二进制文件](https://github.com/Roxedus/Pgloader-bin) 来支持此功能（无需修改代码，只需使用更新的依赖项进行构建）。

> 不要删除 PostgreSQL 实例中的任何表 {.is-danger}

在开始迁移之前，请确保您已经成功地使用创建的 PostgreSQL 数据库运行了 Radarr **至少一次**。按照以下步骤开始迁移：

1. 停止 Radarr
1. 打开您喜欢的数据库管理工具并连接到 PostgreSQL 数据库实例
1. 运行以下命令：

```SQL
DELETE FROM "Profiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. 使用以下任一选项开始迁移：

    - ```bash
      pgloader --with "quote identifiers" --with "data only" radarr.db 'postgresql://qstick:qstick@localhost/radarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/radarr.db:/radarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /radarr.db "postgresql://qstick:qstick@localhost/radarr-main"
      ```

  > 如果使用 pgloader 时遇到错误，可能是因为您的数据库太大，请尝试将 `--with "prefetch rows = 100" --with "batch size = 1MB"` 添加到上述命令中以解决此问题
  {.is-warning}

  > 在告诉它不要更改方案的情况下，使用 `--with "data only"` 处理起来非常简单
  {.is-info}


2. 启动 Radarr

3. 对于那些在从 SQLite 迁移后添加电影时遇到问题的用户，请运行以下命令：
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