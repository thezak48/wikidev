---
title: Readarr Linux Installatie
description: Installatiehandleiding voor Readarr op Linux
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

**Voor de officiële installatie-instructies die 'hands-on' zijn, volg je de [Debian / Ubuntu Hands-on Installatie](#debian-ubuntu-hands-on-install) stappen hieronder.**

[Zie het \*Arr Community Installatiescript](/install-script)

### Debian / Ubuntu Hands-on Installatie

Je moet de binaries installeren met behulp van de onderstaande commando's.

> De onderstaande stappen zullen Readarr downloaden en installeren in `/opt`
> Readarr zal worden uitgevoerd onder de gebruiker `readarr` en de groep `media`; `media` is de veelgebruikte groep om de \*Arrs, downloadclients en mediaserver onder uit te voeren.
> De configuratiebestanden van Readarr worden opgeslagen in `/var/lib/readarr`
{.is-warning}

- Zorg ervoor dat je de vereiste afhankelijkheidspakketten hebt geïnstalleerd:

```shell
sudo apt install curl sqlite3
```

> Waarschuwing: Het negeren van de onderstaande vereisten zal resulteren in een mislukte installatie en een niet-functionele applicatie. {.is-warning}

> **Installatievereisten**
> De onderstaande instructies zijn gebaseerd op de volgende vereisten. Pas de instructies aan indien nodig om aan je specifieke behoeften te voldoen.
> \* De gebruiker `readarr` is aangemaakt
> \* De gebruiker `readarr` maakt deel uit van de groep `media`
> \* Je downloadclients en mediaserver worden uitgevoerd als en maken deel uit van de groep `media`
> \* Je paden die worden gebruikt door je downloadclients en mediaserver zijn toegankelijk (lezen/schrijven) voor de groep `media`
> \* Als Calibre wordt gebruikt, wordt Calibre uitgevoerd als de groep `media` en heeft de Calibre-bibliotheek lees-/schrijfrechten voor `media`
> \* Je hebt de map `/var/lib/readarr` aangemaakt en ervoor gezorgd dat de gebruiker `readarr` lees-/schrijfrechten heeft voor deze map
{.is-danger}

> Door hieronder verder te gaan, bevestig je dat je de bovenstaande vereisten hebt gelezen en voldaan. {.is-warning}

- Download de juiste binaries voor jouw architectuur.
  - Je kunt jouw architectuur bepalen met `dpkg --print-architecture`
    - AMD64 gebruikt `arch=x64`
    - ARM, armf en armh gebruiken `arch=arm`
    - ARM64 gebruikt `arch=arm64`

```shell
wget --content-disposition 'http://readarr.servarr.com/v1/update/develop/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Pak de bestanden uit:

```shell
tar -xvzf Readarr*.linux*.tar.gz
```

- Verplaats de bestanden naar `/opt/`

```shell
sudo mv Readarr /opt/
```

> Opmerking: Dit gaat ervan uit dat je de gebruiker hebt aangemaakt en dat Readarr wordt uitgevoerd als de gebruiker `readarr` en de groep `media`. Je kunt dit aanpassen aan jouw situatie. Het is belangrijk om deze correct te kiezen om problemen met machtigingen voor je mediabestanden te voorkomen. We raden aan om ten minste de groepsnaam identiek te houden tussen je downloadclient(s) en Readarr. Houd er rekening mee dat als je Calibre wilt gebruiken, Readarr machtigingen nodig heeft voor die map.
{.is-danger}

- Zorg ervoor dat de binmap eigendom is van de gebruiker.

```shell  
sudo chown readarr:readarr -R /opt/Readarr
```

- Configureer systemd zodat Readarr automatisch start bij het opstarten.

> Het onderstaande systemd-creatie-script zal een gegevensmap van `/var/lib/readarr` gebruiken. Zorg ervoor dat deze bestaat of pas deze aan indien nodig. Voor de standaard gegevensmap van `/home/$USER/.config/Readarr` verwijder je eenvoudig het `-data` argument. Let op: `$USER` is de gebruiker waar Readarr als wordt uitgevoerd en is hieronder gedefinieerd.
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

- Herlaad systemd:

```shell
sudo systemctl -q daemon-reload
```

- Activeer de Readarr-service:

```shell
sudo systemctl enable --now -q readarr
```

- (Optioneel) Verwijder het tarball-bestand:

```shell
rm Readarr*.linux*.tar.gz
```

Typisch gezien kun je de Readarr web-GUI openen door naar `http://{Het IP-adres van je server}:8787` te gaan

Als Readarr niet lijkt te starten, controleer dan de status van de service:

```shell
sudo journalctl --since today -u readarr
```

---

### Verwijderen

Om te verwijderen en te verwijderen:
> Waarschuwing: Dit zal je applicatiedata vernietigen. {.is-danger}

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /var/lib/readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```

Om te verwijderen en je applicatiedata te behouden:

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```