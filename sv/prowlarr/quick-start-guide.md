---
title: Prowlarr Snabbstartsguide
description: 
published: true
date: 2023-04-06T16:04:33.682Z
tags: 
editor: markdown
dateCreated: 2023-04-06T16:04:33.682Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Indexer](#indexer)
- [Appar](#appar)
  - [Appinställningar](#appinställningar)
- [Nedladdningsklienter](#nedladdningsklienter)
  - [Usenet-klientinställningar](#usenet-klientinställningar)
  - [Torrent-klientinställningar](#torrent-klientinställningar)
  - [Testa nedladdningsklienten](#testa-nedladdningsklienten)
- [Installationen är klar](#installationen-är-klar)

> Denna sida är fortfarande under arbete och inte komplett.

> För en mer detaljerad genomgång av alla inställningar, se [Prowlarr => Inställningar](/prowlarr/settings)

I denna guide kommer vi att försöka förklara den grundläggande installationen du behöver göra för att komma igång med Prowlarr. Vi kommer att hoppa över vissa alternativ som du kan se på skärmen. Om du vill gå djupare in på dessa, se den lämpliga sidan i FAQ och dokumentationen för en fullständig förklaring.

> Observera att inom skärmbilderna och GUI-inställningarna i `orange` finns avancerade alternativ, så du måste klicka på `Visa avancerat` längst upp på sidan för att göra dem synliga.

# Indexer

Det första du behöver göra i Prowlarr är att ställa in indexers. Du kommer att lägga till varje indexer individuellt i Prowlarr.

Klicka på `Indexer` och klicka sedan på + för att lägga till en ny indexer.

![addindexer.png](/assets/prowlarr/addindexer.png)

Alla indexers du kan lägga till (usenet och torrent) listas, och du kan skriva för att delvis matcha någon befintlig post. Om indexeraren du vill lägga till inte finns i listan kan du lägga till "Generic Newznab" (för usenet) eller "Generic Torznab" (för torrents).

![addgeneric.png](/assets/prowlarr/addgeneric.png)

Vissa indexers har speciella inställningar, men de flesta är standard som visas.

![addnewindexer.png](/assets/prowlarr/addnewindexer.png)

- Namn - Välj ett namn för denna indexer. När den synkroniseras med dina appar kommer den att lägga till `(Prowlarr)` efter namnet.
- Aktivera - Markera rutan för att aktivera denna indexer.
- Omdirigering - Markera rutan om en omdirigering krävs. Det finns bara ett par indexers där detta krävs för att undvika att bli förbjuden. Om det är aktiverat skickas hämtlänken direkt till applikationen istället för att omdirigeras via Prowlarr.

> Omdirigering behövs vanligtvis bara för ett fåtal mycket specifika indexers.

- Synkroniseringsprofil - Välj din synkroniseringsprofil här. Dessa kan skapas i [`Inställningar` => `Appar`](/prowlarr/settings#applications). Standardprofilen finns redan och ser ut så här:

> Du kan ha olika inställningar per app genom att skapa flera instanser av indexeraren.

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Välj URL:en som Prowlarr ska använda. Om den är tom används standard-/första URL:en.
- Hämtlänk - Om du lägger till en torrent-indexer kan du behöva välja vilken typ av hämtlänk du vill använda.
- (Avancerat alternativ) API-sökväg - Sökväg till indexerarens API. Vanligtvis `/api`
- Autentisering - Många indexers och spårare kräver att du autentiserar/loggar in på något sätt. Du kan behöva ange en API-nyckel, RSS-nyckel, session-id, cookie eller andra autentiseringsuppgifter från din indexerare (vanligtvis hittas på din profil eller under säkerhet), välja sökordning eller andra alternativ för din specifika indexerare.
  - API-nyckel
  - RSS-nyckel
  - Session-ID
  - Cookie
  - Användarnamn/lösenord
  - osv.
- (Avancerat alternativ) Ytterligare parametrar - Ytterligare parametrar att lägga till i förfrågningarna för denna indexerare.
- VIP-utgång - Ange datumet i ISO-format (yyyy-MM-DD) för att bli meddelad 1 vecka innan utgången; lämna annars tomt
- Taggar - Använd taggar för att ange standardnedladdningsklienter, ange indexerproxys, ange indexers till appar eller bara för att organisera dina indexers.
- (Avancerat alternativ) Frågebegränsning - Om din indexerare begränsar dina API-anrop per dag kan du ange det antalet här för att undvika att överskrida gränsen.
- (Avancerat alternativ) Hämtbegränsning - Om din indexerare begränsar dina hämtningar per dag kan du ange det antalet här för att undvika att överskrida gränsen. När hämtbegränsningen är nådd kommer ytterligare förfrågningar att utlösa ett oväntat undantag i \*Arr-apparna. Andra appar kan variera.
- (Avancerat alternativ) Seedningsförhållande - Endast för torrent-indexerare: Förhållandet en torrent bör nå innan den stoppas, tom är appens standard
- (Avancerat alternativ) Seedningstid - Endast för torrent-indexerare: Tiden en torrent bör seedas innan den stoppas, tom är appens standard
- (Avancerat alternativ) Indexerarprioritet - Välj indexerareprioritet här från 1-50 (1 är högst). Dessa prioriteringar synkroniseras med dina appar.

Testa din post. Om en grön bock visas kan du spara din post och upprepa vid behov för varje indexerare du vill att Prowlarr ska använda. Om det misslyckas måste du kontrollera loggen för felet (URL, API-nyckel osv.).

# Appar

Efter att du har lagt till dina indexerare ansluter vi sedan Prowlarr till dina andra appar.

Klicka på `Inställningar` => `Appar` och klicka sedan på + för att lägga till en stödd app.

![addapps.png](/assets/prowlarr/addapps.png)

Alla program du kan lägga till listas. Du bör bara lägga till program som du redan har installerade, och om du har flera instanser av dem måste du lägga till var och en av dem separat.

> För närvarande stödda appar finns på sidan [Mer information (Stödda)](/prowlarr/supported#applications) för denna sektion

När du lägger till en app måste du ange värden i popup-rutan:

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Observera: Indexerare synkroniseras baserat på de kapabiliteter/kategorier de påstår sig stödja. Om en indexerare bara stöder `tv`-kategorier kommer den inte att synkroniseras med Lidarr, Radarr och Readarr. Den kommer bara att synkroniseras med Sonarr. "Stödda" kategorier kan väljas som en avancerad inställning per app. **Observera också att \*Arrs bara accepterar indexerare vars testförfrågningar returnerar resultat som innehåller minst en av de konfigurerade kategorierna.**

## Appinställningar

- Namn - Ange ett namn för denna app.
- Synkroniseringsnivå - Välj synkroniseringsnivå att använda
  - `Endast lägg till och ta bort` - När indexerare läggs till eller tas bort från Prowlarr kommer den att uppdatera denna fjärrapp. Om indexeraren är nere vid synkroniseringen kommer den att inaktiveras i den fjärrapp.
  - `Fullständig synkronisering` - Fullständig synkronisering kommer att hålla denna apps indexerare fullständigt synkroniserade. Ändringar som görs på indexerare i Prowlarr synkroniseras sedan till denna app. Eventuella ändringar som görs i inställningarna för dessa indexerare på FAQ-sidan inom denna app kommer att skrivas över av Prowlarr vid nästa synkronisering. En lista över faktorer som används för att jämföra och avgöra om en synkronisering ska ske finns i [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Inaktiverad` - kommer att förhindra att indexerare synkroniseras med programmet helt och hållet.

> `Fullständig synkronisering` innebär att Prowlarr kommer att skriva över de flesta inställningar, inklusive användarvalda kategorier som kan konfigureras i Prowlarr. Dock kommer inställningar som inte hanteras av Prowlarr inte att ändras. Dock kommer [nästan alla andra ändringar](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) att utlösa en synkronisering och skriva över motsvarande inställningar i \*Arr.
{.is-warning}

- Taggar - Om du har lagt till en tagg för din indexerare under installationen kommer endast indexerare med denna tagg att användas för denna programpost.
- Prowlarr-server - Ange Prowlarr-serverns URL (inklusive http, port och basurl om det behövs) som appen skulle använda här.

> Observera att om du använder en omvänd proxy måste du lägga till URL-basen här! Om du inte gör det kommer indexerarna att bli trasiga när de synkroniseras, och om du har valt att bara lägga till och ta bort kommer det inte att åtgärdas när du redigerar det!

- Appserver - Ange programserverns URL (inklusive http, port och basurl om det behövs) här. Ange URL-basen om den används.
- API-nyckel - Ange API-nyckeln för ditt program här. För \*Arrs hittar du den i Inställningar => Allmänt. Du kan få den från ditt program på fliken `Inställningar` => `Allmänt` och kopiera/klistra in den här.
- (Avancerad inställning) Synkronisera kategorier - Välj kategorierna som ska synkroniseras med denna app. Indexerare som stöder dessa kategorier kommer att synkroniseras.
  - Anpassade indexerarkategorier kartläggs till standardiserade Torznab/Newznab-kategorier, så sökningar efter standardiserade kategorier inkluderar alla underliggande anpassade kategorier. Anpassade indexerarkategorier listas för finjustering om du inte vill ha dem alla på en gång.

> När du sparar detta kommer det att synkronisera dina indexerare med appen. De läggs till med det namn du har valt för din indexerare plus (Prowlarr) efter det. t.ex. `{Indexer Name} (Prowlarr)`

![nzbgeek.png](/assets/prowlarr/nzbgeek.png)

Du bör sedan gå in i ditt program och inaktivera den icke-Prowlarr-versionen av indexeraren. När allt fungerar smidigt kan du ta bort dessa poster och lämna bara (Prowlarr)-versionerna på plats.

Du kan vilja gå in i dina program och kontrollera kategorierna för Prowlarr-indexerarna. Standardkategorier som ska kartläggas till appen kan konfigureras som en avancerad inställning för appen i Prowlarr.

> **Observera att anpassade/ickestandardiserade indexerarspecifika kategorier kartläggs till standardiserade, så sökningar med standardiserade kategorier kommer att inkludera alla anpassade kategorier**

## Synkroniseringsprofiler

Konfigurera synkroniseringsprofilerna att använda för (en) app(ar)

- Namn - Unikt namn för synkroniseringsprofilen
- Aktivera RSS - För indexerare med denna profil, aktivera RSS-sökningar/förfrågningar för \*Arr-appen
- Aktivera interaktiv sökning - För indexerare med denna profil, aktivera interaktiva (manuella) sökningar för \*Arr-appen
- Aktivera automatisk sökning - För indexerare med denna profil, aktivera automatiska sökningar för \*Arr-appen
- Minsta seeders - För indexerare med denna profil, minsta antal seeders som krävs för att \*Arr ska hämta en torrent

# Nedladdningsklienter (Prowlarr-sökningar)

> Om du avser att göra sökningar direkt i Prowlarr måste du lägga till nedladdningsklienter. Annars behöver du inte lägga till dem här. För sökningar från dina appar används de nedladdningsklienter som konfigurerats där.

> Nedladdningsklienter är endast för Prowlarr-sökningar i appen och synkroniseras inte med appar. Det finns inga planer på att lägga till en sådan funktion.

Klicka på `Inställningar` => `Nedladdningsklienter` och klicka sedan på + för att lägga till en ny nedladdningsklient. Din nedladdningsklient bör redan vara konfigurerad enligt denna guide.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

> För närvarande stödda nedladdningsklienter finns på sidan [Mer information (Stödda)](/prowlarr/supported#downloadclient) för denna sektion

Välj den nedladdningsklient du vill lägga till, och det kommer att visas en popup-ruta för att ange anslutningsdetaljer. Dessa detaljer är liknande för de flesta klienter. Vissa kommer att be om ett användarnamn eller lösenord, vissa kommer att fråga om du vill lägga till nya nedladdningar i ett pausat/startat tillstånd osv.  
![nzbget.png](/assets/prowlarr/nzbget.png)

> Klientprioritet spelar bara roll när 2 av samma typ (usenet eller torrent) läggs till. 1 är högsta prioritet, och om flera klienter av samma typ finns och har samma prioritet kommer Prowlarr att alternera mellan dem.

## Usenet-klientinställningar

- Namn - Namnet på nedladdningsklienten inom Prowlarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en för din nedladdningsklient
- Port - Porten för din nedladdningsklient
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxys.
- API-nyckel - API-nyckeln för att autentisera mot din klient
- Användarnamn - Användarnamnet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Lösenord - Lösenordet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Kategori - Kategorin inom din nedladdningsklient som Prowlarr kommer att använda
- Prioritet - Prioritet för nedladdningsklienten för tillagda objekt
- Klientprioritet - Prioritet för nedladdningsklienten inom Prowlarr. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet.

## Torrent-klientinställningar

- Namn - Namnet på nedladdningsklienten inom Prowlarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en för din nedladdningsklient
- Port - Porten för din nedladdningsklient
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxys.
- Användarnamn - Användarnamnet för att autentisera mot din klient
- Lösenord - Lösenordet för att autentisera mot din klient
- Kategori - Kategorin inom din nedladdningsklient som Prowlarr kommer att använda
- Prioritet - Prioritet för nedladdningsklienten för tillagda objekt
- Initialt tillstånd - Initialt tillstånd för torrents (endast Qbittorrent: Tvingar förbi alla seed-trösklar)
- Klientprioritet - Prioritet för nedladdningsklienten inom Prowlarr. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet.

## Testa nedladdningsklienten

Testa din post. Om en grön bock visas kan du spara din post och upprepa vid behov för varje nedladdningsklient du vill att Prowlarr ska använda. Om det misslyckas måste du kontrollera loggen för felet (anslutning, autentiseringsuppgifter osv.).

# Installationen är klar

Det är allt för grunderna! Du kan sedan lägga till meddelanden och andra mer avancerade installationsalternativ efter behov. Dessa dokumenteras på den fullständiga inställningssidan.