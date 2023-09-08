---
title: Konfigurera PostgreSQL-databas för Lidarr
description: Konfigurera Lidarr med en PostgreSQL-databas
published: true
date: 2023-09-03T17:21:21.279Z
tags: 
editor: markdown
dateCreated: 2022-11-25T01:35:56.796Z
---

# Lidarr och Postgres

Detta dokument kommer att gå igenom de viktigaste punkterna för att migrera och konfigurera Postgres-stöd i Lidarr.

> Lidarr v1.1.2.2890 eller senare krävs
{.is-info}

Denna guide har skapats av den fantastiska [Roxedus](https://github.com/Roxedus).

> Postgres-databaser säkerhetskopieras inte av Lidarr, eventuella säkerhetskopior måste implementeras och underhållas av användaren
{.is-danger}

## Konfigurera Postgres

Först behöver vi en Postgres-instans. Denna guide är skriven för användning av Docker-bilden `postgres:14`.

> Tänk inte ens på att använda taggen `latest`! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=lidarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Skapande av databas

Lidarr behöver två databaser, standardnamnen för dessa är:

- `lidarr-main`   Denna används för att lagra all konfiguration och historik
- `lidarr-log`    Denna används för att lagra händelser som genererar en loggpost

> Lidarr kommer inte att skapa databaserna åt dig. Se till att du skapar dem i förväg{.is-warning}

Skapa de ovan nämnda databaserna med hjälp av din favoritmetod - till exempel [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

Du kan ge databaserna vilket namn du vill, men se till att `config.xml`-filen har de korrekta namnen. För ytterligare information, se [schema creation](/lidarr/postgres-setup#schema-creation).

### Skapande av schema

Vi behöver berätta för Lidarr att använda Postgres. `config.xml` bör redan vara ifylld med de poster vi behöver:

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

Om du vill ange ett databasnamn bör du också inkludera följande konfiguration:

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

Endast **efter att ha skapat** båda databaserna kan du starta Lidarr-migreringen från SQLite till Postgres.

## Migrering av data

> Om du inte vill migrera en befintlig SQLite-databas till Postgres är du redan klar med denna guide! {.is-info}

För att migrera data kan vi använda [PGLoader](https://github.com/dimitri/pgloader). Det har dock vissa fallgropar:

- Som standard är transaktioner skiftlägesokänsliga, vi använder `--with "quote identifiers"` för att göra dem känsliga.
- Versionen som paketeras i Debians och Ubuntus apt-repo är för gammal för nyare versioner av Postgres (Roxedus har inte testat paket i andra distributioner).
  Roxedus [byggde en binär](https://github.com/Roxedus/Pgloader-bin) för att möjliggöra detta stöd (ingen kodmodifiering behövdes, den behövde bara byggas med uppdaterade beroenden).

> Radera inte några tabeller i Postgres-instansen {.is-danger}

Innan du startar en migrering, se till att du har kört Lidarr mot de skapade Postgres-databaserna **minst en gång** framgångsrikt. Påbörja migreringen genom att göra följande:

1. Stoppa Lidarr
1. Öppna ditt föredragna databashanteringsverktyg och anslut till Postgres-databasinstansen
1. Kör följande kommandon:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
DELETE FROM "MetadataProfiles";
```

1. Starta migreringen genom att använda något av dessa alternativ:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" lidarr.db 'postgresql://qstick:qstick@localhost/lidarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/lidarr.db:/lidarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /lidarr.db "postgresql://qstick:qstick@localhost/lidarr-main"
      ```

  > Om du upplever ett fel när du använder pgloader kan det bero på att din databas är för stor, försök att lösa detta genom att lägga till `--with "prefetch rows = 100" --with "batch size = 1MB"` till ovanstående kommando
  {.is-warning}
  
  > Med dessa hanterade är det ganska enkelt efter att ha sagt till den att inte ändra schemat med `--with "data only"`
  {.is-info}

1. Starta Lidarr
2. Kör följande frågor i databasen. Om du får fel som `Npgsql.PostgresException (0x80004005): 23505: duplicate key value violates unique constraint`
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
Observera: Det finns två kommenterade rader eftersom jag inte kunde hitta källtabellen för de sekvenserna.