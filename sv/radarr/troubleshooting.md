---
title: Radarr Felsökning
description: Felsökning för Radarr, inklusive att få loggfiler, felsökning av sökning och vanliga problem, samt felsökning och vanliga problem med nedladdning/importering
published: true
date: 2023-08-12T09:40:45.369Z
tags: radarr, felsökning
editor: markdown
dateCreated: 2021-08-03T21:05:52.988Z
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
    - [Databasens diskavbild är skadad](#databasens-diskavbild-är-skadad)
    - [Migrationsproblem](#migrationsproblem)
    - [UI-migrationsproblem](#ui-migrationsproblem)
    - [Behörighetsproblem](#behörighetsproblem)
  - [Lösning av problemet](#lösning-av-problemet)
    - [Migrationsproblem](#migrationsproblem)
    - [Behörighetsproblem](#behörighetsproblem)
    - [Manuell uppgradering](#manuell-uppgradering)
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
    - [Usenet-nedladdning misslyckas med importering](#usenet-nedladdning-misslyckas-med-importering)
    - [Nedladdningsklient rensar objekt](#nedladdningsklient-rensar-objekt)
    - [Nedladdningen kan inte matchas med ett biblioteksobjekt](#nedladdningen-kan-inte-matchas-med-ett-biblioteksobjekt)
    - [Anslutningstidsgräns överskriden](#anslutningstidsgräns-överskriden)
  - [Problem som inte listas](#problem-som-inte-listas)
- [Sökningar, indexer och spårare](#sökningar-indexer-och-spårare)
  - [Öka loggningsnivån till spårning](#öka-loggningsnivån-till-spårning)
  - [Testa en indexer eller spårare](#testa-en-indexer-eller-spårare)
  - [Testa en sökning](#testa-en-sökning)
  - [Vanliga problem](#vanliga-problem-1)
    - [Spårare kräver RawSearch Caps](#spårare-kräver-rawsearch-caps)
    - [Media är oövervakad](#media-är-oövervakad)
    - [Felaktiga kategorier](#felaktiga-kategorier)
    - [Lyckad förfrågan - Inga resultat returnerade](#lyckad-förfrågan-inga-resultat-returnerade)
    - [Felaktiga resultat](#felaktiga-resultat)
    - [Saknade resultat](#saknade-resultat)
    - [Certifikatvalidering](#certifikatvalidering)
    - [Träffar på begränsningar](#träffar-på-begränsningar)
    - [IP-blockering](#ip-blockering)
    - [Året matchar inte](#året-matchar-inte)
    - [Saknat år](#saknat-år)
    - [Användning av Jackett /all-slutpunkt](#användning-av-jackett-all-slutpunkt)
    - [Användning av NZBHydra2 som enskild post](#användning-av-nzbhydra2-som-enskild-post)
    - [Problem som inte listas](#problem-som-inte-listas-1)
  - [Fel](#fel)
    - [Den underliggande anslutningen stängdes: Ett oväntat fel inträffade vid sändning](#den-underliggande-anslutningen-stängdes-ett-oväntat-fel-inträffade-vid-sändning)
    - [Begäran tog för lång tid](#begäran-tog-för-lång-tid)
    - [Problem som inte listas](#problem-som-inte-listas-2)

# Be om hjälp

Behöver du hjälp? Det är okej, alla behöver hjälp ibland. Du kan få hjälp i realtid via chatt på

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiell Radarr Discord*](https://radarr.video/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiell Radarr Subreddit*](https://reddit.com/r/radarr)
{.links-list}

Men innan du går dit och postar, se till att din hjälpförfrågan är så bra som möjligt. Beskriv tydligt problemet och beskriv kortfattat din konfiguration, inklusive saker som ditt operativsystem/distribution, version av .NET, version av Radarr, nedladdningsklient och dess version. **Om du använder [Docker](https://www.docker.com/) ska du köra igenom [Docker Guide](/docker-guide) först eftersom det kommer att lösa vanliga och frekventa problem med sökvägar/behörigheter. Annars, se till att ha en [docker compose](/docker-guide#docker-compose) till hands. [Så här genererar du en Docker Compose](https://trash-guides.info/compose)** Berätta om vad du redan har försökt, vad du har tittat på. Använd avsnittet [Loggning och loggfiler](#loggning-och-loggfiler) för att öka loggningsnivån till spårning, återskapa problemet, lägg upp den relevanta kontexten på en pastebin-sida och inkludera en länk till den i ditt inlägg. Inkludera kanske även några skärmbilder för att markera problemet.

Ju mer vi vet, desto lättare är det att hjälpa dig.

# Loggning och loggfiler

Det kan vara fördelaktigt att också granska vanliga felsökningsproblem:
- [Vanliga problem med nedladdningar och importering](#vanliga-problem)
- [Vanliga problem med sökningar, indexer och spårare](#vanliga-problem-1)
{.links-list}

Om du ombeds att skicka felsökningsloggar kommer dina loggar att innehålla `debug` och om du ombeds att skicka spårningsloggar kommer dina loggar att innehålla `trace`. Om de loggar du tillhandahåller inte innehåller något av dessa, är de inte de efterfrågade loggarna.

- Undvik att dela hela loggfilen om du inte ombeds att göra det.
- Ladda inte upp loggar direkt till Discord eller klistra in dem som väggar av text, om du inte ombeds att göra det.
- Dela inte loggarna som en bilaga, en zip-fil eller något annat än text som delas via de tjänster som anges nedan.

För att tillhandahålla bra och användbara loggar för delning:

> Se till att ingen spamig uppgift körs, som till exempel en RSS-uppdatering
{.is-warning}

1. [Öka loggningsnivån till spårning (Inställningar => Allmänt => Loggningsnivå eller Redigera konfigurationsfilen)](#spår-felsökningsloggar)
2. [Rensa loggar (System => Loggar => Rensa loggar eller Radera alla loggar i loggmappen)](#rensa-loggar)
3. Återskapa problemet (Gör om det som orsakar problem)
4. [Öppna spårningsloggfilen (radarr.trace.txt) via gränssnittet eller loggfilen](#standardplats-för-loggar) på filsystemet och hitta den relevanta kontexten
5. Kopiera en stor del före problemet, själva problemet och en stor del efter problemet.
6. Använd [Gist](https://gist.github.com/), [0bin (**Se till att inaktivera färgläggning**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntus Pastebin](https://pastebin.ubuntu.com/) eller liknande sidor - undvik de som anges nedan - för att dela de kopierade loggarna ovan

**Varningar:**
- **Använd inte [pastebin.com](https://pastebin.com) eftersom deras filter har en tendens att blockera loggarna.
- Använd inte [pastebin.pl](https://pastebin.pl) eftersom deras webbplats ofta inte är tillgänglig.
- Använd inte [JustPasteIt](https://justpaste.it/) eftersom deras webbplats inte underlättar granskning av loggar.
- Ladda inte upp din logg som en fil.
- Ladda inte upp och dela dina loggar via Google Drive, Dropbox eller någon annan webbplats som inte anges ovan.
- Arkivera inte (zip, tar (tarball), 7zip, etc.) dina loggar.
- Dela inte konsolresultat, dockercontainerresultat eller något annat än de angivna applikationsloggarna

**Viktig anteckning:**
- När du använder [0bin](https://0bin.net/), se till att inaktivera färgläggning och bränn inte efter läsning.

- Alternativt, om du letar efter en specifik post i en gammal loggfil men inte är säker på vilken, kan du använda N++. Du kan använda Notepad++ "Sök i filer"-funktion för att söka i gamla loggfiler vid behov.
- **Endast Unix:** Alternativt, om du letar efter en specifik post i en gammal loggfil men inte är säker på vilken, kan du använda grep. Till exempel, om du vill hitta information om filmen/serien/boken/låten/indexeraren "Shooter" kan du köra följande kommando `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Om din [Appdata-katalog](/radarr/appdata-directory) är i din hemkatalog kör du: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flaggen har följande funktioner
    * -i: ignorera skiftläge
    * -n: visa radnummer
    * -r: sök rekursivt i alla filer i sökvägen
    * -C: ange antal rader före och efter den hittade raden
    * -e: mönstret att söka efter

```

## Standardplats för loggar

Loggfilerna finns i Radarrs [Appdata-katalog](/radarr/appdata-directory), inuti mappen logs/. Du kan också komma åt loggfilerna från gränssnittet på System => Loggar => Filer.

> Observera: Loggarna ("Händelserna") i tabellen i gränssnittet är inte samma som loggfilerna och är inte lika användbara. Om du ombeds att skicka loggar, kopiera/klistra in från loggfilerna och inte från tabellen.
{.is-info}

## Plats för uppdateringsloggar

Uppdateringsloggarna finns i Radarrs [Appdata-katalog](/radarr/appdata-directory), inuti mappen UpdateLogs/.

## Dela loggar

Loggarna kan vara långa och svåra att läsa som en del av ett forum- eller Reddit-inlägg och de är spamiga i Discord, så använd [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller någon annan liknande pastebin-sida. Hela filen behövs vanligtvis inte, bara en bra mängd kontext före och efter problemet/felmeddelandet. Glöm inte att vänta på att spamiga uppgifter som en RSS-synkronisering eller biblioteksuppfräschning ska slutföras.

## Spår-/felsökningsloggar

Du kan ändra loggningsnivån på Inställningar => Allmänt => Loggning. Radarr behöver inte startas om för att ändringen ska träda i kraft. Denna ändring påverkar endast loggfilerna, inte loggningsdatabasen. De senaste felsöknings-/spårningsloggfilerna heter `radarr.debug.txt` respektive `radarr.trace.txt`.

Om du inte kan komma åt gränssnittet för att ställa in loggningsnivån kan du göra det genom att redigera config.xml i AppData-katalogen och ändra värdet på LogLevel till Debug eller Trace istället för Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Rensa loggar

Du kan rensa loggfilerna och loggdatabasen direkt från gränssnittet, under System => Loggar => Rensa loggar och System => Loggar => Radera (Papperskorgsikonen)

# Flera loggfiler

Radarr använder rullande loggfiler som är begränsade till 1 MB vardera. Den aktuella loggfilen är alltid `radarr.txt`, för de andra filerna är `radarr.0.txt` den näst nyaste (ju högre nummer desto äldre är den). Denna loggfil innehåller `fatal`, `error`, `warn` och `info`-poster.

När felsökningsloggnivån är aktiverad kommer det att finnas ytterligare rullande loggfiler med namnen `radarr.debug.txt`. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info` och `debug`-poster. De täcker vanligtvis en period på 40 timmar.

När spårningsloggnivån är aktiverad kommer det att finnas ytterligare rullande loggfiler med namnen `radarr.trace.txt`. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info`, `debug` och `trace`-poster. På grund av spårningsloggnivåns omfattning täcker de endast ett par timmar som mest.

# Återställning efter misslyckad uppdatering

- Vi gör allt vi kan för att förhindra problem vid uppgradering, men om de ändå uppstår kommer detta att guida dig genom stegen för att återställa din installation.
- Detta avsnitt täcker också vanliga problem efter uppdateringen.

## Identifiera problemet

- Det bästa stället att titta när programmet inte startar efter en uppdatering är att granska [uppdateringsloggarna](#plats-för-uppdateringsloggar) och se om uppdateringen slutfördes utan problem. Om det inte finns något problem där är nästa steg att titta på dina vanliga programloggfiler, innan du försöker starta om, använd [Loggning](/radarr/settings#logging) och [Loggfiler](/radarr/system#log-files) för att hitta dem och öka loggningsnivån.
- Det vanligaste problemet är att systemet där appen är installerad har stört med `/tmp`-katalogen och raderat kritiska \*Arr-filer under uppgraderingen, vilket orsakar att både uppgraderingen och återställningen misslyckas. I det fallet kan du helt enkelt installera om över den befintliga trasiga installationen.

### Databasens diskavbild är skadad

- Se vår [FAQ-post](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)

### Migrationsproblem

- Migrationsfel kommer inte att vara identiska, men här är ett exempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### UI-migrationsproblem

- Om du växlar mellan [osupporterade versioner/grenar](/radarr/faq#can-i-switch-between-branches) kan du uppleva ett migrationsproblem som ser ut som nedan. Lösningen är att [gå tillbaka till den tidigare grenen eller högre versionen](/radarr/faq#how-do-i-update-radarr), eller [återställa en säkerhetskopia](/radarr/faq#how-do-i-backuprestore-radarr) för din nuvarande version.

![radarr-migration-error-ui.png](/assets/radarr/radarr-migration-error-ui.png)

### Behörighetsproblem

- Behörighetsproblem beror på att programmet inte kan komma åt de relevanta tillfälliga mapparna och/eller appens binära mapp. Åtgärda behörigheterna så att användaren/gruppen som programmet körs som har lämplig åtkomst.

- Synology-användare kan stöta på detta Synology-bugg `Åtkomst till sökvägen '/proc/{något nummer}/maps' nekas`

- Synology-användare kan också stöta på att det inte finns tillräckligt med utrymme i `/tmp` på vissa NAS-enheter. Du måste ange en annan `/tmp`-sökväg för appen. Se SynoCommunity eller andra Synology-supportkanaler för hjälp med detta.

## Åtgärda problemet

### Migrationsproblem

Vid ett migrationsproblem kan du inte göra mycket omedelbart. Om problemet är specifikt för dig (eller om det ännu inte finns några inlägg), skapa ett inlägg på [vår subreddit](https://reddit.com/r/radarr) eller besök vår [discord](https://radarr.video/discord). Om det finns andra med samma problem kan du vara säker på att vi arbetar med det.

> Se till att du inte har försökt använda en databas från `nightly`-versionen i den stabila versionen. Att byta grenar rekommenderas inte.{.is-info}

### Behörighetsproblem

- Åtgärda behörigheterna för att säkerställa att användaren/gruppen som applikationen körs som har åtkomst (läs- och skrivåtkomst) till både `/tmp` och installationskatalogen för applikationen.

- För Synology-användare som upplever problem med `/proc/###/maps` bör stoppa Sonarr eller de andra \*Arr-applikationerna och uppdatera lösa detta. Detta är ett problem med SynoCommunity-paketet.

### Manuell uppgradering

Hämta den senaste versionen från vår webbplats.

Installera uppdateringen (.exe) eller extrahera (.zip) innehållet över din befintliga installation och kör Radarr som vanligt.

# Nedladdningar och import

Nedladdning och import är där *de flesta* personer upplever problem. På en övergripande nivå behöver Radarr kunna kommunicera med din nedladdningsklient och ha åtkomst till de filer den laddar ner. Det finns många olika nedladdningsklienter som stöds och ännu fler olika konfigurationer. Det innebär att även om det finns några *vanliga* konfigurationer, finns det ingen *rätt* konfiguration och varje persons konfiguration kan vara lite annorlunda.

> **Det första steget är att öka loggningsnivån till Trace, se [Logging and Log Files](#logging-and-log-files) för information om hur du justerar loggningsnivån och söker i loggarna. Du kommer sedan att återskapa problemet och använda loggarna med trace-nivå från den tidsperioden för att undersöka problemet.** Om någon hjälper dig, lägg in kontext från före/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller liknande webbplats för att visa dem. Det behöver inte vara hela filen och det bör inte *bara* vara felet. Du bör också återskapa problemet när uppgifter som spamar loggfilen inte körs.
{.is-danger}

När du söker hjälp, se till att läsa [begära hjälp](#begära-hjälp) så att du kan ge oss de detaljer vi behöver.

## Testa nedladdningsklienten

Se till att din nedladdningsklient(er) körs. Börja med att testa nedladdningsklienten, om den inte fungerar kan du se detaljer i loggarna med trace-nivå. Du bör hitta en URL som du kan ange i din webbläsare och se om den fungerar. Det kan vara ett anslutningsproblem, vilket kan indikera en felaktig IP-adress, värdnamn, port eller till och med en brandvägg som blockerar åtkomsten. Det kan vara uppenbart, som ett autentiseringsproblem där du har angett användarnamn, lösenord eller API-nyckel felaktigt. Observera att vissa seedboxar kräver användning av https, port 443 och en URL-bas (avancerade alternativ), istället för nedladdningsklientens verkliga port.

## Testa en nedladdning

Nu ska vi prova en nedladdning, välj en film och gör en manuell sökning. Välj en av dessa filer och försök ladda ner den. Skickas den till nedladdningsklienten? Hamnar den i rätt kategori? Visas den i Aktivitet? Hamnar den i loggarna med trace-nivå under uppgifterna **Kontrollera färdig nedladdning** (Uppdatera övervakade nedladdningar och Bearbeta övervakade nedladdningar-uppgifter) som körs ungefär varje minut? Blir den korrekt analyserad under den uppgiften? Har den köade nedladdningen ett rimligt namn? Eftersom sökningar görs efter ID på vissa indexerare/spårare kan den köa upp en med ett namn som den inte kan känna igen.

## Testa en import

Importproblem bör nästan alltid visas som ett objekt i Aktivitet med en orange ikon som du kan hålla muspekaren över för att se felet. Om de inte visas i Aktivitet är detta problemet du behöver fokusera på först, så gå tillbaka och ta reda på det. De flesta importfel beror på *behörighets*problem, kom ihåg att behörigheterna måste tillåta läs- och skrivåtkomst till nedladdningsmappen. Ibland kan behörigheter i biblioteksmappen också vara felaktiga, så se till att kontrollera båda.

Det är också möjligt att det finns felaktiga sökvägar, även om det är mindre vanligt i normala konfigurationer. Nyckeln för att förstå sökvägsproblem är att veta att får sökvägen till nedladdningen *från* nedladdningsklienten via dess API. Detta blir ett problem i mer unika användningsfall, som när nedladdningsklienten körs på en annan system (kanske till och med ett annat operativsystem\!). Det kan också förekomma i en Docker-konfiguration när volymer inte är korrekt konfigurerade. En fjärrsökvägsmappning är en bra lösning när du inte har kontroll, som i en seedbox-konfiguration. I en Docker-konfiguration är det bättre att fixa sökvägarna.

## Vanliga problem

Här är några vanliga problem.

### Nedladdningsklientens webbgränssnitt är inte aktiverat

Radarr kommunicerar med din nedladdningsklient via dess API och får åtkomst till den via klientens webbgränssnitt. Du måste se till att nedladdningsklientens webbgränssnitt är aktiverat och att den port den använder inte konflikterar med några andra klientportar som används eller portar som används på ditt system.

### SSL används och är felaktigt konfigurerat

Se till att SSL-kryptering inte är aktiverat om du använder både din instans och din nedladdningsklient i ett lokalt nätverk. Se [SSL FAQ-posten](/radarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) för mer information.

### Kan inte se delad mapp på Windows

Standardanvändaren för en Windows-tjänst är `LocalService`, vilket vanligtvis inte har åtkomst till dina delade mappar. Redigera tjänsten och ställ in den så att den körs som din egen användare, se FAQ-posten [varför kan jag inte se mina filer på en fjärrserver](/radarr/faq#why-cant-i-see-my-files-on-a-remote-server) för detaljer.

### Kartlagda nätverksenheter är inte tillförlitliga

Även om kartlagda nätverksenheter som `X:\` är bekväma, är de inte lika tillförlitliga som UNC-sökvägar som `\\server\share` och de är inte tillgängliga före inloggning. Konfigurera din nedladdningsklient (och eventuellt andra program) så att de använder UNC-sökvägar vid behov. Om ditt bibliotek finns på en delad mapp måste du se till att dina rotmappar använder UNC-sökvägar. Om din nedladdningsklient skickar till en delad mapp måste du konfigurera UNC-sökvägar eftersom får nedladdningssökvägen från nedladdningsklienten. Det är okej att behålla dina kartlagda nätverksenheter för personligt bruk, använd dem bara inte för automation.

### Docker och användare, grupp, ägande, behörigheter och sökvägar

Docker lägger till ett ytterligare lager av komplexitet som är lätt att göra fel, men ändå få en konfiguration som fungerar, men har olika problem. Istället för att gå igenom dem här, läs denna wiki-artikel [för dessa automatiseringsprogram och Docker](/docker-guide) som handlar om användare, grupp, ägande, behörigheter och sökvägar. Den är inte specifik för något Docker-system, istället går den igenom saker på en övergripande nivå så att du kan implementera dem i din egen miljö.

### Fjärrsökvägsmappning

Om du har Radarr i Docker och nedladdningsklienten utanför Docker (eller vice versa) eller om programmen körs på olika servrar kan du behöva en fjärrsökvägsmappning.

Loggarna kommer att indikera något liknande.

```none
2022-02-03 14:03:54.3|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /volume3/data/torrents/movies/The.Orville.2022.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Därför finns inte `/volume3/data` inom Radarrs behållare eller är inte åtkomlig.

- [Inställningar => Nedladdningsklienter => Fjärrsökvägsmappningar](/radarr/settings#remote-path-mappings)
- En fjärrsökvägsmappning används när din nedladdningsklient rapporterar en sökväg för slutförda data antingen på en annan server eller på ett sätt som \*Arr inte hanterar den mappen.
- I allmänhet krävs en fjärrsökvägsmappning endast om din nedladdningsklient körs på Linux när \*Arr körs på Windows eller vice versa. En fjärrsökvägsmappning kan också behövas om du blandar Docker- och nativa klienter eller om du använder en fjärrserver.
- En fjärrsökvägsmappning är en DUMB sök/ersättning (där den hittar det FJÄRRAN värdet, ersätter det med LOKALT värde för den angivna värden).
- Om felmeddelandet om en felaktig sökväg inte innehåller det ERSATTADE värdet fungerar inte sökvägsmappningen som du förväntar dig. Den vanliga lösningen är att lägga till och ta bort mappningen.
- [Se TRaSH's handledning för ytterligare information om fjärrsökvägsmappning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Om både \*Arr och din nedladdningsklient är Docker-behållare behövs sällan en fjärrsökvägsmappning. Det rekommenderas att du [granskar Docker-guiden](/docker-guide) och/eller [följer TRaSH's handledning](https://trash-guides.info/hardlinks)
{.is-info}

#### Fjärrmontering eller fjärrsynkronisering (Syncthing)

- Du behöver att synkroniseringen pågår hela tiden när den laddar ner. Och du behöver att den lokala synkroniseringsdestinationen kan vara hårddiskar när \*Arr importerar, vilket innebär samma filsystem och ser ut som det.
  - Synkronisera till en lägre, gemensam mapp som innehåller både ofullständiga och kompletta filer.
  - Synkronisera till en plats som finns på samma filsystem lokalt som ditt bibliotek och ser ut som det (Docker och nätverksdelningar gör det lätt att konfigurera felaktigt)
  - Du vill synkronisera de ofullständiga och kompletta filerna så att när torrentklienten flyttar dem, återspeglas det lokalt och alla filer är redan "där" (även om de fortfarande laddas ner). Sedan vill du använda hårddiskar eftersom även om den importerar innan den är klar kommer de fortfarande att slutföras.
  - På det här sättet synkroniseras det hela tiden medan det laddas ner, sedan flyttar torrentklienten till en undermapp för TV och synkroniseringen återspeglar det. På det sättet är nedladdningarna i stort sett klara när de deklareras som färdiga. Och även om de inte är helt klara, om det är möjligt att skapa hårddiskar betyder det att det fortfarande är okej.
  - (Valfritt - om det är tillämpligt och/eller nödvändigt (t.ex. fjärrusenetklient)) Konfigurera ett anpassat skript som körs vid import/nedladdning/uppgradering för att ta bort den fjärranslutna filen
- Alternativt är en fjärrmontering istället för en fjärrsynkronisering betydligt mindre komplicerad att konfigurera, men vanligtvis långsammare.
  - Montera din fjärrlagring med sshfs eller en annan nätverksfilsystemprotokoll
  - Se till att användaren och gruppen som \*Arr är konfigurerad att köra som har läs- eller skrivåtkomst.
  - Konfigurera en fjärrsökvägsmappning för att hitta det FJÄRRAN sökvägen och ersätta den med motsvarande LOKAL sökväg

### Behörigheter på biblioteksmappen

Loggarna kommer att se ut som

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/media/Movie Name (2010). Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Glöm inte att kontrollera behörigheter och ägande för *målmappen*. Det är lätt att fastna vid nedladdningens ägande och behörigheter och det är *vanligtvis* orsaken till behörighetsrelaterade problem, men det *kan* också vara målet. Kontrollera att målmappen/mapparna finns. Kontrollera att en målfil inte redan finns eller inte kan raderas eller flyttas till papperskorgen. Kontrollera att ägande och behörigheter tillåter att den nedladdade filen kopieras, skapas som hårddisk eller flyttas. Användaren eller gruppen som körs som måste kunna läsa och skriva i rotmappen.

- För Windows-användare kan detta bero på att du kör som en tjänst:
  - Windows-tjänsten körs under kontot 'Local Service', som standard har detta konto inte behörighet att komma åt din användares hemmapp om inte behörigheter har tilldelats manuellt. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemmapp.
  - 'Local Service' har också generellt sett mycket begränsade behörigheter. Det rekommenderas därför att installera appen som en systemfältapplikation om användaren kan förbli inloggad. Alternativet att göra detta erbjuds under installationen. Se FAQ för hur du konverterar från en tjänst till en systemfältapplikation.

- För Synology-användare, se [SynoCommunity's Permissions Article for their Packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- För icke-Windows-användare: Om du använder en NFS-montering, se till att `nolock` är aktiverat.
- Om du använder en SMB-montering, se till att `nobrl` är aktiverat.

### Behörigheter på nedladdningsmappen

Loggarna kommer att se ut som

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/downloads/The.Movie. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Glöm inte att kontrollera behörigheter och ägande för *källan*. Det är lätt att fastna vid målets ägande och behörigheter och det är en *möjlig* orsak till behörighetsrelaterade problem, men det är vanligtvis källan. Kontrollera att källmappen/mapparna finns. Kontrollera att ägande och behörigheter tillåter att den nedladdade filen kopieras/skapas som hårddisk eller kopieras+raderas/flyttas. Användaren eller gruppen som körs som måste kunna läsa och skriva i nedladdningsmappen.

- För Windows-användare kan detta bero på att du kör som en tjänst:
  - Windows-tjänsten körs under kontot 'Local Service', som standard har detta konto inte behörighet att komma åt din användares hemmapp om inte behörigheter har tilldelats manuellt. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemmapp.
  - 'Local Service' har också generellt sett mycket begränsade behörigheter. Det rekommenderas därför att installera appen som en systemfältapplikation om användaren kan förbli inloggad. Alternativet att göra detta erbjuds under installationen. Se FAQ för hur du konverterar från en tjänst till en systemfältapplikation.

- För Synology-användare, se [SynoCommunity's Permissions Article for their Packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- För icke-Windows-användare: Om du använder en NFS-montering, se till att `nolock` är aktiverat.
- Om du använder en SMB-montering, se till att `nobrl` är aktiverat.

### Nedladdningsmappen och biblioteksmappen är inte olika mappar

Nedladdningsklienten bör ladda ner till en mapp som \*Arr kan komma åt och som inte är din rot/biblioteksmapp. Den bör importera från den separata nedladdningsmappen till din biblioteksmapp. Du bör aldrig ladda ner direkt till din rotmapp. Du bör heller inte använda din rotmapp som nedladdningsklientens slutförda mapp eller ofullständiga mapp.

> Din nedladdningsmapp och din rot/biblioteksmapp MÅSTE vara separata
{.is-warning}

### Felaktig kategori

Radarr bör vara konfigurerad att använda en kategori så att den bara försöker behandla sina egna nedladdningar. Det är sällan som en torrent som skickas in av läggs till utan rätt kategori, men det kan hända. Om du lägger till torrents manuellt och vill behandla dem måste de ha rätt kategori. Kategorin kan ställas in när som helst, eftersom försöker behandla nedladdningar varje minut.

### Packade torrents

Loggarna kommer att visa fel som

```none
No files found are eligible for import
```

Om din torrent är packad i `.rar`-filer måste du ställa in uppackning. Vi rekommenderar [Unpackerr](https://github.com/unpackerr/unpackerr) eftersom det gör uppackningen rätt: förhindrar korrupta partiella importeringar och städar upp de uppackade filerna efter importering.

Felet kan också visas om det inte finns någon giltig mediefil i mappen.

### Upprepade nedladdningar

Det finns några orsaker till upprepade nedladdningar, men en av dem är relaterad till anpassade format. Det är möjligt att utgivningsnamnet matchar ett anpassat format, men nedladdningsfilerna gör det inte. Detta leder till en loop där du laddar ner objekten om och om igen eftersom det ser ut som en uppgradering, sedan inte är det, sedan dyker upp igen och ser ut som en uppgradering, sedan inte är det. Beroende på ditt anpassade format kan du lösa detta genom att inkludera det anpassade formatet i ditt namngivningsschema. (Aktivera anpassat format för att inkluderas i namngivningen och lägg sedan till anpassat format i ditt namngivningsschema)

Detta kan också bero på att nedladdningen faktiskt aldrig importeras och sedan saknas från kön, så en ny nedladdning fångas ständigt och importeras aldrig. Se de olika andra vanliga problemen och felsökningsstegen för detta.

### Usenet-nedladdning missar import

Radarr tittar bara på de 60 senaste nedladdningarna i SABnzbd och NZBGet, så om du behåller din historik innebär det att under stora köer med importproblem kan nedladdningar tyst missas och inte importeras. Det bästa sättet att undvika detta är att hålla din historik ren, så att eventuella objekt som fortfarande visas behöver undersökas. Du kan åstadkomma detta genom att aktivera Ta bort under Avslutade och misslyckade nedladdningshanterare. I NZBGet flyttar detta objekt till den *dolda* historiken, vilket är bra. Tyvärr har inte SABnzbd en liknande funktion. Det bästa du kan åstadkomma där är att använda mapp för säkerhetskopiering av nzb.

### Nedladdningsklient rensar objekt

Nedladdningsklienten bör *inte* vara ansvarig för att ta bort nedladdningar. Usenet-klienter bör konfigureras så att de *inte* tar bort nedladdningar från historiken. Torrent-klienter bör konfigureras så att de *inte* tar bort torrents när de är färdiga med att seeda (pausa eller stoppa istället). Detta beror på att Radarr kommunicerar med nedladdningsklienten för att veta vad som ska importeras, så om de *tas bort* finns det inget att importera... även om det finns en mapp full av filer.

För SABnzbd hanteras detta med inställningen Historikbehållning.

### Nedladdningen kan inte matchas med ett biblioteksobjekt

Av olika skäl kan utgåvor inte analyseras när de har hämtats och skickats till nedladdningsklienten. Aktivitet => Alternativ => Visa okända (detta är nu aktiverat som standard i senaste versionerna) visar alla objekt som inte redan ignoreras / har importerats inom kategorin för nedladdningsklienten för \*Arr. Dessa behöver vanligtvis manuellt matchas och importeras.

Orsaker inkluderar:
- Filnamnet har ett `:` på TMDb och TMDb har ingen alternativ titel med ett `-` eller med ett mellanslag som ersätter `:`
- Filnamnet saknar året som krävs
- AKA eller konstiga flera namn; Radarr har begränsat stöd för dessa
- Filnamnet matchar flera filmer
- Utgåvans namn eller utgåvans ID från indexeraren matchar inte filnamnet

Detta kan också inträffa om du har en utgåva i din nedladdningsklient men att det medieobjektet (film/avsnitt/bok/låt) inte finns i applikationen.

### Underliggande anslutning stängdes: Ett oväntat fel inträffade vid en sändning

Detta beror på att indexeraren använder en SSL-protokoll som inte stöds av den aktuella .NET-versionen som finns i [Radarr => System => Status](/radarr/system#status).

### Begäran har tidsgränsen överskridits

Radarr får inget svar från klienten.

```none
    System.NET.WebException: Begäran har tidsgränsen överskridits: ’https://example.org/api?t=caps&apikey=(borttaget) —> System.NET.WebException: Begäran har tidsgränsen överskridits
```

```none
2022-11-01 10:16:54.3|Varning|Newznab|Kan inte ansluta till indexeraren

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En uppgift avbröts.
```

Detta kan också bero på:

- felaktig konfiguration eller användning av en VPN
- felaktig konfiguration eller användning av en proxy
- lokala DNS-problem - Försök att byta till en annan DNS-leverantör
- lokala IPv6-problem - vanligtvis är IPv6 aktiverat, men fungerar inte
- användning av Privoxy och att det är felaktigt konfigurerat

## Problem som inte listas

Du kan också gå igenom några vanliga behörighets- och nätverksfelsökningskommandon [i vår guide](/permissions-and-networking). Annars diskutera problemet med supportteamet på Discord. Om detta är något som kan vara ett vanligt problem, föreslå att det läggs till i wikin.

# Sök indexeringar och spårare

- Om du använder [Prowlarr](/prowlarr) kan du visa [Historik](/prowlarr/history) över alla förfrågningar som Prowlarr har tagit emot och hur de skickades till webbplatserna. Se till att `Parametrar` är aktiverat i Prowlarr Historik => Alternativ. (i)-ikonen ger ytterligare detaljer.

## Öka loggningen till spårnivå

> **Det första steget är att öka loggningen till spårnivå, se [Loggning och loggfiler](#loggning-och-loggfiler) för information om hur du justerar loggningen och söker i loggarna. Du kommer sedan att återskapa problemet och använda loggarna på spårnivå från den tidsramen för att undersöka problemet.** Om någon hjälper dig, lägg kontexten från före/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller liknande webbplats för att visa dem. Det behöver inte vara hela filen och det bör inte *bara* vara felet. Du bör också återskapa problemet när uppgifter som spammar loggfilen inte körs.
{.is-danger}

## Testa en indexerare eller spårare

När du testar en indexerare eller spårare kan du i felsöknings- eller spårloggar hitta den använda URL:en. Ett exempel på ett lyckat test visas nedan, där du kan se att det frågar indexeraren via en specifik URL med specifika parametrar och sedan svaret. Du kan testa denna URL i din webbläsare genom att ersätta `apikey=(borttaget)` med rätt api-nyckel som `apikey=123`. Du kan experimentera med parametrarna om du får ett fel från indexeraren eller se om du har anslutningsproblem om det inte fungerar alls. Efter att du har testat i din egen webbläsare bör du testa från systemet som kör *om* du inte redan har gjort det.

## Testa en sökning

Precis som med indexerare/spårartestet ovan, när du utlöser en sökning med felsöknings- eller spårloggningsnivå kan du få URL:en som används från loggfilerna. Vid testning är det bäst att använda en så smal sökning som möjligt. En manuell sökning är bra eftersom den är specifik och du kan se resultaten i gränssnittet samtidigt som du undersöker loggarna.

I detta test kommer du att leta efter uppenbara fel och köra några enkla tester. Du kan se att sökningen använde URL:en `https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(borttaget)&q=O+Brother+Where+Art+Thou`, som du kan prova själv i en webbläsare efter att ha ersatt `(borttaget)` med din api-nyckel för den indexeraren. Fungerar det? Ser du de förväntade resultaten? I den URL:en kan du se att den har ställt in den specifika kategorin 2000, så om du inte ser förväntade resultat är detta en trolig anledning. Om filmen inte är korrekt kategoriserad på indexeraren måste det åtgärdas. Titta på Manual Search XML Output nedan för att se ett exempel på utdata från en fungerande förfrågan.

- Utdata för manuell sökning i XML-format

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(borttaget)&q=O+Brother+Where+Art+Thou" rel="self" type="application/rss+xml"/>
<title>api.nzbgeek.info</title>
<description>NZBgeek API</description>
<link>http://api.nzbgeek.info/</link>
<language>en-gb</language>
<webMaster>info@nzbgeek.info (NZBgeek)</webMaster>
<category/>
<image>
<url>https://api.nzbgeek.info/covers/nzbgeek.png</url>
<title>api.nzbgeek.info</title>
<link>http://api.nzbgeek.info/</link>
<description>NZBgeek</description>
</image>
<newznab:response offset="0" total="17"/>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=e83b7ae75bca71e92367fab29b036731&apikey=(borttaget)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(borttaget)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=e83b7ae75bca71e92367fab29b036731</comments>
<pubDate>Sat, 10 Jul 2021 08:33:22 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(borttaget)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="e83b7ae75bca71e92367fab29b036731"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=c00a92567863801ab1a4901458ae31ba&apikey=(borttaget)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(borttaget)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=c00a92567863801ab1a4901458ae31ba</comments>
<pubDate>Sun, 28 Mar 2021 10:50:38 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(borttaget)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="c00a92567863801ab1a4901458ae31ba"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=75f5be8b4cd573c2359b638350689f73&apikey=(borttaget)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(borttaget)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=75f5be8b4cd573c2359b638350689f73</comments>
<pubDate>Sun, 28 Jul 2019 00:46:00 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(borttaget)" length="936738000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="936738000"/>
<newznab:attr name="guid" value="75f5be8b4cd573c2359b638350689f73"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(borttaget)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(borttaget)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=a0fe801d9ba0a703db7d2164e996aa1f</comments>
<pubDate>Mon, 14 Aug 2017 15:34:36 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(borttaget)" length="9746182000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="9746182000"/>
<newznab:attr name="guid" value="a0fe801d9ba0a703db7d2164e996aa1f"/>
</item>
</channel>
</rss>
```

***Bilder behövs***

![searches-indexers-and-trackers1.png](/assets/radarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/radarr/searches-indexers-and-trackers2.png)

- Spårloggsnutt

```none
Nedkortad spårlogg för en manuell sökning som behövs
```

- Fullständig spårlogg för en sökning

```none
Hela avsnittet av spårloggen för en manuell sökning som behövs
```

## Vanliga problem

Här är några vanliga problem.

### Spårare behöver RawSearch Caps

- Radarr söker efter `Kikis Delivery Service` men din spårare har bara resultat för `Kiki's Delivery Service`
- Detta beror på att din spårare inte stöder normaliserade sökningar.
- Lösningen är att uppdatera din spårardefinitions sökfunktioner för att ange att den [kräver och stöder `RawSearch`](https://github.com/Radarr/Radarr/issues/4502#issuecomment-981143905)
- Jackett stöder flaggan, men funktionerna måste uppdateras för varje indexerare. Öppna en funktionförfrågan för Jackett för att lägga till denna funktionalitet för din indexerare.
- Prowlarr stöder flaggan, men funktionerna måste uppdateras för varje indexerare. Öppna en funktionförfrågan för Prowlarr för att lägga till denna funktionalitet för din indexerare.

### Media är oövervakad

Filmerna är inte övervakade.

### Felaktiga kategorier

Felaktiga kategorier är förmodligen den vanligaste orsaken till att resultat visas i en manuell sökning av en indexer/tracker, men *inte* i Radarr. Indexern/trackeren *bör* visa kategorin i sökresultaten, vilket bör hjälpa dig att lista ut vad som saknas. Om du använder Jackett eller Prowlarr har varje tracker en lista över specifikt stödda kategorier. Se till att du använder de korrekta kategorierna för Radarr. Många tycker att det är hjälpsamt att ha listan synlig i ett webbläsarfönster medan de redigerar posten.

### Lyckad sökning - Inga resultat returnerade

Du får ett meddelande liknande `Lyckad sökning, men inga resultat returnerades från din indexer. Detta kan vara ett problem med indexern eller dina indexer-kategorinställningar.`

Detta beror på att din indexer inte returnerar några resultat som är inom de kategorier du har konfigurerat för indexer.

### Felaktiga resultat

Ibland returnerar indexrar helt orelaterade resultat, Radarr kommer att mata in parametrar för att begränsa sökningen, men de returnerade resultaten är helt orelaterade. Eller ibland, mestadels relaterade med några felaktiga resultat. Det första är vanligtvis ett indexerproblem och du kan se vilket indexer som orsakar det från spårningsloggen. Du kan inaktivera den indexern och rapportera problemet. Det andra är vanligtvis kategoriserade utgåvor som kan rapporteras på indexer/tracker.

### Saknade resultat

Om du har resultat på webbplatsen som du inte ser i Radarr är ditt problem förmodligen en av flera möjligheter:

- [Felaktiga kategorier - Se ovan](#wrong-categories)
- En ID-baserad sökning (IMDbId, TMDbId, etc.) görs och indexer har inte korrekt kartlagt utgåvorna till det ID:et. Detta är något som bara din indexer kan lösa. De måste se till att utgåvan är kartlagd till de korrekta tillämpliga ID:erna.
- Du söker inte på samma sätt som Radarr söker; Det är mycket troligt att termerna du söker på indexer inte är hur Radarr frågar efter det. Du kan se hur Radarr frågar från spårningsloggen. Textbaserade sökningar kommer generellt att vara i formatet `q=ord%20och%20saker%20här` denna sträng är HTTP-kodad och kan enkelt avkodas med hjälp av valfri HTML-avkodnings/kodningsverktyg online.
- [Se FAQ för hur utländska filmtitlar hanteras och när Radarr skulle söka efter dem](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

### Certifikatvalidering

Du kommer att ansluta till de flesta indexrar/trackers via https, så du måste se till att det fungerar korrekt på ditt system. Det innebär att din tidszon och tid måste vara inställda *korrekt*. Det innebär också att dina systemcertifikat måste vara uppdaterade.

### Träffar begränsade

Om du kör genom en VPN eller proxy kan du konkurrera med 10-tals, 100-tals eller 1000-tals andra personer som alla försöker använda tjänster som , theXEM och/eller dina indexrar och trackers. Begränsning av hastighet och DDOS-skydd görs ofta efter IP-adress och din VPN/proxy-utgångspunkt är *en* IP-adress. Om du inte befinner dig i ett förtryckande land som Kina, Australien eller Sydafrika behöver du inte använda VPN/proxy .

Rarbg har en tendens att ha någon form av hastighetsbegränsning inom deras API och visas som att svara utan resultat.

### IP-blockering

På samma sätt som hastighetsbegränsningar kan vissa indexrar - som Nyaa - helt enkelt blockera en IP-adress. Detta är vanligtvis halvpermanent och lösningen är att få en ny IP från din internetleverantör eller VPN-leverantör.

### Året matchar inte

- [Se detta FAQ-inlägg](/radarr/faq#how-does-radarr-determine-the-year-of-a-movie)
  - Radarr hämtar metadata från TMDb
  - Radarr använder året för den äldsta **biografiska premiär** och det äldsta **premiär** för matchning
- I vissa fall har filmen skjutits upp eller ändrats och året som används av utgivningsgrupperna matchar varken det äldsta premiäråret eller det äldsta biografiska premiäråret. I dessa situationer måste du hämta och importera manuellt.

### Saknat år

Radarr kommer inte att hämta en utgåva om utgåvans namn inte innehåller ett år. Detta är en dålig utgåva och kan bara hämtas manuellt. Detta är något som ofta glöms bort när man försöker lista ut varför en film inte hämtades som förväntat.

### Användning av Jackett /all slutpunkt

Jackett `/all` slutpunkten är bekväm, men det är den enda fördelen. Allt annat kan orsaka problem, så det krävs att varje tracker läggs till separat. Alternativt kan du kolla in Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

[Till och med Jackett säger att /all bör undvikas och inte användas.](https://github.com/Jackett/Jackett#aggregate-indexers)

Att använda all slutpunkt har inga fördelar (förutom minskad hantering), bara nackdelar:

- du förlorar kontrollen över indexer-specifika inställningar (kategorier, söklägen, etc.)
- blandning av söklägen (IMDB, fråga, etc.) kan ge lågkvalitativa resultat
- indexer-specifika kategorier (\>= 100000) kan inte användas.
- långsamma indexrar kommer att sakta ner det totala resultatet
- totala resultat är begränsade till 1000

Genom att lägga till varje indexer separat kan du finjustera kategorierna för varje indexer, vilket kan vara ett problem med `/all` slutpunkten om fel kategori orsakar fel på vissa trackers. I , är varje indexer begränsad till 1000 resultat om sidindelning stöds eller 100 om det inte stöds, vilket innebär att ju fler trackers du lägger till i Jackett, desto mer sannolikt är det att du klipper resultat. Slutligen, om *en* av trackrarna i `/all` returnerar ett fel, kommer att inaktivera den och nu får du inga resultat.

### Användning av NZBHydra2 som en enda post

Att använda NZBHydra2 som en enda indexerpost (dvs. 1 NZBHydra2-post i Radarr för många indexrar i NZBHydra2) istället för flera (dvs. många NZBHydra2-poster i Radarr för många indexrar i NZBHydra2) har samma problem som noterats ovan med Jacketts `/all` slutpunkt.

### Problem som inte listas

Du kan också gå igenom några vanliga behörighets- och nätverkstestkommandon [i vår guide](/permissions-and-networking). Annars kan du diskutera med supportteamet på Discord. Om detta är något som kan vara ett vanligt problem, föreslå att lägga till det i wikin.

## Fel

Detta är några av de vanliga felen du kan se när du lägger till en indexer

### Underliggande anslutningen stängdes: Ett oväntat fel inträffade vid en sändning

Detta beror på att indexern använder en SSL-protokoll som inte stöds av den aktuella .NET-versionen som finns i [Radarr => System => Status](/radarr/system#status).

### Begäran har tidsgränsen överskridits

Radarr får inget svar från indexern.

```none
    System.NET.WebException: Begäran har tidsgränsen överskridits: ’https://example.org/api?t=caps&apikey=(borttaget) —> System.NET.WebException: Begäran har tidsgränsen överskridits
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
- användning av Privoxy och att det är felaktigt konfigurerat

### Problem som inte listas

Du kan också gå igenom några vanliga behörighets- och nätverkstestkommandon [i vår guide](/permissions-and-networking). Annars kan du diskutera med supportteamet på Discord. Om detta är något som kan vara ett vanligt problem, föreslå att lägga till det i wikin.