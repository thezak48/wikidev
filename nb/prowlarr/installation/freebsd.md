---
title: Prowlarr FreeBSD-installasjon
description: Installasjonsguide for Prowlarr på FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Prowlarr-teamet tilbyr bare bygg for FreeBSD. Utvidelser og porter vedlikeholdes og opprettes av FreeBSD-samfunnet.

Instruksjoner for FreeBSD-installasjoner vedlikeholdes også av FreeBSD-samfunnet, og alle med en GitHub-konto kan oppdatere wikien etter behov.

[Freshports Prowlarr-lenke](https://www.freshports.org/net-p2p/prowlarr/)

## Oppsett av jail ved hjelp av TrueNAS GUI

1. Fra hovedskjermen velger du Jails.

1. Klikk på LEGG TIL.

1. Klikk på Avansert opprettelse av jail.

1. Navn (hvilket som helst navn fungerer): Prowlarr.

1. Jail-type: Standard (klon-jail).

1. Utgivelse: 12.2-Release (eller nyere).

1. Konfigurer grunnleggende egenskaper etter ønske.

1. Konfigurer jail-egenskaper etter ønske, men legg til

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` er nyttig for feilsøking (f.eks. ping, traceroute), men er ikke et krav. {.is-info}

1. Konfigurer nettverksegenskaper etter ønske.

1. Konfigurer egendefinerte egenskaper etter ønske.

1. Klikk på Lagre.

## Prowlarr-installasjon

Gå tilbake til listen over jails og finn den nyopprettede jailen for `prowlarr`, og klikk på "Shell".

For å installere Prowlarr

> \* Sørg for at pkg-repoet ditt er konfigurert for å hente pakker fra `/latest` og ikke `/quarterly`
> \* Sjekk `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Hvis det ikke finnes, kopier `/etc/pkg/FreeBSD.conf` til den plasseringen, åpne den, og erstatt `quarterly` med `latest`
{.is-warning}

```shell
pkg install prowlarr
```

Ikke lukk ut skallet ennå, vi har fortsatt noen flere ting å gjøre!

## Konfigurere Prowlarr

Nå som vi har installert det, kreves det noen flere trinn.

### Oppsett av tjeneste

Det er på tide å aktivere tjenesten, men før vi gjør det, en merknad:

Oppdateringen er deaktivert som standard. `pkg-message` gir instruksjoner om hvordan du aktiverer oppdateringen, men husk: dette kan ødelegge ting som `pkg check -s` og `pkg remove` for prowlarr når den innebygde oppdateringen erstatter filer.

For å aktivere tjenesten:

```shell
sysrc prowlarr_enable=TRUE
```

Hvis du ikke vil bruke bruker/gruppe `prowlarr`, må du fortelle tjenestefilen hvilken bruker/gruppe den skal kjøre under

```shell
sysrc prowlarr_user="BRUKER_DU_VIL_BRUKE"
```

```shell
sysrc prowlarr_group="GRUPPE_DU_VIL_BRUKE"
```

`prowlarr` lagrer data, konfigurasjon, logger og PID-filer i `/usr/local/prowlarr` som standard. Tjenestefilen vil opprette dette og ta eierskap av det HVIS OG BARE HVIS DET IKKE FINNES. Hvis du vil lagre disse filene på et annet sted (f.eks. et datasett montert i jailen for enklere øyeblikksbilder), må du endre det ved hjelp av `sysrc`

```shell
sysrc prowlarr_data_dir="STI_DU_VIL_BRUKE"
```

Påminnelse: Hvis du bruker en eksisterende plassering, må du manuelt enten: endre eierskapet til UID/GID som `prowlarr` bruker OG/ELLER legge til `prowlarr` i en GID som har skrivetilgang.

Nesten ferdig, la oss starte tjenesten:

```shell
service prowlarr start
```

Hvis alt gikk som planlagt, skal prowlarr være oppe og kjøre på IP-adressen til jailen (port 9696)!

Du kan nå trygt lukke skallet.

## Feilsøking

- Tjenesten ser ut til å kjøre, men brukergrensesnittet lastes ikke inn eller siden tar for lang tid å laste
  - Sjekk at `allow_mlock` er aktivert i jailen.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Sørg for at du har `VNET` slått på for jailen din, ip6=inherit eller ip6=new

> Tjenesteskriptet skal nå fungere uten VNET og/eller IP6, og dermed fjerne kravet om VNET eller ip6=inherit. {.is-info}