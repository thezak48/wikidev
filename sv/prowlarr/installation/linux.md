---
title: Prowlarr Linux Installation
description: Linux installationsguide för Prowlarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Observera: Raspberry Pi OS och Raspbian är båda varianter av Debian {.is-info}

### Enkel installation

För Debian / Ubuntu / Raspbian-nybörjare finns det ingen Apt Repository eller Deb-paket.

Om du vill ha en enkel installation, följ denna gemenskapens tillhandahållna och underhållna `Easy Install`-skript för en grundläggande Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installation.

**För officiella installationsinstruktioner som är "Hands on", följ stegen för [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) längre ner.**

[Se gärna \*Arr Community Installation Script](/install-script)

### Debian / Ubuntu Hands on Install

Du behöver installera binärerna med följande kommandon.

> Nedanstående steg kommer att ladda ner Prowlarr och installera det i `/opt`
> Prowlarr kommer att köras under användaren `prowlarr` och gruppen `prowlarr`
> Prowlarrs konfigurationsfiler kommer att lagras i `/var/lib/prowlarr`
{.is-warning}

- Se till att du har de nödvändiga förutsättningspaketerna:

```shell
sudo apt install curl sqlite3
```

> Varning: Om du ignorerar nedanstående förutsättningar kommer installationen att misslyckas och programmet kommer inte att fungera. {.is-warning}

> **Installationens förutsättningar**
> Nedanstående instruktioner är baserade på följande förutsättningar. Ändra instruktionerna vid behov för att passa dina specifika behov.
> \* Användaren `prowlarr` är skapad
> \* Du har skapat katalogen `/var/lib/prowlarr` och säkerställt att användaren `prowlarr` har läs- och skrivrättigheter för den
{.is-danger}

> Genom att fortsätta nedan bekräftar du att du har läst och uppfyllt ovanstående krav. {.is-warning}

- Ladda ner rätt binärer för din arkitektur.
  - Du kan ta reda på din arkitektur med `dpkg --print-architecture`
    - AMD64 använd `arch=x64`
    - ARM, armf och armh använd `arch=arm`
    - ARM64 använd `arch=arm64`

```shell
wget --content-disposition 'http://prowlarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Packa upp filerna:

```shell
tar -xvzf Prowlarr*.linux*.tar.gz
```

- Flytta filerna till `/opt/`

```shell
sudo mv Prowlarr/ /opt
```

> Detta antar att du har skapat användaren och kommer att köra som användaren `prowlarr` och gruppen `prowlarr`. Du kan ändra detta för att passa ditt användningsfall.
{.is-danger}

- Säkerställ ägandeskap för binärkatalogen.

```shell  
sudo chown prowlarr:prowlarr -R /opt/Prowlarr
```

- Konfigurera systemd så att Prowlarr kan starta automatiskt vid uppstart.

> Nedanstående systemd-skript kommer att använda en datakatalog på `/var/lib/prowlarr`. Se till att den finns eller ändra den vid behov. För standarddatakatalogen `/home/$USER/.config/Prowlarr`, ta helt enkelt bort argumentet `-data`. Observera att `$USER` är användaren som Prowlarr körs som och definieras nedan.
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

- Ladda om systemd:

```shell
sudo systemctl -q daemon-reload
```

- Aktivera Prowlarr-tjänsten:

```shell
sudo systemctl enable --now -q prowlarr
```

- (Valfritt) Ta bort tarbollen:

```shell
rm Prowlarr*.linux*.tar.gz
```

Vanligtvis för att komma åt Prowlarr webbgränssnitt, bläddra till `http://{Din server IP-adress}:9696`

Om Prowlarr inte verkar ha startat, kontrollera då statusen för tjänsten:

```shell
sudo journalctl --since today -u prowlarr
```

---

### Avinstallation

För att avinstallera och rensa:

> Varning: Detta kommer att förstöra dina applikationsdata. {.is-danger}

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /var/lib/prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```

För att avinstallera och behålla dina applikationsdata:

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```