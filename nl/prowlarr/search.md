---
title: Prowlarr Zoeken
description: 
published: true
date: 2022-01-02T23:05:56.758Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:31:53.221Z
---

Deze pagina laat zien hoe je een zoekopdracht kunt uitvoeren vanuit Prowlarr. Over het algemeen zou je je zoekopdrachten via de app doen, maar het is ook mogelijk om ze rechtstreeks in Prowlarr te doen.

# Een zoekopdracht uitvoeren

Om een zoekopdracht te starten, klik je op `Zoeken` in het linker menu. Er zal een grotendeels lege pagina verschijnen met enkele opties onderaan het scherm.

![search_1_searchscreen.png](/assets/prowlarr/search_1_searchscreen.png)

- Query - Voer je zoektermen in het Query-veld in.
  - Klik op het vergrootglas om het zoektype te wijzigen. De beschikbare opties zijn:
    - Basiszoekopdracht - Basis tekstzoekopdracht
    - TV-zoekopdracht - Zoeken met behulp van TV-parameters zoals weergegeven in de gebruikersinterface, inclusief ID-gebaseerde (TVDbId, IMDbId, TMDbID, enz.) en seizoen/aflevering-zoekopdrachten
    - Filmzoekopdracht - Zoeken met behulp van filmparameters zoals weergegeven in de gebruikersinterface, inclusief ID-gebaseerde (TMDbId, IMDbId, Genre, enz.)
    - Audiozoekopdracht - Zoeken met behulp van muziekparameters zoals weergegeven in de gebruikersinterface, inclusief Artiest, Album, Label, Genre, enz.
    - Boekzoekopdracht - Zoeken met behulp van boekparameters zoals weergegeven in de gebruikersinterface, inclusief auteur, titel, enz.

> Deze worden over het algemeen opgemaakt als `{VariabeleNaam:Zoekwaarde}` bijvoorbeeld Voor een TV-zoekopdracht van The Simpsons Seizoen 32 zou de zoekopdracht `{TvdbId:71663} {Season:32}` zijn
{.is-info}

> Let op dat niet alle indexers alle soorten zoekopdrachten ondersteunen {.is-info}

- Indexers - Kies je indexers in het vervolgkeuzemenu Indexers. Je kunt "Usenet" of "Torrents" aanvinken om automatisch alle indexers in die categorieën te selecteren, of je kunt specifieke indexers voor je zoekopdracht selecteren uit een van de groepen.
- Categorie - Kies de categorieën waarop je wilt zoeken op je indexers in het vervolgkeuzemenu Categorie. Je kunt hoofdcategorieën (TV, Films, enz.) selecteren om automatisch alle subcategorieën te selecteren, of je kunt specifieke categorieën selecteren uit een van de groepen.

Klik vervolgens op de knop `Zoeken`. Het kan enkele seconden duren voordat de resultaten verschijnen. Zodra ze verschijnen, kun je kolommen toevoegen of verwijderen met behulp van de knop `Opties`, en je kunt je resultaten sorteren en filteren door te klikken op de kolomkoppen of door de knop `Filter` te gebruiken.

Je kunt het resultaat downloaden door te klikken op het downloadpictogram aan de rechterkant van het resultaat. Dit stuurt het naar de juiste downloadclient die je hebt geconfigureerd.

Je kunt resultaten in één keer bulk binnenhalen door de selectievakjes aan de linkerkant aan te vinken en op de knop `Releases binnenhalen` te klikken.

> Alles wat je downloadt, krijgt de categorie toegewezen die je hebt ingesteld in Prowlarr. Dit kan vereisen dat je handmatig importeert in je app-programma vanuit een niet-standaard directory! {.is-info}

# API-eindpunten

## RSS-compatibel - Enkele Indexer Feed

- Standaard Newznab/Torznab-compatibel eindpunt/parameters. Je kunt de zoekopdrachten aanpassen aan je behoeften volgens de gedefinieerde standaarden.

> Er wordt geen samengevoegd multi-indexer eindpunt toegevoegd vanwege de aanzienlijke nadelen van deze functionaliteit {.is-info}

### API-sleutel in Query

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - bijv. `http://192.168.1.100:9696/11/api?t=search&q=mike&apikey={yourkey}&cat=5000,2000`

### API-sleutel in Header

> Zorg ervoor dat je `X-Api-Key` doorgeeft als een header met de API-sleutel {.is-info}

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - bijv. `http://192.168.1.100:9696/{indexerid}/api?t=search&q=mike&cat=5000,2000`

## Zoekfeed

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/api/v1/search?query={encoded term}&indexerIds={comma separated list}&categories={comma separated list}&type={searchtype}`
  - bijv. `http://192.168.1.100/prowlarr/api/v1/search?query=black%20hawk%20down&indexerIds=-1&categories=2000&type=search`
  - bijv. `http://192.168.1.100/prowlarr/api/v1/search?query=%7BTvdbId%3A71663%7D%20%7BSeason%3A32%7D&categories=5000&type=tvsearch`

Parameters

- `query` - URL-gecodeerde zoekreeks
- `indexerIds` - door komma's gescheiden lijst van Indexer ID's
  - Laat de parameter weg uit de URL voor alle indexers
  - `-2` is alle torrents
  - `-1` is alle usenet
  - Indexer ID's
- `categories` - door komma's gescheiden lijst van te gebruiken categorieën
  - laat de parameter weg voor alle categorieën
- `type` - het uit te voeren zoektype
  - `search` - Basis tekstzoekopdracht
  - `tvsearch` - TV-zoekopdracht - Ondersteunt TV-parameters
  - `moviesearch` - Filmzoekopdracht - Ondersteunt Film-parameters
  - `audiosearch` - Audio/Muziek-zoekopdracht - Ondersteunt Muziek-parameters
  - `booksearch` - Boekzoekopdracht - Ondersteunt Boek-parameters