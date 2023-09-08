---
title: Docker Guide
description: Servarr Docker Guide - Oversikt over Docker-konsepter, hardlink-konsepter og eierskap og tillatelser i Linux
published: true
date: 2023-07-15T20:41:38.016Z
tags: 
editor: markdown
dateCreated: 2021-05-16T20:23:46.192Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Den beste Docker-oppsettet](#den-beste-docker-oppsettet)
- [Portainer](#portainer)
- [Introduksjon](#introduksjon)
- [Flere brukere og en delt gruppe](#flere-brukere-og-en-delt-gruppe)
  - [Tillatelser](#tillatelser)
  - [UMASK](#umask)
  - [PUID og PGID](#puid-og-pgid)
  - [Eksempel](#eksempel)
- [Enkeltbruker og valgfri delt gruppe](#enkeltbruker-og-valgfri-delt-gruppe)
- [Eierskap og tillatelser for /config](#eierskap-og-tillatelser-for-config)
- [Konsistente og godt planlagte stier](#konsistente-og-godt-planlagte-stier)
  - [Eksempler](#eksempler)
    - [Torrenter](#torrenter)
    - [Usenet](#usenet)
    - [Medieserver](#medieserver)
    - [Sonarr, Radarr og Lidarr](#sonarr-radarr-og-lidarr)
  - [Problemer](#problemer)
- [Kjøre containere ved hjelp av](#kjøre-containere-ved-hjelp-av)
  - [Docker Compose](#docker-compose)
    - [Oppdater alle bilder og containere](#oppdater-alle-bilder-og-containere)
    - [Oppdater individuelt bilde og container](#oppdater-individuelt-bilde-og-container)
  - [docker run](#docker-run)
  - [Systemd](#systemd)
- [Nyttige kommandoer](#nyttige-kommandoer)
  - [Liste over kjørende containere](#liste-over-kjørende-containere)
  - [Shell *inne i* en container](#shell-inne-i-en-container)
  - [Rens Docker](#rens-docker)
  - [Få docker run-kommando](#få-docker-run-kommando)
  - [Få docker-compose](#få-docker-compose)
  - [Feilsøke nettverk](#feilsøke-nettverk)
  - [Rekursivt endre eier og gruppe](#rekursivt-endre-eier-og-gruppe)
  - [Rekursivt endre chmod til 775/664](#rekursivt-endre-chmod-til-775664)
  - [Finn UID/GID for bruker](#finn-uidgid-for-bruker)
  - [Undersøk filer for hardlinker](#undersøk-filer-for-hardlinker)
- [Interessante Docker-bilder](#interessante-docker-bilder)
  - [Alt-i-ett-løsninger](#alt-i-ett-løsninger)
- [Tilpasset Docker-nettverk og DNS](#tilpasset-docker-nettverk-og-dns)
- [Vanlige problemer](#vanlige-problemer)
  - [Riktige *eksterne* stier, feil *interne* stier](#riktige-eksterne-stier-feil-interne-stier)
  - [Kjøre Docker-containere som rot eller endre brukere](#kjøre-docker-containere-som-rot-eller-endre-brukere)
  - [Kjøre Docker-containere med umask 000](#kjøre-docker-containere-med-umask-000)
- [Få hjelp](#få-hjelp)
  - [Chat-støtte (Discord)](#chat-støtte-discord)
  - [Forumstøtte (Reddit)](#forumstøtte-reddit)

# Den beste Docker-oppsettet

**TL;DR**: En [eponym](https://www.lexico.com/en/definition/eponymous) bruker per daemon og en delt gruppe med en umask på `002`. Konsistente sti-definisjoner mellom *alle* containere som opprettholder mappenstrukturen. Bruk en volum (slik at nedlastingsmappen og biblioteksmappen er på samme filsystem) for å gjøre [hardlinker](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-hardlinks) og [øyeblikkelige flyttinger (atomiske flyttinger)](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-instant-moves-atomic-moves) mulig for Sonarr, Radarr, Lidarr og Readarr. Og fremfor alt, ignorer *mesteparten* av Docker-bildets sti-dokumentasjon!

> Merk: Mange finner [TRaSH's Hardlink Tutorial](https://trash-guides.info/hardlinks/) nyttig og enklere å forstå enn denne veiledningen. Denne veiledningen er mer konseptuell, mens TRaSH's opplæring tar deg gjennom prosessen.
{.is-info}

# Portainer

> **Portainer bør unngås for å sette opp Docker-containere** {.is-danger}

- Portainer gir et pent GUI for å administrere containere, men det er alt det er nyttig for.
- Portainer bør kun brukes for å vise docker-containerlogger / containerstatus.
- Det anbefales sterkt å bruke Docker Compose og ikke bruke Portainer.
- Portainer har mange problemer, som for eksempel:
  - Feil rekkefølge på kilde og mål for monteringer
  - Inkonsistent forskjell på store og små bokstaver
  - Ingen automatisk opprettede egendefinerte nettverk for kommunikasjon mellom containere
  - Inkonsistente implementeringer av compose på forskjellige arkitekturer
  - Henter hver tagg ved oppdatering når du ikke angir en spesifikk tagg
  - Evner er skjulte og noen fungerer ikke i det hele tatt på ARM-plattformer

Se denne [Docker-guiden](/docker-guide) og [TRaSH's Docker-opplæring](https://trash-guides.info/hardlinks/) i stedet for hvordan du setter opp Docker Compose.

# Introduksjon

Denne artikkelen vil ikke vise deg spesifikke detaljer om det beste Docker-oppsettet, men den beskriver en oversikt som du kan bruke til å gjøre ditt eget oppsett så bra som mulig. Ideen er at du kjører hver Docker-container som sin egen bruker, med en delt gruppe og konsistente volumer, slik at hver container ser den samme stistrukturen. Dette er lett å si, men ikke så lett å forstå og forklare.

> Husk at mange finner [TRaSH's Hardlink Tutorial](https://trash-guides.info/hardlinks/) nyttig og enklere å forstå enn denne veiledningen. Denne veiledningen er mer konseptuell, mens TRaSH's opplæring tar deg gjennom prosessen.
{.is-warning}

# Flere brukere og en delt gruppe

## Tillatelser

Ideelt sett kjører hver programvare som sin egen bruker, og de er alle en del av en delt gruppe med mappe-tilganger satt til `775` (`drwxrwxr-x`) og filer satt til `664` (`-rw-rw-r--`), som er en umask på `002`. Et fornuftig alternativ til dette er en enkelt delt bruker, som ville bruke `755` og `644`, som er en umask på `022`. Du kan begrense tillatelsene enda mer ved å nekte lesing fra "andre", som ville være en umask på `007` for en bruker per daemon eller `077` for en enkelt delt bruker. For en dypere forklaring, prøv Arch Linux-wiki-artiklene om [filrettigheter og attributter](https://wiki.archlinux.org/index.php/File_permissions_and_attributes) og [UMASK](https://wiki.archlinux.org/index.php/Umask).

## UMASK

Mange Docker-bilder godtar `-e UMASK=002` som en miljøvariabel, og noen programvare kan konfigureres med en bruker, gruppe og umask (NZBGet) eller mappe-/filrettighet (Sonarr/Radarr), inne i containeren. Dette vil sikre at filer og mapper opprettet av *en* kan leses og skrives av de andre. Hvis du bruker eksisterende mapper og filer, må du også fikse deres nåværende eierskap og tillatelser, men fremover vil de være riktige fordi du har satt opp hver programvare riktig.

## PUID og PGID

Mange Docker-bilder tar også en `-e PUID=123` og `-e PGID=321` som lar deg endre UID/GID som brukes inne i containeren til en konto på utsiden. Hvis du noen gang ser inni, vil du finne at brukernavnet er noe som `abc`, `nobody` eller `hotio`, men fordi det bruker UID/GID-en du sender inn, ser det ut som forventet bruker på utsiden. Hvis du bruker lagring fra et annet system via NFS eller CIFS, vil det gjøre livet ditt enklere hvis *det* systemet også har samsvarende brukere og gruppe. Kanskje la ett system velge UID/GID-ene, og deretter bruke dem på det andre systemet, forutsatt at de ikke kommer i konflikt.

## Eksempel

Du kjører [Sonarr](https://github.com/Sonarr/Sonarr/releases) ved hjelp av [hotio/sonarr](https://github.com/hotio/docker-sonarr), du har opprettet en `sonarr`-bruker med uid `123` og en delt gruppe `media` med gid `321` som `sonarr`-brukeren er medlem av. Du konfigurerer Docker-bildet til å kjøre med `-e PUID=123 -e PGID=321 -e UMASK=002`. Sonarr lar deg også konfigurere brukeren, gruppen samt mappe- og filrettigheter. De tidligere innstillingene skal negere disse, men du kan konfigurere dem hvis du ønsker det. En UMASK på `002` resulterer i `775` (`drwxrwxr-x`) for mapper og `664` (`-rw-rw-r--`) for filer, og bruker/gruppe er litt vanskelig fordi *inne i* containeren har de et annet navn. Typisk er de `abc` eller `nobody`.

# Enkeltbruker og valgfri delt gruppe

En annen populær og antagelig enklere alternativ er en enkelt, delt bruker. Kanskje til og med *din* bruker. Det er ikke like sikkert og følger ikke beste praksis, men til syvende og sist er det enklere å forstå og implementere. UMASK for dette er `022`, som resulterer i `755` (`drwxr-xr-x`) for mapper og `644` (`-rw-r--r--`) for filer. Gruppen betyr ikke så mye lenger, så du vil sannsynligvis bare bruke gruppen som er oppkalt etter brukeren. Dette gjør det imidlertid vanskeligere å dele med *andre* brukere, så du kan ende opp med å ønske en UMASK på `002` selv med dette oppsettet.

# Eierskap og tillatelser for /config

Ikke glem at ditt `/config`-volum også må ha riktig eierskap og tillatelser, vanligvis daemonens bruker og den brukerens gruppe som `sonarr:sonarr` og en umask på `022` eller `077`, slik at *bare* den brukeren har tilgang. I et enkeltbrukeroppsett vil dette selvfølgelig være den ene brukeren du har valgt.

# Konsistente og godt planlagte stier

> Mange finner [TRaSH's Hardlink Tutorial](https://trash-guides.info/hardlinks) nyttig og enklere å forstå enn denne veiledningen. Denne veiledningen er mer konseptuell, mens TRaSH's opplæring tar deg gjennom prosessen.
{.is-info}

Det enkleste og viktigste detaljen er å opprette enhetlige sti-definisjoner på tvers av alle containerne.

Hvis du lurer på hvorfor hardlinker ikke fungerer, eller hvorfor en enkel flytting tar mye lenger tid enn den burde, forklarer denne delen det. Stiene du bruker *inne i* betyr noe. På grunn av hvordan Docker-volumer fungerer, hvis du passerer inn to volumer som for eksempel de vanligvis foreslåtte `/tv`, `/movies` og `/downloads`, ser de ut som to forskjellige filsystemer, selv om de er et enkelt filsystem utenfor containeren. Dette betyr at hardlinker ikke vil fungere *og* i stedet for en øyeblikkelig/atomisk flytting, brukes en tregere og mer IO-intensiv kopi+slett. Hvis du har flere nedlastingsklienter fordi du bruker torrents og usenet, betyr det å ha en enkelt `/downloads`-sti at de vil bli blandet sammen. Fordi Radarr i en container vil spørre NZBGet i sin egen container hvor filene er, betyr det å bruke samme sti i begge at alt vil fungere. Hvis du ikke gjør det, må du fikse det med en ekstern stiavbildning.

Så velg *én* sti-layout og bruk den for alle. Det anbefales å bruke `/data`, men det er andre vanlige navn som `/shared`, `/media` eller `/dvr`. Å holde dette det samme på utsiden *og* inni vil gjøre oppsettet ditt enklere: én sti å huske eller hvis du integrerer Docker og nativ programvare. For eksempel kan Synology bruke `/Volume1/data` og unRAID kan bruke `/mnt/user/data` på utsiden, men `/data` på innsiden fungerer fint.

Det er også viktig å huske at du må sette opp eller konfigurere stier i programvaren som kjører *inne i* disse Docker-containerne. Hvis du endrer stiene for nedlastingsklienten din, må du redigere innstillingene for å matche og sannsynligvis oppdatere eksisterende torrents. Hvis du endrer biblioteksstien din, må du endre disse innstillingene i Sonarr, Radarr, Lidarr, Plex, osv.

## Eksempler

Det som betyr noe her er den generelle strukturen, ikke navnene. Du kan velge mappenavn som gir mening for deg. Og det er også andre måter å organisere ting på. For eksempel er det lite sannsynlig at du laster ned og kjører inn i konflikter med identiske utgivelser mellom usenet og torrents, så du *kan* legge begge i `/data/downloads/{movies|books|music|tv}`-mapper. Nedlastinger trenger ikke engang å sorteres i undermapper heller, siden filmer, musikk og tv sjelden vil komme i konflikt.

Denne eksempel-mappen `data` har undermapper for torrents og usenet, og hver av disse har undermapper for tv-, film- og musikknedlastinger for å holde ting ryddig. Mappen `media` har pent navngitte undermapper som `tv`, `movies`, `books` og `music`. Denne `media`-mappen er biblioteket ditt og det du ville sendt til Plex, Kodi, Emby, Jellyfin, osv.

For eksempelet nedenfor er `data` ekvivalent med vertsstien `/host/data` og Docker-stien `/data`

```none
    data
    ├── torrents
    │  ├── movies
    │  ├── music
    |  ├── books
    │  └── tv
    ├── usenet
    │  ├── movies
    │  ├── music
    │  ├── books
    │  └── tv
    └── media
        ├── movies
        ├── music
        ├── books
        └── tv
```

Stien for hver Docker-container kan være så spesifikk som nødvendig, samtidig som den opprettholder riktig struktur:

### Torrenter

```none
    data
    └── torrents
        ├── movies
        ├── music
        ├── books
        └── tv
```

Torrenter trenger bare tilgang til torrentfiler, så pass `-v /host/data/torrents:/data/torrents`. I innstillingene for torrent-programvaren må du konfigurere stier på nytt, og du kan sortere i undermapper som `/data/torrents/{tv|books|movies|music}`.

### Usenet

```none
    data
    └── usenet
        ├── movies
        ├── music
        └── tv
```

Usenet trenger bare tilgang til usenet-filer, så pass `-v /host/data/usenet:/data/usenet`. I innstillingene for usenet-programvaren må du konfigurere stier på nytt, og du kan sortere i undermapper som `/data/usenet/{tv|movies|music}`.

### Medieserver

```none
    data
    └── media
        ├── movies
        ├── music
        └── tv
```

Plex/Emby trenger bare tilgang til mediebiblioteket ditt, så pass `-v /host/data/media:/data/media`, som kan ha et hvilket som helst antall undermapper som `movies`, `kids movies`, `tv`, `documentary tv` og/eller `music` som undermapper.

### Sonarr, Radarr og Lidarr

```none
    data
    ├── torrents
    │  ├── movies
    │  ├── music
    │  └── tv
    ├── usenet
    │  ├── movies
    │  ├── music
    │  └── tv
    └── media
        ├── movies
        ├── music
        └── tv
```

Sonarr, Radarr og Lidarr får alt ved å bruke `-v /host/data:/data` fordi *nedlastings*-mappen(e) og *media*-mappen vil se ut som og *være* ett filsystem. Hardlinker vil fungere, og flyttinger vil være atomiske, i stedet for kopi + slett.

## Problemer

Det er et par mindre problemer med å ikke følge Docker-bildets foreslåtte stier.

Det største problemet er at volumene som er definert i `dockerfile` vil bli opprettet hvis de ikke er spesifisert. Dette betyr at de vil hope seg opp når du sletter og gjenoppretter containerne. Hvis de inneholder data, kan de uventet ta opp plass og sannsynligvis på et uegnet sted. Du kan finne en [oppryddingskommando](#prune-docker) i den nyttige kommandoer-seksjonen nedenfor. Dette kan også løses ved å sende inn en tom mappe for alle volumene du ikke vil bruke, for eksempel `/data/empty:/movies` og `/data/empty:/downloads`. Kanskje til og med legge en fil med navnet "BRUK IKKE DENNE MAPPEN" inni, for å minne deg selv.

Et annet problem er at noen bilder er forhåndskonfigurert til å bruke de dokumenterte volumene, så du må endre innstillingene i programvaren inne i Docker-containeren. Heldigvis, siden konfigurasjonen lagres utenfor containeren, er dette et engangsproblem. Du kan også velge en sti som `/data` eller `/media`, som noen bilder allerede definerer for en spesifikk bruk. Det burde ikke være et problem, men det kan bli litt mer forvirrende når det kombineres med de tidligere problemene. Til syvende og sist er det verdt det for å få hardlinker og raske flyttinger. Konsistensen og enkelheten er også velkomne bieffekter.

Hvis du bruker den nyeste versjonen av den forlatte [RadarrSync](https://github.com/Sperryfreak01/RadarrSync) for å synkronisere to Radarr-instanser, *avhenger* det av å mappe *samme* sti inni til en annen sti på utsiden, for eksempel `/movies` for en instans vil peke på `/data/media/movies` og den andre på `/data/media/movies4k`. Dette ødelegger *alt* du har lest ovenfor. Det finnes ingen god løsning, du kan enten bruke den gamle versjonen som ikke er like god, gjøre mappingen på en stygg måte som ødelegger hardlinker, eller bare ikke bruke det i det hele tatt.

# Kjøre containere ved hjelp av

## Docker Compose

Dette er det beste alternativet for de fleste brukere, det lar deg kontrollere og konfigurere mange containere og deres avhengigheter i en enkelt fil. Et godt utgangspunkt er Docker sin egen [Kom i gang med Docker Compose](https://docs.docker.com/compose/gettingstarted/). Du kan bruke [composerize](https://composerize.com) eller [ghcr.io/red5d/docker-autocompose](#get-docker-compose) for å konvertere `docker run`-kommandoer til en enkelt `docker-compose.yml`-fil.

> Det følgende er *ikke* et komplett fungerende eksempel! Containerne har bare PID, UID, UMASK og eksempelstier definert for å holde det enkelt.
{.is-warning}

```yml
    # sonarr
    Sonarr:
        image: cr.hotio.dev/hotio/sonarr
        volumes:
            - /path/to/config/sonarr:/config
            - /host/data:/data
        environment:
            - PUID=111
            - PGID=321
            - UMASK=002

    # deluge
    Deluge:
        image: binhex/arch-delugevpn
        volumes:
            - /path/to/config/deluge:/config
            - /host/data/torrents:/data/torrents
        environment:
            - PUID=222
            - PGID=321
            - UMASK=002

    # SABnzbd
    SABnzbd:
        image: cr.hotio.dev/hotio/sabnzbd
        volumes:
            - /path/to/config/sabnzbd:/config
            - /host/data/usenet:/data/usenet
        environment:
            - PUID=333
            - PGID=321
            - UMASK=002

    # plex
    Plex:
        image: cr.hotio.dev/hotio/plex
        volumes:
            - /path/to/config/plex:/config
            - /host/data/media:/data/media

        environment:
            - PUID=444
            - PGID=321
            - UMASK=002
```

### Oppdater alle bilder og containere

```shell
    docker-compose pull
    docker-compose up -d
```

### Oppdater individuelt bilde og container

```shell
    docker-compose pull NAME
    docker-compose up -d NAME
```

## docker run

> Som eksempelet med Docker Compose ovenfor, er følgende `docker run`-kommandoer forenklet til *kun* PUID, PGID, UMASK og volumer for å fungere som et tydelig eksempel.
{.is-warning}

```shell
    # sonarr
    docker run -v /path/to/config/sonarr:/config \
               -v /host/data:/data \
               -e PUID=111 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sonarr

    # deluge
    docker run -v /path/to/config/deluge:/config \
               -v /host/data/torrents:/data/torrents \
               -e PUID=222 -e PGID=321 -e UMASK=002 \
               binhex/arch-delugevpn

    # SABnzbd
    docker run -v /path/to/config/sabnzbd:/config \
               -v /host/data/usenet:/data/usenet \
               -e PUID=333 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sabnzbd

    # plex
    docker run -v /path/to/config/plex:/config \
               -v /host/data/media:/data/media \
               -e PUID=444 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/plex
```

## Systemd

For å vedlikeholde noen få Docker-containere kan du bruke systemd. Det standardiserer kontrollen og forenkler avhengighetene for både native og Docker-tjenester. Det generiske eksempelet nedenfor kan tilpasses til hvilken som helst container ved å justere eller legge til ulike verdier og alternativer.

```shell
    # /etc/systemd/system/thing.service
    [Unit]
    Description=Thing
    Requires=docker.service
    After=network.target docker.service

    [Service]
    ExecStart=/usr/bin/docker run --rm \
                              --name=thing \
                              -v /path/to/config/thing:/config \
                              -v /host/data:/data
                              -e PUID=111 -e PGID=321 -e UMASK=002 \
                              nobody/thing

    ExecStop=/usr/bin/docker stop -t 30 thing

    [Install]
    WantedBy=default.target
```

# Nyttige kommandoer

## Liste over kjørende containere

```shell
    docker ps
```

## Kjør en kommandolinje *innenfor* en container

Å kjøre en kommando inne i en container vil vanligvis logge deg inn som root.

```shell
    docker exec -it CONTAINER_NAME /bin/bash
```

Når du er inne, kan du bytte bruker med

```shell
    su - <brukernavn>
```

For å kjøre som en spesifikk bruker, legg til `-u` som et argument og pass brukernavnet eller ID-en

```shell
    docker exec -u BRUKER -it CONTAINER_NAME /bin/bash
```

### Eksempler som spesifikke brukere

#### LSIO Radarr

```shell
    docker exec -u abc -it radarr bash
```

#### Hotio Sonarr

```shell
    docker exec -u hotio -it sonarr bash
```

For mer informasjon, se [docker exec](https://docs.docker.com/engine/reference/commandline/exec/)-dokumentasjonen.

## Rens Docker

```shell
    docker system prune --all --volumes
```

> Fjerner ubrukte containere, nettverk, volumer, bilder og byggbuffer. Som advarselen denne kommandoen gir, vil den fjerne alle de tidligere nevnte elementene for alt som ikke er i bruk av en kjørende container. I et riktig konfigurert miljø er dette greit. Men vær oppmerksom og gå forsiktig frem første gang. Se [Docker system prune](https://docs.docker.com/engine/reference/commandline/system_prune/)-dokumentasjonen for flere detaljer.
{.is-warning}

## Få docker run-kommandoen

Det kan være vanskelig å få `docker run`-kommandoen fra GUI-verktøy, men dette Docker-bildet gjør det enkelt for en kjørende container ([kilde](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container)).

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike CONTAINER_NAME
```

## Få docker-compose

> I tillegg kan du sjekke ut [TRaSH's Guide for docker-compose](https://trash-guides.info/compose/)
{.is-info}

Det er mulig å få en `docker-compose.yml` fra kjørende instanser med [docker-autocompose](https://github.com/Red5d/docker-autocompose), i tilfelle du allerede har startet containerne dine med `docker run` eller `docker create` og ønsker å bytte til `docker-compose`-stil. Det er også flott for å dele innstillingene dine med andre, siden det ikke spiller noen rolle hvilken administrasjonsprogramvare du bruker. Det siste argumentet/argumentene er navnene på containerne dine, og du kan sende inn så mange som trengs samtidig. Det første containernavnet er påkrevd, flere er valgfritt. Du kan se containernavnene i **NAMES**-kolonnen i `docker ps`, de er vanligvis satt av deg eller kan genereres basert på bildet, for eksempel `binhex-qbittorrent`. Det er *ikke* bildets navn, som for eksempel `binhex/arch-qbittorrentvpn`.

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $CONTAINER_NAME $ANOTHER_CONTAINER_NAME ... $ONE_MORE_CONTAINER_NAME
```

For noen brukere kan dette være:

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose lidarr prowlarr radarr readarr sonarr qbittorrent
```

## Feilsøke nettverk

De fleste Docker-bilder har ikke mange nyttige verktøy for feilsøking, men du kan [koble til et nettverksfeilsøkingsverktøy](https://hub.docker.com/r/nicolaka/netshoot) til en eksisterende container for å hjelpe med det.

```shell
    docker run -it --rm --network container:CONTAINER_NAME nicolaka/netshoot
```

## Rekursivt endre eier og gruppe

```shell
    chown -R bruker:gruppe /noen/sti/her
```

## Rekursivt endre chmod til 775/664

```shell
    chmod -R a=,a+rX,u+w,g+w /noen/sti/her
              ^  ^    ^   ^ legger til skrivetilgang for gruppen
              |  |    | legger til skrivetilgang for brukeren
              |  | legger til lesetilgang for alle og kjøretillatelse for alle mapper (som kontrollerer tilgang)
              | setter alle til `000`
```

## Finn UID/GID for bruker

```shell
    id <brukernavn>
```

## Undersøk filer for hardlinker

```shell
    ls -alhi
    42207934 -rw-r--r--  2 bruker gruppe    0 Sep 11 11:55 # hardlinket
    42207936 -rw-r--r--  1 bruker gruppe    0 Sep 11 11:55 # ingen hardlinker
    42207934 -rw-r--r--  2 bruker gruppe    0 Sep 11 11:55 # original

    stat original
      File: original
      Size: 0               Blocks: 0          IO Block: 4096   regular empty file
    Device: 803h/2051d      Inode: 42207934    Links: 2
    Access: (0644/-rw-r--r--)  Uid: ( 1000/ bruker)   Gid: ( 1001/ gruppe)
    Access: 2020-09-11 11:55:43.803327144 -0500
    Modify: 2020-09-11 11:55:43.803327144 -0500
    Change: 2020-09-11 11:55:49.706660476 -0500
     Birth: 2020-09-11 11:55:43.803327144 -0500
```

# Interessante Docker-bilder

- [rasmunk/sshfs](https://github.com/rasmunk/docker-volume-sshfs)
{.links-list}
- [hotio’s](https://hotio.dev/) Dokumentasjonen og Dockerfile gir ingen dårlige stisuggereringer. Bilder oppdateres automatisk 2 ganger i timen hvis endringer blir funnet. Hotio bygger også våre Pull Requests (unntatt Sonarr), noe som kan være nyttig for testing.
  - [sonarr](https://hotio.dev/containers/sonarr)
  - [radarr](https://hotio.dev/containers/radarr)
  - [lidarr](https://hotio.dev/containers/lidarr)
  - [readarr](https://hotio.dev/containers/readarr)
  - [prowlarr](https://hotio.dev/containers/prowlarr) for usenet og torrent tracker-søk
  - [qbittorrent](https://hotio.dev/containers/qbittorrent/)
  - [NZBGet](https://hotio.dev/containers/nzbget/)
  - [SABnzbd](https://hotio.dev/containers/sabnzbd/)
  - [qflood](https://hotio.dev/containers/qflood/)
  - [ombi](https://hotio.dev/containers/ombi) for å be om media
  - [overseerr](https://hotio.dev/containers/overseerr/) for å be om media
  - [jackett](https://hotio.dev/containers/jackett) for torrent tracker-søk
  - [nzbhydra2](https://hotio.dev/containers/nzbhydra2) for usenet-indeks-søk
  - [bazarr](https://hotio.dev/containers/bazarr) for undertekster
  - [pullio](https://hotio.dev/pullio/) for automatisk oppdatering av containere
  - [unpackerr](https://hotio.dev/containers/unpackerr) er nyttig for utpakking av pakkede torrents på tvers av ulike torrentklienter der utpakking mangler eller er helt fraværende.
{.links-list}
- [linuxserver.io](https://hub.docker.com/u/linuxserver) bilder har bilder for *mange* programvare og de er godt vedlikeholdt. Unngå imidlertid deres 'foreslåtte (valgfritt)' stier.
  - [SWAG Proxy](https://hub.docker.com/r/linuxserver/swag)
  - [qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/)
  - [deluge](https://hub.docker.com/r/linuxserver/deluge/)
  - [rtorrent](https://hub.docker.com/r/linuxserver/rutorrent/)
  - [SABnzbd](https://hub.docker.com/r/linuxserver/sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/)
  - [sonarr](https://hub.docker.com/r/linuxserver/sonarr/)
  - [radarr](https://hub.docker.com/r/linuxserver/radarr/)
  - [lidarr](https://hub.docker.com/r/linuxserver/lidarr/)
- [binhex](https://hub.docker.com/u/binhex) en annen populær vedlikeholder
  - [qbittorrent](https://hub.docker.com/r/binhex/arch-qbittorrentvpn/)
  - [deluge](https://hub.docker.com/r/binhex/arch-delugevpn/)
  - [rtorrent](https://hub.docker.com/r/binhex/arch-rtorrentvpn/)
  - [SABnzbd](https://hub.docker.com/r/binhex/arch-sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/binhex/arch-nzbget/)
  - [sonarr](https://hub.docker.com/r/binhex/arch-sonarr/)
  - [radarr](https://hub.docker.com/r/binhex/arch-radarr/)
  - [lidarr](https://hub.docker.com/r/binhex/arch-lidarr/)
{.links-list}

### Alt-i-ett-løsninger

- [Dette er et GitHub-repositorium](https://github.com/Luctia/ezarr) rettet mot nybegynnere som ønsker å bruke Docker for sin Servarr-stakk. Det er i utgangspunktet en klar-til-bruk-samling av filer og krever bare at du kjører to ting for å få hele greia på nettet. Det fjerner bryderiet rundt brukeradministrasjon og tillatelser på vertsutstyret og har noen andre applikasjoner som PleX.

# Tilpasset Docker-nettverk og DNS

En interessant funksjon med et [tilpasset Docker-nettverk](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks) er at det får sin egen DNS-server. Hvis du oppretter et bro-nettverk for dine containere, kan du bruke vertsnavnene deres i konfigurasjonen din. For eksempel, hvis du `docker run --network=isolated --hostname=deluge binhex/arch-deluge` og `docker run --network=isolated --hostname=radarr binhex/arch-radarr`, kan du deretter konfigurere Nedlastingsklienten i Radarr til å peke bare på `deluge` og det vil fungere *og* kommunisere på sitt eget private nettverk. Det betyr at hvis du ønsket å være enda mer sikker, kunne du *stoppe* videresending av den porten også. Hvis du plasserer reverse proxy-containeren din på det samme nettverket, kan du til og med stoppe videresending av webgrensesnittsportene og gjøre dem enda mer sikre.

# Vanlige problemer

## Riktige *utvendige* stier, feil *innvendige* stier

Mange mennesker leser dette og tror de forstår, men de ender opp med å se den utvendige stien riktig til noe som `/data/usenet`, men så går de glipp av poenget og setter den *innvendige* stien til `/downloads` fortsatt.

- Bra:
  - `/host/data/usenet:/data/usenet`
  - `/data/media:/data/media`
- Dårlig:
  - `/host/data:/downloads`
  - `/host/data:/media`
  - `/data/downloads:/data`

## Kjøre Docker-containere som root eller endre brukere rundt

Hvis du kjører containerne dine som `root:root`, gjør du noe galt. Hvis du ikke sender inn en UID og GID, vil du bruke standardverdien for bildet, og *det* vil sannsynligvis ikke samsvare med en rimelig bruker på systemet ditt. Og hvis du endrer brukeren og gruppen som Docker-containerne dine kjører som, vil du sannsynligvis få tillatelsesproblemer på mapper som `/config`-mappen som sannsynligvis vil ha filer og mapper i seg som ble opprettet første gang med UID/GID du brukte første gang.

## Kjøre Docker-containere med umask 000

Hvis du finner deg selv med å sette en UMASK på `000` (som er 777 for mapper og 666 for filer), gjør du *også* noe galt. Det gjør filene og mappene dine lese/skrive for *alle*, noe som er dårlig Linux-hygiene.

# Få hjelp

## Chat-støtte (Discord)

- [Sonarr Discord](https://discord.sonarr.tv/)
- [Radarr Discord](https://radarr.video/discord)
{.links-list}

## Forumstøtte (Reddit)

- [/r/sonarr](http://reddit.com/r/sonarr)
- [/r/radarr](http://reddit.com/r/radarr)
{.links-list}