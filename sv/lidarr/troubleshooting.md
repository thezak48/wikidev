---
title: Lidarr Felsökning
description: 
published: true
date: 2023-07-24T19:53:24.970Z
tags: lidarr, behöver-kärlek, felsökning
editor: markdown
dateCreated: 2021-06-14T21:36:46.193Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Be om hjälp](#be-om-hjälp)
- [Loggning och loggfiler](#loggning-och-loggfiler)
  - [Standardplats för loggar](#standardplats-för-loggar)
  - [Plats för uppdateringsloggar](#plats-för-uppdateringsloggar)
  - [Dela loggar](#dela-loggar)
  - [Spår-/felsökningsloggar](#spår-felsökningsloggar)
  - [Rensa loggar](#rensa-loggar)
- [Flera loggfiler](#flera-loggfiler)
- [Återställning efter misslyckad uppdatering](#återställning-efter-misslyckad-uppdatering)
  - [Identifiera problemet](#identifiera-problemet)
    - [Migrationsproblem](#migrationsproblem)
    - [Behörighetsproblem](#behörighetsproblem)
  - [Lös problemet](#lös-problemet)
    - [Behörighetsproblem](#behörighetsproblem)
    - [Uppgradera manuellt](#uppgradera-manuellt)
- [Nedladdningar och importering](#nedladdningar-och-importering)
  - [Testa nedladdningsklienten](#testa-nedladdningsklienten)
  - [Testa en nedladdning](#testa-en-nedladdning)
  - [Testa en importering](#testa-en-importering)
  - [Vanliga problem](#vanliga-problem)
    - [Nedladdningsklientens webbgränssnitt är inte aktiverat](#nedladdningsklientens-webbgränssnitt-är-inte-aktiverat)
    - [SSL används och är felkonfigurerat](#ssl-används-och-är-felkonfigurerat)
    - [Kan inte se delning på Windows](#kan-inte-se-delning-på-windows)
    - [Kartlagda nätverksenheter är inte tillförlitliga](#kartlagda-nätverksenheter-är-inte-tillförlitliga)
    - [Docker och användare, grupp, ägande, behörigheter och sökvägar](#docker-och-användare-grupp-ägande-behörigheter-och-sökvägar)
    - [Fjärrsökvägsmappning](#fjärrsökvägsmappning)
      - [Fjärrmontering eller fjärrsynkronisering (Syncthing)](#fjärrmontering-eller-fjärrsynkronisering-syncthing)
    - [Behörigheter för biblioteksmappen](#behörigheter-för-biblioteksmappen)
    - [Behörigheter för nedladdningsmappen](#behörigheter-för-nedladdningsmappen)
    - [Nedladdningsmappen och biblioteksmappen är inte olika mappar](#nedladdningsmappen-och-biblioteksmappen-är-inte-olika-mappar)
    - [Felaktig kategori](#felaktig-kategori)
    - [Packade torrents](#packade-torrents)
    - [Upprepade nedladdningar](#upprepade-nedladdningar)
    - [Usenet-nedladdning missar importering](#usenet-nedladdning-missar-importering)
    - [Nedladdningsklient rensar objekt](#nedladdningsklient-rensar-objekt)
    - [Nedladdningen kan inte matchas med ett biblioteksobjekt](#nedladdningen-kan-inte-matchas-med-ett-biblioteksobjekt)
    - [Anslutningstidsgräns överskriden](#anslutningstidsgräns-överskriden)
  - [Problem som inte listas](#problem-som-inte-listas)
- [Sökningar, indexer och spårare](#sökningar-indexer-och-spårare)
  - [Öka loggningsnivån till spårning](#öka-loggningsnivån-till-spårning)
  - [Testa en indexer eller spårare](#testa-en-indexer-eller-spårare)
  - [Testa en sökning](#testa-en-sökning)
  - [Vanliga problem](#vanliga-problem-1)
    - [Media är oövervakad](#media-är-oövervakad)
    - [Spårare behöver RawSearch-funktioner](#spårare-behöver-rawsearch-funktioner)
    - [Felaktiga kategorier](#felaktiga-kategorier)
    - [Felaktiga resultat](#felaktiga-resultat)
    - [Framgångsrik förfrågan - Inga resultat returnerade](#framgångsrik-förfrågan-inga-resultat-returnerade)
    - [Saknade resultat](#saknade-resultat)
    - [Certifikatvalidering](#certifikatvalidering)
    - [Träffar begränsningar](#träffar-begränsningar)
    - [IP-blockering](#ip-blockering)
    - [Användning av Jackett /all-slutpunkt](#användning-av-jackett-all-slutpunkt)
    - [Användning av NZBHydra2 som enskild post](#användning-av-nzbhydra2-som-enskild-post)
    - [Problem som inte listas](#problem-som-inte-listas-1)
  - [Fel](#fel)
    - [Det underliggande anslutningen stängdes: Ett oväntat fel inträffade vid en sändning](#det-underliggande-anslutningen-stängdes-ett-oväntat-fel-inträffade-vid-en-sändning)
    - [Begäran tog för lång tid](#begäran-tog-för-lång-tid)
    - [Problem som inte listas](#problem-som-inte-listas-2)

# Be om hjälp

Behöver du hjälp? Det är okej, alla behöver hjälp ibland. Du kan få hjälp i realtid via chatt på

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiell Lidarr Discord*](https://lidarr.audio/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiell Lidarr Subreddit*](https://reddit.com/r/lidarr)
{.links-list}

Men innan du går dit och postar, se till att din hjälpförfrågan är så bra som möjligt. Beskriv tydligt problemet och beskriv kortfattat din konfiguration, inklusive saker som ditt operativsystem/distribution, version av .NET, version av Lidarr, nedladdningsklient och dess version. **Om du använder [Docker](https://www.docker.com/) ska du gå igenom [Docker Guide](/docker-guide) först eftersom det kommer att lösa vanliga och frekventa problem med sökvägar/behörigheter. Annars se till att du har en [docker compose](/docker-guide#docker-compose) till hands. [Så här genererar du en Docker Compose](https://trash-guides.info/compose)** Berätta om vad du redan har försökt, vad du har tittat på. Använd avsnittet [Loggning och loggfiler](#loggning-och-loggfiler) för att öka loggningsnivån till spårning, återskapa problemet, ladda upp den relevanta kontexten på en pastebin och inkludera en länk till den i ditt inlägg. Kanske till och med inkludera några skärmbilder för att markera problemet.

Ju mer vi vet, desto lättare är det att hjälpa dig.

# Loggning och loggfiler

Det kan vara fördelaktigt att också granska vanliga felsökningsproblem:
- [Vanliga problem med nedladdningar och importering](#vanliga-problem)
- [Vanliga problem med sökningar, indexer och spårare](#vanliga-problem-1)
{.links-list}

Om du ombeds att skicka felsökningsloggar kommer dina loggar att innehålla `debug` och om du ombeds att skicka spårningsloggar kommer dina loggar att innehålla `trace`. Om de loggar du tillhandahåller inte innehåller något av dessa, är de inte de begärda loggarna.

- Undvik att dela hela loggfilen om du inte ombeds att göra det.
- Ladda inte upp loggar direkt till Discord eller klistra in dem som väggar av text, om du inte ombeds att göra det.
- Dela inte loggarna som en bilaga, en zip-fil eller något annat än text som delas via de tjänster som anges nedan.

För att tillhandahålla bra och användbara loggar för delning:

> Se till att en spamig uppgift INTE körs, till exempel en RSS-uppdatering
{.is-warning}

1. [Öka loggningsnivån till spårning (Inställningar => Allmänt => Loggningsnivå eller Redigera konfigurationsfilen)](#spår-felsökningsloggar)
2. [Rensa loggar (System => Loggar => Rensa loggar eller Radera alla loggar i loggmappen)](#rensa-loggar)
3. Återskapa problemet (Gör om det som orsakar problem)
4. [Öppna spårningsloggfilen (Lidarr.trace.txt) via gränssnittet eller loggfilen](#standardplats-för-loggar) på filsystemet och hitta den relevanta kontexten
5. Kopiera en stor del före problemet, själva problemet och en stor del efter problemet.
6. Använd [Gist](https://gist.github.com/), [0bin (**Se till att inaktivera färgläggning**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntus Pastebin](https://pastebin.ubuntu.com/) eller liknande webbplatser - undvik de som anges nedan - för att dela de kopierade loggarna ovan

**Varningar:**
- **Använd inte [pastebin.com](https://pastebin.com) eftersom deras filter har en tendens att blockera loggarna.
- Använd inte [pastebin.pl](https://pastebin.pl) eftersom deras webbplats ofta inte är tillgänglig.
- Använd inte [JustPasteIt](https://justpaste.it/) eftersom deras webbplats inte underlättar granskning av loggar.
- Ladda inte upp din logg som en fil.
- Ladda inte upp och dela dina loggar via Google Drive, Dropbox eller någon annan webbplats som inte anges ovan.
- Arkivera inte (zip, tar (tarball), 7zip, etc.) dina loggar.
- Dela inte konsolresultat, utdata från Docker-container eller något annat än de angivna applikationsloggarna.

**Viktig anteckning:**
- När du använder [0bin](https://0bin.net/), se till att inaktivera färgläggning och bränn inte efter att ha läst.

- Alternativt, om du letar efter en specifik post i en gammal loggfil men inte är säker på vilken, kan du använda N++. Du kan använda Notepad++ "Sök i filer"-funktion för att söka i gamla loggfiler vid behov.
- **Endast Unix:** Alternativt, om du letar efter en specifik post i en gammal loggfil men inte är säker på vilken, kan du använda grep. Till exempel, om du vill hitta information om filmen/serien/boken/låten/indexeraren "Shooter" kan du köra följande kommando `grep -inr -C 100 -e 'Shooter' /sökväg/till/loggar/*.trace*.txt` Om din [Appdata-katalog](/lidarr/appdata-directory) finns i din hemkatalog skulle du köra: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flaggor har följande funktioner
    * -i: ignorera skiftläge
    * -n: visa radnummer
    * -r: sök rekursivt i alla filer i sökvägen
    * -C: ange antal rader före och efter den hittade raden
    * -e: mönstret att söka efter

```

## Standardplats för loggar

Loggfilerna finns i Lidarrs [Appdata-katalog](/lidarr/appdata-directory), i mappen logs/. Du kan också komma åt loggfilerna från gränssnittet under System => Loggar => Filer.

> Observera: Loggarna ("Händelser") i gränssnittet är inte samma som loggfilerna och är inte lika användbara. Om du ombeds att skicka loggar, kopiera/klistra in från loggfilerna och inte från tabellen.
{.is-info}

## Plats för uppdateringsloggar

Uppdateringsloggarna finns i Lidarrs [Appdata-katalog](/lidarr/appdata-directory), i mappen UpdateLogs/.

## Dela loggar

Loggarna kan vara långa och svåra att läsa som en del av ett forum- eller Reddit-inlägg och de är spamiga i Discord, så använd [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller någon annan liknande pastebin-webbplats. Hela filen behövs vanligtvis inte, bara en bra mängd kontext före och efter problemet/felmeddelandet. Glöm inte att vänta på att spamiga uppgifter som en RSS-synkronisering eller biblioteksuppdatering ska slutföras.

## Spår-/felsökningsloggar

Du kan ändra loggningsnivån under Inställningar => Allmänt => Loggning. Lidarr behöver inte startas om för att ändringen ska träda i kraft. De senaste felsöknings-/spårningsloggfilerna heter `lidarr.debug.txt` respektive `lidarr.trace.txt`.

Om du inte kan komma åt gränssnittet för att ställa in loggningsnivån kan du göra det genom att redigera config.xml i AppData-katalogen och ändra värdet för LogLevel till Debug eller Trace istället för Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Rensa loggar

Du kan rensa loggfilerna och loggdatabasen direkt från gränssnittet, under System => Loggar => Filer och System => Loggar => Radera (Papperskorgsikonen)

# Flera loggfiler

Lidarr använder rullande loggfiler som är begränsade till 1 MB vardera. Den aktuella loggfilen är alltid `lidarr.txt`, för de andra filerna är `.0.txt` den näst nyaste (ju högre nummer desto äldre är den). Denna loggfil innehåller `fatal`, `error`, `warn` och `info`-poster.

När felsökningsloggnivån är aktiverad kommer det att finnas ytterligare rullande loggfiler `lidarr.debug.txt`. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info` och `debug`-poster. De täcker vanligtvis en period på 40 timmar.

När spårningsloggnivån är aktiverad kommer det att finnas ytterligare rullande loggfiler `lidarr.trace.txt`. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info`, `debug` och `trace`-poster. På grund av spårningsvolymen täcker de bara ett par timmar som mest.

# Återställning efter misslyckad uppdatering

Vi gör allt vi kan för att förhindra problem vid uppgradering, men om de ändå uppstår kommer detta att guida dig genom stegen för att återställa din installation.

## Identifiera problemet

- Det bästa stället att titta när programmet inte startar efter en uppdatering är att granska [uppdateringsloggarna](#plats-för-uppdateringsloggar) och se om uppdateringen slutfördes framgångsrikt. Om det inte finns något problem där är nästa steg att titta på dina vanliga programloggfiler, innan du försöker starta igen, använd [Loggning](/lidarr/settings#logging) och [Loggfiler](/lidarr/system#log-files) för att hitta dem och öka loggningsnivån.
- Det vanligaste problemet är att systemet där appen är installerad har manipulerat `/tmp`-katalogen och raderat kritiska \*Arr-filer under uppdateringen, vilket orsakar att både uppdateringen och återställningen misslyckas. I det här fallet installerar du helt enkelt om över den befintliga trasiga installationen.

### Migrationsproblem

- Migrationsfel kommer inte att vara identiska, men här är ett exempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Behörighetsproblem

- Behörighetsproblem beror på att programmet inte kan komma åt de relevanta tillfälliga mapparna och/eller appens binära mapp. Åtgärda behörigheterna så att användaren/gruppen som programmet körs som har lämplig åtkomst.

- Synology-användare kan stöta på detta Synology-fel `Access to the path '/proc/{some number}/maps is denied`

- Synology-användare kan också stöta på att det inte finns tillräckligt med utrymme i `/tmp` på vissa NAS-enheter. Du måste ange en annan sökväg för `/tmp` för appen. Se SynoCommunity eller andra Synology-supportkanaler för hjälp med detta.

## Lös problemet

Vid migrationsproblem kan du inte göra mycket direkt, om problemet är specifikt för dig (eller om det ännu inte finns några inlägg), skapa då en post på [vår subreddit](https://reddit.com/r/lidarr) eller besök vår [discord](https://lidarr.audio/discord), om det finns andra med samma problem kan du vara säker på att vi arbetar med det.

> Se till att du inte försökte använda en databas från `nightly`-versionen i den stabila versionen. Att byta grenar är inte rekommenderat.{.is-info}

### Behörighetsproblem

- Åtgärda behörigheterna för att se till att användaren/gruppen som programmet körs som kan komma åt (läsa och skriva) både `/tmp` och installationsmappen för programmet.

- För Synology-användare som upplever problem med `/proc/###/maps` kommer att stoppa Sonarr eller de andra \*Arr-applikationerna och uppdatera ska lösa detta. Detta är ett problem med SynoCommunity-paketet.

### Uppgradera manuellt

Hämta den senaste versionen från vår webbplats.

Installera uppdateringen (.exe) eller extrahera (.zip) innehållet över din befintliga installation och kör Lidarr som vanligt.

# Nedladdningar och import

Nedladdning och import är där *de flesta* människor upplever problem. Ur ett övergripande perspektiv behöver Lidarr kunna kommunicera med din nedladdningsklient och ha åtkomst till de filer den laddar ner. Det finns en stor variation av stödda nedladdningsklienter och ännu *större* variation av inställningar. Detta innebär att medan det finns några *vanliga* inställningar, finns det ingen *rätt* inställning och varje persons inställning kan vara lite annorlunda.

> **Det första steget är att öka loggningsnivån till Trace, se [Loggning och loggfiler](#loggning-och-loggfiler) för detaljer om hur du justerar loggningen och söker i loggarna. Du kommer sedan att återskapa problemet och använda loggarna med trace-nivå från den tidsramen för att undersöka problemet.** Om någon hjälper dig, lägg kontexten från före/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller liknande webbplats för att visa dem. Det behöver inte vara hela filen och det bör inte *bara* vara felet. Du bör också återskapa problemet när uppgifter som spamar loggfilen inte körs.
{.is-danger}

När du söker hjälp, se till att läsa [begära hjälp](#begära-hjälp) så att du kan ge oss de detaljer vi behöver.

## Testa nedladdningsklienten

Se till att din nedladdningsklient(er) körs. Börja med att testa nedladdningsklienten, om den inte fungerar kan du se detaljer i loggarna med trace-nivå. Du bör hitta en URL som du kan ange i din webbläsare och se om den fungerar. Det kan vara ett anslutningsproblem, vilket kan indikera en felaktig IP-adress, värdnamn, port eller till och med en brandvägg som blockerar åtkomsten. Det kan vara uppenbart, som ett autentiseringsproblem där du har angett användarnamn, lösenord eller API-nyckel felaktigt.

## Testa en nedladdning

Nu ska vi prova en nedladdning, välj en låt och gör en manuell sökning. Välj en av dessa filer och försök ladda ner den. Skickas den till nedladdningsklienten? Hamnar den i rätt kategori? Visas den i Aktivitet? Hamnar den i loggarna med trace-nivå under uppgifterna **Kontrollera färdig nedladdning** (Uppdatera övervakade nedladdningar och Bearbeta övervakade nedladdningar-uppgifter) som körs ungefär varje minut? Blir den korrekt tolkad under den uppgiften? Har den nedladdning som köats upp ett rimligt namn? Eftersom sökningar görs med id på vissa indexerare/spårare kan den köa upp en med ett namn som den inte kan känna igen.

## Testa en import

Importproblem bör nästan alltid visas som ett objekt i Aktivitet med en orange ikon som du kan hovra över för att se felet. Om de inte visas i Aktivitet är detta problemet du behöver fokusera på först, så gå tillbaka och ta reda på det. De flesta importfel beror på *behörighets*problem, kom ihåg att måste kunna läsa och skriva i nedladdningsmappen. Ibland kan behörigheter i biblioteksmappen också vara felaktiga, så se till att kontrollera båda.

Felaktiga sökvägsproblem är också möjliga, men mindre vanliga i normala inställningar. Nyckeln för att förstå sökvägsproblem är att veta att får sökvägen till nedladdningen *från* nedladdningsklienten, via dess API. Detta blir ett problem i mer unika användningsfall, som när nedladdningsklienten körs på en annan system (kanske till och med ett annat operativsystem\!). Det kan också inträffa i en Docker-inställning när volymer inte är korrekt konfigurerade. En fjärrsökvägsmappning är en bra lösning när du inte har kontroll, som en seedbox-inställning. I en Docker-inställning är det bättre att fixa sökvägarna.

## Vanliga problem

Här är några vanliga problem.

### Nedladdningsklientens webbgränssnitt är inte aktiverat

Lidarr kommunicerar med din nedladdningsklient via dess API och får åtkomst till den via klientens webbgränssnitt. Du måste se till att nedladdningsklientens webbgränssnitt är aktiverat och att porten den använder inte konflikterar med några andra klientportar som används eller portar som används på ditt system.

### SSL används och är felaktigt konfigurerat

Se till att SSL-kryptering inte är aktiverat om du använder både din instans och din nedladdningsklient i ett lokalt nätverk. Se [SSL FAQ-posten](/lidarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) för mer information.

### Kan inte se delade resurser på Windows

Standardanvändaren för en Windows-tjänst är `LocalService`, vilket vanligtvis inte har åtkomst till dina delade resurser. Redigera tjänsten och ställ in den så att den körs som din egen användare, se FAQ-posten [varför kan jag inte se mina filer på en fjärrserver](/lidarr/faq#why-cant-see-my-files-on-a-remote-server) för detaljer.

### Kartlagda nätverksenheter är inte tillförlitliga

Även om kartlagda nätverksenheter som `X:\` är bekväma, är de inte lika tillförlitliga som UNC-sökvägar som `\\server\share` och de är inte heller tillgängliga före inloggning. Konfigurera din nedladdningsklient (er) så att de använder UNC-sökvägar vid behov. Om ditt bibliotek finns på en delad resurs, se till att dina rotmappar använder UNC-sökvägar. Om din nedladdningsklient skickar till en delad resurs är det där du behöver konfigurera UNC-sökvägar eftersom får nedladdningsvägen från nedladdningsklienten. Det är okej att behålla dina kartlagda nätverksenheter för egen användning, använd dem bara inte för automation.

### Docker och användare, grupp, ägande, behörigheter och sökvägar

Docker lägger till ett ytterligare lager av komplexitet som är lätt att göra fel, men ändå få en inställning som fungerar, men har olika problem. Istället för att gå igenom dem här, läs den här wiki-artikeln [för dessa automatiseringsprogram och Docker](/docker-guide) som handlar om användare, grupp, ägande, behörigheter och sökvägar. Den är inte specifik för något Docker-system, istället går den igenom saker på en övergripande nivå så att du kan implementera dem i din egen miljö.

### Fjärrsökvägsmappning

Om du har Lidarr i Docker och nedladdningsklienten i icke-Docker (eller vice versa) eller har programmen på olika servrar kan du behöva en fjärrsökvägsmappning.

Loggarna kommer att se ut så här

```none
2022-02-03 14:03:54.3|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /volume3/data/torrents/music/Five Finger Death Punch - F8 (2020) FLAC. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Således finns inte `/volume3/data` inom Lidarrs behållare eller är inte åtkomlig.

- [Inställningar => Nedladdningsklienter => Fjärrsökvägsmappningar](/lidarr/settings#remote-path-mappings)
- En fjärrsökvägsmappning används när din nedladdningsklient rapporterar en sökväg för slutförda data antingen på en annan server eller på ett sätt som \*Arr inte hanterar den mappen.
- I allmänhet krävs en fjärrsökvägsmappning endast om din nedladdningsklient körs på Linux när \*Arr körs på Windows eller vice versa. En fjärrsökvägsmappning kan också behövas om du blandar Docker- och nativa klienter eller om du använder en fjärrserver.
- En fjärrsökvägsmappning är en DUMB-sökning/ersättning (där den hittar det FJÄRR-värdet, ersätter det med det LOKALA värdet för den angivna värden).
- Om felmeddelandet om en felaktig sökväg inte innehåller det ERSATTADE värdet fungerar inte sökvägsmappningen som du förväntar dig. Den vanliga lösningen är att lägga till och ta bort mappningen.
- [Se TRaSH's handledning för ytterligare information om fjärrsökvägsmappning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Om både \*Arr och din nedladdningsklient är Docker-behållare behövs sällan en fjärrsökvägsmappning. Det rekommenderas att du [granskar Docker-guiden](/docker-guide) och/eller [följer TRaSH's handledning](https://trash-guides.info/hardlinks)
{.is-info}

#### Fjärrmontering eller fjärrsynkronisering (Syncthing)

- Du behöver att den synkroniseras hela tiden medan den laddar ner. Och du behöver att den lokala synkroniseringsdestinationen kan vara hårda länkar när \*Arr importerar, vilket innebär samma filsystem och ser ut som det.
  - Synkronisera till en lägre, gemensam mapp som innehåller både ofullständiga och kompletta filer.
  - Synkronisera till en plats som är på samma filsystem lokalt som ditt bibliotek och ser ut som det (Docker och nätverksdelningar gör det lätt att konfigurera felaktigt)
  - Du vill synkronisera de ofullständiga och kompletta så att när torrentklienten flyttar dem, återspeglas det lokalt och alla filer är redan "där" (även om de fortfarande laddas ner). Sedan vill du använda hårda länkar eftersom även om de importeras innan de är klara kommer de fortfarande att slutföras.
  - På det här sättet synkroniseras den hela tiden medan den laddar ner, sedan flyttar torrentklienten till undermappen för tv och synkroniseringen återspeglar det. På det sättet är nedladdningarna i stort sett klara när de deklareras som färdiga. Och även om de inte är helt klara, betyder möjligheten till hårda länkar att det är okej ändå.
  - (Valfritt - om tillämpligt och/eller nödvändigt (t.ex. fjärrusenetklient)) Konfigurera ett anpassat skript som körs vid import/nedladdning/uppgradering för att ta bort den fjärranslutna filen
- Alternativt är en fjärrmontering istället för en fjärrsynkroniseringsinställning betydligt mindre komplicerad att konfigurera, men vanligtvis långsammare.
  - Montera din fjärrlagring med sshfs eller en annan nätverksfilsystemprotokoll
  - Se till att användaren och gruppen som \*Arr är konfigurerad att köra som har läs- eller skrivåtkomst.
  - Konfigurera en fjärrsökvägsmappning för att hitta den FJÄRRAN sökvägen och ersätta den med den LOKALA motsvarigheten

### Behörigheter på biblioteksmappen

Loggarna kommer att se ut så här

```none
2022-02-28 18:51:01.1|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /data/media/music/Jasmine Guillory/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Glöm inte att kontrollera behörigheter och ägande för *målmappen*. Det är lätt att fastna vid nedladdningens ägande och behörigheter och det är *vanligtvis* orsaken till behörighetsrelaterade problem, men det *kan* också vara målet. Kontrollera att målmapparna finns. Kontrollera att en målfil inte redan finns eller inte kan raderas eller flyttas till papperskorgen. Kontrollera att ägande och behörigheter tillåter att den nedladdade filen kopieras, hårdlänkas eller flyttas. Användaren eller gruppen som körs måste kunna läsa och skriva i rotmappen.

- För Windows-användare kan detta bero på att det körs som en tjänst:
  - Windows-tjänsten körs under kontot 'Local Service', som standard har detta konto inte behörighet att komma åt din användares hemkatalog om inte behörigheter har tilldelats manuellt. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemkatalog.
  - 'Local Service' har också generellt sett mycket begränsade behörigheter. Det är därför lämpligt att installera appen som en systemfältapplikation om användaren kan förbli inloggad. Alternativet att göra detta tillhandahålls under installationen. Se FAQ:n för hur du konverterar från en tjänst till en systemfältapplikation.

- För Synology-användare, se [SynoCommunitys artikel om behörigheter för deras paket](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- För icke-Windows-användare: Om du använder en NFS-montering, se till att `nolock` är aktiverat.
- Om du använder en SMB-montering, se till att `nobrl` är aktiverat.

### Behörigheter på nedladdningsmappen

Loggarna kommer att se ut så här

```none
2022-02-28 18:51:01.1|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /data/downloads/music/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Glöm inte att kontrollera behörigheter och ägande för *källan*. Det är lätt att fastna vid målets ägande och behörigheter och det är en *möjlig* orsak till behörighetsrelaterade problem, men det är vanligtvis källan. Kontrollera att källmapparna finns. Kontrollera att ägande och behörigheter tillåter att den nedladdade filen kopieras/hårdlänkas eller kopieras+raderas/flyttas. Användaren eller gruppen som körs måste kunna läsa och skriva i nedladdningsmappen.

- För Windows-användare kan detta bero på att det körs som en tjänst:
  - Windows-tjänsten körs under kontot 'Local Service', som standard har detta konto inte behörighet att komma åt din användares hemkatalog om inte behörigheter har tilldelats manuellt. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemkatalog.
  - 'Local Service' har också generellt sett mycket begränsade behörigheter. Det är därför lämpligt att installera appen som en systemfältapplikation om användaren kan förbli inloggad. Alternativet att göra detta tillhandahålls under installationen. Se FAQ:n för hur du konverterar från en tjänst till en systemfältapplikation.

- För Synology-användare, se [SynoCommunitys artikel om behörigheter för deras paket](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- För icke-Windows-användare: Om du använder en NFS-montering, se till att `nolock` är aktiverat.
- Om du använder en SMB-montering, se till att `nobrl` är aktiverat.

### Nedladdningsmappen och biblioteksmappen är inte olika mappar

Nedladdningsklienten bör ladda ner till en mapp som är åtkomlig för \*Arr och som inte är din rot/biblioteksmapp. Den bör importera från den separata nedladdningsmappen till din biblioteksmapp. Du bör aldrig ladda ner direkt till din rotmapp. Du bör heller inte använda din rotmapp som nedladdningsklientens slutförda mapp eller ofullständiga mapp.

> Din nedladdningsmapp och din rot/biblioteksmapp MÅSTE vara separata
{.is-warning}

### Felaktig kategori

Lidarr bör vara konfigurerad att använda en kategori så att den bara försöker behandla sina egna nedladdningar. Det är sällan som en torrent som skickas in av läggs till utan rätt kategori, men det kan hända. Om du lägger till torrents manuellt och vill behandla dem måste de ha rätt kategori. Den kan ställas in när som helst, eftersom försöker behandla nedladdningar varje minut.

### Packade torrents

Loggarna kommer att indikera fel som

```none
No files found are eligible for import
```

Om din torrent är packad i `.rar`-filer måste du ställa in uppackning. Vi rekommenderar [Unpackerr](https://github.com/unpackerr/unpackerr) eftersom det gör uppackningen rätt: förhindrar korrupta partiella importeringar och städar upp de uppackade filerna efter importering.

Felet kan också visas om det inte finns någon giltig mediefil i mappen.

### Upprepade nedladdningar

Det finns några orsaker till upprepade nedladdningar, men en är relaterad till begränsningen av indexeraren i utgivningsprofiler. Eftersom indexeraren *inte* lagras med datan är alla preferensordpoäng *noll* för media i ditt bibliotek, men under "RSS" och sökning kommer de att tillämpas. Detta får dig att hamna i en loop där du laddar ner objekten om och om igen eftersom de ser ut som en uppgradering, sedan inte är det, sedan dyker upp igen och ser ut som en uppgradering, sedan inte är det. Begränsa inte din utgivningsprofil till en indexer.

Detta kan också bero på att nedladdningen aldrig importerades och sedan saknas i kön, så en ny nedladdning hämtas ständigt och importeras aldrig. Se de olika andra vanliga problemen och felsökningsstegen för detta.

### Usenet-nedladdning missar importering

Lidarr tittar bara på de 60 senaste nedladdningarna i SABnzbd och NZBGet, så om du *behåller* din historik innebär detta att under stora köer med importproblem kan nedladdningar tyst missas och inte importeras. Det bästa sättet att undvika detta är att hålla din historik ren, så att eventuella objekt som fortfarande visas behöver undersökas. Du kan åstadkomma detta genom att aktivera Ta bort under Hanterare för slutförda och misslyckade nedladdningar. I NZBGet flyttar detta objekt till den *dolda* historiken, vilket är bra. Tyvärr har SABnzbd inte en liknande funktion. Det bästa du kan åstadkomma där är att använda mappningen för nzb-säkerhetskopiering.

### Nedladdningsklient rensar objekt

Nedladdningsklienten bör *inte* vara ansvarig för att ta bort nedladdningar. Usenet-klienter bör konfigureras så att de *inte* tar bort nedladdningar från historiken. Torrent-klienter bör konfigureras så att de *inte* tar bort torrents när de är färdiga med att seeda (pausa eller stoppa istället). Detta beror på att Lidarr kommunicerar med nedladdningsklienten för att veta vad som ska importeras, så om de blir *borttagna* finns det inget att importera... även om det finns en mapp med filer.

För SABnzbd hanteras detta med inställningen för historikbevarande.

### Nedladdningen kan inte matchas med en biblioteksartikel

Av olika skäl kan utgåvor inte analyseras när de har hämtats och skickats till nedladdningsklienten. Aktivitet => Alternativ => Visa Okända (detta är nu aktiverat som standard i senaste versionerna) kommer att visa alla objekt som inte ignoreras / redan har importerats inom kategorin för nedladdningsklienten i Lidarr. Dessa måste vanligtvis kartläggas och importeras manuellt.

Detta kan också inträffa om du har en utgåva i din nedladdningsklient men att den medieartikeln (film/avsnitt/bok/låt) inte finns i applikationen.

### Underliggande anslutning stängdes: Ett oväntat fel inträffade vid en sändning

Detta beror på att indexeraren använder en SSL-protokoll som inte stöds av den aktuella .NET-versionen som finns i [Lidarr => System => Status](/lidarr/system#status).

### Förfrågan tog för lång tid

Lidarr får ingen respons från indexeraren.

```none
    System.NET.WebException: Förfrågan tog för lång tid: ’https://example.org/api?t=caps&apikey=(borttaget) —> System.NET.WebException: Förfrågan tog för lång tid
```

```none
2022-11-01 10:16:54.3|Varning|Newznab|Kan inte ansluta till indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En uppgift avbröts.
```

Detta kan också bero på:

- felaktig konfiguration eller användning av en VPN
- felaktig konfiguration eller användning av en proxy
- lokala DNS-problem - Försök att byta till en annan DNS-leverantör
- lokala IPv6-problem - vanligtvis är IPv6 aktiverat, men fungerar inte
- användning av Privoxy och felaktig konfiguration av det

## Problem som inte listas

Du kan också gå igenom några vanliga felsökningskommandon för behörigheter och nätverk [i vår guide](/permissions-and-networking). Annars kan du diskutera problemet med supportteamet på Discord. Om detta är något som kan vara ett vanligt problem, föreslå att det läggs till i wikin.

# Sökningar, indexerare och spårare

- Om du använder [Prowlarr](/prowlarr) kan du visa [Historik](/prowlarr/history) för alla förfrågningar som Prowlarr har tagit emot och hur de skickades till webbplatserna. Se till att `Parametrar` är aktiverat i Prowlarr Historik => Alternativ. (i)-ikonen ger ytterligare detaljer.

## Öka loggningen till spårnivå

> **Det första steget är att öka loggningen till spårnivå, se [Loggning och loggfiler](#loggning-och-loggfiler) för information om hur du justerar loggningen och söker i loggarna. Du ska sedan återskapa problemet och använda loggarna på spårnivå från den tidsperioden för att undersöka problemet.** Om någon hjälper dig, lägg in sammanhanget före/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller liknande webbplats för att visa dem. Det behöver inte vara hela filen och det bör inte *bara* vara felet. Du bör också återskapa problemet när uppgifter som spamar loggfilen inte körs.
{.is-danger}

## Testa en indexerare eller spårare

När du testar en indexerare eller spårare kan du i felsöknings- eller spårloggar hitta den använda URL:en. Ett exempel på ett lyckat test visas nedan, där du kan se att det frågar indexeraren via en specifik URL med specifika parametrar och sedan svaret. Du kan testa denna URL i din webbläsare genom att ersätta `apikey=(borttaget)` med rätt api-nyckel, t.ex. `apikey=123`. Du kan experimentera med parametrarna om du får ett fel från indexeraren eller se om du har anslutningsproblem om det inte fungerar alls. Efter att du har testat i din egen webbläsare bör du testa från systemet som kör *om* du inte redan har gjort det.

## Testa en sökning

Precis som med indexerare/spårartestet ovan, när du utlöser en sökning med felsöknings- eller spårningsloggning på nivån Debug eller Trace kan du få URL:en som används från loggfilerna. Vid testning är det bäst att använda en så snäv sökning som möjligt. En manuell sökning är bra eftersom den är specifik och du kan se resultaten i gränssnittet samtidigt som du undersöker loggarna.

I detta test kommer du att leta efter uppenbara fel och köra några enkla tester. Du kan se att sökningen använde URL:en ***UPPDATERAD URL FÖR MUSIK BEHÖVS - DETTA ÄR ETT SONARR URL-EXEMPEL*** `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(borttaget)&offset=0&limit=100&tvdbid=354629&season=1&ep=1`, som du kan prova själv i en webbläsare efter att ha ersatt (borttaget) med din api-nyckel för den indexeraren. Fungerar det? Ser du de förväntade resultaten? Gäller den här FAQ-posten? I den URL:en kan du se att den har satt specifika kategorier med `cat=5030,5040,5045,5080`, så om du inte ser förväntade resultat är detta en trolig orsak. Du kan också se att den sökte efter tvdbid med `tvdbid=354629`, så om avsnittet inte är korrekt kategoriserat på indexeraren måste det åtgärdas. Du kan också se att den söker efter en specifik säsong och avsnitt med season=1 och ep=1, så om det inte är korrekt på indexeraren kommer du inte att se de resultaten. Titta på exemplet på XML-utdata för manuell sökning nedan för att se hur en fungerande förfrågan ser ut.

- Exempel på XML-utdata för manuell sökning

```xml
EXEMPEL PÅ SVAR FRÅN INDEXERARE EFTER SÖKNING
```

***Bilder behövs***

![searches-indexers-and-trackers1.png](/assets/lidarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/lidarr/searches-indexers-and-trackers2.png)

- Snutt av spårningslogg

```none
Snutt av spårningslogg för en manuell sökning behövs
```

- Fullständig spårningslogg för en sökning

```none
Hela avsnittet av spårningslogg för en manuell sökning behövs
```

## Vanliga problem

Här är några vanliga problem.

### Mediet är inte övervakat

Låten/låtarna övervakas inte.

### Spåraren behöver RawSearch Caps

- Lidarr söker efter `Kikis Delivery Service` men din spårare har bara resultat för `Kiki's Delivery Service`
- Detta beror på att din spårare inte stöder normaliserade sökningar.
- Lösningen är att uppdatera spårarens definition för att ange att den kräver och stöder `RawSearch`
- Jackett stöder flaggan, men funktionerna måste uppdateras för varje indexerare. Öppna en förfrågan om funktionen till Jackett för att lägga till denna funktionalitet för din indexerare.
- Prowlarr stöder flaggan, men funktionerna måste uppdateras för varje indexerare. Öppna en förfrågan om funktionen till Prowlarr för att lägga till denna funktionalitet för din indexerare.

### Felaktiga kategorier

Felaktiga kategorier är förmodligen den vanligaste orsaken till att resultat visas i manuella sökningar på en indexerare/spårare, men *inte* i . Indexeraren/spåraren *bör* visa kategorin i sökresultaten, vilket bör hjälpa dig att lista ut vad som saknas. Om du använder Jackett eller Prowlarr har varje spårare en lista över specifikt stödda kategorier. Se till att du använder de korrekta för kategorierna. Många tycker att det är bra att ha listan synlig i ett webbläsarfönster medan de redigerar posten i .

### Felaktiga resultat

Ibland returnerar indexerare helt irrelevanta resultat, kommer att mata in parametrar för att begränsa sökningen, men de returnerade resultaten är helt irrelevanta. Eller ibland, mestadels relevanta med några felaktiga resultat. Det första beror vanligtvis på ett indexerarproblem och du kan se vilket indexerarproblem det är från spårningsloggarna. Du kan inaktivera den indexeraren och rapportera problemet. Det andra beror vanligtvis på kategoriserade utgåvor som bör rapporteras på indexeraren/spåraren.

### Förfrågan lyckades - Inga resultat returnerades

Du får ett meddelande liknande `Förfrågan lyckades, men inga resultat returnerades från din indexerare. Detta kan vara ett problem med indexeraren eller dina kategorinställningar för indexeraren.`

Detta beror på att din indexerare inte returnerar några resultat som finns inom de kategorier du har konfigurerat för indexeraren.

### Saknade resultat

Om du har resultat på webbplatsen som du kan hitta men som inte visas i Lidarr är ditt problem förmodligen en av flera möjligheter:

- [Kategorierna är felaktiga - Se ovan](#felaktiga-kategorier)
- En ID-baserad sökning görs och indexeraren har inte korrekt kartlagt utgåvorna till det ID:et. Detta är något som bara din indexerare kan lösa. De måste se till att utgåvan är kartlagd till de korrekta tillämpliga ID:erna.
- Du söker inte på samma sätt som Lidarr söker; Det är mycket troligt att termerna du söker på indexeraren inte är hur Lidarr frågar efter dem. Du kan se hur Lidarr frågar i spårningsloggarna. Textbaserade frågor kommer generellt att vara i formatet `q=ord%20och%20saker%20här`  den här strängen är HTTP-kodad och kan enkelt avkodas med hjälp av vilket verktyg för HTML-avkodning/kodning som helst online.

### Certifikatvalidering

Du kommer att ansluta till de flesta indexerare/spårare via https, så du måste se till att det fungerar korrekt på ditt system. Det innebär att din tidszon och tid måste vara inställda *korrekt*. Det innebär också att dina systemcertifikat måste vara uppdaterade.

### Träffar på hastighetsbegränsningar

Om du kör din genom en VPN eller proxy kan du konkurrera med 10-tals, 100-tals eller 1000-tals andra personer som alla försöker använda tjänster som , theXEM och/eller dina indexerare och spårare. Hastighetsbegränsning och DDOS-skydd görs ofta per IP-adress och din VPN/proxy-utgångspunkt är *en* IP-adress. Om du inte befinner dig i ett förtryckande land som Kina, Australien eller Sydafrika behöver du inte använda VPN/proxy .

Rarbg har en tendens att ha någon form av hastighetsbegränsning i sin API och visar att det inte finns några resultat.

### IP-blockering

På samma sätt som hastighetsbegränsningar kan vissa indexerare - som Nyaa - helt enkelt blockera en IP-adress. Detta är vanligtvis halvpermanent och lösningen är att få en ny IP-adress från din internetleverantör eller VPN-leverantör.

### Användning av Jackett /all-slutpunkten

Jackett `/all`-slutpunkten är bekväm, men det är den enda fördelen. Allt annat kan vara potentiella problem, så det krävs att varje spårare läggs till separat. Alternativt kan du överväga att använda Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

[Till och med Jackett säger att /all bör undvikas och inte bör användas.](https://github.com/Jackett/Jackett#aggregate-indexers)

Att använda all-slutpunkten har inga fördelar (förutom minskad hantering), bara nackdelar:

- du förlorar kontrollen över spårarspecifika inställningar (kategorier, söklägen, etc.)
- blandning av söklägen (IMDB, fråga, etc.) kan ge lågkvalitativa resultat
- spårarspecifika kategorier (\>= 100000) kan inte användas.
- långsamma indexerare kommer att sakta ner det totala resultatet
- totala resultat är begränsade till 1000

Genom att lägga till varje indexerare separat kan du finjustera kategorierna för varje indexerare, vilket kan vara ett problem med `/all`-slutpunkten om fel kategori orsakar fel på vissa spårare. I är varje indexerare begränsad till 1000 resultat om sidindelning stöds eller 100 om det inte gör det, vilket innebär att ju fler spårare du lägger till i Jackett, desto större är risken att klippa resultat. Slutligen, om *en* av spårarna i `/all` returnerar ett fel, kommer att inaktivera den och nu får du inga resultat alls.

### Användning av NZBHydra2 som en enda post

Att använda NZBHydra2 som en enda indexeringspost (dvs. 1 NZBHydra2-post i Lidarr för många indexerare i NZBHydra2) istället för flera (dvs. många NZBHydra2-poster i Lidarr för många indexerare i NZBHydra2) har samma problem som noterats ovan med Jacketts `/all`-slutpunkt.

### Problem som inte listas

Du kan också gå igenom några vanliga felsökningskommandon för behörigheter och nätverk [i vår guide](/permissions-and-networking). Annars kan du diskutera problemet med supportteamet på Discord. Om detta är något som kan vara ett vanligt problem, föreslå att det läggs till i wikin.

## Fel

Detta är några av de vanliga felen du kan se när du lägger till en indexerare

### Underliggande anslutning stängdes: Ett oväntat fel inträffade vid en sändning

Detta beror på att indexeraren använder en SSL-protokoll som inte stöds av den aktuella .NET-versionen som finns i [Lidarr => System => Status](/lidarr/system#status).

### Förfrågan tog för lång tid

Lidarr får ingen respons från indexeraren.

```none
    System.NET.WebException: Förfrågan tog för lång tid: ’https://example.org/api?t=caps&apikey=(borttaget) —> System.NET.WebException: Förfrågan tog för lång tid
```

```none
2022-11-01 10:16:54.3|Varning|Newznab|Kan inte ansluta till indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En uppgift avbröts.
```

Detta kan också bero på:

- felaktig konfiguration eller användning av en VPN
- felaktig konfiguration eller användning av en proxy
- lokala DNS-problem - Försök att byta till en annan DNS-leverantör
- lokala IPv6-problem - vanligtvis är IPv6 aktiverat, men fungerar inte
- användning av Privoxy och felaktig konfiguration av det

### Problem som inte listas

Du kan också gå igenom några vanliga felsökningskommandon för behörigheter och nätverk [i vår guide](/permissions-and-networking). Annars kan du diskutera problemet med supportteamet på Discord. Om detta är något som kan vara ett vanligt problem, föreslå att det läggs till i wikin.