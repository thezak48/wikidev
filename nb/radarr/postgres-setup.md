---
title: Radarr Konfigurering av PostgreSQL-database
description: Konfigurering av Radarr med en PostgreSQL-database
published: true
date: 2023-08-09T19:29:31.472Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:42:34.178Z
---

# Radarr og Postgres

Dette dokumentet vil gå gjennom de viktigste punktene for migrering og oppsett av Postgres-støtte i Radarr.

> Radarr v4.1.0.6133 eller nyere er påkrevd
{.is-info}

Denne veiledningen ble opprettet av den fantastiske [Roxedus](https://github.com/Roxedus).

> Postgres-databaser blir IKKE sikkerhetskopiert av Radarr, eventuelle sikkerhetskopier må implementeres og vedlikeholdes av brukeren
{.is-danger}

## Oppsett av Postgres

Først trenger vi en Postgres-instans. Denne veiledningen er skrevet for bruk av `postgres:14` Docker-bilde.

> Ikke engang tenk på å bruke `latest`-taggen! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=radarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Opprettelse av database

Radarr trenger to databaser, standardnavnene på disse er:

- `radarr-main`   Denne brukes til å lagre all konfigurasjon og historikk
- `radarr-log`    Denne brukes til å lagre hendelser som produserer en loggoppføring

> Radarr vil ikke opprette databasene for deg. Sørg for å opprette dem på forhånd{.is-warning}

Opprett de nevnte databasene ved hjelp av din foretrukne metode - for eksempel [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

Du kan gi databasene hvilket som helst navn du ønsker, men sørg for at `config.xml`-filen har de riktige navnene. For mer informasjon, se [oppsett av skjema](/radarr/postgres-setup#schema-creation).

### Opprettelse av skjema

Vi må fortelle Radarr å bruke Postgres. `config.xml` skal allerede være fylt ut med oppføringene vi trenger:

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

Hvis du vil spesifisere et databasenavn, må du også inkludere følgende konfigurasjon:

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

Først **etter at begge databasene er opprettet**, kan du starte migreringen fra SQLite til Postgres i Radarr.

## Migrering av data

> Hvis du ikke ønsker å migrere en eksisterende SQLite-database til Postgres, er du allerede ferdig med denne veiledningen! {.is-info}

For å migrere data kan vi bruke [PGLoader](https://github.com/dimitri/pgloader). Det har imidlertid noen ting å være oppmerksom på:

- Som standard er transaksjoner ikke forskjellsensitive, vi bruker `--with "quote identifiers"` for å gjøre dem sensitive.
- Versjonen som er pakket i Debian og Ubuntus apt-repo er for gammel for nyere versjoner av Postgres (Roxedus har ikke testet pakker i andre distribusjoner).
  Roxedus [har bygget en binær](https://github.com/Roxedus/Pgloader-bin) for å aktivere denne støtten (ingen kodeendringer var nødvendig, den måtte bare bygges med oppdaterte avhengigheter).

> Ikke slett noen tabeller i Postgres-instansen {.is-danger}

Før du starter en migrering, må du forsikre deg om at du har kjørt Radarr mot de opprettede Postgres-databasene **minst én gang**. Start migreringen ved å gjøre følgende:

1. Stopp Radarr
1. Åpne ditt foretrukne databaseadministrasjonsverktøy og koble til Postgres-databaseinstansen
1. Kjør følgende kommandoer:

```SQL
DELETE FROM "Profiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. Start migreringen ved å bruke en av disse alternativene:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" radarr.db 'postgresql://qstick:qstick@localhost/radarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/radarr.db:/radarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /radarr.db "postgresql://qstick:qstick@localhost/radarr-main"
      ```

  > Hvis du opplever en feil ved bruk av pgloader, kan det skyldes at databasen din er for stor. For å løse dette kan du prøve å legge til `--with "prefetch rows = 100" --with "batch size = 1MB"` i kommandoen over
  {.is-warning}

  > Når dette er håndtert, er det ganske enkelt etter å ha fortalt den å ikke endre skjemaet ved å bruke `--with "data only"`
  {.is-info}


2. Start Radarr

3. For de som opplever problemer med å legge til filmer ETTER MIGRERING fra SQLite, kjør følgende:
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