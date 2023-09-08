# Instellingen van Readarr

Deze pagina zal alle beschikbare instellingen in Readarr doorlopen en uitleggen hoe ze werken. Dit is geen uitgebreide handleiding voor het instellen van Readarr. Als je dat wilt, gebruik dan in plaats daarvan de [Snelstartgids](/readarr/quick-start-guide) pagina.

# Menu-opties

Om naar de instellingenpagina te gaan, kies je Instellingen in het linker menu. De volgende submenu-opties zijn beschikbaar:

![settings_1_menu.png](/assets/readarr/settings_1_menu.png)

Let ook op dat voor elke individuele instellingenpagina er enkele opties bovenaan het menu staan:

![settings_2_topmenu.png](/assets/readarr/settings_2_topmenu.png)

- Verbergen/tonen van geavanceerde opties is belangrijk voor items die hieronder zijn gemarkeerd als `(Geavanceerde optie)`, anders worden ze niet weergegeven. Deze menu-items worden weergegeven in het oranje op de schermafbeeldingen.

- Je moet je wijzigingen opslaan voordat je het scherm verlaat. Dit doe je door op het schijf-icoon te klikken. Als je geen wijzigingen hebt aangebracht, wordt "Geen wijzigingen" weergegeven en is het grijs, zoals hierboven getoond.

# Mediabeheer

> Sommige van deze instellingen zijn alleen zichtbaar via `Toon geavanceerde instellingen`, dat zich bevindt in de bovenste balk onder de zoekbalk{.is-info}

## Hoofdmappen

- Een lijst van je geconfigureerde hoofdmappen (bibliotheekmappen) wordt weergegeven.
- Klik op de <kb>+</kb> knop om een nieuwe hoofdmap toe te voegen of klik op de kaart van een bestaande map om deze te bewerken.

### Instellingen van de hoofdmap

- Naam - De naam van de hoofdmap voor UI-doeleinden
- Pad - De map die je boekenbibliotheek bevat, oftewel de uiteindelijke bestemming zoals Readarr het ziet.
  - Let op dat dit anders moet zijn dan de locatie waar je downloadclient bestanden plaatst.
  - Als je Docker en Calibre-integratie gebruikt, moeten de koppelingen hetzelfde zijn als je boekenmap.

