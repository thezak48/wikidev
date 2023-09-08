---
title: Radarr-inställningar
description: Beskrivning av Radarrs inställningsmenyer
published: true
date: 2023-08-27T22:02:11.780Z
tags: radarr, behöver-kärlek, inställningar
editor: markdown
dateCreated: 2021-05-29T15:57:25.304Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Menyalternativ](#menyalternativ)
- [Mediahantering](#mediahantering)
  - [Förslag på gemensam namngivning](#förslag-på-gemensam-namngivning)
  - [Namngivning av filmer](#namngivning-av-filmer)
    - [Standardformat för filmer](#standardformat-för-filmer)
    - [Namngivning av filmer](#namngivning-av-filmer-1)
    - [Film-ID](#film-id)
    - [Kvalitet](#kvalitet)
    - [Medieinformation](#medieinformation)
    - [Releasegrupp](#releasegrupp)
    - [Utgåva](#utgåva)
    - [Anpassade format (namngivning)](#anpassade-format-namngivning)
    - [Original](#original)
  - [Format för mappar för filmer](#format-för-mappar-för-filmer)
    - [Namngivning av filmer](#namngivning-av-filmer-2)
    - [Film-ID](#film-id-1)
  - [Mappar](#mappar)
  - [Importering](#importering)
  - [Filhantering](#filhantering)
  - [Behörigheter](#behörigheter)
  - [Rotmappar](#rotmappar)
- [Profiler](#profiler)
  - [Kvalitetsprofiler](#kvalitetsprofiler)
  - [Fördröjningsprofiler](#fördröjningsprofiler)
    - [Användningsområden](#användningsområden)
    - [Hur fördröjningsprofiler fungerar](#hur-fördröjningsprofiler-fungerar)
      - [Exempel](#exempel)
        - [Exempel 1](#exempel-1)
        - [Exempel 2](#exempel-2)
        - [Exempel 3](#exempel-3)
- [Kvalitet](#kvalitet-1)
  - [Betydelser för kvalitetstabell](#betydelser-för-kvalitetstabell)
  - [Definierade kvaliteter](#definierade-kvaliteter)
- [Anpassade format](#anpassade-format)
  - [Villkor för anpassade format](#villkor-för-anpassade-format)
    - [Modifierare](#modifierare)
    - [Villkor](#villkor)
    - [Inställningar och rangordning för profilering](#inställningar-och-rangordning-för-profilering)
      - [Importera/exportera anpassade format](#importeraexportera-anpassade-format)
      - [Importera/uppdatera befintliga anpassade format](#importerauppdatera-befintliga-anpassade-format)
    - [Samling av anpassade format](#samling-av-anpassade-format)
- [Indexerare](#indexerare)
  - [Stödda indexerare](#stödda-indexerare)
    - [Inställningar för indexerare](#inställningar-för-indexerare)
    - [Konfiguration av Usenet-indexerare](#konfiguration-av-usenet-indexerare)
    - [Konfiguration av torrentspårare](#konfiguration-av-torrentspårare)
      - [Flaggor för indexerare](#flaggor-för-indexerare)
  - [Alternativ](#alternativ)
  - [Begränsningar](#begränsningar)
- [Nedladdningsklienter](#nedladdningsklienter)
  - [Översikt](#översikt)
  - [Processer för nedladdningsklienter](#processer-för-nedladdningsklienter)
    - [Usenet-process](#usenet-process)
    - [Torrent-process](#torrent-process)
  - [Nedladdningsklienter](#nedladdningsklienter-1)
    - [Stödda nedladdningsklienter](#stödda-nedladdningsklienter)
    - [Inställningar för Usenet-klienter](#inställningar-för-usenet-klienter)
    - [Inställningar för torrentklienter](#inställningar-för-torrentklienter)
    - [Kompatibilitet för borttagning av nedladdning i torrentklienter](#kompatibilitet-för-borttagning-av-nedladdning-i-torrentklienter)
  - [Hantering av slutförda nedladdningar](#hantering-av-slutförda-nedladdningar)
    - [Ta bort slutförda nedladdningar](#ta-bort-slutförda-nedladdningar)
    - [Hantering av misslyckade nedladdningar](#hantering-av-misslyckade-nedladdningar)
  - [Fjärrmappmappningar](#fjärrmappmappningar)
- [Importlistor](#importlistor)
  - [Listor](#listor)
  - [Alternativ för listor](#alternativ-för-listor)
  - [Undantag för listor](#undantag-för-listor)
- [Anslutning](#anslutning)
  - [Anslutningar](#anslutningar)
  - [Anslutningstriggers](#anslutningstriggers)
- [Metadata](#metadata)
  - [Alternativ](#alternativ-1)
  - [Metadatakonsumenter](#metadatakonsumenter)
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
  - [Filmer](#filmer)
  - [Datum](#datum)
  - [Stil](#stil)
  - [Språk](#språk)

Den här sidan kommer att gå igenom alla tillgängliga inställningar i Radarr och hur de fungerar. Detta är inte menat att vara en omfattande "hur man ställer in Radarr". Om du vill ha det, använd istället [Snabbstartsguiden](/radarr/snabbstartsguide) sidan.

# Menyalternativ

För att komma till inställningssidan, välj Inställningar från sidofältet. Följande undermenyalternativ kommer att vara tillgängliga:

![settings_1_menu.png](/assets/radarr/settings_1_menu.png)

Observera också att för varje enskild inställningssida finns det några alternativ längst upp i menyn:

![settings_2_topmenu.png](/assets/radarr/settings_2_topmenu.png)

- Dölj/Visa avancerade är viktigt för alla objekt som är markerade nedan som `(Avancerad inställning)`, annars kommer de inte att visas. Dessa menyalternativ visas i orange i skärmbilderna.

- Du måste spara dina ändringar innan du lämnar skärmen. Du gör det genom att klicka på diskikonet. Om du inte har gjort några ändringar kommer det att stå "Inga ändringar" och vara grått, som visas ovan.

# Mediahantering

> Vissa av dessa inställningar är bara synliga genom att använda `Visa avancerade inställningar` som finns i toppfältet under sökfältet{.is-info}

## Förslag på gemensam namngivning

> Nedan finns några förslag på gemensam namngivning från [TRaSH's Guides](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/) {.is-info}

### Filmfiler

- Radarr v4.2.2.6489 eller senare

`{Film RensatTitel} {(Utgivningsår)} {imdb-{ImdbId}} {utgåva-{Utgåva Taggar}} {[Anpassade format]}{[Kvalitet Full]}{[MedieInfo 3D]}{[MedieInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}]{MediaInfo AudioLanguages}[{Mediainfo VideoCodec}]{-Releasegrupp}`

- Äldre versioner av Radarr

`{Film RensatTitel} {(Utgivningsår)} {Utgåva Taggar} [imdb-{ImdbId}]{[Anpassade format]}{[Kvalitet Full]}{[MedieInfo 3D]}{[MedieInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}][{Mediainfo VideoCodec}]{-Releasegrupp}`

### Mappar för filmer

`{Film RensatTitel} ({Utgivningsår})`

## Namngivning av filmer

- Byt namn på filmer - Om detta inte är markerat kommer Radarr att använda det befintliga namnet om namnändring är inaktiverat
  - Om det inte är markerat:
    - Import av nedladdningsklient
      - Nedladdningsklientens utgåvotitel används
    - Manuell (ad hoc) import: Ursprungligt filnamn
- Ersätt otillåtna tecken - Om detta inte är markerat kommer Radarr istället att ta bort dem.

  - Tecknen är: `:` `\` `/` `>` `<` `?` `*` `|` `"`
- Ersättning för kolon (`:`) - Denna inställning styr hur Radarr hanterar kolon inom filnamnet. Detta är endast tillgängligt när ersättning för otillåtna tecken är aktiverat.
  - Ta bort - Självförklarande
    - Exempel: Film,The.mkv => FilmThe.mkv
  - Ersätt med bindestreck - Tar bort kolonet och lägger till ett bindestreck på dess plats
    - Exempel: Film,The.mkv => Film-The.mkv
  - Ersätt med mellanslag - Tar bort kolonet och lägger till ett mellanslag på dess plats
    - Exempel: Film,The.mkv => Film The.mkv
  - Ersätt med mellanslag bindestreck mellanslag - självförklarande
    - Exempel: Film,The.mkv => Film - The.mkv

### Standardformat för filmer

- Här väljer du namnkonventionen för dina filmer

- Rullgardinsmeny (övre högra hörnet)
  - Vänster ruta - Hantering av mellanslag
    Mellanslag ( ) - Använd mellanslag i namngivningen (standard)
    Punkter (.) - Använd punkter istället för mellanslag i namngivningen
    Understreck (_) - Använd understreck istället för mellanslag i namngivningen
    Bindestreck (-) - Använd bindestreck istället för mellanslag i namngivningen
  - Höger ruta - Hantering av gemener/versaler
    Standardläge - Gör titeln både versaler och gemener (~camel-case) (standard)
    Versaler - Gör hela titeln versaler
    Gemener - Gör hela titeln gemener

### Namngivning av filmer

- `{Film Titel}` = Filmens titel!
- `{Film Titel:DE}` = Filmtitel
- `{Film RensatTitel}` = Filmens titel!
- `{Film TitelThe}` = Filmens titel!, The
- `{Film OriginalTitel}` = Τίτλος ταινίας
- `{Film RensadOriginalTitel}` = Τίτλος ταινίας
- `{Film TitelFörstaTecken}` = S
- `{Film Samling}` = Filmkollektionen
- `{Film Certifiering}` = R
- `{Utgivningsår}` = 2009

`RensatTitel` [gör följande](https://github.com/Radarr/Radarr/blob/5948f564827eabb7afc1e89bf4a5987e3c71dc74/src/NzbDrone.Core/Organizer/FileNameBuilder.cs#L207):

- Ersätt `&` med `and`
- Ersätt `/` och `\` med ` `
- Ta bort `,`,`<`,`>`,`/`,`\`,`;`,`:`,`'`,`|`, `~`,`!`,`?`,`@`,`$`,`%`,`^`,`*`,`-`,`_`,`=` enligt följande regex:

```regex
(?<=\s)(,|<|>|\/|\\|;|:|'|""|\||`|~|!|\?|@|$|%|^|\*|-|_|=){1}(?=\s)|('|:|\?|,)(?=(?:(?:s|m)\s)|\s|$)|(\(|\)|\[|\]|\{|\})
```

### Film-ID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

> Imdb-taggar som används i Plex namngivningsformat kommer att döljas villkorligt när värdet är tomt `{imdb-{ImdbId}}` {.is-info}

### Kvalitet

- `{Kvalitet Full}` = HDTV 720p Riktig
- `{Kvalitet Titel}` = HDTV 720p

### Medieinformation

- `{MedieInfo Enkel}` = x264 DTS
- `{MedieInfo Full}` = x264 DTS \[EN+DE\]
- `{MedieInfo AudioCodec}` = DTS
- `{MedieInfo AudioChannels}` = 5.1
- `{MedieInfo AudioLanguages}` = \[EN+DE\]
- `{MedieInfo SubtitleLanguages}` = \[EN\]
- `{MedieInfo VideoCodec}` = x264
- `{MedieInfo VideoBitDepth}` = 8
- `{MedieInfo VideoDynamicRange}` = HDR
- `{MedieInfo VideoDynamicRangeType}` = DV HDR10

> `MedieInfo Full`, `AudioLanguages` och `SubtitleLanguages` stöder för närvarande inte ett suffix `:EN+DE` som tillåts i Sonarr för att filtrera språken som ingår i filnamnet. Det finns en öppen [fråga](https://github.com/Radarr/Radarr/issues/4710) om detta.
~~`MedieInfo Full`, `AudioLanguages` och `SubtitleLanguages` stöder ett suffix `:EN+DE` som gör att du kan filtrera språken som ingår i filnamnet. Använd `-DE` för att exkludera specifika språk. Om du lägger till <kb>+</kb> (t.ex.: `:EN+`) kommer det att generera `[EN]`,`[EN+--]` eller `[--]` beroende på vilka språk som är exkluderade. Till exempel - `{MedieInfo Full:EN+DE}`.~~
{.is-info}

> `MedieInfo VideoDynamicRangeType` ger möjliga värden: DV, DV HDR10, DV HLG, DV SDR, HDR10, HDR10Plus, HLG och PQ.
{.is-info}

### Releasegrupp

- `{Releasegrupp}` = Rls Grp

### Utgåva

- `{Utgåva Taggar}` = IMAX

> Från och med v4.2.2.6489 kommer utgåvotaggar som används i Radarr efter Plex namngivningsformatet `{utgåva-{Utgåva Taggar}}` att döljas villkorligt som `{-Grupp}` gör när värdet för utgåvotaggar är tomt
{.is-info}

### Anpassade format (namngivning)

- `{Anpassade format}` = Surroundljud x264

> Anpassade format kommer att vara det bokstavliga namnet på det anpassade formatet och kräver att det anpassade formatet är aktiverat för att inkluderas i namngivningen {.is-info}

### Original

- `{Original Titel}` = Film.Titel.HDTV.x264-EVOLVE
- `{Original Filnamn}` = Film.titel.hdtv.x264-EVOLVE

> `Original Titel` är utgåvotiteln och det är vad som föreslås att användas.
{.is-info}

>`Original Filnamn` rekommenderas inte. Det är det bokstavliga ursprungliga filnamnet och kan vara förvrängt `t1i0p3s7i8yuti`.{.is-warning}

## Format för mappar för filmer

Här ställer du in namnkonventionen för mappen som innehåller säsongsmapparna eller filmfilerna. Klicka på `?` för att öppna dialogrutan `Mappnamnstokens`.

### Namngivning av filmer

- `{Film Titel}` = Filmtitel!
- `{Film Titel:DE}` = Filmtitel
- `{Film RensatTitel}` = Filmtitel
- `{Film TitelThe}` = Filmtitel, The
- `{Film OriginalTitel}` = Τίτλος ταινίας
- `{Film TitelFörstaTecken}` = S
- `{Film Samling}` = Filmkollektionen
- `{Film Certifiering}` = R
- `{Utgivningsår}` = 2009

### Film-ID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

## Mappar

- Skapa tomma mediamappar - Skapa saknade filmmappar under diskgenomsökningen
- Ta bort tomma mappar - Ta bort tomma filmmappar under diskgenomsökningen och när filmfiler tas bort

## Importering

- Hoppa över kontroll av ledigt utrymme - Använd när Radarr inte kan upptäcka ledigt utrymme från din rotmapp för serier
- Minsta lediga utrymme - Omkoppling av detta förhindrar import om det skulle lämna mindre än denna mängd diskutrymme tillgängligt
- Använd hårda länkar istället för kopiering - Använd hårda länkar när du försöker kopiera filer från torrents som fortfarande seedas

  - För mer information om detta klicka [här](https://trash-guides.info/hardlinks)

> Sällan - men möjligtvis - kan filåtkomsthindringar förhindra att filer som fortfarande seedas byter namn. Du kan tillfälligt inaktivera seedning och använda Radarrs funktion för att byta namn som en lösning.
{.is-warning}

- Importera extra filer - Importera matchande extrafiler (undertexter, nfo, etc.) efter import av en fil

## Filhantering

- Avmarkera borttagna filmer - Filmer som har tagits bort från disken avmarkeras automatiskt i Radarr.
- Ladda ner korrekta och repacks - Om du vill uppgradera automatiskt till korrekta och repacks. Använd "Föredrar inte" för att sortera efter föredragna ordpoäng över korrekta och repacks.

  - Föredrar och uppgradera - Ranka repacks och korrekta högre än icke-repacks och icke-korrekta. Behandla nya repacks och korrekta som uppgraderingar till nuvarande versioner.
  - Uppgradera inte automatiskt - Ranka repacks och korrekta högre än icke-repacks och icke-korrekta. Behandla inte nya repacks och korrekta som uppgraderingar till nuvarande versioner.
  - Föredrar inte - Ignorera effektivt repacks och korrekta. Du måste hantera eventuella preferenser för dessa med [Anpassade format](#anpassade-format).

> \* `KORREKT` - betyder att det fanns ett problem med den tidigare versionen. Nedladdningar som är märkta som KORREKT visar att problemen har åtgärdats i den versionen. Detta görs av en grupp som inte släppte originalet.
> \* `REPACK` - betyder att det fanns ett problem med den tidigare versionen och att det har åtgärdats av den ursprungliga gruppen. Nedladdningar som är märkta som REPACK visar att problemen har åtgärdats i den versionen. Detta görs av en grupp som släppte originalet.
{.is-info}

> [Använd anpassade format för automatiska uppgraderingar till korrekta och repacks](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)
{.is-info}

- Analysera videofiler - Extrahera filinformation som upplösning, speltid och codec-information från filer. Detta kräver att Radarr läser delar av filen vilket kan orsaka hög disk- eller nätverksaktivitet under skanningar.
- Skanna om filmkatalog efter uppdatering
  - Alltid - Detta kommer att skanna filmkataloger baserat på schemalagda uppgifter. Detta rekommenderas för de flesta fall, inklusive om du använder Bazarr.
  - Efter manuell uppdatering - Du måste manuellt skanna disken. Detta rekommenderas för användare av molnlagring.
  - Aldrig - Precis som det låter, skanna aldrig filmkatalogerna. Detta rekommenderas inte.
- Ändra filens datum - Ändra filens datum vid import/skanning
  - Ingen - Radarr kommer inte att ändra datumet som visas i din filhanterare
  - Datum för biografvisning - Datumet då filmen släpptes på bio.
  - Datum för fysisk utgivning - Datumet då filmen släpptes antingen på skiva (fysiskt) eller på webben.
- Återvinningskorg - Filmer kommer att hamna här när de tas bort istället för att raderas permanent
- Städning av återvinningskorgen - Så gammal en given fil kan vara innan den raderas permanent

> Filer i återvinningskorgen som är äldre än det valda antalet dagar kommer att rensas automatiskt {.is-warning}

## Behörigheter

- Ange behörigheter - Ska `chmod` köras när filer importeras/ändras namn?
  - chmod-mapp - Oktal, tillämpas vid import/ändring av behörigheter för mediamappar och filer (utan körbara bitar)

> Listan i rullgardinsmenyn har en förinställd lista över mycket vanligt använda behörigheter som kan användas. Du kan dock manuellt ange en oktal för mappen om du vill.{.is-info}

> Detta fungerar bara om användaren som kör `Radarr` är ägare till filen. Det är bättre att se till att nedladdningsklienten ställer in behörigheterna korrekt.{.is-warning}

- chown-grupp - Gruppnamn eller GID. Använd GID för fjärrfiler

> Detta fungerar bara om användaren som kör `Radarr` är ägare till filen. Det är bättre att se till att nedladdningsklienten ställer in behörigheterna korrekt.{.is-warning}

## Rotmappar

- Sökväg - Detta visar sökvägen till din mediebibliotek
- Ledigt utrymme - Detta är det lediga utrymmet som rapporteras till Radarr från systemet
- Omapperade mappar - Detta är mappar som inte har en film associerad med dem

> "X" i slutet kommer att ta bort denna rotmapp
{.is-info}

- Lägg till rotmapp - Detta gör att du kan välja en rotmapp för att antingen placera nya importerade nedladdningar i denna mapp eller att låta Radarr skanna befintliga medier.

> Användare som inte använder Windows:
> \* Om du använder en NFS-montage, se till att `nolock` är aktiverat.
> \* Om du använder en SMB-montage, se till att `nobrl` är aktiverat.
{.is-warning}

# Profiler

## Kvalitetsprofiler

- Ange profiler för kvaliteten på filmer du vill ladda ner.

> När du väljer en befintlig profil eller lägger till en ytterligare profil kommer ett nytt fönster att visas{.is-info}

> Observera: Kvaliteten som har en blå ruta är kvaliteten som media med denna profil kommer att fortsätta att uppgraderas till.
{.is-info}

- Plus-ikonen (<kb>+</kb>) - Skapa en ny kvalitetsprofil

- Namn - Välj ett **UNIKT** namn för den kvalitetsprofil du skapar
- Uppgraderingar tillåtna - När detta alternativ är markerat och du berättar för Radarr att ladda ner en `WEB 1080p` eftersom det är den första versionen av en specifik film, kommer Radarr automatiskt att uppgradera till bättre kvalitet ***om*** `Uppgradera till` har den kvaliteten vald
- Uppgradera till - När denna kvalitet har uppnåtts kommer Radarr inte längre att ladda ner filmer

> Observera: Detta gäller endast om du har `Bluray-1080p` högre än `WEB 1080p` inom avsnittet `Kvaliteter`
{.is-warning}

- Kvaliteter - Kvaliteter högre upp i listan är mer föredragna även om de inte är markerade. Kvaliteter inom samma grupp är likvärdiga. Endast markerade kvaliteter önskas.
  - Redigera grupper - Vissa kvaliteter grupperas för att minska storleken på listan samt gruppera liknande versioner. Ett bra exempel på detta är `WebDL` och `WebRip` eftersom dessa är mycket liknande och vanligtvis har liknande bitrates. När du redigerar grupperna kan du ändra preferensen inom varje grupp. [Se TRaSH's Guide för hur man slår samman kvaliteter](https://trash-guides.info/merge-quality)

  - [Se Kvaliteter](#kvaliteter-definierade)

> Som standard är kvaliteterna inställda från lägsta (botten) till högsta (topp)
{.is-info}

- Språk - Välj ditt föredragna språk

- Anpassat format - Radarr betygsätter varje version med hjälp av summan av poäng för matchande anpassade format. Om en ny version skulle förbättra poängen, med samma eller bättre kvalitet, kommer Radarr att hämta den.
Se [Anpassade format](#anpassade-format) för mer information.

## Fördröjningsprofiler

- Fördröjningsprofiler gör det möjligt att minska antalet nedladdningar av en film genom att lägga till en fördröjning medan Radarr fortsätter att leta efter versioner som bättre matchar dina preferenser.
- Föredraget protokoll - Detta kommer antingen att vara `Usenet` eller `Torrent` beroende på vilket nedladdningsprotokoll du föredrar
- Usenet-fördröjning - Ange antalet minuter du vill vänta innan nedladdningen startar
- Torrent-fördröjning - Ange antalet minuter du vill vänta innan nedladdningen startar
- Bypassa om högsta kvalitet - Bypassa fördröjningen när en version har den högsta aktiverade kvalitetsprofilen med det föredragna protokollet
- Taggar - Genom att ge denna fördröjningsprofil en tagg kan du tagga en given film för att den ska följa reglerna som anges här.
- Skiftnyckelikonen - Detta gör att du kan redigera fördröjningsprofilen
- Plus-ikonen (<kb>+</kb>) - Skapa en ny fördröjningsprofil

### Användningsområden

Vissa medier får ett halvt dussin olika versioner av varierande kvalitet under timmarna efter en release, och utan fördröjningsprofiler kan Radarr försöka ladda ner alla. Med fördröjningsprofiler kan Radarr konfigureras för att ignorera de första timmarna av versioner.

Fördröjningsprofiler är också användbara om du vill betona ett protokoll (Usenet eller BitTorrent) över det andra. (Se exempel 3)

### Hur fördröjningsprofiler fungerar

Timern startar så snart Radarr upptäcker att en film har en tillgänglig version. Denna version visas i din kö med en klockikon för att indikera att den är under fördröjning.

> Klockan startar från uppladdningstiden för versionen och inte från den tidpunkt då Radarr ser den.
{.is-info}

Under fördröjningsperioden kommer Radarr att notera eventuella nya versioner som blir tillgängliga. När fördröjningstimern löper ut kommer Radarr att ladda ner den enskilda version som bäst matchar dina kvalitetspreferenser.

Tidpunkten för timern kan vara olika för Usenet och Torrents. Varje profil kan associeras med en eller flera taggar för att du ska kunna anpassa vilka filmer som har vilka profiler. En fördröjningsprofil utan tagg betraktas som standard och gäller för alla filmer som inte har en specifik tagg.

> Fördröjningsprofiler startar från tidpunkten då indexeraren rapporterar att versionen laddades upp. Det innebär att innehåll som är äldre än det antal minuter du har ställt in inte påverkas på något sätt av din fördröjningsprofil och kommer att laddas ner omedelbart. Dessutom kommer **alla manuella sökningar** efter innehåll (sökningar som inte är RSS-flöden) att ignorera inställningarna för fördröjningsprofilen.
{.is-warning}

#### Exempel

- För varje exempel, anta att användaren har följande kvalitetsprofil aktiv: WebDL-720p och högre är tillåtna, WebDL-1080p är kvalitetsgränsen, BluRay1080p är den högst rankade kvaliteten

##### Exempel 1

- I detta enkla exempel är profilen inställd med en 120 minuters (två timmar) fördröjning för både Usenet och Torrent.

- Klockan 23:00 upptäcker Radarr den första versionen av en film och den laddades upp kl. 22:50 och 120 minuters klockan börjar ticka. Kl. 00:50 kommer Radarr att utvärdera alla versioner som har hittats under de senaste två timmarna och ladda ner den bästa versionen, som är WebDL 720p.

- Kl. 03:00 hittas en annan version, som är WebDL 720p och lades till i din indexer kl. 02:46. En annan 120 minuters klocka börjar ticka. Kl. 04:46 laddas den bästa tillgängliga versionen ner. Eftersom kvalitetsgränsen nu har nåtts kan filmen inte längre uppgraderas och Radarr kommer att sluta leta efter nya versioner.

- Vid vilken tidpunkt som helst, om en WebDL 1080p-version hittas, kommer den att laddas ner omedelbart eftersom det är den högst rankade kvaliteten. Om det finns en aktiv fördröjningstimer kommer den att avbrytas.

##### Exempel 2

- Detta exempel har olika timrar för Usenet och Torrents. Anta en 120 minuters timer för Usenet och en 180 minuters timer för BitTorrent.

- Kl. 23:00 upptäcker Radarr den första versionen av en film och båda timrarna börjar ticka. Versionen lades till i indexeraren kl. 22:15. Kl. 00:15 kommer Radarr att utvärdera alla versioner och om det finns några acceptabla Usenet-versioner kommer den bästa att laddas ner och båda timrarna kommer att sluta ticka. Om inte kommer Radarr att vänta tills kl. 00:15 och ladda ner den bästa versionen, oavsett vilken källa den kommer från.

##### Exempel 3

- Ett vanligt användningsområde för fördröjningsprofiler är att betona ett protokoll över det andra. Till exempel kan du bara vilja ladda ner en BitTorrent-version om inget har laddats upp på Usenet efter en viss tid.

- Du kan ställa in en 60 minuters timer för BitTorrent och en 0 minuters timer för Usenet.

- Om den första versionen som upptäcks kommer från Usenet kommer Radarr att ladda ner den omedelbart.

- Om den första versionen kommer från BitTorrent kommer Radarr att ställa in en 60 minuters timer. Om någon kvalificerad Usenet-version upptäcks under den tiden kommer BitTorrent-versionen att ignoreras och Usenet-versionen kommer att laddas ner.

## Versionsprofiler

- Här kan du ställa in globala begränsningar baserat på ett par parametrar
- Klicka på <kb>+</kb> och ett nytt fönster öppnas
- Måste innehålla - Här kan du tala om för Radarr att om en version inte innehåller en viss sträng kommer Radarr inte att ladda ner den versionen. Detta är inte skiftlägeskänsligt som standard och regex kan användas.
- Får inte innehålla - Här kan du tala om för Radarr att om en version innehåller en viss sträng kommer Radarr inte att ladda ner den versionen. Detta är inte skiftlägeskänsligt som standard och regex kan användas.
- Taggar - Här kan du tillämpa dessa inställningar på filmer med minst en av de angivna [taggarna](#taggar).

# Kvalitet

## Betydelser för kvalitetstabell

- Kvalitet - Namnet på kvaliteten enligt scenen (hårdkodad)
- Titel - Namnet på kvaliteten i gränssnittet (konfigurerbar)
- Megabyte per minut - Självförklarande
- Storleksgräns - Självförklarande
- Min - Det minsta antalet megabyte per minut (MB/min) som en kvalitet kan ha.
- Föredragen - Det föredragna antalet megabyte per minut (MB/min) som en kvalitet kan ha.
- Max - Det maximala antalet megabyte per minut (MB/min) som en kvalitet kan ha.

## Definierade kvaliteter

- Okänd - Självförklarande
- SDTV - Efterluftning från en analog källa (vanligtvis kabel-TV eller OTA-standardupplösning). Bildkvaliteten är generellt sett bra (för upplösningen) och de är vanligtvis kodade i DivX/XviD eller MP4.
- WEBDL-480p - WEB-DL (P2P) syftar på en fil som har ripats förlustfritt från en strömningstjänst, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., eller laddats ner via en online-distributionswebbplats som iTunes. Kvaliteten är ganska bra eftersom de inte är omkodade. Videon (H.264 eller H.265) och ljudet (AC3/AAC) extraheras vanligtvis från iTunes eller Amazon Video och remuxas till en MKV-behållare utan att förlora kvalitet. En fördel med dessa utgåvor är att de vanligtvis inte har några nätverkslogotyper på skärmen. Dessa är nästan lika bra som en Blu-ray-källa men kan lida av ljudfördröjning eller visuella artefakter från strömningstjänsternas adaptiva bithastighet. Om en ripperns internetanslutning sjunker till en punkt där bithastigheten minskar kan källans bithastighet ändras dynamiskt, vilket kan leda till variationer i bildkvaliteten. De flesta utgåvor som lider av en extrem mängd visuella artefakter är NUKED och en PROPER släpps vanligtvis för att fixa eventuella stora variationer i adaptiv bithastighet. Detta kommer att vara i 480p (SD) kvalitet.
- WEBRip-480p - I en WEB-Rip (P2P) extraheras filen oftast med hjälp av HLS- eller RTMP/E-protokoll och remuxas från en TS-, MP4- eller FLV-behållare till MKV. Detta kommer att vara i 480p (SD) kvalitet.
- DVD - En omkodning av den slutliga utgivna DVD9. Om möjligt släpps detta PRE retail. Det bör vara utmärkt kvalitet (för upplösningen). DVDrips släpps vanligtvis i DivX/XviD eller MP4.
- Bluray-480p - En omkodning av den slutliga utgivna Blu-ray, nedskalad till 480p-upplösning (720x480 @ 16:9, någon annan bildförhållande kan vara en annan upplösning). Om möjligt släpps detta PRE retail. Det bör vara utmärkt kvalitet för upplösningen. Bitrates kan variera, men dessa är generellt kodade till DivX, XviD eller AVC och erbjuder en kompromiss med en liten upplevd kvalitetsminskning jämfört med den ursprungliga källan samtidigt som filstorleken minskas drastiskt. Dessa är vanligtvis MKV eller MP4, men vissa DivX/XviD finns också som använder AVI.
- HDTV-720p - En omkodning av den slutliga utgivna Blu-ray, men sänds över HD-kabel eller satellit (1280x720 @ 16:9, något annat bildförhållande kan vara en annan upplösning). Den kan modifieras för speltid eller innehåll beroende på vilket nätverk den kommer från. Detta släpps vanligtvis flera månader efter en detaljhandelsutgåva, men ibland släpps uppskalade versioner av en film med standardupplösning på kabelkanaler som STARZ eller HBO, och de skulle vara de enda HD-kopiorna av den specifika filmen som är tillgängliga. Dessa är vanligtvis MKV eller MP4.
- HDTV-1080p - En omkodning av den slutliga utgivna Blu-ray, men sänds över HD-kabel eller satellit (1920x1080 @ 16:9, något annat bildförhållande kan vara en annan upplösning). Den kan modifieras för speltid eller innehåll beroende på vilket nätverk den kommer från. Detta släpps vanligtvis flera månader efter en detaljhandelsutgåva, men ibland släpps uppskalade versioner av en film med standardupplösning på kabelkanaler som STARZ eller HBO, och de skulle vara de enda HD-kopiorna av den specifika filmen som är tillgängliga. Dessa är vanligtvis MKV eller MP4-behållare.
- WEBRip-720p - I en WEB-Rip (P2P) extraheras filen oftast med hjälp av HLS- eller RTMP/E-protokoll och remuxas från en TS-, MP4- eller FLV-behållare till MKV. Detta kommer att vara i 720p-kvalitet.
- Bluray-720p - En omkodning av den slutliga utgivna Blu-ray, nedskalad till 720p-upplösning (1280x720 @ 16:9, något annat bildförhållande kan vara en annan upplösning). Om möjligt släpps detta PRE retail. Det bör vara utmärkt kvalitet för upplösningen. Bitrates kan variera, men dessa är generellt kodade till AVC eller HEVC och erbjuder en kompromiss med en liten upplevd kvalitetsminskning jämfört med den ursprungliga källan samtidigt som filstorleken minskas drastiskt. Dessa är vanligtvis MKV eller MP4-behållare.
- WEBDL-1080p - WEB-DL (P2P) syftar på en fil som har ripats förlustfritt från en strömningstjänst, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., eller laddats ner via en online-distributionswebbplats som iTunes. Kvaliteten är ganska bra eftersom de inte är omkodade. Videon (H.264 eller H.265) och ljudet (AC3/AAC) extraheras vanligtvis från iTunes eller Amazon Video och remuxas till en MKV-behållare utan att förlora kvalitet. En fördel med dessa utgåvor är att de vanligtvis inte har några nätverkslogotyper på skärmen. Dessa är nästan lika bra som en Blu-ray-källa men kan lida av ljudfördröjning eller visuella artefakter från strömningstjänsternas adaptiva bithastighet. Om en ripperns internetanslutning sjunker till en punkt där bithastigheten minskar kan källans bithastighet ändras dynamiskt, vilket kan leda till variationer i bildkvaliteten. De flesta utgåvor som lider av en extrem mängd visuella artefakter är NUKED och en PROPER släpps vanligtvis för att fixa eventuella stora variationer i adaptiv bithastighet. Detta kommer att vara i 1080p-kvalitet.
- WEBRip-1080p - I en WEB-Rip (P2P) extraheras filen oftast med hjälp av HLS- eller RTMP/E-protokoll och remuxas från en TS-, MP4- eller FLV-behållare till MKV. Detta kommer att vara i 1080p-kvalitet.
- Bluray-1080p - En omkodning av den slutliga utgivna Blu-ray, i sin nativa 1080p-upplösning (1920x1080 @ 16:9, något annat bildförhållande kan vara en annan upplösning). Om möjligt släpps detta PRE retail. Det bör vara utmärkt kvalitet och samma upplösning som källan. Bitrates kan variera, men dessa är generellt kodade till AVC eller HEVC och erbjuder en kompromiss med en liten upplevd kvalitetsminskning jämfört med den ursprungliga källan samtidigt som filstorleken minskas något. Dessa är vanligtvis MKV eller MP4-behållare.
- Remux-1080p - En remux är en rip av en Blu-ray- eller HD DVD-skiva till en annan behållarformat eller bara borttagning av menyer och bonusmaterial samtidigt som ljud- och videoflödena behålls intakta (och behåller de nuvarande koderna), vilket garanterar exakt 1:1-filmkvalitet som på originalskivan. Detta är i 1080p-kvalitet.
- HDTV-2160p - TVRip är en fångstkälla från ett fångstkort. HDTV står för fångad källa från HD-TV. Med en HDTV-källa kan kvaliteten ibland till och med överträffa DVD. Filmer i detta format börjar bli populära. Viss reklam och kommersiella banderoller kan ses på vissa utgåvor under uppspelning. Detta är i 2160p (4K) kvalitet.
- WEBDL-2160p - WEB-DL (P2P) syftar på en fil som har ripats förlustfritt från en strömningstjänst, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., eller laddats ner via en online-distributionswebbplats som iTunes. Kvaliteten är ganska bra eftersom de inte är omkodade. Videon (H.264 eller H.265) och ljudet (AC3/AAC) extraheras vanligtvis från iTunes eller Amazon Video och remuxas till en MKV-behållare utan att förlora kvalitet. En fördel med dessa utgåvor är att de vanligtvis inte har några nätverkslogotyper på skärmen. Dessa är nästan lika bra som en Blu-ray-källa men kan lida av ljudfördröjning eller visuella artefakter från strömningstjänsternas adaptiva bithastighet. Om en ripperns internetanslutning sjunker till en punkt där bithastigheten minskar kan källans bithastighet ändras dynamiskt, vilket kan leda till variationer i bildkvaliteten. Detta kommer att vara i 2160p (4K) kvalitet.
- WEBRip-2160p - I en WEB-Rip (P2P) extraheras filen oftast med hjälp av HLS- eller RTMP/E-protokoll och remuxas från en TS-, MP4- eller FLV-behållare till MKV. Detta kommer att vara i 2160p (4K) kvalitet.
- Bluray-2160p - En omkodning av den slutliga utgivna Blu-ray, i sin nativa 2160p-upplösning (3840x2160 @ 16:9, något annat bildförhållande kan vara en annan upplösning). 4K-versioner av filmer som släpps är generellt sett i HEVC-codec och kan vara antingen 8-bitars eller 10-bitars färgåtergivning eller från en HDR-källa. Dessa är vanligtvis MKV eller MP4-behållare.
- Remux-2160p - En remux är en rip av en Blu-ray- eller HD DVD-skiva till en annan behållarformat eller bara borttagning av menyer och bonusmaterial samtidigt som ljud- och videoflödena behålls intakta (och behåller de nuvarande koderna), vilket garanterar exakt 1:1-filmkvalitet som på originalskivan. Detta är i 2160p (4K) kvalitet.

# Anpassade format

{#custom-formats-2}

- Se till att du får rätt utgåva varje gång! Anpassade format ger fin kontroll över prioritering och val av utgåvor. Så enkelt som ett enda föredraget ord eller så komplicerat som du vill med flera kriterier och regex.
- Anpassade format beräknas dynamiskt istället för att lagras i databasen, så de uppdateras så snart du ändrar definitionerna.
- Anpassade format används inom dina kvalitetsprofiler för att bestämma poängsättningen för varje anpassat format. Inom varje kvalitetsprofil kan du ange ett minimum för poäng för anpassat format för att en utgåva ska hämtas och även en uppgraderingsscore.
- Det rekommenderas starkt att du lägger till nedanstående anpassade format från [TRaSH's Guides](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) för att undvika oönskade nedladdningar. Se den länkade TRaSH Guide Custom Format-artikeln och ytterligare 3 refererade TRaSH Custom Format Guides högst upp på sidan för Custom Formats för mer information.
  - [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) kommer att undvika att hämta utgåvor med Dolby Vision (DV) som har en grön nyans om DV inte stöds.
  - [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) för att undvika att hämta dåligt namngivna BR-DISKs som inte matchar BR-DISK-kvalitetsanalysen.

---

- Namn - Namnet på det anpassade formatet
- Inkludera anpassat format vid namnändring - Inkludera namnet på det anpassade formatet vid namnändring?

> Anpassade format påverkar inte vad som söks - bara hur resultaten utvärderas. Det är heller inte möjligt att på något sätt ändra den sökning som Radarr använder.
{.is-info}

Profiler är där poängsättningen för anpassade format konfigureras.

## Villkor för anpassade format

### Modifierare

- Negativ - matchningen inverteras, så villkoret uppfylls endast om det icke-inverterade villkoret inte uppfylls
- Obligatorisk - gäller endast för format med fler än ett villkor av samma typ och ändrar matchningsreglerna för typgrupper. Om denna inställning är aktiverad måste detta specifika villkor uppfyllas för att hela det anpassade formatet ska gälla, oavsett om ett annat villkor av samma typ annars skulle uppfylla typgruppen. **Observera: Du använder bara detta om du använder ett villkor mer än en gång. Med andra ord, om du har ett anpassat format med 2 obligatoriska villkor för utgivningstitel och 3 icke-obligatoriska språkvillkor, måste det uppfylla BÅDA de obligatoriska villkoren för utgivningstitel och det måste uppfylla ETT AV de 3 språkvillkoren.** På samma sätt, om du har ett anpassat format med 4 utgivningstitelvillkor och inget av dem är obligatoriska, kommer det anpassade formatet att gälla om NÅGOT av villkoren uppfylls.

### Villkor

> **Olika villkorstyper** fungerar som `och` inom samma anpassade format. **Flera villkor av samma typ** fungerar som `eller` om inte Obligatorisk används
{.is-info}

- **Alla villkor som använder RegEx är skiftlägesokänsliga**
- Observera följande GitHub-ärenden
  - [Anpassade format gäller inte före filmåret i utgivningstitlar #4859](https://github.com/Radarr/Radarr/issues/4859)
  - [Anpassat format matchar inte för termen "xvid" i slutet av utgivningsnamnet #6824](https://github.com/Radarr/Radarr/issues/6824)
- Utgivningstitel - Detta är ett reguljärt uttryck som matchas mot utgivningstiteln och, efter nedladdning, filnamnet på disken.
  - Observera: Radarr betraktar endast text efter filmtiteln och året, vilket innebär att allt som föregår titeln ignoreras.
- Utgåva - Denna tagg matchas mot eventuella utgåvor som Radarr kan analysera. Du kan ange vilket värde som helst som Radarr kommer att försöka matcha mot det som analyserats (skiftlägesokänsligt).
- Språk - Detta språk matchas mot eventuella språk som Radarr analyserar. Alla språk som tidigare var valbara i profiler fungerar här.
- [Indexer Flag](/radarr/settings#indexer-flags) - Denna tagg matchas mot eventuella indexeringsflaggor som Radarr kan analysera.
- Källa - Källan där en utgåva har ripats från (t.ex. BLURAY).
- Upplösning - Upplösningen som analyserats från antingen utgivningsnamnet eller mediainfo (om tillgängligt).
- Kvalitetsmodifierare - Kvalitetsmodifierare ställer in saker som Telescene, Telesync, Remux, Regional. Det gör det möjligt att särskilja en given källa och upplösningspar när det finns flera kvalitets (käll)typer som kan användas.
- Storlek - Detta matchas mot utgivningsstorleken. Utgivningsstorleken konverteras till gigabyte och jämförs med min- och maxvärdena.
- Grupp - Detta matchas mot gruppen som Radarr analyserar baserat på Radarrs logik för gruppdetektering.

### Inställningar för profilering och rangordning

- Anpassade format implementeras inom och påverkas av kvalitetsprofiler. Uppgraderingsscoren förhindrar uppgradering när en utgåva med denna önskade score har hämtats.
- En score på 0 resulterar i att det anpassade formatet endast är informativt och inte påverkar rangordningen av utgåvor eller sökta språk.
- Minsta score kräver att utgåvornas samlade score för anpassat format når denna tröskel, annars kommer de att avvisas.
  - Anpassade format som matchar med oönskade attribut bör ges en negativ score för att sänka deras attraktionskraft.
  - Helt avvisade utgåvor bör ges en negativ score som är tillräckligt låg att även om alla andra format med positiva scores läggs till skulle scoren fortfarande hamna under minimum.
- [Se TRaSH's Guides för hur man konfigurerar och använder anpassade format](https://trash-guides.info/Radarr/Radarr-setup-custom-formats/)

#### Importera / Exportera anpassade format

- [Se TRaSH's Guides för hur man importerar/exporterar anpassade format.](https://trash-guides.info/Radarr/Radarr-import-custom-formats/) Det går dock att importera och exportera anpassade format.

#### Importera / Uppdatera befintliga anpassade format

- [Se TRaSH's Guides för hur man importerar eller uppdaterar befintliga anpassade format.](https://trash-guides.info/Radarr/Radarr-how-to-update-custom-formats/)

### Samling av anpassade format

- [TRaSH har en samling av anpassade format](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)

# Indexerare

> Information om stödda indexerare finns på sidan [Mer information (Stödda)](/radarr/supported#indexers) för den här sektionen
{.is-info}

## Stödda indexerare

- En lista över stödda indexerare finns på sidan [Mer information (Stödda)](/radarr/supported#indexers)

### Inställningar för indexerare

- När du har klickat på <kb>+</kb>-knappen för att lägga till en ny indexerare visas ett nytt fönster med många olika alternativ. För wiki-syften betraktar Radarr både Usenet-indexerare och Torrent-spårare som "indexerare".

- Här finns två avsnitt: Usenet och Torrents. Beroende på vilken nedladdningsklient du kommer att använda vill du välja vilken typ av indexerare du kommer att använda.

### Konfiguration av Usenet-indexerare

- Newznab - Här hittar du förinställda populära Usenet-indexerare (som är förifyllda, allt du behöver är din API-nyckel som tillhandahålls av Usenet-indexeraren du väljer) tillsammans med möjligheten att skapa en anpassad indexerare.
- Programvara som fungerar med Usenet och integrerar väl med Radarr är [NZBHydra2](https://github.com/theotherp/nzbhydra2/) eller [Prowlarr](/prowlarr) som integrerar med både Usenet och Torrents.
- Oavsett om du väljer en förifylld indexerare eller en anpassad indexerare kommer du att presenteras med ett nytt fönster för att ange alla dina inställningar.
- Välj bland förinställningarna eller lägg till en anpassad indexerare (som NZBHydra2 eller Prowlarr).
- Namn - Namnet på indexeraren i Radarr.
- Aktivera RSS - Om aktiverat, använd denna indexerare för att övervaka filer som saknas eller ännu inte har nått sin cutoff.
- Aktivera automatisk sökning - Om aktiverat, använd denna indexerare för automatiska sökningar, inklusive sökning vid tillägg.
- Aktivera interaktiv sökning - Om aktiverat, använd denna indexerare för manuella interaktiva sökningar.
- URL - URL:en som indexeraren tillhandahåller, t.ex. `https://api.nzbgeek.info`.
- API-sökväg - Sökvägen till API:et som indexeraren tillhandahåller. Detta är vanligtvis `/api`.
- Flera språk - Ange vilka språk `MULTI` som gäller för denna indexerare.
- API-nyckel - Nyckeln som indexeraren tillhandahåller för att få åtkomst till API:et.
- Kategorier - Standardkategorier kommer att användas om de inte redigeras. Det är troligt att dessa standardkategorier inte är optimala. När du redigerar denna inställning frågar Radarr indexeraren efter sina tillgängliga kategorier och visar dem i en valbar lista. De gamla standarderna rensas så snart en kategori växlas.
- (Avancerad inställning) Ytterligare parametrar - Ytterligare Newznab-parametrar att lägga till i frågelänken.
- Ta bort år från söksträngen - Ska Radarr ta bort året efter filmtiteln vid sökning på denna indexerare?
- (Avancerad inställning) Indexeringsprioritet - Prioritet för denna indexerare för att föredra en indexerare framför en annan vid likvärdiga utgivningsscenarier. 1 är högsta prioritet och 50 är lägsta prioritet.
- (Avancerad inställning) Nedladdningsklient - Välj och ange vilken nedladdningsklient som används för hämtningar från denna indexerare.
- Taggar - Använd endast denna indexerare för filmer med minst en matchande tagg. Lämna tomt för att använda med alla filmer.

### Konfiguration av torrentspårare

- Precis som med Usenet finns det en mängd förifyllda uppgifter om torrentspårare. Om du inte är medlem i någon av dessa specifika spårare kommer de inte att vara till någon nytta för dig.
- Ett av de bästa och enklaste sätten att använda Torrentspårare som inte stöds nativt av Radarr är att använda ett andra program som [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett). Dessa program fungerar bra tillsammans med Radarr som en sökindexerare som samlar all din information och skickar den till Radarr.
- Torznab - Denna inställning kommer att ge dig en förinställd konfiguration för Jackett. Om du använder flera spårare måste varje post ha ett unikt namn.
- Torznab-indexerare
- Välj bland förinställningarna eller lägg till en anpassad indexerare (som Jackett).
- Namn - Namnet på indexeraren i Radarr.
- Aktivera RSS - Om aktiverat, använd denna indexerare för att övervaka filer som saknas eller ännu inte har nått sin cutoff.
- Aktivera automatisk sökning - Om aktiverat, använd denna indexerare för automatiska sökningar, inklusive sökning vid tillägg.
- Aktivera interaktiv sökning - Om aktiverat, använd denna indexerare för manuella interaktiva sökningar.
- URL - URL:en som indexeraren tillhandahåller, t.ex. `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-sökväg - Sökvägen till API:et som indexeraren tillhandahåller. Detta är vanligtvis `/api`.
- API-nyckel - Nyckeln som indexeraren tillhandahåller för att få åtkomst till API:et.
- Flera språk - Ange vilka språk `MULTI` som gäller för denna indexerare.
- Kategorier - Standardkategorier kommer att användas om de inte redigeras. Det är troligt att dessa standardkategorier inte är optimala. När du redigerar denna inställning frågar Radarr indexeraren efter sina tillgängliga kategorier och visar dem i en valbar lista. De gamla standarderna rensas så snart en kategori växlas.
- (Avancerad inställning) Ytterligare parametrar - Ytterligare Torznab-parametrar att lägga till i frågelänken.
- Ta bort år från söksträngen - Ska Radarr ta bort året efter filmtiteln vid sökning på denna indexerare?
- Minsta antal seeders - Det minsta antalet seeders som krävs för att en utgåva från denna spårare ska hämtas.
- Seedningsförhållande - Om det är tomt används standardinställningen för nedladdningsklienten. Annars är det minsta seedningsförhållandet som krävs för att din nedladdningsklient ska uppfylla för utgåvor från denna indexerare innan de pausas av din klient och tas bort av Radarr (Kräver hantering av slutförd nedladdning - Ta bort aktiverat).
- Seedningstid - Om det är tomt används standardinställningen för nedladdningsklienten. Annars är det minsta seedningstiden i minuter som krävs för att din nedladdningsklient ska uppfylla för utgåvor från denna indexerare innan de pausas av din klient och tas bort av Radarr (Kräver hantering av slutförd nedladdning - Ta bort aktiverat).
- Obligatoriska flaggor - Vilka indexeringsflaggor krävs?

#### Indexeringsflaggor

| Flagga           | Symbol | Beskrivning                                                                                                                                                                                                                 |
| ---------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `G_Freeleech`    | ⬇⬇     | Ibland ställer torrentsajter in en torrent som freeleech. Det betyder att nedladdningen av denna torrent inte räknas mot din nedladdningskvot eller seedningsförhållande. Detta är mycket användbart om du ännu inte har byggt upp ett bra seedningsförhållande. |
| `G_Halfleech`    | ⇩⇩     | Liknande `G_Freeleech`, `G_Halfleech` innebär att endast hälften av storleken på denna torrent räknas mot din nedladdningskvot eller seedningsförhållande.                                                                               |
| `G_DoubleUpload` | ⬆      | Liknande `G_Freeleech`, `G_DoubleUpload` innebär att all data du laddar upp via seedning räknas dubbelt mot din uppladdningskvot och seedningsförhållande. Detta är mycket användbart om du vill bygga upp en buffert för seedningsförhållande.      |
| `PTP_Golden`     | 🌟      | På PassThePopcorn får vissa torrents taggen *Golden* när de uppfyller vissa kodningsstandarder. Dessa är vanligtvis de bästa kodningarna, med nästan ingen märkbar kvalitetsförlust. Du kan läsa mer på deras wikisida. |
| `PTP_Approved`   | ✔      | På PassThePopcorn godkänns vissa torrents när de uppfyller minimistandarderna för kodning (t.ex. inga låga bitrater). Se deras wiki för mer information.                                                              |
| `HDB_Internal`   | 🚪      | Utgåvor på HDBits får denna tagg när utgåvan laddades upp av en av HDBits egna releasegrupper.                                                                                                                               |
| `G_Scene`        | ☠      | Liknande `G_Freeleech`, `G_Freeleech75` innebär att endast 25% av storleken på denna torrent räknas mot din nedladdningskvot eller seedningsförhållande.                                                                              |
| `G_Freeleech75`  | ⇩⬇     | Liknande `G_Freeleech`, `G_Freeleech75` innebär att endast 25% av storleken på denna torrent räknas mot din nedladdningskvot eller seedningsförhållande.                                                                              |
| `G_Freeleech25`  | ⇩      | Liknande `G_Freeleech`, `G_Freeleech25` innebär att endast 75% av storleken på denna torrent räknas mot din nedladdningskvot eller seedningsförhållande.                                                                              |

- (Avancerad inställning) Indexeringsprioritet - Prioritet för denna indexerare för att föredra en indexerare framför en annan vid likvärdiga utgivningsscenarier. 1 är högsta prioritet och 50 är lägsta prioritet.
- (Avancerad inställning) Nedladdningsklient - Välj och ange vilken nedladdningsklient som används för hämtningar från denna indexerare.
- Taggar - Använd endast denna indexerare för filmer med minst en matchande tagg. Lämna tomt för att använda med alla filmer.

## Alternativ

- Minsta ålder - Endast Usenet: Minsta ålder i minuter för NZB-filer innan de hämtas. Använd detta för att ge nya utgåvor tid att sprida sig till din Usenet-leverantör.
- Retention - Endast Usenet: Ange noll för obegränsad retention.
- Maximal storlek - Maximal storlek för en utgåva som ska hämtas i MB. Ange noll för obegränsad storlek. Observera att detta gäller globalt.
- Föredra indexeringsflaggor - Prioritera utgåvor med speciella flaggor. (Se Obligatoriska flaggor ovan)
- Tillgänglighetsfördröjning - Tid innan (-#) eller efter (#) tillgänglighetsdatumet att söka efter filmen
  - Detta är användbart för att fördröja sökningen efter en utgåva för att ge gemenskapen tid att utföra de bästa kodningarna.
  - Vanligtvis rekommenderas en tillgänglighet för film med `Släppt` och en fördröjning på `-21` eller `-14`.
- RSS-synkroniseringsintervall - Intervall i minuter. Ange noll för att inaktivera (detta stoppar all automatisk hämtning av utgåvor) Minimum: 10 minuter Maximum: 120 minuter
  - Se [Hur hittar Radarr filmer?](/radarr/faq#how-does-radarr-find-movies) för en bättre förståelse av hur RSS-synkronisering hjälper dig

> Om Radarr har varit offline under en längre tid kommer Radarr att försöka bläddra tillbaka för att hitta den senaste utgåvan som bearbetades för att undvika att missa en utgåva. Så länge din indexerare stöder bläddring och det inte har gått för lång tid kommer Radarr att kunna bearbeta de utgåvor som den skulle ha missat och undvika att du behöver söka efter de missade utgåvorna.{.is-info}

- Vitlistade undertextstaggar - Taggar som anges här kommer inte att betraktas som inbrända undertexter.
- Tillåt inbrända undertexter - Om aktiverat tillåts utgåvor med inbrända undertexter att laddas ner automatiskt

# Nedladdningsklienter

> Information om stödda nedladdningsklienter finns på sidan [Mer information (Stödda)](/radarr/supported#download-clients) för den här sektionen
{.is-info}

## Översikt

- Nedladdning och import är där de flesta människor upplever problem. Ur ett övergripande perspektiv måste programvaran kunna kommunicera med din nedladdningsklient och ha åtkomst till de filer den laddar ner. Det finns ett stort antal stödda nedladdningsklienter och ännu fler olika konfigurationer. Detta innebär att medan det finns några vanliga konfigurationer finns det ingen rätt konfiguration och varje persons konfiguration kan vara lite annorlunda. Men det finns många felaktiga konfigurationer.

## Process för nedladdningsklienter

### Usenet-process

- Radarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten. Exempel: filmer, tv, serier, musik, etc.
- Radarr övervakar dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- När nedladdningen är klar kommer Radarr att känna till den slutliga filplatsen enligt rapporterad av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp och åtkomlig av Radarr.
- Radarr skannar den avslutade filplatsen efter filer som Radarr kan använda. Den analyserar filnamnet för att matcha det mot den begärda medias. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den angivna medieplatsen.
- Atomiska flyttar (direkta flyttar) är aktiverade som standard. Filsystemet och monteringen måste vara densamma för din avslutade nedladdningsmapp och din mediebibliotek. Om den atomiska flytten misslyckas eller din konfiguration inte stöder hårdlänkar och atomiska flyttar kommer Radarr att falla tillbaka och kopiera filen och sedan ta bort den från källan, vilket är intensivt för I/O.

### Torrent-process

- Radarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten. Exempel: filmer, tv, serier, musik, etc.
- Radarr övervakar dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- Färdiga filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (kvot eller tid kan justeras i nedladdningsklienten eller från Radarr under den specifika nedladdningsklienten). När filer importeras till din mediamapp kommer Radarr att skapa en hårdlänk till filen om det stöds av din konfiguration eller kopiera om hårdlänkar inte stöds.
- Hårdlänkar är aktiverade som standard. [En hårdlänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringen måste vara densamma för din avslutade nedladdningsmapp och din mediebibliotek. Om skapandet av hårdlänken misslyckas eller din konfiguration inte stöder hårdlänkar kommer Radarr att falla tillbaka och kopiera filen.
- Om alternativet "Hantering av slutförd nedladdning - Ta bort" är aktiverat i Radarrs inställningar kommer Radarr att ta bort den ursprungliga filen och torrenten från din klient, men endast om klienten rapporterar att seedningen är klar och torrenten är stoppad (dvs pausad).

## Nedladdningsklienter

Klicka på `Inställningar => Nedladdningsklienter` och klicka sedan på <kb>+</kb> för att lägga till en ny nedladdningsklient. Din nedladdningsklient bör redan vara konfigurerad och igång.

### Stödda nedladdningsklienter

- En lista över stödda nedladdningsklienter finns på sidan [Mer information (Stödda)](/radarr/supported#download-clients)

Välj nedladdningsklienten du vill lägga till, och det kommer att visas en popupruta för att ange anslutningsinformation. Denna information är liknande för de flesta klienter. Vissa kommer att be om ett användarnamn eller lösenord, vissa kommer att fråga om du vill lägga till nya nedladdningar i ett pausat/startat tillstånd, osv.

### Inställningar för Usenet-klient

- Namn - Namnet på nedladdningsklienten inom Radarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en till din nedladdningsklient
- Port - Porten för din nedladdningsklient
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- (Avancerad inställning) URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxys.
- API-nyckel - API-nyckeln för att autentisera mot din klient
- Användarnamn - Användarnamnet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Lösenord - Lösenordet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Kategori - Kategorin inom din nedladdningsklient som \*Arr kommer att använda. För att undvika orelaterade nedladdningar som visas i Aktivitet rekommenderas det starkt att ange en kategori.
- Prioritet för nyligen släppta - Nedladdningsklientens prioritet för nyligen släppt media
- Prioritet för äldre släppta - Nedladdningsklientens prioritet för media som inte släpptes nyligen
- (Avancerad inställning) Klientprioritet - Prioritet för nedladdningsklienten. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet. 1 är högsta prioritet och 50 är lägsta prioritet
- Hantering av slutförd nedladdning
  - Ta bort (Per klientinställning) - Ta bort slutförda nedladdningar när de är klara (usenet) eller stoppade/slutförda (torrenter). Se [Hantering av slutförd nedladdning för mer information](#completed-download-handling)

### Inställningar för torrentklient



- Namn - Namnet på nedladdningsklienten inom Radarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en för din nedladdningsklient
- Port - Porten för din nedladdningsklient; detta är vanligtvis webgui-porten
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- (Avancerad inställning) URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxys.
- Användarnamn - användarnamnet för att autentisera mot din klient
- Lösenord - lösenordet för att autentisera mot din klient
- Kategori - kategorin inom din nedladdningsklient som \*Arr kommer att använda. För att undvika orelaterade nedladdningar som visas i Aktivitet rekommenderas det starkt att du anger en kategori.
- Kategori efter import - kategorin att ställa in efter att releasen har laddats ner och importerats. Observera att detta bryter hanteringen av avslutad nedladdning.
- Prioritet för nyligen släppt - nedladdningsklientens prioritet för nyligen släppt media
- Prioritet för äldre - nedladdningsklientens prioritet för media som inte släpptes nyligen
- Initialt tillstånd - Initialt tillstånd för torrents (endast Qbittorrent: Tvingar förbi alla seed-trösklar)
- (Avancerad inställning) Klientprioritet - Prioritet för nedladdningsklienten. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet. 1 är högsta prioritet och 50 är lägsta prioritet
- Hantering av avslutad nedladdning
  - Ta bort (Per klientinställning) - Ta bort avslutade nedladdningar när de är klara (usenet) eller stoppade/kompletta (torrents). Se [Hantering av avslutad nedladdning för mer information](#hantering-av-avslutad-nedladdning)
    - För torrents kräver detta att din nedladdningsklient pausar när seed-målen nås. Det kräver också att seed-målen stöds av Radarr enligt tabellen nedan. Torrents måste också vara i samma kategori.

### Kompatibilitet för borttagning av nedladdning för torrentklient

- Radarr kan bara ställa in seed-förhållandet/tiden på klienter som stöder att ställa in detta värde via deras API när torrenten läggs till. Seed-mål kan ställas in globalt i klienten själv eller per spårare i \*Arr-inställningar för varje indexerare. Se tabellen nedan för klientkompatibilitet.

|      Klient       |                                Förhållande                                |                                    Tid                                    |
| :---------------: | :---------------------------------------------------------------------: | :-----------------------------------------------------------------------: |
|       Aria2       |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |    ![Stöds inte](https://img.shields.io/badge/Stöds inte-Nej-critical)    |
|      Deluge       |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |    ![Stöds inte](https://img.shields.io/badge/Stöds inte-Nej-critical)    |
| Download Station  | ![Stöds inte](https://img.shields.io/badge/Stöds inte-Nej-critical) |    ![Stöds inte](https://img.shields.io/badge/Stöds inte-Nej-critical)    |
|       Flood       |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |      ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)      |
|     Hadouken      | ![Stöds inte](https://img.shields.io/badge/Stöds inte-Nej-critical) |    ![Stöds inte](https://img.shields.io/badge/Stöds inte-Nej-critical)    |
|    qBittorrent    |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |      ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)      |
|     rTorrent      |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |      ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)      |
| Torrent Blackhole | ![Stöds inte](https://img.shields.io/badge/Stöds inte-Nej-critical) |    ![Stöds inte](https://img.shields.io/badge/Stöds inte-Nej-critical)    |
|   Transmission    |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   | ![Idle-gräns](https://img.shields.io/badge/Stöds-Idle%20gräns*-blue)\* |
|     uTorrent      |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |      ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)      |
|       Vuze        |   ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)   |      ![Stöds](https://img.shields.io/badge/Stöds-Ja-success)      |

> ![Idle-gräns](https://img.shields.io/badge/Stöds-Idle%20gräns*-blue) - Transmission har internt en kontroll för inaktiv tid, men Radarr jämför den med seedningstiden om inaktivitetsgränsen är inställd för varje torrent. Detta görs som en lösning på Transmission's API-begränsningar.{.is-info}

## Hantering av avslutad nedladdning

- Hantering av avslutad nedladdning är hur Radarr importerar media från din nedladdningsklient till dina serie-mappar. Många vanliga problem är relaterade till felaktiga Docker-sökvägar och/eller andra Docker-behörighetsproblem.

- (Avancerad global inställning) Aktivera - Importera automatiskt avslutade nedladdningar från nedladdningsklienten
- (Avancerad inställning) Kontrollera intervall för färdiga nedladdningar - Ange hur ofta du vill fråga nedladdningsklienternas köer och uppdatera övervakade nedladdningar, minst 1 minut
- (Per klientinställning) Ta bort - Ta bort avslutade nedladdningar när de är klara (usenet) eller stoppade/kompletta (torrents)
  - För torrents kräver detta att din nedladdningsklient pausar när seed-målen nås. Det kräver också att seed-målen stöds av Radarr enligt tabellen ovan. Torrents måste också vara i samma kategori.

### Ta bort avslutade nedladdningar

- Radarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
- Radarr övervakar dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- När nedladdningen är klar vet Radarr den slutliga filplatsen enligt rapporterad av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp.
- Radarr skannar den avslutade filplatsen efter videofiler. Den analyserar videofilens namn för att matcha den med en film. Om den kan göra det, kommer den att döpa om filen enligt dina specifikationer och flytta den till den tilldelade biblioteksmappen.
- Överblivna filer från nedladdningen skickas till papperskorgen eller återvinningen.

Om du laddar ner med en BitTorrent-klient är processen något annorlunda:

- Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda. När filer importeras till din tilldelade biblioteksmapp kommer Radarr att försöka skapa en hårdlänk till filen eller falla tillbaka till att kopiera (använda dubbel plats) om hårdlänkar inte stöds.
- Om alternativet "Hantering av avslutad nedladdning - Ta bort" är aktiverat i inställningarna kommer Radarr att be torrentklienten att ta bort den ursprungliga filen och torrenten, men detta kommer bara att ske om klienten rapporterar att seedningen är klar, torrenten är i samma kategori (dvs. inte använder en kategori efter import), seedmålet som nåtts stöds av Radarr och torrenten är pausad (stoppad).

## Hantering av misslyckade nedladdningar

- Hantering av misslyckade nedladdningar är endast kompatibel med SABnzbd och NZBGet.
- Hantering av misslyckade nedladdningar gäller inte för torrents och det finns inga planer på att lägga till en sådan funktion.

- Det finns flera komponenter som ingår i processen för hantering av misslyckade nedladdningar:

- Kontrollera nedladdare:
  - Kö - Kontrollera din nedladdares kö för lösenordsskyddade (krypterade) releaser som markerats som misslyckade
  - Historik - Kontrollera din nedladdares historik för misslyckande (t.ex. inte tillräckligt med reparationer eller extrahering misslyckades)
- När Radarr hittar en misslyckad nedladdning börjar den bearbeta dem och gör några saker:
  - Lägger till en misslyckad händelse i Radarrs historik
  - Tar bort den misslyckade nedladdningen från nedladdningsklienten för att frigöra utrymme och rensa nedladdade filer (valfritt)
  - Börjar söka efter en ersättningsfil (valfritt)
  - Blockering (tidigare "Svartlistning") gör att nzbs automatiskt hoppas över när de misslyckas, detta innebär att nzb aldrig kommer att laddas ner automatiskt av Radarr igen (du kan fortfarande tvinga nedladdningen via en manuell sökning).
  - Det finns 2 avancerade alternativ (på sidan "Nedladdningsklient" inställningar) som styr beteendet för misslyckade nedladdningar i Radarr, för närvarande är de alla aktiverade som standard.

- Ladda ner igen - Styr om Radarr ska söka efter samma fil efter ett misslyckande
- (Avancerad inställning) Ta bort - Om nedladdningen automatiskt ska tas bort från nedladdningsklienten när misslyckandet upptäcks

## Fjärrsökvägsmappningar

- Fjärrsökvägsmappning fungerar som en enkel sökning efter fjärrsökväg och ersättning med lokal sökväg. Detta används främst för antingen sammanslagna lokala/fjärruppsättningar med hjälp av mergerfs eller liknande, eller används när programmet och nedladdningsklienten inte är på samma server.
- En fjärrsökvägsmappning används när din nedladdningsklient rapporterar en sökväg för slutförda data antingen på en annan server eller på ett sätt som \*Arr inte hanterar den mappen.
- Generellt sett krävs en fjärrsökvägsmappning endast om din nedladdningsklient körs på Linux när \*Arr körs på Windows eller vice versa. En fjärrsökvägsmappning kan också behövas om du blandar Docker- och Native-klienter eller om du använder en fjärrserver.
- En fjärrsökvägsmappning är en ENKEL sökning/ersättning (där den hittar VÄRDET FÖR FJÄRRSÖKVÄGEN, ersätt det med VÄRDET FÖR LOKAL SÖKVÄG för den angivna värden).
- Om felmeddelandet om en felaktig sökväg inte innehåller VÄRDET SOM ERSATTS, fungerar inte sökvägsmappningen som du förväntar dig. Den vanliga lösningen är att lägga till och ta bort mappningen.
- [Se TRaSH's handledning för ytterligare information om fjärrsökvägsmappning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Om både \*Arr och din nedladdningsklient är Docker-containrar behövs sällan en fjärrsökvägsmappning. Det rekommenderas att du [granskar Docker-guiden](/docker-guide) och/eller [följer TRaSH's handledning](https://trash-guides.info/hardlinks)
{.is-info}

# Importlistor

> Information om stödda listtyper finns på sidan [Mer information (Stödda)](/radarr/supported#lists) för denna sektion
{.is-info}

## Listor

Importlistor är en del av Radarr som gör att du kan följa en given listskapare. Säg att du följer en viss listskapare på Trakt/TMDb och verkligen gillar deras ArrowVerse Collection-sektion och vill titta på varje show på deras lista. Du tittar i din Radarr och inser att du inte har dessa serier. Istället för att söka en efter en och lägga till dessa objekt och sedan söka igenom dina indexerare efter dessa serier kan du göra allt detta på en gång med en lista. Listorna kan ställas in för att importera alla serier på den kurators lista samt att automatiskt tilldela en kvalitetsprofil, automatiskt lägga till och automatiskt övervaka den serien.

- VARNING: Om listor utförs på fel sätt kommer de absolut att förstöra ditt bibliotek med en massa skräp som du inte har någon avsikt att titta på. Så se till att du vet vad du importerar innan du klickar på spara. Dvs. titta fysiskt på listan innan du ens går till Radarr.

- Här kan du välja <kb>+</kb>-knappen för att öppna ett nytt popup-fönster
- I detta nya fönster presenteras du med många olika alternativ för att konfigurera din lista från många olika listleverantörer. Som tidigare nämnts, var försiktig när du gör listor. Det rekommenderas starkt att du inte väljer knappen Sök vid tillägg innan du är helt säker på att listan du väljer/inställer lägger till de serier du letar efter.
- När du har valt listleverantören som du vill hämta från (t.ex. IMDb eller Trakt) kommer du att presenteras med ett nytt fönster.
De flesta listinställningar är ganska självförklarande, vissa listor kräver att du autentiserar med leverantören som Trakt (vilket kräver att du har ett konto med Trakt.tv)

## Listalternativ

- (Avancerad inställning) Uppdateringsintervall för lista - Hur ofta ska Radarr fråga listan efter uppdateringar? [Detta är minst 6 timmar.](/radarr/faq#why-are-lists-sync-times-so-long-and-can-i-change-it)
- (Avancerad inställning) Nivå för rensning av bibliotek - Filmer i biblioteket kommer att tas bort eller sluta övervakas om de inte finns i dina listor
  - Inaktiverad - Rensa inte biblioteket (Rekommenderas)
  - Endast logga - Logga bara filmerna som inte finns i listorna och vidta inga andra åtgärder
  - Behåll och sluta övervaka film - Behåll filmer som inte finns i listorna, men sluta övervaka dem i Radarr.
  - Ta bort film och behåll filer - Ta bort filmer som inte finns i listorna från Radarr, men radera inte deras filer
  - Ta bort film och radera filer - Ta bort filmer som inte finns i listorna från Radarr och radera deras filer

## Listexkluderingar

- Importera listexkludering - Detta gör att du kan rensa din lista över filmer du inte vill se igen. Ett exempel på detta är om din lista råkar innehålla en film som är på ett främmande språk och det är osannolikt att du någonsin kommer att hitta den här filmen på ditt modersmål och inte vill titta på den med undertexter. Du kan utesluta en film från att läggas till i framtiden. Men i avsnittet för listexkludering kan du lägga till den i listan igen så att när listan körs igen kommer den att läsas in i ditt bibliotek.

# Anslutning

> Information om stödda anslutningstyper finns på sidan [Mer information (Stödda)](/radarr/supported#notifications) för denna sektion
{.is-info}

## Anslutningar

Anslutningar är hur du vill att Radarr ska kommunicera med omvärlden.

- Genom att trycka på <kb>+</kb>-knappen kommer du att presenteras med ett nytt fönster som låter dig konfigurera många olika slutpunkter

- En lista över stödda meddelanden och anslutningar finns på sidan [Mer information (Stödda)](/radarr/supported#notifications)

## Anslutningstriggers

- Vid hämtning - Få meddelande när filmer är tillgängliga för nedladdning och har skickats till en nedladdningsklient
- Vid import - Få meddelande när filmer har importerats framgångsrikt
- Vid uppgradering - Få meddelande när filmer uppgraderas till bättre kvalitet
- Vid namnbyte - Få meddelande när filmer byter namn
- Vid tillägg av film - Få meddelande när filmer läggs till i Radarrs bibliotek för att hantera eller övervaka
- Vid borttagning av film - Få meddelande när filmer tas bort
- Vid borttagning av filmfil - Få meddelande när filmfiler tas bort
- Vid borttagning av filmfil för uppgradering - Få meddelande när filmfiler tas bort för uppgraderingar
- Vid hälsoproblem - Få meddelande om hälsokontrollfel
  - Inkludera hälsovarningar - Få meddelande om hälsovarningar i tillägg till fel.
- Vid programuppdatering - Få meddelande när Radarr uppdateras till en ny version

# Metadata

## Alternativ

- Certifieringsland - Välj landet att använda för filmcertifieringar (t.ex. R (US) eller 12A (UK))

## Metadatakonsumenter

> Information om stödda metadatakonsumenter finns på sidan [Mer information (Stödda)](/radarr/supported#metadata) för denna sektion
{.is-info}

Här kan du välja vilken typ av metadata som din mediaspelare ska använda

Kodi kommer att vara ett av de vanligast använda alternativen här om det är den programvaran som används. Detta gör att Radarr kan skapa en NFO-fil samt associerade filaffischer som ska skrapas in i din spelare

# Taggar

- Taggsektionen i Radarr används för att länka olika aspekter av Radarr. De är också användbara för att spåra vilka filmer som kommer från vilka listor.
- Taggar är särskilt användbara för:

  - Fördröjningsprofiler
  - Restriktioner
  - Indexerare

- Taggar kan användas för att länka Fördröjningsprofiler, Indexerare och Restriktioner och Filmer tillsammans.
- Till exempel:
  - Du vill bara att en specifik indexerare ska användas för en specifik film. Du skulle skapa en tagg och tilldela filmen och indexeraren den taggen.
  - Du vill att en specifik Restriktion endast ska gälla för en specifik film. Du skulle skapa en tagg och tilldela Restriktionen och filmen den taggen.
  - Denna process är densamma för Fördröjningsprofiler.

> En film kommer att använda både indexerare som har matchande taggar och indexerare som inte har några taggar.
{.is-warning}

> Observera: Taggar påverkar inte några "Anpassade format", "Kvalitetsprofiler" eller någon annan aspekt som inte nämns ovan.
{.is-info}

# Allmänt

## Värd

- Bind Address - Giltig IPv4-adress eller '*' för alla gränssnitt
  - 0.0.0.0 eller `*` - alla adresser kan ansluta
  - 127.0.0.1 eller localhost - endast lokala program kan ansluta
  - Annan IP (t.ex. 1.2.3.4) - endast den IP-adressen (1.2.3.4) kan ansluta
- Portnummer - Portnumret som du vill använda för att komma åt webbgränssnittet för Radarr

> Observera: Om du använder Docker ska du inte ändra den här inställningen.
{.is-warning}

- URL-bas - För stöd för omvänd proxy, standard är tomt

> Observera: Om du använder en omvänd proxy (exempel: mydomain.com/radarr) ska du ange '/radarr' för URL-bas.
{.is-info}

- Aktivera SSL - Om du har SSL-legitimationer och vill säkra kommunikationen till och från din Radarr, aktivera detta alternativ.

> Observera: Använd inte detta om du inte vet vad du gör.
{.is-warning}

## Säkerhet

- Autentisering - Hur vill du autentisera för att komma åt din Radarr-instans
  - Från och med Radarr v5 är autentisering nu obligatorisk. [Se den obligatoriska autentiserings-FAQ-posten för detaljer.](/radarr/faq#forced-authentication)
  - ~~Ingen - Du har ingen autentisering för att komma åt din Radarr. Vanligtvis om du är den enda användaren i ditt nätverk, inte har någon på ditt nätverk som skulle vilja komma åt din Radarr eller om din Radarr inte är exponerad för webben~~
  - Grundläggande (webbläsarpopup) - Detta alternativ visar en liten popup när du går in på din Radarr där du kan ange användarnamn och lösenord
  - Formulär (inloggningssida) - Detta alternativ har en bekant inloggningsskärm liknande andra webbplatser för att låta dig logga in på din Radarr
- API-nyckel - Så här kommunicerar andra program eller har Radarr kommunicera med andra program. Om denna nyckel ges till fel person med åtkomst kan den göra alla möjliga saker med din bibliotek. Detta är varför API-nyckeln är maskerad i loggarna
- Certifikatvalidering - Ändra hur strikt HTTPS-certifikatvalidering är
  - Aktiverad - Validera alla HTTPS-certifikat (rekommenderas)
  - Inaktiverad för lokala adresser - Validera alla HTTPS-certifikat utom de på localhost och LAN
  - Inaktiverad - Validera inga HTTPS-certifikat
  
## Proxy

Proxy - Detta alternativ låter dig köra informationen som Radarr hämtar och söker igenom en proxy. Detta kan vara användbart om du befinner dig i ett land som inte tillåter nedladdning av torrentfiler

- Använd Proxy - Aktivera för att använda en proxy
- Proxytyp - Välj din proxytyp (HTTPS, Socks4 eller Socks5)
- Värdnamn - Ange ditt proxy-värdnamn (Inkludera inte http/https eller någon annan protokoll)
- Port - Ange din proxyport
- Användarnamn - Ange ditt proxy-användarnamn om tillämpligt
- Lösenord - Ange ditt proxy-lösenord om tillämpligt
- Ignorerade adresser - Ange en kommaseparerad lista över adresser som undviker proxyt
- Bypassa proxy för lokala adresser - Markera rutan för att bypassa proxyt för lokala adresser. Lokala förfrågningar identifieras genom att de saknar en punkt (.) i URI:en, som i <http://webserver/>, eller genom att komma åt den lokala servern, inklusive <http://localhost>, <http://loopback> eller <http://127.0.0.1>. När detta inte är markerat görs alla internetförfrågningar via proxyservern.

## Loggning

- Loggnivå - Förmodligen ett av de mest användbara felsökningsverktygen
  - Info - Detta är det mest grundläggande sättet som Radarr samlar information på, detta inkluderar mycket minimal mängd information i loggarna. Denna loggfil innehåller fatala, fel, varningar och info-poster.
  - Debug - Debug kommer att inkludera all information som Info inkluderar plus mer information som kan vara användbar. Denna loggfil innehåller fatala, fel, varningar, info och debug-poster.
  - Spårning - Den mest avancerade och detaljerade loggningen på Radarr, Spårning kommer att inkludera all information som samlas in av Info och Debug och mer. Detta är den vanligaste typen av logg som kommer att begäras vid felsökning på Discord eller Reddit. Om du behöver hjälp, välj din logg till Spårning och gör om uppgiften som gav dig problem för att fånga loggen. Denna loggfil innehåller fatala, fel, varningar, info, debug och spårningsposter.

## Analys

- Analys - Skicka anonym användnings- och felinformation till Radarrs servrar (Servarr). Detta inkluderar information om din webbläsare, vilka Radarr WebUI-sidor du använder, felrapportering samt OS- och runtime-version. Vi kommer att använda denna information för att prioritera funktioner och felkorrigeringar.

## Uppdateringar

- (Avancerad inställning) Gren - Detta är grenen av Radarr som du kör på.
  - [Se denna FAQ-post för mer information](/radarr/faq#how-do-i-update-radarr)
- Automatisk - Ladda ner och installera uppdateringar automatiskt. Du kommer fortfarande att kunna installera från System: Uppdateringar. Observera: Windows-användare uppdateras alltid automatiskt.
- Mekanism - Använd Radarrs inbyggda uppdaterare eller ett skript
  - Inbyggd - Använd Radarrs egen uppdaterare
  - Skript - Låt Radarr köra uppdateringsskriptet
  - Docker - Uppdatera inte Radarr från insidan av Docker, dra istället en helt ny bild med den nya uppdateringen
- Skript - Synlig endast när Mekanism är inställd på Skript - Sökväg till uppdateringsskriptet
- Uppdateringsprocess - Radarr kommer att ladda ner uppdateringsfilen, verifiera dess integritet och extrahera den till en temporär plats och anropa den valda metoden. Uppdateringsprocessen körs under samma användare som Radarr körs under, den behöver behörighet att uppdatera Radarr-filerna samt stoppa/starta Radarr.
- Inbyggd - Den inbyggda metoden kommer att säkerhetskopiera Radarr-filer och inställningar, stoppa Radarr, uppdatera installationen och starta Radarr igen. Om ditt system inte klarar av att stoppa Radarr och försöker starta om det automatiskt kan det vara bäst att använda ett skript istället. Vid misslyckande kommer den tidigare versionen av Radarr att startas om.
- Skript - Skriptet bör hantera samma saker som den inbyggda uppdateraren, om du behöver hantera stopp och start av tjänster (upstart/launchd/etc) måste du göra det här.

## Säkerhetskopior

- Säkerhetskopieringsavsnittet låter dig berätta för Radarr hur du vill hantera säkerhetskopior

- (Avancerad inställning) Mapp - Detta låter dig välja säkerhetskopieringsplatsen. I Docker kommer du att vara begränsad till vad du tillåter att behållaren ser. Sökvägar är relativa till appdata-mappen; om det behövs kan du ange en absolut sökväg för att säkerhetskopiera utanför appdata-mappen.
- (Avancerad inställning) Intervall - Hur ofta vill du att Radarr ska göra en säkerhetskopia
- (Avancerad inställning) Förvaring - Hur länge vill du att Radarr ska behålla varje säkerhetskopia. Efter att en ny säkerhetskopia har gjorts kommer den äldsta säkerhetskopian att tas bort

> Manuella säkerhetskopior behålls för evigt, lagras i samma mapp och har olika namn.
{.is-info}

# Användargränssnitt

## Kalender

- Första veckodagen - Här kan du välja vilken dag du tycker ska vara den första dagen i veckan.
- Kolumnrubrik för vecka - Här kan du välja rubriken för kolumnerna

## Filmer

- Format för körtid - Välj hur körtider ska formateras, antingen timmar och minuter eller minuter

## Datum

- Format för kort datum - Hur vill du att Radarr ska visa korta datum?
- Format för långt datum - Hur vill du att Radarr ska visa datum i långt format?
- Tidsformat - Vill du ha ett 12-timmars eller 24-timmars format?
- Visa relativa datum - Vill du att Radarr ska visa relativa (Idag/Igår/osv) eller absoluta datum?

## Stil

- Aktivera färgblind läge - Ändrad stil för att färgblinda användare ska kunna skilja färgkodad information bättre

## Språk

- Språk för filminformation - Välj språket för att visa filminformation i användargränssnittet för Radarr
- Språk för användargränssnitt - Välj språket för Radarr att använda i applikationens användargränssnitt