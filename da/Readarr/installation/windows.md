---
title: Readarr Windows Installation
description: Windows installationsguide til Readarr
published: true
date: 2023-07-04T15:23:25.114Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:03.495Z
---

# Windows

Readarr understøttes naturligt på Windows. Readarr kan installeres på Windows som enten en Windows-tjeneste eller en systembakke-applikation.
> Windows-versioner er kun begrænset til understøttelse af dem, der i øjeblikket understøttes af Microsoft. Andre versioner kan virke, men dette er en ikke-understøttet konfiguration
{.is-warning}

En Windows-tjeneste kører selv når brugeren ikke er logget ind, men der skal tages særlige forholdsregler, da Windows-tjenester [ikke kan få adgang til netværksdrev](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\ mappet drev eller \\\server\share UNC-stier) uden særlige konfigurationssteps.

Derudover kører Windows-tjenesten under kontoen 'Local Service'. Som standard har denne konto **ikke tilladelse til at få adgang til din brugers hjemmemappe, medmindre der er tildelt tilladelser manuelt**. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.

Derfor anbefales det at installere Readarr som en systembakke-applikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette gives under installationsprogrammet.

> Du skal muligvis køre "Som administrator" én gang efter installationen, hvis du får en adgangsfejl - som f.eks. Adgang til stien `C:\ProgramData\Readarr\config.xml` er nægtet - eller hvis du bruger mappet netværksdrev. Dette giver Readarr de nødvendige tilladelser. Du behøver ikke at køre Som administrator hver gang.
{.is-warning}

> Advarsel: Hvis du kører Plex som en tjeneste via [PmsService](https://github.com/cjmurph/PmsService), skal du enten ændre PMsServices port fra `8787`, eller du skal ændre den port, som Readarr kører på i `config.xml`-filen.
{.is-info}

1. Download den nyeste version af Readarr til din arkitektur via linkene nedenfor.
1. Kør installationsprogrammet.
1. Gå til <http://localhost:8787> for at begynde at bruge Readarr.

- [Windows x64 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det er muligt at installere Readarr manuelt ved hjælp af [x64 .zip-downloaden](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64). I så fald skal du dog manuelt håndtere afhængigheder, installation og tilladelser.
{.is-info}