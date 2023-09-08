---
title: Readarr Bibliotek
description: 
published: true
date: 2021-11-30T01:41:54.243Z
tags: readarr, needs-love, library
editor: markdown
dateCreated: 2021-11-30T00:50:59.442Z
---

# Bibliotek

Den här sektionen är för att hantera ditt bibliotek av [författare](#författare) och [böcker](#böcker).

# Författare

- Biblioteksvisning
  - Uppdatera allt - Uppdatera metadata för alla författare, uppdatera affischer, skanna om författarmappar och skanna om bokfiler (om aktiverat)
  - Uppdatera och skanna - Uppdatera metadata för den aktuellt visade författaren och skanna om dess mapp
  - RSS-synkronisering - Uppdatera RSS-flödet från dina indexeringsservrar och se om något nytt har publicerats för att hämtas
  - Författarredigerare / Författarindex - Växla mellan Massredigeringsläge och Författarindex (Bibliotek) läge
  - Alternativ - Ändra visningsalternativ
  - Visa - Växla visningstyp
    - Tabell - Tabellvisning (listvy)
    - Affischer - Visa affischer (liknande Plex)
    - Översikt - Visa översiktsinformation och affischen (detaljerad vy)
  - Sortera - Sortera aktuell vy
  - Filtrera - Filtrera aktuell vy

# Böcker

- Biblioteksvisning
  - Uppdatera allt - Uppdatera metadata för alla författare, uppdatera affischer, skanna om författarmappar och skanna om bokfiler (om aktiverat)
  - Uppdatera och skanna - Uppdatera metadata för den aktuellt visade författaren och skanna om dess mapp
  - RSS-synkronisering - Uppdatera RSS-flödet från dina indexeringsservrar och se om något nytt har publicerats för att hämtas
  - Sök alla / Sök filtrerade / Sök valda - Sök alla böcker eller valda böcker i den aktuella vyn
  - Bokredigerare / Bokindex - Växla mellan Massredigeringsläge och Bokindex (Bibliotek) läge
  - Alternativ - Ändra visningsalternativ
  - Visa - Växla visningstyp
    - Tabell - Tabellvisning (listvy)
    - Affischer - Visa affischer (liknande Plex)
    - Översikt - Visa översiktsinformation och affischen (detaljerad vy)
  - Sortera - Sortera aktuell vy
  - Filtrera - Filtrera aktuell vy
  
# Lägg till ny

![addnew.png](/assets/readarr/addnew.png)

- Du kan lägga till nya författare eller enskilda böcker genom att ange författarens namn eller boktitel här och välja det från resultatlistan.
  - Du hittar instruktioner i vår [Snabbstartsguide](/readarr/quick-start-guide)
- Du kan också lägga till författare med GoodReads ID, ISBN eller ASIN vid behov, med hjälp av den angivna formatet.

![poe.png](/assets/readarr/poe.png)

- Klicka på författarens eller bokens namn för att lägga till det i Readarr. En ruta kommer att dyka upp med alternativ för dig.

![addauthor.png](/assets/readarr/addauthor.png)

- Rotmapp - Välj rotmappen här. Ändra inte detta om du använder Calibre Content Server.
- Övervaka - Välj övervakningsstatus för alla böcker av denna författare.
- Kvalitetsprofil - Välj kvalitetsprofil att använda när du letar efter böcker av denna författare.
- (Endast bok) Metadataprofil - Välj metadataprofil att använda för denna bok.
- Taggar - Om du vill ha en tagg tillämpad på denna författares böcker, ange den här.
- Starta sökning efter saknade böcker - Välj om du vill starta en historisk sökning i dina indexeringsservrar efter alla böcker av denna författare omedelbart. Om du inte gör detta kommer endast NYLIGEN uppladdade böcker att hämtas från och med nu.
- Lägg till {Författarnamn} eller Lägg till {Boknamn} - Klicka på Lägg till-knappen för att lägga till denna författare i Readarr och börja hämta metadata för alla böcker av denna författare. Denna process kan ta lite tid, så det skulle vara klokt att inte lägga till för många författare för snabbt.

> Om du lägger till en enskild bok och väljer `None`\* för [metadataprofilen](/readarr/settings#metadata-profiles), kommer endast den boken att visas under författaren när den läggs till. Om du vill lägga till andra böcker för den författaren, välj en lämplig metadataprofil.
> \* **Observera att `None` inte tillämpar några metadatafilter och du kan få oönskade utländska utgåvor. För att komma runt detta [skapa en metadataprofil enligt anvisningarna i FAQ](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Omatchade filer

![unmappedfiles.png](/assets/readarr/unmappedfiles.png)

Om det finns böcker listade här, så är de inte igenkända av Readarr och de listas inte som "befintliga" i Readarr, men de finns i en av de rotmappar du har definierat.

Du kan få mer information genom att klicka på *i*-ikonen till höger.

Du kan manuellt importera boken genom att klicka på *person*-ikonen till höger.

Du kan ta bort bokfilen genom att klicka på *papperskorg*-ikonen till höger.

Du kan också klicka på *Lägg till saknade* längst upp för att försöka lägga till alla böcker i Readarr. Observera att detta kan ta lång tid om du har många böcker listade här.