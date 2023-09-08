---
title: Sonarr-inställningar
description: 
published: true
date: 2023-04-29T18:16:05.634Z
tags: sonarr, behöver-kärlek, inställningar
editor: markdown
dateCreated: 2021-06-11T23:29:12.300Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Menyalternativ](#menyalternativ)
- [Mediahantering](#mediahantering)
  - [Förslag på gemensam namngivning](#förslag-på-gemensam-namngivning)
  - [Namngivning av avsnitt](#namngivning-av-avsnitt)
    - [Standardformat för avsnitt](#standardformat-för-avsnitt)
    - [Namngivning av serier](#namngivning-av-serier)
    - [Serienummer](#serienummer)
    - [Säsonger](#säsonger)
    - [Avsnitt](#avsnitt)
    - [Sändningsdatum](#sändningsdatum)
    - [Avsnittstitel](#avsnittstitel)
    - [Kvalitet](#kvalitet)
    - [Medieinformation](#medieinformation)
    - [Övrigt](#övrigt)
    - [Original](#original)
  - [Format för dagliga avsnitt](#format-för-dagliga-avsnitt)
  - [Format för animeavsnitt](#format-för-animeavsnitt)
    - [Absolutt avsnittsnummer](#absolutt-avsnittsnummer)
  - [Format för seriemappar](#format-för-seriemappar)
    - [Namngivning av serier](#namngivning-av-serier-1)
    - [Serienummer](#serienummer-1)
  - [Format för säsongsmappar](#format-för-säsongsmappar)
    - [Säsonger](#säsonger-1)
  - [Format för säsongsmappar](#format-för-säsongsmappar-1)
    - [Specialavsnitt](#specialavsnitt)
  - [Format för flera avsnitt](#format-för-flera-avsnitt)
  - [Mappar](#mappar)
  - [Importering](#importering)
  - [Filhantering](#filhantering)
  - [Behörigheter](#behörigheter)
  - [Rotmappar](#rotmappar)
- [Profiler](#profiler)
  - [Kvalitetsprofiler](#kvalitetsprofiler)
  - [Språkprofiler](#språkprofiler)
  - [Fördröjningsprofiler](#fördröjningsprofiler)
    - [Användning](#användning)
    - [Hur fördröjningsprofiler fungerar](#hur-fördröjningsprofiler-fungerar)
      - [Exempel](#exempel)
        - [Exempel 1](#exempel-1)
        - [Exempel 2](#exempel-2)
        - [Exempel 3](#exempel-3)
  - [Utgivningsprofiler](#utgivningsprofiler)
- [Kvalitet](#kvalitet-1)
  - [Betydelser för kvalitetstabell](#betydelser-för-kvalitetstabell)
  - [Definierade kvaliteter](#definierade-kvaliteter)
- [Indexerare](#indexerare)
  - [Stödda indexerare](#stödda-indexerare)
    - [Inställningar för indexerare](#inställningar-för-indexerare)
    - [Konfiguration av Usenet-indexerare](#konfiguration-av-usenet-indexerare)
    - [Konfiguration av torrentspårare](#konfiguration-av-torrentspårare)
  - [Alternativ](#alternativ)
- [Nedladdningsklienter](#nedladdningsklienter)
  - [Översikt](#översikt)
  - [Processer för nedladdningsklienter](#processer-för-nedladdningsklienter)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Nedladdningsklienter](#nedladdningsklienter-1)
    - [Stödda nedladdningsklienter](#stödda-nedladdningsklienter)
    - [Inställningar för Usenet-klienter](#inställningar-för-usenet-klienter)
    - [Inställningar för torrentklienter](#inställningar-för-torrentklienter)
    - [Kompatibilitet för borttagning av nedladdning i torrentklient](#kompatibilitet-för-borttagning-av-nedladdning-i-torrentklient)
  - [Hantering av slutförda nedladdningar](#hantering-av-slutförda-nedladdningar)
    - [Ta bort slutförda nedladdningar](#ta-bort-slutförda-nedladdningar)
    - [Hantering av misslyckade nedladdningar](#hantering-av-misslyckade-nedladdningar)
  - [Mappningar av fjärrsökvägar](#mappningar-av-fjärrsökvägar)
- [Importlistor](#importlistor)
  - [Listor](#listor)
  - [Listexkluderingar](#listexkluderingar)
- [Anslutning](#anslutning)
  - [Anslutningar](#anslutningar)
  - [Anslutningstriggers](#anslutningstriggers)
- [Metadata](#metadata)
  - [Metadata](#metadata-1)
- [Taggar](#taggar)
- [Allmänt](#allmänt)
  - [Värd](#värd)
  - [Säkerhet](#säkerhet)
  - [Proxy](#proxy)
  - [Loggning](#loggning)
  - [Analys](#analys)
  - [Uppdateringar](#uppdateringar)
  - [Säkerhetskopior](#säkerhetskopior)
- [Användargränssnitt](#användargränssnitt)
  - [Kalender](#kalender)
  - [Datum](#datum)
  - [Stil](#stil)
  
Den här sidan kommer att gå igenom alla inställningar som finns tillgängliga i Sonarr och hur de fungerar. Detta är inte menat att vara en omfattande "Hur man konfigurerar Sonarr". Se istället [Snabbstartsguide](/sonarr/quick-start-guide)-sidan.

# Menyalternativ

För att komma till inställningssidan, välj Inställningar i vänstermenyn. Följande undermenyalternativ kommer att vara tillgängliga:

![settings_1_menu.png](/assets/sonarr/settings_1_menu.png)

Observera också att för varje enskild inställningssida finns det några alternativ längst upp i menyn:

![settings_2_topmenu.png](/assets/sonarr/settings_2_topmenu.png)

- Dölj/Visa avancerat är viktigt för alla objekt som är markerade nedan som `(Avancerad inställning)`, annars kommer de inte att visas. Dessa menyalternativ visas i orange i skärmbilderna.

- Du måste spara dina ändringar innan du lämnar skärmen. Du gör det genom att klicka på diskikonet. Om du inte har gjort några ändringar kommer det att stå "Inga ändringar" och vara grått, som visas ovan.

# Mediahantering

> Vissa av dessa inställningar är bara synliga genom att använda `Visa avancerade inställningar` som finns längst upp på fältet under sökfältet{.is-info}

## Förslag på gemensam namngivning

> Nedan finns några förslag på gemensam namngivning från [TRaSH's Guides](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/) {.is-info}

> Varning: Från och med v3.0.6.1431 stöder Sonarr nu igenkänning av Dolby Vision (DV) och High Dynamic Range (HDR). Om du använder en äldre version, ersätt: `{[MediaInfo VideoDynamicRangeType]}` med `{[MediaInfoVideoDynamicRange]}` {.is-warning}

- Standardserier: `{Series TitleYear} - S{season:00}E{episode:00} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Dagliga serier: `{Series TitleYear} - {Air-Date} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Animeserier: `{Series TitleYear} - S{season:00}E{episode:00} - {absolute:000} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}[{MediaInfo VideoBitDepth}bit]{[MediaInfo VideoCodec]}[{Mediainfo AudioCodec} { Mediainfo AudioChannels}]{MediaInfo AudioLanguages}{-Release Group}`

- Säsongsmappar: `Säsong {season:00}`

- Format för flera avsnitt: `Scene`

- Seriemappar: `{Series TitleYear} [imdb-{ImdbId}]`

## Namngivning av avsnitt

- Byt namn på avsnitt - Markera för att aktivera att Sonarr byter namn på filer
  - Om ej markerad:
    - Import av nedladdningsklient
      - Icke-säsongspaket: Nedladdningsklientens utgivningstitel används
      - Säsongspaket: Ursprungligt filnamn
    - Manuell (ad hoc) import: Ursprungligt filnamn

- Ersätt otillåtna tecken - Om ej markerad kommer Sonarr att ta bort dem istället.
  - Tecknen är: `:` `\` `/` `>` `<` `?` `*` `|` `"`

### Standardformat för avsnitt

Standardformat för avsnitt - Ange namnkonventionen för dina avsnitt av typen Standardserie. Klicka på `?`-ikonen för att öppna dialogrutan `Token för filnamn`.

- Rullgardinsmeny (övre högra hörnet)
  - Vänster ruta - Hantering av mellanslag
  - Mellanslag ( ) - Använd mellanslag i namngivningen (standard)
  - Period (.) - Använd punkter istället för mellanslag i namngivningen
  - Understreck (_) - Använd understreck istället för mellanslag i namngivningen
  - Bindestreck (-) - Använd bindestreck istället för mellanslag i namngivningen
  - Höger ruta - Hantering av versaler
  - Standardversaler - Gör titeln versaler och gemener (~camel-case) (standard)
  - Versaler - Gör hela titeln versaler
  - Gemener - Gör hela titeln gemener

### Namngivning av serier

- `{Series Title}` = Seriens namn!
- `{Series CleanTitleYear}` = Seriens namn! 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Seriens namn!
- `{Series TitleThe}` = Seriens namn!, The
- `{Series TitleYear}` = Seriens namn (2010)
- `{Series Year}` = (2010)

### Serienummer

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}`= 54321

### Säsonger

- `{season:0}` = 1
- `{season:00}` =  01

### Avsnitt

- `{episode:0}` = 1
- `{episode:00}` = 01

### Sändningsdatum

- `{Air-Date}` = 2020-09-03
- `{Air Date}` = 2020 09 03

### Avsnittstitel

- `{Episode Title}` = Avsnittstitel
- `{Episode CleanTitle}` =  Avsnittstitel

### Kvalitet

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### Medieinformation

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

> `MediaInfo Full`, `AudioLanguages` och `SubtitleLanguages` stöder ett suffix `:EN+DE` som gör att du kan filtrera språken som ingår i filnamnet. Använd `-DE` för att exkludera specifika språk. Om du lägger till <kb>+</kb> (t.ex.: `:EN+`) kommer det att generera `[EN]`,`[EN+--]` eller `[--]` beroende på exkluderade språk. Till exempel `{MediaInfo Full:EN+DE}`.
{.is-info}

> `AudioLanguages` kommer inte att visa ett språk för ljud om bara ett språk finns och det är EN (engelska). För att få önskat beteende och som exempelvis visa tyska och engelska, använd {MediaInfo AudioLanguagesAll:DE+EN} istället.
{.is-info}

> `MediaInfo VideoDynamicRangeType` ger möjliga värden: DV, DV HDR10, HDR10, HDR10Plus, HLG, PQ och HDR
{.is-info}

### Övrigt

- `{Release Group}` = Rls Grp
- `{Preferred Words}` = iNTERNAL eller NF

> \* Preferred words kommer att vara det ord eller de ord som var de bokstavliga matchningarna för eventuella preferensord du har. I exemplet ovan skulle det vara ett preferensord av `iNTERNAL` eller liknande ett preferensord av `/\b(amzn|amazon)\b(?=[ ._-]web[ ._-]?(dl|rip)\b)/i` skulle returnera `AMZN` eller `Amazon`
\* `{Preferred Words:<Release Profile Name>}` är ett ytterligare alternativ för att använda matchningar från specifika utgivningsprofiler endast
{.is-info}

### Original

- `{Original Title}` = Series.Title.S01E01.WEBDL.NF.1080P.x264-EVOLVE
- `{Original Filename}` = Series.title.s01e01.WEBDL.NF.1080P.x264-EVOLVE

> `Original Title` är utgivningsnamnet och det är vad som föreslås att användas.
{.is-info}

>`Original Filename` rekommenderas inte. Det är det bokstavliga ursprungliga filnamnet och kan vara förvrängt `t1i0p3s7i8yu7ti`.
{.is-warning}

## Format för dagliga avsnitt

Format för dagliga avsnitt - Ange namnkonventionen för dina avsnitt av typen Daglig serie. Klicka på `?`-ikonen för att öppna dialogrutan `Token för filnamn`.

Se [Standardformat för avsnitt](/sonarr/settings#standard-episode-format) för mer information om denna dialogruta.

## Format för animeavsnitt

Format för animeavsnitt - Ange namnkonventionen för dina avsnitt av typen Animeserie. Klicka på `?`-ikonen för att öppna dialogrutan `Token för filnamn`.

Se [Standardformat för avsnitt](/sonarr/settings#standard-episode-format) för mer information om denna dialogruta.

### Absolutt avsnittsnummer

- `{absolute:0}` = 1
- `{absolute:00}` = 01
- `{absolute:000}` =001

## Format för seriemappar

(Avancerad inställning) - Seriemapp - Ange namnkonventionen för mappen. Klicka på `?`-ikonen för att öppna dialogrutan `Token för filnamn`.

### Namngivning av serier

- `{Series Title}` = Seriens namn!
- `{Series CleanTitleYear}` = Seriens namn! 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Seriens namn!
- `{Series TitleThe}` = Seriens namn!, The
- `{Series TitleYear}` = Seriens namn (2010)
- `{Series Year}` = (2010)

### Serienummer

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}` = 54321

## Format för säsongsmappar

### Säsonger

- `{season:0}` = 1
- `{season:00}` = 01

## Format för säsongsmappar

### Specialavsnitt

Namn för mappen `Specials` (säsong)

- `Specials`

> Det rekommenderas att använda `Specials`
{.is-info}

## Format för flera avsnitt

- `Extend` = `S01E01-02-03`
- `Duplicate` = `S01E01.S01E01`
- `Repeat` = `S01E01E02E03`
- `Scene` = `S01E01-E02-E03`
- `Range` = `S01E01-03`
- `Prefixed Range` = `S01E01-E03`

> Det rekommenderas att använda `Scene`
{.is-info}

## Mappar

- Skapa tomma mediamappar - Skapa saknade seriemappar under diskgenomsökningen
- Ta bort tomma mappar - Ta bort tomma seriemappar och säsongsmappar under diskgenomsökningen och när avsnittsfiler tas bort

## Importering

- Avsnittstitel krävs - Förhindra import i upp till 48 timmar från avsnittens [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time)-sändningstid om avsnittstiteln är i namnformatet och avsnittstiteln är TBA (To Be Announced). Efter 48 timmar kommer importen att ske även om titeln fortfarande är TBA.
  - Alltid - Vänta alltid upp till 48 timmar på en titel innan import om avsnittet är TBA.
  - Endast för säsongsvis import - Vänta upp till 48 timmar på en titel innan import om avsnittet är TBA, endast om en säsongs-pack eller bulk-import hittas. <- Detta rekommenderas.
  - Aldrig - Fördröj inte import om avsnittet är TBA.
- Hoppa över kontroll av ledigt utrymme - Använd när Sonarr inte kan detektera ledigt utrymme från din serie rotmapp.
- Minsta lediga utrymme - Att växla detta kommer att förhindra import om det skulle lämna mindre än denna mängd diskutrymme tillgängligt.
- Använd hårda länkar istället för kopiering - Använd hårda länkar när du försöker kopiera filer från torrents som fortfarande är seedade.
  - För mer information om detta klicka [här](https://trash-guides.info/hardlinks)

 > Sällan - men möjligtvis - kan filåtkomstsspärrar förhindra att filer som fortfarande seedas byter namn. Du kan tillfälligt inaktivera seedning och använda Sonarrs omdöpningsfunktion som en lösning. {.is-warning}

- Importera extra filer - Importera matchande extra filer (undertexter, nfo, etc) efter att en fil har importerats.
  Om ett undertextfilnamn innehåller ytterligare taggar som `cc` eller `forced`, kommer de att bevaras så länge de erkänns (för närvarande i utvecklingsversionen).

## Filhantering

- Avmarkera borttagna avsnitt - Avsnitt som raderas från disken avmarkeras automatiskt i Sonarr.
- Ladda ner korrekta och repacks - Om du vill uppgradera automatiskt till korrekta och repacks. Använd "Föredrar inte" för att sortera efter föredragna ordpoäng över korrekta/repacks.
  - Föredrar och uppgradera - Ranka repacks och korrekta högre än icke-repacks och icke-korrekta. Behandla nya repacks och korrekta som uppgraderingar till nuvarande utgåvor.
  - Uppgradera inte automatiskt - Ranka repacks och korrekta högre än icke-repacks och icke-korrekta. Behandla inte nya repacks och korrekta som uppgraderingar till nuvarande utgåvor.
  - Föredrar inte - Ignorera i princip repacks och korrekta. Du måste hantera eventuella preferenser för dessa med [Utgivningsprofiler (Föredragna ord)](#release-profiles).

> `PROPER` - betyder att det fanns ett problem med den tidigare utgåvan. Nedladdningar som är märkta som PROPER visar att problemen har åtgärdats i den utgåvan. Detta görs av en grupp som inte släppte originalversionen.
> `REPACK` - betyder att det fanns ett problem med den tidigare utgåvan och att det har åtgärdats av den ursprungliga gruppen. Nedladdningar som är märkta som REPACK visar att problemen har åtgärdats i den utgåvan. Detta görs av en grupp som släppte originalversionen. {.is-info}

> [Använd föredragna ord för automatiska uppgraderingar till korrekta/repacks](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#propers-and-repacks) {.is-info}

- Analysera videofiler - Extrahera filinformation som upplösning, speltid och codec-information från filer. Detta kräver att Sonarr läser delar av filen vilket kan orsaka hög disk- eller nätverksaktivitet under skanningar.
- Skanna om seriemapp efter uppdatering - Skanna om seriemappen efter att serien har uppdaterats.
  - Alltid - Detta kommer att skanna om seriemappen baserat på schemalagda uppgifter.
  - Efter manuell uppdatering - Du måste manuellt skanna disken.
  - Aldrig - Precis som det låter, skanna aldrig om seriemappen.
- Ändra filens datum - Ändra filens datum vid import/skanning.
  - Ingen - Sonarr kommer inte att ändra datumet som visas i din filbläddrare.
  - Lokalt utgivningsdatum - Datumet då videon sändes lokalt.
  - UTC-utgivningsdatum - Datumet då videon släpptes baserat på UTC.
- Återvinningskorg - Avsnittsfiler kommer att hamna här när de raderas istället för att raderas permanent.
- Rensa återvinningskorgen - Så gammal en given fil kan vara innan den raderas permanent.

> Filer i återvinningskorgen som är äldre än det valda antalet dagar kommer att rensas automatiskt. {.is-warning}

## Behörigheter

- Ange behörigheter - Ska `chmod` köras när filer importeras/ändras namn?
  - chmod-mapp - Oktal, tillämpas vid import/ändring av behörigheter för mediamappar och filer (utan exekveringsbitar).

> Listan i rullgardinsmenyn har en förinställd lista över mycket vanligt använda behörigheter som kan användas. Du kan dock manuellt ange en oktal mapp om du vill. {.is-info}

> Detta fungerar endast om användaren som kör `Sonarr` är ägare till filen. Det är bättre att se till att nedladdningsklienten ställer in behörigheterna korrekt. {.is-warning}

- chown-grupp - Gruppnamn eller GID. Använd GID för fjärrfiler.

> Detta fungerar endast om användaren som kör `Sonarr` är ägare till filen. Det är bättre att se till att nedladdningsklienten ställer in behörigheterna korrekt. {.is-warning}

## Rotmappar

- Sökväg - Detta visar sökvägen till din mediebibliotek.
- Ledigt utrymme - Detta är det lediga utrymmet som rapporteras till Sonarr från systemet.
- Omappade mappar - Detta är mappar som inte har en associerad serie.

> `X` i slutet kommer att ta bort denna rotmapp. {.is-info}

- Lägg till rotmapp - Detta gör att du kan välja en rotmapp för att antingen placera nya importerade nedladdningar i denna mapp eller att låta Sonarr skanna befintlig media.

> Användare som inte använder Windows:
> \* Om du använder en NFS-mapp, se till att `nolock` är aktiverat.
> \* Om du använder en SMB-mapp, se till att `nobrl` är aktiverat. {.is-warning}

# Profiler

## Kvalitetsprofiler

- Ange profiler för kvaliteten på serier du vill ladda ner.

> När du väljer en befintlig profil eller lägger till en ytterligare profil visas ett nytt fönster. {.is-info}

> Observera: Kvaliteten som har en blå ruta är kvaliteten som alla medier med denna profil kommer att uppgraderas till. {.is-info}

- Namn - Välj ett **UNIKT** namn för den kvalitetsprofil du skapar.
- Uppgraderingar tillåtna - När detta alternativ är markerat och du ber Sonarr att ladda ner en `WEB 1080p` eftersom det är den första utgåvan av ett specifikt avsnitt, om någon senare kan ladda upp en `Bluray-1080p` kommer Sonarr automatiskt att uppgradera till bättre kvalitet ***om*** `Uppgradera till` har den kvaliteten vald.
- Uppgradera till - När denna kvalitet har uppnåtts kommer Sonarr inte längre att ladda ner avsnitt.

> Observera: Detta gäller endast om du har `Bluray-1080p` högre än `WEB 1080p` inom avsnittet `Kvaliteter`. {.is-warning}

- Kvaliteter - Kvaliteter högre upp i listan är mer föredragna även om de inte är markerade. Kvaliteter inom samma grupp är likvärdiga. Endast markerade kvaliteter önskas.
- Redigera grupper - Vissa kvaliteter grupperas för att minska storleken på listan samt gruppera liknande utgåvor. Ett bra exempel på detta är `WebDL` och `WebRip` eftersom dessa är mycket liknande och vanligtvis har liknande bitrater. När du redigerar grupperna kan du ändra preferensen inom varje grupp. [Se TRaSh's Guide för hur man slår samman kvaliteter](https://trash-guides.info/merge-quality)
  - [Se Kvaliteter](#qualities-defined)

> Som standard är kvaliteterna inställda från lägsta (botten) till högsta (topp). {.is-info}

## Språkprofiler

- Ange profiler för språket på serier du vill ladda ner.

> Observera att prioriteringen/ordningen spelar roll även om språket inte önskas (valt). {.is-info}

- Namn - Välj ett **UNIKT** namn för språkprofilen du skapar.
- Uppgraderingar tillåtna - Om inte markerad (inaktiverad) kommer språk inte att uppgraderas. Till exempel, om du ber Sonarr att ladda ner en kinesisk version eftersom det är den första utgåvan av en specifik serie och senare kan någon ladda upp en engelsk version, då kommer Sonarr automatiskt att uppgradera till bättre kvalitet med detta valt.

> Detta gäller endast om engelska är högre upp i språklistan än kinesiska och båda är markerade. {.is-warning}

- Språk - Språk högre upp i listan är mer föredragna. Endast markerade språk önskas.

## Fördröjningsprofiler

- Fördröjningsprofiler gör det möjligt att minska antalet utgåvor som laddas ner för ett avsnitt genom att lägga till en fördröjning medan Sonarr fortsätter att leta efter utgåvor som bättre matchar dina preferenser.
- Föredraget protokoll - Detta kommer antingen vara `Usenet` eller `Torrent` beroende på vilket nedladdningsprotokoll du föredrar.
- Usenet-fördröjning - Ange antalet minuter du vill vänta innan nedladdningen startar.
- Torrent-fördröjning - Ange antalet minuter du vill vänta innan nedladdningen startar.
- Bypassa om högsta kvalitet - Bypassa fördröjningen när utgåvan har den högsta aktiverade kvalitetsprofilen med det föredragna protokollet.
- Taggar - Genom att ge denna fördröjningsprofil en tagg kan du tagga en given serie för att följa reglerna som anges här.
- Skiftnyckelikonen - Detta gör att du kan redigera fördröjningsprofilen.
- Plusikonen (<kb>+</kb>) - Skapa en ny fördröjningsprofil

### Användningsområden

Vissa medier kommer att få ett halvt dussin olika utgåvor av varierande kvalitet under timmarna efter en utgåva, och utan fördröjningsprofiler kan Sonarr försöka ladda ner alla. Med fördröjningsprofiler kan Sonarr konfigureras för att ignorera de första några timmarna av utgåvor.

Fördröjningsprofiler är också användbara om du vill betona ett protokoll (Usenet eller BitTorrent) över det andra. (Se [Exempel 3](/sonarr/settings/#example-3))

### Hur fördröjningsprofiler fungerar

Timern börjar så snart Sonarr upptäcker att ett avsnitt har en tillgänglig utgåva. Denna utgåva kommer att visas i din kö med en klockikon för att indikera att den är under fördröjning.

> Klockan börjar från tidpunkten då utgåvan laddades upp och inte från den tidpunkt då Sonarr ser den. {.is-info}

Under fördröjningsperioden kommer Sonarr att notera eventuella nya utgåvor som blir tillgängliga. När fördröjningstimern löper ut kommer Sonarr att ladda ner den enskilda utgåvan som bäst matchar dina kvalitetspreferenser.

Tidperioden kan vara olika för Usenet och Torrents. Varje profil kan associeras med en eller flera taggar för att du ska kunna anpassa vilka program som har vilka profiler. En fördröjningsprofil utan tagg betraktas som standard och gäller för alla program som inte har en specifik tagg.

> Fördröjningsprofiler börjar från tidpunkten då indexeraren rapporterar att utgåvan laddades upp. Detta innebär att allt innehåll som är äldre än det antal minuter du har ställt in påverkas inte på något sätt av din fördröjningsprofil och kommer att laddas ner omedelbart. Dessutom kommer **alla manuella sökningar** efter innehåll (sökningar utanför RSS-flöden) att ignorera inställningarna för fördröjningsprofil. {.is-warning}

#### Exempel

- För varje exempel, anta att användaren har följande kvalitetsprofil aktiv: HDTV 720p och högre är tillåtna, WebDL 720p är kvalitetsgränsen, WebDL 1080p är den högst rankade kvaliteten.

##### Exempel 1

- I detta enkla exempel är profilen inställd med en 120 minuters (två timmar) fördröjning för både Usenet och Torrent.

- Klockan 23:00 upptäcker Sonarr den första utgåvan för ett avsnitt och den laddades upp kl. 22:50 och 120 minuters klocka börjar ticka. Kl. 00:50 kommer Sonarr att utvärdera alla utgåvor som den har hittat under de senaste två timmarna och ladda ner den bästa, som är WebDL 720p.

- Kl. 03:00 hittas en annan utgåva, som är WebDL 720p och lades till i din indexer kl. 02:46. En annan 120 minuters klocka börjar ticka. Kl. 04:46 laddas den bästa tillgängliga utgåvan ner. Eftersom kvalitetsgränsen nu har nåtts kan avsnittet inte längre uppgraderas och Sonarr kommer att sluta leta efter nya utgåvor.

- När som helst om en WebDL 1080p-utgåva hittas kommer den att laddas ner omedelbart eftersom det är den högst rankade kvaliteten. Om det finns en aktiv fördröjningstimer kommer den att avbrytas.

##### Exempel 2

- Detta exempel har olika timer för Usenet och Torrents. Anta en 120 minuters timer för Usenet och en 180 minuters timer för BitTorrent.

- Kl. 23:00 upptäcker Sonarr den första utgåvan för ett avsnitt och båda timrarna börjar ticka. Utgåvan lades till i indexeraren kl. 22:15. Kl. 00:15 kommer Sonarr att utvärdera alla utgåvor och om det finns några acceptabla Usenet-utgåvor kommer den bästa att laddas ner och båda timrarna kommer att sluta ticka. Om det inte finns några sådana utgåvor kommer Sonarr att vänta tills kl. 00:15 och ladda ner den bästa utgåvan, oavsett vilken källa den kommer från.

##### Exempel 3

- Ett vanligt användningsområde för fördröjningsprofiler är att betona ett protokoll över det andra. Till exempel kan du bara vilja ladda ner en BitTorrent-utgåva om ingenting har laddats upp på Usenet efter en viss tid.

- Du kan ställa in en 60 minuters timer för BitTorrent och en 0 minuters timer för Usenet.

- Om den första utgåvan som upptäcks kommer från Usenet kommer Sonarr att ladda ner den omedelbart.

- Om den första utgåvan kommer från BitTorrent kommer Sonarr att ställa in en 60 minuters timer. Om någon kvalificerad Usenet-utgåva upptäcks under den tiden kommer BitTorrent-utgåvan att ignoreras och Usenet-utgåvan kommer att laddas ner.

## Utgivningsprofiler

- Inte alla utgåvor är lika bra, varje utgivningsgrupp har sin egen metod för att packa och koda sitt material. Här kan du välja de föredragna utgåvorna du letar efter.

> Du kan använda regex (standard är skiftlägeskänsligt) i fälten "Måste innehålla", "Får inte innehålla" och "Föredragna" ord. Regex måste vara i formatet `/regex-här/i`. {.is-info}

- Namn - Välj ett **UNIKT** namn för utgivningsprofilen du skapar.
- Aktivera profil - Växla denna profil på eller av.
- Måste innehålla - Utgåvan måste innehålla minst ett av dessa termer (skiftlägesokänsligt).
- Får inte innehålla - Utgåvan kommer att avvisas om den innehåller en eller flera av dessa termer (skiftlägesokänsligt).
- Föredragna - Här kan du välja en given term och ge den ett poängvärde.
  - Låt oss säga att du letar efter utgåvor med en specifik gruppering av ord. Låt oss säga att du vill berätta för Sonarr att du vill ha Repacks eller Propers framför vanliga utgåvor. Här lägger du in ordet Repack i ett av fälten och ger det ett värde (säg 100), men du letar också efter DTS-HD-ljud så du lägger in det också och ger det ett poängvärde (säg 100 igen). När Sonarr går igenom och tittar på alla utgåvor från RSS-flödet och den stöter på en utgåva som har både Repack och DTS-HD kommer det att ge den ett poängvärde på 200. Vilket är mycket högre än alla andra som inte har något av dessa ord. Detta talar om för Sonarr att detta har ett högre poängvärde och det kommer att vara den första filen som väljs för nedladdning.
- Inkludera föredragna vid namnändring - När du använder taggen {Preferred Words} i namnschemat.
- Indexer - Ange vilken indexer profilen gäller för.

> Detta är användbart om du bara vill ha specifika utgåvor från en viss indexer/trackersajt. {.is-info}

- Taggar - Genom att ge denna utgivningsprofil en tagg kan du tagga en given serie för att följa reglerna som anges här. Om du lämnar detta fält tomt kommer dessa regler att gälla för alla serier.

- [TRaSH har en lista över WEB-DL utgivningsprofiler](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/)
- [TRaSH Anime Profiler](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx-Anime/)

# Kvalitet

## Betydelser för kvalitetstabell

- Kvalitet - Namnet på kvaliteten enligt scenen (hårdkodat).
- Titel - Namnet på kvaliteten i gränssnittet (konfigurerbart).
- Megabyte per timme - Självförklarande.
- Storleksgräns - Självförklarande.
- Min - Minsta megabyte per minut (MB/min) en kvalitet kan ha.
- Max - Högsta megabyte per minut (MB/min) en kvalitet kan ha.

## Definierade kvaliteter

- Okänd - Självförklarande
- SDTV - Efterluftskopior från en analog källa (vanligtvis kabel-TV eller OTA-standardupplösning). Bildkvaliteten är generellt sett bra (för upplösningen) och de är vanligtvis kodade i DivX/XviD eller MP4.
- WEBDL-480p - WEB-DL (P2P) hänvisar till en fil som har kopierats förlustfritt från en strömningstjänst, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., eller laddats ner via en online-distributionswebbplats som iTunes. Kvaliteten är ganska bra, eftersom de inte är omkodade. Videon (H.264 eller H.265) och ljudet (AC3/AAC) extraheras vanligtvis från iTunes eller Amazon Video och remuxas till en MKV-behållare utan att förlora kvalitet. En fördel med dessa utgåvor är att de vanligtvis inte har några nätverkslogotyper på skärmen. Dessa är nästan lika bra som en Blu-ray-källa men kan lida av ljudfördröjning eller visuella artefakter från den adaptiva bitfrekvensen hos strömningstjänster. Om en ripperns internetanslutning sjunker till en punkt där bitfrekvensen minskar kan källans bitfrekvens ändras dynamiskt, vilket leder till variationer i bildkvaliteten. De flesta utgåvor som lider av en extrem mängd visuella artefakter är NUKED och en PROPER släpps vanligtvis för att fixa eventuella vilda variationer i adaptiv bitfrekvens. Detta kommer att vara i 480p (SD) kvalitet.
- WEBRip-480p - I en WEB-Rip (P2P) extraheras filen ofta med hjälp av protokollen HLS eller RTMP/E och remuxas från en TS-, MP4- eller FLV-behållare till MKV. Detta kommer att vara i 480p (SD) kvalitet.
- DVD - En omkodning av den slutliga utgivna DVD9. Om möjligt släpps detta PRE retail. Det bör vara utmärkt kvalitet (för upplösningen). DVDrips släpps vanligtvis i DivX/XviD eller MP4.
- Bluray-480p - En omkodning av den slutliga utgivna Blu-ray, nedskalad till 480p-upplösning (720x480 @ 16:9, någon annan bildförhållande kan vara en annan upplösning). Om möjligt släpps detta PRE retail. Det bör vara utmärkt kvalitet för upplösningen. Bitfrekvenserna kan variera, men dessa är generellt kodade till DivX, XviD eller AVC och erbjuder en kompromiss med en liten upplevd kvalitetsminskning jämfört med den ursprungliga källan samtidigt som filstorleken minskas drastiskt. Dessa är vanligtvis MKV eller MP4, men det finns även några DivX/XviD som använder AVI.
- HDTV-720p - En omkodning av den slutliga utgivna Blu-ray, men sänds över HD-kabel eller satellit (1280x720 @ 16:9, något annat bildförhållande kan vara en annan upplösning). Den kan modifieras för körtid eller innehåll beroende på vilket nätverk den kommer från. Detta släpps vanligtvis flera månader efter en detaljhandelsutgåva, men ibland släpps uppskalade versioner av en film med standardupplösning på kabelkanaler som STARZ eller HBO, och de skulle vara de enda HD-kopiorna av den specifika filmen som är tillgängliga. Dessa är vanligtvis MKV eller MP4.
- HDTV-1080p - En omkodning av den slutliga utgivna Blu-ray, men sänds över HD-kabel eller satellit (1920x1080 @ 16:9, något annat bildförhållande kan vara en annan upplösning). Den kan modifieras för körtid eller innehåll beroende på vilket nätverk den kommer från. Detta släpps vanligtvis flera månader efter en detaljhandelsutgåva, men ibland släpps uppskalade versioner av en film med standardupplösning på kabelkanaler som STARZ eller HBO, och de skulle vara de enda HD-kopiorna av den specifika filmen som är tillgängliga. Dessa är vanligtvis MKV eller MP4-behållare.
- Raw-HD - En rå strömning av en HD-ström.
- WEBRip-720p - I en WEB-Rip (P2P) extraheras filen ofta med hjälp av protokollen HLS eller RTMP/E och remuxas från en TS-, MP4- eller FLV-behållare till MKV. Detta kommer att vara i 720p-kvalitet.
- Bluray-720p - En omkodning av den slutliga utgivna Blu-ray, nedskalad till 720p-upplösning (1280x720 @ 16:9, något annat bildförhållande kan vara en annan upplösning). Om möjligt släpps detta PRE retail. Det bör vara utmärkt kvalitet för upplösningen. Bitfrekvenserna kan variera, men dessa är generellt kodade till AVC eller HEVC och erbjuder en kompromiss med en liten upplevd kvalitetsminskning jämfört med den ursprungliga källan samtidigt som filstorleken minskas drastiskt. Dessa är vanligtvis MKV eller MP4-behållare.
- WEBDL-1080p - WEB-DL (P2P) hänvisar till en fil som har kopierats förlustfritt från en strömningstjänst, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., eller laddats ner via en online-distributionswebbplats som iTunes. Kvaliteten är ganska bra, eftersom de inte är omkodade. Videon (H.264 eller H.265) och ljudet (AC3/AAC) extraheras vanligtvis från iTunes eller Amazon Video och remuxas till en MKV-behållare utan att förlora kvalitet. En fördel med dessa utgåvor är att de vanligtvis inte har några nätverkslogotyper på skärmen. Dessa är nästan lika bra som en Blu-ray-källa men kan lida av ljudfördröjning eller visuella artefakter från den adaptiva bitfrekvensen hos strömningstjänster. Om en ripperns internetanslutning sjunker till en punkt där bitfrekvensen minskar kan källans bitfrekvens ändras dynamiskt, vilket leder till variationer i bildkvaliteten. De flesta utgåvor som lider av en extrem mängd visuella artefakter är NUKED och en PROPER släpps vanligtvis för att fixa eventuella vilda variationer i adaptiv bitfrekvens. Detta kommer att vara i 1080p-kvalitet.
- WEBRip-1080p - I en WEB-Rip (P2P) extraheras filen ofta med hjälp av protokollen HLS eller RTMP/E och remuxas från en TS-, MP4- eller FLV-behållare till MKV. Detta kommer att vara i 1080p-kvalitet.
- Bluray-1080p - En omkodning av den slutliga utgivna Blu-ray, i sin nativa 1080p-upplösning (1920x1080 @ 16:9, något annat bildförhållande kan vara en annan upplösning). Om möjligt släpps detta PRE retail. Det bör vara utmärkt kvalitet och samma upplösning som källan. Bitfrekvenserna kan variera, men dessa är generellt kodade till AVC eller HEVC och erbjuder en kompromiss med en liten upplevd kvalitetsminskning jämfört med den ursprungliga källan samtidigt som filstorleken minskas något. Dessa är vanligtvis MKV eller MP4-behållare.
- Remux-1080p - En remux är en kopia av en Blu-ray- eller HD DVD-skiva till en annan behållarformat eller bara borttagning av skivans menyer och bonusmaterial samtidigt som ljud- och videospåren behålls intakta (och behåller de nuvarande koderna), vilket garanterar exakt 1:1-filmkvalitet som på originalskivan. Detta är i 1080p-kvalitet.
- HDTV-2160p - TVRip är en fångstkälla från ett fångstkort. HDTV står för fångad källa från HD-TV. Med en HDTV-källa kan kvaliteten ibland till och med överträffa DVD. Filmer i detta format börjar bli populära. Viss reklam och kommersiella banderoller kan ses på vissa utgåvor under uppspelning. Detta är i 2160p (4K) kvalitet.
- WEBDL-2160p - WEB-DL (P2P) hänvisar till en fil som har kopierats förlustfritt från en strömningstjänst, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., eller laddats ner via en online-distributionswebbplats som iTunes. Kvaliteten är ganska bra, eftersom de inte är omkodade. Videon (H.264 eller H.265) och ljudet (AC3/AAC) extraheras vanligtvis från iTunes eller Amazon Video och remuxas till en MKV-behållare utan att förlora kvalitet. En fördel med dessa utgåvor är att de vanligtvis inte har några nätverkslogotyper på skärmen. Dessa är nästan lika bra som en Blu-ray-källa men kan lida av ljudfördröjning eller visuella artefakter från den adaptiva bitfrekvensen hos strömningstjänster. Om en ripperns internetanslutning sjunker till en punkt där bitfrekvensen minskar kan källans bitfrekvens ändras dynamiskt, vilket leder till variationer i bildkvaliteten. De flesta utgåvor som lider av en extrem mängd visuella artefakter är NUKED och en PROPER släpps vanligtvis för att fixa eventuella vilda variationer i adaptiv bitfrekvens. Detta kommer att vara i 2160p (4K) kvalitet.
- WEBRip-2160p - I en WEB-Rip (P2P) extraheras filen ofta med hjälp av protokollen HLS eller RTMP/E och remuxas från en TS-, MP4- eller FLV-behållare till MKV. Detta kommer att vara i 2160p (4K) kvalitet.
- Bluray-2160p - En omkodning av den slutliga utgivna Blu-ray, i sin nativa 2160p-upplösning (3840x2160 @ 16:9, något annat bildförhållande kan vara en annan upplösning). 4K-versioner av filmer som släpps i allmänhetens HEVC-codec och kan vara antingen 8-bitars eller 10-bitars färgåtergivning eller från en HDR-källa. något reducerar filstorleken. Dessa är vanligtvis MKV eller MP4-behållare.
- Remux-2160p - En remux är en kopia av en Blu-ray- eller HD DVD-skiva till en annan behållarformat eller bara borttagning av skivans menyer och bonusmaterial samtidigt som ljud- och videospåren behålls intakta (och behåller de nuvarande koderna), vilket garanterar exakt 1:1-filmkvalitet som på originalskivan. Detta är i 2160p (4K) kvalitet.

# Indexer

> Information om stödda indexeringstjänster finns på sidan [Mer information (Stödda)](/sonarr/supported#indexers) för den här sektionen
{.is-info}

## Stödda indexeringstjänster

- En lista över stödda indexeringstjänster finns på sidan [Mer information (Stödda)](/sonarr/supported#indexers)

### Inställningar för indexeringstjänster

- När du har klickat på knappen <kb>+</kb> för att lägga till en ny indexeringstjänst visas ett nytt fönster med många olika alternativ. För Sonarr betraktas både Usenet-indexeringstjänster och Torrent-spårare som "indexeringstjänster".

- Här finns två avsnitt: Usenet och Torrents. Beroende på vilken nedladdningsklient du kommer att använda vill du välja vilken typ av indexeringstjänst du kommer att använda.

### Konfiguration av Usenet-indexeringstjänst

- Newznab - Här hittar du förinställda populära Usenet-indexeringstjänster (som är förifyllda, allt du behöver är din API-nyckel som tillhandahålls av Usenet-indexeringstjänsten du väljer) tillsammans med möjligheten att skapa en anpassad indexeringstjänst.
- Programvara som fungerar med Usenet och integreras väl med Sonarr är [NZBHydra2](https://github.com/theotherp/nzbhydra2/) eller [Prowlarr](/prowlarr) som integrerar både Usenet och Torrents
- Oavsett om du väljer en förifylld indexeringstjänst eller en anpassad indexeringstjänst kommer du att presenteras med ett nytt fönster för att ange alla dina inställningar
- Välj bland förinställningarna eller lägg till en anpassad indexeringstjänst (som NZBHydra2 eller Prowlarr)
- Namn - Namnet på indexeringstjänsten i Sonarr
- Aktivera RSS - Om det är aktiverat används denna indexeringstjänst för att leta efter filer som saknas eller ännu inte har nått sin avskärningstidpunkt.
- Aktivera automatisk sökning - Om det är aktiverat används denna indexeringstjänst för automatiska sökningar, inklusive sökning vid tillägg
- Aktivera interaktiv sökning - Om det är aktiverat används denna indexeringstjänst för manuella interaktiva sökningar.
- URL - URL:en till indexeringstjänsten som tillhandahålls av indexeringstjänsten, till exempel `https://api.nzbgeek.info`.
- API-sökväg - Sökvägen till API:et som tillhandahålls av indexeringstjänsten. Detta är vanligtvis `/api`
- API-nyckel - Nyckeln som tillhandahålls av indexeringstjänsten för att få åtkomst till API:et.
- Kategorier - Standardkategorier används om de inte redigeras. Det är troligt att dessa standardkategorier inte är optimala. När du redigerar denna inställning frågar Sonarr indexeringstjänsten efter sina tillgängliga kategorier och visar dem i en valbar lista. De gamla standarderna rensas så snart en kategori växlas.
- Animekategorier - Kategorierna som Sonarr kommer att använda för animesökningar. Inga kategorier används om de inte redigeras. När du redigerar denna inställning frågar Sonarr indexeringstjänsten efter sina tillgängliga kategorier och visar dem i en valbar lista. De gamla standarderna rensas så snart en kategori växlas.
- Sök efter standardformat för anime - Sök också efter anime med standardnummerering (gäller endast för animeserier) [Mer information om serietyper här](/sonarr/faq#whats-the-different-series-types)
- (Avancerad inställning) Ytterligare parametrar - Ytterligare Newznab-parametrar att lägga till i frågelänken
- (Avancerad inställning) Indexeringsprioritet - Prioritet för denna indexeringstjänst för att föredra en indexeringstjänst framför en annan i scenarier där flera utgåvor släpps samtidigt. 1 är högsta prioritet och 50 är lägsta prioritet.
- (Avancerad inställning) Nedladdningsklient - Välj och ange vilken nedladdningsklient som används för hämtningar från denna indexeringstjänst
- Taggar - Använd endast denna indexeringstjänst för serier med minst en matchande tagg. Lämna tomt för att använda med alla serier.

### Konfiguration av Torrent-spårare

- Precis som med Usenet finns det en mängd förifyllda Torrent-spårarinformation. Om du inte är medlem i någon av dessa specifika spårare kommer de inte att vara till någon nytta för dig.
- Ett av de bästa och enklaste sätten att använda Torrent-spårare som inte stöds nativt med Sonarr är att använda ett andra program som [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett). Dessa program fungerar bra med Sonarr som en sökindexer som innehåller all din information och skickar den till Sonarr.
- Torznab - Detta alternativ kommer att ställa in dig med en förinställd Jackett, om du använder flera spårare måste varje post ha ett unikt namn
- Torznab-indexeringstjänst
- Välj bland förinställningarna eller lägg till en anpassad indexeringstjänst (som Jackett eller Prowlarr)
- Namn - Namnet på indexeringstjänsten i Sonarr
- Aktivera RSS - Om det är aktiverat används denna indexeringstjänst för att leta efter filer som saknas eller ännu inte har nått sin avskärningstidpunkt.
- Aktivera automatisk sökning - Om det är aktiverat används denna indexeringstjänst för automatiska sökningar, inklusive sökning vid tillägg
- Aktivera interaktiv sökning - Om det är aktiverat används denna indexeringstjänst för manuella interaktiva sökningar.
- URL - URL:en som tillhandahålls av indexeringstjänsten, till exempel `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-sökväg - Sökvägen till API:et som tillhandahålls av indexeringstjänsten. Detta är vanligtvis `/api`
- API-nyckel - Nyckeln som tillhandahålls av indexeringstjänsten för att få åtkomst till API:et.
- Kategorier - Standardkategorier används om de inte redigeras. Det är troligt att dessa standardkategorier inte är optimala. När du redigerar denna inställning frågar Sonarr indexeringstjänsten efter sina tillgängliga kategorier och visar dem i en valbar lista. De gamla standarderna rensas så snart en kategori växlas.
- Animekategorier - Kategorierna som Sonarr kommer att använda för animesökningar. Inga kategorier används om de inte redigeras. När du redigerar denna inställning frågar Sonarr indexeringstjänsten efter sina tillgängliga kategorier och visar dem i en valbar lista. De gamla standarderna rensas så snart en kategori växlas.
- Sök efter standardformat för anime - Sök också efter anime med standardnummerering (gäller endast för animeserier) [Mer information om serietyper här](/sonarr/faq#whats-the-different-series-types)
- (Avancerad inställning) Ytterligare parametrar - Ytterligare Torznab-parametrar att lägga till i frågelänken
- (Avancerad inställning) Minsta antal seeders - Det minsta antalet seeders som krävs för att en utgåva från denna spårare ska hämtas.
- (Avancerad inställning) Seed-förhållande - Om det är tomt används standardvärdet för nedladdningsklienten. Annars är det minsta seed-förhållandet som krävs för att din nedladdningsklient ska uppfylla för utgåvor från denna indexeringstjänst innan den pausas av din klient och tas bort av Sonarr (Kräver att hantering av slutförda nedladdningar - Ta bort är aktiverat)
- (Avancerad inställning) Seed-tid - Om det är tomt används standardvärdet för nedladdningsklienten. Annars är det minsta seed-tiden i minuter som krävs för att din nedladdningsklient ska uppfylla för utgåvor från denna indexeringstjänst innan den pausas av din klient och tas bort av Sonarr (Kräver att hantering av slutförda nedladdningar - Ta bort är aktiverat)
- (Avancerad inställning) Indexeringsprioritet - Prioritet för denna indexeringstjänst för att föredra en indexeringstjänst framför en annan i scenarier där flera utgåvor släpps samtidigt. 1 är högsta prioritet och 50 är lägsta prioritet.
- (Avancerad inställning) Nedladdningsklient - Välj och ange vilken nedladdningsklient som används för hämtningar från denna indexeringstjänst
- Taggar - Använd endast denna indexeringstjänst för serier med minst en matchande tagg. Lämna tomt för att använda med alla serier.

## Alternativ

- Minsta ålder - Endast Usenet: Minsta ålder i minuter för NZB-filer innan de hämtas. Använd detta för att ge nya utgåvor tid att sprida sig till din Usenet-leverantör.
- Behållning - Endast Usenet: Ställ in till noll för obegränsad behållning
- Maximal storlek - Maximal storlek för en utgåva som ska hämtas i MB. Ställ in till noll för obegränsad. Observera att detta gäller globalt.
- RSS-synkroniseringsintervall - Intervall i minuter. Ställ in till noll för att inaktivera (detta stoppar all automatisk hämtning av utgåvor) Minimum: 10 minuter Maximum: 120 minuter
  - Se [Hur hittar Sonarr avsnitt?](/sonarr/faq#how-does-sonarr-find-episodes) för en bättre förståelse av hur RSS-synkronisering hjälper dig

> Om Sonarr har varit offline under en längre tid kommer Sonarr att försöka bläddra tillbaka för att hitta den senaste utgåvan som bearbetades i ett försök att undvika att missa en utgåva. Så länge din indexeringstjänst stöder bläddringssidor och det inte har gått för lång tid kommer Sonarr att kunna bearbeta de utgåvor som den skulle ha missat och undvika att du behöver söka efter de missade utgåvorna.{.is-info}

# Nedladdningsklienter

> Information om stödda nedladdningsklienter finns på sidan [Mer information (Stödda)](/sonarr/supported#download-clients) för den här sektionen
{.is-info}

## Översikt

- Nedladdning och import är där de flesta människor upplever problem. På en övergripande nivå behöver programvaran kunna kommunicera med din nedladdningsklient och ha åtkomst till de filer den laddar ner. Det finns en stor variation av stödda nedladdningsklienter och ännu fler olika inställningar. Det betyder att medan det finns några vanliga inställningar finns det ingen rätt inställning och varje persons inställning kan vara lite annorlunda. Men det finns många felaktiga inställningar.

## Processer för nedladdningsklienter

## Usenet

- Sonarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Sonarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- När nedladdningen är klar kommer Sonarr att känna till den slutliga filplatsen som rapporteras av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp och åtkomlig av Sonarr.
- Sonarr kommer att skanna den avslutade filplatsen efter filer som Sonarr kan använda. Den kommer att analysera filnamnet för att matcha det mot den begärda medias. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den angivna medieplatsen.
- Atomiska flyttar (direktflyttar) är aktiverade som standard. Filsystemet och monteringspunkterna måste vara desamma för din avslutade nedladdningskatalog och ditt mediebibliotek. Om den atomiska flytten misslyckas eller din konfiguration inte stöder hårddisklänkar och atomiska flyttar kommer Sonarr att falla tillbaka och kopiera filen och sedan ta bort den från källan, vilket är intensivt för I/O.
- Om alternativet "Completed Download Handling - Remove" är aktiverat i Sonarrs inställningar kommer eventuella överblivna filer från nedladdningen att skickas till papperskorgen eller återvinningen genom en begäran till din klient att ta bort nedladdningen.

## BitTorrent

- Sonarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Sonarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Denna övervakning sker via din nedladdningsklients API.
- Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (förhållande eller tid kan justeras i nedladdningsklienten eller från Sonarr under den specifika nedladdningsklienten). När filer importeras till din mediamapp kommer Sonarr att skapa en hårdlänk till filen om det stöds av din konfiguration, annars kopieras filen om hårddisklänkar inte stöds.
- Hårddisklänkar är aktiverade som standard. [En hårddisklänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringspunkterna måste vara desamma för din avslutade nedladdningskatalog och ditt mediebibliotek. Om skapandet av hårddisklänken misslyckas eller din konfiguration inte stöder hårddisklänkar kommer Sonarr att falla tillbaka och kopiera filen.
- Om alternativet "Completed Download Handling - Remove" är aktiverat i Sonarrs inställningar kommer Sonarr att ta bort torrenten från din klient och be klienten att ta bort torrentdata, men endast om klienten rapporterar att seedningen är klar och torrenten är stoppad (pausad vid slutförandet).

## Nedladdningsklienter

Klicka på `Inställningar` => `Nedladdningsklienter` och klicka sedan på <kb>+</kb> för att lägga till en ny nedladdningsklient. Din nedladdningsklient bör redan vara konfigurerad och igång.

### Stödda nedladdningsklienter

- En lista över stödda nedladdningsklienter finns på sidan [Mer information (Stödda)](/sonarr/supported#download-clients)

Välj den nedladdningsklient du vill lägga till, och det kommer att visas en popup-ruta för att ange anslutningsinformation. Dessa detaljer är liknande för de flesta klienter. Vissa kommer att be om användarnamn eller lösenord, vissa kommer att fråga om du vill lägga till nya nedladdningar i ett pausat/startat tillstånd, etc.

### Inställningar för Usenet-klient

- Namn - Namnet på nedladdningsklienten inom Sonarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en för din nedladdningsklient
- Port - Porten för din nedladdningsklient; detta är vanligtvis webgui-porten
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- (Avancerad inställning) URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxys.
- API-nyckel - API-nyckeln för att autentisera mot din klient
- Användarnamn - användarnamnet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Lösenord - lösenordet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Kategori - kategorin inom din nedladdningsklient som \*Arr kommer att använda. För att undvika orelaterade nedladdningar som visas i Aktivitet rekommenderas det starkt att ange en kategori.
- Prioritet för nyligen släppt media - nedladdningsklientens prioritet för nyligen släppt media
- Prioritet för äldre media - nedladdningsklientens prioritet för media som inte släpptes nyligen
- (Avancerad inställning) Klientprioritet - Prioritet för nedladdningsklienten. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet. 1 är högsta prioritet och 50 är lägsta prioritet
- Hantering av slutförda nedladdningar
  - Ta bort (Per klientinställning) - Ta bort slutförda nedladdningar när de är klara (usenet) eller stoppade/slutförda (torrenter). Se [Hantering av slutförda nedladdningar för mer information](#hantering-av-slutförda-nedladdningar)

### Inställningar för Torrent-klient

- Namn - Namnet på nedladdningsklienten inom Sonarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en för din nedladdningsklient
- Port - Porten för din nedladdningsklient
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- (Avancerad inställning) URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxys.
- Användarnamn - användarnamnet för att autentisera mot din klient
- Lösenord - lösenordet för att autentisera mot din klient
- Kategori - kategorin inom din nedladdningsklient som \*Arr kommer att använda. För att undvika orelaterade nedladdningar som visas i Aktivitet rekommenderas det starkt att ange en kategori.
- Kategori efter import - kategorin att ange efter att släppet har laddats ner och importerats. Observera att detta bryter hanteringen av borttagning av slutförda nedladdningar.
- Prioritet för nyligen släppt media - nedladdningsklientens prioritet för nyligen släppt media
- Prioritet för äldre media - nedladdningsklientens prioritet för media som inte släpptes nyligen
- Initialt tillstånd - Initialt tillstånd för torrenter (endast Qbittorrent: Tvingar förbigående av alla seed-trösklar)
- (Avancerad inställning) Klientprioritet - Prioritet för nedladdningsklienten. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet. 1 är högsta prioritet och 50 är lägsta prioritet
- Hantering av slutförda nedladdningar
  - Ta bort (Per klientinställning) - Ta bort slutförda nedladdningar när de är klara (usenet) eller stoppade/slutförda (torrenter). Se [Hantering av slutförda nedladdningar för mer information](#hantering-av-slutförda-nedladdningar)
    - För torrenter krävs att din nedladdningsklient pausar när seed-målen nås. Det kräver också att seed-målen stöds av Sonarr enligt tabellen nedan. Torrenter måste också vara i samma kategori.

### Kompatibilitet för borttagning av nedladdning i Torrent-klient

- Sonarr kan bara ställa in seed-förhållandet/tiden på klienter som stöder att ställa in detta värde via deras API när torrenten läggs till. Seed-mål kan ställas in globalt i klienten själv eller per spårare i \*Arr-inställningar för varje indexer. Se tabellen nedan för klientkompatibilitet.

|      Klient       |                                Förhållande                                |                                   Tid                                    |
| :---------------: | :---------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |   ![Stöds inte](https://img.shields.io/badge/Stöds-Nej-critical)   |
|      Deluge       |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |   ![Stöds inte](https://img.shields.io/badge/Stöds-Nej-critical)   |
| Download Station  | ![Stöds inte](https://img.shields.io/badge/Stöds-Nej-critical) |   ![Stöds inte](https://img.shields.io/badge/Stöds-Nej-critical)   |
|       Flood       |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |     ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)     |
|     Hadouken      | ![Stöds inte](https://img.shields.io/badge/Stöds-Nej-critical) |   ![Stöds inte](https://img.shields.io/badge/Stöds-Nej-critical)   |
|    qBittorrent    |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |     ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)     |
|     rTorrent      |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |     ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)     |
| Torrent Blackhole | ![Stöds inte](https://img.shields.io/badge/Stöds-Nej-critical) |   ![Stöds inte](https://img.shields.io/badge/Stöds-Nej-critical)   |
|   Transmission    |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Stöds-Idle%20Limit*-blue) |
|     uTorrent      |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |     ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)     |
|       Vuze        |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |     ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)     |

> ![Idle Limit](https://img.shields.io/badge/Stöds-Idle%20Limit*-blue) - Transmission har internt en kontroll för inaktiv tid, men Sonarr jämför den med seedningstiden om inaktivitetsgränsen är inställd för varje torrent. Detta görs som en lösning på Transmission's API-begränsningar.{.is-info}

## Hantering av slutförda nedladdningar

- Hantering av slutförda nedladdningar är hur Sonarr importerar media från din nedladdningsklient till dina serie-mappar. Många vanliga problem beror på felaktiga Docker-sökvägar och/eller andra Docker-behörighetsproblem.

- (Avancerad global inställning) Aktivera - Importera automatiskt slutförda nedladdningar från nedladdningsklienten
- (Per klientinställning) Ta bort - Ta bort slutförda nedladdningar när de är klara (usenet) eller stoppade/slutförda (torrenter)
  - För torrenter krävs att din nedladdningsklient pausar när seed-målen nås. Det kräver också att seed-målen stöds av Sonarr enligt tabellen ovan. Torrenter måste också vara i samma kategori.

### Ta bort slutförda nedladdningar

- Sonarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
- Sonarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- När nedladdningen är klar kommer Sonarr att känna till den slutliga filplatsen som rapporteras av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp.
- Sonarr kommer att skanna den avslutade filplatsen efter videofiler. Den kommer att analysera videofilens namn för att matcha den med en episod. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den tilldelade biblioteksmappen.
- Överblivna filer från nedladdningen kommer att skickas till papperskorgen eller återvinningen.

Om du laddar ner med en BitTorrent-klient är processen något annorlunda:

- Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda. När filer importeras till din tilldelade biblioteksmapp kommer Sonarr att försöka skapa en hårdlänk till filen eller falla tillbaka till att kopiera (använda dubbel plats) om hårddisklänkar inte stöds.
- Om alternativet "Completed Download Handling - Remove" är aktiverat i inställningarna kommer Sonarr att be torrentklienten att ta bort den ursprungliga filen och torrenten, men detta kommer bara att ske om klienten rapporterar att seedningen är klar, torrenten är i samma kategori (dvs. inte använder en kategori efter import) och torrenten är pausad (stoppad).

### Hantering av misslyckade nedladdningar

- Hantering av misslyckade nedladdningar är endast kompatibel med SABnzbd och NZBGet.
- Hantering av misslyckade nedladdningar gäller inte för torrenter och det finns inga planer på att lägga till en sådan funktion.

- Det finns flera komponenter som ingår i processen för hantering av misslyckade nedladdningar:

- Kontrollera nedladdare:
  - Kö - Kontrollera din nedladdares kö för lösenordsskyddade (krypterade) släpp som markeras som misslyckade
  - Historik - Kontrollera din nedladdares historik för misslyckande (t.ex. inte tillräckligt med block för att reparera eller extraheringen misslyckades)
- När Sonarr hittar en misslyckad nedladdning börjar den bearbeta dem och gör några saker:
  - Lägger till ett misslyckat händelse i Sonarrs historik
  - Tar bort den misslyckade nedladdningen från nedladdningsklienten för att frigöra utrymme och rensa nedladdade filer (valfritt)
  - Börjar söka efter en ersättningsfil (valfritt)
  - Blocklista (tidigare känd som 'Blacklisting') möjliggör automatiskt hopp över nzbs när de misslyckas, vilket innebär att nzb aldrig kommer att laddas ner automatiskt av Sonarr igen (du kan fortfarande tvinga nedladdningen via en manuell sökning).
  - Det finns 2 avancerade alternativ (på sidan 'Nedladdningsklient' inställningar) som styr beteendet för misslyckade nedladdningar i Sonarr, för närvarande är de alla aktiverade som standard.

- Ladda ner igen - Styr om Sonarr ska söka efter samma fil efter ett misslyckande
- (Avancerat alternativ) Ta bort - Om nedladdningen automatiskt ska tas bort från nedladdningsklienten när misslyckandet upptäcks

## Fjärrsökvägsmappningar

- Fjärrsökvägsmappning fungerar som en enkel sökning efter fjärrsökväg och ersättning med lokal sökväg. Detta används främst för antingen sammanslagna lokala/fjärrsökvägar med hjälp av mergerfs eller liknande, eller används när applikationen och nedladdningsklienten inte är på samma server.
- En fjärrsökvägsmappning används när din nedladdningsklient rapporterar en sökväg för slutförda data antingen på en annan server eller på ett sätt som \*Arr inte hanterar den mappen.
- Generellt sett krävs en fjärrsökvägsmappning endast om din nedladdningsklient körs på Linux när \*Arr körs på Windows eller vice versa. En fjärrsökvägsmappning kan också behövas om du blandar Docker- och nativa klienter eller om du använder en fjärrserver.
- En fjärrsökvägsmappning är en ENKEL sökning/ersättning (där den hittar VÄRDET FÖR FJÄRRSÖKVÄGEN och ersätter det med VÄRDET FÖR LOKAL SÖKVÄG för den angivna Värden).
- Om felmeddelandet om en felaktig sökväg inte innehåller VÄRDET SOM ERSATTS, fungerar inte sökvägsmappningen som du förväntar dig. Den vanliga lösningen är att lägga till och ta bort mappningen.
- [Se TRaSH's handledning för ytterligare information om fjärrsökvägsmappning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Om både \*Arr och din nedladdningsklient är Docker-containrar behövs sällan en fjärrsökvägsmappning. Det rekommenderas att du [granskar Docker-guiden](/docker-guide) och/eller [följer TRaSH's handledning](https://trash-guides.info/hardlinks)
{.is-info}

# Importlistor

> Information om stödda listtyper finns på sidan [Mer information (Stödda)](/sonarr/supported#lists) för den här sektionen
{.is-info}

## Listor

- Importlistor är en del av Sonarr som gör att du kan följa en given listskapare. Säg att du följer en viss listskapare på Trakt/TMDb och verkligen gillar deras ArrowVerse Collection-sektion och vill titta på varje show på deras lista. Du tittar i din Sonarr och inser att du inte har dessa serier. Istället för att söka en efter en och lägga till dessa objekt och sedan söka igenom dina indexeringstjänster efter dessa serier kan du göra allt detta på en gång med en lista. Listorna kan ställas in för att importera alla serier på den kurators lista samt att automatiskt tilldela en kvalitetsprofil, automatiskt lägga till och automatiskt övervaka dessa serier.

- VARNING: Om listor görs på fel sätt kommer de absolut att förstöra ditt bibliotek med en massa skräp som du inte har någon avsikt att titta på. Så se till att du vet vad du importerar innan du klickar på spara. Dvs. titta fysiskt på listan innan du ens går till Sonarr.

- Här kan du välja knappen <kb>+</kb> för att öppna ett nytt popup-fönster
- I detta nya fönster presenteras du med många olika alternativ för att konfigurera din lista från många olika listleverantörer. Som tidigare nämnts, var försiktig när du använder listor. Det rekommenderas starkt att inte välja knappen Sök vid tillägg innan du är helt säker på att listan du väljer/inställer lägger till de serier du letar efter.
- När du har valt listleverantören som du vill hämta från (t.ex. IMDb eller Trakt) kommer du att presenteras med ett nytt fönster.
De flesta inställningarna för listor är ganska självförklarande, vissa listor kräver att du autentiserar dig med leverantören som Trakt (vilket kräver att du har ett konto på Trakt.tv)

- Importera listexkludering - Detta gör det möjligt för dig att rensa din lista över serier som du inte vill se igen. Ett exempel på detta är om din lista råkar innehålla en serie på ett främmande språk och det är osannolikt att du någonsin kommer att hitta denna film på ditt modersmål och inte vill titta på den med undertexter. Du kan utesluta en serie från att läggas till i framtiden. Men i avsnittet för listexkludering kan du lägga till den igen i listan så att när listan körs igen kommer den att läsas in i din bibliotek.

# Anslutning

> Information om stödda anslutningstyper finns på sidan [Mer information (Stödda)](/sonarr/supported#notifications) för detta avsnitt
{.is-info}

## Anslutningar

- Anslutningar är hur du vill att Sonarr ska kommunicera med omvärlden.

- Genom att trycka på <kb>+</kb>-knappen kommer du att få upp ett nytt fönster där du kan konfigurera många olika slutpunkter

- En lista över stödda meddelanden och anslutningar finns på sidan [Mer information (Stödda)](/sonarr/supported#notifications)

## Anslutningstriggers

- Vid hämtning - Få meddelande när avsnitt är tillgängliga för nedladdning och har skickats till en nedladdningsklient
- Vid import - {Tidigare känd som Vid nedladdning} Få meddelande när avsnitt har importerats framgångsrikt
- Vid uppgradering - Få meddelande när avsnitt uppgraderas till bättre kvalitet
- Vid namnändring - Få meddelande när avsnitt byter namn
- Vid borttagning av serie - Få meddelande när serier tas bort
- Vid borttagning av avsnittsfiler - Få meddelande när avsnittsfiler tas bort
- Vid borttagning av avsnittsfiler för uppgradering - Få meddelande när avsnittsfiler tas bort för uppgraderingar
- Vid hälsoproblem - Få meddelande vid hälsokontrollfel
  - Inkludera hälsovarningar - Få meddelande om hälsovarningar utöver felmeddelanden.
- Vid programuppdatering - Få meddelande när Sonarr uppdateras till en ny version

# Metadata

## Metadata

> Information om stödda metadatakonsumenter finns på sidan [Mer information (Stödda)](/sonarr/supported#metadata) för detta avsnitt
{.is-info}

- Här kan du välja vilken typ av metadata som din mediaspelare ska använda

- Kodi kommer att vara ett av de vanligast använda alternativen här om det är den programvaran som används. Detta gör att Sonarr kan skapa en NFO-fil samt tillhörande filmposters som kan skrapas in i din spelare

# Taggar

- Taggavsnittet i Sonarr används för att koppla olika aspekter av Sonarr.
- Taggar är särskilt användbara för:
  - Fördröjningsprofiler
  - Utgivningsprofiler
  - Indexerare
- Taggar kan användas för att koppla samman Fördröjningsprofiler, Utgivningsprofiler, Indexerare och Serier.
- Till exempel:
  - Du vill bara att en specifik indexerare ska användas för en specifik serie. Du skulle skapa en tagg och tilldela serien och indexeraren den taggen.
  - Du vill att en specifik Utgivningsprofil bara ska använda en specifik Fördröjningsprofil. Du skulle skapa en tagg och tilldela Utgivningsprofilen och Fördröjningsprofilen den taggen.

> En serie kommer att använda både indexerare med matchande taggar och indexerare utan taggar.
{.is-warning}

> Observera: Taggar påverkar inte "Måste innehålla", "Får inte innehålla", "Föredragna" ord eller någon annan aspekt som inte nämns ovan.
{.is-info}

# Allmänt

## Värd

- Bindadress - Giltig IPv4-adress eller '*' för alla gränssnitt
  - 0.0.0.0 eller `*` - alla adresser kan ansluta
  - 127.0.0.1 eller localhost - endast program på localhost kan ansluta
  - Annan IP (t.ex. 1.2.3.4) - endast den IP-adressen (1.2.3.4) kan ansluta
- Portnummer - Portnumret som du vill använda för att komma åt webbgränssnittet för Sonarr

> Observera: Om du använder Docker ska du inte ändra den här inställningen.
{.is-warning}

- URL-bas - För stöd för omvänd proxy, standard är tomt

> Observera: Om du använder en omvänd proxy (exempel: mydomain.com/sonarr) ska du ange '/sonarr' som URL-bas.
{.is-info}

- Instansnamn - Instansnamn i flik och för Syslog-appnamn

> Om du kör flera instanser läggs instansnamnet till i webbläsarens fliknamn. {.is-info}

- Aktivera SSL - Om du har SSL-legitimationer och vill säkra kommunikationen till och från din Sonarr aktiverar du det här alternativet.

> Observera: Använd inte detta om du inte vet vad du gör.
{.is-warning}

## Säkerhet

- Autentisering - Hur vill du autentisera för att komma åt din Sonarr-instans
  - Ingen - Du har ingen autentisering för att komma åt din Sonarr. Detta är vanligt om du är den enda användaren i ditt nätverk, inte har någon på ditt nätverk som skulle vilja komma åt din Sonarr eller om din Sonarr inte är exponerad för webben
  - Grundläggande (webbläsarpopup) - Detta alternativ visar en liten popup när du går in på din Sonarr där du kan ange användarnamn och lösenord
  - Formulär (inloggningssida) - Detta alternativ har en bekant inloggningsruta liknande andra webbplatser för att du ska kunna logga in på din Sonarr
- API-nyckel - Så här kommunicerar andra program eller har Sonarr kommunicera med andra program. Om den här nyckeln ges till fel person med åtkomst kan den göra alla möjliga saker med ditt bibliotek. Detta är varför API-nyckeln är maskerad i loggarna
- Certifikatvalidering - Ändra hur strikt HTTPS-certifikatvalidering är
  - Aktiverad - Validera alla HTTPS-certifikat (rekommenderas)
  - Inaktiverad för lokala adresser - Validera alla HTTPS-certifikat utom de på localhost och LAN
  - Inaktiverad - Validera inga HTTPS-certifikat

## Proxy

- Proxy - Det här alternativet gör att du kan köra informationen som Sonarr hämtar och söker igenom en proxy. Detta kan vara användbart om du befinner dig i ett land som inte tillåter nedladdning av torrentfiler

- Använd proxy - Aktivera för att använda en proxy
- Proxytyp - Välj din proxytyp (HTTPS, Socks4 eller Socks5)
- Värdnamn - Ange ditt proxy-värdnamn (Inkludera inte http/https eller någon annan protokoll)
- Port - Ange din proxyport
- Användarnamn - Ange ditt proxyanvändarnamn om det är tillämpligt
- Lösenord - Ange ditt proxylösenord om det är tillämpligt
- Ignorerade adresser - Ange en kommaseparerad lista över adresser som ska undantas från proxyt
- Bypassa proxy för lokala adresser - Markera rutan för att bypassa proxyt för lokala adresser. Lokala förfrågningar identifieras genom avsaknaden av en punkt (.) i URI:et, som i <http://webserver/>, eller genom att komma åt den lokala servern, inklusive <http://localhost>, <http://loopback> eller <http://127.0.0.1>. När detta inte är markerat görs alla internetförfrågningar via proxyservern.

## Loggning

- Loggnivå - Förmodligen ett av de mest användbara felsökningsverktygen
  - Info - Detta är det mest grundläggande sättet som Sonarr samlar information på, detta kommer att inkludera mycket minimal mängd information i loggarna. Denna loggfil innehåller fatala, fel, varningar och info-poster.
  - Debug - Debug kommer att inkludera all information som Info inkluderar plus mer information som kan vara användbar. Denna loggfil innehåller fatala, fel, varningar, info och debug-poster
  - Spårning - Den mest avancerade och detaljerade loggningen på Sonarr, Spårning kommer att inkludera all information som samlas in av Info och Debug och mer. Detta är den vanligaste typen av logg som kommer att begäras vid felsökning på Discord eller Reddit. Om du behöver hjälp väljer du din logg till Spårning och gör om uppgiften som gav dig problem för att fånga loggen. Denna loggfil innehåller fatala, fel, varningar, info, debug och spårningsposter.

## Analys

- Analys - Skicka anonym användnings- och felinformation till Sonarrs servrar (SkyHook). Detta inkluderar information om din webbläsare, vilka Sonarr WebUI-sidor du använder, felrapportering samt OS- och runtime-version. Vi kommer att använda denna information för att prioritera funktioner och felkorrigeringar.

## Uppdateringar

- (Avancerad inställning) Gren - Detta är grenen av Sonarr som du kör på.
  - [Se den här FAQ-posten för mer information](/sonarr/faq#how-do-i-update-sonarr)
- Automatisk - Ladda ner och installera uppdateringar automatiskt. Du kommer fortfarande att kunna installera från System: Uppdateringar. Obs: Windows-användare uppdateras alltid automatiskt.
- Mekanism - Använd Sonarrs inbyggda uppdaterare eller ett skript
  - Inbyggd - Använd Sonarrs egen uppdaterare
  - Skript - Låt Sonarr köra uppdateringsskriptet
  - Docker - Uppdatera inte Sonarr från insidan av Docker, dra istället en helt ny bild med den nya uppdateringen
  - Apt - Ställs in av Debian/Ubuntu-paketet när uppdatering hanteras uteslutande via Apt
- Skript - Synligt endast när Mekanism är inställd på Skript - Sökväg till uppdateringsskript
- Uppdateringsprocess - Sonarr kommer att ladda ner uppdateringsfilen, verifiera dess integritet och extrahera den till en temporär plats och anropa den valda metoden. Uppdateringsprocessen körs under samma användare som Sonarr körs under, den behöver behörighet att uppdatera Sonarr-filerna samt stoppa/starta Sonarr.
- Inbyggd - Den inbyggda metoden kommer att säkerhetskopiera Sonarr-filer och inställningar, stoppa Sonarr, uppdatera installationen och starta Sonarr igen. Om ditt system inte klarar av att stoppa Sonarr och försöker starta om det automatiskt kan det vara bäst att använda ett skript istället. Vid misslyckande kommer den tidigare versionen av Sonarr att startas om.
- Skript - Skriptet bör hantera samma saker som den inbyggda uppdateraren, om du behöver hantera stopp och start av tjänster (upstart/launchd/etc) måste du göra det här.

## Säkerhetskopior

- Säkerhetskopieringsavsnittet gör att du kan ange hur du vill att Sonarr ska hantera säkerhetskopior

- Mapp - Detta gör att du kan välja platsen för säkerhetskopieringen. I Docker kommer du att vara begränsad till vad du tillåter att behållaren ser. Sökvägar är relativa till appdata-mappen; om det behövs kan du ange en absolut sökväg för att säkerhetskopiera utanför appdata-mappen.
- Intervall - Hur ofta vill du att Sonarr ska göra en säkerhetskopia
- Förvaring - Hur länge vill du att Sonarr ska behålla varje säkerhetskopia. Efter att en ny säkerhetskopia har gjorts kommer den äldsta säkerhetskopian att tas bort

# Användargränssnitt

## Kalender

- Första veckodagen - Här kan du välja vilken dag du tycker att veckan ska börja på.
- Kolumnrubrik för vecka - Här kan du välja rubriken för kolumnerna

## Datum

- Kort datumformat - Hur vill du att Sonarr ska visa korta datum?
- Långt datumformat - Hur vill du att Sonarr ska visa långa datumformat?
- Tidsformat - Vill du ha ett 12-timmars eller 24-timmars format?
- Visa relativa datum - Vill du att Sonarr ska visa relativa (Idag/Igår/etc) eller absoluta datum?

## Stil

- Aktivera färgblind läge - Ändrad stil för att färgblinda användare bättre ska kunna skilja färgkodad information