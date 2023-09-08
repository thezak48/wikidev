---
title: Prowlarr FreeBSD-installatie
description: Installatiehandleiding voor Prowlarr op FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Het Prowlarr-team biedt alleen builds aan voor FreeBSD. Plugins en Ports worden onderhouden en gemaakt door de FreeBSD-community.

Instructies voor FreeBSD-installaties worden ook onderhouden door de FreeBSD-community en iedereen met een GitHub-account kan de wiki bijwerken indien nodig.

[Freshports Prowlarr-link](https://www.freshports.org/net-p2p/prowlarr/)

## Jail-instelling met TrueNAS GUI

1. Selecteer Jails vanaf het hoofdscherm.

1. Klik op TOEVOEGEN.

1. Klik op Geavanceerde jail-creatie.

1. Naam (elke naam werkt): Prowlarr.

1. Jailtype: Standaard (Clone Jail).

1. Release: 12.2-Release (of nieuwer).

1. Configureer de basisinstellingen naar wens.

1. Configureer de jail-eigenschappen naar wens, maar voeg het volgende toe:

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` is handig voor probleemoplossing (bijv. ping, traceroute), maar is geen vereiste. {.is-info}

1. Configureer de netwerkeigenschappen naar wens.

1. Configureer de aangepaste eigenschappen naar wens.

1. Klik op Opslaan.

## Prowlarr-installatie

Ga terug naar de lijst met jails en zoek de zojuist aangemaakte jail voor `prowlarr` en klik op "Shell".

Om Prowlarr te installeren:

> \* Zorg ervoor dat uw pkg-repo is geconfigureerd om pakketten te krijgen van `/latest` en niet van `/quarterly`
> \* Controleer `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Als dat niet bestaat, kopieer dan `/etc/pkg/FreeBSD.conf` naar die locatie, open het bestand en vervang `quarterly` door `latest`
{.is-warning}

```shell
pkg install prowlarr
```

Sluit de shell nog niet af, we hebben nog een paar dingen te doen!

## Prowlarr configureren

Nu we het geïnstalleerd hebben, zijn er nog een paar stappen vereist.

### Service-instellingen

Tijd om de service in te schakelen, maar voordat we dat doen, een opmerking:

De updater is standaard uitgeschakeld. Het `pkg-message`-bestand geeft instructies over hoe de updater ingeschakeld kan worden, maar houd er rekening mee dat dit dingen kan breken zoals `pkg check -s` en `pkg remove` voor prowlarr wanneer de ingebouwde updater bestanden vervangt.

Om de service in te schakelen:

```shell
sysrc prowlarr_enable=TRUE
```

Als u geen gebruik wilt maken van de gebruiker/groep `prowlarr`, moet u het servicebestand vertellen onder welke gebruiker/groep het moet worden uitgevoerd.

```shell
sysrc prowlarr_user="GEBRUIKER_DIE_U_WILT"
```

```shell
sysrc prowlarr_group="GROEP_DIE_U_WILT"
```

`prowlarr` slaat zijn gegevens, configuratie, logs en PID-bestanden standaard op in `/usr/local/prowlarr`. Het servicebestand zal dit aanmaken en eigendom ervan nemen ALS EN ALLEEN ALS HET NIET BESTAAT. Als u deze bestanden op een andere plaats wilt opslaan (bijv. een dataset die in de jail is gemount voor eenvoudigere snapshots), dan moet u dit wijzigen met behulp van `sysrc`.

```shell
sysrc prowlarr_data_dir="MAP_DIE_U_WILT"
```

Herinnering: Als u een bestaande locatie gebruikt, moet u handmatig de eigendom wijzigen naar de UID/GID die `prowlarr` gebruikt EN/OF `prowlarr` toevoegen aan een GID met schrijftoegang.

Bijna klaar, laten we de service starten:

```shell
service prowlarr start
```

Als alles volgens plan is verlopen, zou prowlarr moeten werken op het IP-adres van de jail (poort 9696)!

U kunt nu veilig de shell sluiten.

## Problemen oplossen

- De service lijkt actief te zijn, maar de gebruikersinterface wordt niet geladen of de pagina loopt vast.
  - Controleer nogmaals of `allow_mlock` is ingeschakeld in de jail.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Zorg ervoor dat u `VNET` hebt ingeschakeld voor uw jail, ip6=inherit of ip6=new.

> Het servicescript zou nu moeten werken zonder VNET en/of IP6, waardoor de vereiste voor VNET of ip6=inherit wordt verwijderd. {.is-info}