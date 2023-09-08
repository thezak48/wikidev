---
title: Radarr Windows Installation
description: Windows installationsguide til Radarr
published: true
date: 2023-07-04T15:22:03.589Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:19.928Z
---

# Windows

Radarr understøttes naturligt på Windows. Radarr kan installeres på Windows som enten en Windows Service eller en systembakke-applikation.
> Windows-versioner er kun understøttet for dem, der i øjeblikket understøttes af Microsoft. Andre versioner kan virke, men dette er en ikke-understøttet konfiguration
{.is-warning}

En Windows Service kører selv når brugeren ikke er logget ind, men der skal tages særlige forholdsregler, da Windows Services [ikke kan få adgang til netværksdrev](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ mappet drev eller \\\server\share UNC-stier) uden særlige konfigurationsforanstaltninger.

Derudover kører Windows Service under kontoen 'Local Service', som som standard **ikke har tilladelse til at få adgang til brugerens hjemmemappe, medmindre der er tildelt tilladelser manuelt**. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.

Derfor anbefales det at installere Radarr som en systembakke-applikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette gives under installationsprogrammet.

> Du skal muligvis køre "Som administrator" en gang efter installationen, hvis du får en adgangsfejl - f.eks. Adgang til stien `C:\ProgramData\Radarr\config.xml` er nægtet - eller hvis du bruger mappet netværksdrev. Dette giver Radarr de nødvendige tilladelser. Du skal ikke køre Som administrator hver gang.
{.is-warning}

1. Download den nyeste version af Radarr til din arkitektur ved at følge nedenstående links.
1. Kør installationsprogrammet.
1. Gå til <http://localhost:7878> for at begynde at bruge Radarr.

- [Windows x64 Installer](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det er muligt at installere Radarr manuelt ved hjælp af [x64 .zip-downloaden](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). I så fald skal du dog manuelt håndtere afhængigheder, installation og tilladelser.
{.is-info}