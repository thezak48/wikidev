---
title: Prowlarr FreeBSD Installation
description: FreeBSD installationsvejledning til Prowlarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Prowlarr-teamet leverer kun bygninger til FreeBSD. Plugins og Ports vedligeholdes og oprettes af FreeBSD-fællesskabet.

Instruktioner til FreeBSD-installationer vedligeholdes også af FreeBSD-fællesskabet, og enhver med en GitHub-konto kan opdatere wikien efter behov.

[Freshports Prowlarr Link](https://www.freshports.org/net-p2p/prowlarr/)

## Jail Opsætning ved brug af TrueNAS GUI

1. Fra hovedskærmen skal du vælge Jails.

1. Klik på TILFØJ.

1. Klik på Avanceret Jail-oprettelse.

1. Navn (ethvert navn fungerer): Prowlarr.

1. Jail-type: Standard (Clone Jail).

1. Udgivelse: 12.2-Release (eller nyere).

1. Konfigurer grundlæggende egenskaber efter dit ønske.

1. Konfigurer Jail-egenskaber efter dit ønske, men tilføj

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` er nyttigt til fejlfinding (f.eks. ping, traceroute), men det er ikke et krav. {.is-info}

1. Konfigurer netværksegenskaber efter dit ønske.

1. Konfigurer brugerdefinerede egenskaber efter dit ønske.

1. Klik på Gem.

## Prowlarr Installation

Når du er tilbage på jails-listen, skal du finde din nyoprettede jail til `prowlarr` og klikke på "Shell".

For at installere Prowlarr

> \* Sørg for, at din pkg-repo er konfigureret til at hente pakker fra `/latest` og ikke `/quarterly`.
> \* Kontroller `/usr/local/etc/pkg/repos/FreeBSD.conf`.
> \* Hvis det ikke findes, skal du kopiere `/etc/pkg/FreeBSD.conf` til den placering, åbne den og erstatte `quarterly` med `latest`.
{.is-warning}

```shell
pkg install prowlarr
```

Luk ikke skallen endnu, vi har stadig et par ting!

## Konfiguration af Prowlarr

Nu hvor vi har det installeret, kræves der et par flere trin.

### Serviceopsætning

Det er tid til at aktivere tjenesten, men før vi gør det, en note:

Opdateringen er som standard deaktiveret. `pkg-message` giver instruktioner om, hvordan du aktiverer opdateringen, men husk: dette kan ødelægge ting som `pkg check -s` og `pkg remove` for prowlarr, når den indbyggede opdatering erstatter filer.

For at aktivere tjenesten:

```shell
sysrc prowlarr_enable=TRUE
```

Hvis du ikke ønsker at bruge bruger/gruppe `prowlarr`, skal du fortælle tjenestefilen, hvilken bruger/gruppe den skal køre under.

```shell
sysrc prowlarr_user="BRUGER_DU_VIL_BRUGE"
```

```shell
sysrc prowlarr_group="GRUPPE_DU_VIL_BRUGE"
```

`prowlarr` gemmer sine data, konfiguration, logfiler og PID-filer i `/usr/local/prowlarr` som standard. Tjenestefilen opretter dette og tager ejerskab af det, HVIS OG KUN HVIS DET IKKE EKSISTERER. Hvis du vil gemme disse filer et andet sted (f.eks. et datasæt monteret i jailen for nemmere snapshots), skal du ændre det ved hjælp af `sysrc`.

```shell
sysrc prowlarr_data_dir="STI_DU_VIL_BRUGE"
```

Påmindelse: Hvis du bruger en eksisterende placering, skal du manuelt enten ændre ejerskabet til UID/GID, som `prowlarr` bruger, OG/ELLER tilføje `prowlarr` til en GID, der har skriveadgang.

Næsten færdig, lad os starte tjenesten:

```shell
service prowlarr start
```

Hvis alt gik efter planen, skal prowlarr være i gang og køre på jailens IP (port 9696)!

Du kan nu trygt lukke skallen.

## Fejlfinding

- Tjenesten ser ud til at køre, men brugergrænsefladen indlæses ikke, eller siden udløber
  - Dobbelttjek, at `allow_mlock` er aktiveret i jailen.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Sørg for, at du har `VNET` aktiveret for din jail, ip6=inherit eller ip6=new.

> Tjenesteskriptet burde nu fungere uden VNET og/eller IP6 og fjerne kravet om VNET eller ip6=inherit. {.is-info}