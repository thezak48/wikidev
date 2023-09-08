---
title: Sonarr FreeBSD Installation
description: FreeBSD installationsvejledning til Sonarr
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# FreeBSD

Sonarr-teamet leverer kun bygninger til FreeBSD. Plugins og Ports vedligeholdes og oprettes af FreeBSD-fællesskabet.

Instruktioner til FreeBSD-installationer vedligeholdes også af FreeBSD-fællesskabet, og enhver med en GitHub-konto kan opdatere wikien efter behov.

[Freshports Sonarr Link](https://www.freshports.org/net-p2p/sonarr/)

## Jail-opsætning ved hjælp af TrueNAS GUI

1. Vælg Jails fra hovedskærmen

1. Klik på TILFØJ

1. Klik på Avanceret jail-oprettelse

1. Navn (ethvert navn fungerer): Sonarr

1. Jail-type: Standard (klon-jail)

1. Udgivelse: 12.2-Release (eller nyere)

1. Konfigurer grundlæggende egenskaber efter eget ønske

1. Konfigurer jail-egenskaber efter eget ønske, men tilføj

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` er nyttigt til fejlfinding (f.eks. ping, traceroute), men er ikke et krav. {.is-info}

1. Konfigurer netværksegenskaber efter eget ønske

1. Konfigurer brugerdefinerede egenskaber efter eget ønske

1. Klik på Gem

1. Når jailen er oprettet, starter den automatisk. Der kræves en yderligere egenskab for at Sonarr kan se lagerpladsen for dine monterede medielokationer. Åbn en root shell på serveren og indtast disse kommandoer:

```shell
iocage stop <jailnavn>
iocage set enforce_statfs=1 <jailnavn>
iocage start <jailnavn>
```

## Jail-opsætning ved hjælp af CLI

Forudsætter, at iocage er installeret og konfigureret (<https://iocage.readthedocs.io/en/latest/install.html>)
Forudsætter, at iocage-netværksbroen (vnet) er konfigureret (<https://iocage.readthedocs.io/en/latest/networking.html>)

Erstat "10.0.0.100" med en åben IPV4-adresse på dit netværk
Erstat "13.1-RELEASE" med foretrukken FreeBSD-version
Erstat "sonarr" med dit foretrukne jail-navn
Erstat "accept_rtadv" eller fjern ip6_addr, hvis du ikke ønsker automatisk konfiguration af IPV6

```shell
iocage create -n "sonarr" -r 13.1-RELEASE ip4_addr="vnet0|10.0.0.100/24" vnet="on" allow_raw_sockets="1" boot="on" allow_mlock="1" ip6_addr="vnet0|accept_rtadv" enforce_statfs="1"
iocage console sonarr
```

## Sonarr Mono-installation

Gå tilbage til listen over jails, find din nyoprettede jail for `sonarr` og klik på "Shell"

For at installere Sonarr

> \* Sørg for, at din pkg-repo er konfigureret til at hente pakker fra `/latest` og ikke `/quarterly`
> \* Kontroller `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Hvis det ikke findes, kopier `/etc/pkg/FreeBSD.conf` til den placering, åbn den og erstatt `quarterly` med `latest`
{.is-warning}

```shell
pkg install sonarr
```

Luk ikke shell'en endnu, vi har stadig et par ting tilbage!

## Sonarr .NET-installation

Gå tilbage til listen over jails, find din nyoprettede jail for `sonarr` og klik på "Shell"

For at installere Sonarr

> \* Sørg for, at din pkg-repo er konfigureret til at hente pakker fra `/latest` og ikke `/quarterly`
> \* Kontroller `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Hvis det ikke findes, kopier `/etc/pkg/FreeBSD.conf` til den placering, åbn den og erstatt `quarterly` med `latest`
{.is-warning}

Installer følgende biblioteker for at understøtte Sonarr

```shell
pkg install icu libunwind krb5 libnotify libinotify sqlite3
```

Opret Sonarr-bruger og -gruppe (Hvis du ikke ønsker at bruge bruger/gruppe 'sonarr', kan det ændres efter præference)

```shell
pw user add sonarr -c sonarr -u 351 -d /nonexistent -s /usr/bin/nologin
```

Download den nyeste version fra <https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64> og angiv dens tilladelser

```shell
curl -J -L "https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64" -o Sonarr.develop.freebsd-x64.tar.gz
tar -xvf Sonarr.develop.freebsd-x64.tar.gz -C /usr/local/share
chown -R sonarr:sonarr /usr/local/share/Sonarr
```

Opret en rc.subr-script til at køre Sonarr som en daemon i en editor efter eget valg (du kan muligvis springe linje 1 over, hvis mappen allerede findes), og brug indholdet af sonarr rc.subr nedenfor

```shell
mkdir -p /usr/local/etc/rc.d
vi /usr/local/etc/rc.d/sonarr
chmod +x /usr/local/etc/rc.d/sonarr
```

```shell
#!/bin/sh

# PROVIDE: sonarr
# REQUIRE: LOGIN
# KEYWORD: shutdown
#
# Tilføj følgende linjer til /etc/rc.conf.local eller /etc/rc.conf
# for at aktivere denne service:
#
# sonarr_enable:   Sæt til ja for at aktivere sonarr-tjenesten.
#                       Standard: nej
# sonarr_user:     Brugerkontoen, der bruges til at køre sonarr-daemonen.
#                       Dette er valgfrit, men indstil ikke specifikt dette til en
#                       tom streng, da dette vil få daemonen til at køre som root.
#                       Standard: sonarr
# sonarr_group:    Gruppekontoen, der bruges til at køre sonarr-daemonen.
#                       Dette er valgfrit, men indstil ikke specifikt dette til en
#                       tom streng, da dette vil få daemonen til at køre med gruppen wheel.
#                       Standard: sonarr
# sonarr_data_dir: Mappen, hvor sonarr-konfigurationsdata gemmes.
#                       Standard: /var/db/sonarr
# sonarr_pid:      Navnet på pid-filen.
#                       Standard: sonarr.pid
# sonarr_pid_dir:  Stien til pid-filen.
#                       Standard: /var/run/sonarr

. /etc/rc.subr
name=sonarr
rcvar=${name}_enable
load_rc_config ${name}

: ${sonarr_enable:="no"}
: ${sonarr_user:="sonarr"}
: ${sonarr_group:="sonarr"}
: ${sonarr_data_dir:="/var/db/sonarr"}
: ${sonarr_pid:="sonarr.pid"}
: ${sonarr_pid_dir:="/var/run/sonarr"}

pidfile="${sonarr_pid_dir}/${sonarr_pid}"
command="/usr/sbin/daemon"
command_args="-r -f -P ${pidfile} /usr/local/share/Sonarr/Sonarr --debug --data=${sonarr_data_dir} --nobrowser"

start_precmd=sonarr_start_precmd
sonarr_start_precmd()
{
 [ -d ${sonarr_pid_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_pid_dir}
 [ -d ${sonarr_data_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_data_dir}

 # .NET 6+ bruger dual mode-sockets for at undgå separat AF-håndtering.
 # deaktiver .NET-brug af V6, hvis der ikke er konfigureret ipv6.
 # Se https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259194#c17
 ifconfig | grep -q inet6
 if [ $? == 1 ]; then
  export DOTNET_SYSTEM_NET_DISABLEIPV6=1
 fi
}

run_rc_command "$1"
```

Luk ikke shell'en endnu, vi har stadig et par ting tilbage!

## Konfiguration af Sonarr

Nu hvor vi har det installeret, kræves der et par flere trin.

### Tjenesteopsætning

Det er tid til at aktivere tjenesten, men før vi gør det, en note:

Opdateringen er som standard deaktiveret. `pkg-message` giver instruktioner om, hvordan du aktiverer opdateringen, men husk: dette kan ødelægge ting som `pkg check -s` og `pkg remove` for Sonarr, når den indbyggede opdatering erstatter filer.

For at aktivere tjenesten:

```shell
sysrc sonarr_enable=TRUE
```

Hvis du ikke ønsker at bruge bruger/gruppe `sonarr`, skal du fortælle tjenestefilen, hvilken bruger/gruppe den skal køre under

```shell
sysrc sonarr_user="BRUGER_DU_VIL_BRUGE"
```

```shell
sysrc sonarr_group="GRUPPE_DU_VIL_BRUGE"
```

`sonarr` gemmer sine data, konfiguration, logfiler og PID-filer i `/usr/local/sonarr` som standard. Tjenestefilen opretter dette og tager ejerskab af det, HVIS OG KUN HVIS DET IKKE EKSISTERER. Hvis du vil gemme disse filer et andet sted (f.eks. et datasæt monteret i jailen for nemmere snapshots), skal du ændre det ved hjælp af `sysrc`

```shell
sysrc sonarr_data_dir="MAPPE_DU_VIL_BRUGE"
```

Påmindelse: Hvis du bruger en eksisterende placering, skal du manuelt enten ændre ejerskabet til UID/GID, som `sonarr` bruger, OG/ELLER tilføje `sonarr` til en GID, der har skriveadgang.

Næsten færdig, lad os starte tjenesten:

```shell
service sonarr start
```

Hvis alt gik efter planen, skal Sonarr være oppe og køre på jailens IP (port 8989)!

Du kan nu trygt lukke shell'en

## Fejlfinding

- Tjenesten ser ud til at køre, men brugergrænsefladen indlæses ikke, eller siden timeouter
  - Dobbelttjek, at `allow_mlock` er aktiveret i jailen
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Sørg for, at du har `VNET` slået til for din jail, ip6=inherit eller ip6=new

> Tjenesteskriptet bør nu omgå manglen på VNET og/eller IP6 og dermed fjerne kravet om VNET eller ip6=inherit
{.is-info}

### BSD Mono SSL-problemer

- SSL- eller andre certifikatproblemer (f.eks. `unable to verify SSL certificate`)
  - Se [dette TrueNAS-forumindlæg, da du skal opdatere og synkronisere mono's certifikater](https://www.truenas.com/community/threads/sonarr-radarr-probably-other-arr-jails-unable-to-verify-ssl-certificates-after-latest-update.96008/)