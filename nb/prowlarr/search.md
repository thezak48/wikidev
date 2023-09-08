---
title: Prowlarr Søk
description: 
published: true
date: 2022-01-02T23:05:56.758Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:31:53.221Z
---

Denne siden vil vise deg hvordan du utfører et søk fra Prowlarr. Generelt sett vil søkene dine bli gjort via appen, men det er også mulig å gjøre dem direkte i Prowlarr.

# Utføre et søk

For å starte et søk, klikk på `Søk` i venstre meny. Det vil være en stort sett tom side med noen alternativer nederst på skjermen.

![search_1_searchscreen.png](/assets/prowlarr/search_1_searchscreen.png)

- Spørring - Skriv inn søkeordene dine i Spørring-feltet.
  - Klikk på forstørrelsesglasset for å endre søketype. Tilgjengelige alternativer er:
    - Grunnleggende søk - Grunnleggende tekstspørring
    - TV-søk - Søk ved hjelp av TV-parametere som vises i brukergrensesnittet, inkludert ID-baserte søk (TVDbId, IMDbId, TMDbID, osv.) og sesong/episodesøk
    - Film-søk - Søk ved hjelp av film-parametere som vises i brukergrensesnittet, inkludert ID-baserte søk (TMDbId, IMDbId, Sjanger, osv.)
    - Lyd-søk - Søk ved hjelp av musikk-parametere som vises i brukergrensesnittet, inkludert Artist, Album, Plateselskap, Sjanger, osv.
    - Bok-søk - Søk ved hjelp av bok-parametere som vises i brukergrensesnittet, inkludert forfatter, tittel, osv.

> Disse er generelt formatert som `{VariabelNavn:Søkeverdi}` f.eks. For et TV-søk etter The Simpsons sesong 32, vil søkeinndataene være `{TvdbId:71663} {Season:32}`
{.is-info}

> Merk at ikke alle Indekseringsverktøy støtter alle typer spørringer {.is-info}

- Indekseringsverktøy - Velg indekseringsverktøyene dine i rullegardinmenyen for Indekseringsverktøy. Du kan merke av for "Usenet" eller "Torrents" for å velge alle indekseringsverktøyene i de kategoriene automatisk, eller du kan velge spesifikke indekseringsverktøy for søket ditt fra begge gruppene.
- Kategori - Velg kategoriene du vil søke etter på indekseringsverktøyene dine fra rullegardinmenyen. Du kan velge toppnivåkategorier (TV, Filmer, osv.) for å velge alle underkategoriene automatisk, eller du kan velge spesifikke kategorier fra noen av gruppene.

Klikk deretter på `Søk`-knappen. Resultatene dine kan ta noen sekunder å vises. Når de vises, kan du legge til eller fjerne kolonner ved å bruke `Alternativer`-knappen, og du kan sortere og filtrere resultatene dine ved å klikke på kolonneoverskriftene eller bruke `Filter`-knappen.

Du kan laste ned resultatet ved å klikke på nedlastingsikonet til høyre for resultatet. Dette vil sende det til riktig nedlastingsklient du har konfigurert.

Du kan ta tak i flere resultater samtidig ved å merke av i avmerkingsboksene på venstre side og trykke på `Hent utgivelser`-knappen.

> Alt som blir lastet ned, vil ha kategoritildelingen du har satt i Prowlarr. Dette kan kreve en manuell import i app-programmet ditt fra en ikke-standard mappe! {.is-info}

# API-sluttpunkter

## RSS-kompatibel - Enkelt indekseringsverktøy-feed

- Standard Newznab/Torznab-kompatibelt sluttpunkt/parametere. Du kan justere spørringene i henhold til dine behov i henhold til de definerte standardene.

> Et aggregert fler-indekseringsverktøy-sluttpunkt vil ikke bli lagt til på grunn av de betydelige ulempene ved en slik funksjonalitet {.is-info}

### API-nøkkel i spørring

- `http://{prowlarrvert}:{prowlarrport}/{baseurl}/{indekseringsverktøyid}/api?t=search&q={term}&apikey={din nøkkel}&cat={kommaseparert liste}`
  - f.eks. `http://192.168.1.100:9696/11/api?t=search&q=mike&apikey={din nøkkel}&cat=5000,2000`

### API-nøkkel i overskrift

> Pass på å sende med `X-Api-Key` med API-nøkkelen som en overskrift {.is-info}

- `http://{prowlarrvert}:{prowlarrport}/{baseurl}/{indekseringsverktøyid}/api?t=search&q={term}&apikey={din nøkkel}&cat={kommaseparert liste}`
  - f.eks. `http://192.168.1.100:9696/{indekseringsverktøyid}/api?t=search&q=mike&cat=5000,2000`

## Søke-feed

- `http://{prowlarrvert}:{prowlarrport}/{baseurl}/api/v1/search?query={kodet term}&indexerIds={kommaseparert liste}&categories={kommaseparert liste}&type={søketype}`
  - f.eks. `http://192.168.1.100/prowlarr/api/v1/search?query=black%20hawk%20down&indexerIds=-1&categories=2000&type=search`
  - f.eks. `http://192.168.1.100/prowlarr/api/v1/search?query=%7BTvdbId%3A71663%7D%20%7BSeason%3A32%7D&categories=5000&type=tvsearch`

Parametere

- `query` - URL-kodet søkestreng
- `indexerIds` - kommaseparert liste over indekseringsverktøy-ID
  - La parameteren være borte fra URL-en for alle indekseringsverktøy
  - `-2` er alle torrents
  - `-1` er all usenet
  - Indekseringsverktøy-ID-er
- `categories` - kommaseparert liste over kategorier som skal brukes
  - la parameteren være borte for alle
- `type` - søketype å utføre
  - `search` - Grunnleggende tekstspørring
  - `tvsearch` - TV-spørring - Støtter TV-parametere
  - `moviesearch` - Film-spørring - Støtter film-parametere
  - `audiosearch` - Lyd/musikk-spørring - Støtter musikk-parametere
  - `booksearch` - Bok-spørring - Støtter bok-parametere