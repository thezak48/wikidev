---
title: Prowlarr Windows Installation
description: Installationsguide för Prowlarr på Windows
published: true
date: 2023-08-28T19:43:08.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:39.779Z
---

# Windows

Prowlarr stöds nativt på Windows. Prowlarr kan installeras på Windows som antingen en Windows-tjänst eller en systemfältapplikation.
> Stöd för Windows-versioner är begränsat till de som för närvarande stöds av Microsoft. Andra versioner kan fungera, men detta är en konfiguration som inte stöds
{.is-warning}

En Windows-tjänst körs även när användaren inte är inloggad.
Annars kan en systemfältapplikation användas om användaren kan förbli inloggad. Alternativet att göra detta tillhandahålls under installationen.

> Du kan behöva köra "Som administratör" en gång efter installationen om du får ett åtkomstfel som till exempel "Åtkomst nekad" för sökvägen `C:\ProgramData\Prowlarr\config.xml`. Detta ger Prowlarr de behörigheter den behöver. Du bör inte behöva köra som administratör varje gång.
{.is-warning}

1. Ladda ner den senaste versionen av Prowlarr för din arkitektur via länkarna nedan.
1. Kör installationsprogrammet.
1. Surfa till <http://localhost:9696> för att börja använda Prowlarr.

- [Windows x64 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det är möjligt att installera Prowlarr manuellt genom att använda [x64 .zip nedladdningen](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). I det fallet måste du dock manuellt hantera beroenden, installation och behörigheter.
{.is-info}

> Om du använder [Certify The Web](https://docs.certifytheweb.com/docs/backgroundservice/) för LetsEncrypt-certifikatshantering för IIS och installerar Prowlarr på samma dator, används port `9696` av bakgrundstjänsten. Du måste antingen ändra lyssningsporten för Prowlarr i din `config.xml` till något annat eller ändra porten för Certify The Web-bakgrundstjänsten.
{.is-info}