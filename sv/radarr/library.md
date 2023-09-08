---
title: Radarr Bibliotek
description: 
published: true
date: 2022-11-14T15:04:06.364Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:24:18.386Z
---

# Filmer

## Biblioteksvisning

- Uppdatera alla - Uppdatera metadata för alla filmer, uppdatera affischer, skanna om filmmappar och skanna om filmfiler (om det är aktiverat)
- Uppdatera och skanna - Uppdatera metadata för den aktuellt visade filmen och skanna om dess mapp
- RSS-synkronisering - Uppdatera RSS-flödet från dina indexeringsservrar och se om något nytt har lagts upp för att hämtas
- Sök alla / Sök filtrerade / Sök markerade - Sök alla filmer eller markerade filmer i den aktuella vyn
- Manuell import (filindex) - Manuellt importera en filmfil för en film du har lagt till i Radarr från vilken mapp som helst som Radarr kan komma åt
  - Flytta automatiskt - Försök automatiskt matcha en fil med en film i Radarr och importera genom att flytta den.
  - Interaktiv import - Granska alla filer inom sökvägen och försök matcha med en film i Radarr så att användaren kan granska resultaten. Flytta eller kopiera/hårdlänk är ett valbart alternativ i det nedre vänstra hörnet.
- Manuell import (film) - Manuellt importera en filmfil för en film du har lagt till i Radarr från filmens tilldelade mapp
  - Flytta automatiskt - Försök automatiskt matcha en fil med en film i Radarr och importera genom att flytta den.
  - Interaktiv import - Granska alla filer inom sökvägen och försök matcha med en film i Radarr så att användaren kan granska resultaten. Flytta eller kopiera/hårdlänk är ett valbart alternativ i det nedre vänstra hörnet.
- Filmredigerare / Filmindex - Växla mellan Massredigeringsläge och Filmindex (Bibliotek) -läge
- Alternativ - Ändra visningsalternativ
- Visa - Växla vistyp
  - Tabell - Tabellvy (listvy)
  - Affischer - Visa affischer (liknande Plex)
  - Översikt - Visa översiktsinformation och affischen (detaljerad vy)
- Sortera - Sortera den aktuella vyn

### Filter

- Filter - Filtrera den aktuella vyn
  - Endast övervakade - Titlar som övervakas för uppdateringar.
  - Ej övervakade - Titlar som INTE övervakas för uppdateringar.
  - Saknas - I databasen, övervakas, men saknas från filsystemet.
  - Efterfrågade - I databasen, övervakas, saknas, men bör finnas tillgängliga enligt tillgänglighetsinställningarna
  - Avskuren ouppfylld - Titel på filsystemet, men övervakas fortfarande för önskad kvalitet.
  - Anpassade filter
    - Övervakad (boolesk)
    - Ansedd tillgänglig (boolesk)
    - Minsta tillgänglighet (Enum)
      - Tillkännagiven
      - På bio
      - Släppt
    - Titel \[innehåller\] (Sträng)
    - Släppstatus (Enum)
      - Kommer
      - Tillkännagiven
      - På bio
      - Släppt
      - Borttagen
        - Borttagen från TMDb
    - Studio (Enum Studios)
    - Samling (Enum Samlingar)
    - Kvalitetsprofil (Enum Kvalitetsprofiler)
    - Tillagd (statiskt DateTime, relativt TimeDelta)
    - År (Int)
    - På bio (statiskt DateTime, relativt TimeDelta)
    - Fysisk utgåva (statiskt DateTime, relativt TimeDelta)
    - Digital utgåva (statiskt DateTime, relativt TimeDelta)
    - Speltid (Int)
    - Sökväg \[innehåller\] (Sträng)
    - Storlek på disk (Int)
    - Genrer \[innehåller\] (Enum Genrer)
    - TMDB-betyg (Flyttal)
    - TMDB-röster (Int)
    - IMDb-betyg
    - Tomato-betyg
    - IMDb-röster
    - Certifiering (Enum Betyg (PG-13, R, etc))
    - Taggar \[innehåller\] (Enum Taggar)

# Lägg till ny

![radarr-add-new-empty.png](/assets/radarr/radarr-add-new-empty.png)

- Om du vill lägga till en ny film är det här sidan du vill använda.
  - Du hittar instruktionerna i vår [Snabbstartsguide](/radarr/quick-start-guide).
