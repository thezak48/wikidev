---
title: Readarr FreeBSD-installasjon
description: Installasjonsguide for Readarr på FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Readarr-teamet tilbyr bare bygg for FreeBSD. Utvidelser og porter vedlikeholdes og opprettes av FreeBSD-samfunnet.

Instruksjoner for FreeBSD-installasjoner vedlikeholdes også av FreeBSD-samfunnet, og alle med en GitHub-konto kan oppdatere wikien etter behov.

[Freshports Readarr Link](https://www.freshports.org/net-p2p/readarr/)

## Oppsett av jail ved hjelp av TrueNAS GUI

1. Fra hovedskjermen velger du Jails.

1. Klikk på ADD.

1. Klikk på Advanced Jail Creation.

1. Navn (hvilket som helst navn fungerer): Readarr.

1. Jail Type: Default (Clone Jail).

1. Release: 12.2-Release (eller nyere).

1. Konfigurer Basic Properties etter ønske.

1. Konfigurer Jail Properties etter ønske, men legg til

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` er nyttig for feilsøking (f.eks. ping, traceroute), men er ikke et krav. {.is-info}

1. Konfigurer Network Properties etter ønske.

1. Konfigurer Custom Properties etter ønske.

1. Klikk på Save.

1. Etter at jailen er opprettet, starter den automatisk. En tilleggsinnstilling må settes for at Readarr skal kunne se lagringsplassen til de monterte medielokasjonene dine. Åpne en rotshell på serveren og skriv inn disse kommandoene:

```shell
iocage stop <jailnavn>
iocage set enforce_statfs=1 <jailnavn>
iocage start <jailnavn>
```

## Readarr-installasjon

Gå tilbake til listen over jails og finn jailen du nettopp opprettet for `readarr`. Klikk på "Shell".

For å installere Readarr

> \* Sørg for at pkg-repoet ditt er konfigurert til å hente pakker fra `/latest` og ikke `/quarterly`
> \* Sjekk `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Hvis den ikke eksisterer, kopier `/etc/pkg/FreeBSD.conf` til den plasseringen, åpne den og erstatt `quarterly` med `latest`
{.is-warning}

```shell
pkg install readarr
```

Ikke lukk shellen ennå, vi har fortsatt noen flere ting å gjøre!

## Konfigurering av Readarr

Nå som vi har installert det, kreves det noen flere trinn.

### Oppsett av tjeneste

Det er på tide å aktivere tjenesten, men før vi gjør det, en merknad:

Oppdateringen er deaktivert som standard. `pkg-message` gir instruksjoner om hvordan du aktiverer oppdateringen, men husk: dette kan ødelegge ting som `pkg check -s` og `pkg remove` for Readarr når den innebygde oppdateringen erstatter filer.

For å aktivere tjenesten:

```shell
sysrc readarr_enable=TRUE
```

Hvis du ikke vil bruke bruker/gruppe `readarr`, må du fortelle tjenestefilen hvilken bruker/gruppe den skal kjøre under

```shell
sysrc readarr_user="BRUKER_DU_VIL_HA"
```

```shell
sysrc readarr_group="GRUPPE_DU_VIL_HA"
```

`readarr` lagrer data, konfigurasjon, logger og PID-filer i `/usr/local/readarr` som standard. Tjenestefilen vil opprette dette og ta eierskap av det HVIS OG BARE HVIS DET IKKE EKSISTERER. Hvis du vil lagre disse filene på et annet sted (f.eks. et datasett montert i jailen for enklere øyeblikksbilder), må du endre det ved hjelp av `sysrc`

```shell
sysrc readarr_data_dir="MAPPE_DU_VIL_HA"
```

Påminnelse: Hvis du bruker en eksisterende plassering, må du manuelt enten: endre eierskapet til UID/GID som `readarr` bruker OG/ELLER legge til `readarr` i en GID som har skrivetilgang.

Nesten ferdig, la oss starte tjenesten:

```shell
service readarr start
```

Hvis alt gikk som planlagt, skal readarr være oppe og kjøre på IP-adressen til jailen (port 8787)!

Du kan nå trygt lukke shellen.

## Feilsøking

- Tjenesten ser ut til å kjøre, men brukergrensesnittet lastes ikke inn eller siden tar for lang tid å laste
  - Sjekk at `allow_mlock` er aktivert i jailen.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Sørg for at du har `VNET` slått på for jailen din, ip6=inherit eller ip6=new

> Tjenesteskriptet skal nå fungere uten VNET og/eller IP6, og fjerne kravet om VNET eller ip6=inherit. {.is-info}