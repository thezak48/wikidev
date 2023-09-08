# Status

## Hälsa

Den här sidan innehåller en lista över hälsokontrollfel. Dessa hälsokontroller utförs regelbundet av Prowlarr och vid vissa händelser. De resulterande varningarna och felen listas här för att ge råd om hur man löser dem.

### Systemvarningar

#### Grenen är inte en giltig utgåvogren

- Den gren du har angett är inte en giltig utgåvogren. Du kommer inte att få uppdateringar. Ändra till en av de [aktuella utgåvogrenarna](/prowlarr/faq#how-do-i-update-prowlarr).

#### För närvarande installerad SQLite-version stöds inte

- Prowlarr lagrar sina data i en SQLite-databas. Den installerade SQLite3-biblioteket på ditt system är för gammalt. Prowlarr kräver minst version 3.9.0. Observera att Prowlarr använder `libSQLite3.so` som kan eller inte kan ingå i en SQLite3-uppgraderingspaket.

#### Ny uppdatering finns tillgänglig

- Fira, utvecklarna har släppt en ny uppdatering. Detta innebär vanligtvis fantastiska nya funktioner och lösta buggar (eller hur?). Tydligen har du inte aktiverat automatisk uppdatering, så du måste ta reda på hur du uppdaterar på din plattform. Att trycka på Installera-knappen på sidan System => Uppdateringar är förmodligen en bra startpunkt.

> Denna varning visas inte om din nuvarande version är mindre än 14 dagar gammal
{.is-info}

#### Kan inte installera uppdatering eftersom startmappen inte kan skrivas av användaren

- Detta innebär att Prowlarr inte kommer att kunna uppdatera sig själv. Du måste uppdatera Prowlarr manuellt eller ange behörigheterna för Prowlarrs startmapp (installationsmappen) för att tillåta Prowlarr att uppdatera sig själv.

#### Uppdatering kommer inte att vara möjlig för att förhindra att AppData raderas vid uppdatering

- Prowlarr upptäckte att AppData-mappen för ditt operativsystem är placerad inuti mappen som innehåller Prowlarr-binärerna. Normalt skulle det vara C:\ProgramData för Windows och ~/.config för Linux.

- Titta på System => Info för att se de aktuella AppData- och startmapparna.
- Detta innebär att Prowlarr inte kommer att kunna uppdatera sig själv utan att riskera förlust av data.
- Om du använder Linux måste du förmodligen ändra hemkatalogen för användaren som kör Prowlarr och kopiera innehållet i den aktuella mappen ~/.config/Prowlarr för att bevara din databas.

#### Grenen är för en tidigare version

- Uppdateringsgrenen som är inställd i Inställningar/Allmänt är för en tidigare version av Prowlarr, därför kommer instansen inte att se korrekt uppdateringsinformation i System/Uppdateringar och kanske inte får nya uppdateringar när de släpps.

#### Kunde inte ansluta till signalR

- signalR driver de dynamiska UI-uppdateringarna, så om din webbläsare inte kan ansluta till signalR på din server kommer du inte att se några realtidsuppdateringar i gränssnittet.

- Det vanligaste förekomsten av detta är användning av en omvänd proxy eller Cloudflare.
  - Cloudflare kräver aktiverade websockets.
  - Nginx kräver följande tillägg till platsblocket för appen:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Se till att du inte inkluderar proxy_set_header Connection "Upgrade"; som föreslås av nginx-dokumentationen. DETTA KOMMER INTE ATT FUNGERA
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

- För Apache2 omvänd proxy måste du aktivera följande moduler: proxy, proxy_http och proxy_wstunnel. Lägg sedan till denna websocket-tunnelanvisning i din vhost-konfiguration:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:9696/$1 [P,L]
```

Om du har en omvänd proxy under en underkatalog bör RewriteRule inkludera din basbana, t.ex.

```none
RewriteRule /prowlarr/(.*) ws://127.0.0.1:9696/prowlarr/$1 [P,L]
```

Om Prowlarr inte körs på samma dator som din omvända proxy. Byt ut 127.0.0.1 mot rätt IP-adress/DNS-namn för din Prowlarr-app.

- För Caddy (V1) använd detta:

> Observera: du måste också lägga till websocket-anvisningen i din Prowlarr-konfiguration{.is-info}

```none
 proxy /prowlarr 127.0.0.1:9696 {
     websocket
     transparent
 }
```

#### Kunde inte lösa IP-adressen för den konfigurerade proxyvärden

- Granska dina proxyinställningar och se till att de är korrekta.
- Se till att din proxy är igång, fungerar och är tillgänglig.

#### Proxytest misslyckades

- Din konfigurerade proxy misslyckades med att testa framgångsrikt, granska den HTTP-felinformation som tillhandahålls och/eller kontrollera loggarna för mer information.

#### Systemtiden är mer än 1 dag felaktig

- Systemtiden är mer än 1 dag felaktig. Schemalagda uppgifter kan inte köras korrekt förrän tiden är rättad.
- Granska din systemtid och se till att den är synkroniserad med en auktoritativ tidsserver och är korrekt.

### Nedladdningsklienter

#### Ingen nedladdningsklient är tillgänglig

- En korrekt konfigurerad och aktiverad nedladdningsklient krävs för att Prowlarr ska kunna ladda ner media. Eftersom Prowlarr stöder olika nedladdningsklienter bör du bestämma vilken som bäst motsvarar dina krav. Om du redan har en nedladdningsklient installerad bör du konfigurera Prowlarr att använda den och skapa en kategori. Se Inställningar => Nedladdningsklient.

#### Kan inte kommunicera med nedladdningsklient

- Prowlarr kunde inte kommunicera med den konfigurerade nedladdningsklienten. Kontrollera om nedladdningsklienten är igång och dubbelkolla URL:en. Detta kan också indikera ett autentiseringsfel.
- Detta beror vanligtvis på en felaktigt konfigurerad nedladdningsklient. Saker du vanligtvis kan kontrollera:
- IP-adressen för dina nedladdningsklienter, om de körs på samma fysiska maskin är detta vanligtvis 127.0.0.1
- Portnumret som din nedladdningsklient använder, dessa fylls i med standardportnumret men om du har ändrat det måste du ange samma nummer i Prowlarr.
- Se till att SSL-kryptering inte är aktiverad om du använder både din Prowlarr-instans och din nedladdningsklient i ett lokalt nätverk. Se SSL-FAQ-inlägget för mer information.
- Användning av rutorrent kräver speciella inställningsändringar eftersom det kräver https.

#### Nedladdningsklienter är otillgängliga på grund av fel

- En eller flera av dina nedladdningsklienter svarar inte på förfrågningar från Prowlarr. Därför har Prowlarr beslutat att tillfälligt sluta fråga nedladdningsklienten på sin normala 1-minuterscykel, som normalt används för att spåra aktiva nedladdningar och importera färdiga nedladdningar. Men Prowlarr kommer att fortsätta försöka skicka nedladdningar till klienten, men kommer förmodligen att misslyckas.
- Du bör inspektera System=>Loggar för att se vad orsaken till felen är.
- Om du inte längre använder denna nedladdningsklient bör du inaktivera den i Prowlarr för att förhindra felen.

#### Dåliga inställningar för nedladdningsklient

- Platsen där din nedladdningsklient laddar ner filer orsakar problem. Kontrollera loggarna för ytterligare information. Detta kan bero på behörigheter eller försök att gå från Windows till Linux eller från Linux till Windows utan en fjärrsökvägskarta.

### Indexer

#### Indexer har ingen definition

- Dina indexer har ingen befintlig definition (fil), detta beror vanligtvis på att din indexer inte längre stöds och har tagits bort eller att Cardigann YML-definitionen inte längre är tillgänglig.

#### Indexer är föråldrade

- Din indexer(s) definition är föråldrad och inaktuell. Detta har två möjliga orsaker som anges nedan.

##### Föråldrad på grund av kodändringar

- På grund av kodändringar är indexer(s) föråldrade som de är konfigurerade för närvarande. Ta bort och lägg till indexer i Prowlarr för att lösa problemet.
- Detta beror vanligtvis på att API:er konverteras eller från YML till C# eller vice versa.

##### Föråldrad på grund av borttagna webbplatser

- Vissa webbplatser kan begära att tas bort från Prowlarr eller Jackett. Dessa kan sedan markeras som föråldrade.
  - [TVVault](https://github.com/Prowlarr/Prowlarr/issues/573) i [Prowlarr #700](https://github.com/Prowlarr/Prowlarr/pull/700)
  - Audiobookbay har begärt att Prowlarr inte ska få åtkomst till deras API
  - Ebookbay har begärt att Prowlarr inte ska få åtkomst till deras API
  - Rarbg har [stängt ner från och med 2023-05-31](https://torrentfreak.com/iconic-torrent-site-rarbg-shuts-down-all-content-releases-stop-230531/)

#### Inga indexer är aktiverade

- Prowlarr kräver indexer för att kunna upptäcka nya utgåvor. Läs instruktionerna i wikin om hur du lägger till indexer.

#### Indexer är otillgängliga på grund av fel

- (Ett) fel uppstår när Prowlarr försökte använda en av dina indexer. För att begränsa omförsök kommer Prowlarr inte att använda indexeraren under en ökande tid (upp till 24 timmar).
- Kontrollera händelser och filtrera efter varningar för att få en snabb uppfattning om vilka problem som har uppstått historiskt sett.
- Denna mekanism utlöses om Prowlarr inte kunde få ett svar från indexeraren (kan bero på DNS, proxy/vpn-anslutning, autentisering eller indexeringsproblem) eller inte kunde hämta nzb/torrent-filen från indexeraren. Granska loggarna för att avgöra vilken typ av fel som orsakar problemet.
- Du kan förhindra varningen genom att inaktivera den berörda indexeraren.
- Kör testet på indexeraren för att tvinga Prowlarr att kontrollera indexeraren igen, observera att hälsokontrollvarningen inte alltid försvinner omedelbart.

#### Indexer VIP förfaller

- Ditt VIP-abonnemang eller förmåner för din indexer förfaller inom de närmaste 7 dagarna eller mindre baserat på utgångsdatumet du har konfigurerat för din indexer i Prowlarr.

#### Indexer VIP har förfallit

- Ditt VIP-abonnemang eller förmåner för din indexer har förfallit baserat på utgångsdatumet du har konfigurerat för indexer i Prowlarr.

### Applikationer

#### Applikationer är otillgängliga på grund av fel

- (Ett) fel uppstår när Prowlarr försökte använda en av dina applikationer. För att begränsa omförsök kommer Prowlarr inte att använda applikationen under en ökande tid (upp till 24 timmar).
- Denna mekanism utlöses om Prowlarr inte kunde få ett svar från applikationen (kan bero på DNS, anslutning, autentisering eller applikationsproblem). Granska loggarna för att avgöra vilken typ av fel som orsakar problemet.
- Kontrollera händelser och filtrera efter varningar för att få en snabb uppfattning om vilka problem som har uppstått historiskt sett.
- Prowlarr kommer inte att kunna synkronisera med applikationen och det är mycket troligt att applikationen inte kommer att kunna använda Prowlarrs indexer.
- Du kan förhindra varningen genom att inaktivera den berörda applikationen.
- Kör testet på applikationen för att tvinga Prowlarr att kontrollera applikationen igen, observera att hälsokontrollvarningen inte alltid försvinner omedelbart.

## Diskutrymme

Den här avsnittet visar tillgängligt diskutrymme.
I Docker kan detta vara knepigt eftersom det vanligtvis visar det tillgängliga utrymmet inom din Docker-bild.

## Om

Detta kommer att berätta om din nuvarande installation av Prowlarr.

## Mer information

Hemsida: Prowlarrs hemsida
Wiki: Du är redan här
Reddit: r/prowlarr
Discord: Gå med i vår discord
Donationer: Om du känner dig generös och vill donera klicka här
Donationer till Sonarr: Om du känner dig generös och vill donera till projektet som startade allt klicka här
Källa: GitHub
Funktionsförfrågningar: Har du en bra idé, lägg upp den här

# Uppgifter

## Schemalagda

Den här sidan listar alla schemalagda uppgifter som Prowlarr kör

- Kontrollera uppdatering av applikation - Detta körs enligt den schemalagda tiden som visas i gränssnittet och kontrollerar om Prowlarr är på den senaste versionen och utlöser sedan uppdateringsskriptet för att uppdatera Prowlarr. Inställningar => Uppdatering

> Observera: Om du använder Docker kommer detta inte att uppdatera din behållare eftersom en ny bild måste laddas ner.
{.is-warning}

- Säkerhetskopiering - Detta körs enligt en schemalagd tid och säkerhetskopierar Prowlarrs databas. Mer information om detta finns här. Mer information om säkerhetskopior finns under System => Säkerhetskopior.
- Kontrollera hälsa - Kontrollera hälsa körs enligt den schemalagda tiden som visas i gränssnittet och kontrollerar Prowlarrs övergripande hälsa. För att se en lista över möjliga hälsorelaterade problem, se Wiki-posten om hälsokontroller.
- Städning - Enligt den schemalagda tiden som visas i gränssnittet kommer detta att dammsuga bort alla spindelväv, sopa och dammsuga golven, moppa, polera och till och med göra fina små vikta anteckningar bara för dig. Men det tar inte ut soporna. Det fick helt enkelt inte tillräckligt med betalt för det.
- Städa upp meddelanden - Enligt den schemalagda tiden som visas i gränssnittet rensar detta upp de meddelanden som visas i nedre vänstra hörnet av Prowlarr.

> Alla dessa uppgifter kan köras manuellt utanför sina schemalagda tider genom att klicka på ikonen längst till höger för varje uppgift.
{.is-info}

## Kö

Kön visar kommande uppgifter samt en historik över nyligen körda uppgifter samt hur lång tid dessa uppgifter tog.

# Säkerhetskopiering

> Den här avsnittet kommer att vara mer anpassat till knapparna och den övergripande poängen på sidan.
> Om du dock letar efter hur du säkerhetskopierar/återställer din Prowlarr-instans, [se vår FAQ](/prowlarr/faq).
{.is-info}

Inom avsnittet för säkerhetskopiering kommer du att presenteras med tidigare säkerhetskopior (om du inte har en ny installation som inte har gjort några säkerhetskopior ännu).

Här har du två alternativ längst upp på skärmen:

- Säkerhetskopiera nu - Detta alternativ kommer att utlösa en manuell säkerhetskopiering av din Prowlarr-databas.
- Återställ säkerhetskopia - Detta kommer att öppna en ny skärm för att återställa från en tidigare säkerhetskopia.
Genom att välja Välj fil kommer din webbläsare att öppna en dialogruta för att återställa från en Prowlarr-zip-säkerhetskopia.

Slutligen, om du har några tidigare säkerhetskopior och vill ladda ner dem från Prowlarr för att placera dem på en icke-standard plats, kan du helt enkelt välja en av dessa filer för att ladda ner dem.
Till höger om varje tidigare nedladdning har du två alternativ.

- Ett - För att återställa från en tidigare säkerhetskopia - Detta kommer att öppna ett nytt fönster för att bekräfta att du vill återställa från denna säkerhetskopia.
- Två - För att ta bort en tidigare säkerhetskopia

# Uppdateringar

Uppdateringsskärmen visar de senaste 5 uppdateringarna som har gjorts samt den nuvarande versionen du använder.
Den här sidan visar också uppdateringsanteckningarna från utvecklarna som berättar vad som har åtgärdats eller lagts till i Prowlarr (Fira!)

> En underhållsversion innehåller buggfixar och andra olika förbättringar. Ta en titt på ändringshistoriken för specifika detaljer.
{.is-info}

# Händelser

Fliken Händelser visar vad som har hänt inom din Prowlarr. Detta kan användas för att diagnostisera vissa mindre problem. Observera att detta inte ersätter spårningsloggar som diskuteras i Loggning. Händelser motsvarar INFO-loggar.

- Komponenter - Denna kolumn berättar vilken komponent inom Prowlarr som har utlösts.
- Meddelande - Denna kolumn berättar vilket meddelande som har skickats från komponenten i föregående kolumn.
- Kugghjulsikon - Detta alternativ låter dig ändra hur många komponenter/meddelanden som visas per sida (standard är 50).
- Alternativ längst upp på sidan
  - Uppdatera - Detta alternativ kommer att uppdatera den aktuella sidan och hämta en ny händelselogg.
  - Rensa - Detta kommer att rensa den aktuella händelseloggen och låta dig börja om från början.

# Loggfiler

Den här sidan låter dig ladda ner och se vilka aktuella loggfiler som är tillgängliga för Prowlarr.

På den översta raden finns flera alternativ som låter dig kontrollera dina loggfiler.

- På den översta raden längst till vänster finns en rullgardinsmeny som låter dig växla mellan Loggfiler och Uppdateringsloggfiler.
  - Loggfiler - Grunden för alla supportärenden, mer information om loggfiler finns här.
  - Uppdateringsloggfiler - Detta visar loggfiler som är associerade med Prowlarrs uppdateringsskript.

> Om du använder Docker kommer detta vara tomt eftersom du bör uppdatera genom att ladda ner en ny Docker-bild.
{.is-info}

- Uppdatera - Detta kommer att uppdatera den aktuella sidan och visa eventuellt nyss skapade loggar.
- Radera - Detta kommer att rensa alla loggar och låta dig börja om från början.
- Filnamn - Detta kommer att visa filnamnet som är associerat med loggen.
- Senast skrivet - Detta är den lokala tiden då denna specifika loggfil skrevs.
  - Prowlarr använder rullande loggfiler som är begränsade till 1 MB var. Den nuvarande loggfilen är alltid prowlarr.txt, för de andra filerna är prowlarr.0.txt den näst nyaste (ju högre nummer desto äldre är den) upp till totalt 51 loggfiler. Denna loggfil innehåller `fatal`, `error`, `warn` och `info`-poster.
  - När felsökningsloggning är aktiverad kommer ytterligare prowlarr.debug.txt rullande loggfiler att finnas, upp till 51 filer. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info` och `debug`-poster. De täcker vanligtvis en ~40-timmarsperiod.
  - När spårningsloggning är aktiverad kommer ytterligare prowlarr.trace.txt rullande loggfiler att finnas, upp till 51 filer. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info`, `debug` och `trace`-poster. På grund av spårningsvolymen täcker de bara ett par timmar som mest.