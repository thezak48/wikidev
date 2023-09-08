---
title: Radarr-bibliotheek
description: 
published: true
date: 2022-11-14T15:04:06.364Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:24:18.386Z
---

# Films

## Weergave bibliotheek

- Alles bijwerken - Metadata bijwerken voor alle films, posters vernieuwen, filmmappen opnieuw scannen en filmbestanden opnieuw scannen (indien ingeschakeld)
- Vernieuwen en scannen - Metadata van de momenteel bekeken film vernieuwen en de map opnieuw scannen
- RSS-synchronisatie - De RSS-feed van uw indexers vernieuwen en controleren of er iets nieuws is gepost om te downloaden
- Alles zoeken / Gefilterd zoeken / Geselecteerd zoeken - Zoeken naar alle films of geselecteerde films in de huidige weergave
- Handmatig importeren (filmbestand) - Handmatig een filmbestand importeren voor een film die u aan Radarr hebt toegevoegd vanuit een map die toegankelijk is voor Radarr
  - Automatisch verplaatsen - Automatisch proberen een bestand te koppelen aan een film in Radarr en importeren door het te verplaatsen.
  - Interactieve import - Alle bestanden in het pad bekijken en proberen overeen te komen met een film in Radarr, waarbij de gebruiker de resultaten kan bekijken. Verplaatsen of kopiëren/hardlinken is een selecteerbare optie in de linkerbenedenhoek.
- Handmatig importeren (film) - Handmatig een filmbestand importeren voor een film die u aan Radarr hebt toegevoegd vanuit de map van de betreffende film
  - Automatisch verplaatsen - Automatisch proberen een bestand te koppelen aan een film in Radarr en importeren door het te verplaatsen.
  - Interactieve import - Alle bestanden in het pad bekijken en proberen overeen te komen met een film in Radarr, waarbij de gebruiker de resultaten kan bekijken. Verplaatsen of kopiëren/hardlinken is een selecteerbare optie in de linkerbenedenhoek.
- Filmbewerker / Filmbestand - Schakelen tussen de modus Massabewerker en de modus Filmbestand (bibliotheek)
- Opties - Weergaveopties wijzigen
- Weergave - Weergavetype schakelen
  - Tabel - Tabulaire weergave (lijstweergave)
  - Posters - Posters weergeven (vergelijkbaar met Plex)
  - Overzicht - Overzichtsinformatie en de poster weergeven (gedetailleerde weergave)
- Sorteren - De huidige weergave sorteren

### Filters

- Filter - De huidige weergave filteren
  - Alleen gemonitord - Titels die worden gemonitord voor updates.
  - Niet gemonitord - Titels die NIET worden gemonitord voor updates.
  - Ontbrekend - In de database, gemonitord, maar ontbreekt in het bestandssysteem.
  - Gewenst - In de database, gemonitord, ontbreekt, maar zou beschikbaar moeten zijn op basis van de beschikbaarheidsinstellingen.
  - Onvoldoende kwaliteit - Titel aanwezig in het bestandssysteem, maar nog steeds controleren op gewenste kwaliteit.
  - Aangepaste filters
    - Gemonitord (boolean)
    - Beschouwd als beschikbaar (boolean)
    - Minimale beschikbaarheid (Enum)
      - Aangekondigd
      - In bioscopen
      - Uitgebracht
    - Titel \[bevat\] (String)
    - Status release (Enum)
      - Nog te bepalen
      - Aangekondigd
      - In bioscopen
      - Uitgebracht
      - Verwijderd
        - Verwijderd uit TMDb
    - Studio (Enum Studios)
    - Collectie (Enum Collecties)
    - Kwaliteitsprofiel (Enum Kwaliteitsprofielen)
    - Toegevoegd (statische DateTime, relatieve TimeDelta)
    - Jaar (Int)
    - In bioscopen (statische DateTime, relatieve TimeDelta)
    - Fysieke release (statische DateTime, relatieve TimeDelta)
    - Digitale release (statische DateTime, relatieve TimeDelta)
    - Speelduur (Int)
    - Pad \[bevat\] (String)
    - Grootte op schijf (Int)
    - Genres \[bevat\] (Enum Genres)
    - TMDB-beoordeling (Float)
    - TMDB-stemmen (Int)
    - IMDb-beoordeling
    - Tomato-beoordeling
    - IMDb-stemmen
    - Certificering (Enum Beoordeling (PG-13, R, enz.))
    - Tags \[bevat\] (Enum Tags)

# Nieuwe film toevoegen

![radarr-add-new-empty.png](/assets/radarr/radarr-add-new-empty.png)

- Als u een nieuwe film wilt toevoegen, is dit de pagina waar u dat wilt doen.
  - U vindt de instructies in onze [Snelstartgids](/radarr/quick-start-guide).
