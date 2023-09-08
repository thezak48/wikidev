---
title: Radarr Snabbstartsguide
description: 
published: true
date: 2023-08-27T22:14:05.687Z
tags: radarr, snabbstart
editor: markdown
dateCreated: 2021-06-20T20:05:44.814Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Snabbstartsguide för installation](#snabbstartsguide-för-installation)
- [Uppstart](#uppstart)
- [Mediehantering](#mediehantering)
  - [Filnamn för filmer](#filnamn-för-filmer)
  - [Importera](#importera)
  - [Filhantering](#filhantering)
  - [Rotmappar](#rotmappar)
- [Profiler](#profiler)
- [Kvalitet](#kvalitet)
- [Indexerare](#indexerare)
- [Nedladdningsklienter](#nedladdningsklienter)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Hur du importerar ditt befintliga organiserade mediebibliotek](#hur-du-importerar-ditt-befintliga-organiserade-mediebibliotek)
  - [Importera filmer](#importera-filmer)
  - [Importera befintligt media](#importera-befintligt-media)
    - [Ingen matchning hittades](#ingen-matchning-hittades)
    - [Fixa felaktigt mappnamn efter import](#fixa-felaktigt-mappnamn-efter-import)
  - [Hur du lägger till en film](#hur-du-lägger-till-en-film)

# Snabbstartsguide för installation

> Denna sida är fortfarande under arbete och inte komplett. Bidrag är välkomna.

> För en mer detaljerad genomgång av alla inställningar, se [Radarr => Inställningar](/radarr/settings)
{.is-info}

I denna guide kommer vi att försöka förklara den grundläggande installationen du behöver göra för att komma igång med Radarr. Vi kommer att hoppa över vissa alternativ som du kan se på skärmen. Om du vill gå djupare in på dessa, se den lämpliga sidan i FAQ och dokumentationen för en fullständig förklaring.

> Observera att inom skärmbilderna och GUI-inställningarna i `orange` finns avancerade alternativ, så du måste klicka på `Visa avancerat` längst upp på sidan för att göra dem synliga.
{.is-warning}

# Uppstart

Efter installation och start öppnar du en webbläsare och går till `http://{din_ip_här}:7878`

![Radarr-start.png](/assets/radarr/Radarr-start.png)

# Mediehantering

Först ska vi titta på inställningarna för `Mediehantering` där vi kan ställa in våra önskade namngivnings- och filhanteringsinställningar.

`Inställningar` => `Mediehantering`

![Radarr-settings-mm.png](/assets/radarr/Radarr-settings-mm.png)

## Filnamn för filmer

![Radarr-settings-mm-movie-naming.png](/assets/radarr/Radarr-settings-mm-movie-naming.png)

1. Aktivera/inaktivera namnändring av dina filmer (istället för att behålla namnen som de är eller som de var när du laddade ner dem).
2. Om du vill ersätta eller ta bort otillåtna tecken (`\ / : * ? " < > | ~ # % & + { }`).
3. Denna inställning styr hur Radarr hanterar kolon i filnamnet.
4. Här väljer du namnkonventionen för de faktiska filerna för filmen.
5. *(Avancerat alternativ) Här ställer du in namnkonventionen för mappen som innehåller videofilen.*

> Om du vill ha ett rekommenderat namnschema och exempel, se [TRaSH's rekommenderade namnscheman](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/).
{.is-info}

## Importera

![Radarr-settings-mm-importing.png](/assets/radarr/Radarr-settings-mm-importing.png)

1. *(Avancerat alternativ) Aktivera `Använd hårddisklänkar istället för att kopiera` för mer information om hur och varför med exempel, se [TRaSH's guide för hårddisklänkar](https://trash-guides.info/hardlinks).
1. *(Avancerat alternativ) Importera matchande extrafiler (undertexter, nfo, etc.) efter att en fil har importerats.*

## Filhantering

![Radarr-settings-mm-fm.png](/assets/radarr/Radarr-settings-mm-fm.png)

1. Filmer som har raderats från disken avmarkeras automatiskt i Radarr.
    - Du kanske vill ta bort en film men vill inte att Radarr ska ladda ner filmen igen. Du skulle använda detta alternativ.
1. *(Avancerat alternativ) Ange en plats för borttagna filer att gå till (ifall du vill återställa dem innan papperskorgen töms).*
1. *(Avancerat alternativ) Detta är hur gammal en given fil kan vara innan den raderas permanent.*

## Rotmappar

![Radarr-settings-mm-root-folder.png](/assets/radarr/Radarr-settings-mm-root-folder.png)

Här lägger vi till rotmappen som Radarr kommer att använda för att importera ditt befintliga organiserade mediebibliotek och där Radarr kommer att importera (kopiera/hårddisklänka/flytta) ditt media efter att din nedladdningsklient har laddat ner det.

> \* Ej Windows: Om du använder en NFS-mapp, se till att `nolock` är aktiverat.
> \* Om du använder en SMB-mapp, se till att `nobrl` är aktiverat.
{.is-warning}

> **Användaren och gruppen som du har konfigurerat Radarr att köra som måste ha läs- och skrivrättigheter till denna plats.** {.is-info}

> Din nedladdningsklient laddar ner till en nedladdningsmapp och Radarr importerar det till din mediamapp (slutdestination) som din mediaserver använder.
{.is-info}

> **Din nedladdningsmapp och din media (bibliotek/rot) mapp kan inte vara samma plats**
{.is-danger}

Glöm inte att spara dina ändringar

# Profiler

`Inställningar` => `Profiler`

![Radarr-settings-profiles.png](/assets/radarr/Radarr-settings-profiles.png)

Här kan du konfigurera profiler för kvalitet, önskat språk och anpassad formatbedömning för en film du vill ladda ner.

Vi rekommenderar att du skapar dina egna profiler och bara väljer de kvalitetskällor och språk du verkligen vill ha.

För mer information om utländska titlar och språk, se [denna FAQ-post](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

Många användare tycker att [TRaSH's guide för anpassade format och språk](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) är till hjälp för att specificera vilka språk de vill ha för filmer.

Profiler är också där anpassade formatbedömningar konfigureras. Det rekommenderas starkt att lägga till nedanstående anpassade format från [TRaSH's guider](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) för att undvika oönskade nedladdningar. Se den länkade TRaSH-guiden för anpassade format och ytterligare 3 refererade TRaSH-guider för anpassade format längst upp på sidan för samlingen av anpassade format för mer information.

- [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) undviker att hämta utgåvor med Dolby Vision (DV) som har en grön nyans om DV inte stöds.
- [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) undviker att hämta dåligt namngivna BR-DISKs som inte matchar BR-DISK-kvalitetsanalysen.

> Mer information finns på [Inställningar => Profiler](/radarr/settings#profiles).
> För att se skillnaden mellan kvalitetskällorna, se [våra kvalitetsdefinitioner](/radarr/settings#qualities-defined).
{.is-info}

# Kvalitet

`Inställningar` => `Kvalitet`

![Radarr-settings-quality.png](/assets/radarr/Radarr-settings-quality.png)

Här kan du ändra/finajustera minsta och största storlek på dina önskade mediefiler (när du använder Usenet, tänk på RAR/PAR2-filerna)

> Om du behöver hjälp med vilka inställningar du ska använda för kvalitetsinställningar, se [TRaSH's rekommendationer för storlek](https://trash-guides.info/Radarr/Radarr-Quality-Settings-File-Size/) för ett testat exempel.
{.is-info}

# Indexerare

`Inställningar` => `Indexerare`

![Radarr-settings-indexers.png](/assets/radarr/Radarr-settings-indexers.png)

Här lägger du till indexeraren/spåraren som du kommer att använda för att faktiskt ladda ner dina filer.

När du har klickat på <kb>+</kb>-knappen för att lägga till en ny indexerare kommer du att få upp ett nytt fönster med många olika alternativ. För wikiändamål betraktar Radarr både Usenet-indexerare och torrentspårare som "indexerare".

Här finns två avsnitt: Usenet och Torrents. Beroende på vilken nedladdningsklient du kommer att använda vill du välja vilken typ av indexerare du ska använda.

För torrentspårare - nästan alla kräver användning av [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett).

# Nedladdningsklienter

`Inställningar` => `Nedladdningsklienter`

![Radarr-settings-download-clients.png](/assets/radarr/Radarr-settings-download-clients.png)

Nedladdning och import är där de flesta människor upplever problem. På en övergripande nivå måste programvaran kunna kommunicera med din nedladdningsklient och ha läs- och skrivrättigheter till platsen där nedladdningsklienten rapporterar filer som klienten laddar ner. Det finns många olika nedladdningsklienter som stöds och ännu fler olika inställningar. Det innebär att det finns några vanliga inställningar, men det finns ingen rätt inställning och varje persons inställning kan vara lite annorlunda. Men det finns många felaktiga inställningar.

> Se [inställningssidan](/radarr/settings#download-clients), på sidan [Mer information (stödda)](/radarr/supported#download-clients) för detta avsnitt och [TRaSH's guider för nedladdningsklienter](https://trash-guides.info/Downloaders/) för mer information.
{.is-info}

## Nedladdningsprotokoll {.tabset}

### Usenet

{#usenet}

- Radarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Radarr övervakar dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Övervakningen sker via din nedladdningsklients API.
- När nedladdningen är klar känner Radarr till den slutliga filplatsen enligt rapporten från din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp och åtkomlig av Radarr.
- Radarr skannar den färdiga filplatsen efter filer som Radarr kan använda. Den analyserar filnamnet för att matcha det mot det begärda mediet. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den angivna medieplatsen.
- Atomiska flyttar (direktflyttar) är aktiverade som standard. Filsystemet och monteringspunkterna måste vara desamma för din färdiga nedladdningsmapp och ditt mediebibliotek. Om den atomiska flytten misslyckas eller din konfiguration inte stöder hårddisklänkar och atomiska flyttar kommer Radarr att falla tillbaka och kopiera filen och sedan ta bort den från källan, vilket är intensivt för I/O.
- Om alternativet "Hantering av färdig nedladdning - Ta bort" är aktiverat i Radarrs inställningar kommer överblivna filer från nedladdningen att skickas till papperskorgen eller återvinningen genom en begäran till din klient att ta bort nedladdningen.

### BitTorrent

{#bittorrent}

- Radarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Radarr övervakar dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Övervakningen sker via din nedladdningsklients API.
- Färdiga nedladdningar som fortfarande seedas lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (kvot eller tid kan justeras i nedladdningsklienten eller från Radarr under den specifika nedladdningsklienten). När filer importeras till din mediamapp kommer Radarr att skapa en hårddisklänk om det stöds av din konfiguration eller kopiera om hårddisklänkar inte stöds. Torrenter som är pausade och har slutfört seedningen kommer att atomiskt flyttas om hårddisklänkar stöds eller kopieras och raderas om de inte stöds.
- Hårddisklänkar är aktiverade som standard. [En hårddisklänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringspunkterna måste vara desamma för din färdiga nedladdningsmapp och ditt mediebibliotek. Om skapandet av hårddisklänken misslyckas eller din konfiguration inte stöder hårddisklänkar kommer Radarr att falla tillbaka och kopiera filen.
- Om alternativet "Hantering av färdig nedladdning - Ta bort" är aktiverat i Radarrs inställningar kommer Radarr att ta bort torrenten från din klient och be klienten att ta bort torrentdata, men endast om klienten rapporterar att seedningen är klar och torrenten är stoppad (pausad vid slutförandet).

# Hur du importerar ditt befintliga organiserade mediebibliotek

> Observera att Radarr inte söker efter filmer regelbundet. Se FAQ-posten [Hur fungerar Radarr?](/radarr/faq#how-does-radarr-work) för detaljer om hur Radarr fungerar.
{.is-info}

Efter att ha ställt in dina profiler/kvalitetsstorlekar och lagt till dina indexerare och nedladdningsklient(er) är det dags att importera ditt befintliga organiserade mediebibliotek.

`Filmer`

![Radarr-movies.png](/assets/radarr/Radarr-movies.png)

Välj `Importera befintliga filmer` eller välj `Importera` i sidofältet.

## Importera filmer

![Radarr-movies-import.png](/assets/radarr/Radarr-movies-import.png)

Välj den rotmapp du lade till tidigare [i avsnittet om rotmappar.](#rot-folders)

## Importera befintligt media

![Radarr-importing-existing.png](/assets/radarr/Radarr-importing-existing.png)

Beroende på hur väl dina befintliga filmmappar är namngivna kommer Radarr att försöka matcha dem med rätt film som visas i nr. 5. Om alla dina filmer finns i en enda mapp följ denna [guide](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

1. Namnet på din filmmapp.
1. Övervaka - Hur du vill att filmen ska läggas till i Radarr.

- Ingen - Övervaka varken filmen eller samlingen för nya utgåvor
- Endast film - Övervaka endast filmen för nya utgåvor
- Film och samling - Övervaka både filmen för nya utgåvor och lägg till och övervaka eventuella filmer i filmens samling (om den finns)

1. Tillgänglighet - När Radarr anser att en film är tillgänglig.

- **Tillkännagiven**: Radarr anser att filmer är tillgängliga så snart de har lagts till i Radarr. Denna inställning är *rekommenderad* om du har bra privata indexerare som inte har fejkade utgåvor.
- **I biograferna**: Radarr anser att filmer är tillgängliga så snart de har premiär på biograferna. Denna inställning rekommenderas *inte*.
- **Släppt**: Radarr anser att filmer är tillgängliga så snart Blu-ray-skivan släpps. Denna inställning är *rekommenderad* om dina indexerare ofta innehåller fejkade utgåvor.

1. Kvalitetsprofil - Välj din önskade profil att använda.
1. Film - Vad Radarr tror att filmen matchade. Det är viktigt att du granskar detta och redigerar/söker om matchningen inte är korrekt. Felmatchningar orsakas ofta av dåligt namngivna mappar.
1. Massmarkera övervakningsstatus.
1. Massmarkera minsta tillgänglighet.
1. Massmarkera kvalitetsprofil.
1. Börja importera ditt befintliga mediebibliotek.

När en film har lagts till i Radarr kommer Radarr att skanna filmens mapp och försöka matcha en videofil i mappen med filmen. Den vanligaste orsaken till att Radarr inte matchar filen och filmen har statusen "Saknas" i Radarr är att filnamnet inte innehåller året. Radarr kräver att året finns i filnamnet för att kunna analysera det.

### Ingen matchning hittades

Om du får ett felmeddelande som detta

![Radarr-importing-existing-no-match.png](/assets/radarr/Radarr-importing-existing-no-match.png)

Då har du förmodligen gjort ett fel med namngivningen av dina filmmappar.

För att åtgärda detta kan du försöka följande

Expandera felmeddelandet

![Radarr-importing-existing-no-match-expand.png](/assets/radarr/Radarr-importing-existing-no-match-expand.png)

och kontrollera på [themoviedb](https://www.themoviedb.org/) om året eller titeln matchar. I detta exempel kan du se att året är felaktigt och du kan ändra det genom att ändra året och klicka på uppdateringsikonen.

![radarr-importing-existing-no-match-expand-refresh.png](/assets/radarr/radarr-importing-existing-no-match-expand-refresh.png)

Eller så kan du bara använda tmdb:id eller imdb:id (om tmdb är länkat till imdb) och sedan välja den hittade filmen om den matchar.

![Radarr-importing-existing-no-match-expand-tmdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-tmdb.png)

![Radarr-importing-existing-no-match-expand-imdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-imdb.png)

### Fixa felaktigt mappnamn efter import

![Radarr-wrong-folder-name.png](/assets/radarr/Radarr-wrong-folder-name.png)

Du kommer att märka att efter att vi har fixat under importen så har mappnamnet fortfarande fel år i det. För att fixa detta ska vi göra en liten magisk trick.

Gå till filmöversikten

`Filmer`

Klicka på `Filmredigerare` längst upp

![Radarr-movie-editor.png](/assets/radarr/Radarr-movie-editor.png)

Efter att ha aktiverat det väljer du filmen/filmerna från vilken du vill ha mapparna omdöpta.

![Radarr-movie-editor-select.png](/assets/radarr/Radarr-movie-editor-select.png)

1. Om du vill att alla dina filmmappar ska döpas om till ditt tidigare inställda mappnamnsschema [sektionen för filnamn](#movie-naming).
2. Välj filmen/filmerna från vilken du vill ha mapparna omdöpta.
3. Välj samma `Rotmapp`

En ny popup visas

![Radarr-movie-editor-move-files-yes.png](/assets/radarr/Radarr-movie-editor-move-files-yes.png)

Välj `Ja, flytta filerna`

Sedan magi

![Radarr-correct-folder-name.png](/assets/radarr/Radarr-correct-folder-name.png)

Som du kan se har mappen döpts om till rätt år enligt ditt namngivningsschema.

## Hur man lägger till en film

Efter att du har importerat ditt befintliga välorganiserade mediebibliotek är det dags att lägga till de filmer du vill ha.

`Filmer` => `Lägg till ny`

![Radarr-add-new.png](/assets/radarr/Radarr-add-new.png)

Skriv in filmen du vill ha i rutan eller använd tmdb:id eller imdb:id.

När du skriver in filmnamnet kommer du att se att det börjar visa resultat.

![Radarr-movie-search.png](/assets/radarr/Radarr-movie-search.png)

När du ser den film du vill ha klickar du på den.

![Radarr-movie-add.png](/assets/radarr/Radarr-movie-add.png)

1. Rotmapp - Radarr kommer att lägga till filmen i den rotmapp du har ställt in [i rotmapparna](#root-folders)
1. Övervaka - Hur du vill att filmen ska läggas till i Radarr.

- Endast film = Radarr kommer att övervaka RSS-flödet efter filmen i ditt bibliotek som du inte har (ännu) eller uppgradera den befintliga filmen till bättre kvalitet.
- Film och samling = Radarr kommer att övervaka RSS-flödet efter filmen i ditt bibliotek som du inte har (ännu) eller uppgradera den befintliga filmen till bättre kvalitet. Den kommer också att lägga till alla filmer i denna films samling (om det finns några) med dina valda inställningar.
- Ingen = Radarr kommer inte att övervaka RSS-flödet, eventuella uppgraderingar eller nya filmer kommer att ignoreras och måste göras manuellt. Alla sökningar efter oövervakade filmer måste vara manuellt utlösta sökningar eller interaktiva sökningar.

1. Tillgänglighet - När Radarr ska anse att en film är tillgänglig.

> För mer information om TMDB:s datum som påverkar nedanstående tillgängligheter, se [Hur bestämmer Radarr året för en film](#how-does-radarr-determine-the-year-of-a-movie)
{.is-info}

- **Tillkännagiven**: Radarr ska anse att filmer är tillgängliga så snart de läggs till i Radarr. Denna inställning rekommenderas om du har bra privata spårare (eller riktigt bra offentliga, t.ex. rarbg.to) som inte har fejkade filmer.
- **På bio**: Radarr ska anse att filmer är tillgängliga så snart de visas på bio (Biografdatum på TMDb). Denna inställning rekommenderas inte.
- **Släppt**: Radarr ska anse att filmer är tillgängliga så snart Blu-Ray- eller streamingversionen släpps (Digitala och fysiska datum på TMDb). Denna inställning rekommenderas och bör förmodligen kombineras med en Tillgänglighetsfördröjning på `-14` eller `-21` dagar.
  - Om TMDb inte har ett datum, antas det att filmen är tillgänglig 90 dagar efter `Biografdatum` (Äldsta datum på bio) på webben eller fysiska tjänster.

1. Kvalitetsprofil - Välj din profil att använda för denna film
1. Taggar - Här kan du lägga till vissa taggar för avancerad användning.
1. Sök vid tillägg - Se till att du aktiverar detta om du vill att Radarr ska söka efter den saknade filmen när den läggs till i Radarr [mer information](/radarr/faq#how-does-radarr-find-movies)
1. Klicka på `Lägg till film` för att lägga till filmen i Radarr.

- Om du får ett felmeddelande "sökvägen är redan konfigurerad" [se den här FAQ-posten](/radarr/faq#path-is-already-configured-for-an-existing-movie)