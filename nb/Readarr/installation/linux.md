---
title: Readarr Linux-installasjon
description: Linux-installasjonsveiledning for Readarr
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

Hvis du vil ha en enkel installasjon, kan du følge denne fellesskapets tilgjengeliggjorte og vedlikeholdte `Enkel installasjon`-skriptet for en grunnleggende Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installasjon.

**For de offisielle installasjonsinstruksjonene som er "Hands on", følg [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install)-trinnene lenger ned.**

[Vennligst se \*Arr Community Installation Script](/install-script)

### Debian / Ubuntu Hands on Install

Du må installere binærene ved hjelp av følgende kommandoer.

> Trinnene nedenfor vil laste ned Readarr og installere det i `/opt`
> Readarr vil kjøre under brukeren `readarr` og gruppen `media`; `media` er den vanlig anbefalte gruppen å kjøre \*Arrs, nedlastingsklienter og medieserver under.
> Readarrs konfigurasjonsfiler vil bli lagret i `/var/lib/readarr`
{.is-warning}

- Sørg for at du har de nødvendige forutsetningspakkene:

```shell
sudo apt install curl sqlite3
```

> Advarsel: Hvis du ignorerer de følgende forutsetningene, vil det resultere i en mislykket installasjon og en ikke-fungerende applikasjon. {.is-warning}

> **Installasjonsforutsetninger**
> Instruksjonene nedenfor er basert på følgende forutsetninger. Endre instruksjonene etter behov for å tilpasse dine spesifikke behov hvis nødvendig.
> \* Brukeren `readarr` er opprettet
> \* Brukeren `readarr` er en del av gruppen `media`
> \* Nedlastingsklientene og medieserveren kjører som og er en del av gruppen `media`
> \* Stiene som brukes av nedlastingsklientene og medieserveren er tilgjengelige (lese/skrive) for gruppen `media`
> \* Hvis Calibre skal brukes, kjører Calibre som gruppen `media` og Calibre-biblioteket har lese-/skrivetilgang for `media`
> \* Du har opprettet mappen `/var/lib/readarr` og sørget for at brukeren `readarr` har lese-/skrivetilgang til den
{.is-danger}

> Ved å fortsette nedenfor, erkjenner du at du har lest og oppfylt de ovennevnte kravene. {.is-warning}

- Last ned riktige binærer for arkitekturen din.
  - Du kan finne ut arkitekturen din med `dpkg --print-architecture`
    - AMD64 bruk `arch=x64`
    - ARM, armf og armh bruk `arch=arm`
    - ARM64 bruk `arch=arm64`

```shell
wget --content-disposition 'http://readarr.servarr.com/v1/update/develop/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Pakk ut filene:

```shell
tar -xvzf Readarr*.linux*.tar.gz
```

- Flytt filene til `/opt/`

```shell
sudo mv Readarr /opt/
```

> Merk: Dette antar at du har opprettet brukeren og vil kjøre som brukeren `readarr` og gruppen `media`. Du kan endre dette for å passe ditt brukstilfelle. Det er viktig å velge disse riktig for å unngå tillatelsesproblemer med mediefilene dine. Vi anbefaler at du holder minst gruppenavnet identisk mellom nedlastingsklienten(e) dine og Readarr. Vær oppmerksom på at hvis du ønsker å bruke Calibre, vil Readarr trenge tillatelser for den mappen.
{.is-danger}

- Sørg for eierskap av binærkatalogen.

```shell  
sudo chown readarr:readarr -R /opt/Readarr
```

- Konfigurer systemd slik at Readarr kan starte automatisk ved oppstart.

> Nedenstående systemd-opprettingsskript vil bruke en datamappe på `/var/lib/readarr`. Sørg for at den eksisterer eller endre den etter behov. For standard datamappe på `/home/$USER/.config/Readarr`, fjern bare `-data`-argumentet. Merk at `$USER` er brukeren Readarr kjører som og er definert nedenfor.
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

- Last inn systemd på nytt:

```shell
sudo systemctl -q daemon-reload
```

- Aktiver Readarr-tjenesten:

```shell
sudo systemctl enable --now -q readarr
```

- (Valgfritt) Fjern tarballen:

```shell
rm Readarr*.linux*.tar.gz
```

Vanligvis for å få tilgang til Readarr web-GUI, gå til `http://{IP-adressen til serveren din}:8787`

Hvis Readarr ikke ser ut til å starte, kan du sjekke statusen til tjenesten:

```shell
sudo journalctl --since today -u readarr
```

---

### Avinstallasjon

For å avinstallere og fjerne fullstendig:
> Advarsel: Dette vil ødelegge applikasjonsdataene dine. {.is-danger}

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /var/lib/readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```

For å avinstallere og beholde applikasjonsdataene dine:

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```