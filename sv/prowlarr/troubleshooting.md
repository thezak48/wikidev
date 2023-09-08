---
title: Felsökning av Prowlarr
description: 
published: true
date: 2023-08-20T00:20:04.841Z
tags: prowlarr, felsökning
editor: markdown
dateCreated: 2021-06-20T20:05:25.223Z
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
- [NGINX-fel](#nginx-fel)
- [Indexer-, applikations- och nedladdningsklientproblem](#indexer-applikations-och-nedladdningsklientproblem)
  - [Kan inte bestämma bildstorlek eller en korrupt bild mottogs](#kan-inte-bestämma-bildstorlek-eller-en-korrupt-bild-mottogs)
  - [Anslutning avbruten](#anslutning-avbruten)
  - [Sonarr HTTP 404-fel](#sonarr-http-404-fel)
  - [\*Arr HTTP 400-fel](#arr-http-400-fel)
  - [503 HTTP Service otillgänglig](#503-http-service-otillgänglig)
  - [Ogiltiga torrents](#ogiltiga-torrents)
  - [Sökningar och indexerare](#sökningar-och-indexerare)

# Be om hjälp

Behöver du hjälp? Det är okej, alla behöver hjälp ibland. Du kan få hjälp i realtid via chatt på

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiell Prowlarr Discord*](https://prowlarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiell Prowlarr Subreddit*](https://reddit.com/r/prowlarr)
{.links-list}

Men innan du går dit och postar, se till att din hjälpförfrågan är så bra som möjligt. Beskriv tydligt problemet och beskriv kortfattat din konfiguration, inklusive saker som ditt OS/distribution, version av .NET, version av Prowlarr, nedladdningsklient och dess version. **Om du använder [Docker](https://www.docker.com/) kan du köra igenom [Docker Guide](/docker-guide) först eftersom det kommer att lösa vanliga och frekventa problem med sökvägar/behörigheter. Annars se till att ha en [docker compose](/docker-guide#docker-compose) till hands. [Så här genererar du en Docker Compose](https://trash-guides.info/compose)** Berätta om vad du redan har försökt, vad du har tittat på. Använd avsnittet [Loggning och loggfiler](#loggning-och-loggfiler) för att öka loggningen till spårnivå, återskapa problemet, lägg upp den relevanta kontexten på en pastebin och inkludera en länk till den i ditt inlägg. Du kan till och med inkludera några skärmbilder för att markera problemet.

Ju mer vi vet, desto lättare är det att hjälpa dig.

# Loggning och loggfiler

Det kan vara fördelaktigt att också granska [Vanliga problem med indexerare, applikationer och nedladdningsklienter](#indexer-applikations-och-nedladdningsklientproblem).

> Om du ombeds att tillhandahålla indexerarens svar för utveckling eller felsökning, fortsätt att läsa detta blåa avsnitt...annars fortsätt till stegen nedan. För att felsöka indexerarsvar kan det vara användbart att gå till `inställningar/utveckling` (dold sida) i Prowlarr och tillfälligt aktivera förbättrad indexerarloggning för att logga indexerarens svar. Det behöver inte vara aktiverat hela tiden
{.is-info}

Om du ombeds om felsökningsloggar kommer dina loggar att innehålla `debug` och om du ombeds om spårloggar kommer dina loggar att innehålla `trace`. Om de loggar du tillhandahåller inte innehåller något av dessa, är de inte de begärda loggarna.

- Undvik att dela hela loggfilen om du inte ombeds om det.
- Ladda inte upp loggar direkt till Discord eller klistra in dem som väggar av text, om du inte ombeds om det.
- Dela inte loggarna som en bilaga, en zip-fil eller något annat än text som delas via de tjänster som anges nedan

För att tillhandahålla bra och användbara loggar för delning:

> Se till att det inte körs någon spamig uppgift, som en RSS-uppdatering
{.is-warning}

1. [Öka loggningen till spårnivå (Inställningar => Allmänt => Loggnivå eller Redigera konfigurationsfilen)](#spår-felsökningsloggar)
2. [Rensa loggar (System => Loggar => Rensa loggar eller Ta bort alla loggar i loggkatalogen)](#rensa-loggar)
3. Återskapa problemet (Gör om det som orsakar problem)
4. [Öppna spårloggen (Lidarr.trace.txt) via användargränssnittet eller loggfilen](#standardplats-för-loggar) på filsystemet och hitta den relevanta kontexten
5. Kopiera en stor del före problemet, själva problemet och en stor del efter problemet.
6. Använd [Gist](https://gist.github.com/), [0bin (**Se till att inaktivera färgläggning**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntus Pastebin](https://pastebin.ubuntu.com/) eller liknande webbplatser - undvik de som anges nedan - för att dela de kopierade loggarna ovan

**Varningar:**
- **Använd inte [pastebin.com](https://pastebin.com) eftersom deras filter har en tendens att blockera loggarna.
- Använd inte [pastebin.pl](https://pastebin.pl) eftersom deras webbplats ofta inte är tillgänglig.
- Använd inte [JustPasteIt](https://justpaste.it/) eftersom deras webbplats inte underlättar granskning av loggar.
- Ladda inte upp din logg som en fil
- Ladda inte upp och dela dina loggar via Google Drive, Dropbox eller någon annan webbplats som inte anges ovan.
- Arkivera inte (zip, tar (tarball), 7zip, etc.) dina loggar.
- Dela inte konsolresultat, utdata från docker-container eller något annat än de angivna applikationsloggarna

**Viktig anteckning:**
- När du använder [0bin](https://0bin.net/), se till att inaktivera färgläggning och bränn inte efter att ha läst.

- Alternativt, om du letar efter en specifik post i en gammal loggfil men inte är säker på vilken, kan du använda N++. Du kan använda Notepad++ "Sök i filer"-funktion för att söka i gamla loggfiler vid behov.
- **Endast Unix:** Alternativt, om du letar efter en specifik post i en gammal loggfil men inte är säker på vilken, kan du använda grep. Om du till exempel vill hitta information om filmen/serien/boken/låten/indexeraren "Shooter" kan du köra följande kommando `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Om din [Appdata-katalog](/prowlarr/appdata-directory) är i din hemkatalog kör du: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flaggor har följande funktioner
    * -i: ignorera skiftläge
    * -n: visa radnummer
    *  -r: sök rekursivt i alla filer i sökvägen
    * -C: ange antal rader före och efter den hittade raden
    * -e: mönstret att söka efter

```

## Standardplats för loggar

Loggfilerna finns i Prowlarrs [Appdata-katalog](/prowlarr/appdata-directory), inuti mappen logs/. Du kan också komma åt loggfilerna från användargränssnittet under System => Loggar => Filer.

> Observera: Loggarna ("Händelserna") i användargränssnittet är inte samma som loggfilerna och är inte lika användbara. Om du ombeds om loggar, kopiera/klistra in från loggfilerna och inte från tabellen.
{.is-info}

## Plats för uppdateringsloggar

Uppdateringsloggarna finns i Prowlarrs [Appdata-katalog](/prowlarr/appdata-directory), inuti mappen UpdateLogs/.

## Dela loggar

Loggarna kan vara långa och svåra att läsa som en del av ett forum- eller Reddit-inlägg och de är spamiga i Discord, så använd [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller någon annan liknande pastebin-webbplats. Hela filen behövs vanligtvis inte, bara en bra mängd kontext före och efter problemet/felmeddelandet. Glöm inte att vänta på att spamiga uppgifter som en RSS-synkronisering eller biblioteksuppfräschning ska slutföras.

## Spår-/felsökningsloggar

Du kan ändra loggnivån under Inställningar => Allmänt => Loggning. Prowlarr behöver inte startas om för att ändringen ska träda i kraft. Denna ändring påverkar endast loggfilerna, inte loggdatabasen. De senaste felsöknings-/spårloggfilerna heter `prowlarr.debug.txt` respektive `prowlarr.trace.txt`.

Om du inte kan komma åt användargränssnittet för att ställa in loggningsnivån kan du göra det genom att redigera config.xml i AppData-katalogen och ändra värdet för LogLevel till Debug eller Trace istället för Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Rensa loggar

Du kan rensa loggfilerna och loggdatabasen direkt från användargränssnittet, under `System` => `Loggar` => `Filer` och `System` => `Loggar` => `Ta bort` (Papperskorgsikonen).

# Flera loggfiler

Prowlarr använder rullande loggfiler som är begränsade till 1 MB vardera. Den aktuella loggfilen är alltid Prowlarr.txt, för de andra filerna är Prowlarr.0.txt den näst nyaste (ju högre nummer desto äldre är den). Denna loggfil innehåller `fatal`, `error`, `warn` och `info`-poster.

När felsökningsloggning är aktiverad kommer det att finnas ytterligare rullande loggfiler för `prowlarr.debug.txt`. Denna loggfil innehåller `fatal`, `error`, `warn`, `info` och `debug`-poster. Den täcker vanligtvis en period på 40 timmar.

När spårloggning är aktiverad kommer det att finnas ytterligare rullande loggfiler för `prowlarr.trace.txt`. Denna loggfil innehåller `fatal`, `error`, `warn`, `info`, `debug` och `trace`-poster. På grund av spårloggningens omfattning täcker den endast några timmar som mest, och ibland mindre än en minut om du gör något intensivt.

# Återställning efter misslyckad uppdatering

Vi gör allt vi kan för att förhindra problem vid uppdatering, men om de ändå uppstår kommer detta att guida dig genom stegen för att återställa din installation.

## Identifiera problemet

- Det bästa stället att titta när programmet inte startar efter en uppdatering är att granska [uppdateringsloggar](#plats-för-uppdateringsloggar) och se om uppdateringen slutfördes utan problem. Om det inte finns något problem där är nästa steg att titta på dina vanliga programloggfiler, innan du försöker starta om, använd [Loggning](/prowlarr/settings#logging) och [Loggfiler](/prowlarr/system#log-files) för att hitta dem och öka loggnivån.
- Det vanligaste problemet är att systemet där appen är installerad har manipulerat `/tmp`-katalogen och raderat kritiska \*Arr-filer under uppdateringen, vilket orsakar både uppdateringen och återställningen att misslyckas. I det här fallet installerar du helt enkelt om appen på plats över den befintliga trasiga installationen.

### Migrationsproblem

- Migrationsfel kommer inte att vara identiska, men här är ett exempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Behörighetsproblem

- Behörighetsproblem beror på att appen inte kan komma åt de relevanta temporära mapparna och/eller appens binära mapp. Åtgärda behörigheterna så att användaren/gruppen som appen körs som har lämplig åtkomst.

- Synology-användare kan stöta på denna Synology-bugg `Access to the path '/proc/{some number}/maps is denied`

- Synology-användare kan också stöta på att det inte finns tillräckligt med utrymme i `/tmp` på vissa NAS-enheter. Du måste ange en annan sökväg för `/tmp` för appen. Se SynoCommunity eller andra Synology-supportkanaler för hjälp med detta.

## Lös problemet

Vid migrationsproblem kan du inte göra mycket direkt, om problemet är specifikt för dig (eller om det inte finns några inlägg än), skapa gärna ett inlägg på [vår subreddit](https://reddit.com/r/prowlarr) eller besök vår [discord](https://prowlarr.com/discord). Om det finns andra med samma problem kan du vara säker på att vi arbetar med det.

> Se till att du inte försökte använda en databas från `nightly`-versionen i den stabila versionen. Att byta grenar är inte rekommenderat.{.is-info}

### Behörighetsproblem

- Åtgärda behörigheterna så att användaren/gruppen som appen körs som kan komma åt (läsa och skriva) både `/tmp` och installationskatalogen för appen.

- För Synology-användare som upplever problem med `/proc/###/maps` bör stoppa Sonarr eller de andra \*Arr-apparna och uppdatera för att lösa detta. Detta är ett problem med SynoCommunity-paketet.

### Uppgradera manuellt

Hämta den senaste versionen från vår webbplats.

Installera uppdateringen (.exe) eller extrahera (.zip) innehållet över din befintliga installation och kör Prowlarr som vanligt.

# NGINX-fel

I din Prowlarr-konfiguration behöver du denna rad:

`proxy_set_header Host $host;`

Om du har någon annan `proxy_set_header` måste du ersätta den med raden ovan.

# Indexerar-, applikations- och nedladdningsklientproblem

- På en grundläggande nivå behöver Prowlarr kunna kommunicera med dina indexerare.
- Om du använder applikationssynkronisering behöver Prowlarr också kunna kommunicera med dina applikationer och applikationerna behöver kunna kommunicera med Prowlarr.
- Om du har en nedladdningsklient i Prowlarr för manuella nedladdningar i Prowlarr behöver Prowlarr kunna kommunicera med din nedladdningsklient.

> Observera att loggar som indikerar att en fråga ställs till indexerare ID 0: ID 0 är en generisk teständpunkt som gör att vi kan testa om \*Arr kan ringa tillbaka och ansluta till Prowlarr utan att faktiskt förlita sig på att en indexerare fungerar.
{.is-info}

Här är några vanliga orsaker

## Kan inte bestämma bildstorlek eller en korrupt bild mottogs

`Cannot determine the frame size or a corrupted frame was received.`

Prowlarr hade ett säkerhetsproblem vid anslutning till webbplatsen.

Detta orsakas vanligtvis av:

- lokala DNS-problem - Försök att byta till en annan DNS-leverantör

## Anslutning avbruten

`The request timed out`

Prowlarr får inget svar från klienten. [Se vår guide för allmän nätverks- och behörighetsfelsökning](/permissions-and-networking)

Detta orsakas vanligtvis av:

- felaktig konfiguration eller användning av en VPN
- felaktig konfiguration eller användning av en proxy
- lokala DNS-problem - Försök att byta till en annan DNS-leverantör
- lokala IPv6-problem - vanligtvis är IPv6 aktiverat, men fungerar inte
- användning av Privoxy

## Sonarr HTTP 404-fel

- Detta beror vanligtvis på att du kör en utdaterad (EOL) version av Sonarr som inte har v3 API-slutpunkterna
- Prowlarr stöder inte Sonarr v2
- Prowlarr stöder endast Sonarr v3

## \*Arr HTTP 400-fel

- Se denna FAQ-post: [Prowlarr kommer inte att synkronisera X Indexer till App](/prowlarr/faq#prowlarr-will-not-sync-x-indexer-to-app)

## 503 HTTP Service otillgänglig

- Detta beror vanligtvis på att din tracker blockerar dig via Cloudflare och kräver [FlareSolverr](https://github.com/FlareSolverr/FlareSolverr)

## Ogiltiga torrents

- Försök att ladda ner länken via URL:en och variablerna som Prowlarr använde.
- Försök att ladda ner torrenten via prowlarr (det vill säga använd länken som prowlarr-appen använde för att hämta filen).
- Se till att dina cookies eller andra autentiseringsuppgifter för din indexer inte har gått ut eller är ogiltiga.
- Om problemet beror på Prowlarr, vänligen rapportera en bugg.

## Sökning, indexer och spårare

- [Lidarr Sökning och Indexerare](/lidarr/troubleshooting#searches-indexers-and-trackers)
- [Radarr Sökning och Indexerare](/radarr/troubleshooting#searches-indexers-and-trackers)
- [Readarr Sökning och Indexerare](/readarr/troubleshooting#searches-indexers-and-trackers)
- [Sonarr Sökning och Indexerare](/sonarr/troubleshooting#searches-indexers-and-trackers)
{.links-list}