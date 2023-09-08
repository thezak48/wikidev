---
title: Readarr-bibliotheek
description: 
published: true
date: 2021-11-30T01:41:54.243Z
tags: readarr, needs-love, library
editor: markdown
dateCreated: 2021-11-30T00:50:59.442Z
---

# Bibliotheek

Deze sectie is bedoeld voor het beheren van je bibliotheek met [auteurs](#auteurs) en [boeken](#boeken).

# Auteurs

- Weergave bibliotheek
  - Alles bijwerken - Metadata bijwerken voor alle auteurs, posters vernieuwen, auteursmappen opnieuw scannen en boekbestanden opnieuw scannen (indien ingeschakeld)
  - Vernieuwen en scannen - De metadata van de momenteel bekeken auteur vernieuwen en de map opnieuw scannen
  - RSS-synchronisatie - De RSS-feed vernieuwen van je indexers en controleren of er iets nieuws is om te downloaden
  - Auteurseditor / Auteursindex - Schakelen tussen de modus voor massabewerking en de modus voor auteursindex (bibliotheek)
  - Opties - Weergaveopties wijzigen
  - Weergave - Weergavetype schakelen
    - Tabel - Tabelweergave (lijstweergave)
    - Posters - Posters weergeven (vergelijkbaar met Plex)
    - Overzicht - Overzichtsinformatie en de poster weergeven (gedetailleerde weergave)
  - Sorteren - De huidige weergave sorteren
  - Filteren - De huidige weergave filteren

# Boeken

- Weergave bibliotheek
  - Alles bijwerken - Metadata bijwerken voor alle auteurs, posters vernieuwen, auteursmappen opnieuw scannen en boekbestanden opnieuw scannen (indien ingeschakeld)
  - Vernieuwen en scannen - De metadata van de momenteel bekeken auteur vernieuwen en de map opnieuw scannen
  - RSS-synchronisatie - De RSS-feed vernieuwen van je indexers en controleren of er iets nieuws is om te downloaden
  - Alles doorzoeken / Gefilterd doorzoeken / Geselecteerd doorzoeken - Alle boeken of geselecteerde boeken in de huidige weergave doorzoeken
  - Boekeneditor / Boekenindex - Schakelen tussen de modus voor massabewerking en de modus voor boekenindex (bibliotheek)
  - Opties - Weergaveopties wijzigen
  - Weergave - Weergavetype schakelen
    - Tabel - Tabelweergave (lijstweergave)
    - Posters - Posters weergeven (vergelijkbaar met Plex)
    - Overzicht - Overzichtsinformatie en de poster weergeven (gedetailleerde weergave)
  - Sorteren - De huidige weergave sorteren
  - Filteren - De huidige weergave filteren
  
# Nieuwe toevoegen

![addnew.png](/assets/readarr/addnew.png)

- Je kunt nieuwe auteurs of individuele boeken toevoegen door hier de naam van de auteur of een boeknaam in te voeren en deze te selecteren uit de resultatenlijst.
  - Je vindt de instructies in onze [Snelstartgids](/readarr/quick-start-guide)
- Je kunt ook auteurs toevoegen op basis van GoodReads ID, ISBN of ASIN, indien nodig, met behulp van het getoonde formaat.

![poe.png](/assets/readarr/poe.png)

- Klik op de naam van de auteur of het boek om het aan Readarr toe te voegen. Er verschijnt een venster met opties.

![addauthor.png](/assets/readarr/addauthor.png)

- Hoofdmap - Selecteer hier de hoofdmap. Verander dit niet als je Calibre Content Server gebruikt.
- Monitor - Selecteer de monitorstatus van alle boeken van deze auteur.
- Kwaliteitsprofiel - Selecteer het kwaliteitsprofiel dat moet worden gebruikt bij het zoeken naar boeken van deze auteur.
- (Alleen boek) Metadataprofiel - Selecteer het metadataprofiel dat moet worden gebruikt voor dit boek.
- Tags - Als je een tag wilt toepassen op de boeken van deze auteur, voer deze dan hier in.
- Zoeken naar ontbrekend(e) boek(en) starten - Kies of je direct een historische zoekopdracht wilt starten naar alle boeken van deze auteur op je indexers. Als je dit niet doet, worden alleen NIEUW geüploade boeken vanaf dit punt gedownload.
- Toevoegen {Auteursnaam} of Toevoegen {Boeknaam} - Klik op de knop Toevoegen om deze auteur aan Readarr toe te voegen en metadata op te halen voor alle boeken van deze auteur. Dit proces kan enige tijd duren, dus het is raadzaam om niet te snel te veel auteurs toe te voegen.

> Als je een individueel boek toevoegt en `Geen`\* selecteert voor het [metadataprofiel](/readarr/settings#metadata-profiles), wordt alleen dat boek weergegeven onder de auteur wanneer het wordt toegevoegd. Als je andere boeken van die auteur wilt toevoegen, kies dan een geschikt metadataprofiel.
> \* **Let op dat `Geen` geen enkele metadatavergelijking toepast en je mogelijk ongewenste buitenlandse edities krijgt. Om dit op te lossen, [maak je een metadataprofiel aan zoals voorgeschreven in de FAQ](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Niet-gekoppelde bestanden

![unmappedfiles.png](/assets/readarr/unmappedfiles.png)

Als hier boeken worden vermeld, worden ze niet herkend door Readarr en staan ze niet vermeld als "bestaand" in Readarr, maar ze bevinden zich wel in een van de door jou gedefinieerde hoofdmappen.

Je kunt meer informatie krijgen door te klikken op het *i*-pictogram aan de rechterkant.

Je kunt het boek handmatig importeren door te klikken op het *persoon*-pictogram aan de rechterkant.

Je kunt het boekbestand verwijderen door te klikken op het *prullenbak*-pictogram aan de rechterkant.

Je kunt ook op *Ontbrekende toevoegen* bovenaan klikken om te proberen alle boeken aan Readarr toe te voegen. Houd er rekening mee dat dit veel tijd kan kosten als je hier veel boeken hebt vermeld.