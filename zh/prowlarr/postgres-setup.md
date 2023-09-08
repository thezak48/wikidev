---
title: Prowlarr 配置 PostgreSQL 数据库
description: 使用 PostgreSQL 配置 Prowlarr
published: true
date: 2022-11-29T13:19:38.953Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:38:53.538Z
---

# Prowlarr 和 PostgreSQL

本文档将介绍在 Prowlarr 中迁移和设置 PostgreSQL 支持的关键要点。

本指南由令人惊叹的 [Roxedus](https://github.com/Roxedus) 创建。

> Prowlarr 不会备份 PostgreSQL 数据库，任何备份必须由用户自行实施和维护
{.is-danger}

## 设置 PostgreSQL

首先，我们需要一个 PostgreSQL 实例。本指南是针对使用 `postgres:14` Docker 镜像编写的。

> 切勿考虑使用 `latest` 标签！{.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=prowlarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## 创建数据库

Prowlarr 需要两个数据库，它们的默认名称如下：

- `prowlarr-main`：用于存储所有配置和历史记录
- `prowlarr-log`：用于存储生成日志条目的事件

> Prowlarr 不会为您创建这些数据库。请确保您提前创建它们{.is-warning}

使用您喜欢的方法创建上述数据库，例如 [pgAdmin](https://www.pgadmin.org/) 或 [Adminer](https://www.adminer.org/)。

> 为了使 `Housekeeping` 任务运行，此用户必须是超级用户，因为它执行了 vacuum 任务{.is-info}

您可以为数据库指定任何名称，但请确保 `config.xml` 文件中具有正确的名称。有关更多信息，请参阅 [模式创建](/prowlarr/postgres-setup#schema-creation)。

### 模式创建

我们需要告诉 Prowlarr 使用 PostgreSQL。`config.xml` 应该已经填充了我们需要的条目：

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

只有在创建了这两个数据库之后，您才可以开始从 SQLite 迁移到 PostgreSQL 的 Prowlarr 迁移。

## 迁移数据

> 如果您不想将现有的 SQLite 数据库迁移到 PostgreSQL，则已经完成了本指南！{.is-info}

要迁移数据，我们可以使用 [PGLoader](https://github.com/dimitri/pgloader)。但是，它有一些注意事项：

- 默认情况下，事务是不区分大小写的，我们使用 `--with "quote identifiers"` 使其区分大小写。
- Debian 和 Ubuntu 的 apt 存储库中打包的版本对于较新版本的 PostgreSQL 来说太旧（Roxedus 尚未在其他发行版中测试过软件包）。
  Roxedus [构建了一个二进制文件](https://github.com/Roxedus/Pgloader-bin) 来支持此功能（无需修改代码，只需使用更新的依赖项进行构建）。

> 不要删除 Postgres 实例中的任何表 {.is-danger}

在开始迁移之前，请确保您已经成功地将 Prowlarr 运行在创建的 PostgreSQL 数据库上**至少一次**。按照以下步骤开始迁移：

1. 停止 Prowlarr
1. 打开您喜欢的数据库管理工具并连接到 PostgreSQL 数据库实例
1. 使用以下任一选项开始迁移：

    - ```bash
      pgloader --with "quote identifiers" --with "data only" prowlarr.db 'postgresql://qstick:qstick@localhost/prowlarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/prowlarr.db:/prowlarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /prowlarr.db "postgresql://qstick:qstick@localhost/prowlarr-main"
      ```

  > 如果使用 pgloader 时遇到错误，可能是因为您的数据库太大，解决此问题，请尝试将 `--with "prefetch rows = 100" --with "batch size = 1MB"` 添加到上述命令中
  {.is-warning}

  > 在告诉它不要修改方案的情况下，使用 `--with "data only"` 处理起来非常简单
  {.is-info}

1. 启动 Prowlarr