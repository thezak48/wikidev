---
title: Radarr FreeBSD Installation
description: Installationsguide för Radarr på FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Radarr-teamet tillhandahåller endast byggen för FreeBSD. Tillägg och portar underhålls och skapas av FreeBSD-communityn.

Instruktioner för FreeBSD-installationer underhålls också av FreeBSD-communityn och vem som helst med ett GitHub-konto kan uppdatera wikin vid behov.

[Länk till Freshports Radarr](https://www.freshports.org/net-p2p/radarr/)

## Konfigurera jail med TrueNAS GUI

1. Välj Jails från huvudskärmen.

1. Klicka på LÄGG TILL.

1. Klicka på Avancerad skapelse av jail.

1. Namn (valfritt namn fungerar): Radarr.

1. Jailtyp: Standard (klonad jail).

1. Version: 12.2-Release (eller senare).

1. Konfigurera grundläggande egenskaper efter eget tycke.

1. Konfigurera jail-egenskaper efter eget tycke, men lägg till:

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` är användbart för felsökning (t.ex. ping, traceroute) men är inte ett krav. {.is-info}

1. Konfigurera nätverksegenskaper efter eget tycke.

1. Konfigurera anpassade egenskaper efter eget tycke.

1. Klicka på Spara.

1. När jailen har skapats startar den automatiskt. En till egenskap måste ställas in för att Radarr ska kunna se lagringsutrymmet för dina monterade medieplatser. Öppna en rotshell på servern och ange följande kommandon:

```shell
iocage stop <jailnamn>
iocage set enforce_statfs=1 <jailnamn>
iocage start <jailnamn>
```

## Installation av Radarr

Gå tillbaka till jail-listan och hitta den nyss skapade jailen för `radarr` och klicka på `Shell`.

För att installera Radarr:

> \* Se till att din pkg-repo är konfigurerad för att hämta paket från `/latest` och inte `/quarterly`.
> \* Kontrollera `/usr/local/etc/pkg/repos/FreeBSD.conf`.
> \* Om den inte finns, kopiera över `/etc/pkg/FreeBSD.conf` till den platsen, öppna filen och ersätt `quarterly` med `latest`.
{.is-warning}

```shell
pkg install radarr
```

Stäng inte av shellen än, vi har några fler saker att göra!

## Konfigurera Radarr

Nu när vi har installerat det krävs några fler steg.

### Konfigurera tjänsten

Dags att aktivera tjänsten, men innan vi gör det, en notering:

Uppdateraren är inaktiverad som standard. `pkg-message` ger instruktioner om hur du aktiverar uppdateraren, men kom ihåg: detta kan bryta saker som `pkg check -s` och `pkg remove` för Radarr när den inbyggda uppdateraren ersätter filer.

För att aktivera tjänsten:

```shell
sysrc radarr_enable=TRUE
```

Om du inte vill använda användargruppen `radarr` måste du tala om för tjänstefilen vilken användargrupp den ska köras under.

```shell
sysrc radarr_user="ANVÄNDARE_DU_VILL"
```

```shell
sysrc radarr_group="GRUPP_DU_VILL"
```

`radarr` lagrar sina data, konfiguration, loggar och PID-filer i `/usr/local/radarr` som standard. Tjänstefilen kommer att skapa detta och ta ägarskap av det OM OCH ENDAST OM DET INTE REDAN FINNS. Om du vill lagra dessa filer på en annan plats (t.ex. en dataset monterad i jailen för enklare ögonblicksbilder) måste du ändra det med hjälp av `sysrc`.

```shell
sysrc radarr_data_dir="MAPP_DU_VILL"
```

Påminnelse: Om du använder en befintlig plats måste du manuellt antingen ändra ägarskapet till UID/GID som `radarr` använder OCH/ELLER lägga till `radarr` i en GID som har skrivåtkomst.

Nästan klart, låt oss starta tjänsten:

```shell
service radarr start
```

Om allt gick enligt planen ska Radarr vara igång och köra på jailens IP-adress (port 7878)!

Du kan nu tryggt stänga av shellen.

## Felsökning

- Tjänsten verkar vara igång men användargränssnittet laddas inte eller sidan tar för lång tid att ladda.
  - Dubbelkolla att `allow_mlock` är aktiverat i jailen.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Se till att du har `VNET` aktiverat för din jail, ip6=inherit eller ip6=new.

> Tjänsteskriptet bör nu fungera även utan VNET och/eller IP6 och därmed ta bort kravet på VNET eller ip6=inherit. {.is-info}