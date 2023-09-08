---
title: Sonarr Windows Installation
description: Windows installationsguide til Sonarr
published: true
date: 2023-07-04T15:22:44.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:54.851Z
---

# Windows

Sonarr understøttes naturligt på Windows. Sonarr kan installeres på Windows som enten en Windows Service eller en systembakke-applikation.

> Windows-versioner er kun begrænset til understøttelse af dem, der i øjeblikket understøttes af Microsoft. Andre versioner kan fungere, men dette er en ikke-understøttet konfiguration.
{.is-warning}

En Windows Service kører selv når brugeren ikke er logget ind, men der skal tages særlige forholdsregler, da Windows Services [ikke kan få adgang til netværksdrev](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ mappet drev eller \\\server\share UNC-stier) uden særlige konfigurationssteps.

Derudover kører Windows Service under kontoen 'Local Service', som som standard **ikke har tilladelser til at få adgang til brugerens hjemmemappe, medmindre der er tildelt tilladelser manuelt**. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.

Derfor anbefales det at installere Sonarr som en systembakke-applikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette tilbydes under installationen.

> Du skal muligvis køre "Som administrator" en gang efter installationen, hvis du får en adgangsfejl - f.eks. Adgang til stien `C:\ProgramData\Sonarr\config.xml` er nægtet - eller hvis du bruger mappet netværksdrev. Dette giver Sonarr de nødvendige tilladelser. Du skal ikke køre Som administrator hver gang.
{.is-warning}

1. Download den nyeste version af Sonarr til din arkitektur via linket nedenfor.
1. Kør installationsprogrammet.
1. Gå til <http://localhost:8989> for at begynde at bruge Sonarr.

- [Windows x32 Installer](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows&installer=true)
{.links-list}

> Det er muligt at installere Sonarr manuelt ved hjælp af [x32 .zip-downloaden](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows). I så fald skal du dog manuelt håndtere afhængigheder, installation og tilladelser.
{.is-info}