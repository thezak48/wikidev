---
title: Lidarr 配置 PostgreSQL 数据库
description: 使用 PostgreSQL 配置 Lidarr
published: true
date: 2023-09-03T17:21:21.279Z
tags: 
editor: markdown
dateCreated: 2022-11-25T01:35:56.796Z
---

# Lidarr 和 PostgreSQL

本文档将介绍在 Lidarr 中迁移和设置 PostgreSQL 支持的关键要点。

> 需要 Lidarr v1.1.2.2890 或更新版本
{.is-info}

本指南由出色的 [Roxedus](https://github.com/Roxedus) 创建。

> Lidarr 不会备份 PostgreSQL 数据库，任何备份必须由用户自行实施和维护
{.is-danger}

## 设置 PostgreSQL

首先，我们需要一个 PostgreSQL 实例。本指南是针对使用 `postgres:14` Docker 镜像的情况编写的。

> 切勿考虑使用 `latest` 标签！{.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=lidarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## 创建数据库

Lidarr 需要两个数据库，它们的默认名称如下：

- `lidarr-main`：用于存储所有配置和历史记录
- `lidarr-log`：用于存储生成日志条目的事件

> Lidarr 不会为您创建这些数据库。请确保提前创建它们{.is-warning}

使用您喜欢的方法（例如 [pgAdmin](https://www.pgadmin.org/) 或 [Adminer](https://www.adminer.org/)）创建上述数据库。

您可以为数据库指定任何名称，但请确保 `config.xml` 文件中有正确的名称。有关更多信息，请参阅 [模式创建](/lidarr/postgres-setup#schema-creation)。

### 模式创建

我们需要告诉 Lidarr 使用 PostgreSQL。`config.xml` 应该已经填充了我们需要的条目：

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

只有在创建了这两个数据库之后，您才可以开始从 SQLite 迁移到 PostgreSQL 的 Lidarr 迁移。

## 迁移数据

> 如果您不想将现有的 SQLite 数据库迁移到 PostgreSQL，则已经完成了本指南！{.is-info}

要迁移数据，我们可以使用 [PGLoader](https://github.com/dimitri/pgloader)。但是，它有一些注意事项：

- 默认情况下，事务是不区分大小写的，我们使用 `--with "quote identifiers"` 使其区分大小写。
- Debian 和 Ubuntu 的 apt 存储库中打包的版本对于较新版本的 PostgreSQL 来说太旧（Roxedus 尚未测试其他发行版中的软件包）。
  Roxedus [构建了一个二进制文件](https://github.com/Roxedus/Pgloader-bin) 来支持此功能（无需修改代码，只需使用更新的依赖项进行构建）。

> 不要删除 Postgres 实例中的任何表 {.is-danger}

在开始迁移之前，请确保您已经成功地至少运行了一次 Lidarr 对创建的 PostgreSQL 数据库。按照以下步骤开始迁移：

1. 停止 Lidarr
2. 打开您喜欢的数据库管理工具并连接到 PostgreSQL 数据库实例
3. 运行以下命令：

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
DELETE FROM "MetadataProfiles";
```

4. 使用以下任一选项开始迁移：

    - ```bash
      pgloader --with "quote identifiers" --with "data only" lidarr.db 'postgresql://qstick:qstick@localhost/lidarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/lidarr.db:/lidarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /lidarr.db "postgresql://qstick:qstick@localhost/lidarr-main"
      ```

  > 如果使用 pgloader 时遇到错误，可能是因为您的数据库太大，尝试在上述命令中添加 `--with "prefetch rows = 100" --with "batch size = 1MB"` 以解决此问题
  {.is-warning}
  
  > 处理这些后，使用 `--with "data only"` 告诉它不要更改模式非常简单
  {.is-info}

5. 启动 Lidarr
6. 在数据库中执行以下查询。如果出现类似 ` Npgsql.PostgresException (0x80004005): 23505: duplicate key value violates unique constraint` 的错误，请执行以下查询：
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
注意：其中有两个是注释的，因为我找不到那些序列的 'source' 表。