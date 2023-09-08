---
title: Readarr Windows Installatie
description: Installatiehandleiding voor Readarr op Windows
published: true
date: 2023-07-04T15:23:25.114Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:03.495Z
---

# Windows

Readarr wordt native ondersteund op Windows. Readarr kan op Windows worden geïnstalleerd als een Windows-service of als een systeemvaktoepassing.
> Windows-versies worden alleen ondersteund voor de versies die momenteel worden ondersteund door Microsoft. Andere versies kunnen werken, maar dit is een niet-ondersteunde configuratie.
{.is-warning}

Een Windows-service wordt uitgevoerd, zelfs wanneer de gebruiker niet is ingelogd, maar er moet speciale aandacht worden besteed omdat Windows-services [geen toegang hebben tot netwerkstations](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ toegewezen stations of \\\server\share UNC-paden) zonder speciale configuratiestappen.

Daarnaast wordt de Windows-service uitgevoerd onder het account 'Local Service'. Standaard heeft dit account **geen toestemming om toegang te krijgen tot de thuismap van de gebruiker, tenzij er handmatig toestemming is gegeven**. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw thuismap.

Daarom is het raadzaam om Readarr als een systeemvaktoepassing te installeren als de gebruiker ingelogd kan blijven. Deze optie wordt tijdens de installatie aangeboden.

> Het kan zijn dat u na de installatie eenmaal "Als administrator" moet uitvoeren als u een toegangsfout krijgt, zoals Toegang tot het pad `C:\ProgramData\Readarr\config.xml` is geweigerd, of als u gebruikmaakt van toegewezen netwerkstations. Hiermee geeft u Readarr de benodigde machtigingen. U hoeft niet elke keer als administrator uit te voeren.
{.is-warning}

> Waarschuwing: Als u Plex als een service uitvoert via [PmsService](https://github.com/cjmurph/PmsService), moet u ofwel de poort van PMsService wijzigen van `8787` of u moet de poort wijzigen waarop Readarr wordt uitgevoerd in het `config.xml`-bestand.
{.is-info}

1. Download de nieuwste versie van Readarr voor uw architectuur via onderstaande links.
1. Voer de installatie uit.
1. Ga naar <http://localhost:8787> om Readarr te gebruiken.

- [Windows x64 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Het is mogelijk om Readarr handmatig te installeren met behulp van de [x64 .zip-download](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64). In dat geval moet u echter handmatig omgaan met afhankelijkheden, installatie en machtigingen.
{.is-info}