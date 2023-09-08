---
title: Readarr Konfigurering av PostgreSQL-database
description: Konfigurering av Readarr med en PostgreSQL-database
published: true
date: 2022-12-04T23:00:38.482Z
tags: 
editor: markdown
dateCreated: 2022-07-25T22:49:56.668Z
---

# Readarr og PostgreSQL

Denne dokumentasjonen vil gå gjennom de viktigste punktene for migrering og oppsett av PostgreSQL-støtte i Readarr.

> Readarr v0.1.1.1408 eller nyere er påkrevd
{.is-info}

Denne guiden ble laget av den fantastiske [Roxedus](https://github.com/Roxedus).

> PostgreSQL-databaser blir IKKE sikkerhetskopiert av Readarr, eventuelle sikkerhetskopier må implementeres og vedlikeholdes av brukeren
{.is-danger}

## Oppsett av PostgreSQL

Først trenger vi en PostgreSQL-instans. Denne guiden er skrevet for bruk av `postgres:14` Docker-bilde.

> Ikke engang tenk på å bruke `latest`-taggen! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=readarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Opprettelse av database

Readarr trenger tre databaser, standardnavnene på disse er:

- `readarr-main`   Denne brukes til å lagre all konfigurasjon og historikk
- `readarr-log`    Denne brukes til å lagre hendelser som produserer en loggoppføring
- `readarr-cache`    Denne brukes til å lagre GoodReads-buffer

> Readarr vil ikke opprette databasene for deg. Sørg for å opprette dem på forhånd{.is-warning}

Opprett de nevnte databasene ved hjelp av din foretrukne metode - for eksempel [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

Du kan gi databasene hvilket som helst navn du ønsker, men sørg for at `config.xml`-filen har riktige navn. For mer informasjon, se [opprettelse av skjema](/readarr/postgres-setup#schema-creation).

### Opprettelse av skjema

Vi må fortelle Readarr å bruke PostgreSQL. `config.xml` skal allerede være fylt ut med de oppføringene vi trenger:

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
<PostgresCacheDb>CacheDbName</PostgresCacheDb>
```

Først **etter at** begge databasene er opprettet, kan du starte migreringen fra SQLite til PostgreSQL i Readarr.

## Migrering av data

> Hvis du ikke ønsker å migrere en eksisterende SQLite-database til PostgreSQL, er du allerede ferdig med denne guiden! {.is-info}

For å migrere data kan vi bruke [PGLoader](https://github.com/dimitri/pgloader). Det er imidlertid noen ting du må være oppmerksom på:

- Som standard er transaksjoner skrivebeskyttet, vi bruker `--with "quote identifiers"` for å gjøre dem skrivebeskyttet.
- Versjonen som er pakket i Debian og Ubuntu's apt-repo er for gammel for nyere versjoner av PostgreSQL (Roxedus har ikke testet pakker i andre distribusjoner).
  Roxedus [har bygget en binær](https://github.com/Roxedus/Pgloader-bin) for å aktivere denne støtten (ingen kodeendringer var nødvendig, den måtte bare bygges med oppdaterte avhengigheter).

> Ikke slett noen tabeller i PostgreSQL-instansen {.is-danger}

Før du starter en migrering, må du forsikre deg om at du har kjørt Readarr mot de opprettede PostgreSQL-databasene **minst én gang**. Start migreringen ved å gjøre følgende:

1. Stopp Readarr
1. Åpne ditt foretrukne databaseadministrasjonsverktøy og koble til PostgreSQL-databaseinstansen
1. Kjør følgende kommandoer:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "MetadataProfiles";
```

1. Start migreringen ved å bruke en av disse alternativene:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" readarr.db 'postgresql://qstick:qstick@localhost/readarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/readarr.db:/readarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /readarr.db "postgresql://qstick:qstick@localhost/readarr-main"
      ```

> Hvis du opplever en feil ved bruk av pgloader, kan det skyldes at databasen din er for stor. For å løse dette kan du prøve å legge til `--with "prefetch rows = 100" --with "batch size = 1MB"` i den ovennevnte kommandoen {.is-warning}

> Når dette er håndtert, er det ganske enkelt etter å ha fortalt den å ikke endre skjemaet ved å bruke `--with "data only"`
{.is-info}

1. Start Readarr