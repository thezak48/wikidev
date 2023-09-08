---
title: Prowlarr Linux Installatie
description: Installatiehandleiding voor Prowlarr op Linux
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

[Zie de \*Arr Community Installatiescript](/install-script)

### Debian / Ubuntu Hands-on Installatie

Je moet de binaries installeren met behulp van de onderstaande commando's.

> De onderstaande stappen zullen Prowlarr downloaden en installeren in `/opt`
> Prowlarr zal worden uitgevoerd onder de gebruiker `prowlarr` en de groep `prowlarr`
> De configuratiebestanden van Prowlarr worden opgeslagen in `/var/lib/prowlarr`
{.is-warning}

- Zorg ervoor dat je de vereiste afhankelijkheidspakketten hebt geïnstalleerd:

```shell
sudo apt install curl sqlite3
```

> Waarschuwing: Het negeren van de onderstaande vereisten zal resulteren in een mislukte installatie en een niet-functionele applicatie. {.is-warning}

> **Installatievereisten**
> De onderstaande instructies zijn gebaseerd op de volgende vereisten. Pas de instructies indien nodig aan om aan je specifieke behoeften te voldoen.
> \* De gebruiker `prowlarr` is aangemaakt
> \* Je hebt de map `/var/lib/prowlarr` aangemaakt en ervoor gezorgd dat de gebruiker `prowlarr` lees-/schrijfrechten heeft
{.is-danger}

> Door hieronder verder te gaan, bevestig je dat je de bovenstaande vereisten hebt gelezen en voldaan. {.is-warning}

- Download de juiste binaries voor jouw architectuur.
  - Je kunt jouw architectuur bepalen met `dpkg --print-architecture`
    - AMD64 gebruikt `arch=x64`
    - ARM, armf en armh gebruiken `arch=arm`
    - ARM64 gebruikt `arch=arm64`

```shell
wget --content-disposition 'http://prowlarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Pak de bestanden uit:

```shell
tar -xvzf Prowlarr*.linux*.tar.gz
```

- Verplaats de bestanden naar `/opt/`

```shell
sudo mv Prowlarr/ /opt
```

> Dit gaat ervan uit dat je de gebruiker hebt aangemaakt en dat Prowlarr wordt uitgevoerd als de gebruiker `prowlarr` en de groep `prowlarr`. Je kunt dit aanpassen aan jouw gebruikssituatie.
{.is-danger}

- Zorg ervoor dat de eigenaar van de map met binaries correct is.

```shell  
sudo chown prowlarr:prowlarr -R /opt/Prowlarr
```

- Configureer systemd zodat Prowlarr automatisch start bij het opstarten.

> Het onderstaande systemd-creatie script zal een gegevensmap van `/var/lib/prowlarr` gebruiken. Zorg ervoor dat deze bestaat of pas deze aan indien nodig. Voor de standaard gegevensmap van `/home/$USER/.config/Prowlarr` verwijder je eenvoudig het `-data` argument. Let op: `$USER` is de gebruiker waar Prowlarr onder wordt uitgevoerd en wordt hieronder gedefinieerd.
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

- Herlaad systemd:

```shell
sudo systemctl -q daemon-reload
```

- Schakel de Prowlarr-service in:

```shell
sudo systemctl enable --now -q prowlarr
```

- (Optioneel) Verwijder het tarball-bestand:

```shell
rm Prowlarr*.linux*.tar.gz
```

Meestal kun je de Prowlarr web-GUI openen door naar `http://{Het IP-adres van jouw server}:9696` te gaan.

Als Prowlarr niet lijkt te starten, controleer dan de status van de service:

```shell
sudo journalctl --since today -u prowlarr
```

---

### Deïnstallatie

Om te deïnstalleren en te verwijderen:
> Waarschuwing: Dit zal je applicatiedata vernietigen. {.is-danger}

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /var/lib/prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```

Om te deïnstalleren en je applicatiedata te behouden:

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```