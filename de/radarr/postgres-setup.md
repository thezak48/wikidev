---
title: Radarr Konfiguration mit PostgreSQL-Datenbank
description: Konfiguration von Radarr mit einer PostgreSQL-Datenbank
published: true
date: 2023-08-09T19:29:31.472Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:42:34.178Z
---

# Radarr und Postgres

Dieses Dokument behandelt die wichtigsten Punkte zur Migration und Einrichtung der Postgres-Unterstützung in Radarr.

> Radarr v4.1.0.6133 oder neuer erforderlich
{.is-info}

Dieser Leitfaden wurde von dem großartigen [Roxedus](https://github.com/Roxedus) erstellt.

> Postgres-Datenbanken werden von Radarr NICHT gesichert. Backups müssen vom Benutzer implementiert und gewartet werden
{.is-danger}

## Einrichtung von Postgres

Zunächst benötigen wir eine Postgres-Instanz. Dieser Leitfaden ist für die Verwendung des Docker-Images `postgres:14` geschrieben.

> Verwenden Sie auf keinen Fall das Tag `latest`! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=radarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Erstellung der Datenbank

Radarr benötigt zwei Datenbanken, deren Standardnamen wie folgt lauten:

- `radarr-main`   Hier werden alle Konfigurationen und Verlaufsdaten gespeichert
- `radarr-log`    Hier werden Ereignisse gespeichert, die zu einem Logeintrag führen

> Radarr erstellt die Datenbanken nicht automatisch. Stellen Sie sicher, dass Sie sie im Voraus erstellen{.is-warning}

Erstellen Sie die oben genannten Datenbanken mit Ihrer bevorzugten Methode - zum Beispiel [pgAdmin](https://www.pgadmin.org/) oder [Adminer](https://www.adminer.org/).

Sie können den Datenbanken beliebige Namen geben, stellen Sie jedoch sicher, dass die Datei `config.xml` die korrekten Namen enthält. Weitere Informationen finden Sie unter [Schema-Erstellung](/radarr/postgres-setup#schema-creation).

### Schema-Erstellung

Wir müssen Radarr mitteilen, dass es Postgres verwenden soll. Die `config.xml` sollte bereits mit den erforderlichen Einträgen gefüllt sein:

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
```

Erstellen Sie die beiden Datenbanken **nachdem** Sie sie erstellt haben, können Sie mit der Migration von Radarr von SQLite zu Postgres beginnen.

## Datenmigration

> Wenn Sie keine vorhandene SQLite-Datenbank zu Postgres migrieren möchten, sind Sie mit diesem Leitfaden bereits fertig! {.is-info}

Zur Migration der Daten können wir [PGLoader](https://github.com/dimitri/pgloader) verwenden. Es gibt jedoch einige Dinge zu beachten:

- Standardmäßig sind Transaktionen nicht case-sensitive. Wir verwenden `--with "quote identifiers"`, um sie case-sensitive zu machen.
- Die in den Debian- und Ubuntu-Apt-Repositories enthaltenen Versionen sind für neuere Versionen von Postgres zu alt (Roxedus hat die Pakete in anderen Distributionen nicht getestet).
  Roxedus hat [ein Binärpaket](https://github.com/Roxedus/Pgloader-bin) erstellt, um diese Unterstützung zu ermöglichen (keine Code-Änderungen waren erforderlich, es musste nur mit aktualisierten Abhängigkeiten erstellt werden).

> Löschen Sie keine Tabellen in der Postgres-Instanz {.is-danger}

Bevor Sie mit der Migration beginnen, stellen Sie bitte sicher, dass Sie Radarr mindestens einmal erfolgreich gegen die erstellten Postgres-Datenbanken ausgeführt haben. Führen Sie die Migration wie folgt durch:

1. Stoppen Sie Radarr.
1. Öffnen Sie Ihr bevorzugtes Datenbankverwaltungstool und stellen Sie eine Verbindung zur Postgres-Datenbankinstanz her.
1. Führen Sie die folgenden Befehle aus:

```SQL
DELETE FROM "Profiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. Starten Sie die Migration mit einer der folgenden Optionen:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" radarr.db 'postgresql://qstick:qstick@localhost/radarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/radarr.db:/radarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /radarr.db "postgresql://qstick:qstick@localhost/radarr-main"
      ```

  > Wenn bei der Verwendung von pgloader ein Fehler auftritt, kann dies daran liegen, dass Ihre Datenbank zu groß ist. Versuchen Sie in diesem Fall, `--with "prefetch rows = 100" --with "batch size = 1MB"` zu dem obigen Befehl hinzuzufügen, um das Problem zu beheben
  {.is-warning}

  > Nachdem Sie dies erledigt haben, ist es ziemlich einfach, indem Sie es einfach auffordern, das Schema nicht zu ändern, indem Sie `--with "data only"` verwenden
  {.is-info}


2. Starten Sie Radarr.

3. Für diejenigen, bei denen nach der Migration von SQLite Probleme beim Hinzufügen von Filmen auftreten, führen Sie Folgendes aus:
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