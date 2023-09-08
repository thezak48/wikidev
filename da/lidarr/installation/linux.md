---
title: Lidarr Linux Installation
description: Linux installationsguide til Lidarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Bemærk: Raspberry Pi OS og Raspbian er begge varianter af Debian {.is-info}

> Lidarr v0.8 er ikke kompatibel eller understøttet på Ubuntu 22.04 [Se denne FAQ-indgang for detaljer](/lidarr/faq#lidarr-stopped-working-after-updating-to-ubuntu-2204)
{.is-warning}

### Nem installation

For Debian / Ubuntu / Raspbian begyndere er der ikke et Apt Repository eller Deb-pakke.

Hvis du vil have en nem liv, skal du følge denne fællesskabsleverede og vedligeholdte `Easy Install`-script til en grundlæggende Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installation.

**For de officielle installationsinstruktioner, der er 'Hands on', skal du følge [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) trinene længere nede.**

[Se venligst \*Arr Community Installation Script](/install-script)

### Debian / Ubuntu Hands on Install

Du skal installere binærerne ved hjælp af nedenstående kommandoer.

> Nedenstående trin vil downloade Lidarr og installere det i `/opt`
> Lidarr vil køre under brugeren `lidarr` og gruppen `media`
> Lidarr's konfigurationsfiler vil blive gemt i `/var/lib/lidarr`
{.is-warning}

- Sørg for, at du har de nødvendige forudsætningspakker:

```shell
sudo apt install curl mediainfo sqlite3 libchromaprint-tools
```

> Advarsel: Hvis du ignorerer nedenstående forudsætninger, vil det resultere i en mislykket installation og en ikke-fungerende applikation. {.is-warning}

> **Installation Prerequisites**
> Nedenstående instruktioner er baseret på følgende forudsætninger. Ændr instruktionerne efter behov for at passe til dine specifikke behov, hvis det er nødvendigt.
> \* Brugeren `lidarr` er oprettet
> \* Brugeren `lidarr` er en del af gruppen `media`
> \* Dine downloadklienter og medieserver kører som og er en del af gruppen `media`
> \* Dine stier, der bruges af dine downloadklienter og medieserver, er tilgængelige (læse/skrive) for gruppen `media`
> \* Du har oprettet mappen `/var/lib/lidarr` og sikret, at brugeren `lidarr` har læse/skrive-rettigheder til den
{.is-danger}

> Ved at fortsætte nedenfor bekræfter du, at du har læst og opfyldt ovenstående krav. {.is-warning}

- Download de korrekte binærer til din arkitektur.
  - Du kan bestemme din arkitektur med `dpkg --print-architecture`
    - AMD64 brug `arch=x64`
    - ARM, armf og armh brug `arch=arm`
    - ARM64 brug `arch=arm64`

```shell
wget --content-disposition 'http://lidarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Udpak filerne:

```shell
tar -xvzf Lidarr*.linux*.tar.gz
```

- Flyt filerne til `/opt/`

```shell
sudo mv Lidarr/ /opt
```

> Dette antager, at du har oprettet brugeren og vil køre som brugeren `lidarr` og gruppen `media`. Du kan ændre dette for at passe til dit brugstilfælde. Det er vigtigt at vælge disse korrekt for at undgå tilladelsesproblemer med dine mediefiler. Vi foreslår, at du holder mindst gruppenavnet identisk mellem dine downloadklient(er) og Lidarr.
{.is-danger}

- Sørg for ejerskab af binærmappen.

```shell
sudo chown -R lidarr:media /opt/Lidarr
```

- Konfigurer systemd, så Lidarr kan starte automatisk ved opstart.

> Nedenstående systemd-oprettelsesscript vil bruge en data-mappe på `/var/lib/lidarr`. Sørg for, at den eksisterer, eller ændr den efter behov. For standarddata-mappen `/home/$USER/.config/Lidarr` skal du blot fjerne `-data`-argumentet. Bemærk, at `$USER` er brugeren, som Lidarr kører som, og som er defineret nedenfor.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/lidarr.service > /dev/null
[Unit]
Description=Lidarr Daemon
After=syslog.target network.target
[Service]
User=lidarr
Group=media
Type=simple

ExecStart=/opt/Lidarr/Lidarr -nobrowser -data=/var/lib/lidarr/
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
```

- Genindlæs systemd:

```shell
sudo systemctl -q daemon-reload
```

- Aktivér Lidarr-tjenesten:

```shell
sudo systemctl enable --now -q lidarr
```

- (Valgfrit) Fjern tarballen:

```shell
rm Lidarr*.linux*.tar.gz
```

Normalt for at få adgang til Lidarr-web-GUI'en skal du browse til `http://{Din server IP-adresse}:8686`

Hvis Lidarr ikke ser ud til at starte, skal du kontrollere status for tjenesten:

```shell
sudo journalctl --since today -u lidarr
```

---

### Afinstallation

For at afinstallere og fjerne:

> Advarsel: Dette vil ødelægge dine applikationsdata. {.is-danger}

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /var/lib/lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```

For at afinstallere og beholde dine applikationsdata:

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```