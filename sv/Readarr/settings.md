---
title: Readarr-inställningar
description: 
published: true
date: 2023-04-29T18:17:11.930Z
tags: readarr, inställningar
editor: markdown
dateCreated: 2021-11-25T15:07:27.926Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Menyalternativ](#menyalternativ)
- [Mediahantering](#mediahantering)
  - [Rotmappar](#rotmappar)
    - [Inställningar för rotmapp](#inställningar-för-rotmapp)
  - [Fjärrsökvägsmappningar](#fjärrsökvägsmappningar)
  - [Bokfilnamn](#bokfilnamn)
  - [Boknamn](#boknamn)
    - [Standardformat för bok](#standardformat-för-bok)
    - [Författare](#författare)
    - [Bok](#bok)
    - [Utgivningsdatum](#utgivningsdatum)
    - [Kvalitet](#kvalitet)
    - [Mediainformation](#mediainformation)
    - [Övrigt](#övrigt)
    - [Original](#original)
  - [Mappformat för författare](#mappformat-för-författare)
    - [Författare](#författare-1)
  - [Mappar](#mappar)
  - [Importering](#importering)
  - [Filhantering](#filhantering)
- [Behörigheter](#behörigheter)
- [Profiler](#profiler)
  - [Kvalitetsprofiler](#kvalitetsprofiler)
  - [Metadataprofiler](#metadataprofiler)
  - [Utgivningsprofiler](#utgivningsprofiler)
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
- [Indexerare](#indexerare)
  - [Stödda indexerare](#stödda-indexerare)
    - [Inställningar för indexerare](#inställningar-för-indexerare)
    - [Konfiguration av Usenet-indexerare](#konfiguration-av-usenet-indexerare)
    - [Konfiguration av torrentspårare](#konfiguration-av-torrentspårare)
  - [Alternativ](#alternativ)
- [Nedladdningsklienter](#nedladdningsklienter)
  - [Översikt](#översikt)
  - [Processer för nedladdningsklient](#processer-för-nedladdningsklient)
    - [Usenet-process](#usenet-process)
    - [Torrent-process](#torrent-process)
  - [Nedladdningsklienter](#nedladdningsklienter-1)
    - [Stödda nedladdningsklienter](#stödda-nedladdningsklienter)
    - [Inställningar för Usenet-klient](#inställningar-för-usenet-klient)
    - [Inställningar för torrentklient](#inställningar-för-torrentklient)
    - [Kompatibilitet för borttagning av nedladdning för torrentklient](#kompatibilitet-för-borttagning-av-nedladdning-för-torrentklient)
  - [Hantering av slutförda nedladdningar](#hantering-av-slutförda-nedladdningar)
    - [Ta bort slutförda nedladdningar](#ta-bort-slutförda-nedladdningar)
    - [Hantering av misslyckade nedladdningar](#hantering-av-misslyckade-nedladdningar)
  - [Fjärrsökvägsmappningar](#fjärrsökvägsmappningar-1)
- [Importlistor](#importlistor)
  - [Importlistor](#importlistor-1)
  - [Undantag för importlistor](#undantag-för-importlistor)
  - [Lägga till en importlista](#lägga-till-en-importlista)
- [Anslutning](#anslutning)
  - [Anslutningar](#anslutningar)
  - [Anslutningstriggers](#anslutningstriggers)
- [Metadata](#metadata)
  - [Calibre-metadata](#calibre-metadata)
  - [Skriv metadata till ljudfiler](#skriv-metadata-till-ljudfiler)
- [Taggar](#taggar)
- [Allmänt](#allmänt)
  - [Värd](#värd)
  - [Säkerhet](#säkerhet)
  - [Proxy](#proxy)
  - [Loggning](#loggning)
  - [Analys](#analys)
  - [Uppdateringar](#uppdateringar)
  - [Uppdateringar](#uppdateringar-1)
  - [Säkerhetskopior](#säkerhetskopior)
- [Användargränssnitt (UI)](#användargränssnitt-ui)
  - [Kalender](#kalender)
  - [Datum](#datum)
  - [Stil](#stil)
  - [Språk](#språk)

Den här sidan kommer att gå igenom alla inställningar som är tillgängliga i Readarr och hur de fungerar. Detta är inte menat att vara en omfattande "hur man ställer in Readarr". Om du vill ha det, använd sidan [Snabbstartsguide](/readarr/quick-start-guide) istället.

# Menyalternativ

För att komma till inställningssidan, välj Inställningar i vänstermenyn. Följande undermenyalternativ kommer att vara tillgängliga:

![settings_1_menu.png](/assets/readarr/settings_1_menu.png)

Observera också att för varje enskild inställningssida finns det några alternativ längst upp i menyn:

![settings_2_topmenu.png](/assets/readarr/settings_2_topmenu.png)

- Dölj/Visa avancerat är viktigt för alla objekt som är markerade nedan som `(Avancerad inställning)`, annars kommer de inte att visas. Dessa menyalternativ visas i orange i skärmbilderna.

- Du måste spara dina ändringar innan du lämnar skärmen. Du gör det genom att klicka på diskikonet. Om du inte har gjort några ändringar kommer det att stå "Inga ändringar" och vara grått, som visas ovan.

# Mediahantering

> Vissa av dessa inställningar är bara synliga genom att använda `Visa avancerade inställningar` som finns längst upp i verktygsfältet under sökfältet{.is-info}

## Rotmappar

- En lista över dina konfigurerade rotmappar (biblioteksmappar) visas.
- Klicka på <kb>+</kb>-knappen för att lägga till en ny rotmapp eller klicka på en befintlig mapp för att redigera den.

### Inställningar för rotmapp

- Namn - Namnet på rotmappen för användargränssnittet
- Sökväg - Mappen som innehåller ditt bokbibliotek, dvs. slutdestinationen som Readarr ser det.
  - Observera att detta måste vara annorlunda än platsen där din nedladdningsklient placerar filer.
  - Om du använder docker och Calibre-integration måste monteringen vara densamma som för dina böcker.

{#calibre}

- Specifika inställningar för Calibre (Endast om Använd Calibre är aktiverat)
  - Använd Calibre - Aktivera / Inaktivera användningen av Calibre Content Server för att hantera din rotmapp.

> \* Observera att detta **inte kan aktiveras för en befintlig rotmapp**.
> \* Observera att detta **inte kan inaktiveras för en befintlig rotmapp som har Calibre aktiverat**.
> \* Observera att detta kräver **Calibre Content Server** och fungerar inte med Calibre Web eller Calibre.
> \* Observera att hårddisklänkar inte fungerar med Calibre-integration.
> \* Observera att detta kräver att Calibre har "Kräv användarnamn och lösenord för att komma åt innehållsservern" aktiverat.
> \* Om "Kräv användarnamn och lösenord för att komma åt innehållsservern" inte är aktiverat i Calibre kommer det att resultera i ett felmeddelande om att "Anonyma användare får inte göra ändringar".
{.is-warning}

- Calibre-värd - IP/domän för värd för Calibre Content Server
- Calibre-port - Porten som Calibre Content Server lyssnar på
- (Avancerat) Calibre URL-bas - Lägg till ett prefix i Calibre URL, t.ex. `http://[värd]:[port]/[urlBase]`
- Calibre-användarnamn - Användarnamn för att komma åt Calibre Content Server
- Calibre-lösenord - Lösenord för att komma åt Calibre Content Server
- Calibre-bibliotek - Namn på Calibre Content Server-biblioteket. Lämna tomt för standard
- Konvertera till format - (Valfritt) Be Calibre Content Server att konvertera till andra format med en kommaseparerad lista.
  - Granska (i)-ikonen i appen för en aktuell lista över alternativ.
  - Alternativ är: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-utdataprofil - Välj utdataprofil för Calibre Content Server att använda
  - Utdataprofilen berättar för Calibre Content Server-konverteringssystemet hur man optimerar det skapade dokumentet för den angivna enheten (t.ex. genom att ändra storlek på bilder för enhetens skärmstorlek). I vissa fall kan en utdataprofil användas för att optimera utdata för en specifik enhet, men detta är sällan nödvändigt.
- Använd SSL - Aktivera eller inaktivera användningen av SSL (HTTPS) för Calibre Content Server
- Övervaka - Konfigurera dina övervakningsalternativ för böcker som upptäcks i denna mapp
  - Alla böcker - Övervaka alla böcker
  - Kommande böcker - Övervaka böcker som ännu inte har släppts
  - Saknade böcker - Övervaka böcker som inte har filer eller ännu inte har släppts
  - Befintliga böcker - Övervaka böcker som har filer eller ännu inte har släppts
  - Första boken - Övervaka den första boken. Alla andra böcker kommer att ignoreras
  - Senaste boken - Övervaka den senaste boken och kommande böcker
  - Ingen - Inga böcker kommer att övervakas om de inte läggs till explicit
- Kvalitetsprofil - Standardkvalitetsprofil för böcker och författare som upptäcks i denna mapp
- Metadataprofil - Välj metadataprofilen att använda för författare som upptäcks i denna mapp. För att bara ladda in böcker som har lagts till eller upptäckts explicit, välj Ingen.
- Standardtaggar för Readarr - Standardtaggar för författare som upptäcks i denna mapp

> Användare som inte använder Windows:
> \* Om du använder en NFS-montering, se till att `nolock` är aktiverat.
> \* Om du använder en SMB-montering, se till att `nobrl` är aktiverat.
{.is-warning}

## Fjärrsökvägsmappningar

- Fjärrsökvägsmappning fungerar som en dum sökning efter fjärrsökväg och ersättning med lokal sökväg. Detta används främst för antingen sammanslagna lokala/fjärruppsättningar med mergerfs eller liknande, eller används när applikationen och nedladdningsklienten eller Calibre inte är på samma server.
- För mer information, se avsnittet i [Nedladdningsklienter => Fjärrsökvägsmappning](#fjärrsökvägsmappningar-1) ersätt `<Nedladdningsklient>` med `<Calibre>`

## Bokfilnamn

![bookfilenaming.png](/assets/readarr/bookfilenaming.png)

**Om du använder Calibre-integration får du inte namnge bokfiler. Calibre tar hand om detta åt dig. Du bör bara ändra dessa inställningar om du inte använder Calibre.**

> Observera att medan Readarr är i beta; om du använder Calibre rekommenderas det att inaktivera namnändring i Readarr bara för att vara på den säkra sidan ifall en oavsiktlig bugg smyger sig igenom. {.is-info}

Vanligt använda namnscheman är:

- Standardformat för bok
  - `{Boktitel}\{Författarnamn}` - `{Boktitel}` vilket sedan skulle ge en mapp med namnet `Cujo` och en undermapp som innehåller en fil med namnet `Stephen King - Cujo.m4b`

- Mappformat för författare
  - `{Författarnamn}` vilket sedan skulle ge: `Stephen King`

## Boknamn

- Byt namn på böcker - Om detta är avmarkerat (ingen bock i rutan) kommer Readarr att använda det befintliga filnamnet om namnändring är inaktiverat.
  - Om det inte är markerat:
    - Import från nedladdningsklient
      - Nedladdningsklientens utgivningstitel används
    - Manuell (ad hoc) import: Originalfilnamn

> Om du lämnar Byt namn på böcker avmarkerat, gäller inte något av namngivningen nedan - du har sagt till Readarr att du inte vill ha någon namnändring alls. Boken kommer att importeras direkt till författarmappen.
{.is-info}

> Detta gäller inte om Calibre används eftersom Calibre hanterar fil-/mappnamn med sin egen interna struktur.
{.is-info}

- Ersätt otillåtna tecken - Om det är inaktiverat kommer Readarr att ta bort otillåtna tecken. Om det är aktiverat kommer Readarr att ersätta otillåtna tecken. Exempel på otillåtna tecken är `\ # / $ * < >` och mer.

### Standardformat för bok

- Välj namngivningen

- Rullgardinsmeny (övre högra hörnet)
  - Vänster ruta - Hantering av mellanslag
    - `Mellanslag ( )` - Använd mellanslag i namngivningen (Standard)
    - `Punkt (.)` - Använd punkter istället för mellanslag i namngivningen
    - `Understreck (_)` - Använd understreck istället för mellanslag i namngivningen
    - `Bindestreck (-)` - Använd bindestreck istället för mellanslag i namngivningen
  - Höger ruta - Hantering av versaler/gemener
    - `Standardvärde` - Gör titeln versaler och gemener (~camel-case) (Standard)
    - `Versaler` - Gör hela titeln versaler
    - `Gemener` - Gör hela titeln gemener

### Författare

- `{Författarnamn}` = Författarens namn
- `{FörfattarnamnThe}` = Författarens namn, The
- `{FörfattarCleanName}` = Författarens namn
- `{FörfattarSortName}` = Namn, Författare
- `{FörfattarDisambiguation}` = Författarnamn (disambiguation används från GoodReads för flera författare med samma namn)

### Bok

- `{Boktitel}` = Bokens titel!: Undertitel!
- `{BoktitelThe}` = Bokens titel!, The: Undertitel!
- `{BokCleanTitle}` = Bokens titel: Undertitel
- `{BoktitelNoSub}` = Bokens titel!
- `{BoktitelTheNoSub}` = Bokens titel!, The
- `{BokCleanTitleNoSub}` = Bokens titel
- `{BokUndertitel}` = Undertitel!
- `{BokUndertitelThe}` Undertitel!, The
- `{BokCleanUndertitel}` = Undertitel
- `{BokDisambiguation}` = Boknamn! (disambiguationstitel används från GoodReads)
- `{BokSerie}` = Serietitel
- `{BokSeriePosition}` = 1
- `{BokSerieTitle}` = Serietitel #1
- `{Delnummer:0}` eller `{Delnummer:0}` = 2
- `{Delnummer:00}` = 02
- `{Delantal}` eller `{Delantal:0} = 9
- `{Delantal:00}` = 09

### Utgivningsdatum

- `{Utgivningsår}` = 2016
- `{UtgivningsårFörst}` = 2015
- `{Utgåvaår}` = 2016

### Kvalitet

- `{KvalitetFull}` = AZW3 Proper
- `{KvalitetTitel}` = AZW3

### Mediainformation

- `{MediaInfoLjudCodec}` = MP3
- `{MediaInfoLjudKanaler}` = 2.0
- `{MediaInfoLjudBitrate}` = 320kbps
- `{MediaInfoLjudBitsPerSample}` = 24bit
- `{MediaInfoLjudSamplingsfrekvens}` = 44.1kHz

### Övrigt

- `{Utgivargrupp}` = Rls Grp
- `{Föredragna ord}` = iNTERNAL

### Original

- `{Originaltitel}` = Författare.Namn.Bok.Namn.2018.AZW3-EVOLVE
- `{Originalfilnamn}` = 01-boknamn

> Originalfilnamn rekommenderas inte. Det är det bokstavliga ursprungliga filnamnet och kan vara förklädd till t1i0p3s7i8yuti. Originaltitel är utgåvans namn och bör användas istället.
{.is-info}
  
## Mappformat för författare

- (Avancerad inställning) Här ställer du in namnkonventionen för författarmappens namn.

> Detta gäller inte om Calibre används eftersom Calibre hanterar fil-/mappnamn med sin egen interna struktur.
{.is-info}

### Författare

- `{Författarnamn}` = Författarens namn
- `{FörfattarnamnThe}` = Författarens namn, The
- `{FörfattarCleanName}` = Författarens namn
- `{FörfattarSortName}` = Namn, Författare
- `{FörfattarDisambiguation}` = Författarnamn (disambiguation används från GoodReads för flera författare med samma namn)

## Mappar
  
![mm_folders.png](/assets/readarr/mm_folders.png)
  
- (Avancerad inställning) Skapa tomma författarmappar - Markera rutan för att skapa tomma författarmappar när en ny författare läggs till.
- (Avancerad inställning) Ta bort tomma författarmappar - Markera rutan för att ta bort tomma författarmappar om det inte finns några böcker i dem.
  
> En av dessa rutor kan markeras, men de får INTE båda vara markerade. {.is-warning}

> Detta gäller inte om Calibre används eftersom Calibre hanterar fil-/mappnamn med sin egen interna struktur.
{.is-info}

## Importera
  
![mm_importing.png](/assets/readarr/mm_importing.png)
  
- (Avancerad inställning) Hoppa över kontroll av ledigt utrymme - Om detta är aktiverat kommer kontrollen av ledigt utrymme att hoppas över innan importering.
- (Avancerad inställning) Minsta lediga utrymme - Ange det minsta lediga utrymmet för enheten innan importeringen stoppas.
- (Avancerad inställning) Använd hårddisklänkar istället för kopior - Markera den här rutan för att använda hårddisklänkar istället för kopior (för torrents). Observera att detta är aktiverat som standard.
  
> Du bör helst använda detta när det är möjligt. För att kunna använda hårddisklänkar måste källan/målet finnas på samma filsystem (enhet, partition) och monteringspunkter. [Se TRaSH's Hardlink Guide för mer information](https://trash-guides.info/hardlinks/)
  
- Importera extra filer - Om detta är aktiverat importeras angivna extra filer som finns i mappen för boken när den importeras.
- (Avancerad inställning) Importera extra filer - Om importera extra filer är aktiverat, ange en kommaseparerad lista med filändelser som ska importeras.

> Om du använder Readarr för ljudböcker bör du lägga till .cue i denna lista, eftersom den innehåller din kapitelinformation!
{.is-info}
  
## Filhantering
  
  ![mm_filemgmt.png](/assets/readarr/mm_filemgmt.png)

- Ignorera borttagna böcker - Markera den här rutan för att inte övervaka böcker som har upptäckts som borttagna eller otillgängliga från Readarrs rotmapp.
- Ladda ner korrekta och repacks - Om du vill uppgradera automatiskt till korrekta och repacks. Använd "Föredrar inte" för att sortera efter föredragna ordpoäng över korrekta/repacks.
  - Föredrar och uppgradera - Ranka repacks och korrekta högre än icke-repacks och icke-korrekta. Behandla nya repacks och korrekta som uppgraderingar av nuvarande utgåvor.
  - Uppgradera inte automatiskt - Ranka repacks och korrekta högre än icke-repacks och icke-korrekta. Behandla inte nya repacks och korrekta som uppgraderingar av nuvarande utgåvor.
  - Föredrar inte - Ignorera i princip repacks och korrekta. Du måste hantera eventuella preferenser för dessa med [Föredragna ord](#release-profiler).
  
> \* `PROPER` - betyder att det fanns ett problem med den tidigare utgåvan. Nedladdningar som är märkta som PROPER visar att problemen har åtgärdats i den utgåvan. Detta görs av en grupp som inte släppte originalet.
> \* `REPACK` - betyder att det fanns ett problem med den tidigare utgåvan och att det har åtgärdats av den ursprungliga gruppen. Nedladdningar som är märkta som REPACK visar att problemen har åtgärdats i den utgåvan. Detta görs av en grupp som släppte originalet.
{.is-info}

- (Avancerad inställning) Bevaka rotmappar för filändringar - Markera den här rutan för att utlösa en omsökning när det upptäcks att rotmappen har ändrats.
- (Avancerad inställning) Omsök författarmapp efter uppdatering - Välj när en författarmapp ska omsökas efter att författaren har uppdaterats.
  - Alltid - Detta kommer att omsöka författarmappar baserat på schemalagda uppgifter
  - Efter manuell uppdatering - Du måste manuellt omsöka disken
  - Aldrig - Precis som det låter, aldrig omsök författarmapparna.
- (Avancerad inställning) Tillåt fingeravtryck - Välj hur fingeravtryck ska hanteras, vilket möjliggör ökad noggrannhet för matchning av böcker, på bekostnad av CPU/disktid.
  - Alltid - Använd alltid fingeravtryck om möjligt
  - Endast för nya importeringar - Använd endast fingeravtryck för nyimporterade utgåvor
  - Aldrig - Precis som det låter, använd aldrig fingeravtryck
- (Avancerad inställning) Ändra filens datum - Ändra filens datum vid import/omskanning
  - Ingen - Readarr kommer inte att ändra datumet som visas i din filbläddrare
  - Bokens utgivningsdatum - Datumet då boken släpptes.
- (Avancerad inställning) Återvinningskorg - Bokfiler kommer att hamna här när de raderas istället för att raderas permanent
- (Avancerad inställning) Rensa återvinningskorgen - Så gammal en given fil kan vara innan den raderas permanent

> Det rekommenderas starkt att du använder en återvinningskorg. Det är lätt att radera filer, och det är enkelt att återställa dem om du använder återvinningskorgen.
{.is-warning}

# Behörigheter

- Ange behörigheter - Ska `chmod` köras när filer importeras/ändras?
  - chmod-mapp - Oktal, tillämpas vid import/ändring av mediemappar och filer (utan körbara bitar)

> Listrutan har en förinställd lista med mycket vanligt använda behörigheter som kan användas. Du kan dock manuellt ange en mapp-oktal om du vill.
{.is-info}

> Detta fungerar endast om användaren som kör `Readarr` är ägare till filen. Det är bättre att se till att nedladdningsklienten ställer in behörigheterna korrekt.
{.is-warning}

- chown-grupp - Gruppnamn eller GID. Använd GID för fjärrfiler

> Detta fungerar endast om användaren som kör `Readarr` är ägare till filen. Det är bättre att se till att nedladdningsklienten ställer in behörigheterna korrekt.
{.is-warning}

# Profiler

## Kvalitetsprofiler

Kvalitetsprofiler används för att bestämma vilka format av böcker som är acceptabla för en bok i ditt bibliotek.
  
![qualityprofile.png](/assets/readarr/qualityprofile.png)

- Ange profiler för kvaliteten på böcker du vill ladda ner.

> När du väljer en befintlig profil eller lägger till en ytterligare profil visas ett nytt fönster
> Observera: Kvaliteten som har en blå ruta är kvaliteten som alla medier med denna profil kommer att uppgraderas till.
{.is-info}

- Plusikon (<kb>+</kb>) - Skapa en ny kvalitetsprofil

- Namn - Ange ett **UNIKT** namn för den kvalitetsprofil du skapar
- Uppgraderingar tillåtna - När detta alternativ är markerat och du ber Readarr att ladda ner en `EPUB` eftersom det är den första utgåvan av en specifik bok och senare kan någon ladda upp en `AZW3` kommer Readarr automatiskt att uppgradera till bättre kvalitet ***om*** `Uppgradera tills` har den kvaliteten vald
  - Uppgradera tills - När denna kvalitet har uppnåtts kommer Readarr inte längre att ladda ner böcker

> Observera: Detta gäller endast om du har `AZW3` högre än `EPUB` inom avsnittet `Kvaliteter`
{.is-warning}

- Kvaliteter - Kvaliteter högre upp i listan är mer föredragna oavsett önskad (aktiverad/bockad) status. Kvaliteter inom samma grupp är likvärdiga. Endast aktiverade (bockade) kvaliteter är önskade (tillåtna)
  - Redigera grupper - Vissa kvaliteter grupperas för att minska storleken på listan samt gruppera liknande utgåvor. Ett bra exempel på detta är `WebDL` och `WebRip` eftersom dessa är mycket lika och vanligtvis har liknande bitrater. När du redigerar grupperna kan du ändra preferensen inom varje grupp.

  - [Se Kvaliteter](#kvaliteter-definierade)

> Som standard är kvaliteterna inställda från "sämst" (nedre delen) till "bäst" (övre delen)
{.is-info}

## Metadataprofiler

Metadataprofiler används för att bestämma vilka böcker från GoodReads som ska läggas till under en författare när en ny författare läggs till.

- Plusikon (<kb>+</kb>) - Skapa en ny metadataprofil

![metaprofiles.png](/assets/readarr/metaprofiles.png)
  
- Namn - Ange ett **UNIKT** namn för metadataprofilen
- Minsta popularitet - Ange den minsta populariteten för en bok som ska läggas till för en författare.

> Om du ställer in detta för högt kommer böcker inte att läggas till i Readarr, men om du ställer in det för lågt kan obskyra publikationer visas.
{.is-warning}

> Ställ in detta på `10000000000` exakt för att skapa en profil som motsvarar `Ingen` men fortfarande tillåter andra filtreringar av utgåvor och böcker. Observera att `Ingen` inte tillämpar några metadatafilter och du kan få utländska utgåvor.
{.is-info}

- Minsta antal sidor - Ange det minsta antalet sidor som en bok måste ha för att läggas till för en författare.
- Hoppa över böcker utan utgivningsdatum - Aktivera för att hoppa över böcker utan utgivningsdatum.
- Hoppa över böcker utan ISBN eller ASIN - Aktivera för att hoppa över böcker som inte innehåller något ISBN eller ASIN-nummer.
- Hoppa över delböcker och serier - Aktivera för att hoppa över delböcker och serier.
- Hoppa över sekundära serieböcker - Aktivera för att hoppa över sekundära serieböcker.
- Tillåtna språk - Ange en kommaseparerad lista med ISO 639-3-språkkoder eller 'null' för tillåtna språk för dina böcker
- Får inte innehålla - Ange ord eller fraser som en boktitel inte får innehålla för att läggas till.

> Du kan skapa flera metadataprofiler och tillämpa en separat profil på varje författare vid behov. Men du kan bara tillämpa en enda metadataprofil på en given författare.
{.is-info}
  
## Utgivningsprofiler

Utgivningsprofiler används för att avgöra om indexeringsnamn kvalificerar sig för nedladdning.

![releaseprofiles.png](/assets/readarr/releaseprofiles.png)  
  
- Aktivera profil - Markera rutan för att aktivera denna profil.
- Måste innehålla - Lägg till en lista med ord eller fraser som MÅSTE finnas i utgivningsnamnet för att det ska anses vara giltigt.
- Får inte innehålla - Lägg till en lista med ord eller fraser som INTE FÅR finnas i utgivningsnamnet för att det ska anses vara giltigt.
- Föredragna (ord) - Här kan du lägga till termer eller regex med poäng (positiva och negativa) som ska anses vara mer eller mindre föredragna. Till exempel kan du föredra "unabridged" med en positiv poäng.
  
> Utgåvor med en högre poäng för föredragna ord än den befintliga filen är ALLTID en uppgradering!
{.is-info}
  
- Inkludera föredragna vid namngivning Markera den här rutan för att inkludera dina föredragna ord (eller regex-matchningar) i tilldelningen av filnamn med `{Preferred Words}`.

> Du bör inkludera `{Preferred Words}` i ditt filnamn och markera den här rutan om du använder dem, eftersom du annars kan hamna i en nedladdningsloop.
{.is-warning}

- Indexer - I den här listrutan kan du begränsa denna utgivningsprofil till en enda indexer. Detta bör nästan alltid lämnas som `(any)` (vilken som helst)
- Taggar - Ange en tagg här för att kunna tillämpa denna tagg på författare med samma tagg. Om du inte tillämpar en tagg här gäller denna profil för ALLA författare.

## Fördröjningsprofiler

- Fördröjningsprofiler gör det möjligt att minska antalet utgåvor som laddas ner för en bok genom att lägga till en fördröjning medan Readarr fortsätter att övervaka utgåvor som bättre matchar dina preferenser.
- Protokoll - Detta kommer antingen att vara `Usenet` eller `Torrent` beroende på vilket nedladdningsprotokoll du föredrar
- Usenet-fördröjning - Ange antalet minuter du vill vänta innan nedladdningen startar
- Torrent-fördröjning - Ange antalet minuter du vill vänta innan nedladdningen startar
- Bypassa om högsta kvalitet - Bypassa fördröjningen när utgåvan har den högsta aktiverade kvalitetsprofilen med det föredragna protokollet
- Taggar - Genom att ge denna fördröjningsprofil en tagg kan du tagga en given bok för att få den att följa reglerna som är inställda här.
- Skiftnyckelikon - Detta låter dig redigera fördröjningsprofilen
- Plusikon (<kb>+</kb>) - Skapa en ny fördröjningsprofil

### Användningsområden

Vissa media kommer att få ett halvt dussin olika utgåvor av varierande kvalitet under timmarna efter en utgivning, och utan fördröjningsprofiler kan Readarr försöka ladda ner alla. Med fördröjningsprofiler kan Readarr konfigureras för att ignorera de första timmarna av utgåvor.

Fördröjningsprofiler är också användbara om du vill betona ett protokoll (Usenet eller BitTorrent) över det andra. (Se exempel 3)

### Hur fördröjningsprofiler fungerar

Timern börjar så snart Readarr upptäcker att en bok har en tillgänglig utgåva. Denna utgåva visas i din kö med en klockikon för att indikera att den är under fördröjning.

> Klockan börjar från tidpunkten då utgåvan laddades upp och inte från den tidpunkt då Readarr ser den. {.is-info}

Under fördröjningsperioden kommer Readarr att notera eventuella nya utgåvor som blir tillgängliga. När fördröjningstimern löper ut kommer Readarr att ladda ner den enda utgåvan som bäst matchar dina kvalitetspreferenser.

Tidperioden kan vara olika för Usenet och torrents. Varje profil kan associeras med en eller flera taggar för att du ska kunna anpassa vilka böcker som har vilka profiler. En fördröjningsprofil utan tagg betraktas som standard och gäller för alla böcker som inte har en specifik tagg.

> Fördröjningsprofiler börjar från tidsstämpeln som indexer rapporterar att utgåvan laddades upp. Det innebär att allt innehåll som är äldre än det antal minuter du har ställt in påverkas inte på något sätt av din fördröjningsprofil och kommer att laddas ner omedelbart. Dessutom kommer **alla manuella sökningar** efter innehåll (sökningar som inte är RSS-flödessökningar) att ignorera inställningarna för fördröjningsprofil.
{.is-warning}

#### Exempel

- För varje exempel, anta att användaren har följande kvalitetsprofil aktiv: EPUB och högre är tillåtna MOBI är kvalitetsgränsen * AZW3 är den högst rankade kvaliteten

##### Exempel 1

- I detta enkla exempel är profilen inställd med en 120 minuters (två timmar) fördröjning för både Usenet och torrents.

- Klockan 23:00 upptäcker Readarr den första utgåvan av en bok och den laddades upp kl. 22:50 och 120 minuters klockan börjar ticka. Kl. 00:50 kommer Readarr att utvärdera alla utgåvor som den har hittat under de senaste två timmarna och ladda ner den bästa, som är MOBI.

- Kl. 03:00 hittas en annan utgåva, som är MOBI och lades till i din indexer kl. 02:46. En annan 120 minuters klocka börjar ticka. Kl. 04:46 laddas den bästa tillgängliga utgåvan ner. Eftersom kvalitetsgränsen nu har nåtts kan boken inte längre uppgraderas och Readarr kommer att sluta leta efter nya utgåvor.

- Vid vilken tidpunkt som helst, om en AZW3-utgåva hittas, kommer den att laddas ner omedelbart eftersom det är den högst rankade kvaliteten. Om det finns en aktiv fördröjningstimer kommer den att avbrytas.

##### Exempel 2

- Detta exempel har olika timrar för Usenet och torrents. Anta en 120 minuters timer för Usenet och en 180 minuters timer för BitTorrent.

- Kl. 23:00 upptäcker Readarr den första utgåvan av en bok och båda timrarna börjar ticka. Utgåvan lades till i indexer kl. 22:15. Kl. 00:15 kommer Readarr att utvärdera alla utgåvor och om det finns några godtagbara Usenet-utgåvor kommer den bästa att laddas ner och båda timrarna kommer att sluta ticka. Om det inte finns några sådana utgåvor kommer Readarr att vänta tills kl. 00:15 och ladda ner den bästa utgåvan, oavsett vilken källa den kommer från.

##### Exempel 3

- Ett vanligt användningsområde för fördröjningsprofiler är att betona ett protokoll över det andra. Till exempel kan du bara vilja ladda ner en BitTorrent-utgåva om ingenting har laddats upp till Usenet efter en viss tid.

- Du kan ställa in en 60 minuters timer för BitTorrent och en 0 minuters timer för Usenet.

- Om den första utgåvan som upptäcks kommer från Usenet kommer Readarr att ladda ner den omedelbart.

- Om den första utgåvan kommer från BitTorrent kommer Readarr att ställa in en 60 minuters timer. Om någon kvalificerad Usenet-utgåva upptäcks under den tiden kommer BitTorrent-utgåvan att ignoreras och Usenet-utgåvan kommer att laddas ner.

# Kvalitet

![qualitydefinitions.png](/assets/readarr/qualitydefinitions.png)

## Betydelser för kvalitetstabell

- Kvalitet - Namnet på kvaliteten enligt scenen (hårdkodad)
- Titel - Namnet på kvaliteten i gränssnittet (konfigurerbar)
- Megabyte per minut - Självförklarande
- Storleksgräns - Självförklarande
- Min - Minsta antal byte eller kilobyte per sekund (b/s|kb/s) som en kvalitet kan ha.
- Max - Högsta antal byte eller kilobyte per sekund (b/s|kb/s) som en kvalitet kan ha.

## Definierade kvaliteter

- Okänd text - Självförklarande
- PDF - Bärbar dokumentfil
- MOBI - Ett av de mest använda e-boksformaten
- EPUB - Ett annat av de mest använda e-boksformaten
- AZW3 - AZW3 är en e-boksfil som utvecklats av Amazon. Den används i Amazon Kindles för att visa e-böcker.
- Okänt ljud - Självförklarande
- MP3 - Vanligt förlustrikt ljudformat
- M4B - Vanligt ljudboksfilformat
- FLAC - Free Lossless Audio Codec, ett ljudformat som liknar MP3, men förlustfritt

# Indexerare

> Information om stödda indexerare finns på sidan [Mer information (Stödda)](/readarr/supported#indexers) för detta avsnitt
{.is-info}

## Stödda indexerare

- En lista över stödda indexerare finns på sidan [Mer information (Stödda)](/readarr/supported#indexers)

### Inställningar för indexerare

- När du har klickat på <kb>+</kb>-knappen för att lägga till en ny indexerare visas ett nytt fönster med många olika alternativ. För syftet med denna dokumentation betraktar Readarr både Usenet-indexerare och torrentspårare som "indexerare".

- Här finns två avsnitt: Usenet och torrents. Beroende på vilken nedladdningsklient du kommer att använda vill du välja vilken typ av indexerare du kommer att använda.

### Konfiguration av Usenet-indexerare

- Enable - If enabled, Readarr will remove completed downloads from your download client after importing them.
- Remove Method - Choose the method to remove completed downloads. Options are:
  - Move to Recycle Bin - Moves the completed downloads to the recycle bin.
  - Delete Permanently - Deletes the completed downloads permanently without moving them to the recycle bin.
- Remove Trigger - Choose when to trigger the removal of completed downloads. Options are:
  - When seeding is complete - Removes the completed downloads when they have finished seeding.
  - When torrent is stopped - Removes the completed downloads when the torrent is stopped.
- Remove Delay - Set a delay in minutes before removing the completed downloads. This can be useful if you want to keep the completed downloads for a certain period of time before removing them.

### Failed Download Handling

- Failed Download Handling is how Readarr handles failed downloads from your download client.

- Enable - If enabled, Readarr will handle failed downloads from your download client.
- Retry Failed Downloads - If enabled, Readarr will automatically retry failed downloads.
- Retry Delay - Set a delay in minutes before retrying failed downloads.
- Retry Limit - Set the maximum number of times Readarr will retry failed downloads before giving up.

### Remote Path Mappings

- Remote Path Mappings are used to map the remote paths reported by your download client to the local paths on your system. This is necessary if your download client reports remote paths that are different from the actual paths on your system.

- Local Path - The local path on your system.
- Remote Path - The remote path reported by your download client.
- Enabled - If enabled, the remote path mapping will be used.

## Download Client Priority

- Download Client Priority is used to prioritize one download client over another when multiple download clients are available.

- Priority - Set the priority of the download client. The lower the number, the higher the priority. The highest priority download client will be used first.

## Importing Existing Media

- Importing Existing Media is used to import media that is already on your system into Readarr.

- Import Existing Series - If enabled, Readarr will scan your media folders for existing series and add them to your library.
- Import Existing Episodes - If enabled, Readarr will scan your media folders for existing episodes and match them to the corresponding series in your library.

## Import Extra Files

- Import Extra Files is used to import additional files that are associated with your media files.

- Enable - If enabled, Readarr will import extra files such as subtitles, artwork, etc. that are associated with your media files.
- Extra File Extensions - Specify the file extensions of the extra files that you want to import. Separate multiple extensions with commas.

## Metadata

- Metadata is used to retrieve additional information about your media files.

- Language - Set the language for the metadata.
- Metadata Profile - Choose the metadata profile to use. Options are:
  - Default - Use the default metadata profile.
  - Plex - Use the Plex metadata profile.
  - Custom - Use a custom metadata profile.

## Permissions

- Permissions are used to control access to Readarr.

- Enable - If enabled, Readarr will enforce permissions.
- Admin Only - If enabled, only administrators will have access to Readarr.

- Readarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
- Readarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- När nedladdningen är klar kommer Readarr att känna till den slutliga filplatsen som rapporteras av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp.
- Readarr kommer att skanna den avslutade filplatsen efter videofiler. Den kommer att analysera videofilens namn för att matcha den med en bok. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den tilldelade biblioteksmappen.
- Överblivna filer från nedladdningen skickas till papperskorgen eller återvinningen.

Om du laddar ner med en BitTorrent-klient är processen något annorlunda:

- Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda. När filer importeras till din tilldelade biblioteksmapp kommer Readarr att försöka skapa en hårdlänk till filen eller falla tillbaka till att kopiera (använda dubbel mellanslag) om hårdlänkar inte stöds.
- Om alternativet "Hantering av slutförda nedladdningar - Ta bort" är aktiverat i inställningarna kommer Readarr att be torrentklienten att ta bort den ursprungliga filen och torrenten, men detta kommer bara att ske om klienten rapporterar att seedningen är klar, torrenten är i samma kategori (dvs. inte använder en efter-importkategori), målet för seedning som stöds av Readarr har nåtts och torrenten är pausad (stoppad).

### Hantering av misslyckade nedladdningar

- Hantering av misslyckade nedladdningar är endast kompatibel med SABnzbd och NZBGet.
- Hantering av misslyckade nedladdningar gäller inte för torrents och det finns inga planer på att lägga till en sådan funktion.

- Det finns flera komponenter som ingår i processen för hantering av misslyckade nedladdningar:

- Kontrollera nedladdare:
  - Kö - Kontrollera din nedladdares kö för lösenordsskyddade (krypterade) släpp som markerats som misslyckade
  - Historik - Kontrollera din nedladdares historik för misslyckanden (t.ex. inte tillräckligt med reparationer eller extrahering misslyckades)
- När Readarr hittar en misslyckad nedladdning börjar den bearbeta dem och gör några saker:
  - Lägger till en misslyckad händelse i Readarrs historik
  - Tar bort den misslyckade nedladdningen från nedladdningsklienten för att frigöra utrymme och rensa nedladdade filer (valfritt)
  - Börjar söka efter en ersättningsfil (valfritt)
  - Blocklistning (tidigare kallat 'Blacklisting') möjliggör automatisk hoppning över nzbs när de misslyckas, vilket innebär att nzb aldrig kommer att laddas ner automatiskt av Readarr igen (du kan fortfarande tvinga nedladdningen via en manuell sökning).
  - Det finns 2 avancerade alternativ (på sidan 'Nedladdningsklientens' inställningar) som styr beteendet för misslyckade nedladdningar i Readarr, för närvarande är de alla aktiverade som standard.

- Ladda ner igen - Styr om Readarr ska söka efter samma fil efter ett misslyckande
- (Avancerat alternativ) Ta bort - Om nedladdningen automatiskt ska tas bort från nedladdningsklienten när felet upptäcks

## Fjärrsökvägsmappningar

- Fjärrsökvägsmappning fungerar som en enkel sökning efter fjärrsökväg och ersättning med lokal sökväg. Detta används främst för antingen sammanslagna lokala/fjärruppsättningar med hjälp av mergerfs eller liknande, eller används när programmet och nedladdningsklienten inte finns på samma server.
- En fjärrsökvägsmappning används när din nedladdningsklient rapporterar en sökväg för slutförda data antingen på en annan server eller på ett sätt som \*Arr inte adresserar den mappen.
- Generellt sett krävs en fjärrsökvägsmappning endast om din nedladdningsklient körs på Linux när \*Arr körs på Windows eller vice versa. En fjärrsökvägsmappning kan också behövas om du blandar Docker- och nativa klienter eller om du använder en fjärrserver.
- En fjärrsökvägsmappning är en ENKEL sökning/ersättning (där den hittar VÄRDET FÖR FJÄRRSÖKVÄGEN och ersätter det med VÄRDET FÖR LOKAL SÖKVÄG för den angivna värden).
- Om felmeddelandet om en felaktig sökväg inte innehåller VÄRDET FÖR ERSÄTTNINGEN fungerar inte sökvägsmappningen som du förväntar dig. Den vanliga lösningen är att lägga till och ta bort mappningen.
- [Se TRaSH's handledning för ytterligare information om fjärrsökvägsmappning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Om både \*Arr och din nedladdningsklient är Docker-kontainrar behövs det sällan en fjärrsökvägsmappning. Det rekommenderas att du [granskar Docker-guiden](/docker-guide) och/eller [följer TRaSH's handledning](https://trash-guides.info/hardlinks)
{.is-info}

# Importlistor

> Information om stödda listtyper finns på sidan [Mer information (Stödda)](/readarr/supported#lists) för den här sektionen
{.is-info}

Importlistor gör det möjligt att automatiskt lägga till objekt i Readarr från dina GoodReads-hyllor eller från andra användare. Detta kan lägga till många oväntade objekt i din Readarr-databas, så använd det med försiktighet.

![importlists.png](/assets/readarr/importlists.png)

## Importlistor

Detta visar de listor du för närvarande har och låter dig lägga till nya listor. Att lägga till listor täcks mer detaljerat nedan.

## Importlistexkluderingar

Allt som finns här har uteslutits från att läggas till av listor och kommer aldrig att läggas till från någon lista. Du kan ta bort objekt från detta genom att klicka på det.

## Lägga till en importlista

Efter att ha klickat på <kb>+</kb>, välj vilken typ av lista du vill lägga till:

![addlist.png](/assets/readarr/addlist.png)

I det här fallet kommer vi att lägga till en GoodReads bokhylllista.

![bookshelflist.png](/assets/readarr/bookshelflist.png)

- Namn - Ange ett namn för denna lista.
- Aktivera automatiskt lägg till - Om det är aktiverat kommer allt på listan automatiskt att läggas till i Readarr.

> Detta kommer att lägga till alla författare och ALLA BÖCKER från den författaren i Readarr!

- Övervaka - Välj din övervakningsnivå för de saker som läggs till. Giltiga alternativ är `Inget`, `Vald bok` och `Alla författare böcker`. Alla böcker läggs till i Readarr, men kommer att övervakas eller inte övervakas baserat på detta val.
- Sök efter nya objekt - Om det är aktiverat kommer Readarr att initiera en sökning efter saknade övervakade objekt när de läggs till från en lista. Om du lägger till många författare/övervakade böcker kan detta överbelasta ditt system!
- Rotmapp - Välj rotmappen för författare som läggs till från denna lista
- Kvalitetsprofil - Välj din kvalitetsprofil för författare som läggs till från denna lista
- Metadataprofil - Välj din metadataprofil för författare som läggs till från denna lista
- Readarr-taggar - Välj vilka taggar som gäller för författare som läggs till från denna lista

> Det rekommenderas starkt att du lägger till en beskrivande tagg här. Annars kommer du inte att veta vilken lista som har lagt till dessa objekt i Readarr, och när de väl har lagts till kan du aldrig få denna information igen! Denna information loggas inte!

Listor synkroniseras som standard var 24:e timme, men kan utlösas manuellt från sidan `Inställningar` => `Uppgifter`. Du kan inte automatisera denna process snabbare än så.

# Anslutning

> Information om stödda anslutningstyper finns på sidan [Mer information (Stödda)](/readarr/supported#notifications) för den här sektionen
{.is-info}

## Anslutningar

Anslutningar är hur du vill att Readarr ska kommunicera med omvärlden.

- Genom att trycka på <kb>+</kb>-knappen kommer du att presenteras med ett nytt fönster som låter dig konfigurera många olika slutpunkter

- En lista över stödda meddelanden och anslutningar finns på sidan [Mer information (Stödda)](/readarr/supported#notifications)

## Anslutningstriggers

- Vid hämtning - Få meddelande när böcker finns tillgängliga för nedladdning och har skickats till en nedladdningsklient
- Vid import av släpp - Få meddelande när böcker har importerats framgångsrikt
- Vid uppgradering - Få meddelande när böcker uppgraderas till bättre kvalitet
- Vid nedladdningsfel - Få meddelande när en boknedladdning misslyckas (endast Usenet)
- Vid importfel - Få meddelande när en boknedladdning misslyckas att importeras
- Vid namnbyte - Få meddelande när böcker byter namn
- Vid radering av författare - Få meddelande när en författare raderas
- Vid radering av bok - Få meddelande när en bok raderas
- Vid radering av bokfil - Få meddelande när en bokfil raderas
- Vid radering av bokfil för uppgradering - Få meddelande när en bokfil raderas för en uppgradering
- Vid omtaggning av bok - Få meddelande när böcker omtaggas
- Vid hälsoproblem - Få meddelande om hälsokontrollfel
  - Inkludera hälsovarningar - Få meddelande om hälsovarningar utöver fel.

# Metadata

{#write-metadata-to-book-files}

> Information om stödda metadatakonsumenter finns på sidan [Mer information (Stödda)](/readarr/supported#metadata) för den här sektionen
{.is-info}

Den här sidan låter dig skapa/uppdatera metadata-taggar/omslag.

![metadata.png](/assets/readarr/metadata.png)

## Calibre-metadata

Om du använder Calibre för att hantera din e-bokssamling kommer du att använda dessa alternativ för att styra det.

- Skicka metadata till Calibre
  - Alla filer; håll synkroniserad med GoodReads - Skriv taggar till alla filer och uppdatera om GoodReads uppdaterar
  - Alla filer; endast första import - Skriv taggar till alla filer en gång och uppdatera inte om GoodReads uppdaterar
  - Endast för nya nedladdningar - Skriv taggar till endast nya nedladdningar när de importeras
- Uppdatera omslag - Aktivera för att tala om för Calibre Content Server att använda samma bokomslag som Readarr
- Bädda in metadata i bokfiler - Aktivera för att tala om för Calibre Content Server att skriva och bädda in metadata i bokfilerna.

## Skriv metadata till ljudfiler

Om du använder ljudböcker kommer du att använda dessa alternativ för att styra det.

- Tagga ljudfiler med metadata
  - Alla filer; håll synkroniserad med GoodReads - Skriv taggar till alla filer och uppdatera om GoodReads uppdaterar
  - Alla filer; endast första import - Skriv taggar till alla filer en gång och uppdatera inte om GoodReads uppdaterar
  - Endast för nya nedladdningar - Skriv taggar till endast nya nedladdningar när de importeras
- Rensa befintliga taggar - Aktivera för att ta bort alla taggar från filer utom de som har lagts till av Readarr

# Taggar

- Taggavsnittet i Readarr används för att länka olika aspekter av Readarr.
- Taggar är särskilt användbara för:

  - Släppprofiler
  - Indexerare
  - Importlistor

- Taggar kan användas för att länka släppprofiler, indexerare, importlistor och författare/böcker tillsammans.
- Till exempel:
  - Du vill att en specifik författare/bok endast ska använda en specifik indexerare. Du skulle skapa en tagg och tilldela författaren/boken och indexeraren den taggen.
  - Du vill att en specifik importlista endast ska använda en specifik släppprofil. Du skulle skapa en tagg och tilldela importlistan och släppprofilen den taggen.

> Det rekommenderas starkt att du lägger till en beskrivande tagg till en importlista förutom det som nämns ovan.

> Observera: Taggar påverkar inte några "Kvalitetsprofiler", "Metadataprofiler" eller någon annan aspekt som inte nämns ovan.
{.is-info}

# Allmänt

Den här sidan är för allmänna Readarr-inställningar som inte täcks i andra avsnitt.

## Värd

![genhost.png](/assets/readarr/genhost.png)

- Bindningsadress - Giltig IP4-adress eller '*' för alla gränssnitt
  - 0.0.0.0 eller `*` - alla adresser kan ansluta
  - 127.0.0.1 eller localhost - endast program på localhost kan ansluta
  - Någon annan IP (t.ex. 1.2.3.4) - endast den IP-adressen (1.2.3.4) kan ansluta
- Portnummer - Portnumret som du vill använda för att komma åt webbgränssnittet för Readarr

> Observera: Om du använder Docker ska du inte ändra den här inställningen.
{.is-warning}

- URL-bas - För stöd för omvänd proxy, standard är tomt

> Observera: Om du använder en omvänd proxy (exempel: mydomain.com/readarr) ska du ange '/readarr' för URL-bas.
{.is-info}

- Aktivera SSL - Om du har SSL-legitimationer och vill säkra kommunikationen till och från din Readarr, aktivera detta alternativ.

> Observera: Använd inte detta om du inte vet vad du gör.
{.is-warning}

## Säkerhet

![gensecurity.png](/assets/readarr/gensecurity.png)

- Autentisering - Hur vill du autentisera för att komma åt din Readarr-instans
  - Ingen - Du har ingen autentisering för att komma åt din Readarr. Vanligtvis om du är den enda användaren i ditt nätverk, inte har någon på ditt nätverk som skulle vilja komma åt din Readarr eller om din Readarr inte är exponerad för webben
  - Grundläggande (webbläsarpopup) - Detta alternativ visar en liten popup när du går till din Readarr och låter dig ange ett användarnamn och lösenord
  - Formulär (inloggningssida) - Detta alternativ har en bekant inloggningsskärm som liknar andra webbplatser för att låta dig logga in på din Readarr
- API-nyckel - Så här kommunicerar andra program eller har Readarr kommunicera med andra program. Om denna nyckel ges till fel person med åtkomst kan den göra alla möjliga saker med din bibliotek. Detta är varför API-nyckeln är maskerad i loggarna
- Certifikatvalidering - Ändra hur strikt HTTPS-certifikatvalidering är
  - Aktiverad - Validera alla HTTPS-certifikat (rekommenderas)
  - Inaktiverad för lokala adresser - Validera alla HTTPS-certifikat utom de på localhost och LAN
  - Inaktiverad - Validera inga HTTPS-certifikat

## Proxy

![genproxy.png](/assets/readarr/genproxy.png)

- Proxy - Detta alternativ låter dig köra informationen som din Radarr hämtar och söker igenom en proxy. Detta kan vara användbart om du befinner dig i ett land som inte tillåter nedladdning av torrentfiler

- Använd proxy - Aktivera för att använda en proxy
- Proxytyp - Välj din proxytyp (HTTPS, Socks4 eller Socks5)
- Värdnamn - Ange ditt proxyvärdnamn (Inkludera inte http/https eller någon annan protokoll)
- Port - Ange din proxyport
- Användarnamn - Ange ditt proxyanvändarnamn om det är tillämpligt
- Lösenord - Ange ditt proxylösenord om det är tillämpligt
- Ignorerade adresser - Ange en kommaseparerad lista över adresser som ska undantas från proxyt
- Bypass proxy för lokala adresser - Markera rutan för att undanta proxyt för lokala adresser.

## Loggning

![genlogging.png](/assets/readarr/genlogging.png)

- Loggnivå - Förmodligen ett av de mest användbara felsökningsverktygen
  - Info - Detta är det mest grundläggande sättet som Readarr samlar information på, detta kommer att inkludera mycket minimal mängd information i loggarna. Denna loggfil innehåller fatal, error, warn och info-anteckningar.
  - Debug - Debug kommer att inkludera all information som Info inkluderar plus mer information som kan vara användbar. Denna loggfil innehåller fatal, error, warn, info och debug-anteckningar
  - Trace - Den mest avancerade och detaljerade loggningen på Readarr, Trace kommer att inkludera all information som samlas in av Info och Debug och mer. Detta är den vanligaste typen av logg som kommer att begäras vid felsökning på Discord eller Reddit. Om du behöver hjälp, välj din logg till Trace och gör om uppgiften som gav dig problem för att fånga loggen. Denna loggfil innehåller fatal, error, warn, info, debug och trace-anteckningar.

## Analys

![genanalytics.png](/assets/readarr/genanalytics.png)

- Analys - Skicka anonym användnings- och felinformation till Readarrs servrar (Servarr). Detta inkluderar information om din webbläsare, vilka Readarr WebUI-sidor du använder, felrapportering samt OS- och runtime-version. Vi kommer att använda denna information för att prioritera funktioner och buggfixar.

## Uppdateringar

![genupdates.png](/assets/readarr/genupdates.png)

- (Avancerat alternativ) Gren - Detta är grenen av Readarr som du kör på.
  - [Se den här FAQ-posten för mer information](/readarr/faq#how-do-i-update-readarr)
- Automatisk - Ladda ner och installera uppdateringar automatiskt. Du kommer fortfarande att kunna installera från System: Uppdateringar. Observera: Windows-användare uppdateras alltid automatiskt.
- Mekanism - Använd Readarrs inbyggda uppdaterare eller ett skript
  - Inbyggd - Använd Readarrs egen uppdaterare
  - Skript - Låt Readarr köra uppdateringsskriptet
  - Docker - Uppdatera inte Readarr från inuti Docker, dra istället en helt ny bild med den nya uppdateringen
- Skript - Synligt endast när Mekanism är inställd på Skript - Sökväg till uppdateringsskriptet
- Uppdateringsprocess - Readarr kommer att ladda ner uppdateringsfilen, verifiera dess integritet och extrahera den till en temporär plats och anropa den valda metoden. Uppdateringsprocessen körs under samma användare som Readarr körs under, den behöver behörighet att uppdatera Readarr-filerna samt stoppa/starta Readarr.
- Inbyggd - Den inbyggda metoden kommer att säkerhetskopiera Readarr-filer och inställningar, stoppa Readarr, uppdatera installationen och starta Readarr, om ditt system inte hanterar att stoppa Readarr och försöker starta om den automatiskt kan det vara bäst att använda ett skript istället. Vid misslyckande kommer den tidigare versionen av Readarr att startas om.
- Skript - Skriptet bör hantera samma som den inbyggda uppdateraren, om du behöver hantera stopp och start av tjänster (upstart/launchd/etc) måste du göra det här.

## Säkerhetskopior

![genbackups.png](/assets/readarr/genbackups.png)

- Säkerhetskopieringsavsnittet låter dig berätta för Readarr hur du vill att den ska hantera säkerhetskopior

- Mapp - Detta låter dig välja säkerhetskopieringsplatsen. I Docker kommer du att vara begränsad till vad du tillåter att behållaren ser. Sökvägar är relativa till appdata-mappen; om det behövs kan du ange en absolut sökväg för att säkerhetskopiera utanför appdata-mappen.
- Intervall - Hur ofta vill du att Readarr ska göra en säkerhetskopia
- Behållning - Hur länge vill du att Readarr ska behålla varje säkerhetskopia. Efter att en ny säkerhetskopia har gjorts kommer den äldsta säkerhetskopian att tas bort som standard.

Som standard utförs säkerhetskopior var 7:e dag och de senaste 4 behålls.

# Användargränssnitt (UI)

Den här sidan låter dig anpassa visningsalternativen för användargränssnittet.

## Kalender

![uicalendar.png](/assets/readarr/uicalendar.png)

- Första veckodagen - Här kan du välja vilken dag du tycker ska vara den första dagen i veckan.
- Veckokolumnrubrik - Här kan du välja rubriken för kolumnerna.

## Datum

![caldates.png](/assets/readarr/caldates.png)

- Kort datumformat - Hur vill du att Readarr ska visa korta datum?
- Långt datumformat - Hur vill du att Readarr ska visa datum i långt format?
- Tidsformat - Vill du ha ett 12-timmars eller 24-timmars format?
- Visa relativa datum - Vill du att Readarr ska visa relativa (Idag/Igår/osv) eller absoluta datum?

## Stil

![calstyle.png](/assets/readarr/calstyle.png)

- Aktivera färgblindläge - Ändrad stil för att färgblinda användare ska kunna skilja färgkodad information bättre.

## Språk

![callanguage.png](/assets/readarr/callanguage.png)

- Användargränssnittsspråk - Välj språket som Radarr ska använda i applikationens användargränssnitt.