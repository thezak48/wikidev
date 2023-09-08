---
title: Lidarr Windows Installation
description: Windows installationsguide för Lidarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Windows

Lidarr stöds nativt på Windows. Lidarr kan installeras på Windows som antingen en Windows-tjänst eller en applikation i systemfältet.
> Windows-versioner är begränsade till de som för närvarande stöds av Microsoft. Andra versioner kan fungera, men det är en konfiguration som inte stöds
{.is-warning}

En Windows-tjänst körs även när användaren inte är inloggad, men särskild försiktighet måste tas eftersom Windows-tjänster [inte kan komma åt nätverksenheter](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ mappade enheter eller \\\server\share UNC-sökvägar) utan särskilda konfigurationssteg.

Dessutom körs Windows-tjänsten under kontot 'Local Service'. Som standard har detta konto **inte behörighet att komma åt användarens hemkatalog om inte behörigheter har tilldelats manuellt**. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemkatalog.

Det är därför rekommenderat att installera Lidarr som en applikation i systemfältet om användaren kan förbli inloggad. Alternativet att göra detta erbjuds under installationsprogrammet.

> Du kan behöva köra "Som administratör" en gång efter att du har installerat i systemfältet om du får ett åtkomstfel - till exempel "Åtkomst nekad" för sökvägen `C:\ProgramData\Lidarr\config.xml` - eller om du använder mappade nätverksenheter. Detta ger Lidarr de behörigheter som behövs. Du bör inte behöva köra som administratör varje gång.
{.is-warning}

1. Ladda ner den senaste versionen av Lidarr för din arkitektur genom länkarna nedan.
1. Kör installationsprogrammet.
1. Surfa till <http://localhost:8686> för att börja använda Lidarr.

- [Windows x64 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det är möjligt att installera Lidarr manuellt genom att använda [x64 .zip-nedladdningen](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). I det fallet måste du dock manuellt hantera beroenden, installation och behörigheter.
{.is-info}