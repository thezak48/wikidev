---
title: Lidarr Snabbstart
description: 
published: true
date: 2022-07-14T14:10:13.343Z
tags: 
editor: markdown
dateCreated: 2021-06-13T06:14:53.615Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Snabbstartsguide för installation](#snabbstartsguide-för-installation)
- [Försiktighetsåtgärder](#försiktighetsåtgärder)
- [Koncept](#koncept)
  - [Utgåvor (Metadata)](#utgåvor-metadata)
  - [Artist (Metadata)](#artist-metadata)
- [Första start](#första-start)
- [Inställningar](#inställningar)
  - [Mediehantering](#mediehantering)
  - [Profiler](#profiler)
  - [Kvalitet](#kvalitet)
  - [Indexerare](#indexerare)
  - [Nedladdningsklienter](#nedladdningsklienter)
    - [{.tabset}](#tabset)
      - [Usenet](#usenet)
      - [BitTorrent](#bittorrent)
- [Första artist](#första-artist)
- [Första nedladdning/import](#första-nedladdningimport)
- [Snabbstart - Avancerad](#snabbstart-avancerad)
  - [Lidarr användningsfall](#lidarr-användningsfall)
    - [Lös filer](#lös-filer)
    - [Specialbibliotek](#specialbibliotek)
  - [Importera befintligt bibliotek eller filer](#importera-befintligt-bibliotek-eller-filer)
    - [Förbereda befintliga filer](#förbereda-befintliga-filer)
      - [Mappstruktur](#mappstruktur)
      - [Taggning](#taggning)
    - [För-import-överväganden](#för-import-överväganden)
    - [Börja importera](#börja-importera)

# Snabbstartsguide för installation

> Den här sidan är fortfarande under arbete och inte komplett. Bidrag är välkomna.

> För en mer detaljerad genomgång av alla inställningar, se [Lidarr => Inställningar](/lidarr/settings)
{.is-info}

I den här guiden kommer vi att försöka förklara den grundläggande konfigurationen du behöver göra för att komma igång med Lidarr. Vi kommer att hoppa över vissa alternativ som du kan se på skärmen. Om du vill gå djupare in på dessa, se den lämpliga sidan i FAQ och dokumentationen för en fullständig förklaring.

> Observera att de avancerade alternativen visas i `orange` på skärmbilderna och i GUI-inställningarna, så du måste klicka på `Visa avancerat` längst upp på sidan för att göra dem synliga.
{.is-warning}

# Försiktighetsåtgärder

I den här guiden förklarar vi de grundläggande stegen för att börja använda Lidarr. Guiden förutsätter att du redan har installerat applikationen. Installationsinstruktioner finns på följande sida [installation](/lidarr/installation). Vi kommer att fokusera på den minsta konfigurationen/alternativen för att få en fungerande konfiguration. Det finns ytterligare inställningar och överväganden om någon av följande situationer gäller:

- Befintligt bibliotek eller befintliga filer
- Felaktigt användningsfall
- Felaktig mappstruktur
- Felaktig eller extremt komplicerad taggning
- Lösa filer
- Specialbaserade musikbibliotek: Klassisk musik, Singlar, Elektronisk musik

Om någon av ovanstående situationer gäller, se avsnittet Snabbstart - Avancerad.

Den här guiden är uppdelad i avsnitt. Det rekommenderas att du läser hela guiden för att få en komplett förståelse, men du kan hoppa till specifika avsnitt om du har omedelbara frågor. Använd innehållsförteckningen till vänster för att snabbt hoppa till avsnitten.

# Koncept

För att kunna använda Lidarr på rätt sätt måste de underliggande koncepten förstås. På en övergripande nivå följer det principerna för de andra Arr-applikationerna. Lidarr fungerar som ett system för hantering av musikbibliotek, en datatjänst och en automatiseringsplattform för att hitta och ladda ner media.

Därefter är avvikelsen ganska betydande. Hanteringen av musikbibliotek är en mycket komplicerad process eftersom det finns många konkurrerande variabler som hindrar processen. Till skillnad från hanteringen av filmer eller TV-program finns det inte en konsekvent uppsättning standarder för taggning, namngivning eller lagring av musik. Detta har ytterligare komplicerats av de förändrade metoderna för musikdistribution från fysiska medier till elektroniska. Slutligen är åsikterna om hur man hanterar denna hantering många och varierade.

Lidarr använder information från datatjänster för att korrekt tagga och hantera musikbiblioteket. Denna tredjepartsdata representerar media i definierade kategorier och typer.

> Om datan inte finns i tredjepartstjänsterna kan den INTE hanteras av Lidarr.
Detaljer finns nedan för att delta och bidra.
{.is-warning}

Den huvudsakliga tjänsten som används är [MusicBrainz](https://musicbrainz.org/). Detta är en gratis tjänst som drivs av gemenskapen och överlever på dina bidrag och deltagande. Skapande och bidrag till utgåvor ligger utanför omfattningen av denna guide. Instruktioner finns här: [Hur man bidrar](https://musicbrainz.org/doc/How_to_Contribute)

Till syvende och sist definieras datan av tredjepartsdatastandarderna. Om standarderna inte överensstämmer med ditt användningsfall kan **Lidarr vara fel lösning**. Andra applikationer för hantering av ditt media kan inkludera:

[Beets Media Management](https://beets.io/)
[MusicBrainz Picard](https://picard.musicbrainz.org/)
[Music Bee](https://getmusicbee.com/)

Dessa implementationer kan användas tillsammans med Lidarr, men detta ligger utanför omfattningen av denna guide.

## Utgåvor (Metadata)

Lidarr har valt standarden `Utgåva` för hantering av musikmedia. Det innebär att för att systemet ska fungera korrekt måste all media som bearbetas av systemet vara en `Utgåva`.

Exempel på utgåvor:

- Album
- EP
- Singel
- Sändning

Varje objekt som ska hanteras måste ha en motsvarande `Utgåva` i tredjepartsdatatjänsten.

> `Utgåvor` måste finnas i tredjepartstjänsterna för att kunna hanteras i Lidarr.

## Artist (Metadata)

Artister är precis vad man kan förvänta sig av `Utgåva Artist`. Tyvärr har artistnamn, stil, förändrats över tid, användarpreferenser och andra skäl förvirrat vad som utgör denna `Utgåva Artist`.

Exempel på korrekta och inkorrekta "Artister":

- Bob Dylan
- BOB DYLAN
- The Bob Dylan
- Bob Dylan, The
- Bob Dylan & the Band
- Bob Dylan feat. The Band
- The Band featuring Bob Dylan
- ...

Listan kan fortsätta i all oändlighet. Återigen är alla `Utgåvor` kopplade till en `Artist`. Du måste hitta (steg senare i denna guide) och använda rätt `Artist` för att ladda ner en `Utgåva`.

> `Utgåva Artister` måste finnas i tredjepartstjänsterna för att kunna hanteras i Lidarr.

# Första start

Efter installation och start av Lidarr kan du komma åt det genom att öppna en webbläsare och gå till `http://{din_ip_här}:8686`

![lidarr_qs_startup.png](/assets/lidarr/quick-start-guide/lidarr_qs_startup.png)

Det visas två alternativ på startskärmen, men vi kommer inte att använda dem i början.

# Inställningar

Vi kommer att använda standardkonfigurationen av inställningar för att konfigurera Lidarr. Detta kommer att använda befintliga profiler, kvalitet, taggar, etc.

> För en mer detaljerad genomgång av alla inställningar, se [Lidarr > Inställningar](/lidarr/settings)
{.is-info}

## Mediehantering

Först ska vi titta på `Mediehantering` där vi kommer att ställa in `Rotmappen`. Detta kommer att vara platsen där mediefilerna kommer att lagras.

> Lagra inte Lidarr-media på en molnlagringstjänst! På grund av hur Lidarr använder taggar kommer detta att överskrida eventuella API-begränsningar och orsaka problem. Håll ditt bibliotek på ditt nätverk.
{.is-warning}

Klicka på `Inställningar` > `Mediehantering` i vänstermenyn.

![lidarr_qs_mediamanagement.png](/assets/lidarr/quick-start-guide/lidarr_qs_mediamanagement.png)

Klicka på `Lägg till (+)` för `Rotmappar`.

Du kommer att presenteras med följande fönster:

![lidarr_qs_rootfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_rootfolder.png)

- **Namn** - Detta är det `Vänliga namnet` på lagringsplatsen.
- **Sökväg** - Detta är den faktiska `Sökvägen` till datalagringsplatsen. Systemet/användaren måste ha rättigheter till denna lagringsplats. Den här mappen kan inte vara din nedladdningsplats!

Lämna de andra alternativen som standard.

> Om du använder en `Rotmapp` med befintliga filer, se avsnittet Snabbstart - Avancerad för överväganden.
{.is-warning}

> \* Icke-Windows: Om du använder en NFS-montering, se till att `nolock` är aktiverat.
> \* Om du använder en SMB-montering, se till att `nobrl` är aktiverat.
{.is-warning}

> **Användaren och gruppen som du har konfigurerat Lidarr att köra som måste ha läs- och skrivrättigheter till denna plats.** {.is-info}

> Din nedladdningsklient laddar ner till en nedladdningsmapp och Lidarr importerar den till din mediamapp (slutdestination) som din mediaserver använder.
{.is-info}

> **Din nedladdningsmapp och mediamapp kan inte vara samma plats**
{.is-danger}

## Profiler

`Inställningar` > `Profiler`

Profilinställningarna kommer att vara oförändrade.

## Kvalitet

`Inställningar` > `Kvalitet`

Kvalitetsinställningarna kommer att vara oförändrade.

## Indexerare

`Inställningar` > `Indexerare`

Den här sektionen ställer in indexerare/spårare som du kommer att använda för att hitta nedladdningsbara mediefiler.

Klicka på `Lägg till (+)` för `Indexerare`. Du kommer att presenteras med ett nytt fönster med många olika alternativ. Lidarr betraktar både Usenet-indexerare och BitTorrent-spårare som `Indexerare`.

Lägg till minst en `Indexerare` för att Lidarr ska kunna hitta tillgängliga filer korrekt.

Förstå konfigurationen/koncepten bakom `Indexerare` ligger utanför omfattningen av denna guide. Internet är fullt av information om ämnet.

## Nedladdningsklienter

`Inställningar` => `Nedladdningsklienter`

![Lidarr-settings-download-clients.png](/assets/lidarr/Lidarr-settings-download-clients.png)

Nedladdning och import är där de flesta människor upplever problem. På en övergripande nivå måste programvaran kunna kommunicera med din nedladdningsklient och ha åtkomst till de filer den laddar ner. Det finns många olika nedladdningsklienter som stöds och ännu fler olika inställningar. Det innebär att medan det finns några vanliga inställningar finns det ingen rätt inställning och varje persons inställning kan vara lite annorlunda. Men det finns många felaktiga inställningar.

> Se [inställningssidan](/lidarr/settings#download-clients), sidan [Mer information (Stödda)](/lidarr/supported#download-clients) för den här sektionen och [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) för mer information.
{.is-info}

### {.tabset}

#### Usenet

{#usenet}

- Lidarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Lidarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- När nedladdningen är klar kommer Lidarr att känna till den slutliga filplatsen enligt rapporterad av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp och åtkomlig av Lidarr.
- Lidarr kommer att skanna den avslutade filplatsen efter filer som Lidarr kan använda. Den kommer att analysera filnamnet för att matcha det mot den begärda median. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den angivna medieplatsen.
- Atomiska flyttar (direkta flyttar) är aktiverade som standard. Filsystemet och monteringspunkterna måste vara desamma för din avslutade nedladdningsmapp och ditt mediebibliotek. Om den atomiska flytten misslyckas eller din konfiguration inte stöder hårdlänkar och atomiska flyttar kommer Lidarr att backa och kopiera filen och sedan ta bort den från källan, vilket är I/O-intensivt.
- Om alternativet "Hantering av avslutade nedladdningar - Ta bort" är aktiverat i Lidarrs inställningar kommer kvarvarande filer från nedladdningen att skickas till papperskorgen eller återvinningen genom en begäran till din klient att ta bort utgåvan.

#### BitTorrent

{#bittorrent}

- Lidarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Lidarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Denna övervakning sker via din nedladdningsklients API.
- Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (förhållande eller tid kan justeras i nedladdningsklienten eller från Lidarr under den specifika nedladdningsklienten). När filer importeras till din mediamapp kommer Lidarr att skapa en hårdlänk till filen om det stöds av din konfiguration eller kopiera om hårdlänkar inte stöds.
- Hårdlänkar är aktiverade som standard. [En hårdlänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringspunkterna måste vara desamma för din avslutade nedladdningsmapp och ditt mediebibliotek. Om skapandet av hårdlänken misslyckas eller din konfiguration inte stöder hårdlänkar kommer Lidarr att backa och kopiera filen.
- Om alternativet "Hantering av avslutade nedladdningar - Ta bort" är aktiverat i Lidarrs inställningar kommer Lidarr att ta bort torrenten från din klient och be klienten att ta bort torrentdata, men endast om klienten rapporterar att seedningen är klar och torrenten är stoppad (pausad vid slutförandet).

# Första artist

Om du följer den här guiden och din `Rotmapp` inte hade några mediefiler måste du lägga till en `Artist`.

`Bibliotek` > `Lägg till ny`

![lidarr_qs_addnew.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnew.png)

Detta kommer att länka till sökskärmen för att hitta en artist. Sök och välj den `Artist` du vill lägga till. Detta kommer att öppna fönstret "Lägg till ny artist".

![lidarr_qs_addnewdylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnewdylan.png)

Vi kommer att använda standardvalen. Vilket bör inkludera:

- Rotmapp - Mappen du skapade
- Övervaka - Ingen
- Kvalitetsprofil - Alla
- Taggar - (tomt)
- Starta sökning efter saknade album - Avmarkerad

Detta kommer att starta nedladdningen av `Artist`-metadata. Detta tar tid beroende på mängden data som ska samlas in. Kom ihåg att denna information kommer från tredjepartskällor och är bara så komplett som vad gemenskapen har bidragit med.

Klicka på den nyss tillagda `Artisten`. (Bob Dylan i det här exemplet)

> Standard `Metadataprofil` används, de enda `Utgåvorna` som visas kommer att vara av typen `Studioalbum`.

![lidarr_qs_dylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylan.png)

> Gillar du inte den nedladdade metadatan? - Bidra för att göra den bättre!
{.is-info}

# Första nedladdning/import

Äntligen dags att ladda ner/importera din första `Utgåva`!

Hitta den `Utgåva` som du vill lägga till i ditt bibliotek. Välj ikonen för manuell sökning (människa) bredvid utgåvan.

![lidarr_qs_dylanrelease.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanrelease.png)

Detta kommer att öppna fönstret för val av `Utgåva`. Detta fönster visar resultaten av `Indexerare`-frågan eller helt enkelt sökresultaten för tillgängliga nedladdningar.

> Standard `Kvalitetsprofil` tillåter alla filtyper. Standard `Utgåvoprofil` tillåter alla nedladdningar. För en detaljerad genomgång av dessa avancerade inställningar, se [Lidarr > Inställningar](/lidarr/settings)

![lidarr_qs_dylandownload.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylandownload.png)

Granska nedladdningsfönstret för den olika tillhandahållna informationen:

1. Titel - Detta är namnet på nedladdningen som returneras av `Indexeraren`.
1. Kvalitet - Detta är kvaliteten som bestäms av Lidarr med hjälp av titeln.
1. Varningsindikatorerna ger en beskrivning av varför nedladdningen har misslyckats med Lidarrs kontroller. I exemplet returnerade sökningen "Fel album".

När du har granskat väljer du nedladdningsikonen (nummer 4) för att ladda ner den tillgängliga `Utgåvan`.

Om konfigurationen är korrekt skickas nedladdningen till din `Nedladdningsklient`.

Nedladdningen läggs till i `Kön` och går igenom olika stadier beroende på vilken typ av `Nedladdningsklient` du använder.

Slutligen importeras nedladdningen till din `Rotmapp`. Om allt går som det ska bör den visas som nedan.

![lidarr_qs_dylansucess.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylansuccess.png)

Du kan hitta dina nedladdade filer i din `Rotmapp` och använda dem med din valda mediaspelare.

![lidarr_qs_dylanfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanfolder.png)

# Snabbstart - Avancerad

Denna avancerade avsnitt är avsett för installationer som kan ha speciella överväganden. Granska om något av dessa gäller för din konfiguration och potentiellt spara lite huvudvärk.

>Följande avsnitt kommer att hjälpa till med vanliga fallgropar och problem.
{.is-warning}

## Lidarr Användningsfall

Som tidigare nämnts i Konceptavsnittet bör Lidarr inte användas om ditt avsedda användningsområde inte matchar Lidarrs hanteringssystem för `Releases`. Lidarr kommer INTE att fungera med följande användningsfall:

- Lösa filer - Filer från flera artister (inte samlingar) eller flera `Releases`
- Specialiserade musikbibliotek: Klassiskt, Singlar, Elektroniskt

### Lösa filer

Låg till ingen kurering av lösa filer kommer inte att fungera med Lidarr. Det är bäst att inte försöka använda dessa filer med Lidarr.

### Specialiserade bibliotek

Specialiserade bibliotek skapar unika problem för alla hanteringssystem. Dessa situationer kan fungera med Lidarr, men det kan kräva omfattande arbete från din sida och i stort sett försumma de inbyggda automatiseringarna. Till exempel:

- **Klassisk musik** - Har vanligtvis omfattande taggningskrav eller önskemål. `Releases`-metadata kommer troligen inte att finnas eller vara felaktig.
- **Singlar** - Singlar kan inte vara faktiska `Releases`. Tredjepartsdata-tjänster kommer inte att returnera någon metadata. De kommer inte att automatiseras och Lidarr kommer inte att kunna tillämpa hantering.
- **Elektroniskt** - Detta gäller INTE för `Releases` inom den elektroniska genren. Detta gäller bibliotek med mixar, beats, samples osv. (Beatport). Tredjepartsdatakällor känner inte igen dessa som `Releases`. De kommer inte att automatiseras och Lidarr kommer inte att kunna tillämpa hantering.

## Importera befintligt bibliotek eller filer

> Observera att Lidarr inte söker efter `Releases` regelbundet. Se dessa två FAQ-poster för detaljer om hur Lidarr fungerar.
[Hur hittar Lidarr `Releases`?](/lidarr/faq#hur-hittar-lidarr-releases) och [Hur fungerar Lidarr?](/lidarr/faq#hur-fungerar-lidarr)
{.is-info}

> Automatisk import är en schemalagd process och kan inte stoppas när den har startat.
LÄGG INTE till en `Root Folder` med befintliga filer förrän du har granskat detta avsnitt i sin helhet.
{.is-warning}

Lidarr använder ett automatiserat system för att lägga till `Release Artists` och `Releases` som finns i din `Root Folder`.

Om Lidarrs användningsfall matchar och du inte har unika eller specialiserade bibliotek kan du fortsätta med att importera ditt befintliga bibliotek.

Det är viktigt att dina befintliga biblioteksfiler är strukturerade och följer Lidarrs hanteringssystem för `Releases`. Detta innebär att följande inte kommer att fungera:

- Felaktig mappstruktur - Filer som finns i en enda mapp - Se avsnittet Förberedelse>Mappstruktur
- Felaktig eller extremt komplicerad taggning - Se avsnittet Förberedelse>Taggning

### Förbereda dina befintliga filer

För att den automatiserade processen ska fungera måste dina filer förberedas för att säkerställa att allt flyter smidigt eller fungerar överhuvudtaget.

#### Mappstruktur

Det rekommenderas att följa den standardiserade mappstrukturen:

\Root Folder\Release Artist\Release\XX - Track

Detta, tillsammans med korrekta taggar, kommer att möjliggöra att nästan 95% eller mer av filerna känns igen av mediaspelare.

#### Taggning

Taggning kan vara en komplicerad procedur. Antalet filer och hur de för närvarande är taggade kommer att avgöra ansträngningen som krävs.

De rekommenderade metoderna för att tagga dina filer inkluderar:

- MusicBrainz Picard
- Beets
- MusicBee, MediaMonkey, JRiver

Användning av dessa applikationer ligger utanför omfattningen av denna guide, men det är föredraget att associera MusicBrainz Release ID:er som en del av taggningsprocessen.

> De flesta taggningsprogram kan strukturera och döpa om mappar samt tagga filer på rätt sätt.
{.is-info}

### Överväganden före import

När filerna är korrekt taggade och namngivna bör följande kontrolleras för att säkerställa att processen slutförs framgångsrikt:

- **Systemarkitektur** - Rekommenderas x64 / 64-bitars - Import av stora bibliotek kräver att systemet har tillgång till stora mängder RAM och beräknar mer effektivt. x86 / 32-bitars stöds men kommer inte att vara lika effektivt och kommer att ta betydligt längre tid.
- **Systemminneskrav (RAM)** - Minst 4 GB, rekommenderat 8 GB - Importprocessen är minnesintensiv och om Lidarr importerar och en webbläsare är öppen kommer det att resultera i betydande användning av RAM.
- **Begränsningar för `Release`-skiva/spår** - `Releases` som har betydande mängder spår eller skivor bör tas bort från importprocessen. De kan importeras manuellt med hjälp av de inbyggda procedurerna. Det finns ingen exakt gräns, men för att vara säker bör `Releases` med fler än 25 skivor eller 250 spår tas bort.
- **`Release Artist` med många `Releases`** - Lidarrs automatiserade process jämför `Releases` med dina filer. Även om det inte är troligt att det misslyckas kommer dessa filer att öka importtiden avsevärt. Det finns enskilda artister med tusentals `Releases`.
- **Tid** - Den automatiserade importprocessen tar tid. En rimlig uppskattning skulle vara 1 timme för 500 korrekt taggade `Releases`. Detta varierar mycket beroende på din lagring, internetanslutningens hastighet och systemets prestanda.

### Börja importera

//

Kommer snart

- Övervaka * - Detta ställer in standardövervakningsalternativet (`Releases`) för `Root Folder`.
- Kvalitetsprofil * - Detta ställer in standardkvalitetsalternativet för `Root Folder`.
- Metadataprofil * - Detta ställer in standardmetadataalternativet för `Root Folder`.