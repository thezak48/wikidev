---
title: Radarr Linux Installation
description: Linux installationsguide för Radarr
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

Om du vill ha ett enkelt liv, följ denna gemenskapens tillhandahållna och underhållna `Easy Install`-skript för en grundläggande Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installation.

**För officiella installationsinstruktioner som är "Hands on", följ stegen för [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) längre ner.**

[Se \*Arr Community Installation Script](/install-script)

> Radarr använder en buntad version av ffprobe för analys av mediefiler och kräver inte att ffprobe eller ffmpeg är installerade på systemet. Om Radarr säger att Ffprobe inte hittas kan detta vanligtvis åtgärdas genom en ominstallation.
{.is-info}

### Debian / Ubuntu Hands on Install

Du måste installera binärerna med följande kommandon.

> Nedanstående steg kommer att ladda ner Radarr och installera det i `/opt`
> Radarr kommer att köras under användaren `radarr` och gruppen `media`; `media` är den vanligt föreslagna gruppen att köra \*Arrs, nedladdningsklienter och mediaserver under.
> Radarrs konfigurationsfiler kommer att lagras i `/var/lib/radarr`
{.is-success}

- Se till att du har de nödvändiga förutsättningspaketerna:

```shell
sudo apt install curl sqlite3
```

> Varning: Om du ignorerar följande förutsättningar kommer installationen att misslyckas och programmet kommer inte att fungera. {.is-warning}

> **Installationsförutsättningar**
> Nedanstående instruktioner är baserade på följande förutsättningar. Ändra instruktionerna vid behov för att passa dina specifika behov.
> \* Användaren `radarr` är skapad
> \* Användaren `radarr` tillhör gruppen `media`
> \* Dina nedladdningsklienter och mediaserver körs som och tillhör gruppen `media`
> \* Dina sökvägar som används av dina nedladdningsklienter och mediaserver är åtkomliga (läs/skriv) för gruppen `media`
> \* Du har skapat katalogen `/var/lib/radarr` och säkerställt att användaren `radarr` har läs-/skrivrättigheter för den
{.is-danger}

> Genom att fortsätta nedan bekräftar du att du har läst och uppfyllt ovanstående krav. {.is-success}

- Ladda ner rätt binärer för din arkitektur.
  - Du kan ta reda på din arkitektur med `dpkg --print-architecture`
    - AMD64 använd `arch=x64`
    - ARM, armf och armh använd `arch=arm`
    - ARM64 använd `arch=arm64`

```shell
wget --content-disposition 'http://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Packa upp filerna:

```shell
tar -xvzf Radarr*.linux*.tar.gz
```

- Flytta filerna till `/opt/`

```shell
sudo mv Radarr /opt/
```

> Observera: Detta antar att du kommer att köra som användaren `radarr` och gruppen `media`. Du kan ändra detta för att passa ditt användningsområde. Det är viktigt att välja dessa korrekt för att undvika behörighetsproblem med dina mediefiler. Vi föreslår att du åtminstone håller gruppnamnet identiskt mellan dina nedladdningsklient(er) och Radarr.
{.is-danger}

- Säkerställ ägande av binärkatalogen.

```shell  
sudo chown radarr:radarr -R /opt/Radarr
```

- Konfigurera systemd så att Radarr kan startas automatiskt vid uppstart.

> Nedanstående systemd-skript kommer att använda en datakatalog på `/var/lib/radarr`. Se till att den finns eller ändra den vid behov. För standarddatakatalogen `/home/$USER/.config/Radarr` tar du helt enkelt bort argumentet `-data`. Observera att `$USER` är användaren som Radarr körs som och som definieras nedan.
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

- Ladda om systemd:

```shell
sudo systemctl -q daemon-reload
```

- Aktivera Radarr-tjänsten:

```shell
sudo systemctl enable --now -q radarr
```

- (Valfritt) Ta bort tarbollen:

```shell
rm Radarr*.linux*.tar.gz
```

Vanligtvis för att komma åt Radarr webbgränssnitt, bläddra till `http://{Din server IP-adress}:7878`

> Radarr använder en buntad version av ffprobe för analys av mediefiler och kräver inte att ffprobe eller ffmpeg är installerade på systemet. Om Radarr säger att Ffprobe inte hittas kan detta vanligtvis åtgärdas genom en ominstallation.
{.is-info}

Om Radarr inte verkar ha startat, kontrollera då statusen för tjänsten:

```shell
sudo journalctl --since today -u radarr
```

---

### Avinstallation

För att avinstallera och rensa:

> Varning: Detta kommer att förstöra dina applikationsdata. {.is-danger}

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /var/lib/radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```

För att avinstallera och behålla dina applikationsdata:

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```