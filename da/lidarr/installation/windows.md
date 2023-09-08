---
title: Lidarr Windows Installation
description: Windows installationsguide til Lidarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Windows

Lidarr understøttes naturligt på Windows. Lidarr kan installeres på Windows som enten en Windows Service eller en systembakke-applikation.
> Windows-versioner er kun begrænset til support for dem, der i øjeblikket understøttes af Microsoft. Andre versioner kan fungere, men dette er en ikke-understøttet konfiguration.
{.is-warning}

En Windows Service kører selv når brugeren ikke er logget ind, men der skal tages særlige forholdsregler, da Windows Services [ikke kan få adgang til netværksdrev](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ mappet drev eller \\\server\share UNC-stier) uden særlige konfigurationssteps.

Derudover kører Windows Service under kontoen 'Local Service'. Som standard har denne konto **ikke tilladelse til at få adgang til brugerens hjemmemappe, medmindre der er tildelt tilladelser manuelt**. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.

Derfor anbefales det at installere Lidarr som en systembakke-applikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette tilbydes under installationen.

> Du skal muligvis køre "Som administrator" en gang efter installationen i bakke-tilstand, hvis du får en adgangsfejl - f.eks. Adgang til stien `C:\ProgramData\Lidarr\config.xml` er nægtet - eller hvis du bruger mappet netværksdrev. Dette giver Lidarr de nødvendige tilladelser. Du behøver ikke at køre Som administrator hver gang.
{.is-warning}

1. Download den nyeste version af Lidarr til din arkitektur, som er linket nedenfor.
1. Kør installationsprogrammet.
1. Gå til <http://localhost:8686> for at begynde at bruge Lidarr.

- [Windows x64 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det er muligt at installere Lidarr manuelt ved hjælp af [x64 .zip-downloaden](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). I så fald skal du dog manuelt håndtere afhængigheder, installation og tilladelser.
{.is-info}