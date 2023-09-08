---
title: Sonarr Windows Installation
description: Windows installationsguide för Sonarr
published: true
date: 2023-07-04T15:22:44.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:54.851Z
---

# Windows

Sonarr stöds nativt på Windows. Sonarr kan installeras på Windows som antingen en Windows-tjänst eller en applikation i systemfältet.

> Windows-versioner har begränsat stöd och omfattar endast de versioner som för närvarande stöds av Microsoft. Andra versioner kan fungera, men detta är en konfiguration som inte stöds.
{.is-warning}

En Windows-tjänst körs även när användaren inte är inloggad, men särskild försiktighet måste tas eftersom Windows-tjänster [inte kan komma åt nätverksenheter](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ mappade enheter eller \\\server\share UNC-sökvägar) utan särskilda konfigurationssteg.

Dessutom körs Windows-tjänsten under kontot 'Local Service'. Som standard har detta konto **inte behörighet att komma åt användarens hemkatalog om inte behörigheter har tilldelats manuellt**. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemkatalog.

Det är därför rekommenderat att installera Sonarr som en applikation i systemfältet om användaren kan förbli inloggad. Alternativet att göra detta erbjuds under installationsprogrammet.

> Du kan behöva köra "Som administratör" en gång efter installationen om du får ett åtkomstfel - till exempel "Åtkomst nekad" till sökvägen `C:\ProgramData\Sonarr\config.xml` - eller om du använder mappade nätverksenheter. Detta ger Sonarr de behörigheter som behövs. Du bör inte behöva köra som administratör varje gång.
{.is-warning}

1. Ladda ner den senaste versionen av Sonarr för din arkitektur via länken nedan.
1. Kör installationsprogrammet.
1. Surfa till <http://localhost:8989> för att börja använda Sonarr.

- [Windows x32 Installer](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows&installer=true)
{.links-list}

> Det är möjligt att installera Sonarr manuellt med hjälp av [x32 .zip-nedladdningen](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows). I det fallet måste du dock manuellt hantera beroenden, installation och behörigheter.
{.is-info}