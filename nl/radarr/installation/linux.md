---
title: Radarr Linux Installatie
description: Installatiehandleiding voor Radarr op Linux
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Opmerking: Raspberry Pi OS en Raspbian zijn beide varianten van Debian {.is-info}

### Eenvoudige installatie

Voor beginners op Debian / Ubuntu / Raspbian is er geen Apt Repository of Deb-pakket beschikbaar.

Als je het jezelf gemakkelijk wilt maken, volg dan dit door de community geleverde en onderhouden `Eenvoudige installatie` script voor een basisinstallatie van Debian (Raspbian / Raspberry Pi OS) / Ubuntu.

**Voor de officiële installatie-instructies die 'hands-on' zijn, volg je de [Debian / Ubuntu Hands-on Installatie](#debian-ubuntu-hands-on-installatie) stappen hieronder.**

[Zie het \*Arr Community Installatiescript](/install-script)

> Radarr gebruikt een gebundelde versie van ffprobe voor het analyseren van mediabestanden en vereist geen installatie van ffprobe of ffmpeg op het systeem. Als Radarr aangeeft dat Ffprobe niet is gevonden, kan dit meestal worden opgelost met een herinstallatie.
{.is-info}

### Debian / Ubuntu Hands-on Installatie

Je moet de binaries installeren met behulp van de onderstaande commando's.

> De onderstaande stappen zullen Radarr downloaden en installeren in `/opt`
> Radarr zal worden uitgevoerd onder de gebruiker `radarr` en de groep `media`; `media` is de veelgebruikte groep om de \*Arrs, downloadclients en mediaserver onder uit te voeren.
> De configuratiebestanden van Radarr worden opgeslagen in `/var/lib/radarr`
{.is-success}

- Zorg ervoor dat je de vereiste afhankelijkheidspakketten hebt:

```shell
sudo apt install curl sqlite3
```

> Waarschuwing: Het negeren van de onderstaande vereisten zal leiden tot een mislukte installatie en een niet-functionele applicatie. {.is-warning}

> **Installatievereisten**
> De onderstaande instructies zijn gebaseerd op de volgende vereisten. Pas de instructies indien nodig aan om aan je specifieke behoeften te voldoen.
> \* De gebruiker `radarr` is aangemaakt
> \* De gebruiker `radarr` maakt deel uit van de groep `media`
> \* Je downloadclients en mediaserver worden uitgevoerd als en maken deel uit van de groep `media`
> \* Je paden die worden gebruikt door je downloadclients en mediaserver zijn toegankelijk (lezen/schrijven) voor de groep `media`
> \* Je hebt de map `/var/lib/radarr` aangemaakt en ervoor gezorgd dat de gebruiker `radarr` lees-/schrijfrechten heeft voor deze map
{.is-danger}

> Door hieronder verder te gaan, bevestig je dat je de bovenstaande vereisten hebt gelezen en voldaan. {.is-success}

- Download de juiste binaries voor jouw architectuur.
  - Je kunt jouw architectuur bepalen met `dpkg --print-architecture`
    - AMD64 gebruikt `arch=x64`
    - ARM, armf en armh gebruiken `arch=arm`
    - ARM64 gebruikt `arch=arm64`

```shell
wget --content-disposition 'http://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Pak de bestanden uit:

```shell
tar -xvzf Radarr*.linux*.tar.gz
```

- Verplaats de bestanden naar `/opt/`

```shell
sudo mv Radarr /opt/
```

> Opmerking: Dit gaat ervan uit dat je als gebruiker `radarr` en groep `media` zult draaien. Je kunt dit aanpassen aan jouw situatie. Het is belangrijk om deze correct te kiezen om problemen met machtigingen voor je mediabestanden te voorkomen. We raden aan om ten minste de groepsnaam identiek te houden tussen je downloadclient(s) en Radarr.
{.is-danger}

- Zorg ervoor dat de binmap eigendom is van de gebruiker.

```shell  
sudo chown radarr:radarr -R /opt/Radarr
```

- Configureer systemd zodat Radarr automatisch start bij het opstarten.

> Het onderstaande systemd-creatie script zal een gegevensmap van `/var/lib/radarr` gebruiken. Zorg ervoor dat deze bestaat of pas deze aan indien nodig. Voor de standaard gegevensmap van `/home/$USER/.config/Radarr` verwijder je eenvoudig het `-data` argument. Let op: `$USER` is de gebruiker waar Radarr onder draait en wordt hieronder gedefinieerd.
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

- Herlaad systemd:

```shell
sudo systemctl -q daemon-reload
```

- Activeer de Radarr-service:

```shell
sudo systemctl enable --now -q radarr
```

- (Optioneel) Verwijder het tarball-bestand:

```shell
rm Radarr*.linux*.tar.gz
```

Typisch gezien kun je de Radarr web-GUI openen door naar `http://{Het IP-adres van je server}:7878` te gaan

> Radarr gebruikt een gebundelde versie van ffprobe voor het analyseren van mediabestanden en vereist geen installatie van ffprobe of ffmpeg op het systeem. Als Radarr aangeeft dat Ffprobe niet is gevonden, kan dit meestal worden opgelost met een herinstallatie.
{.is-info}

Als Radarr niet lijkt te zijn gestart, controleer dan de status van de service:

```shell
sudo journalctl --since today -u radarr
```

---

### Verwijderen

Om te verwijderen en te verwijderen:
> Waarschuwing: Dit zal je applicatiegegevens vernietigen. {.is-danger}

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /var/lib/radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```

Om te verwijderen en je applicatiegegevens te behouden:

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```