- Onder het zoekveld vindt u ook de knop Bestaande films importeren. Als dat het geval is, vindt u hierover ook uitgebreide informatie in onze [Snelstartgids](/radarr/quick-start-guide).
- Als u de foutmelding "pad is al geconfigureerd" krijgt, [raadpleeg dan deze FAQ-vermelding](/radarr/faq#path-is-already-configured-for-an-existing-movie).

# Bibliotheek importeren

Met de bibliotheekimport kunt u bestaande georganiseerde films en de bestanden van elke film importeren via bestaande bestanden in de map van het pad. Dit is vooral handig wanneer u een nieuwe Radarr-instantie maakt en uw bestaande films wilt behouden.

- Met de bibliotheekimport kunt u een bestaande georganiseerde filmcollectie importeren en toevoegen aan Radarr.
- De bibliotheekimport kan niet worden gebruikt voor:
  - Het importeren van bestanden uit een downloadmap
  - Het toevoegen of importeren van één of meer bestanden die niet correct zijn benoemd en georganiseerd in hun eigen filmap binnen uw hoofdmap of een map die u wilt toevoegen als hoofdmap
  - Andere toepassingen die geen film aan Radarr toevoegen en de film en het bestand importeren vanuit de hoofdmap (bibliotheekmap) die is ingevoerd in de bibliotheekimport
- Als u de foutmelding "pad is al geconfigureerd" krijgt, [raadpleeg dan deze FAQ-vermelding](/radarr/faq#path-is-already-configured-for-an-existing-movie).
  
> Het is vereist dat filmmappen en -bestanden het jaartal in hun naam hebben om te kunnen worden geïmporteerd en geanalyseerd.{.is-warning}

> \* Niet-Windows: Als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
> \* Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.
{.is-warning}

> **De gebruiker en groep die u hebt geconfigureerd om Radarr uit te voeren, moeten lees- en schrijftoegang hebben tot deze locatie.**
{.is-info}

> Uw downloadclient downloadt naar een downloadmap en Radarr importeert het naar uw mediamap (eindbestemming) die uw mediaserver gebruikt.
{.is-info}

> **Uw downloadmap en mediamap kunnen niet dezelfde locatie zijn**
{.is-danger}

# Collecties

De wiki wordt ontwikkeld en onderhouden door de community.
Voor dit gedeelte zijn geen bijdragen geleverd om de pagina over collecties in Radarr te beschrijven.

# Ontdekken

Ontdekken toont aanbevolen films

- Als u geen lijst(en) heeft, worden de 90 meest aanbevolen films op basis van de TMDb-films die worden aanbevolen voor de films in uw bibliotheek weergegeven, samen met de 10 aanbevelingen van uw meest recente toevoegingen.

> Tip: U kunt aanbevolen films van Radarr uitschakelen en alleen films van uw lijsten bekijken in `Opties`.
{.is-info}

- Als u lijst(en) heeft, worden de hierboven genoemde aanbevelingen weergegeven EN vermeldingen van uw lijst(en).

> Tip: Wijzig het `Filter` naar `Nieuw Niet-Uitgesloten` om alleen films te tonen die niet in uw bibliotheek staan.
{.is-info}

![radarr-discover-empty.png](/assets/radarr/radarr-discover-empty.png)

- De kans is groot dat uw ontdekkingsaanbevelingen schaars zullen zijn als u een nieuwe installatie heeft met weinig of geen films. U moet bibliotheekinhoud toevoegen om aanbevelingsrichting te krijgen. U heeft verschillende opties:
  1. Klik op de knop [Nieuwe film toevoegen](/radarr/library#add-new) om handmatig films toe te voegen.
  1. Klik op de knop [Bestaande bibliotheek importeren](/radarr/library#library-import) om een bestaande bibliotheek te importeren.
  1. Klik op de knop [Lijsten toevoegen](/radarr/settings#lists) om een lijst aan Radarr toe te voegen. Meer informatie over lijsten vindt u op de pagina [Meer informatie (Ondersteund)](/radarr/faq#what-are-lists-and-what-can-they-do-for-me) voor dit gedeelte.

![radarr-discover-add-new-movies.png](/assets/radarr/radarr-discover-add-new-movies.png)

- Nadat u een film hebt toegevoegd via een van de bovenstaande drie opties, krijgt u verschillende films te zien om te ontdekken.
    1. Hier kunt u selecteren welke films u aan uw bibliotheek wilt toevoegen
    1. Hier kunt u alle films op deze lijst selecteren als u extra gek wilt doen
    1. Selecteer het hoofdpad waar u wilt dat deze films naartoe gaan zodra ze zijn geïmporteerd
    1. Selecteer de beschikbaarheid die u wilt dat de film heeft voordat deze wordt gedownload
    1. Selecteer eventuele kwaliteitsprofielen die u al hebt aangemaakt ([Meer informatie](/radarr/settings#quality-profiles))
    1. Wilt u dat Radarr deze film controleert op upgrades in kwaliteit?
    1. Wilt u dat Radarr automatisch naar deze film zoekt nadat u deze hebt toegevoegd?
    1. Wilt u dat Radarr deze films uitsluit van eventuele lijsten die worden geïmporteerd? ([Meer informatie](/radarr/settings#list-exclusion))
    1. Voeg de film uiteindelijk toe aan uw bibliotheek.