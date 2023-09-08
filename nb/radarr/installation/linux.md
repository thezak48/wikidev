---
title: Radarr Linux-installasjon
description: Linux-installasjonsveiledning for Radarr
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

For Debian / Ubuntu / Raspbian-nybegynnere finnes det ingen Apt Repository eller Deb-pakke.

Hvis du vil ha en enkel installasjon, kan du følge denne fellesskapsleverte og vedlikeholdte "Easy Install"-skriptet for en grunnleggende Debian (Raspbian / Raspberry Pi OS) / Ubuntu-installasjon.

**For de offisielle installasjonsinstruksjonene som er "Hands on", følg [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install)-trinnene lenger ned.**

[Vennligst se \*Arr Community Installation Script](/install-script)

> Radarr bruker en buntet versjon av ffprobe for analyse av mediefiler og krever ikke at ffprobe eller ffmpeg er installert på systemet. Hvis Radarr sier at Ffprobe ikke er funnet, kan dette vanligvis løses med en reinstallasjon.
{.is-info}

### Debian / Ubuntu Hands on Install

Du må installere binærene ved hjelp av følgende kommandoer.

> Trinnene nedenfor vil laste ned Radarr og installere det i `/opt`
> Radarr vil kjøre under brukeren `radarr` og gruppen `media`; `media` er den vanlig anbefalte gruppen å kjøre \*Arrs, nedlastingsklienter og medieserver under.
> Radarrs konfigurasjonsfiler vil bli lagret i `/var/lib/radarr`
{.is-success}

- Sørg for at du har de nødvendige forutsetningspakkene:

```shell
sudo apt install curl sqlite3
```

> Advarsel: Hvis du ignorerer de følgende forutsetningene, vil det resultere i en mislykket installasjon og en ikke-fungerende applikasjon. {.is-warning}

> **Installasjonsforutsetninger**
> Instruksjonene nedenfor er basert på følgende forutsetninger. Endre instruksjonene etter behov for å tilpasse dine spesifikke behov hvis nødvendig.
> \* Brukeren `radarr` er opprettet
> \* Brukeren `radarr` er en del av gruppen `media`
> \* Nedlastingsklientene og medieserveren kjører som og er en del av gruppen `media`
> \* Stiene som brukes av nedlastingsklientene og medieserveren er tilgjengelige (lese/skrive) for gruppen `media`
> \* Du har opprettet mappen `/var/lib/radarr` og sikret at brukeren `radarr` har lese-/skrivetilgang til den
{.is-danger}

> Ved å fortsette nedenfor, erkjenner du at du har lest og oppfylt de ovennevnte kravene. {.is-success}

- Last ned riktige binærer for arkitekturen din.
  - Du kan finne ut arkitekturen din med `dpkg --print-architecture`
    - AMD64 bruk `arch=x64`
    - ARM, armf og armh bruk `arch=arm`
    - ARM64 bruk `arch=arm64`

```shell
wget --content-disposition 'http://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Pakk ut filene:

```shell
tar -xvzf Radarr*.linux*.tar.gz
```

- Flytt filene til `/opt/`

```shell
sudo mv Radarr /opt/
```

> Merk: Dette antar at du vil kjøre som brukeren `radarr` og gruppen `media`. Du kan endre dette for å passe til ditt brukstilfelle. Det er viktig å velge disse riktig for å unngå tillatelsesproblemer med mediefilene dine. Vi anbefaler at du holder minst gruppenavnet identisk mellom nedlastingsklienten(e) dine og Radarr.
{.is-danger}

- Sørg for eierskapet til binærkatalogen.

```shell  
sudo chown radarr:radarr -R /opt/Radarr
```

- Konfigurer systemd slik at Radarr kan starte automatisk ved oppstart.

> Nedenstående systemd-opprettingsskript vil bruke en datamappe på `/var/lib/radarr`. Sørg for at den eksisterer eller endre den etter behov. For standard datamappe på `/home/$USER/.config/Radarr`, fjern bare `-data`-argumentet. Merk at `$USER` er brukeren Radarr kjører som og er definert nedenfor.
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

- Last inn systemd på nytt:

```shell
sudo systemctl -q daemon-reload
```

- Aktiver Radarr-tjenesten:

```shell
sudo systemctl enable --now -q radarr
```

- (Valgfritt) Fjern tarballen:

```shell
rm Radarr*.linux*.tar.gz
```

Vanligvis kan du få tilgang til Radarr web-GUI ved å gå til `http://{IP-adressen til serveren din}:7878`

> Radarr bruker en buntet versjon av ffprobe for analyse av mediefiler og krever ikke at ffprobe eller ffmpeg er installert på systemet. Hvis Radarr sier at Ffprobe ikke er funnet, kan dette vanligvis løses med en reinstallasjon.
{.is-info}

Hvis Radarr ikke ser ut til å starte, kan du sjekke statusen til tjenesten:

```shell
sudo journalctl --since today -u radarr
```

---

### Avinstallasjon

For å avinstallere og fjerne fullstendig:
> Advarsel: Dette vil ødelegge applikasjonsdataene dine. {.is-danger}

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /var/lib/radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```

For å avinstallere og beholde applikasjonsdataene dine:

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```