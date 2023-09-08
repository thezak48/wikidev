---
title: Sonarr FreeBSD-installasjon
description: Installasjonsveiledning for Sonarr på FreeBSD
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# FreeBSD

Sonarr-teamet tilbyr bare bygg for FreeBSD. Plugins og porter vedlikeholdes og opprettes av FreeBSD-samfunnet.

Instruksjoner for FreeBSD-installasjoner vedlikeholdes også av FreeBSD-samfunnet, og alle med en GitHub-konto kan oppdatere wikien etter behov.

[Freshports Sonarr-lenke](https://www.freshports.org/net-p2p/sonarr/)

## Oppsett av jail ved hjelp av TrueNAS GUI

1. Fra hovedskjermen velger du Jails.

1. Klikk på ADD.

1. Klikk på Advanced Jail Creation.

1. Navn (hvilket som helst navn fungerer): Sonarr.

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

1. Etter at jailen er opprettet, starter den automatisk. En annen egenskap må settes for at Sonarr skal kunne se lagringsplassen til de monterte medielokasjonene dine. Åpne en rotshell på serveren og skriv inn disse kommandoene:

```shell
iocage stop <jailnavn>
iocage set enforce_statfs=1 <jailnavn>
iocage start <jailnavn>
```

## Oppsett av jail ved hjelp av CLI

Forutsetter at iocage er installert og konfigurert (<https://iocage.readthedocs.io/en/latest/install.html>)
Forutsetter at iocage-nettverksbro (vnet) er konfigurert (<https://iocage.readthedocs.io/en/latest/networking.html>)

Erstatt "10.0.0.100" med en åpen IPV4-adresse på nettverket ditt.
Erstatt "13.1-RELEASE" med ønsket FreeBSD-versjon.
Erstatt "sonarr" med ønsket jailnavn.
Erstatt "accept_rtadv" eller fjern ip6_addr hvis du ikke ønsker automatisk konfigurering av IPV6.

```shell
iocage create -n "sonarr" -r 13.1-RELEASE ip4_addr="vnet0|10.0.0.100/24" vnet="on" allow_raw_sockets="1" boot="on" allow_mlock="1" ip6_addr="vnet0|accept_rtadv" enforce_statfs="1"
iocage console sonarr
```

## Sonarr Mono-installasjon

Gå tilbake til listen over jailer og finn jailen du opprettet for `sonarr`. Klikk på "Shell".

For å installere Sonarr:

> \* Sørg for at pkg-repoet ditt er konfigurert for å hente pakker fra `/latest` og ikke `/quarterly`.
> \* Sjekk `/usr/local/etc/pkg/repos/FreeBSD.conf`.
> \* Hvis den ikke eksisterer, kopier `/etc/pkg/FreeBSD.conf` til den plasseringen, åpne den og erstatt `quarterly` med `latest`.
{.is-warning}

```shell
pkg install sonarr
```

Ikke lukk skallet ennå, vi har fortsatt noen flere ting å gjøre!

## Sonarr .NET-installasjon

Gå tilbake til listen over jailer og finn jailen du opprettet for `sonarr`. Klikk på "Shell".

For å installere Sonarr:

> \* Sørg for at pkg-repoet ditt er konfigurert for å hente pakker fra `/latest` og ikke `/quarterly`.
> \* Sjekk `/usr/local/etc/pkg/repos/FreeBSD.conf`.
> \* Hvis den ikke eksisterer, kopier `/etc/pkg/FreeBSD.conf` til den plasseringen, åpne den og erstatt `quarterly` med `latest`.
{.is-warning}

Installer følgende biblioteker for å støtte Sonarr:

```shell
pkg install icu libunwind krb5 libnotify libinotify sqlite3
```

Opprett Sonarr-bruker og -gruppe (Hvis du ikke ønsker å bruke bruker/gruppe 'sonarr', kan det endres etter preferanse):

```shell
pw user add sonarr -c sonarr -u 351 -d /nonexistent -s /usr/bin/nologin
```

Last ned den nyeste versjonen fra <https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64> og sett tillatelser for den:

```shell
curl -J -L "https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64" -o Sonarr.develop.freebsd-x64.tar.gz
tar -xvf Sonarr.develop.freebsd-x64.tar.gz -C /usr/local/share
chown -R sonarr:sonarr /usr/local/share/Sonarr
```

Opprett en rc.subr-skript for å kjøre Sonarr som en daemon i en redigerer etter eget valg (du kan kanskje hoppe over linje 1 hvis mappen allerede eksisterer), og bruk innholdet i sonarr rc.subr nedenfor:

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
# Add the following lines to /etc/rc.conf.local or /etc/rc.conf
# to enable this service:
#
# sonarr_enable:   Set to yes to enable the sonarr service.
#                       Default: no
# sonarr_user:     The user account used to run the sonarr daemon.
#                       This is optional, however do not specifically set this to an
#                       empty string as this will cause the daemon to run as root.
#                       Default: sonarr
# sonarr_group:    The group account used to run the sonarr daemon.
#                       This is optional, however do not specifically set this to an
#                       empty string as this will cause the daemon to run with group wheel.
#                       Default: sonarr
# sonarr_data_dir: Directory where sonarr configuration data is stored.
#                       Default: /var/db/sonarr
# sonarr_pid:      Name of the pid file.
#                       Default: sonarr.pid
# sonarr_pid_dir:  Path of the pid file.
#                       Default: /var/run/sonarr

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

 # .NET 6+ uses dual mode sockets to avoid the separate AF handling.
 # disable .NET use of V6 if no ipv6 is configured.
 # See https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259194#c17
 ifconfig | grep -q inet6
 if [ $? == 1 ]; then
  export DOTNET_SYSTEM_NET_DISABLEIPV6=1
 fi
}

run_rc_command "$1"
```

Ikke lukk skallet ennå, vi har fortsatt noen flere ting å gjøre!

## Konfigurere Sonarr

Nå som vi har installert det, er det noen flere trinn som kreves.

### Oppsett av tjeneste

Det er på tide å aktivere tjenesten, men før vi gjør det, en merknad:

Oppdateringen er deaktivert som standard. `pkg-message` gir instruksjoner om hvordan du aktiverer oppdateringen, men husk: dette kan ødelegge ting som `pkg check -s` og `pkg remove` for Sonarr når den innebygde oppdateringen erstatter filer.

For å aktivere tjenesten:

```shell
sysrc sonarr_enable=TRUE
```

Hvis du ikke ønsker å bruke bruker/gruppe `sonarr`, må du fortelle tjenestefilen hvilken bruker/gruppe den skal kjøre under:

```shell
sysrc sonarr_user="BRUKER_DU_VIL_BRUKE"
```

```shell
sysrc sonarr_group="GRUPPE_DU_VIL_BRUKE"
```

`sonarr` lagrer data, konfigurasjon, logger og PID-filer i `/usr/local/sonarr` som standard. Tjenestefilen vil opprette dette og ta eierskap av det HVIS OG BARE HVIS DET IKKE EKSISTERER. Hvis du vil lagre disse filene på et annet sted (f.eks. et datasett montert i jailen for enklere øyeblikksbilder), må du endre det ved hjelp av `sysrc`.

```shell
sysrc sonarr_data_dir="MAPPE_DU_VIL_BRUKE"
```

Påminnelse: Hvis du bruker en eksisterende plassering, må du manuelt enten endre eierskapet til UID/GID som `sonarr` bruker OG/ELLER legge til `sonarr` i en GID som har skrivetilgang.

Nesten ferdig, la oss starte tjenesten:

```shell
service sonarr start
```

Hvis alt gikk som planlagt, skal Sonarr være oppe og kjøre på IP-adressen til jailen (port 8989)!

Du kan nå trygt lukke skallet.

## Feilsøking

- Tjenesten ser ut til å kjøre, men brukergrensesnittet lastes ikke inn eller siden tar for lang tid å laste
  - Sjekk at `allow_mlock` er aktivert i jailen.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Sørg for at du har `VNET` slått på for jailen din, ip6=inherit eller ip6=new

> Tjenesteskriptet skal nå fungere uten VNET og/eller IP6, og dermed fjerne kravet om VNET eller ip6=inherit. {.is-info}

### BSD Mono SSL-problemer

- SSL- eller andre sertifikatproblemer (f.eks. `unable to verify SSL certificate`)
  - Se [denne TrueNAS-forumtråden, da du må oppdatere og synkronisere mono-sertifikatene](https://www.truenas.com/community/threads/sonarr-radarr-probably-other-arr-jails-unable-to-verify-ssl-certificates-after-latest-update.96008/)