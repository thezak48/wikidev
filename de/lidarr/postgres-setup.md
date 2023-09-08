---
title: Lidarr Konfiguration der PostgreSQL-Datenbank
description: Konfiguration von Lidarr mit einer PostgreSQL-Datenbank
published: true
date: 2023-09-03T17:21:21.279Z
tags: 
editor: markdown
dateCreated: 2022-11-25T01:35:56.796Z
---

# Lidarr und Postgres

Dieses Dokument behandelt die wichtigsten Punkte zur Migration und Einrichtung von Postgres-Unterstützung in Lidarr.

> Lidarr v1.1.2.2890 oder neuer erforderlich
{.is-info}

Dieser Leitfaden wurde von dem großartigen [Roxedus](https://github.com/Roxedus) erstellt.

> Postgres-Datenbanken werden von Lidarr NICHT gesichert. Alle Backups müssen vom Benutzer implementiert und gewartet werden
{.is-danger}

## Einrichten von Postgres

Zunächst benötigen wir eine Postgres-Instanz. Dieser Leitfaden ist für die Verwendung des Docker-Images `postgres:14` geschrieben.

> Verwenden Sie auf keinen Fall das Tag `latest`! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=lidarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Erstellung der Datenbank

Lidarr benötigt zwei Datenbanken, deren Standardnamen sind:

- `lidarr-main`   Hier werden alle Konfigurationen und Verlaufsdaten gespeichert
- `lidarr-log`    Hier werden Ereignisse gespeichert, die zu einem Protokolleintrag führen

> Lidarr erstellt die Datenbanken nicht automatisch für Sie. Stellen Sie sicher, dass Sie sie im Voraus erstellen{.is-warning}

Erstellen Sie die oben genannten Datenbanken mit Ihrer bevorzugten Methode - zum Beispiel [pgAdmin](https://www.pgadmin.org/) oder [Adminer](https://www.adminer.org/).

Sie können den Datenbanken beliebige Namen geben, stellen Sie jedoch sicher, dass die Datei `config.xml` die korrekten Namen enthält. Weitere Informationen finden Sie unter [Schemaerstellung](/lidarr/postgres-setup#schema-creation).

### Schemaerstellung

Wir müssen Lidarr mitteilen, dass es Postgres verwenden soll. Die `config.xml` sollte bereits mit den erforderlichen Einträgen gefüllt sein:

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

Erst **nachdem** Sie beide Datenbanken erstellt haben, können Sie mit der Lidarr-Migration von SQLite nach Postgres beginnen.

## Datenmigration

> Wenn Sie keine vorhandene SQLite-Datenbank nach Postgres migrieren möchten, sind Sie mit diesem Leitfaden bereits fertig! {.is-info}

Zur Migration der Daten können wir [PGLoader](https://github.com/dimitri/pgloader) verwenden. Es gibt jedoch einige Dinge zu beachten:

- Standardmäßig sind Transaktionen nicht case-sensitive. Wir verwenden `--with "quote identifiers"`, um sie case-sensitive zu machen.
- Die in den apt-Repositories von Debian und Ubuntu gepackte Version ist für neuere Versionen von Postgres zu alt (Roxedus hat die Pakete in anderen Distributionen nicht getestet).
  Roxedus hat [ein Binärpaket erstellt](https://github.com/Roxedus/Pgloader-bin), um diese Unterstützung zu ermöglichen (keine Code-Änderung war erforderlich, es musste nur mit aktualisierten Abhängigkeiten erstellt werden).

> Löschen Sie keine Tabellen in der Postgres-Instanz {.is-danger}

Bevor Sie mit einer Migration beginnen, stellen Sie bitte sicher, dass Sie Lidarr bereits erfolgreich gegen die erstellten Postgres-Datenbanken ausgeführt haben. Beginnen Sie die Migration, indem Sie Folgendes tun:

1. Stoppen Sie Lidarr
1. Öffnen Sie Ihr bevorzugtes Datenbankverwaltungstool und stellen Sie eine Verbindung zur Postgres-Datenbankinstanz her
1. Führen Sie die folgenden Befehle aus:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
DELETE FROM "MetadataProfiles";
```

1. Starten Sie die Migration mit einer der folgenden Optionen:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" lidarr.db 'postgresql://qstick:qstick@localhost/lidarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/lidarr.db:/lidarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /lidarr.db "postgresql://qstick:qstick@localhost/lidarr-main"
      ```

  > Wenn bei der Verwendung von pgloader ein Fehler auftritt, kann dies daran liegen, dass Ihre Datenbank zu groß ist. Versuchen Sie in diesem Fall, `--with "prefetch rows = 100" --with "batch size = 1MB"` zu dem obigen Befehl hinzuzufügen, um das Problem zu beheben
  {.is-warning}
  
  > Nachdem Sie dies erledigt haben, ist es ziemlich einfach, indem Sie ihm sagen, dass er das Schema nicht ändern soll, indem Sie `--with "data only"` verwenden
  {.is-info}

1. Starten Sie Lidarr
2. Führen Sie die folgenden Abfragen in der Datenbank aus. Wenn Sie Fehler wie `Npgsql.PostgresException (0x80004005): 23505: duplicate key value violates unique constraint` erhalten:
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
Hinweis: Es gibt zwei auskommentierte Zeilen, da ich die 'source'-Tabelle für diese Sequenzen nicht finden konnte.