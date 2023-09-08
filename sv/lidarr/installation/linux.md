---
title: Lidarr Linux Installation
description: Linux installationsguide för Lidarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Notera: Raspberry Pi OS och Raspbian är båda varianter av Debian {.is-info}

> Lidarr v0.8 är inte kompatibel eller stöds på Ubuntu 22.04 [Se denna FAQ-post för detaljer](/lidarr/faq#lidarr-stopped-working-after-updating-to-ubuntu-2204)
{.is-warning}

### Enkel installation

För Debian / Ubuntu / Raspbian-nybörjare finns det ingen Apt Repository eller Deb-paket.

Om du vill ha en enkel installation, följ denna gemenskapens tillhandahållna och underhållna `Easy Install`-skript för en grundläggande Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installation.

**För officiella installationsinstruktioner som är 'Hands on', följ stegen för [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) längre ner.**

[Se det \*Arr Community Installation Script](/install-script)

### Debian / Ubuntu Hands on Install

Du måste installera binärerna med följande kommandon.

> Stegen nedan kommer att ladda ner Lidarr och installera det i `/opt`
> Lidarr kommer att köras under användaren `lidarr` och gruppen `media`
> Lidarrs konfigurationsfiler kommer att lagras i `/var/lib/lidarr`
{.is-warning}

- Se till att du har de nödvändiga förutsättningspaketerna:

```shell
sudo apt install curl mediainfo sqlite3 libchromaprint-tools
```

> Varning: Att ignorera följande förutsättningar kommer att resultera i en misslyckad installation och en icke-fungerande applikation. {.is-warning}

> **Installationsförutsättningar**
> Följande instruktioner är baserade på följande förutsättningar. Ändra instruktionerna vid behov för att passa dina specifika behov om det behövs.
> \* Användaren `lidarr` är skapad
> \* Användaren `lidarr` är en del av gruppen `media`
> \* Dina nedladdningsklienter och mediaserver körs som och är en del av gruppen `media`
> \* Dina sökvägar som används av dina nedladdningsklienter och mediaserver är åtkomliga (läs/skriv) för gruppen `media`
> \* Du har skapat katalogen `/var/lib/lidarr` och säkerställt att användaren `lidarr` har läs- och skrivrättigheter för den
{.is-danger}

> Genom att fortsätta nedan bekräftar du att du har läst och uppfyllt ovanstående krav. {.is-warning}

- Ladda ner rätt binärer för din arkitektur.
  - Du kan ta reda på din arkitektur med `dpkg --print-architecture`
    - AMD64 använd `arch=x64`
    - ARM, armf och armh använd `arch=arm`
    - ARM64 använd `arch=arm64`

```shell
wget --content-disposition 'http://lidarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Packa upp filerna:

```shell
tar -xvzf Lidarr*.linux*.tar.gz
```

- Flytta filerna till `/opt/`

```shell
sudo mv Lidarr/ /opt
```

> Detta antar att du har skapat användaren och kommer att köra som användaren `lidarr` och gruppen `media`. Du kan ändra detta för att passa ditt användningsfall. Det är viktigt att välja dessa korrekt för att undvika behörighetsproblem med dina mediefiler. Vi föreslår att du håller minst gruppnamnet identiskt mellan dina nedladdningsklient(er) och Lidarr.
{.is-danger}

- Säkerställ ägandeskapet för binärkatalogen.

```shell
sudo chown -R lidarr:media /opt/Lidarr
```

- Konfigurera systemd så att Lidarr kan startas automatiskt vid uppstart.

> Skapningsskriptet för systemd nedan kommer att använda en datakatalog på `/var/lib/lidarr`. Se till att den finns eller ändra den vid behov. För standarddatakatalogen `/home/$USER/.config/Lidarr`, ta helt enkelt bort argumentet `-data`. Observera att `$USER` är användaren som Lidarr körs som och definieras nedan.
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

- Ladda om systemd:

```shell
sudo systemctl -q daemon-reload
```

- Aktivera Lidarr-tjänsten:

```shell
sudo systemctl enable --now -q lidarr
```

- (Valfritt) Ta bort tarbollen:

```shell
rm Lidarr*.linux*.tar.gz
```

Vanligtvis för att komma åt Lidarr webbgränssnitt, bläddra till `http://{Din server IP-adress}:8686`

Om Lidarr inte verkar ha startat, kontrollera då statusen för tjänsten:

```shell
sudo journalctl --since today -u lidarr
```

---

### Avinstallation

För att avinstallera och rensa bort:
> Varning: Detta kommer att förstöra dina applikationsdata. {.is-danger}

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /var/lib/lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```

För att avinstallera och behålla dina applikationsdata:

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```