{#calibre}

- Specifieke Calibre-instellingen (Alleen als Calibre gebruikt wordt)
  - Calibre gebruiken - In- of uitschakelen van het gebruik van de Calibre Content Server om je hoofdmap te beheren.

> \* Let op dat dit **niet ingeschakeld kan worden voor een bestaande hoofdmap**.
> \* Let op dat dit **niet uitgeschakeld kan worden voor een bestaande Calibre-ingeschakelde hoofdmap**.
> \* Let op dat hiervoor de **Calibre Content Server** vereist is en dit niet werkt met Calibre Web of Calibre.
> \* Let op dat hardlinks niet werken met Calibre-integratie.
> \* Let op dat hiervoor vereist is dat Calibre `Require username and password to access the content server` ingeschakeld heeft.
> \* Als `Require username and password to access the content server` niet ingeschakeld is in Calibre, krijg je een foutmelding `Anonymous users are not allowed to make changes`.
{.is-warning}

- Calibre-host - Het IP/domein van de host van de Calibre Content Server
- Calibre-poort - De poort waarop de Calibre Content Server luistert
- (Geavanceerd) Calibre URL-basis - Voeg een voorvoegsel toe aan de Calibre-URL, bijv. `http://[host]:[port]/[urlBase]`
- Calibre-gebruikersnaam - Gebruikersnaam om toegang te krijgen tot de Calibre Content Server
- Calibre-wachtwoord - Wachtwoord om toegang te krijgen tot de Calibre Content Server
- Calibre-bibliotheek - Naam van de Calibre Content Server-bibliotheek. Laat leeg voor standaardwaarde
- Converteren naar formaat - (Optioneel) Vraag de Calibre Content Server om te converteren naar andere formaten met een door komma's gescheiden lijst.
  - Bekijk het (i)-pictogram in de app voor een actuele lijst met opties.
  - Opties zijn: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-uitvoerprofiel - Selecteer het uitvoerprofiel van de Calibre Content Server dat gebruikt moet worden
  - Het uitvoerprofiel vertelt het conversiesysteem van de Calibre Content Server hoe het document geoptimaliseerd moet worden voor het gespecificeerde apparaat (bijvoorbeeld door afbeeldingen aan te passen aan de schermgrootte van het apparaat). In sommige gevallen kan een uitvoerprofiel worden gebruikt om de uitvoer te optimaliseren voor een bepaald apparaat, maar dit is zelden nodig.
- SSL gebruiken - SSL (HTTPS) gebruiken voor de Calibre Content Server in- of uitschakelen
- Monitor - Configureer je opties voor het monitoren van boeken die in deze map gedetecteerd worden
  - Alle boeken - Alle boeken monitoren
  - Toekomstige boeken - Boeken monitoren die nog niet zijn uitgebracht
  - Ontbrekende boeken - Boeken monitoren die geen bestanden hebben of nog niet zijn uitgebracht
  - Bestaande boeken - Boeken monitoren die bestanden hebben of nog niet zijn uitgebracht
  - Eerste boek - Het eerste boek monitoren. Alle andere boeken worden genegeerd
  - Laatste boek - Het laatste boek en toekomstige boeken monitoren
  - Geen - Geen boeken worden gemonitord tenzij expliciet toegevoegd
- Kwaliteitsprofiel - Standaard kwaliteitsprofiel voor boeken en auteurs die in deze map gedetecteerd worden
- Metagegevensprofiel - Selecteer het metagegevensprofiel dat gebruikt moet worden voor auteurs die in deze map gedetecteerd worden. Selecteer Geen om alleen boeken te laden die expliciet zijn toegevoegd of gedetecteerd.
- Standaard Readarr-tags - Standaardtags voor auteurs die in deze map gedetecteerd worden

> Gebruikers van niet-Windows-systemen:
> \* Als je een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
> \* Als je een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.
{.is-warning}

## Externe padtoewijzingen

- Externe padtoewijzing werkt als een eenvoudige zoekopdracht naar een extern pad en vervangt dit door een lokaal pad. Dit wordt voornamelijk gebruikt voor samengevoegde lokale/externe configuraties met behulp van mergerfs of iets soortgelijks, of wanneer de applicatie en de downloadclient of Calibre zich niet op dezelfde server bevinden.
- Zie het gedeelte in [Downloadclients => Externe padtoewijzing](#remote-path-mappings-1) vervang `<Downloadclient>` door `<Calibre>` voor meer informatie.

## Bestandsnaamgeving van boeken

![bookfilenaming.png](/assets/readarr/bookfilenaming.png)

**Als je Calibre-integratie gebruikt, kun je de bestandsnaam van boeken niet zelf instellen. Calibre regelt dit voor je. Je moet deze instellingen alleen wijzigen als je geen Calibre gebruikt.**

> Let op dat zolang Readarr in bèta is; als je Calibre gebruikt, wordt het aanbevolen om het hernoemen in Readarr uit te schakelen voor het geval er per ongeluk een bug doorheen glipt. {.is-info}

Veelgebruikte naamgevingsschema's zijn:

- Standaard boekformaat
  - `{Boektitel}\{Auteursnaam}` - `{Boektitel}` wat resulteert in een map met de naam `Cujo` en een submap met een bestand met de naam `Stephen King - Cujo.m4b`

- Auteursmapformaat
  - `{Auteursnaam}` wat resulteert in: `Stephen King`

## Naamgeving van boeken

- Boeken hernoemen - Als dit uitgeschakeld is (geen vinkje in het vakje), zal Readarr de bestaande bestandsnaam gebruiken als hernoemen is uitgeschakeld.
  - Als het niet aangevinkt is:
    - Importeren via downloadclient
      - De titel van de release van de downloadclient wordt gebruikt
    - Handmatige (ad-hoc) import: Originele bestandsnaam

> Als je "Boeken hernoemen" niet aanvinkt, is geen van de onderstaande naamgeving van toepassing - je hebt Readarr verteld dat je helemaal geen hernoeming wilt. Het boek wordt rechtstreeks in de auteursmap geïmporteerd.
{.is-info}

> Dit is niet van toepassing als Calibre wordt gebruikt, omdat Calibre de bestands-/mapnaamgeving afhandelt met behulp van zijn eigen interne schema.
{.is-info}

- Onwettige tekens vervangen - Als dit is uitgeschakeld, zal Readarr onwettige tekens verwijderen. Als dit is ingeschakeld, zal Readarr onwettige tekens vervangen. Voorbeelden zijn `\ # / $ * < >` en meer.

### Standaard boekformaat

- Selecteer de naamgeving

- Dropdown Box (rechtsboven)
  - Linker vak - Behandeling van spaties
    - `Spatie ( )` - Spaties gebruiken in de naamgeving (Standaard)
    - `Punt (.)` - Punten gebruiken in plaats van spaties in de naamgeving
    - `Onderstrepingsteken (_)` - Onderstrepingstekens gebruiken in plaats van spaties in de naamgeving
    - `Koppelteken (-)` - Koppeltekens gebruiken in plaats van spaties in de naamgeving
  - Rechter vak - Behandeling van hoofdletters
    - `Standaardhoofdletters` - Titel in hoofdletters en kleine letters maken (~camel-case) (Standaard)
    - `HOOFDLETTERS` - Titel volledig in hoofdletters maken
    - `kleine letters` - Titel volledig in kleine letters maken

### Auteur

- `{Auteursnaam}` = Naam van de auteur
- `{AuteursnaamThe}` = Naam van de auteur, De
- `{AuteursSchoneNaam}` = Schone naam van de auteur
- `{AuteursSorteernaam}` = Naam, Auteur
- `{AuteursDisambiguatie}` = Auteursnaam (disambiguatie gebruikt van GoodReads voor meerdere auteurs met dezelfde naam)

### Boek

- `{Boektitel}` = De titel van het boek!: Ondertitel!
- `{BoektitelThe}` = Titel van het boek!, De: Ondertitel!
- `{BoekSchoneTitel}` = De titel van het boek: Ondertitel
- `{BoektitelGeenSub}` = De titel van het boek!
- `{BoektitelTheGeenSub}` = Titel van het boek!, De
- `{BoekSchoneTitelGeenSub}` = De titel van het boek
- `{BoekOndertitel}` = Ondertitel!
- `{BoekOndertitelThe}` Ondertitel!, De
- `{BoekSchoneOndertitel}` = Ondertitel
- `{BoekDisambiguatie}` = Boeknaam! (disambiguatietitel gebruikt van GoodReads)
- `{BoekSerie}` = Serietitel
- `{BoekSeriePositie}` = 1
- `{BoekSerieTitel}` = Serietitel #1
- `{Deelnummer:0}` of `{Deelnummer:0}` = 2
- `{Deelnummer:00}` = 02
- `{DeelAantal}` of `{DeelAantal:0} = 9
- `{DeelAantal:00}` = 09

### Releasedatum

- `{Jaar van uitgave}` = 2016
- `{Eerste jaar van uitgave}` = 2015
- `{Jaar van uitgave van de editie}` = 2016

### Kwaliteit

- `{Volledige kwaliteit}` = AZW3 Proper
- `{Titelkwaliteit}` = AZW3

### Mediainformatie

- `{MediaInfo Audiocodec}` = MP3
- `{MediaInfo Audiokanalen}` = 2.0
- `{MediaInfo Audiobitrate}` = 320kbps
- `{MediaInfo Audiobits per sample}` = 24bit
- `{MediaInfo Audiosamplerate}` = 44.1kHz

### Overige

- `{Releasewerkgroep}` = Rls Grp
- `{Voorkeurswoorden}` = iNTERNAL

### Origineel

- `{Originele titel}` = Auteur.Naam.Boek.Naam.2018.AZW3-EVOLVE
- `{Originele bestandsnaam}` = 01-boeknaam

> Originele bestandsnaam wordt niet aanbevolen. Het is de letterlijke originele bestandsnaam en kan geobfusceerd zijn t1i0p3s7i8yuti. Gebruik in plaats daarvan de originele titel. {.is-info}

## Indeling van auteursmappen

- (Geavanceerde optie) Hier stel je de naamgevingsconventie in voor de naam van de auteursmap.

> Dit is niet van toepassing als Calibre wordt gebruikt, omdat Calibre de bestands-/mapnaamgeving afhandelt met behulp van zijn eigen interne schema.
{.is-info}

### Auteur

- `{Auteursnaam}` = Naam van de auteur
- `{AuteursnaamThe}` = Naam van de auteur, De
- `{AuteursSchoneNaam}` = Schone naam van de auteur
- `{AuteursSorteernaam}` = Naam, Auteur
- `{AuteursDisambiguatie}` = Auteursnaam (disambiguatie gebruikt van GoodReads voor meerdere auteurs met dezelfde naam)

## Mappen

![mm_folders.png](/assets/readarr/mm_folders.png)

- (Geavanceerde optie) Lege auteursmappen maken - Vink het vakje aan om lege auteursmappen te maken wanneer er een nieuwe auteur wordt toegevoegd.
- (Geavanceerde optie) Lege auteursmappen verwijderen - Vink het vakje aan om lege auteursmappen te verwijderen als er geen boeken in staan.

> Eén van die vakjes kan aangevinkt worden, maar ze mogen NIET allebei aangevinkt worden. {.is-warning}

> Dit is niet van toepassing als Calibre wordt gebruikt, omdat Calibre de bestands-/mapnaamgeving afhandelt met behulp van zijn eigen interne schema.
{.is-info}

## Importeren
  
![mm_importing.png](/assets/readarr/mm_importing.png)
  
- (Geavanceerde optie) Overslaan van vrije ruimtecontrole - Als dit is ingeschakeld, wordt de vrije ruimte niet gecontroleerd voordat er wordt geïmporteerd.
- (Geavanceerde optie) Minimale vrije ruimte - Voer de minimale vrije ruimte in die de schijf moet hebben voordat het importeren stopt.
- (Geavanceerde optie) Gebruik hardlinks in plaats van kopiëren - Vink dit vakje aan om hardlinks in plaats van kopieën te gebruiken (voor torrents). Houd er rekening mee dat dit standaard is ingeschakeld.
  
> Je zou dit idealiter overal moeten gebruiken waar mogelijk. Om hardlinks te kunnen gebruiken, moeten de bron/bestemming zich op hetzelfde bestandssysteem (schijf, partitie) en koppelpunten bevinden. [Zie de Hardlink-gids van TRaSH voor meer informatie](https://trash-guides.info/hardlinks/)
  
- Extra bestanden importeren - Als dit is ingeschakeld, worden de opgegeven extra bestanden geïmporteerd die zich in de map van het boek bevinden wanneer het wordt geïmporteerd.
- (Geavanceerde optie) Extra bestanden importeren - Als Extra bestanden importeren is ingeschakeld, voer dan een lijst met extensies gescheiden door komma's in om te importeren.

> Als je Readarr gebruikt voor luisterboeken, moet je .cue aan deze lijst toevoegen, omdat dit je hoofdstukinformatie bevat!
{.is-info}
  
## Bestandsbeheer
  
  ![mm_filemgmt.png](/assets/readarr/mm_filemgmt.png)

- Genegeerde verwijderde boeken - Vink dit vakje aan om boeken die als verwijderd of ontoegankelijk zijn gedetecteerd in de hoofdmap van Readarr niet te monitoren.
- Downloaden van juiste versies en repacks - Of automatisch upgraden naar juiste versies/repacks. Gebruik `Niet voorkeur geven` om te sorteren op voorkeurswoordenscore boven juiste versies/repacks
  - Voorkeur en upgraden - Rangschik repacks en juiste versies hoger dan niet-repacks en niet-juiste versies. Behandel nieuwe repacks en juiste versies als een upgrade naar huidige releases.
  - Niet automatisch upgraden - Rangschik repacks en juiste versies hoger dan niet-repacks en niet-juiste versies. Behandel nieuwe repacks en juiste versies niet als een upgrade naar huidige releases.
  - Geen voorkeur - Dit negeert effectief repacks en juiste versies. Je moet zelf de voorkeur beheren voor die met [Voorkeurswoorden](#release-profielen).
  
> \* `JUIST` - betekent dat er een probleem was met de vorige release. Downloads met de tag JUIST geven aan dat de problemen in die release zijn opgelost. Dit wordt gedaan door een groep die de oorspronkelijke release niet heeft uitgebracht.
> \* `REPACK` - betekent dat er een probleem was met de vorige release en dat dit is gecorrigeerd door de oorspronkelijke groep. Downloads met de tag REPACK geven aan dat de problemen in die release zijn opgelost. Dit wordt gedaan door een groep die de oorspronkelijke release wel heeft uitgebracht.
{.is-info}

- (Geavanceerde optie) Rootmappen controleren op bestandswijzigingen - Vink dit vakje aan om een heranalyse te starten wanneer wordt gedetecteerd dat de rootmap is gewijzigd.
- (Geavanceerde optie) Auteursmap opnieuw scannen na vernieuwen - Kies wanneer een auteursmap opnieuw moet worden gescand na het vernieuwen van de auteur.
  - Altijd - Dit zal auteursmappen opnieuw scannen op basis van de taakplanning
  - Na handmatige vernieuwing - Je moet de schijf handmatig opnieuw scannen
  - Nooit - Zoals het zegt, de auteursmappen nooit opnieuw scannen.
- (Geavanceerde optie) Vingerafdrukken toestaan - Kies hoe vingerafdrukken moeten worden afgehandeld, wat zorgt voor een nauwkeurigere boekovereenkomst, maar ten koste van CPU/schijftijd.
  - Altijd - Vingerafdrukken altijd gebruiken indien mogelijk
  - Alleen voor nieuwe imports - Alleen vingerafdrukken gebruiken voor nieuw geïmporteerde releases
  - Nooit - Zoals het zegt, nooit vingerafdrukken gebruiken
- (Geavanceerde optie) Bestandsdatum wijzigen - Bestandsdatum wijzigen bij importeren/heranalyseren
  - Geen - Readarr wijzigt de datum niet die wordt weergegeven in je bestandsbrowser
  - Boekpublicatiedatum - De datum waarop het boek is uitgebracht.
- (Geavanceerde optie) Prullenbak - Boekbestanden worden hierheen verplaatst wanneer ze worden verwijderd in plaats van permanent te worden verwijderd
- (Geavanceerde optie) Prullenbak opruimen - Dit is hoe oud een bepaald bestand kan zijn voordat het permanent wordt verwijderd

> Het wordt sterk aanbevolen om een prullenbak te gebruiken. Het is gemakkelijk om bestanden te verwijderen en ze kunnen gemakkelijk worden hersteld als je de prullenbak gebruikt.
{.is-warning}

# Machtigingen

- Machtigingen instellen - Moet `chmod` worden uitgevoerd wanneer bestanden worden geïmporteerd/hernoemd?
  - chmod-map - Octaal, toegepast tijdens importeren/hernoemen op mediamappen en -bestanden (zonder uitvoerbare bits)

> Het keuzemenu bevat een vooraf ingestelde lijst met veelgebruikte machtigingen die kunnen worden gebruikt. Je kunt echter handmatig een mapoctaal invoeren als je dat wilt.
{.is-info}

> Dit werkt alleen als de gebruiker die `Readarr` uitvoert de eigenaar van het bestand is. Het is beter om ervoor te zorgen dat de downloadclient de machtigingen correct instelt.
{.is-warning}

- chown-groep - Groepsnaam of GID. Gebruik GID voor externe bestandssystemen

> Dit werkt alleen als de gebruiker die `Readarr` uitvoert de eigenaar van het bestand is. Het is beter om ervoor te zorgen dat de downloadclient de machtigingen correct instelt.
{.is-warning}

# Profielen

## Kwaliteitsprofielen

Kwaliteitsprofielen worden gebruikt om te bepalen welke formaten van boeken acceptabel zijn voor een boek in je bibliotheek.
  
![qualityprofile.png](/assets/readarr/qualityprofile.png)

- Stel profielen in voor de kwaliteit van boeken die je wilt downloaden.

> Bij het selecteren van een bestaand profiel of het toevoegen van een extra profiel verschijnt er een nieuw venster
> Opmerking: de kwaliteit met een blauw vakje is de kwaliteit waarnaar alle media met dit profiel blijven upgraden.
{.is-info}

- Plus-pictogram (<kb>+</kb>) - Maak een nieuw kwaliteitsprofiel

- Naam - Voer een **UNIEKE** naam in voor het kwaliteitsprofiel dat je maakt
- Upgrades toegestaan - Wanneer deze optie is aangevinkt en je Readarr vertelt om een `EPUB` te downloaden omdat dit de eerste release van een specifiek boek is en later iemand een `AZW3` kan uploaden, zal Readarr automatisch upgraden naar de betere kwaliteit ***als*** `Upgrade tot` die kwaliteit heeft geselecteerd
  - Upgrade tot - Zodra deze kwaliteit is bereikt, zal Readarr geen boeken meer downloaden

> Opmerking: dit is alleen van toepassing als je `AZW3` hoger hebt dan `EPUB` binnen de sectie `Kwaliteiten`
{.is-warning}

- Kwaliteiten - Kwaliteiten hoger in de lijst hebben meer voorkeur, ongeacht de status van gewenst (ingeschakeld/aangevinkt). voor rangschikking ongeacht de ingeschakelde status. Kwaliteiten binnen dezelfde groep zijn gelijk. Alleen ingeschakelde (ingeschakelde) kwaliteiten zijn gewenst (toegestaan)
  - Groepen bewerken - Sommige kwaliteiten zijn gegroepeerd om de grootte van de lijst te verkleinen en vergelijkbare releases te groeperen. Een goed voorbeeld hiervan is `WebDL` en `WebRip`, omdat deze zeer vergelijkbaar zijn en meestal vergelijkbare bitrates hebben. Bij het bewerken van de groepen kun je de voorkeur binnen elke groep wijzigen.

  - [Zie Kwaliteiten](#kwaliteiten-gedefinieerd)

> Standaard zijn de kwaliteiten ingesteld van "slechtste" (onderaan) tot "beste" (bovenaan)
{.is-info}

## Metagegevensprofielen

Metagegevensprofielen worden gebruikt om te bepalen welke boeken van GoodReads moeten worden toegevoegd onder een auteur wanneer een nieuwe auteur wordt toegevoegd.

- Plus-pictogram (<kb>+</kb>) - Maak een nieuw metagegevensprofiel

![metaprofiles.png](/assets/readarr/metaprofiles.png)
  
- Naam - Voer een **UNIEKE** naam in voor het metagegevensprofiel
- Minimale populariteit - Voer de minimale populariteit in die een boek moet hebben om te worden toegevoegd voor een auteur.

> Als je dit te hoog instelt, worden boeken niet toegevoegd aan Readarr, maar als je dit te laag instelt, worden obscure publicaties weergegeven.
{.is-warning}

> Stel dit precies in op `10000000000` om een profiel te maken dat gelijk is aan `Geen`, maar toch andere filtering van edities en boeken toestaat. Merk op dat `Geen` geen metagegevensfilters toepast en je mogelijk buitenlandse edities krijgt.
{.is-info}

- Minimale pagina's - Voer het minimale aantal pagina's in dat een boek moet hebben om te worden toegevoegd voor een auteur.
- Boeken overslaan zonder publicatiedatum - Inschakelen om boeken over te slaan zonder een publicatiedatum.
- Boeken overslaan zonder ISBN of ASIN - Inschakelen om boeken over te slaan die geen ISBN of ASIN-nummer bevatten.
- Deelboeken en sets overslaan - Inschakelen om deelboeken en sets over te slaan.
- Secundaire serieboeken overslaan - Inschakelen om secundaire serieboeken over te slaan.
- Toegestane talen - Voer een lijst met ISO 639-3 taalcodes gescheiden door komma's in, of 'null' voor toegestane talen voor je boeken
- Mag niet bevatten - Voer woorden of zinnen in die een boektitel niet mag bevatten om te worden toegevoegd.
  
> Je kunt meerdere metagegevensprofielen maken en een apart profiel toepassen op elke auteur indien nodig. Maar je kunt slechts één metagegevensprofiel toepassen op een bepaalde auteur.
{.is-info}
  
## Releaseprofielen

Releaseprofielen worden gebruikt om te bepalen of indexeringsnamen in aanmerking komen voor het downloaden.

![releaseprofiles.png](/assets/readarr/releaseprofiles.png)  
  
- Profiel inschakelen - Vink het vakje aan om dit profiel in te schakelen.
- Moet bevatten - Voeg een lijst met woorden of zinnen toe die MOETEN voorkomen in de releasenaam om als geldig te worden beschouwd.
- Mag niet bevatten - Voeg een lijst met woorden of zinnen toe die NIET in de releasenaam mogen voorkomen om als geldig te worden beschouwd.
- Voorkeur (Woorden) - Hier kun je termen of regex toevoegen met scores (positief en negatief) om meer of minder wenselijk te worden beschouwd. Je kunt bijvoorbeeld de voorkeur geven aan "ongekort" met een positieve score.
  
> Releases met een hogere voorkeurswoordscore dan het bestaande bestand zijn ALTIJD een upgrade!
{.is-info}
  
- Voorkeur opnemen bij hernoemen Vink dit vakje aan om je voorkeurswoorden (of regex-overeenkomsten) op te nemen in de `{Voorkeurswoorden}` bestandsnaam toewijzingstoken.
  
> Je moet `{Voorkeurswoorden}` opnemen in je bestandsnaam en dit vakje aanvinken als je ze gebruikt, omdat je anders in een downloadlus terecht kunt komen.
{.is-warning}

- Indexer - In deze vervolgkeuzelijst kun je dit releaseprofiel beperken tot een enkele indexer. Dit moet bijna altijd op `(elke)` worden gelaten.
- Tags - Voer hier een tag in, zodat je deze tag kunt toepassen op auteurs met dezelfde tag. Als je hier geen tag toepast, is dit profiel van toepassing op ALLE auteurs.

## Vertragingsprofielen

- Vertragingsprofielen stellen je in staat om het aantal releases dat wordt gedownload voor een boek te verminderen door een vertraging toe te voegen terwijl Readarr blijft zoeken naar releases die beter overeenkomen met je voorkeuren.
- Protocol - Dit is ofwel `Usenet` of `Torrent`, afhankelijk van welk downloadprotocol je verkiest
- Usenet-vertraging - Ingesteld op het aantal minuten dat je wilt wachten voordat de download begint
- Torrent-vertraging - Ingesteld op het aantal minuten dat je wilt wachten voordat de download begint
- Bypass als hoogste kwaliteit - Vertraging omzeilen wanneer de release de hoogste ingeschakelde kwaliteitsprofiel heeft met het voorkeursprotocol
- Tags - Door dit vertragingsprofiel een tag te geven, kun je een bepaalde film taggen om deze te laten voldoen aan de hier ingestelde regels.
- Moersleutelpictogram - Hiermee kun je het vertragingsprofiel bewerken
- Plus-pictogram (<kb>+</kb>) - Maak een nieuw vertragingsprofiel

### Gebruik

Voor sommige media worden in de uren na een release een half dozijn verschillende releases van verschillende kwaliteit ontvangen, en zonder vertragingsprofielen kan Readarr proberen ze allemaal te downloaden. Met vertragingsprofielen kan Readarr worden geconfigureerd om de eerste paar uur van releases te negeren.

Vertragingsprofielen zijn ook handig als je de nadruk wilt leggen op één protocol (Usenet of BitTorrent) boven het andere. (Zie voorbeeld 3)

### Hoe vertragingsprofielen werken

De timer begint zodra Readarr een release detecteert die beschikbaar is voor een boek. Deze release wordt weergegeven in je Wachtrij met een klokpictogram om aan te geven dat deze onder vertraging staat.

> De klok begint vanaf het tijdstip waarop de release is geüpload en niet vanaf het moment dat Readarr deze ziet. {.is-info}

Tijdens de vertraging worden alle nieuwe releases die beschikbaar komen door Readarr opgemerkt. Wanneer de vertragingstimer afloopt, downloadt Readarr de enkele release die het beste overeenkomt met je kwaliteitsvoorkeuren.

De timerperiode kan verschillend zijn voor Usenet en torrents. Elk profiel kan worden geassocieerd met één of meer tags, zodat je kunt aanpassen welke shows welke profielen hebben. Een vertragingsprofiel zonder tag wordt beschouwd als de standaard en is van toepassing op alle shows die geen specifieke tag hebben.

> Vertragingsprofielen beginnen vanaf het tijdstempel dat de indexer rapporteert dat de release is geüpload. Dit betekent dat inhoud die ouder is dan het aantal minuten dat je hebt ingesteld, op geen enkele manier wordt beïnvloed door je vertragingsprofiel en direct wordt gedownload. Bovendien **negeert elke handmatige zoekopdracht** naar inhoud (niet-RSS-feed-zoekopdrachten) de instellingen van het vertragingsprofiel.
{.is-warning}

#### Voorbeelden

- Voor elk voorbeeld moet worden aangenomen dat de gebruiker het volgende kwaliteitsprofiel actief heeft: EPUB en hoger zijn toegestaan MOBI is de kwaliteitsdrempel * AZW3 is de hoogst gerangschikte kwaliteit

##### Voorbeeld 1

- In dit eenvoudige voorbeeld is het profiel ingesteld met een vertraging van 120 minuten (twee uur) voor zowel Usenet als torrents.

- Om 23:00 uur wordt de eerste release voor een boek gedetecteerd door Readarr en deze is geüpload om 22:50 uur en de 120 minuten durende timer begint. Om 00:50 uur zal Readarr alle releases evalueren die het in de afgelopen twee uur heeft gevonden en de beste downloaden, wat MOBI is.

- Om 03:00 uur wordt er een andere release gevonden, die MOBI is en om 02:46 uur aan je indexer is toegevoegd. Er begint een nieuwe 120 minuten durende timer. Om 04:46 uur wordt de best beschikbare release gedownload. Aangezien de kwaliteitsdrempel nu is bereikt, kan het boek niet meer worden geüpgraded en stopt Readarr met zoeken naar nieuwe releases.

- Op elk moment, als er een AZW3-release wordt gevonden, wordt deze direct gedownload omdat dit de hoogst gerangschikte kwaliteit is. Als er op dat moment een vertragingstimer actief is, wordt deze geannuleerd.

##### Voorbeeld 2

- Dit voorbeeld heeft verschillende timers voor Usenet en torrents. Stel een timer van 120 minuten in voor Usenet en een timer van 180 minuten voor BitTorrent.

- Om 23:00 uur wordt de eerste release voor een boek gedetecteerd door Readarr en beide timers beginnen. De release is om 22:15 uur aan de indexer toegevoegd. Om 00:15 uur zal Readarr alle releases evalueren en als er acceptabele Usenet-releases zijn, wordt de beste gedownload en eindigen beide timers. Zo niet, dan wacht Readarr tot 00:15 uur en downloadt de beste release, ongeacht de bron.

##### Voorbeeld 3

- Een veelvoorkomend gebruik voor vertragingsprofielen is om de nadruk te leggen op één protocol boven het andere. Bijvoorbeeld, je wilt alleen een BitTorrent-release downloaden als er na een bepaalde tijd niets naar Usenet is geüpload.

- Je kunt een timer van 60 minuten instellen voor BitTorrent en een timer van 0 minuten voor Usenet.

- Als de eerste release die wordt gedetecteerd afkomstig is van Usenet, downloadt Readarr deze direct.

- Als de eerste release afkomstig is van BitTorrent, stelt Readarr een timer van 60 minuten in. Als er tijdens die timer een geschikte Usenet-release wordt gedetecteerd, wordt de BitTorrent-release genegeerd en wordt de Usenet-release gedownload.

# Kwaliteit

![qualitydefinitions.png](/assets/readarr/qualitydefinitions.png)

## Betekenissen van de kwaliteitstabel

- Kwaliteit - De naam van de kwaliteit volgens de scene (hardcoded)
- Titel - De naam van de kwaliteit in de GUI (configureerbaar)
- Megabytes per minuut - Voor zichzelf sprekend
- Groottebeperking - Voor zichzelf sprekend
- Min - De minimale bytes of kilobytes per seconde (b/s|kb/s) die een kwaliteit kan hebben.
- Max - De maximale bytes of kilobytes per seconde (b/s|kb/s) die een kwaliteit kan hebben.

## Gedefinieerde kwaliteiten

- Onbekende tekst - Voor zichzelf sprekend
- PDF - Draagbaar documentformaat
- MOBI - Een van de meest gebruikte ebook-bestandsindelingen
- EPUB - Nog een van de meest gebruikte ebook-bestandsindelingen
- AZW3 - AZW3 is een eBook-bestand dat is ontwikkeld door Amazon. Het wordt gebruikt in Amazon Kindles om eBooks te bekijken.
- Onbekend audio - Voor zichzelf sprekend
- MP3 - Gangbaar lossy audioformaat
- M4B - Gangbaar audioboekbestandsformaat
- FLAC - Free Lossless Audio Codec, een audioformaat vergelijkbaar met MP3, maar lossless

# Indexers

> Informatie over ondersteunde indexers is te vinden op de [Meer informatie (Ondersteund)](/readarr/supported#indexers) pagina voor dit gedeelte
{.is-info}

## Ondersteunde indexers

- Een lijst met ondersteunde indexers is te vinden op de [Meer informatie (Ondersteund)](/readarr/supported#indexers) pagina

### Indexerinstellingen

- Zodra je op de <kb>+</kb>-knop hebt geklikt om een nieuwe indexer toe te voegen, krijg je een nieuw venster met veel verschillende opties te zien. Voor de doeleinden van deze wiki beschouwt Readarr zowel Usenet-indexers als torrent-trackers als "indexers".

- Hier zijn twee secties: Usenet en torrents. Op basis van welke downloadclient je gaat gebruiken, moet je het type indexer selecteren waarmee je aan de slag gaat.

### Usenet-indexerconfiguratie

- Verwijder voltooide downloads - Verwijder voltooide downloads wanneer deze klaar zijn (usenet) of gestopt/voltooid zijn (torrents)

- Readarr stuurt een downloadverzoek naar uw client en koppelt het aan een label of categorie die u hebt geconfigureerd in de instellingen van de downloadclient.
- Readarr controleert de actieve downloads van uw downloadclient die deze categorie gebruiken. Dit wordt gedaan via de API van uw downloadclient.
- Wanneer de download is voltooid, weet Readarr de uiteindelijke bestandslocatie zoals gerapporteerd door uw downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang het maar ergens apart van uw mediabibliotheek is.
- Readarr scant die voltooide bestandslocatie op videobestanden. Het analyseert de bestandsnaam van de video om deze te koppelen aan een boek. Als dat lukt, wordt het bestand hernoemd volgens uw specificaties en verplaatst naar de toegewezen bibliotheekmap.
- Overgebleven bestanden van de download worden naar uw prullenbak gestuurd of gerecycled.

Als u downloadt met een BitTorrent-client, verloopt het proces iets anders:

- Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat u kunt seeden. Wanneer bestanden worden geïmporteerd naar uw toegewezen bibliotheekmap, zal Readarr proberen een hardlink naar het bestand te maken of overschakelen naar kopiëren (gebruik dubbele ruimte) als hardlinks niet worden ondersteund.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen, zal Readarr de torrentclient vragen om het oorspronkelijke bestand en de torrent te verwijderen. Dit gebeurt echter alleen als de client rapporteert dat het seeden is voltooid, de torrent dezelfde categorie heeft (d.w.z. geen post-importcategorie gebruikt), het seeddoel wordt ondersteund door Readarr en de torrent is gepauzeerd (gestopt).

### Verwerking van mislukte downloads

- Verwerking van mislukte downloads is alleen compatibel met SABnzbd en NZBGet.
- Verwerking van mislukte downloads is niet van toepassing op torrents en er zijn geen plannen om deze functionaliteit toe te voegen.

- Er zijn verschillende componenten die deel uitmaken van het proces voor het verwerken van mislukte downloads:

- Controleer de downloader:
  - Wachtrij - Controleer de wachtrij van uw downloader op versleutelde releases die als mislukt zijn gemarkeerd
  - Geschiedenis - Controleer de geschiedenis van uw downloader op mislukkingen (bijv. niet genoeg om te repareren of extractie mislukt)
- Wanneer Readarr een mislukte download vindt, begint het met het verwerken ervan en doet het een paar dingen:
  - Voegt een mislukte gebeurtenis toe aan de geschiedenis van Readarr
  - Verwijdert de mislukte download uit de downloadclient om ruimte vrij te maken en gedownloade bestanden te wissen (optioneel)
  - Begint te zoeken naar een vervangend bestand (optioneel)
  - Blokkeerlijst (voorheen 'Blacklist') maakt automatisch overslaan van nzbs mogelijk wanneer ze mislukken, dit betekent dat die nzb nooit meer automatisch door Readarr wordt gedownload (u kunt de download nog steeds afdwingen via een handmatige zoekopdracht).
  - Er zijn 2 geavanceerde opties (op de pagina 'Downloadclient' instellingen) die het gedrag van het mislukken van downloads in Readarr bepalen, op dit moment staan ze allemaal standaard aan.

- Opnieuw downloaden - Bepaalt of Readarr zal zoeken naar hetzelfde bestand na een mislukking
- (Geavanceerde optie) Verwijderen - Bepaalt of de download automatisch moet worden verwijderd uit de downloadclient wanneer de mislukking wordt gedetecteerd

## Mappen van externe paden

- Het mappen van externe paden werkt als een eenvoudige zoekopdracht naar een extern pad en vervanging door een lokaal pad. Dit wordt voornamelijk gebruikt voor samengevoegde lokale/externe configuraties met behulp van mergerfs of iets dergelijks, of wanneer de toepassing en de downloadclient zich niet op dezelfde server bevinden.
- Een mapping van een extern pad wordt gebruikt wanneer uw downloadclient een pad rapporteert voor voltooide gegevens, ofwel op een andere server of op een manier die \*Arr niet adresseert naar die map.
- Over het algemeen is een mapping van een extern pad alleen nodig als uw downloadclient op Linux staat terwijl \*Arr op Windows staat, of vice versa. Een mapping van een extern pad is mogelijk ook nodig als u Docker- en native clients mixt, of als u een externe server gebruikt.
- Een mapping van een extern pad is een DOMME zoek/vervang (waarbij het de WAARDE VAN HET EXTERNE pad vindt en vervangt door de WAARDE VAN HET LOKALE pad voor de opgegeven host).
- Als het foutbericht over een ongeldig pad de VERVANGENDE waarde niet bevat, werkt de padmapping niet zoals u verwacht. De gebruikelijke oplossing is om de mapping toe te voegen en te verwijderen.
- [Zie de tutorial van TRaSH voor aanvullende informatie over het mappen van externe paden](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Als zowel \*Arr als uw Downloadclient Docker-containers zijn, is het zelden nodig om een mapping van een extern pad te gebruiken. Het wordt aanbevolen om [de Docker-handleiding](/docker-guide) te raadplegen en/of [de tutorial van TRaSH](https://trash-guides.info/hardlinks) te volgen.
{.is-info}

# Importlijsten

> Informatie over ondersteunde lijsttypen is te vinden op de [Meer informatie (Ondersteund)](/readarr/supported#lists) pagina voor dit gedeelte
{.is-info}

Met importlijsten kunt u items automatisch toevoegen aan Readarr vanuit uw GoodReads-boekenplanken of van andere gebruikers. Dit kan veel onverwachte items aan uw Readarr-database toevoegen, dus gebruik het alstublieft met zorg.

![importlists.png](/assets/readarr/importlists.png)

## Importlijsten

Hier ziet u de lijsten die u momenteel heeft en kunt u nieuwe lijsten toevoegen. Het toevoegen van lijsten wordt hieronder in meer detail besproken.

## Importlijstuitsluitingen

Alles wat hier staat, is uitgesloten van toevoeging door lijsten en wordt nooit toegevoegd vanuit welke lijst dan ook. U kunt items hiervan verwijderen door erop te klikken.

## Een importlijst toevoegen

Na het klikken op het <kb>+</kb>-teken, kiest u het soort lijst dat u wilt toevoegen:

![addlist.png](/assets/readarr/addlist.png)

In dit geval gaan we een GoodReads-boekenplanklijst toevoegen.

![bookshelflist.png](/assets/readarr/bookshelflist.png)

- Naam - Voer een naam in voor deze lijst.
- Automatisch toevoegen inschakelen - Als dit is ingeschakeld, worden alle items op de lijst automatisch toegevoegd aan Readarr.

> Dit voegt alle auteurs en ALLE BOEKEN van die auteur toe aan Readarr!

- Monitoren - Selecteer uw bewakingsniveau voor toegevoegde items. Geldige opties zijn `Geen`, `Geselecteerd boek` en `Alle boeken van de auteur`. Alle boeken worden toegevoegd aan Readarr, maar worden bewaakt of niet bewaakt op basis van deze selectie.
- Zoeken naar nieuwe items - Als dit is ingeschakeld, start Readarr een zoekopdracht naar ontbrekende bewaakte items wanneer ze worden toegevoegd vanuit een lijst. Als u veel auteurs/bewaakte boeken toevoegt, kan dit uw systeem overbelasten!
- Hoofdmap - Kies de hoofdmap voor auteurs die vanuit deze lijst worden toegevoegd
- Kwaliteitsprofiel - Kies uw kwaliteitsprofiel voor auteurs die vanuit deze lijst worden toegevoegd
- Metagegevensprofiel - Kies uw metagegevensprofiel voor auteurs die vanuit deze lijst worden toegevoegd
- Readarr-tags - Kies welke tags van toepassing zijn op auteurs die vanuit deze lijst worden toegevoegd

> Het wordt sterk aanbevolen om hier een beschrijvende tag toe te voegen. Anders weet u niet welke lijst deze items aan Readarr heeft toegevoegd, en zodra ze zijn toegevoegd, kunt u deze informatie nooit meer krijgen! Deze informatie wordt niet gelogd!

Standaard worden lijsten elke 24 uur gesynchroniseerd, maar kunnen handmatig worden geactiveerd vanaf de pagina `Instellingen` => `Taken`. U kunt dit proces niet automatiseren sneller dan dat.

# Verbinding maken

> Informatie over ondersteunde verbindingssoorten is te vinden op de [Meer informatie (Ondersteund)](/readarr/supported#notifications) pagina voor dit gedeelte
{.is-info}

## Verbindingen

Verbindingen bepalen hoe Readarr communiceert met de buitenwereld.

- Door op de <kb>+</kb>-knop te drukken, wordt een nieuw venster geopend waarin u veel verschillende eindpunten kunt configureren.

- Een lijst met ondersteunde meldingen en verbindingen is te vinden op de [Meer informatie (Ondersteund)](/readarr/supported#notifications) pagina.

## Verbindingsacties

- Bij het grijpen - Ontvang een melding wanneer boeken beschikbaar zijn om te downloaden en naar een downloadclient zijn gestuurd
- Bij importeren van release - Ontvang een melding wanneer boeken succesvol zijn geïmporteerd
- Bij upgraden - Ontvang een melding wanneer boeken worden geüpgraded naar een betere kwaliteit
- Bij mislukte download - Ontvang een melding wanneer een boekdownload mislukt (alleen Usenet)
- Bij mislukt importeren - Ontvang een melding wanneer een boekdownload niet kan worden geïmporteerd
- Bij hernoemen - Ontvang een melding wanneer boeken worden hernoemd
- Bij verwijderen van auteur - Ontvang een melding wanneer een auteur wordt verwijderd
- Bij verwijderen van boek - Ontvang een melding wanneer een boek wordt verwijderd
- Bij verwijderen van boekbestand - Ontvang een melding wanneer een boekbestand wordt verwijderd
- Bij verwijderen van boekbestand voor upgrade - Ontvang een melding wanneer een boekbestand wordt verwijderd voor een upgrade
- Bij opnieuw taggen van boek - Ontvang een melding wanneer boeken opnieuw worden getagd
- Bij problemen met de gezondheid - Ontvang een melding bij mislukte gezondheidscontroles
  - Gezondheidswaarschuwingen opnemen - Ontvang een melding bij gezondheidswaarschuwingen naast fouten.

# Metagegevens

{#write-metadata-to-book-files}

> Informatie over ondersteunde metagegevensverbruikers is te vinden op de [Meer informatie (Ondersteund)](/readarr/supported#metadata) pagina voor dit gedeelte
{.is-info}

Op deze pagina kunt u metagegevenstags/omslagen maken/bijwerken.

![metadata.png](/assets/readarr/metadata.png)

## Calibre-metagegevens

Als u Calibre gebruikt om uw e-boekencollectie te beheren, kunt u hiermee de controle over Calibre instellen.

- Metagegevens naar Calibre sturen
  - Alle bestanden; synchroniseren met GoodReads - Tags naar alle bestanden schrijven en bijwerken als GoodReads wordt bijgewerkt
  - Alle bestanden; alleen initiële import - Tags naar alle bestanden schrijven en niet bijwerken als GoodReads wordt bijgewerkt
  - Alleen voor nieuwe downloads - Tags alleen naar nieuwe downloads schrijven wanneer ze worden geïmporteerd
- Omslagen bijwerken - Inschakelen om Calibre Content Server te vertellen dezelfde boekomslagen als Readarr te gebruiken
- Metagegevens insluiten in boekbestanden - Inschakelen om Calibre Content Server te vertellen metagegevens in de boekbestanden te schrijven en in te sluiten.

## Metagegevens schrijven naar audiobestanden

Als u luisterboeken gebruikt, kunt u hiermee de controle over audiobestanden instellen.

- Audiobestanden taggen met metagegevens
  - Alle bestanden; synchroniseren met GoodReads - Tags naar alle bestanden schrijven en bijwerken als GoodReads wordt bijgewerkt
  - Alle bestanden; alleen initiële import - Tags naar alle bestanden schrijven en niet bijwerken als GoodReads wordt bijgewerkt
  - Alleen voor nieuwe downloads - Tags alleen naar nieuwe downloads schrijven wanneer ze worden geïmporteerd
- Bestaande tags verwijderen - Inschakelen om alle tags van bestanden te verwijderen, behalve die toegevoegd door Readarr

# Tags

- Het tag-gedeelte in Readarr wordt gebruikt om verschillende aspecten van Readarr met elkaar te verbinden.
- Tags zijn met name handig voor:

  - Releaseprofielen
  - Indexers
  - Importlijsten

- Tags kunnen worden gebruikt om Releaseprofielen, Indexers, Importlijsten en Auteurs/Boeken met elkaar te verbinden.
- Bijvoorbeeld:
  - U wilt dat een specifieke auteur/boek alleen een specifieke indexer gebruikt. U zou een tag maken en de auteur/boek en indexer aan die tag toewijzen.
  - U wilt dat een specifieke Importlijst alleen een specifiek Releaseprofiel gebruikt. U zou een tag maken en de Importlijst en het Releaseprofiel aan die tag toewijzen.

> Het wordt sterk aanbevolen om een beschrijvende tag toe te voegen aan een Importlijst, afgezien van wat hierboven is vermeld.

> Opmerking: Tags hebben geen invloed op "Kwaliteitsprofielen", "Metagegevensprofielen" of andere aspecten die hierboven niet worden genoemd.
{.is-info}

# Algemeen

Deze pagina bevat algemene instellingen voor Readarr die niet worden behandeld in andere secties.

## Host

![genhost.png](/assets/readarr/genhost.png)

- Bindadres - Geldig IPv4-adres of '*' voor alle interfaces
  - 0.0.0.0 of `*` - elk adres kan verbinding maken
  - 127.0.0.1 of localhost - alleen toepassingen op localhost kunnen verbinding maken
  - Elk ander IP (bijv. 1.2.3.4) - alleen dat IP (1.2.3.4) kan verbinding maken
- Poortnummer - Het poortnummer dat u wilt gebruiken om toegang te krijgen tot de webinterface van Readarr

> Opmerking: Raak deze instelling niet aan als u Docker gebruikt.
{.is-warning}

- URL-basis - Voor ondersteuning van omgekeerde proxy, standaard leeg

> Opmerking: Als u een omgekeerde proxy gebruikt (bijvoorbeeld mydomain.com/readarr), voert u '/readarr' in voor URL-basis.
{.is-info}

- SSL inschakelen - Als u SSL-certificaten heeft en de communicatie van en naar uw Readarr wilt beveiligen, schakel dan deze optie in.

> Opmerking: Gebruik dit niet tenzij u weet wat u doet.
{.is-warning}

## Beveiliging

![gensecurity.png](/assets/readarr/gensecurity.png)

- Authenticatie - Hoe wilt u zich authenticeren om toegang te krijgen tot uw Readarr-instantie
  - Geen - U heeft geen authenticatie nodig om toegang te krijgen tot uw Readarr. Meestal als u de enige gebruiker van uw netwerk bent, niemand op uw netwerk heeft die toegang tot uw Readarr zou willen hebben, of uw Readarr is niet blootgesteld aan het web
  - Basis (Browser pop-up) - Deze optie toont bij het openen van uw Readarr een klein pop-upvenster waarin u een gebruikersnaam en wachtwoord kunt invoeren
  - Formulieren (Aanmeldingspagina) - Deze optie heeft een vertrouwd uitziend aanmeldingsscherm, vergelijkbaar met andere websites, waarmee u kunt inloggen op uw Readarr
- API-sleutel - Hiermee kunnen andere programma's communiceren of Readarr communiceren met andere programma's. Deze sleutel kan, als deze in handen komt van de verkeerde persoon met toegang, allerlei dingen doen met uw bibliotheek. Daarom wordt de API-sleutel in de logboeken afgeschermd.
- Certificaatvalidatie - Wijzig hoe strikt de validatie van HTTPS-certificaten is
  - Ingeschakeld - Valideer alle HTTPS-certificaten (aanbevolen)
  - Uitgeschakeld voor lokale adressen - Valideer alle HTTPS-certificaten behalve die op localhost en het LAN
  - Uitgeschakeld - Valideer geen enkel HTTPS-certificaat

## Proxy

![genproxy.png](/assets/readarr/genproxy.png)

- Proxy - Met deze optie kunt u de informatie die uw Radarr ophaalt en doorzoekt via een proxy laten lopen. Dit kan handig zijn als u zich in een land bevindt dat het downloaden van torrentbestanden niet toestaat.

- Proxy gebruiken - Inschakelen om een proxy te gebruiken
- Proxytype - Selecteer uw proxytype (HTTPS, Socks4 of Socks5)
- Hostnaam - Voer de hostnaam van uw proxy in (Voeg geen http/https of een ander protocol toe)
- Poort - Voer de poort van uw proxy in
- Gebruikersnaam - Voer uw proxygebruikersnaam in indien van toepassing
- Wachtwoord - Voer uw proxysleutelwoord in indien van toepassing
- Genegeerde adressen - Voer een door komma's gescheiden lijst in van adressen die de proxy moeten omzeilen
- Proxy omzeilen voor lokale adressen - Vink het vakje aan om de proxy te omzeilen voor lokale adressen.

## Logboeken

![genlogging.png](/assets/readarr/genlogging.png)

- Logboekniveau - Waarschijnlijk een van de meest nuttige probleemoplossingstools
  - Info - Dit is de meest basale manier waarop Readarr informatie verzamelt. Dit bevat een zeer minimale hoeveelheid informatie in de logboeken. Dit logbestand bevat fatale, fout-, waarschuwings- en informatieberichten.
  - Debug - Debug bevat alle informatie die Info bevat, plus meer informatie die nuttig kan zijn. Dit logbestand bevat fatale, fout-, waarschuwings-, informatie- en debugberichten.
  - Trace - Het meest geavanceerde en gedetailleerde loggen op Readarr, Trace bevat alle informatie die Info en Debug bevatten en meer. Dit is het meest voorkomende type log dat wordt gevraagd bij het oplossen van problemen op Discord of Reddit. Als u hulp nodig heeft, selecteer dan uw logboek op Trace en voer de taak opnieuw uit die u problemen gaf om het logboek vast te leggen. Dit logbestand bevat fatale, fout-, waarschuwings-, informatie-, debug- en traceberichten.

## Analyse

![genanalytics.png](/assets/readarr/genanalytics.png)

- Analyse - Anonieme gebruiks- en foutinformatie naar de servers van Readarr (Servarr) sturen. Dit omvat informatie over uw browser, welke Readarr WebUI-pagina's u gebruikt, foutenrapportage, evenals OS- en runtimeversie. We zullen deze informatie gebruiken om functies en bugfixes te prioriteren.

## Updates

![genupdates.png](/assets/readarr/genupdates.png)

## Updates

- (Geavanceerde optie) Branch - Dit is de branch van Readarr waarop u draait.
  - [Raadpleeg deze FAQ voor meer informatie](/readarr/faq#how-do-i-update-readarr)
- Automatisch - Updates automatisch downloaden en installeren. U kunt nog steeds installeren via Systeem: Updates. Opmerking: Windows-gebruikers worden altijd automatisch bijgewerkt.
- Mechanisme - Gebruik de ingebouwde updater van Readarr of een script
  - Ingebouwd - Gebruik de eigen updater van Readarr
  - Script - Laat Readarr het update-script uitvoeren
  - Docker - Werk Readarr niet bij vanuit Docker, maar haal een geheel nieuwe image op met de nieuwe update
- Script - Alleen zichtbaar wanneer Mechanisme is ingesteld op Script - Pad naar update-script
- Updateproces - Readarr downloadt het updatebestand, controleert de integriteit ervan, extrahert het naar een tijdelijke locatie en roept de gekozen methode aan. Het updateproces wordt uitgevoerd onder dezelfde gebruiker als waar Readarr onder wordt uitgevoerd, het heeft toestemming nodig om de Readarr-bestanden bij te werken en Readarr te stoppen/starten.
- Ingebouwd - De ingebouwde methode maakt een back-up van de Readarr-bestanden en -instellingen, stopt Readarr, werkt de installatie bij en start Readarr opnieuw op. Als uw systeem het stoppen van Readarr niet aankan en automatisch probeert het opnieuw te starten, is het misschien beter om in plaats daarvan een script te gebruiken. Bij een fout wordt de vorige versie van Readarr opnieuw gestart.
- Script - Het script moet hetzelfde behandelen als de ingebouwde updater. Als u services moet stoppen en starten (upstart/launchd/etc), moet u dat hier doen.

## Back-ups

![genbackups.png](/assets/readarr/genbackups.png)

- Het back-upgedeelte stelt u in staat om Readarr te vertellen hoe u back-ups wilt beheren

- Map - Hiermee kunt u de back-uplocatie selecteren. In Docker bent u beperkt tot wat u de container laat zien. Padnamen zijn relatief ten opzichte van de appdata-map; indien nodig kunt u een absoluut pad instellen om een back-up buiten de appdata-map te maken.
- Interval - Hoe vaak wilt u dat Readarr een back-up maakt
- Behoud - Hoe lang wilt u dat Readarr elke back-up bewaart. Na het maken van een nieuwe back-up wordt de oudste back-up verwijderd.

Standaard worden back-ups elke 7 dagen uitgevoerd en worden de laatste 4 bewaard.

# UI (Gebruikersinterface)

Deze pagina stelt u in staat om de weergaveopties van de gebruikersinterface aan te passen.

## Kalender

![uicalendar.png](/assets/readarr/uicalendar.png)

- Eerste dag van de week - Hier kunt u selecteren wat u denkt dat de eerste dag van de week moet zijn.
- Weekkolomkop - Hier kunt u de kop voor de kolommen selecteren.

## Datums

![caldates.png](/assets/readarr/caldates.png)

- Korte datumnotatie - Hoe wilt u dat Readarr korte datums weergeeft?
- Lange datumnotatie - Hoe wilt u dat Readarr lange datums weergeeft?
- Tijdnotatie - Wilt u een 12-uurs of 24-uurs notatie?
- Relatieve datums weergeven - Wilt u dat Readarr relatieve (Vandaag/Gisteren/etc.) of absolute datums weergeeft?

## Stijl

![calstyle.png](/assets/readarr/calstyle.png)

- Kleurenblinde modus inschakelen - Gewijzigde stijl om kleurenblinde gebruikers in staat te stellen kleurgecodeerde informatie beter te onderscheiden.

## Taal

![callanguage.png](/assets/readarr/callanguage.png)

- UI-taal - Selecteer de taal die Radarr moet gebruiken binnen de applicatie-UI.