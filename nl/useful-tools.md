---
title: Handige Tools
description: 
published: true
date: 2023-08-28T09:19:27.683Z
tags: handige-tools
editor: markdown
dateCreated: 2021-06-05T20:51:53.183Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Herstellen van een beschadigde database](#herstellen-van-een-beschadigde-database)
  - [Herstellen van een beschadigde database (UI) (Windows)](#herstellen-van-een-beschadigde-database-ui-windows)
  - [Command Line Databaseherstel](#command-line-databaseherstel)
- [Cookies vinden](#cookies-vinden)
  - [Chrome](#chrome)
  - [Firefox](#firefox)
- [Cookies en lokale opslag wissen](#cookies-en-lokale-opslag-wissen)
  - [Chrome](#chrome-1)
  - [Firefox](#firefox-1)
  - [Microsoft Edge (Chromium)](#microsoft-edge-chromium)
  {.links-list}
- [Andere projecten en programma's - Verzoek-apps \*Arrs](#andere-projecten-en-programmas-verzoek-apps-arrs)
  - [Notifiarr](#notifiarr-fka-discord-notifier)
  - [Ombi](#ombi)
  - [Overseerr](#overseerr)
  - [Petio](#petio)
  {.links-list}
- [Andere projecten en programma's - \*Arr-gerelateerd](#andere-projecten-en-programmas-arr-gerelateerd)
  - [Afstandsbediening](#afstandsbediening)
    - [LunaSea](#lunasea)
    - [Radarr & Sonarr Companion - Android-app](#radarr-sonarr-companion-android-app)
    - [nzb360 - Android-app](#nzb360-android-app)
    {.links-list}
  - [Lidarr](#lidarr)
    - [AMD](#amd)
    - [AMVD](#amvd)
  - [Radarr](#radarr)
    - [AMTD](#amtd)
  - [Ondertitels](#ondertitels)
    - [Bazarr](#bazarr)
- [Andere projecten en programma's - Torrents/Downloaden](#andere-projecten-en-programmas-torrentsdownloaden)
  - [Cross-Seed](#cross-seed)
  - [Unpackerr](#unpackerr)
  - [qBit Management](#qbit-management)
- [Andere projecten en programma's](#andere-projecten-en-programmas)
  - [Filebot](#filebot)
  - [JDupes](#jdupes)
  - [Just A Bunch Of Starr Scripts](#just-a-bunch-of-starr-scripts)
  - [Just A Bunch Of Plex Scripts (JBOPS)](#just-a-bunch-of-plex-scripts)
  - [Plex Meta Manager](#plex-meta-manager)
  - [Tautulli](#tautulli)
  - [Tdarr](#tdarr)
  - [tdarr_inform](#tdarr_inform)
  {.links-list}
- [Twitter Connect-instructies](#twitter-connect-instructies)

De volgende apps zijn metgezellen van de \*Arr Suite of Applications of media-opslag in het algemeen. Ze worden niet onderhouden, ontwikkeld of ondersteund door het \*Arr Development Team. Richt specifieke ondersteuningsvragen aan het ontwikkelingsteam van de betreffende applicatie.

# Herstellen van een beschadigde database

Merk op dat de database van de applicatie te vinden is in de Application Data Directory, die hieronder is gelinkt. De map kan ook worden doorgegeven als een datadir-argument.

- [Lidarr Appdata Directory](/lidarr/appdata-directory)
- [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- [Radarr Appdata Directory](/radarr/appdata-directory)
- [Readarr Appdata Directory](/readarr/appdata-directory)
- [Sonarr Appdata Directory](/sonarr/appdata-directory)
{.links-list}

> Er zijn twee opties om de database te herstellen, die hieronder worden vermeld.{.is-info}

- [Gebruik DB Browser for SQLite en de UI](#herstellen-van-een-beschadigde-database-ui)
- [Gebruik de `.recover`-functie van Sqlite via de opdrachtregel](#command-line-databaseherstel)
{.links-list}

## Herstellen van een beschadigde database (UI) (Windows)

{#windows}
{#herstellen-van-een-beschadigde-database-ui}

> Merk op dat dit in feite hetzelfde doet als `.recover`, wat Sqlite v3.29 vereist. [Raadpleeg de Sqlite-documentatie voor meer details over de `.recover`-opdracht](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database). De stappen om dit te doen, zijn hieronder gelinkt {.is-info}

> [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/) is een hoogwaardige, visuele, open source tool om databasebestanden te maken, ontwerpen en bewerken die compatibel zijn met SQLite. DB4S is bedoeld voor gebruikers en ontwikkelaars die databases willen maken, doorzoeken en bewerken. DB4S maakt gebruik van een vertrouwde interface zoals een spreadsheet en er hoeven geen ingewikkelde SQL-opdrachten te worden geleerd.
{.is-info}

1. Stop de applicatie
1. Maak een kopie van uw beschadigde database (`.db`) en kopieer eventuele `.shm`- en `.wal`-bestanden mee
1. Open uw beschadigde database in [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/)
1. Bestand => Exporteren => Database exporteren naar SQL-bestand
1. Selecteer alle tabellen
1. Vink "Kolomnamen behouden in INSERT INTO" aan
1. Alles exporteren
1. Oude schema overschrijven
1. Opslaan
1. Sluit de database
1. Nieuwe database => Bestand => Importeren => importeer het bestand van de vorige exportstap
1. Bij eventuele importfouten of beperkingen, repareer de problematische invoegingsverklaring indien mogelijk of verwijder deze
1. Voer de volgende SQL uit: `VACUUM;`
1. Sla de database op wanneer daarom wordt gevraagd.
1. Gereedschap => Integriteitscontrole; het resultaat moet OK zeggen
1. Sluit de database
1. Verwijder alle `wal`, `shm` en `db`-bestanden uit de configuratiemap
1. Sla (of kopieer, als \*Arr niet op hetzelfde systeem als DB4S staat) de nieuwe database op in de configuratiemap en wijs de applicatie daarnaar toe. Alle \*Arrs noemen hun database `<appname>.db`, bijvoorbeeld `radarr.db`
1. Corrigeer de machtigingen voor de herstelde database indien nodig. De eigenaar moet de gebruiker en groep zijn waarmee \*Arr is geconfigureerd om uit te voeren.
1. Start de applicatie

Let op: de gif dekt het `VACUUM;`-commando niet af

![dbrecover.gif](/dbrecover.gif)

## Command Line Databaseherstel

{#nix}

De onderstaande instructies zijn voor \*Nix-besturingssystemen, maar het concept zal vergelijkbaar zijn op de Windows-opdrachtregel.

> Dit maakt gebruik van de [sqlite3 `.recover`-opdracht](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database) en is ideaal. Merk op dat Sqlite 3.29+ vereist is.
{.is-info}

> Aangezien sqlite3 vereist is door \*Arrs, wordt ervan uitgegaan dat u sqlite3 geïnstalleerd heeft op uw systeem {.is-info}

1. Stop de applicatie
1. Maak verbinding met uw server via SSH of open een shell op een andere manier
1. Voer `sqlite3 <pad naar beschadigde database> ".recover" | sqlite3 <uitvoerpad voor herstelde database>"` in
1. Corrigeer de machtigingen voor de herstelde database indien nodig. De eigenaar moet de gebruiker en groep zijn waarmee \*Arr is geconfigureerd om uit te voeren.
1. Verwijder of verplaats/hernoem de oude beschadigde database en eventuele `wal`- of `shm`-bestanden in de map
1. Hernoem de herstelde database. Alle \*Arrs noemen hun database `<appname>.db`, bijvoorbeeld `radarr.db`
1. Start de applicatie

# Cookies vinden

- Sommige sites kunnen niet automatisch worden ingelogd en vereisen dat u handmatig inlogt en vervolgens de cookies doorgeeft om te kunnen werken. De onderstaande pagina's beschrijven hoe u dat kunt doen.

## Algemene instructies

1. Log in op de website met uw browser met behulp van het gekozen Site Link-adres uit de Prowlarr-indexerconfiguratie
1. Open het DevTools-paneel door op F12 te drukken
1. Selecteer het tabblad Netwerk
1. Klik op de knop Doc (Chrome-browser) of HTML (Firefox-browser)
1. Vernieuw de pagina door op F5 te drukken
1. Klik op de eerste rijvermelding
1. Selecteer het tabblad Headers in het rechterpaneel
1. Zoek 'cookie:' in het gedeelte Request Headers. Raadpleeg de helptekst binnen de UI van uw tracker voor meer informatie
1. Selecteer en kopieer de volledige cookiestring (alles na de cookie:)
1. Verwijder alles wat al in het cookievak van de Prowlarr-indexerconfiguratie staat
1. Plak de gekopieerde cookiestring in dat vak
1. Klik op Opslaan

> Als de gebruikersagent vereist is voor uw tracker, is deze te vinden in de Request Headers
{.is-info}

### Opmerkingen

- Zorg ervoor dat u de browser van dezelfde machine gebruikt waarop Prowlarr wordt uitgevoerd, omdat cookies zelden werken vanaf andere platforms.
- Op de inlogpagina van de website moet u geen opties aanvinken die uw sessie beperken tot één IP-adres of uitloggen na korte tijd. Als er een optie "Onthoud mij" is, gebruik deze dan.
- Zorg ervoor dat u voordat u de cookie ophaalt, toegang heeft tot de torrentzoekpagina van de site, omdat alles wat de site doet om dit te voorkomen (waarschuwingen, ongelezen berichten of ongelezen PM, of een waarschuwing voor een lage ratio) Prowlarr zal stoppen om een succesvolle test uit te voeren na het gebruik van de cookie.

## Chrome

- Ga naar de website van de torrenttracker en log in.

- Druk op F12

- Onder het tabblad Toepassing bovenaan staat "Opslag" aan de linkerkant. U ziet een subsectie "Cookies" en daaronder ziet u de URL van uw tracker. Klik daarop.

- Klik op "Pass" op dat tabblad of een vergelijkbare vermelding, en er verschijnt een venster met de tekst "Cookie Value" met een tekenreeks van ongeveer 25-30 tekens lang. Kopieer dat en plak het in de toepassing die het nodig heeft.

  - Als de tekenreeks er ongeveer uitziet als `cid=cid-that-you-got-from-the-browser; sid=sid-that-you-got-from-the-browser`, moet de hele vermelding worden gebruikt.

![cookie_chrome.png](/assets/prowlarr/cookie_chrome.png)

- U kunt ook de documentatie van Chrome raadplegen [Chrome cookies](https://developer.chrome.com/docs/devtools/storage/cookies/)

## Firefox

- [Raadpleeg de documentatie van Mozilla](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Cookies)

![faq_3_cookies.png](/assets/general/faq_3_cookies.png)

# Cookies en lokale opslag wissen

## Chrome

1. Ga naar `chrome://settings/siteData`
1. Voer de naam van de site (of app) in die u wilt wissen
1. Klik op het prullenbakpictogram voor de site

## Firefox

- Raadpleeg [het helpartikel van Mozilla](https://support.mozilla.org/en-US/kb/clear-cookies-and-site-data-firefox)

## Microsoft Edge (Chromium)

1. Ga naar `edge://settings/siteData`
1. Voer de naam van de site (of app) in die u wilt wissen
1. Klik op de pijl voor de site
1. Klik op het prullenbakpictogram voor de site

# Andere projecten en programma's - Verzoek-apps \*Arrs

## Notifiarr (fka Discord Notifier)

[Notifiarr](https://notifiarr.com/) is een tool die is gemaakt om gedetailleerde Discord-meldingen te faciliteren door een van de \*Arr-ontwikkelaars. Het biedt een configureerbare manier om meldingen (inclusief reacties) toe te voegen op basis van door u gekozen triggers. De website biedt een UI om te kiezen wat er in de melding moet worden weergegeven. Het omvat ondersteuning voor meldingen van Grab, Import, Upgrade, Health en Failed, en nog veel meer.

[Wiki](https://notifiarr.wiki/)

Hoogtepunten

- Applicatiestatus
- Verzoeken en goedkeuringen (\~Ombi)
- Aanpasbare meldingen voor \*ARR-applicaties
- Verzoeksysteem met goedkeuringen
- Volgsysteem voor gebruikers om een serie of film te volgen en meldingen te ontvangen (via @mentions)
- Serverstatus
- Regelmatig nieuwe functies

## Ombi

[Ombi](https://github.com/tidusjar/Ombi/) geeft gebruikers de mogelijkheid om films, tv-shows (series, seizoenen of afzonderlijke afleveringen) en muziekalbums aan te vragen.

## Overseerr

[Overseerr](https://overseerr.dev/) is een tool voor verzoekbeheer en media-ontdekking die is ontwikkeld om te werken met uw bestaande Plex-ecosysteem.

## Petio

[Petio](https://petio.tv/) is een externe metgezel-app die beschikbaar is voor eigenaren van Plex-servers om hun gebruikers in staat te stellen content aan te vragen, te beoordelen en te ontdekken.

De app is ontworpen om direct vertrouwd en intuïtief te zijn, zelfs voor de meest technisch-agnostische gebruikers. Petio helpt u bij het beheren van verzoeken van uw gebruikers, maakt verbinding met andere apps van derden zoals Sonarr en Radarr, meldt gebruikers wanneer content beschikbaar is en volgt de voortgang van verzoeken. Petio stelt gebruikers ook in staat om media zowel op als buiten uw server te ontdekken, snel en gemakkelijk gerelateerde inhoud te vinden en recensies achter te laten voor andere gebruikers.

# Andere projecten en programma's - \*Arr-gerelateerd

## Afstandsbediening

### LunaSea

[LunaSea](https://www.lunasea.app/) is een volledig uitgeruste, open source self-hosted controller! Gericht op een naadloze ervaring tussen al uw self-hosted mediasoftware.

### Radarr & Sonarr Companion - Android-app

Voeg eenvoudig nieuwe films/series toe aan uw systeem met uw telefoon. App beschikbaar op [Google Play](https://play.google.com/store/apps/details?id=easy.radarr)

### nzb360 - Android-app

nzb360 biedt beheer van Sonarr, Radarr, Lidarr, torrents, usenet en andere services. App beschikbaar op [Google Play](https://play.google.com/store/apps/details?id=com.kevinforeman.nzb360) Bekijk [de officiële website](https://nzb360.com/) voor meer informatie.

## Lidarr

### AMD

[Automated Music Downloader](https://github.com/RandomNinjaAtk/docker-amd) RandomNinjaAtk/amd is een Lidarr-companion-script om automatisch muziek te downloaden voor Lidarr

### AMVD

[Automated Music Video Downloader](https://github.com/RandomNinjaAtk/docker-amvd) RandomNinjaAtk/amvd is een Lidarr-companion-script om automatisch muziekvideo's te downloaden en te taggen voor gebruik in andere videotoepassingen (plex/kodi/jellyfin/emby)

## Radarr

## AMTD

[Automated Movie Trailer Downloader](https://github.com/RandomNinjaAtk/docker-amtd) RandomNinjaAtk/amtd is een Radarr-companion-script om automatisch filmtrailers en extra's te downloaden voor gebruik in andere videotoepassingen (plex/kodi/jellyfin/emby)

## Ondertitels

## Bazarr

[Bazarr](https://github.com/morpheus65535/bazarr) is een metgezeltoepassing voor Sonarr en Radarr die ondertitels beheert en downloadt op basis van uw vereisten.

# Andere projecten en programma's - Torrents/Downloaden

## Cross-Seed

[Cross-Seed](https://github.com/mmgoodnow/cross-seed) is een app die is ontworpen om u te helpen torrents te downloaden die u kunt kruiszaaien op basis van uw bestaande torrents. Het is ontworpen om conservatief overeen te komen om handmatige interventie tot een minimum te beperken. Het ondersteunt Jackett en Qbittorrent/rTorrent op dit moment.

## Toolbarr

[Toolbarr](https://github.com/Notifiarr/toolbarr) biedt een reeks hulpprogramma's om problemen met Starr-applicaties op te lossen. Met Toolbarr kunt u verschillende acties uitvoeren tegen uw Starr-apps en hun SQLite3-databases.

## Unpackerr

[Unpackerr](https://github.com/unpackerr/unpackerr) Deze applicatie draait als een daemon op uw downloadhost. Het controleert voltooide downloads en pakt ze uit zodat \*Arr ze kan importeren.

Er zijn een handvol opties beschikbaar om bestanden uit te pakken en te verwijderen nadat uw client ze heeft gedownload. Captain vond geen van hen echter prettig, dus hij heeft zijn eigen programma geschreven. Hij wilde een kleine single-binary met redelijke logging die gedownloade archieven kan uitpakken en de rommel kan opruimen nadat ze zijn geïmporteerd.

## qBit Management

[qBit Management, ook wel "qbit_manage" genoemd](https://github.com/StuffAnThings/qbit_manage), is een programma dat wordt gebruikt om uw qBittorrent-instantie te beheren, zoals:

- Tag torrents op basis van tracker-URL (alleen torrents taggen die geen tags hebben)
- Categorieën bijwerken op basis van opslagmap
- Verwijder niet-geregistreerde torrents (verwijder gegevens en torrent als deze niet wordt gekruist, anders wordt alleen de torrent verwijderd)
- Voeg automatisch cross-seed torrents toe in gepauzeerde staat (gebruikt in combinatie met het [cross-seed script](#cross-seed))
- Controleer gepauzeerde torrents opnieuw, gesorteerd op kleinste grootte, en hervat als ze voltooid zijn
- Verwijder weesbestanden uit uw hoofdmap die niet worden verwezen door qBittorrent
- Tag torrents die geen harde links hebben en optionele opruiming toestaan om deze torrents en inhoud te verwijderen op basis van maximale ratio en/of tijd dat ze gezaaid zijn

# Andere projecten en programma's

## Filebot

[FileBot](https://www.filebot.net/) is de ultieme tool voor het organiseren en hernoemen van uw films, tv-shows en anime, evenals het ophalen van ondertitels en artwork. Het is slim en werkt gewoon.

## JDupes

[Jdupes](https://github.com/jbruchon/jdupes) is een programma om dubbele bestanden te identificeren en acties te ondernemen.

> TRaSH [heeft een handleiding](https://trash-guides.info/jdupes) ook {.is-info}

- `jdupes -M -r "/data/tv/" "/data/tv/.torrents/"` <= dit controleert op dubbele bestanden en geeft een samenvatting van de resultaten weer

- `jdupes -L -r "/data/tv/" "/data/tv/.torrents/"` <= dit maakt ze opnieuw aan als harde links, waardoor de gebruikte duplicatieruimte wordt verminderd

## Just A Bunch Of Starr Scripts

- [Just A Bunch Of Starr Scripts](https://github.com/angrycuban13/Just-A-Bunch-Of-Starr-Scripts)
- [Upgradinatorr](https://github.com/angrycuban13/Scripts/blob/main/Upgradinatorr/README.md) is een PowerShell-script om handmatig n items te zoeken die niet zijn getagd met een specifieke tag in uw Radarr/Sonarr-mediatheek. n is het aantal items waarop dit script zal zoeken, dit heeft als bijkomend voordeel dat u uw indexers niet overbelast en verbannen wordt :)

## Just A Bunch Of Plex Scripts

- [Just A Bunch Of Plex Scripts (JBOPS)](https://github.com/blacktwin/JBOPS)
- [TRaSH Guides JBOPS 4K Transcode Stopping with Tautulli](https://trash-guides.info/Plex/Tips/4k-transcoding/)

## Plex Meta Manager

[Plex Meta Manager (PMM)](https://github.com/meisnate12/Plex-Meta-Manager) is een Python-script om metagegevensinformatie voor films, shows en collecties bij te werken en automatisch collecties te bouwen.

## Tautulli

[Tautulli](https://tautulli.com/) is een applicatie van derden die u naast uw Plex Media Server kunt uitvoeren om activiteiten te monitoren en verschillende statistieken bij te houden. Belangrijker nog, deze statistieken omvatten wat er is bekeken, wie het heeft bekeken, wanneer en waar ze het hebben bekeken, en hoe het is bekeken. Het enige wat ontbreekt is "waarom ze het hebben bekeken", maar wie ben ik om je 42 keer Frozen te vragen. Alle statistieken worden gepresenteerd in een mooie en schone interface met veel tabellen en grafieken, waardoor het gemakkelijk is om op te scheppen over je server tegen iedereen.

## Tdarr

[Tdarr](https://tdarr.io) is een gesloten web-app voor het automatiseren van transcode/remux-beheer van mediatheek en ervoor zorgen dat uw bestanden precies zijn zoals u ze nodig heeft in termen van codecs/streams/containers, enz. Ontworpen om samen te werken met [Sonarr](/sonarr)/[Radarr](/radarr) en gebouwd met het oog op modularisatie, parallelisatie en schaalbaarheid, heeft elke bibliotheek die u toevoegt zijn eigen transcode-instellingen, filters en planning. Werkers kunnen worden opgestart en afgesloten indien nodig, en zijn onderverdeeld in 3 typen - 'algemeen', 'transcode' en 'gezondheidscontrole'. Werkergrenzen kunnen worden beheerd door de planner en ook handmatig.

## tdarr_inform

[tdarr_inform](https://github.com/deathbybandaid/tdarr_inform) is een aangepast script voor Sonarr en Radarr om Tdarr te informeren over nieuwe/gewijzigde/verwijderde bestanden zonder te vertrouwen op bestandssysteemgebeurtenissen of frequente schijfscans.

## Deleterr

[Deleterr](https://github.com/rfsbraz/deleterr) is een tool om verouderde en inactieve media te verwijderen uit Plex/Sonarr/Radarr. Het helpt bij het beheren van beperkte ruimte wanneer u gebruikers toestaat shows aan te vragen via Overseerr/Ombi, maar geen handmatige controle wilt uitvoeren op beschikbare schijfruimte. Het is configureerbaar om alleen media te verwijderen die voldoet aan uw gedefinieerde criteria.

## Twitter Connect

Maak een Twitter-applicatie aan (als je dat nog niet hebt gedaan) op <https://apps.twitter.com/>

Vul de verplichte velden in, evenals de callback-URL, stel deze in op een openbaar beschikbare URL (geen localhost), het hoeft niet te bestaan, maar het moet wel worden ingesteld, gebruik van <https://sonarr.tv/twitter> of <https://radarr.video> is voldoende.