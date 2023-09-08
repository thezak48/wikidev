---
title: Lidarr Configureren van PostgreSQL Database
description: Lidarr configureren met een Postgres Database
published: true
date: 2023-09-03T17:21:21.279Z
tags: 
editor: markdown
dateCreated: 2022-11-25T01:35:56.796Z
---

# Lidarr en Postgres

Dit document gaat over de belangrijkste punten van het migreren en instellen van Postgres-ondersteuning in Lidarr.

> Lidarr v1.1.2.2890 of nieuwer vereist
{.is-info}

Deze handleiding is gemaakt door de geweldige [Roxedus](https://github.com/Roxedus).

> Postgres-databases worden NIET door Lidarr geback-upt, eventuele back-ups moeten worden geïmplementeerd en onderhouden door de gebruiker
{.is-danger}

## Postgres instellen

Allereerst hebben we een Postgres-instantie nodig. Deze handleiding is geschreven voor het gebruik van de `postgres:14` Docker-image.

> Denk er niet eens aan om de `latest`-tag te gebruiken! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=lidarr-main \
    -p 5432:5432/tcp \
    -v /pad/naar/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Aanmaken van database

Lidarr heeft twee databases nodig, de standaardnamen hiervan zijn:

- `lidarr-main`   Hierin worden alle configuratie- en geschiedenisgegevens opgeslagen
- `lidarr-log`    Hierin worden gebeurtenissen opgeslagen die een logboekvermelding genereren

> Lidarr zal de databases niet voor je aanmaken. Zorg ervoor dat je ze van tevoren aanmaakt{.is-warning}

Maak de hierboven genoemde databases aan met behulp van je favoriete methode - bijvoorbeeld [pgAdmin](https://www.pgadmin.org/) of [Adminer](https://www.adminer.org/).

Je kunt de databases elke gewenste naam geven, maar zorg ervoor dat het bestand `config.xml` de juiste namen heeft. Voor meer informatie zie [schema-creatie](/lidarr/postgres-setup#schema-creatie).

### Schema-creatie

We moeten Lidarr vertellen om Postgres te gebruiken. Het `config.xml`-bestand moet al zijn ingevuld met de benodigde gegevens:

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

Als je een databasenaam wilt specificeren, moet je ook de volgende configuratie opnemen:

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

Pas **nadat** je beide databases hebt aangemaakt, kun je beginnen met de migratie van Lidarr van SQLite naar Postgres.

## Gegevens migreren

> Als je geen bestaande SQLite-database naar Postgres wilt migreren, ben je al klaar met deze handleiding! {.is-info}

Om gegevens te migreren kunnen we [PGLoader](https://github.com/dimitri/pgloader) gebruiken. Het heeft echter enkele aandachtspunten:

- Standaard zijn transacties hoofdletterongevoelig, we gebruiken `--with "quote identifiers"` om ze hoofdlettergevoelig te maken.
- De versie die is verpakt in de apt-repo's van Debian en Ubuntu is te oud voor nieuwere versies van Postgres (Roxedus heeft de pakketten niet getest in andere distributies).
  Roxedus heeft [een binair bestand gebouwd](https://github.com/Roxedus/Pgloader-bin) om deze ondersteuning mogelijk te maken (er was geen codeaanpassing nodig, het moest alleen worden gebouwd met bijgewerkte afhankelijkheden).

> Verwijder geen tabellen in de Postgres-instantie {.is-danger}

Voordat je een migratie start, zorg ervoor dat je Lidarr al minstens één keer succesvol hebt uitgevoerd tegen de aangemaakte Postgres-databases. Begin de migratie door het volgende te doen:

1. Stop Lidarr
1. Open je favoriete databasebeheertool en maak verbinding met de Postgres-database-instantie
1. Voer de volgende opdrachten uit:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
DELETE FROM "MetadataProfiles";
```

1. Start de migratie door een van de volgende opties te gebruiken:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" lidarr.db 'postgresql://qstick:qstick@localhost/lidarr-main'
      ```

    - ```bash
      docker run --rm -v /absoluut/pad/naar/lidarr.db:/lidarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /lidarr.db "postgresql://qstick:qstick@localhost/lidarr-main"
      ```

  > Als je een foutmelding krijgt bij het gebruik van pgloader, kan dit te wijten zijn aan de grootte van je database. Probeer dit op te lossen door `--with "prefetch rows = 100" --with "batch size = 1MB"` aan de bovenstaande opdracht toe te voegen
  {.is-warning}
  
  > Met deze instellingen is het vrij eenvoudig nadat je hebt aangegeven dat het schema niet moet worden gewijzigd met behulp van `--with "data only"`
  {.is-info}

1. Start Lidarr
2. Voer de volgende query's uit in de database. Als je fouten krijgt zoals `Npgsql.PostgresException (0x80004005): 23505: duplicate key value violates unique constraint`
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
Opmerking: er zijn twee opmerkingen omdat ik de 'source'-tabel voor die sequenties niet kon vinden.