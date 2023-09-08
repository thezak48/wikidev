---
title: Konfigurera Prowlarr med PostgreSQL-databas
description: Konfigurera Prowlarr med en PostgreSQL-databas
published: true
date: 2022-11-29T13:19:38.953Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:38:53.538Z
---

# Prowlarr och Postgres

Detta dokument kommer att gå igenom de viktigaste punkterna för att migrera och konfigurera Postgres-stöd i Prowlarr.

Denna guide har skapats av den fantastiska [Roxedus](https://github.com/Roxedus).

> Postgres-databaser säkerhetskopieras inte av Prowlarr, eventuella säkerhetskopior måste implementeras och underhållas av användaren
{.is-danger}

## Konfigurera Postgres

Först behöver vi en Postgres-instans. Denna guide är skriven för användning av Docker-bilden `postgres:14`.

> Tänk inte ens på att använda taggen `latest`! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=prowlarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Skapande av databas

Prowlarr behöver två databaser, de förvalda namnen på dessa är:

- `prowlarr-main`   Denna används för att lagra all konfiguration och historik
- `prowlarr-log`    Denna används för att lagra händelser som genererar en loggpost

> Prowlarr kommer inte att skapa databaserna åt dig. Se till att du skapar dem i förväg{.is-warning}

Skapa de ovan nämnda databaserna med hjälp av din favoritmetod - till exempel [pgAdmin](https://www.pgadmin.org/) eller [Adminer](https://www.adminer.org/).

> För att `Housekeeping`-uppgiften ska köras måste denna användare vara en superanvändare, eftersom den utför vakuumuppgiften{.is-info}

Du kan ge databaserna vilket namn du vill, men se till att `config.xml`-filen har de korrekta namnen. För ytterligare information, se [schema creation](/prowlarr/postgres-setup#schema-creation).

### Skapande av schema

Vi måste berätta för Prowlarr att använda Postgres. `config.xml` bör redan vara ifylld med de poster vi behöver:

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

Om du vill ange ett databasnamn bör du också inkludera följande konfiguration:

```xml
<PostgresMainDb>MainDbName</PostgresMainDb>
<PostgresLogDb>LogDbName</PostgresLogDb>
```

Endast **efter att ha skapat** båda databaserna kan du starta Prowlarr-migreringen från SQLite till Postgres.

## Migrering av data

> Om du inte vill migrera en befintlig SQLite-databas till Postgres är du redan klar med denna guide! {.is-info}

För att migrera data kan vi använda [PGLoader](https://github.com/dimitri/pgloader). Det har dock vissa saker att tänka på:

- Som standard är transaktioner skiftlägesokänsliga, vi använder `--with "quote identifiers"` för att göra dem känsliga.
- Versionen som paketeras i Debians och Ubuntus apt-repo är för gammal för nyare versioner av Postgres (Roxedus har inte testat paket i andra distributioner).
  Roxedus [byggde en binär](https://github.com/Roxedus/Pgloader-bin) för att möjliggöra detta stöd (ingen kodmodifiering behövdes, det behövde bara byggas med uppdaterade beroenden).

> Radera inte några tabeller i Postgres-instansen {.is-danger}

Innan du startar en migrering, se till att du har kört Prowlarr mot de skapade Postgres-databaserna **minst en gång framgångsrikt**. Påbörja migreringen genom att göra följande:

1. Stoppa Prowlarr
1. Öppna ditt föredragna databashanteringsverktyg och anslut till Postgres-databasinstansen
1. Starta migreringen genom att använda något av dessa alternativ:

    - ```bash
      pgloader --with "quote identifiers" --with "data only" prowlarr.db 'postgresql://qstick:qstick@localhost/prowlarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/prowlarr.db:/prowlarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /prowlarr.db "postgresql://qstick:qstick@localhost/prowlarr-main"
      ```

  > Om du upplever ett fel när du använder pgloader kan det bero på att din databas är för stor, för att lösa detta kan du försöka lägga till `--with "prefetch rows = 100" --with "batch size = 1MB"` till ovanstående kommando
  {.is-warning}

  > Med dessa hanterade är det ganska enkelt efter att ha sagt åt det att inte ändra schemat med `--with "data only"`
  {.is-info}

1. Starta Prowlarr