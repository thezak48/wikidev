# Status

## Hälsa

- Den här sidan innehåller en lista över hälsokontrollfel. Dessa hälsokontroller utförs regelbundet av Sonarr och vid vissa händelser. De resulterande varningarna och felen listas här för att ge råd om hur man löser dem.

### Systemvarningar

#### För närvarande installerad .NET Framework är gammal och stöds inte

- Sonarr använder .NET Framework. Vi behöver bygga Sonarr mot den lägsta stödda versionen som fortfarande används av våra användare. Ibland ökar vi versionen vi bygger mot för att kunna använda nya funktioner. Tydligen har du inte tillämpat de lämpliga Windows-uppdateringarna på ett tag och behöver uppgradera .NET för att kunna använda nyare versioner av Sonarr.

- Att uppgradera .NET Framework är mycket enkelt på Windows, även om det ofta kräver en omstart.

#### För närvarande installerad .NET Framework stöds men uppgradering rekommenderas

- Sonarr använder .NET Framework. Vi behöver bygga Sonarr mot den lägsta stödda versionen som fortfarande används av våra användare. Genom att uppgradera till nyare versioner kan vi bygga mot nyare versioner och använda nya ramverksfunktioner.

- Att uppgradera .NET Framework är mycket enkelt på Windows, även om det ofta kräver en

#### För närvarande installerad mono-version är gammal och stöds inte

- Sonarr v4 är skrivet i .NET och v3 krävde Mono. Mono 5.20 är det absoluta minimum för Sonarr.
- Uppgraderingsproceduren för Mono varierar per plattform.

> Mono stöds inte längre från och med Sonarr version 4.0
{.is-warning}

#### För närvarande installerad SQLite-version stöds inte

- Sonarr lagrar sina data i en SQLite-databas. Den installerade SQLite3-biblioteket på ditt system är för gammalt. Sonarr kräver minst version 3.9.0.

> Observera att Sonarr använder `libSQLite3.so` som kan finnas eller inte finnas i ett SQLite3-uppgraderingspaket.
{.is-info}

#### Paketansvarig meddelande

- Din paketansvarige har ett meddelande till dig. Detta styrs av din ansvarige och inte av Sonarr.

#### Ny uppdatering finns tillgänglig

- Fira, utvecklarna har släppt en ny uppdatering. Detta innebär vanligtvis fantastiska nya funktioner och lösta buggar (eller hur?). Tydligen har du inte aktiverat automatisk uppdatering, så du måste ta reda på hur du uppdaterar på din plattform. Att trycka på Installera-knappen på sidan System => Uppdateringar är förmodligen en bra startpunkt.

> Denna varning visas inte om din nuvarande version är mindre än 14 dagar gammal
{.is-info}

#### Kan inte installera uppdatering eftersom startmappen och/eller UI-mappen inte kan skrivas av användaren

