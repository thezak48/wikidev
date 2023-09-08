---
title: Radarr Linux Installation
description: Linux installationsguide til Radarr
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

**For de officielle installationsinstruktioner, der er 'Hands on', følg [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) trinene længere nede.**

[Se venligst \*Arr Community Installation Script](/install-script)

> Radarr bruger en pakket version af ffprobe til analyse af mediefiler og kræver ikke, at ffprobe eller ffmpeg er installeret på systemet. Hvis Radarr siger, at Ffprobe ikke findes, kan dette typisk løses med en geninstallation.
{.is-info}

### Debian / Ubuntu Hands on Install

Du skal installere binærerne ved hjælp af følgende kommandoer.

> Nedenstående trin vil downloade Radarr og installere det i `/opt`
> Radarr vil køre under brugeren `radarr` og gruppen `media`; `media` er den almindeligt foreslåede gruppe at køre \*Arrs, downloadklienter og medieserver under.
> Radarr's konfigurationsfiler vil blive gemt i `/var/lib/radarr`
{.is-success}

- Sørg for, at du har de nødvendige forudsætningspakker:

```shell
sudo apt install curl sqlite3
```

> Advarsel: Hvis du ignorerer nedenstående forudsætninger, vil det resultere i en mislykket installation og en ikke-fungerende applikation. {.is-warning}

> **Installation Forudsætninger**
> Nedenstående instruktioner er baseret på følgende forudsætninger. Ændr instruktionerne efter behov for at passe til dine specifikke behov, hvis det er nødvendigt.
> \* Brugeren `radarr` er oprettet
> \* Brugeren `radarr` er en del af gruppen `media`
> \* Dine downloadklienter og medieserver kører som og er en del af gruppen `media`
> \* Dine stier, der bruges af dine downloadklienter og medieserver, er tilgængelige (læse/skrive) for gruppen `media`
> \* Du har oprettet mappen `/var/lib/radarr` og sikret, at brugeren `radarr` har læse/skrive-rettigheder til den
{.is-danger}

> Ved at fortsætte nedenfor bekræfter du, at du har læst og opfyldt ovenstående krav. {.is-success}

- Download de korrekte binærer til din arkitektur.
  - Du kan bestemme din arkitektur med `dpkg --print-architecture`
    - AMD64 brug `arch=x64`
    - ARM, armf og armh brug `arch=arm`
    - ARM64 brug `arch=arm64`

```shell
wget --content-disposition 'http://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Udpak filerne:

```shell
tar -xvzf Radarr*.linux*.tar.gz
```

- Flyt filerne til `/opt/`

```shell
sudo mv Radarr /opt/
```

> Bemærk: Dette antager, at du kører som brugeren `radarr` og gruppen `media`. Du kan ændre dette for at passe til dit brugstilfælde. Det er vigtigt at vælge disse korrekt for at undgå tilladelsesproblemer med dine mediefiler. Vi foreslår, at du holder mindst gruppenavnet identisk mellem dine downloadklient(er) og Radarr.
{.is-danger}

- Sørg for ejerskab af binærmappen.

```shell  
sudo chown radarr:radarr -R /opt/Radarr
```

- Konfigurer systemd, så Radarr kan starte automatisk ved opstart.

> Nedenstående systemd-oprettelsesscript vil bruge en data-mappe på `/var/lib/radarr`. Sørg for, at den eksisterer, eller ændr den efter behov. For standard-datamappen `/home/$USER/.config/Radarr` skal du blot fjerne `-data`-argumentet. Bemærk, at `$USER` er brugeren, som Radarr kører som, og er defineret nedenfor.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/radarr.service > /dev/null
[Unit]
Description=Radarr Daemon
After=syslog.target network.target
[Service]
User=radarr
Group=media
Type=simple

ExecStart=/opt/Radarr/Radarr -nobrowser -data=/var/lib/radarr/
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

- Aktivér Radarr-tjenesten:

```shell
sudo systemctl enable --now -q radarr
```

- (Valgfrit) Fjern tarballen:

```shell
rm Radarr*.linux*.tar.gz
```

Normalt kan du få adgang til Radarr-webgrænsefladen ved at browse til `http://{Din server IP-adresse}:7878`

> Radarr bruger en pakket version af ffprobe til analyse af mediefiler og kræver ikke, at ffprobe eller ffmpeg er installeret på systemet. Hvis Radarr siger, at Ffprobe ikke findes, kan dette typisk løses med en geninstallation.
{.is-info}

Hvis Radarr ikke ser ud til at starte, skal du kontrollere status for tjenesten:

```shell
sudo journalctl --since today -u radarr
```

---

### Afinstallation

For at afinstallere og fjerne helt:
> Advarsel: Dette vil ødelægge dine applikationsdata. {.is-danger}

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /var/lib/radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```

For at afinstallere og beholde dine applikationsdata:

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```