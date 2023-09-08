---
title: Prowlarr Windows-installatie
description: Installatiehandleiding voor Prowlarr op Windows
published: true
date: 2023-08-28T19:43:08.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:39.779Z
---

# Windows

Prowlarr wordt native ondersteund op Windows. Prowlarr kan op Windows worden geïnstalleerd als een Windows-service of een systeemvaktoepassing.
> Windows-versies worden alleen ondersteund voor de versies die momenteel worden ondersteund door Microsoft. Andere versies kunnen werken, maar dit is een niet-ondersteunde configuratie.
{.is-warning}

Een Windows-service wordt uitgevoerd, zelfs wanneer de gebruiker niet is ingelogd.
Als de gebruiker ingelogd kan blijven, kan er ook een systeemvaktoepassing worden gebruikt. Deze optie wordt tijdens de installatie aangeboden.

> Het kan zijn dat je na de installatie eenmaal "Als administrator" moet uitvoeren als je een toegangsfout krijgt, zoals "Toegang tot het pad 'C:\ProgramData\Prowlarr\config.xml' is geweigerd". Hiermee geeft je Prowlarr de benodigde machtigingen. Je hoeft niet elke keer "Als administrator" uit te voeren.
{.is-warning}

1. Download de nieuwste versie van Prowlarr voor jouw architectuur via onderstaande links.
1. Voer de installatie uit.
1. Ga naar <http://localhost:9696> om Prowlarr te gebruiken.

- [Windows x64 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Het is mogelijk om Prowlarr handmatig te installeren met behulp van de [x64 .zip-download](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). In dat geval moet je echter handmatig omgaan met afhankelijkheden, installatie en machtigingen.
{.is-info}

> Als je [Certify The Web](https://docs.certifytheweb.com/docs/backgroundservice/) gebruikt voor het beheer van LetsEncrypt-certificaten voor IIS en Prowlarr op dezelfde machine installeert, wordt poort `9696` gebruikt door de achtergrondservice. Je moet dan ofwel de luisterpoort van Prowlarr in je `config.xml` wijzigen naar iets anders, ofwel de poort van de Certify The Web-achtergrondservice wijzigen.
{.is-info}