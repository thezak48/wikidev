---
title: Sonarr Snelstartgids
description: 
published: true
date: 2022-07-14T14:07:19.793Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-09-03T19:14:22.283Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Snelstart Installatiegids](#snelstart-installatiegids)
- [Opstarten](#opstarten)
- [Mediabeheer](#mediabeheer)
  - [Aflevering benaming](#aflevering-benaming)
  - [Importeren](#importeren)
  - [Hoofdmappen](#hoofdmappen)
- [Profielen](#profielen)
- [Indexers](#indexers)
- [Download Clients](#download-clients)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
- [Hoe je je bestaande georganiseerde mediatheek importeert](#hoe-je-je-bestaande-georganiseerde-mediatheek-importeert)
  - [Afleveringen importeren](#afleveringen-importeren)
    - [Bestaande media importeren](#bestaande-media-importeren)
    - [Geen overeenkomst gevonden](#geen-overeenkomst-gevonden)
    - [Foutieve mapnaam na import herstellen](#foutieve-mapnaam-na-import-herstellen)
- [Nieuwe serie toevoegen](#nieuwe-serie-toevoegen)

# Snelstart Installatiegids

> Deze pagina is nog in ontwikkeling en niet compleet. Bijdragen zijn welkom.

> Voor een gedetailleerdere uitleg van alle instellingen, bekijk [Sonarr => Instellingen](/sonarr/settings)
{.is-info}

In deze gids zullen we proberen de basisinstellingen uit te leggen die je moet doen om aan de slag te gaan met Sonarr. We zullen enkele opties overslaan die je op het scherm kunt zien. Als je hier dieper op in wilt gaan, raadpleeg dan de juiste pagina in de FAQ en documentatie voor een volledige uitleg.

> Houd er rekening mee dat de geavanceerde opties in de screenshots en GUI-instellingen in `oranje` zijn, dus je moet bovenaan de pagina op `Toon geavanceerd` klikken om ze zichtbaar te maken.
{.is-warning}

# Opstarten

Na installatie en het opstarten, open je een browser en ga je naar `http://{jouw_ip_hier}:8989`

![qs_startup.png](/assets/sonarr/qs_startup.png)

# Mediabeheer

Als eerste gaan we kijken naar de instellingen voor `Mediabeheer`, waar we onze voorkeursbenaming en bestandsbeheerinstellingen kunnen instellen.

Klik op `Instellingen` => `Mediabeheer` in het linker menu.

## Aflevering benaming

![qs_episodenaming.png](/assets/sonarr/qs_episodenaming.png)

- Vink het vakje aan om Afleveringen hernoemen in te schakelen.
- Beslis over je standaard, dagelijkse en anime aflevering benaming conventies. Je zou de aanbevolen benaming conventies [hier](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/) moeten bekijken.

> Als je ervoor kiest om geen kwaliteit/resolutie of releasegroep op te nemen, is dit informatie die je later niet meer kunt terugkrijgen. Het wordt sterk aanbevolen om deze op te nemen in je benaming conventie.
{.is-info}

## Importeren

![mm_importing.png](/assets/sonarr/mm_importing.png)

- (Geavanceerde optie) Als je wilt dat TBA-afleveringen direct worden geïmporteerd, wijzig dan "Vereiste afleveringstitel" in "Nooit".
- (Geavanceerde optie) Schakel `Gebruik hardlinks in plaats van kopiëren` in voor meer informatie over hoe en waarom met voorbeelden [TRaSH's Hardlinks Guide](https://trash-guides.info/hardlinks).
- Vink het vakje aan om extra bestanden te importeren en voeg ten minste `.srt` toe aan de lijst.

## Hoofdmappen

Hier voegen we de hoofdmap toe die Sonarr zal gebruiken om je bestaande georganiseerde mediatheek te importeren en waar Sonarr je media zal importeren (kopiëren/hardlinken/verplaatsen) nadat je downloadclient het heeft gedownload. Dit is de map waar je series en afleveringen zijn opgeslagen, zodat je mediaspeler ze kan afspelen. Dit is NIET de map waar je bestanden naar downloadt!

> \* Gebruikers van niet-Windows: Als je een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
> \* Als je een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.
{.is-warning}

> **De gebruiker en groep die je hebt geconfigureerd om Sonarr uit te voeren, moeten lees- en schrijftoegang hebben tot deze locatie.**
{.is-info}

> **Je downloadmap en mediamap kunnen niet dezelfde locatie zijn**
{.is-danger}

Vergeet niet om je wijzigingen op te slaan!

# Profielen

`Instellingen` => `Profielen`

We raden je aan om je eigen profielen te maken en alleen de gewenste kwaliteitsbronnen te selecteren. Er zijn echter ook verschillende voorgedefinieerde kwaliteitsprofielen beschikbaar om uit te kiezen, als een van die profielen geschikt is. Als je meer informatie wilt over profielen, raadpleeg dan de [juiste wiki-pagina](/sonarr/settings#profiles) voor dat gedeelte.

# Indexers

`Instellingen` => `Indexers`

Hier voeg je de indexer/trackers toe die je daadwerkelijk zult gebruiken om je bestanden te downloaden.

Nadat je op de <kb>+</kb> knop hebt geklikt om een nieuwe indexer toe te voegen, krijg je een nieuw venster te zien met veel verschillende opties. Voor de doeleinden van deze wiki beschouwt Sonarr zowel Usenet-indexers als Torrent-trackers als "Indexers".

Er zijn hier twee secties: Usenet en Torrents. Afhankelijk van welke downloadclient je zult gebruiken, wil je het type indexer selecteren dat je gaat gebruiken.

De meeste Usenet-indexers vereisen een API-sleutel, die te vinden is op je profielpagina op de website van de indexer.

De meeste torrent-trackers vereisen [Prowlarr](/prowlarr) of Jackett om te worden gebruikt in Sonarr.

Voeg ten minste één indexer toe zodat Sonarr correct kan werken.

> Zie de [instellingenpagina](/sonarr/settings#indexers) en de [Meer informatie (Ondersteund)](/sonarr/supported#indexers) pagina voor dit gedeelte voor meer informatie.
{.is-info}

# Download Clients

`Instellingen` => `Download Clients`

Het downloaden en importeren is waar de meeste mensen problemen ervaren. Vanuit een hoog niveau gezien moet de software kunnen communiceren met je downloadclient en toegang hebben tot de bestanden die het downloadt. Er is een grote verscheidenheid aan ondersteunde downloadclients en nog veel meer verschillende configuraties. Dit betekent dat hoewel er enkele veelvoorkomende configuraties zijn, er geen juiste configuratie is en de configuratie van iedereen een beetje anders kan zijn. Maar er zijn veel verkeerde configuraties.

> Zie de [instellingenpagina](/sonarr/settings#download-clients), de [Meer informatie (Ondersteund)](/sonarr/supported#download-clients) pagina voor dit gedeelte, en [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) voor meer informatie.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Sonarr stuurt een downloadverzoek naar je client en koppelt het aan een label of categorienaam die je hebt geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Sonarr controleert de actieve downloads van je downloadclient die deze categorienaam gebruiken. Dit gebeurt via de API van je downloadclient.
- Wanneer de download is voltooid, weet Sonarr de uiteindelijke bestandslocatie zoals gerapporteerd door je downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang het maar ergens apart van je mediamap is en toegankelijk is voor Sonarr.
- Sonarr scant die voltooide bestandslocatie op bestanden die Sonarr kan gebruiken. Het analyseert de bestandsnaam om deze te vergelijken met de gevraagde media. Als dat lukt, hernoemt het het bestand volgens je specificaties en verplaatst het naar de opgegeven medialocatie.
- Atomic Moves (directe verplaatsingen) zijn standaard ingeschakeld. Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor je voltooide downloadmap en je mediatheek. Als de atomic move mislukt of je configuratie geen hardlinks en atomic moves ondersteunt, zal Sonarr teruggaan naar het kopiëren van het bestand en het vervolgens verwijderen van de bron, wat IO-intensief is.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Sonarr, worden overgebleven bestanden van de download naar je prullenbak of recycling gestuurd via een verzoek aan je client om de release te verwijderen.

### BitTorrent

{#bittorrent}

- Sonarr stuurt een downloadverzoek naar je client en koppelt het aan een label of categorienaam die je hebt geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Sonarr controleert de actieve downloads van je downloadclient die deze categorienaam gebruiken. Deze controle gebeurt via de API van je downloadclient.
- Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat je het bestand kunt seeden (de verhouding of tijd kan worden aangepast in de downloadclient of vanuit Sonarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar je mediamap, zal Sonarr het bestand hardlinken als dit wordt ondersteund door je configuratie, anders wordt het gekopieerd.
- Hardlinks zijn standaard ingeschakeld. [Een hardlink zal geen extra schijfruimte gebruiken.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor je voltooide downloadmap en je mediamap. Als het maken van een hardlink mislukt of je configuratie geen hardlinks ondersteunt, zal Sonarr teruggaan naar het kopiëren van het bestand.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Sonarr, zal Sonarr de torrent verwijderen uit je client en de client vragen om de torrentgegevens te verwijderen, maar alleen als de client meldt dat het seeden is voltooid en de torrent is gestopt (gepauzeerd na voltooiing).

# Hoe je je bestaande georganiseerde mediatheek importeert

> Let op: Sonarr zoekt niet regelmatig naar afleveringen. Zie de FAQ-entry voor details om te begrijpen hoe Sonarr werkt.
[Hoe vindt Sonarr afleveringen?](/sonarr/faq#how-does-sonarr-find-episodes)
{.is-info}

Nadat je je profielen/kwaliteitsgroottes hebt ingesteld en je indexers en downloadclient(s) hebt toegevoegd, is het tijd om je bestaande georganiseerde mediatheek te importeren.

Binnenkort beschikbaar - Bijdragen zijn welkom

## Bestaande media importeren

Afhankelijk van hoe goed je bestaande serie mappen zijn genoemd, zal Sonarr proberen deze te koppelen aan de juiste serie. Je moet deze lijst zorgvuldig controleren voordat je importeert.

Bibliotheekimport moet alleen worden gebruikt voor een bestaande georganiseerde bibliotheek en mag niet worden gebruikt voor een downloadmap of om media ad-hoc te importeren.

1. Ga naar Bibliotheekimport
1. Lees en begrijp de Help-tekst voor Bibliotheekimport
1. Selecteer of voeg de hoofdmap (bibliotheek) toe om series van te importeren
1. Controleer de koppeling/matching van de serie mappen van Sonarr met TVDb-series
1. Stel je bewakingsinstellingen en kwaliteitsprofiel in zoals gewenst
1. Klik op Start Importeren

### Geen overeenkomst gevonden

1. Zoek de serienaam of TVDbId in het selectievak van de serie
1. Raadpleeg [deze FAQ-entry](/sonarr/faq#why-can-i-not-add-a-series) als de serie niet kan worden gevonden

### Foutieve mapnaam na import herstellen

1. Verwijder de serie uit Sonarr
1. Bibliotheekimport
1. Zorg ervoor dat de serie correct is gekoppeld

# Nieuwe serie toevoegen

[Zie de Pagina Bibliotheek voor aanvullende informatie](/sonarr/library#add-new)

# Afleveringen importeren

- Gebruik Wanted => Handmatig importeren om afleveringsbestanden op ad-hoc basis naar hun serie mappen te importeren
- Gebruik Beheer afleveringen op de pagina van een serie om bestaande afleveringsbestanden in een serie map opnieuw te koppelen of te koppelen