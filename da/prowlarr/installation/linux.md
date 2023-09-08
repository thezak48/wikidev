---
title: Prowlarr Linux Installation
description: Linux installationsguide til Prowlarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Bemærk: Raspberry Pi OS og Raspbian er begge varianter af Debian {.is-info}

### Nem installation

For Debian / Ubuntu / Raspbian begyndere er der ikke et Apt Repository eller Deb-pakke.

Hvis du vil have en nem installation, skal du følge denne fællesskabsleverede og vedligeholdte `Easy Install`-script til en grundlæggende Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installation.

**Følg de officielle installationsinstruktioner, der er 'Hands on', i [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) trinene længere nede.**

[Se venligst \*Arr Community Installation Script](/install-script)

### Debian / Ubuntu Hands on Install

Du skal installere binærerne ved hjælp af følgende kommandoer.

> Nedenstående trin vil downloade Prowlarr og installere det i `/opt`
> Prowlarr vil køre under brugeren `prowlarr` og gruppen `prowlarr`
> Prowlarr's konfigurationsfiler vil blive gemt i `/var/lib/prowlarr`
{.is-warning}

- Sørg for, at du har de nødvendige forudsætningspakker:

```shell
sudo apt install curl sqlite3
```

> Advarsel: Hvis du ignorerer nedenstående forudsætninger, vil det resultere i en mislykket installation og en ikke-fungerende applikation. {.is-warning}

> **Installation Forudsætninger**
> Nedenstående instruktioner er baseret på følgende forudsætninger. Ændr instruktionerne efter behov for at passe til dine specifikke behov, hvis det er nødvendigt.
> \* Brugeren `prowlarr` er oprettet
> \* Du har oprettet mappen `/var/lib/prowlarr` og sikret, at brugeren `prowlarr` har læse/skrive adgang til den
{.is-danger}

> Ved at fortsætte nedenfor bekræfter du, at du har læst og opfyldt ovenstående krav. {.is-warning}

- Download de korrekte binærer til din arkitektur.
  - Du kan bestemme din arkitektur med `dpkg --print-architecture`
    - AMD64 brug `arch=x64`
    - ARM, armf og armh brug `arch=arm`
    - ARM64 brug `arch=arm64`

```shell
wget --content-disposition 'http://prowlarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Udpak filerne:

```shell
tar -xvzf Prowlarr*.linux*.tar.gz
```

- Flyt filerne til `/opt/`

```shell
sudo mv Prowlarr/ /opt
```

> Dette antager, at du har oprettet brugeren og vil køre som brugeren `prowlarr` og gruppen `prowlarr`. Du kan ændre dette, så det passer til dit brugsscenarie.
{.is-danger}

- Sørg for, at du ejer binærmappen.

```shell  
sudo chown prowlarr:prowlarr -R /opt/Prowlarr
```

- Konfigurer systemd, så Prowlarr kan starte automatisk ved opstart.

> Nedenstående systemd-oprettelsesscript vil bruge en data-mappe på `/var/lib/prowlarr`. Sørg for, at den eksisterer, eller ændr den efter behov. For standard data-mappen `/home/$USER/.config/Prowlarr` skal du blot fjerne `-data`-argumentet. Bemærk, at `$USER` er brugeren, som Prowlarr kører som, og er defineret nedenfor.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/prowlarr.service > /dev/null
[Unit]
Description=Prowlarr Daemon
After=syslog.target network.target
[Service]
User=prowlarr
Group=prowlarr
Type=simple

ExecStart=/opt/Prowlarr/Prowlarr -nobrowser -data=/var/lib/prowlarr/
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

- Aktivér Prowlarr-tjenesten:

```shell
sudo systemctl enable --now -q prowlarr
```

- (Valgfrit) Fjern tarballen:

```shell
rm Prowlarr*.linux*.tar.gz
```

Normalt kan du få adgang til Prowlarr web-GUI'en ved at browse til `http://{Din server IP-adresse}:9696`

Hvis Prowlarr ikke ser ud til at starte, skal du kontrollere status for tjenesten:

```shell
sudo journalctl --since today -u prowlarr
```

---

### Afinstallation

For at afinstallere og fjerne:

> Advarsel: Dette vil ødelægge dine applikationsdata. {.is-danger}

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /var/lib/prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```

For at afinstallere og beholde dine applikationsdata:

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```