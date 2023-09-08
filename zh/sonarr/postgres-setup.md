---
title: Sonarr配置PostgreSQL数据库
description: 配置Sonarr与PostgreSQL数据库
published: true
date: 2023-08-21T19:37:53.766Z
tags: 
editor: markdown
dateCreated: 2023-08-12T12:26:25.094Z
---

# Sonarr和PostgreSQL

本文档将介绍在Sonarr中迁移和设置PostgreSQL支持的关键要点。

> 需要Sonarr v4.0.0.615或更高版本
{.is-info}

此指南由了不起的[Roxedus](https://github.com/Roxedus)创建。

> Sonarr不会备份Postgres数据库，任何备份必须由用户自行实施和维护
{.is-danger}

## 设置PostgreSQL

首先，我们需要一个PostgreSQL实例。本指南是针对使用`postgres:14` Docker镜像的情况编写的。

> 切勿考虑使用`latest`标签！{.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=sonarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## 创建数据库

Sonarr需要两个数据库，这些数据库的默认名称如下：

- `sonarr-main`   用于存储所有配置和历史记录
- `sonarr-log`    用于存储生成日志条目的事件

> Sonarr不会为您创建数据库。请确保提前创建它们{.is-warning}

使用您喜欢的方法（例如[pgAdmin](https://www.pgadmin.org/)或[Adminer](https://www.adminer.org/)）创建上述数据库。

您可以为数据库指定任何名称，但请确保`config.xml`文件中有正确的名称。有关更多信息，请参阅[模式创建](/sonarr/postgres-setup#schema-creation)。

### 模式创建

我们需要告诉Sonarr使用PostgreSQL。`config.xml`应该已经填充了我们需要的条目：

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

只有在创建了这两个数据库之后，您才可以开始从SQLite迁移到PostgreSQL的Sonarr迁移。

## 迁移数据

> 如果您不想将现有的SQLite数据库迁移到PostgreSQL，则此指南已经完成！{.is-info}

要迁移数据，我们可以使用[PGLoader](https://github.com/dimitri/pgloader)。但是，它有一些注意事项：

- 默认情况下，事务是不区分大小写的，我们使用`--with "quote identifiers"`使其区分大小写。
- Debian和Ubuntu的apt仓库中打包的版本对于较新版本的Postgres来说太旧（Roxedus尚未测试其他发行版中的软件包）。
  Roxedus [构建了一个二进制文件](https://github.com/Roxedus/Pgloader-bin)以启用此支持（无需修改代码，只需使用更新的依赖项进行构建）。

> 不要删除Postgres实例中的任何表 {.is-danger}

在开始迁移之前，请确保您已经成功地使用创建的Postgres数据库运行了至少一次Sonarr。按照以下步骤开始迁移：

1. 停止Sonarr
1. 打开您喜欢的数据库管理工具并连接到Postgres数据库实例
1. 运行以下命令：

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. 使用以下任一选项开始迁移：

    - ```bash
      pgloader --with "quote identifiers" --with "data only" sonarr.db 'postgresql://qstick:qstick@localhost/sonarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/sonarr.db:/sonarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /sonarr.db "postgresql://qstick:qstick@localhost/sonarr-main"
      ```

  > 如果使用pgloader时遇到错误，可能是由于您的数据库太大，可以尝试在上述命令中添加`--with "prefetch rows = 100" --with "batch size = 1MB"`来解决此问题
  {.is-warning}

  > 处理这些后，使用`--with "data only"`告诉它不要修改模式就很简单了
  {.is-info}


2. 启动Sonarr


3. 对于那些在从SQLite迁移后添加系列或在日志中出现错误的人，请运行以下命令：
```SQL
select setval('public."AutoTagging_Id_seq"',(SELECT MAX("Id")+1 FROM "AutoTagging"));
select setval('public."Blacklist_Id_seq"',(SELECT MAX("Id")+1 FROM "Blocklist"));
select setval('public."Commands_Id_seq"',(SELECT MAX("Id")+1 FROM "Commands"));
select setval('public."Config_Id_seq"',(SELECT MAX("Id")+1 FROM "Config"));
select setval('public."CustomFilters_Id_seq"',(SELECT MAX("Id")+1 FROM "CustomFilters"));
select setval('public."CustomFormats_Id_seq"',(SELECT MAX("Id")+1 FROM "CustomFormats"));
select setval('public."DelayProfiles_Id_seq"',(SELECT MAX("Id")+1 FROM "DelayProfiles"));
select setval('public."DownloadClientStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "DownloadClientStatus"));
select setval('public."DownloadClients_Id_seq"',(SELECT MAX("Id")+1 FROM "DownloadClients"));
select setval('public."DownloadHistory_Id_seq"',(SELECT MAX("Id")+1 FROM "DownloadHistory"));
select setval('public."EpisodeFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "EpisodeFiles"));
select setval('public."Episodes_Id_seq"',(SELECT MAX("Id")+1 FROM "Episodes"));
select setval('public."ExtraFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "ExtraFiles"));
select setval('public."History_Id_seq"',(SELECT MAX("Id")+1 FROM "History"));
select setval('public."ImportListExclusions_Id_seq"',(SELECT MAX("Id")+1 FROM "ImportListExclusions"));
select setval('public."ImportListStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "ImportListStatus"));
select setval('public."ImportLists_Id_seq"',(SELECT MAX("Id")+1 FROM "ImportLists"));
select setval('public."IndexerStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "IndexerStatus"));
select setval('public."Indexers_Id_seq"',(SELECT MAX("Id")+1 FROM "Indexers"));
select setval('public."MetadataFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "MetadataFiles"));
select setval('public."Metadata_Id_seq"',(SELECT MAX("Id")+1 FROM "Metadata"));
select setval('public."NamingConfig_Id_seq"',(SELECT MAX("Id")+1 FROM "NamingConfig"));
select setval('public."NotificationStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "NotificationStatus"));
select setval('public."Notifications_Id_seq"',(SELECT MAX("Id")+1 FROM "Notifications"));
select setval('public."PendingReleases_Id_seq"',(SELECT MAX("Id")+1 FROM "PendingReleases"));
select setval('public."QualityDefinitions_Id_seq"',(SELECT MAX("Id")+1 FROM "QualityDefinitions"));
select setval('public."QualityProfiles_Id_seq"',(SELECT MAX("Id")+1 FROM "QualityProfiles"));
select setval('public."RemotePathMappings_Id_seq"',(SELECT MAX("Id")+1 FROM "RemotePathMappings"));
select setval('public."Restrictions_Id_seq"',(SELECT MAX("Id")+1 FROM "Restrictions"));
select setval('public."RootFolders_Id_seq"',(SELECT MAX("Id")+1 FROM "RootFolders"));
select setval('public."SceneMappings_Id_seq"',(SELECT MAX("Id")+1 FROM "SceneMappings"));
select setval('public."ScheduledTasks_Id_seq"',(SELECT MAX("Id")+1 FROM "ScheduledTasks"));
select setval('public."Series_Id_seq"',(SELECT MAX("Id")+1 FROM "Series"));
select setval('public."SubtitleFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "SubtitleFiles"));
select setval('public."Tags_Id_seq"',(SELECT MAX("Id")+1 FROM "Tags"));
select setval('public."Users_Id_seq"',(SELECT MAX("Id")+1 FROM "Users"));
```
