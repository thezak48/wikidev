---
title: Lidarr Snelstart
description: 
published: true
date: 2022-07-14T14:10:13.343Z
tags: 
editor: markdown
dateCreated: 2021-06-13T06:14:53.615Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Snelstart Installatiegids](#snelstart-installatiegids)
- [Aandachtspunten](#aandachtspunten)
- [Concept](#concept)
  - [Releases (Metadata)](#releases-metadata)
  - [Artiest (Metadata)](#artiest-metadata)
- [Eerste Start](#eerste-start)
- [Instellingen](#instellingen)
  - [Mediabeheer](#mediabeheer)
  - [Profielen](#profielen)
  - [Kwaliteit](#kwaliteit)
  - [Indexers](#indexers)
  - [Downloadclients](#downloadclients)
    - [{.tabset}](#tabset)
      - [Usenet](#usenet)
      - [BitTorrent](#bittorrent)
- [Eerste Artiest](#eerste-artiest)
- [Eerste Download/Import](#eerste-downloadimport)
- [Snelstart - Geavanceerd](#snelstart-geavanceerd)
  - [Lidarr Gebruiksscenario](#lidarr-gebruiksscenario)
    - [Losse bestanden](#losse-bestanden)
    - [Speciale bibliotheken](#speciale-bibliotheken)
  - [Importeren van bestaande bibliotheek of bestanden](#importeren-van-bestaande-bibliotheek-of-bestanden)
    - [Voorbereiden van bestaande bestanden](#voorbereiden-van-bestaande-bestanden)
      - [Mapstructuur](#mapstructuur)
      - [Tagging](#tagging)
    - [Overwegingen voorafgaand aan import](#overwegingen-voorafgaand-aan-import)
    - [Begin met importeren](#begin-met-importeren)

# Snelstart Installatiegids

> Deze pagina is nog in ontwikkeling en niet compleet. Bijdragen zijn welkom.

> Voor een gedetailleerde uitleg van alle instellingen, zie [Lidarr => Instellingen](/lidarr/settings)
{.is-info}

In deze gids zullen we proberen de basisconfiguratie uit te leggen die je moet doen om aan de slag te gaan met Lidarr. We zullen enkele opties overslaan die je op het scherm kunt zien. Als je dieper op die opties wilt ingaan, raadpleeg dan de juiste pagina in de FAQ en documentatie voor een volledige uitleg.

> Houd er rekening mee dat in de screenshots en GUI-instellingen in `oranje` geavanceerde opties worden weergegeven, dus je moet bovenaan de pagina op `Toon geavanceerd` klikken om ze zichtbaar te maken.
{.is-warning}

# Aandachtspunten

In deze gids zullen we de basisstappen uitleggen om aan de slag te gaan met Lidarr. Deze gids gaat ervan uit dat je de applicatie al hebt geïnstalleerd. Installatie-instructies vind je op de volgende pagina: [installatie](/lidarr/installation). We zullen ons richten op de minimale configuratie/opties om een werkende configuratie te krijgen. Er zijn aanvullende instellingen en overwegingen als een van de volgende situaties van toepassing is:

- Bestaande bibliotheek of bestanden
- Onjuist gebruiksscenario
- Onjuiste mapstructuur
- Onjuiste of extreem complexe tagging
- Losse verzameling bestanden
- Muziekbibliotheken op basis van specialiteiten: Klassiek, Singles, Elektronisch

Als een van de bovenstaande situaties van toepassing is, raadpleeg dan het gedeelte Snelstart - Geavanceerd.

Deze gids is opgedeeld in secties. Het wordt aanbevolen om de hele gids te lezen om een volledig begrip te krijgen, maar je kunt naar specifieke secties springen voor directe vragen. Gebruik de inhoudsopgave aan de linkerkant om snel te navigeren.

# Concept

Om Lidarr op de juiste manier te gebruiken, moeten de onderliggende concepten worden begrepen. Op hoog niveau volgt het de principes van de andere Arr-toepassingen. Lidarr fungeert als een muziekbibliotheekbeheersysteem, gegevensaggregator en automatiseringsplatform voor het vinden en downloaden van media.

Daarvan afwijken is behoorlijk substantieel. Het beheer van een muziekbibliotheek is een zeer complex proces, omdat er veel concurrerende variabelen zijn die het proces belemmeren. In tegenstelling tot het beheer van films of tv-shows zijn er geen consistente normen voor het taggen, benoemen of opslaan van muziek. Dit is verder gecompliceerd door de veranderende methoden van muziekdistributie van fysieke media naar elektronische media. Tot slot zijn de meningen over hoe dit beheer moet worden aangepakt zeer uiteenlopend.

Lidarr maakt gebruik van informatie van gegevensaggregatiediensten om de muziekbibliotheek op de juiste manier te taggen en te beheren. Deze gegevens van derden vertegenwoordigen media in gedefinieerde categorieën en typen.

> Als de gegevens niet bestaan in de diensten van derden, kan Lidarr ze NIET beheren.
Details hierover zijn hieronder te vinden om deel te nemen en bij te dragen.
{.is-warning}

De belangrijkste gebruikte dienst is [MusicBrainz](https://musicbrainz.org/). Dit is een gratis dienst die wordt aangedreven door de gemeenschap en uiteindelijk bestaat en overleeft op basis van jouw bijdragen en deelname. Het maken en bijdragen van releases valt buiten de reikwijdte van deze gids. Instructies zijn hier te vinden: [How To Contribute](https://musicbrainz.org/doc/How_to_Contribute)

Uiteindelijk worden de gegevens gedefinieerd door de normen van de gegevens van derden. Als de normen niet overeenkomen met jouw gebruiksscenario, is **Lidarr mogelijk niet de juiste oplossing**. Andere toepassingen voor het beheer van jouw media kunnen zijn:

[Beets Media Management](https://beets.io/)
[MusicBrainz Picard](https://picard.musicbrainz.org/)
[Music Bee](https://getmusicbee.com/)

Deze implementaties kunnen samen met Lidarr worden gebruikt, maar dit valt buiten de reikwijdte van deze gids.

## Releases (Metadata)

Lidarr heeft de `Release`-standaard voor het beheer van muziekmedia geselecteerd. Dit betekent dat voor het systeem om correct te werken, alle media die door het systeem worden verwerkt een `Release` moeten zijn.

Voorbeelden van Releases:

- Album
- EP
- Single
- Uitzending

Elk item dat beheerd moet worden, moet een overeenkomstige `Release` hebben in de gegevensservice van derden.

> `Releases` moeten bestaan in de diensten van derden om in Lidarr te kunnen worden beheerd.

## Artiest (Metadata)

Artiesten zijn precies wat je zou verwachten van de `Release Artiest`. Helaas hebben zaken als de naamgeving van artiesten, stijl, veranderingen in de loop der tijd, gebruikersvoorkeuren en andere redenen de definitie van deze `Release Artiest` vertroebeld.

Voorbeelden van juiste en onjuiste "Artiesten":

- Bob Dylan
- BOB DYLAN
- The Bob Dylan
- Bob Dylan, The
- Bob Dylan & the Band
- Bob Dylan feat. The Band
- The Band featuring Bob Dylan
- ...

Deze lijst kan eindeloos doorgaan. Nogmaals, alle `Releases` zijn gekoppeld aan een `Artiest`. Je moet de juiste `Artiest` vinden (stappen later in deze gids) en gebruiken om een `Release` te downloaden.

> `Release Artiesten` moeten bestaan in de diensten van derden om in Lidarr te kunnen worden beheerd.

# Eerste Start

Na de installatie en het starten van Lidarr kun je er toegang toe krijgen door een browser te openen en naar `http://{jouw_ip_hier}:8686` te gaan.

![lidarr_qs_startup.png](/assets/lidarr/quick-start-guide/lidarr_qs_startup.png)

Er worden twee opties weergegeven op het opstartscherm, maar we zullen die in eerste instantie niet gebruiken.

# Instellingen

We zullen de standaardconfiguratie van de instellingen gebruiken om Lidarr te configureren. Dit maakt gebruik van de bestaande profielen, kwaliteit, tags, enz.

> Voor een gedetailleerde uitleg van alle instellingen, zie [Lidarr > Instellingen](/lidarr/settings)
{.is-info}

## Mediabeheer

Als eerste gaan we kijken naar het `Mediabeheer`, waar we de `Hoofdmap` zullen instellen. Dit wordt de locatie waar de mediabestanden worden opgeslagen.

> Sla Lidarr-media niet op bij een cloudopslagprovider! Vanwege de manier waarop Lidarr tags gebruikt, zal dit alle API-limieten overschrijden en problemen veroorzaken. Bewaar je bibliotheek op je netwerk.
{.is-warning}

Klik op `Instellingen` > `Mediabeheer` in het linkermenu.

![lidarr_qs_mediamanagement.png](/assets/lidarr/quick-start-guide/lidarr_qs_mediamanagement.png)

Klik op `Toevoegen (+)` bij `Hoofdmappen`.

Je krijgt het volgende venster te zien:

![lidarr_qs_rootfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_rootfolder.png)

- **Naam** - Dit is de `Vriendelijke naam` van de opslaglocatie.
- **Pad** - Dit is het daadwerkelijke `Pad` naar de opslaglocatie van de gegevens. Het systeem/de gebruiker moet de juiste machtigingen hebben voor dit opslagpad. Deze map kan niet je downloadlocatie zijn!

Laat de andere opties op hun standaardwaarden staan.

> Als je een `Hoofdmap` met bestaande bestanden gebruikt, bekijk dan het gedeelte Snelstart - Geavanceerd voor overwegingen.
{.is-warning}

> \* Niet-Windows: Als je een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
> \* Als je een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.
{.is-warning}

> **De gebruiker en groep die je hebt geconfigureerd om Lidarr uit te voeren, moeten lees- en schrijftoegang hebben tot deze locatie.** {.is-info}

> Je downloadclient downloadt naar een downloadmap en Lidarr importeert het naar je mediamap (eindbestemming) die je mediaserver gebruikt.
{.is-info}

> **Je downloadmap en mediamap kunnen niet dezelfde locatie zijn**
{.is-danger}

## Profielen

`Instellingen` > `Profielen`

De profielinstellingen blijven op hun standaardwaarden.

## Kwaliteit

`Instellingen` > `Kwaliteit`

De kwaliteitsinstellingen blijven op hun standaardwaarden.

## Indexers

`Instellingen` > `Indexers`

In dit gedeelte stel je de indexer/trackers in die je zult gebruiken om downloadbare mediabestanden te vinden.

Klik op `Toevoegen (+)` bij `Indexers`. Je krijgt een nieuw venster te zien met veel verschillende opties. Lidarr beschouwt zowel Usenet-indexers als BitTorrent-trackers als `Indexers`.

Voeg ten minste één `Indexer` toe om Lidarr in staat te stellen beschikbare bestanden correct te vinden.

Het begrijpen van de configuratie/concepten achter `Indexers` valt buiten de reikwijdte van deze gids. Het internet staat vol met informatie over dit onderwerp.

## Downloadclients

`Instellingen` => `Downloadclients`

![Lidarr-settings-download-clients.png](/assets/lidarr/Lidarr-settings-download-clients.png)

Het downloaden en importeren is waar de meeste mensen problemen ondervinden. Vanuit een hoog niveau gezien moet de software kunnen communiceren met je downloadclient en toegang hebben tot de bestanden die het downloadt. Er is een grote verscheidenheid aan ondersteunde downloadclients en nog veel meer verschillende configuraties. Dit betekent dat hoewel er enkele veelvoorkomende configuraties zijn, er geen juiste configuratie is en de configuratie van iedereen een beetje anders kan zijn. Maar er zijn veel verkeerde configuraties.

> Zie de [instellingenpagina](/lidarr/settings#download-clients), de [Meer informatie (Ondersteund)](/lidarr/supported#download-clients) pagina voor dit gedeelte, en [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) voor meer informatie.
{.is-info}

### {.tabset}

#### Usenet

{#usenet}

- Lidarr stuurt een downloadverzoek naar je client en koppelt het aan een label of categorie die je hebt geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Lidarr controleert de actieve downloads van je downloadclient die die categorie gebruiken. Dit gebeurt via de API van je downloadclient.
- Wanneer de download is voltooid, weet Lidarr de uiteindelijke bestandslocatie zoals gerapporteerd door je downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang het maar ergens apart van je mediamap is en toegankelijk is voor Lidarr.
- Lidarr scant die voltooide bestandslocatie op bestanden die Lidarr kan gebruiken. Het analyseert de bestandsnaam om deze te matchen met de gevraagde media. Als dat lukt, wordt het bestand hernoemd volgens jouw specificaties en verplaatst naar de opgegeven medialocatie.
- Atomic Moves (directe verplaatsingen) zijn standaard ingeschakeld. Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor je voltooide downloadmap en je mediatheek. Als de directe verplaatsing mislukt of je configuratie geen hardlinks en directe verplaatsingen ondersteunt, zal Lidarr teruggaan naar het kopiëren van het bestand en het vervolgens verwijderen van de bron, wat IO-intensief is.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Lidarr, worden overgebleven bestanden van de download naar je prullenbak of recycling gestuurd via een verzoek aan je client om de release te verwijderen.

#### BitTorrent

{#bittorrent}

- Lidarr stuurt een downloadverzoek naar je client en koppelt het aan een label of categorie die je hebt geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Lidarr controleert de actieve downloads van je downloadclient die die categorie gebruiken. Deze controle gebeurt via de API van je downloadclient.
- Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat je het bestand kunt seeden (de verhouding of tijd kan worden aangepast in de downloadclient of vanuit Lidarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar je mediamap, zal Lidarr een hardlink maken naar het bestand als dit wordt ondersteund door je configuratie, anders wordt het bestand gekopieerd als hardlinks niet worden ondersteund.
- Hardlinks zijn standaard ingeschakeld. [Een hardlink zal geen extra schijfruimte gebruiken.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor je voltooide downloadmap en je mediamap. Als het maken van een hardlink mislukt of je configuratie geen hardlinks ondersteunt, zal Lidarr teruggaan naar het kopiëren van het bestand.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Lidarr, zal Lidarr de torrent uit je client verwijderen en de client vragen om de torrentgegevens te verwijderen, maar alleen als de client meldt dat het seeden is voltooid en de torrent is gestopt (gepauzeerd na voltooiing).

# Eerste Artiest

Als je deze gids volgt en je `Hoofdmap` geen mediabestanden bevat, moet je een `Artiest` toevoegen.

`Bibliotheek` > `Nieuwe toevoegen`

![lidarr_qs_addnew.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnew.png)

Dit linkt naar het zoekscherm om een artiest te vinden. Zoek en selecteer de `Artiest` die je wilt toevoegen. Dit opent het venster "Nieuwe artiest toevoegen".

![lidarr_qs_addnewdylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnewdylan.png)

We zullen de standaardselecties gebruiken. Deze moeten het volgende bevatten:

- Hoofdmap - De map die je hebt gemaakt
- Monitoren - Geen
- Kwaliteitsprofiel - Elk
- Tags - (leeg)
- Begin met zoeken naar ontbrekende albums - Niet aangevinkt

Dit zal de download van de `Artiest`-metadata starten. Dit kan even duren, afhankelijk van de hoeveelheid gegevens die verzameld moeten worden. Onthoud dat deze informatie afkomstig is van bronnen van derden en alleen zo compleet is als wat de gemeenschap heeft bijgedragen.

Klik op de zojuist toegevoegde `Artiest`. (Bob Dylan in dit voorbeeld)

> Het standaard `Metadataprofiel` wordt gebruikt, de enige getoonde `Releases` zijn van het type `Studioalbums`.

![lidarr_qs_dylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylan.png)

> Vind je de gedownloade metadata niet leuk? - Draag bij om het beter te maken!
{.is-info}

# Eerste Download/Import

Eindelijk tijd om je eerste `Release` te downloaden/importeren!

Zoek de `Release` die je aan je bibliotheek wilt toevoegen. Selecteer het pictogram voor handmatig zoeken (menselijk) naast de release.

![lidarr_qs_dylanrelease.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanrelease.png)

Dit opent het venster voor het selecteren van de `Release`. In dit venster worden de resultaten van de `Indexer`-query weergegeven, of simpel gezegd de zoekresultaten van beschikbare downloads.

> Het standaard `Kwaliteitsprofiel` staat alle bestandstypen toe. Het standaard `Releaseprofiel` staat alle downloads toe. Voor een gedetailleerde uitleg van deze geavanceerde instellingen, zie [Lidarr > Instellingen](/lidarr/settings)

![lidarr_qs_dylandownload.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylandownload.png)

Bekijk het downloadvenster voor de verschillende verstrekte informatie:

1. Titel - Dit is de naam van de download zoals geretourneerd door de `Indexer`.
1. Kwaliteit - Dit is de kwaliteit zoals bepaald door Lidarr op basis van de titel.
1. De waarschuwingsindicatoren geven een beschrijving van waarom de download niet aan de Lidarr-controles voldoet. In het voorbeeld gaf de zoekopdracht "Verkeerd album" terug.

Als je alles hebt bekeken, selecteer dan het downloadpictogram (nummer 4) om de beschikbare `Release` te downloaden.

Als alles goed is geconfigureerd, wordt de download naar je `Downloadclient` gestuurd.

De download wordt toegevoegd aan de `Wachtrij` en doorloopt de verschillende statussen van je type `Downloadclient`.

Uiteindelijk wordt de download geïmporteerd naar je `Hoofdmap`. Als alles succesvol is verlopen, zou het er als volgt uit moeten zien.

![lidarr_qs_dylansucess.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylansuccess.png)

Je kunt je gedownloade bestanden vinden in je `Hoofdmap` en ze afspelen met de mediaspeler van jouw keuze.

![lidarr_qs_dylanfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanfolder.png)

# Snel aan de slag - Geavanceerd

Dit geavanceerde gedeelte is bedoeld voor configuraties die mogelijk speciale overwegingen vereisen. Bekijk dit gedeelte als er toepassingen zijn op uw configuratie en bespaar mogelijk wat hoofdpijn.

> De volgende secties zullen helpen bij veelvoorkomende valkuilen en problemen.
{.is-warning}

## Lidarr Gebruiksscenario

Zoals eerder vermeld in het gedeelte Concept. Lidarr moet niet worden gebruikt als uw beoogde gebruik niet overeenkomt met het beheersysteem van Lidarr's `Releases`. Lidarr werkt NIET met de volgende gebruiksscenario's:

- Losse verzameling bestanden - Bestanden van meerdere artiesten (geen compilaties) of meerdere `Releases`
- Muziekbibliotheken op basis van specialiteit: Klassiek, Singles, Elektronisch

### Losse bestanden

Weinig tot geen beheer van losse bestanden werkt niet met Lidarr. Het is het beste om deze bestanden niet te proberen te gebruiken met Lidarr.

### Speciale bibliotheken

Speciale bibliotheken creëren unieke problemen voor elk beheersysteem. Deze situaties kunnen werken met Lidarr, maar het kan veel werk van uw kant vereisen, waarbij de ingebouwde automatisering grotendeels wordt genegeerd. Bijvoorbeeld:

- **Klassieke muziek** - Heeft meestal uitgebreide tagvereisten of wensen. Metadata van `Releases` zal waarschijnlijk niet bestaan of onjuist zijn.
- **Singles** - Singles kunnen geen echte `Releases` zijn. Gegevensservices van derden zullen geen metadata retourneren. Ze worden niet geautomatiseerd en Lidarr kan geen beheer toepassen.
- **Elektronisch** - Dit is NIET van toepassing op `Releases` in het elektronische genre. Dit heeft betrekking op bibliotheken met mixen, beats, samples, enz. (Beatport). Gegevensbronnen van derden herkennen deze niet als `Releases`. Ze worden niet geautomatiseerd en Lidarr kan geen beheer toepassen.

## Importeren van bestaande bibliotheek of bestanden

> Let op dat Lidarr niet regelmatig zoekt naar Releases. Raadpleeg deze twee FAQ-items voor details om te begrijpen hoe Lidarr werkt.
[Hoe vindt Lidarr releases?](/lidarr/faq#how-does-lidarr-find-releases) en [Hoe werkt Lidarr?](/lidarr/faq#how-does-lidarr-work)
{.is-info}

> Geautomatiseerde import is een gepland proces en kan niet worden gestopt nadat het is gestart.
Voeg GEEN `Root Folder` toe met bestaande bestanden totdat u dit gedeelte volledig hebt doorgenomen.
{.is-warning}

Lidarr maakt gebruik van een geautomatiseerd systeem om `Release Artists` en `Releases` toe te voegen die zich bevinden in uw `Root Folder`.

Als het gebruiksscenario van Lidarr overeenkomt en u geen unieke of speciale bibliotheken heeft, kunt u doorgaan met het importeren van uw bestaande bibliotheek.

Het is van cruciaal belang dat uw bestaande bibliotheekbestanden gestructureerd zijn en voldoen aan het beheersysteem van Lidarr's `Releases`. Dit betekent dat het volgende niet werkt:

- Onjuiste mapstructuur - Bestanden bevinden zich in één map - Raadpleeg de sectie Voorbereiden>Mapstructuur
- Onjuiste of extreem ingewikkelde tagging - Raadpleeg de sectie Voorbereiden>Tagging

### Voorbereiden van uw bestaande bestanden

Om het geautomatiseerde proces te laten werken, moeten uw bestanden worden voorbereid om ervoor te zorgen dat dit efficiënt verloopt of überhaupt werkt.

#### Mapstructuur

Het wordt aanbevolen om de standaard mapstructuur te volgen:

\Root Folder\Release Artist\Release\XX - Track

In combinatie met de juiste tags zorgt dit ervoor dat bijna 95% of meer herkenning mogelijk is door mediaspelers.

#### Tagging

Tagging kan een ingewikkeld proces zijn. De hoeveelheid bestanden en hoe ze momenteel zijn getagd, bepalen de hoeveelheid inspanning die nodig is.

De aanbevolen methoden voor het taggen van uw bestanden zijn onder andere:

- MusicBrainz Picard
- Beets
- MusicBee, MediaMonkey, JRiver

Het gebruik van deze applicaties valt buiten de reikwijdte van deze handleiding, maar het is raadzaam om MusicBrainz Release ID's te associëren als onderdeel van het tagproces.

> De meeste tag-software kan de mapstructuur en bestandsnaam wijzigen terwijl ze de bestanden correct taggen.
{.is-info}

### Overwegingen vóór import

Zodra de bestanden correct zijn getagd en benoemd, moeten de volgende items worden geverifieerd om ervoor te zorgen dat het proces succesvol wordt voltooid:

- **Systeemarchitectuur** - Aanbevolen x64 / 64-bits - Het importeren van grote bibliotheken vereist dat het systeem grote hoeveelheden RAM kan gebruiken en efficiënter kan berekenen. x86 / 32-bits wordt ondersteund, maar is niet zo efficiënt en kost aanzienlijk meer tijd.
- **Systeemvereiste voor geheugen (RAM)** - Minimaal 4 GB, Aanbevolen 8 GB - Het importproces vereist veel geheugen en als Lidarr importeert en een browser open heeft, zal dit leiden tot aanzienlijk veel RAM-gebruik.
- **Beperkingen voor `Release` schijf/track** - Releases met veel tracks of schijven moeten uit het importproces worden verwijderd. Ze kunnen handmatig worden geïmporteerd met behulp van de ingebouwde procedures. Er is geen exacte limiet, maar om veilig te zijn, moeten releases met meer dan 25 schijven of 250 tracks worden verwijderd.
- **`Release Artist` met veel `Releases`** - Het geautomatiseerde proces van Lidarr vergelijkt releases met uw bestanden. Hoewel het niet waarschijnlijk is dat dit mislukt, zal het doorlopen van deze bestanden via de geautomatiseerde procedure leiden tot een aanzienlijke toename van de importtijd. Er zijn individuele artiesten met duizenden releases.
- **Tijd** - Het geautomatiseerde importproces kost tijd. Een redelijke schatting zou zijn 1 uur voor 500 correct getagde `Releases`. Dit is sterk variabel op basis van uw opslag, internetsnelheid en systeemprestaties.

### Begin met importeren

//

Binnenkort beschikbaar

- Monitor * - Hiermee stelt u de standaard bewakingsoptie (`Releases`) in voor de `Root Folder`.
- Kwaliteitsprofiel * - Hiermee stelt u de standaard kwaliteitsoptie in voor de `Root Folder`.
- Metagegevensprofiel * - Hiermee stelt u de standaard metagegevensoptie in voor de `Root Folder`.