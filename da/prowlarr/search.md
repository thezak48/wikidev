---
title: Prowlarr Søgning
description: 
published: true
date: 2022-01-02T23:05:56.758Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:31:53.221Z
---

Denne side viser dig, hvordan du udfører en søgning fra Prowlarr. Generelt set vil dine søgninger foregå via appen, men det er også muligt at udføre dem direkte i Prowlarr.

# Udførelse af en søgning

For at starte en søgning skal du klikke på `Søg` i venstre menu. Der vises en stort set tom side med nogle muligheder i bunden af skærmen.

![search_1_searchscreen.png](/assets/prowlarr/search_1_searchscreen.png)

- Forespørgsel - Indtast dine søgetermer i feltet Forespørgsel.
  - Klik på forstørrelsesglasset for at ændre søgetypen. De tilgængelige muligheder er:
    - Grundlæggende søgning - Grundlæggende tekstforespørgsel
    - TV-søgning - Søgning ved hjælp af TV-parametre som vist i brugergrænsefladen, herunder ID-baserede søgninger (TVDbId, IMDbId, TMDbID osv.) og sæson-/episodesøgninger
    - Film-søgning - Søgning ved hjælp af filmparametre som vist i brugergrænsefladen, herunder ID-baserede søgninger (TMDbId, IMDbId, Genre osv.)
    - Lyd-søgning - Søgning ved hjælp af musikparametre som vist i brugergrænsefladen, herunder kunstner, album, label, genre osv.
    - Bog-søgning - Søgning ved hjælp af bogparametre som vist i brugergrænsefladen, herunder forfatter, titel osv.

> Disse er generelt formateret som `{VariabelNavn:SøgeVærdi}` f.eks. For en TV-søgning af The Simpsons sæson 32 ville søgeinputtet være `{TvdbId:71663} {Season:32}`
{.is-info}

> Bemærk, at ikke alle indekser understøtter alle forespørgselstyper {.is-info}

- Indekser - Vælg dine indekser i rullemenuen Indekser. Du kan markere "Usenet" eller "Torrents" for at vælge alle indekser i disse kategorier automatisk, eller du kan vælge specifikke indekser til din søgning fra enten gruppen.
- Kategori - Vælg de kategorier, du vil søge på dine indekser fra rullemenuen. Du kan vælge topniveau-kategorier (TV, film osv.) for at vælge alle underkategorier automatisk, eller du kan vælge specifikke kategorier fra en af grupperne.

Klik derefter på knappen `Søg`. Dine resultater kan tage nogle få sekunder om at blive vist. Når de vises, kan du tilføje eller fjerne kolonner ved hjælp af knappen `Indstillinger`, og du kan sortere og filtrere dine resultater ved enten at klikke på kolonneoverskrifterne eller bruge knappen `Filtrer`.

Du kan downloade resultatet ved at klikke på download-ikonet til højre for resultatet. Dette sender det til den korrekte downloadklient, du har konfigureret.

Du kan også hente flere resultater på én gang ved at markere afkrydsningsfelterne på venstre side og klikke på knappen `Hent udgivelser`.

> Alt, hvad der downloades, vil have den kategori, du har angivet i Prowlarr. Dette kan kræve en manuel import i din app fra en ikke-standard mappe! {.is-info}

# API-slutpunkter

## RSS-kompatibel - Enkelt indekserfeed

- Standard Newznab/Torznab-kompatibelt slutpunkt/parametre. Du kan justere forespørgslerne i overensstemmelse med dine behov i henhold til de definerede standarder.

> Der vil ikke blive tilføjet et samlet multi-indekser-slutpunkt på grund af de betydelige ulemper ved denne funktionalitet {.is-info}

### API-nøgle i forespørgsel

- `http://{prowlarrvært}:{prowlarrport}/{baseurl}/{indekserid}/api?t=search&q={term}&apikey={din nøgle}&cat={kommasepareret liste}`
  - f.eks. `http://192.168.1.100:9696/11/api?t=search&q=mike&apikey={din nøgle}&cat=5000,2000`

### API-nøgle i header

> Sørg for at medsende `X-Api-Key` med API-nøglen som en header {.is-info}

- `http://{prowlarrvært}:{prowlarrport}/{baseurl}/{indekserid}/api?t=search&q={term}&apikey={din nøgle}&cat={kommasepareret liste}`
  - f.eks. `http://192.168.1.100:9696/{indekserid}/api?t=search&q=mike&cat=5000,2000`

## Søgefeed

- `http://{prowlarrvært}:{prowlarrport}/{baseurl}/api/v1/search?query={kodet term}&indexerIds={kommasepareret liste}&categories={kommasepareret liste}&type={søgetype}`
  - f.eks. `http://192.168.1.100/prowlarr/api/v1/search?query=black%20hawk%20down&indexerIds=-1&categories=2000&type=search`
  - f.eks. `http://192.168.1.100/prowlarr/api/v1/search?query=%7BTvdbId%3A71663%7D%20%7BSeason%3A32%7D&categories=5000&type=tvsearch`

Parametre

- `query` - URL-kodet søgestreng
- `indexerIds` - kommasepareret liste over indekser-ID'er
  - Efterlad parameteren udeladt i URL'en for alle indekser
  - `-2` er alle torrents
  - `-1` er alle usenet
  - Indekser-ID'er
- `categories` - kommasepareret liste over kategorier, der skal bruges
  - Efterlad parameteren udeladt for alle
- `type` - den søgetype, der skal udføres
  - `search` - Grundlæggende tekstforespørgsel
  - `tvsearch` - TV-forespørgsel - Understøtter TV-parametre
  - `moviesearch` - Filmforespørgsel - Understøtter filmparametre
  - `audiosearch` - Lyd/musik-forespørgsel - Understøtter musikparametre
  - `booksearch` - Bogforespørgsel - Understøtter bogparametre