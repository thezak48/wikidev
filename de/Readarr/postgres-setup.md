---
title: Readarr Konfiguration der PostgreSQL-Datenbank
description: Konfiguration von Readarr mit einer PostgreSQL-Datenbank
published: true
date: 2022-12-04T23:00:38.482Z
tags: 
editor: markdown
dateCreated: 2022-07-25T22:49:56.668Z
---

# Readarr und Postgres

Dieses Dokument erläutert die wichtigsten Punkte zur Migration und Einrichtung der Postgres-Unterstützung in Readarr.

> Readarr v0.1.1.1408 oder neuer erforderlich
{.is-info}

Dieser Leitfaden wurde von dem großartigen [Roxedus](https://github.com/Roxedus) erstellt.

> Postgres-Datenbanken werden von Readarr NICHT gesichert. Sicherungen müssen vom Benutzer implementiert und gewartet werden
{.is-danger}

## Einrichten von Postgres

Zunächst benötigen wir eine Postgres-Instanz. Dieser Leitfaden ist für die Verwendung des Docker-Images `postgres:14` geschrieben.

> Verwenden Sie auf keinen Fall das Tag `latest`! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=readarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Erstellung der Datenbank

Readarr benötigt drei Datenbanken, deren Standardnamen wie folgt lauten:

- `readarr-main`   Hier werden alle Konfigurationen und Verlaufsdaten gespeichert
- `readarr-log`    Hier werden Ereignisse gespeichert, die einen Protokolleintrag erzeugen
- `readarr-cache`    Hier wird der GoodReads-Cache gespeichert

> Readarr erstellt die Datenbanken nicht automatisch. Stellen Sie sicher, dass Sie sie im Voraus erstellen{.is-warning}

Erstellen Sie die oben genannten Datenbanken mit Ihrer bevorzugten Methode - zum Beispiel [pgAdmin](https://www.pgadmin.org/) oder [Adminer](https://www.adminer.org/).

Sie können den Datenbanken beliebige Namen geben, stellen Sie jedoch sicher, dass die Datei `config.xml` die korrekten Namen enthält. Weitere Informationen finden Sie unter [Schema-Erstellung](/readarr/postgres-setup#schema-creation).

### Schema-Erstellung

Wir müssen Readarr mitteilen, dass es Postgres verwenden soll. Die `config.xml` sollte bereits mit den erforderlichen Einträgen gefüllt sein:

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

Wenn Sie einen Datenbanknamen angeben möchten, sollten Sie auch die folgende Konfiguration hinzufügen:

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
<PostgresCacheDb>CacheDbName</PostgresCacheDb>
```

Erstellen Sie **nach der Erstellung** beider Datenbanken die Migration von SQLite nach Postgres.

## Datenmigration

> Wenn Sie keine vorhandene SQLite-Datenbank nach Postgres migrieren möchten, sind Sie mit diesem Leitfaden bereits fertig! {.is-info}

Zur Migration der Daten können wir [PGLoader](https://github.com/dimitri/pgloader) verwenden. Es gibt jedoch einige Dinge zu beachten:

- Standardmäßig sind Transaktionen nicht case-sensitive. Wir verwenden `--with "quote identifiers"`, um sie case-sensitive zu machen.
- Die in den apt-Repositories von Debian und Ubuntu gepackte Version ist für neuere Versionen von Postgres zu alt (Roxedus hat die Pakete in anderen Distributionen nicht getestet).
  Roxedus hat [ein Binärpaket](https://github.com/Roxedus/Pgloader-bin) erstellt, um diese Unterstützung zu ermöglichen (keine Code-Änderung war erforderlich, es musste nur mit aktualisierten Abhängigkeiten erstellt werden).

> Löschen Sie keine Tabellen in der Postgres-Instanz {.is-danger}

Vor dem Start einer Migration stellen Sie bitte sicher, dass Sie Readarr mindestens einmal erfolgreich gegen die erstellten Postgres-Datenbanken ausgeführt haben. Beginnen Sie die Migration, indem Sie Folgendes tun:

1. Stoppen Sie Readarr
1. Öffnen Sie Ihr bevorzugtes Datenbankverwaltungstool und stellen Sie eine Verbindung zur Postgres-Datenbankinstanz her
1. Führen Sie die folgenden Befehle aus:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "MetadataProfiles";
```

1. Starten Sie die Migration mit einer der folgenden Optionen:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" readarr.db 'postgresql://qstick:qstick@localhost/readarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/readarr.db:/readarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /readarr.db "postgresql://qstick:qstick@localhost/readarr-main"
      ```

> Wenn beim Verwenden von pgloader ein Fehler auftritt, kann dies daran liegen, dass Ihre Datenbank zu groß ist. Versuchen Sie in diesem Fall, `--with "prefetch rows = 100" --with "batch size = 1MB"` zu dem obigen Befehl hinzuzufügen {.is-warning}

> Nachdem Sie dies erledigt haben, ist es ziemlich einfach, indem Sie ihm sagen, dass er das Schema nicht ändern soll, indem Sie `--with "data only"` verwenden
{.is-info}

1. Starten Sie Readarr