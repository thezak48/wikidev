---
title: Readarr FreeBSD Installatie
description: Installatiehandleiding voor Readarr op FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Het Readarr-team biedt alleen builds aan voor FreeBSD. Plugins en Ports worden onderhouden en gemaakt door de FreeBSD-community.

Instructies voor FreeBSD-installaties worden ook onderhouden door de FreeBSD-community en iedereen met een GitHub-account kan de wiki indien nodig bijwerken.

[Freshports Readarr Link](https://www.freshports.org/net-p2p/readarr/)

## Jail-instellingen met behulp van TrueNAS GUI

1. Selecteer Jails vanaf het hoofdscherm.

1. Klik op TOEVOEGEN.

1. Klik op Geavanceerde jail-creatie.

1. Naam (elke naam werkt): Readarr.

1. Jailtype: Standaard (Kloonjail).

1. Release: 12.2-Release (of nieuwer).

1. Configureer de basisinstellingen naar wens.

1. Configureer de jail-eigenschappen naar wens, maar voeg het volgende toe:

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` is handig voor probleemoplossing (bijv. ping, traceroute), maar is niet vereist. {.is-info}

1. Configureer de netwerkeigenschappen naar wens.

1. Configureer de aangepaste eigenschappen naar wens.

1. Klik op Opslaan.

1. Nadat de jail is aangemaakt, wordt deze automatisch gestart. Er moet nog één eigenschap worden ingesteld zodat Readarr de opslagruimte van uw gemonteerde media-locaties kan zien. Open een root-shell op de server en voer deze commando's in:

```shell
iocage stop <jailnaam>
iocage set enforce_statfs=1 <jailnaam>
iocage start <jailnaam>
```

## Readarr-installatie

Zoek op de jail-lijst uw nieuw aangemaakte jail voor `readarr` en klik op "Shell".

Om Readarr te installeren:

> \* Zorg ervoor dat uw pkg-repo is geconfigureerd om pakketten te krijgen van `/latest` en niet van `/quarterly`
> \* Controleer `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Als dat niet bestaat, kopieer dan `/etc/pkg/FreeBSD.conf` naar die locatie, open het en vervang `quarterly` door `latest`
{.is-warning}

```shell
pkg install readarr
```

Sluit de shell nog niet af, we hebben nog een paar dingen te doen!

## Configuratie van Readarr

Nu we het geïnstalleerd hebben, zijn er nog een paar stappen vereist.

### Service-instellingen

Tijd om de service in te schakelen, maar voordat we dat doen, een opmerking:

De updater is standaard uitgeschakeld. Het `pkg-message` geeft instructies over hoe de updater ingeschakeld kan worden, maar houd er rekening mee dat dit dingen kan breken zoals `pkg check -s` en `pkg remove` voor Readarr wanneer de ingebouwde updater bestanden vervangt.

Om de service in te schakelen:

```shell
sysrc readarr_enable=TRUE
```

Als u geen gebruik wilt maken van de gebruiker/groep `readarr`, moet u het servicebestand vertellen onder welke gebruiker/groep het moet worden uitgevoerd.

```shell
sysrc readarr_user="GEBRUIKER_DIE_U_WILT"
```

```shell
sysrc readarr_group="GROEP_DIE_U_WILT"
```

`readarr` slaat zijn gegevens, configuratie, logs en PID-bestanden standaard op in `/usr/local/readarr`. Het servicebestand zal dit maken en de eigenaar ervan worden ALS EN ALLEEN ALS HET NIET BESTAAT. Als u deze bestanden op een andere plaats wilt opslaan (bijv. een dataset die in de jail is gemonteerd voor eenvoudigere snapshots), dan moet u dit wijzigen met behulp van `sysrc`.

```shell
sysrc readarr_data_dir="MAP_DIE_U_WILT"
```

Herinnering: Als u een bestaande locatie gebruikt, moet u handmatig de eigendom wijzigen naar de UID/GID die `readarr` gebruikt EN/OF `readarr` toevoegen aan een GID met schrijftoegang.

Bijna klaar, laten we de service starten:

```shell
service readarr start
```

Als alles volgens plan is verlopen, zou Readarr moeten werken op het IP-adres van de jail (poort 8787)!

U kunt nu veilig de shell sluiten.

## Probleemoplossing

- De service lijkt actief te zijn, maar de gebruikersinterface wordt niet geladen of de pagina loopt vast.
  - Controleer nogmaals of `allow_mlock` is ingeschakeld in de jail.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Zorg ervoor dat u `VNET` hebt ingeschakeld voor uw jail, ip6=inherit of ip6=new.

> Het servicescript zou nu moeten werken zonder VNET en/of IP6, waardoor de vereiste voor VNET of ip6=inherit wordt verwijderd. {.is-info}