---
title: Docker Guide
description: Servarr Docker Guide - Översikt över Docker-koncept, hardlink-koncept och Linux-ägande och behörigheter
published: true
date: 2023-07-15T20:41:38.016Z
tags: 
editor: markdown
dateCreated: 2021-05-16T20:23:46.192Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Den bästa Docker-inställningen](#den-bästa-docker-inställningen)
- [Portainer](#portainer)
- [Introduktion](#introduktion)
- [Flera användare och en delad grupp](#flera-användare-och-en-delad-grupp)
  - [Behörigheter](#behörigheter)
  - [UMASK](#umask)
  - [PUID och PGID](#puid-och-pgid)
  - [Exempel](#exempel)
- [En användare och valfri delad grupp](#en-användare-och-valfri-delad-grupp)
- [Ägande och behörigheter för /config](#ägande-och-behörigheter-för-config)
- [Konsekventa och välplanerade sökvägar](#konsekventa-och-välplanerade-sökvägar)
  - [Exempel](#exempel)
    - [Torrents](#torrents)
    - [Usenet](#usenet)
    - [Mediaserver](#mediaserver)
    - [Sonarr, Radarr och Lidarr](#sonarr-radarr-och-lidarr)
  - [Problem](#problem)
- [Kör containrar med](#kör-containrar-med)
  - [Docker Compose](#docker-compose)
    - [Uppdatera alla bilder och containrar](#uppdatera-alla-bilder-och-containrar)
    - [Uppdatera enskild bild och container](#uppdatera-enskild-bild-och-container)
  - [docker run](#docker-run)
  - [Systemd](#systemd)
- [Användbara kommandon](#användbara-kommandon)
  - [Lista körande containrar](#lista-körande-containrar)
  - [Kör en kommandotolk *inuti* en container](#kör-en-kommandotolk-inuti-en-container)
  - [Rensa Docker](#rensa-docker)
  - [Hämta docker run-kommando](#hämta-docker-run-kommando)
  - [Hämta docker-compose](#hämta-docker-compose)
  - [Felsök nätverk](#felsök-nätverk)
  - [Ändra ägare och grupp rekursivt](#ändra-ägare-och-grupp-rekursivt)
  - [Ändra behörigheter rekursivt till 775/664](#ändra-behörigheter-rekursivt-till-775664)
  - [Hitta UID/GID för användare](#hitta-uidgid-för-användare)
  - [Undersök filer för hard links](#undersök-filer-för-hard-links)
- [Intressanta Docker-bilder](#intressanta-docker-bilder)
  - [Allt-i-ett-lösningar](#allt-i-ett-lösningar)
- [Anpassat Docker-nätverk och DNS](#anpassat-docker-nätverk-och-dns)
- [Vanliga problem](#vanliga-problem)
  - [Korrekta *externa* sökvägar, felaktiga *interna* sökvägar](#korrekta-externa-sökvägar-felaktiga-interna-sökvägar)
  - [Kör Docker-containrar som root eller ändra användare](#kör-docker-containrar-som-root-eller-ändra-användare)
  - [Kör Docker-containrar med umask 000](#kör-docker-containrar-med-umask-000)
- [Få hjälp](#få-hjälp)
  - [Chattstöd (Discord)](#chattstöd-discord)
  - [Forumstöd (Reddit)](#forumstöd-reddit)

# Den bästa Docker-inställningen

**TL;DR**: En [eponym](https://www.lexico.com/en/definition/eponymous) användare per daemon och en delad grupp med en umask på `002`. Konsekventa sökvägsdefinitioner mellan *alla* containrar som bibehåller mappstrukturen. Genom att använda en volym (så att nedladdningsmappen och biblioteksmappen finns på samma filsystem) möjliggörs [hardlinks](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-hardlinks) och [instant moves (atomiska förflyttningar)](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-instant-moves-atomic-moves) för Sonarr, Radarr, Lidarr och Readarr. Och framför allt, ignorera *det mesta* av Docker-bildens sökvägsdokumentation!

> Observera: Många människor tycker att [TRaSH's Hardlink Tutorial](https://trash-guides.info/hardlinks/) är användbart och lättare att förstå än den här guiden. Den här guiden är mer konceptuell till sin natur medan TRaSH's handledning går igenom processen.
{.is-info}

# Portainer

> **Portainer bör undvikas för att konfigurera Docker-containrar** {.is-danger}

- Portainer ger ett snyggt GUI för att hantera containrar, men det är allt det är användbart för.
- Portainer bör endast användas för att visa loggar för Docker-containrar / status för containrar.
- Det rekommenderas starkt att använda Docker Compose och inte använda Portainer.
- Portainer har många problem, såsom:
  - Felaktig ordning av källa och mål för monteringar
  - Inkonsekvent skiftlägeskänslighet
  - Inga automatiskt skapade anpassade nätverk för kommunikation mellan containrar
  - Inkonsekventa kompositionsimplementationer på olika arkitekturer
  - Hämtar varje tagg vid uppdatering om du inte anger en specifik tagg
  - Vissa funktioner är dolda och fungerar inte alls på ARM-plattformar

Se denna [Docker Guide](/docker-guide) och [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) istället för hur man konfigurerar Docker Compose.

# Introduktion

Den här artikeln kommer inte att visa dig specifika detaljer om den bästa Docker-inställningen, men den beskriver en översikt som du kan använda för att göra din egen inställning så bra som möjligt. Tanken är att du kör varje Docker-container som sin egen användare, med en delad grupp och konsekventa volymer så att varje container ser samma sökvägsstruktur. Detta är lätt att säga, men inte så lätt att förstå och förklara.

> Kom ihåg att många människor tycker att [TRaSH's Hardlink Tutorial](https://trash-guides.info/hardlinks/) är användbart och lättare att förstå än den här guiden. Den här guiden är mer konceptuell till sin natur medan TRaSH's handledning går igenom processen.
{.is-warning}

# Flera användare och en delad grupp

## Behörigheter

Idealt sett körs varje programvara som sin egen användare och de är alla en del av en delad grupp med mappbehörigheter inställda på `775` (`drwxrwxr-x`) och filer inställda på `664` (`-rw-rw-r--`), vilket är en umask på `002`. Ett vettigt alternativ till detta är en enda delad användare, som skulle använda `755` och `644` vilket är en umask på `022`. Du kan begränsa behörigheterna ännu mer genom att neka läsning från "other", vilket skulle vara en umask på `007` för en användare per daemon eller `077` för en enda delad användare. För en djupare förklaring kan du prova Arch Linux-wiki-artiklarna om [filbehörigheter och attribut](https://wiki.archlinux.org/index.php/File_permissions_and_attributes) och [UMASK](https://wiki.archlinux.org/index.php/Umask).

## UMASK

Många Docker-bilder accepterar `-e UMASK=002` som en miljövariabel och viss programvara kan konfigureras med en användare, grupp och umask (NZBGet) eller mapp-/filbehörighet (Sonarr/Radarr) inuti containern. Detta kommer att säkerställa att filer och mappar som skapas av *en* kan läsas och skrivas av de andra. Om du använder befintliga mappar och filer måste du också fixa deras nuvarande ägande och behörigheter, men framåt kommer de att vara korrekta eftersom du ställde in varje programvara rätt.

## PUID och PGID

Många Docker-bilder tar också emot `-e PUID=123` och `-e PGID=321` som låter dig ändra UID/GID som används inuti till det för ett konto på utsidan. Om du tittar in kommer du att se att användarnamnet är något som `abc`, `nobody` eller `hotio`, men eftersom det använder UID/GID som du skickar in ser det ut som den förväntade användaren på utsidan. Om du använder lagring från ett annat system via NFS eller CIFS blir ditt liv enklare om *det* systemet också har matchande användare och grupp. Låt kanske ett system välja UID/GID, sedan återanvänder du dem på det andra systemet, förutsatt att de inte krockar.

## Exempel

Du kör [Sonarr](https://github.com/Sonarr/Sonarr/releases) med [hotio/sonarr](https://github.com/hotio/docker-sonarr), du har skapat en `sonarr`-användare med UID `123` och en delad grupp `media` med GID `321` som `sonarr`-användaren är medlem i. Du konfigurerar Docker-bilden att köra med `-e PUID=123 -e PGID=321 -e UMASK=002`. Sonarr låter dig också konfigurera användaren, gruppen samt mapp- och filbehörigheter. De tidigare inställningarna bör upphäva dessa, men du kan konfigurera dem om du vill. En UMASK på `002` resulterar i `775` (`drwxrwxr-x`) för mappar och `664` (`-rw-rw-r--`) för filer. och användare/grupp är lite knepiga eftersom de har ett annat namn *inuti* containern. Vanligtvis är de `abc` eller `nobody`.

# En användare och valfri delad grupp

Ett annat populärt och förmodligen enklare alternativ är en enda delad användare. Kanske till och med *din* användare. Det är inte lika säkert och följer inte bästa praxis, men i slutändan är det lättare att förstå och implementera. UMASK för detta är `022` vilket resulterar i `755` (`drwxr-xr-x`) för mappar och `644` (`-rw-r--r--`) för filer. Gruppen spelar inte längre så stor roll, så du kommer förmodligen bara att använda gruppen med samma namn som användaren. Detta gör det svårare att dela med *andra* användare, så du kan fortfarande vilja ha en UMASK på `002` även med denna inställning.

# Ägande och behörigheter för /config

Glöm inte att din `/config`-volym också måste ha korrekt ägande och behörigheter, vanligtvis daemonens användare och den användarens grupp som `sonarr:sonarr` och en umask på `022` eller `077` så att *endast* den användaren har åtkomst. I en inställning med en enda användare skulle detta naturligtvis vara den enda användaren du har valt.

# Konsekventa och välplanerade sökvägar

> Många människor tycker att [TRaSH's Hardlink Tutorial](https://trash-guides.info/hardlinks) är användbart och lättare att förstå än den här guiden. Den här guiden är mer konceptuell till sin natur medan TRaSH's handledning går igenom processen.
{.is-info}

Det enklaste och viktigaste detaljen är att skapa enhetliga sökvägsdefinitioner över alla containrar.

Om du undrar varför hardlinks inte fungerar eller varför en enkel flyttning tar mycket längre tid än den borde, förklaras det här i avsnittet. Sökvägarna du använder *inuti* spelar roll. På grund av hur Dockers volymer fungerar, om du passerar in två volymer som de vanligtvis föreslagna `/tv`, `/movies` och `/downloads` ser de ut som två olika filsystem, även om de är ett enda filsystem utanför containern. Detta innebär att hardlinks inte fungerar *och* istället för en omedelbar/atomisk flyttning används en långsammare och mer IO-intensiv kopiering+radering. Om du har flera nedladdningsklienter eftersom du använder torrents och usenet, innebär en enda `/downloads`-sökväg att de kommer att blandas ihop. Eftersom Radarr i en container kommer att fråga NZBGet i sin egen container var filerna finns, kommer att använda samma sökväg i båda betyder att det bara kommer att fungera. Om du inte gör det måste du fixa det med en fjärrsökvägskarta.

Så välj *en* sökvägsstruktur och använd den för alla. Det föreslås att använda `/data`, men det finns andra vanliga namn som `/shared`, `/media` eller `/dvr`. Genom att hålla detta likadant på utsidan *och* insidan blir din inställning enklare: en sökväg att komma ihåg eller om du integrerar Docker och nativ programvara. Till exempel kan Synology använda `/Volume1/data` och unRAID kan använda `/mnt/user/data` på utsidan, men `/data` på insidan fungerar bra.

Det är också viktigt att komma ihåg att du måste ställa in eller konfigurera sökvägar i programvaran som körs *inuti* dessa Docker-containrar. Om du ändrar sökvägarna för din nedladdningsklient måste du redigera dess inställningar så att de matchar och förmodligen uppdatera befintliga torrents. Om du ändrar sökvägen för ditt bibliotek måste du ändra dessa inställningar i Sonarr, Radarr, Lidarr, Plex, etc.

## Exempel

Det som spelar roll här är den allmänna strukturen, inte namnen. Du är fri att välja mappnamn som gör mening för dig. Och det finns andra sätt att organisera saker också. Till exempel kommer du inte troligtvis att ladda ner och stöta på konflikter med identiska utgåvor mellan usenet och torrents, så du *kan* placera båda i `/data/downloads/{movies|books|music|tv}`-mappar. Nedladdningar behöver inte ens sorteras i undermappar, eftersom filmer, musik och tv sällan kommer att krocka.

Denna exempelmapp `data` har undermappar för torrents och usenet och var och en av dessa har undermappar för tv-, film- och musiknedladdningar för att hålla ordning på saker. Mappen `media` har snyggt namngivna undermappar `tv`, `movies`, `books` och `music`. Denna `media`-mapp är ditt bibliotek och vad du skulle skicka till Plex, Kodi, Emby, Jellyfin, etc.

För exemplet nedan är `data` ekvivalent med värdens sökväg `/host/data` och Docker-sökvägen `/data`

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

Sökvägen för varje Docker-container kan vara så specifik som behövs samtidigt som den bibehåller rätt struktur:

### Torrents

```none
    data
    └── torrents
        ├── movies
        ├── music
        ├── books
        └── tv
```

Torrents behöver bara åtkomst till torrentfiler, så skicka in `-v /host/data/torrents:/data/torrents`. I torrentprogrammets inställningar måste du konfigurera om sökvägar och du kan sortera in i undermappar som `/data/torrents/{tv|books|movies|music}`.

### Usenet

```none
    data
    └── usenet
        ├── movies
        ├── music
        └── tv
```

Usenet behöver bara åtkomst till usenetfiler, så skicka in `-v /host/data/usenet:/data/usenet`. I usenetprogrammets inställningar måste du konfigurera om sökvägar och du kan sortera in i undermappar som `/data/usenet/{tv|movies|music}`.

### Mediaserver

```none
    data
    └── media
        ├── movies
        ├── music
        └── tv
```

Plex/Emby behöver bara åtkomst till ditt mediebibliotek, så skicka in `-v /host/data/media:/data/media`, vilket kan ha vilket antal undermappar som `movies`, `kids movies`, `tv`, `documentary tv` och/eller `music` som undermappar.

### Sonarr, Radarr och Lidarr

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

Sonarr, Radarr och Lidarr får allt med `-v /host/data:/data` eftersom *nedladdnings*mappen/mapparna och *mediamappen* kommer att se ut som och *vara* ett filsystem. Hardlinks kommer att fungera och flyttningar kommer att vara atomiska, istället för kopiering + radering.

## Problem

Det finns ett par mindre problem med att inte följa Docker-bildens föreslagna sökvägar.

Det största problemet är att volymer som definieras i `dockerfile` kommer att skapas om de inte anges, vilket innebär att de kommer att ansamlas när du tar bort och återskapar behållarna. Om de innehåller data kan de oavsiktligt ta upp utrymme på en olämplig plats. Du kan hitta en [städkommando](#prune-docker) i avsnittet med användbara kommandon nedan. Detta kan också åtgärdas genom att ange en tom mapp för alla volymer som du inte vill använda, som `/data/empty:/movies` och `/data/empty:/downloads`. Du kan till och med lägga en fil med namnet "ANVÄND INTE DENNA MAPP" i mappen för att påminna dig själv.

Ett annat problem är att vissa bilder är förkonfigurerade för att använda de dokumenterade volymerna, så du måste ändra inställningarna i programvaran inuti Docker-behållaren. Som tur är detta bara ett engångsproblem eftersom konfigurationen finns kvar utanför behållaren. Du kan också välja en sökväg som `/data` eller `/media`, som vissa bilder redan definierar för en specifik användning. Det borde inte vara ett problem, men det kan bli lite förvirrande när det kombineras med de tidigare problemen. I slutändan är det värt det för att få fungerande hårda länkar och snabba flyttar. Konsekvensen och enkelheten är också välkomna bieffekter.

Om du använder den senaste versionen av den övergivna [RadarrSync](https://github.com/Sperryfreak01/RadarrSync) för att synkronisera två Radarr-instanser, *beroende* den på att samma sökväg inuti pekar på en annan sökväg utanför, till exempel skulle `/movies` för en instans peka på `/data/media/movies` och den andra på `/data/media/movies4k`. Detta bryter *allt* du har läst ovan. Det finns ingen bra lösning, antingen använder du den gamla versionen som inte är lika bra, gör din mappning på ett sätt som är fult och bryter hårda länkar eller använder den inte alls.

# Kör behållare med

## Docker Compose

Detta är det bästa alternativet för de flesta användare, det låter dig styra och konfigurera många behållare och deras beroenden i en fil. En bra startpunkt är Dockers egna [Kom igång med Docker Compose](https://docs.docker.com/compose/gettingstarted/). Du kan använda [composerize](https://composerize.com) eller [ghcr.io/red5d/docker-autocompose](#get-docker-compose) för att konvertera `docker run`-kommandon till en enda `docker-compose.yml`-fil.

> Nedan är *inte* ett komplett fungerande exempel! Behållarna har bara PID, UID, UMASK och exempelsökvägar definierade för att hålla det enkelt.
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

### Uppdatera alla bilder och behållare

```shell
    docker-compose pull
    docker-compose up -d
```

### Uppdatera enskild bild och behållare

```shell
    docker-compose pull NAMN
    docker-compose up -d NAMN
```

## docker run

> Liksom exemplet med Docker Compose ovan är följande `docker run`-kommandon avskalade till *endast* PUID, PGID, UMASK och volymer för att fungera som ett tydligt exempel.
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

För att underhålla några Docker-behållare kan du använda systemd. Det standardiserar kontrollen och förenklar beroenden för både nativa och Docker-tjänster. Det generiska exemplet nedan kan anpassas till vilken behållare som helst genom att justera eller lägga till olika värden och alternativ.

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

# Användbara kommandon

## Lista körande behållare

```shell
    docker ps
```

## Kör en shell *inne i* en behållare

Att köra en shell i en behållare kommer vanligtvis att logga in dig som root

```shell
    docker exec -it CONTAINER_NAME /bin/bash
```

När du är inne kan du byta användare med

```shell
    su - <användarnamn>
```

För att köra som en specifik användare, lägg till `-u` som ett argument och ange användarnamnet eller ID:et

```shell
    docker exec -u USER -it CONTAINER_NAME /bin/bash
```

### Exempel som specifika användare

#### LSIO Radarr

```shell
    docker exec -u abc -it radarr bash
```

#### Hotio Sonarr

```shell
    docker exec -u hotio -it sonarr bash
```

För mer information, se [docker exec](https://docs.docker.com/engine/reference/commandline/exec/)-dokumentationen.

## Rensa Docker

```shell
    docker system prune --all --volumes
```

> Ta bort oanvända behållare, nätverk, volymer, bilder och byggcache. Som varningen som detta kommando ger säger, kommer det att ta bort alla tidigare nämnda objekt för allt som inte används av en körande behållare. I en korrekt konfigurerad miljö är detta okej. Men var medveten om detta och gå försiktigt fram första gången. Se [Docker system prune](https://docs.docker.com/engine/reference/commandline/system_prune/)-dokumentationen för mer information.
{.is-warning}

## Hämta docker run-kommando

Att få `docker run`-kommandot från GUI-hanterare kan vara svårt, men med den här Docker-bilden blir det enkelt för en körande behållare ([källa](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container)).

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike CONTAINER_NAME
```

## Hämta docker-compose

> Dessutom kan du kolla in [TRaSH's Guide för docker-compose](https://trash-guides.info/compose/)
{.is-info}

Det är möjligt att få en `docker-compose.yml` från körande instanser med [docker-autocompose](https://github.com/Red5d/docker-autocompose), om du redan har startat dina behållare med `docker run` eller `docker create` och vill byta till `docker-compose`-stil. Det är också bra för att dela dina inställningar med andra, eftersom det inte spelar någon roll vilken hanteringsprogramvara du använder. Det sista argumentet (eller argumenten) är dina behållarnamn och du kan ange så många som behövs samtidigt. Det första behållarnamnet är obligatoriskt, fler är valfria. Du kan se behållarnamn i **NAMES**-kolumnen i `docker ps`, de är vanligtvis inställda av dig eller kan genereras baserat på bilden som `binhex-qbittorrent`. Det är *inte* bildnamnet, som `binhex/arch-qbittorrentvpn`.

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $CONTAINER_NAME $ANOTHER_CONTAINER_NAME ... $ONE_MORE_CONTAINER_NAME
```

För vissa användare kan detta vara:

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose lidarr prowlarr radarr readarr sonarr qbittorrent
```

## Felsök nätverk

De flesta Docker-bilder har inte många användbara verktyg för felsökning, men du kan [koppla en bild för nätverksfelsökning](https://hub.docker.com/r/nicolaka/netshoot) till en befintlig behållare för att hjälpa till med det.

```shell
    docker run -it --rm --network container:CONTAINER_NAME nicolaka/netshoot
```

## Ändra ägare och grupp rekursivt

```shell
    chown -R user:group /some/path/here
```

## Ändra chmod rekursivt till 775/664

```shell
    chmod -R a=,a+rX,u+w,g+w /some/path/here
              ^  ^    ^   ^ lägger till skrivbehörighet för grupp
              |  |    | lägger till skrivbehörighet för användare
              |  | lägger till läsbehörighet för alla och exekveringsbehörighet för alla mappar (som styr åtkomst)
              | sätter alla till `000`
```

## Hitta UID/GID för användare

```shell
    id <användarnamn>
```

## Undersök filer för hårda länkar

```shell
    ls -alhi
    42207934 -rw-r--r--  2 user group    0 Sep 11 11:55 # hårdat länkat
    42207936 -rw-r--r--  1 user group    0 Sep 11 11:55 # inga hårda länkar
    42207934 -rw-r--r--  2 user group    0 Sep 11 11:55 # original

    stat original
      File: original
      Size: 0               Blocks: 0          IO Block: 4096   regular empty file
    Device: 803h/2051d      Inode: 42207934    Links: 2
    Access: (0644/-rw-r--r--)  Uid: ( 1000/ user)   Gid: ( 1001/ group)
    Access: 2020-09-11 11:55:43.803327144 -0500
    Modify: 2020-09-11 11:55:43.803327144 -0500
    Change: 2020-09-11 11:55:49.706660476 -0500
     Birth: 2020-09-11 11:55:43.803327144 -0500
```

# Intressanta Docker-bilder

- [rasmunk/sshfs](https://github.com/rasmunk/docker-volume-sshfs)
{.links-list}
- [hotio’s](https://hotio.dev/) Dokumentationen och Dockerfilen ger inga dåliga sökvägsförslag. Bilderna uppdateras automatiskt 2 gånger på 1 timme om förändringar hittas i källkoden. Hotio bygger också våra Pull Requests (utom Sonarr) vilket kan vara användbart för testning.
  - [sonarr](https://hotio.dev/containers/sonarr)
  - [radarr](https://hotio.dev/containers/radarr)
  - [lidarr](https://hotio.dev/containers/lidarr)
  - [readarr](https://hotio.dev/containers/readarr)
  - [prowlarr](https://hotio.dev/containers/prowlarr) för usenet och torrent tracker-sökning
  - [qbittorrent](https://hotio.dev/containers/qbittorrent/)
  - [NZBGet](https://hotio.dev/containers/nzbget/)
  - [SABnzbd](https://hotio.dev/containers/sabnzbd/)
  - [qflood](https://hotio.dev/containers/qflood/)
  - [ombi](https://hotio.dev/containers/ombi) för att begära media
  - [overseerr](https://hotio.dev/containers/overseerr/) för att begära media
  - [jackett](https://hotio.dev/containers/jackett) för torrent tracker-sökning
  - [nzbhydra2](https://hotio.dev/containers/nzbhydra2) för usenet indexer-sökning
  - [bazarr](https://hotio.dev/containers/bazarr) för undertexter
  - [pullio](https://hotio.dev/pullio/) för automatisk uppdatering av containrar
  - [unpackerr](https://hotio.dev/containers/unpackerr) är användbart för packad torrent-extraktion över olika torrentklienter där uppackning saknas eller är bristfällig.
{.links-list}
- [linuxserver.io](https://hub.docker.com/u/linuxserver) har bilder för *massor* av programvara och de är väl underhållna. Undvik dock deras 'suggested (optional)' sökvägar.
  - [SWAG Proxy](https://hub.docker.com/r/linuxserver/swag)
  - [qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/)
  - [deluge](https://hub.docker.com/r/linuxserver/deluge/)
  - [rtorrent](https://hub.docker.com/r/linuxserver/rutorrent/)
  - [SABnzbd](https://hub.docker.com/r/linuxserver/sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/)
  - [sonarr](https://hub.docker.com/r/linuxserver/sonarr/)
  - [radarr](https://hub.docker.com/r/linuxserver/radarr/)
  - [lidarr](https://hub.docker.com/r/linuxserver/lidarr/)
- [binhex](https://hub.docker.com/u/binhex) en annan populär underhållare
  - [qbittorrent](https://hub.docker.com/r/binhex/arch-qbittorrentvpn/)
  - [deluge](https://hub.docker.com/r/binhex/arch-delugevpn/)
  - [rtorrent](https://hub.docker.com/r/binhex/arch-rtorrentvpn/)
  - [SABnzbd](https://hub.docker.com/r/binhex/arch-sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/binhex/arch-nzbget/)
  - [sonarr](https://hub.docker.com/r/binhex/arch-sonarr/)
  - [radarr](https://hub.docker.com/r/binhex/arch-radarr/)
  - [lidarr](https://hub.docker.com/r/binhex/arch-lidarr/)
{.links-list}

### All-in-One-lösningar

- [Detta är ett GitHub-repositorium](https://github.com/Luctia/ezarr) riktat till nybörjare som vill använda Docker för sin Servarr-stack. Det är i princip en färdig samling av filer och kräver bara att du kör två saker för att få hela grejen online. Det tar bort krånglet med användarhantering och behörigheter på värdmaskinen och har några andra applikationer som PleX.

# Anpassat Docker-nätverk och DNS

En intressant funktion med ett [anpassat Docker-nätverk](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks) är att det får sin egen DNS-server. Om du skapar ett brygg-nätverk för dina containrar kan du använda deras värdnamn i din konfiguration. Till exempel, om du kör `docker run --network=isolated --hostname=deluge binhex/arch-deluge` och `docker run --network=isolated --hostname=radarr binhex/arch-radarr`, kan du sedan konfigurera nedladdningsklienten i Radarr att peka på bara `deluge` och det kommer att fungera *och* kommunicera i sitt eget privata nätverk. Det betyder att om du vill vara ännu säkrare kan du *sluta* vidarebefordra den porten också. Om du placerar din omvända proxycontainer på samma nätverk kan du till och med sluta vidarebefordra webbgränssnittsportarna och göra dem ännu säkrare.

# Vanliga problem

## Korrekta *externa* sökvägar, inkorrekta *interna* sökvägar

Många läser detta och tror att de förstår, men de ser den externa sökvägen korrekt till något som `/data/usenet`, men missar poängen och ställer fortfarande in den *interna* sökvägen till `/downloads`.

- Bra:
  - `/host/data/usenet:/data/usenet`
  - `/data/media:/data/media`
- Dåligt:
  - `/host/data:/downloads`
  - `/host/data:/media`
  - `/data/downloads:/data`

## Kör Docker-containrar som root eller ändra användare

Om du kör dina containrar som `root:root` gör du något fel. Om du inte skickar in en UID och GID kommer du att använda standardvärdet för bilden och *det* kommer sannolikt inte att stämma överens med en rimlig användare på ditt system. Och om du ändrar användaren och gruppen som dina Docker-containrar körs som kommer du förmodligen att stöta på behörighetsproblem på mappar som `/config`-mappen som förmodligen kommer att ha filer och mappar i sig som skapades första gången med den UID/GID du använde första gången.

## Kör Docker-containrar med umask 000

Om du ställer in en UMASK på `000` (vilket är 777 för mappar och 666 för filer) gör du *också* något fel. Det gör att dina filer och mappar blir läs/skrivbara för *alla*, vilket är dålig Linux-hygien.

# Få hjälp

## Chattstöd (Discord)

- [Sonarr Discord](https://discord.sonarr.tv/)
- [Radarr Discord](https://radarr.video/discord)
{.links-list}

## Forumstöd (Reddit)

- [/r/sonarr](http://reddit.com/r/sonarr)
- [/r/radarr](http://reddit.com/r/radarr)
{.links-list}