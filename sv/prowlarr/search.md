---
title: Prowlarr Sökning
description: 
published: true
date: 2022-01-02T23:05:56.758Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:31:53.221Z
---

Denna sida visar hur du utför en sökning från Prowlarr. Vanligtvis skulle du söka via appen, men det är också möjligt att göra det direkt i Prowlarr.

# Utföra en sökning

För att starta en sökning, klicka på `Sök` i vänstermenyn. Det kommer att visas en mestadels tom sida med några alternativ längst ner på skärmen.

![search_1_searchscreen.png](/assets/prowlarr/search_1_searchscreen.png)

- Fråga - Skriv in dina söktermer i Frågefältet.
  - Klicka på förstoringsglaset för att ändra söktypen, tillgängliga alternativ är:
    - Grundläggande sökning - Grundläggande textfråga
    - TV-sökning - Sökning med TV-parametrar som visas i gränssnittet, inklusive ID-baserade (TVDbId, IMDbId, TMDbID, etc.) och säsong/avsnitt-sökningar
    - Film-sökning - Sökning med filmparametrar som visas i gränssnittet, inklusive ID-baserade (TMDbId, IMDbId, Genre, etc.)
    - Ljud-sökning - Sökning med musikparametrar som visas i gränssnittet, inklusive Artist, Album, Label, Genre, etc.
    - Bok-sökning - Sökning med bokparametrar som visas i gränssnittet, inklusive författare, titel, etc.

> Dessa är vanligtvis formaterade som `{VariabelNamn:SökVärde}` t.ex. För en TV-sökning av The Simpsons Säsong 32 skulle sökningen vara `{TvdbId:71663} {Season:32}`
{.is-info}

> Observera att inte alla indexeringstjänster stöder alla typer av frågor {.is-info}

- Indexeringstjänster - Välj dina indexeringstjänster i rullgardinsmenyn Indexeringstjänster. Du kan markera "Usenet" eller "Torrents" för att automatiskt välja alla indexeringstjänster i dessa kategorier, eller så kan du välja specifika indexeringstjänster för din sökning från någon av grupperna.
- Kategori - Välj de kategorier du vill söka på dina indexeringstjänster från rullgardinsmenyn. Du kan välja överordnade kategorier (TV, Filmer, etc.) för att automatiskt välja alla underkategorier, eller så kan du välja specifika kategorier från någon av grupperna.

Klicka sedan på `Sök`-knappen. Dina resultat kan ta några sekunder att visas. När de gör det kan du lägga till eller ta bort kolumner med hjälp av `Alternativ`-knappen, och du kan sortera och filtrera dina resultat genom att antingen klicka på kolumnrubrikerna eller använda `Filter`-knappen.

Du kan ladda ner resultatet genom att klicka på nedladdningsikonen till höger om resultatet. Detta skickar det till den korrekta nedladdningsklienten som du har konfigurerat.

Du kan också hämta flera resultat samtidigt genom att markera rutorna på vänster sida och klicka på `Hämta utgåvor`-knappen.

> Allt som laddas ner kommer att ha den kategoritilldelning du har ställt in i Prowlarr. Detta kan kräva en manuell import i din app från en icke-standardmapp! {.is-info}

# API-slutpunkter

## RSS-kompatibel - Enskild indexeringstjänst-feed

- Standard Newznab/Torznab-kompatibel slutpunkt/parametrar. Du kan justera frågorna efter behov enligt de definierade standarderna.

> En samlad flerindexeringstjänst-slutpunkt kommer inte att läggas till på grund av de betydande nackdelarna med den funktionaliteten {.is-info}

### API-nyckel i frågan

- `http://{prowlarrvärd}:{prowlarrport}/{basurl}/{indexeringstjänstid}/api?t=search&q={term}&apikey={dinnyckel}&cat={kommaseparerad lista}`
  - t.ex. `http://192.168.1.100:9696/11/api?t=search&q=mike&apikey={dinnyckel}&cat=5000,2000`

### API-nyckel i huvudet

> Se till att skicka med `X-Api-Key` med API-nyckeln som en huvudparameter {.is-info}

- `http://{prowlarrvärd}:{prowlarrport}/{basurl}/{indexeringstjänstid}/api?t=search&q={term}&apikey={dinnyckel}&cat={kommaseparerad lista}`
  - t.ex. `http://192.168.1.100:9696/{indexeringstjänstid}/api?t=search&q=mike&cat=5000,2000`

## Sök-feed

- `http://{prowlarrvärd}:{prowlarrport}/{basurl}/api/v1/search?query={kodad term}&indexerIds={kommaseparerad lista}&categories={kommaseparerad lista}&type={söktyp}`
  - t.ex. `http://192.168.1.100/prowlarr/api/v1/search?query=black%20hawk%20down&indexerIds=-1&categories=2000&type=search`
  - t.ex. `http://192.168.1.100/prowlarr/api/v1/search?query=%7BTvdbId%3A71663%7D%20%7BSeason%3A32%7D&categories=5000&type=tvsearch`

Parametrar

- `query` - URL-kodad söksträng
- `indexerIds` - kommaseparerad lista av indexeringstjänst-ID
  - Lämna bort parametern från URL:en för alla indexeringstjänster
  - `-2` är alla torrents
  - `-1` är all usenet
  - Indexeringstjänst-ID:n
- `categories` - kommaseparerad lista av kategorier att använda
  - lämna bort parametern för alla
- `type` - söktypen att utföra
  - `search` - Grundläggande textfråga
  - `tvsearch` - TV-fråga - Stöder TV-parametrar
  - `moviesearch` - Filmfråga - Stöder filmparametrar
  - `audiosearch` - Ljud/Musik-fråga - Stöder musikparametrar
  - `booksearch` - Bokfråga - Stöder bokparametrar