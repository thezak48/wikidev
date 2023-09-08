---
title: Prowlarr Configureren met PostgreSQL Database
description: Prowlarr configureren met een PostgreSQL-database
published: true
date: 2022-11-29T13:19:38.953Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:38:53.538Z
---

# Prowlarr en Postgres

Dit document behandelt de belangrijkste punten voor het migreren en instellen van Postgres-ondersteuning in Prowlarr.

Deze handleiding is gemaakt door de geweldige [Roxedus](https://github.com/Roxedus).

> Postgres-databases worden NIET door Prowlarr geback-upt. Back-ups moeten door de gebruiker worden geïmplementeerd en onderhouden.
{.is-danger}

## Postgres instellen

Allereerst hebben we een Postgres-instantie nodig. Deze handleiding is geschreven voor het gebruik van de `postgres:14` Docker-image.

> Denk er niet eens aan om de `latest`-tag te gebruiken! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=prowlarr-main \
    -p 5432:5432/tcp \
    -v /pad/naar/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Aanmaken van de database

Prowlarr heeft twee databases nodig, de standaardnamen hiervan zijn:

- `prowlarr-main`   Hierin worden alle configuratie- en geschiedenisgegevens opgeslagen.
- `prowlarr-log`    Hierin worden gebeurtenissen opgeslagen die een logboekvermelding genereren.

> Prowlarr zal de databases niet voor je aanmaken. Zorg ervoor dat je ze van tevoren aanmaakt{.is-warning}

Maak de hierboven genoemde databases aan met je favoriete methode - bijvoorbeeld [pgAdmin](https://www.pgadmin.org/) of [Adminer](https://www.adminer.org/).

> Om de taak 'Housekeeping' uit te voeren, moet deze gebruiker een supergebruiker zijn, omdat deze de vacuumtaak uitvoert{.is-info}

Je kunt de databases een willekeurige naam geven, maar zorg ervoor dat het bestand `config.xml` de juiste namen heeft. Voor meer informatie zie [schema-creatie](/prowlarr/postgres-setup#schema-creation).

### Schema-creatie

We moeten Prowlarr vertellen om Postgres te gebruiken. Het bestand `config.xml` moet al zijn ingevuld met de benodigde gegevens:

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

Pas **nadat** je beide databases hebt aangemaakt, kun je beginnen met de migratie van Prowlarr van SQLite naar Postgres.

## Gegevens migreren

> Als je geen bestaande SQLite-database naar Postgres wilt migreren, ben je al klaar met deze handleiding! {.is-info}

Om gegevens te migreren, kunnen we [PGLoader](https://github.com/dimitri/pgloader) gebruiken. Het heeft echter enkele aandachtspunten:

- Standaard zijn transacties hoofdletterongevoelig, we gebruiken `--with "quote identifiers"` om ze hoofdlettergevoelig te maken.
- De versie die is verpakt in de apt-opslagplaatsen van Debian en Ubuntu is te oud voor nieuwere versies van Postgres (Roxedus heeft de pakketten niet getest in andere distributies).
  Roxedus heeft [een binair bestand gebouwd](https://github.com/Roxedus/Pgloader-bin) om deze ondersteuning mogelijk te maken (er was geen codeaanpassing nodig, het moest alleen worden gebouwd met bijgewerkte afhankelijkheden).

> Verwijder geen tabellen in de Postgres-instantie {.is-danger}

Voordat je een migratie start, zorg ervoor dat je Prowlarr al minstens één keer succesvol hebt uitgevoerd tegen de aangemaakte Postgres-databases. Begin de migratie door het volgende te doen:

1. Stop Prowlarr.
1. Open je favoriete databasebeheertool en maak verbinding met de Postgres-database-instantie.
1. Start de migratie met een van de volgende opties:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" prowlarr.db 'postgresql://qstick:qstick@localhost/prowlarr-main'
      ```

    - ```bash
      docker run --rm -v /absoluut/pad/naar/prowlarr.db:/prowlarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /prowlarr.db "postgresql://qstick:qstick@localhost/prowlarr-main"
      ```

  > Als je een foutmelding krijgt bij het gebruik van pgloader, kan dit te wijten zijn aan de grootte van je database. Probeer dit op te lossen door `--with "prefetch rows = 100" --with "batch size = 1MB"` aan de bovenstaande opdracht toe te voegen.
  {.is-warning}

  > Met deze aanpak is het vrij eenvoudig nadat je hebt aangegeven dat het schema niet moet worden gewijzigd met behulp van `--with "data only"`.
  {.is-info}

1. Start Prowlarr.