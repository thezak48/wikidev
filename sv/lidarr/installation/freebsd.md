---
title: Lidarr FreeBSD Installation
description: Installationsguide för Lidarr på FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Lidarr-teamet tillhandahåller endast byggen för FreeBSD. Tillägg och portar underhålls och skapas av FreeBSD-communityn.

Instruktioner för FreeBSD-installationer underhålls också av FreeBSD-communityn och vem som helst med ett GitHub-konto kan uppdatera wikin vid behov.

[Länk till Freshports Lidarr](https://www.freshports.org/net-p2p/lidarr/)

## Konfigurera Jail med TrueNAS GUI

1. Välj Jails från huvudskärmen.

1. Klicka på LÄGG TILL.

1. Klicka på Avancerad skapelse av Jail.

1. Namn (valfritt namn fungerar): Lidarr.

1. Jailtyp: Standard (Klonad Jail).

1. Utgåva: 12.2-Release (eller senare).

1. Konfigurera grundläggande egenskaper efter eget tycke.

1. Konfigurera Jail-egenskaper efter eget tycke, men lägg till

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` är användbart för felsökning (t.ex. ping, traceroute) men är inte ett krav. {.is-info}

1. Konfigurera nätverksegenskaper efter eget tycke.

1. Konfigurera anpassade egenskaper efter eget tycke.

1. Klicka på Spara.

1. Efter att Jail har skapats startar den automatiskt. En till egenskap måste ställas in för att Lidarr ska kunna se lagringsutrymmet för dina monterade medieplatser. Öppna en rotshell på servern och ange dessa kommandon:

```shell
iocage stop <jailnamn>
iocage set enforce_statfs=1 <jailnamn>
iocage start <jailnamn>
```

## Installation av Lidarr

Gå tillbaka till listan över jail och hitta din nyss skapade jail för `lidarr` och klicka på "Shell".

För att installera Lidarr

> \* Se till att din pkg-repo är konfigurerad för att hämta paket från `/latest` och inte `/quarterly`
> \* Kontrollera `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Om den inte finns, kopiera över `/etc/pkg/FreeBSD.conf` till den platsen, öppna den och ersätt `quarterly` med `latest`
{.is-warning}

```shell
pkg install lidarr
```

Stäng inte av shellen än, vi har några fler saker att göra!

## Konfigurera Lidarr

Nu när vi har installerat det krävs några fler steg.

### Konfigurera tjänst

Dags att aktivera tjänsten, men innan vi gör det, en notering:

Uppdateraren är inaktiverad som standard. `pkg-message` ger instruktioner om hur du aktiverar uppdateraren, men kom ihåg: detta kan bryta saker som `pkg check -s` och `pkg remove` för Lidarr när den inbyggda uppdateraren ersätter filer.

För att aktivera tjänsten:

```shell
sysrc lidarr_enable=TRUE
```

Om du inte vill använda användargrupp `lidarr` måste du tala om för tjänstefilen vilken användargrupp den ska köras under

```shell
sysrc lidarr_user="ANVÄNDARE_DU_VILL"
```

```shell
sysrc lidarr_group="GRUPP_DU_VILL"
```

`lidarr` lagrar sina data, konfiguration, loggar och PID-filer i `/usr/local/lidarr` som standard. Tjänstefilen kommer att skapa detta och ta ägarskap av det OM OCH ENDAST OM DET INTE FINNS. Om du vill lagra dessa filer på en annan plats (t.ex. en dataset monterad i jailen för enklare ögonblicksbilder) måste du ändra det med hjälp av `sysrc`

```shell
sysrc lidarr_data_dir="PLATS_DU_VILL"
```

Påminnelse: Om du använder en befintlig plats måste du manuellt antingen: ändra ägandeskapet till UID/GID som `lidarr` använder OCH/ELLER lägga till `lidarr` i en GID som har skrivåtkomst.

Nästan klart, låt oss starta tjänsten:

```shell
service lidarr start
```

Om allt gick enligt planen ska Lidarr vara igång och köra på IP-adressen för jailen (port 8686)!

Du kan nu tryggt stänga av shellen.

## Felsökning

- Tjänsten verkar vara igång men användargränssnittet laddas inte eller sidan tar för lång tid att ladda
  - Dubbelkolla att `allow_mlock` är aktiverat i jailen
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Se till att du har `VNET` aktiverat för din jail, ip6=inherit eller ip6=new

> Tjänsteskriptet bör nu fungera utan VNET och/eller IP6 och därmed ta bort kravet på VNET eller ip6=inherit
{.is-info}