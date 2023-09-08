---
title: Readarr PostgreSQL 데이터베이스 설정
description: Readarr를 PostgreSQL 데이터베이스와 함께 설정하는 방법
published: true
date: 2022-12-04T23:00:38.482Z
tags: 
editor: markdown
dateCreated: 2022-07-25T22:49:56.668Z
---

# Readarr와 Postgres

이 문서에서는 Readarr에서 Postgres 지원을 마이그레이션하고 설정하는 주요 사항을 다룹니다.

> Readarr v0.1.1.1408 이상이 필요합니다
{.is-info}

이 가이드는 놀라운 [Roxedus](https://github.com/Roxedus)에 의해 작성되었습니다.

> Readarr는 Postgres 데이터베이스를 백업하지 않습니다. 백업은 사용자가 직접 구현하고 유지해야 합니다
{.is-danger}

## Postgres 설정하기

먼저, Postgres 인스턴스가 필요합니다. 이 가이드는 `postgres:14` Docker 이미지를 사용하는 것으로 작성되었습니다.

> `latest` 태그를 사용하려고 하지 마세요! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=readarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## 데이터베이스 생성

Readarr는 세 개의 데이터베이스가 필요합니다. 이들의 기본 이름은 다음과 같습니다:

- `readarr-main`: 모든 구성 및 이력을 저장하는 데 사용됩니다.
- `readarr-log`: 로그 항목을 생성하는 이벤트를 저장하는 데 사용됩니다.
- `readarr-cache`: GoodReads 캐시를 저장하는 데 사용됩니다.

> Readarr는 데이터베이스를 자동으로 생성하지 않습니다. 미리 생성해야 합니다{.is-warning}

위에서 언급한 데이터베이스를 원하는 방법으로 생성하세요. 예를 들어 [pgAdmin](https://www.pgadmin.org/)이나 [Adminer](https://www.adminer.org/)를 사용할 수 있습니다.

데이터베이스에 원하는 이름을 지정할 수 있지만, `config.xml` 파일에 올바른 이름이 있는지 확인하세요. 자세한 내용은 [스키마 생성](/readarr/postgres-setup#schema-creation)을 참조하세요.

### 스키마 생성

Readarr에게 Postgres를 사용하도록 알려주어야 합니다. `config.xml`에 이미 필요한 항목이 채워져 있어야 합니다:

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
<PostgresCacheDb>CacheDbName</PostgresCacheDb>
```

두 데이터베이스를 **생성한 후에만** SQLite에서 Postgres로의 Readarr 마이그레이션을 시작할 수 있습니다.

## 데이터 마이그레이션

> 기존의 SQLite 데이터베이스를 Postgres로 마이그레이션하고 싶지 않다면, 이미 이 가이드로 완료되었습니다! {.is-info}

데이터를 마이그레이션하기 위해 [PGLoader](https://github.com/dimitri/pgloader)를 사용할 수 있습니다. 그러나 몇 가지 주의 사항이 있습니다:

- 기본적으로 트랜잭션은 대소문자를 구분하지 않습니다. `--with "quote identifiers"`를 사용하여 대소문자를 구분하도록 설정합니다.
- Debian 및 Ubuntu의 apt 저장소에 포장된 버전은 더 최신 버전의 Postgres에서 사용하기에는 너무 오래되었습니다 (Roxedus는 다른 배포판에서 패키지를 테스트하지 않았습니다).
  Roxedus는 이 지원을 활성화하기 위해 [바이너리](https://github.com/Roxedus/Pgloader-bin)를 빌드했습니다 (코드 수정이 필요하지 않았으며, 업데이트된 종속성으로 빌드되기만 하면 됩니다).

> Postgres 인스턴스에서 어떤 테이블도 삭제하지 마세요 {.is-danger}

마이그레이션을 시작하기 전에, Readarr를 생성한 Postgres 데이터베이스에 대해 **적어도 한 번** 성공적으로 실행했는지 확인하세요. 다음을 수행하여 마이그레이션을 시작하세요:

1. Readarr를 중지하세요.
1. 선호하는 데이터베이스 관리 도구를 열고 Postgres 데이터베이스 인스턴스에 연결하세요.
1. 다음 명령을 실행하세요:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "MetadataProfiles";
```

1. 다음 옵션 중 하나를 사용하여 마이그레이션을 시작하세요:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" readarr.db 'postgresql://qstick:qstick@localhost/readarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/readarr.db:/readarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /readarr.db "postgresql://qstick:qstick@localhost/readarr-main"
      ```

> pgloader를 사용할 때 오류가 발생하는 경우, DB가 너무 큰 경우일 수 있습니다. 이 경우 위 명령에 `--with "prefetch rows = 100" --with "batch size = 1MB"`를 추가하여 해결할 수 있습니다 {.is-warning}

> 이를 처리한 후에는 `--with "data only"`를 사용하여 스키마를 변경하지 않도록 지정하면 됩니다
{.is-info}

1. Readarr를 시작하세요.