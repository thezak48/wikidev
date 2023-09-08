---
title: Prowlarr Konfiguration af PostgreSQL Database
description: Konfiguration af Prowlarr med en PostgreSQL Database
published: true
date: 2022-11-29T13:19:38.953Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:38:53.538Z
---

# Prowlarr og Postgres

Dette dokument vil gennemgå de vigtigste punkter ved migrering og opsætning af Postgres-understøttelse i Prowlarr.

Denne guide er blevet oprettet af den fantastiske [Roxedus](https://github.com/Roxedus).

> Postgres-databaser bliver IKKE sikkerhedskopieret af Prowlarr, eventuelle sikkerhedskopier skal implementeres og vedligeholdes af brugeren
{.is-danger}

## Opsætning af Postgres

Først har vi brug for en Postgres-instans. Denne guide er skrevet til brug af `postgres:14` Docker-billedet.

> Tænk ikke engang på at bruge `latest`-tagget! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=prowlarr-main \
    -p 5432:5432/tcp \
    -v /sti/til/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Oprettelse af database

Prowlarr har brug for to databaser, de standardnavne for disse er:

- `prowlarr-main`   Denne bruges til at gemme al konfiguration og historik
- `prowlarr-log`    Denne bruges til at gemme begivenheder, der producerer en logindgang

> Prowlarr vil ikke oprette databaserne for dig. Sørg for at oprette dem på forhånd{.is-warning}

Opret de ovennævnte databaser ved hjælp af din foretrukne metode - for eksempel [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

> For at `Housekeeping`-opgaven kan køre, skal denne bruger være en superbruger, da den udfører vakuumopgaven{.is-info}

Du kan give databaserne et hvilket som helst navn, men sørg for, at `config.xml`-filen har de korrekte navne. For yderligere information, se [schema creation](/prowlarr/postgres-setup#schema-creation).

### Oprettelse af skema

Vi skal fortælle Prowlarr at bruge Postgres. `config.xml`-filen skal allerede være udfyldt med de indtastninger, vi har brug for:

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

Først **efter at have oprettet** begge databaser kan du starte Prowlarr-migreringen fra SQLite til Postgres.

## Migrering af data

> Hvis du ikke ønsker at migrere en eksisterende SQLite-database til Postgres, er du allerede færdig med denne guide! {.is-info}

For at migrere data kan vi bruge [PGLoader](https://github.com/dimitri/pgloader). Det har dog nogle faldgruber:

- Som standard er transaktioner ikke skriftstørrelsessensitive, vi bruger `--with "quote identifiers"` for at gøre dem følsomme.
- Versionen, der er pakket i Debian og Ubuntu's apt-repo, er for gammel til nyere versioner af Postgres (Roxedus har ikke testet pakkerne i andre distributioner).
  Roxedus [har bygget en binær fil](https://github.com/Roxedus/Pgloader-bin) for at aktivere denne understøttelse (der var ikke behov for nogen kodeændring, den skulle bare bygges med opdaterede afhængigheder).

> Drop ikke nogen tabeller i Postgres-instansen {.is-danger}

Inden du starter en migrering, skal du sikre dig, at du har kørt Prowlarr mod de oprettede Postgres-databaser **mindst én gang med succes**. Begynd migreringen ved at gøre følgende:

1. Stop Prowlarr
1. Åbn dit foretrukne databaseadministration-værktøj og opret forbindelse til Postgres-databaseinstansen
1. Start migreringen ved at bruge en af disse muligheder:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" prowlarr.db 'postgresql://qstick:qstick@localhost/prowlarr-main'
      ```

    - ```bash
      docker run --rm -v /absolut/sti/til/prowlarr.db:/prowlarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /prowlarr.db "postgresql://qstick:qstick@localhost/prowlarr-main"
      ```

  > Hvis du oplever en fejl ved brug af pgloader, kan det skyldes, at din database er for stor. For at løse dette skal du prøve at tilføje `--with "prefetch rows = 100" --with "batch size = 1MB"` til den ovenstående kommando
  {.is-warning}

  > Når dette er håndteret, er det ret ligetil efter at have fortalt den ikke at ændre skemaet ved hjælp af `--with "data only"`
  {.is-info}

1. Start Prowlarr