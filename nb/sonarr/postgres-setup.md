---
title: Sonarr Konfigurering av PostgreSQL-database
description: Konfigurering av Sonarr med en PostgreSQL-database
published: true
date: 2023-08-21T19:37:53.766Z
tags: 
editor: markdown
dateCreated: 2023-08-12T12:26:25.094Z
---

# Sonarr og Postgres

Dette dokumentet vil gå gjennom de viktigste punktene for migrering og oppsett av Postgres-støtte i Sonarr.

> Sonarr v4.0.0.615 eller nyere er påkrevd
{.is-info}

Denne veiledningen ble opprettet av den fantastiske [Roxedus](https://github.com/Roxedus).

> Postgres-databaser blir IKKE sikkerhetskopiert av Sonarr, eventuelle sikkerhetskopier må implementeres og vedlikeholdes av brukeren
{.is-danger}

## Oppsett av Postgres

Først trenger vi en Postgres-instans. Denne veiledningen er skrevet for bruk av `postgres:14` Docker-bildet.

> Ikke engang tenk på å bruke `latest`-taggen! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=sonarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Opprettelse av database

Sonarr trenger to databaser, standardnavnene på disse er:

- `sonarr-main`   Denne brukes til å lagre all konfigurasjon og historikk
- `sonarr-log`    Denne brukes til å lagre hendelser som produserer en loggoppføring

> Sonarr vil ikke opprette databasene for deg. Sørg for å opprette dem på forhånd{.is-warning}

Opprett de nevnte databasene ved hjelp av din foretrukne metode - for eksempel [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

Du kan gi databasene hvilket som helst navn du ønsker, men sørg for at `config.xml`-filen har de riktige navnene. For mer informasjon, se [oppsett av skjema](/sonarr/postgres-setup#schema-creation).

### Opprettelse av skjema

Vi må fortelle Sonarr å bruke Postgres. `config.xml`-filen skal allerede være fylt ut med oppføringene vi trenger:

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

Bare **etter å ha opprettet** begge databasene kan du starte Sonarr-migreringen fra SQLite til Postgres.

## Migrering av data

> Hvis du ikke ønsker å migrere en eksisterende SQLite-database til Postgres, er du allerede ferdig med denne veiledningen! {.is-info}

For å migrere data kan vi bruke [PGLoader](https://github.com/dimitri/pgloader). Det har imidlertid noen ting å være oppmerksom på:

- Som standard er transaksjoner ikke forskjellsbehandlet med hensyn til store og små bokstaver, vi bruker `--with "quote identifiers"` for å gjøre dem forskjellsbehandlet.
- Versjonen som er pakket i Debian og Ubuntu apt-repoene er for gammel for nyere versjoner av Postgres (Roxedus har ikke testet pakker i andre distribusjoner).
  Roxedus [har bygget en binær](https://github.com/Roxedus/Pgloader-bin) for å aktivere denne støtten (ingen kodeendringer var nødvendig, den måtte bare bygges med oppdaterte avhengigheter).

> Ikke slett noen tabeller i Postgres-instansen {.is-danger}

Før du starter en migrering, må du forsikre deg om at du har kjørt Sonarr mot de opprettede Postgres-databasene **minst én gang**. Start migreringen ved å gjøre følgende:

1. Stopp Sonarr
1. Åpne ditt foretrukne databaseadministrasjonsverktøy og koble til Postgres-databaseinstansen
1. Kjør følgende kommandoer:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. Start migreringen ved å bruke en av disse alternativene:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" sonarr.db 'postgresql://qstick:qstick@localhost/sonarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/sonarr.db:/sonarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /sonarr.db "postgresql://qstick:qstick@localhost/sonarr-main"
      ```

  > Hvis du opplever en feil ved bruk av pgloader, kan det skyldes at databasen din er for stor. For å løse dette kan du prøve å legge til `--with "prefetch rows = 100" --with "batch size = 1MB"` i den ovennevnte kommandoen
  {.is-warning}

  > Når dette er håndtert, er det ganske enkelt etter å ha fortalt den å ikke endre skjemaet ved å bruke `--with "data only"`
  {.is-info}


2. Start Sonarr


3. For de som opplever problemer med å legge til serier eller feil i loggen etter POST-MIGRATION fra SQLite, kjør følgende:
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
