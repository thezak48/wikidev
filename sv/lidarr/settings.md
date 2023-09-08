---
title: Lidarr-inställningar
description: 
published: true
date: 2022-07-24T14:21:19.994Z
tags: lidarr, behöver-kärlek, inställningar
editor: markdown
dateCreated: 2021-06-14T21:36:07.513Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Inställningar](#inställningar)
- [Nedladdningsklienter](#nedladdningsklienter)
  - [Översikt](#översikt)
  - [Processer för nedladdningsklienter](#processer-för-nedladdningsklienter)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Nedladdningsklienter](#nedladdningsklienter-1)
    - [Stödda nedladdningsklienter](#stödda-nedladdningsklienter)
    - [Inställningar för Usenet-klient](#inställningar-för-usenet-klient)
    - [Inställningar för Torrent-klient](#inställningar-för-torrent-klient)
    - [Kompatibilitet för borttagning av nedladdning i Torrent-klient](#kompatibilitet-för-borttagning-av-nedladdning-i-torrent-klient)
  - [Hantering av slutförda nedladdningar](#hantering-av-slutförda-nedladdningar)
    - [Ta bort slutförda nedladdningar](#ta-bort-slutförda-nedladdningar)
    - [Hantering av misslyckade nedladdningar](#hantering-av-misslyckade-nedladdningar)
  - [Fjärrsökvägsmappningar](#fjärrsökvägsmappningar)
- [Importlistor](#importlistor)
  - [Importlistor](#importlistor-1)
  - [Undantag för importlistor](#undantag-för-importlistor)
  - [Lägga till en importlista](#lägga-till-en-importlista)
- [Anslutningar](#anslutningar)
- [Taggar](#taggar)
- [Allmänt](#allmänt)
  - [Uppdateringar](#uppdateringar)

# Inställningar

Den här sidan är under arbete och bidrag - baserat på andra \*Arr-sidor - är både välkomna och starkt uppmuntrade.

# Nedladdningsklienter

> Information om stödda nedladdningsklienter finns på sidan [Mer information (Stödda)](/lidarr/supported#nedladdningsklienter) för den här sektionen
{.is-info}

## Översikt

- Nedladdning och import är där de flesta människor upplever problem. På en övergripande nivå måste programvaran kunna kommunicera med din nedladdningsklient och ha åtkomst till de filer den laddar ner. Det finns ett stort antal stödda nedladdningsklienter och ännu fler olika inställningar. Det innebär att det inte finns en enda rätt inställning och att varje persons inställning kan vara lite annorlunda. Men det finns många felaktiga inställningar.

## Processer för nedladdningsklienter

## Usenet

- Lidarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Lidarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- När nedladdningen är klar kommer Lidarr att känna till den slutliga filplatsen enligt rapporterad av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp och åtkomlig av Lidarr.
- Lidarr kommer att skanna den avslutade filplatsen efter filer som Lidarr kan använda. Den kommer att analysera filnamnet för att matcha det mot den begärda medias filnamn. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den angivna medieplatsen.
- Atomiska flyttar (direkta flyttar) är aktiverade som standard. Filsystemet och monteringspunkterna måste vara desamma för din avslutade nedladdningsmapp och din mediebibliotek. Om den atomiska flytten misslyckas eller din inställning inte stöder hårddisklänkar och atomiska flyttar kommer Lidarr att backa och kopiera filen och sedan ta bort den från källan, vilket är intensivt för I/O.
- Om alternativet "Hantering av slutförda nedladdningar - Ta bort" är aktiverat i Lidarrs inställningar kommer överblivna filer från nedladdningen att skickas till papperskorgen eller återvinningen via en begäran till din klient att ta bort nedladdningen.

## BitTorrent

- Lidarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Lidarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (förhållande eller tid kan justeras i nedladdningsklienten eller från Lidarr under den specifika nedladdningsklienten). När filer importeras till din mediamapp kommer Lidarr att skapa en hårdlänk till filen om det stöds av din inställning eller kopiera om hårdlänkar inte stöds.
- Hårdlänkar är aktiverade som standard. [En hårdlänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringspunkterna måste vara desamma för din avslutade nedladdningsmapp och ditt mediebibliotek. Om skapandet av hårdlänken misslyckas eller din inställning inte stöder hårdlänkar kommer Lidarr att backa och kopiera filen.
- Om alternativet "Hantering av slutförda nedladdningar - Ta bort" är aktiverat i Lidarrs inställningar kommer Lidarr att ta bort torrenten från din klient och be klienten att ta bort torrentdata, men endast om klienten rapporterar att seedningen är klar och torrenten är stoppad (pausad vid slutförandet).

## Nedladdningsklienter

Klicka på `Inställningar => Nedladdningsklienter` och klicka sedan på <kb>+</kb> för att lägga till en ny nedladdningsklient. Din nedladdningsklient bör redan vara konfigurerad och igång.

### Stödda nedladdningsklienter

- En lista över stödda nedladdningsklienter finns på sidan [Mer information (Stödda)](/lidarr/supported#nedladdningsklienter) för den här sektionen

Välj nedladdningsklienten du vill lägga till, och det kommer att visas en popup-ruta för att ange anslutningsdetaljer. Dessa detaljer är liknande för de flesta klienter. Vissa kommer att be om ett användarnamn eller lösenord, vissa kommer att fråga om du vill lägga till nya nedladdningar i ett pausat/startat tillstånd, etc.

### Inställningar för Usenet-klient

- Namn - Namnet på nedladdningsklienten inom Lidarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en för din nedladdningsklient
- Port - Porten för din nedladdningsklient
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- (Avancerad inställning) URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxys.
- API-nyckel - API-nyckeln för att autentisera mot din klient
- Användarnamn - Användarnamnet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Lösenord - Lösenordet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Kategori - Kategorin inom din nedladdningsklient som \*Arr kommer att använda. För att undvika orelaterade nedladdningar som visas i Aktivitet rekommenderas det starkt att ange en kategori.
- Prioritet för nyligen släppt media - Nedladdningsklientens prioritet för nyligen släppt media
- Prioritet för äldre media - Nedladdningsklientens prioritet för media som inte släpptes nyligen
- (Avancerad inställning) Klientprioritet - Prioritet för nedladdningsklienten. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet. 1 är högsta prioritet och 50 är lägsta prioritet

### Inställningar för Torrent-klient

- Namn - Namnet på nedladdningsklienten inom Lidarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en för din nedladdningsklient
- Port - Porten för din nedladdningsklient; detta är vanligtvis webgui-porten
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- (Avancerad inställning) URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxys.
- Användarnamn - Användarnamnet för att autentisera mot din klient
- Lösenord - Lösenordet för att autentisera mot din klient
- Kategori - Kategorin inom din nedladdningsklient som \*Arr kommer att använda. För att undvika orelaterade nedladdningar som visas i Aktivitet rekommenderas det starkt att ange en kategori.
- Kategori efter import - Kategorin att ställa in efter att släppet har laddats ner och importerats. Observera att detta bryter mot borttagning av hantering av slutförda nedladdningar.
- Prioritet för nyligen släppt media - Nedladdningsklientens prioritet för nyligen släppt media
- Prioritet för äldre media - Nedladdningsklientens prioritet för media som inte släpptes nyligen
- Initialt tillstånd - Inledande tillstånd för torrents (endast Qbittorrent: Tvingar förbigåelse av alla seed-trösklar)
- (Avancerad inställning) - Prioritet för nedladdningsklienten. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet. 1 är högsta prioritet och 50 är lägsta prioritet

### Kompatibilitet för borttagning av nedladdning i Torrent-klient

- Lidarr kan bara ställa in seed-förhållandet/tiden på klienter som stöder att ställa in detta värde via deras API när torrenten läggs till. Seed-mål kan ställas in globalt i klienten själv eller per spårare i \*Arr-inställningar för varje indexerare. Se tabellen nedan för klientkompatibilitet.

|      Klient       |                                Förhållande                                 |                                   Tid                                   |
| :---------------: | :-----------------------------------------------------------------------: | :----------------------------------------------------------------------: |
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

> ![Idle Limit](https://img.shields.io/badge/Stöds-Idle%20Limit*-blue) - Transmission har internt en kontroll för inaktiv tid, men Lidarr jämför den med seedningstiden om inaktivitetsgränsen är inställd för varje torrent. Detta görs som en lösning på Transmission API:s begränsningar.{.is-info}

## Hantering av slutförda nedladdningar

- Hantering av slutförda nedladdningar är hur Lidarr importerar media från din nedladdningsklient till dina seriemappar.

- Aktivera (Avancerad global inställning) - Importera automatiskt slutförda nedladdningar från nedladdningsklienten
- Ta bort (Inställning per klient) - Ta bort slutförda nedladdningar när de är klara (usenet) eller stoppade/slutförda (torrenter)
  - För torrenter krävs att din nedladdningsklient pausar när seed-målen nås. Det kräver också att seed-målen stöds av Lidarr enligt tabellen ovan. Torrenter måste också vara i samma kategori.

### Ta bort slutförda nedladdningar

- Lidarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
- Lidarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- När nedladdningen är klar kommer Lidarr att känna till den slutliga filplatsen enligt rapporterad av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp.
- Lidarr kommer att skanna den avslutade filplatsen efter videofiler. Den kommer att analysera videofilens namn för att matcha den med en episod. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den tilldelade biblioteksmappen.
- Överblivna filer från nedladdningen kommer att skickas till papperskorgen eller återvinningen.

Om du laddar ner med en BitTorrent-klient är processen något annorlunda:

- Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda. När filer importeras till din tilldelade biblioteksmapp kommer Lidarr att försöka skapa en hårdlänk till filen eller backa och kopiera (använda dubbel plats) om hårdlänkar inte stöds.
- Om alternativet "Hantering av slutförda nedladdningar - Ta bort" är aktiverat i inställningarna kommer Lidarr att be torrentklienten att ta bort den ursprungliga filen och torrenten, men detta kommer bara att ske om klienten rapporterar att seedningen är klar, torrenten är i samma kategori (dvs. inte använder en kategori efter import), seed-målet som nåtts stöds av Lidarr och torrenten är pausad (stoppad).

### Hantering av misslyckade nedladdningar

- Hantering av misslyckade nedladdningar är endast kompatibel med SABnzbd och NZBGet.
- Hantering av misslyckade nedladdningar gäller inte för Torrenter och det finns inga planer på att lägga till en sådan funktion.

- Det finns flera komponenter som utgör processen för hantering av misslyckade nedladdningar:

- Kontrollera nedladdare:
  - Kö - Kontrollera din nedladdares kö för lösenordsskyddade (krypterade) släpp som är markerade som misslyckade
  - Historik - Kontrollera din nedladdares historik för misslyckanden (t.ex. inte tillräckligt med block för reparation eller extrahering misslyckades)
- När Lidarr hittar en misslyckad nedladdning börjar den bearbeta dem och gör några saker:
  - Lägger till en misslyckad händelse i Lidarrs historik
  - Tar bort den misslyckade nedladdningen från nedladdningsklienten för att frigöra utrymme och rensa nedladdade filer (valfritt)
  - Börjar söka efter en ersättningsfil (valfritt)
  - Blocklistning (tidigare "Blacklisting") gör att nzbs automatiskt hoppas över när de misslyckas, vilket innebär att den nzb aldrig kommer att laddas ner automatiskt av Lidarr igen (du kan fortfarande tvinga nedladdningen via en manuell sökning).
  - Det finns 2 avancerade alternativ (på sidan "Nedladdningsklientens" inställningar) som styr beteendet för misslyckade nedladdningar i Lidarr, för närvarande är de alla aktiverade som standard.

- Ladda ner igen - Styr om Lidarr ska söka efter samma fil efter ett misslyckande
- (Avancerat alternativ) Ta bort - Om nedladdningen automatiskt ska tas bort från nedladdningsklienten när misslyckandet upptäcks

## Fjärrsökvägsmappningar

- Fjärrsökvägsmappning fungerar som en enkel sökning efter fjärrsökväg och ersättning med lokal sökväg. Detta används främst för antingen sammanslagna lokala/fjärrinställningar med mergerfs eller liknande, eller används när applikationen och nedladdningsklienten inte är på samma server.
- En fjärrsökvägsmappning används när din nedladdningsklient rapporterar en sökväg för slutförda data antingen på en annan server eller på ett sätt som \*Arr inte adresserar den mappen.
- I allmänhet krävs en fjärrsökvägsmappning endast om din nedladdningsklient körs på Linux när \*Arr körs på Windows eller vice versa. En fjärrsökvägsmappning kan också behövas om du blandar Docker- och nativa klienter eller om du använder en fjärrserver.
- En fjärrsökvägsmappning är en ENKEL sökning/ersättning (där den hittar VÄRDET FÖR FJÄRRSÖKVÄGEN, ersätter det med VÄRDET FÖR LOKAL SÖKVÄG för den angivna Värden).
- Om felmeddelandet om en ogiltig sökväg inte innehåller VÄRDET SOM ERSATTS, fungerar inte sökvägsmappningen som du förväntar dig. Den vanliga lösningen är att lägga till och ta bort mappningen.
- [Se TRaSH:s handledning för ytterligare information om fjärrsökvägsmappning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Om både \*Arr och din nedladdningsklient är Docker-containrar behövs sällan en fjärrsökvägsmappning. Det rekommenderas att du [granskar Docker-guiden](/docker-guide) och/eller [följer TRaSH's handledning](https://trash-guides.info/hardlinks)
{.is-info}

# Importlistor

> Information om stödda listtyper finns på sidan [Mer information (Stödda)](/lidarr/supported#lists) för den här sektionen
{.is-info}

Importlistor gör det möjligt att lägga till objekt i Lidarr från Spotify eller Last.fm. Detta kan potentiellt lägga till många oväntade objekt i din Lidarr-databas, så använd det med försiktighet.

<!-- ![importlists.png](/assets/readarr/importlists.png) -->

## Importlistor

Här visas de listor du för närvarande har och du kan lägga till nya listor. Hur du lägger till listor täcks mer detaljerat nedan.

## Importlistexkluderingar

Allt som finns här har exkluderats från att läggas till av listor och kommer aldrig att läggas till från någon lista. Du kan ta bort objekt från listan genom att klicka på dem.

## Lägga till en importlista

Efter att ha klickat på <kb>+</kb>, välj vilken typ av lista du vill lägga till:

<!-- ![addlist.png](/assets/readarr/addlist.png) -->

I det här fallet kommer vi att lägga till en Spotify Sparade Album-lista.

<!-- ![bookshelflist.png](/assets/readarr/bookshelflist.png) -->

- Namn - Ange ett namn för denna lista.
- Aktivera automatiskt tillägg - Om aktiverat kommer allt på listan automatiskt att läggas till i Lidarr.

> Detta kommer att lägga till ALLA ALBUM från den artisten i Lidarr!

- Övervaka - Välj din övervakningsnivå för tillagda objekt. Giltiga alternativ är `Inget`, `Specifikt album` och `Alla artistalbum`. Alla album läggs till i Lidarr, men kommer att övervakas eller inte övervakas baserat på detta val.
- Rotmapp - Välj rotmappen för artister som läggs till från denna lista.
- Övervaka nya album - Välj vad Lidarr ska göra med framtida album från den tillagda artisten. Giltiga alternativ är `Alla album`, `Inget`, `Nya`.
- Kvalitetsprofil - Välj din kvalitetsprofil för artister som läggs till från denna lista.
- Metadataprofil - Välj din metadataprofil för artister som läggs till från denna lista.
- Lidarr-taggar - Välj vilka taggar som gäller för artister som läggs till från denna lista.

> Det rekommenderas starkt att du lägger till en beskrivande tagg här. Annars kommer du inte att veta vilken lista som lade till dessa objekt i Lidarr, och när de väl är tillagda kan du aldrig få denna information igen! Denna information loggas inte!

Listor synkroniseras som standard var 24:e timme, men kan utlösas manuellt från sidan `System` => `Uppgifter`. Du kan inte automatisera denna process snabbare än så.

# Anslutningar

> Information om stödda anslutningstyper finns på sidan [Mer information (Stödda)](/lidarr/supported#notifications) för den här sektionen
{.is-info}

# Taggar

- Taggsektionen i Lidarr används för att koppla samman olika aspekter av Lidarr.
- Taggar är särskilt användbara för:

  - Fördröjningsprofiler
  - Utgivningsprofiler
  - Indexerare

- Taggar kan användas för att koppla samman Fördröjningsprofiler, Utgivningsprofiler, Indexerare och Artister/Album.
- Till exempel:
  - Du vill att en specifik Artist/Album endast ska använda en specifik indexerare. Du skulle skapa en tagg och tilldela Artist/Album och indexeraren den taggen.
  - Du vill att en specifik Utgivningsprofil endast ska använda en specifik Fördröjningsprofil. Du skulle skapa en tagg och tilldela Utgivningsprofilen och Fördröjningsprofilen den taggen.

> Observera: Taggar påverkar inte några "Kvalitetsprofiler", "Metadataprofiler" eller någon annan aspekt som inte nämns ovan.
{.is-info}

# Allmänt

## Uppdateringar

- (Avancerad inställning) Gren - Detta är grenen av Lidarr som du kör på.
  - [Se denna FAQ-post för mer information](/lidarr/faq#how-do-i-update-lidarr)
- Automatisk - Ladda ner och installera uppdateringar automatiskt. Du kommer fortfarande att kunna installera från System: Uppdateringar. Observera: Windows-användare uppdateras alltid automatiskt.
- Mekanism - Använd Lidarrs inbyggda uppdaterare eller ett skript
  - Inbyggd - Använd Lidarrs egna uppdaterare
  - Skript - Låt Lidarr köra uppdateringsskriptet
  - Docker - Uppdatera inte Lidarr inifrån Docker, dra istället en helt ny bild med den nya uppdateringen
- Skript - Synlig endast när Mekanism är inställd på Skript - Sökväg till uppdateringsskriptet
- Uppdateringsprocess - Lidarr kommer att ladda ner uppdateringsfilen, verifiera dess integritet och extrahera den till en temporär plats och anropa den valda metoden. Uppdateringsprocessen körs under samma användare som Lidarr körs under, den behöver behörighet att uppdatera Lidarr-filerna samt att starta/stoppa Lidarr.
- Inbyggd - Den inbyggda metoden kommer att säkerhetskopiera Lidarr-filer och inställningar, stoppa Lidarr, uppdatera installationen och starta Lidarr igen. Om ditt system inte klarar av att stoppa Lidarr och försöker starta om det automatiskt kan det vara bäst att använda ett skript istället. Vid misslyckande kommer den tidigare versionen av Lidarr att startas om.
- Skript - Skriptet bör hantera samma saker som den inbyggda uppdateraren, om du behöver hantera stopp och start av tjänster (upstart/launchd/etc) måste du göra det här.