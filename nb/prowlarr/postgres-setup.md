---
title: Prowlarr Konfigurering av PostgreSQL-database
description: Konfigurering av Prowlarr med en PostgreSQL-database
published: true
date: 2022-11-29T13:19:38.953Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:38:53.538Z
---

# Prowlarr og Postgres

Dette dokumentet vil gå gjennom de viktigste punktene for migrering og oppsett av Postgres-støtte i Prowlarr.

Denne veiledningen ble opprettet av den fantastiske [Roxedus](https://github.com/Roxedus).

> Postgres-databaser blir IKKE sikkerhetskopiert av Prowlarr, eventuelle sikkerhetskopier må implementeres og vedlikeholdes av brukeren
{.is-danger}

## Oppsett av Postgres

Først trenger vi en Postgres-instans. Denne veiledningen er skrevet for bruk av `postgres:14` Docker-bilde.

> Ikke engang tenk på å bruke `latest`-taggen! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=prowlarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Opprettelse av database

Prowlarr trenger to databaser, standardnavnene på disse er:

- `prowlarr-main`   Denne brukes til å lagre all konfigurasjon og historikk
- `prowlarr-log`    Denne brukes til å lagre hendelser som produserer en loggoppføring

> Prowlarr vil ikke opprette databasene for deg. Sørg for å opprette dem på forhånd{.is-warning}

Opprett de nevnte databasene ved hjelp av din foretrukne metode - for eksempel [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

> For at oppgaven `Housekeeping` skal kjøre, må denne brukeren være en superbruker, siden den utfører vakuumoppgaven{.is-info}

Du kan gi databasene hvilket som helst navn du ønsker, men sørg for at `config.xml`-filen har de riktige navnene. For mer informasjon, se [oppsett av skjema](/prowlarr/postgres-setup#schema-creation).

### Opprettelse av skjema

Vi må fortelle Prowlarr å bruke Postgres. `config.xml`-filen skal allerede være fylt ut med oppføringene vi trenger:

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

Først **etter at begge databasene er opprettet**, kan du starte migreringen fra SQLite til Postgres i Prowlarr.

## Migrering av data

> Hvis du ikke ønsker å migrere en eksisterende SQLite-database til Postgres, er du allerede ferdig med denne veiledningen! {.is-info}

For å migrere data kan vi bruke [PGLoader](https://github.com/dimitri/pgloader). Det har imidlertid noen fallgruver:

- Som standard er transaksjoner ikke forskjellsbehandling mellom store og små bokstaver, vi bruker `--with "quote identifiers"` for å gjøre dem forskjellsbehandling.
- Versjonen som er pakket i Debian og Ubuntus apt-repo er for gammel for nyere versjoner av Postgres (Roxedus har ikke testet pakker i andre distribusjoner).
  Roxedus [bygde en binær](https://github.com/Roxedus/Pgloader-bin) for å aktivere denne støtten (ingen kodeendringer var nødvendig, den måtte bare bygges med oppdaterte avhengigheter).

> Ikke slett noen tabeller i Postgres-instansen {.is-danger}

Før du starter en migrering, må du forsikre deg om at du har kjørt Prowlarr mot de opprettede Postgres-databasene **minst én gang vellykket**. Start migreringen ved å gjøre følgende:

1. Stopp Prowlarr
1. Åpne ditt foretrukne databaseadministrasjonsverktøy og koble til Postgres-databaseinstansen
1. Start migreringen ved å bruke en av disse alternativene:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" prowlarr.db 'postgresql://qstick:qstick@localhost/prowlarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/prowlarr.db:/prowlarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /prowlarr.db "postgresql://qstick:qstick@localhost/prowlarr-main"
      ```

  > Hvis du opplever en feil ved bruk av pgloader, kan det skyldes at databasen din er for stor. For å løse dette kan du prøve å legge til `--with "prefetch rows = 100" --with "batch size = 1MB"` i kommandoen ovenfor
  {.is-warning}

  > Når dette er håndtert, er det ganske enkelt etter å ha fortalt den å ikke endre skjemaet ved hjelp av `--with "data only"`
  {.is-info}

1. Start Prowlarr