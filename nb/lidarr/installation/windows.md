---
title: Lidarr Windows-installasjon
description: Windows-installasjonsveiledning for Lidarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Windows

Lidarr støttes naturlig på Windows. Lidarr kan installeres på Windows som enten en Windows-tjeneste eller en systemstatusapplikasjon.
> Støtten for Windows-versjoner er begrenset til de som for øyeblikket støttes av Microsoft. Andre versjoner kan fungere, men dette er en konfigurasjon som ikke støttes
{.is-warning}

En Windows-tjeneste kjører selv når brukeren ikke er logget på, men spesiell oppmerksomhet må tas siden Windows-tjenester [ikke kan få tilgang til nettverksstasjoner](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ kartlagte stasjoner eller \\\server\share UNC-stier) uten spesielle konfigurasjonstrinn.

I tillegg kjører Windows-tjenesten under kontoen 'Local Service'. Som standard har denne kontoen **ikke tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt**. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.

Det anbefales derfor å installere Lidarr som en systemstatusapplikasjon hvis brukeren kan være logget på. Du får muligheten til å gjøre dette under installasjonen.

> Du må kanskje kjøre "Som administrator" én gang etter installasjonen i systemstatusmodus hvis du får en tilgangsfeil - for eksempel at tilgangen til banen `C:\ProgramData\Lidarr\config.xml` er nektet - eller hvis du bruker kartlagte nettverksstasjoner. Dette gir Lidarr de nødvendige tillatelsene. Du trenger ikke å kjøre som administrator hver gang.
{.is-warning}

1. Last ned den nyeste versjonen av Lidarr for arkitekturen din via lenkene nedenfor.
1. Kjør installasjonsprogrammet.
1. Gå til <http://localhost:8686> for å begynne å bruke Lidarr.

- [Windows x64 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det er mulig å installere Lidarr manuelt ved å bruke [x64 .zip-nedlastingen](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). I så fall må du imidlertid håndtere avhengigheter, installasjon og tillatelser manuelt.
{.is-info}