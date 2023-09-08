---
title: Konfigurering av PostgreSQL-database for Lidarr
description: Konfigurering av Lidarr med en PostgreSQL-database
published: true
date: 2023-09-03T17:21:21.279Z
tags: 
editor: markdown
dateCreated: 2022-11-25T01:35:56.796Z
---

# Lidarr og PostgreSQL

Denne dokumentasjonen vil gå gjennom de viktigste punktene for migrering og oppsett av PostgreSQL-støtte i Lidarr.

> Lidarr v1.1.2.2890 eller nyere er påkrevd
{.is-info}

Denne guiden ble laget av den fantastiske [Roxedus](https://github.com/Roxedus).

> PostgreSQL-databaser blir IKKE sikkerhetskopiert av Lidarr, eventuelle sikkerhetskopier må implementeres og vedlikeholdes av brukeren
{.is-danger}

## Oppsett av PostgreSQL

Først trenger vi en PostgreSQL-instans. Denne guiden er skrevet for bruk av `postgres:14` Docker-bilde.

> Ikke engang tenk på å bruke `latest`-taggen! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=lidarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Opprettelse av database

Lidarr trenger to databaser, standardnavnene på disse er:

- `lidarr-main`   Denne brukes til å lagre all konfigurasjon og historikk
- `lidarr-log`    Denne brukes til å lagre hendelser som produserer en loggoppføring

> Lidarr vil ikke opprette databasene for deg. Sørg for å opprette dem på forhånd{.is-warning}

Opprett de nevnte databasene ved hjelp av din foretrukne metode - for eksempel [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

Du kan gi databasene hvilket som helst navn du ønsker, men sørg for at `config.xml`-filen har de riktige navnene. For mer informasjon, se [opprettelse av skjema](/lidarr/postgres-setup#schema-creation).

### Opprettelse av skjema

Vi må fortelle Lidarr å bruke PostgreSQL. `config.xml`-filen skal allerede være fylt ut med oppføringene vi trenger:

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

Hvis du vil spesifisere et databasenavn, bør du også inkludere følgende konfigurasjon:

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

Bare **etter å ha opprettet** begge databasene kan du starte migreringen fra SQLite til PostgreSQL i Lidarr.

## Migrering av data

> Hvis du ikke ønsker å migrere en eksisterende SQLite-database til PostgreSQL, er du allerede ferdig med denne guiden! {.is-info}

For å migrere data kan vi bruke [PGLoader](https://github.com/dimitri/pgloader). Det har imidlertid noen ting å være oppmerksom på:

- Som standard er transaksjoner ikke forskjellsbehandlet mellom store og små bokstaver, vi bruker `--with "quote identifiers"` for å gjøre dem forskjellsbehandlet.
- Versjonen som er pakket i Debian og Ubuntus apt-repo er for gammel for nyere versjoner av PostgreSQL (Roxedus har ikke testet pakker i andre distribusjoner).
  Roxedus [har bygget en binær](https://github.com/Roxedus/Pgloader-bin) for å aktivere denne støtten (ingen kodeendringer var nødvendig, den måtte bare bygges med oppdaterte avhengigheter).

> Ikke slett noen tabeller i PostgreSQL-instansen {.is-danger}

Før du starter en migrering, sørg for at du har kjørt Lidarr mot de opprettede PostgreSQL-databasene **minst én gang**. Start migreringen ved å gjøre følgende:

1. Stopp Lidarr
1. Åpne ditt foretrukne databaseadministrasjonsverktøy og koble til PostgreSQL-databaseinstansen
1. Kjør følgende kommandoer:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
DELETE FROM "MetadataProfiles";
```

1. Start migreringen ved å bruke en av disse alternativene:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" lidarr.db 'postgresql://qstick:qstick@localhost/lidarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/lidarr.db:/lidarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /lidarr.db "postgresql://qstick:qstick@localhost/lidarr-main"
      ```

  > Hvis du opplever en feil ved bruk av pgloader, kan det skyldes at databasen din er for stor. For å løse dette kan du prøve å legge til `--with "prefetch rows = 100" --with "batch size = 1MB"` i den ovennevnte kommandoen
  {.is-warning}
  
  > Når dette er håndtert, er det ganske enkelt etter å ha fortalt den å ikke endre skjemaet ved å bruke `--with "data only"`
  {.is-info}

1. Start Lidarr
2. Kjør følgende spørringer i databasen. Hvis du får feilmeldinger som `Npgsql.PostgresException (0x80004005): 23505: duplicate key value violates unique constraint`
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
Merk: Det er to kommentert ut siden jeg ikke kunne finne 'source'-tabellen for de sekvensene.