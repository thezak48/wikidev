---
title: Radarr Snelstartgids
description: 
published: true
date: 2023-08-27T22:14:05.687Z
tags: radarr, snelstart
editor: markdown
dateCreated: 2021-06-20T20:05:44.814Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Snelstart installatiegids](#snelstart-installatiegids)
- [Opstarten](#opstarten)
- [Mediabeheer](#mediabeheer)
  - [Films benoemen](#films-benoemen)
  - [Importeren](#importeren)
  - [Bestandsbeheer](#bestandsbeheer)
  - [Hoofdmappen](#hoofdmappen)
- [Profielen](#profielen)
- [Kwaliteit](#kwaliteit)
- [Indexers](#indexers)
- [Downloadclients](#downloadclients)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Hoe u uw bestaande georganiseerde mediatheek importeert](#hoe-u-uw-bestaande-georganiseerde-mediatheek-importeert)
  - [Films importeren](#films-importeren)
  - [Bestaande media importeren](#bestaande-media-importeren)
    - [Geen overeenkomst gevonden](#geen-overeenkomst-gevonden)
    - [Foutieve mapnaam na import corrigeren](#foutieve-mapnaam-na-import-corrigeren)
  - [Hoe u een film toevoegt](#hoe-u-een-film-toevoegt)

# Snelstart installatiegids

> Deze pagina is nog in bewerking en niet compleet. Bijdragen zijn welkom.

> Voor een gedetailleerd overzicht van alle instellingen, zie [Radarr => Instellingen](/radarr/settings)
{.is-info}

In deze gids proberen we de basisinstellingen uit te leggen die u moet doen om aan de slag te gaan met Radarr. We slaan enkele opties over die u op het scherm kunt zien. Als u hier dieper op in wilt gaan, raadpleeg dan de juiste pagina in de FAQ en documentatie voor een volledige uitleg.

> Houd er rekening mee dat geavanceerde opties worden weergegeven in `oranje` in de schermafbeeldingen en GUI-instellingen. U moet op `Toon geavanceerd` boven aan de pagina klikken om ze zichtbaar te maken.
{.is-warning}

# Opstarten

Na installatie en het opstarten opent u een browser en gaat u naar `http://{uw_ip_hier}:7878`

![Radarr-start.png](/assets/radarr/Radarr-start.png)

# Mediabeheer

Laten we eerst kijken naar de instellingen voor `Mediabeheer`, waar we onze voorkeursinstellingen voor het benoemen en beheren van bestanden kunnen instellen.

`Instellingen` => `Mediabeheer`

![Radarr-settings-mm.png](/assets/radarr/Radarr-settings-mm.png)

## Films benoemen

![Radarr-settings-mm-movie-naming.png](/assets/radarr/Radarr-settings-mm-movie-naming.png)

1. In- of uitschakelen van het hernoemen van uw films (in plaats van de namen te behouden zoals ze zijn of zoals ze waren toen u ze downloadde).
2. Als u wilt dat ongeldige tekens worden vervangen of verwijderd (`\ / : * ? " < > | ~ # % & + { }`).
3. Deze instelling bepaalt hoe Radarr omgaat met dubbele punten in het filmbestand.
4. Hier selecteert u de benaming voor de daadwerkelijke filmbestanden.
5. *(Geavanceerde optie) Hier stelt u de benaming in voor de map die het videobestand bevat.*

> Als u een aanbevolen benamingsschema en voorbeelden wilt, bekijk dan [TRaSH's Aanbevolen benamingsschema's](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/).
{.is-info}

## Importeren

![Radarr-settings-mm-importing.png](/assets/radarr/Radarr-settings-mm-importing.png)

1. *(Geavanceerde optie) Schakel `Gebruik hardlinks in plaats van kopiëren` in voor meer informatie over hoe en waarom met voorbeelden [TRaSH's Hardlinks-gids](https://trash-guides.info/hardlinks).
1. *(Geavanceerde optie) Importeer bijpassende extra bestanden (ondertitels, nfo, enz.) na het importeren van een bestand.*

## Bestandsbeheer

![Radarr-settings-mm-fm.png](/assets/radarr/Radarr-settings-mm-fm.png)

1. Films die van de schijf zijn verwijderd, worden automatisch niet meer gevolgd in Radarr.
    - U wilt mogelijk een film verwijderen, maar wilt niet dat Radarr de film opnieuw downloadt. Gebruik deze optie.
1. *(Geavanceerde optie) Wijs een locatie aan waar verwijderde bestanden naartoe moeten gaan (voor het geval u ze wilt herstellen voordat de prullenbak wordt geleegd).*
1. *(Geavanceerde optie) Dit is hoe oud een bepaald bestand kan zijn voordat het permanent wordt verwijderd.*

## Hoofdmappen

![Radarr-settings-mm-root-folder.png](/assets/radarr/Radarr-settings-mm-root-folder.png)

Hier voegt u de hoofdmap toe die Radarr zal gebruiken om uw bestaande georganiseerde mediatheek te importeren en waar Radarr uw media zal importeren (kopiëren/hardlinken/verplaatsen) nadat uw downloadclient deze heeft gedownload.

> \* Niet-Windows: Als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
> \* Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.
{.is-warning}

> **De gebruiker en groep die u hebt geconfigureerd om Radarr uit te voeren, moeten lees- en schrijftoegang hebben tot deze locatie.** {.is-info}

> Uw downloadclient downloadt naar een downloadmap en Radarr importeert het naar uw mediamap (eindbestemming) die uw mediaserver gebruikt.
{.is-info}

> **Uw downloadmap en mediamap (bibliotheek / hoofdmap) kunnen niet dezelfde locatie zijn.**
{.is-danger}

Vergeet niet om uw wijzigingen op te slaan.

# Profielen

`Instellingen` => `Profielen`

![Radarr-settings-profiles.png](/assets/radarr/Radarr-settings-profiles.png)

Hier kunt u profielen configureren voor de kwaliteit, voorkeurstaal en aangepaste indelingsscore van een film die u wilt downloaden.

We raden u aan uw eigen profielen te maken en alleen de gewenste kwaliteitsbronnen en talen te selecteren.

Voor meer informatie over buitenlandse titels en talen, zie [deze FAQ-entry](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

Veel gebruikers vinden [TRaSH's gids voor aangepaste indelingstaal](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) handig om de talen van films die ze willen specificeren.

Profielen is ook waar aangepaste indelingsscores worden geconfigureerd. Het wordt sterk aanbevolen om de volgende aangepaste indelingen toe te voegen van [TRaSH's gidsen](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) om ongewenste downloads te voorkomen. Raadpleeg het gekoppelde TRaSH Guide Custom Format-artikel en de 3 extra genoemde TRaSH Custom Format Guides boven aan de pagina Collection of Custom Formats voor meer informatie.

- [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) voorkomt het downloaden van releases met Dolby Vision (DV) die een groene tint hebben als DV niet wordt ondersteund.
- [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) voorkomt het downloaden van slecht genoemde BR-DISK's die niet overeenkomen met de BR-DISK-kwaliteitsanalyse.

> Meer informatie op [Instellingen => Profielen](/radarr/settings#profiles).
> Om te zien wat het verschil is tussen de kwaliteitsbronnen, bekijk [onze kwaliteitsdefinities](/radarr/settings#qualities-defined).
{.is-info}

# Kwaliteit

`Instellingen` => `Kwaliteit`

![Radarr-settings-quality.png](/assets/radarr/Radarr-settings-quality.png)

Hier kunt u de minimale en maximale grootte van uw gewenste mediabestanden wijzigen/afstemmen (bij gebruik van Usenet moet u rekening houden met de RAR/PAR2-bestanden)

> Als u hulp nodig heeft bij het instellen van de kwaliteitsinstellingen, bekijk dan [TRaSH's aanbevolen bestandsgrootte](https://trash-guides.info/Radarr/Radarr-Quality-Settings-File-Size/) voor een getest voorbeeld.
{.is-info}

# Indexers

`Instellingen` => `Indexers`

![Radarr-settings-indexers.png](/assets/radarr/Radarr-settings-indexers.png)

Hier voegt u de indexer/tracker toe die u daadwerkelijk gaat gebruiken om uw bestanden te downloaden.

Nadat u op de <kb>+</kb>-knop heeft geklikt om een nieuwe indexer toe te voegen, wordt er een nieuw venster geopend met veel verschillende opties. Voor de doeleinden van deze wiki beschouwt Radarr zowel Usenet-indexers als torrent-trackers als "indexers".

Er zijn twee secties: Usenet en Torrents. Afhankelijk van welke downloadclient u gebruikt, wilt u het type indexer selecteren dat u gaat gebruiken.

Voor torrent-trackers - bijna allemaal vereisen het gebruik van [Prowlarr](/prowlarr) of [Jackett](https://github.com/Jackett/Jackett).

# Downloadclients

`Instellingen` => `Downloadclients`

![Radarr-settings-download-clients.png](/assets/radarr/Radarr-settings-download-clients.png)

Het downloaden en importeren is waar de meeste mensen problemen ondervinden. Vanuit een hoog niveau gezien moet de software kunnen communiceren met uw downloadclient en lees- en schrijftoegang hebben tot de locatie waar de downloadclient bestanden rapporteert die de client downloadt. Er is een grote verscheidenheid aan ondersteunde downloadclients en een nog grotere verscheidenheid aan configuraties. Dit betekent dat hoewel er enkele veelvoorkomende configuraties zijn, er geen juiste configuratie is en de configuratie van iedereen een beetje anders kan zijn. Maar er zijn veel verkeerde configuraties.

> Zie de [instellingenpagina](/radarr/settings#download-clients), de [Meer informatie (Ondersteund)](/radarr/supported#download-clients) pagina voor dit gedeelte, en [TRaSH's Download Client-gidsen](https://trash-guides.info/Downloaders/) voor meer informatie.
{.is-info}

## Downloadprotocollen {.tabset}

### Usenet

{#usenet}

- Radarr stuurt een downloadverzoek naar uw client en koppelt het aan een label of categorie die u heeft geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Radarr controleert de actieve downloads van uw downloadclients die deze categorie gebruiken. Dit gebeurt via de API van uw downloadclient.
- Wanneer de download is voltooid, weet Radarr de definitieve bestandslocatie zoals gerapporteerd door uw downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang het maar ergens apart van uw mediamap is en toegankelijk is voor Radarr.
- Radarr scant die voltooide bestandslocatie op bestanden die Radarr kan gebruiken. Het analyseert de bestandsnaam om deze te vergelijken met de gevraagde media. Als dat lukt, wordt het bestand hernoemd volgens uw specificaties en verplaatst naar de opgegeven medialocatie.
- Atomic Moves (directe verplaatsingen) zijn standaard ingeschakeld. Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediatheek. Als de atomic move mislukt of uw configuratie geen hardlinks en atomic moves ondersteunt, zal Radarr teruggaan naar het kopiëren van het bestand en het vervolgens verwijderen van de bron, wat veel IO vereist.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Radarr, worden overgebleven bestanden van de download naar uw prullenbak of recycling gestuurd via een verzoek aan uw client om de release te verwijderen.

### BitTorrent

{#bittorrent}

- Radarr stuurt een downloadverzoek naar uw client en koppelt het aan een label of categorie die u heeft geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Radarr controleert de actieve downloads van uw downloadclients die deze categorie gebruiken. Deze controle gebeurt via de API van uw downloadclient.
- Voltooide downloads die nog steeds aan het seeden zijn, worden in hun oorspronkelijke locatie achtergelaten zodat u het bestand kunt seeden (ratio of tijd kan worden aangepast in de downloadclient of vanuit Radarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar uw mediamap, maakt Radarr een hardlink naar het bestand als dit wordt ondersteund door uw configuratie, anders wordt het gekopieerd als hardlinks niet worden ondersteund. Torrents die zijn gepauzeerd en volledig zijn geseed, worden direct verplaatst als hardlinks worden ondersteund, anders wordt er gekopieerd en verwijderd.
- Hardlinks zijn standaard ingeschakeld. [Een hardlink gebruikt geen extra schijfruimte.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediamap. Als het maken van een hardlink mislukt of uw configuratie geen hardlinks ondersteunt, zal Radarr teruggaan naar het kopiëren van het bestand.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Radarr, zal Radarr de torrent uit uw client verwijderen en de client vragen om de torrentgegevens te verwijderen, maar alleen als de client rapporteert dat het seeden is voltooid en de torrent is gestopt (gepauzeerd na voltooiing).

# Hoe u uw bestaande georganiseerde mediatheek importeert

> Let op: Radarr zoekt niet regelmatig naar films. Zie de [Hoe werkt Radarr?](/radarr/faq#how-does-radarr-work) FAQ-entry voor details over hoe Radarr werkt.
{.is-info}

Nadat u uw profielen/kwaliteitsgroottes heeft ingesteld en uw indexers en downloadclient(s) heeft toegevoegd, is het tijd om uw bestaande georganiseerde mediatheek te importeren.

`Films`

![Radarr-movies.png](/assets/radarr/Radarr-movies.png)

Selecteer `Bestaande films importeren` of selecteer `Importeren` in de zijbalk.

## Films importeren

![Radarr-movies-import.png](/assets/radarr/Radarr-movies-import.png)

Selecteer het hoofdpad dat u eerder heeft toegevoegd [in het gedeelte Hoofdmappen.](#hoofdmappen)

## Bestaande media importeren

![Radarr-importing-existing.png](/assets/radarr/Radarr-importing-existing.png)

Afhankelijk van hoe goed uw bestaande mappen met films zijn genoemd, zal Radarr proberen deze te koppelen aan de juiste film, zoals te zien is bij Nr.5. Als al uw films zich in één map bevinden, volg dan deze [gids](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

1. De naam van uw filmmapper.
1. Monitor - Hoe u wilt dat de film aan Radarr wordt toegevoegd.

- Geen - Volg de film of collectie niet voor nieuwe releases
- Alleen film - Volg alleen de film voor nieuwe releases
- Film en collectie - Volg zowel de film voor nieuwe releases als voeg en volg eventuele films in de collectie van de film toe (indien aanwezig)

1. Beschikbaarheid - Wanneer Radarr een film als beschikbaar beschouwt.

- **Aangekondigd**: Radarr beschouwt films als beschikbaar zodra ze aan Radarr zijn toegevoegd. Deze instelling wordt *aanbevolen* als u goede privé-trackers heeft die geen vervalsingen bevatten.
- **In de bioscoop**: Radarr beschouwt films als beschikbaar zodra ze in de bioscoop verschijnen. Deze optie wordt *niet aanbevolen*.
- **Uitgebracht**: Radarr beschouwt films als beschikbaar zodra de Blu-ray is uitgebracht. Deze optie wordt *aanbevolen* als uw indexers vaak vervalsingen bevatten.

1. Kwaliteitsprofiel - Selecteer uw voorkeursprofiel.
1. Film - Wat Radarr denkt dat de overeenkomende film is. Het is belangrijk dat u dit controleert en bewerkt/zoekt als de overeenkomst niet correct is. Foutieve overeenkomsten worden vaak veroorzaakt door slecht genoemde mappen.
1. Selecteer de monitorstatus voor meerdere items.
1. Selecteer de minimale beschikbaarheid voor meerdere items.
1. Selecteer het kwaliteitsprofiel voor meerdere items.
1. Start met het importeren van uw bestaande mediatheek.

Zodra een film aan Radarr is toegevoegd, zal Radarr de map van de film scannen en proberen een videobestand in de map te koppelen aan de film. De meest voorkomende reden waarom Radarr het bestand niet koppelt en de film dus de status "Ontbreekt" heeft, is dat de bestandsnaam het jaartal niet bevat. Radarr vereist het jaartal in de bestandsnaam om het te kunnen analyseren.  

### Geen overeenkomst gevonden

Als u een foutmelding krijgt zoals deze

![Radarr-importing-existing-no-match.png](/assets/radarr/Radarr-importing-existing-no-match.png)

Dan heeft u waarschijnlijk een fout gemaakt bij het benoemen van uw filmmappen.

Om dit probleem op te lossen, kunt u het volgende proberen

Breid de foutmelding uit

![Radarr-importing-existing-no-match-expand.png](/assets/radarr/Radarr-importing-existing-no-match-expand.png)

en controleer op [themoviedb](https://www.themoviedb.org/) of het jaartal of de titel overeenkomt. In dit voorbeeld ziet u dat het jaartal onjuist is en u kunt dit corrigeren door het jaartal te wijzigen en op het vernieuwingspictogram te klikken.

![radarr-importing-existing-no-match-expand-refresh.png](/assets/radarr/radarr-importing-existing-no-match-expand-refresh.png)

Of je kunt gewoon de tmdb:id of imdb:id gebruiken (als tmdb is gekoppeld aan imdb) en vervolgens de gevonden film selecteren als deze overeenkomt.

![Radarr-importing-existing-no-match-expand-tmdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-tmdb.png)

![Radarr-importing-existing-no-match-expand-imdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-imdb.png)

### Foutieve mapnaam na import herstellen

![Radarr-wrong-folder-name.png](/assets/radarr/Radarr-wrong-folder-name.png)

Je zult merken dat de mapnaam na de herstelling tijdens de import nog steeds het verkeerde jaar bevat. Om dit op te lossen gaan we een klein trucje doen.

Ga naar het overzicht van je film

`Movies`

Klik bovenaan op `Movie Editor`

![Radarr-movie-editor.png](/assets/radarr/Radarr-movie-editor.png)

Nadat je het hebt geactiveerd, selecteer je de film(s) waarvan je de map(pen) wilt hernoemen.

![Radarr-movie-editor-select.png](/assets/radarr/Radarr-movie-editor-select.png)

1. Als je wilt dat al je filmmappen worden hernoemd naar het eerder ingestelde mapnaamschema [sectie over het benoemen van films](#movie-naming).
2. Selecteer de film(s) waarvan je de map(pen) wilt hernoemen.
3. Kies dezelfde `Root Folder`

Er wordt een nieuw pop-upvenster weergegeven

![Radarr-movie-editor-move-files-yes.png](/assets/radarr/Radarr-movie-editor-move-files-yes.png)

Selecteer `Ja, verplaats de bestanden`

En dan magie

![Radarr-correct-folder-name.png](/assets/radarr/Radarr-correct-folder-name.png)

Zoals je kunt zien, is de map hernoemd naar het juiste jaar volgens je benoemingsschema.

## Hoe voeg je een film toe

Nadat je je bestaande, goed georganiseerde mediatheek hebt geïmporteerd, is het tijd om de films toe te voegen die je wilt.

`Movies` => `Nieuwe toevoegen`

![Radarr-add-new.png](/assets/radarr/Radarr-add-new.png)

Typ in het vak de film die je wilt of gebruik de tmdb:id of imdb:id.

Wanneer je de filmtitel typt, zie je dat er resultaten worden weergegeven.

![Radarr-movie-search.png](/assets/radarr/Radarr-movie-search.png)

Wanneer je de gewenste film ziet, klik je erop.

![Radarr-movie-add.png](/assets/radarr/Radarr-movie-add.png)

1. Root Folder - Radarr voegt de film toe aan de Root Folder die je hebt ingesteld [in de sectie over rootmappen](#root-folders)
1. Monitor - Hoe je wilt dat de film aan Radarr wordt toegevoegd.

- Alleen film = Radarr controleert de RSS-feed op de film in je bibliotheek die je nog niet hebt of verbetert de bestaande film naar een betere kwaliteit.
- Film en collectie = Radarr controleert de RSS-feed op de film in je bibliotheek die je nog niet hebt of verbetert de bestaande film naar een betere kwaliteit. Het voegt ook alle films in de collectie van deze film toe (indien aanwezig) met je geselecteerde instellingen.
- Geen = Radarr controleert de RSS-feed niet, eventuele upgrades of nieuwe films worden genegeerd en moeten handmatig worden gedaan. Alle zoekopdrachten voor niet-gecontroleerde films moeten handmatig worden gestart of interactieve zoekopdrachten zijn.

1. Beschikbaarheid - Wanneer Radarr een film als beschikbaar moet beschouwen.

> Voor meer informatie over de datums van TMDB die van invloed zijn op de onderstaande beschikbaarheden, zie [Hoe bepaalt Radarr het jaar van de film](#how-does-radarr-determine-the-year-of-a-movie)
{.is-info}

- **Aangekondigd**: Radarr beschouwt films als beschikbaar zodra ze aan Radarr zijn toegevoegd. Deze instelling wordt aanbevolen als je goede privé-trackers hebt (of echt goede openbare trackers, zoals rarbg.to) die geen vervalsingen hebben.
- **In de bioscoop**: Radarr beschouwt films als beschikbaar zodra ze in de bioscoop verschijnen (Theatrical Date op TMDb). Deze optie wordt niet aanbevolen.
- **Uitgebracht**: Radarr beschouwt films als beschikbaar zodra de Blu-Ray- of streamingversie is uitgebracht (Digitale en fysieke datums op TMDb). Deze optie wordt aanbevolen en moet waarschijnlijk worden gecombineerd met een beschikbaarheidsvertraging van `-14` of `-21` dagen.
  - Als TMDb niet is ingevuld met een datum, wordt aangenomen dat 90 dagen na `Theatrical Date` (Oudste datum in de bioscoop) de film beschikbaar is op web- of fysieke services.

1. Kwaliteitsprofiel - Selecteer je profiel dat je voor deze film wilt gebruiken
1. Tags - Hier kun je bepaalde tags toevoegen voor geavanceerd gebruik.
1. Zoeken bij toevoegen - Zorg ervoor dat je dit inschakelt als je wilt dat Radarr zoekt naar de ontbrekende film wanneer deze aan Radarr wordt toegevoegd [meer informatie](/radarr/faq#how-does-radarr-find-movies)
1. Klik op `Film toevoegen` om de film aan Radarr toe te voegen.

- Als je een foutmelding krijgt van "pad is al geconfigureerd" [zie deze FAQ-entry](/radarr/faq#path-is-already-configured-for-an-existing-movie)