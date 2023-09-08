---
title: Lidarr Windows Installatie
description: Windows installatiehandleiding voor Lidarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Windows

Lidarr wordt native ondersteund op Windows. Lidarr kan op Windows worden geïnstalleerd als een Windows-service of een systeemvaktoepassing.
> Windows-versies worden alleen ondersteund voor de versies die momenteel worden ondersteund door Microsoft. Andere versies kunnen werken, maar dit is een niet-ondersteunde configuratie.
{.is-warning}

Een Windows-service wordt uitgevoerd, zelfs wanneer de gebruiker niet is ingelogd, maar er moet speciale aandacht worden besteed omdat Windows-services [geen toegang hebben tot netwerkstations](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ toegewezen stations of \\\server\share UNC-paden) zonder speciale configuratiestappen.

Daarnaast wordt de Windows-service uitgevoerd onder het account 'Local Service'. Standaard heeft dit account **geen toestemming om toegang te krijgen tot de gebruikersmap, tenzij er handmatig toestemming is gegeven**. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw gebruikersmap.

Daarom is het raadzaam om Lidarr te installeren als een systeemvaktoepassing als de gebruiker ingelogd kan blijven. Deze optie wordt tijdens de installatie aangeboden.

> Het kan zijn dat u na de installatie in systeemvakmodus één keer "Als administrator" moet uitvoeren als u een toegangsfout krijgt, zoals Toegang tot het pad `C:\ProgramData\Lidarr\config.xml` is geweigerd, of als u gebruikmaakt van toegewezen netwerkstations. Hiermee krijgt Lidarr de benodigde machtigingen. U hoeft niet elke keer als administrator uit te voeren.
{.is-warning}

1. Download de nieuwste versie van Lidarr voor uw architectuur via onderstaande links.
1. Voer de installatie uit.
1. Ga naar <http://localhost:8686> om Lidarr te gebruiken.

- [Windows x64 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Het is mogelijk om Lidarr handmatig te installeren met behulp van de [x64 .zip-download](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). In dat geval moet u echter handmatig omgaan met afhankelijkheden, installatie en machtigingen.
{.is-info}