- Under sökfältet hittar du också knappen Importera befintliga filmer. Om det är fallet för dig, hittar du bra information om det också i vår [Snabbstartsguide](/radarr/quick-start-guide).
- Om du får ett felmeddelande "sökvägen är redan konfigurerad", [se den här FAQ-posten](/radarr/faq#path-is-already-configured-for-an-existing-movie).

# Biblioteksimport

Biblioteksimport gör det möjligt att importera befintliga organiserade filmer och varje films fil via befintliga filer i sökvägsmappen. Detta är särskilt användbart när du skapar en ny Radarr-instans och vill behålla dina befintliga filmer.

- Biblioteksimport används för att lägga till och importera ett befintligt organiserat filmbibliotek i Radarr.
- Biblioteksimport kan inte användas för:
  - Importera filer från en nedladdningsmapp
  - Lägga till eller importera en eller flera filer som inte är korrekt namngivna och organiserade i sin egen filmapp inom din rotmapp eller en mapp du vill lägga till som rotmapp
  - Alla andra användningsområden som inte innebär att lägga till en film i Radarr och importera filmen och dess fil från rotmappen (biblioteket) som angavs vid biblioteksimporten
- Om du får ett felmeddelande "sökvägen är redan konfigurerad", [se den här FAQ-posten](/radarr/faq#path-is-already-configured-for-an-existing-movie).
  
> Det krävs att filmappar och filer har året i sitt namn för att kunna importeras och analyseras.{.is-warning}

> \* Ej Windows: Om du använder en NFS-montage, se till att `nolock` är aktiverat.
> \* Om du använder en SMB-montage, se till att `nobrl` är aktiverat.
{.is-warning}

> **Användaren och gruppen som du har konfigurerat Radarr att köra som måste ha läs- och skrivrättigheter till denna plats.**
{.is-info}

> Din nedladdningsklient laddar ner till en nedladdningsmapp och Radarr importerar den till din mediamapp (slutdestination) som din mediaserver använder.
{.is-info}

> **Din nedladdningsmapp och mediamapp kan inte vara samma plats**
{.is-danger}

# Samlingar

Wikin utvecklas och underhålls av gemenskapen.
Detta avsnitt har inte fått några bidrag för att återspegla och beskriva samlingssidan i Radarr.

# Upptäck

Upptäck visar rekommenderade filmer

- Om du inte har några listor visas de 90 mest rekommenderade filmerna baserat på TMDb-filmer som rekommenderas för filmerna i ditt bibliotek, samt de 10 rekommendationerna från dina senaste tillägg.

> Tips: Du kan inaktivera Radarrs rekommenderade filmer och bara visa filmer från dina listor i `Alternativ`.
{.is-info}

- Om du har listor visas rekommendationerna ovan OCH poster från dina listor.

> Tips: Ändra `Filter` till `Nya icke-uteslutna` för att bara visa filmer som inte finns i ditt bibliotek.
{.is-info}

![radarr-discover-empty.png](/assets/radarr/radarr-discover-empty.png)

- Det är troligt att dina upptäcktrekommendationer kommer att vara få om du har en ny installation med få eller inga filmer. Du måste lägga till innehåll i biblioteket för att få rekommendationer. Du har flera alternativ:
  1. Klicka på knappen [Lägg till ny film](/radarr/library#add-new) för att manuellt lägga till filmer.
  1. Klicka på knappen [Importera befintligt bibliotek](/radarr/library#library-import) för att importera ett befintligt bibliotek.
  1. Klicka på knappen [Lägg till listor](/radarr/settings#lists) för att lägga till en lista i Radarr. Mer information om listor finns på sidan [Mer information (stöds)](/radarr/faq#what-are-lists-and-what-can-they-do-for-me) för detta avsnitt.

![radarr-discover-add-new-movies.png](/assets/radarr/radarr-discover-add-new-movies.png)

- När du har lagt till en film med något av de tre alternativen ovan kommer du att presenteras med olika filmer att upptäcka.
    1. Här kan du välja vilka filmer du vill lägga till i ditt bibliotek
    1. Här kan du välja alla filmer som finns på denna lista om du känner dig extra galen
    1. Välj vilken rotmapp du vill att dessa filmer ska gå till när de importeras
    1. Välj vilken tillgänglighet du vill att filmen ska ha innan den hämtas
    1. Välj eventuella kvalitetsprofiler du redan har skapat ([Mer information](/radarr/settings#quality-profiles))
    1. Vill du att Radarr ska övervaka den här filmen för eventuella uppgraderingar i kvalitet?
    1. Vill du att Radarr automatiskt ska söka efter den här filmen efter att du har lagt till den?
    1. Vill du att Radarr ska utesluta dessa filmer från eventuella listor som skulle importeras? ([Mer information](/radarr/settings#list-exclusion))
    1. Slutligen, lägg till filmen i ditt bibliotek.