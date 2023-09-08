---
title: Readarr Snelstartgids
description: 
published: true
date: 2022-09-07T23:19:05.590Z
tags: readarr
editor: markdown
dateCreated: 2021-12-11T19:42:31.825Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Snelstart installatiegids](#snelstart-installatiegids)
- [Opstarten](#opstarten)
- [Mediabeheer](#mediabeheer)
- [Boeknaamgeving](#boeknaamgeving)
- [Mappen](#mappen)
- [Importeren](#importeren)
- [Bestandsbeheer](#bestandsbeheer)
- [Hoofdmappen en Calibre-integratie](#hoofdmappen-en-calibre-integratie)
  - [Calibre Content Server (Optioneel)](#calibre-content-server-optioneel)
  - [Calibre-integratie](#calibre-integratie)
- [Downloadclients](#downloadclients)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Hoe u uw bestaande georganiseerde mediatheek importeert](#hoe-u-uw-bestaande-georganiseerde-mediatheek-importeert)
  - [Bestaande media importeren](#bestaande-media-importeren)
- [Nieuwe boeken toevoegen](#nieuwe-boeken-toevoegen)

# Snelstart installatiegids

> Deze pagina is nog in ontwikkeling en niet compleet. Bijdragen zijn welkom.

> Voor een gedetailleerdere uitleg van alle instellingen, zie [Readarr => Instellingen](/readarr/settings)
{.is-info}

In deze gids proberen we de basisinstellingen uit te leggen die u moet doen om aan de slag te gaan met Readarr. We zullen enkele opties overslaan die u op het scherm kunt zien. Als u hier dieper op in wilt gaan, raadpleeg dan de juiste pagina in de FAQ en documentatie voor een volledige uitleg.

> Houd er rekening mee dat geavanceerde opties binnen de schermafbeeldingen en GUI-instellingen in `oranje` zijn, dus u moet bovenaan de pagina op `Geavanceerd weergeven` klikken om ze zichtbaar te maken.
{.is-warning}

# Opstarten

Na installatie en het opstarten opent u een browser en gaat u naar `http://{uw_ip_hier}:8787`

![qs_startup.png](/assets/readarr/qs_startup.png)

# Mediabeheer

Als eerste gaan we kijken naar de instellingen voor `Mediabeheer`, waar we onze voorkeursinstellingen voor naamgeving en bestandsbeheer kunnen instellen.

`Instellingen` => `Mediabeheer`

![mediamanagement.png](/assets/readarr/mediamanagement.png)

# Boeknaamgeving

![booknaming.png](/assets/readarr/booknaming.png)

- In- of uitschakelen van het hernoemen van uw boeken (in plaats van de namen te laten zoals ze zijn of zoals ze waren toen u ze downloadde).
- Als u wilt dat ongeldige tekens worden vervangen of verwijderd (`\ / : * ? " < > | ~ - % & + { }`).
- Hier selecteert u de naamgevingsconventie voor de daadwerkelijke boekbestanden. Let op dat de mapnaam van het boek hier ook wordt gedefinieerd.
- `(Geavanceerde optie) Hier stelt u de naamgevingsconventie in voor de map van de auteur.`

> Dit is niet van toepassing als Calibre wordt gebruikt, omdat Calibre de bestands-/mapnaamgeving afhandelt met behulp van zijn eigen interne schema.
{.is-info}

# Mappen

![folders.png](/assets/readarr/folders.png)

- (Geavanceerde optie) Lege auteursmappen maken - Inschakelen om lege auteursmappen te maken wanneer er een nieuwe auteur aan Readarr wordt toegevoegd.
- (Geavanceerde optie) Lege mappen verwijderen - Inschakelen om lege auteursmappen te verwijderen wanneer er geen boeken meer zijn voor die auteur.

> Een van deze vakjes kan worden aangevinkt, maar ze mogen NIET allebei worden aangevinkt.
{.is-warning}

> Dit is niet van toepassing als Calibre wordt gebruikt, omdat Calibre de bestands-/mapnaamgeving afhandelt met behulp van zijn eigen interne schema.
{.is-info}

# Importeren

![importing.png](/assets/readarr/importing.png)

- (Geavanceerde optie) Overslaan van controle op vrije ruimte - Als dit is ingeschakeld, wordt de controle op vrije ruimte overgeslagen voordat er wordt geïmporteerd.
- (Geavanceerde optie) Minimale vrije ruimte - Voer de minimale vrije ruimte in die de schijf moet hebben voordat het importeren stopt.
- (Geavanceerde optie) Gebruik hardlinks in plaats van kopiëren - Vink dit vakje aan om hardlinks te gebruiken in plaats van kopiëren (voor torrents). Let op dat dit standaard is ingeschakeld.
  
> U moet dit bij voorkeur overal gebruiken waar mogelijk. Om hardlinks te kunnen gebruiken, moeten uw bron-/bestemmingslocatie zich op hetzelfde bestandssysteem (schijf, partitie) en koppelingspunten bevinden. [Zie de Hardlink-gids van TRaSH voor meer informatie](https://trash-guides.info/hardlinks/)
{.is-info}
  
- Extra bestanden importeren - Als dit is ingeschakeld, worden de opgegeven extra bestanden geïmporteerd die zich in de map van het boek bevinden wanneer het wordt geïmporteerd.
- (Geavanceerde optie) Extra bestanden importeren - Als Extra bestanden importeren is ingeschakeld, voert u een door komma's gescheiden lijst van extensies in om te importeren.

> Als u Readarr gebruikt voor luisterboeken, moet u .cue aan deze lijst toevoegen, omdat dit uw hoofdstukinformatie bevat!
{.is-info}

# Bestandsbeheer

![filemanagement.png](/assets/readarr/filemanagement.png)

- Boeken die van de schijf zijn verwijderd, worden automatisch niet meer gevolgd in Readarr.

- Verwijderde boeken negeren - Vink dit vakje aan om boeken die als verwijderd of ontoegankelijk zijn gedetecteerd in de hoofdmap van Readarr niet meer te volgen.
- Download Proper & Repacks - Of er al dan niet automatisch wordt geüpgraded naar Propers/Repacks. Gebruik `Niet voorkeur geven` om te sorteren op voorkeurswoordenscore boven propers/repacks
  - Voorkeur en upgraden - Rangschik repacks en propers hoger dan niet-repacks en niet-propers. Behandel nieuwe repacks en propers als een upgrade naar huidige releases.
  - Niet automatisch upgraden - Rangschik repacks en propers hoger dan niet-repacks en niet-propers. Behandel nieuwe repacks en propers niet als een upgrade naar huidige releases.
  - Geen voorkeur geven - Dit negeert effectief repacks en propers. U moet eventuele voorkeur hiervoor beheren met [Voorkeurswoorden](#release-profielen).

> \* `PROPER` - betekent dat er een probleem was met de vorige release. Downloads met de tag PROPER laten zien dat de problemen zijn opgelost in die release. Dit wordt gedaan door een groep die de oorspronkelijke release niet heeft uitgebracht.
> \* `REPACK` - betekent dat er een probleem was met de vorige release en dat dit is gecorrigeerd door de oorspronkelijke groep. Downloads met de tag REPACK laten zien dat de problemen zijn opgelost in die release. Dit wordt gedaan door een groep die de oorspronkelijke release wel heeft uitgebracht.
{.is-info}

- (Geavanceerde optie) Hoofdmappen controleren op bestandswijzigingen - Vink dit vakje aan om een nieuwe scan te starten wanneer wordt gedetecteerd dat de hoofdmap is gewijzigd.
- (Geavanceerde optie) Auteursmap opnieuw scannen na vernieuwen - Kies wanneer een auteursmap opnieuw moet worden gescand na het vernieuwen van de auteur.
  - Altijd - Dit scant auteursmappen op basis van de taakplanning
  - Na handmatige vernieuwing - U moet handmatig de schijf opnieuw scannen
  - Nooit - Zoals de naam al zegt, auteursmappen nooit opnieuw scannen.
- (Geavanceerde optie) Vingerafdrukken toestaan - Kies hoe vingerafdrukken moeten worden behandeld, wat zorgt voor een nauwkeurigere boekovereenkomst, maar ten koste van CPU-/schijftijd.
  - Altijd - Altijd vingerafdrukken gebruiken indien mogelijk
  - Alleen voor nieuwe imports - Alleen vingerafdrukken gebruiken voor nieuw geïmporteerde releases
  - Nooit - Zoals de naam al zegt, nooit vingerafdrukken gebruiken
- (Geavanceerde optie) Bestandsdatum wijzigen - Bestandsdatum wijzigen bij importeren/opnieuw scannen
  - Geen - Readarr wijzigt de datum niet die wordt weergegeven in uw bestandsbrowser
  - Boekpublicatiedatum - De datum waarop het boek is uitgebracht.
- (Geavanceerde optie) Prullenbak - Boekbestanden worden hierheen verplaatst wanneer ze worden verwijderd in plaats van permanent te worden verwijderd
- (Geavanceerde optie) Prullenbak opruimen - Dit is hoe oud een bepaald bestand kan zijn voordat het permanent wordt verwijderd

> Het wordt sterk aanbevolen om een prullenbak te gebruiken. Het is gemakkelijk om bestanden te verwijderen en ze te herstellen is eenvoudig als u de prullenbak gebruikt.
{.is-warning}

# Hoofdmappen en Calibre-integratie

![rootfolders1.png](/assets/readarr/rootfolders1.png)

Hier voegen we de hoofdmap toe die Readarr zal gebruiken om uw bestaande georganiseerde mediatheek te importeren en waar Readarr uw media zal importeren (kopiëren/hardlink/verplaatsen) nadat uw downloadclient het heeft gedownload.

> **De gebruiker en groep die u heeft geconfigureerd om Readarr uit te voeren, moeten lees- en schrijftoegang hebben tot deze locatie.** {.is-info}

U kunt er ook voor kiezen om Calibre te gebruiken om uw bibliotheek op dit scherm te beheren. Hiervoor moet u de Calibre Content Server uitvoeren. Dit is NIET Calibre-Web.

> Gebruikers van niet-Windows-besturingssystemen:
> \* Als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
> \* Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.
{.is-warning}

> Als u Calibre gaat gebruiken, moeten de boeken die u wilt laten herkennen door Readarr bij de initiële bibliotheekimport **al in Calibre staan**. Boeken in de map die niet in Calibre staan, worden genegeerd. Hardlinks worden niet gebruikt bij het toevoegen van Calibre-integratie.
> **Let op dat u geen Calibre-integratie kunt toevoegen aan een hoofdmap nadat deze is aangemaakt.**
{.is-danger}

> Uw downloadclient downloadt naar een downloadmap en Readarr importeert het naar uw mediamap (eindbestemming) die uw mediaserver gebruikt. Uw downloadmap en mediamap kunnen niet dezelfde locatie zijn!
{.is-warning}

Vergeet niet om uw wijzigingen op te slaan.

## Calibre Content Server (Optioneel)

Als u Calibre wilt gebruiken om uw boeken te beheren, moet u de Calibre Content Server instellen. Dit is opnieuw geen Calibre-Web, maar een onderdeel van Calibre zelf. U moet Calibre uitvoeren en de Content Server instellen.

> Als u ervoor kiest om Calibre te gebruiken, kunt u niets wijzigen in de database van Calibre. Als u deze waarschuwing negeert, moet u uw Readarr-database verwijderen en opnieuw beginnen
{.is-danger}

Als u Docker gebruikt, moeten uw Calibre gemonteerde boekdirectory en uw Readarr gemonteerde boekdirectory hetzelfde zijn.

> Houd er rekening mee dat terwijl Readarr in bèta is; als u Calibre gebruikt, wordt het aanbevolen om Hernoemen in Readarr uit te schakelen voor het geval er een onbedoelde bug doorheen glipt.
{.is-info}

Om dit te doen, opent u Calibre en klikt u op `Voorkeuren / Delen via het netwerk`

![calibreprefs.png](/assets/readarr/calibreprefs.png)

Voeg eerst een gebruikersaccount toe. Het account moet toegang hebben om wijzigingen aan te brengen.

![calibreacct.png](/assets/readarr/calibreacct.png)

Vervolgens moet u Calibre opnieuw opstarten. Zodra u weer in het programma bent, configureert u de contentserver en start u deze op. Het zou moeten aangeven dat het actief is. Stel in dat het automatisch wordt gestart bij het opstarten. Nadat u hebt opgeslagen, moet u Calibre opnieuw opstarten. Zorg ervoor dat de server wordt gestart wanneer deze weer wordt opgestart, en ga dan naar het volgende gedeelte.

> U moet "Require username and password to access the content server" selecteren om ervoor te zorgen dat Readarr correct werkt. Als u dit niet doet, krijgt u een foutmelding met de melding "Anonymous users are not allowed to make changes" wanneer Readarr een boek importeert!
{.is-info}

![calibreserver.png](/assets/readarr/calibreserver.png)

## Calibre-integratie

![calibre1.png](/assets/readarr/calibre1.png)

De onderstaande instellingen zijn specifiek voor Calibre en worden alleen weergegeven als `Gebruik Calibre` is ingeschakeld

- Gebruik Calibre - In-/uitschakelen van het gebruik van de Calibre Content Server om uw hoofdmap te beheren.

> \* Let op dat dit **niet kan worden ingeschakeld voor een bestaande hoofdmap**.
> \* Let op dat dit **niet kan worden uitgeschakeld voor een bestaande Calibre-ingeschakelde hoofdmap**.
> \* Let op dat hiervoor de **Calibre Content Server** vereist is en niet werkt met Calibre Web of Calibre.
> \* Let op dat hardlinks niet werken met Calibre-integratie.
> \* Let op dat hiervoor moet worden ingesteld dat Calibre `Require username and password to access the content server` vereist.
> \* Als u `Require username and password to access the content server` niet inschakelt in Calibre, krijgt u een foutmelding met de melding `Anonymous users are not allowed to make changes`
{.is-warning}

> Als u Calibre gaat gebruiken, kunt u niets wijzigen in de database van Calibre. Als u deze waarschuwing negeert, moet u uw Readarr-database verwijderen en opnieuw beginnen
{.is-danger}

- Calibre-host - Het IP/domein van de host van de Calibre Content Server
- Calibre-poort - De poort waarop de Calibre Content Server luistert
- (Geavanceerd) Calibre-URL-basis - Voeg een voorvoegsel toe aan de Calibre-URL, bijv. `http://[host]:[port]/[urlBase]`
- Calibre-gebruikersnaam - Gebruikersnaam om toegang te krijgen tot de Calibre Content Server
- Calibre-wachtwoord - Wachtwoord om toegang te krijgen tot de Calibre Content Server
- Calibre-bibliotheek - Naam van de Calibre Content Server-bibliotheek. Laat leeg voor standaardwaarde
- Converteren naar indeling - (Optioneel) Vraag de Calibre Content Server om te converteren naar andere indelingen met een door komma's gescheiden lijst.
  - Bekijk het (i)-pictogram in de app voor een actuele lijst met opties.
  - Opties zijn: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-uitvoerprofiel - Selecteer het uitvoerprofiel van de Calibre Content Server dat moet worden gebruikt
  - Het uitvoerprofiel vertelt het conversiesysteem van de Calibre Content Server hoe het document moet worden geoptimaliseerd voor het gespecificeerde apparaat (bijvoorbeeld door afbeeldingen aan te passen aan de schermgrootte van het apparaat). In sommige gevallen kan een uitvoerprofiel worden gebruikt om de uitvoer te optimaliseren voor een bepaald apparaat, maar dit is zelden nodig.
- Gebruik SSL - In-/uitschakelen van het gebruik van SSL (HTTPS) voor de Calibre Content Server

> Als u een individueel boek toevoegt en `Geen`\* selecteert voor het [metadataprofiel](/readarr/settings#metadata-profiles), wordt alleen dat boek weergegeven onder de auteur wanneer het wordt toegevoegd. Als u andere boeken voor die auteur wilt toevoegen, kiest u een geschikt metadataprofiel.
> \* **Let op dat `Geen` geen metadatavilters toepast en dat u ongewenste buitenlandse edities kunt krijgen. Om dit op te lossen [maakt u een metadataprofiel aan zoals voorgeschreven in de FAQ](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Downloadclients

`Instellingen` => `Downloadclients`

Downloaden en importeren is waar de meeste mensen problemen ondervinden. Vanuit een hoog niveau gezien moet de software kunnen communiceren met uw downloadclient en toegang hebben tot de bestanden die deze downloadt. Er is een grote verscheidenheid aan ondersteunde downloadclients en nog veel meer verschillende configuraties. Dit betekent dat hoewel er enkele veelvoorkomende configuraties zijn, er geen juiste configuratie is en de configuratie van iedereen een beetje anders kan zijn. Maar er zijn veel verkeerde configuraties.

> Zie de [instellingenpagina](/readarr/settings#download-clients), de [Meer informatie (Ondersteund)](/readarr/supported#download-clients) pagina voor dit gedeelte, en [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) voor meer informatie.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Readarr stuurt een downloadverzoek naar uw client en koppelt dit aan een label of categorie die u heeft geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Readarr controleert de actieve downloads van uw downloadclient die deze categorie gebruiken. Dit wordt gecontroleerd via de API van uw downloadclient.
- Wanneer de download is voltooid, weet Readarr de definitieve bestandslocatie zoals gerapporteerd door uw downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang het maar ergens apart van uw mediamap is en toegankelijk is voor Readarr.
- Readarr scant die voltooide bestandslocatie op bestanden die Readarr kan gebruiken. Het analyseert de bestandsnaam om deze te matchen met de gevraagde media. Als dat lukt, wordt het bestand hernoemd volgens uw specificaties en verplaatst naar de opgegeven medialocatie.
- Atomic Moves (directe verplaatsingen) zijn standaard ingeschakeld. Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediatheek. Als de atomic move mislukt of uw configuratie geen hardlinks en atomic moves ondersteunt, zal Readarr terugvallen op het kopiëren van het bestand en vervolgens verwijderen van de bron, wat IO-intensief is.
- Als de optie "Afgehandelde gedownloade bestanden verwijderen" is ingeschakeld in de instellingen van Readarr, worden overgebleven bestanden van de download naar uw prullenbak of verwijdering gestuurd via een verzoek aan uw client om de release te verwijderen.

### BitTorrent

{#bittorrent}

- Readarr stuurt een downloadverzoek naar uw client en koppelt het aan een label of categorie die u hebt geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Readarr controleert de actieve downloads van uw downloadclient die gebruik maken van die categorie. Deze controle gebeurt via de API van uw downloadclient.
- Voltooide bestanden worden op hun oorspronkelijke locatie achtergelaten zodat u het bestand kunt seeden (de verhouding of tijd kan worden aangepast in de downloadclient of vanuit Readarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar uw mediabibliotheek, zal Readarr het bestand hardlinken als dit wordt ondersteund door uw systeem, anders wordt het gekopieerd als hardlinks niet worden ondersteund.
- Hardlinks zijn standaard ingeschakeld. [Een hardlink zal geen extra schijfruimte gebruiken.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediatheek. Als het maken van een hardlink mislukt of uw systeem geen hardlinks ondersteunt, zal Readarr terugvallen en het bestand kopiëren.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Readarr, zal Readarr de torrent verwijderen uit uw client en de client vragen om de torrentgegevens te verwijderen, maar alleen als de client aangeeft dat het seeden is voltooid en de torrent is gestopt (gepauzeerd na voltooiing).

# Hoe importeer je je bestaande georganiseerde mediatheek

> Let op: Readarr zoekt niet regelmatig naar boeken. Zie deze twee FAQ-items voor details om te begrijpen hoe Readarr werkt.
[Hoe vindt Readarr boeken?](/readarr/faq#hoe-vindt-readarr-boeken) en [Hoe werkt Readarr?](/readarr/faq#hoe-werkt-readarr)
{.is-info}

Nadat u uw profielen/kwaliteitsgroottes hebt ingesteld en uw indexers en downloadclients hebt toegevoegd, is het tijd om uw bestaande georganiseerde mediatheek te importeren.

Binnenkort beschikbaar - Bijdragen zijn welkom

## Importeren van bestaande media

Binnenkort beschikbaar - Bijdragen zijn welkom

# Nieuwe boeken toevoegen

[Zie de bibliotheekpagina voor aanvullende informatie](/readarr/library#nieuwe-toevoegen)