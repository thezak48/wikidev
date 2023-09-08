---
title: Readarr Snabbstartsguide
description: 
published: true
date: 2022-09-07T23:19:05.590Z
tags: readarr
editor: markdown
dateCreated: 2021-12-11T19:42:31.825Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Snabbstartsguide för installation](#snabbstartsguide-för-installation)
- [Uppstart](#uppstart)
- [Mediehantering](#mediehantering)
- [Boknamn](#boknamn)
- [Mappar](#mappar)
- [Importering](#importering)
- [Filhantering](#filhantering)
- [Rotmappar och Calibre-integration](#rotmappar-och-calibre-integration)
  - [Calibre Content Server (valfritt)](#calibre-content-server-valfritt)
  - [Calibre-integration](#calibre-integration)
- [Nedladdningsklienter](#nedladdningsklienter)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Hur du importerar ditt befintliga organiserade mediebibliotek](#hur-du-importerar-ditt-befintliga-organiserade-mediebibliotek)
  - [Importera befintligt media](#importera-befintligt-media)
- [Lägg till nya böcker](#lägg-till-nya-böcker)

# Snabbstartsguide för installation

> Denna sida är fortfarande under arbete och inte komplett. Bidrag är välkomna.

> För en mer detaljerad genomgång av alla inställningar, se [Readarr => Inställningar](/readarr/settings)
{.is-info}

I den här guiden kommer vi att försöka förklara den grundläggande installationen du behöver göra för att komma igång med Readarr. Vi kommer att hoppa över vissa alternativ som du kan se på skärmen. Om du vill fördjupa dig i dessa, se den lämpliga sidan i FAQ och dokumentationen för en fullständig förklaring.

> Observera att inom skärmbilderna och GUI-inställningarna är `orange` avancerade alternativ, så du måste klicka på `Visa avancerat` längst upp på sidan för att göra dem synliga.
{.is-warning}

# Uppstart

Efter installation och start öppnar du en webbläsare och går till `http://{din_ip_här}:8787`

![qs_startup.png](/assets/readarr/qs_startup.png)

# Mediehantering

Först ska vi titta på inställningarna för `Mediehantering` där vi kan ställa in våra önskade namngivnings- och filhanteringsinställningar.

`Inställningar` => `Mediehantering`

![mediamanagement.png](/assets/readarr/mediamanagement.png)

# Boknamn

![booknaming.png](/assets/readarr/booknaming.png)

- Aktivera/inaktivera omdöpning av dina böcker (istället för att lämna namnen som de är för närvarande eller som de var när du laddade ner dem).
- Om du vill att olagliga tecken ska ersättas eller tas bort (`\ / : * ? " < > | ~ - % & + { }`).
- Här väljer du namnkonventionen för de faktiska bokfilerna. Observera att namnet på bokmappen definieras här också.
- `(Avancerat alternativ) Här ställer du in namnkonventionen för författarmappen.`

> Detta gäller inte om Calibre används eftersom Calibre hanterar fil-/mappnamn med sin egen interna struktur.
{.is-info}

# Mappar

![folders.png](/assets/readarr/folders.png)

- (Avancerat alternativ) Skapa tomma författarmappar - Aktivera för att skapa tomma författarmappar när en ny författare läggs till i Readarr.
- (Avancerat alternativ) Ta bort tomma mappar - Aktivera för att ta bort tomma författarmappar när det inte finns några böcker kvar för den författaren.

> En av dessa rutor kan markeras, men de får INTE båda markeras.
{.is-warning}

> Detta gäller inte om Calibre används eftersom Calibre hanterar fil-/mappnamn med sin egen interna struktur.
{.is-info}

# Importering

![importing.png](/assets/readarr/importing.png)

- (Avancerat alternativ) Hoppa över kontroll av ledigt utrymme - Om det är aktiverat hoppas kontrollen av ledigt utrymme över innan importering.
- (Avancerat alternativ) Minsta lediga utrymme - Ange det minsta lediga utrymmet som disken måste ha innan importeringen stoppas.
- (Avancerat alternativ) Använd hårddisklänkar istället för kopior - Markera den här rutan för att använda hårddisklänkar istället för kopior (för torrents). Observera att detta är aktiverat som standard.

> Du bör använda detta så mycket som möjligt. För att hårddisklänkar ska kunna användas måste källan/målet vara på samma filsystem (disk, partition) och monteringspunkter. [Se TRaSH:s guide om hårddisklänkar för mer information](https://trash-guides.info/hardlinks/)
{.is-info}

- Importera extra filer - Om det är aktiverat importeras angivna extra filer som finns i bokens mapp när den importeras.
- (Avancerat alternativ) Importera extra filer - Om import av extra filer är aktiverat anger du en kommaseparerad lista med filändelser att importera.

> Om du använder Readarr för ljudböcker bör du lägga till .cue i den här listan, eftersom den innehåller din kapitelinformation!
{.is-info}

# Filhantering

![filemanagement.png](/assets/readarr/filemanagement.png)

- Böcker som har raderats från disken övervakas inte längre i Readarr.

- Ignorera raderade böcker - Markera den här rutan för att sluta övervaka böcker som har identifierats som raderade eller otillgängliga från Readarrs rotmapp.
- Ladda ner korrekta versioner och repacks - Om du vill uppgradera automatiskt till korrekta versioner och repacks. Använd `Föredrar inte` för att sortera efter föredragna ordpoäng över korrekta versioner och repacks.
  - Föredrar och uppgradera - Ranka repacks och korrekta versioner högre än icke-repacks och icke-korrekta versioner. Betrakta nya repacks och korrekta versioner som uppgraderingar av befintliga utgåvor.
  - Uppgradera inte automatiskt - Ranka repacks och korrekta versioner högre än icke-repacks och icke-korrekta versioner. Betrakta inte nya repacks och korrekta versioner som uppgraderingar av befintliga utgåvor.
  - Föredrar inte - Ignorera repacks och korrekta versioner. Du måste hantera eventuella preferenser för dessa med [Föredragna ord](#release-profiles).

> \* `KORREKT` - betyder att det fanns ett problem med den tidigare utgåvan. Nedladdningar som är märkta som KORREKT visar att problemen har åtgärdats i den utgåvan. Detta görs av en grupp som inte släppte originalversionen.
> \* `REPACK` - betyder att det fanns ett problem med den tidigare utgåvan och att det har åtgärdats av den ursprungliga gruppen. Nedladdningar som är märkta som REPACK visar att problemen har åtgärdats i den utgåvan. Detta görs av en grupp som släppte originalversionen.
{.is-info}

- (Avancerat alternativ) Övervaka rotmappar för filändringar - Markera den här rutan för att utlösa en omgenomsökning när det upptäcks att rotmappen har ändrats.
- (Avancerat alternativ) Omgenomsök författarmapp efter uppdatering - Välj när en omgenomsökning av en författarmapp ska utföras efter att författaren har uppdaterats.
  - Alltid - Omgenomsök författarmappar baserat på schemalagda uppgifter
  - Efter manuell uppdatering - Du måste manuellt omgenomsöka disken
  - Aldrig - Precis som det låter, omgenomsök aldrig författarmapparna.
- (Avancerat alternativ) Tillåt fingeravtryck - Välj hur fingeravtryck ska hanteras, vilket ger ökad noggrannhet vid matchning av böcker, på bekostnad av CPU/disktid.
  - Alltid - Använd alltid fingeravtryck om möjligt
  - Endast för nya importeringar - Använd bara fingeravtryck för nyimporterade utgåvor
  - Aldrig - Precis som det låter, använd aldrig fingeravtryck
- (Avancerat alternativ) Ändra filens datum - Ändra filens datum vid import/omgenomsökning
  - Ingen - Readarr ändrar inte datumet som visas i din filhanterare
  - Bokens utgivningsdatum - Datumet då boken släpptes.
- (Avancerat alternativ) Återvinningskorg - Bokfiler kommer att hamna här när de raderas istället för att raderas permanent
- (Avancerat alternativ) Städning av återvinningskorg - Så gammal en given fil kan vara innan den raderas permanent

> Det rekommenderas starkt att du använder en återvinningskorg. Det är lätt att radera filer, och det är enkelt att återställa dem om du använder återvinningskorgen.
{.is-warning}

# Rotmappar och Calibre-integration

![rootfolders1.png](/assets/readarr/rootfolders1.png)

Här lägger vi till rotmappen som Readarr kommer att använda för att importera ditt befintliga organiserade mediebibliotek och där Readarr kommer att importera (kopiera/hårddisklänka/flytta) ditt media efter att din nedladdningsklient har laddat ner det.

> **Användaren och gruppen som du har konfigurerat Readarr att köra som måste ha läs- och skrivrättigheter till denna plats.** {.is-info}

Du kan också välja att använda Calibre för att hantera ditt bibliotek på den här skärmen. Detta kräver att du kör Calibre Content Server. Detta är INTE Calibre-Web.

> Användare som inte använder Windows:
> \* Om du använder en NFS-montage, se till att `nolock` är aktiverat.
> \* Om du använder en SMB-montage, se till att `nobrl` är aktiverat.
{.is-warning}

> Om du ska använda Calibre måste böckerna som du vill att Readarr ska känna igen vid den ursprungliga biblioteksimporten **redan finnas i Calibre**. Böcker i mappen som inte finns i Calibre kommer att ignoreras. Hårddisklänkar används inte när Calibre-integration läggs till.
> **Observera att du inte kan lägga till Calibre-integration till en rotmapp efter att den har skapats.**
{.is-danger}

> Din nedladdningsklient laddar ner till en nedladdningsmapp, och Readarr importerar det till din mediamapp (slutdestination) som din mediaserver använder. Din nedladdningsmapp och mediamapp kan inte vara samma plats!
{.is-warning}

Glöm inte att spara dina ändringar.

## Calibre Content Server (valfritt)

Om du ska använda Calibre för att hantera dina böcker måste du konfigurera Calibre Content Server. Återigen, detta är inte Calibre-Web, utan en del av Calibre självt. Du måste köra Calibre och du måste konfigurera Content Server.

> Om du väljer att använda Calibre kan du inte ändra något i Calibres databas. Om du inte följer detta varning kommer du att behöva radera din Readarr-databas och börja om.
{.is-danger}

Om du använder docker måste din monterade Calibre-bokmapp och din monterade Readarr-bokmapp vara samma.

> Observera att medan Readarr är i beta rekommenderas det att du inaktiverar omdöpning i Readarr om en oavsiktlig bugg skulle smyga sig igenom.
{.is-info}

För att göra detta öppnar du Calibre och klickar på `Inställningar / Delning över nätet`

![calibreprefs.png](/assets/readarr/calibreprefs.png)

Lägg först till ett användarkonto. Kontot MÅSTE ha åtkomst för att "göra ändringar".

![calibreacct.png](/assets/readarr/calibreacct.png)

Därefter måste du starta om Calibre. När du är tillbaka konfigurerar du och startar upp innehållsservern. Den bör visa att den körs. Ställ in den så att den körs automatiskt vid uppstart. Efter att du har sparat måste du starta om Calibre igen. Se till att servern är igång när den startar upp igen, sedan kan du gå vidare till nästa avsnitt.

> Du måste välja "Kräv användarnamn och lösenord för att komma åt innehållsservern" för att Readarr ska fungera korrekt. Om du inte gör det kommer du att få ett felmeddelande som säger "Anonyma användare får inte göra ändringar" när Readarr importerar en bok!
{.is-info}

![calibreserver.png](/assets/readarr/calibreserver.png)

## Calibre-integration

![calibre1.png](/assets/readarr/calibre1.png)

Nedan finns inställningar som är specifika för Calibre och visas endast om `Använd Calibre` är aktiverat

- Använd Calibre - Aktivera/inaktivera användningen av Calibre Content Server för att hantera din rotmapp.

> \* Observera att detta **inte kan aktiveras för en befintlig rotmapp**.
> \* Observera att detta **inte kan inaktiveras för en befintlig rotmapp med Calibre-integration**.
> \* Observera att detta kräver **Calibre Content Server** och fungerar inte med Calibre Web eller Calibre.
> \* Observera att hårddisklänkar inte fungerar med Calibre-integration.
> \* Observera att Calibre måste ha `Kräv användarnamn och lösenord för att komma åt innehållsservern` aktiverat.
> \* Om du inte har `Kräv användarnamn och lösenord för att komma åt innehållsservern` aktiverat i Calibre kommer du att få ett felmeddelande som säger "Anonyma användare får inte göra ändringar"
{.is-warning}

> Om du väljer att använda Calibre kan du inte ändra något i Calibres databas. Om du inte följer detta varning kommer du att behöva radera din Readarr-databas och börja om.
{.is-danger}

- Calibre-värd - IP/domän för värd för Calibre Content Server
- Calibre-port - Porten som Calibre Content Server lyssnar på
- (Avancerat) Calibre URL-bas - Lägg till ett prefix till Calibre URL, t.ex. `http://[värd]:[port]/[urlBase]`
- Calibre-användarnamn - Användarnamn för att komma åt Calibre Content Server
- Calibre-lösenord - Lösenord för att komma åt Calibre Content Server
- Calibre-bibliotek - Namn på Calibre Content Server-biblioteket. Lämna tomt för standard
- Konvertera till format - (Valfritt) Be Calibre Content Server att konvertera till andra format med en kommaseparerad lista.
  - Granska (i)-ikonen i appen för en aktuell lista över alternativ.
  - Alternativen är: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-utdataprofil - Välj utdataprofilen för Calibre Content Server att använda
  - Utdataprofilen talar om för Calibre Content Server-konverteringssystemet hur dokumentet ska optimeras för den angivna enheten (t.ex. genom att ändra storlek på bilder för enhetens skärmstorlek). I vissa fall kan en utdataprofil användas för att optimera utdata för en specifik enhet, men detta är sällan nödvändigt.
- Använd SSL - Aktivera eller inaktivera användningen av SSL (HTTPS) för Calibre Content Server

> Om du lägger till en enskild bok och väljer `Ingen`\* för [metadataprofilen](/readarr/settings#metadata-profiles), kommer endast den boken att visas under författaren när den läggs till. Om du vill lägga till andra böcker för den författaren, välj en lämplig metadataprofil.
> \* **Observera att `Ingen` inte tillämpar några metadatafilter och du kan få oönskade utländska utgåvor. För att komma runt detta [skapa en metadataprofil enligt anvisningarna i FAQ](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Nedladdningsklienter

`Inställningar` => `Nedladdningsklienter`

Nedladdning och import är där de flesta människor upplever problem. Från ett övergripande perspektiv måste programvaran kunna kommunicera med din nedladdningsklient och ha åtkomst till de filer den laddar ner. Det finns många olika nedladdningsklienter som stöds och ännu fler olika inställningar. Det innebär att det finns några vanliga inställningar, men det finns ingen rätt inställning och varje persons inställning kan vara lite annorlunda. Men det finns många felaktiga inställningar.

> Se [inställningssidan](/readarr/settings#download-clients), sidan [Mer information (stöd)](/readarr/supported#download-clients) för den här sektionen och [TRaSH:s guider för nedladdningsklienter](https://trash-guides.info/Downloaders/) för mer information.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Readarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Readarr övervakar dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Den övervakar detta via din nedladdningsklients API.
- När nedladdningen är klar vet Readarr den slutliga filplatsen enligt rapporterad av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp och åtkomlig av Readarr.
- Readarr skannar den avslutade filplatsen efter filer som Readarr kan använda. Den analyserar filnamnet för att matcha det mot det begärda mediet. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den angivna medieplatsen.
- Atomiska flyttar (direkta flyttar) är aktiverade som standard. Filsystemet och monteringspunkterna måste vara desamma för din avslutade nedladdningsmapp och ditt mediebibliotek. Om den atomiska flytten misslyckas eller din konfiguration inte stöder hårddisklänkar och atomiska flyttar kommer Readarr att använda kopiering och sedan radera filen från källan, vilket är I/O-intensivt.
- Om alternativet "Hantering av slutförda nedladdningar - Ta bort" är aktiverat i Readarrs inställningar kommer överblivna filer från nedladdningen att skickas till papperskorgen eller återvinningen genom en begäran till din klient att ta bort utgåvan.

### BitTorrent

{#bittorrent}

- Readarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, osv.
- Readarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Denna övervakning sker via din nedladdningsklients API.
- Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (förhållande eller tid kan justeras i nedladdningsklienten eller från Readarr under den specifika nedladdningsklienten). När filer importeras till din mediamapp kommer Readarr att skapa en hårdlänk till filen om det stöds av din konfiguration, annars kopieras filen om hårdlänkar inte stöds.
- Hårdlänkar är aktiverade som standard. [En hårdlänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringspunkterna måste vara desamma för din slutförda nedladdningsmapp och din mediebibliotek. Om skapandet av hårdlänken misslyckas eller om din konfiguration inte stöder hårdlänkar kommer Readarr att falla tillbaka och kopiera filen.
- Om alternativet "Hantering av slutförda nedladdningar - Ta bort" är aktiverat i Readarrs inställningar kommer Readarr att ta bort torrenten från din klient och be klienten att ta bort torrentdata, men endast om klienten rapporterar att seedningen är slutförd och torrenten är stoppad (pausad vid slutförandet).

# Hur du importerar ditt befintliga organiserade mediebibliotek

> Observera att Readarr inte regelbundet söker efter böcker. Se dessa två FAQ-inlägg för detaljer för att förstå hur Readarr fungerar.
[Hur hittar Readarr böcker?](/readarr/faq#hur-hittar-readarr-böcker) och [Hur fungerar Readarr?](/readarr/faq#hur-fungerar-readarr)
{.is-info}

När du har konfigurerat dina profiler/kvalitetsstorlekar och lagt till dina indexerare och nedladdningsklient(er) är det dags att importera ditt befintliga organiserade mediebibliotek.

Kommer snart - Bidrag välkomnas

## Importera befintligt media

Kommer snart - Bidrag välkomnas

# Lägg till nya böcker

[Hänvisa till bibliotekssidan för ytterligare information](/readarr/library#lägg-till-nya)