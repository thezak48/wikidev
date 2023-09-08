---
title: Radarr-instellingen
description: Beschrijving van de instellingenmenu's van Radarr
published: true
date: 2023-08-27T22:02:11.780Z
tags: radarr, needs-love, instellingen
editor: markdown
dateCreated: 2021-05-29T15:57:25.304Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Menu-opties](#menu-opties)
- [Mediabeheer](#mediabeheer)
  - [Suggesties voor gemeenschappelijke benaming](#suggesties-voor-gemeenschappelijke-benaming)
  - [Filmbenaming](#filmbenaming)
    - [Standaard filmformaat](#standaard-filmformaat)
    - [Filmbenaming](#filmbenaming-1)
    - [Film-ID's](#film-ids)
    - [Kwaliteit](#kwaliteit)
    - [Mediainformatie](#mediainformatie)
    - [Releasegroep](#releasegroep)
    - [Editie](#editie)
    - [Aangepaste formaten (benaming)](#aangepaste-formaten-benaming)
    - [Origineel](#origineel)
  - [Filmmapformaat](#filmmapformaat)
    - [Filmbenaming](#filmbenaming-2)
    - [Film-ID](#film-id)
  - [Mappen](#mappen)
  - [Importeren](#importeren)
  - [Bestandsbeheer](#bestandsbeheer)
  - [Machtigingen](#machtigingen)
  - [Hoofdmappen](#hoofdmappen)
- [Profielen](#profielen)
  - [Kwaliteitsprofielen](#kwaliteitsprofielen)
  - [Vertragingsprofielen](#vertragingsprofielen)
    - [Gebruik](#gebruik)
    - [Hoe vertragingsprofielen werken](#hoe-vertragingsprofielen-werken)
      - [Voorbeelden](#voorbeelden)
        - [Voorbeeld 1](#voorbeeld-1)
        - [Voorbeeld 2](#voorbeeld-2)
        - [Voorbeeld 3](#voorbeeld-3)
- [Kwaliteit](#kwaliteit-1)
  - [Betekenissen van de kwaliteitstabel](#betekenissen-van-de-kwaliteitstabel)
  - [Gedefinieerde kwaliteiten](#gedefinieerde-kwaliteiten)
- [Aangepaste formaten](#aangepaste-formaten)
  - [Voorwaarden voor aangepaste formaten](#voorwaarden-voor-aangepaste-formaten)
    - [Modifiers](#modifiers)
    - [Voorwaarden](#voorwaarden)
    - [Profielinstellingen en rangschikking](#profielinstellingen-en-rangschikking)
      - [Aangepaste formaten importeren/exporteren](#aangepaste-formaten-importerenexporteren)
      - [Aangepaste formaten importeren/bestaande aangepaste formaten bijwerken](#aangepaste-formaten-importerenbestaande-aangepaste-formaten-bijwerken)
    - [Verzameling van aangepaste formaten](#verzameling-van-aangepaste-formaten)
- [Indexers](#indexers)
  - [Ondersteunde indexers](#ondersteunde-indexers)
    - [Indexerinstellingen](#indexerinstellingen)
    - [Usenet-indexerconfiguratie](#usenet-indexerconfiguratie)
    - [Torrent-trackerconfiguratie](#torrent-trackerconfiguratie)
      - [Indexerflags](#indexerflags)
  - [Opties](#opties)
  - [Beperkingen](#beperkingen)
- [Downloadclients](#downloadclients)
  - [Overzicht](#overzicht)
  - [Processen van downloadclients](#processen-van-downloadclients)
    - [Usenetproces](#usenetproces)
    - [Torrentproces](#torrentproces)
  - [Downloadclients](#downloadclients-1)
    - [Ondersteunde downloadclients](#ondersteunde-downloadclients)
    - [Usenet-clientinstellingen](#usenet-clientinstellingen)
    - [Torrent-clientinstellingen](#torrent-clientinstellingen)
    - [Compatibiliteit van verwijderen van downloads door torrentclient](#compatibiliteit-van-verwijderen-van-downloads-door-torrentclient)
  - [Afhandeling van voltooide downloads](#afhandeling-van-voltooide-downloads)
    - [Voltooide downloads verwijderen](#voltooide-downloads-verwijderen)
    - [Afhandeling van mislukte downloads](#afhandeling-van-mislukte-downloads)
  - [Mappen voor externe paden](#mappen-voor-externe-paden)
- [Importlijsten](#importlijsten)
  - [Lijsten](#lijsten)
  - [Lijstopties](#lijstopties)
  - [Uitsluitingen van lijsten](#uitsluitingen-van-lijsten)
- [Verbinding maken](#verbinding-maken)
  - [Verbindingen](#verbindingen)
  - [Verbindingsactiveringen](#verbindingsactiveringen)
- [Metadata](#metadata)
  - [Opties](#opties-1)
  - [Metadata-consumenten](#metadata-consumenten)
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
  - [Films](#films)
  - [Datums](#datums)
  - [Stijl](#stijl)
  - [Taal](#taal)

Deze pagina behandelt alle beschikbare instellingen in Radarr en hoe ze werken. Dit is niet bedoeld als een uitgebreide "hoe stel ik Radarr in". Als je dat wilt, gebruik dan in plaats daarvan de [Quick Start](/radarr/quick-start-guide) pagina.

# Menu-opties

Om naar de instellingenpagina te gaan, kies je Instellingen in de zijbalk. De volgende submenu-opties zijn beschikbaar:

![settings_1_menu.png](/assets/radarr/settings_1_menu.png)

Let ook op dat voor elke individuele instellingenpagina enkele opties bovenaan het menu staan:

![settings_2_topmenu.png](/assets/radarr/settings_2_topmenu.png)

- Verbergen/tonen van geavanceerde opties is belangrijk voor items die hieronder zijn gemarkeerd als `(Geavanceerde optie)`, anders worden ze niet weergegeven. Deze menu-items worden weergegeven in het oranje op de schermafbeeldingen.

- Je moet je wijzigingen opslaan voordat je het scherm verlaat. Dit doe je door op het schijficoon te klikken. Als je geen wijzigingen hebt aangebracht, wordt "Geen wijzigingen" weergegeven en is het grijs, zoals hierboven getoond.

# Mediabeheer

> Sommige van deze instellingen zijn alleen zichtbaar via `Toon geavanceerde instellingen`, dat zich bevindt in de bovenste balk onder de zoekbalk{.is-info}

## Suggesties voor gemeenschappelijke benaming

> Hieronder staan enkele suggesties voor gemeenschappelijke benaming van [TRaSH's Gidsen](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/){.is-info}

### Filmbestanden

- Radarr v4.2.2.6489 of nieuwer

`{Film SchoneTitel} {(Jaar van uitgave)} {imdb-{ImdbId}} {editie-{Editie Tags}} {[Aangepaste formaten]}{[Kwaliteit Volledig]}{[Mediainfo 3D]}{[Mediainfo VideoDynamischBereikType]}{[Mediainfo AudioCodec}{ Mediainfo AudioKanalen}]{MediaInfo AudioTalen}[{Mediainfo VideoCodec}]{-Releasegroep}`

- Oudere versies van Radarr

`{Film SchoneTitel} {(Jaar van uitgave)} {Editie Tags} [imdb-{ImdbId}]{[Aangepaste formaten]}{[Kwaliteit Volledig]}{[Mediainfo 3D]}{[Mediainfo VideoDynamischBereikType]}{[Mediainfo AudioCodec}{ Mediainfo AudioKanalen}][{Mediainfo VideoCodec}]{-Releasegroep}`

### Filmmappen

`{Film SchoneTitel} ({Jaar van uitgave})`

## Filmbenaming

- Filmpjes hernoemen - Als dit niet is aangevinkt, gebruikt Radarr de bestaande naam als hernoemen is uitgeschakeld
  - Als het niet is aangevinkt:
    - Importeren door downloadclient
      - De titel van de release van de downloadclient wordt gebruikt
    - Handmatig (ad-hoc) importeren: Oorspronkelijke bestandsnaam
- Vervang ongeldige tekens - Als dit niet is aangevinkt, verwijdert Radarr ze in plaats daarvan.

  - De tekens zijn: `:` `\` `/` `>` `<` `?` `*` `|` `"`
- Vervanging van dubbele punt (`:`) - Deze instelling bepaalt hoe Radarr dubbele punten in het filmbestand behandelt. Dit is alleen beschikbaar wanneer Vervang ongeldige tekens is ingeschakeld.
  - Verwijderen - Voor de hand liggend
    - Voorbeeld: Film,De.mkv => FilmDe.mkv
  - Vervangen door streepje - Verwijdert de dubbele punt en voegt een streepje toe op die plaats
    - Voorbeeld: Film,De.mkv => Film-De.mkv
  - Vervangen door spatie - Verwijdert de dubbele punt en voegt een spatie toe op die plaats
    - Voorbeeld: Film,De.mkv => Film De.mkv
  - Vervangen door spatie streepje spatie - voor de hand liggend
    - Voorbeeld: Film,De.mkv => Film - De.mkv

### Standaard filmformaat

- Hier selecteer je de benaming voor je films

- Dropdownbox (rechterbovenhoek)
  - Linkervak - Spatiebehandeling
    Spatie ( ) - Gebruik spaties in de benaming (standaard)
    Punt (.) - Gebruik punten in plaats van spaties in de benaming
    Onderstrepingsteken (_) - Gebruik onderstrepingstekens in plaats van spaties in de benaming
    Streepje (-) - Gebruik streepjes in plaats van spaties in de benaming
  - Rechtervak - Hoofdletterbehandeling
    Standaardhoofdletters - Maak de titel hoofdletters en kleine letters (~camel-case) (standaard)
    Hoofdletters - Maak de titel volledig in hoofdletters
    Kleine letters - Maak de titel volledig in kleine letters

### Filmbenaming

- `{Film Titel}` = De titel van de film!
- `{Film Titel:DE}` = Titel van de film
- `{Film SchoneTitel}` = De titel van de film!
- `{Film TitelThe}` = Titel van de film!, De
- `{Film OrigineleTitel}` = Τίτλος ταινίας
- `{Film SchoneOrigineleTitel}` = Τίτλος ταινίας
- `{Film TitelEersteKarakter}` = S
- `{Film Collectie}` = De filmcollectie
- `{Film Certificering}` = R
- `{Jaar van uitgave}` = 2009

`SchoneTitel` [doet het volgende](https://github.com/Radarr/Radarr/blob/5948f564827eabb7afc1e89bf4a5987e3c71dc74/src/NzbDrone.Core/Organizer/FileNameBuilder.cs#L207):

- Vervang `&` door `and`
- Vervang `/` en `\` door ` `
- Verwijder `,`,`<`,`>`,`/`,`\`,`;`,`:`,`'`,`|`, `~`,`!`,`?`,`@`,`$`,`%`,`^`,`*`,`-`,`_`,`=` zoals aangegeven in de volgende regex:

```regex
(?<=\s)(,|<|>|\/|\\|;|:|'|""|\||`|~|!|\?|@|$|%|^|\*|-|_|=){1}(?=\s)|('|:|\?|,)(?=(?:(?:s|m)\s)|\s|$)|(\(|\)|\[|\]|\{|\})
```

### Film-ID's

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

> Imdb-tags die worden gebruikt in het Plex-benaming formaat worden conditioneel verborgen wanneer de waarde leeg is `{imdb-{ImdbId}}` {.is-info}

### Kwaliteit

- `{Kwaliteit Volledig}` = HDTV 720p Juist
- `{Kwaliteit Titel}` = HDTV 720p

### Mediainformatie

- `{Mediainfo Eenvoudig}` = x264 DTS
- `{Mediainfo Volledig}` = x264 DTS \[EN+DE\]
- `{Mediainfo AudioCodec}` = DTS
- `{Mediainfo AudioKanalen}` = 5.1
- `{Mediainfo AudioTalen}` = \[EN+DE\]
- `{Mediainfo OndertitelTalen}` = \[EN\]
- `{Mediainfo VideoCodec}` = x264
- `{Mediainfo VideoBitdiepte}` = 8
- `{Mediainfo VideoDynamischBereik}` = HDR
- `{Mediainfo VideoDynamischBereikType}` = DV HDR10

> `Mediainfo Volledig`, `AudioTalen` en `OndertitelTalen` ondersteunen momenteel geen `:EN+DE` achtervoegsel zoals toegestaan in Sonarr om de talen in de bestandsnaam te filteren. Er is een open [issue](https://github.com/Radarr/Radarr/issues/4710) over dit onderwerp.
~~`Mediainfo Volledig`, `AudioTalen` en `OndertitelTalen` ondersteunen een `:EN+DE` achtervoegsel waarmee je de talen kunt filteren die in de bestandsnaam worden opgenomen. Gebruik `-DE` om specifieke talen uit te sluiten. Het toevoegen van <kb>+</kb> (bijv.: `:EN+`) geeft `[EN]`,`[EN+--]` of `[--]` afhankelijk van de uitgesloten talen. Bijvoorbeeld - `{Mediainfo Volledig:EN+DE}`.~~
{.is-info}

> `Mediainfo VideoDynamischBereikType` geeft mogelijke waarden van: DV, DV HDR10, DV HLG, DV SDR, HDR10, HDR10Plus, HLG en PQ.
{.is-info}

### Releasegroep

- `{Releasegroep}` = Rls Grp

### Editie

- `{Editie Tags}` = IMAX

> Vanaf v4.2.2.6489 worden Editie Tags die in Radarr worden gebruikt volgens de benaming van Plex `{editie-{Editie Tags}}` conditioneel verborgen zoals `{-Groep}` doet wanneer de waarde van Editie Tags leeg is
{.is-info}

### Aangepaste formaten (benaming)

- `{Aangepaste formaten}` = Surround Sound x264

> Aangepaste formaten zijn de letterlijke naam van het aangepaste formaat en moeten zijn ingeschakeld om te worden opgenomen in de hernoeming {.is-info}

### Origineel

- `{Originele Titel}` = Film.Titel.HDTV.x264-EVOLVE
- `{Originele Bestandsnaam}` = Film.titel.hdtv.x264-EVOLVE

> `Originele Titel` is de releasenaam en het wordt aanbevolen om deze te gebruiken.
{.is-info}

>`Originele Bestandsnaam` wordt niet aanbevolen. Het is de letterlijke originele bestandsnaam en kan versleuteld zijn `t1i0p3s7i8yuti`.{.is-warning}

## Filmmapformaat

Hier stel je de benaming in voor de map die de seizoensmappen of filmbestanden bevat. Klik op het `?`-teken om het dialoogvenster `Mapnaamtokens` te openen.

### Filmbenaming

- `{Film Titel}` = Filmtitel!
- `{Film Titel:DE}` = Bestandstitel
- `{Film SchoneTitel}` = Filmtitel
- `{Film TitelThe}` = Filmtitel, De
- `{Film OrigineleTitel}` = Τίτλος ταινίας
- `{Film TitelEersteKarakter}` = S
- `{Film Collectie}` = De filmcollectie
- `{Film Certificering}` = R
- `{Jaar van uitgave}` = 2009

### Film-ID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

## Mappen

- Lege mediamappen maken - Maak ontbrekende filmmappen tijdens het scannen van de schijf
- Lege mappen verwijderen - Verwijder lege filmmappen tijdens het scannen van de schijf en wanneer filmbestanden worden verwijderd

## Importeren

- Controle op vrije ruimte overslaan - Gebruik dit wanneer Radarr geen vrije ruimte kan detecteren vanuit je hoofdmap voor series
- Minimale vrije ruimte - Als dit wordt omgeschakeld, voorkomt dit importeren als er minder dan deze hoeveelheid schijfruimte beschikbaar is
- Gebruik harde koppelingen in plaats van kopiëren - Gebruik harde koppelingen bij het proberen te kopiëren van bestanden van torrents die nog steeds worden geüpload

  - Voor meer informatie hierover klik [hier](https://trash-guides.info/hardlinks)

> Zelden - maar mogelijk -, kunnen bestandsvergrendelingen voorkomen dat bestanden die worden geüpload, worden hernoemd. Je kunt het uploaden tijdelijk uitschakelen en de hernoemingsfunctie van Radarr gebruiken als oplossing.
{.is-warning}

- Extra bestanden importeren - Importeer bijpassende extra bestanden (ondertitels, nfo, enz.) na het importeren van een bestand

## Bestandsbeheer

- Unmonitor Verwijderde Films - Films die van de schijf zijn verwijderd, worden automatisch niet meer gemonitord in Radarr.
- Download Propers & Repacks - Of er automatisch moet worden geüpgraded naar Propers/Repacks. Gebruik `Niet Voorkeur` om te sorteren op voorkeurswoordenscore boven propers/repacks.

  - Voorkeur en Upgraden - Rangschik repacks en propers hoger dan niet-repacks en niet-propers. Behandel nieuwe repacks en propers als een upgrade naar huidige releases.
  - Niet Automatisch Upgraden - Rangschik repacks en propers hoger dan niet-repacks en niet-propers. Behandel nieuwe repacks en propers niet als een upgrade naar huidige releases.
  - Niet Voorkeur - Dit negeert effectief repacks en propers. Je moet eventuele voorkeur voor deze beheren met [Aangepaste Formaten](#aangepaste-formaten).

> \* `PROPER` - betekent dat er een probleem was met de vorige release. Downloads met de tag PROPER laten zien dat de problemen zijn opgelost in die release. Dit wordt gedaan door een groep die de oorspronkelijke release niet heeft uitgebracht.
> \* `REPACK` - betekent dat er een probleem was met de vorige release en dat dit is gecorrigeerd door de oorspronkelijke groep. Downloads met de tag REPACK laten zien dat de problemen zijn opgelost in die release. Dit wordt gedaan door een groep die de oorspronkelijke release heeft uitgebracht.
{.is-info}

> [Gebruik aangepaste formaten voor automatische upgrades naar propers/repacks](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)
{.is-info}

- Video-bestanden analyseren - Bestandsinformatie zoals resolutie, looptijd en codec-informatie uit bestanden halen. Hiervoor moet Radarr delen van het bestand lezen, wat kan leiden tot hoge schijf- of netwerkactiviteit tijdens scans.
- Filmmap opnieuw scannen na vernieuwen
  - Altijd - Dit zal filmmappen opnieuw scannen op basis van de takenplanning. Dit wordt aanbevolen voor de meeste gevallen, inclusief als je Bazarr gebruikt.
  - Na handmatige vernieuwing - Je moet de schijf handmatig opnieuw scannen. Dit wordt aanbevolen voor gebruikers van cloudopslag.
  - Nooit - Zoals de naam al zegt, filmmappen nooit opnieuw scannen. Dit wordt niet aanbevolen.
- Bestandsdatum wijzigen - Bestandsdatum wijzigen bij importeren/opnieuw scannen
  - Geen - Radarr wijzigt de datum niet die wordt weergegeven in je bestandsbrowser
  - Releasedatum in bioscoop - De datum waarop de film in de bioscoop werd uitgebracht.
  - Fysieke releasedatum - De datum waarop de film op schijf (fysiek) of op het web werd uitgebracht.
- Prullenbak - Filmbestanden worden hierheen verplaatst wanneer ze worden verwijderd in plaats van permanent te worden verwijderd
- Prullenbak opruimen - Dit is hoe oud een bepaald bestand kan zijn voordat het permanent wordt verwijderd

> Bestanden in de prullenbak die ouder zijn dan het geselecteerde aantal dagen worden automatisch opgeruimd {.is-warning}

## Rechten

- Rechten instellen - Moet `chmod` worden uitgevoerd wanneer bestanden worden geïmporteerd/hernoemd?
  - chmod-map - Octaal, toegepast tijdens importeren/hernoemen op mediamappen en -bestanden (zonder uitvoerbare bits)

> De vervolgkeuzelijst bevat een vooraf ingestelde lijst met veelgebruikte rechten die kunnen worden gebruikt. Je kunt echter ook handmatig een octaal voor de map invoeren als je dat wilt.
{.is-info}

> Dit werkt alleen als de gebruiker die `Radarr` uitvoert de eigenaar van het bestand is. Het is beter om ervoor te zorgen dat de downloadclient de rechten correct instelt.{.is-warning}

- chown-groep - Groepsnaam of GID. Gebruik GID voor externe bestandssystemen

> Dit werkt alleen als de gebruiker die `Radarr` uitvoert de eigenaar van het bestand is. Het is beter om ervoor te zorgen dat de downloadclient de rechten correct instelt.{.is-warning}

## Hoofdmappen

- Pad - Dit toont het pad naar je mediatheek
- Vrije ruimte - Dit is de vrije ruimte die door het systeem aan Radarr wordt gerapporteerd
- Niet-toegewezen mappen - Dit zijn mappen die niet zijn gekoppeld aan een film

> Het `X`-teken aan het einde verwijdert dit hoofdpad
{.is-info}

- Hoofdmap toevoegen - Hiermee kun je een hoofdpad selecteren waar nieuwe geïmporteerde downloads in deze map kunnen worden geplaatst of waar Radarr bestaande media kan scannen.

> Gebruikers van niet-Windows:
> \* Als je een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
> \* Als je een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.
{.is-warning}

# Profielen

## Kwaliteitsprofielen

- Stel profielen in voor de kwaliteit van films die je wilt downloaden.

> Bij het selecteren van een bestaand profiel of het toevoegen van een extra profiel verschijnt er een nieuw venster{.is-info}

> Opmerking: de kwaliteit met een blauw vakje is de kwaliteit waarnaar alle media met dit profiel blijven upgraden.
{.is-info}

- Plus-pictogram (<kb>+</kb>) - Maak een nieuw kwaliteitsprofiel

- Naam - Selecteer een **UNIEKE** naam voor het kwaliteitsprofiel dat je maakt
- Upgrades toegestaan - Wanneer deze optie is aangevinkt en je Radarr vertelt om een `WEB 1080p` te downloaden omdat dit de eerste release van een specifieke film is, zal Radarr automatisch upgraden naar een betere kwaliteit ***als*** `Upgrade tot` die kwaliteit heeft geselecteerd
- Upgrade tot - Zodra deze kwaliteit is bereikt, zal Radarr geen films meer downloaden

> Opmerking: dit is alleen van toepassing als je `Bluray-1080p` hoger hebt dan `WEB 1080p` binnen de sectie `Kwaliteiten`
{.is-warning}

- Kwaliteiten - Kwaliteiten hoger in de lijst hebben meer voorkeur, zelfs als ze niet zijn aangevinkt. Kwaliteiten binnen dezelfde groep zijn gelijk. Alleen aangevinkte kwaliteiten zijn gewenst.
  - Groepen bewerken - Sommige kwaliteiten zijn gegroepeerd om de grootte van de lijst te verkleinen, evenals het groeperen van vergelijkbare releases. Een goed voorbeeld hiervan is `WebDL` en `WebRip`, omdat deze zeer vergelijkbaar zijn en meestal vergelijkbare bitrates hebben. Bij het bewerken van de groepen kun je de voorkeur binnen elke groep wijzigen. [Zie TRaSH's gids voor het samenvoegen van kwaliteiten](https://trash-guides.info/merge-quality)

  - [Zie Kwaliteiten](#kwaliteiten-gedefinieerd)

> Standaard zijn de kwaliteiten ingesteld van laagste (onderaan) naar hoogste (bovenaan)
{.is-info}

- Taal - Selecteer je voorkeurstaal

- Aangepast formaat - Radarr geeft elke release een score op basis van de som van scores voor overeenkomende aangepaste formaten. Als een nieuwe release de score zou verbeteren, bij dezelfde of betere kwaliteit, zal Radarr deze downloaden.
Zie [Aangepaste Formaten](#aangepaste-formaten) voor meer informatie.

## Vertragingprofielen

- Vertragingprofielen stellen je in staat om het aantal releases dat wordt gedownload voor een film te verminderen door een vertraging toe te voegen terwijl Radarr blijft zoeken naar releases die beter overeenkomen met je voorkeuren.
- Voorkeursprotocol - Dit kan `Usenet` of `Torrent` zijn, afhankelijk van welk downloadprotocol je verkiest
- Usenet-vertraging - Ingesteld op het aantal minuten dat je wilt wachten voordat de download begint
- Torrent-vertraging - Ingesteld op het aantal minuten dat je wilt wachten voordat de download begint
- Overslaan als hoogste kwaliteit - Vertraging overslaan wanneer een release de hoogst ingeschakelde kwaliteitsprofiel heeft met het voorkeursprotocol
- Tags - Door dit vertragingprofiel een tag te geven, kun je een bepaalde film taggen zodat deze wordt behandeld volgens de hier ingestelde regels.
- Sleutelpictogram - Hiermee kun je het vertragingprofiel bewerken
- Plus-pictogram (<kb>+</kb>) - Maak een nieuw vertragingprofiel

### Gebruik

Sommige media ontvangen in de uren na een release een half dozijn verschillende releases van verschillende kwaliteit, en zonder vertragingprofielen kan Radarr proberen ze allemaal te downloaden. Met vertragingprofielen kan Radarr worden geconfigureerd om de eerste paar uur van releases te negeren.

Vertragingprofielen zijn ook handig als je de nadruk wilt leggen op één protocol (Usenet of BitTorrent) ten opzichte van het andere. (Zie Voorbeeld 3)

### Hoe vertragingprofielen werken

De timer begint zodra Radarr detecteert dat er een release beschikbaar is voor een film. Deze release wordt weergegeven in je Wachtrij met een klokpictogram om aan te geven dat deze onder vertraging staat.

> De klok begint vanaf het moment van uploaden van de releases en niet vanaf het moment dat Radarr ze ziet.
{.is-info}

Tijdens de vertragingperiode zal Radarr eventuele nieuwe releases die beschikbaar komen, opmerken. Wanneer de vertragingstimer afloopt, zal Radarr de enkele release downloaden die het beste overeenkomt met je kwaliteitsvoorkeuren.

De timerperiode kan verschillend zijn voor Usenet en Torrents. Elk profiel kan worden geassocieerd met één of meer tags, zodat je kunt aanpassen welke shows welke profielen hebben. Een vertragingprofiel zonder tag wordt beschouwd als de standaard en is van toepassing op alle shows die geen specifieke tag hebben.

> Vertragingprofielen beginnen vanaf het tijdstip waarop de indexer meldt dat de release is geüpload. Dit betekent dat inhoud die ouder is dan het aantal minuten dat je hebt ingesteld, op geen enkele manier wordt beïnvloed door je vertragingprofiel en direct wordt gedownload. Bovendien worden **elke handmatige zoekopdrachten** naar inhoud (niet-RSS-feed-zoekopdrachten) genegeerd in de vertragingprofielinstellingen.
{.is-warning}

#### Voorbeelden

- Voor elk voorbeeld wordt ervan uitgegaan dat de gebruiker het volgende actieve kwaliteitsprofiel heeft: WebDL-720p en hoger zijn toegestaan, WebDL-1080p is de kwaliteitsgrens, BluRay1080p is de hoogst gerangschikte kwaliteit

##### Voorbeeld 1

- In dit eenvoudige voorbeeld is het profiel ingesteld met een vertraging van 120 minuten (twee uur) voor zowel Usenet als Torrent.

- Om 23:00 uur detecteert Radarr de eerste release voor een film en deze is geüpload om 22:50 uur, waarna de 120 minuten durende klok begint te lopen. Om 00:50 uur zal Radarr alle releases evalueren die het in de afgelopen twee uur heeft gevonden en de beste, WebDL 720p, downloaden.

- Om 03:00 uur wordt er een andere release gevonden, WebDL 720p, die om 02:46 uur aan je indexer is toegevoegd. Er begint opnieuw een 120 minuten durende klok. Om 04:46 uur wordt de best beschikbare release gedownload. Aangezien de kwaliteitsgrens nu is bereikt, kan de film niet meer worden geüpgraded en stopt Radarr met zoeken naar nieuwe releases.

- Op elk moment, als er een WebDL 1080p-release wordt gevonden, wordt deze direct gedownload omdat dit de hoogst gerangschikte kwaliteit is. Als er op dat moment een vertragingstimer actief is, wordt deze geannuleerd.

##### Voorbeeld 2

- Dit voorbeeld heeft verschillende timers voor Usenet en Torrents. Stel een timer van 120 minuten in voor Usenet en een timer van 180 minuten voor BitTorrent.

- Om 23:00 uur detecteert Radarr de eerste release voor een film en beide timers beginnen te lopen. De release is om 22:15 uur aan de indexer toegevoegd. Om 00:15 uur zal Radarr alle releases evalueren en als er acceptabele Usenet-releases zijn, wordt de beste gedownload en eindigen beide timers. Zo niet, dan wacht Radarr tot 00:15 uur en downloadt de beste release, ongeacht de bron.

##### Voorbeeld 3

- Een veelvoorkomend gebruik van vertragingprofielen is om de nadruk te leggen op één protocol ten opzichte van het andere. Bijvoorbeeld, je wilt alleen een BitTorrent-release downloaden als er na een bepaalde tijd niets naar Usenet is geüpload.

- Je kunt een timer van 60 minuten instellen voor BitTorrent en een timer van 0 minuten voor Usenet.

- Als de eerste release die wordt gedetecteerd afkomstig is van Usenet, zal Radarr deze direct downloaden.

- Als de eerste release afkomstig is van BitTorrent, stelt Radarr een timer van 60 minuten in. Als er tijdens die timer een kwalificerende Usenet-release wordt gedetecteerd, wordt de BitTorrent-release genegeerd en wordt de Usenet-release gedownload.

## Releaseprofielen

- Hier kun je wereldwijde beperkingen instellen op basis van een aantal parameters
- Klik op het <kb>+</kb> en er wordt een nieuw venster geopend
- Moet bevatten - Hiermee kun je Radarr vertellen dat als een release een bepaalde tekenreeks niet bevat, Radarr die release niet zal downloaden. Dit is standaard hoofdletterongevoelig en regex kan worden gebruikt.
- Mag niet bevatten - Hiermee kun je Radarr vertellen dat als een release een bepaalde tekenreeks bevat, Radarr die release niet zal downloaden. Dit is standaard hoofdletterongevoelig en regex kan worden gebruikt.
- Tags - Hier kun je deze instellingen toepassen op films met minimaal één van de gegeven [tag](#tags).

# Kwaliteit

## Betekenissen van de kwaliteitstabel

- Kwaliteit - De naam van de kwaliteit volgens de scene (hardcoded)
- Titel - De naam van de kwaliteit in de GUI (configureerbaar)
- Megabytes per minuut - Voor zichzelf sprekend
- Groottegrens - Voor zichzelf sprekend
- Min - Het minimum aantal megabytes per minuut (MB/min) dat een kwaliteit kan hebben.
- Voorkeur - Het gewenste aantal megabytes per minuut (MB/min) dat een kwaliteit kan hebben.
- Max - Het maximum aantal megabytes per minuut (MB/min) dat een kwaliteit kan hebben.

## Gedefinieerde kwaliteiten

- Onbekend - Zelfverklarend
- SDTV - Post-air rips van een analoge bron (meestal kabeltelevisie of OTA standaard definitie). De beeldkwaliteit is over het algemeen goed (voor de resolutie) en ze worden meestal gecodeerd in DivX/XviD of MP4.
- WEBDL-480p - WEB-DL (P2P) verwijst naar een bestand dat verliesloos is geript van een streamingdienst, zoals Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., of gedownload via een online distributiewebsite zoals iTunes. De kwaliteit is behoorlijk goed, omdat ze niet opnieuw worden gecodeerd. De video (H.264 of H.265) en audio (AC3/AAC) streams worden meestal geëxtraheerd uit iTunes of Amazon Video en opnieuw in een MKV-container geplaatst zonder verlies van kwaliteit. Een voordeel van deze releases is dat ze, net als BD/DVDRips, meestal geen netwerklogo's op het scherm hebben. Deze zijn bijna net zo goed als een Blu-ray bron, maar kunnen last hebben van audiodelay of visuele artefacten door de adaptieve bitrate van streamingdiensten. Als de internetverbinding van een ripper zakt tot een punt waarop de bitrate daalt, kan de bronbitrate dynamisch veranderen, wat kan leiden tot variaties in de beeldkwaliteit. De meeste releases die last hebben van een extreme hoeveelheid visuele artefacten worden NUKED en er wordt meestal een PROPER uitgebracht om eventuele wilde variaties in adaptieve bitrate te corrigeren. Dit zal in 480p (SD) kwaliteit zijn.
- WEBRip-480p - In een WEB-Rip (P2P) wordt het bestand vaak geëxtraheerd met behulp van de HLS- of RTMP/E-protocollen en opnieuw in een MKV-container geplaatst vanuit een TS-, MP4- of FLV-container. Dit zal in 480p (SD) kwaliteit zijn.
- DVD - Een hercodering van de uiteindelijk uitgebrachte DVD9. Indien mogelijk wordt dit voorafgaand aan de release uitgebracht. Het zou een uitstekende kwaliteit moeten hebben (voor de resolutie). DVDrips worden meestal uitgebracht in DivX/XviD of MP4.
- Bluray-480p - Een hercodering van de uiteindelijk uitgebrachte Blu-ray, verkleind naar een resolutie van 480p (720x480 @ 16:9, een andere beeldverhouding kan een andere resolutie zijn). Indien mogelijk wordt dit voorafgaand aan de release uitgebracht. Het zou een uitstekende kwaliteit moeten hebben voor de resolutie. Bitrates kunnen variëren, maar deze worden over het algemeen gecodeerd naar DivX, XviD of AVC en bieden het compromis van een kleine waargenomen kwaliteitsvermindering ten opzichte van de originele bron, terwijl de bestandsgrootte drastisch wordt verkleind. Deze zijn meestal MKV of MP4, maar er zijn ook enkele DivX/XviD-bestanden beschikbaar die AVI gebruiken.
- HDTV-720p - Een hercodering van de uiteindelijk uitgebrachte Blu-ray, maar uitgezonden via HD-kabel of satelliet (1280x720 @ 16:9, een andere beeldverhouding kan een andere resolutie zijn). Het kan worden aangepast voor de looptijd of inhoud, afhankelijk van het netwerk waar het vandaan komt. Dit wordt meestal enkele maanden na de winkelrelease uitgebracht, maar soms worden opgeschaalde versies van een film met standaarddefinitie uitgebracht op kabelkanalen zoals STARZ of HBO, en dit zouden de enige HD-kopieën van die specifieke film zijn. Deze zijn meestal MKV of MP4.
- HDTV-1080p - Een hercodering van de uiteindelijk uitgebrachte Blu-ray, maar uitgezonden via HD-kabel of satelliet (1920x1080 @ 16:9, een andere beeldverhouding kan een andere resolutie zijn). Het kan worden aangepast voor de looptijd of inhoud, afhankelijk van het netwerk waar het vandaan komt. Dit wordt meestal enkele maanden na de winkelrelease uitgebracht, maar soms worden opgeschaalde versies van een film met standaarddefinitie uitgebracht op kabelkanalen zoals STARZ of HBO, en dit zouden de enige HD-kopieën van die specifieke film zijn. Deze zijn meestal MKV of MP4-container.
- WEBRip-720p - In een WEB-Rip (P2P) wordt het bestand vaak geëxtraheerd met behulp van de HLS- of RTMP/E-protocollen en opnieuw in een MKV-container geplaatst vanuit een TS-, MP4- of FLV-container. Dit zal in 720p kwaliteit zijn.
- Bluray-720p - Een hercodering van de uiteindelijk uitgebrachte Blu-ray, verkleind naar een resolutie van 720p (1280x720 @ 16:9, een andere beeldverhouding kan een andere resolutie zijn). Indien mogelijk wordt dit voorafgaand aan de release uitgebracht. Het zou een uitstekende kwaliteit moeten hebben voor de resolutie. Bitrates kunnen variëren, maar deze worden over het algemeen gecodeerd naar AVC of HEVC en bieden het compromis van een kleine waargenomen kwaliteitsvermindering ten opzichte van de originele bron, terwijl de bestandsgrootte drastisch wordt verkleind. Deze zijn meestal MKV of MP4-container.
- WEBDL-1080p - WEB-DL (P2P) verwijst naar een bestand dat verliesloos is geript van een streamingdienst, zoals Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., of gedownload via een online distributiewebsite zoals iTunes. De kwaliteit is behoorlijk goed, omdat ze niet opnieuw worden gecodeerd. De video (H.264 of H.265) en audio (AC3/AAC) streams worden meestal geëxtraheerd uit iTunes of Amazon Video en opnieuw in een MKV-container geplaatst zonder verlies van kwaliteit. Een voordeel van deze releases is dat ze, net als BD/DVDRips, meestal geen netwerklogo's op het scherm hebben. Deze zijn bijna net zo goed als een Blu-ray bron, maar kunnen last hebben van audiodelay of visuele artefacten door de adaptieve bitrate van streamingdiensten. Als de internetverbinding van een ripper zakt tot een punt waarop de bitrate daalt, kan de bronbitrate dynamisch veranderen, wat kan leiden tot variaties in de beeldkwaliteit. De meeste releases die last hebben van een extreme hoeveelheid visuele artefacten worden NUKED en er wordt meestal een PROPER uitgebracht om eventuele wilde variaties in adaptieve bitrate te corrigeren. Dit zal in 1080p kwaliteit zijn.
- WEBRip-1080p - In een WEB-Rip (P2P) wordt het bestand vaak geëxtraheerd met behulp van de HLS- of RTMP/E-protocollen en opnieuw in een MKV-container geplaatst vanuit een TS-, MP4- of FLV-container. Dit zal in 1080p kwaliteit zijn.
- Bluray-1080p - Een hercodering van de uiteindelijk uitgebrachte Blu-ray, op zijn oorspronkelijke 1080p resolutie (1920x1080 @ 16:9, een andere beeldverhouding kan een andere resolutie zijn). Indien mogelijk wordt dit voorafgaand aan de release uitgebracht. Het zou een uitstekende kwaliteit moeten hebben en dezelfde resolutie als de bron. Bitrates kunnen variëren, maar deze worden over het algemeen gecodeerd naar AVC of HEVC en bieden het compromis van een kleine waargenomen kwaliteitsvermindering ten opzichte van de originele bron, terwijl de bestandsgrootte iets wordt verkleind. Deze zijn meestal MKV of MP4-container.
- Remux-1080p - Een remux is een rip van een Blu-ray of HD DVD-schijf naar een andere containerindeling of gewoon het verwijderen van de menu's en bonusmateriaal van de schijf terwijl de inhoud van de audio- en videostreams intact blijft (ook de huidige codecs behouden), waardoor de exacte 1:1 filmkwaliteit behouden blijft zoals op de originele schijf. Dit is in 1080p kwaliteit.
- HDTV-2160p - TVRip is een opnamebron van een capture card. HDTV staat voor een opgenomen bron van HD-televisie. Met een HDTV-bron kan de kwaliteit soms zelfs beter zijn dan een DVD. Films in dit formaat worden steeds populairder. Sommige advertenties en commerciële banners kunnen te zien zijn op sommige releases tijdens het afspelen. Dit is in 2160p (4K) kwaliteit.
- WEBDL-2160p - WEB-DL (P2P) verwijst naar een bestand dat verliesloos is geript van een streamingdienst, zoals Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., of gedownload via een online distributiewebsite zoals iTunes. De kwaliteit is behoorlijk goed, omdat ze niet opnieuw worden gecodeerd. De video (H.264 of H.265) en audio (AC3/AAC) streams worden meestal geëxtraheerd uit iTunes of Amazon Video en opnieuw in een MKV-container geplaatst zonder verlies van kwaliteit. Een voordeel van deze releases is dat ze, net als BD/DVDRips, meestal geen netwerklogo's op het scherm hebben. Deze zijn bijna net zo goed als een Blu-ray bron, maar kunnen last hebben van audiodelay of visuele artefacten door de adaptieve bitrate van streamingdiensten. Als de internetverbinding van een ripper zakt tot een punt waarop de bitrate daalt, kan de bronbitrate dynamisch veranderen, wat kan leiden tot variaties in de beeldkwaliteit. De meeste releases die last hebben van een extreme hoeveelheid visuele artefacten worden NUKED en er wordt meestal een PROPER uitgebracht om eventuele wilde variaties in adaptieve bitrate te corrigeren. Dit zal in 2160p (4K) kwaliteit zijn.
- WEBRip-2160p - In een WEB-Rip (P2P) wordt het bestand vaak geëxtraheerd met behulp van de HLS- of RTMP/E-protocollen en opnieuw in een MKV-container geplaatst vanuit een TS-, MP4- of FLV-container. Dit zal in 2160p (4K) kwaliteit zijn.
- Bluray-2160p - Een hercodering van de uiteindelijk uitgebrachte Blu-ray, op zijn oorspronkelijke 2160p resolutie (3840x2160 @ 16:9, een andere beeldverhouding kan een andere resolutie zijn). 4K-versies van films worden meestal uitgebracht in de HEVC-codec en kunnen 8-bits of 10-bits kleurreproductie hebben of afkomstig zijn van een HDR-bron. Dit is in 2160p (4K) kwaliteit.
- Remux-2160p - Een remux is een rip van een Blu-ray of HD DVD-schijf naar een andere containerindeling of gewoon het verwijderen van de menu's en bonusmateriaal van de schijf terwijl de inhoud van de audio- en videostreams intact blijft (ook de huidige codecs behouden), waardoor de exacte 1:1 filmkwaliteit behouden blijft zoals op de originele schijf. Dit is in 2160p (4K) kwaliteit.

# Aangepaste formaten

{#custom-formats-2}

- Zorg ervoor dat je elke keer de juiste release krijgt! Aangepaste formaten bieden fijne controle over prioritering en selectie van releases. Zo eenvoudig als een enkel voorkeurswoord of zo complex als je wilt met meerdere criteria en regex.
- Aangepaste formaten worden on-the-fly berekend in plaats van opgeslagen in de database, dus ze worden bijgewerkt zodra je de definities wijzigt.
- Aangepaste formaten worden gebruikt binnen je kwaliteitsprofielen om de score van elk aangepast formaat te bepalen. Binnen elk kwaliteitsprofiel kun je een minimale aangepaste formaatscore instellen voor het vastleggen van een release en ook een score voor een upgrade tot een bepaalde score.
- Het wordt sterk aanbevolen om de onderstaande aangepaste formaten van [TRaSH's Guides](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) toe te voegen om ongewenste downloads te voorkomen. Raadpleeg het gelinkte TRaSH Guide Custom Format-artikel en de aanvullende genoemde 3 TRaSH Custom Format Guides bovenaan de pagina Collection of Custom Formats voor meer informatie.
  - [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) voorkomt het downloaden van releases met Dolby Vision (DV) die een groene tint hebben als DV niet wordt ondersteund.
  - [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) voorkomt het downloaden van slecht genoemde BR-DISKs die niet overeenkomen met de BR-DISK-kwaliteitsanalyse.

---

- Naam - De naam van het aangepaste formaat
- Aangepast formaat opnemen bij hernoemen - De naam van het aangepaste formaat opnemen bij het hernoemen?

> Aangepaste formaten hebben geen invloed op wat er wordt gezocht - alleen hoe de resultaten worden geëvalueerd. Het is ook niet mogelijk om op enige manier de zoekopdracht van Radarr aan te passen.
{.is-info}

Profielen is waar aangepaste formaatscores worden geconfigureerd.

## Voorwaarden voor aangepaste formaten

### Modifiers

- Negate - de overeenkomst wordt omgekeerd, dus de voorwaarde is voldaan als en alleen als de niet-omgekeerde voorwaarde niet is voldaan
- Vereist - is alleen van toepassing op formaten met meer dan één voorwaarde van hetzelfde type en verandert de regels voor het matchen van typegroepen. Als deze optie is ingeschakeld, moet aan deze specifieke voorwaarde worden voldaan voor het hele aangepaste formaat, ongeacht of een andere voorwaarde van hetzelfde type anderszins aan de typegroep zou voldoen. **Opmerking: je gebruikt dit alleen als je een voorwaarde meer dan eens gebruikt. Met andere woorden, als je een aangepast formaat hebt met 2 vereiste voorwaarden voor de releasetitel en 3 niet-vereiste taalvoorwaarden, dan MOETEN BEIDE vereiste voorwaarden voor de releasetitel worden voldaan en MOET EEN VAN de 3 taalvoorwaarden worden voldaan.** Op dezelfde manier, als je een aangepast formaat hebt met 4 releasetitelvoorwaarden en geen daarvan is vereist, dan wordt het aangepaste formaat toegepast als AAN EEN VAN de voorwaarden wordt voldaan.

### Voorwaarden

> **Verschillende voorwaardetypes** werken als `en` binnen hetzelfde aangepaste formaat. **Meerdere voorwaarden van hetzelfde type** werken als `of` tenzij Vereist wordt gebruikt
{.is-info}

- **Alle voorwaarden die RegEx gebruiken zijn hoofdletterongevoelig**
- Let op de volgende GitHub-problemen
  - [Aangepaste formaten worden niet toegepast vóór het jaartal van de film in releasetitels #4859](https://github.com/Radarr/Radarr/issues/4859)
  - [Aangepast formaat komt niet overeen met term "xvid" aan het einde van de releasenaam #6824](https://github.com/Radarr/Radarr/issues/6824)
- Releasetitel - Dit is een reguliere expressie die wordt vergeleken met de releasetitel en, na het downloaden, de bestandsnaam op schijf.
  - Opmerking: Radarr houdt alleen rekening met tekst na de filmtitel en het jaartal, wat betekent dat alles voorafgaand aan de titel wordt genegeerd.
- Editie - Deze tag wordt vergeleken met eventuele edities die Radarr kan parsen. Je kunt elke waarde opgeven die Radarr zal proberen te matchen met wat het heeft geparseerd (hoofdletterongevoelig).
- Taal - Deze taal wordt vergeleken met eventuele taal(talen) die Radarr parsen. Alle eerder selecteerbare talen in profielen werken hier.
- [Indexer-vlag](/radarr/settings#indexer-flags) - Deze tag wordt vergeleken met eventuele indexer-vlaggen die Radarr kan parsen.
- Bron - De bron waaruit een release is geript (bijv. BLURAY).
- Resolutie - De resolutie die is geparseerd uit de releasenaam of mediainfo (indien beschikbaar).
- Kwaliteitsmodifier - Kwaliteitsmodifier stelt zaken in zoals Telescene, Telesync, Remux, Regionaal. Het onderscheidt een bepaalde bron en resolutie combinatie wanneer er meerdere kwaliteits (bron) typen van toepassing kunnen zijn.
- Grootte - Dit wordt vergeleken met de bestandsgrootte van de release. De bestandsgrootte wordt omgezet naar gigabytes en vergeleken met de min- en max-waarden.
- Groep - Dit wordt vergeleken met de groep die Radarr parsen op basis van de groepdetectielogica van Radarr.

### Profielinstellingen en rangschikking

- Aangepaste formaten worden geïmplementeerd binnen en hebben hun impact gecontroleerd door kwaliteitsprofielen. De score voor een upgrade tot bepaalde score voorkomt dat er wordt geüpgraded nadat een release met deze gewenste score is gedownload.
- Een score van 0 zorgt ervoor dat het aangepaste formaat alleen informatief is en geen invloed heeft op de rangschikking van releases of de gezochte talen.
- De minimale score vereist dat de cumulatieve aangepaste formaatscore van releases deze drempelwaarde bereikt, anders worden ze afgewezen.
  - Aangepaste formaten die overeenkomen met ongewenste kenmerken moeten een negatieve score krijgen om hun aantrekkingskracht te verminderen.
  - Volledige afwijzingen moeten een negatieve score krijgen die laag genoeg is dat zelfs als alle andere formaten met positieve scores worden toegevoegd, de score nog steeds onder de minimumwaarde valt.
- [Zie TRaSH's Guides voor het instellen en gebruiken van aangepaste formaten](https://trash-guides.info/Radarr/Radarr-setup-custom-formats/)

#### Aangepaste formaten importeren / exporteren

- [Zie TRaSH's Guides voor het importeren/exporteren van aangepaste formaten.](https://trash-guides.info/Radarr/Radarr-import-custom-formats/) Het is echter mogelijk om aangepaste formaten te importeren en exporteren.

#### Aangepaste formaten importeren / bijwerken

- [Zie TRaSH's Guides voor het importeren of bijwerken van bestaande aangepaste formaten.](https://trash-guides.info/Radarr/Radarr-how-to-update-custom-formats/)

### Verzameling van aangepaste formaten

- [TRaSH onderhoudt een verzameling aangepaste formaten](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)

# Indexers

> Informatie over ondersteunde indexers is te vinden op de [Meer informatie (Ondersteund)](/radarr/supported#indexers) pagina voor dit gedeelte
{.is-info}

## Ondersteunde indexers

- Een lijst met ondersteunde indexers is te vinden op de [Meer informatie (Ondersteund)](/radarr/supported#indexers) pagina

### Indexerinstellingen

- Nadat je op de <kb>+</kb> knop hebt geklikt om een nieuwe indexer toe te voegen, krijg je een nieuw venster te zien met veel verschillende opties. Voor de doeleinden van deze wiki beschouwt Radarr zowel Usenet-indexers als torrent-trackers als "indexers".

- Er zijn hier twee secties: Usenet en Torrents. Afhankelijk van welke downloadclient je gaat gebruiken, moet je het type indexer selecteren waarmee je aan de slag gaat.

### Configuratie van Usenet-indexer



- Newznab - Hier vind je vooraf ingestelde populaire Usenet-indexers (die al zijn ingevuld, je hebt alleen je API-sleutel nodig die wordt verstrekt door de Usenet-indexer van jouw keuze), samen met de mogelijkheid om een aangepaste indexer te maken.
- Software die werkt met Usenet en goed integreert met Radarr zijn [NZBHydra2](https://github.com/theotherp/nzbhydra2/) of [Prowlarr](/prowlarr) die zowel met Usenet als Torrents integreren.
- Ongeacht of je een vooraf ingevulde indexer of een aangepaste indexer selecteert, krijg je een nieuw venster te zien om al je instellingen in te voeren.
- Kies uit de vooraf ingestelde opties of voeg een aangepaste indexer toe (zoals NZBHydra2 of Prowlarr).
- Naam - De naam van de indexer in Radarr.
- RSS inschakelen - Indien ingeschakeld, gebruik deze indexer om te zoeken naar bestanden die ontbreken of nog niet aan hun limiet hebben voldaan.
- Automatisch zoeken inschakelen - Indien ingeschakeld, gebruik deze indexer voor automatische zoekopdrachten, inclusief zoeken bij toevoegen.
- Interactief zoeken inschakelen - Indien ingeschakeld, gebruik deze indexer voor handmatige interactieve zoekopdrachten.
- URL - De URL die door de indexer wordt verstrekt, zoals `https://api.nzbgeek.info`.
- API-pad - Het pad naar de API dat door de indexer wordt verstrekt. Dit is meestal `/api`.
- Meertaligheid - Stel in welke talen `MULTI` beschikbaar zijn voor deze indexer.
- API-sleutel - De sleutel die door de indexer wordt verstrekt om toegang te krijgen tot de API.
- Categorieën - Standaardcategorieën worden gebruikt, tenzij ze worden bewerkt. Waarschijnlijk zijn deze standaardcategorieën niet optimaal. Bij het bewerken van deze instelling vraagt Radarr de indexer om de beschikbare categorieën en toont ze in een selecteerbare lijst. De verouderde standaardinstellingen worden gewist zodra een categorie wordt gewijzigd.
- (Geavanceerde optie) Extra parameters - Extra Newznab-parameters om toe te voegen aan de querylink.
- Jaar verwijderen uit zoekreeks - Moet Radarr het jaar na de titel van de film verwijderen bij tekstgebaseerde zoekopdrachten naar deze indexer?
- (Geavanceerde optie) Indexervoorkeur - Voorkeur van deze indexer om de ene indexer boven de andere te verkiezen in geval van gelijkstand bij releases. 1 is de hoogste prioriteit en 50 is de laagste prioriteit.
- (Geavanceerde optie) Downloadclient - Selecteer en specificeer welke downloadclient wordt gebruikt voor downloads van deze indexer.
- Tags - Gebruik deze indexer alleen voor films met minstens één overeenkomende tag. Laat leeg om te gebruiken met alle films.

### Torrent Tracker-configuratie

- Net als bij Usenet zijn er verschillende vooraf ingevulde Torrent-trackerinformatie. Als je geen lid bent van een van deze specifieke trackers, heb je er niets aan.
- Een van de beste en eenvoudigste manieren om Torrent-trackers te gebruiken die niet standaard worden ondersteund door Radarr, is door gebruik te maken van een tweede programma zoals [Prowlarr](/prowlarr) of [Jackett](https://github.com/Jackett/Jackett). Deze software werkt goed samen met Radarr als een zoekindexer die al je informatie bevat en naar Radarr stuurt.
- Torznab - Deze optie stelt je in staat om een Jackett-voorinstelling te gebruiken. Als je meerdere trackers gebruikt, moet elke invoer een unieke naam hebben.
- Torznab-indexer
- Kies uit de vooraf ingestelde opties of voeg een aangepaste indexer toe (zoals Jackett).
- Naam - De naam van de indexer in Radarr.
- RSS inschakelen - Indien ingeschakeld, gebruik deze indexer om te zoeken naar bestanden die ontbreken of nog niet aan hun limiet hebben voldaan.
- Automatisch zoeken inschakelen - Indien ingeschakeld, gebruik deze indexer voor automatische zoekopdrachten, inclusief zoeken bij toevoegen.
- Interactief zoeken inschakelen - Indien ingeschakeld, gebruik deze indexer voor handmatige interactieve zoekopdrachten.
- URL - De URL die door de indexer wordt verstrekt, zoals `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-pad - Het pad naar de API dat door de indexer wordt verstrekt. Dit is meestal `/api`.
- API-sleutel - De sleutel die door de indexer wordt verstrekt om toegang te krijgen tot de API.
- Meertaligheid - Stel in welke talen `MULTI` beschikbaar zijn voor deze indexer.
- Categorieën - Standaardcategorieën worden gebruikt, tenzij ze worden bewerkt. Waarschijnlijk zijn deze standaardcategorieën niet optimaal. Bij het bewerken van deze instelling vraagt Radarr de indexer om de beschikbare categorieën en toont ze in een selecteerbare lijst. De verouderde standaardinstellingen worden gewist zodra een categorie wordt gewijzigd.
- (Geavanceerde optie) Extra parameters - Extra Torznab-parameters om toe te voegen aan de querylink.
- Jaar verwijderen uit zoekreeks - Moet Radarr het jaar na de titel van de film verwijderen bij tekstgebaseerde zoekopdrachten naar deze indexer?
- Minimale seeders - Het minimum aantal seeders dat vereist is voor een release van deze tracker om te worden gedownload.
- Seedratio - Indien leeg, wordt de standaard seedratio van de downloadclient gebruikt. Anders is dit de minimale seedratio die je downloadclient moet halen voor releases van deze indexer voordat ze worden gepauzeerd door je client en verwijderd door Radarr (vereist ingeschakelde voltooide downloadverwerking - verwijderen).
- Seedtijd - Indien leeg, wordt de standaard seedtijd van de downloadclient gebruikt. Anders is dit de minimale seedtijd in minuten die je downloadclient moet halen voor releases van deze indexer voordat ze worden gepauzeerd door je client en verwijderd door Radarr (vereist ingeschakelde voltooide downloadverwerking - verwijderen).
- Vereiste vlaggen - Welke indexeringsvlaggen zijn vereist?

#### Indexeringsvlaggen

| Vlag             | Symbool | Beschrijving                                                                                                                                                                                                                 |
| ---------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `G_Freeleech`    | ⬇⬇     | Soms stellen torrentsites een torrent in als freeleech. Dit betekent dat het downloaden van deze torrent niet meetelt voor je downloadquotum of ratio. Dit is erg handig als je nog geen goede ratio hebt opgebouwd. |
| `G_Halfleech`    | ⇩⇩     | Vergelijkbaar met `G_Freeleech`, geeft `G_Halfleech` aan dat slechts de helft van de grootte van deze torrent meetelt voor je downloadquotum of ratio.                                                                               |
| `G_DoubleUpload` | ⬆      | Vergelijkbaar met `G_Freeleech`, geeft `G_DoubleUpload` aan dat elke hoeveelheid data die je uploadt via seeding twee keer wordt geteld voor je uploadquotum en ratio. Dit is erg handig als je een ratio-buffer wilt opbouwen.      |
| `PTP_Golden`     | 🌟      | Op PassThePopcorn krijgen sommige torrents het *Golden*-label wanneer ze voldoen aan bepaalde coderingsstandaarden. Dit zijn meestal de beste encodes, met bijna geen waarneembaar kwaliteitsverlies. Je kunt meer informatie vinden op hun wiki-pagina. |
| `PTP_Approved`   | ✔      | Op PassThePopcorn worden sommige torrents goedgekeurd wanneer ze voldoen aan de minimale standaarden voor codering (bijv. geen lage bitrates). Zie hun wiki voor meer informatie.                                                              |
| `HDB_Internal`   | 🚪      | Releases op HDBits krijgen dit label wanneer de release is geüpload door een van de releasegroepen van HDBits zelf.                                                                                                       |
| `G_Scene`        | ☠      | Vergelijkbaar met `G_Freeleech`, geeft `G_Freeleech75` aan dat slechts 25% van de grootte van deze torrent meetelt voor je downloadquotum of ratio.                                                                              |
| `G_Freeleech75`  | ⇩⬇     | Vergelijkbaar met `G_Freeleech`, geeft `G_Freeleech75` aan dat slechts 25% van de grootte van deze torrent meetelt voor je downloadquotum of ratio.                                                                              |
| `G_Freeleech25`  | ⇩      | Vergelijkbaar met `G_Freeleech`, geeft `G_Freeleech25` aan dat slechts 75% van de grootte van deze torrent meetelt voor je downloadquotum of ratio.                                                                              |

- (Geavanceerde optie) Indexervoorkeur - Voorkeur van deze indexer om de ene indexer boven de andere te verkiezen in geval van gelijkstand bij releases. 1 is de hoogste prioriteit en 50 is de laagste prioriteit.
- (Geavanceerde optie) Downloadclient - Selecteer en specificeer welke downloadclient wordt gebruikt voor downloads van deze indexer.
- Tags - Gebruik deze indexer alleen voor films met minstens één overeenkomende tag. Laat leeg om te gebruiken met alle films.

## Opties

- Minimale leeftijd - Alleen voor Usenet: Minimale leeftijd in minuten van NZB's voordat ze worden gedownload. Gebruik dit om nieuwe releases de tijd te geven om zich te verspreiden naar je Usenet-provider.
- Retentie - Alleen voor Usenet: Stel in op nul voor onbeperkte retentie.
- Maximale grootte - Maximale grootte voor een release om te worden gedownload in MB. Stel in op nul voor onbeperkt. Houd er rekening mee dat dit wereldwijd van toepassing is.
- Voorkeur voor indexeringsvlaggen - Prioriteit geven aan releases met speciale vlaggen. (Zie Vereiste vlaggen hierboven)
- Beschikbaarheidsvertraging - Tijd voor (-#) of na (#) de beschikbaarheidsdatum om te zoeken naar een film.
  - Dit is handig om het zoeken naar een release te vertragen om de community de tijd te geven om de beste encodes te maken.
  - Meestal wordt een beschikbaarheid van `Uitgebracht` met een vertraging van `-21` of `-14` aanbevolen.
- RSS-synchronisatie-interval - Interval in minuten. Stel in op nul om uit te schakelen (dit stopt alle automatische release-download). Minimum: 10 minuten Maximum: 120 minuten
  - Zie [Hoe vindt Radarr films?](/radarr/faq#how-does-radarr-find-movies) voor een beter begrip van hoe RSS-synchronisatie je kan helpen.

> Als Radarr langere tijd offline is geweest, zal Radarr proberen terug te bladeren om de laatste release te vinden die het heeft verwerkt om te voorkomen dat er een release wordt gemist. Zolang je indexer paginering ondersteunt en het niet te lang geleden is, kan Radarr de releases verwerken die het anders zou hebben gemist en hoef je geen zoekopdracht uit te voeren voor de gemiste releases.{.is-info}

- Whitelisted ondertiteltags - Tags die hier worden ingevoerd, worden niet beschouwd als hardcoded ondertitels.
- Harde ondertitels toestaan - Indien ingeschakeld, sta toe dat releases met hardcoded ondertitels automatisch worden gedownload.

# Downloadclients

> Informatie over ondersteunde downloadclients is te vinden op de [Meer informatie (Ondersteund)](/radarr/supported#download-clients) pagina voor dit gedeelte
{.is-info}

## Overzicht

- Downloaden en importeren is waar de meeste mensen problemen ervaren. Vanuit een hoog niveau perspectief moet de software kunnen communiceren met je downloadclient en toegang hebben tot de bestanden die het downloadt. Er is een grote verscheidenheid aan ondersteunde downloadclients en een nog grotere verscheidenheid aan configuraties. Dit betekent dat hoewel er enkele veelvoorkomende configuraties zijn, er geen juiste configuratie is en de configuratie van iedereen een beetje anders kan zijn. Maar er zijn veel verkeerde configuraties.

## Processen van downloadclients

### Usenet-proces

- Radarr stuurt een downloadverzoek naar je client en koppelt het aan een label of categorienaam die je hebt geconfigureerd in de instellingen van de downloadclient. Voorbeelden: films, tv, series, muziek, enz.
- Radarr controleert de actieve downloads van je downloadclient die deze categorienaam gebruiken. Dit gebeurt via de API van je downloadclient.
- Wanneer de download is voltooid, weet Radarr de uiteindelijke bestandslocatie zoals gerapporteerd door je downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang het maar ergens apart van je mediabibliotheek staat en toegankelijk is voor Radarr.
- Radarr scant die voltooide bestandslocatie op bestanden die Radarr kan gebruiken. Het analyseert de bestandsnaam om deze te matchen met de gevraagde media. Als dat lukt, wordt het bestand hernoemd volgens jouw specificaties en verplaatst naar de opgegeven mediabibliotheek.
- Atomic Moves (directe verplaatsingen) zijn standaard ingeschakeld. Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor je voltooide downloadmap en je mediabibliotheek. Als de atomic move mislukt of je configuratie geen hardlinks en atomic moves ondersteunt, zal Radarr teruggaan naar het kopiëren van het bestand en het vervolgens verwijderen van de bron, wat IO-intensief is.

### Torrentproces

- Radarr stuurt een downloadverzoek naar je client en koppelt het aan een label of categorienaam die je hebt geconfigureerd in de instellingen van de downloadclient. Voorbeelden: films, tv, series, muziek, enz.
- Radarr controleert de actieve downloads van je downloadclient die deze categorienaam gebruiken. Deze controle gebeurt via de API van je downloadclient.
- Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat je het bestand kunt seeden (ratio of tijd kan worden aangepast in de downloadclient of vanuit Radarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar je mediabibliotheek, zal Radarr een harde koppeling maken naar het bestand als dit wordt ondersteund door je configuratie, anders wordt het bestand gekopieerd als harde koppelingen niet worden ondersteund.
- Harde koppelingen zijn standaard ingeschakeld. [Een harde koppeling gebruikt geen extra schijfruimte.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor je voltooide downloadmap en je mediabibliotheek. Als het maken van een harde koppeling mislukt of je configuratie geen harde koppelingen ondersteunt, zal Radarr teruggaan naar het kopiëren van het bestand.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen van Radarr, zal Radarr het oorspronkelijke bestand en de torrent verwijderen uit je client, maar alleen als de client meldt dat het seeden is voltooid en de torrent is gestopt (d.w.z. gepauzeerd).

## Downloadclients

Klik op `Instellingen => Downloadclients` en klik vervolgens op het <kb>+</kb> om een nieuwe downloadclient toe te voegen. Je downloadclient moet al geconfigureerd en actief zijn.

### Ondersteunde downloadclients

- Een lijst met ondersteunde downloadclients is te vinden op de [Meer informatie (Ondersteund)](/radarr/supported#download-clients) pagina

Selecteer de downloadclient die je wilt toevoegen en er verschijnt een pop-upvenster om de verbindingsgegevens in te voeren. Deze gegevens zijn vergelijkbaar voor de meeste clients. Sommige vragen om een gebruikersnaam of wachtwoord, andere vragen of nieuwe downloads in een gepauzeerde/startstatus moeten worden toegevoegd, enz.

### Instellingen voor Usenet-client

- Naam - De naam van de downloadclient in Radarr.
- Inschakelen - Deze downloadclient inschakelen.
- Host - De URL van je downloadclient.
- Poort - De poort van je downloadclient.
- SSL gebruiken - Een beveiligde verbinding gebruiken met je downloadclient. Let op deze veelvoorkomende fout.
- (Geavanceerde optie) URL-basis - Een voorvoegsel toevoegen aan de URL; dit is vaak nodig voor omgekeerde proxies.
- API-sleutel - De API-sleutel om te authenticeren bij je client.
- Gebruikersnaam - De gebruikersnaam om te authenticeren bij je client (meestal niet nodig).
- Wachtwoord - Het wachtwoord om te authenticeren bij je client (meestal niet nodig).
- Categorie - De categorie binnen je downloadclient die \*Arr zal gebruiken. Om te voorkomen dat niet-gerelateerde downloads worden weergegeven in de activiteit, wordt het sterk aanbevolen om een categorie in te stellen.
- Prioriteit recente downloads - Downloadclientprioriteit voor recent uitgebrachte media.
- Prioriteit oudere downloads - Downloadclientprioriteit voor media die niet recent is uitgebracht.
- (Geavanceerde optie) Clientprioriteit - Prioriteit van de downloadclient. Round-Robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) met dezelfde prioriteit. 1 is de hoogste prioriteit en 50 is de laagste prioriteit.
- Voltooide downloadverwerking
  - Verwijderen (Per clientinstelling) - Voltooide downloads verwijderen wanneer deze zijn voltooid (usenet) of gestopt/voltooid (torrents). Zie [Voltooide downloadverwerking voor meer details](#completed-download-handling).

### Instellingen voor torrentclient

- Naam - De naam van de downloadclient binnen Radarr
- Inschakelen - Schakel deze downloadclient in
- Host - De URL van uw downloadclient
- Poort - De poort van uw downloadclient; dit is meestal de webgui-poort
- Gebruik SSL - Gebruik een beveiligde verbinding met uw downloadclient. Let op deze veelgemaakte fout.
- (Geavanceerde optie) URL-basis - Voeg een voorvoegsel toe aan de URL; dit is vaak nodig voor omgekeerde proxies.
- Gebruikersnaam - de gebruikersnaam om u aan te melden bij uw client
- Wachtwoord - het wachtwoord om u aan te melden bij uw client
- Categorie - de categorie binnen uw downloadclient die \*Arr zal gebruiken. Om ongerelateerde downloads te voorkomen die worden weergegeven in Activiteit, wordt het sterk aanbevolen om een categorie in te stellen.
- Categorie na importeren - de categorie om in te stellen nadat de release is gedownload en geïmporteerd. Houd er rekening mee dat dit het verwijderen van voltooide downloadverwerking verbreekt.
- Recente prioriteit - downloadclientprioriteit voor recent uitgebrachte media
- Oudere prioriteit - downloadclientprioriteit voor media die niet recentelijk is uitgebracht
- Initiële status - Initiële status voor torrents (alleen Qbittorrent: geforceerd om alle seeddrempels te omzeilen)
- (Geavanceerde optie) Clientprioriteit - Prioriteit van de downloadclient. Round-Robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) met dezelfde prioriteit. 1 is de hoogste prioriteit en 50 is de laagste prioriteit
- Voltooide downloadverwerking
  - Verwijderen (per clientinstelling) - Verwijder voltooide downloads wanneer deze zijn voltooid (usenet) of gestopt/voltooid (torrents). Zie [Voltooide downloadverwerking voor meer informatie](#voltooide-downloadverwerking)
    - Voor torrents moet uw downloadclient pauzeren wanneer de seeddoelen zijn bereikt. Het vereist ook dat de seeddoelen worden ondersteund door Radarr volgens de onderstaande tabel. Torrents moeten ook in dezelfde categorie blijven.

### Compatibiliteit verwijderen torrentclient downloaden

- Radarr kan alleen de seedverhouding/tijd instellen op clients die deze waarde kunnen instellen via hun API wanneer de torrent wordt toegevoegd. Seeddoelen kunnen wereldwijd worden ingesteld in de client zelf of per tracker in de instellingen van \*Arr voor elke indexer. Zie de onderstaande tabel voor compatibiliteit van de client.

|      Client       |                                Verhouding                                 |                                    Tijd                                    |
| :---------------: | :-----------------------------------------------------------------------: | :------------------------------------------------------------------------: |
|       Aria2       |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)    |    ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)    |
|      Deluge       |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)    |    ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)    |
| Download Station  | ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek) |    ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)    |
|       Flood       |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)    |      ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)      |
|     Hadouken      | ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek) |    ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)    |
|    qBittorrent    |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)    |      ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)      |
|     rTorrent      |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)    |      ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)      |
| Torrent Blackhole | ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek) |    ![Niet ondersteund](https://img.shields.io/badge/Ondersteund-Nee-kritiek)    |
|   Transmission    |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)    | ![Idle Limit](https://img.shields.io/badge/Ondersteund-Idle%20Limit*-blauw)\* |
|     uTorrent      |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)    |      ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)      |
|       Vuze        |   ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)    |      ![Ondersteund](https://img.shields.io/badge/Ondersteund-Ja-succes)      |

> ![Idle Limit](https://img.shields.io/badge/Ondersteund-Idle%20Limit*-blauw) - Transmission heeft intern een Idle Time-controle, maar Radarr vergelijkt deze met de seedtijd als de idle-limiet is ingesteld op basis van een specifieke torrent. Dit wordt gedaan als workaround voor de api-beperkingen van Transmission.{.is-info}

## Voltooide downloadverwerking

- Voltooide downloadverwerking is hoe Radarr media importeert van uw downloadclient naar uw serie-mappen. Veelvoorkomende problemen hebben te maken met slechte Docker-paden en/of andere Docker-machtigingsproblemen.

- (Geavanceerde globale instelling) Inschakelen - Voltooide downloads automatisch importeren vanuit de downloadclient
- (Geavanceerde optie) Interval controleren op voltooide downloads - Stel in hoe vaak de wachtrijen van de downloadclients moeten worden gecontroleerd en gemonitorde downloads moeten worden vernieuwd, minimaal 1 minuut
- (Per clientinstelling) Verwijderen - Voltooide downloads verwijderen wanneer deze zijn voltooid (usenet) of gestopt/voltooid (torrents)
  - Voor torrents moet uw downloadclient pauzeren wanneer de seeddoelen zijn bereikt. Het vereist ook dat de seeddoelen worden ondersteund door Radarr volgens de bovenstaande tabel. Torrents moeten ook in dezelfde categorie blijven.

### Voltooide downloads verwijderen

- Radarr stuurt een downloadverzoek naar uw client en koppelt het aan een label of categorienaam die u heeft geconfigureerd in de instellingen van de downloadclient.
- Radarr controleert de actieve downloads van uw downloadclients die deze categorienaam gebruiken. Dit wordt gemonitord via de API van uw downloadclient.
- Wanneer de download is voltooid, weet Radarr de uiteindelijke bestandslocatie zoals gerapporteerd door uw downloadclient. Deze bestandslocatie kan bijna overal zijn, zolang het maar ergens anders is dan uw mediabestand.
- Radarr scant die voltooide bestandslocatie op videobestanden. Het analyseert de bestandsnaam van de video om deze te matchen met een film. Als dat lukt, wordt het bestand hernoemd volgens uw specificaties en verplaatst naar de toegewezen bibliotheekmap.
- Overgebleven bestanden van de download worden naar uw prullenbak of recycling gestuurd.

Als u downloadt met een BitTorrent-client, verloopt het proces iets anders:

- Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat u kunt seeden. Wanneer bestanden worden geïmporteerd naar uw toegewezen bibliotheekmap, zal Radarr proberen een harde koppeling naar het bestand te maken of overschakelen naar kopiëren (gebruik dubbele ruimte) als harde koppelingen niet worden ondersteund.
- Als de optie "Voltooide downloadverwerking - Verwijderen" is ingeschakeld in de instellingen, zal Radarr de torrentclient vragen om het oorspronkelijke bestand en de torrent te verwijderen, maar dit gebeurt alleen als de client meldt dat het seeden is voltooid, de torrent dezelfde categorie heeft (d.w.z. geen gebruik van een categorie na importeren), het seeddoel dat is bereikt wordt ondersteund door Radarr en de torrent is gepauzeerd (gestopt).

### Mislukte downloadverwerking

- Mislukte downloadverwerking is alleen compatibel met SABnzbd en NZBGet.
- Mislukte downloadverwerking is niet van toepassing op torrents en er zijn geen plannen om deze functionaliteit toe te voegen.

- Er zijn verschillende componenten die deel uitmaken van het proces van mislukte downloadverwerking:

- Controleer Downloader:
  - Wachtrij - Controleer de wachtrij van uw downloader op versleutelde releases die zijn gemarkeerd als mislukt
  - Geschiedenis - Controleer de geschiedenis van uw downloader op mislukkingen (bijv. niet genoeg om te repareren, of extractie mislukt)
- Wanneer Radarr een mislukte download vindt, begint het met het verwerken ervan en doet het een paar dingen:
  - Voegt een mislukt evenement toe aan de geschiedenis van Radarr
  - Verwijdert de mislukte download van de downloadclient om ruimte vrij te maken en gedownloade bestanden te wissen (optioneel)
  - Begint te zoeken naar een vervangend bestand (optioneel)
  - Blocklisting (voorheen 'Blacklisting') maakt automatisch overslaan van nzbs mogelijk wanneer ze mislukken, dit betekent dat die nzb nooit meer automatisch door Radarr wordt gedownload (u kunt de download nog steeds forceren via een handmatige zoekopdracht).
  - Er zijn 2 geavanceerde opties (op de pagina 'Download Client' instellingen) die het gedrag van mislukte downloadverwerking in Radarr bepalen, op dit moment staan ze allemaal standaard aan.

- Opnieuw downloaden - Bepaalt of Radarr na een mislukking naar hetzelfde bestand zal zoeken
- (Geavanceerde optie) Verwijderen - Bepaalt of de download automatisch moet worden verwijderd uit de downloadclient wanneer de mislukking wordt gedetecteerd

## Externe padtoewijzingen

- Externe padtoewijzing fungeert als een eenvoudige zoekopdracht naar extern pad en vervanging door lokaal pad. Dit wordt voornamelijk gebruikt voor samengevoegde lokale/externe configuraties met behulp van mergerfs of iets dergelijks, of wordt gebruikt wanneer de toepassing en de downloadclient zich niet op dezelfde server bevinden.
- Een externe padtoewijzing wordt gebruikt wanneer uw downloadclient een pad rapporteert voor voltooide gegevens op een andere server of op een manier die \*Arr niet adresseert naar die map.
- Over het algemeen is een externe padtoewijzing alleen vereist als uw downloadclient op Linux staat wanneer \*Arr op Windows staat of vice versa. Een externe padtoewijzing is ook mogelijk nodig bij het mixen van Docker- en Native-clients of bij het gebruik van een externe server.
- Een externe padtoewijzing is een DOMME zoek/vervang (waarbij de WAARDE VAN HET EXTERNE pad wordt gevonden en vervangen door de WAARDE VAN HET LOKALE pad voor de opgegeven Host).
- Als het foutbericht over een ongeldig pad de VERVANGENDE waarde niet bevat, werkt de padtoewijzing niet zoals u verwacht. De gebruikelijke oplossing is om de toewijzing toe te voegen en te verwijderen.
- [Zie de tutorial van TRaSH voor aanvullende informatie over externe padtoewijzing](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Als zowel \*Arr als uw Download Client Docker-containers zijn, is een externe padtoewijzing zelden nodig. Het wordt aanbevolen om [de Docker-gids](/docker-guide) te bekijken en/of [de tutorial van TRaSH](https://trash-guides.info/hardlinks) te volgen{.is-info}

# Importlijsten

> Informatie over ondersteunde lijsttypen is te vinden op de [Meer informatie (Ondersteund)](/radarr/supported#lists) pagina voor dit gedeelte{.is-info}

## Lijsten

Importlijsten maken deel uit van Radarr en stellen u in staat een bepaalde lijstmaker te volgen. Laten we zeggen dat u een bepaalde lijstmaker volgt op Trakt/TMDb en dat u hun ArrowVerse-collectiegedeelte echt leuk vindt en elke show op hun lijst wilt bekijken. U kijkt in uw Radarr en realiseert zich dat u die series niet heeft. In plaats van één voor één te zoeken en die items toe te voegen en vervolgens uw indexers te doorzoeken naar die series, kunt u dit allemaal tegelijk doen met een lijst. De lijsten kunnen worden ingesteld om alle series op die lijst van de curator te importeren, evenals automatisch een kwaliteitsprofiel toewijzen, automatisch toevoegen en automatisch bewaken van die series.

- LET OP: Als lijsten verkeerd worden gedaan, zullen ze absoluut uw bibliotheek vernietigen met een hoop rommel waarvan u niet van plan bent om te kijken. Zorg er dus voor dat u weet wat u importeert voordat u opslaat. D.w.z. bekijk de lijst fysiek voordat u zelfs naar Radarr gaat.

- Hier kunt u op de <kb>+</kb>-knop klikken om een nieuw pop-upvenster te openen
- In dit nieuwe venster krijgt u veel verschillende opties om uw lijst in te stellen vanuit veel verschillende lijstproviders. Zoals eerder vermeld, wees voorzichtig bij het maken van lijsten. Het wordt ten zeerste aanbevolen om niet op de knop Zoeken bij toevoegen te klikken voordat u er absoluut zeker van bent dat de lijst die u selecteert/opzet de series toevoegt die u zoekt.
- Nadat u de lijstprovider heeft geselecteerd waaruit u wilt putten (zoals IMDb of Trakt), krijgt u een nieuw venster te zien.
De meeste instellingen van de lijsten zijn vrij duidelijk, sommige lijsten vereisen dat u zich authenticeert bij de provider, zoals Trakt (waarvoor u een account bij Trakt.tv moet hebben)

## Lijstopties

- (Geavanceerde optie) Interval bijwerken lijst - Hoe vaak moet Radarr de lijst controleren op updates? [Dit is minimaal 6 uur.](/radarr/faq#why-are-lists-sync-times-so-long-and-can-i-change-it)
- (Geavanceerde optie) Niveau bibliotheek opschonen - Films in de bibliotheek worden verwijderd of niet bewaakt als ze niet in uw lijst(en) staan
  - Uitgeschakeld - Schoon de bibliotheek niet op (Aanbevolen)
  - Alleen loggen - Log alleen de films die niet op de lijst(en) staan en onderneem geen andere acties
  - Film behouden en niet bewaken - Houd films die niet op de lijst(en) staan, maar bewaak ze niet in Radarr.
  - Film verwijderen en bestanden behouden - Verwijder films die niet op de lijst(en) staan uit Radarr, maar verwijder hun bestanden niet
  - Film verwijderen en bestanden verwijderen - Verwijder films die niet op de lijst(en) staan uit Radarr en verwijder hun bestanden

## Lijstuitsluitingen

- Importlijstuitsluiting - Hiermee kunt u uw lijst van films snoeien die u niet meer wilt zien. Een voorbeeld hiervan is als uw lijst toevallig een film bevat die in een vreemde taal is en het is niet waarschijnlijk dat u deze film ooit in uw moedertaal zult vinden en deze niet met ondertitels wilt bekijken. U kunt een film uitsluiten van toevoeging in de toekomst. U kunt de film echter in het gedeelte lijstuitsluiting weer toevoegen, zodat deze bij de volgende uitvoering van de lijst naar uw bibliotheek wordt gelezen.

# Verbinding

> Informatie over ondersteunde verbindingssoorten is te vinden op de [Meer informatie (Ondersteund)](/radarr/supported#notifications) pagina voor dit gedeelte{.is-info}

## Verbindingen

Verbindingen bepalen hoe Radarr communiceert met de buitenwereld.

- Door op de <kb>+</kb>-knop te drukken, wordt een nieuw venster geopend waarin u veel verschillende eindpunten kunt configureren

- Een lijst met ondersteunde meldingen en verbindingen is te vinden op de [Meer informatie (Ondersteund)](/radarr/supported#notifications) pagina

## Verbindingsacties

- Bij pakken - Ontvang een melding wanneer films beschikbaar zijn om te downloaden en naar een downloadclient zijn gestuurd
- Bij importeren - Ontvang een melding wanneer films succesvol zijn geïmporteerd
- Bij upgraden - Ontvang een melding wanneer films worden geüpgraded naar een betere kwaliteit
- Bij hernoemen - Ontvang een melding wanneer films worden hernoemd
- Bij toevoegen film - Ontvang een melding wanneer films aan de bibliotheek van Radarr worden toegevoegd om te beheren of te monitoren
- Bij verwijderen film - Ontvang een melding wanneer films worden verwijderd
- Bij verwijderen filmbestand - Ontvang een melding wanneer filmbestanden worden verwijderd
- Bij verwijderen filmbestand voor upgrade - Ontvang een melding wanneer filmbestanden worden verwijderd voor upgrades
- Bij gezondheidsprobleem - Ontvang een melding bij mislukte gezondheidscontroles
  - Gezondheidswaarschuwingen opnemen - Ontvang ook meldingen bij gezondheidswaarschuwingen.
- Bij toepassingsupdate - Ontvang een melding wanneer Radarr wordt bijgewerkt naar een nieuwe versie

# Metadata

## Opties

- Certificeringsland - Selecteer het land dat moet worden gebruikt voor filmcertificeringen (bijv. R (VS) of 12A (VK))

## Metadata-consumenten

> Informatie over ondersteunde metadata-consumenten is te vinden op de [Meer informatie (Ondersteund)](/radarr/supported#metadata) pagina voor dit gedeelte{.is-info}

Hier kunt u het type metadata selecteren dat door uw mediaspeler wordt gebruikt

Kodi zal hier een van de meest gebruikte opties zijn als dat de gebruikte software is. Hierdoor kan Radarr een NFO-bestand maken en bijbehorende filmposters laten ophalen in uw speler

# Tags

- Het tag-gedeelte in Radarr wordt gebruikt om verschillende aspecten van Radarr met elkaar te verbinden. Ze zijn ook handig om bij te houden welke films afkomstig zijn van welke lijsten.
- Tags zijn met name handig voor:

  - Vertragingprofielen
  - Beperkingen
  - Indexers

- Tags kunnen worden gebruikt om Vertragingprofielen, Indexers en Beperkingen en Films met elkaar te verbinden.
- Bijvoorbeeld:
  - U wilt dat een specifieke indexer alleen wordt gebruikt voor een specifieke film. U zou een tag maken en de film en indexer aan die tag toewijzen.
  - U wilt dat een specifieke Beperking alleen van toepassing is op een specifieke film. U zou een tag maken en de Beperking en Film aan die tag toewijzen.
  - Dit proces is hetzelfde voor Vertragingprofielen.

> Een film zal zowel indexers gebruiken met overeenkomende tags als indexers zonder tags.
{.is-warning}

> Opmerking: Tags hebben geen invloed op "Aangepaste indelingen", "Kwaliteitsprofielen" of andere aspecten die hierboven niet worden genoemd.
{.is-info}

# Algemeen

## Host

- Bind Adres - Geldig IPv4-adres of '*' voor alle interfaces
  - 0.0.0.0 of `*` - elk adres kan verbinding maken
  - 127.0.0.1 of localhost - alleen lokale toepassingen kunnen verbinding maken
  - Elk ander IP (bijv. 1.2.3.4) - alleen dat IP (1.2.3.4) kan verbinding maken
- Poortnummer - Het poortnummer dat u wilt gebruiken om toegang te krijgen tot de webUI voor Radarr

> Opmerking: Als u Docker gebruikt, raak deze instelling dan niet aan.
{.is-warning}

- URL-basis - Voor ondersteuning van omgekeerde proxy, standaard leeg

> Opmerking: Als u een omgekeerde proxy gebruikt (bijvoorbeeld mydomain.com/radarr), voert u '/radarr' in voor URL-basis.
{.is-info}

- SSL inschakelen - Als u SSL-inloggegevens heeft en de communicatie naar en van uw Radarr wilt beveiligen, schakel dan deze optie in.

> Opmerking: Gebruik dit niet tenzij u weet wat u doet.
{.is-warning}

## Beveiliging

- Authenticatie - Hoe wilt u authenticeren om toegang te krijgen tot uw Radarr-instantie
  - Vanaf Radarr v5 is authenticatie nu verplicht. [Zie de verplichte authenticatie FAQ voor meer informatie.](/radarr/faq#forced-authentication)
  - ~~Geen - U heeft geen authenticatie om toegang te krijgen tot uw Radarr. Meestal als u de enige gebruiker van uw netwerk bent, niemand op uw netwerk heeft die toegang tot uw Radarr zou willen hebben of uw Radarr is niet blootgesteld aan het web~~
  - Basis (Browser pop-up) - Deze optie toont bij het openen van uw Radarr een klein pop-upvenster waarin u een gebruikersnaam en wachtwoord kunt invoeren
  - Formulieren (Aanmeldingspagina) - Deze optie heeft een vertrouwd uitziend aanmeldingsscherm, vergelijkbaar met andere websites, waarmee u kunt inloggen op uw Radarr
- API-sleutel - Hiermee kunnen andere programma's communiceren of Radarr communiceren met andere programma's. Deze sleutel kan, als deze in handen komt van de verkeerde persoon met toegang, allerlei dingen doen met uw bibliotheek. Daarom wordt de API-sleutel in de logboeken gecensureerd
- Certificaatvalidatie - Wijzig hoe strikt de validatie van HTTPS-certificaten is
  - Ingeschakeld - Valideer alle HTTPS-certificaten (aanbevolen)
  - Uitgeschakeld voor lokale adressen - Valideer alle HTTPS-certificaten behalve die op localhost en het LAN
  - Uitgeschakeld - Valideer geen enkel HTTPS-certificaat
  
## Proxy

Proxy - Met deze optie kunt u de informatie die uw Radarr ophaalt en doorzoekt via een proxy laten lopen. Dit kan handig zijn als u zich in een land bevindt dat het downloaden van torrentbestanden niet toestaat

- Proxy gebruiken - Inschakelen om een proxy te gebruiken
- Proxytype - Selecteer uw proxytype (HTTPS, Socks4 of Socks5)
- Hostnaam - Voer de hostnaam van uw proxy in (inclusief http/https of een ander protocol)
- Poort - Voer de poort van uw proxy in
- Gebruikersnaam - Voer uw proxygebruikersnaam in indien van toepassing
- Wachtwoord - Voer uw proxys wachtwoord in indien van toepassing
- Genegeerde adressen - Voer een door komma's gescheiden lijst van adressen in die de proxy omzeilen
- Proxy omzeilen voor lokale adressen - Vink het vakje aan om de proxy te omzeilen voor lokale adressen. Lokale verzoeken worden geïdentificeerd door het ontbreken van een punt (.) in de URI, zoals <http://webserver/>, of toegang tot de lokale server, inclusief <http://localhost>, <http://loopback> of <http://127.0.0.1>. Wanneer dit niet is aangevinkt, worden alle internetverzoeken via de proxyserver gemaakt.

## Logboeken

- Logboekniveau - Waarschijnlijk een van de meest nuttige probleemoplossingstools
  - Info - Dit is de meest basale manier waarop Radarr informatie verzamelt. Dit bevat een zeer minimale hoeveelheid informatie in de logboeken. Dit logbestand bevat fatale, fout-, waarschuwings- en infovermeldingen.
  - Debug - Debug bevat alle informatie die Info bevat, plus meer informatie die nuttig kan zijn. Dit logbestand bevat fatale, fout-, waarschuwings-, info- en debugvermeldingen.
  - Trace - De meest geavanceerde en gedetailleerde logging op Radarr, Trace bevat alle informatie die is verzameld door Info en Debug en meer. Dit is het meest voorkomende type logboek dat wordt gevraagd bij het oplossen van problemen op Discord of Reddit. Als u hulp nodig heeft, selecteer dan uw logboek op Trace en voer de taak opnieuw uit die u problemen gaf om het logboek vast te leggen. Dit logbestand bevat fatale, fout-, waarschuwings-, info-, debug- en tracevermeldingen.

## Analyse

- Analyse - Stuur anonieme gebruiks- en foutinformatie naar de servers van Radarr (Servarr). Dit omvat informatie over uw browser, welke Radarr WebUI-pagina's u gebruikt, foutenrapportage, evenals OS- en runtimeversie. We zullen deze informatie gebruiken om functies en bugfixes te prioriteren.

## Updates

- (Geavanceerde optie) Branch - Dit is de branch van Radarr waarop u draait.
  - [Zie deze FAQ voor meer informatie](/radarr/faq#how-do-i-update-radarr)
- Automatisch - Updates automatisch downloaden en installeren. U kunt nog steeds installeren via Systeem: Updates. Opmerking: Windows-gebruikers worden altijd automatisch bijgewerkt.
- Mechanisme - Gebruik de ingebouwde updater van Radarr of een script
  - Ingebouwd - Gebruik de eigen updater van Radarr
  - Script - Laat Radarr het update-script uitvoeren
  - Docker - Werk Radarr niet bij vanuit de Docker, maar haal een gloednieuwe image op met de nieuwe update
- Script - Alleen zichtbaar wanneer Mechanisme is ingesteld op Script - Pad naar update-script
- Updateproces - Radarr zal het updatebestand downloaden, de integriteit ervan controleren en het naar een tijdelijke locatie extraheren en de gekozen methode aanroepen. Het updateproces wordt uitgevoerd onder dezelfde gebruiker als waar Radarr onder wordt uitgevoerd, het heeft toestemming nodig om de Radarr-bestanden bij te werken en Radarr te stoppen/starten.
- Ingebouwd - De ingebouwde methode zal Radarr-bestanden en -instellingen back-uppen, Radarr stoppen, de installatie bijwerken en Radarr starten. Als uw systeem het stoppen van Radarr niet aankan en automatisch probeert te herstarten, is het misschien beter om in plaats daarvan een script te gebruiken. Bij een storing wordt de vorige versie van Radarr opnieuw gestart.
- Script - Het script moet hetzelfde behandelen als de ingebouwde updater. Als u services wilt stoppen en starten (upstart/launchd/etc), moet u dat hier doen.

## Back-ups

- Het gedeelte back-up stelt u in staat om Radarr te vertellen hoe u back-ups wilt beheren

- (Geavanceerde optie) Map - Hiermee kunt u de back-uplocatie selecteren. In Docker bent u beperkt tot wat de container kan zien. Padnamen zijn relatief ten opzichte van de appdata-map; indien nodig kunt u een absoluut pad instellen om buiten de appdata-map een back-up te maken.
- (Geavanceerde optie) Interval - Hoe vaak wilt u dat Radarr een back-up maakt
- (Geavanceerde optie) Retentie - Hoe lang wilt u dat Radarr elke back-up bewaart. Na het maken van een nieuwe back-up wordt de oudste back-up verwijderd

> Handmatige back-ups worden voor altijd bewaard, opgeslagen in dezelfde map en hebben een andere naam.
{.is-info}

# UI

## Kalender

- Eerste dag van de week - Hier kunt u selecteren wat volgens u de eerste dag van de week moet zijn.
- Kolomkop van de week - Hier kunt u de kop voor de kolommen selecteren

## Films

- Indeling looptijd - Selecteer hoe u looptijden wilt weergeven, als uren en minuten of minuten

## Datums

- Korte datumnotatie - Hoe wilt u dat Radarr korte datums weergeeft?
- Lange datumnotatie - Hoe wilt u dat Radarr lange datums weergeeft?
- Tijdnotatie - Wilt u een 12-uurs of 24-uurs formaat?
- Relatieve datums weergeven - Wilt u dat Radarr relatieve (Vandaag/Gisteren/etc) of absolute datums weergeeft?

## Stijl

- Kleurenblindmodus inschakelen - Gewijzigde stijl om kleurenblinde gebruikers in staat te stellen kleurgecodeerde informatie beter te onderscheiden

## Taal

- Taal van filminfo - Selecteer de taal waarin Radarr filminformatie in de UI weergeeft
- UI-taal - Selecteer de taal die Radarr in de applicatie-UI gebruikt