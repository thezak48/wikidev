---
title: Readarr配置PostgreSQL数据库
description: 使用PostgreSQL配置Readarr
published: true
date: 2022-12-04T23:00:38.482Z
tags: 
editor: markdown
dateCreated: 2022-07-25T22:49:56.668Z
---

# Readarr和PostgreSQL

本文档将介绍在Readarr中迁移和设置PostgreSQL支持的关键要点。

> 需要Readarr v0.1.1.1408或更高版本
{.is-info}

本指南由令人惊叹的[Roxedus](https://github.com/Roxedus)创建。

> Readarr不会备份PostgreSQL数据库，任何备份必须由用户自行实施和维护
{.is-danger}

## 设置PostgreSQL

首先，我们需要一个PostgreSQL实例。本指南是针对使用`postgres:14` Docker镜像的情况编写的。

> 切勿考虑使用`latest`标签！{.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=readarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## 创建数据库

Readarr需要三个数据库，这些数据库的默认名称如下：

- `readarr-main`   用于存储所有配置和历史记录
- `readarr-log`    用于存储生成日志条目的事件
- `readarr-cache`    用于存储GoodReads缓存

> Readarr不会为您创建这些数据库。请确保提前创建它们{.is-warning}

使用您喜欢的方法（例如[pgAdmin](https://www.pgadmin.org/)或[Adminer](https://www.adminer.org/)）创建上述数据库。

您可以为数据库指定任何名称，但请确保`config.xml`文件中有正确的名称。有关更多信息，请参阅[schema creation](/readarr/postgres-setup#schema-creation)。

### 创建模式

我们需要告诉Readarr使用PostgreSQL。`config.xml`应该已经填充了我们需要的条目：

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
<PostgresCacheDb>CacheDbName</PostgresCacheDb>
```

只有在创建了这两个数据库之后，您才可以开始从SQLite迁移到PostgreSQL的Readarr迁移。

## 迁移数据

> 如果您不想将现有的SQLite数据库迁移到PostgreSQL，则此指南已经完成！{.is-info}

要迁移数据，我们可以使用[PGLoader](https://github.com/dimitri/pgloader)。但是，它有一些注意事项：

- 默认情况下，事务是不区分大小写的，我们使用`--with "quote identifiers"`使其区分大小写。
- Debian和Ubuntu的apt仓库中打包的版本对于较新版本的PostgreSQL来说太旧（Roxedus尚未在其他发行版中测试过软件包）。
  Roxedus [构建了一个二进制文件](https://github.com/Roxedus/Pgloader-bin)以启用此支持（无需修改代码，只需使用更新的依赖项进行构建）。

> 不要删除PostgreSQL实例中的任何表格{.is-danger}

在开始迁移之前，请确保您已经成功地将Readarr运行在创建的PostgreSQL数据库上**至少一次**。按照以下步骤开始迁移：

1. 停止Readarr
1. 打开您喜欢的数据库管理工具并连接到PostgreSQL数据库实例
1. 运行以下命令：

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "MetadataProfiles";
```

1. 使用以下任一选项开始迁移：

    - ```bash
      pgloader --with "quote identifiers" --with "data only" readarr.db 'postgresql://qstick:qstick@localhost/readarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/readarr.db:/readarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /readarr.db "postgresql://qstick:qstick@localhost/readarr-main"
      ```

> 如果使用pgloader时遇到错误，可能是由于您的数据库太大，为解决此问题，请尝试将`--with "prefetch rows = 100" --with "batch size = 1MB"`添加到上述命令中{.is-warning}

> 处理这些后，告诉它不要更改模式，使用`--with "data only"`非常简单
{.is-info}

1. 启动Readarr