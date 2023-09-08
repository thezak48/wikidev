---
title: Radarr Windows Installation
description: Windows installationsguide för Radarr
published: true
date: 2023-07-04T15:22:03.589Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:19.928Z
---

# Windows

Radarr stöds nativt på Windows. Radarr kan installeras på Windows som antingen en Windows-tjänst eller en applikation i systemfältet.
> Windows-versioner är begränsade till de som för närvarande stöds av Microsoft. Andra versioner kan fungera, men detta är en konfiguration som inte stöds
{.is-warning}

En Windows-tjänst körs även när användaren inte är inloggad, men särskild försiktighet måste tas eftersom Windows-tjänster [inte kan komma åt nätverksenheter](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ mappade enheter eller \\\server\share UNC-sökvägar) utan särskilda konfigurationssteg.

Dessutom körs Windows-tjänsten under kontot 'Local Service'. Som standard har detta konto **inte behörighet att komma åt användarens hemkatalog om inte behörigheter har tilldelats manuellt**. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemkatalog.

Det är därför rekommenderat att installera Radarr som en applikation i systemfältet om användaren kan förbli inloggad. Alternativet att göra detta tillhandahålls under installationsprogrammet.

> Du kan behöva köra "Som administratör" en gång efter installationen om du får ett åtkomstfel - till exempel "Åtkomst nekad" till sökvägen `C:\ProgramData\Radarr\config.xml` - eller om du använder mappade nätverksenheter. Detta ger Radarr de behörigheter som behövs. Du bör inte behöva köra som administratör varje gång.
{.is-warning}

1. Ladda ner den senaste versionen av Radarr för din arkitektur genom länken nedan.
1. Kör installationsprogrammet.
1. Surfa till <http://localhost:7878> för att börja använda Radarr.

- [Windows x64 Installer](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det är möjligt att installera Radarr manuellt genom att använda [x64 .zip-nedladdningen](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). I det fallet måste du dock manuellt hantera beroenden, installation och behörigheter.
{.is-info}