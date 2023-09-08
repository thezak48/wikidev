---
title: Readarr Konfiguration af PostgreSQL Database
description: Konfiguration af Readarr med en PostgreSQL-database
published: true
date: 2022-12-04T23:00:38.482Z
tags: 
editor: markdown
dateCreated: 2022-07-25T22:49:56.668Z
---

# Readarr og Postgres

Dette dokument vil gennemgå de vigtigste punkter ved migrering og opsætning af Postgres-support i Readarr.

> Readarr v0.1.1.1408 eller nyere er påkrævet
{.is-info}

Denne guide er blevet oprettet af den fantastiske [Roxedus](https://github.com/Roxedus).

> Postgres-databaser bliver IKKE sikkerhedskopieret af Readarr, eventuelle sikkerhedskopier skal implementeres og vedligeholdes af brugeren
{.is-danger}

## Opsætning af Postgres

Først har vi brug for en Postgres-instans. Denne guide er skrevet til brug af `postgres:14` Docker-billedet.

> Tænk ikke engang på at bruge `latest`-tagget! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=readarr-main \
    -p 5432:5432/tcp \
    -v /sti/til/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Oprettelse af database

Readarr har brug for tre databaser, de standardnavne er:

- `readarr-main`   Denne bruges til at gemme al konfiguration og historik
- `readarr-log`    Denne bruges til at gemme begivenheder, der producerer en logindgang
- `readarr-cache`    Denne bruges til at gemme GoodReads-cache

> Readarr vil ikke oprette databaserne for dig. Sørg for at oprette dem på forhånd{.is-warning}

Opret de ovennævnte databaser ved hjælp af din foretrukne metode - f.eks. [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

Du kan give databaserne hvilket som helst navn, du ønsker, men sørg for, at `config.xml`-filen har de korrekte navne. For yderligere information, se [skemaoprettelse](/readarr/postgres-setup#schema-creation).

### Skemaoprettelse

Vi skal fortælle Readarr at bruge Postgres. `config.xml`-filen skal allerede være udfyldt med de indtastninger, vi har brug for:

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
<PostgresCacheDb>CacheDbName</PostgresCacheDb>
```

Først **efter oprettelse** af begge databaser kan du starte Readarr-migreringen fra SQLite til Postgres.

## Migrering af data

> Hvis du ikke ønsker at migrere en eksisterende SQLite-database til Postgres, er du allerede færdig med denne guide! {.is-info}

For at migrere data kan vi bruge [PGLoader](https://github.com/dimitri/pgloader). Det har dog nogle faldgruber:

- Som standard er transaktioner ikke skriftstørrelsessensitive, vi bruger `--with "quote identifiers"` for at gøre dem sensitive.
- Versionen, der er pakket i Debian og Ubuntu's apt-repo, er for gammel til nyere versioner af Postgres (Roxedus har ikke testet pakkerne i andre distributioner).
  Roxedus [har bygget en binær fil](https://github.com/Roxedus/Pgloader-bin) for at aktivere denne understøttelse (der var ikke behov for kodeændringer, den skulle blot bygges med opdaterede afhængigheder).

> Drop ikke nogen tabeller i Postgres-instansen {.is-danger}

Før du starter en migration, skal du sikre dig, at du har kørt Readarr mod de oprettede Postgres-databaser **mindst én gang** med succes. Begynd migreringen ved at gøre følgende:

1. Stop Readarr
1. Åbn dit foretrukne databaseadministrationværktøj og opret forbindelse til Postgres-databaseinstansen
1. Kør følgende kommandoer:

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "MetadataProfiles";
```

1. Start migreringen ved at bruge en af følgende muligheder:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" readarr.db 'postgresql://qstick:qstick@localhost/readarr-main'
      ```

    - ```bash
      docker run --rm -v /absolut/sti/til/readarr.db:/readarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /readarr.db "postgresql://qstick:qstick@localhost/readarr-main"
      ```

> Hvis du oplever en fejl ved brug af pgloader, kan det skyldes, at din database er for stor. For at løse dette skal du prøve at tilføje `--with "prefetch rows = 100" --with "batch size = 1MB"` til den ovenstående kommando {.is-warning}

> Når dette er håndteret, er det ret ligetil efter at have fortalt den, at den ikke skal rode med skemaet ved hjælp af `--with "data only"`
{.is-info}

1. Start Readarr