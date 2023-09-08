---
title: Readarr Windows-installasjon
description: Veiledning for Windows-installasjon av Readarr
published: true
date: 2023-07-04T15:23:25.114Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:03.495Z
---

# Windows

Readarr støttes naturlig på Windows. Readarr kan installeres på Windows som enten en Windows-tjeneste eller en systemstatusapplikasjon.
> Støtten for Windows-versjoner er begrenset til de som for øyeblikket støttes av Microsoft. Andre versjoner kan fungere, men dette er en konfigurasjon som ikke støttes
{.is-warning}

En Windows-tjeneste kjører selv når brukeren ikke er logget på, men spesiell oppmerksomhet må tas siden Windows-tjenester [ikke kan få tilgang til nettverksstasjoner](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\-mappede stasjoner eller \\\server\share UNC-stier) uten spesielle konfigurasjonstrinn.

I tillegg kjører Windows-tjenesten under kontoen 'Local Service'. Som standard har denne kontoen **ikke tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt**. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.

Det anbefales derfor å installere Readarr som en systemstatusapplikasjon hvis brukeren kan være logget på. Du får muligheten til å gjøre dette under installasjonen.

> Du må kanskje kjøre "Som administrator" én gang etter installasjonen hvis du får en tilgangsfeil - for eksempel at tilgangen til banen `C:\ProgramData\Readarr\config.xml` er nektet - eller hvis du bruker mappede nettverksstasjoner. Dette gir Readarr de nødvendige tillatelsene. Du bør ikke trenge å kjøre Som administrator hver gang.
{.is-warning}

> Advarsel: Hvis du kjører Plex som en tjeneste via [PmsService](https://github.com/cjmurph/PmsService), må du enten endre PMsService-porten fra `8787`, eller så må du endre porten som Readarr kjører på i `config.xml`-filen.
{.is-info}

1. Last ned den nyeste versjonen av Readarr for din arkitektur via lenkene nedenfor.
1. Kjør installasjonsprogrammet.
1. Gå til <http://localhost:8787> for å begynne å bruke Readarr.

- [Windows x64 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det er mulig å installere Readarr manuelt ved å bruke [x64 .zip-nedlastingen](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64). I så fall må du imidlertid håndtere avhengigheter, installasjon og tillatelser manuelt.
{.is-info}