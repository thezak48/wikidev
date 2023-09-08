---
title: Radarr FreeBSD Installation
description: FreeBSD installationsguide til Radarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Radarr-teamet leverer kun bygninger til FreeBSD. Plugins og porte vedligeholdes og oprettes af FreeBSD-fællesskabet.

Instruktioner til FreeBSD-installationer vedligeholdes også af FreeBSD-fællesskabet, og enhver med en GitHub-konto kan opdatere wikien efter behov.

[Freshports Radarr Link](https://www.freshports.org/net-p2p/radarr/)

## Opsætning af jail ved hjælp af TrueNAS GUI

1. Vælg Jails fra hovedskærmen

1. Klik på TILFØJ

1. Klik på Avanceret jail-oprettelse

1. Navn (ethvert navn fungerer): Radarr

1. Jail-type: Standard (Klon-jail)

1. Udgivelse: 12.2-Release (eller nyere)

1. Konfigurer grundlæggende egenskaber efter dit ønske

1. Konfigurer jail-egenskaber efter dit ønske, men tilføj

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` er nyttigt til fejlfinding (f.eks. ping, traceroute), men er ikke et krav. {.is-info}

1. Konfigurer netværksegenskaber efter dit ønske

1. Konfigurer brugerdefinerede egenskaber efter dit ønske

1. Klik på Gem

1. Når jailen er oprettet, starter den automatisk. Der kræves en yderligere egenskab for at Radarr kan se lagerpladsen for dine monterede medielokationer. Åbn en root shell på serveren og indtast disse kommandoer:

```shell
iocage stop <jailnavn>
iocage set enforce_statfs=1 <jailnavn>
iocage start <jailnavn>
```

## Radarr-installation

Find din nyoprettede jail til `radarr` på jail-listen og klik på `Shell`

For at installere Radarr

> \* Sørg for, at din pkg-repo er konfigureret til at hente pakker fra `/latest` og ikke `/quarterly`
> \* Kontroller `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Hvis det ikke findes, kopier `/etc/pkg/FreeBSD.conf` til den placering, åbn den og erstatt `quarterly` med `latest`
{.is-warning}

```shell
pkg install radarr
```

Luk ikke shell'en endnu, vi har stadig et par ting tilbage!

## Konfiguration af Radarr

Nu hvor vi har det installeret, kræves der et par flere trin.

### Serviceopsætning

Det er tid til at aktivere tjenesten, men før vi gør det, en note:

Opdateringen er som standard deaktiveret. `pkg-message` giver instruktioner om, hvordan du aktiverer opdateringen, men husk: dette kan ødelægge ting som `pkg check -s` og `pkg remove` for Radarr, når den indbyggede opdatering erstatter filer.

For at aktivere tjenesten:

```shell
sysrc radarr_enable=TRUE
```

Hvis du ikke ønsker at bruge bruger/gruppe `radarr`, skal du fortælle tjenestefilen, hvilken bruger/gruppe den skal køre under

```shell
sysrc radarr_user="BRUGER_DU_VIL_BRUGE"
```

```shell
sysrc radarr_group="GRUPPE_DU_VIL_BRUGE"
```

`radarr` gemmer sine data, konfiguration, logfiler og PID-filer i `/usr/local/radarr` som standard. Tjenestefilen opretter dette og tager ejerskab af det, HVIS OG KUN HVIS DET IKKE EKSISTERER. Hvis du vil gemme disse filer et andet sted (f.eks. et datasæt monteret i jailen for nemmere snapshots), skal du ændre det ved hjælp af `sysrc`

```shell
sysrc radarr_data_dir="STI_DU_VIL_BRUGE"
```

Påmindelse: Hvis du bruger en eksisterende placering, skal du manuelt enten ændre ejerskabet til UID/GID, som `radarr` bruger, OG/ELLER tilføje `radarr` til en GID, der har skriveadgang.

Næsten færdig, lad os starte tjenesten:

```shell
service radarr start
```

Hvis alt gik efter planen, skal radarr være oppe og køre på jailens IP (port 7878)!

Du kan nu trygt lukke shell'en

## Fejlfinding

- Tjenesten ser ud til at køre, men brugergrænsefladen indlæses ikke, eller siden udløber
  - Dobbelttjek, at `allow_mlock` er aktiveret i jailen
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Sørg for, at du har `VNET` aktiveret for din jail, ip6=inherit eller ip6=new

> Tjenesteskriptet bør nu fungere uden VNET og/eller IP6 og fjerne kravet om VNET eller ip6=inherit
{.is-info}