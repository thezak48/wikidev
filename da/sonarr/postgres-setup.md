---
title: Sonarr Konfiguration af PostgreSQL Database
description: Konfiguration af Sonarr med en PostgreSQL Database
published: true
date: 2023-08-21T19:37:53.766Z
tags: 
editor: markdown
dateCreated: 2023-08-12T12:26:25.094Z
---

# Sonarr og Postgres

Dette dokument vil gennemgå de vigtigste punkter ved migrering og opsætning af Postgres-support i Sonarr.

> Sonarr v4.0.0.615 eller nyere er påkrævet
{.is-info}

Denne guide er blevet oprettet af den fantastiske [Roxedus](https://github.com/Roxedus).

> Postgres-databaser bliver IKKE sikkerhedskopieret af Sonarr, eventuelle sikkerhedskopier skal implementeres og vedligeholdes af brugeren
{.is-danger}

## Opsætning af Postgres

Først har vi brug for en Postgres-instans. Denne guide er skrevet til brug af `postgres:14` Docker-billedet.

> Tænk ikke engang på at bruge mærket `latest`! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=sonarr-main \
    -p 5432:5432/tcp \
    -v /sti/til/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Oprettelse af database

Sonarr har brug for to databaser, de standardnavne for disse er:

- `sonarr-main`   Denne bruges til at gemme al konfiguration og historik
- `sonarr-log`    Denne bruges til at gemme begivenheder, der producerer en logindgang

> Sonarr vil ikke oprette databaserne for dig. Sørg for at oprette dem på forhånd{.is-warning}

Opret de ovennævnte databaser ved hjælp af din foretrukne metode - f.eks. [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

Du kan give databaserne et hvilket som helst navn, du ønsker, men sørg for, at `config.xml`-filen har de korrekte navne. For yderligere information, se [skemaoprettelse](/sonarr/postgres-setup#schema-creation).

### Skemaoprettelse

Vi skal fortælle Sonarr at bruge Postgres. `config.xml`-filen skal allerede være udfyldt med de indtastninger, vi har brug for:

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

Først **efter at have oprettet** begge databaser kan du starte Sonarr-migreringen fra SQLite til Postgres.

## Migrering af data

> Hvis du ikke ønsker at migrere en eksisterende SQLite-database til Postgres, er du allerede færdig med denne guide! {.is-info}

For at migrere data kan vi bruge [PGLoader](https://github.com/dimitri/pgloader). Det har dog nogle faldgruber:

- Som standard er transaktioner ikke forskelsbehandlende for store og små bogstaver, vi bruger `--with "quote identifiers"` for at gøre dem forskelsbehandlende.
- Versionen, der er pakket i Debian og Ubuntus apt-repo, er for gammel til nyere versioner af Postgres (Roxedus har ikke testet pakkerne i andre distributioner).
  Roxedus [har bygget en binær fil](https://github.com/Roxedus/Pgloader-bin) for at muliggøre denne understøttelse (der var ikke behov for kodeændringer, den skulle blot bygges med opdaterede afhængigheder).

> Drop ikke nogen tabeller i Postgres-instansen {.is-danger}

Inden du starter en migrering, skal du sikre dig, at du har kørt Sonarr mod de oprettede Postgres-databaser **mindst én gang** med succes. Begynd migreringen ved at gøre følgende:

1. Stop Sonarr
1. Åbn dit foretrukne databaseadministrationværktøj og opret forbindelse til Postgres-databaseinstansen
1. Kør følgende kommandoer:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. Start migreringen ved at bruge en af følgende muligheder:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" sonarr.db 'postgresql://qstick:qstick@localhost/sonarr-main'
      ```

    - ```bash
      docker run --rm -v /absolut/sti/til/sonarr.db:/sonarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /sonarr.db "postgresql://qstick:qstick@localhost/sonarr-main"
      ```

  > Hvis du oplever en fejl ved brug af pgloader, kan det skyldes, at din database er for stor. For at løse dette skal du prøve at tilføje `--with "prefetch rows = 100" --with "batch size = 1MB"` til den ovenstående kommando
  {.is-warning}

  > Når dette er håndteret, er det ret ligetil efter at have fortalt den ikke at ændre skemaet ved hjælp af `--with "data only"`
  {.is-info}


2. Start Sonarr


3. Hvis du har problemer med at tilføje serier eller fejl i loggen efter POST-MIGRATION fra SQLite, skal du køre følgende:
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
