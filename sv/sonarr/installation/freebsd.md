---
title: Sonarr FreeBSD Installation
description: Installationsguide för Sonarr på FreeBSD
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# FreeBSD

Sonarr-teamet tillhandahåller endast byggen för FreeBSD. Tillägg och portar underhålls och skapas av FreeBSD-communityn.

Instruktioner för FreeBSD-installationer underhålls också av FreeBSD-communityn och vem som helst med ett GitHub-konto kan uppdatera wikin vid behov.

[Länk till Freshports Sonarr](https://www.freshports.org/net-p2p/sonarr/)

## Inställning av jail med TrueNAS GUI

1. Välj Jails från huvudskärmen.

1. Klicka på LÄGG TILL.

1. Klicka på Avancerad jail-skapelse.

1. Namn (valfritt namn fungerar): Sonarr.

1. Jailtyp: Standard (klonad jail).

1. Utgåva: 12.2-Release (eller senare).

1. Konfigurera grundläggande egenskaper efter eget tycke.

1. Konfigurera jail-egenskaper efter eget tycke, men lägg till

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` är användbart för felsökning (t.ex. ping, traceroute) men är inte ett krav. {.is-info}

1. Konfigurera nätverksegenskaper efter eget tycke.

1. Konfigurera anpassade egenskaper efter eget tycke.

1. Klicka på Spara.

1. Efter att jailen har skapats startar den automatiskt. En till egenskap måste ställas in för att Sonarr ska kunna se lagringsutrymmet för dina monterade medieplatser. Öppna en rotshell på servern och ange dessa kommandon:

```shell
iocage stop <jailnamn>
iocage set enforce_statfs=1 <jailnamn>
iocage start <jailnamn>
```

## Inställning av jail med CLI

Förutsätter att iocage är installerat och konfigurerat (<https://iocage.readthedocs.io/en/latest/install.html>)
Förutsätter att iocage-nätverksbryggan (vnet) är konfigurerad (<https://iocage.readthedocs.io/en/latest/networking.html>)

Ersätt "10.0.0.100" med en ledig IPV4-adress i ditt nätverk
Ersätt "13.1-RELEASE" med önskad FreeBSD-version
Ersätt "sonarr" med ditt önskade jail-namn
Ersätt "accept_rtadv" eller ta bort ip6_addr om du inte vill ha automatisk konfiguration av IPV6

```shell
iocage create -n "sonarr" -r 13.1-RELEASE ip4_addr="vnet0|10.0.0.100/24" vnet="on" allow_raw_sockets="1" boot="on" allow_mlock="1" ip6_addr="vnet0|accept_rtadv" enforce_statfs="1"
iocage console sonarr
```

## Installation av Sonarr Mono

Gå tillbaka till jail-listan och hitta din nyss skapade jail för `sonarr` och klicka på "Shell".

För att installera Sonarr:

> \* Se till att ditt pkg-repo är konfigurerat för att hämta paket från `/latest` och inte `/quarterly`
> \* Kontrollera `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Om det inte finns, kopiera över `/etc/pkg/FreeBSD.conf` till den platsen, öppna den och ersätt `quarterly` med `latest`
{.is-warning}

```shell
pkg install sonarr
```

Stäng inte av shellen än, vi har några fler saker att göra!

## Installation av Sonarr .NET

Gå tillbaka till jail-listan och hitta din nyss skapade jail för `sonarr` och klicka på "Shell".

För att installera Sonarr:

> \* Se till att ditt pkg-repo är konfigurerat för att hämta paket från `/latest` och inte `/quarterly`
> \* Kontrollera `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Om det inte finns, kopiera över `/etc/pkg/FreeBSD.conf` till den platsen, öppna den och ersätt `quarterly` med `latest`
{.is-warning}

Installera följande bibliotek för att stödja Sonarr:

```shell
pkg install icu libunwind krb5 libnotify libinotify sqlite3
```

Skapa användare och grupp för Sonarr (Om du inte vill använda användare/grupp 'sonarr' kan du ändra det efter eget tycke):

```shell
pw user add sonarr -c sonarr -u 351 -d /nonexistent -s /usr/bin/nologin
```

Ladda ner den senaste versionen från <https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64> och ange dess behörigheter:

```shell
curl -J -L "https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64" -o Sonarr.develop.freebsd-x64.tar.gz
tar -xvf Sonarr.develop.freebsd-x64.tar.gz -C /usr/local/share
chown -R sonarr:sonarr /usr/local/share/Sonarr
```

Skapa ett rc.subr-skript för att köra Sonarr som en daemon i en redigerare efter eget val (du kan eventuellt hoppa över rad 1 om mappen redan finns) och använd innehållet i sonarr rc.subr nedan:

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
# Lägg till följande rader i /etc/rc.conf.local eller /etc/rc.conf
# för att aktivera denna tjänst:
#
# sonarr_enable:   Ställ in till yes för att aktivera sonarr-tjänsten.
#                       Standard: no
# sonarr_user:     Användarkontot som används för att köra sonarr-daemonen.
#                       Detta är valfritt, men ställ inte in det till en
#                       tom sträng eftersom detta kommer att få daemonen att köras som root.
#                       Standard: sonarr
# sonarr_group:    Gruppkontot som används för att köra sonarr-daemonen.
#                       Detta är valfritt, men ställ inte in det till en
#                       tom sträng eftersom detta kommer att få daemonen att köras med gruppen wheel.
#                       Standard: sonarr
# sonarr_data_dir: Katalog där sonarr-konfigurationsdata lagras.
#                       Standard: /var/db/sonarr
# sonarr_pid:      Namn på pid-filen.
#                       Standard: sonarr.pid
# sonarr_pid_dir:  Sökväg till pid-filen.
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

 # .NET 6+ använder dubbelmodessocklar för att undvika separat AF-hantering.
 # inaktivera .NET:s användning av V6 om ingen ipv6 är konfigurerad.
 # Se https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259194#c17
 ifconfig | grep -q inet6
 if [ $? == 1 ]; then
  export DOTNET_SYSTEM_NET_DISABLEIPV6=1
 fi
}

run_rc_command "$1"
```

Stäng inte av shellen än, vi har några fler saker att göra!

## Konfigurera Sonarr

Nu när vi har installerat det krävs några fler steg.

### Inställning av tjänst

Dags att aktivera tjänsten, men innan vi gör det, en anteckning:

Uppdateraren är inaktiverad som standard. `pkg-message` ger instruktioner om hur du aktiverar uppdateraren, men kom ihåg: detta kan bryta saker som `pkg check -s` och `pkg remove` för Sonarr när den inbyggda uppdateraren ersätter filer.

För att aktivera tjänsten:

```shell
sysrc sonarr_enable=TRUE
```

Om du inte vill använda användare/grupp `sonarr` måste du tala om för tjänstefilen vilken användare/grupp den ska köras under

```shell
sysrc sonarr_user="ANVÄNDARE_DU_VILL"
```

```shell
sysrc sonarr_group="GRUPP_DU_VILL"
```

`sonarr` lagrar sina data, konfiguration, loggar och PID-filer i `/usr/local/sonarr` som standard. Tjänstefilen kommer att skapa detta och ta ägarskap av det OM OCH ENDAST OM DET INTE REDAN FINNS. Om du vill lagra dessa filer på en annan plats (t.ex. en dataset monterad i jailen för enklare ögonblicksbilder) måste du ändra det med `sysrc`

```shell
sysrc sonarr_data_dir="KATALOG_DU_VILL"
```

Påminnelse: Om du använder en befintlig plats måste du manuellt antingen ändra ägandet till UID/GID som `sonarr` använder OCH/ELLER lägga till `sonarr` i en GID som har skrivåtkomst.

Nästan klart, låt oss starta tjänsten:

```shell
service sonarr start
```

Om allt gick enligt planen ska Sonarr vara igång och köra på jailens IP-adress (port 8989)!

Du kan nu tryggt stänga shellen.

## Felsökning

- Tjänsten verkar vara igång men användargränssnittet laddas inte eller sidan tar för lång tid att ladda
  - Dubbelkolla att `allow_mlock` är aktiverat i jailen.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Se till att du har `VNET` aktiverat för din jail, ip6=inherit eller ip6=new

> Tjänsteskriptet bör nu fungera även utan VNET och/eller IP6 och därmed ta bort kravet på VNET eller ip6=inherit. {.is-info}

### Problem med SSL i BSD Mono

- SSL- eller andra certifikatproblem (t.ex. `unable to verify SSL certificate`)
  - Se [detta inlägg på TrueNAS-forumet eftersom du behöver uppdatera och synkronisera monos certifikat](https://www.truenas.com/community/threads/sonarr-radarr-probably-other-arr-jails-unable-to-verify-ssl-certificates-after-latest-update.96008/)