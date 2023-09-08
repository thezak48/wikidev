---
title: Sonarr Felsökning
description: 
published: true
date: 2023-07-24T19:54:54.368Z
tags: sonarr, felsökning
editor: markdown
dateCreated: 2021-06-20T19:13:01.108Z
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
    - [En eller flera förväntade avsnitt i utgåvan importerades inte eller saknas](#en-eller-flera-förväntade-avsnitt-i-utgåvan-importerades-inte-eller-saknas)
    - [Använder Sonarr v2](#använder-sonarr-v2)
    - [Webbgränssnittet för nedladdningsklienten är inte aktiverat](#webbgränssnittet-för-nedladdningsklienten-är-inte-aktiverat)
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
      - [Hittade matchande serier via hämtningshistorik, men serien matchades efter seriens ID. Automatisk importering är inte möjlig](#hittade-matchande-serier-via-hämtningshistorik-men-serien-matchades-efter-seriens-id-automatisk-importering-är-inte-möjlig)
    - [Avsnittsnamn är TBA](#avsnittsnamn-är-tba)
    - [Anslutningstidsgräns överskreds](#anslutningstidsgräns-överskreds)
  - [Problem som inte listas](#problem-som-inte-listas)
- [Sökning, indexerare och spårare](#sökning-indexerare-och-spårare)
  - [Öka loggningsnivån till spårning](#öka-loggningsnivån-till-spårning)
  - [Testa en indexerare eller spårare](#testa-en-indexerare-eller-spårare)
  - [Testa en sökning](#testa-en-sökning)
  - [Vanliga problem](#vanliga-problem-1)
    - [Indexerare söks inte](#indexerare-söks-inte)
    - [Dåligt namngivna utgåvor](#dåligt-namngivna-utgåvor)
    - [Spårare behöver RawSearch Caps](#spårare-behöver-rawsearch-caps)
    - [Serien behöver ett alias](#serien-behöver-ett-alias)
    - [Serien behöver en XEM-mappning](#serien-behöver-en-xem-mappning)
    - [Felaktig serietyp](#felaktig-serietyp)
      - [Daglig](#daglig)
      - [Standard](#standard)
      - [Anime](#anime)
    - [Media är oövervakad](#media-är-oövervakad)
    - [Förfrågan lyckades - inga resultat returnerades](#förfrågan-lyckades-inga-resultat-returnerades)
    - [Felaktiga kategorier](#felaktiga-kategorier)
    - [Felaktiga resultat](#felaktiga-resultat)
    - [Saknade resultat](#saknade-resultat)
    - [Certifikatvalidering](#certifikatvalidering)
    - [Träffar begränsningar för hastighet](#träffar-begränsningar-för-hastighet)
    - [IP-blockering](#ip-blockering)
    - [Användning av Jackett /all-endpoint](#användning-av-jackett-all-endpoint)
    - [Användning av NZBHydra2 som enskild post](#användning-av-nzbhydra2-som-enskild-post)
    - [Indexerare söks inte](#indexerare-söks-inte)
    - [Jackett manuell sökning hittar fler resultat](#jackett-manuell-sökning-hittar-fler-resultat)
    - [Releaseprofiler respekteras inte](#releaseprofiler-respekteras-inte)
    - [Problem som inte listas](#problem-som-inte-listas-1)
  - [Fel](#fel)
    - [Det underliggande anslutningen stängdes: Ett oväntat fel inträffade vid en sändning](#det-underliggande-anslutningen-stängdes-ett-oväntat-fel-inträffade-vid-en-sändning)
    - [Begäran tog för lång tid](#begäran-tog-för-lång-tid)
    - [Problem som inte listas](#problem-som-inte-listas-2)

# Be om hjälp

Behöver du hjälp? Det är okej, alla behöver hjälp ibland. Du kan få hjälp i realtid via chatt på

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiell Sonarr Discord*](https://discord.sonarr.tv/)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiell Sonarr Subreddit*](https://reddit.com/r/sonarr)
{.links-list}

Men innan du går dit och postar, se till att din hjälpförfrågan är så bra som möjligt. Beskriv tydligt problemet och beskriv kortfattat din konfiguration, inklusive saker som ditt OS/distribution, version av .net/Mono, version av Sonarr, nedladdningsklient och dess version. **Om du använder [Docker](https://www.docker.com/) ska du köra igenom [Docker Guide](/docker-guide) först eftersom det kommer att lösa vanliga och frekventa problem med sökvägar/behörigheter. Annars se till att du har en [docker compose](/docker-guide#docker-compose) till hands. [Så här genererar du en Docker Compose](https://trash-guides.info/compose)** Berätta vad du redan har försökt, vad du har tittat på. Använd avsnittet [Loggning och loggfiler](#loggning-och-loggfiler) för att öka loggningsnivån till spårning, återskapa problemet, lägg upp den relevanta kontexten på en pastebin och inkludera en länk till den i ditt inlägg. Du kan till och med inkludera några skärmbilder för att tydliggöra problemet.

Ju mer vi vet, desto lättare är det att hjälpa dig.

# Loggning och loggfiler

Det kan vara fördelaktigt att också granska vanliga felsökningsproblem:
- [Vanliga problem med nedladdningar och importering](#vanliga-problem)
- [Vanliga problem med sökning, indexerare och spårare](#vanliga-problem-1)
{.links-list}

Om du ombeds att lämna felsökningsloggar kommer dina loggar att innehålla `debug` och om du ombeds att lämna spårningsloggar kommer dina loggar att innehålla `trace`. Om de loggar du tillhandahåller inte innehåller något av dessa, är de inte de efterfrågade loggarna.

- Undvik att dela hela loggfilen om du inte ombeds att göra det.
- Ladda inte upp loggar direkt till Discord eller klistra in dem som väggar av text, om du inte ombeds att göra det.
- Dela inte loggarna som en bilaga, en zip-fil eller något annat än text som delas via de tjänster som anges nedan.

För att tillhandahålla bra och användbara loggar för delning:

> Se till att det inte körs någon spamig uppgift, som t.ex. en RSS-uppdatering
{.is-warning}

1. [Öka loggningsnivån till spårning (Inställningar => Allmänt => Loggnivå eller Redigera konfigurationsfilen)](#spår-felsökningsloggar)
2. [Rensa loggar (System => Loggar => Rensa loggar eller Radera alla loggar i loggmappen)](#rensa-loggar)
3. Återskapa problemet (Gör om det som orsakar problem)
4. [Öppna spårningsloggfilen (sonarr.trace.txt) via gränssnittet eller loggfilen](#standardplats-för-loggar) på filsystemet och hitta den relevanta kontexten
5. Kopiera en stor del före problemet, själva problemet och en stor del efter problemet.
6. Använd [Gist](https://gist.github.com/), [0bin (**Se till att inaktivera färgläggning**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntus Pastebin](https://pastebin.ubuntu.com/) eller liknande webbplatser - undvik de som anges nedan - för att dela de kopierade loggarna ovan

**Varningar:**
- **Använd inte [pastebin.com](https://pastebin.com) eftersom deras filter har en tendens att blockera loggarna.
- Använd inte [pastebin.pl](https://pastebin.pl) eftersom deras webbplats ofta inte är tillgänglig.
- Använd inte [JustPasteIt](https://justpaste.it/) eftersom deras webbplats inte underlättar granskning av loggar.
- Ladda inte upp din logg som en fil.
- Ladda inte upp och dela dina loggar via Google Drive, Dropbox eller någon annan webbplats som inte anges ovan.
- Arkivera inte (zip, tar (tarball), 7zip, etc.) dina loggar.
- Dela inte konsolresultat, utdata från Docker-kontainrar eller något annat än de angivna applikationsloggarna.

**Viktig anteckning:**
- När du använder [0bin](https://0bin.net/), se till att inaktivera färgläggning och bränn inte efter att ha läst.

- Alternativt, om du letar efter en specifik post i en gammal loggfil men inte är säker på vilken, kan du använda N++. Du kan använda Notepad++ "Sök i filer"-funktion för att söka i gamla loggfiler vid behov.
- **Endast Unix:** Alternativt, om du letar efter en specifik post i en gammal loggfil men inte är säker på vilken, kan du använda grep. Till exempel, om du vill hitta information om filmen/serien/boken/låten/indexeraren "Shooter" kan du köra följande kommando `grep -inr -C 100 -e 'Shooter' /sökväg/till/loggar/*.trace*.txt` Om din [Appdata-katalog](/sonarr/appdata-directory) finns i din hemkatalog kör du: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flaggor har följande funktioner
    * -i: ignorera skiftläge
    * -n: visa radnummer
    * -r: sök rekursivt i alla filer i sökvägen
    * -C: ange antal rader före och efter den hittade raden
    * -e: mönstret att söka efter

```

## Standardplats för loggar

Loggfilerna finns i Sonarrs [Appdata-katalog](/sonarr/appdata-directory), i mappen logs/. Du kan också komma åt loggfilerna från gränssnittet på System => Loggar => Filer.

> Observera: Loggarna ("Händelser") i gränssnittet är inte samma som loggfilerna och är inte lika användbara. Om du ombeds att lämna loggar, kopiera/klipp in från loggfilerna och inte från tabellen.
{.is-info}

## Plats för uppdateringsloggar

Uppdateringsloggarna finns i Sonarrs [Appdata-katalog](/sonarr/appdata-directory), i mappen UpdateLogs/.

## Dela loggar

Loggarna kan vara långa och svåra att läsa som en del av ett forum- eller Reddit-inlägg och de är spamiga i Discord, så använd [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller någon annan liknande pastebin-webbplats. Hela filen behövs vanligtvis inte, bara en bra mängd kontext före och efter problemet/felmeddelandet. Glöm inte att vänta på att spamiga uppgifter som en RSS-synkronisering eller biblioteksuppfräschning ska slutföras.

## Spår-/felsökningsloggar

Du kan ändra loggningsnivån under Inställningar => Allmänt => Loggning. Sonarr behöver inte startas om för att ändringen ska träda i kraft. Denna ändring påverkar endast loggfilerna, inte loggningsdatabasen. De senaste felsöknings-/spårningsloggarna heter `sonarr.debug.txt` respektive `sonarr.trace.txt`.

Om du inte kan komma åt gränssnittet för att ställa in loggningsnivån kan du göra det genom att redigera config.xml i AppData-katalogen genom att ändra värdet för LogLevel till Debug eller Trace istället för Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Rensa loggar

Du kan rensa loggfilerna och loggdatabasen direkt från gränssnittet, under System => Loggar => Filer och System => Loggar => Radera (papperskorgsikonen)

# Flera loggfiler

Sonarr använder rullande loggfiler som är begränsade till 1 MB vardera. Den aktuella loggfilen är alltid `sonarr.txt`, för de andra filerna är `sonarr.0.txt` den näst nyaste (ju högre nummer desto äldre är den). Denna loggfil innehåller `fatal`, `error`, `warn` och `info`-poster.

När felsökningsloggnivån är aktiverad kommer det att finnas ytterligare rullande loggfiler `sonarr.debug.txt`. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info` och `debug`-poster. De täcker vanligtvis en period på 40 timmar.

När spårningsloggnivån är aktiverad kommer det att finnas ytterligare rullande loggfiler `sonarr.trace.txt`. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info`, `debug` och `trace`-poster. På grund av spårningsloggnivåns detaljnivå täcker de endast ett par timmar som mest.

# Återställning efter misslyckad uppdatering

Vi gör allt vi kan för att förhindra problem vid uppgradering, men om de ändå uppstår kommer detta att guida dig genom stegen för att återställa din installation.

## Identifiera problemet

Det bästa stället att titta när programmet inte startar efter en uppdatering är att granska [uppdateringsloggar](#plats-för-uppdateringsloggar) och se om uppdateringen slutfördes framgångsrikt. Om dessa inte har något problem är nästa steg att titta på dina vanliga programloggfiler, innan du försöker starta om, använd [Loggning](/sonarr/settings#logging) och [Loggfiler](/sonarr/system#log-files) för att hitta dem och öka loggningsnivån.

### Migrationsproblem

- Migrationsfel kommer inte att vara identiska, men här är ett exempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Behörighetsproblem

- Behörighetsproblem beror på att programmet inte kan komma åt de relevanta temporära mapparna och/eller appens binära mapp. Åtgärda behörigheterna så att användaren/gruppen som programmet körs som har lämplig åtkomst.

- Synology-användare kan stöta på detta Synology-bugg `Access to the path '/proc/{some number}/maps is denied`

- Synology-användare kan också stöta på att det inte finns tillräckligt med utrymme i `/tmp` på vissa NAS-enheter. Du måste ange en annan `/tmp`-sökväg för appen. Se SynoCommunity eller andra Synology-supportkanaler för hjälp med detta.

## Lösning av problemet

Vid en migrationsfråga kan du inte göra mycket omedelbart. Om problemet är specifikt för dig (eller om det ännu inte finns några inlägg), skapa ett inlägg på [vår subreddit](https://reddit.com/r/sonarr) eller besök vår [discord](https://discord.sonarr.tv/). Om det finns andra med samma problem kan du vara säker på att vi arbetar med det.

> Se till att du inte har försökt använda en databas från `develop` i den stabila versionen. Att byta grenar rekommenderas inte.{.is-info}

### Behörighetsproblem

- Åtgärda behörigheterna för att säkerställa att användaren/gruppen som programmet körs som kan få åtkomst (läsa och skriva) till både `/tmp` och installationsmappen för programmet.

- För Synology-användare som upplever problem med `/proc/###/maps` bör stoppa Sonarr eller de andra \*Arr-applikationerna och uppdatera lösa detta. Detta är ett problem med SynoCommunity-paketet.

### Manuell uppgradering

Hämta den senaste versionen från vår webbplats.

Installera uppdateringen (.exe) eller extrahera (.zip) innehållet över din befintliga installation och kör Sonarr som vanligt.

# Nedladdningar och import

Nedladdning och import är där *de flesta* personer upplever problem. Från ett övergripande perspektiv måste Sonarr kunna kommunicera med din nedladdningsklient och ha åtkomst till de filer den laddar ner. Det finns ett stort antal nedladdningsklienter som stöds och ännu *fler* olika konfigurationer. Det innebär att medan det finns några *vanliga* konfigurationer, finns det ingen *rätt* konfiguration och varje persons konfiguration kan vara lite annorlunda.

> **Det första steget är att öka loggningsnivån till Trace, se [Logging and Log Files](#logging-and-log-files) för detaljer om hur du justerar loggningsnivån och söker i loggarna. Du kommer sedan att återskapa problemet och använda loggarna med trace-nivå från den tidsperioden för att undersöka problemet.**
> Om någon hjälper dig, lägg in sammanhanget före/efter på en [pastebin](https://0bin.net), [Gist](https://gist.com) eller liknande webbplats för att visa dem.
> Det behöver inte vara hela filen och det bör inte *bara* vara felet. Du bör också återskapa problemet när uppgifter som spamar loggfilen inte körs.
{.is-danger}

När du söker hjälp, se till att läsa [begära hjälp](#begära-hjälp) så att du kan ge oss de detaljer vi behöver.

## Testa nedladdningsklienten

Se till att din nedladdningsklient(er) körs. Börja med att testa nedladdningsklienten, om den inte fungerar kan du se detaljer i loggarna med trace-nivå. Du bör hitta en URL som du kan ange i din webbläsare och se om den fungerar. Det kan vara ett anslutningsproblem, vilket kan indikera en felaktig IP-adress, värdnamn, port eller till och med en brandvägg som blockerar åtkomsten. Det kan vara uppenbart, som ett autentiseringsproblem där du har angett användarnamn, lösenord eller API-nyckel felaktigt.

## Testa en nedladdning

Nu ska vi prova en nedladdning, välj en episod för en serie och gör en manuell sökning. Välj en av dessa filer och försök ladda ner den. Skickas den till nedladdningsklienten? Hamnar den i rätt kategori? Visas den i Aktivitet? Hamnar den i loggarna med trace-nivå under uppgifterna **Kontrollera färdig nedladdning** (Uppdatera övervakade nedladdningar och Bearbeta övervakade nedladdningar) som körs ungefär varje minut? Blir den korrekt tolkad under den uppgiften? Har den nedladdning som är i kö ett rimligt namn? Eftersom sökningar görs med ID på vissa indexerare/spårare kan den sätta en nedladdning i kö med ett namn som den inte kan känna igen.

## Testa en import

Importproblem bör nästan alltid visas som ett objekt i Aktivitet med en orange ikon som du kan hålla över för att se felet. Om de inte visas i Aktivitet är detta problemet du behöver fokusera på först, så gå tillbaka och ta reda på det. De flesta importfel beror på *behörighets*problem, kom ihåg att Sonarr måste kunna läsa och skriva i nedladdningsmappen. Ibland kan behörigheter i biblioteksmappen också vara felaktiga, så se till att kontrollera båda.

Det är också möjligt att det finns felaktiga sökvägar, även om det är mindre vanligt i normala konfigurationer. Nyckeln för att förstå sökvägsproblem är att veta att får sökvägen till nedladdningen *från* nedladdningsklienten via dess API. Detta blir ett problem i mer unika användningsfall, som när nedladdningsklienten körs på en annan system (kanske till och med ett annat operativsystem\!). Det kan också förekomma i en Docker-konfiguration när volymer inte är korrekt konfigurerade. En fjärrsökvägsmappning är en bra lösning när du inte har kontroll, som i en seedbox-konfiguration. I en Docker-konfiguration är det bättre att fixa sökvägarna.

## Vanliga problem

Här är några vanliga problem.

### En eller flera förväntade avsnitt i utgåvan importerades inte eller saknas

- Om alla avsnitt importerades är den vanligaste orsaken att en säsongspaket laddades ner, men inte innehåller alla avsnitt i säsongen. Klicka på `X` för att ta bort och ignorera utgåvan.
- För alla andra problem importerades en eller flera avsnitt inte. Granska informationen i användargränssnittet och andra vanliga problem.

### Använder Sonarr v2

Sonarr v2 har nått slutet av livet och stöds inte sedan 3/2021. Den är inte kompatibel med qBittorrent v4.3.0 eller senare. Uppgradera till Sonarr v3.

### Nedladdningsklientens webbgränssnitt är inte aktiverat

Sonarr kommunicerar med din nedladdningsklient via dess API och får åtkomst till den via klientens webbgränssnitt. Du måste se till att klientens webbgränssnitt är aktiverat och att porten den använder inte konflikterar med några andra klientportar som används eller portar som används på ditt system.

### SSL används och är felaktigt konfigurerat

Se till att SSL-kryptering inte är aktiverat om du använder både din instans och din nedladdningsklient i ett lokalt nätverk. Se [SSL FAQ-inlägget](/sonarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) för mer information.

### Kan inte se delning på Windows

Standardanvändaren för en Windows-tjänst är `LocalService` som vanligtvis inte har åtkomst till dina delningar. Redigera tjänsten och ställ in den att köras som din egen användare, se FAQ-inlägget [why can’t see my files on a remote server](/sonarr/faq#why-cant-i-see-my-files-on-a-remote-server) för detaljer.

### Kartlagda nätverksenheter är inte tillförlitliga

Även om kartlagda nätverksenheter som `X:\` är bekväma, är de inte lika tillförlitliga som UNC-sökvägar som `\\server\share` och de är inte tillgängliga före inloggning. Konfigurera dina nedladdningsklient(er) så att de använder UNC-sökvägar vid behov. Om ditt bibliotek finns på en delning, se till att dina rotmappar använder UNC-sökvägar. Om din nedladdningsklient skickar till en delning är det där du behöver konfigurera UNC-sökvägar eftersom får nedladdningssökvägen från nedladdningsklienten. Det är okej att behålla dina kartlagda nätverksenheter för personligt bruk, använd dem bara inte för automation.

### Docker och användare, grupp, ägande, behörigheter och sökvägar

Docker lägger till ett ytterligare lager av komplexitet som är lätt att göra fel, men ändå få en konfiguration som fungerar, men har olika problem. Istället för att gå igenom dem här, läs denna wiki-artikel [för dessa automatiseringsprogram och Docker](/docker-guide) som handlar om användare, grupp, ägande, behörigheter och sökvägar. Den är inte specifik för något Docker-system, istället går den igenom saker på en övergripande nivå så att du kan implementera dem i din egen miljö.

### Fjärrsökvägsmappning

Om du har Sonarr i Docker och nedladdningsklienten utanför Docker (eller vice versa) eller har programmen på olika servrar kan du behöva en fjärrsökvägsmappning.

Loggarna kommer att se ut så här

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/torrents/tv/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Så `/volume3/data` finns inte inom Sonarrs behållare eller är inte åtkomlig.

- [Inställningar => Nedladdningsklienter => Fjärrsökvägsmappningar](/sonarr/settings#remote-path-mappings)
- En fjärrsökvägsmappning används när din nedladdningsklient rapporterar en sökväg för slutförda data antingen på en annan server eller på ett sätt som \*Arr inte hanterar för den mappen.
- Generellt sett krävs en fjärrsökvägsmappning endast om din nedladdningsklient körs på Linux när \*Arr körs på Windows eller vice versa. En fjärrsökvägsmappning kan också behövas om du blandar Docker och nativa klienter eller om du använder en fjärrserver.
- En fjärrsökvägsmappning är en DUMB sök/ersättning (där den hittar det FJÄRR-värdet, ersätter det med LOKALT-värdet för den angivna värden).
- Om felmeddelandet om en felaktig sökväg inte innehåller det ERSATTADE värdet fungerar inte sökvägsmappningen som du förväntar dig. Den vanliga lösningen är att lägga till och ta bort mappningen.
- [Se TRaSH's handledning för ytterligare information om fjärrsökvägsmappning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Om både \*Arr och din nedladdningsklient är Docker-behållare behövs sällan en fjärrsökvägsmappning. Det rekommenderas att du [granskar Docker-guiden](/docker-guide) och/eller [följer TRaSH's handledning](https://trash-guides.info/hardlinks)
{.is-info}

#### Fjärrmontering eller fjärrsynkronisering (Syncthing)

- Du behöver att det synkroniseras hela tiden medan det laddar ner. Och du behöver att den lokala synkroniseringsdestinationen kan vara hårddiskar när \*Arr importerar, vilket innebär samma filsystem och ser ut som det.
  - Synkronisera till en lägre, gemensam mapp som innehåller både ofullständiga och kompletta filer.
  - Synkronisera till en plats som finns på samma filsystem lokalt som ditt bibliotek och ser ut som det (Docker och nätverksdelningar gör det lätt att konfigurera felaktigt).
  - Du vill synkronisera de ofullständiga och kompletta filerna så att när torrentklienten flyttar dem, återspeglas det lokalt och alla filer är redan "där" (även om de fortfarande laddas ner). Sedan vill du använda hårddiskar eftersom även om de importeras innan de är klara kommer de fortfarande att slutföras.
  - På det här sättet synkroniseras det hela tiden medan det laddar ner, sedan flyttar torrentklienten till undermappen för tv och synkroniseringen återspeglar det. På det sättet är nedladdningarna i stort sett klara när de deklareras som färdiga. Och även om de inte är helt klara, innebär möjligheten till hårddiskar att det fortfarande är okej.
  - (Valfritt - om det är tillämpligt och/eller nödvändigt (t.ex. fjärrusenetklient)) Konfigurera ett anpassat skript som körs vid import/nedladdning/uppgradering för att ta bort den fjärranslutna filen
- Alternativt är en fjärrmontering istället för en fjärrsynkroniseringskonfiguration betydligt mindre komplicerad att konfigurera, men vanligtvis långsammare.
  - Montera din fjärrlagring med sshfs eller en annan nätverksfilsystemprotokoll.
  - Se till att användaren och gruppen som \*Arr är konfigurerad att köra som har läs- eller skrivåtkomst.
  - Konfigurera en fjärrsökvägsmappning för att hitta det FJÄRR-värdet och ersätta det med det LOKALA motsvarande

### Behörigheter på biblioteksmappen

Loggarna kommer att se ut så här

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/tv/The Orville/Season 03/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Glöm inte att kontrollera behörigheter och ägande för *målet*. Det är lätt att fastna vid nedladdningens ägande och behörigheter och det är *vanligtvis* orsaken till behörighetsrelaterade problem, men det *kan* också vara målet. Kontrollera att målmappen/mapparna finns. Kontrollera att en målfil inte redan finns eller inte kan raderas eller flyttas till papperskorgen. Kontrollera att ägande och behörigheter tillåter att den nedladdade filen kopieras, hårdlänkas eller flyttas. Användaren eller gruppen som körs som måste kunna läsa och skriva i rotmappen.

- För Windows-användare kan detta bero på att det körs som en tjänst:
  - Windows-tjänsten körs under kontot 'Local Service', som som standard inte har behörighet att komma åt din användares hemkatalog om inte behörigheter har tilldelats manuellt. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemkatalog.
  - 'Local Service' har också generellt sett mycket begränsade behörigheter. Det är därför rekommenderat att installera appen som en systemfältapplikation om användaren kan förbli inloggad. Alternativet att göra detta tillhandahålls under installationen. Se FAQ för hur du konverterar från en tjänst till en systemfältapplikation.

- För Synology-användare hänvisas till [SynoCommunity's Permissions Article for their Packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- För icke-Windows-användare: Om du använder en NFS-montering, se till att `nolock` är aktiverat.
- Om du använder en SMB-montering, se till att `nobrl` är aktiverat.

### Behörigheter på nedladdningsmappen

Du kommer att se ett fel liknande följande

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES.1/a4187f6c3c4445f98e85da52b83c84e8.mkv. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

eller

```none
2022-02-03 10:40:41.8|Warn|Sabnzbd|[Resident.Alien.S02E02.720p.WEB.H264-CAKES] Error occurred while trying to delete data from '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES/'.
 
[v3.0.6.1342] System.UnauthorizedAccessException: Access to the path '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES' is denied.
```

Glöm inte att kontrollera behörigheter och ägande för *källan*. Det är lätt att fastna vid målets ägande och behörigheter och det är en *möjlig* orsak till behörighetsrelaterade problem, men det är vanligtvis källan. Kontrollera att källmappen/mapparna finns. Kontrollera att ägande och behörigheter tillåter att den nedladdade filen kopieras/hårdlänkas eller kopieras+raderas/flyttas. Användaren eller gruppen som Sonarr körs som måste kunna läsa och skriva i nedladdningsfilerna.

- För Windows-användare kan detta bero på att det körs som en tjänst:
  - Windows-tjänsten körs under kontot 'Local Service', som som standard inte har behörighet att komma åt din användares hemkatalog om inte behörigheter har tilldelats manuellt. Detta är särskilt relevant när du använder nedladdningsklienter som är konfigurerade att ladda ner till din hemkatalog.
  - 'Local Service' har också generellt sett mycket begränsade behörigheter. Det är därför rekommenderat att installera appen som en systemfältapplikation om användaren kan förbli inloggad. Alternativet att göra detta tillhandahålls under installationen. Se FAQ för hur du konverterar från en tjänst till en systemfältapplikation.

- För Synology-användare hänvisas till [SynoCommunity's Permissions Article for their Packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- För icke-Windows-användare: Om du använder en NFS-montering, se till att `nolock` är aktiverat.
- Om du använder en SMB-montering, se till att `nobrl` är aktiverat.

### Nedladdningsmappen och biblioteksmappen är inte olika mappar

- Nedladdningsklienten bör ladda ner till en mapp som är åtkomlig av \*Arr och som inte är din rot-/biblioteksmapp; du bör importera från den separata nedladdningsmappen till din biblioteksmapp.
- Du bör aldrig ladda ner direkt till din rotmapp. Du bör heller inte använda din rotmapp som nedladdningsklients slutförda mapp eller ofullständiga mapp.
- [**Detta kommer också att orsaka en hälsokontroll i System**](/sonarr/system#downloading-into-root-folder)
- Inom applikationen definieras en rotmapp som den konfigurerade mediebiblioteksmappen. Detta är inte rotmappen för en montering. Din nedladdningsklient har en ofullständig eller slutförd mapp (eller flyttar slutförda nedladdningar) till din rot (biblioteks) mapp. Detta orsakar ofta problem och rekommenderas inte. För att åtgärda detta, ändra din nedladdningsklient så att den inte placerar nedladdningar i din rotmapp. Observera att 'placering' även inkluderar om din nedladdningsklients kategori är inställd på din rotmapp eller om NZBGet/SABnzbd har sorteringsfunktionen aktiverad och sorterar till din rotmapp. Observera att denna kontroll tittar på alla definierade/konfigurerade rotmappar som har lagts till, inte bara rotmappar som för närvarande används. Med andra ord bör inte mappen där din nedladdningsklient laddar ner eller flyttar slutförda nedladdningar till vara samma mapp som du har konfigurerat som din rot-/biblioteks-/slutliga mediadestinationsmapp i \*Arr-applikationen.
- Konfigurerade rotmappar (även kända som biblioteksmappar) finns under [Inställningar => Mediehantering => Rotmappar](/sonarr/settings/#root-folders)
- Ett exempel är om dina nedladdningar hamnar i `\data\downloads`, då har du en rotmapp som är inställd som `\data\downloads`.
- Det rekommenderas att använda sökvägar som `\data\media\` för din rotmapp/bibliotek och `\data\downloads\` för dina nedladdningar.

> Din nedladdningsmapp och din rot-/biblioteksmapp MÅSTE vara separata
{.is-warning}

### Felaktig kategori

Sonarr bör vara konfigurerad att använda en kategori så att den bara försöker bearbeta sina egna nedladdningar. Det är sällan som en torrent som läggs till manuellt inte har rätt kategori, men det kan hända. Om du lägger till torrents manuellt och vill bearbeta dem måste de ha rätt kategori. Kategorin kan ställas in när som helst, eftersom Sonarr försöker bearbeta nedladdningar varje minut.

### Packade torrents

Loggarna kommer att visa fel som

```none
Inga filer hittades som är berättigade till import
```

Om din torrent är packad i `.rar`-filer måste du ställa in uppackning. Vi rekommenderar [Unpackerr](https://github.com/unpackerr/unpackerr) eftersom det gör uppackningen rätt: förhindrar korrupta partiella importeringar och städar upp de uppackade filerna efter importering.

Felet kan också visas om det inte finns någon giltig mediefil i mappen.

### Upprepade nedladdningar

Det finns några orsaker till upprepade nedladdningar, men en är relaterad till begränsningen av indexer i utgivningsprofiler. Eftersom indexeraren *inte* lagras med datan är alla `preferred word`-poäng *noll* för media i ditt bibliotek, men under "RSS" och sökning kommer de att tillämpas. På samma sätt gäller begränsningarna `must contain` eller `must-not` bara för den indexeraren; allt annat är fritt fram. Detta leder till en loop där du laddar ner objekten om och om igen eftersom det ser ut som en uppgradering, sedan inte är det, sedan dyker upp igen och ser ut som en uppgradering, sedan inte är det. Begränsa inte din utgivningsprofil till en indexerare.

Detta kan också bero på att nedladdningen faktiskt aldrig importeras och sedan saknas i kön, så en ny nedladdning hämtas ständigt och importeras aldrig. Se de olika andra vanliga problemen och felsökningsstegen för detta.

### Usenet-nedladdning missar importering

Sonarr tittar bara på de 60 senaste nedladdningarna i SABnzbd och NZBGet, så om du *behåller* din historik innebär det att under stora köer med importproblem kan nedladdningar tyst missas och inte importeras. Det bästa sättet att undvika detta är att hålla din historik ren, så att eventuella objekt som fortfarande visas behöver undersökas. Du kan åstadkomma detta genom att aktivera Ta bort under Slutförda och misslyckade nedladdningshanteraren. I NZBGet flyttar detta objekt till den *dolda* historiken, vilket är bra. Tyvärr har inte SABnzbd en liknande funktion. Det bästa du kan åstadkomma där är att använda nzb-säkerhetskopieringsmappen.

### Nedladdningsklienten rensar objekt

Nedladdningsklienten bör *inte* vara ansvarig för att ta bort nedladdningar. Usenet-klienter bör konfigureras så att de *inte* tar bort nedladdningar från historiken. Torrentklienter bör ställas in så att de *inte* tar bort torrents när de är färdiga med att seeda (pausa eller stoppa istället). Detta beror på att Sonarr kommunicerar med nedladdningsklienten för att veta vad som ska importeras, så om de *tas bort* finns det inget att importera, även om det finns en mapp full av filer.

För SABnzbd hanteras detta med inställningen Historikbehållning.

### Nedladdningen kan inte matchas med ett biblioteksobjekt

Av olika skäl kan utgåvor inte analyseras när de hämtas och skickas till nedladdningsklienten. Aktivitet => Alternativ => Visa okända (detta är nu aktiverat som standard i senaste versionerna) kommer att visa alla objekt som inte ignoreras på annat sätt / redan har importerats inom \*Arr:s nedladdningsklientskategori. Dessa behöver vanligtvis kartläggas och importeras manuellt.

Detta kan också inträffa om du har en utgåva i din nedladdningsklient men att det medieobjektet (film/avsnitt/bok/låt) inte finns i applikationen.

#### Hittade matchande serier via hämtningshistorik, men serien matchades med seriens ID. Automatisk importering är inte möjlig

- Detta importfel är liknande det ovanstående omöjliga att matcha-felet.
- Sonarr hämtade utgåvan eftersom din indexerare eller spårare rapporterade att utgåvan hade TVDb-ID (eller IMDb-ID) för en serie du ville ha.
- Serien för den nedladdade filen matchar inte det rapporterade ID:t, så Sonarr kommer inte att importera filen.
- Beroende på seriens titel och utgåvans namn - under förutsättning att utgåvan är korrekt för det ID den är associerad med - kommer Sonarr förmodligen att behöva lägga till ett alias, [den här FAQ-posten har mer information](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x) om hur man begär att ett alias läggs till.
- Alternativt kan utgåvan vara felmärkt och inte vara för det ID för serien som rapporterades. Detta bör rapporteras till din indexerare så att de kan vidta rätt åtgärder.
- För att hantera detta fel:
  1. Verifiera serien för filen
  1. Begär ett alias (om tillämpligt)
  1. Importera filen manuellt (människosymbolen till höger) från Aktivitet => Kö ELLER klicka på `X` i kön för att ignorera utgåvan i din klient och eventuellt blockera den / eventuellt ta bort den från klienten

### Avsnittsnamn är TBA

På TVDB kommer avsnittsnamn att vara TBA (To Be Announced) när de är okända, och det finns en cache på 24 timmar på API:et. Vanligtvis tar ändringar på TVDB-webbplatsen 24-48 timmar att nå Sonarr på grund av TVDB-cache, Skyhook-cache och seriens uppdateringsintervall.

Inställningen [Kräv avsnittstitel](/sonarr/settings#importing) i Sonarr styr importbeteendet när titeln är TBA, men efter 24 timmar från avsnittets sändningsdatum kommer utgåvan att importeras även om titeln fortfarande är TBA. Det sker heller ingen automatisk omdöpning av filer med TBA-titlar.

### Den underliggande anslutningen stängdes: Ett oväntat fel inträffade vid en sändning

Detta orsakas av att indexeraren använder en SSL-protokoll som inte stöds av den aktuella .NET-versionen som finns i [Sonarr => System => Status](/sonarr/system#status).

### Förfrågan tog för lång tid

Sonarr får inget svar från klienten.

```none
    System.NET.WebException: Förfrågan tog för lång tid: ’https://example.org/api?t=caps&apikey=(borttaget) —> System.NET.WebException: Förfrågan tog för lång tid
```

```none
2022-11-01 10:16:54.3|Varn|Newznab|Kan inte ansluta till indexeraren

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En uppgift avbröts.
```

Detta kan också orsakas av:

- felaktig konfiguration eller användning av en VPN
- felaktig konfiguration eller användning av en proxy
- lokala DNS-problem - Försök att byta till en annan DNS-leverantör
- lokala IPv6-problem - vanligtvis är IPv6 aktiverat, men fungerar inte
- användning av Privoxy och felaktig konfiguration av det

## Problem som inte listas

Du kan också gå igenom några vanliga behörighets- och nätverksfelsökningskommandon [i vår guide](/permissions-and-networking). Annars diskutera problemet med supportteamet på Discord. Om detta är något som kan vara ett vanligt problem, föreslå att det läggs till i wikin.

# Sökningar, indexerare och spårare

- [Varför hämtade inte Sonarr ett avsnitt jag förväntade mig?](/sonarr/faq#why-didnt-sonarr-grab-an-episode-i-was-expecting) FAQ-posten kan också vara till hjälp.
- Om du använder [Prowlarr](/prowlarr) kan du visa [Historik](/prowlarr/history) över alla förfrågningar som Prowlarr har tagit emot och hur de skickades till webbplatserna. Se till att `Parametrar` är aktiverat i Prowlarr Historik => Alternativ. (i)-ikonen ger ytterligare detaljer.
- Felsökningsstegen finns nedan

## Höj loggningsnivån till Trace

> **Det första steget är att höja loggningsnivån till Trace, se [Loggning och loggfiler](#logging-and-log-files) för information om hur du justerar loggningsnivån och söker i loggarna. Du kommer sedan att återskapa problemet och använda loggarna med trace-nivå från den tidsperioden för att undersöka problemet.** Om någon hjälper dig, lägg kontexten från före/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller liknande webbplats för att visa dem. Det behöver inte vara hela filen och det bör inte *bara* vara felet. Du bör också återskapa problemet när uppgifter som spammar loggfilen inte körs.
{.is-danger}

## Testa en indexerare eller spårare

När du testar en indexerare eller spårare kan du i felsöknings- eller trace-loggarna hitta den använda URL:en. Ett exempel på ett lyckat test visas nedan, där du kan se att det frågar indexeraren via en specifik URL med specifika parametrar och sedan svaret. Du kan testa denna URL i din webbläsare genom att ersätta `apikey=(borttaget)` med rätt api-nyckel, t.ex. `apikey=123`. Du kan experimentera med parametrarna om du får ett fel från indexeraren eller se om du har anslutningsproblem om det inte fungerar alls. Efter att du har testat i din egen webbläsare bör du testa från systemet som kör *om* du inte redan har gjort det.

## Testa en sökning

Precis som med indexerar-/spårartestet ovan, när du utlöser en sökning med felsöknings- eller trace-nivåloggar kan du få URL:en som används från loggfilerna. Vid testning är det bäst att använda en så smal sökning som möjligt. En manuell (interaktiv) sökning efter ett enskilt avsnitt eller en säsong är bra eftersom den är specifik och du kan se resultaten i gränssnittet samtidigt som du undersöker loggarna. Manuella (interaktiva) sökningar utlöses genom att gå till en serie och klicka på människosymbolen för ett avsnitt eller en säsong.

I detta test kommer du att leta efter uppenbara fel och köra några enkla tester. Du kan se att sökningen använde URL:en `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(borttaget)&offset=0&limit=100&tvdbid=354629&season=1&ep=1`, som du kan prova själv i en webbläsare efter att ha ersatt (borttaget) med din api-nyckel för den indexeraren. Fungerar det? Ser du de förväntade resultaten? Gäller den här FAQ-posten? I den URL:en kan du se att den har ställt in specifika kategorier med `cat=5030,5040,5045,5080`, så om du inte ser förväntade resultat är detta en trolig anledning. Du kan också se att den sökte efter tvdbid med `tvdbid=354629`, så om avsnittet inte är korrekt kategoriserat på indexeraren måste det åtgärdas. Du kan också se att den sökte efter en specifik säsong och ett specifikt avsnitt med season=1 och ep=1, så om det inte är korrekt på indexeraren kommer du inte att se de resultaten. Titta på exemplet på XML-utdata för manuell sökning nedan för att se hur en fungerande frågas utdata ser ut.

- XML-utdata för manuell sökning

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1" rel="self" type="application/rss+xml"/>
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
<newznab:response offset="0" total="2"/>
<item>
<title>The.Fix.S01E01.1080p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/358e0f946f953771c7688864b0334ba1
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=358e0f946f953771c7688864b0334ba1
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:32 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.1080p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)" length="3810861000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="3810861000"/>
<newznab:attr name="guid" value="358e0f946f953771c7688864b0334ba1"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="55"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:54:15 +0000"/>
</item>
<item>
<title>The.Fix.S01E01.720p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/f7e4ac2875b6a1ce45bae91ab19e9699
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=f7e4ac2875b6a1ce45bae91ab19e9699
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:33 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.720p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)" length="1195794000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="1195794000"/>
<newznab:attr name="guid" value="f7e4ac2875b6a1ce45bae91ab19e9699"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="14"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:51:45 +0000"/>
</item>
</channel>
</rss>
```

![searches-indexers-and-trackers1.png](/assets/sonarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/sonarr/searches-indexers-and-trackers2.png)

- Spårningsloggavsnitt

```none
2021-03-20 13:15:23.6|Info|NzbSearchService|Söker igenom 1 indexeringssidor efter [The Fix : S01E01]
2021-03-20 13:15:23.6|Debug|Newznab|Hämtar flöde https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
2021-03-20 13:15:23.6|Trace|HttpClient|Begäran: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
```

- Fullständig spårningslogg för en sökning

```none
2022-04-24 20:14:26.7|Info|ReleaseSearchService|Searching indexers for [Fairy Tail : S02E91 (91)]. 1 active indexers
2022-04-24 20:14:26.7|Debug|ReleaseSearchService|Total of 0 reports were found for [Fairy Tail : S02E91 (91)] from 1 indexers
2022-04-24 20:14:26.7|Info|DownloadDecisionMaker|No results found
```

- Note that in the above case there are 1 indexer being searched, but 0 reports were found. This means that the indexer was searched, but no results were returned. This can happen if the release is poorly named or if the indexer does not have the release available.
- To troubleshoot this issue, you can try the following:
  - Manually search for the release on the indexer's website to see if it is available.
  - Check if the release is listed on other indexers. If it is available on other indexers, you may need to add or configure additional indexers in Sonarr.
  - Check if the release is listed on other search engines. You can use a tool like Jackett to search multiple indexers at once.
  - If the release is poorly named, you can try adding a custom format or renaming rule in Sonarr to match the release.
  - If the release is not available on any indexers, it may not be released yet or it may be a rare release. In this case, you may need to manually download the release and import it into Sonarr.

- Serieförpackningar stöds inte
- Flera säsongsförpackningar stöds inte
- I många fall kan Sonarr helt enkelt inte matcha det returnerade resultatet med en känd serie. I dessa fall kommer dina loggar att se liknande ut som nedan. Dessa skulle behöva hämtas och förmodligen importeras manuellt. Den viktiga frasen att se i loggarna är `|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings`

```none
2022-02-23 14:11:09.7|Debug|Parser|Parsing string 'Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR'
2022-02-23 14:11:09.7|Trace|Parser|^(?<title>.+?)[-_. ]+?(?:S|Season|Saison|Series)[-_. ]?(?<season>\d{1,2}(?![-_. ]?\d+))(\W+|_|$)(?<extras>EXTRAS|SUBPACK)?(?!\\)
2022-02-23 14:11:09.7|Debug|Parser|Episode Parsed. Johnny Bravo 1997 Season 1 4 - Season 01 
2022-02-23 14:11:09.7|Debug|Parser|Language parsed: English
2022-02-23 14:11:09.7|Debug|QualityParser|Trying to parse quality for Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR
2022-02-23 14:11:09.7|Debug|Parser|Quality parsed: SDTV v1
2022-02-23 14:11:09.7|Debug|Parser|Release Group parsed: 
2022-02-23 14:11:09.8|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings
```

### Tracker behöver RawSearch Caps

- Sonarr söker efter `9 1 1` men din tracker har bara resultat för `9-1-1` eller `John s Show` och `John's Show`
- Detta beror på att din tracker inte stöder normaliserade sökningar.
- Lösningen är att din trackers definition av sökfunktioner måste uppdateras för att ange att den [kräver och stöder `RawSearch`](https://github.com/Sonarr/Sonarr/issues/1225#issuecomment-981153943)
- Jackett stöder flaggan, men funktionerna måste uppdateras för varje indexer. Öppna en förfrågan om funktion för Jackett för att lägga till denna funktionalitet för din indexer.
- Prowlarr stöder flaggan, men funktionerna måste uppdateras för varje indexer. Öppna en förfrågan om funktion för Prowlarr för att lägga till denna funktionalitet för din indexer.

### Serien behöver ett alias

Utgåvor kan laddas upp som `The Series Name`, men TVDB har serien som `Series Name` eller liknande namnvariationer. Se [denna FAQ-post](/sonarr/faq#why-cannot-sonarr-import-episode-files-for-series-x-why-cannot-sonarr-find-releases-for-series-x) för mer information.

### Serien behöver en XEM-mappning

Utgåvor kan laddas upp som `Series Title S02E45` eller `Other Series Title S2022E42`, men TVDB har detta avsnitt som `Series Title S03E01` eller `Other Series Title S03E42`. Se [denna FAQ-post](/sonarr/faq#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc) för mer information.

### Felaktig serietyp

Serietypen påverkar hur Sonarr söker. Serietypen bör väljas baserat på hur serien släpps på indexerarna.
[Se denna FAQ-post för mer information](/sonarr/faq#whats-the-different-series-types)

> Om **Anime** serietyp används - är det [möjligt att också söka efter din indexer med standardtypen.](/sonarr/settings#indexers)
{.is-info}

#### Daglig

Loggarna kommer att visa `Söker indexerare för [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Loggarna kommer att visa `Söker indexerare för [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Loggarna kommer att visa `Söker indexerare för [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

### Media är oövervakad

Loggarna kommer att visa något liknande

```none
2022-03-30 13:46:03.0|Debug|MonitoredEpisodeSpecification|No episodes in the release are monitored. Rejecting
2022-03-30 13:46:03.0|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] One or more episodes is not monitored
```

Serien/säsongen/avsnitten är inte övervakade. Kontrollera övervakningsstatusen för serien, säsongen och avsnitten.

> Säsongsförpackningar kommer bara att hämtas om alla avsnitt i säsongen övervakas och säsongsförpackningen uppgraderar alla befintliga avsnitt eller om alla avsnitt saknas.
{.is-info}

### Lyckad sökning - Inga resultat returnerade

Du får ett meddelande liknande `Query successful, but no results were returned from your indexer. This may be an issue with the indexer or your indexer category settings.`

Detta beror på att din indexer inte returnerar några resultat som finns inom de kategorier du har konfigurerat för indexeraren.

### Felaktiga kategorier

Felaktiga kategorier är förmodligen den vanligaste orsaken till att resultat visas i manuella sökningar på en indexer/tracker, men *inte* i \*Arr. Indexer/tracker *bör* visa kategorin i sökresultaten, vilket bör hjälpa dig att lista ut vad som saknas. Om du använder Jackett eller Prowlarr har varje tracker en lista över specifikt stödda kategorier. Se till att du använder rätt kategorier för Categories. Många tycker att det är användbart att ha listan synlig i ett webbläsarfönster medan de redigerar posten i Sonarr.

> Observera att om du har `Anime Categories` tomt i dina indexerinställningar kommer indexeraren inte att användas för sökningar av typen Anime Series Type.
> På samma sätt, om du har `Categories` tomt i dina indexerinställningar kommer indexeraren inte att användas för Standard eller Daily Series Type-sökningar.
{.is-info}

### Felaktiga resultat

Ibland returnerar indexerare helt irrelevanta resultat; Sonarr matar in parametrar för att begränsa sökningen till en serie. Ibland är de returnerade resultaten helt irrelevanta. Eller ibland, mestadels relaterade med några felaktiga resultat. Det första är vanligtvis ett indexeringsproblem och du kan se från spårloggen vilken indexerare som orsakar det. Du kan inaktivera den indexeraren och rapportera problemet. Det andra är vanligtvis kategoriserade utgåvor som bör kunna rapporteras på indexeraren/tracker.

Vissa indexerare - som EZTV och andra offentliga - returnerar slumpmässiga resultat om de inte har en exakt matchning för den sökta serien/säsongen/avsnittet. Det finns ingen lösning för detta.

### Saknade resultat

Om du har resultat på webbplatsen som du kan hitta men som inte visas i Sonarr är ditt problem förmodligen en av flera möjligheter:

- [Felaktiga kategorier - Se ovan](#wrong-categories)
- En ID-baserad sökning (IMDbId, TVDBId, etc.) görs och indexeraren har inte korrekt kartlagt utgåvorna till det ID:et. Detta är något som bara din indexerare kan lösa. De måste se till att utgåvan är kartlagd till de korrekta tillämpliga ID:erna.
- Inte söka på samma sätt som Sonarr söker; Det är mycket troligt att termerna du söker på indexeraren inte är hur Sonarr frågar efter det. Du kan se hur Sonarr frågar i Trace-loggarna. Textbaserade sökningar kommer generellt att vara i formatet `q=words%20and%20things%20here` denna sträng är HTTP-kodad och kan enkelt avkodas med hjälp av vilket HTML-avkodnings/kodningsverktyg som helst online.
- Missade delar av RSS-flödet för nya uppladdningar. Loggarna kommer att se ut som följer och en händelse av varning kommer att noteras.

```none
2022-02-22 08:03:38.7|Debug|Torznab|Downloading Feed http://jackett:9117/api/v2.0/indexers/torrentdownloads/results/torznab?t=tvsearch&cat=5000,100008&extended=1&apikey=(removed)&offset=2900&limit=100
2022-02-22 08:03:40.7|Warn|Torznab|Indexer TorrentDownloads rss sync didn't cover the period between 2/21/2022 8:32:06 PM and 2/21/2022 9:02:42 PM UTC. Search may be required.
```

### Certifikatvalidering

Du kommer att ansluta till de flesta indexerare/trackerare via https, så du måste se till att det fungerar korrekt på ditt system. Det innebär att din tidszon och tid måste vara inställda *korrekt*. Det innebär också att dina systemcertifikat måste vara uppdaterade.

### Träffar på hastighetsbegränsningar

Om du kör ditt genom en VPN eller proxy kan du konkurrera med 10-tals eller 100-tals eller 1000-tals andra personer som alla försöker använda tjänster som , theXEM och/eller dina indexerare och trackerare. Hastighetsbegränsning och DDOS-skydd görs ofta efter IP-adress och din VPN/proxy-utgångspunkt är *en* IP-adress. Om du inte befinner dig i ett förtryckande land som Kina, Australien eller Sydafrika behöver du inte använda VPN/proxy.

Rarbg har en tendens att ha någon form av hastighetsbegränsning inom deras API och visas som att svara utan resultat.

### IP-blockering

På samma sätt som hastighetsbegränsningar kan vissa indexerare - som Nyaa - helt enkelt blockera en IP-adress. Detta är vanligtvis halvpermanent och lösningen är att få en ny IP från din internetleverantör eller VPN-leverantör.

### Användning av Jackett /all-endpoint

Jackett `/all`-endpunkt är bekväm, men det är den enda fördelen. Allt annat kan vara potentiella problem, så det krävs att varje indexerare läggs till separat. Alternativt kan du överväga att använda Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

[Till och med Jackett säger att /all bör undvikas och inte bör användas.](https://github.com/Jackett/Jackett#aggregate-indexers)

Att använda all-endpoint har inga fördelar (förutom minskad hantering), bara nackdelar:

- du förlorar kontrollen över indexer-specifika inställningar (kategorier, söklägen, etc.)
- att blanda söklägen (IMDB, fråga, etc.) kan leda till lågkvalitativa resultat
- indexer-specifika kategorier (\>= 100000) kan inte användas.
- långsamma indexerare kommer att sakta ner det totala resultatet
- totala resultat är begränsade till 1000
- irrelevanta resultat
- saknade resultat

Genom att lägga till varje indexerare separat kan du finjustera kategorierna för varje indexerare, vilket kan vara ett problem med `/all`-endpunkten om fel kategori orsakar fel på vissa trackerare. I Sonarr är varje indexerare begränsad till 1000 resultat om sidindelning stöds eller 100 om det inte gör det, vilket innebär att ju fler indexerare du lägger till i Jackett, desto mer sannolikt är det att du klipper resultat. Slutligen, om *en* av indexerarna i `/all` returnerar ett fel, kommer att inaktivera den och nu får du inga resultat alls.

### Användning av NZBHydra2 som en enda post

Att använda NZBHydra2 som en enda indexeringspost (dvs. 1 NZBHydra2-post i Sonarr för många indexerare i NZBHydra2) istället för flera (dvs. många NZBHydra2-poster i Sonarr för många indexerare i NZBHydra2) har samma problem som noterats ovan med Jacketts `/all`-endpunkt.

### Indexeraren söks inte

- Om en indexerare inte verkar bli sökt beror det förmodligen på att indexeraren inte stöder söktypen. Det vanligaste fallet är att Nyaa bara stöder frågesökningar och inte säsong/avsnitt-sökningar. Trace-loggarna indikerar efter en omstart vid den första sökningen vilka förmågor en indexerare har eller inte har.

### Jackett manuell sökning hittar fler resultat

- [Se denna FAQ-post](/sonarr/faq#jackett-shows-more-results-than-sonarr-when-manually-searching)

### Release-profiler respekteras inte

Det finns några orsaker till varför det kan verka som att dina profiler ignoreras. Den vanligaste är relaterad till indexeringsbegränsningen i release-profiler. Eftersom indexeraren *inte* lagras med datan är alla `preferred word`-poäng *noll* för media i ditt bibliotek, *men* under "RSS" och sökning kommer de att tillämpas. På samma sätt för eventuella begränsningar för `must contain` eller `must-not` contain, gäller begränsningarna endast för den indexeraren; allt annat är fritt fram. Detta kan då göra att release-profiler verkar ignoreras eller att uppgraderingsloopar uppstår.

### Problem som inte listas

Du kan också gå igenom några vanliga behörighets- och nätverkstestkommandon för felsökning [i vår guide](/permissions-and-networking). Annars diskutera med supportteamet på Discord. Om detta är något som kan vara ett vanligt problem, föreslå att det läggs till i wikin.

## Fel

Detta är några av de vanliga felen du kan se när du lägger till en indexerare

### The underlying connection was closed: An unexpected error occurred on a send

Detta beror på att indexeraren använder en SSL-protokoll som inte stöds av den aktuella .NET-versionen som finns i [Sonarr => System => Status](/sonarr/system#status).

### The request timed out

Sonarr får inget svar från indexeraren.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

Detta kan också bero på:

- felaktig konfiguration eller användning av en VPN
- felaktig konfiguration eller användning av en proxy
- lokala DNS-problem - Försök att byta till en annan DNS-leverantör
- lokala IPv6-problem - vanligtvis är IPv6 aktiverat, men fungerar inte
- användning av Privoxy och att det är felaktigt konfigurerat

### Problem som inte listas

Du kan också gå igenom några vanliga behörighets- och nätverkstestkommandon för felsökning [i vår guide](/permissions-and-networking). Annars diskutera med supportteamet på Discord. Om detta är något som kan vara ett vanligt problem, föreslå att det läggs till i wikin.