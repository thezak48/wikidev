---
title: Readarr Configureren van PostgreSQL Database
description: Readarr configureren met een PostgreSQL-database
published: true
date: 2022-12-04T23:00:38.482Z
tags: 
editor: markdown
dateCreated: 2022-07-25T22:49:56.668Z
---

# Readarr en Postgres

Dit document behandelt de belangrijkste punten voor het migreren en instellen van Postgres-ondersteuning in Readarr.

> Readarr v0.1.1.1408 of nieuwer is vereist
{.is-info}

Deze handleiding is gemaakt door de geweldige [Roxedus](https://github.com/Roxedus).

> Postgres-databases worden NIET door Readarr geback-upt, eventuele back-ups moeten worden geïmplementeerd en onderhouden door de gebruiker
{.is-danger}

## Postgres instellen

Allereerst hebben we een Postgres-instantie nodig. Deze handleiding is geschreven voor het gebruik van de `postgres:14` Docker-image.

> Denk er niet eens aan om de `latest`-tag te gebruiken! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=readarr-main \
    -p 5432:5432/tcp \
    -v /pad/naar/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Aanmaken van de database

Readarr heeft drie databases nodig, de standaardnamen hiervan zijn:

- `readarr-main`   Hierin worden alle configuratie- en geschiedenisgegevens opgeslagen
- `readarr-log`    Hierin worden gebeurtenissen opgeslagen die een logboekvermelding genereren
- `readarr-cache`    Hierin wordt de GoodReads-cache opgeslagen

> Readarr zal de databases niet voor je aanmaken. Zorg ervoor dat je ze van tevoren aanmaakt{.is-warning}

Maak de hierboven genoemde databases aan met je favoriete methode - bijvoorbeeld [pgAdmin](https://www.pgadmin.org/) of [Adminer](https://www.adminer.org/).

Je kunt de databases elke gewenste naam geven, maar zorg ervoor dat het `config.xml`-bestand de juiste namen heeft. Voor meer informatie zie [schema-aanmaak](/readarr/postgres-setup#schema-creation).

### Schema-aanmaak

We moeten Readarr vertellen om Postgres te gebruiken. Het `config.xml`-bestand zou al moeten zijn ingevuld met de benodigde gegevens:

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
<PostgresCacheDb>CacheDbName</PostgresCacheDb>
```

Pas **nadat** je beide databases hebt aangemaakt, kun je beginnen met de migratie van Readarr van SQLite naar Postgres.

## Gegevens migreren

> Als je geen bestaande SQLite-database naar Postgres wilt migreren, ben je al klaar met deze handleiding! {.is-info}

Om gegevens te migreren kunnen we [PGLoader](https://github.com/dimitri/pgloader) gebruiken. Het heeft echter enkele aandachtspunten:

- Standaard zijn transacties hoofdletterongevoelig, we gebruiken `--with "quote identifiers"` om ze hoofdlettergevoelig te maken.
- De versie die is verpakt in de apt-opslagplaatsen van Debian en Ubuntu is te oud voor nieuwere versies van Postgres (Roxedus heeft de pakketten niet getest in andere distributies).
  Roxedus heeft [een binair bestand gebouwd](https://github.com/Roxedus/Pgloader-bin) om deze ondersteuning mogelijk te maken (er was geen codeaanpassing nodig, het moest alleen worden gebouwd met bijgewerkte afhankelijkheden).

> Verwijder geen tabellen in de Postgres-instantie {.is-danger}

Voordat je een migratie start, zorg ervoor dat je Readarr al minstens één keer succesvol hebt uitgevoerd tegen de aangemaakte Postgres-databases. Begin de migratie door het volgende te doen:

1. Stop Readarr
1. Open je favoriete databasebeheertool en maak verbinding met de Postgres-database-instantie
1. Voer de volgende opdrachten uit:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "MetadataProfiles";
```

1. Start de migratie met een van deze opties:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" readarr.db 'postgresql://qstick:qstick@localhost/readarr-main'
      ```

    - ```bash
      docker run --rm -v /absoluut/pad/naar/readarr.db:/readarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /readarr.db "postgresql://qstick:qstick@localhost/readarr-main"
      ```

> Als je een foutmelding krijgt bij het gebruik van pgloader, kan dit te wijten zijn aan een te grote database. Probeer dit op te lossen door `--with "prefetch rows = 100" --with "batch size = 1MB"` aan de bovenstaande opdracht toe te voegen {.is-warning}

> Met deze stappen is het vrij eenvoudig nadat je hebt aangegeven dat het schema niet mag worden gewijzigd met `--with "data only"`
{.is-info}

1. Start Readarr