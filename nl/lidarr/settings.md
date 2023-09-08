---
title: Lidarr-instellingen
description: 
published: true
date: 2022-07-24T14:21:19.994Z
tags: lidarr, needs-love, instellingen
editor: markdown
dateCreated: 2021-06-14T21:36:07.513Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Instellingen](#instellingen)
- [Downloadclients](#downloadclients)
  - [Overzicht](#overzicht)
  - [Processen van downloadclients](#processen-van-downloadclients)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Downloadclients](#downloadclients-1)
    - [Ondersteunde downloadclients](#ondersteunde-downloadclients)
    - [Instellingen voor Usenet-client](#instellingen-voor-usenet-client)
    - [Instellingen voor Torrent-client](#instellingen-voor-torrent-client)
    - [Compatibiliteit verwijderen download in Torrent-client](#compatibiliteit-verwijderen-download-in-torrent-client)
  - [Afhandeling voltooide downloads](#afhandeling-voltooide-downloads)
    - [Voltooide downloads verwijderen](#voltooide-downloads-verwijderen)
    - [Afhandeling mislukte downloads](#afhandeling-mislukte-downloads)
  - [Mappen voor externe paden](#mappen-voor-externe-paden)
- [Importlijsten](#importlijsten)
  - [Importlijsten](#importlijsten-1)
  - [Uitsluitingen importlijst](#uitsluitingen-importlijst)
  - [Een importlijst toevoegen](#een-importlijst-toevoegen)
- [Verbindingen](#verbindingen)
- [Tags](#tags)
- [Algemeen](#algemeen)
  - [Updates](#updates)

# Instellingen

Deze pagina is nog in ontwikkeling en bijdragen - gebaseerd op andere \*Arr-pagina's - zijn welkom en worden sterk aangemoedigd.

# Downloadclients

> Informatie over ondersteunde downloadclients is te vinden op de [Meer informatie (Ondersteund)](/lidarr/ondersteund#downloadclients) pagina voor dit gedeelte
{.is-info}

## Overzicht

- Het downloaden en importeren is waar de meeste mensen problemen ervaren. Vanuit een hoog niveau gezien moet de software kunnen communiceren met uw downloadclient en toegang hebben tot de bestanden die het downloadt. Er zijn veel verschillende ondersteunde downloadclients en nog veel meer verschillende configuraties. Dit betekent dat hoewel er enkele veelvoorkomende configuraties zijn, er geen juiste configuratie is en de configuratie van iedereen een beetje anders kan zijn. Maar er zijn veel foute configuraties.

## Processen van downloadclients

## Usenet

- Lidarr stuurt een downloadverzoek naar uw client en koppelt het aan een label- of categorienaam die u hebt geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Lidarr controleert de actieve downloads van uw downloadclients die deze categorienaam gebruiken. Dit gebeurt via de API van uw downloadclient.
- Wanneer de download is voltooid, weet Lidarr de uiteindelijke bestandslocatie zoals gerapporteerd door uw downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang deze maar ergens apart van uw mediabibliotheek staat en toegankelijk is voor Lidarr.
- Lidarr scant die voltooide bestandslocatie op bestanden die Lidarr kan gebruiken. Het analyseert de bestandsnaam om deze te vergelijken met de gevraagde media. Als dat lukt, wordt het bestand hernoemd volgens uw specificaties en verplaatst naar de opgegeven mediabibliotheek.
- Atomic Moves (directe verplaatsingen) zijn standaard ingeschakeld. Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediabibliotheek. Als de atomic move mislukt of uw configuratie geen hardlinks en atomic moves ondersteunt, zal Lidarr terugvallen op het kopiëren van het bestand en vervolgens verwijderen van de bron, wat intensief is voor de IO.
- Als de optie "Afhandeling voltooide downloads - Verwijderen" is ingeschakeld in de instellingen van Lidarr, worden overgebleven bestanden van de download naar uw prullenbak of recycling gestuurd via een verzoek aan uw client om de release te verwijderen.

## BitTorrent

- Lidarr stuurt een downloadverzoek naar uw client en koppelt het aan een label- of categorienaam die u hebt geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Lidarr controleert de actieve downloads van uw downloadclients die deze categorienaam gebruiken. Deze controle gebeurt via de API van uw downloadclient.
- Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat u het bestand kunt seeden (de verhouding of tijd kan worden aangepast in de downloadclient of vanuit Lidarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar uw mediabibliotheek, zal Lidarr een harde koppeling maken naar het bestand als dit wordt ondersteund door uw configuratie, anders wordt het bestand gekopieerd als harde koppelingen niet worden ondersteund.
- Harde koppelingen zijn standaard ingeschakeld. [Een harde koppeling gebruikt geen extra schijfruimte.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediabibliotheek. Als het maken van een harde koppeling mislukt of uw configuratie geen harde koppelingen ondersteunt, zal Lidarr het bestand kopiëren.
- Als de optie "Afhandeling voltooide downloads - Verwijderen" is ingeschakeld in de instellingen van Lidarr, zal Lidarr de torrent verwijderen uit uw client en de client vragen om de torrentgegevens te verwijderen, maar alleen als de client rapporteert dat het seeden is voltooid en de torrent is gestopt (gepauzeerd na voltooiing).

## Downloadclients

Klik op `Instellingen => Downloadclients` en klik vervolgens op het <kb>+</kb> om een nieuwe downloadclient toe te voegen. Uw downloadclient moet al geconfigureerd en actief zijn.

### Ondersteunde downloadclients

- Een lijst met ondersteunde downloadclients is te vinden op de [Meer informatie (Ondersteund)](/lidarr/ondersteund#downloadclient) pagina voor dit gedeelte

Selecteer de downloadclient die u wilt toevoegen en er verschijnt een pop-upvenster om de verbindingsgegevens in te voeren. Deze gegevens zijn vergelijkbaar voor de meeste clients. Sommige vragen om een gebruikersnaam of wachtwoord, andere vragen of nieuwe downloads in een gepauzeerde/startstatus moeten worden toegevoegd, enz.

### Instellingen voor Usenet-client

- Naam - De naam van de downloadclient binnen Lidarr
- Inschakelen - Deze downloadclient inschakelen
- Host - De URL van uw downloadclient
- Poort - De poort van uw downloadclient
- Gebruik SSL - Gebruik een beveiligde verbinding met uw downloadclient. Let op deze veelvoorkomende fout.
- (Geavanceerde optie) URL-basis - Voeg een voorvoegsel toe aan de URL; dit is vaak nodig voor omgekeerde proxies.
- API-sleutel - De API-sleutel om te authenticeren bij uw client
- Gebruikersnaam - De gebruikersnaam om te authenticeren bij uw client (meestal niet nodig)
- Wachtwoord - Het wachtwoord om te authenticeren bij uw client (meestal niet nodig)
- Categorie - De categorie binnen uw downloadclient die \*Arr zal gebruiken. Om te voorkomen dat niet-gerelateerde downloads worden weergegeven in de activiteit, wordt sterk aanbevolen om een categorie in te stellen.
- Prioriteit recent - Downloadclientprioriteit voor recent uitgebrachte media
- Prioriteit ouder - Downloadclientprioriteit voor niet recent uitgebrachte media
- (Geavanceerde optie) Prioriteit client - Prioriteit van de downloadclient. Round-Robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) met dezelfde prioriteit. 1 is de hoogste prioriteit en 50 is de laagste prioriteit

### Instellingen voor Torrent-client

- Naam - De naam van de downloadclient binnen Lidarr
- Inschakelen - Deze downloadclient inschakelen
- Host - De URL van uw downloadclient
- Poort - De poort van uw downloadclient; dit is meestal de webgui-poort
- Gebruik SSL - Gebruik een beveiligde verbinding met uw downloadclient. Let op deze veelvoorkomende fout.
- (Geavanceerde optie) URL-basis - Voeg een voorvoegsel toe aan de URL; dit is vaak nodig voor omgekeerde proxies.
- Gebruikersnaam - De gebruikersnaam om te authenticeren bij uw client
- Wachtwoord - Het wachtwoord om te authenticeren bij uw client
- Categorie - De categorie binnen uw downloadclient die \*Arr zal gebruiken. Om te voorkomen dat niet-gerelateerde downloads worden weergegeven in de activiteit, wordt sterk aanbevolen om een categorie in te stellen.
- Categorie na import - De categorie die moet worden ingesteld nadat de release is gedownload en geïmporteerd. Houd er rekening mee dat dit de verwijdering van afgehandelde downloads verbreekt.
- Prioriteit recent - Downloadclientprioriteit voor recent uitgebrachte media
- Prioriteit ouder - Downloadclientprioriteit voor niet recent uitgebrachte media
- Initiële status - Initiële status voor torrents (alleen Qbittorrent: geforceerd omzeilt alle seeddrempels)
- (Geavanceerde optie) Prioriteit client - Prioriteit van de downloadclient. Round-Robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) met dezelfde prioriteit. 1 is de hoogste prioriteit en 50 is de laagste prioriteit

### Compatibiliteit verwijderen download in Torrent-client

- Lidarr kan alleen de seedverhouding/tijd instellen op clients die deze waarde kunnen instellen via hun API bij het toevoegen van de torrent. Seeddoelen kunnen globaal worden ingesteld in de client zelf of per tracker in de \*Arr-instellingen voor elke indexer. Zie de onderstaande tabel voor de compatibiliteit van clients.

|      Client       |                                Verhouding                                |                                   Tijd                                   |
| :---------------: | :---------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)   |   ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)   |
|      Deluge       |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)   |   ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)   |
| Download Station  | ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek) |   ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)   |
|       Flood       |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)   |     ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)     |
|     Hadouken      | ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek) |   ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)   |
|    qBittorrent    |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)   |     ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)     |
|     rTorrent      |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)   |     ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)     |
| Torrent Blackhole | ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek) |   ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)   |
|   Transmission    |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)   | ![Idle-limiet](https://img.shields.io/badge/Ondersteund-Idle%20limiet*-blauw) |
|     uTorrent      |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)   |     ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)     |
|       Vuze        |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)   |     ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)     |

> ![Idle-limiet](https://img.shields.io/badge/Ondersteund-Idle%20limiet*-blauw) - Transmission heeft intern een controle op de inactiviteitstijd, maar Lidarr vergelijkt deze met de seedtijd als de inactiviteitslimiet is ingesteld op basis van een specifieke torrent. Dit wordt gedaan als een workaround voor de beperkingen van de api van Transmission.{.is-info}

## Afhandeling voltooide downloads

- Afhandeling voltooide downloads is hoe Lidarr media importeert van uw downloadclient naar uw serie-mappen.

- Inschakelen (Geavanceerde globale instelling) - Voltooide downloads automatisch importeren van de downloadclient
- Verwijderen (Per client-instelling) - Voltooide downloads verwijderen wanneer deze zijn voltooid (usenet) of gestopt/voltooid (torrents)
  - Voor torrents moet uw downloadclient pauzeren wanneer de seeddoelen zijn bereikt. Het vereist ook dat de seeddoelen worden ondersteund door Lidarr volgens de bovenstaande tabel. Torrents moeten ook in dezelfde categorie blijven.

### Voltooide downloads verwijderen

- Lidarr stuurt een downloadverzoek naar uw client en koppelt het aan een label- of categorienaam die u hebt geconfigureerd in de instellingen van de downloadclient.
- Lidarr controleert de actieve downloads van uw downloadclients die deze categorienaam gebruiken. Dit gebeurt via de API van uw downloadclient.
- Wanneer de download is voltooid, weet Lidarr de uiteindelijke bestandslocatie zoals gerapporteerd door uw downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang deze maar ergens apart van uw mediabibliotheek staat.
- Lidarr scant die voltooide bestandslocatie op videobestanden. Het analyseert de bestandsnaam van de video om deze te vergelijken met een aflevering. Als dat lukt, wordt het bestand hernoemd volgens uw specificaties en verplaatst naar de toegewezen bibliotheekmap.
- Overgebleven bestanden van de download worden naar uw prullenbak of recycling gestuurd.

Als u downloadt met een BitTorrent-client, verloopt het proces iets anders:

- Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat u kunt seeden. Wanneer bestanden worden geïmporteerd naar uw toegewezen bibliotheekmap, zal Lidarr proberen een harde koppeling te maken naar het bestand of overschakelen naar kopiëren (dubbele ruimte gebruiken) als harde koppelingen niet worden ondersteund.
- Als de optie "Afhandeling voltooide downloads - Verwijderen" is ingeschakeld in de instellingen, zal Lidarr de torrentclient vragen om het oorspronkelijke bestand en de torrent te verwijderen, maar dit gebeurt alleen als de client rapporteert dat het seeden is voltooid, de torrent in dezelfde categorie staat (d.w.z. geen gebruik van een categorie na import) en de torrent is gepauzeerd (gestopt).

### Afhandeling mislukte downloads

- Afhandeling mislukte downloads is alleen compatibel met SABnzbd en NZBGet.
- Afhandeling mislukte downloads is niet van toepassing op torrents en er zijn geen plannen om deze functionaliteit toe te voegen.

- Er zijn verschillende componenten die deel uitmaken van het proces van afhandeling van mislukte downloads:

- Controleer downloader:
  - Wachtrij - Controleer de wachtrij van uw downloader op beveiligde (gecodeerde) releases die als mislukt zijn gemarkeerd
  - Geschiedenis - Controleer de geschiedenis van uw downloader op mislukkingen (bijv. niet genoeg blokken om te repareren, of extractie mislukt)
- Wanneer Lidarr een mislukte download vindt, begint het met het verwerken ervan en doet het een aantal dingen:
  - Voegt een mislukt evenement toe aan de geschiedenis van Lidarr
  - Verwijdert de mislukte download uit de downloadclient om ruimte vrij te maken en gedownloade bestanden te wissen (optioneel)
  - Begint te zoeken naar een vervangend bestand (optioneel)
  - Blokkeerlijst (voorheen 'Blacklist') maakt automatisch overslaan van nzbs mogelijk wanneer ze mislukken, dit betekent dat die nzb nooit meer automatisch door Lidarr wordt gedownload (u kunt de download nog steeds afdwingen via een handmatige zoekopdracht).
  - Er zijn 2 geavanceerde opties (op de pagina 'Downloadclient' instellingen) die het gedrag van mislukte downloads in Lidarr bepalen, op dit moment staan ze allemaal standaard aan.

- Opnieuw downloaden - Bepaalt of Lidarr al dan niet naar hetzelfde bestand zal zoeken na een mislukking
- (Geavanceerde optie) Verwijderen - Bepaalt of de download automatisch moet worden verwijderd uit de downloadclient wanneer de mislukking wordt gedetecteerd

## Mappen voor externe paden

- Mappen voor externe paden fungeren als een eenvoudige zoekopdracht naar een extern pad en vervangen dit door een lokaal pad. Dit wordt voornamelijk gebruikt voor samengevoegde lokale/externe configuraties met behulp van mergerfs of iets dergelijks, of wordt gebruikt wanneer de toepassing en de downloadclient zich niet op dezelfde server bevinden.
- Een externe padmapping wordt gebruikt wanneer uw downloadclient een pad rapporteert voor voltooide gegevens, hetzij op een andere server, hetzij op een manier die \*Arr niet naar die map verwijst.
- Over het algemeen is een externe padmapping alleen nodig als uw downloadclient op Linux staat terwijl \*Arr op Windows staat of vice versa. Een externe padmapping is ook mogelijk nodig bij het mixen van Docker- en Native-clients of bij het gebruik van een externe server.
- Een externe padmapping is een DOMME zoek/vervang (waar het de WAARDE van het EXTERNE pad vindt, vervangt het door de WAARDE van het LOKALE pad voor de opgegeven Host).
- Als het foutbericht over een ongeldig pad de VERVANGENDE waarde niet bevat, werkt de padmapping niet zoals u verwacht. De gebruikelijke oplossing is om de mapping toe te voegen en te verwijderen.
- [Zie de tutorial van TRaSH voor aanvullende informatie over externe padmapping](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Als zowel \*Arr als uw Download Client Docker Containers zijn, is het zelden nodig om een externe padmapping te gebruiken. Het wordt aanbevolen om de [Docker-handleiding](/docker-guide) te raadplegen en/of de [Tutorial van TRaSH](https://trash-guides.info/hardlinks) te volgen.
{.is-info}

# Importeerlijsten

> Informatie over ondersteunde lijsttypen is te vinden op de pagina [Meer informatie (Ondersteund)](/lidarr/supported#lists) voor dit gedeelte.
{.is-info}

Importeerlijsten stellen u in staat om items aan Lidarr toe te voegen vanuit Spotify of Last.fm. Dit kan veel onverwachte items aan uw Lidarr-database toevoegen, dus gebruik het alstublieft met zorg.

<!-- ![importlists.png](/assets/readarr/importlists.png) -->

## Importeerlijsten

Hier ziet u de lijsten die u momenteel heeft en kunt u nieuwe lijsten toevoegen. Het toevoegen van lijsten wordt hieronder in meer detail besproken.

## Importeerlijstuitsluitingen

Alles wat hier staat, is uitgesloten van toevoeging door lijsten en zal nooit worden toegevoegd vanuit welke lijst dan ook. U kunt items hiervan verwijderen door erop te klikken.

## Een importeerlijst toevoegen

Na het klikken op het <kb>+</kb>, kiest u het soort lijst dat u wilt toevoegen:

<!-- ![addlist.png](/assets/readarr/addlist.png) -->

In dit geval gaan we een lijst van opgeslagen albums van Spotify toevoegen.

<!-- ![bookshelflist.png](/assets/readarr/bookshelflist.png) -->

- Naam - Voer een naam in voor deze lijst.
- Automatisch toevoegen inschakelen - Als dit is ingeschakeld, worden alle items op de lijst automatisch aan Lidarr toegevoegd.

> Dit voegt ALLE ALBUMS van die artiest toe aan Lidarr!

- Monitoren - Selecteer uw monitoringsniveau voor toegevoegde items. Geldige opties zijn `Geen`, `Specifiek album` en `Alle albums van de artiest`. Alle albums worden aan Lidarr toegevoegd, maar worden gemonitord of niet gemonitord op basis van deze selectie.
- Hoofdmap - Kies de hoofdmap voor artiesten die vanuit deze lijst worden toegevoegd.
- Nieuwe albums monitoren - Kies wat Lidarr moet doen met toekomstige albums van de toegevoegde artiest. Geldige opties zijn `Alle albums`, `Geen`, `Nieuw`.
- Kwaliteitsprofiel - Kies uw kwaliteitsprofiel voor artiesten die vanuit deze lijst worden toegevoegd.
- Metagegevensprofiel - Kies uw metagegevensprofiel voor artiesten die vanuit deze lijst worden toegevoegd.
- Lidarr-tags - Kies welke tags van toepassing zijn op artiesten die vanuit deze lijst worden toegevoegd.

> Het wordt sterk aanbevolen om hier een beschrijvende tag toe te voegen. Anders weet u niet welke lijst deze items aan Lidarr heeft toegevoegd, en zodra ze zijn toegevoegd, kunt u deze informatie nooit meer krijgen! Deze informatie wordt niet gelogd!

Standaard worden lijsten elke 24 uur gesynchroniseerd, maar u kunt dit handmatig activeren vanaf de pagina `Systeem` => `Taken`. U kunt dit proces niet sneller automatiseren dan dat.

# Verbindingen

> Informatie over ondersteunde verbindingssoorten is te vinden op de pagina [Meer informatie (Ondersteund)](/lidarr/supported#notifications) voor dit gedeelte.
{.is-info}

# Tags

- Het tag-gedeelte in Lidarr wordt gebruikt om verschillende aspecten van Lidarr met elkaar te verbinden.
- Tags zijn met name handig voor:

  - Vertragingsprofielen
  - Uitgaveprofielen
  - Indexers

- Tags kunnen worden gebruikt om Vertragingsprofielen, Uitgaveprofielen, Indexers en Artiesten/Albums met elkaar te verbinden.
- Bijvoorbeeld:
  - U wilt dat een specifieke Artiest/Album alleen een specifieke indexer gebruikt. U zou een tag maken en de Artiest/Album en indexer aan die tag toewijzen.
  - U wilt dat een specifiek Uitgaveprofiel alleen een specifiek Vertragingsprofiel gebruikt. U zou een tag maken en het Uitgaveprofiel en Vertragingsprofiel aan die tag toewijzen.

> Opmerking: Tags hebben geen invloed op "Kwaliteitsprofielen", "Metagegevensprofielen" of andere aspecten die hierboven niet worden genoemd.
{.is-info}

# Algemeen

## Updates

- (Geavanceerde optie) Branch - Dit is de branch van Lidarr die u gebruikt.
  - [Zie deze FAQ voor meer informatie](/lidarr/faq#how-do-i-update-lidarr)
- Automatisch - Updates automatisch downloaden en installeren. U kunt nog steeds installeren via Systeem: Updates. Opmerking: Windows-gebruikers worden altijd automatisch bijgewerkt.
- Mechanisme - Gebruik de ingebouwde updater van Lidarr of een script
  - Ingebouwd - Gebruik de eigen updater van Lidarr
  - Script - Laat Lidarr het update-script uitvoeren
  - Docker - Werk Lidarr niet bij vanuit de Docker, maar haal een gloednieuwe image op met de nieuwe update
- Script - Alleen zichtbaar wanneer Mechanisme is ingesteld op Script - Pad naar update-script
- Updateproces - Lidarr zal het updatebestand downloaden, de integriteit ervan controleren en het naar een tijdelijke locatie extraheren en de gekozen methode aanroepen. Het updateproces wordt uitgevoerd onder dezelfde gebruiker als waar Lidarr onder wordt uitgevoerd, het heeft toestemming nodig om de Lidarr-bestanden bij te werken en Lidarr te stoppen/starten.
- Ingebouwd - De ingebouwde methode maakt een back-up van Lidarr-bestanden en -instellingen, stopt Lidarr, werkt de installatie bij en start Lidarr opnieuw op. Als uw systeem het stoppen van Lidarr niet aankan en automatisch probeert het opnieuw te starten, is het misschien beter om in plaats daarvan een script te gebruiken. Bij een mislukking wordt de vorige versie van Lidarr opnieuw gestart.
- Script - Het script moet hetzelfde behandelen als de ingebouwde updater. Als u services wilt stoppen en starten (upstart/launchd/etc), moet u dat hier doen.