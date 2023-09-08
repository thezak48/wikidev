---
title: Användbara verktyg
description: 
published: true
date: 2023-08-28T09:19:27.683Z
tags: useful-tools
editor: markdown
dateCreated: 2021-06-05T20:51:53.183Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Återställning av en korrupt databas](#återställning-av-en-korrupt-databas)
  - [Återställning av en korrupt databas (UI) (Windows)](#återställning-av-en-korrupt-databas-ui-windows)
  - [Kommandoradsåterställning av databas](#kommandoradsåterställning-av-databas)
- [Hitta kakor](#hitta-kakor)
  - [Chrome](#chrome)
  - [Firefox](#firefox)
- [Rensa kakor och lokal lagring](#rensa-kakor-och-lokal-lagring)
  - [Chrome](#chrome-1)
  - [Firefox](#firefox-1)
  - [Microsoft Edge (Chromium)](#microsoft-edge-chromium)
  {.links-list}
- [Andra projekt och program - Begär appar \*Arrs](#andra-projekt-och-program-begär-appar-arrs)
  - [Notifiarr](#notifiarr-fka-discord-notifier)
  - [Ombi](#ombi)
  - [Overseerr](#overseerr)
  - [Petio](#petio)
  {.links-list}
- [Andra projekt och program - \*Arr Relaterade](#andra-projekt-och-program-arr-relaterade)
  - [Fjärrkontroll](#fjärrkontroll)
    - [LunaSea](#lunasea)
    - [Radarr & Sonarr Companion - Android App](#radarr-sonarr-companion-android-app)
    - [nzb360 - Android App](#nzb360-android-app)
    {.links-list}
  - [Lidarr](#lidarr)
    - [AMD](#amd)
    - [AMVD](#amvd)
  - [Radarr](#radarr)
    - [AMTD](#amtd)
  - [Undertexter](#undertexter)
    - [Bazarr](#bazarr)
- [Andra projekt och program - Torrents/Nedladdning](#andra-projekt-och-program-torrentsnedladdning)
  - [Cross-Seed](#cross-seed)
  - [Unpackerr](#unpackerr)
  - [qBit Management](#qbit-management)
- [Andra projekt och program](#andra-projekt-och-program)
  - [Filebot](#filebot)
  - [JDupes](#jdupes)
  - [Just A Bunch Of Starr Scripts](#just-a-bunch-of-starr-scripts)
  - [Just A Bunch Of Plex Scripts (JBOPS)](#just-a-bunch-of-plex-scripts)
  - [Plex Meta Manager](#plex-meta-manager)
  - [Tautulli](#tautulli)
  - [Tdarr](#tdarr)
  - [tdarr_inform](#tdarr_inform)
  {.links-list}
- [Anslutningsinstruktioner för Twitter](#anslutningsinstruktioner-för-twitter)

Följande appar är komplement till \*Arr Suite of Applications eller mediahoarding generellt. De underhålls, utvecklas och stöds inte av \*Arr Development Team. Vänligen rikta eventuella specifika supportfrågor till respektive applikationsutvecklingsteam.

# Återställning av en korrupt databas

Observera att applikationens databas kan hittas i Application Data Directory som är länkade nedan. Katalogen kan också passeras som ett datadir-argument.

- [Lidarr Appdata Directory](/lidarr/appdata-directory)
- [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- [Radarr Appdata Directory](/radarr/appdata-directory)
- [Readarr Appdata Directory](/readarr/appdata-directory)
- [Sonarr Appdata Directory](/sonarr/appdata-directory)
{.links-list}

> Det finns två alternativ för att återställa databasen som listas nedan.{.is-info}

- [Använda DB Browser for SQLite och använda UI](#återställning-av-en-korrupt-db-ui)
- [Använda Sqlites `.recover`-funktion](#kommandoradsåterställning-av-databas)
{.links-list}

## Återställning av en korrupt databas (UI) (Windows)

{#windows}
{#återställning-av-en-korrupt-db-ui}

> Observera att detta i princip gör samma sak som `.recover` som kräver Sqlite v3.29 | [Se Sqlites dokumentation för mer information om kommandot `.recover`](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database). Stegen för att göra detta är länkade nedan {.is-info}

> [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/) är ett högkvalitativt, visuellt, öppen källkod-verktyg för att skapa, designa och redigera databasfiler som är kompatibla med SQLite. DB4S är för användare och utvecklare som vill skapa, söka och redigera databaser. DB4S använder ett bekant gränssnitt som liknar ett kalkylblad, och komplicerade SQL-kommandon behöver inte läras sig.
{.is-info}

1. Stoppa applikationen
1. Gör en kopia av din korrupta databas (`.db`) och kopiera med eventuella `.shm` och `.wal`-filer
1. Öppna din korrupta databas i [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/)
1. Fil => Exportera => Exportera databas till SQL-fil
1. Välj alla tabeller
1. Markera/aktivera "Behåll kolumnnamn i INSERT INTO"
1. Exportera allt
1. Skriv över gammalt schema
1. Spara
1. Stäng databasen
1. Ny databas => Fil => Importera => importera den filen från föregående exportsteg
1. Vid eventuella importfel eller begränsningsproblem, rensa upp det problematiska infogningssatsen om möjligt eller ta bort den
1. Kör följande SQL `VACUUM;`
1. Spara databasen när du uppmanas.
1. Verktyg => Integritetskontroll; resultatet bör säga OK
1. Stäng databasen
1. Ta bort alla `wal`, `shm` och `db`-filer från konfigurationsmappen
1. Spara (eller kopiera, om \*Arr inte är på samma system som DB4S) den nya databasen i konfigurationsmappen och peka applikationen på den. Alla \*Arrs namnger sin databas som `<appnamn>.db` t.ex. `radarr.db`
1. Rätta till behörigheterna för den återställda databasen om det behövs. Ägaren bör vara användaren och gruppen som \*Arr är konfigurerad att köras som.
1. Starta applikationen

Observera att gif-filen inte täcker kommandot `VACUUM;`

![dbrecover.gif](/dbrecover.gif)

## Kommandoradsåterställning av databas

{#nix}

Följande instruktioner är för \*Nix-operativsystem, men konceptet kommer att vara liknande i Windows-kommandoraden.

> Detta använder [sqlite3 `.recover`-kommandot](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database) och är idealiskt. Observera att det kräver Sqlite 3.29+
{.is-info}

> Eftersom sqlite3 krävs av \*Arrs antas det att du har sqlite3 installerat på ditt system {.is-info}

1. Stoppa applikationen
1. SSH:a in på din server eller på annat sätt öppna en terminal
1. Skriv `sqlite3 <sökväg till den korrupta databasen> ".recover" | sqlite3 <sökväg till den återställda databasen>`
1. Rätta till behörigheterna för den återställda databasen om det behövs. Ägaren bör vara användaren och gruppen som \*Arr är konfigurerad att köras som.
1. Ta bort eller flytta/ändra namn på den gamla korrupta databasen och eventuella `wal`- eller `shm`-filer i mappen
1. Byt namn på den återställda databasen. Alla \*Arrs namnger sin databas som `<appnamn>.db` t.ex. `radarr.db`
1. Starta applikationen

# Hitta kakor

- Vissa webbplatser kan inte loggas in automatiskt och kräver att du loggar in manuellt och sedan ger kakorna för att fungera. Sidorna nedan beskriver hur du gör det.

## Allmänna instruktioner

1. Logga in på webbplatsen med din webbläsare med hjälp av den webbadress du har valt att använda från Prowlarr indexer-konfigurationen
1. Öppna DevTools-panelen genom att trycka på F12
1. Välj fliken Nätverk
1. Klicka på knappen Doc (Chrome-webbläsare) eller HTML (Firefox-webbläsare)
1. Uppdatera sidan genom att trycka på F5
1. Klicka på den första radposten
1. Välj fliken Headers i den högra panelen
1. Hitta 'cookie:' i avsnittet Request Headers. Se hjälptexten inom UI för din tracker för detaljer
1. Markera och kopiera hela kaksträngen (allt efter cookie: )
1. Ta bort allt som redan finns i Prowlarr indexer-konfigurationens kakefält
1. Klistra in den kopierade kaksträngen i det fältet
1. Klicka på Spara

> Om användaragent krävs för din tracker kan den hittas i Request Headers
{.is-info}

### Anteckningar

- Se till att använda webbläsaren från samma dator som kör Prowlarr, eftersom kakor sällan fungerar från andra plattformar.
- På inloggningssidan för webbplatsen, bocka inte i några alternativ som begränsar din session till en IP-adress eller logga ut efter en kort tid. Om det finns ett alternativ att Kom ihåg mig, använd det.
- Se till att du innan du hämtar kakan kan komma åt webbplatsens torrentsöksida, eftersom allt som webbplatsen gör för att förhindra detta (aviseringar, olästa meddelanden eller olästa PM eller en varning om låg förhållande) kommer att stoppa Prowlarr från att ha ett framgångsrikt test efter att ha använt kakan.

## Chrome

- Gå till torrentspårarens webbplats och logga in.

- Tryck på F12

- Under fliken Application längst upp finns "Storage" på vänster sida. Du kommer att se en del som heter "Cookies", och under den kommer du att se din spårarens URL. Klicka på den.

- Klicka på "Pass" på den fliken eller en liknande post, och det kommer att dyka upp en ruta som säger "Cookie Value" med en sträng på cirka 25-30 tecken. Kopiera det och klistra in det i applikationen som behöver det.

  - Om strängen ser liknande ut som `cid=cid-that-you-got-from-the-browser; sid=sid-that-you-got-from-the-browser` bör hela posten användas.

![cookie_chrome.png](/assets/prowlarr/cookie_chrome.png)

- Du kan också hänvisa till Chromes dokument [Chrome cookies](https://developer.chrome.com/docs/devtools/storage/cookies/)

## Firefox

- [Se Mozillas dokumentation](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Cookies)

![faq_3_cookies.png](/assets/general/faq_3_cookies.png)

# Rensa kakor och lokal lagring

## Chrome

1. Gå till `chrome://settings/siteData`
1. Skriv in webbplatsens (eller appens) namn som du vill rensa
1. Klicka på papperskorgen bredvid webbplatsen

## Firefox

- Se [Mozillas hjälpartikel](https://support.mozilla.org/en-US/kb/clear-cookies-and-site-data-firefox)

## Microsoft Edge (Chromium)

1. Gå till `edge://settings/siteData`
1. Skriv in webbplatsens (eller appens) namn som du vill rensa
1. Klicka på pilen bredvid webbplatsen
1. Klicka på papperskorgen bredvid webbplatsen

# Andra projekt och program - Begär appar \*Arrs

## Notifiarr (fka Discord Notifier)

[Notifiarr](https://notifiarr.com/) är ett verktyg skapat för att underlätta mer detaljerade Discord-notifikationer av en av \*Arrs utvecklare. Det ger ett konfigurerbart sätt att lägga till notifikationer (inklusive reaktioner) baserat på de utlösare du väljer. Webbplatsen erbjuder ett användargränssnitt för att välja vad som ska visas i notifikationen. Inkluderar stöd för Grab, Import, Upgrade, Health och Failed-notifikationer samt mycket mer.

[Wiki](https://notifiarr.wiki/)

Höjdpunkter

- Applikationsstatus
- Begäranden och godkännanden (\~Ombi)
- Anpassningsbara *ARR-applikationsnotifikationer
- Begärandesystem med godkännanden
- Följsystem för användare att övervaka en serie eller film och bli notifierade (via @mentions)
- Serverstatus
- Frekventa nya funktioner

## Ombi

[Ombi](https://github.com/tidusjar/Ombi/) ger användarna möjlighet att begära filmer, tv-serier (serier, säsonger eller enskilda avsnitt) och musikalbum.

## Overseerr

[Overseerr](https://overseerr.dev/) är ett verktyg för hantering av begäranden och upptäckt av media som är byggt för att fungera med din befintliga Plex-ekosystem.

## Petio

[Petio](https://petio.tv/) är en tredjeparts komplementapp till Plex-serverägare för att låta deras användare begära, granska och upptäcka innehåll.

Appen är utformad för att omedelbart kännas bekant och intuitiv även för de mest teknik-agnostiska användarna. Petio hjälper dig att hantera begäranden från dina användare, ansluta till andra tredjepartsappar som Sonarr och Radarr, meddela användare när innehåll är tillgängligt och spåra begärandens framsteg. Petio låter också användare upptäcka media både på och utanför din server, snabbt och enkelt hitta relaterat innehåll och lämna sin åsikt för andra användare.

# Andra projekt och program - \*Arr Relaterade

## Fjärrkontroll

### LunaSea

[LunaSea](https://www.lunasea.app/) är en helt utrustad, öppen källkod, självhostad kontroller! Fokuserad på att ge dig en sömlös upplevelse mellan all din självhostade mediasoftware

### Radarr & Sonarr Companion - Android App

Lägg till nya filmer/serier i ditt system enkelt med din telefon. Appen finns på [Google Play](https://play.google.com/store/apps/details?id=easy.radarr)

### nzb360 - Android App

nzb360 hanterar Sonarr, Radarr, Lidarr, torrents, usenet och andra tjänster. Appen finns på [Google Play](https://play.google.com/store/apps/details?id=com.kevinforeman.nzb360) Kolla [officiell webbplats](https://nzb360.com/) för mer information.

## Lidarr

### AMD

[Automated Music Downloader](https://github.com/RandomNinjaAtk/docker-amd) RandomNinjaAtk/amd är ett Lidarr-kompanjonsskript för att automatiskt ladda ner musik till Lidarr

### AMVD

[Automated Music Video Downloader](https://github.com/RandomNinjaAtk/docker-amvd) RandomNinjaAtk/amvd är ett Lidarr-kompanjonsskript för att automatiskt ladda ner och tagga musikvideor för användning i andra videoapplikationer (plex/kodi/jellyfin/emby)

## Radarr

## AMTD

[Automated Movie Trailer Downloader](https://github.com/RandomNinjaAtk/docker-amtd) RandomNinjaAtk/amtd är ett Radarr-kompanjonsskript för att automatiskt ladda ner filmtrailers och extramaterial för användning i andra videoapplikationer (plex/kodi/jellyfin/emby)

## Undertexter

## Bazarr

[Bazarr](https://github.com/morpheus65535/bazarr) är en komplementapplikation till Sonarr och Radarr som hanterar och laddar ner undertexter baserat på dina krav.

# Andra projekt och program - Torrents/Nedladdning

## Cross-Seed

[Cross-Seed](https://github.com/mmgoodnow/cross-seed) är en app som är utformad för att hjälpa dig att ladda ner torrents som du kan korsa baserat på dina befintliga torrents. Den är utformad för att matcha konservativt för att minimera manuell intervention. Den stöder Jackett och Qbittorrent/rTorrent för närvarande.

## Toolbarr

[Toolbarr](https://github.com/Notifiarr/toolbarr) tillhandahåller en uppsättning verktyg för att lösa problem med Starr-applikationer. Toolbarr låter dig utföra olika åtgärder mot dina Starr-appar och deras SQLite3-databaser.

## Unpackerr

[Unpackerr](https://github.com/unpackerr/unpackerr) Denna applikation körs som en daemon på din nedladdningsserver. Den kontrollerar färdiga nedladdningar och packar upp dem så att \*Arr kan importera dem.

Det finns ett antal alternativ där ute för att packa upp och ta bort filer efter att din klient har laddat ner dem. Kaptenen gillade helt enkelt inte något av dem, så han skrev sin egen. Han ville ha en liten enda binär med rimlig loggning som kan packa upp nedladdade arkiv och städa upp röran efter att de har importerats.

## qBit Management

[qBit Management a.k.a. "qbit_manage"](https://github.com/StuffAnThings/qbit_manage) är ett program som används för att hantera din qBittorrent-instans, som:



- Tagga torrents baserat på spårarens URL (endast tagga torrents som inte har några taggar)
- Uppdatera kategorier baserat på sparad mapp
- Ta bort oregistrerade torrents (radera data och torrent om den inte korsfröas, annars kommer den bara att ta bort torrenten)
- Lägg automatiskt till korsfröade torrents i pausat läge (används i kombination med [korsfröningsskriptet](#cross-seed))
- Kontrollera pausade torrents sorterade efter minsta storlek och återuppta om de är färdiga
- Ta bort föräldralösa filer från din rotmapp som inte refereras av qBittorrent
- Tagga torrents som inte har några hårda länkar och tillåter valfri rensning för att ta bort dessa torrents och innehåll baserat på maximal ratio och/eller tid som de har seedats

# Andra projekt och program

## Filebot

[FileBot](https://www.filebot.net/) är det ultimata verktyget för att organisera och döpa om dina filmer, TV-serier och anime, samt hämta undertexter och konstverk. Det är smart och fungerar bara.

## JDupes

[Jdupes](https://github.com/jbruchon/jdupes) är ett program för att identifiera och vidta åtgärder på dubbla filer.

> TRaSH [har en guide](https://trash-guides.info/jdupes) också {.is-info}

- `jdupes -M -r "/data/tv/" "/data/tv/.torrents/"` <= detta skulle kontrollera dubbla filer och skriva ut en sammanfattning av resultaten

- `jdupes -L -r "/data/tv/" "/data/tv/.torrents/"` <= detta skulle återskapa dem som hårda länkar och därmed minska den använda dubbla utrymmet

## Just A Bunch Of Starr Scripts

- [Just A Bunch Of Starr Scripts](https://github.com/angrycuban13/Just-A-Bunch-Of-Starr-Scripts)
- [Upgradinatorr](https://github.com/angrycuban13/Scripts/blob/main/Upgradinatorr/README.md) är ett PowerShell-skript för att manuellt söka efter n objekt som inte är taggade med en specifik tagg i ditt Radarr/Sonarr-mediebibliotek. n är antalet objekt som detta skript kommer att söka efter, detta har fördelen att du inte överbelastar dina indexeringstjänster och blir avstängd :)

## Just A Bunch Of Plex Scripts

- [Just A Bunch Of Plex Scripts (JBOPS)](https://github.com/blacktwin/JBOPS)
- [TRaSH Guides JBOPS 4K Transcode Stopping with Tautulli](https://trash-guides.info/Plex/Tips/4k-transcoding/)

## Plex Meta Manager

[Plex Meta Manager (PMM)](https://github.com/meisnate12/Plex-Meta-Manager) är ett Python-skript för att uppdatera metadatainformation för filmer, TV-serier och samlingar samt automatiskt bygga samlingar.

## Tautulli

[Tautulli](https://tautulli.com/) är en tredjepartsapplikation som du kan köra bredvid din Plex Media Server för att övervaka aktivitet och spåra olika statistik. Dessa statistik inkluderar framför allt vad som har tittats på, vem som tittade på det, när och var de tittade på det, och hur det tittades på. Det enda som saknas är "varför de tittade på det", men vem är jag att ifrågasätta dina 42 visningar av Frost. Alla statistik presenteras i ett snyggt och rent gränssnitt med många tabeller och diagram, vilket gör det enkelt att skryta om din server för alla andra.

## Tdarr

[Tdarr](https://tdarr.io) är en sluten självhostad webbapp för automatisering av transkodning/remux-hantering av mediebibliotek och för att se till att dina filer är exakt som du behöver dem när det gäller codecs/strömmar/kontainrar etc. Designad för att fungera tillsammans med [Sonarr](/sonarr)/[Radarr](/radarr) och byggd med syftet att vara modulär, parallelliserad och skalbar, har varje bibliotek du lägger till sina egna transkodningsinställningar, filter och schema. Arbetare kan startas och stängas av vid behov och är uppdelade i tre typer - 'allmän', 'transkodning' och 'hälsokontroll'. Arbetargränser kan hanteras av schemaläggaren såväl som manuellt.

## tdarr_inform

[tdarr_inform](https://github.com/deathbybandaid/tdarr_inform) är ett anpassat skript för Sonarr och Radarr för att informera Tdarr om nya/ändrade/borttagna filer utan att förlita sig på filsystemhändelser eller frekvent skanning av disken.

## Deleterr

[Deleterr](https://github.com/rfsbraz/deleterr) är ett verktyg för att ta bort gamla och inaktiva medier från Plex/Sonarr/Radarr. Det hjälper till att hantera begränsat utrymme när du tillåter användare att begära program via Overseerr/Ombi men inte vill övervaka tillgängligt diskutrymme manuellt. Det är konfigurerbart för att bara ta bort medier som uppfyller dina definierade kriterier.

## Twitter Connect

Skapa en Twitter-applikation (om du inte redan har gjort det) på <https://apps.twitter.com/>

Fyll i de obligatoriska fälten samt callback-URL:en, ställ in den på en offentligt tillgänglig URL (inte localhost), den behöver inte existera, men den måste vara inställd, användning av <https://sonarr.tv/twitter> eller <https://radarr.video> är tillräckligt.