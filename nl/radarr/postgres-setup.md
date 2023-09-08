---
title: Radarr Configureren van PostgreSQL Database
description: Radarr configureren met een PostgreSQL-database
published: true
date: 2023-08-09T19:29:31.472Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:42:34.178Z
---

# Radarr en Postgres

Dit document gaat over de belangrijkste punten van het migreren en instellen van Postgres-ondersteuning in Radarr.

> Radarr v4.1.0.6133 of nieuwer is vereist
{.is-info}

Deze handleiding is gemaakt door de geweldige [Roxedus](https://github.com/Roxedus).

> Postgres-databases worden NIET door Radarr geback-upt, eventuele back-ups moeten worden geïmplementeerd en onderhouden door de gebruiker
{.is-danger}

## Postgres instellen

Allereerst hebben we een Postgres-instantie nodig. Deze handleiding is geschreven voor het gebruik van de `postgres:14` Docker-image.

> Denk er niet eens aan om de `latest`-tag te gebruiken! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=radarr-main \
    -p 5432:5432/tcp \
    -v /pad/naar/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Aanmaken van de database

Radarr heeft twee databases nodig, de standaardnamen hiervan zijn:

- `radarr-main`   Hierin worden alle configuratie- en geschiedenisgegevens opgeslagen
- `radarr-log`    Hierin worden gebeurtenissen opgeslagen die een logboekvermelding genereren

> Radarr zal de databases niet voor je aanmaken. Zorg ervoor dat je ze van tevoren aanmaakt{.is-warning}

Maak de hierboven genoemde databases aan met behulp van je favoriete methode - bijvoorbeeld [pgAdmin](https://www.pgadmin.org/) of [Adminer](https://www.adminer.org/).

Je kunt de databases elke gewenste naam geven, maar zorg ervoor dat het `config.xml`-bestand de juiste namen heeft. Voor meer informatie zie [schema-creatie](/radarr/postgres-setup#schema-creatie).

### Schema-creatie

We moeten Radarr vertellen om Postgres te gebruiken. Het `config.xml`-bestand moet al zijn ingevuld met de benodigde gegevens:

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

Pas **nadat** je beide databases hebt aangemaakt, kun je beginnen met de migratie van Radarr van SQLite naar Postgres.

## Gegevens migreren

> Als je geen bestaande SQLite-database naar Postgres wilt migreren, ben je al klaar met deze handleiding! {.is-info}

Om gegevens te migreren kunnen we [PGLoader](https://github.com/dimitri/pgloader) gebruiken. Het heeft echter enkele aandachtspunten:

- Standaard zijn transacties hoofdletterongevoelig, we gebruiken `--with "quote identifiers"` om ze hoofdlettergevoelig te maken.
- De versie die is verpakt in de apt-opslagplaatsen van Debian en Ubuntu is te oud voor nieuwere versies van Postgres (Roxedus heeft de pakketten niet getest in andere distributies).
  Roxedus heeft [een binair bestand gebouwd](https://github.com/Roxedus/Pgloader-bin) om deze ondersteuning mogelijk te maken (er was geen codeaanpassing nodig, het moest alleen worden gebouwd met bijgewerkte afhankelijkheden).

> Verwijder geen tabellen in de Postgres-instantie {.is-danger}

Voordat je een migratie start, zorg ervoor dat je Radarr al minstens één keer succesvol hebt uitgevoerd tegen de aangemaakte Postgres-databases. Begin de migratie door het volgende te doen:

1. Stop Radarr
1. Open je favoriete databasebeheertool en maak verbinding met de Postgres-database-instantie
1. Voer de volgende opdrachten uit:

```SQL
DELETE FROM "Profiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. Start de migratie door een van de volgende opties te gebruiken:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" radarr.db 'postgresql://qstick:qstick@localhost/radarr-main'
      ```

    - ```bash
      docker run --rm -v /absoluut/pad/naar/radarr.db:/radarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /radarr.db "postgresql://qstick:qstick@localhost/radarr-main"
      ```

  > Als je een foutmelding krijgt bij het gebruik van pgloader, kan dit te wijten zijn aan de grootte van je database. Probeer dit op te lossen door `--with "prefetch rows = 100" --with "batch size = 1MB"` aan de bovenstaande opdracht toe te voegen
  {.is-warning}

  > Met deze instellingen is het vrij eenvoudig nadat je hebt aangegeven dat het schema niet mag worden gewijzigd met behulp van `--with "data only"`
  {.is-info}


2. Start Radarr

3. Voor degenen die problemen hebben met het toevoegen van films NA DE MIGRATIE vanuit SQLite, voer het volgende uit:
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