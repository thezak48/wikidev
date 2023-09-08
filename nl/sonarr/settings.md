---
title: Sonarr-instellingen
description: 
published: true
date: 2023-04-29T18:16:05.634Z
tags: sonarr, needs-love, instellingen
editor: markdown
dateCreated: 2021-06-11T23:29:12.300Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Menu-opties](#menu-opties)
- [Mediabeheer](#mediabeheer)
  - [Community-namingsuggesties](#community-namingsuggesties)
  - [Afleveringsnaamgeving](#afleveringsnaamgeving)
    - [Standaard afleveringsindeling](#standaard-afleveringsindeling)
    - [Serienamegeving](#serienamegeving)
    - [Serie-IDs](#serie-ids)
    - [Seizoenen](#seizoenen)
    - [Afleveringen](#afleveringen)
    - [Uitzenddatum](#uitzenddatum)
    - [Afleveringstitel](#afleveringstitel)
    - [Kwaliteit](#kwaliteit)
    - [Mediainformatie](#mediainformatie)
    - [Overige](#overige)
    - [Origineel](#origineel)
  - [Indeling dagelijkse afleveringen](#indeling-dagelijkse-afleveringen)
  - [Indeling anime-afleveringen](#indeling-anime-afleveringen)
    - [Absoluut afleveringsnummer](#absoluut-afleveringsnummer)
  - [Indeling seriesmap](#indeling-seriesmap)
    - [Serienamegeving](#serienamegeving-1)
    - [Serie-IDs](#serie-ids-1)
  - [Indeling seizoensmap](#indeling-seizoensmap)
    - [Seizoenen](#seizoenen-1)
  - [Indeling seizoensmap](#indeling-seizoensmap-1)
    - [Speciale afleveringen](#speciale-afleveringen)
  - [Stijl voor meerdere afleveringen](#stijl-voor-meerdere-afleveringen)
  - [Mappen](#mappen)
  - [Importeren](#importeren)
  - [Bestandsbeheer](#bestandsbeheer)
  - [Machtigingen](#machtigingen)
  - [Hoofdmappen](#hoofdmappen)
- [Profielen](#profielen)
  - [Kwaliteitsprofielen](#kwaliteitsprofielen)
  - [Taalprofielen](#taalprofielen)
  - [Vertragingsprofielen](#vertragingsprofielen)
    - [Gebruik](#gebruik)
    - [Hoe vertragingsprofielen werken](#hoe-vertragingsprofielen-werken)
      - [Voorbeelden](#voorbeelden)
        - [Voorbeeld 1](#voorbeeld-1)
        - [Voorbeeld 2](#voorbeeld-2)
        - [Voorbeeld 3](#voorbeeld-3)
  - [Releaseprofielen](#releaseprofielen)
- [Kwaliteit](#kwaliteit-1)
  - [Betekenissen van kwaliteitstabellen](#betekenissen-van-kwaliteitstabellen)
  - [Gedefinieerde kwaliteiten](#gedefinieerde-kwaliteiten)
- [Indexers](#indexers)
  - [Ondersteunde indexers](#ondersteunde-indexers)
    - [Indexerinstellingen](#indexerinstellingen)
    - [Usenet-indexerconfiguratie](#usenet-indexerconfiguratie)
    - [Torrent-trackerconfiguratie](#torrent-trackerconfiguratie)
  - [Opties](#opties)
- [Downloadclients](#downloadclients)
  - [Overzicht](#overzicht)
  - [Processen van downloadclients](#processen-van-downloadclients)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Downloadclients](#downloadclients-1)
    - [Ondersteunde downloadclients](#ondersteunde-downloadclients)
    - [Usenet-clientinstellingen](#usenet-clientinstellingen)
    - [Torrent-clientinstellingen](#torrent-clientinstellingen)
    - [Compatibiliteit verwijderen download in torrentclient](#compatibiliteit-verwijderen-download-in-torrentclient)
  - [Afgehandelde voltooide downloads](#afgehandelde-voltooide-downloads)
    - [Voltooide downloads verwijderen](#voltooide-downloads-verwijderen)
    - [Foutafhandeling bij downloaden](#foutafhandeling-bij-downloaden)
  - [Mappen voor externe paden](#mappen-voor-externe-paden)
- [Importlijsten](#importlijsten)
  - [Lijsten](#lijsten)
  - [Uitsluitingen van lijsten](#uitsluitingen-van-lijsten)
- [Verbinding maken](#verbinding-maken)
  - [Verbindingen](#verbindingen)
  - [Verbindingsactiveringen](#verbindingsactiveringen)
- [Metadata](#metadata)
  - [Metadata](#metadata-1)
- [Tags](#tags)
- [Algemeen](#algemeen)
  - [Host](#host)
  - [Beveiliging](#beveiliging)
  - [Proxy](#proxy)
  - [Logging](#logging)
  - [Analyse](#analyse)
  - [Updates](#updates)
  - [Back-ups](#back-ups)
- [UI](#ui)
  - [Kalender](#kalender)
  - [Datums](#datums)
  - [Stijl](#stijl)
  
Deze pagina behandelt alle beschikbare instellingen in Sonarr en hoe ze werken. Dit is geen uitgebreide "Hoe stel ik Sonarr in." Raadpleeg in plaats daarvan de [Snelstartgids](/sonarr/quick-start-guide) pagina.

# Menu-opties

Om naar de instellingenpagina te gaan, kies je Instellingen in het linkermenu. De volgende submenu-opties zijn beschikbaar:

![settings_1_menu.png](/assets/sonarr/settings_1_menu.png)

Let ook op dat voor elke individuele instellingenpagina enkele opties bovenaan het menu staan:

![settings_2_topmenu.png](/assets/sonarr/settings_2_topmenu.png)

- Verbergen/tonen van geavanceerde opties is belangrijk voor items die hieronder zijn gemarkeerd als `(Geavanceerde optie)`, anders worden ze niet weergegeven. Deze menu-items worden weergegeven in het oranje op de schermafbeeldingen.

- Je moet je wijzigingen opslaan voordat je het scherm verlaat. Dit doe je door op het schijf-icoon te klikken. Als je geen wijzigingen hebt aangebracht, wordt "Geen wijzigingen" weergegeven en is het grijs, zoals hierboven getoond.

# Mediabeheer

> Sommige van deze instellingen zijn alleen zichtbaar via `Geavanceerde instellingen weergeven`, dat zich bevindt in de bovenste balk onder de zoekbalk{.is-info}

## Community-namingsuggesties

> Hieronder staan enkele Community-namingsuggesties van [TRaSH's Guides](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/) {.is-info}

> Waarschuwing: Vanaf v3.0.6.1431 ondersteunt Sonarr nu het herkennen van Dolby Vision (DV) en High Dynamic Range (HDR) types. Als je een lagere versie gebruikt, vervang dan: `{[MediaInfo VideoDynamicRangeType]}` door `{[MediaInfoVideoDynamicRange]}` {.is-warning}

- Standaardserie: `{Series TitleYear} - S{season:00}E{episode:00} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Dagelijkse serie: `{Series TitleYear} - {Air-Date} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Animeserie: `{Series TitleYear} - S{season:00}E{episode:00} - {absolute:000} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}[{MediaInfo VideoBitDepth}bit]{[MediaInfo VideoCodec]}[{Mediainfo AudioCodec} { Mediainfo AudioChannels}]{MediaInfo AudioLanguages}{-Release Group}`

- Seizoensmappen: `Seizoen {season:00}`

- Stijl voor meerdere afleveringen: `Scene`

- Seriesmappen: `{Series TitleYear} [imdb-{ImdbId}]`

## Afleveringsnaamgeving

- Hernoem afleveringen - Vink aan om Sonarr in staat te stellen bestanden te hernoemen
  - Als niet aangevinkt:
    - Importeren van downloadclient
      - Niet-seizoenspakket: de titel van de release van de downloadclient wordt gebruikt
      - Seizoenspakket: oorspronkelijke bestandsnaam
    - Handmatig (ad-hoc) importeren: oorspronkelijke bestandsnaam

- Vervang ongeldige tekens - Als niet aangevinkt, zal Sonarr ze verwijderen.
  - De tekens zijn: `:` `\` `/` `>` `<` `?` `*` `|` `"`

### Standaard afleveringsindeling

Standaard afleveringsindeling - Stel de naamgevingsconventie in voor je standaard serieafleveringen. Klik op het `?`-pictogram om het dialoogvenster `Bestandsnaamtokens` te openen.

- Keuzelijst (rechterbovenhoek)
  - Linkervak - Spatiebehandeling
  - Spatie ( ) - Gebruik spaties in de naamgeving (standaard)
  - Punt (.) - Gebruik punten in plaats van spaties in de naamgeving
  - Onderstrepingsteken (_) - Gebruik onderstrepingstekens in plaats van spaties in de naamgeving
  - Streepje (-) - Gebruik streepjes in plaats van spaties in de naamgeving
  - Rechtervak - Hoofdletterbehandeling
  - Standaardhoofdletters - Maak de titel hoofdletters en kleine letters (~camel-case) (standaard)
  - Hoofdletters - Maak de titel volledig in hoofdletters
  - Kleine letters - Maak de titel volledig in kleine letters

### Serienamegeving

- `{Series Title}` = De titel van de serie!
- `{Series CleanTitleYear}` = De titel van de serie! 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = De titel van de serie!
- `{Series TitleThe}` = De titel van de serie!, The
- `{Series TitleYear}` = De titel van de serie (2010)
- `{Series Year}` = (2010)

### Serie-IDs

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}`= 54321

### Seizoenen

- `{season:0}` = 1
- `{season:00}` =  01

### Afleveringen

- `{episode:0}` = 1
- `{episode:00}` = 01

### Uitzenddatum

- `{Air-Date}` = 2020-09-03
- `{Air Date}` = 2020 09 03

### Afleveringstitel

- `{Episode Title}` = Afleveringstitel
- `{Episode CleanTitle}` =  Afleveringstitel

### Kwaliteit

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### Mediainformatie

- `{MediaInfo Simple}` = x264 DTS
- `{MediaInfo Full}` = x264 DTS \[EN+DE\]
- `{MediaInfo AudioCodec}` = DTS
- `{MediaInfo AudioChannels}` = 5.1
- `{MediaInfo AudioLanguagesAll}` = \[DE\]
- `{MediaInfo AudioLanguagesAll}` = \[EN+DE\]
- `{MediaInfo SubtitleLanguages}` = \[EN\]
- `{MediaInfo VideoCodec}` = x264
- `{MediaInfo VideoBitDepth}` = 8
- `{MediaInfo VideoDynamicRange}` = HDR
- `{MediaInfo VideoDynamicRangeType}` = DV HDR10

> `MediaInfo Full`, `AudioLanguages` en `SubtitleLanguages` ondersteunen een `:EN+DE`-achtervoegsel waarmee je de talen kunt filteren die in de bestandsnaam zijn opgenomen. Gebruik `-DE` om specifieke talen uit te sluiten. Het toevoegen van <kb>+</kb> (bijv.: `:EN+`) geeft `[EN]`, `[EN+--]` of `[--]` afhankelijk van de uitgesloten talen. Gebruik bijvoorbeeld `{MediaInfo Full:EN+DE}`.
{.is-info}

> `AudioLanguages` geeft geen taal weer voor audio als er slechts één taal bestaat en het EN (Engels) is. Om het gewenste gedrag te krijgen en als voorbeeld Duits en Engels weer te geven, gebruik je {MediaInfo AudioLanguagesAll:DE+EN} in plaats daarvan.
{.is-info}

> `MediaInfo VideoDynamicRangeType` geeft mogelijke waarden van: DV, DV HDR10, HDR10, HDR10Plus, HLG, PQ en HDR
{.is-info}

### Overige

- `{Release Group}` = Rls Grp
- `{Preferred Words}` = iNTERNAL of NF

> \* Voorkeurswoorden zijn het woord of de woorden die letterlijke overeenkomsten zijn met eventuele voorkeurswoorden die je hebt. Het bovenstaande voorbeeld zou een voorkeurswoord zijn van `iNTERNAL` of vergelijkbaar een voorkeurswoord van `/\b(amzn|amazon)\b(?=[ ._-]web[ ._-]?(dl|rip)\b)/i` zou `AMZN` of `Amazon` retourneren
\* `{Preferred Words:<Release Profile Name>}` is een extra optie om overeenkomsten alleen uit specifieke releaseprofielen te gebruiken
{.is-info}

### Origineel

- `{Original Title}` = Series.Title.S01E01.WEBDL.NF.1080P.x264-EVOLVE
- `{Original Filename}` = Series.title.s01e01.WEBDL.NF.1080P.x264-EVOLVE

> `Original Title` is de releasenaam en het wordt aanbevolen om deze te gebruiken.
{.is-info}

>`Original Filename` wordt niet aanbevolen. Het is de letterlijke oorspronkelijke bestandsnaam en kan worden versluierd `t1i0p3s7i8yu7ti`.
{.is-warning}

## Indeling dagelijkse afleveringen

Indeling dagelijkse afleveringen - Stel de naamgevingsconventie in voor je dagelijkse serieafleveringen. Klik op het `?`-pictogram om het dialoogvenster `Bestandsnaamtokens` te openen.

Zie [Standaard afleveringsindeling](/sonarr/settings#standaard-afleveringsindeling) voor meer informatie over dit dialoogvenster.

## Indeling anime-afleveringen

Indeling anime-afleveringen - Stel de naamgevingsconventie in voor je anime serieafleveringen. Klik op het `?`-pictogram om het dialoogvenster `Bestandsnaamtokens` te openen.

Zie [Standaard afleveringsindeling](/sonarr/settings#standaard-afleveringsindeling) voor meer informatie over dit dialoogvenster.

### Absoluut afleveringsnummer

- `{absolute:0}` = 1
- `{absolute:00}` = 01
- `{absolute:000}` =001

## Indeling seriesmap

(Geavanceerde optie) - Seriesmap - Stel de naamgevingsconventie in voor de map. Klik op het `?`-pictogram om het dialoogvenster `Bestandsnaamtokens` te openen.

### Serienamegeving

- `{Series Title}` = Serienaam!
- `{Series CleanTitleYear}` = Serienaam 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Serienaam
- `{Series TitleThe}` = Serienaam, The
- `{Series TitleYear}` = Serienaam (2010)
- `{Series Year}` = (2010)

### Serie-IDs

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}` = 54321

## Indeling seizoensmap

### Seizoenen

- `{season:0}` = 1
- `{season:00}` = 01

## Indeling seizoensmap

### Speciale afleveringen

Naam voor de `Speciale afleveringen` (Seizoen) map

- `Speciale afleveringen`

> Het wordt aanbevolen om `Speciale afleveringen` te gebruiken
{.is-info}

## Stijl voor meerdere afleveringen

- `Uitbreiden` = `S01E01-02-03`
- `Dupliceren` = `S01E01.S01E01`
- `Herhalen` = `S01E01E02E03`
- `Scene` = `S01E01-E02-E03`
- `Reeks` = `S01E01-03`
- `Voorvoegselreeks` = `S01E01-E03`

> Het wordt aanbevolen om `Scene` te gebruiken
{.is-info}

## Mappen

- Lege mediamappen maken - Ontbrekende seriesmappen maken tijdens het scannen van de schijf
- Lege mappen verwijderen - Lege series- en seizoenmappen verwijderen tijdens het scannen van de schijf en wanneer afleveringsbestanden worden verwijderd

## Importeren

- Episode Titel Vereist - Voorkom importeren gedurende maximaal 48 uur vanaf de [UTC](https://nl.wikipedia.org/wiki/Coordinated_Universal_Time) uitzendtijd van de aflevering als de afleveringstitel in het juiste formaat staat en de afleveringstitel TBA is. Na 48 uur wordt de release geïmporteerd, zelfs als de titel nog steeds TBA is.
  - Altijd - Wacht altijd maximaal 48 uur op een titel voordat je importeert als de aflevering TBA is.
  - Alleen voor bulkseizoensreleases - Wacht alleen maximaal 48 uur op een titel voordat je importeert als er een seizoenspakket of bulkrelease is gevonden en de aflevering TBA is. <- Dit wordt aanbevolen.
  - Nooit - Vertraag het importeren niet als de aflevering TBA is.
- Overslaan van vrije ruimtecontrole - Gebruik dit wanneer Sonarr geen vrije ruimte kan detecteren vanuit de hoofdmap van je serie.
- Minimale vrije ruimte - Het in- of uitschakelen hiervan voorkomt importeren als er minder dan deze hoeveelheid schijfruimte beschikbaar is.
- Gebruik harde koppelingen in plaats van kopiëren - Gebruik harde koppelingen bij het kopiëren van bestanden van torrents die nog steeds worden gezaaid.
  - Klik [hier](https://trash-guides.info/hardlinks) voor meer informatie hierover.

 > Zelden - maar mogelijk - kunnen bestandsvergrendelingen voorkomen dat bestanden die worden gezaaid, worden hernoemd. U kunt het zaaien tijdelijk uitschakelen en de hernoemingsfunctie van Sonarr gebruiken als tijdelijke oplossing.
{.is-warning}

- Extra bestanden importeren - Importeer bijpassende extra bestanden (ondertitels, nfo, etc.) na het importeren van een bestand.
  Als een ondertitelbestandsnaam extra tags bevat zoals `cc` of `forced`, worden deze behouden zolang ze worden herkend (momenteel in de ontwikkelversie).

## Bestandsbeheer

- Niet-bewaakte verwijderde afleveringen - Afleveringen die van de schijf zijn verwijderd, worden automatisch niet-bewaakt in Sonarr.
- Download Proper & Repacks - Of er automatisch moet worden geüpgraded naar Propers/Repacks. Gebruik `Niet voorkeur geven` om te sorteren op voorkeurswoordenscore boven propers/repacks.
  - Voorkeur en upgraden - Rangschik repacks en propers hoger dan niet-repacks en niet-propers. Behandel nieuwe repacks en propers als een upgrade naar huidige releases.
  - Niet automatisch upgraden - Rangschik repacks en propers hoger dan niet-repacks en niet-propers. Behandel nieuwe repacks en propers niet als een upgrade naar huidige releases.
  - Geen voorkeur geven - Dit negeert effectief repacks en propers. U moet eventuele voorkeur hiervoor beheren met [Releaseprofielen (Voorkeurswoorden)](#releaseprofielen).

> `PROPER` - betekent dat er een probleem was met de vorige release. Downloads met de tag PROPER geven aan dat de problemen in die release zijn opgelost. Dit wordt gedaan door een groep die de oorspronkelijke release niet heeft uitgebracht.
> `REPACK` - betekent dat er een probleem was met de vorige release en dat dit is gecorrigeerd door de oorspronkelijke groep. Downloads met de tag REPACK geven aan dat de problemen in die release zijn opgelost. Dit wordt gedaan door een groep die de oorspronkelijke release heeft uitgebracht.
{.is-info}

> [Gebruik voorkeurswoorden voor automatische upgrades naar propers/repacks](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#propers-and-repacks)
{.is-info}

- Video-bestanden analyseren - Bestandsinformatie zoals resolutie, looptijd en codec-informatie uit bestanden halen. Hiervoor moet Sonarr delen van het bestand lezen, wat kan leiden tot hoge schijf- of netwerkactiviteit tijdens scans.
- Seriesmap opnieuw scannen na vernieuwen - De seriesmap opnieuw scannen na het vernieuwen van de serie
  - Altijd - Dit scant de seriesmap opnieuw op basis van de taakplanning
  - Na handmatige vernieuwing - U moet handmatig de schijf opnieuw scannen
  - Nooit - Zoals de naam al zegt, de seriesmap nooit opnieuw scannen.
- Bestandsdatum wijzigen - Bestandsdatum wijzigen bij importeren/opnieuw scannen
  - Geen - Sonarr wijzigt de datum niet die wordt weergegeven in je bestandsbrowser
  - Lokale release - De datum waarop de video lokaal is uitgezonden
  - UTC-release datum - De datum waarop de video is uitgebracht op basis van UTC
- Prullenbak - Afleveringsbestanden worden hierheen verplaatst wanneer ze worden verwijderd in plaats van permanent te worden verwijderd
- Prullenbak opruimen - Dit is hoe oud een gegeven bestand kan zijn voordat het permanent wordt verwijderd

> Bestanden in de prullenbak die ouder zijn dan het geselecteerde aantal dagen worden automatisch opgeruimd {.is-warning}

## Machtigingen

- Machtigingen instellen - Moet `chmod` worden uitgevoerd wanneer bestanden worden geïmporteerd/hernoemd?
  - chmod-map - Octaal, toegepast tijdens importeren/hernoemen op mediamappen en -bestanden (zonder uitvoeringsbits)

> Het vervolgkeuzemenu bevat een vooraf ingestelde lijst met veelgebruikte machtigingen die kunnen worden gebruikt. U kunt echter handmatig een map-octaal invoeren als u dat wilt.
{.is-info}

> Dit werkt alleen als de gebruiker die `Sonarr` uitvoert de eigenaar van het bestand is. Het is beter om ervoor te zorgen dat de downloadclient de machtigingen correct instelt.
{.is-warning}

- chown-groep - Groepsnaam of GID. Gebruik GID voor externe bestandssystemen

> Dit werkt alleen als de gebruiker die `Sonarr` uitvoert de eigenaar van het bestand is. Het is beter om ervoor te zorgen dat de downloadclient de machtigingen correct instelt.
{.is-warning}

## Hoofdmappen

- Pad - Dit toont het pad naar je mediatheek
- Vrije ruimte - Dit is de vrije ruimte die aan Sonarr wordt gerapporteerd door het systeem
- Niet-toegewezen mappen - Dit zijn mappen waar geen serie aan is gekoppeld

> Het `X`-teken aan het einde verwijdert dit hoofdpad
{.is-info}

- Hoofdmap toevoegen - Hiermee kunt u een hoofdpad selecteren als een plaats om nieuwe geïmporteerde downloads in deze map te plaatsen of om Sonarr bestaande media te laten scannen.

> Gebruikers van niet-Windows:
> \* Als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
> \* Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.
{.is-warning}

# Profielen

## Kwaliteitsprofielen

- Stel profielen in voor de kwaliteit van series die je wilt downloaden.

> Bij het selecteren van een bestaand profiel of het toevoegen van een extra profiel verschijnt er een nieuw venster
{.is-info}

> Opmerking: De kwaliteit met een blauw vakje is de kwaliteit waarop alle media met dit profiel blijven upgraden.
{.is-info}

- Naam - Selecteer een **UNIEKE** naam voor het kwaliteitsprofiel dat je maakt
- Upgrades toegestaan - Wanneer deze optie is aangevinkt en je Sonarr vertelt om een `WEB 1080p` te downloaden omdat het de eerste release van een specifieke aflevering is, en later iemand in staat is om een `Bluray-1080p` te uploaden, zal Sonarr automatisch upgraden naar de betere kwaliteit ***als*** `Upgrade Until` die kwaliteit heeft geselecteerd
- Upgrade Until - Zodra deze kwaliteit is bereikt, zal Sonarr geen afleveringen meer downloaden

> Opmerking: Dit is alleen van toepassing als je `Bluray-1080p` hoger hebt dan `WEB 1080p` binnen de sectie `Kwaliteiten`
{.is-warning}

- Kwaliteiten - Kwaliteiten hoger in de lijst hebben meer voorkeur, zelfs als ze niet zijn aangevinkt. Kwaliteiten binnen dezelfde groep zijn gelijk. Alleen aangevinkte kwaliteiten zijn gewenst.
- Groepen bewerken - Sommige kwaliteiten zijn gegroepeerd om de grootte van de lijst te verkleinen, evenals het groeperen van vergelijkbare releases. Een goed voorbeeld hiervan is `WebDL` en `WebRip`, omdat deze zeer vergelijkbaar zijn en meestal vergelijkbare bitrates hebben. Bij het bewerken van de groepen kunt u de voorkeur binnen elke groep wijzigen. [Zie TRaSh's gids voor het samenvoegen van kwaliteiten](https://trash-guides.info/merge-quality)
  - [Zie Kwaliteiten](#kwaliteiten-gedefinieerd)

> Standaard zijn de kwaliteiten ingesteld van laagste (onderaan) naar hoogste (bovenaan)
{.is-info}

## Taalprofielen

- Stel profielen in voor de taal van series die je wilt downloaden.

> Houd er rekening mee dat de prioriteit/volgorde wel van belang is, zelfs als de taal niet gewenst (geselecteerd) is.
{.is-info}

- Naam - Selecteer een **UNIEKE** naam voor het taalprofiel dat je maakt
- Upgrades toegestaan - Als uitgevinkt (uitgeschakeld) worden talen niet geüpgraded. Als je bijvoorbeeld Sonarr vertelt om een Chinese versie te downloaden omdat het de eerste release van een specifieke serie is en later iemand in staat is om een Engelse versie te uploaden, dan zal Sonarr met deze optie geselecteerd automatisch upgraden naar de betere kwaliteit

> Dit is alleen geldig als Engels hoger in de taallijst staat dan Chinees en beide zijn geselecteerd
{.is-warning}

- Talen - Talen hoger in de lijst hebben meer voorkeur. Alleen aangevinkte talen zijn gewenst

## Vertragingsprofielen

- Vertragingsprofielen stellen je in staat om het aantal releases dat wordt gedownload voor een aflevering te verminderen door een vertraging toe te voegen terwijl Sonarr blijft zoeken naar releases die beter overeenkomen met je voorkeuren.
- Voorkeursprotocol - Dit zal ofwel `Usenet` of `Torrent` zijn, afhankelijk van welk downloadprotocol je verkiest
- Usenet-vertraging - Ingesteld op het aantal minuten dat je wilt wachten voordat de download begint
- Torrent-vertraging - Ingesteld op het aantal minuten dat je wilt wachten voordat de download begint
- Overslaan als hoogste kwaliteit - Vertraging overslaan wanneer de release de hoogst ingeschakelde kwaliteitsprofiel heeft met het voorkeursprotocol
- Tags - Door dit vertragingsprofiel een tag te geven, kun je een bepaalde serie taggen om zich te houden aan de hier ingestelde regels.
- Moersleutel-icoon - Hiermee kun je het vertragingsprofiel bewerken
- Plus-icoon (<kb>+</kb>) - Maak een nieuw vertragingsprofiel

### Gebruik

Sommige media ontvangen in de uren na een release een half dozijn verschillende releases van verschillende kwaliteit, en zonder vertragingsprofielen kan Sonarr proberen ze allemaal te downloaden. Met vertragingsprofielen kan Sonarr worden geconfigureerd om de eerste paar uur van releases te negeren.

Vertragingsprofielen zijn ook handig als je de nadruk wilt leggen op één protocol (Usenet of BitTorrent) boven het andere. (Zie [Voorbeeld 3](/sonarr/settings/#example-3))

### Hoe vertragingsprofielen werken

De timer begint zodra Sonarr detecteert dat er een release beschikbaar is voor een aflevering. Deze release wordt weergegeven in je Wachtrij met een klokpictogram om aan te geven dat deze onder vertraging staat.

> De klok begint vanaf het moment dat de releases zijn geüpload en niet vanaf het moment dat Sonarr ze ziet.
{.is-info}

Tijdens de vertraging worden eventuele nieuwe releases die beschikbaar komen door Sonarr opgemerkt. Wanneer de vertragingstimer afloopt, zal Sonarr de enkele release downloaden die het beste overeenkomt met je kwaliteitsvoorkeuren.

De timerperiode kan verschillend zijn voor Usenet en torrents. Elk profiel kan worden geassocieerd met één of meer tags, zodat je kunt aanpassen welke shows welke profielen hebben. Een vertragingsprofiel zonder tag wordt beschouwd als de standaard en is van toepassing op alle shows die geen specifieke tag hebben.

> Vertragingsprofielen beginnen vanaf het tijdstempel waarop de indexer meldt dat de release is geüpload. Dit betekent dat inhoud die ouder is dan het aantal minuten dat je hebt ingesteld op geen enkele manier wordt beïnvloed door je vertragingsprofiel en direct wordt gedownload. Bovendien **negeert elke handmatige zoekopdracht** naar inhoud (niet-RSS-feedzoekopdrachten) de instellingen van het vertragingsprofiel.
{.is-warning}

#### Voorbeelden

- Voor elk voorbeeld wordt ervan uitgegaan dat de gebruiker het volgende kwaliteitsprofiel actief heeft: HDTV 720p en hoger zijn toegestaan, WebDL 720p is de kwaliteitsdrempel, WebDL 1080p is de hoogst gerangschikte kwaliteit.

##### Voorbeeld 1

- In dit eenvoudige voorbeeld is het profiel ingesteld met een vertraging van 120 minuten (twee uur) voor zowel Usenet als torrents.

- Om 23:00 uur wordt de eerste release voor een aflevering gedetecteerd door Sonarr en deze is geüpload om 22:50 uur, waarna de 120 minuten durende klok begint te lopen. Om 00:50 uur zal Sonarr alle releases evalueren die het in de afgelopen twee uur heeft gevonden en de beste downloaden, namelijk WebDL 720p.

- Om 03:00 uur wordt er een andere release gevonden, namelijk WebDL 720p die om 02:46 uur aan je indexer is toegevoegd. Er begint opnieuw een 120 minuten durende klok. Om 04:46 uur wordt de best beschikbare release gedownload. Aangezien de kwaliteitsdrempel nu is bereikt, kan de aflevering niet meer worden geüpgraded en stopt Sonarr met zoeken naar nieuwe releases.

- Op elk moment, als er een WebDL 1080p-release wordt gevonden, wordt deze direct gedownload omdat dit de hoogst gerangschikte kwaliteit is. Als er op dat moment een vertragingstimer actief is, wordt deze geannuleerd.

##### Voorbeeld 2

- Dit voorbeeld heeft verschillende timers voor Usenet en torrents. Stel een timer van 120 minuten in voor Usenet en een timer van 180 minuten voor BitTorrent.

- Om 23:00 uur wordt de eerste release voor een aflevering gedetecteerd door Sonarr en beide timers beginnen te lopen. De release is om 22:15 uur aan de indexer toegevoegd. Om 00:15 uur zal Sonarr alle releases evalueren en als er acceptabele Usenet-releases zijn, wordt de beste gedownload en eindigen beide timers. Zo niet, dan wacht Sonarr tot 00:15 uur en downloadt de beste release, ongeacht de bron.

##### Voorbeeld 3

- Een veelvoorkomend gebruik voor vertragingsprofielen is om de nadruk te leggen op één protocol boven het andere. Bijvoorbeeld, je wilt alleen een BitTorrent-release downloaden als er na een bepaalde tijd niets naar Usenet is geüpload.

- Je kunt een timer van 60 minuten instellen voor BitTorrent en een timer van 0 minuten voor Usenet.

- Als de eerste release die wordt gedetecteerd afkomstig is van Usenet, zal Sonarr deze direct downloaden.

- Als de eerste release afkomstig is van BitTorrent, zal Sonarr een timer van 60 minuten instellen. Als er tijdens die timer een kwalificerende Usenet-release wordt gedetecteerd, wordt de BitTorrent-release genegeerd en wordt de Usenet-release gedownload.

## Releaseprofielen

- Niet alle releases zijn gelijk, elke releasegroep heeft zijn eigen manier om hun materiaal te verpakken en te coderen. Hier kun je de gewenste releases selecteren.

> Je kunt regex (standaard hoofdlettergevoelig) gebruiken in de waarden `Moet bevatten`, `Mag niet bevatten` en `Voorkeurswoorden`. Regex moet zijn zoals `/regex-hier/i`
{.is-info}

- Naam - Selecteer een **UNIEKE** naam voor het releaseprofiel dat je maakt
- Profiel inschakelen - Schakel dit profiel in of uit
- Moet bevatten - De release moet ten minste een van deze termen bevatten (hoofdletterongevoelig)
- Mag niet bevatten - De release wordt afgewezen als deze een of meer van deze termen bevat (hoofdletterongevoelig)
- Voorkeurswoorden - Hier kun je een bepaalde term selecteren en er een score aan geven.
  - Stel dat je op zoek bent naar releases met een specifieke combinatie van woorden. Stel dat je Sonarr wilt vertellen dat je Repacks of Propers verkiest boven reguliere releases. Hier plaats je het woord Repack in een van de velden en geef je het een waarde (bijvoorbeeld 100), maar je bent ook op zoek naar DTS-HD-audio, dus je plaatst dat er ook in en geeft het ook een score (bijvoorbeeld weer 100). Wanneer Sonarr alle releases uit de RSS-feed bekijkt en een release tegenkomt die zowel Repack als DTS-HD bevat, krijgt deze een score van 200. Dit is veel hoger dan alle andere releases die geen van beide woorden bevatten. Dit vertelt Sonarr dat dit een hogere score heeft en het zal het als eerste bestand selecteren om te downloaden.
- Voorkeurswoorden opnemen bij hernoemen - Bij gebruik van de tag {Preferred Words} in het benamingsschema
- Indexer - Specificeer op welke indexer het profiel van toepassing is.

> Dit is handig als je alleen specifieke releases wilt van een bepaalde indexer/tracker
{.is-info}

- Tags - Door dit releaseprofiel een tag te geven, kun je een bepaalde serie taggen om zich te houden aan de hier ingestelde regels. Als je dit veld leeg laat, zijn deze regels van toepassing op alle series

- [TRaSH onderhoudt een lijst met WEB-DL Releaseprofielen](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/)
- [TRaSH Anime-profielen](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx-Anime/)

# Kwaliteit

## Betekenissen van de kwaliteitstabel

- Kwaliteit - De naam van de kwaliteit in de scene (hardcoded)
- Titel - De naam van de kwaliteit in de GUI (configureerbaar)
- Megabytes per uur - Voor zichzelf sprekend
- Groottegrens - Voor zichzelf sprekend
- Min - Het minimum aantal megabytes per minuut (MB/min) dat een kwaliteit kan hebben.
- Max - Het maximum aantal megabytes per minuut (MB/min) dat een kwaliteit kan hebben.

## Gedefinieerde kwaliteiten

- On Usenet, Sonarr sends a request to your download client to download the NZB file.
- The download client then sends the NZB file to your Usenet provider to download the actual files.
- Once the files are downloaded, the download client notifies Sonarr that the download is complete.
- Sonarr then moves the files to the appropriate location and updates your media library.

## Torrents

- For torrents, Sonarr sends a request to your download client to download the torrent file or magnet link.
- The download client then starts downloading the files from the torrent swarm.
- Once the files are downloaded, the download client notifies Sonarr that the download is complete.
- Sonarr then moves the files to the appropriate location and updates your media library.

## Supported Download Clients

- A list of supported download clients is located at the [More Info (Supported)](/sonarr/supported#download-clients) page.

### Download Client Settings

- Once you've clicked the <kb>+</kb> button to add a new download client you will be presented with a new window with many different options.
- There are two sections here: Usenet and Torrents. Based upon what type of download client you will be using you will want to select the appropriate section.

### Usenet Download Client Configuration

- SABnzbd - This is a popular Usenet download client that works well with Sonarr. You will need to provide the URL of your SABnzbd server along with your API key.
- NZBGet - Another popular Usenet download client that integrates well with Sonarr. You will need to provide the URL of your NZBGet server along with your username and password.
- Newshosting - This is a Usenet provider that also offers a built-in download client. You will need to provide your Newshosting username and password.
- NewsDemon - Another Usenet provider with a built-in download client. You will need to provide your NewsDemon username and password.
- Custom Script - If you are using a different Usenet download client, you can create a custom script to communicate with Sonarr. You will need to provide the path to your script and any additional parameters.

### Torrent Download Client Configuration

- qBittorrent - This is a popular torrent download client that works well with Sonarr. You will need to provide the URL of your qBittorrent server along with your username and password.
- Deluge - Another popular torrent download client that integrates well with Sonarr. You will need to provide the URL of your Deluge server along with your username and password.
- Transmission - This is a lightweight torrent download client that can be used with Sonarr. You will need to provide the URL of your Transmission server along with your username and password.
- rTorrent - A command-line torrent download client that can be used with Sonarr. You will need to provide the path to your rTorrent installation.
- Custom Script - If you are using a different torrent download client, you can create a custom script to communicate with Sonarr. You will need to provide the path to your script and any additional parameters.

## Options

- Completed Download Handling - When enabled, Sonarr will automatically import downloaded files into your media library. You can choose to either move or copy the files, and Sonarr can also rename the files based on your preferences.
- Remove - When enabled, Sonarr will remove the downloaded files from your download client after importing them into your media library.
- Failed Download Handling - When enabled, Sonarr will handle failed downloads by either retrying the download or marking it as failed. You can choose the number of retries and the interval between retries.
- Redownload Failed - When enabled, Sonarr will redownload failed episodes if they meet certain criteria, such as being within a certain time frame or having a certain number of seeders.
- Use Hardlinks instead of Copy - When enabled, Sonarr will use hardlinks instead of copying files when importing them into your media library. This can save disk space, but it requires that your media library and download client are on the same filesystem.
- Drone Factory - When enabled, Sonarr will monitor a folder for new files and automatically import them into your media library. This can be useful if you have a separate program that downloads files and places them in a specific folder.
- Import Extra Files - When enabled, Sonarr will import extra files that are included with the episode, such as subtitles or artwork.
- Analyze Video Files - When enabled, Sonarr will analyze video files to determine their quality and other metadata. This can be useful for filtering out low-quality releases.
- Use Hardlinks instead of Copy - When enabled, Sonarr will use hardlinks instead of copying files when importing them into your media library. This can save disk space, but it requires that your media library and download client are on the same filesystem.
- Enable SSL/TLS - When enabled, Sonarr will use SSL/TLS to communicate with your download client. This is recommended for security reasons.
- SSL/TLS Certificate Validation - When enabled, Sonarr will validate the SSL/TLS certificate of your download client. This is recommended for security reasons.
- SSL/TLS Certificate Path - If you have a custom SSL/TLS certificate for your download client, you can provide the path to the certificate file here.
- Use Proxy - When enabled, Sonarr will use a proxy server to communicate with your download client. You will need to provide the proxy server address and port.
- Proxy Type - The type of proxy server to use, such as HTTP or SOCKS5.
- Proxy Username - If your proxy server requires authentication, you can provide the username here.
- Proxy Password - If your proxy server requires authentication, you can provide the password here.

- Sonarr zal een downloadverzoek naar uw client sturen en het associëren met een label of categorie die u hebt geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Sonarr zal de actieve downloads van uw downloadclients controleren die deze categorie gebruiken. Dit wordt gedaan via de API van uw downloadclient.
- Wanneer de download is voltooid, zal Sonarr de uiteindelijke bestandslocatie weten zoals gerapporteerd door uw downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang het maar ergens apart van uw mediabibliotheek staat en toegankelijk is voor Sonarr.
- Sonarr zal die voltooide bestandslocatie scannen op bestanden die Sonarr kan gebruiken. Het zal de bestandsnaam analyseren om deze te matchen met de gevraagde media. Als dat lukt, zal het bestand worden hernoemd volgens uw specificaties en verplaatst naar de opgegeven mediabibliotheek.
- Atomic Moves (directe verplaatsingen) zijn standaard ingeschakeld. Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediabibliotheek. Als de atomic move mislukt of uw configuratie geen hardlinks en atomic moves ondersteunt, zal Sonarr overschakelen naar het kopiëren van het bestand en het vervolgens verwijderen van de bron, wat veel IO vereist.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Sonarr, worden overgebleven bestanden van de download naar de prullenbak of recycling gestuurd via een verzoek aan uw client om de release te verwijderen.

## BitTorrent

- Sonarr zal een downloadverzoek naar uw client sturen en het associëren met een label of categorie die u hebt geconfigureerd in de instellingen van de downloadclient.
  - Voorbeelden: films, tv, series, muziek, enz.
- Sonarr zal de actieve downloads van uw downloadclients controleren die deze categorie gebruiken. Dit wordt gedaan via de API van uw downloadclient.
- Voltooide bestanden blijven op hun oorspronkelijke locatie staan om het mogelijk te maken het bestand te seeden (de verhouding of tijd kan worden aangepast in de downloadclient of vanuit Sonarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar uw mediabibliotheek, zal Sonarr het bestand hardlinken als dit wordt ondersteund door uw configuratie, anders wordt het gekopieerd als hardlinks niet worden ondersteund.
- Hardlinks zijn standaard ingeschakeld. [Een hardlink gebruikt geen extra schijfruimte.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediabibliotheek. Als het maken van een hardlink mislukt of uw configuratie geen hardlinks ondersteunt, zal Sonarr het bestand kopiëren.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Sonarr, zal Sonarr de torrent verwijderen uit uw client en de client vragen om de torrentgegevens te verwijderen, maar alleen als de client meldt dat het seeden is voltooid en de torrent is gestopt (gepauzeerd na voltooiing).

## Downloadclients

Klik op `Instellingen` => `Downloadclients` en klik vervolgens op het <kb>+</kb> om een nieuwe downloadclient toe te voegen. Uw downloadclient moet al geconfigureerd en actief zijn.

### Ondersteunde downloadclients

- Een lijst met ondersteunde downloadclients is te vinden op de [Meer informatie Ondersteund](/sonarr/supported#download-clients) pagina

Selecteer de downloadclient die u wilt toevoegen en er verschijnt een pop-upvenster om de verbindingsgegevens in te voeren. Deze gegevens zijn vergelijkbaar voor de meeste clients. Sommige vragen om een gebruikersnaam of wachtwoord, andere vragen of nieuwe downloads in een gepauzeerde/starttoestand moeten worden toegevoegd, enz.

### Usenet-clientinstellingen

- Naam - De naam van de downloadclient binnen Sonarr
- Inschakelen - Deze downloadclient inschakelen
- Host - De URL van uw downloadclient
- Poort - De poort van uw downloadclient; dit is meestal de webgui-poort
- Gebruik SSL - Gebruik een beveiligde verbinding met uw downloadclient. Let op deze veelvoorkomende fout.
- (Geavanceerde optie) URL-basis - Voeg een voorvoegsel toe aan de URL; dit is vaak nodig voor omgekeerde proxies.
- API-sleutel - de API-sleutel om te authenticeren bij uw client
- Gebruikersnaam - de gebruikersnaam om te authenticeren bij uw client (meestal niet nodig)
- Wachtwoord - het wachtwoord om te authenticeren bij uw client (meestal niet nodig)
- Categorie - de categorie binnen uw downloadclient die \*Arr zal gebruiken. Om te voorkomen dat niet-gerelateerde downloads worden weergegeven in Activiteit, wordt sterk aanbevolen om een categorie in te stellen.
- Recente prioriteit - downloadclientprioriteit voor recent uitgebrachte media
- Oudere prioriteit - downloadclientprioriteit voor media die niet recent is uitgebracht
- (Geavanceerde optie) Clientprioriteit - Prioriteit van de downloadclient. Round-Robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) met dezelfde prioriteit. 1 is de hoogste prioriteit en 50 is de laagste prioriteit
- Voltooide downloadverwerking
  - Verwijderen (Per clientinstelling) - Voltooide downloads verwijderen wanneer deze zijn voltooid (usenet) of gestopt/voltooid (torrents). Zie [Voltooide downloadverwerking voor meer details](#voltooide-downloadverwerking)

### Torrent-clientinstellingen

- Naam - De naam van de downloadclient binnen Sonarr
- Inschakelen - Deze downloadclient inschakelen
- Host - De URL van uw downloadclient
- Poort - De poort van uw downloadclient
- Gebruik SSL - Gebruik een beveiligde verbinding met uw downloadclient. Let op deze veelvoorkomende fout.
- (Geavanceerde optie) URL-basis - Voeg een voorvoegsel toe aan de URL; dit is vaak nodig voor omgekeerde proxies.
- Gebruikersnaam - de gebruikersnaam om te authenticeren bij uw client
- Wachtwoord - het wachtwoord om te authenticeren bij uw client
- Categorie - de categorie binnen uw downloadclient die \*Arr zal gebruiken. Om te voorkomen dat niet-gerelateerde downloads worden weergegeven in Activiteit, wordt sterk aanbevolen om een categorie in te stellen.
- Post-importcategorie - de categorie om in te stellen nadat de release is gedownload en geïmporteerd. Houd er rekening mee dat dit de verwijdering van voltooide downloadverwerking verbreekt.
- Recente prioriteit - downloadclientprioriteit voor recent uitgebrachte media
- Oudere prioriteit - downloadclientprioriteit voor media die niet recent is uitgebracht
- Initiële status - Initiële status voor torrents (alleen Qbittorrent: geforceerd om alle seeddrempels te omzeilen)
- (Geavanceerde optie) Clientprioriteit - Prioriteit van de downloadclient. Round-Robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) met dezelfde prioriteit. 1 is de hoogste prioriteit en 50 is de laagste prioriteit
- Voltooide downloadverwerking
  - Verwijderen (Per clientinstelling) - Voltooide downloads verwijderen wanneer deze zijn voltooid (usenet) of gestopt/voltooid (torrents). Zie [Voltooide downloadverwerking voor meer details](#voltooide-downloadverwerking)
    - Voor torrents is het vereist dat uw downloadclient pauzeert wanneer de seeddoelen zijn bereikt. Het vereist ook dat de seeddoelen worden ondersteund door Sonarr volgens de onderstaande tabel. Torrents moeten ook in dezelfde categorie blijven.

### Compatibiliteit van het verwijderen van torrentdownloads door de torrentclient

- Sonarr kan alleen de seedverhouding/tijd instellen op clients die deze waarde kunnen instellen via hun API wanneer de torrent wordt toegevoegd. Seeddoelen kunnen wereldwijd worden ingesteld in de client zelf of per tracker in de instellingen van \*Arr voor elke indexer. Zie de onderstaande tabel voor de compatibiliteit van de client.

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

> ![Idle-limiet](https://img.shields.io/badge/Ondersteund-Idle%20limiet*-blauw) - Transmission heeft intern een controle op Idle Time, maar Sonarr vergelijkt dit met de seedtijd als de idle-limiet per torrent is ingesteld. Dit wordt gedaan als workaround voor de beperkingen van de Transmission API.{.is-info}

## Voltooide downloadverwerking

- Voltooide downloadverwerking is hoe Sonarr media importeert van uw downloadclient naar uw mappen voor series. Veelvoorkomende problemen hebben vaak te maken met verkeerde Docker-paden en/of andere Docker-machtigingsproblemen.

- (Geavanceerde globale instelling) Inschakelen - Voltooide downloads automatisch importeren van de downloadclient
- (Per clientinstelling) Verwijderen - Voltooide downloads verwijderen wanneer deze zijn voltooid (usenet) of gestopt/voltooid (torrents)
  - Voor torrents is het vereist dat uw downloadclient pauzeert wanneer de seeddoelen zijn bereikt. Het vereist ook dat de seeddoelen worden ondersteund door Sonarr volgens de bovenstaande tabel. Torrents moeten ook in dezelfde categorie blijven.

### Voltooide downloads verwijderen

- Sonarr zal een downloadverzoek naar uw client sturen en het associëren met een label of categorie die u hebt geconfigureerd in de instellingen van de downloadclient.
- Sonarr zal de actieve downloads van uw downloadclients controleren die deze categorie gebruiken. Dit wordt gedaan via de API van uw downloadclient.
- Wanneer de download is voltooid, zal Sonarr de uiteindelijke bestandslocatie weten zoals gerapporteerd door uw downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang het maar ergens apart van uw mediabibliotheek staat.
- Sonarr zal die voltooide bestandslocatie scannen op videobestanden. Het zal de bestandsnaam van de video analyseren om deze te matchen met een aflevering. Als dat lukt, zal het bestand worden hernoemd volgens uw specificaties en verplaatst naar de toegewezen bibliotheekmap.
- Overgebleven bestanden van de download worden naar de prullenbak of recycling gestuurd.

Als u downloadt met een BitTorrent-client, verloopt het proces iets anders:

- Voltooide bestanden blijven op hun oorspronkelijke locatie staan om het mogelijk te maken te seeden. Wanneer bestanden worden geïmporteerd naar uw toegewezen bibliotheekmap, zal Sonarr proberen het bestand te hardlinken of indien niet ondersteund, te kopiëren (dubbele ruimte te gebruiken).
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen, zal Sonarr de torrentclient vragen om het oorspronkelijke bestand en de torrent te verwijderen, maar dit gebeurt alleen als de client meldt dat het seeden is voltooid, de torrent in dezelfde categorie staat (d.w.z. geen gebruik van een post-importcategorie), het seeddoel dat is bereikt wordt ondersteund door Sonarr en de torrent is gepauzeerd (gestopt).

### Mislukte downloadverwerking

- Mislukte downloadverwerking is alleen compatibel met SABnzbd en NZBGet.
- Mislukte downloadverwerking is niet van toepassing op torrents en er zijn geen plannen om deze functionaliteit toe te voegen.

- Er zijn verschillende componenten die deel uitmaken van het proces van mislukte downloadverwerking:

- Controleer Downloader:
  - Wachtrij - Controleer de wachtrij van uw downloader op versleutelde releases die zijn gemarkeerd als mislukt vanwege een wachtwoord
  - Geschiedenis - Controleer de geschiedenis van uw downloader op mislukkingen (bijv. niet genoeg blokken om te repareren, of extractie mislukt)
- Wanneer Sonarr een mislukte download vindt, begint het met het verwerken ervan en doet het een paar dingen:
  - Voegt een mislukte gebeurtenis toe aan de geschiedenis van Sonarr
  - Verwijdert de mislukte download uit de downloadclient om ruimte vrij te maken en gedownloade bestanden te wissen (optioneel)
  - Begint te zoeken naar een vervangend bestand (optioneel)
  - Blocklisting (voorheen 'Blacklisting') maakt automatisch overslaan van nzbs mogelijk wanneer ze mislukken, dit betekent dat die nzb nooit meer automatisch door Sonarr wordt gedownload (u kunt de download nog steeds afdwingen via een handmatige zoekopdracht).
  - Er zijn 2 geavanceerde opties (op de pagina 'Downloadclient' instellingen) die het gedrag van mislukte downloadverwerking in Sonarr bepalen, op dit moment staan ze allemaal standaard aan.

- Opnieuw downloaden - Bepaalt of Sonarr al dan niet zal zoeken naar hetzelfde bestand na een mislukking
- (Geavanceerde optie) Verwijderen - Of de download automatisch moet worden verwijderd uit de downloadclient wanneer de mislukking wordt gedetecteerd

## Externe pad-toewijzingen

- Externe pad-toewijzing fungeert als een eenvoudige zoekopdracht naar een extern pad en vervangt dit door een lokaal pad. Dit wordt voornamelijk gebruikt voor samengevoegde lokale/externe configuraties met behulp van mergerfs of vergelijkbaar, of wordt gebruikt wanneer de toepassing en de downloadclient zich niet op dezelfde server bevinden.
- Een externe pad-toewijzing wordt gebruikt wanneer uw downloadclient een pad rapporteert voor voltooide gegevens dat zich op een andere server bevindt of op een manier die \*Arr niet herkent.
- Over het algemeen is een externe pad-toewijzing alleen nodig als uw downloadclient op Linux staat terwijl \*Arr op Windows staat of vice versa. Een externe pad-toewijzing is ook mogelijk nodig bij het mixen van Docker- en native clients of bij het gebruik van een externe server.
- Een externe pad-toewijzing is een DOMME zoek/vervang (waarbij het de WAARDE VAN HET EXTERNE pad vindt en vervangt door de WAARDE VAN HET LOKALE pad voor de opgegeven Host).
- Als het foutbericht over een ongeldig pad de VERVANGENDE waarde niet bevat, werkt de pad-toewijzing niet zoals u verwacht. De gebruikelijke oplossing is om de toewijzing toe te voegen en te verwijderen.
- [Zie de tutorial van TRaSH voor aanvullende informatie over externe pad-toewijzingen](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Als zowel \*Arr als uw Downloadclient Docker-containers zijn, is een externe pad-toewijzing zelden nodig. Het wordt aanbevolen om [de Docker-gids](/docker-guide) te bekijken en/of [de tutorial van TRaSH](https://trash-guides.info/hardlinks) te volgen.{.is-info}

# Importlijsten

> Informatie over ondersteunde lijsttypen is te vinden op de [Meer informatie (Ondersteund)](/sonarr/supported#lists) pagina voor dit gedeelte
{.is-info}

## Lijsten

- Importlijsten zijn een onderdeel van Sonarr waarmee u een lijstmaker kunt volgen. Stel dat u een bepaalde lijstmaker volgt op Trakt/TMDb en hun ArrowVerse-collectiegedeelte echt leuk vindt en elke show op hun lijst wilt bekijken. U kijkt in uw Sonarr en realiseert zich dat u die series niet hebt. In plaats van één voor één te zoeken en die items toe te voegen en vervolgens uw indexers te doorzoeken naar die series, kunt u dit allemaal tegelijk doen met een lijst. De lijsten kunnen worden ingesteld om alle series op die lijst van de curator te importeren, evenals automatisch een kwaliteitsprofiel toewijzen, automatisch toevoegen en automatisch bewaken van die series.

- LET OP: Als lijsten verkeerd worden gebruikt, zullen ze absoluut uw bibliotheek vernietigen met een hoop troep die u niet van plan bent te bekijken. Zorg er dus voor dat u weet wat u importeert voordat u opslaat. D.w.z. bekijk de lijst fysiek voordat u zelfs naar Sonarr gaat.

- Hier kunt u op de <kb>+</kb>-knop klikken om een nieuw pop-upvenster te openen
- In dit nieuwe venster krijgt u veel verschillende opties om uw lijst in te stellen vanuit veel verschillende lijstproviders. Zoals eerder vermeld, wees voorzichtig bij het maken van lijsten. Het wordt ten zeerste aanbevolen om niet op de Zoeken bij toevoegen-knop te klikken voordat u er absoluut zeker van bent dat de lijst die u selecteert/opzet de series toevoegt die u zoekt.
- Zodra u de lijstprovider hebt geselecteerd waarvan u wilt putten (zoals IMDb of Trakt), krijgt u een nieuw venster te zien.
De meeste instellingen van de lijsten zijn vrij duidelijk, sommige lijsten vereisen dat u zich authenticeert bij de provider, zoals Trakt (waarvoor u een account bij Trakt.tv moet hebben).

- Importeren van lijstuitsluiting - Hiermee kunt u uw lijst met series snoeien die u niet meer wilt zien. Een voorbeeld hiervan is als uw lijst toevallig een serie bevat die in een vreemde taal is en het is niet waarschijnlijk dat u deze film ooit in uw moedertaal zult vinden en deze niet met ondertitels wilt bekijken. U kunt een serie uitsluiten van toevoeging in de toekomst. In de sectie lijstuitsluiting kunt u deze echter weer aan de lijst toevoegen, zodat wanneer de lijst opnieuw wordt uitgevoerd, deze naar uw bibliotheek wordt gelezen.

# Verbinding maken

> Informatie over ondersteunde verbindingssoorten is te vinden op de [Meer informatie (Ondersteund)](/sonarr/supported#notifications) pagina voor deze sectie
{.is-info}

## Verbindingen

- Verbindingen zijn de manier waarop u wilt dat Sonarr communiceert met de buitenwereld.

- Door op de <kb>+</kb> knop te drukken, wordt u een nieuw venster getoond waarmee u veel verschillende eindpunten kunt configureren.

- Een lijst met ondersteunde meldingen en verbindingen is te vinden op de [Meer informatie (Ondersteund)](/sonarr/supported#notifications) pagina.

## Verbindingsacties

- Bij downloaden - Word op de hoogte gesteld wanneer afleveringen beschikbaar zijn om te downloaden en naar een downloadclient zijn verzonden.
- Bij importeren - {Vroeger bekend als Bij downloaden} Word op de hoogte gesteld wanneer afleveringen succesvol zijn geïmporteerd.
- Bij upgraden - Word op de hoogte gesteld wanneer afleveringen worden geüpgraded naar een betere kwaliteit.
- Bij hernoemen - Word op de hoogte gesteld wanneer afleveringen worden hernoemd.
- Bij verwijderen van serie - Word op de hoogte gesteld wanneer series worden verwijderd.
- Bij verwijderen van afleveringsbestand - Word op de hoogte gesteld wanneer afleveringsbestanden worden verwijderd.
- Bij verwijderen van afleveringsbestand voor upgrade - Word op de hoogte gesteld wanneer afleveringsbestanden worden verwijderd voor upgrades.
- Bij gezondheidsprobleem - Word op de hoogte gesteld van fouten bij de gezondheidscontrole.
  - Gezondheidswaarschuwingen opnemen - Word ook op de hoogte gesteld van gezondheidswaarschuwingen naast fouten.
- Bij bijwerken van applicatie - Word op de hoogte gesteld wanneer Sonarr wordt bijgewerkt naar een nieuwe versie.

# Metadata

## Metadata

> Informatie over ondersteunde metadata-consumenten is te vinden op de [Meer informatie (Ondersteund)](/sonarr/supported#metadata) pagina voor deze sectie
{.is-info}

- Hier kunt u het type metadata selecteren dat door uw mediaspeler wordt gebruikt.

- Kodi zal een van de meest gebruikte opties zijn als dat de software is die wordt gebruikt. Hiermee kan Sonarr een NFO-bestand maken en bijbehorende filmposters ophalen voor uw speler.

# Tags

- De tagsectie in Sonarr wordt gebruikt om verschillende aspecten van Sonarr met elkaar te verbinden.
- Tags zijn met name handig voor:
  - Vertragingprofielen
  - Releaseprofielen
  - Indexers
- Tags kunnen worden gebruikt om vertragingprofielen, releaseprofielen, indexers en series met elkaar te verbinden.
- Bijvoorbeeld:
  - U wilt dat een specifieke indexer alleen wordt gebruikt voor een specifieke serie. U zou een tag maken en de serie en indexer aan die tag toewijzen.
  - U wilt dat een specifiek releaseprofiel alleen een specifiek vertragingprofiel gebruikt. U zou een tag maken en het releaseprofiel en vertragingprofiel aan die tag toewijzen.

> Een serie zal zowel indexers gebruiken die overeenkomende tags hebben als indexers die geen tags hebben.
{.is-warning}

> Opmerking: Tags hebben geen invloed op "Moet bevatten", "Mag niet bevatten", "Voorkeurs" woorden of andere aspecten die hierboven niet worden genoemd.
{.is-info}

# Algemeen

## Host

- Bindadres - Geldig IPv4-adres of '*' voor alle interfaces
  - 0.0.0.0 of `*` - elk adres kan verbinding maken
  - 127.0.0.1 of localhost - alleen toepassingen op localhost kunnen verbinding maken
  - Elk ander IP (bijv. 1.2.3.4) - alleen dat IP (1.2.3.4) kan verbinding maken
- Poortnummer - Het poortnummer dat u wilt gebruiken om toegang te krijgen tot de webinterface van Sonarr

> Opmerking: Raak deze instelling niet aan als u Docker gebruikt.
{.is-warning}

- URL-basis - Voor ondersteuning van omgekeerde proxy, standaard leeg

> Opmerking: Als u een omgekeerde proxy gebruikt (bijvoorbeeld mydomain.com/sonarr), voert u '/sonarr' in voor URL-basis.
{.is-info}

- Instantienaam - Instantienaam in tabblad en voor Syslog-app-naam

> Als u meerdere instanties uitvoert, wordt de instantienaam toegevoegd aan de naam van het webbrowser-tabblad. {.is-info}

- SSL inschakelen - Als u SSL-certificaten heeft en de communicatie van en naar uw Sonarr wilt beveiligen, schakel dan deze optie in.

> Opmerking: Gebruik dit niet tenzij u weet wat u doet.
{.is-warning}

## Beveiliging

- Authenticatie - Hoe wilt u authenticeren om toegang te krijgen tot uw Sonarr-instantie
  - Geen - U heeft geen authenticatie nodig om toegang te krijgen tot uw Sonarr. Typisch als u de enige gebruiker van uw netwerk bent, niemand op uw netwerk hebt die toegang wil tot uw Sonarr of uw Sonarr niet blootgesteld is aan het web
  - Basis (Browser pop-up) - Deze optie toont een klein pop-upvenster wanneer u toegang krijgt tot uw Sonarr, waarmee u een gebruikersnaam en wachtwoord kunt invoeren
  - Formulieren (Aanmeldingspagina) - Deze optie heeft een vertrouwd uitziend aanmeldingsscherm, net als andere websites, waarmee u kunt inloggen op uw Sonarr
- API-sleutel - Hiermee kunnen andere programma's communiceren of Sonarr communiceren met andere programma's. Deze sleutel kan, als deze wordt gegeven aan de verkeerde persoon met toegang, allerlei dingen doen met uw bibliotheek. Daarom wordt de API-sleutel in de logboeken gecensureerd.
- Certificaatvalidatie - Wijzig hoe strikt HTTPS-certificaatvalidatie is
  - Ingeschakeld - Valideer alle HTTPS-certificaten (aanbevolen)
  - Uitgeschakeld voor lokale adressen - Valideer alle HTTPS-certificaten behalve die op localhost en het LAN
  - Uitgeschakeld - Valideer geen enkel HTTPS-certificaat

## Proxy

- Proxy - Met deze optie kunt u de informatie die Sonarr ophaalt en doorzoekt via een proxy laten lopen. Dit kan handig zijn als u zich in een land bevindt dat het downloaden van torrentbestanden niet toestaat.

- Proxy gebruiken - Inschakelen om een proxy te gebruiken
- Proxytype - Selecteer uw proxytype (HTTPS, Socks4 of Socks5)
- Hostnaam - Voer de hostnaam van uw proxy in (inclusief http/https of een ander protocol)
- Poort - Voer de poort van uw proxy in
- Gebruikersnaam - Voer uw proxygebruikersnaam in indien van toepassing
- Wachtwoord - Voer uw proxysleutelwoord in indien van toepassing
- Genegeerde adressen - Voer een door komma's gescheiden lijst in van adressen die de proxy moeten omzeilen
- Proxy omzeilen voor lokale adressen - Vink het vakje aan om de proxy te omzeilen voor lokale adressen. Lokale verzoeken worden geïdentificeerd door het ontbreken van een punt (.) in de URI, zoals <http://webserver/>, of door toegang tot de lokale server, inclusief <http://localhost>, <http://loopback> of <http://127.0.0.1>. Wanneer dit niet is aangevinkt, worden alle internetverzoeken via de proxyserver gemaakt.

## Logboeken

- Logboekniveau - Waarschijnlijk een van de meest nuttige probleemoplossingstools
  - Info - Dit is de meest basale manier waarop Sonarr informatie verzamelt. Dit bevat een zeer minimale hoeveelheid informatie in de logboeken. Dit logbestand bevat fatale, fout-, waarschuwings- en infovermeldingen.
  - Debug - Debug bevat alle informatie die Info bevat, plus meer informatie die nuttig kan zijn. Dit logbestand bevat fatale, fout-, waarschuwings-, info- en debugvermeldingen.
  - Trace - Het meest geavanceerde en gedetailleerde logboek van Sonarr. Trace bevat alle informatie die is verzameld door Info en Debug en meer. Dit is het meest voorkomende type logboek dat wordt gevraagd bij het oplossen van problemen op Discord of Reddit. Als u hulp nodig heeft, selecteer dan uw logboek op Trace en voer de taak opnieuw uit die u problemen gaf om het logboek vast te leggen. Dit logbestand bevat fatale, fout-, waarschuwings-, info-, debug- en tracevermeldingen.

## Analyse

- Analyse - Stuur anonieme gebruiks- en foutinformatie naar de servers van Sonarr (SkyHook). Dit omvat informatie over uw browser, welke Sonarr WebUI-pagina's u gebruikt, foutenrapportage, evenals OS- en runtimeversie. We zullen deze informatie gebruiken om functies en bugfixes te prioriteren.

## Updates

- (Geavanceerde optie) Branch - Dit is de branch van Sonarr waarop u draait.
  - [Zie deze FAQ-invoer voor meer informatie](/sonarr/faq#how-do-i-update-sonarr)
- Automatisch - Updates automatisch downloaden en installeren. U kunt nog steeds installeren via Systeem: Updates. Opmerking: Windows-gebruikers worden altijd automatisch bijgewerkt.
- Mechanisme - Gebruik de ingebouwde updater van Sonarr of een script
  - Ingebouwd - Gebruik de eigen updater van Sonarr
  - Script - Laat Sonarr het update-script uitvoeren
  - Docker - Werk Sonarr niet bij vanuit de Docker, maar haal in plaats daarvan een gloednieuwe image op met de nieuwe update
  - Apt - Ingesteld door het Debian/Ubuntu-pakket wanneer bijwerken uitsluitend via Apt wordt beheerd
- Script - Alleen zichtbaar wanneer Mechanisme is ingesteld op Script - Pad naar update-script
- Updateproces - Sonarr zal het updatebestand downloaden, de integriteit ervan controleren en het naar een tijdelijke locatie extraheren en de gekozen methode aanroepen. Het updateproces wordt uitgevoerd onder dezelfde gebruiker als waar Sonarr onder wordt uitgevoerd, het heeft toestemming nodig om de Sonarr-bestanden bij te werken en Sonarr te stoppen/starten.
- Ingebouwd - De ingebouwde methode zal Sonarr-bestanden en -instellingen back-uppen, Sonarr stoppen, de installatie bijwerken en Sonarr starten. Als uw systeem het stoppen van Sonarr niet aankan en automatisch probeert te herstarten, is het misschien beter om in plaats daarvan een script te gebruiken. Bij een mislukking wordt de vorige versie van Sonarr opnieuw gestart.
- Script - Het script moet hetzelfde behandelen als de ingebouwde updater. Als u services wilt stoppen en starten (upstart/launchd/etc), moet u dat hier doen.

## Back-ups

- Het back-upgedeelte stelt u in staat om Sonarr te vertellen hoe u back-ups wilt beheren.

- Map - Hiermee kunt u de back-uplocatie selecteren. In Docker bent u beperkt tot wat u de container toestaat te zien. Padnamen zijn relatief ten opzichte van de appdata-map; indien nodig kunt u een absoluut pad instellen om buiten de appdata-map een back-up te maken.
- Interval - Hoe vaak wilt u dat Sonarr een back-up maakt
- Behoud - Hoe lang wilt u dat Sonarr elke back-up bewaart. Na het maken van een nieuwe back-up wordt de oudste back-up verwijderd.

# UI

## Kalender

- Eerste dag van de week - Hier kunt u selecteren wat volgens u de eerste dag van de week moet zijn.
- Kolomkop van de week - Hier kunt u de kop voor de kolommen selecteren

## Datums

- Korte datumnotatie - Hoe wilt u dat Sonarr korte datums weergeeft?
- Lange datumnotatie - Hoe wilt u dat Sonarr lange datums weergeeft?
- Tijdnotatie - Wilt u een 12-uurs of 24-uurs notatie?
- Relatieve datums weergeven - Wilt u dat Sonarr relatieve (Vandaag/Gisteren/etc) of absolute datums weergeeft?

## Stijl

- Kleurenblindmodus inschakelen - Gewijzigde stijl om kleurenblinde gebruikers in staat te stellen kleurgecodeerde informatie beter te onderscheiden