---
title: Docker-Anleitung
description: Servarr Docker-Anleitung - Übersicht über Docker-Konzepte, Hardlink-Konzepte und Linux-Besitz und -Berechtigungen
published: true
date: 2023-07-15T20:41:38.016Z
tags: 
editor: markdown
dateCreated: 2021-05-16T20:23:46.192Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Die beste Docker-Konfiguration](#die-beste-docker-konfiguration)
- [Portainer](#portainer)
- [Einführung](#einführung)
- [Mehrere Benutzer und eine gemeinsame Gruppe](#mehrere-benutzer-und-eine-gemeinsame-gruppe)
  - [Berechtigungen](#berechtigungen)
  - [UMASK](#umask)
  - [PUID und PGID](#puid-und-pgid)
  - [Beispiel](#beispiel)
- [Einzelner Benutzer und optionale gemeinsame Gruppe](#einzelner-benutzer-und-optionale-gemeinsame-gruppe)
- [Besitz und Berechtigungen von /config](#besitz-und-berechtigungen-von-config)
- [Konsistente und gut geplante Pfade](#konsistente-und-gut-geplante-pfade)
  - [Beispiele](#beispiele)
    - [Torrents](#torrents)
    - [Usenet](#usenet)
    - [Medienserver](#medienserver)
    - [Sonarr, Radarr und Lidarr](#sonarr-radarr-und-lidarr)
  - [Probleme](#probleme)
- [Container ausführen mit](#container-ausführen-mit)
  - [Docker Compose](#docker-compose)
    - [Alle Images und Container aktualisieren](#alle-images-und-container-aktualisieren)
    - [Einzelnes Image und Container aktualisieren](#einzelnes-image-und-container-aktualisieren)
  - [docker run](#docker-run)
  - [Systemd](#systemd)
- [Hilfreiche Befehle](#hilfreiche-befehle)
  - [Liste der laufenden Container](#liste-der-laufenden-container)
  - [Shell *innerhalb* eines Containers](#shell-innerhalb-eines-containers)
  - [Docker bereinigen](#docker-bereinigen)
  - [Docker run-Befehl abrufen](#docker-run-befehl-abrufen)
  - [Docker Compose abrufen](#docker-compose-abrufen)
  - [Netzwerkprobleme beheben](#netzwerkprobleme-beheben)
  - [Benutzer und Gruppe rekursiv ändern](#benutzer-und-gruppe-rekursiv-ändern)
  - [Rekursiv chmod auf 775/664](#rekursiv-chmod-auf-775664)
  - [UID/GID für Benutzer ermitteln](#uidgid-für-benutzer-ermitteln)
  - [Dateien auf Hardlinks überprüfen](#dateien-auf-hardlinks-überprüfen)
- [Interessante Docker-Images](#interessante-docker-images)
  - [All-in-One-Lösungen](#all-in-one-lösungen)
- [Benutzerdefiniertes Docker-Netzwerk und DNS](#benutzerdefiniertes-docker-netzwerk-und-dns)
- [Häufige Probleme](#häufige-probleme)
  - [Richtige *externe* Pfade, falsche *interne* Pfade](#richtige-externe-pfade-falsche-interne-pfade)
  - [Docker-Container als Root ausführen oder Benutzer ändern](#docker-container-als-root-ausführen-oder-benutzer-ändern)
  - [Docker-Container mit umask 000 ausführen](#docker-container-mit-umask-000-ausführen)
- [Hilfe erhalten](#hilfe-erhalten)
  - [Chat-Support (Discord)](#chat-support-discord)
  - [Foren-Support (Reddit)](#foren-support-reddit)

# Die beste Docker-Konfiguration

**TL;DR**: Ein [eponymer](https://www.lexico.com/en/definition/eponymous) Benutzer pro Daemon und eine gemeinsame Gruppe mit einer Umask von `002`. Konsistente Pfaddefinitionen zwischen *allen* Containern, die die Ordnerstruktur beibehalten. Die Verwendung eines einzigen Volumes (damit der Download-Ordner und der Bibliotheksordner auf demselben Dateisystem liegen) ermöglicht [Hardlinks](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-hardlinks) und [sofortige Verschiebungen (atomare Verschiebungen)](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-instant-moves-atomic-moves) für Sonarr, Radarr, Lidarr und Readarr. Und vor allem: Ignorieren Sie *die meisten* Pfad-Dokumentationen des Docker-Images!

> Hinweis: Viele Leute finden [TRaSH's Hardlink-Tutorial](https://trash-guides.info/hardlinks/) hilfreich und einfacher zu verstehen als diese Anleitung. Diese Anleitung ist eher konzeptioneller Natur, während TRaSH's Tutorial Sie durch den Prozess führt.
{.is-info}

# Portainer

> **Portainer sollte vermieden werden, um Docker-Container einzurichten** {.is-danger}

- Portainer bietet eine hübsche GUI zur Verwaltung von Containern, aber das ist auch schon alles, wofür es nützlich ist.
- Portainer sollte nur zur Anzeige von Docker-Container-Logs / Container-Status verwendet werden.
- Es wird dringend empfohlen, Docker Compose zu verwenden und Portainer nicht zu verwenden.
- Portainer hat viele Probleme, wie z.B.:
  - Falsche Reihenfolge von Quelle und Ziel von Mounts
  - Inkonsistente Groß-/Kleinschreibung
  - Keine automatisch erstellten benutzerdefinierten Netzwerke für die Kommunikation zwischen Containern
  - Inkonsistente Compose-Implementierungen auf verschiedenen Architekturen
  - Zieht bei einem Update alle Tags, wenn kein bestimmter Tag festgelegt ist
  - Fähigkeiten sind versteckt und einige funktionieren auf ARM-Plattformen überhaupt nicht

Lesen Sie stattdessen diese [Docker-Anleitung](/docker-guide) und [TRaSH's Docker-Tutorial](https://trash-guides.info/hardlinks/), um Docker Compose einzurichten.

# Einführung

Dieser Artikel zeigt Ihnen nicht die Details der besten Docker-Konfiguration, sondern beschreibt einen Überblick, den Sie verwenden können, um Ihre eigene Konfiguration so gut wie möglich zu gestalten. Die Idee besteht darin, jeden Docker-Container als eigenen Benutzer auszuführen, mit einer gemeinsamen Gruppe und konsistenten Volumes, sodass jeder Container denselben Pfadlayout sieht. Das ist leicht gesagt, aber nicht so leicht zu verstehen und zu erklären.

> Beachten Sie, dass viele Leute [TRaSH's Hardlink-Tutorial](https://trash-guides.info/hardlinks/) hilfreich und einfacher zu verstehen finden als diese Anleitung. Diese Anleitung ist eher konzeptioneller Natur, während TRaSH's Tutorial Sie durch den Prozess führt.
{.is-warning}

# Mehrere Benutzer und eine gemeinsame Gruppe

## Berechtigungen

Idealerweise läuft jede Software als eigener Benutzer und alle sind Teil einer gemeinsamen Gruppe mit Ordnerberechtigungen von `775` (`drwxrwxr-x`) und Dateiberechtigungen von `664` (`-rw-rw-r--`), was einer Umask von `002` entspricht. Eine vernünftige Alternative dazu ist ein einzelner gemeinsamer Benutzer, der `755` und `644` verwendet, was einer Umask von `022` entspricht. Sie können die Berechtigungen noch weiter einschränken, indem Sie Lesezugriff für "andere" verweigern, was einer Umask von `007` für einen Benutzer pro Daemon oder `077` für einen einzelnen gemeinsamen Benutzer entspricht. Für eine ausführlichere Erklärung lesen Sie die Arch Linux Wiki-Artikel zu [Dateiberechtigungen und Attributen](https://wiki.archlinux.org/index.php/File_permissions_and_attributes) und [UMASK](https://wiki.archlinux.org/index.php/Umask).

## UMASK

Viele Docker-Images akzeptieren `-e UMASK=002` als Umgebungsvariable, und einige Software kann mit einem Benutzer, einer Gruppe und einer Umask (NZBGet) oder mit Ordner-/Dateiberechtigungen (Sonarr/Radarr) innerhalb des Containers konfiguriert werden. Dadurch wird sichergestellt, dass Dateien und Ordner, die von *einer* Software erstellt werden, von den anderen gelesen und geschrieben werden können. Wenn Sie vorhandene Ordner und Dateien verwenden, müssen Sie auch deren aktuellen Besitz und Berechtigungen korrigieren, aber in Zukunft werden sie korrekt sein, weil Sie jede Software richtig eingerichtet haben.

## PUID und PGID

Viele Docker-Images akzeptieren auch `-e PUID=123` und `-e PGID=321`, mit denen Sie die im Inneren verwendete UID/GID in die einer Benutzerkonto außerhalb ändern können. Wenn Sie einen Blick hineinwerfen, werden Sie feststellen, dass der Benutzername etwas wie `abc`, `nobody` oder `hotio` ist, aber weil er die von Ihnen übergebenen UID/GID verwendet, sieht es von außen aus wie der erwartete Benutzer. Wenn Sie Speicher von einem anderen System über NFS oder CIFS verwenden, wird Ihnen das Leben leichter gemacht, wenn *dieses* System auch passende Benutzer und Gruppen hat. Lassen Sie ein System die UID/GID auswählen und verwenden Sie diese dann auf dem anderen System, vorausgesetzt, sie kollidieren nicht.

## Beispiel

Sie führen [Sonarr](https://github.com/Sonarr/Sonarr/releases) mit [hotio/sonarr](https://github.com/hotio/docker-sonarr) aus, Sie haben einen Benutzer `sonarr` mit der UID `123` und eine gemeinsame Gruppe `media` mit der GID `321`, zu der der Benutzer `sonarr` gehört. Sie konfigurieren das Docker-Image mit `-e PUID=123 -e PGID=321 -e UMASK=002`. Sonarr ermöglicht es Ihnen auch, den Benutzer, die Gruppe sowie Ordner- und Dateiberechtigungen zu konfigurieren. Die vorherigen Einstellungen sollten diese jedoch aufheben, aber Sie könnten sie konfigurieren, wenn Sie wollten. Eine Umask von `002` ergibt `775` (`drwxrwxr-x`) für Ordner und `664` (`-rw-rw-r--`) für Dateien, und der Benutzer/Gruppe ist etwas knifflig, weil sie *innerhalb* des Containers einen anderen Namen haben. Normalerweise sind sie `abc` oder `nobody`.

# Einzelner Benutzer und optionale gemeinsame Gruppe

Eine weitere beliebte und wohl einfachere Option ist ein einzelner, gemeinsamer Benutzer. Vielleicht sogar *Ihr* Benutzer. Es ist nicht so sicher und folgt nicht den besten Praktiken, aber am Ende ist es einfacher zu verstehen und umzusetzen. Die Umask dafür ist `022`, was `755` (`drwxr-xr-x`) für Ordner und `644` (`-rw-r--r--`) für Dateien ergibt. Die Gruppe spielt keine Rolle mehr, daher verwenden Sie wahrscheinlich einfach die nach dem Benutzer benannte Gruppe. Dadurch wird es schwieriger, mit *anderen* Benutzern zu teilen, sodass Sie möglicherweise trotz dieser Konfiguration eine Umask von `002` verwenden möchten.

# Besitz und Berechtigungen von /config

Vergessen Sie nicht, dass Ihr `/config`-Volume ebenfalls den korrekten Besitz und die korrekten Berechtigungen haben muss, normalerweise den Benutzer des Daemons und die Gruppe dieses Benutzers wie `sonarr:sonarr` und eine Umask von `022` oder `077`, sodass *nur* dieser Benutzer Zugriff hat. Bei einer Einzelbenutzer-Konfiguration wäre dies natürlich der von Ihnen gewählte Benutzer.

# Konsistente und gut geplante Pfade

> Viele Leute finden [TRaSH's Hardlink-Tutorial](https://trash-guides.info/hardlinks) hilfreich und einfacher zu verstehen als diese Anleitung. Diese Anleitung ist eher konzeptioneller Natur, während TRaSH's Tutorial Sie durch den Prozess führt.
{.is-info}

Das einfachste und wichtigste Detail besteht darin, einheitliche Pfaddefinitionen für alle Container zu erstellen.

Wenn Sie sich fragen, warum Hardlinks nicht funktionieren oder warum ein einfacher Verschiebevorgang viel länger dauert als er sollte, erklärt dieser Abschnitt dies. Die Pfade, die Sie im *Inneren* verwenden, sind wichtig. Aufgrund der Funktionsweise der Docker-Volumes sehen zwei übergebene Volumes wie beispielsweise die häufig vorgeschlagenen `/tv`, `/movies` und `/downloads` aus, als wären es zwei verschiedene Dateisysteme, auch wenn es sich außerhalb des Containers um ein einziges Dateisystem handelt. Das bedeutet, dass Hardlinks nicht funktionieren *und* anstelle eines sofortigen/atomaren Verschiebens eine langsamere und IO-intensivere Kopie+Löschen verwendet wird. Wenn Sie mehrere Download-Clients haben, weil Sie Torrents und Usenet verwenden, bedeutet ein einziger `/downloads`-Pfad, dass sie durcheinander geraten. Da das Radarr in einem Container das NZBGet in seinem eigenen Container nach Dateien fragt, funktioniert es, wenn Sie denselben Pfad in beiden verwenden. Andernfalls müssten Sie es mit einer Remote-Pfadzuordnung beheben.

Wählen Sie also *einen* Pfadlayout und verwenden Sie es für alle. Es wird empfohlen, `/data` zu verwenden, aber es gibt auch andere gebräuchliche Namen wie `/shared`, `/media` oder `/dvr`. Wenn Sie Docker und native Software integrieren, sollten Sie dies außerhalb und innerhalb gleich halten: ein Pfad, den Sie sich merken können. Zum Beispiel könnte Synology außerhalb `/Volume1/data` und unRAID `/mnt/user/data` verwenden, aber innen ist `/data` in Ordnung.

Es ist auch wichtig zu beachten, dass Sie die Pfade in der Software, die *innerhalb* dieser Docker-Container ausgeführt wird, einrichten oder neu konfigurieren müssen. Wenn Sie die Pfade für Ihren Download-Client ändern, müssen Sie dessen Einstellungen anpassen und wahrscheinlich vorhandene Torrents aktualisieren. Wenn Sie Ihren Bibliothekspfad ändern, müssen Sie diese Einstellungen in Sonarr, Radarr, Lidarr, Plex usw. ändern.

## Beispiele

Wichtig ist hier die allgemeine Struktur, nicht die Namen. Sie können Ordnerbezeichnungen wählen, die für Sie sinnvoll sind. Und es gibt auch andere Möglichkeiten, Dinge anzuordnen. Zum Beispiel werden Sie wahrscheinlich keine Konflikte mit identischen Veröffentlichungen zwischen Usenet und Torrents herunterladen und ausführen, sodass Sie beides in den Ordnern `/data/downloads/{movies|books|music|tv}` platzieren *könnten*. Downloads müssen nicht einmal in Unterordner sortiert werden, da Filme, Musik und Fernsehen selten in Konflikt geraten.

Dieses Beispiel `data`-Verzeichnis hat Unterordner für Torrents und Usenet, und jeder von ihnen hat Unterordner für TV-, Film- und Musik-Downloads, um die Dinge ordentlich zu halten. Das `media`-Verzeichnis hat schön benannte Unterordner für TV, Filme, Bücher und Musik. Dieses `media`-Verzeichnis ist Ihre Bibliothek und das, was Sie an Plex, Kodi, Emby, Jellyfin usw. weitergeben würden.

Für das folgende Beispiel ist `data` gleichbedeutend mit dem Host-Pfad `/host/data` und dem Docker-Pfad `/data`

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

Der Pfad für jeden Docker-Container kann so spezifisch sein, wie es erforderlich ist, und dennoch die korrekte Struktur beibehalten:

### Torrents

```none
    data
    └── torrents
        ├── movies
        ├── music
        ├── books
        └── tv
```

Torrents benötigt nur Zugriff auf Torrent-Dateien, also geben Sie `-v /host/data/torrents:/data/torrents` an. In den Einstellungen der Torrent-Software müssen Sie Pfade neu konfigurieren, und Sie können in Unterordner wie `/data/torrents/{tv|books|movies|music}` sortieren.

### Usenet

```none
    data
    └── usenet
        ├── movies
        ├── music
        └── tv
```

Usenet benötigt nur Zugriff auf Usenet-Dateien, also geben Sie `-v /host/data/usenet:/data/usenet` an. In den Einstellungen der Usenet-Software müssen Sie Pfade neu konfigurieren, und Sie können in Unterordner wie `/data/usenet/{tv|movies|music}` sortieren.

### Medienserver

```none
    data
    └── media
        ├── movies
        ├── music
        └── tv
```

Plex/Emby benötigt nur Zugriff auf Ihre Medienbibliothek, also geben Sie `-v /host/data/media:/data/media` an, die beliebig viele Unterordner wie `movies`, `kids movies`, `tv`, `documentary tv` und/oder `music` haben kann.

### Sonarr, Radarr und Lidarr

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

Sonarr, Radarr und Lidarr erhalten alles mit `-v /host/data:/data`, weil der *Download*-Ordner und der *Medien*-Ordner wie ein einziges Dateisystem aussehen und *sind*. Hardlinks funktionieren und Verschiebungen sind atomar, anstatt Kopie + Löschen zu verwenden.

## Probleme

Es gibt ein paar kleinere Probleme, wenn man sich nicht an die vorgeschlagenen Pfade des Docker-Images hält.

Das größte Problem ist, dass Volumes, die in der `dockerfile` definiert sind, erstellt werden, wenn sie nicht angegeben sind. Das bedeutet, dass sie sich ansammeln, wenn Sie die Container löschen und neu erstellen. Wenn sie Daten enthalten, können sie unerwartet Speicherplatz verbrauchen und wahrscheinlich an einem ungeeigneten Ort. Sie können einen [Aufräum-Befehl](#prune-docker) im Abschnitt der hilfreichen Befehle unten finden. Dies könnte auch durch das Übergeben eines leeren Ordners für alle Volumes, die Sie nicht verwenden möchten, wie z.B. `/data/empty:/movies` und `/data/empty:/downloads`, gemildert werden. Vielleicht können Sie sogar eine Datei mit dem Namen `DO NOT USE THIS FOLDER` darin platzieren, um sich selbst daran zu erinnern.

Ein weiteres Problem ist, dass einige Images vorab so konfiguriert sind, dass sie die dokumentierten Volumes verwenden. Sie müssen daher die Einstellungen in der Software innerhalb des Docker-Containers ändern. Glücklicherweise ist dies ein einmaliges Problem, da die Konfiguration außerhalb des Containers erhalten bleibt. Sie könnten auch einen Pfad wie `/data` oder `/media` wählen, den einige Images bereits für einen bestimmten Zweck definieren. Das sollte kein Problem sein, kann aber in Kombination mit den vorherigen Problemen etwas verwirrender sein. Am Ende lohnt es sich jedoch für funktionierende Hardlinks und schnelle Verschiebungen. Die Konsistenz und Einfachheit sind ebenfalls willkommene Nebeneffekte.

Wenn Sie die neueste Version des aufgegebenen [RadarrSync](https://github.com/Sperryfreak01/RadarrSync) verwenden, um zwei Radarr-Instanzen zu synchronisieren, *muss* der *gleiche* Pfad im Inneren auf einen anderen Pfad im Äußeren gemappt werden, z.B. `/movies` für eine Instanz würde auf `/data/media/movies` zeigen und die andere auf `/data/media/movies4k`. Das bricht *alles*, was Sie oben gelesen haben. Es gibt keine gute Lösung, entweder Sie verwenden die alte Version, die nicht so gut ist, Sie machen Ihre Zuordnung auf eine hässliche Weise, die Hardlinks bricht, oder Sie verwenden es einfach gar nicht.

# Ausführen von Containern mit

## Docker Compose

Dies ist die beste Option für die meisten Benutzer, da es Ihnen ermöglicht, viele Container und ihre Abhängigkeiten in einer Datei zu steuern und zu konfigurieren. Ein guter Ausgangspunkt ist die eigene [Docker Compose-Get-Started-Anleitung](https://docs.docker.com/compose/gettingstarted/) von Docker. Sie können [composerize](https://composerize.com) oder [ghcr.io/red5d/docker-autocompose](#get-docker-compose) verwenden, um `docker run`-Befehle in eine einzelne `docker-compose.yml`-Datei umzuwandeln.

> Das folgende ist *kein* vollständiges funktionierendes Beispiel! Die Container haben nur PID, UID, UMASK und Beispiel-Pfade definiert, um es einfach zu halten.
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

### Alle Images und Container aktualisieren

```shell
    docker-compose pull
    docker-compose up -d
```

### Einzelnes Image und Container aktualisieren

```shell
    docker-compose pull NAME
    docker-compose up -d NAME
```

## docker run

> Wie im obigen Docker Compose-Beispiel sind die folgenden `docker run`-Befehle auf *nur* die PUID, PGID, UMASK und Volumes reduziert, um als offensichtliches Beispiel zu dienen.
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

Für die Verwaltung einiger Docker-Container ist die Verwendung von systemd eine Option. Es standardisiert die Steuerung und vereinfacht die Abhängigkeiten sowohl für native als auch für Docker-Services. Das generische Beispiel unten kann an jeden Container angepasst werden, indem die verschiedenen Werte und Optionen angepasst oder hinzugefügt werden.

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

# Hilfreiche Befehle

## Liste der laufenden Container anzeigen

```shell
    docker ps
```

## Shell *innerhalb* eines Containers

Das Ausführen eines Befehls in einen Container hinein, wird Sie in der Regel als Root-Benutzer anmelden.

```shell
    docker exec -it CONTAINER_NAME /bin/bash
```

Sobald Sie sich drinnen befinden, können Sie mit dem Befehl

```shell
    su - <Benutzername>
```

den Benutzer wechseln.

Um als bestimmter Benutzer einzuloggen, fügen Sie `-u` als Argument hinzu und geben Sie den Benutzernamen oder die ID an.

```shell
    docker exec -u BENUTZER -it CONTAINER_NAME /bin/bash
```

### Beispiele als bestimmte Benutzer

#### LSIO Radarr

```shell
    docker exec -u abc -it radarr bash
```

#### Hotio Sonarr

```shell
    docker exec -u hotio -it sonarr bash
```

Weitere Informationen finden Sie in der [docker exec](https://docs.docker.com/engine/reference/commandline/exec/)-Dokumentation.

## Docker aufräumen

```shell
    docker system prune --all --volumes
```

> Entfernt nicht verwendete Container, Netzwerke, Volumes, Images und Build-Cache. Wie in der WARNUNG dieses Befehls angegeben, werden dadurch alle zuvor genannten Elemente für alles entfernt, was nicht von einem laufenden Container verwendet wird. In einer korrekt konfigurierten Umgebung ist dies in Ordnung. Seien Sie jedoch vorsichtig und gehen Sie beim ersten Mal vorsichtig vor. Weitere Informationen finden Sie in der [Docker system prune](https://docs.docker.com/engine/reference/commandline/system_prune/)-Dokumentation.
{.is-warning}

## Docker run-Befehl abrufen

Das Abrufen des `docker run`-Befehls von GUI-Managern kann schwierig sein, aber mit diesem Docker-Image ist es einfach für einen laufenden Container ([Quelle](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container)).

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike CONTAINER_NAME
```

## Docker-Compose abrufen

> Darüber hinaus können Sie [TRaSH's Guide für docker-compose](https://trash-guides.info/compose/) überprüfen.
{.is-info}

Das Abrufen einer `docker-compose.yml` von laufenden Instanzen ist mit [docker-autocompose](https://github.com/Red5d/docker-autocompose) möglich, falls Sie Ihre Container bereits mit `docker run` oder `docker create` gestartet haben und zu einem `docker-compose`-Stil wechseln möchten. Es ist auch großartig, um Ihre Einstellungen mit anderen zu teilen, da es keine Rolle spielt, welche Management-Software Sie verwenden. Der letzte Argument(e) sind die Namen Ihrer Container und Sie können so viele auf einmal übergeben, wie Sie benötigen. Der erste Containername ist erforderlich, weitere sind optional. Sie können die Container-Namen in der **NAMES**-Spalte von `docker ps` sehen, sie werden normalerweise von Ihnen festgelegt oder können basierend auf dem Image generiert werden, wie z.B. `binhex-qbittorrent`. Es ist *nicht* der Image-Name, wie z.B. `binhex/arch-qbittorrentvpn`.

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $CONTAINER_NAME $ANOTHER_CONTAINER_NAME ... $ONE_MORE_CONTAINER_NAME
```

Für einige Benutzer könnte dies sein:

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose lidarr prowlarr radarr readarr sonarr qbittorrent
```

## Netzwerkprobleme beheben

Die meisten Docker-Images enthalten nicht viele nützliche Tools zur Fehlerbehebung, aber Sie können einem vorhandenen Container ein Netzwerk-Fehlerbehebungs-Image [anhängen](https://hub.docker.com/r/nicolaka/netshoot), um dabei zu helfen.

```shell
    docker run -it --rm --network container:CONTAINER_NAME nicolaka/netshoot
```

## Benutzer und Gruppe rekursiv ändern

```shell
    chown -R benutzer:gruppe /pfad/hier
```

## Rekursiv auf 775/664 chmod setzen

```shell
    chmod -R a=,a+rX,u+w,g+w /pfad/hier
              ^  ^    ^   ^ fügt Schreibzugriff für Gruppe hinzu
              |  |    | fügt Schreibzugriff für Benutzer hinzu
              |  | fügt Lesezugriff für alle und Ausführung für alle Ordner hinzu (steuert den Zugriff)
              | setzt alle auf `000`
```

## UID/GID für Benutzer ermitteln

```shell
    id <benutzername>
```

## Dateien auf Hardlinks überprüfen

```shell
    ls -alhi
    42207934 -rw-r--r--  2 benutzer gruppe    0 Sep 11 11:55 # hardlinked
    42207936 -rw-r--r--  1 benutzer gruppe    0 Sep 11 11:55 # keine Hardlinks
    42207934 -rw-r--r--  2 benutzer gruppe    0 Sep 11 11:55 # Original

    stat original
      Datei: original
      Größe: 0               Blöcke: 0          IO-Block: 4096   normale leere Datei
    Gerät: 803h/2051d      Inode: 42207934    Links: 2
    Zugriff: (0644/-rw-r--r--)  Uid: ( 1000/ benutzer)   Gid: ( 1001/ gruppe)
    Zugriff: 2020-09-11 11:55:43.803327144 -0500
    Änderung: 2020-09-11 11:55:43.803327144 -0500
    Statusänderung: 2020-09-11 11:55:49.706660476 -0500
     Erstellt: 2020-09-11 11:55:43.803327144 -0500
```

# Interessante Docker-Images

- [rasmunk/sshfs](https://github.com/rasmunk/docker-volume-sshfs)
{.links-list}
- Die Dokumentation und das Dockerfile von [hotio](https://hotio.dev/) machen keine schlechten Pfadvorschläge. Die Images werden automatisch alle 2 Stunden aktualisiert, wenn Änderungen am Upstream gefunden werden. Hotio baut auch unsere Pull Requests (außer Sonarr), was für Tests nützlich sein kann.
  - [sonarr](https://hotio.dev/containers/sonarr)
  - [radarr](https://hotio.dev/containers/radarr)
  - [lidarr](https://hotio.dev/containers/lidarr)
  - [readarr](https://hotio.dev/containers/readarr)
  - [prowlarr](https://hotio.dev/containers/prowlarr) für Usenet- und Torrent-Tracker-Suche
  - [qbittorrent](https://hotio.dev/containers/qbittorrent/)
  - [NZBGet](https://hotio.dev/containers/nzbget/)
  - [SABnzbd](https://hotio.dev/containers/sabnzbd/)
  - [qflood](https://hotio.dev/containers/qflood/)
  - [ombi](https://hotio.dev/containers/ombi) zur Anforderung von Medien
  - [overseerr](https://hotio.dev/containers/overseerr/) zur Anforderung von Medien
  - [jackett](https://hotio.dev/containers/jackett) zur Torrent-Tracker-Suche
  - [nzbhydra2](https://hotio.dev/containers/nzbhydra2) zur Usenet-Indexer-Suche
  - [bazarr](https://hotio.dev/containers/bazarr) für Untertitel
  - [pullio](https://hotio.dev/pullio/) zur automatischen Aktualisierung von Containern
  - [unpackerr](https://hotio.dev/containers/unpackerr) ist nützlich für das Entpacken von gepackten Torrents bei verschiedenen Torrent-Clients, bei denen das Entpacken fehlt oder vollständig fehlt.
{.links-list}
- [linuxserver.io](https://hub.docker.com/u/linuxserver) bietet Images für *viele* Software an und sie werden gut gepflegt. Vermeiden Sie jedoch ihre 'vorgeschlagenen (optionalen)' Pfade.
  - [SWAG Proxy](https://hub.docker.com/r/linuxserver/swag)
  - [qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/)
  - [deluge](https://hub.docker.com/r/linuxserver/deluge/)
  - [rtorrent](https://hub.docker.com/r/linuxserver/rutorrent/)
  - [SABnzbd](https://hub.docker.com/r/linuxserver/sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/)
  - [sonarr](https://hub.docker.com/r/linuxserver/sonarr/)
  - [radarr](https://hub.docker.com/r/linuxserver/radarr/)
  - [lidarr](https://hub.docker.com/r/linuxserver/lidarr/)
- [binhex](https://hub.docker.com/u/binhex) ist ein weiterer beliebter Betreuer
  - [qbittorrent](https://hub.docker.com/r/binhex/arch-qbittorrentvpn/)
  - [deluge](https://hub.docker.com/r/binhex/arch-delugevpn/)
  - [rtorrent](https://hub.docker.com/r/binhex/arch-rtorrentvpn/)
  - [SABnzbd](https://hub.docker.com/r/binhex/arch-sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/binhex/arch-nzbget/)
  - [sonarr](https://hub.docker.com/r/binhex/arch-sonarr/)
  - [radarr](https://hub.docker.com/r/binhex/arch-radarr/)
  - [lidarr](https://hub.docker.com/r/binhex/arch-lidarr/)
{.links-list}

### All-in-One-Lösungen

- [Dies ist ein GitHub-Repository](https://github.com/Luctia/ezarr), das sich an Anfänger richtet, die Docker für ihren Servarr-Stack verwenden möchten. Es ist im Grunde eine fertige Sammlung von Dateien und erfordert nur das Ausführen von zwei Befehlen, um alles online zu bringen. Es beseitigt den Aufwand bei der Benutzerverwaltung und den Berechtigungen auf dem Host-Gerät und enthält einige andere Anwendungen wie PleX.

# Benutzerdefiniertes Docker-Netzwerk und DNS

Ein interessantes Feature eines [benutzerdefinierten Docker-Netzwerks](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks) ist, dass es seinen eigenen DNS-Server hat. Wenn Sie ein Bridge-Netzwerk für Ihre Container erstellen, können Sie deren Hostnamen in Ihrer Konfiguration verwenden. Zum Beispiel, wenn Sie `docker run --network=isolated --hostname=deluge binhex/arch-deluge` und `docker run --network=isolated --hostname=radarr binhex/arch-radarr` ausführen, können Sie den Download-Client in Radarr so konfigurieren, dass er nur auf `deluge` zeigt, und es funktioniert *und* kommuniziert in seinem eigenen privaten Netzwerk. Das bedeutet, dass Sie, wenn Sie noch sicherer sein möchten, *auch* das Weiterleiten dieses Ports stoppen könnten. Wenn Sie Ihren Reverse-Proxy-Container im selben Netzwerk platzieren, können Sie sogar das Weiterleiten der Web-Schnittstellen-Ports stoppen und sie noch sicherer machen.

# Häufige Probleme

## Richtige *externe* Pfade, falsche *interne* Pfade

Viele Leute lesen das und denken, sie verstehen es, aber sie sehen den externen Pfad korrekt als etwas wie `/data/usenet`, aber dann verstehen sie den Punkt nicht und setzen den *internen* Pfad immer noch auf `/downloads`.

- Gut:
  - `/host/data/usenet:/data/usenet`
  - `/data/media:/data/media`
- Schlecht:
  - `/host/data:/downloads`
  - `/host/data:/media`
  - `/data/downloads:/data`

## Ausführen von Docker-Containern als root oder Ändern von Benutzern

Wenn Sie feststellen, dass Sie Ihre Container als `root:root` ausführen, machen Sie etwas falsch. Wenn Sie keine UID und GID übergeben, verwenden Sie standardmäßig das, was für das Image voreingestellt ist, und *das* wird wahrscheinlich nicht mit einem vernünftigen Benutzer auf Ihrem System übereinstimmen. Und wenn Sie den Benutzer und die Gruppe ändern, unter der Ihre Docker-Container ausgeführt werden, treten wahrscheinlich Berechtigungsprobleme in Ordnern wie dem `/config`-Ordner auf, in dem wahrscheinlich Dateien und Ordner vorhanden sind, die beim ersten Mal mit der UID/GID erstellt wurden, die Sie beim ersten Mal verwendet haben.

## Ausführen von Docker-Containern mit umask 000

Wenn Sie feststellen, dass Sie eine UMASK von `000` setzen (was 777 für Ordner und 666 für Dateien ist), machen Sie *auch* etwas falsch. Dadurch werden Ihre Dateien und Ordner für *jeden* lesbar/schreibbar, was schlechte Linux-Hygiene ist.

# Hilfe erhalten

## Chat-Support (Discord)

- [Sonarr Discord](https://discord.sonarr.tv/)
- [Radarr Discord](https://radarr.video/discord)
{.links-list}

## Foren-Support (Reddit)

- [/r/sonarr](http://reddit.com/r/sonarr)
- [/r/radarr](http://reddit.com/r/radarr)
{.links-list}