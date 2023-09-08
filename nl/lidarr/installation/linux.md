---
title: Lidarr Linux Installatie
description: Installatiehandleiding voor Lidarr op Linux
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Opmerking: Raspberry Pi OS en Raspbian zijn beide varianten van Debian {.is-info}

> Lidarr v0.8 is niet compatibel en wordt niet ondersteund op Ubuntu 22.04 [Zie deze FAQ-entry voor details](/lidarr/faq#lidarr-stopped-working-after-updating-to-ubuntu-2204)
{.is-warning}

### Eenvoudige installatie

Voor beginners met Debian / Ubuntu / Raspbian is er geen Apt Repository of Deb-pakket beschikbaar.

Als je het jezelf gemakkelijk wilt maken, volg dan dit door de community geleverde en onderhouden `Easy Install` script voor een basisinstallatie van Debian (Raspbian / Raspberry Pi OS) / Ubuntu.

**Voor de officiële installatie-instructies die 'hands-on' zijn, volg je de [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install)-stappen hieronder.**

[Zie het \*Arr Community-installatiescript](/install-script)

### Debian / Ubuntu Hands on Install

Je moet de binaries installeren met behulp van de onderstaande commando's.

> De onderstaande stappen zullen Lidarr downloaden en installeren in `/opt`
> Lidarr zal worden uitgevoerd onder de gebruiker `lidarr` en de groep `media`
> De configuratiebestanden van Lidarr worden opgeslagen in `/var/lib/lidarr`
{.is-warning}

- Zorg ervoor dat je de vereiste afhankelijkheidspakketten hebt:

```shell
sudo apt install curl mediainfo sqlite3 libchromaprint-tools
```

> Waarschuwing: Het negeren van de onderstaande vereisten zal leiden tot een mislukte installatie en een niet-functionele applicatie. {.is-warning}

> **Installatievereisten**
> De onderstaande instructies zijn gebaseerd op de volgende vereisten. Pas de instructies indien nodig aan om aan je specifieke behoeften te voldoen.
> \* De gebruiker `lidarr` is aangemaakt
> \* De gebruiker `lidarr` maakt deel uit van de groep `media`
> \* Je downloadclients en mediaserver worden uitgevoerd als en maken deel uit van de groep `media`
> \* Je paden die worden gebruikt door je downloadclients en mediaserver zijn toegankelijk (lezen/schrijven) voor de groep `media`
> \* Je hebt de map `/var/lib/lidarr` aangemaakt en ervoor gezorgd dat de gebruiker `lidarr` lees-/schrijfrechten heeft
{.is-danger}

> Door hieronder verder te gaan, bevestig je dat je de bovenstaande vereisten hebt gelezen en voldaan. {.is-warning}

- Download de juiste binaries voor je architectuur.
  - Je kunt je architectuur bepalen met `dpkg --print-architecture`
    - AMD64 gebruikt `arch=x64`
    - ARM, armf en armh gebruiken `arch=arm`
    - ARM64 gebruikt `arch=arm64`

```shell
wget --content-disposition 'http://lidarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Pak de bestanden uit:

```shell
tar -xvzf Lidarr*.linux*.tar.gz
```

- Verplaats de bestanden naar `/opt/`

```shell
sudo mv Lidarr/ /opt
```

> Dit gaat ervan uit dat je de gebruiker hebt aangemaakt en dat Lidarr wordt uitgevoerd als de gebruiker `lidarr` en de groep `media`. Je kunt dit aanpassen aan je eigen situatie. Het is belangrijk om deze correct te kiezen om problemen met machtigingen voor je mediabestanden te voorkomen. We raden aan om ten minste de groepsnaam identiek te houden tussen je downloadclient(s) en Lidarr.
{.is-danger}

- Zorg ervoor dat de binmap eigendom is van de gebruiker.

```shell
sudo chown -R lidarr:media /opt/Lidarr
```

- Configureer systemd zodat Lidarr automatisch start bij het opstarten.

> Het onderstaande systemd-creatie-script zal een gegevensmap van `/var/lib/lidarr` gebruiken. Zorg ervoor dat deze bestaat of pas deze aan indien nodig. Voor de standaard gegevensmap `/home/$USER/.config/Lidarr` verwijder je eenvoudig het `-data`-argument. Let op: `$USER` is de gebruiker waar Lidarr als wordt uitgevoerd en is hieronder gedefinieerd.
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

- Herlaad systemd:

```shell
sudo systemctl -q daemon-reload
```

- Schakel de Lidarr-service in:

```shell
sudo systemctl enable --now -q lidarr
```

- (Optioneel) Verwijder het tarball-bestand:

```shell
rm Lidarr*.linux*.tar.gz
```

Typisch gezien kun je de Lidarr-webinterface openen door naar `http://{Het IP-adres van je server}:8686` te gaan

Als Lidarr niet lijkt te starten, controleer dan de status van de service:

```shell
sudo journalctl --since today -u lidarr
```

---

### Verwijderen

Om te verwijderen en te verwijderen:
> Waarschuwing: Dit zal je applicatiegegevens vernietigen. {.is-danger}

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /var/lib/lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```

Om te verwijderen en je applicatiegegevens te behouden:

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```