{#cannot-install-update-because-UI-folder-is-not-writable-by-the-user}

{#cannot-install-update-because-startup-folder-is-not-writable-by-the-user}

Detta innebär att Sonarr inte kommer att kunna uppdatera sig själv. Du måste uppdatera Sonarr manuellt eller ange behörigheterna för Sonarrs startmapp (installationsmappen) för att tillåta Sonarr att uppdatera sig själv.

#### Kan inte installera uppdatering eftersom startmappen är i en App Translocation-mapp

I macOS Sierra lade Apple till en konstig säkerhetsfunktion som kallas App Translocation (ibland känd som Gatekeeper Path Randomization), vilket innebär att efter att ha laddat ner en applikation, om du inte flyttar den resulterande applikationen någonstans (var som helst!), med Finder (du måste använda Finder!), kommer applikationen att köras som om den är placerad på en slumpmässigt vald sökväg av systemet.

#### Uppdatering kommer inte att vara möjlig för att förhindra att AppData raderas vid uppdatering

Sonarr upptäckte att AppData-mappen för ditt operativsystem är placerad inuti mappen som innehåller Sonarr-binärerna. Normalt skulle det vara C:\ProgramData för Windows och ~/.config för Linux.

Titta på System => Info för att se de aktuella AppData- och Startmapparna.
Detta innebär att Sonarr inte kommer att kunna uppdatera sig själv utan att riskera dataförlust.
Om du använder Linux måste du förmodligen ändra hemkatalogen för användaren som kör Sonarr och kopiera innehållet i den aktuella mappen ~/.config/Sonarr för att bevara din databas.

#### Kunde inte lösa IP-adressen för den konfigurerade proxyvärden

Granska dina proxyinställningar och se till att de är korrekta
Se till att din proxy är igång, fungerar och är tillgänglig

#### Proxy misslyckades test

Din konfigurerade proxy misslyckades med att testa framgångsrikt, granska HTTP-felmeddelandet och/eller kontrollera loggarna för mer information.

#### Systemtiden är mer än 1 dag felaktig

Systemtiden är mer än 1 dag felaktig. Schemalagda uppgifter kan inte köras korrekt förrän tiden har korrigerats
Granska din systemtid och se till att den är synkroniserad med en auktoritativ tidsserver och är korrekt

#### MediaInfo-biblioteket kunde inte laddas

MediaInfo-biblioteket kunde inte laddas. Sonarr kräver MediaInfo (`libmediainfo`) för att utvärdera videoattributen hos filer.

#### Mono Legacy TLS är aktiverat

{#sonarr-mono-4.x-tls-workaround-still-enabled-consider-removing-mono_tls_provider-legacy-environment-option}

Mono 4.x TLS-åtgärden är fortfarande aktiverad, överväg att ta bort miljöalternativet MONO_TLS_PROVIDER=legacy.

### Nedladdningsklienter

#### Ingen nedladdningsklient är tillgänglig

En korrekt konfigurerad och aktiverad nedladdningsklient krävs för att Sonarr ska kunna ladda ner media. Eftersom Sonarr stöder olika nedladdningsklienter bör du bestämma vilken som bäst motsvarar dina krav. Om du redan har en nedladdningsklient installerad bör du konfigurera Sonarr att använda den och skapa en kategori. Se Inställningar => Nedladdningsklient.

#### Kan inte kommunicera med nedladdningsklient

Sonarr kunde inte kommunicera med den konfigurerade nedladdningsklienten. Kontrollera om nedladdningsklienten är igång och dubbelkolla URL:en. Detta kan också indikera ett autentiseringsfel.
Detta beror vanligtvis på en felaktigt konfigurerad nedladdningsklient. Saker du vanligtvis kan kontrollera:
IP-adressen för din nedladdningsklient, om den är på samma fysiska maskin är detta vanligtvis 127.0.0.1
Portnumret som din nedladdningsklient använder, dessa är ifyllda med standardportnumret men om du har ändrat det måste du ange samma nummer i Sonarr.
Se till att SSL-kryptering inte är aktiverad om du använder både din Sonarr-instans och din nedladdningsklient i ett lokalt nätverk. Se SSL-FAQ:en för mer information.

#### Nedladdningsklienter är otillgängliga på grund av fel

En eller flera av dina nedladdningsklienter svarar inte på förfrågningar från Sonarr. Därför har Sonarr beslutat att tillfälligt sluta fråga nedladdningsklienten på sin normala 1-minuterscykel, som normalt används för att spåra aktiva nedladdningar och importera färdiga nedladdningar. Men Sonarr kommer att fortsätta försöka skicka nedladdningar till klienten, men kommer med stor sannolikhet att misslyckas.
Du bör inspektera System => Loggar för att se vad orsaken till felen är.
Om du inte längre använder denna nedladdningsklient, inaktivera den i Sonarr för att förhindra felen.

#### Aktivera hantering av färdiga nedladdningar

- Sonarr kräver hantering av färdiga nedladdningar för att kunna importera filer som laddats ner av nedladdningsklienten. Det rekommenderas att aktivera hantering av färdiga nedladdningar.
(Hantering av färdiga nedladdningar är aktiverat som standard...)

#### Docker felaktig fjärrsökvägsmappning

- Det här felet är vanligtvis associerat med felaktiga docker-sökvägar antingen i din nedladdningsklient eller Sonarr

- Ett exempel på detta skulle vara:
  - Nedladdningsklient: Nedladdningsmapp: /mnt/user/downloads:/downloads
  - Radarr: Nedladdningsmapp: /mnt/user/downloads:/data
- I det här exemplet placerar nedladdningsklienten sina nedladdningar i /downloads och talar sedan om för Radarr när de är klara att den färdiga filmen finns i /downloads. Sonarr kommer sedan och säger "Okej, coolt, låt mig kolla i /downloads" Tja, inuti Radarr har du inte tilldelat en /downloads-sökväg, du har tilldelat en /data-sökväg så det här felet uppstår.
- Det enklaste sättet att fixa detta är KONSISTENS om du använder ett schema i din nedladdningsklient, använd det över hela linjen.

- Team Sonarr gillar att helt enkelt använda /data.
  - Nedladdningsklient: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Nu kan du inom nedladdningsklienten ange var i /data du vill placera dina nedladdningar, nu varierar detta beroende på klienten men du bör kunna tala om för den "Ja, nedladdningsklient, placera mina filer i." /data/torrents (eller usenet)/movies och eftersom du använde /data i Radarr när nedladdningsklienten berättar för Radarr att den är klar kommer Radarr att säga "Bra, jag har en /data och jag kan också se /torrents (eller usenet)/movies allt är rätt i världen."
- Det finns många bra skrivuppgifter: vår wiki [Docker Guide](/docker-guide) och TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Dessa guider lägger stor vikt vid hardlänkar och atomiska flyttningar, men det allmänna konceptet med containrar och hur sökvägsmappning fungerar är kärnan i dessa diskussioner.

- Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) för mer information.

#### Laddar ner till rotmappen

{#downloads-in-root-folder}

- Inom applikationen definieras en rotmapp som den konfigurerade mediebiblioteksmappen. Detta är inte rotmappen för en montering. Din nedladdningsklient har en ofullständig eller komplett (eller flyttar färdiga nedladdningar) till din rot (biblioteks) mapp.
- Detta orsakar ofta problem - inklusive dataförlust - och bör inte göras. För att åtgärda detta, ändra din nedladdningsklient så att den inte placerar nedladdningar inom din rotmapp. Observera att 'placering' även inkluderar om din nedladdningsklients kategori är inställd på din rotmapp eller om NZBGet/SABnzbd har sorteringsfunktionen aktiverad och sorterar till din rotmapp.
- Observera att den här kontrollen tittar på alla definierade/konfigurerade rotmappar som har lagts till, inte bara rotmappar som för närvarande används. Med andra ord bör inte mappen där din nedladdningsklient laddar ner eller flyttar färdiga nedladdningar till vara samma mapp som du har konfigurerat som din rot/biblioteks/slutmålsplatsmapp i *arr-applikationen.
- Konfigurerade rotmappar (även kända som biblioteksmappar) finns i [Inställningar => Mediehantering => Rotmappar](/sonarr/settings/#root-folders)
- Ett exempel är om dina nedladdningar går till `/data/downloads` då har du en rotmapp inställd som `/data/downloads`.
- Det rekommenderas att använda sökvägar som `/data/media/` för din rotmapp/bibliotek och `/data/downloads/` för dina nedladdningar.
- Granska vår [Docker Guide](/docker-guide) och TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) för mer information om korrekt och optimal sökvägsinställning. Observera att koncepten gäller både för docker och icke-docker

> Din nedladdningsmapp där din nedladdningsklient placerar nedladdningarna och din rot/biblioteksmapp MÅSTE vara separata. \*Arr kommer att importera filen/filerna från din nedladdningsklients mapp till ditt bibliotek. Nedladdningsklienten bör inte flytta något eller ladda ner något till ditt bibliotek.
{.is-warning}

#### Felaktiga inställningar för nedladdningsklient

- Platsen där din nedladdningsklient laddar ner filer orsakar problem. Kontrollera loggarna för mer information. Detta kan bero på behörigheter eller försök att gå från Windows till Linux eller Linux till Windows utan en fjärrsökvägsmappning.

#### Felaktig fjärrsökvägsmappning

- Platsen där din nedladdningsklient laddar ner filer orsakar problem. Kontrollera loggarna för mer information. Detta kan bero på behörigheter eller försök att gå från Windows till Linux eller Linux till Windows utan en fjärrsökvägsmappning. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) för mer information.

#### Behörighetsfel

- Sonarr eller användaren som Sonarr körs som kan inte komma åt platsen där din nedladdningsklient laddar ner filer. Detta beror vanligtvis på ett behörighetsproblem.

#### Fjärrfilen togs bort under pågående bearbetning

- En fil som är tillgänglig via en fjärrsökvägsmappning verkar ha tagits bort innan bearbetningen var klar.

#### Fjärrsökväg används och importen misslyckades

- Kontrollera loggarna för mer information; Hänvisa till våra felsökningsguider

### Laddar ner till rotmappen

{#downloads-in-root-folder}

- Inom applikationen definieras en rotmapp som den konfigurerade mediebiblioteksmappen. Detta är inte rotmappen för en montering. Din nedladdningsklient har en ofullständig eller komplett (eller flyttar färdiga nedladdningar) till din rot (biblioteks) mapp.
- Detta orsakar ofta problem - inklusive dataförlust - och bör inte göras. För att åtgärda detta, ändra din nedladdningsklient så att den inte placerar nedladdningar i din rotmapp. Observera att 'placering' även inkluderar om din nedladdningsklients kategori är inställd på din rotmapp eller om NZBGet/SABnzbd har sorteringsfunktionen aktiverad och sorterar till din rotmapp.
- Observera att denna kontroll tittar på alla definierade/konfigurerade rotmappar som har lagts till, inte bara rotmappar som för närvarande används. Med andra ord bör inte mappen där din nedladdningsklient laddar ner eller flyttar färdiga nedladdningar vara samma mapp som du har konfigurerat som din rot/biblioteks/finala mediamålmapp i *arr-applikationen.
- Konfigurerade rotmappar (även kallade biblioteksmappar) finns i [Inställningar => Mediehantering => Rotmappar](/sonarr/settings/#root-folders)
- Ett exempel är om dina nedladdningar hamnar i `/data/downloads` då har du en rotmapp inställd som `/data/downloads`.
- Det rekommenderas att använda sökvägar som `/data/media/` för din rotmapp/bibliotek och `/data/downloads/` för dina nedladdningar.
- Granska vår [Docker Guide](/docker-guide) och TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) för mer information om korrekt och optimal konfiguration av sökvägar. Observera att koncepten gäller både för docker och icke-docker

> Din nedladdningsmapp där din nedladdningsklient placerar nedladdningarna och din rot/biblioteksmapp MÅSTE vara separata. \*Arr kommer att importera filerna från din nedladdningsklients mapp till ditt bibliotek. Nedladdningsklienten bör inte flytta något eller ladda ner något till ditt bibliotek.
{.is-warning}

#### Hantering av färdiga nedladdningar är inaktiverad

{#completedfailed-download-handling}

- Det är nödvändigt att använda hantering av färdiga nedladdningar eftersom det ger bättre kompatibilitet för uppackning och efterbehandlingslogik för olika nedladdningsklienter. Med det kommer Sonarr bara att importera en nedladdning när nedladdningsklienten rapporterar att den är klar.
- Om hantering av färdiga nedladdningar är inaktiverad:
  - Alla importeringar måste hanteras manuellt
  - Denna hälsokontroll kommer att finnas kvar och kan inte avfärdas eller inaktiveras
  - Avsnitt kommer alltid att saknas i Sonarr och vara tillgängliga för att hämtas i all framtid
    - Avsnitt som manuellt flyttas och byter namn av användaren till seriens mapp i Sonarrs biblioteksmapp kan eventuellt plockas upp av den två gånger dagliga omsökningen om de har rätt namn och därmed inte saknas vid den tidpunkten.
  - Användaren måste manuellt sluta övervaka eller konfigurera ett anpassat skript för att sluta övervaka avsnitt.
  - FlexGet är förmodligen ett bättre verktyg för användare som inte vill använda Sonarrs funktioner för mediebibliotekshantering och bara behöver något för att analysera RSS-flöden och skicka utgåvor till nedladdningsklienten

> \* Hantering av färdiga nedladdningar fungerar bara korrekt om nedladdningsklienten och Sonarr körs på samma maskin eftersom den får sökvägen att importera direkt från nedladdningsklienten, annars krävs en fjärrkarta.
> \* Hantering av färdiga nedladdningar kräver att Sonarr har läs- och skrivåtkomst till den färdiga nedladdningsmappen
{.is-warning}

### Indexerare

#### Inga indexerare är tillgängliga med aktiverad automatisk sökning, Sonarr kommer inte att ge några automatiska sökresultat

- Helt enkelt sagt har du inte några indexerare inställda för att tillåta automatiska sökningar
Gå till Inställningar > Indexerare, välj en indexerare du vill tillåta automatiska sökningar för och klicka sedan på Spara.

#### Inga indexerare är tillgängliga med aktiverad RSS-synkronisering, Sonarr kommer inte att automatiskt hämta nya utgåvor

{#no-indexers-available-with-rss-sync-enabled,-sonarr-will-not-grab-new-releases-automatically}
{#all-rss-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Sonarr använder RSS-flödet för att plocka upp nya utgåvor när de kommer. [Se FAQ för mer information](/sonarr/faq#how-does-sonarr-find-episodes)
- För att åtgärda detta problem går du till Inställningar > Indexerare, välj en indexerare som du har och aktivera RSS-synkronisering.

#### Inga indexerare är aktiverade

- Sonarr kräver indexerare för att kunna upptäcka nya utgåvor. Antingen är alla dina indexerare inaktiverade eller så har du inte lagt till några indexerare.

#### Aktiverade indexerare stöder inte sökning

{#all-search-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Ingen av de indexerare du har aktiverade och tillgängliga stöder sökning. Detta innebär att Sonarr bara kommer att kunna hitta nya utgåvor via RSS-flödena. Men att söka efter serier (antingen automatisk sökning eller manuell sökning) kommer aldrig att ge några resultat. Det enda sättet att åtgärda detta är att lägga till en annan indexerare.

#### Inga indexerare är tillgängliga med aktiverad interaktiv sökning

{#no-indexers-available-with-interactive-search-enabled-sonarr-will-not-provide-any-interactive-search-results}

- Ingen av de indexerare du har aktiverade och tillgängliga stöder interaktiv sökning. Detta innebär att applikationen bara kommer att kunna hitta nya utgåvor via RSS-flöden eller en automatisk sökning.

#### Indexerare är otillgängliga på grund av fel

- Fel uppstår när Sonarr försökte använda en av dina indexerare. För att begränsa försöken kommer Sonarr inte att använda indexeraren under en ökande tid (upp till 24 timmar).
- Denna mekanism utlöses om Sonarr inte kunde få svar från indexeraren (kan bero på DNS, proxy/vpn-anslutning, autentisering eller indexeringsproblem) eller om den inte kunde hämta nzb/torrent-filen från indexeraren. Granska loggarna för att avgöra vilken typ av fel som orsakade problemet.
- Du kan förhindra denna varning genom att inaktivera den berörda indexeraren.
- Kör ett `Test` på indexeraren för att tvinga Sonarr att kontrollera indexeraren igen; observera att hälsokontrollvarningen inte alltid försvinner omedelbart och du kan behöva köra uppgiften `Kontrollera hälsa`

#### Jackett All Endpoint används

- Jackett /all-endpointen är bekväm, men det är den enda fördelen. Allt annat är potentiella problem, så det krävs nu att varje spårare läggs till individuellt.
- [Även Jacketts utvecklare säger att den bör undvikas och inte användas.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Att använda /all-endpointen har inga fördelar, bara nackdelar:
  - du förlorar kontrollen över inställningar för specifika indexerare (kategorier, söklägen, etc.)
  - att blanda söklägen (IMDB, fråga, etc.) kan ge lågkvalitativa resultat
  - indexerarspecifika kategorier (\>= 100000) kan inte användas.
  - långsamma indexerare kommer att sakta ner det övergripande resultatet
  - totala resultat är begränsade till 1000
  - om en av spårarna i /all returnerar ett fel kommer \*Arr att inaktivera den och nu får du inga resultat.

##### Lösningar

- Lägg till varje spårare i Jackett manuellt som en indexerare i \*Arr
- Kolla in [Prowlarr](/prowlarr) som kan synkronisera indexerare till \*Arr och från Lidarr/Radarr/Readarr-utvecklingsteamet.
- Kolla in [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisera indexerare till \*Arr. Men använd inte deras enskilda samlade slutpunkt och använd `multi` om synkronisering kommer att användas.

### Media & Listor

#### Serier borttagna från TheTVDB

- Den berörda serien/serierna har tagits bort från [The TVDb](https://thetvdb.com). Detta händer vanligtvis eftersom serien är en duplicering eller anses vara en del av en annan serie. Alternativt kan TVDb behandla den som en serie; förhoppningsvis gör även TMDb det så att [Radarr](/radarr) kan användas istället. För att åtgärda detta måste du ta bort den berörda serien och lägga till rätt serie om det är tillämpligt.

#### Listor är otillgängliga på grund av fel

{#import-lists-are-unavailable-due-to-failures}

- Vanligtvis betyder detta helt enkelt att Sonarr inte längre kan kommunicera via API eller genom att logga in på din valda listtjänst. Om problemet kvarstår är det bästa alternativet att kontakta dem för att utesluta dem, eftersom deras system kan vara överbelastade från tid till annan.
- Granska System => Händelser filtrerade för varningar (varningar och fel) för att se de historiska felen eller kontrollera loggarna för detaljer.

#### Importlista saknar rotmapp

- En eller flera av dina importlistor är konfigurerade till en rotmapp som inte är åtkomlig för Sonarr.
- Detta kan bero på behörighetsproblem, en saknad montering eller helt enkelt att listorna behöver uppdateras efter att du har omorganiserat din konfiguration.

#### Saknad rotmapp

- En rotmapp har lagts till i Sonarr och finns inte eller är inte åtkomlig
- Detta fel identifieras vanligtvis om en serie letar efter en rotmapp men den rotmappen är inte längre tillgänglig.
- Detta fel kan också uppstå om en lista fortfarande pekar på en rotmapp men den rotmappen inte längre är tillgänglig.
- Om du vill ta bort denna varning kan du helt enkelt hitta serien som fortfarande använder den gamla rotmappen och redigera den till rätt rotmapp.

- Enklaste sättet att hitta problemserierna är att:

  - Gå till fliken Massredigerare
  - Skapa ett anpassat filter med den gamla sökvägen till rotmappen
  - Välj massredigering i den översta menyn och välj den nya rotmappen som du vill flytta dessa serier till från rullgardinsmenyn Rotmappar.
  - Sedan får du en popupruta som frågar Vill du flytta seriemapparna till 'rotmapp' ? Detta kommer också att ange Detta kommer också att döpa om seriemappen enligt seriemappens format i inställningarna. Välj helt enkelt Nej om du inte vill att Lidarr ska flytta dina filer
  - Kör uppgiften Kontrollera hälsa i System => Uppgifter

#### Seriebanans montering är skrivskyddad

{#series-mount-ro}

En montering som innehåller en seriebana är skrivskyddad och kan inte skrivas till av användaren som Sonarr körs som.

## Diskutrymme

- Den här sektionen visar tillgängligt diskutrymme
- I docker kan detta vara knepigt eftersom det vanligtvis visar det tillgängliga utrymmet inom din Docker-bild.

## Om

- Detta kommer att berätta om din nuvarande installation av Sonarr.

## Mer information

- Hemsida: Sonarrs [hemsida](https://www.sonarr.tv)
- Wiki: Du är redan här.
- Reddit: [r/sonarr](https://www.reddit.com/r/sonarr)
- Discord: Gå med i vår [discord](https://discord.sonarr.tv/)
- Donationer: Om du känner dig generös och vill donera, klicka [här](https://sonarr.tv/donate).
- Källa: [GitHub](https://www.github.com/sonarr/sonarr)
- Funktionsförfrågningar: Har du en bra idé, lämna den [här](https://www.github.com/sonarr/sonarr/issues).

# Uppgifter

## Schemalagda

- Den här sektionen listar alla schemalagda uppgifter som Sonarr kör

- Kontrollera uppdatering av applikationen - Detta körs enligt den schemalagda tiden som visas i gränssnittet och kontrollerar om Sonarr är den senaste versionen och utlöser sedan uppdateringsskriptet för att uppdatera Sonarr. Inställningar => Uppdatering

> Observera: Om du använder Docker kommer detta inte att uppdatera din behållare eftersom en ny bild måste laddas ner.
{.is-warning}

- Säkerhetskopiering - Detta körs enligt den schemalagda tiden och säkerhetskopierar Sonarrs databas. Mer information om säkerhetskopiering finns under System => Säkerhetskopior.
- Kontrollera hälsa - Kontrollera hälsa körs enligt den schemalagda tiden och kontrollerar den övergripande hälsan för din Sonarr. För att se en lista över möjliga hälsorelaterade problem, se Wiki-posten om hälsokontroller.
- Rensa återvinning - Återvinningskorgen töms enligt den schemalagda tiden. Detta används endast om återvinningskorgen är inställd i Filhantering
- Städning - Enligt den schemalagda tiden dammsugs spindelväv bort, golven sopas och dammsugs, moppas, poleras och till och med gör snygga små vikta anteckningar bara för dig. Men det tar inte ut soporna. Det fick helt enkelt inte tillräckligt betalt för det.
- Synkronisera importlista - Enligt den schemalagda tiden körs detta dina listor och importerar eventuella nya serier. Mer information om listor finns under Inställningar => Listor.
- Rensa meddelanden - Enligt den schemalagda tiden rensas de meddelanden som visas i det nedre vänstra hörnet av Sonarr
- Uppdatera övervakade nedladdningar - Detta går igenom och uppdaterar nedladdningskön som finns under Aktivitet. Det pingar helt enkelt din nedladdningsklient för att kontrollera färdiga nedladdningar.
- Uppdatera serier - Detta går igenom och uppdaterar all metadata för alla övervakade och oövervakade serier
- RSS-synkronisering - Detta körs RSS-synkroniseringen. Detta kan ändras under Inställningar => Indexerare => Alternativ. Mer information om RSS-funktionen finns i vår [FAQ](/sonarr/faq)
  
> Alla dessa uppgifter kan köras manuellt utanför sina schemalagda tider genom att klicka på ikonen längst till höger för varje uppgift.
{.is-info}

## Kö

Kön visar pågående och kommande uppgifter samt en historik över nyligen körda uppgifter och hur lång tid dessa uppgifter tog.

# Säkerhetskopiering

> Om du vill veta hur du säkerhetskopierar/återställer din Sonarr-instans klicka [här](/sonarr/faq).
{.is-info}

Inom säkerhetskopieringsavsnittet presenteras du med tidigare säkerhetskopior (om du har en färsk installation som inte har gjort några säkerhetskopior visas inga tidigare säkerhetskopior).
  
- Säkerhetskopiera nu - Detta alternativ kommer att utlösa en manuell säkerhetskopiering av din Sonarrs databas
- Återställ säkerhetskopia - Detta öppnar en ny skärm för att återställa från en tidigare säkerhetskopia
  - Genom att välja Välj fil kommer din webbläsare att öppna en dialogruta för att återställa från en Sonarr-zip-säkerhetskopia
  
- Om du har några tidigare säkerhetskopior och vill ladda ner dem från Sonarr för att placera dem på en icke-standard plats kan du helt enkelt välja en av dessa filer för att ladda ner dem
- Till höger om varje tidigare nedladdning har du två alternativ.

  - Återställ (Klockikon) - För att återställa från en tidigare säkerhetskopia - Detta öppnar ett nytt fönster för att bekräfta att du vill återställa från denna säkerhetskopia
  - Ta bort (Soptunna) - För att ta bort en tidigare säkerhetskopia

# Uppdateringar

Uppdateringsskärmen visar de senaste 5 uppdateringarna som har gjorts samt den nuvarande versionen du använder.
Denna sida visar också uppdateringsanteckningarna från utvecklarna som berättar vad som har åtgärdats eller lagts till i Sonarr (Fira!)

> En underhållsutgåva innehåller buggfixar och andra olika förbättringar. Ta en titt på commit-historiken på Github för specifika detaljer.
{.is-info}

# Händelser

Händelsefliken visar vad som har hänt i din Sonarr. Detta kan användas för att diagnostisera vissa mindre problem. Detta ersätter dock inte spårloggar som diskuteras i Loggning.

> Händelser motsvarar INFO-loggar. {.is-info}

- Komponenter - Denna kolumn berättar vilken komponent inom Sonarr som har utlösts
- Meddelande - Denna kolumn berättar vilket meddelande som har skickats från komponenten i föregående kolumn.
- Kugghjulsikon - Detta alternativ låter dig ändra hur många komponenter/meddelanden som visas per sida (standard är 50)
- Alternativ längst upp på sidan
  - Uppdatera - Detta alternativ kommer att uppdatera den aktuella sidan och hämta en ny händelselogg
  - Rensa - Detta kommer att rensa den aktuella händelseloggen och låta dig börja om från början

# Loggfiler

- Den här sidan låter dig ladda ner och se vilka loggfiler som är tillgängliga för Sonarr.

- På översta raden finns flera alternativ som låter dig kontrollera dina loggfiler.

- Översta raden längst till vänster finns en rullgardinsmeny som låter dig växla mellan Loggfiler och Uppdateringsloggfiler
  - Loggfiler - Brödet och smöret i alla supportärenden, mer om loggfiler finns här.
  - Uppdateringsloggfiler - Detta visar loggfiler som är associerade med Sonarrs uppdateringsskript

> Om du använder Docker kommer detta att vara tomt eftersom du bör uppdatera genom att ladda ner en ny Docker-bild
{.is-info}

- Uppdatera - Detta kommer att uppdatera den aktuella sidan och visa eventuellt nyss skapade loggar
- Ta bort - Detta kommer att rensa alla loggar och låta dig börja om från början
- Filnamn - Detta kommer att visa filnamnet som är associerat med loggen
- Senast skrivet - Detta är den lokala tiden då denna specifika loggfil skrevs.
  - Sonarr använder rullande loggfiler begränsade till 1 MB vardera. Den aktuella loggfilen är alltid sonarr.txt, för de andra filerna är sonarr.0.txt den näst nyaste (ju högre nummer desto äldre är den) upp till totalt 51 loggfiler. Denna loggfil innehåller `fatal`, `error`, `warn` och `info`-poster.
  - När felsökningsloggnivån är aktiverad kommer ytterligare sonarr.debug.txt rullande loggfiler att finnas, upp till 51 filer. Denna loggfil innehåller `fatal`, `error`, `warn`, `info` och `debug`-poster. Den täcker vanligtvis en ~40-timmarsperiod.
  - När spårningsloggnivån är aktiverad kommer ytterligare sonarr.trace.txt rullande loggfiler att finnas, upp till 51 filer. Denna loggfil innehåller `fatal`, `error`, `warn`, `info`, `debug` och `trace`-poster. På grund av spårningsvolymen täcker den bara ett par timmar som mest.