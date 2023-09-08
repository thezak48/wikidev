---
title: Docker Guide
description: Servarr Docker Guide - Oversigt over Docker-koncepter, hardlink-koncepter og Linux-ejerskab og -tilladelser
published: true
date: 2023-07-15T20:41:38.016Z
tags: 
editor: markdown
dateCreated: 2021-05-16T20:23:46.192Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Den bedste Docker-konfiguration](#den-bedste-docker-konfiguration)
- [Portainer](#portainer)
- [Introduktion](#introduktion)
- [Flere brugere og en delt gruppe](#flere-brugere-og-en-delt-gruppe)
  - [Tilladelser](#tilladelser)
  - [UMASK](#umask)
  - [PUID og PGID](#puid-og-pgid)
  - [Eksempel](#eksempel)
- [Enkelt bruger og valgfri delt gruppe](#enkelt-bruger-og-valgfri-delt-gruppe)
- [Ejerskab og tilladelser for /config](#ejerskab-og-tilladelser-for-config)
- [Konsistente og velplanlagte stier](#konsistente-og-velplanlagte-stier)
  - [Eksempler](#eksempler)
    - [Torrents](#torrents)
    - [Usenet](#usenet)
    - [Medieserver](#medieserver)
    - [Sonarr, Radarr og Lidarr](#sonarr-radarr-og-lidarr)
  - [Problemer](#problemer)
- [Kørsel af containere ved hjælp af](#kørsel-af-containere-ved-hjælp-af)
  - [Docker Compose](#docker-compose)
    - [Opdater alle billeder og containere](#opdater-alle-billeder-og-containere)
    - [Opdater individuelt billede og container](#opdater-individuelt-billede-og-container)
  - [docker run](#docker-run)
  - [Systemd](#systemd)
- [Nyttige kommandoer](#nyttige-kommandoer)
  - [Liste over kørende containere](#liste-over-kørende-containere)
  - [Shell *inde i* en container](#shell-inde-i-en-container)
  - [Ryd op i Docker](#ryd-op-i-docker)
  - [Få docker run-kommando](#få-docker-run-kommando)
  - [Få docker-compose](#få-docker-compose)
  - [Fejlfinding af netværk](#fejlfinding-af-netværk)
  - [Rekursivt ændre ejer og gruppe](#rekursivt-ændre-ejer-og-gruppe)
  - [Rekursivt ændre chmod til 775/664](#rekursivt-ændre-chmod-til-775664)
  - [Find UID/GID for bruger](#find-uidgid-for-bruger)
  - [Undersøg filer for hardlinks](#undersøg-filer-for-hardlinks)
- [Interessante Docker-billeder](#interessante-docker-billeder)
  - [Alt-i-en-løsninger](#alt-i-en-løsninger)
- [Tilpasset Docker-netværk og DNS](#tilpasset-docker-netværk-og-dns)
- [Almindelige problemer](#almindelige-problemer)
  - [Korrekte *eksterne* stier, forkerte *interne* stier](#korrekte-eksterne-stier-forkerte-interne-stier)
  - [Kørsel af Docker-containere som root eller ændring af brugere](#kørsel-af-docker-containere-som-root-eller-ændring-af-brugere)
  - [Kørsel af Docker-containere med umask 000](#kørsel-af-docker-containere-med-umask-000)
- [Få hjælp](#få-hjælp)
  - [Chat-support (Discord)](#chat-support-discord)
  - [Forum-support (Reddit)](#forum-support-reddit)

# Den bedste Docker-konfiguration

**TL;DR**: En [eponym](https://www.lexico.com/en/definition/eponymous) bruger pr. daemon og en delt gruppe med en umask på `002`. Konsistente sti-definitioner mellem *alle* containere, der opretholder mappestrukturen. Ved at bruge et enkelt volumen (så downloadmappen og biblioteksmappen er på samme filsystem) gør hardlinks og øjeblikkelige flytninger (atomiske flytninger) mulige for Sonarr, Radarr, Lidarr og Readarr. Og frem for alt, ignorer *de fleste* af Docker-billedets sti-dokumentation!

> Bemærk: Mange mennesker finder [TRaSH's Hardlink Tutorial](https://trash-guides.info/hardlinks/) nyttig og nemmere at forstå end denne vejledning. Denne vejledning er mere konceptuel, mens TRaSH's tutorial guider dig gennem processen.
{.is-info}

# Portainer

> **Portainer bør undgås til opsætning af Docker-containere** {.is-danger}

- Portainer giver et pænt GUI til administration af containere, men det er alt, det er nyttigt til.
- Portainer bør kun bruges til visning af Docker-containerlogs / containerstatus.
- Det anbefales stærkt at bruge Docker Compose og ikke bruge Portainer.
- Portainer har mange problemer, såsom:
  - Forkert rækkefølge af kilder og mål for monteringer
  - Inkonsistent forskel på store og små bogstaver
  - Ingen automatisk oprettelse af brugerdefinerede netværk til inter-container-kommunikation
  - Inkonsistente compose-implementeringer på forskellige arkitekturer
  - Henter alle tags ved opdatering, når du ikke angiver et specifikt tag
  - Evner er skjulte, og nogle fungerer slet ikke på ARM-platforme

Se denne [Docker Guide](/docker-guide) og [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) i stedet for at konfigurere Docker Compose.

# Introduktion

Denne artikel vil ikke vise dig specifikke detaljer om den bedste Docker-konfiguration, men den beskriver et overblik, som du kan bruge til at gøre din egen konfiguration så god som muligt. Ideen er, at du kører hver Docker-container som sin egen bruger, med en delt gruppe og konsistente volumener, så hver container ser den samme sti-layout. Dette er nemt at sige, men ikke så nemt at forstå og forklare.

> Husk på, at mange mennesker finder [TRaSH's Hardlink Tutorial](https://trash-guides.info/hardlinks/) nyttig og nemmere at forstå end denne vejledning. Denne vejledning er mere konceptuel, mens TRaSH's tutorial guider dig gennem processen.
{.is-warning}

# Flere brugere og en delt gruppe

## Tilladelser

Ideelt set kører hver software som sin egen bruger, og de er alle en del af en delt gruppe med mappe-tilladelser sat til `775` (`drwxrwxr-x`) og filer sat til `664` (`-rw-rw-r--`), hvilket er en umask på `002`. Et fornuftigt alternativ til dette er en enkelt delt bruger, der ville bruge `755` og `644`, hvilket er en umask på `022`. Du kan begrænse tilladelserne endnu mere ved at nægte læsning fra "andre", hvilket ville være en umask på `007` for en bruger pr. daemon eller `077` for en enkelt delt bruger. For en dybere forklaring kan du prøve Arch Linux-wiki-artiklerne om [fil-tilladelser og attributter](https://wiki.archlinux.org/index.php/File_permissions_and_attributes) og [UMASK](https://wiki.archlinux.org/index.php/Umask).

## UMASK

Mange Docker-billeder accepterer `-e UMASK=002` som en miljøvariabel, og nogle software kan konfigureres med en bruger, gruppe og umask (NZBGet) eller mappe-/fil-tilladelse (Sonarr/Radarr) inde i containeren. Dette sikrer, at filer og mapper, der oprettes af *én*, kan læses og skrives af de andre. Hvis du bruger eksisterende mapper og filer, skal du også rette deres nuværende ejerskab og tilladelser, men fremadrettet vil de være korrekte, fordi du har konfigureret hver software korrekt.

## PUID og PGID

Mange Docker-billeder tager også en `-e PUID=123` og `-e PGID=321`, der giver dig mulighed for at ændre UID/GID, der bruges indeni, til en konto udenfor. Hvis du nogensinde kigger indeni, vil du opdage, at brugernavnet er noget som `abc`, `nobody` eller `hotio`, men fordi det bruger den UID/GID, du passerer ind, ser det ud som den forventede bruger udenfor. Hvis du bruger lager fra et andet system via NFS eller CIFS, vil det gøre dit liv lettere, hvis *det* system også har matchende brugere og gruppe. Lad måske det ene system vælge UID/GID'erne og genbrug dem på det andet system, hvis de ikke konflikter.

## Eksempel

Du kører [Sonarr](https://github.com/Sonarr/Sonarr/releases) ved hjælp af [hotio/sonarr](https://github.com/hotio/docker-sonarr), du har oprettet en `sonarr`-bruger med UID `123` og en delt gruppe `media` med GID `321`, som `sonarr`-brugeren er medlem af. Du konfigurerer Docker-billedet til at køre med `-e PUID=123 -e PGID=321 -e UMASK=002`. Sonarr giver også mulighed for at konfigurere brugeren, gruppen samt mappe- og fil-tilladelser. De tidligere indstillinger skulle gøre disse indstillinger overflødige, men du kan konfigurere dem, hvis du ønsker det. En UMASK på `002` resulterer i `775` (`drwxrwxr-x`) for mapper og `664` (`-rw-rw-r--`) for filer, og bruger/gruppe er lidt tricky, fordi de *inde i* containeren har et andet navn. Typisk er de `abc` eller `nobody`.

# Enkelt bruger og valgfri delt gruppe

En anden populær og argumenteret nemmere mulighed er en enkelt, delt bruger. Måske endda *din* bruger. Det er ikke så sikkert og følger ikke bedste praksis, men i sidste ende er det nemmere at forstå og implementere. UMASK for dette er `022`, hvilket resulterer i `755` (`drwxr-xr-x`) for mapper og `644` (`-rw-r--r--`) for filer. Gruppen betyder ikke så meget længere, så du vil sandsynligvis bare bruge gruppenavnet efter brugeren. Dette gør det dog sværere at dele med *andre* brugere, så du ender måske stadig med at ønske en UMASK på `002` selv med denne konfiguration.

# Ejerskab og tilladelser for /config

Glem ikke, at dit `/config`-volumen også skal have korrekt ejerskab og tilladelser, normalt daemonens bruger og den brugers gruppe som f.eks. `sonarr:sonarr` og en umask på `022` eller `077`, så *kun* den bruger har adgang. I en enkelt bruger-konfiguration vil dette selvfølgelig være den ene bruger, du har valgt.

# Konsistente og velplanlagte stier

> Mange mennesker finder [TRaSH's Hardlink Tutorial](https://trash-guides.info/hardlinks) nyttig og nemmere at forstå end denne vejledning. Denne vejledning er mere konceptuel, mens TRaSH's tutorial guider dig gennem processen.
{.is-info}

Det nemmeste og vigtigste detalje er at oprette ensartede sti-definitioner på tværs af alle containere.

Hvis du spekulerer på, hvorfor hardlinks ikke virker, eller hvorfor en simpel flytning tager meget længere tid end den burde, forklarer denne sektion det. Stierne, du bruger *inde i* containeren, betyder noget. På grund af, hvordan Docker-volumener fungerer, når du passerer to volumener som f.eks. de almindeligt foreslåede `/tv`, `/movies` og `/downloads`, ser de ud som to forskellige filsystemer, selvom de er et enkelt filsystem uden for containeren. Dette betyder, at hardlinks ikke virker, og i stedet for en øjeblikkelig/atomisk flytning bruges en langsommere og mere IO-intensiv kopi+slet. Hvis du har flere downloadklienter, fordi du bruger torrents og usenet, betyder en enkelt `/downloads`-sti, at de bliver blandet sammen. Fordi Radarr i en container vil spørge NZBGet i sin egen container, hvor filerne er, vil det hele bare fungere ved at bruge den samme sti i begge tilfælde. Hvis du ikke gør det, skal du rette det med en fjernsti-kortlægning.

Så vælg *én* sti-layout og brug det for dem alle. Det anbefales at bruge `/data`, men der er andre almindelige navne som f.eks. `/shared`, `/media` eller `/dvr`. Ved at holde dette ens både udenfor og indeni vil din konfiguration blive enklere: én sti at huske eller hvis du integrerer Docker og native software. For eksempel kan Synology bruge `/Volume1/data` og unRAID kan bruge `/mnt/user/data` udenfor, men `/data` indeni er fint.

Det er også vigtigt at huske, at du skal opsætte eller genkonfigurere stier i softwaren, der kører *inde i* disse Docker-containere. Hvis du ændrer stierne for din downloadklient, skal du redigere dens indstillinger, så de passer, og sandsynligvis opdatere eksisterende torrents. Hvis du ændrer din bibliotekssti, skal du ændre disse indstillinger i Sonarr, Radarr, Lidarr, Plex osv.

## Eksempler

Det vigtige her er den generelle struktur, ikke navnene. Du er fri til at vælge mappenavne, der giver mening for dig. Og der er også andre måder at organisere tingene på. For eksempel er det usandsynligt, at du downloader og støder på konflikter mellem identiske udgivelser mellem usenet og torrents, så du *kunne* placere begge i `/data/downloads/{movies|books|music|tv}`-mapper. Downloads behøver heller ikke sorteres i undermapper, da film, musik og tv sjældent vil konflikte.

Denne eksempelmappe `data` har undermapper til torrents og usenet, og hver af disse har undermapper til tv-, film- og musikdownloads for at holde tingene pæne. Mappen `media` har pænt navngivne undermapper `tv`, `movies`, `books` og `music`. Denne `media`-mappe er dit bibliotek og det, du ville give til Plex, Kodi, Emby, Jellyfin osv.

For nedenstående eksempel er `data` ækvivalent med værtsstien `/host/data` og Docker-stien `/data`

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

Stien for hver Docker-container kan være så specifik, som det er nødvendigt, samtidig med at den opretholder den korrekte struktur:

### Torrents

```none
    data
    └── torrents
        ├── movies
        ├── music
        ├── books
        └── tv
```

Torrents har kun brug for adgang til torrentfiler, så giv den `-v /host/data/torrents:/data/torrents`. I torrent-softwarens indstillinger skal du genkonfigurere stier, og du kan sortere i undermapper som `/data/torrents/{tv|books|movies|music}`.

### Usenet

```none
    data
    └── usenet
        ├── movies
        ├── music
        └── tv
```

Usenet har kun brug for adgang til usenet-filer, så giv den `-v /host/data/usenet:/data/usenet`. I usenet-softwarens indstillinger skal du genkonfigurere stier, og du kan sortere i undermapper som `/data/usenet/{tv|movies|music}`.

### Medieserver

```none
    data
    └── media
        ├── movies
        ├── music
        └── tv
```

Plex/Emby har kun brug for adgang til dit mediebibliotek, så giv `-v /host/data/media:/data/media`, som kan have et hvilket som helst antal undermapper som f.eks. `movies`, `kids movies`, `tv`, `documentary tv` og/eller `music` som undermapper.

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

Sonarr, Radarr og Lidarr får alt ved at bruge `-v /host/data:/data`, fordi *download*-mappen(e) og *media*-mappen vil se ud som og *være* ét filsystem. Hardlinks vil virke, og flytninger vil være atomiske i stedet for kopi + slet.

## Problemer

Der er et par mindre problemer med ikke at følge Docker-billedets foreslåede stier.

Det største problem er, at volumener defineret i `dockerfile` vil blive oprettet, hvis de ikke er specificeret. Dette betyder, at de vil hobe sig op, når du sletter og genopretter containere. Hvis de ender med at have data i sig, kan de uventet forbruge plads og sandsynligvis på et uegnet sted. Du kan finde en [oprydningskommando](#prune-docker) i afsnittet med nyttige kommandoer nedenfor. Dette kan også afhjælpes ved at overføre en tom mappe til alle de volumener, du ikke ønsker at bruge, f.eks. `/data/empty:/movies` og `/data/empty:/downloads`. Du kan måske endda lægge en fil med navnet "BRUG IKKE DENNE MAPPE" indeni for at minde dig selv.

Et andet problem er, at nogle billeder er forudkonfigureret til at bruge de dokumenterede volumener, så du bliver nødt til at ændre indstillingerne i softwaren inde i Docker-containeren. Heldigvis, da konfigurationen persistere uden for containeren, er dette kun et problem én gang. Du kan også vælge en sti som f.eks. `/data` eller `/media`, som nogle billeder allerede definerer til en specifik brug. Det burde ikke være et problem, men det vil være lidt mere forvirrende, når det kombineres med de tidligere problemer. I sidste ende er det det værd for at få hard links og hurtige flytninger. Konsistensen og enkelheden er også velkomne sideeffekter.

Hvis du bruger den nyeste version af det forladte [RadarrSync](https://github.com/Sperryfreak01/RadarrSync) til at synkronisere to Radarr-instanser, *afhænger* det af at mappe den *samme* sti indeni til en anden sti udenfor, f.eks. `/movies` for én instans ville pege på `/data/media/movies` og den anden på `/data/media/movies4k`. Dette ødelægger *alt*, hvad du har læst ovenfor. Der er ingen god løsning, du kan enten bruge den gamle version, som ikke er lige så god, lave din mapping på en måde, der er grim og ødelægger hard links, eller bare lade være med at bruge det overhovedet.

# Kør containere ved hjælp af

## Docker Compose

Dette er den bedste mulighed for de fleste brugere, da det giver dig mulighed for at styre og konfigurere mange containere og deres afhængigheder i en enkelt fil. Et godt udgangspunkt er Docker's egen [Kom godt i gang med Docker Compose](https://docs.docker.com/compose/gettingstarted/). Du kan bruge [composerize](https://composerize.com) eller [ghcr.io/red5d/docker-autocompose](#get-docker-compose) til at konvertere `docker run`-kommandoer til en enkelt `docker-compose.yml`-fil.

> Nedenstående er *ikke* et komplet fungerende eksempel! Containerne har kun PID, UID, UMASK og eksempelstier defineret for at holde det enkelt.
{.is-warning}

```yml
    # sonarr
    Sonarr:
        image: cr.hotio.dev/hotio/sonarr
        volumes:
            - /sti/til/config/sonarr:/config
            - /vært/data:/data
        environment:
            - PUID=111
            - PGID=321
            - UMASK=002

    # deluge
    Deluge:
        image: binhex/arch-delugevpn
        volumes:
            - /sti/til/config/deluge:/config
            - /vært/data/torrents:/data/torrents
        environment:
            - PUID=222
            - PGID=321
            - UMASK=002

    # SABnzbd
    SABnzbd:
        image: cr.hotio.dev/hotio/sabnzbd
        volumes:
            - /sti/til/config/sabnzbd:/config
            - /vært/data/usenet:/data/usenet
        environment:
            - PUID=333
            - PGID=321
            - UMASK=002

    # plex
    Plex:
        image: cr.hotio.dev/hotio/plex
        volumes:
            - /sti/til/config/plex:/config
            - /vært/data/media:/data/media

        environment:
            - PUID=444
            - PGID=321
            - UMASK=002
```

### Opdater alle billeder og containere

```shell
    docker-compose pull
    docker-compose up -d
```

### Opdater individuelt billede og container

```shell
    docker-compose pull NAVN
    docker-compose up -d NAVN
```

## docker run

> Ligesom Docker Compose-eksemplet ovenfor er de følgende `docker run`-kommandoer afkortet til *kun* PUID, PGID, UMASK og volumener for at fungere som et tydeligt eksempel.
{.is-warning}

```shell
    # sonarr
    docker run -v /sti/til/config/sonarr:/config \
               -v /vært/data:/data \
               -e PUID=111 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sonarr

    # deluge
    docker run -v /sti/til/config/deluge:/config \
               -v /vært/data/torrents:/data/torrents \
               -e PUID=222 -e PGID=321 -e UMASK=002 \
               binhex/arch-delugevpn

    # SABnzbd
    docker run -v /sti/til/config/sabnzbd:/config \
               -v /vært/data/usenet:/data/usenet \
               -e PUID=333 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sabnzbd

    # plex
    docker run -v /sti/til/config/plex:/config \
               -v /vært/data/media:/data/media \
               -e PUID=444 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/plex
```

## Systemd

Hvis du kun vil vedligeholde et par Docker-containere, kan du bruge systemd. Det standardiserer kontrol og gør afhængigheder enklere for både native og Docker-tjenester. Det generiske eksempel nedenfor kan tilpasses til enhver container ved at justere eller tilføje forskellige værdier og indstillinger.

```shell
    # /etc/systemd/system/thing.service
    [Unit]
    Description=Thing
    Requires=docker.service
    After=network.target docker.service

    [Service]
    ExecStart=/usr/bin/docker run --rm \
                              --name=thing \
                              -v /sti/til/config/thing:/config \
                              -v /vært/data:/data
                              -e PUID=111 -e PGID=321 -e UMASK=002 \
                              nobody/thing

    ExecStop=/usr/bin/docker stop -t 30 thing

    [Install]
    WantedBy=default.target
```

# Nyttige kommandoer

## Vis kørende containere

```shell
    docker ps
```

## Shell *inde i* en container

Når du kører `exec` i en container, vil du normalt blive logget ind som root.

```shell
    docker exec -it CONTAINER_NAVN /bin/bash
```

Når du er inde, kan du skifte bruger med

```shell
    su - <brugernavn>
```

For at køre som en bestemt bruger skal du tilføje `-u` som et argument og angive brugernavnet eller id'en

```shell
    docker exec -u BRUGER -it CONTAINER_NAVN /bin/bash
```

### Eksempler som specifikke brugere

#### LSIO Radarr

```shell
    docker exec -u abc -it radarr bash
```

#### Hotio Sonarr

```shell
    docker exec -u hotio -it sonarr bash
```

For mere information, se [docker exec](https://docs.docker.com/engine/reference/commandline/exec/) dokumentationen.

## Ryd op i Docker

```shell
    docker system prune --all --volumes
```

> Fjerner ubrugte containere, netværk, volumener, billeder og byggecache. Som advarslen denne kommando giver, vil det fjerne alle de tidligere nævnte elementer for alt, der ikke er i brug af en kørende container. I en korrekt konfigureret miljø er dette fint. Men vær opmærksom og gå forsigtigt frem første gang. Se [Docker system prune](https://docs.docker.com/engine/reference/commandline/system_prune/) dokumentationen for flere detaljer.
{.is-warning}

## Få docker run-kommando

Det kan være svært at få `docker run`-kommandoen fra GUI-managere, men dette Docker-billede gør det nemt for en kørende container ([kilde](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container)).

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike CONTAINER_NAVN
```

## Få docker-compose

> Derudover kan du tjekke [TRaSH's Guide til docker-compose](https://trash-guides.info/compose/)
{.is-info}

Det er muligt at få en `docker-compose.yml` fra kørende instanser med [docker-autocompose](https://github.com/Red5d/docker-autocompose), hvis du allerede har startet dine containere med `docker run` eller `docker create` og ønsker at skifte til `docker-compose`-stil. Det er også fantastisk til at dele dine indstillinger med andre, da det ikke betyder noget, hvilken administrationssoftware du bruger. Det sidste argument(er) er dine container-navne, og du kan angive så mange som nødvendigt på samme tid. Det første container-navn er påkrævet, flere er valgfrie. Du kan se container-navne i **NAMES**-kolonnen i `docker ps`, de er normalt enten sat af dig eller kan genereres baseret på billedet som f.eks. `binhex-qbittorrent`. Det er *ikke* billednavnet som f.eks. `binhex/arch-qbittorrentvpn`.

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $CONTAINER_NAVN $ET_ANDET_CONTAINER_NAVN ... $ENDNU_EN_CONTAINER_NAVN
```

For nogle brugere kunne det være:

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose lidarr prowlarr radarr readarr sonarr qbittorrent
```

## Fejlfinding af netværk

De fleste Docker-billeder har ikke mange nyttige værktøjer til fejlfinding, men du kan [tilknytte et netværksfejlfindingsbillede](https://hub.docker.com/r/nicolaka/netshoot) til en eksisterende container for at hjælpe med det.

```shell
    docker run -it --rm --network container:CONTAINER_NAVN nicolaka/netshoot
```

## Rekursivt ændre ejer og gruppe

```shell
    chown -R bruger:gruppe /sti/til/mappe
```

## Rekursivt ændre chmod til 775/664

```shell
    chmod -R a=,a+rX,u+w,g+w /sti/til/mappe
              ^  ^    ^   ^ tilføjer skrivetilladelse til gruppen
              |  |    | tilføjer skrivetilladelse til brugeren
              |  | tilføjer læsetilladelse til alle og udførelse til alle mapper (som styrer adgang)
              | sætter alle til `000`
```

## Find UID/GID for bruger

```shell
    id <brugernavn>
```

## Undersøg filer for hard links

```shell
    ls -alhi
    42207934 -rw-r--r--  2 bruger gruppe    0 Sep 11 11:55 # hardlinked
    42207936 -rw-r--r--  1 bruger gruppe    0 Sep 11 11:55 # ingen hardlinks
    42207934 -rw-r--r--  2 bruger gruppe    0 Sep 11 11:55 # original

    stat original
      File: original
      Size: 0               Blocks: 0          IO Block: 4096   regular empty file
    Device: 803h/2051d      Inode: 42207934    Links: 2
    Access: (0644/-rw-r--r--)  Uid: ( 1000/ bruger)   Gid: ( 1001/ gruppe)
    Access: 2020-09-11 11:55:43.803327144 -0500
    Modify: 2020-09-11 11:55:43.803327144 -0500
    Change: 2020-09-11 11:55:49.706660476 -0500
     Birth: 2020-09-11 11:55:43.803327144 -0500
```

# Interessante Docker-billeder

- [rasmunk/sshfs](https://github.com/rasmunk/docker-volume-sshfs)
{.links-list}
- [hotio’s](https://hotio.dev/) Dokumentationen og Dockerfilen giver ikke nogen dårlige stisuggestions. Billederne opdateres automatisk 2 gange i timen, hvis der findes ændringer i upstream. Hotio bygger også vores Pull Requests (undtagen Sonarr), hvilket kan være nyttigt til testning.
  - [sonarr](https://hotio.dev/containers/sonarr)
  - [radarr](https://hotio.dev/containers/radarr)
  - [lidarr](https://hotio.dev/containers/lidarr)
  - [readarr](https://hotio.dev/containers/readarr)
  - [prowlarr](https://hotio.dev/containers/prowlarr) til usenet og torrent tracker søgning
  - [qbittorrent](https://hotio.dev/containers/qbittorrent/)
  - [NZBGet](https://hotio.dev/containers/nzbget/)
  - [SABnzbd](https://hotio.dev/containers/sabnzbd/)
  - [qflood](https://hotio.dev/containers/qflood/)
  - [ombi](https://hotio.dev/containers/ombi) til anmodning om medier
  - [overseerr](https://hotio.dev/containers/overseerr/) til anmodning om medier
  - [jackett](https://hotio.dev/containers/jackett) til torrent tracker søgning
  - [nzbhydra2](https://hotio.dev/containers/nzbhydra2) til usenet indexer søgning
  - [bazarr](https://hotio.dev/containers/bazarr) til undertekster
  - [pullio](https://hotio.dev/pullio/) til automatisk opdatering af containere
  - [unpackerr](https://hotio.dev/containers/unpackerr) er nyttig til udpakning af pakkede torrents på tværs af forskellige torrentklienter, hvor udpakning mangler eller mangler helt.
{.links-list}
- [linuxserver.io](https://hub.docker.com/u/linuxserver) billeder har billeder til *masser* af software, og de er godt vedligeholdt. Undgå dog deres 'foreslåede (valgfri)' stier.
  - [SWAG Proxy](https://hub.docker.com/r/linuxserver/swag)
  - [qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/)
  - [deluge](https://hub.docker.com/r/linuxserver/deluge/)
  - [rtorrent](https://hub.docker.com/r/linuxserver/rutorrent/)
  - [SABnzbd](https://hub.docker.com/r/linuxserver/sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/)
  - [sonarr](https://hub.docker.com/r/linuxserver/sonarr/)
  - [radarr](https://hub.docker.com/r/linuxserver/radarr/)
  - [lidarr](https://hub.docker.com/r/linuxserver/lidarr/)
- [binhex](https://hub.docker.com/u/binhex) en anden populær vedligeholder
  - [qbittorrent](https://hub.docker.com/r/binhex/arch-qbittorrentvpn/)
  - [deluge](https://hub.docker.com/r/binhex/arch-delugevpn/)
  - [rtorrent](https://hub.docker.com/r/binhex/arch-rtorrentvpn/)
  - [SABnzbd](https://hub.docker.com/r/binhex/arch-sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/binhex/arch-nzbget/)
  - [sonarr](https://hub.docker.com/r/binhex/arch-sonarr/)
  - [radarr](https://hub.docker.com/r/binhex/arch-radarr/)
  - [lidarr](https://hub.docker.com/r/binhex/arch-lidarr/)
{.links-list}

### Alt-i-én løsninger

- [Dette er et GitHub repository](https://github.com/Luctia/ezarr) rettet mod begyndere, der ønsker at bruge Docker til deres Servarr stack. Det er i bund og grund en klar-til-brug samling af filer og kræver kun, at du kører to ting for at få det hele online. Det fjerner besværet med brugerstyring og tilladelser på værtsenheden og har også nogle andre applikationer som PleX.

# Brugerdefineret Docker-netværk og DNS

En interessant funktion ved et [brugerdefineret Docker-netværk](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks) er, at det får sin egen DNS-server. Hvis du opretter et bridge-netværk til dine containere, kan du bruge deres værtsnavne i din konfiguration. For eksempel, hvis du `docker run --network=isolated --hostname=deluge binhex/arch-deluge` og `docker run --network=isolated --hostname=radarr binhex/arch-radarr`, kan du derefter konfigurere Download Client i Radarr til kun at pege på `deluge`, og det vil fungere *og* kommunikere på sit eget private netværk. Det betyder, at hvis du ønsker at være endnu mere sikker, kan du *stoppe* videresendelsen af den port også. Hvis du placerer din reverse proxy-container på det samme netværk, kan du endda stoppe videresendelsen af webinterface-portene og gøre dem endnu mere sikre.

# Almindelige problemer

## Korrekte *udvendige* stier, forkerte *indvendige* stier

Mange mennesker læser dette og tror, at de forstår det, men de ender med at se den korrekte udvendige sti til noget som `/data/usenet`, men så misser de pointen og sætter stadig den *indvendige* sti til `/downloads`.

- Godt:
  - `/host/data/usenet:/data/usenet`
  - `/data/media:/data/media`
- Dårligt:
  - `/host/data:/downloads`
  - `/host/data:/media`
  - `/data/downloads:/data`

## Kører Docker-containere som root eller ændrer brugere rundt

Hvis du finder dig selv med at køre dine containere som `root:root`, gør du noget forkert. Hvis du ikke angiver en UID og GID, vil du bruge standardværdien for billedet, og *det* vil sandsynligvis ikke stemme overens med en rimelig bruger på dit system. Og hvis du ændrer den bruger og gruppe, som dine Docker-containere kører som, vil du sandsynligvis få problemer med tilladelser på mapper som f.eks. `/config`-mappen, som sandsynligvis vil have filer og mapper i sig, der blev oprettet første gang med den UID/GID, du brugte første gang.

## Kører Docker-containere med umask 000

Hvis du finder dig selv med at indstille en UMASK på `000` (som er 777 for mapper og 666 for filer), gør du *også* noget forkert. Det efterlader dine filer og mapper læse/skrive for *alle*, hvilket er dårlig Linux-hygiejne.

# Få hjælp

## Chat-support (Discord)

- [Sonarr Discord](https://discord.sonarr.tv/)
- [Radarr Discord](https://radarr.video/discord)
{.links-list}

## Forum-support (Reddit)

- [/r/sonarr](http://reddit.com/r/sonarr)
- [/r/radarr](http://reddit.com/r/radarr)
{.links-list}