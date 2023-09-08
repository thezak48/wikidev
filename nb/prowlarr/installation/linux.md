---
title: Prowlarr Linux-installasjon
description: Linux-installasjonsveiledning for Prowlarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Merk: Raspberry Pi OS og Raspbian er begge varianter av Debian {.is-info}

### Enkel installasjon

For Debian / Ubuntu / Raspbian nybegynnere finnes det ingen Apt Repository eller Deb-pakke.

Hvis du vil ha en enkel installasjon, kan du følge denne fellesskapets tilgjengeliggjorte og vedlikeholdte "Enkel installasjon"-skriptet for en grunnleggende Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installasjon.

**For de offisielle installasjonsinstruksjonene som er "Hands on", følg [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install)-trinnene lenger ned.**

[Vennligst se \*Arr Community Installation Script](/install-script)

### Debian / Ubuntu Hands on Install

Du må installere binærene ved hjelp av følgende kommandoer.

> Trinnene nedenfor vil laste ned Prowlarr og installere det i `/opt`
> Prowlarr vil kjøre under brukeren `prowlarr` og gruppen `prowlarr`
> Prowlarrs konfigurasjonsfiler vil bli lagret i `/var/lib/prowlarr`
{.is-warning}

- Sørg for at du har de nødvendige forutsetningspakkene:

```shell
sudo apt install curl sqlite3
```

> Advarsel: Hvis du ignorerer de følgende forutsetningene, vil det resultere i en mislykket installasjon og en ikke-fungerende applikasjon. {.is-warning}

> **Installasjonsforutsetninger**
> Instruksjonene nedenfor er basert på følgende forutsetninger. Endre instruksjonene etter behov for å tilpasse dine spesifikke behov hvis nødvendig.
> \* Brukeren `prowlarr` er opprettet
> \* Du har opprettet mappen `/var/lib/prowlarr` og sørget for at brukeren `prowlarr` har lese-/skrivetilgang til den
{.is-danger}

> Ved å fortsette nedenfor, erkjenner du at du har lest og oppfylt de ovennevnte kravene. {.is-warning}

- Last ned riktig binærer for arkitekturen din.
  - Du kan finne ut arkitekturen din med `dpkg --print-architecture`
    - AMD64 bruk `arch=x64`
    - ARM, armf og armh bruk `arch=arm`
    - ARM64 bruk `arch=arm64`

```shell
wget --content-disposition 'http://prowlarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Pakk ut filene:

```shell
tar -xvzf Prowlarr*.linux*.tar.gz
```

- Flytt filene til `/opt/`

```shell
sudo mv Prowlarr/ /opt
```

> Dette forutsetter at du har opprettet brukeren og vil kjøre som brukeren `prowlarr` og gruppen `prowlarr`. Du kan endre dette for å passe til ditt brukstilfelle.
{.is-danger}

- Sørg for eierskap av binærkatalogen.

```shell  
sudo chown prowlarr:prowlarr -R /opt/Prowlarr
```

- Konfigurer systemd slik at Prowlarr kan starte automatisk ved oppstart.

> Nedenstående systemd-opprettingsskript vil bruke en datamappe på `/var/lib/prowlarr`. Sørg for at den eksisterer eller endre den etter behov. For standard datamappe på `/home/$USER/.config/Prowlarr`, fjern bare `-data`-argumentet. Merk at `$USER` er brukeren Prowlarr kjører som og er definert nedenfor.
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

- Last inn systemd på nytt:

```shell
sudo systemctl -q daemon-reload
```

- Aktiver Prowlarr-tjenesten:

```shell
sudo systemctl enable --now -q prowlarr
```

- (Valgfritt) Fjern tarballen:

```shell
rm Prowlarr*.linux*.tar.gz
```

Vanligvis for å få tilgang til Prowlarr web-GUI, gå til `http://{IP-adressen til serveren din}:9696`

Hvis Prowlarr ikke ser ut til å starte, kan du sjekke statusen til tjenesten:

```shell
sudo journalctl --since today -u prowlarr
```

---

### Avinstallasjon

For å avinstallere og fjerne fullstendig:
> Advarsel: Dette vil ødelegge applikasjonsdataene dine. {.is-danger}

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /var/lib/prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```

For å avinstallere og beholde applikasjonsdataene dine:

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```