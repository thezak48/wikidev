---
title: Prowlarr Windows-installasjon
description: Veiledning for Windows-installasjon av Prowlarr
published: true
date: 2023-08-28T19:43:08.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:39.779Z
---

# Windows

Prowlarr støttes nativt på Windows. Prowlarr kan installeres på Windows som enten en Windows-tjeneste eller en systemstatusapplikasjon.
> Støtten for Windows-versjoner er begrenset til de som for øyeblikket støttes av Microsoft. Andre versjoner kan fungere, men dette er en konfigurasjon som ikke støttes
{.is-warning}

En Windows-tjeneste kjører selv når brukeren ikke er logget inn.
Alternativt kan en systemstatusapplikasjon brukes hvis brukeren kan være logget inn. Muligheten til å gjøre dette tilbys under installasjonsprogrammet.

> Du må kanskje kjøre "Som administrator" én gang etter installasjonen hvis du får en tilgangsfeil som f.eks. "Tilgang til banen `C:\ProgramData\Prowlarr\config.xml` er nektet". Dette gir Prowlarr de nødvendige tillatelsene. Du bør ikke trenge å kjøre som administrator hver gang.
{.is-warning}

1. Last ned den nyeste versjonen av Prowlarr for din arkitektur fra lenkene nedenfor.
1. Kjør installasjonsprogrammet.
1. Gå til <http://localhost:9696> for å begynne å bruke Prowlarr.

- [Windows x64 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Det er mulig å installere Prowlarr manuelt ved å bruke [x64 .zip-nedlastingen](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). I så fall må du manuelt håndtere avhengigheter, installasjon og tillatelser.
{.is-info}

> Hvis du bruker [Certify The Web](https://docs.certifytheweb.com/docs/backgroundservice/) for LetsEncrypt-sertifikatstyring for IIS og installerer Prowlarr på samme maskin, brukes port `9696` av bakgrunnstjenesten. Du må enten endre lytteporten til Prowlarr i `config.xml` til noe annet, eller endre porten til Certify The Web-bakgrunnstjenesten.
{.is-info}