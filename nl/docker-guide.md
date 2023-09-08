---
title: Docker Gids
description: Servarr Docker Gids - Overzicht van Docker-concepten, Hardlink-concepten en Linux-eigenaarschap en -machtigingen
published: true
date: 2023-07-15T20:41:38.016Z
tags: 
editor: markdown
dateCreated: 2021-05-16T20:23:46.192Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [De beste Docker-opstelling](#de-beste-docker-opstelling)
- [Portainer](#portainer)
- [Inleiding](#inleiding)
- [Meerdere gebruikers en een gedeelde groep](#meerdere-gebruikers-en-een-gedeelde-groep)
  - [Machtigingen](#machtigingen)
  - [UMASK](#umask)
  - [PUID en PGID](#puid-en-pgid)
  - [Voorbeeld](#voorbeeld)
- [Enkele gebruiker en optionele gedeelde groep](#enkele-gebruiker-en-optionele-gedeelde-groep)
- [Eigendom en machtigingen van /config](#eigendom-en-machtigingen-van-config)
- [Consistente en goed geplande paden](#consistente-en-goed-geplande-paden)
  - [Voorbeelden](#voorbeelden)
    - [Torrents](#torrents)
    - [Usenet](#usenet)
    - [Mediaserver](#mediaserver)
    - [Sonarr, Radarr en Lidarr](#sonarr-radarr-en-lidarr)
  - [Problemen](#problemen)
- [Containers uitvoeren met](#containers-uitvoeren-met)
  - [Docker Compose](#docker-compose)
    - [Alle afbeeldingen en containers bijwerken](#alle-afbeeldingen-en-containers-bijwerken)
    - [Individuele afbeelding en container bijwerken](#individuele-afbeelding-en-container-bijwerken)
  - [docker run](#docker-run)
  - [Systemd](#systemd)
- [Handige commando's](#handige-commandos)
  - [Lijst met actieve containers](#lijst-met-actieve-containers)
  - [Shell *binnen* een container](#shell-binnen-een-container)
  - [Docker opschonen](#docker-opruimen)
  - [Docker run-opdracht ophalen](#docker-run-opdracht-ophalen)
  - [Docker-compose ophalen](#docker-compose-ophalen)
  - [Netwerkproblemen oplossen](#netwerkproblemen-oplossen)
  - [Gebruiker en groep recursief wijzigen](#gebruiker-en-groep-recursief-wijzigen)
  - [Rechten recursief wijzigen naar 775/664](#rechten-recursief-wijzigen-naar-775664)
  - [UID/GID zoeken voor gebruiker](#uidgid-zoeken-voor-gebruiker)
  - [Bestanden controleren op harde koppelingen](#bestanden-controleren-op-harde-koppelingen)
- [Interessante Docker-afbeeldingen](#interessante-docker-afbeeldingen)
  - [All-in-One-oplossingen](#all-in-one-oplossingen)
- [Aangepast Docker-netwerk en DNS](#aangepast-docker-netwerk-en-dns)
- [Veelvoorkomende problemen](#veelvoorkomende-problemen)
  - [Correcte *externe* paden, onjuiste *interne* paden](#correcte-externe-paden-onjuiste-interne-paden)
  - [Docker-containers uitvoeren als root of gebruikers wijzigen](#docker-containers-uitvoeren-als-root-of-gebruikers-wijzigen)
  - [Docker-containers uitvoeren met umask 000](#docker-containers-uitvoeren-met-umask-000)
- [Hulp krijgen](#hulp-krijgen)
  - [Chatondersteuning (Discord)](#chatondersteuning-discord)
  - [Forumsupport (Reddit)](#forumsupport-reddit)

# De beste Docker-opstelling

**TL;DR**: Een [eponieme](https://www.lexico.com/en/definition/eponymous) gebruiker per daemon en een gedeelde groep met een umask van `002`. Consistente paddefinities tussen *alle* containers die de mapstructuur behouden. Het gebruik van één volume (zodat de downloadmap en de bibliotheekmap zich op hetzelfde bestandssysteem bevinden) maakt [harde koppelingen](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-hardlinks) en [directe verplaatsingen (atomische verplaatsingen)](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-instant-moves-atomic-moves) mogelijk voor Sonarr, Radarr, Lidarr en Readarr. En bovenal, negeer *de meeste* paddocumentatie van de Docker-afbeelding!

> Opmerking: Veel mensen vinden de [TRaSH's Hardlink-tutorial](https://trash-guides.info/hardlinks/) handiger en gemakkelijker te begrijpen dan deze gids. Deze gids is meer conceptueel van aard, terwijl de tutorial van TRaSH je door het proces leidt.
{.is-info}

# Portainer

> **Portainer moet worden vermeden voor het instellen van Docker-containers** {.is-danger}

- Portainer biedt een mooie GUI voor het beheren van containers, maar dat is waar het nuttig voor is.
- Portainer moet alleen worden gebruikt voor het bekijken van logboeken / status van Docker-containers.
- Het wordt sterk aanbevolen om Docker Compose te gebruiken en geen Portainer te gebruiken.
- Portainer heeft veel problemen, zoals:
  - Onjuiste volgorde van bron en doel van koppelingen
  - Inconsistentie in hoofdlettergevoeligheid
  - Geen automatisch aangemaakte aangepaste netwerken voor inter-container communicatie
  - Inconsistentie in de implementatie van Compose op verschillende architecturen
  - Haalt elke tag op bij het bijwerken wanneer je geen specifieke tag instelt
  - Mogelijkheden zijn verborgen en sommige werken helemaal niet op ARM-platforms

Bekijk deze [Docker Gids](/docker-guide) en [TRaSH's Docker-tutorial](https://trash-guides.info/hardlinks/) in plaats daarvan voor het instellen van Docker Compose.

# Inleiding

Dit artikel laat je niet de specifieke details zien van de beste Docker-opstelling, maar het geeft een overzicht dat je kunt gebruiken om je eigen opstelling zo goed mogelijk te maken. Het idee is dat je elke Docker-container uitvoert als zijn eigen gebruiker, met een gedeelde groep en consistente volumes, zodat elke container dezelfde padindeling ziet. Dit is gemakkelijk gezegd, maar niet zo gemakkelijk te begrijpen en uit te leggen.

> Onthoud dat veel mensen de [TRaSH's Hardlink-tutorial](https://trash-guides.info/hardlinks/) handiger en gemakkelijker te begrijpen vinden dan deze gids. Deze gids is meer conceptueel van aard, terwijl de tutorial van TRaSH je door het proces leidt.
{.is-warning}

# Meerdere gebruikers en een gedeelde groep

## Machtigingen

Idealiter wordt elke software uitgevoerd als zijn eigen gebruiker en maken ze allemaal deel uit van een gedeelde groep met mapmachtigingen ingesteld op `775` (`drwxrwxr-x`) en bestanden ingesteld op `664` (`-rw-rw-r--`), wat een umask van `002` is. Een alternatief hiervoor is een enkele gedeelde gebruiker, die `755` en `644` zou gebruiken, wat een umask van `022` is. Je kunt de machtigingen nog verder beperken door lezen van "anderen" te weigeren, wat een umask van `007` zou zijn voor een gebruiker per daemon of `077` voor een enkele gedeelde gebruiker. Voor een diepere uitleg kun je de Arch Linux-wiki-artikelen over [bestandsmachtigingen en attributen](https://wiki.archlinux.org/index.php/File_permissions_and_attributes) en [UMASK](https://wiki.archlinux.org/index.php/Umask) proberen.

## UMASK

Veel Docker-afbeeldingen accepteren `-e UMASK=002` als een omgevingsvariabele en sommige software kan worden geconfigureerd met een gebruiker, groep en umask (NZBGet) of map-/bestandsmachtiging (Sonarr/Radarr), binnen de container. Dit zorgt ervoor dat bestanden en mappen die door *één* zijn gemaakt, kunnen worden gelezen en geschreven door de anderen. Als je bestaande mappen en bestanden gebruikt, moet je ook de huidige eigendom en machtigingen ervan aanpassen, maar in de toekomst zullen ze correct zijn omdat je elke software correct hebt ingesteld.

## PUID en PGID

Veel Docker-afbeeldingen accepteren ook een `-e PUID=123` en `-e PGID=321` waarmee je de UID/GID binnenin kunt wijzigen naar die van een account aan de buitenkant. Als je erin kijkt, zul je zien dat de gebruikersnaam iets is als `abc`, `nobody` of `hotio`, maar omdat het de UID/GID gebruikt die je doorgeeft, ziet het er aan de buitenkant uit als de verwachte gebruiker. Als je opslag van een ander systeem gebruikt via NFS of CIFS, wordt je leven gemakkelijker als *dat* systeem ook overeenkomende gebruikers en groepen heeft. Laat één systeem de UID/GID kiezen en hergebruik deze vervolgens op het andere systeem, op voorwaarde dat ze niet conflicteren.

## Voorbeeld

Je voert [Sonarr](https://github.com/Sonarr/Sonarr/releases) uit met behulp van [hotio/sonarr](https://github.com/hotio/docker-sonarr), je hebt een `sonarr`-gebruiker gemaakt met uid `123` en een gedeelde groep `media` met gid `321` waar de `sonarr`-gebruiker lid van is. Je configureert de Docker-afbeelding om uit te voeren met `-e PUID=123 -e PGID=321 -e UMASK=002`. Sonarr biedt ook de mogelijkheid om de gebruiker, groep en map-/bestandsmachtigingen te configureren. De vorige instellingen zouden deze moeten negeren, maar je kunt ze configureren als je dat wilt. Een UMASK van `002` resulteert in `775` (`drwxrwxr-x`) voor mappen en `664` (`-rw-rw-r--`) voor bestanden. en de gebruiker/groep zijn een beetje lastig omdat ze *binnen* de container een andere naam hebben. Meestal zijn ze `abc` of `nobody`.

# Enkele gebruiker en optionele gedeelde groep

Een andere populaire en naar verluidt eenvoudigere optie is een enkele, gedeelde gebruiker. Misschien zelfs *jouw* gebruiker. Het is niet zo veilig en volgt niet de beste praktijken, maar uiteindelijk is het gemakkelijker te begrijpen en te implementeren. De UMASK hiervoor is `022`, wat resulteert in `755` (`drwxr-xr-x`) voor mappen en `644` (`-rw-r--r--`) voor bestanden. De groep doet er niet echt meer toe, dus je zult waarschijnlijk gewoon de groep gebruiken die vernoemd is naar de gebruiker. Dit maakt het moeilijker om te delen met *andere* gebruikers, dus je wilt mogelijk nog steeds een UMASK van `002`, zelfs met deze opstelling.

# Eigendom en machtigingen van /config

Vergeet niet dat je volume `/config` ook de juiste eigendom en machtigingen moet hebben, meestal de gebruiker van de daemon en de groep van die gebruiker, zoals `sonarr:sonarr` en een umask van `022` of `077`, zodat *alleen* die gebruiker toegang heeft. In een enkele gebruikersopstelling zou dit natuurlijk de enige gebruiker zijn die je hebt gekozen.

# Consistente en goed geplande paden

> Veel mensen vinden de [TRaSH's Hardlink-tutorial](https://trash-guides.info/hardlinks) handiger en gemakkelijker te begrijpen dan deze gids. Deze gids is meer conceptueel van aard, terwijl de tutorial van TRaSH je door het proces leidt.
{.is-info}

Het gemakkelijkste en belangrijkste detail is om uniforme paddefinities te maken voor alle containers.

Als je je afvraagt waarom harde koppelingen niet werken of waarom een eenvoudige verplaatsing veel langer duurt dan zou moeten, legt dit gedeelte het uit. De paden die je *binnenin* gebruikt, zijn belangrijk. Vanwege hoe de volumes van Docker werken, lijken twee volumes zoals de vaak voorgestelde `/tv`, `/movies` en `/downloads` op twee verschillende bestandssystemen, zelfs als ze buiten de container één bestandssysteem zijn. Dit betekent dat harde koppelingen niet werken *en* in plaats van een directe/atomische verplaatsing, een langzamere en meer IO-intensieve kopie+verwijdering wordt gebruikt. Als je meerdere downloadclients hebt omdat je torrents en usenet gebruikt, betekent een enkel `/downloads`-pad dat ze door elkaar worden gehaald. Omdat de Radarr in één container aan de NZBGet in zijn eigen container vraagt waar bestanden zijn, betekent het gebruik van hetzelfde pad in beide dat het gewoon werkt. Als je dat niet doet, moet je het oplossen met een externe padtoewijzing.

Kies *één* padindeling en gebruik deze voor allemaal. Het wordt aanbevolen om `/data` te gebruiken, maar er zijn andere veelvoorkomende namen zoals `/shared`, `/media` of `/dvr`. Door dit aan de buitenkant *en* binnenin hetzelfde te houden, wordt je opstelling eenvoudiger: één pad om te onthouden of als je Docker en native software integreert. Bijvoorbeeld, Synology kan `/Volume1/data` gebruiken en unRAID kan `/mnt/user/data` gebruiken aan de buitenkant, maar `/data` aan de binnenkant is prima.

Het is ook belangrijk om te onthouden dat je de paden in de software die *binnenin* deze Docker-containers draait, moet instellen of opnieuw moet configureren. Als je de paden voor je downloadclient wijzigt, moet je de instellingen aanpassen en waarschijnlijk bestaande torrents bijwerken. Als je het pad van je bibliotheek wijzigt, moet je die instellingen wijzigen in Sonarr, Radarr, Lidarr, Plex, enz.

## Voorbeelden

Wat hier belangrijk is, is de algemene structuur, niet de namen. Je kunt mapnamen kiezen die voor jou logisch zijn. En er zijn ook andere manieren om dingen te ordenen. Bijvoorbeeld, je zult waarschijnlijk geen conflicten hebben met identieke releases tussen usenet en torrents, dus je *kunt* beide in `/data/downloads/{movies|books|music|tv}`-mappen plaatsen. Downloads hoeven zelfs niet in submappen te worden gesorteerd, aangezien films, muziek en tv zelden conflicteren.

Deze voorbeeldmap `data` heeft submappen voor torrents en usenet, en elk van deze heeft submappen voor tv-, film- en muziekdownloads om de zaken netjes te houden. De map `media` heeft mooi genoemde submappen `tv`, `movies`, `books` en `music`. Deze `media`-map is je bibliotheek en wat je zou doorgeven aan Plex, Kodi, Emby, Jellyfin, enz.

Voor het onderstaande voorbeeld is `data` equivalent aan het hostpad `/host/data` en het Docker-pad `/data`

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

Het pad voor elke Docker-container kan zo specifiek zijn als nodig is, terwijl de juiste structuur behouden blijft:

### Torrents

```none
    data
    └── torrents
        ├── movies
        ├── music
        ├── books
        └── tv
```

Torrents hebben alleen toegang tot torrentbestanden, dus geef het door `-v /host/data/torrents:/data/torrents`. In de torrentsoftware-instellingen moet je de paden opnieuw configureren en je kunt sorteren in submappen zoals `/data/torrents/{tv|books|movies|music}`.

### Usenet

```none
    data
    └── usenet
        ├── movies
        ├── music
        └── tv
```

Usenet heeft alleen toegang tot usenetbestanden, dus geef het door `-v /host/data/usenet:/data/usenet`. In de usenetsoftware-instellingen moet je de paden opnieuw configureren en je kunt sorteren in submappen zoals `/data/usenet/{tv|movies|music}`.

### Mediaserver

```none
    data
    └── media
        ├── movies
        ├── music
        └── tv
```

Plex/Emby heeft alleen toegang tot je mediacollectie, dus geef door `-v /host/data/media:/data/media`, wat meerdere submappen kan hebben zoals `movies`, `kids movies`, `tv`, `documentary tv` en/of `music` als submappen.

### Sonarr, Radarr en Lidarr

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

Sonarr, Radarr en Lidarr krijgen alles binnen met `-v /host/data:/data` omdat de *download*-map(pen) en de *media*-map eruitzien als en *zijn* één bestandssysteem. Harde koppelingen werken en verplaatsingen zijn atomair, in plaats van kopiëren + verwijderen.

## Problemen

Er zijn een paar kleine problemen als je niet de voorgestelde paden van de Docker-image volgt.

Het grootste probleem is dat volumes die in het `dockerfile` zijn gedefinieerd, worden aangemaakt als ze niet zijn gespecificeerd. Dit betekent dat ze zich opstapelen als je de containers verwijdert en opnieuw maakt. Als ze gegevens bevatten, kunnen ze onverwacht ruimte innemen en waarschijnlijk op een ongeschikte plaats. Je kunt een [opruimopdracht](#prune-docker) vinden in de sectie met handige opdrachten hieronder. Dit kan ook worden verholpen door een lege map door te geven voor alle volumes die je niet wilt gebruiken, zoals `/data/empty:/movies` en `/data/empty:/downloads`. Misschien kun je zelfs een bestand met de naam `DO NOT USE THIS FOLDER` erin plaatsen, om jezelf eraan te herinneren.

Een ander probleem is dat sommige images al zijn geconfigureerd om de gedocumenteerde volumes te gebruiken, dus je moet de instellingen in de software binnen de Docker-container wijzigen. Gelukkig is dit een eenmalig probleem, omdat de configuratie buiten de container behouden blijft. Je kunt ook een pad kiezen zoals `/data` of `/media`, dat sommige images al definiëren voor een specifiek gebruik. Dit zou geen probleem moeten zijn, maar het kan wel wat verwarrend zijn in combinatie met de eerdere problemen. Uiteindelijk is het de moeite waard voor werkende harde koppelingen en snelle verplaatsingen. De consistentie en eenvoud zijn ook welkome bijwerkingen.

Als je de nieuwste versie van de verlaten [RadarrSync](https://github.com/Sperryfreak01/RadarrSync) gebruikt om twee Radarr-instanties te synchroniseren, *hangt* dit af van het toewijzen van het *zelfde* pad binnenin naar een ander pad aan de buitenkant, bijvoorbeeld `/movies` voor de ene instantie zou wijzen naar `/data/media/movies` en de andere naar `/data/media/movies4k`. Dit breekt *alles* wat je hierboven hebt gelezen. Er is geen goede oplossing, je kunt ofwel de oude versie gebruiken die niet zo goed is, je mapping op een lelijke manier doen en harde koppelingen verbreken, of het gewoon helemaal niet gebruiken.

# Containers uitvoeren met

## Docker Compose

Dit is de beste optie voor de meeste gebruikers, het stelt je in staat om veel containers en hun onderlinge afhankelijkheden te beheren en configureren in één bestand. Een goed startpunt is de eigen [Handleiding voor Docker Compose](https://docs.docker.com/compose/gettingstarted/) van Docker. Je kunt [composerize](https://composerize.com) of [ghcr.io/red5d/docker-autocompose](#get-docker-compose) gebruiken om `docker run`-opdrachten om te zetten in één `docker-compose.yml`-bestand.

> Het onderstaande is *geen* volledig werkend voorbeeld! De containers hebben alleen PID, UID, UMASK en voorbeeldpaden gedefinieerd om het eenvoudig te houden.
{.is-warning}

```yml
    # sonarr
    Sonarr:
        image: cr.hotio.dev/hotio/sonarr
        volumes:
            - /pad/naar/config/sonarr:/config
            - /host/data:/data
        environment:
            - PUID=111
            - PGID=321
            - UMASK=002

    # deluge
    Deluge:
        image: binhex/arch-delugevpn
        volumes:
            - /pad/naar/config/deluge:/config
            - /host/data/torrents:/data/torrents
        environment:
            - PUID=222
            - PGID=321
            - UMASK=002

    # SABnzbd
    SABnzbd:
        image: cr.hotio.dev/hotio/sabnzbd
        volumes:
            - /pad/naar/config/sabnzbd:/config
            - /host/data/usenet:/data/usenet
        environment:
            - PUID=333
            - PGID=321
            - UMASK=002

    # plex
    Plex:
        image: cr.hotio.dev/hotio/plex
        volumes:
            - /pad/naar/config/plex:/config
            - /host/data/media:/data/media

        environment:
            - PUID=444
            - PGID=321
            - UMASK=002
```

### Alle images en containers bijwerken

```shell
    docker-compose pull
    docker-compose up -d
```

### Individuele image en container bijwerken

```shell
    docker-compose pull NAAM
    docker-compose up -d NAAM
```

## docker run

> Net als het bovenstaande Docker Compose-voorbeeld zijn de volgende `docker run`-opdrachten vereenvoudigd tot *alleen* de PUID, PGID, UMASK en volumes om als duidelijk voorbeeld te dienen.
{.is-warning}

```shell
    # sonarr
    docker run -v /pad/naar/config/sonarr:/config \
               -v /host/data:/data \
               -e PUID=111 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sonarr

    # deluge
    docker run -v /pad/naar/config/deluge:/config \
               -v /host/data/torrents:/data/torrents \
               -e PUID=222 -e PGID=321 -e UMASK=002 \
               binhex/arch-delugevpn

    # SABnzbd
    docker run -v /pad/naar/config/sabnzbd:/config \
               -v /host/data/usenet:/data/usenet \
               -e PUID=333 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sabnzbd

    # plex
    docker run -v /pad/naar/config/plex:/config \
               -v /host/data/media:/data/media \
               -e PUID=444 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/plex
```

## Systemd

Voor het beheren van een paar Docker-containers is het gebruik van systemd een optie. Het standaardiseert de controle en vereenvoudigt de afhankelijkheden voor zowel native als Docker-services. Het onderstaande generieke voorbeeld kan worden aangepast aan elke container door de verschillende waarden en opties aan te passen of toe te voegen.

```shell
    # /etc/systemd/system/thing.service
    [Unit]
    Description=Thing
    Requires=docker.service
    After=network.target docker.service

    [Service]
    ExecStart=/usr/bin/docker run --rm \
                              --name=thing \
                              -v /pad/naar/config/thing:/config \
                              -v /host/data:/data
                              -e PUID=111 -e PGID=321 -e UMASK=002 \
                              nobody/thing

    ExecStop=/usr/bin/docker stop -t 30 thing

    [Install]
    WantedBy=default.target
```

# Handige opdrachten

## Lijst met actieve containers

```shell
    docker ps
```

## Shell *binnen* een container

Exec in een container zal je meestal inloggen als root

```shell
    docker exec -it CONTAINER_NAAM /bin/bash
```

Eenmaal binnen kun je van gebruiker wisselen met

```shell
    su - <gebruikersnaam>
```

Om in te loggen als een specifieke gebruiker, voeg je `-u` toe als argument en geef je de gebruikersnaam of id door

```shell
    docker exec -u GEBRUIKER -it CONTAINER_NAAM /bin/bash
```

### Voorbeelden als specifieke gebruikers

#### LSIO Radarr

```shell
    docker exec -u abc -it radarr bash
```

#### Hotio Sonarr

```shell
    docker exec -u hotio -it sonarr bash
```

Voor meer informatie, zie de [docker exec](https://docs.docker.com/engine/reference/commandline/exec/) documentatie.

## Docker opruimen

```shell
    docker system prune --all --volumes
```

> Verwijder ongebruikte containers, netwerken, volumes, images en build cache. Zoals de WAARSCHUWING van deze opdracht aangeeft, worden hiermee alle eerder genoemde items verwijderd voor alles wat niet in gebruik is door een actieve container. In een correct geconfigureerde omgeving is dit prima. Maar wees op de hoogte en ga voorzichtig te werk de eerste keer. Zie de [Docker system prune](https://docs.docker.com/engine/reference/commandline/system_prune/) documentatie voor meer details.
{.is-warning}

## Docker run-opdracht ophalen

Het verkrijgen van de `docker run`-opdracht van GUI-managers kan lastig zijn, maar met deze Docker-image is het eenvoudig voor een actieve container ([bron](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container)).

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike CONTAINER_NAAM
```

## Docker-compose ophalen

> Daarnaast kun je [TRaSH's Gids voor docker-compose](https://trash-guides.info/compose/) bekijken
{.is-info}

Het is mogelijk om een `docker-compose.yml` te krijgen van actieve instanties met [docker-autocompose](https://github.com/Red5d/docker-autocompose), voor het geval je je containers al hebt gestart met `docker run` of `docker create` en wilt overschakelen naar de `docker-compose`-stijl. Het is ook handig om je instellingen te delen met anderen, omdat het niet uitmaakt welke beheersoftware je gebruikt. Het laatste argument(en) zijn de namen van je containers en je kunt er zoveel tegelijk doorgeven als nodig is. De eerste container naam is verplicht, meer zijn optioneel. Je kunt container namen zien in de **NAMES** kolom van `docker ps`, ze worden meestal door jou ingesteld of kunnen worden gegenereerd op basis van de image, zoals `binhex-qbittorrent`. Het is *niet* de image naam, zoals `binhex/arch-qbittorrentvpn`.

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $CONTAINER_NAAM $ANDERE_CONTAINER_NAAM ... $NOG_EEN_CONTAINER_NAAM
```

Voor sommige gebruikers kan dit er als volgt uitzien:

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose lidarr prowlarr radarr readarr sonarr qbittorrent
```

## Problemen met netwerken oplossen

De meeste Docker-images hebben niet veel nuttige tools voor probleemoplossing, maar je kunt een [netwerkprobleemoplossingstype image](https://hub.docker.com/r/nicolaka/netshoot) koppelen aan een bestaande container om daarbij te helpen.

```shell
    docker run -it --rm --network container:CONTAINER_NAAM nicolaka/netshoot
```

## Gebruiker en groep recursief wijzigen

```shell
    chown -R gebruiker:groep /pad/naar/hier
```

## Recursief chmod naar 775/664

```shell
    chmod -R a=,a+rX,u+w,g+w /pad/naar/hier
              ^  ^    ^   ^ voegt schrijfrechten toe aan groep
              |  |    | voegt schrijfrechten toe aan gebruiker
              |  | voegt leesrechten toe aan iedereen en uitvoerrechten aan alle mappen (die de toegang regelen)
              | stelt alles in op `000`
```

## UID/GID voor gebruiker vinden

```shell
    id <gebruikersnaam>
```

## Bestanden onderzoeken op harde koppelingen

```shell
    ls -alhi
    42207934 -rw-r--r--  2 gebruiker groep    0 11 sep 11:55 # harde koppeling
    42207936 -rw-r--r--  1 gebruiker groep    0 11 sep 11:55 # geen harde koppelingen
    42207934 -rw-r--r--  2 gebruiker groep    0 11 sep 11:55 # origineel

    stat origineel
      Bestand: origineel
      Grootte: 0               Blokken: 0          IO-blok: 4096   gewoon leeg bestand
    Apparaat: 803h/2051d      inode: 42207934    Links: 2
    Toegang: (0644/-rw-r--r--)  Uid: ( 1000/ gebruiker)   Gid: ( 1001/ groep)
    Toegang: 2020-09-11 11:55:43.803327144 -0500
    Wijziging: 2020-09-11 11:55:43.803327144 -0500
    Statuswijziging: 2020-09-11 11:55:49.706660476 -0500
     Creatie: 2020-09-11 11:55:43.803327144 -0500
```

# Interessante Docker-images

- [rasmunk/sshfs](https://github.com/rasmunk/docker-volume-sshfs)
{.links-list}
- [hotio’s](https://hotio.dev/) De documentatie en Dockerfile doen geen slechte pad suggesties. Afbeeldingen worden automatisch 2 keer per uur bijgewerkt als er wijzigingen worden gevonden. Hotio bouwt ook onze Pull Requests (behalve Sonarr), wat handig kan zijn voor testen.
  - [sonarr](https://hotio.dev/containers/sonarr)
  - [radarr](https://hotio.dev/containers/radarr)
  - [lidarr](https://hotio.dev/containers/lidarr)
  - [readarr](https://hotio.dev/containers/readarr)
  - [prowlarr](https://hotio.dev/containers/prowlarr) voor usenet en torrent tracker zoeken
  - [qbittorrent](https://hotio.dev/containers/qbittorrent/)
  - [NZBGet](https://hotio.dev/containers/nzbget/)
  - [SABnzbd](https://hotio.dev/containers/sabnzbd/)
  - [qflood](https://hotio.dev/containers/qflood/)
  - [ombi](https://hotio.dev/containers/ombi) voor het aanvragen van media
  - [overseerr](https://hotio.dev/containers/overseerr/) voor het aanvragen van media
  - [jackett](https://hotio.dev/containers/jackett) voor torrent tracker zoeken
  - [nzbhydra2](https://hotio.dev/containers/nzbhydra2) voor usenet indexer zoeken
  - [bazarr](https://hotio.dev/containers/bazarr) voor ondertitels
  - [pullio](https://hotio.dev/pullio/) voor het automatisch bijwerken van containers
  - [unpackerr](https://hotio.dev/containers/unpackerr) is handig voor het uitpakken van verpakte torrents bij verschillende torrent clients waar het uitpakken ontbreekt of volledig ontbreekt.
{.links-list}
- [linuxserver.io](https://hub.docker.com/u/linuxserver) afbeeldingen hebben afbeeldingen voor *veel* software en ze worden goed onderhouden. Vermijd echter hun 'suggested (optional)' paden.
  - [SWAG Proxy](https://hub.docker.com/r/linuxserver/swag)
  - [qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/)
  - [deluge](https://hub.docker.com/r/linuxserver/deluge/)
  - [rtorrent](https://hub.docker.com/r/linuxserver/rutorrent/)
  - [SABnzbd](https://hub.docker.com/r/linuxserver/sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/)
  - [sonarr](https://hub.docker.com/r/linuxserver/sonarr/)
  - [radarr](https://hub.docker.com/r/linuxserver/radarr/)
  - [lidarr](https://hub.docker.com/r/linuxserver/lidarr/)
- [binhex](https://hub.docker.com/u/binhex) een andere populaire onderhouder
  - [qbittorrent](https://hub.docker.com/r/binhex/arch-qbittorrentvpn/)
  - [deluge](https://hub.docker.com/r/binhex/arch-delugevpn/)
  - [rtorrent](https://hub.docker.com/r/binhex/arch-rtorrentvpn/)
  - [SABnzbd](https://hub.docker.com/r/binhex/arch-sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/binhex/arch-nzbget/)
  - [sonarr](https://hub.docker.com/r/binhex/arch-sonarr/)
  - [radarr](https://hub.docker.com/r/binhex/arch-radarr/)
  - [lidarr](https://hub.docker.com/r/binhex/arch-lidarr/)
{.links-list}

### All-in-One Oplossingen

- [Dit is een GitHub repository](https://github.com/Luctia/ezarr) gericht op beginners die Docker willen gebruiken voor hun Servarr stack. Het is in feite een kant-en-klare verzameling bestanden en vereist alleen dat je twee dingen uitvoert om het geheel online te krijgen. Het verwijdert het gedoe rond gebruikersbeheer en machtigingen op het hostapparaat en bevat enkele andere toepassingen zoals PleX.

# Aangepast Docker-netwerk en DNS

Een interessante functie van een [aangepast Docker-netwerk](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks) is dat het een eigen DNS-server heeft. Als je een bridge-netwerk maakt voor je containers, kun je hun hostnamen gebruiken in je configuratie. Bijvoorbeeld, als je `docker run --network=isolated --hostname=deluge binhex/arch-deluge` en `docker run --network=isolated --hostname=radarr binhex/arch-radarr` uitvoert, kun je vervolgens de Download Client in Radarr configureren om alleen naar `deluge` te verwijzen en het zal werken *en* communiceren via zijn eigen privénetwerk. Dit betekent dat als je nog veiliger wilt zijn, je die poort *ook* kunt stoppen met doorsturen. Als je je reverse proxy-container op hetzelfde netwerk plaatst, kun je zelfs stoppen met het doorsturen van de webinterfacepoorten en ze nog veiliger maken.

# Veelvoorkomende problemen

## Juiste *externe* paden, onjuiste *interne* paden

Veel mensen lezen dit en denken dat ze het begrijpen, maar ze zien het externe pad correct naar iets als `/data/usenet`, maar dan missen ze het punt en stellen ze het *interne* pad nog steeds in op `/downloads`.

- Goed:
  - `/host/data/usenet:/data/usenet`
  - `/data/media:/data/media`
- Slecht:
  - `/host/data:/downloads`
  - `/host/data:/media`
  - `/data/downloads:/data`

## Docker-containers uitvoeren als root of gebruikers wijzigen

Als je merkt dat je je containers uitvoert als `root:root`, doe je iets verkeerd. Als je geen UID en GID doorgeeft, gebruik je standaard wat het is voor de afbeelding en *dat* zal waarschijnlijk niet overeenkomen met een redelijke gebruiker op je systeem. En als je de gebruiker en groep wijzigt waarin je Docker-containers worden uitgevoerd, krijg je waarschijnlijk machtigingsproblemen op mappen zoals de `/config` map waar waarschijnlijk bestanden en mappen in staan die de eerste keer zijn aangemaakt met de UID/GID die je de eerste keer hebt gebruikt.

## Docker-containers uitvoeren met umask 000

Als je jezelf betrapt op het instellen van een UMASK van `000` (wat 777 is voor mappen en 666 voor bestanden), doe je *ook* iets verkeerd. Het laat je bestanden en mappen lezen/schrijven voor *iedereen*, wat slechte Linux-hygiëne is.

# Hulp krijgen

## Chatondersteuning (Discord)

- [Sonarr Discord](https://discord.sonarr.tv/)
- [Radarr Discord](https://radarr.video/discord)
{.links-list}

## Forumondersteuning (Reddit)

- [/r/sonarr](http://reddit.com/r/sonarr)
- [/r/radarr](http://reddit.com/r/radarr)
{.links-list}