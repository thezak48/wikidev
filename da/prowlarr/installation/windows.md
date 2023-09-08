---
title: Prowlarr Windows Installation
description: Windows installationsguide til Prowlarr
published: true
date: 2023-08-28T19:43:08.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:39.779Z
---

# Windows

Prowlarr understøttes nativt på Windows. Prowlarr kan installeres på Windows som enten en Windows Service eller en systembakke-applikation.
> Supporten til Windows-versioner er begrænset til dem, der i øjeblikket understøttes af Microsoft. Andre versioner kan virke, men dette er en ikke-understøttet konfiguration.
{.is-warning}

En Windows Service kører selv når brugeren ikke er logget ind.
Alternativt kan en systembakke-applikation bruges, hvis brugeren kan forblive logget ind. Denne mulighed tilbydes under installationen.

> Du skal muligvis køre programmet én gang som administrator efter installationen, hvis du får en adgangsfejl som f.eks. "Adgang til stien `C:\ProgramData\Prowlarr\config.xml` blev nægtet". Dette giver Prowlarr de nødvendige tilladelser. Du skal ikke køre programmet som administrator hver gang.
{.is-warning}

1. Download den nyeste version af Prowlarr til din arkitektur ved at følge nedenstående links.
1. Kør installationsprogrammet.
1. Gå til <http://localhost:9696> for at begynde at bruge Prowlarr.

- [Windows x64 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det er muligt at installere Prowlarr manuelt ved at downloade [x64 .zip-filen](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). I så fald skal du dog manuelt håndtere afhængigheder, installation og tilladelser.
{.is-info}

> Hvis du bruger [Certify The Web](https://docs.certifytheweb.com/docs/backgroundservice/) til LetsEncrypt-certifikatstyring for IIS og installerer Prowlarr på samme maskine, bruger baggrundstjenesten port `9696`. Du skal enten ændre Prowlarrs lytteport i din `config.xml` til noget andet eller ændre porten for Certify The Web-baggrundstjenesten.
{.is-info}