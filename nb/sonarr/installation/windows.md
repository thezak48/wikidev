---
title: Sonarr Windows-installasjon
description: Veiledning for Windows-installasjon av Sonarr
published: true
date: 2023-07-04T15:22:44.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:54.851Z
---

# Windows

Sonarr støttes naturlig på Windows. Sonarr kan installeres på Windows som enten en Windows-tjeneste eller en systemstatusapplikasjon.

> Støtten for Windows-versjoner er begrenset til de som for øyeblikket støttes av Microsoft. Andre versjoner kan fungere, men dette er en konfigurasjon som ikke støttes.
{.is-warning}

En Windows-tjeneste kjører selv når brukeren ikke er logget på, men spesiell oppmerksomhet må tas siden Windows-tjenester [ikke kan få tilgang til nettverksstasjoner](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ kartlagte stasjoner eller \\\server\share UNC-stier) uten spesielle konfigurasjonstrinn.

I tillegg kjører Windows-tjenesten under kontoen 'Local Service'. Som standard har denne kontoen **ikke tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt**. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.

Det anbefales derfor å installere Sonarr som en systemstatusapplikasjon hvis brukeren kan være logget på. Du får muligheten til å gjøre dette under installasjonen.

> Du må kanskje kjøre "Som administrator" én gang etter installasjonen hvis du får en tilgangsfeil - for eksempel at tilgangen til banen `C:\ProgramData\Sonarr\config.xml` er nektet - eller hvis du bruker kartlagte nettverksstasjoner. Dette gir Sonarr de nødvendige tillatelsene. Du bør ikke trenge å kjøre Som administrator hver gang.
{.is-warning}

1. Last ned den nyeste versjonen av Sonarr for din arkitektur fra lenken nedenfor.
1. Kjør installasjonsprogrammet.
1. Gå til <http://localhost:8989> for å begynne å bruke Sonarr.

- [Windows x32 Installer](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows&installer=true)
{.links-list}

> Det er mulig å installere Sonarr manuelt ved å bruke [x32 .zip-nedlastingen](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows). I så fall må du imidlertid håndtere avhengigheter, installasjon og tillatelser manuelt.
{.is-info}