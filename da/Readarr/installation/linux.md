---
title: Readarr Linux Installation
description: Linux installationsguide til Readarr
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

Hvis du vil have en nem liv, så følg denne fællesskabsleverede og vedligeholdte `Easy Install`-script til en grundlæggende Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installation.

**For de officielle installationsinstruktioner, der er 'Hands on', skal du følge [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) trinene længere nede.**

[Se venligst \*Arr Community Installation Script](/install-script)

### Debian / Ubuntu Hands on Install

Du skal installere binærerne ved hjælp af følgende kommandoer.

> Nedenstående trin vil downloade Readarr og installere det i `/opt`
> Readarr vil køre under brugeren `readarr` og gruppen `media`; `media` er den almindeligt foreslåede gruppe at køre \*Arrs, downloadklienter og medieservere under.
> Readarr's konfigurationsfiler vil blive gemt i `/var/lib/readarr`
{.is-warning}

- Sørg for, at du har de nødvendige forudsætningspakker:

```shell
sudo apt install curl sqlite3
```

> Advarsel: Hvis du ignorerer nedenstående forudsætninger, vil det resultere i en mislykket installation og en ikke-fungerende applikation. {.is-warning}

> **Installation Prerequisites**
> Nedenstående instruktioner er baseret på følgende forudsætninger. Ændr instruktionerne efter behov for at passe til dine specifikke behov, hvis det er nødvendigt.
> \* Brugeren `readarr` er oprettet
> \* Brugeren `readarr` er en del af gruppen `media`
> \* Dine downloadklienter og medieservere kører som og er en del af gruppen `media`
> \* Dine stier, der bruges af dine downloadklienter og medieservere, er tilgængelige (læse/skrive) for gruppen `media`
> \* Hvis Calibre skal bruges, kører Calibre som gruppen `media`, og Calibre-biblioteket har læse/skrive-adgang til `media`
> \* Du har oprettet mappen `/var/lib/readarr` og sikret, at brugeren `readarr` har læse/skrive-adgang til den
{.is-danger}

> Ved at fortsætte nedenfor bekræfter du, at du har læst og opfyldt ovenstående krav. {.is-warning}

- Download de korrekte binærer til din arkitektur.
  - Du kan bestemme din arkitektur med `dpkg --print-architecture`
    - AMD64 brug `arch=x64`
    - ARM, armf og armh brug `arch=arm`
    - ARM64 brug `arch=arm64`

```shell
wget --content-disposition 'http://readarr.servarr.com/v1/update/develop/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Udpak filerne:

```shell
tar -xvzf Readarr*.linux*.tar.gz
```

- Flyt filerne til `/opt/`

```shell
sudo mv Readarr /opt/
```

> Bemærk: Dette antager, at du har oprettet brugeren og vil køre som brugeren `readarr` og gruppen `media`. Du kan ændre dette for at passe til dit brugstilfælde. Det er vigtigt at vælge disse korrekt for at undgå tilladelsesproblemer med dine mediefiler. Vi foreslår, at du holder mindst gruppenavnet identisk mellem dine downloadklient(er) og Readarr. Bemærk venligst, at hvis du ønsker at bruge Calibre - skal Readarr have tilladelser til den mappe.
{.is-danger}

- Sørg for ejerskab af binærmappen.

```shell  
sudo chown readarr:readarr -R /opt/Readarr
```

- Konfigurer systemd, så Readarr kan starte automatisk ved opstart.

> Nedenstående systemd-oprettelsesscript vil bruge en data-mappe på `/var/lib/readarr`. Sørg for, at den eksisterer, eller ændr den efter behov. For standarddata-mappen `/home/$USER/.config/Readarr` skal du blot fjerne `-data`-argumentet. Bemærk, at `$USER` er brugeren, som Readarr kører som, og som er defineret nedenfor.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr.service > /dev/null
[Unit]
Description=Readarr Daemon
After=syslog.target network.target
[Service]
User=readarr
Group=media
Type=simple

ExecStart=/opt/Readarr/Readarr -nobrowser -data=/var/lib/readarr/
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

- Aktivér Readarr-tjenesten:

```shell
sudo systemctl enable --now -q readarr
```

- (Valgfrit) Fjern tarballen:

```shell
rm Readarr*.linux*.tar.gz
```

Normalt for at få adgang til Readarr web-GUI, skal du browse til `http://{Din server IP-adresse}:8787`

Hvis Readarr ikke ser ud til at starte, skal du kontrollere status for tjenesten:

```shell
sudo journalctl --since today -u readarr
```

---

### Afinstallation

For at afinstallere og fjerne:

> Advarsel: Dette vil ødelægge dine applikationsdata. {.is-danger}

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /var/lib/readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```

For at afinstallere og beholde dine applikationsdata:

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```