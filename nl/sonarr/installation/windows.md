---
title: Sonarr Windows Installatie
description: Installatiehandleiding voor Sonarr op Windows
published: true
date: 2023-07-04T15:22:44.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:54.851Z
---

# Windows

Sonarr wordt native ondersteund op Windows. Sonarr kan op Windows worden geïnstalleerd als een Windows-service of als een toepassing in het systeemvak.

> Windows-versies worden alleen ondersteund voor de versies die momenteel worden ondersteund door Microsoft. Andere versies kunnen werken, maar dit is een niet-ondersteunde configuratie.
{.is-warning}

Een Windows-service wordt uitgevoerd, zelfs wanneer de gebruiker niet is ingelogd, maar er moet speciale aandacht worden besteed omdat Windows-services [geen toegang hebben tot netwerkstations](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ toegewezen stations of \\\server\share UNC-paden) zonder speciale configuratiestappen.

Daarnaast wordt de Windows-service uitgevoerd onder het account 'Local Service'. Standaard heeft dit account **geen toestemming om toegang te krijgen tot de thuismap van de gebruiker, tenzij er handmatig toestemming is gegeven**. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw thuismap.

Daarom is het raadzaam om Sonarr te installeren als een toepassing in het systeemvak als de gebruiker ingelogd kan blijven. Deze optie wordt tijdens de installatie aangeboden.

> Het kan zijn dat u na de installatie eenmaal "Als administrator" moet uitvoeren als u een toegangsfout krijgt, zoals Toegang tot het pad `C:\ProgramData\Sonarr\config.xml` is geweigerd -- of als u gebruikmaakt van toegewezen netwerkstations. Hiermee geeft u Sonarr de benodigde machtigingen. U hoeft niet elke keer als administrator uit te voeren.
{.is-warning}

1. Download de nieuwste versie van Sonarr voor uw architectuur via onderstaande link.
1. Voer het installatieprogramma uit.
1. Ga naar <http://localhost:8989> om Sonarr te gebruiken.

- [Windows x32 Installer](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows&installer=true)
{.links-list}

> Het is mogelijk om Sonarr handmatig te installeren met behulp van de [x32 .zip-download](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows). In dat geval moet u echter handmatig omgaan met afhankelijkheden, installatie en machtigingen.
{.is-info}