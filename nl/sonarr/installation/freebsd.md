---
title: Sonarr FreeBSD-installatie
description: Installatiehandleiding voor Sonarr op FreeBSD
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# FreeBSD

Het Sonarr-team biedt alleen builds aan voor FreeBSD. Plugins en Ports worden onderhouden en gemaakt door de FreeBSD-community.

Instructies voor FreeBSD-installaties worden ook onderhouden door de FreeBSD-community en iedereen met een GitHub-account kan de wiki bijwerken indien nodig.

[Freshports Sonarr-link](https://www.freshports.org/net-p2p/sonarr/)

## Jail-instellingen met behulp van TrueNAS GUI

1. Selecteer Jails vanaf het hoofdscherm

1. Klik op TOEVOEGEN

1. Klik op Geavanceerde jail-creatie

1. Naam (elke naam werkt): Sonarr

1. Jailtype: Standaard (Kloonjail)

1. Release: 12.2-Release (of nieuwer)

1. Configureer de basisinstellingen naar wens

1. Configureer de jail-eigenschappen naar wens, maar voeg het volgende toe

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` is handig voor probleemoplossing (bijv. ping, traceroute), maar is niet vereist. {.is-info}

1. Configureer de netwerkeigenschappen naar wens

1. Configureer de aangepaste eigenschappen naar wens

1. Klik op Opslaan

1. Nadat de jail is aangemaakt, wordt deze automatisch gestart. Er moet nog één eigenschap worden ingesteld zodat Sonarr de opslagruimte van uw gemonteerde mediaplekken kan zien. Open een rootshell op de server en voer deze commando's in:

```shell
iocage stop <jailnaam>
iocage set enforce_statfs=1 <jailnaam>
iocage start <jailnaam>
```

## Jail-instellingen met behulp van CLI

Gaat ervan uit dat iocage is geïnstalleerd en geconfigureerd (<https://iocage.readthedocs.io/en/latest/install.html>)
Gaat ervan uit dat iocage-netwerkbrug (vnet) is geconfigureerd (<https://iocage.readthedocs.io/en/latest/networking.html>)

Vervang "10.0.0.100" door een open IPV4-adres in uw netwerk
Vervang "13.1-RELEASE" door de gewenste FreeBSD-versie
Vervang "sonarr" door uw gewenste jailnaam
Vervang "accept_rtadv" of verwijder ip6_addr als u geen automatische configuratie van IPV6 wilt

```shell
iocage create -n "sonarr" -r 13.1-RELEASE ip4_addr="vnet0|10.0.0.100/24" vnet="on" allow_raw_sockets="1" boot="on" allow_mlock="1" ip6_addr="vnet0|accept_rtadv" enforce_statfs="1"
iocage console sonarr
```

## Sonarr Mono-installatie

Ga terug naar de jail-lijst en zoek de zojuist aangemaakte jail voor `sonarr` en klik op "Shell"

Om Sonarr te installeren

> \* Zorg ervoor dat uw pkg-repo is geconfigureerd om pakketten van `/latest` te krijgen en niet van `/quarterly`
> \* Controleer `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Als dat niet bestaat, kopieer dan `/etc/pkg/FreeBSD.conf` naar die locatie, open het en vervang `quarterly` door `latest`
{.is-warning}

```shell
pkg install sonarr
```

Sluit de shell nog niet af, we hebben nog een paar dingen te doen!

## Sonarr .NET-installatie

Ga terug naar de jail-lijst en zoek de zojuist aangemaakte jail voor `sonarr` en klik op "Shell"

Om Sonarr te installeren

> \* Zorg ervoor dat uw pkg-repo is geconfigureerd om pakketten van `/latest` te krijgen en niet van `/quarterly`
> \* Controleer `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Als dat niet bestaat, kopieer dan `/etc/pkg/FreeBSD.conf` naar die locatie, open het en vervang `quarterly` door `latest`
{.is-warning}

Installeer de volgende bibliotheken om Sonarr te ondersteunen

```shell
pkg install icu libunwind krb5 libnotify libinotify sqlite3
```

Maak de Sonarr-gebruiker en -groep aan (Als u de gebruiker/groep 'sonarr' niet wilt gebruiken, kunt u deze naar wens wijzigen)

```shell
pw user add sonarr -c sonarr -u 351 -d /nonexistent -s /usr/bin/nologin
```

Download de nieuwste versie van <https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64> en stel de machtigingen in

```shell
curl -J -L "https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64" -o Sonarr.develop.freebsd-x64.tar.gz
tar -xvf Sonarr.develop.freebsd-x64.tar.gz -C /usr/local/share
chown -R sonarr:sonarr /usr/local/share/Sonarr
```

Maak een rc.subr-script aan om Sonarr als een daemon uit te voeren in een editor naar keuze (u kunt regel 1 mogelijk overslaan als de map al bestaat) en gebruik de inhoud van sonarr rc.subr hieronder

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
# Voeg de volgende regels toe aan /etc/rc.conf.local of /etc/rc.conf
# om deze service in te schakelen:
#
# sonarr_enable:   Stel in op ja om de sonarr-service in te schakelen.
#                       Standaard: nee
# sonarr_user:     Het gebruikersaccount dat wordt gebruikt om de sonarr-daemon uit te voeren.
#                       Dit is optioneel, stel dit echter niet expliciet in op een
#                       lege tekenreeks, omdat de daemon dan als root wordt uitgevoerd.
#                       Standaard: sonarr
# sonarr_group:    De groepsaccount die wordt gebruikt om de sonarr-daemon uit te voeren.
#                       Dit is optioneel, stel dit echter niet expliciet in op een
#                       lege tekenreeks, omdat de daemon dan wordt uitgevoerd met de groep wiel.
#                       Standaard: sonarr
# sonarr_data_dir: Map waarin de sonarr-configuratiegegevens worden opgeslagen.
#                       Standaard: /var/db/sonarr
# sonarr_pid:      Naam van het pid-bestand.
#                       Standaard: sonarr.pid
# sonarr_pid_dir:  Pad van het pid-bestand.
#                       Standaard: /var/run/sonarr

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

 # .NET 6+ gebruikt dual mode sockets om afzonderlijke AF-verwerking te vermijden.
 # schakel .NET-gebruik van V6 uit als er geen ipv6 is geconfigureerd.
 # Zie https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259194#c17
 ifconfig | grep -q inet6
 if [ $? == 1 ]; then
  export DOTNET_SYSTEM_NET_DISABLEIPV6=1
 fi
}

run_rc_command "$1"
```

Sluit de shell nog niet af, we hebben nog een paar dingen te doen!

## Configuratie van Sonarr

Nu we het hebben geïnstalleerd, zijn er nog een paar stappen vereist.

### Service-instellingen

Tijd om de service in te schakelen, maar voordat we dat doen, een opmerking:

De updater is standaard uitgeschakeld. De `pkg-message` geeft instructies over hoe u de updater kunt inschakelen, maar houd er rekening mee dat dit dingen kan breken zoals `pkg check -s` en `pkg remove` voor Sonarr wanneer de ingebouwde updater bestanden vervangt.

Om de service in te schakelen:

```shell
sysrc sonarr_enable=TRUE
```

Als u geen gebruik wilt maken van gebruiker/groep `sonarr`, moet u het servicebestand vertellen onder welke gebruiker/groep het moet worden uitgevoerd

```shell
sysrc sonarr_user="GEBRUIKER_DIE_U_WILT"
```

```shell
sysrc sonarr_group="GROEP_DIE_U_WILT"
```

`sonarr` slaat zijn gegevens, configuratie, logs en PID-bestanden standaard op in `/usr/local/sonarr`. Het servicebestand maakt dit aan en neemt het in bezit ALS EN ALLEEN ALS HET NIET BESTAAT. Als u deze bestanden op een andere plaats wilt opslaan (bijv. een dataset die in de jail is gemount voor eenvoudigere snapshots), dan moet u dit wijzigen met behulp van `sysrc`

```shell
sysrc sonarr_data_dir="MAP_DIE_U_WILT"
```

Herinnering: Als u een bestaande locatie gebruikt, moet u handmatig de eigendom wijzigen naar de UID/GID die `sonarr` gebruikt EN/OF `sonarr` toevoegen aan een GID met schrijftoegang.

Bijna klaar, laten we de service starten:

```shell
service sonarr start
```

Als alles volgens plan is verlopen, zou Sonarr moeten werken op het IP-adres van de jail (poort 8989)!

U kunt nu veilig de shell sluiten

## Problemen oplossen

- De service lijkt actief te zijn, maar de gebruikersinterface wordt niet geladen of de pagina loopt vast
  - Controleer nogmaals of `allow_mlock` is ingeschakeld in de jail
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Zorg ervoor dat `VNET` is ingeschakeld voor uw jail, ip6=inherit of ip6=new

> Het servicescript zou nu moeten werken zonder VNET en/of IP6, waardoor de vereiste voor VNET of ip6=inherit wordt verwijderd
{.is-info}

### BSD Mono SSL-problemen

- SSL- of andere certificaatproblemen (bijv. `unable to verify SSL certificate`)
  - Zie [deze TrueNAS-forumpost, omdat u de certificaten van mono moet bijwerken en synchroniseren](https://www.truenas.com/community/threads/sonarr-radarr-probably-other-arr-jails-unable-to-verify-ssl-certificates-after-latest-update.96008/)