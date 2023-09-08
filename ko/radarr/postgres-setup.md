---
title: Radarr PostgreSQL 데이터베이스 구성
description: Radarr를 PostgreSQL 데이터베이스와 함께 구성하는 방법
published: true
date: 2023-08-09T19:29:31.472Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:42:34.178Z
---

# Radarr와 Postgres

이 문서에서는 Radarr에서 Postgres 지원을 마이그레이션하고 설정하는 주요 사항을 다룹니다.

> Radarr v4.1.0.6133 이상이 필요합니다
{.is-info}

이 가이드는 놀라운 [Roxedus](https://github.com/Roxedus)에 의해 작성되었습니다.

> Radarr에서는 Postgres 데이터베이스를 백업하지 않습니다. 백업은 사용자가 직접 구현하고 유지해야 합니다
{.is-danger}

## Postgres 설정

먼저, Postgres 인스턴스가 필요합니다. 이 가이드는 `postgres:14` Docker 이미지를 사용하는 것으로 작성되었습니다.

> `latest` 태그를 사용하려고 하지 마십시오! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=radarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## 데이터베이스 생성

Radarr는 두 개의 데이터베이스가 필요합니다. 이들의 기본 이름은 다음과 같습니다:

- `radarr-main`: 모든 구성 및 이력을 저장하는 데 사용됩니다.
- `radarr-log`: 로그 항목을 생성하는 이벤트를 저장하는 데 사용됩니다.

> Radarr는 데이터베이스를 자동으로 생성하지 않습니다. 미리 생성해야 합니다{.is-warning}

위에서 언급한 데이터베이스를 원하는 방법으로 생성하십시오. 예를 들어 [pgAdmin](https://www.pgadmin.org/)이나 [Adminer](https://www.adminer.org/)를 사용할 수 있습니다.

데이터베이스의 이름은 원하는 대로 지정할 수 있지만, `config.xml` 파일에 올바른 이름이 있는지 확인하십시오. 자세한 내용은 [스키마 생성](/radarr/postgres-setup#schema-creation)을 참조하십시오.

### 스키마 생성

Radarr에게 Postgres를 사용하도록 알려주어야 합니다. `config.xml`은 이미 필요한 항목으로 채워져 있어야 합니다:

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

데이터베이스 이름을 지정하려면 다음 구성도 포함해야 합니다:

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

두 데이터베이스를 **생성한 후에만** SQLite에서 Postgres로의 Radarr 마이그레이션을 시작할 수 있습니다.

## 데이터 마이그레이션

> 기존의 SQLite 데이터베이스를 Postgres로 마이그레이션하고 싶지 않다면, 이미 이 가이드로 완료되었습니다! {.is-info}

데이터를 마이그레이션하기 위해 [PGLoader](https://github.com/dimitri/pgloader)를 사용할 수 있습니다. 그러나 몇 가지 주의 사항이 있습니다:

- 기본적으로 트랜잭션은 대소문자를 구분하지 않습니다. `--with "quote identifiers"`를 사용하여 대소문자를 구분하도록 설정합니다.
- Debian 및 Ubuntu의 apt 저장소에 포장된 버전은 최신 버전의 Postgres에는 너무 오래되었습니다 (Roxedus는 다른 배포판의 패키지를 테스트하지 않았습니다).
  Roxedus는 이 지원을 활성화하기 위해 [바이너리](https://github.com/Roxedus/Pgloader-bin)를 빌드했습니다 (코드 수정이 필요하지 않았으며, 업데이트된 종속성으로 빌드하기만 하면 됩니다).

> Postgres 인스턴스에서 어떤 테이블도 삭제하지 마십시오 {.is-danger}

마이그레이션을 시작하기 전에 Radarr를 생성한 Postgres 데이터베이스에 대해 **적어도 한 번** 성공적으로 실행했는지 확인하십시오. 다음을 수행하여 마이그레이션을 시작합니다:

1. Radarr를 중지합니다.
1. 선호하는 데이터베이스 관리 도구를 열고 Postgres 데이터베이스 인스턴스에 연결합니다.
1. 다음 명령을 실행합니다:

```SQL
DELETE FROM "Profiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. 다음 옵션 중 하나를 사용하여 마이그레이션을 시작합니다:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" radarr.db 'postgresql://qstick:qstick@localhost/radarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/radarr.db:/radarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /radarr.db "postgresql://qstick:qstick@localhost/radarr-main"
      ```

  > pgloader를 사용할 때 오류가 발생하는 경우 DB가 너무 큰 경우일 수 있습니다. 이 경우 위의 명령에 `--with "prefetch rows = 100" --with "batch size = 1MB"`를 추가하여 해결할 수 있습니다
  {.is-warning}

  > 이러한 작업을 수행한 후에는 `--with "data only"`를 사용하여 스키마를 변경하지 않도록 지정하면 됩니다
  {.is-info}


2. Radarr를 시작합니다.

3. SQLite에서 마이그레이션 이후에 영화를 추가하는 문제가 있는 경우 다음을 실행합니다:
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