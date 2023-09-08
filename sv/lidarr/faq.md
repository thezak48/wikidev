---
title: Lidarr FAQ
description: Vanliga frågor och svar om Lidarr
published: true
date: 2023-08-31T19:08:18.905Z
tags: lidarr, needs-love, faq
editor: markdown
dateCreated: 2021-06-14T14:33:41.344Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
  - [Hur fungerar Lidarr?](#hur-fungerar-lidarr)
  - [Hur hittar Lidarr släpp?](#hur-hittar-lidarr-släpp)
  - [Tvingad autentisering](#tvingad-autentisering)
  - [Hur jämförs möjliga nedladdningar?](#hur-jämförs-möjliga-nedladdningar)
  - [Lidarr slutade fungera efter att ha uppdaterat till Ubuntu 22.04](#lidarr-slutade-fungera-efter-att-ha-uppdaterat-till-ubuntu-2204)
  - [Varför kan jag inte lägga till en ny utgåva eller artist i Lidarr?](#varför-kan-jag-inte-lägga-till-en-ny-utgåva-eller-artist-i-lidarr)
  - [Varför kan jag inte lägga till ett album med olika artister?](#varför-kan-jag-inte-lägga-till-ett-album-med-olika-artister)
  - [Varför visar Lidarr bara studioalbum, hur hittar jag singlar eller EP-skivor?](#varför-visar-lidarr-bara-studioalbum-hur-hittar-jag-singlar-eller-ep-skivor)
  - [Kan jag bara lägga till ett album?](#kan-jag-bara-lägga-till-ett-album)
  - [Kan jag ladda ner enskilda låtar?](#kan-jag-ladda-ner-enskilda-låtar)
  - [Varför visas inte artisten X i sökresultaten?](#varför-visas-inte-artisten-x-i-sökresultaten)
  - [Lidarr matchade ett album med för många låtar. Hur kan jag ändra albumet till rätt utgåva?](#lidarr-matchade-ett-album-med-för-många-låtar-hur-kan-jag-ändra-albumet-till-rätt-utgåva)
  - [Jag kan inte hitta en utgåva i Lidarr men den finns på MusicBrainz](#jag-kan-inte-hitta-en-utgåva-i-lidarr-men-den-finns-på-musicbrainz)
  - [Hur ofta synkroniseras Lidarrs och MusicBrainz databaser?](#hur-ofta-synkroniseras-lidarrs-och-musicbrainz-databaser)
  - [Hur kan jag lägga till saknade artistbilder?](#hur-kan-jag-lägga-till-saknade-artistbilder)
  - [Hur kan jag få saknade albumbilder? (Omslag)](#hur-kan-jag-få-saknade-albumbilder-omslag)
  - [Jag har problem med att importera mina artister, vad kan det bero på?](#jag-har-problem-med-att-importera-mina-artister-vad-kan-det-bero-på)
  - [Hur kan jag döpa om mina artistmappar?](#hur-kan-jag-döpa-om-mina-artistmappar)
  - [Hur kan jag massradera artister från önskelistan?](#hur-kan-jag-massradera-artister-från-önskelistan)
  - [Varför fungerar inte Lidarr bakom en omvänd proxy](#varför-fungerar-inte-lidarr-bakom-en-omvänd-proxy)
  - [Hur uppdaterar jag Lidarr?](#hur-uppdaterar-jag-lidarr)
    - [Kan jag uppdatera Lidarr inuti min Docker-container?](#kan-jag-uppdatera-lidarr-inuti-min-docker-container)
    - [Installation av en nyare version](#installation-av-en-nyare-version)
      - [Lokal installation](#lokal-installation)
      - [Docker](#docker)
  - [Kan jag växla från `nightly` tillbaka till `develop`?](#kan-jag-växla-från-nightly-tillbaka-till-develop)
  - [Kan jag växla mellan grenar?](#kan-jag-växla-mellan-grenar)
  - [Jag får ett felmeddelande: Databasens diskavbildning är skadad](#jag-får-ett-felmeddelande-databasens-diskavbildning-är-skadad)
  - [Hur säkerhetskopierar/återställer jag min Lidarr?](#hur-säkerhetskopieraråterställer-jag-min-lidarr)
    - [Säkerhetskopiering av Lidarr](#säkerhetskopiering-av-lidarr)
      - [Använda inbyggd säkerhetskopiering](#använda-inbyggd-säkerhetskopiering)
      - [Använda filsystemet direkt](#använda-filsystemet-direkt)
    - [Återställning från säkerhetskopia](#återställning-från-säkerhetskopia)
      - [Använda zip-säkerhetskopia](#använda-zip-säkerhetskopia)
      - [Använda filsystemets säkerhetskopia](#använda-filsystemets-säkerhetskopia)
      - [Återställning av filsystemet på Synology NAS](#återställning-av-filsystemet-på-synology-nas)
  - [Jag använder Lidarr på en Mac och den slutade plötsligt fungera. Vad har hänt?](#jag-använder-lidarr-på-en-mac-och-den-slutade-plötsligt-fungera-vad-har-hänt)
  - [Jag använder en Pi och Raspbian och Lidarr startar inte](#jag-använder-en-pi-och-raspbian-och-lidarr-startar-inte)
  - [Varför tar det så lång tid att synkronisera listor och kan jag ändra det?](#varför-tar-det-så-lång-tid-att-synkronisera-listor-och-kan-jag-ändra-det)
  - [Kan jag inaktivera uppdatering av utgåvor?](#kan-jag-inaktivera-uppdatering-av-utgåvor)
  - [Varför kan inte Lidarr se mina filer på en fjärrserver?](#varför-kan-inte-lidarr-se-mina-filer-på-en-fjärrserver)
    - [Lidarr körs som standard under kontot LocalService som inte har åtkomst till skyddade fjärrfiler](#lidarr-körs-som-standard-under-kontot-localservice-som-inte-har-åtkomst-till-skyddade-fjärrfiler)
    - [Du använder en kartad nätverksenhet (inte en UNC-sökväg)](#du-använder-en-kartad-nätverksenhet-inte-en-unc-sökväg)
  - [Hjälp, jag har låst mig själv ute](#hjälp-jag-har-låst-mig-själv-ute)
  - [Hur stoppar jag webbläsaren från att starta vid uppstart?](#hur-stoppar-jag-webbläsaren-från-att-starta-vid-uppstart)
  - [Märkliga problem med användargränssnittet](#märkliga-problem-med-användargränssnittet)
  - [VPN, Jackett och \*ARRs](#vpn-jackett-och-arrs)
  - [Jacketts /all-endpunkt](#jacketts-all-endpunkt)
    - [Jackett /All-lösningar](#jackett-all-lösningar)
  - [Varför finns det två filer? | Varför finns det en fil kvar i nedladdningar?](#varför-finns-det-två-filer--varför-finns-det-en-fil-kvar-i-nedladdningar)
  - [Jag får ständiga varningar från min molnlagring om API-begränsningar](#jag-får-ständiga-varningar-från-min-molnlagring-om-api-begränsningar)

## Hur fungerar Lidarr?

- Lidarr använder RSS-flöden för att automatisera hämtning av släpp när de publiceras, både nya släpp och tidigare släppta släpp som publiceras eller återpubliceras. RSS-flödet är de senaste släppen från en webbplats, vanligtvis mellan 50 och 100 släpp, även om vissa webbplatser tillhandahåller fler eller färre. RSS-flödet består av alla nyligen tillgängliga släpp, inklusive släpp för efterfrågad media som du inte följer. Om du tittar på felsökningsloggar kommer du att se att dessa släpp bearbetas, vilket är helt normalt.
- Lidarr tvingar en minimumtid på 10 minuter för RSS-synkronisering och en maximal tid på 2 timmar. 15 minuter är det rekommenderade minimum av de flesta indexerare, även om vissa tillåter kortare intervall och 2 timmar säkerställer att Lidarr kontrollerar tillräckligt ofta för att inte missa ett släpp (även om den kan bläddra igenom RSS-flödet på många indexerare för att underlätta detta). Vissa indexerare tillåter klienter att utföra en RSS-synkronisering oftare än 10 minuter, i dessa scenarier rekommenderar vi att du använder Lidarrs Release-Push API-slutpunkt tillsammans med en IRC-kanal för att skicka släpp till Lidarr för bearbetning, vilket kan ske i nära realtid och med mindre belastning på indexeraren och Lidarr eftersom Lidarr inte behöver begära RSS-flödet för ofta och bearbeta samma släpp om och om igen.

## Hur hittar Lidarr släpp?

- Lidarr söker ''inte'' regelbundet efter albumfiler som saknas eller inte uppfyller sina kvalitetsmål. Istället frågar den dina indexerare och spårare ganska ofta efter ''alla'' nyligen publicerade släpp och jämför sedan det med sin lista över släpp som saknas eller behöver uppgraderas. Eventuella matchningar laddas ner. Detta gör att Lidarr kan täcka en bibliotek av ''vilken storlek som helst'' med endast 24-100 förfrågningar per dag (RSS-intervall på 15-60 minuter). Om du förstår detta kommer du att inse att det bara täcker ''framtidens'' släpp.
- Så hur hanterar du nuet och det förflutna? När du lägger till ett album måste du ange rätt sökväg, profil och övervakningsstatus och sedan använda kryssrutan Starta sökning efter saknat album. Om albumet inte har släppts än behöver du inte starta en sökning.
- Med andra ord kommer Lidarr bara att hitta släpp som nyligen har laddats upp till dina indexerare. Den kommer inte aktivt att försöka hitta släpp som du vill ha som laddades upp i det förflutna.
- Om du redan har lagt till albumet, men nu vill söka efter det, har du några valmöjligheter. Du kan gå till albumets sida och använda sökknappen, vilket kommer att göra en sökning och sedan automatiskt välja ett. Du kan använda fliken Sök och se ''alla'' resultaten och välja det du vill ha. Eller så kan du använda filtren för `Saknas`, `Efterfrågat` eller `Avklippt ej uppfyllt`.
- Om Lidarr har varit offline under en längre tid kommer Lidarr att försöka bläddra tillbaka för att hitta det senaste släppet som bearbetades för att undvika att missa ett släpp. Så länge din indexerare stöder bläddring och det inte har gått för lång tid kommer Lidarr att kunna bearbeta de släpp som den skulle ha missat och undvika att du behöver utföra en sökning efter de missade släppen.

## Tvingad autentisering

Om Lidarr är exponerad så att användargränssnittet kan nås utanför ditt lokala nätverk bör du ha någon form av autentiseringsmetod aktiverad för att kunna komma åt användargränssnittet. Detta krävs också alltmer av spårare och indexerare.

Från och med Lidarr v2 är autentisering obligatorisk.

### Autentiseringsmetod

- `Basic` (Webbläsarpopup) - Denna alternativ visar en liten popup när du går till Lidarr och låter dig ange ett användarnamn och lösenord.
- `Forms` (Inloggningssida) - Detta alternativ har en bekant inloggningsskärm som liknar andra webbplatser för att låta dig logga in på Lidarr.
- `External` - Konfigurerbart via konfigurationsfilen endast
  - Om du använder **extern autentisering** som Authelia, Authetik, NGINX Basic auth, etc. kan du undvika dubbel autentisering genom att stänga av appen, ange `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurationsfilen](/lidarr/appdata-directory) och starta om appen. **Observera att flera `AuthenticationMethod`-poster i filen inte stöds och bara det översta värdet används**

### Obligatorisk autentisering

- Om du inte exponerar appen externt och/eller inte vill ha autentisering krävd för lokal (t.ex. LAN) åtkomst kan du ändra i Inställningar => Allmänt => Obligatorisk autentisering till `Inaktiverad för lokala adresser`
  - Konfigurationsfilens motsvarighet till detta är `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Hur jämförs möjliga nedladdningar?

> Generellt sett prioriteras kvalitet framför allt. Om du vill att kvalitet inte ska vara den främsta prioriteringen kan du slå samman dina kvaliteter. [Se TRaSH's Guide](https://trash-guides.info/merge-quality)***
{.is-info}

- Den nuvarande logiken [kan hittas här](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs).

- Från och med 2022-01-23 är logiken följande:

1. Kvalitet
1. Föredraget ordpoäng
1. Protokoll (som konfigurerats i den relevanta fördröjningsprofilen)
1. Indexerprioritet
1. Seeders/Peers (om Torrent)
1. Antal album
1. Ålder (om Usenet)
1. Storlek

## Lidarr slutade fungera efter att ha uppdaterat till Ubuntu 22.04

- Lidarr v0.8 är inte kompatibel och stöds inte på Ubuntu 22.04
- Endast Lidarr v1 stöder Ubuntu 22.04
- [Se detta FAQ-inlägg för grenar och versioner](#hur-uppdaterar-jag-lidarr)

## Varför kan jag inte lägga till en ny utgåva eller artist i Lidarr?

- Utgåvan är troligtvis av typen `unknown` på MusicBrainz

## Varför kan jag inte lägga till ett album med olika artister?

- Album med olika artister och andra metaartister på MusicBrainz beror på antalet poster de tillhandahåller.

## Varför visar Lidarr bara studioalbum, hur hittar jag singlar eller EP-skivor?

- Lidarr visar som standard bara studioalbum för varje artist. Du kan dock utöka albumtyperna för en artist eller för hela ditt bibliotek genom att använda metadataprofiler.

## Kan jag bara lägga till ett album?

- För tillfället går det inte.

## Kan jag ladda ner enskilda låtar?

- Lidarr fungerar genom att söka efter och ladda ner hela släpp, därför kan enskilda låtar inte laddas ner om de inte släpps som singlar av artisten.

## Varför visas inte artisten X i sökresultaten?

- Sökfunktionen är fortfarande under utveckling. Artister som inte visas i sökresultaten kan läggas till genom att söka efter `lidarr:mbid` där `mbid` är artistens MusicBrainz-ID.

## Lidarr matchade ett album med för många låtar. Hur kan jag ändra albumet till rätt utgåva?

- Öppna albumets detaljsida och välj redigeringsikonen i toppmenyn. Där kan du hitta en rullgardinsmeny med alla utgåvor som är kopplade till det albumet.

## Jag kan inte hitta en utgåva i Lidarr men den finns på MusicBrainz

- Detta beror troligtvis på att utgåvan har en `unknown` utgivningsstatus. Uppdatera MusicBrainz.

## Hur ofta synkroniseras Lidarrs och MusicBrainz databaser?

- Varje timme, 5 minuter efter timmen

## Hur kan jag lägga till saknade artistbilder?

- Lägg till bilder på fanart.tv och vänta ~7+ dagar för att det ska rensas i cacheminnet. Uppdatera sedan metadata.

## Hur kan jag få saknade albumbilder? (Omslag)

- Lägg till omslag på musicbrainz och vänta ~1 timme+ för att det ska rensas i cacheminnet. Uppdatera sedan metadata.

## Jag har problem med att importera mina artister, vad kan det bero på?

- Importprocessen för artister importerar bara artistnamn och sökvägar, som sedan lagras i databasen så att a) metadata kan hämtas och b) nedladdat innehåll kan placeras på samma plats i framtiden. Till detta behöver användarkontot som Lidarr körs under både läs- och skrivrättigheter till din datakatalog.

## Hur kan jag döpa om mina artistmappar?

{#rename-folders}

> Samma process gäller också för att flytta/ändra artistmappar.
{.is-info}

1. Bibliotek
1. Massredigerare
1. Välj vilka artister som behöver byta namn på sina mappar
1. Ändra rotmappen till samma rotmapp som artisterna redan finns i
1. Välj "Ja, flytta filer"

## Hur kan jag massradera artister från önskelistan?

- Använd Massredigerare => Välj artister du vill radera => Radera

## Varför fungerar inte Lidarr bakom en omvänd proxy

- Lidarr använder .NET och en ny webbserver. För att SignalR ska fungera, att knapparna i användargränssnittet ska fungera, att databasändringar ska göras och andra saker. Krävs följande tillägg till platsblocket för Lidarr:
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;

- Se till att du `inte` inkluderar `proxy_set_header Connection "Upgrade";` som föreslagits av nginx-dokumentationen. `DET HÄR KOMMER INTE ATT FUNGERA`
- [Se detta ASP.NET Core-problem](https://github.com/aspnet/AspNetCore/issues/17081)
- Om du använder en CDN som Cloudflare, se till att websockets är aktiverade för att tillåta websockets-anslutningar.

## Hur uppdaterar jag Lidarr?

- Gå till Inställningar och sedan fliken Allmänt och visa avancerade inställningar (använd växlingen bredvid spara-knappen).

1. Under avsnittet Uppdateringar ändra grennamnet till `master` eller `develop`
1. Spara

*Detta kommer inte att installera bitarna från den grenen omedelbart, det kommer att ske under nästa uppdatering.*

- `master` - ![Nuvarande Master/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Den har testats av användare på utvecklings- och nattliga grenar och det är inte känt att den har några större problem. Den här versionen kommer att uppdateras ungefär varje månad. På GitHub är detta `master`-grenen.

- `develop` - ![Nuvarande Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) - (Beta): Detta är kanten för testning. Släppt efter att ha testats i nattliga för att säkerställa att det inte finns några omedelbara problem. Nya funktioner och buggfixar släpps här först efter nattliga. Det kan betraktas som halvstabilt, men är fortfarande `beta`. Den här versionen kommer att uppdateras antingen veckovis eller varannan vecka beroende på utveckling.

> **Varning: Du kanske inte kan gå tillbaka till `master` efter att ha bytt till den här grenen.** På GitHub är detta en ögonblicksbild av `develop`-grenen vid en specifik tidpunkt.
{.is-warning}

- `nightly` - ![Nuvarande Nightly/Ostabilt](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) - (Alfa/Ostabilt): Detta är den absolut senaste versionen. Den släpps så snart koden har skickats och passerar alla automatiserade tester. Den här versionen kan ännu inte ha använts av oss eller andra användare. Det finns ingen garanti för att den ens kommer att fungera i vissa fall. Den här grenen rekommenderas endast för avancerade användare. Problem och egen undersökning förväntas i denna gren. ***Använd den här grenen endast om du vet vad du gör och är villig att ta i lite för att återställa en misslyckad uppdatering.*** Den här versionen uppdateras omedelbart.

> **Varning: Du kanske inte kan gå tillbaka till `master` efter att ha bytt till den här grenen.** På GitHub är detta `develop`-grenen.
{.is-danger}

- Observera: Om du installerar via Docker, lägg till `:release`, `:latest`, `:testing` eller `:develop` i slutet av din container-tagg beroende på vem som gör dina byggen. Observera att `nightly`-grenar medvetet inte listas nedan.

|                                                                    | `master` (stabil) ![Nuvarande Master/Senaste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Nuvarande Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) | `nightly` (alfa) ![Nuvarande Nightly/Alfa](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/lidarr)                       | `release`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-lidarr) | `latest`                                                                                                                                                                                                              | `develop`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |

### Kan jag uppdatera Lidarr i min Docker-container?

- *Tekniskt sett, ja.* **Men du bör absolut inte göra det.** Det är en grundläggande filosofi för Docker. Det kan uppstå databasproblem om du uppgraderar din installation till den senaste `nightly`, men sedan uppdaterar Docker-behållaren själv (eventuellt nedgraderar till en äldre version).

### Installera en nyare version

#### Nativa

1. Gå till System och sedan fliken Uppdateringar.
1. Nyare versioner som ännu inte är installerade kommer att ha en uppdateringsknapp bredvid dem. Klicka på den knappen för att installera uppdateringen.

#### Docker

1. Dra om din tagg och uppdatera din behållare.

## Kan jag växla från `nightly` tillbaka till `develop`?

## Kan jag växla mellan grenar?

- Om versionen är identisk kan du växla, annars kontrollera med utvecklingsteamet om du kan växla från `nightly` till `master`; `nightly` till `develop`; eller `develop` till `master` för din specifika byggning.
- Om du inte följer dessa instruktioner kan din Lidarr bli oanvändbar eller kasta fel. Du har blivit varnad
  - Det vanligaste felet är något som `Error parsing column 45 (Language=31 - Int64)` eller andra liknande databasfel som saknar kolumner eller tabeller.

## Jag får ett felmeddelande: Database disk image is malformed

- **Felmeddelanden som `Error creating log database` indikerar problem med logs.db**
  - Detta kan snabbt åtgärdas genom att byta namn på eller ta bort databasen. Loggdatabasen innehåller oviktig information om kommandohistorik och uppdateringsinstallationshistorik, samt Info-, Warn- och Error-poster.
- **Felmeddelanden som `Error creating main database` eller generella `database disk image is malformed` utan angiven databas indikerar problem med lidarr.db**
  - Fortsätt med de nedan angivna stegen.
- Detta innebär att din SQLite-databas som lagrar det mesta av informationen för Lidarr är korrupt. Dina alternativ är att försöka (ett) säkerhetskopiera, försöka återställa den befintliga databasen, försöka återställa säkerhetskopior eller om allt annat misslyckas börja om med en helt ny databas.
- Detta fel kan visas om databasfilen inte kan skrivas av användaren/gruppen som \*Arr körs som. Problem med behörigheter kan troligen bara uppstå vid nya installationer, migrerade installationer till en ny server, om du nyligen har ändrat behörigheterna för din appdata-katalog eller om du har ändrat användaren och gruppen som \*Arr körs som.
- Ditt bästa och första alternativ är att [försöka återställa från en säkerhetskopia](#hur-säkerhetskopierar-och-återställer-jag-min-lidarr)
- Du kan också försöka återställa din databas. Detta är vanligtvis det enda alternativet när detta problem uppstår efter en uppdatering. Prova [sqlite3 `.recover`-kommandot](/useful-tools#recovering-a-corrupt-db)
  - Om din sqlite inte har `.recover` eller om du vill ha ett mer GUI-vänligt sätt (t.ex. Windows) kan du följa [våra instruktioner på denna wiki](/useful-tools#recovering-a-corrupt-db-ui).
- En annan möjlig orsak till att du får ett fel med din databas är att du placerar din databas på en nätverksenhet (nfs eller smb eller något annat som inte är lokalt). **SQLite är utformat för situationer där data och applikationen existerar på samma maskin.** Därför måste din \*Arr AppData-mapp (/config-montering för docker) vara på lokal lagring. [SQLite och nätverksenheter fungerar inte bra tillsammans och kommer att orsaka en felaktig databas förr eller senare](https://www.sqlite.org/draft/useovernet.html).
- Om du använder mergerFS måste du ta bort `direct_io` eftersom SQLite använder mmap som inte stöds av `direct_io`, som förklaras i mergerFS [dokumentationen här](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Hur säkerhetskopierar och återställer jag min Lidarr?

### Säkerhetskopiering av Lidarr

#### Använda inbyggd säkerhetskopiering

- Gå till System => Backup i Lidarr UI
- Klicka på Backup-knappen
- Ladda ner zip-filen efter att säkerhetskopieringen har skapats för att spara den på ett säkert ställe

#### Använda filsystemet direkt

- Hitta platsen för AppData-katalogen för Lidarr  
  - Via Lidarr UI, gå till System => About  
  - [Lidarr Appdata Directory](/lidarr/appdata-directory)
- Stoppa Lidarr - Detta förhindrar att databasen blir korrupt
- Kopiera innehållet till en säker plats

### Återställning från säkerhetskopia

> Att återställa till ett operativsystem som använder olika sökvägar kommer inte att fungera (Windows till Linux, Linux till Windows, Windows till OS X eller OS X till Windows), att flytta mellan OS X och Linux kan fungera, eftersom båda använder sökvägar som innehåller `/` istället för `\` som Windows använder, men det stöds inte. Du måste manuellt redigera alla sökvägar i databasen.
{.is-warning}

#### Använda zip-säkerhetskopia

- Installera Lidarr igen (om tillämpligt / inte redan installerat)
- Kör Lidarr
- Gå till System => Backup
- Välj Återställ säkerhetskopia
- Välj Välj fil
- Välj din säkerhetskopia i zip-format
- Välj Återställ

#### Använda filsystemets säkerhetskopior

- Installera Lidarr igen (om tillämpligt / inte redan installerat)
- Hitta platsen för AppData-katalogen för Lidarr  
  - Kör Lidarr en gång och gå via UI till System => About  
  - [Lidarr Appdata Directory](/lidarr/appdata-directory)
- Stoppa Lidarr
- Ta bort innehållet i AppData-katalogen **(inklusive .db-wal/.db-journal-filerna om de finns)**
- Återställ från din säkerhetskopia
- Starta Lidarr
- Så länge sökvägarna är desamma kommer allt att fortsätta där det slutade

#### Återställning av filsystem på Synology NAS

> VARNING: Återställning på en Synology kräver kunskap om Linux och Root SSH-åtkomst till Synology-enheten.
{.is-warning}

- Installera Lidarr igen (om tillämpligt / inte redan installerat)
- Hitta platsen för AppData-katalogen för Lidarr  
  - Kör Lidarr en gång och gå via UI till System => About  
  - [Lidarr Appdata Directory](/lidarr/appdata-directory)
- Stoppa Lidarr
- Anslut till Synology NAS via SSH och logga in som root  

> På vissa installationer är användaren annorlunda än nedanstående kommandon: `chown -R sc-Lidarr:Lidarr *` {.is-info}

- Kör följande kommandon:

```shell
rm -r /usr/local/Lidarr/var/.config/Lidarr/Lidarr.db
cp -f /tmp/Lidarr_backup/* /usr/local/Lidarr/var/.config/Lidarr/
```

- Uppdatera behörigheterna för filerna:

 ```shell
cd /usr/local/Lidarr/var/.config/Lidarr/
chown -R Lidarr:users *
chmod -R 0644 *
```

- Starta Lidarr

## Jag använder Lidarr på en Mac och den slutade plötsligt fungera. Vad har hänt?

- Detta beror förmodligen på en bugg i MacOS som orsakade att en av databaserna blev korrupt.

- Se ovanstående inlägg om att databasen är felaktig.

- Försök sedan starta och se om det fungerar. Om det inte fungerar behöver du ytterligare support. Skriv inlägg i vår [subreddit /r/lidarr](http://reddit.com/r/lidarr) eller hoppa in på [vår discord](https://lidarr.audio/discord) för hjälp.

## Jag använder en Pi och Raspbian och Lidarr startar inte

Raspbian har en version av libseccomp2 som är för gammal för att kunna köra en Docker-container baserad på Ubuntu 20.04, vilket både hotio och LinuxServer använder som sin grund. Du behöver antingen använda `--privileged`, uppdatera libseccomp2 från Ubuntu eller få ett bättre operativsystem (Vi rekommenderar Ubuntu 20.04 arm64).

**Möjlig Lösning:**

Lyckades lösa problemet genom att installera backporten från debian repo. Det rekommenderas generellt inte att använda backport i blanket-uppgraderingsläge. Installation av en enda paket kan vara okej men kan också orsaka problem. Så förstå vad du gör.

Steg för att lösa:

Se först till att du kör Raspbian buster, t.ex. genom att använda `lsb_release -a`

> Distributor ID: Raspbian
> Description: Raspbian GNU/Linux 10 (buster)
> Release: 10
> Codename: buster

- Om du använder buster:
  - Kör följande för att lägga till backports i dina källor

  ```shell
   echo "deb <http://deb.debian.org/debian> buster-backports main" | sudo tee /etc/apt/sources.list.d/buster-backports.list
   ```

  - Installera backporten av libseccomp2

  ```shell
  sudo apt update && sudo apt-get -t buster-backports install libseccomp2
  ```

## Varför tar det så lång tid att synkronisera listor och kan jag ändra det?

Listor var aldrig och är inte avsedda att vara "lägg till det nu", de är verktyg för "jag vill ha det här, lägg till det så småningom".

Du kan manuellt trigga en listuppdatering, skapa ett skript och trigga det via API:et eller lägga till utgåvor direkt i Lidarr.

Denna ändring gjordes för att vår server inte skulle överbelastas av människor som uppdaterar listor var 10:e minut.

## Kan jag inaktivera uppdateringen av utgåvor?

Nej, och du bör inte göra det genom någon SQL-hackning heller. Uppdateringen av utgåvor frågar Servarr-proxyt uppströms och kontrollerar om metadata för varje utgåva (ID, rollista, sammanfattning, betyg, översättningar, alternativa titlar, etc.) har uppdaterats jämfört med vad som finns i Lidarr för närvarande. Vid behov kommer den att uppdatera de tillämpliga utgåvorna.

En vanlig klagomål är att uppdateringsuppgiften orsakar tung I/O-användning. En inställning som kan orsaka problem är "Skanna om artistmapp efter uppdatering". Om din disk I/O-användning ökar under en uppdatering kan du ändra inställningen för skanning till `Manuell`. Ändra inte detta till `Aldrig` om inte alla ändringar i din samling (nya utgåvor, uppgraderingar, borttagningar etc.) görs genom Lidarr. Om du tar bort utgåvor manuellt eller med ett program från tredje part, ställ inte in detta till `Aldrig`.

## Varför kan inte Lidarr se mina filer på en fjärrserver?

- För alla operativsystem, se till att användaren/gruppen som du kör \*Arr som har läs- och skrivåtkomst till den monterade enheten.
- För Linux, se till att:
  - Om du använder en NFS-montering, se till att `nolock` är aktiverat för din montering.
  - Om du använder en SMB-montering, se till att `nobrl` är aktiverat för din montering.
- För Windows: Kort sagt, användaren som \*Arr körs som (om det är en tjänst) eller under (om det är en fönsterapp) kan inte komma åt filvägen på fjärrservern. Detta kan bero på olika orsaker, men det vanligaste är att \*Arr körs som en tjänst, vilket orsakar de problem som beskrivs nedan.

### Lidarr körs som standard under LocalService-kontot som inte har åtkomst till skyddade fjärrfilresurser

- Kör Lidarr-tjänsten som en annan användare som har åtkomst till den resursen
- Öppna fönstret "Administrativa verktyg" => "Tjänster" på din Windows-server.
- Stoppa Lidarr-tjänsten.
- Öppna dialogrutan "Egenskaper" => "Logga på".
- Ändra användarkontot för tjänsten till den önskade användaren.
- Kör Lidarr.exe med hjälp av mappen "Autostart"

### Du använder en mappad nätverksenhet (inte en UNC-sökväg)

- Ändra dina sökvägar till UNC-sökvägar (`\\server\share`)
- Kör Lidarr.exe via mappen "Autostart"

## Hjälp, jag har låst mig ute

{#help-i-have-forgotten-my-password}

För att inaktivera autentisering (för att återställa ditt glömda användarnamn eller lösenord) måste du redigera `config.xml`, som kommer att finnas i [Lidarr Appdata Directory](/lidarr/appdata-directory).

1. Öppna config.xml i en textredigerare.
1. Hitta raden för autentiseringsmetod, som kommer att vara antingen `<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`.
1. Ändra raden för `AuthenticationMethod` till `<AuthenticationMethod>None</AuthenticationMethod>`.
1. Starta om Lidarr.
1. Lidarr kommer nu att vara tillgängligt utan lösenord. Du bör gå till "Inställningar: Allmänt" i gränssnittet och ange ditt användarnamn och lösenord.

## Hur stoppar jag webbläsaren från att starta vid uppstart?

Beroende på ditt operativsystem finns det flera möjliga sätt.

- I "Inställningar" => "Allmänt" på vissa operativsystem finns det en kryssruta för att starta webbläsaren vid uppstart.
- När du startar Lidarr kan du lägga till `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumenten.
- Stoppa Lidarr och redigera config.xml-filen och ändra `<LaunchBrowser>True</LaunchBrowser>` till `<LaunchBrowser>False</LaunchBrowser>`.

## Konstiga problem med användargränssnittet

- Om du upplever konstiga problem med användargränssnittet, som att bibliotekssidan inte listar något eller att en viss vy eller sortering inte fungerar, försök att visa sidan i ett inkognitofönster i Chrome eller en privat flik i Firefox. Om det fungerar bra där, rensa webbläsarens cache och cookies för din specifika IP/domän. För mer information, se artikeln [Rensa cache, cookies och lokal lagring](/useful-tools#clearing-cookies-and-local-storage) i wikin.

## VPN, Jackett och \*ARRs

- Om du inte befinner dig i ett förtryckande land som Kina, Australien eller Sydafrika är det vanligtvis bara torrentklienten som behöver vara bakom en VPN. Eftersom VPN-ändpunkten delas av många användare kan du och kommer att uppleva begränsningar av hastigheten, DDOS-skydd och IP-blockeringar från olika tjänster som varje programvara använder.
- Med andra ord kan det göra att \*Arrs (Lidarr, Prowlarr, Radarr, Readarr och Lidarr) blir oanvändbara i vissa fall på grund av att tjänsterna inte är tillgängliga om du placerar dem bakom en VPN.

> **För att vara tydlig handlar det inte om ifall VPN kommer att orsaka problem med \*Arrs, utan när: bildleverantörer kommer att blockera dig och cloudflare finns framför de flesta \*Arr-servrar (uppdateringar, metadata, etc.) och kan också blockera dig**
{.is-warning}

- **Många privata spårare kommer att blockera dig om du använder eller får åtkomst till dem (t.ex. genom att använda Jackett eller Prowlarr) via en VPN.**

### Användning av en VPN

- Om en VPN krävs och Docker används rekommenderas det att använda Hotio eller Binhex's Download Client + VPN Containers.
- Om en VPN krävs och Docker inte används måste din VPN-klient ***stödja split tunneling*** så att endast de nödvändiga (Download Client) apparna är bakom VPN:en.
- Många problem med att komma åt spårare kan lösas genom att använda Googles eller Cloudflares DNS-servrar istället för din internetleverantörs DNS-servrar.
- I vissa fall (t.ex. brittiska internetleverantörer) kan du behöva placera din torrentnedladdningsklient bakom en VPN och Jackett/Prowlarr enligt följande:
  - Placera Jackett bakom VPN:en och se till att split tunneling tillåter lokal åtkomst.
  - För Prowlarr, konfigurera din VPN-klient för att tillhandahålla en proxy och lägg till proxyn i Inställningar => Indexers. Ge proxyn en tagg och ge samma tagg till de indexers som behöver använda den.
    - Om det absolut behövs och om din VPN inte tillhandahåller ett sätt att skapa en proxy kan du placera Prowlarr bakom VPN:en och se till att split tunneling tillåter lokal åtkomst.

## Jacketts /all Endpoint

{#jackett-all-endpoint}

- Jacketts `/all`-endpoint är bekväm, men det är den enda fördelen. Allt annat kan orsaka problem, så det krävs att varje spårare läggs till individuellt. Alternativt kan du överväga att använda det alternativa programmet [Prowlarr](/prowlarr) som kombinerar Jackett och NZBHydra2.
- **Uppdatering april 2022: Stödet för \*Arr har tagits bort för jackett `/all` på grund av att det bara orsakar problem.**
- Jacketts /all-endpoint är bekväm, men det är den enda fördelen. Allt annat kan orsaka problem, så nu krävs det att varje spårare läggs till individuellt.
- [Även Jacketts utvecklare säger att det bör undvikas och inte användas.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Att använda /all-endpoint har inga fördelar, bara nackdelar:
  - du förlorar kontrollen över inställningar för specifika spårare (kategorier, söklägen, etc.)
  - att blanda söklägen (IMDB, fråga, etc.) kan ge lågkvalitativa resultat
  - specifika spårarkategorier (\>= 100000) kan inte användas.
  - långsamma spårare kommer att sakta ner det totala resultatet
  - totalt antal resultat är begränsat till 1000
  - om en av spårarna i /all returnerar ett fel kommer \*Arr att inaktivera den och du får inga resultat längre.

### Lösningar för Jacketts /All

- Lägg till varje spårare i Jackett manuellt som en indexer i \*Arr.
- Kolla in [Prowlarr](/prowlarr) som kan synkronisera indexers till \*Arr och är utvecklat av Lidarr/Radarr/Readarr-teamet.
- Kolla in [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisera indexers till \*Arr. Men använd inte deras enda samlade endpoint, använd `multi` om synkronisering kommer att användas.

## Varför finns det två filer? | Varför finns det en fil kvar i nedladdningar?

Detta är normalt. Med en konfiguration som stöder [hårddelning](https://trash-guides.info/hardlinks) kommer inte dubbel diskutrymme att användas. Nedan beskrivs hur Torrent-processen fungerar.

1. Lidarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten. Exempel: filmer, tv, serier, musik, etc.
1. Lidarr övervakar dina aktiva nedladdningar i din nedladdningsklient som använder det kategorinamnet. Denna övervakning sker via nedladdningsklientens API.
1. Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (kvot eller tid kan justeras i nedladdningsklienten eller inom specifika nedladdningsklienten). När filer importeras till din mediamapp kommer de att skapa en hårdlänk till filen om din konfiguration stöder det, annars kopieras filen om hårdlänkar inte stöds.
1. Om alternativet "Hantering av slutförda nedladdningar - Ta bort slutförda" är aktiverat i Lidarrs inställningar kommer Lidarr att ta bort den ursprungliga filen och torrenten från din nedladdningsklient, men endast om nedladdningsklienten rapporterar att seedningen är klar och torrenten är stoppad (dvs. pausad). Se [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) för hur du optimerar konfigurationen av din nedladdningsklient.

> Hårdlänkar är aktiverade som standard. [En hårdlänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringspunkterna måste vara desamma för din slutförda nedladdningsmapp och din mediebiblioteksmapp. Om skapandet av hårdlänken misslyckas eller om din konfiguration inte stöder hårdlänkar kommer den att använda kopiering som fallback.
{.is-info}

## Jag får ständiga varningar från min molnlagring om API-begränsningar

Lidarr skiljer sig från de andra Arrs. Den använder taggar istället för filnamn för sin funktion. Om du har Lidarr-filer på molnlagringen måste den ladda ner filen för att läsa taggarna. Detta kommer snabbt att överskrida eventuella API-begränsningar som du har hos din lagringsleverantör. Vi avråder starkt från att använda molnlagring för ditt Lidarr-bibliotek, och eventuella problem du kan uppleva beror troligen på den konfigurationen.