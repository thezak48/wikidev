---
title: Konfiguration af PostgreSQL-database i Lidarr
description: Konfiguration af Lidarr med en PostgreSQL-database
published: true
date: 2023-09-03T17:21:21.279Z
tags: 
editor: markdown
dateCreated: 2022-11-25T01:35:56.796Z
---

# Lidarr og Postgres

Dette dokument vil gennemgå de vigtigste punkter ved migrering og opsætning af Postgres-understøttelse i Lidarr.

> Lidarr v1.1.2.2890 eller nyere er påkrævet
{.is-info}

Denne guide er blevet oprettet af den fantastiske [Roxedus](https://github.com/Roxedus).

> Postgres-databaser bliver IKKE sikkerhedskopieret af Lidarr, eventuelle sikkerhedskopier skal implementeres og vedligeholdes af brugeren
{.is-danger}

## Opsætning af Postgres

Først har vi brug for en Postgres-instans. Denne guide er skrevet til brug af `postgres:14` Docker-billedet.

> Tænk ikke engang på at bruge `latest`-tagget! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=lidarr-main \
    -p 5432:5432/tcp \
    -v /sti/til/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Oprettelse af database

Lidarr har brug for to databaser, de standardnavne for disse er:

- `lidarr-main`   Denne bruges til at gemme al konfiguration og historik
- `lidarr-log`    Denne bruges til at gemme begivenheder, der producerer en logindgang

> Lidarr vil ikke oprette databaserne for dig. Sørg for at oprette dem på forhånd{.is-warning}

Opret de ovennævnte databaser ved hjælp af din foretrukne metode - f.eks. [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

Du kan give databaserne hvilket som helst navn, du ønsker, men sørg for, at `config.xml`-filen har de korrekte navne. For yderligere information, se [oprettelse af skema](/lidarr/postgres-setup#schema-creation).

### Oprettelse af skema

Vi skal fortælle Lidarr at bruge Postgres. `config.xml`-filen skal allerede være udfyldt med de indtastninger, vi har brug for:

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

Hvis du vil angive et databasenavn, skal du også inkludere følgende konfiguration:

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

Først **efter at have oprettet** begge databaser kan du starte Lidarr-migreringen fra SQLite til Postgres.

## Migrering af data

> Hvis du ikke ønsker at migrere en eksisterende SQLite-database til Postgres, er du allerede færdig med denne guide! {.is-info}

For at migrere data kan vi bruge [PGLoader](https://github.com/dimitri/pgloader). Det har dog nogle faldgruber:

- Som standard er transaktioner ikke forskelsbehandlende mellem store og små bogstaver, vi bruger `--with "quote identifiers"` for at gøre dem forskelsbehandlende.
- Versionen, der er pakket i Debian og Ubuntus apt-repo, er for gammel til nyere versioner af Postgres (Roxedus har ikke testet pakkerne i andre distributioner).
  Roxedus [har bygget en binær fil](https://github.com/Roxedus/Pgloader-bin) for at aktivere denne understøttelse (der var ikke behov for nogen kodeændring, den skulle blot bygges med opdaterede afhængigheder).

> Drop ikke nogen tabeller i Postgres-instansen {.is-danger}

Inden du starter en migrering, skal du sikre dig, at du har kørt Lidarr mod de oprettede Postgres-databaser **mindst én gang** med succes. Begynd migreringen ved at gøre følgende:

1. Stop Lidarr
1. Åbn dit foretrukne databaseadministrationværktøj og opret forbindelse til Postgres-databaseinstansen
1. Kør følgende kommandoer:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
DELETE FROM "MetadataProfiles";
```

1. Start migreringen ved at bruge en af følgende muligheder:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" lidarr.db 'postgresql://qstick:qstick@localhost/lidarr-main'
      ```

    - ```bash
      docker run --rm -v /absolut/sti/til/lidarr.db:/lidarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /lidarr.db "postgresql://qstick:qstick@localhost/lidarr-main"
      ```

  > Hvis du oplever en fejl ved brug af pgloader, kan det skyldes, at din database er for stor. For at løse dette skal du prøve at tilføje `--with "prefetch rows = 100" --with "batch size = 1MB"` til den ovenstående kommando
  {.is-warning}
  
  > Når disse er håndteret, er det ret ligetil efter at have fortalt den ikke at ændre skemaet ved hjælp af `--with "data only"`
  {.is-info}

1. Start Lidarr
2. Udfør følgende forespørgsler i databasen. Hvis du får fejl som f.eks. `Npgsql.PostgresException (0x80004005): 23505: duplicate key value violates unique constraint`
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
Bemærk: Der er to kommenteret ud, da jeg ikke kunne finde 'source'-tabellen for de sekvenser.