---
title: Readarr Windows Installation
description: Windows installationsguide för Readarr
published: true
date: 2023-07-04T15:23:25.114Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:03.495Z
---

# Windows

Readarr stöds nativt på Windows. Readarr kan installeras på Windows som antingen en Windows-tjänst eller en applikation i systemfältet.
> Windows-versioner har begränsat stöd och omfattar endast de versioner som för närvarande stöds av Microsoft. Andra versioner kan fungera, men detta är en konfiguration som inte stöds
{.is-warning}

En Windows-tjänst körs även när användaren inte är inloggad, men särskild försiktighet måste tas eftersom Windows-tjänster [inte kan komma åt nätverksenheter](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ mappade enheter eller \\\server\share UNC-sökvägar) utan särskilda konfigurationssteg.

Dessutom körs Windows-tjänsten under kontot 'Local Service'. Som standard har detta konto **inte behörighet att komma åt användarens hemkatalog om inte behörigheter har tilldelats manuellt**. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemkatalog.

Det är därför rekommenderat att installera Readarr som en applikation i systemfältet om användaren kan förbli inloggad. Alternativet att göra detta erbjuds under installationsprogrammet.

> Du kan behöva köra "Som administratör" en gång efter installationen om du får ett åtkomstfel - till exempel att åtkomst till sökvägen `C:\ProgramData\Readarr\config.xml` nekas - eller om du använder mappade nätverksenheter. Detta ger Readarr de behörigheter som behövs. Du bör inte behöva köra som administratör varje gång.
{.is-warning}

> Varning: Om du kör Plex som en tjänst via [PmsService](https://github.com/cjmurph/PmsService) måste du antingen ändra PMsService-porten från `8787` eller så måste du ändra porten som Readarr körs på i filen `config.xml`.
{.is-info}

1. Ladda ner den senaste versionen av Readarr för din arkitektur via länkarna nedan.
1. Kör installationsprogrammet.
1. Surfa till <http://localhost:8787> för att börja använda Readarr.

- [Windows x64 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det är möjligt att installera Readarr manuellt genom att använda [x64 .zip-nedladdningen](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64). I det fallet måste du dock manuellt hantera beroenden, installation och behörigheter.
{.is-info}