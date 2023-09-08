---
title: Sonarr Konfiguration mit PostgreSQL-Datenbank
description: Konfiguration von Sonarr mit einer PostgreSQL-Datenbank
published: true
date: 2023-08-21T19:37:53.766Z
tags: 
editor: markdown
dateCreated: 2023-08-12T12:26:25.094Z
---

# Sonarr und Postgres

Dieses Dokument behandelt die wichtigsten Punkte zur Migration und Einrichtung von Postgres-Unterstützung in Sonarr.

> Sonarr v4.0.0.615 oder neuer erforderlich
{.is-info}

Dieser Leitfaden wurde von dem großartigen [Roxedus](https://github.com/Roxedus) erstellt.

> Postgres-Datenbanken werden von Sonarr NICHT gesichert. Backups müssen vom Benutzer implementiert und gewartet werden
{.is-danger}

## Einrichtung von Postgres

Zunächst benötigen wir eine Postgres-Instanz. Dieser Leitfaden ist für die Verwendung des Docker-Images `postgres:14` geschrieben.

> Verwenden Sie auf keinen Fall das Tag `latest`! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=sonarr-main \
    -p 5432:5432/tcp \
    -v /Pfad/zum/AppData/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Erstellung der Datenbank

Sonarr benötigt zwei Datenbanken, deren Standardnamen wie folgt lauten:

- `sonarr-main`   Hier werden alle Konfigurationen und Verlaufsdaten gespeichert
- `sonarr-log`    Hier werden Ereignisse gespeichert, die zu einem Logeintrag führen

> Sonarr erstellt die Datenbanken nicht automatisch. Stellen Sie sicher, dass Sie sie im Voraus erstellen{.is-warning}

Erstellen Sie die oben genannten Datenbanken mit Ihrer bevorzugten Methode - zum Beispiel [pgAdmin](https://www.pgadmin.org/) oder [Adminer](https://www.adminer.org/).

Sie können den Datenbanken beliebige Namen geben, stellen Sie jedoch sicher, dass die Datei `config.xml` die korrekten Namen enthält. Weitere Informationen finden Sie unter [Schema-Erstellung](/sonarr/postgres-setup#schema-creation).

### Schema-Erstellung

Wir müssen Sonarr mitteilen, dass es Postgres verwenden soll. Die `config.xml` sollte bereits mit den erforderlichen Einträgen gefüllt sein:

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

Erst **nachdem** Sie beide Datenbanken erstellt haben, können Sie mit der Sonarr-Migration von SQLite zu Postgres beginnen.

## Datenmigration

> Wenn Sie keine vorhandene SQLite-Datenbank zu Postgres migrieren möchten, sind Sie mit diesem Leitfaden bereits fertig! {.is-info}

Zur Migration der Daten können wir [PGLoader](https://github.com/dimitri/pgloader) verwenden. Es gibt jedoch einige Dinge zu beachten:

- Standardmäßig sind Transaktionen nicht case-sensitive. Wir verwenden `--with "quote identifiers"`, um sie case-sensitive zu machen.
- Die in den apt-Repositories von Debian und Ubuntu gepackte Version ist für neuere Versionen von Postgres zu alt (Roxedus hat die Pakete in anderen Distributionen nicht getestet).
  Roxedus hat [ein Binärpaket](https://github.com/Roxedus/Pgloader-bin) erstellt, um diese Unterstützung zu ermöglichen (keine Code-Änderung war erforderlich, es musste nur mit aktualisierten Abhängigkeiten erstellt werden).

> Löschen Sie keine Tabellen in der Postgres-Instanz {.is-danger}

Stellen Sie vor dem Start einer Migration bitte sicher, dass Sie Sonarr mindestens einmal erfolgreich gegen die erstellten Postgres-Datenbanken ausgeführt haben. Beginnen Sie die Migration, indem Sie Folgendes tun:

1. Stoppen Sie Sonarr
1. Öffnen Sie Ihr bevorzugtes Datenbankverwaltungstool und stellen Sie eine Verbindung zur Postgres-Datenbankinstanz her
1. Führen Sie die folgenden Befehle aus:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. Starten Sie die Migration mit einer der folgenden Optionen:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" sonarr.db 'postgresql://qstick:qstick@localhost/sonarr-main'
      ```

    - ```bash
      docker run --rm -v /absoluter/Pfad/zur/sonarr.db:/sonarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /sonarr.db "postgresql://qstick:qstick@localhost/sonarr-main"
      ```

  > Wenn bei der Verwendung von pgloader ein Fehler auftritt, kann dies daran liegen, dass Ihre Datenbank zu groß ist. Versuchen Sie in diesem Fall, `--with "prefetch rows = 100" --with "batch size = 1MB"` zu dem obigen Befehl hinzuzufügen, um das Problem zu beheben
  {.is-warning}

  > Nachdem Sie dies erledigt haben, ist es ziemlich einfach, wenn Sie ihm sagen, dass er das Schema nicht ändern soll, indem Sie `--with "data only"` verwenden
  {.is-info}


2. Starten Sie Sonarr


3. Für diejenigen, die nach der POST-MIGRATION von SQLite Probleme beim Hinzufügen von Serien oder Fehlermeldungen im Protokoll haben, führen Sie Folgendes aus:
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
