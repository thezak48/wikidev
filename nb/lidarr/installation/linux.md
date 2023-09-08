---
title: Lidarr Linux-installasjon
description: Linux-installasjonsveiledning for Lidarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Merk: Raspberry Pi OS og Raspbian er begge varianter av Debian {.is-info}

> Lidarr v0.8 er ikke kompatibel eller støttet på Ubuntu 22.04 [Se denne FAQ-innføringen for detaljer](/lidarr/faq#lidarr-stopped-working-after-updating-to-ubuntu-2204)
{.is-warning}

### Enkel installasjon

For Debian / Ubuntu / Raspbian-nybegynnere finnes det ingen Apt Repository eller Deb-pakke.

Hvis du vil ha en enkel installasjon, kan du følge denne fellesskapsleverte og vedlikeholdte "Easy Install"-skriptet for en grunnleggende Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installasjon.

**For de offisielle installasjonsinstruksjonene som er "Hands on", følg [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install)-trinnene lenger ned.**

[Vennligst se \*Arr Community Installation Script](/install-script)

### Debian / Ubuntu Hands on Install

Du må installere binærene ved hjelp av følgende kommandoer.

> Trinnene nedenfor vil laste ned Lidarr og installere det i `/opt`
> Lidarr vil kjøre under brukeren `lidarr` og gruppen `media`
> Lidarrs konfigurasjonsfiler vil bli lagret i `/var/lib/lidarr`
{.is-warning}

- Sørg for at du har de nødvendige forutsetningspakkene:

```shell
sudo apt install curl mediainfo sqlite3 libchromaprint-tools
```

> Advarsel: Hvis du ignorerer de følgende forutsetningene, vil installasjonen mislykkes og applikasjonen vil ikke fungere. {.is-warning}

> **Installasjonsforutsetninger**
> Instruksjonene nedenfor er basert på følgende forutsetninger. Endre instruksjonene etter behov for å passe dine spesifikke behov hvis nødvendig.
> \* Brukeren `lidarr` er opprettet
> \* Brukeren `lidarr` er en del av gruppen `media`
> \* Nedlastingsklientene og medieserveren kjører som og er en del av gruppen `media`
> \* Stiene som brukes av nedlastingsklientene og medieserveren er tilgjengelige (lese/skrive) for gruppen `media`
> \* Du har opprettet mappen `/var/lib/lidarr` og sørget for at brukeren `lidarr` har lese-/skrivetilgang til den
{.is-danger}

> Ved å fortsette nedenfor, erkjenner du at du har lest og oppfylt de ovennevnte kravene. {.is-warning}

- Last ned riktig binærer for arkitekturen din.
  - Du kan finne ut arkitekturen din med `dpkg --print-architecture`
    - AMD64 bruker `arch=x64`
    - ARM, armf og armh bruker `arch=arm`
    - ARM64 bruker `arch=arm64`

```shell
wget --content-disposition 'http://lidarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Pakk ut filene:

```shell
tar -xvzf Lidarr*.linux*.tar.gz
```

- Flytt filene til `/opt/`

```shell
sudo mv Lidarr/ /opt
```

> Dette forutsetter at du har opprettet brukeren og vil kjøre som brukeren `lidarr` og gruppen `media`. Du kan endre dette for å passe ditt brukstilfelle. Det er viktig å velge disse riktig for å unngå tillatelsesproblemer med mediefilene dine. Vi anbefaler at du holder minst gruppenavnet identisk mellom nedlastingsklienten(e) dine og Lidarr.
{.is-danger}

- Sørg for eierskap av binærkatalogen.

```shell
sudo chown -R lidarr:media /opt/Lidarr
```

- Konfigurer systemd slik at Lidarr kan starte automatisk ved oppstart.

> Skriptet for opprettelse av systemd nedenfor vil bruke en datamappe på `/var/lib/lidarr`. Sørg for at den eksisterer eller endre den etter behov. For standard datamappe på `/home/$USER/.config/Lidarr`, fjern bare `-data`-argumentet. Merk at `$USER` er brukeren Lidarr kjører som og er definert nedenfor.
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

- Last inn systemd på nytt:

```shell
sudo systemctl -q daemon-reload
```

- Aktiver Lidarr-tjenesten:

```shell
sudo systemctl enable --now -q lidarr
```

- (Valgfritt) Fjern tarballen:

```shell
rm Lidarr*.linux*.tar.gz
```

Vanligvis kan du få tilgang til Lidarr-webgrensesnittet ved å gå til `http://{IP-adressen til serveren din}:8686`

Hvis Lidarr ikke ser ut til å starte, kan du sjekke statusen til tjenesten:

```shell
sudo journalctl --since today -u lidarr
```

---

### Avinstallasjon

For å avinstallere og fjerne:

> Advarsel: Dette vil ødelegge applikasjonsdataene dine. {.is-danger}

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /var/lib/lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```

For å avinstallere og beholde applikasjonsdataene dine:

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```