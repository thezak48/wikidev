---
title: Readarr Linux Installation
description: Linux installationsguide för Readarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Notera: Raspberry Pi OS och Raspbian är båda varianter av Debian {.is-info}

### Enkel installation

För Debian / Ubuntu / Raspbian-nybörjare finns det ingen Apt Repository eller Deb-paket.

Om du vill ha en enkel installation, följ denna gemenskapsgivna och underhållna `Enkel installation`-skript för en grundläggande Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installation.

**För officiella installationsinstruktioner som är 'Hands on', följ stegen för [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) längre ner.**

[Se gärna \*Arr Community Installation Script](/install-script)

### Debian / Ubuntu Hands on Install

Du behöver installera binärerna med hjälp av följande kommandon.

> Nedanstående steg kommer att ladda ner Readarr och installera det i `/opt`
> Readarr kommer att köras under användaren `readarr` och gruppen `media`; `media` är den vanligt föreslagna gruppen att köra \*Arrs, nedladdningsklienter och mediaserver under.
> Readarrs konfigurationsfiler kommer att sparas i `/var/lib/readarr`
{.is-warning}

- Se till att du har de nödvändiga förutsättningspaketerna:

```shell
sudo apt install curl sqlite3
```

> Varning: Om du ignorerar de nedanstående förutsättningarna kommer installationen att misslyckas och programmet kommer inte att fungera. {.is-warning}

> **Installationens förutsättningar**
> Nedanstående instruktioner är baserade på följande förutsättningar. Ändra instruktionerna vid behov för att passa dina specifika behov.
> \* Användaren `readarr` är skapad
> \* Användaren `readarr` tillhör gruppen `media`
> \* Dina nedladdningsklienter och mediaserver körs som och tillhör gruppen `media`
> \* Dina sökvägar som används av dina nedladdningsklienter och mediaserver är åtkomliga (läs/skriv) för gruppen `media`
> \* Om Calibre kommer att användas, körs Calibre som gruppen `media` och Calibre-biblioteket har läs/skrivrättigheter för `media`
> \* Du har skapat katalogen `/var/lib/readarr` och säkerställt att användaren `readarr` har läs/skrivrättigheter för den
{.is-danger}

> Genom att fortsätta nedan bekräftar du att du har läst och uppfyllt ovanstående krav. {.is-warning}

- Ladda ner rätt binärer för din arkitektur.
  - Du kan bestämma din arkitektur med `dpkg --print-architecture`
    - AMD64 använd `arch=x64`
    - ARM, armf och armh använd `arch=arm`
    - ARM64 använd `arch=arm64`

```shell
wget --content-disposition 'http://readarr.servarr.com/v1/update/develop/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Packa upp filerna:

```shell
tar -xvzf Readarr*.linux*.tar.gz
```

- Flytta filerna till `/opt/`

```shell
sudo mv Readarr /opt/
```

> Notera: Detta antar att du har skapat användaren och kommer att köra som användaren `readarr` och gruppen `media`. Du kan ändra detta för att passa ditt användningsområde. Det är viktigt att välja dessa korrekt för att undvika behörighetsproblem med dina mediefiler. Vi föreslår att du håller minst gruppnamnet identiskt mellan dina nedladdningsklient(er) och Readarr. Observera att om du vill använda Calibre - Readarr kommer att behöva behörighet för den katalogen.
{.is-danger}

- Säkerställ ägandeskapet för binärkatalogen.

```shell  
sudo chown readarr:readarr -R /opt/Readarr
```

- Konfigurera systemd så att Readarr kan starta automatiskt vid uppstart.

> Nedanstående systemd-skript kommer att använda en datakatalog på `/var/lib/readarr`. Se till att den finns eller ändra den vid behov. För standarddatakatalogen `/home/$USER/.config/Readarr` kan du helt enkelt ta bort argumentet `-data`. Observera att `$USER` är användaren som Readarr körs som och som definieras nedan.
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

- Ladda om systemd:

```shell
sudo systemctl -q daemon-reload
```

- Aktivera Readarr-tjänsten:

```shell
sudo systemctl enable --now -q readarr
```

- (Valfritt) Ta bort tarbollen:

```shell
rm Readarr*.linux*.tar.gz
```

Vanligtvis för att komma åt Readarr webbgränssnittet, bläddra till `http://{Din server IP-adress}:8787`

Om Readarr inte verkar ha startat, kontrollera då statusen för tjänsten:

```shell
sudo journalctl --since today -u readarr
```

---

### Avinstallation

För att avinstallera och rensa bort:
> Varning: Detta kommer att förstöra dina applikationsdata. {.is-danger}

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /var/lib/readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```

För att avinstallera och behålla dina applikationsdata:

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```