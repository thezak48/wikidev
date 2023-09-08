---
title: Prowlarr-inställningar
description: 
published: true
date: 2023-03-30T14:07:39.851Z
tags: 
editor: markdown
dateCreated: 2021-06-06T15:04:48.057Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Menyalternativ](#menyalternativ)
- [Indexer Proxies](#indexer-proxies)
  - [Proxyinställningar](#proxyinställningar)
  - [FlareSolverr Proxyinställningar](#flaresolverr-proxyinställningar)
  - [HTTP Proxyinställningar](#http-proxyinställningar)
  - [Socks4 Proxyinställningar](#socks4-proxyinställningar)
  - [Socks5 Proxyinställningar](#socks5-proxyinställningar)
- [Applikationer](#applikationer)
  - [Applikationsinställningar](#applikationsinställningar)
  - [Testa applikationen](#testa-applikationen)
- [Nedladdningsklienter (Prowlarr-sökningar)](#nedladdningsklienter-prowlarr-sökningar)
  - [Usenet-klientinställningar](#usenet-klientinställningar)
  - [Torrent-klientinställningar](#torrent-klientinställningar)
  - [Testa nedladdningsklienten](#testa-nedladdningsklienten)
- [Notifieringar](#notifieringar)
  - [Anslutningar](#anslutningar)
  - [Notifieringstriggers](#notifieringstriggers)
- [Taggar](#taggar)
- [Allmänt](#allmänt)
  - [Värd](#värd)
  - [Säkerhet](#säkerhet)
  - [Proxy](#proxy)
  - [Loggning](#loggning)
  - [Analys](#analys)
  - [Uppdateringar](#uppdateringar)
  - [Säkerhetskopior](#säkerhetskopior)
- [Användargränssnitt](#användargränssnitt)
  - [Datum](#datum)
  - [Stil](#stil)
  - [Språk](#språk)
  
Den här sidan går igenom alla tillgängliga inställningar i Prowlarr och hur de fungerar. Detta är inte menat att vara en omfattande "hur man ställer in Prowlarr." Om du vill ha det, använd istället [Snabbstartsguide](/prowlarr/quick-start-guide)-sidan.

# Menyalternativ

För att komma till inställningssidan, välj Inställningar i vänstermenyn. Följande undermenyalternativ kommer att vara tillgängliga:

![settings_1_menu.png](/assets/prowlarr/settings_1_menu.png)

Observera också att för varje enskild inställningssida finns det några alternativ längst upp i menyn:

![settings_2_topmenu.png](/assets/prowlarr/settings_2_topmenu.png)

- Dölj/Visa avancerat är viktigt för alla objekt som är markerade nedan som `(Avancerad inställning)`, annars kommer de inte att visas. Dessa menyalternativ visas i orange i skärmbilderna.

- Du måste spara dina ändringar innan du lämnar skärmen. Du gör det genom att klicka på diskikonet. Om du inte har gjort några ändringar visas "Inga ändringar" och är gråtonad, som visas ovan.

# Indexer Proxies

> Information om stödda proxytyper finns på sidan [Mer information (Stödda)](/prowlarr/supported#indexer-proxies) för den här sektionen
{.is-info}

Här kan du lägga till proxyservrar eller Flaresolverr-konfigurationer för de indexeringstjänster som kräver dem.

Gå till `Inställningar` => `Indexer Proxies` och klicka sedan på <kb>+</kb> för att lägga till en proxy.

![proxies.png](/assets/prowlarr/proxies.png)

## Proxyinställningar
  
- Namn - Namn på proxy i Prowlarr
- Taggar - Taggar för denna proxy. Proxyservrar gäller för alla matchande (samma tagg) indexeringstjänster. Om det är tomt gäller denna proxy för alla indexeringstjänster.

## FlareSolverr Proxyinställningar

- Värd - Hela värdadressen (inklusive http och port) till din FlareSolverr-instans
- (Avancerad inställning) Tidsgräns för begäran (sekunder) - [FlareSolver-begäran `maxTimeout`-värde](https://github.com/FlareSolverr/FlareSolverr#-requestget) som Prowlarr ska använda för FlareSolverr-begäranden. Måste vara mellan `1` sekund och `180` sekunder (standard: `60` sekunder)

> \* En FlareSolverr-proxy används endast för begäranden om och endast om Cloudflare upptäcks av Prowlarr
> \* En FlareSolverr-proxy används endast för begäranden om och endast om proxyservern och indexeringstjänsten har matchande taggar
> \* **En Flaresolverr-proxy som konfigurerats utan några taggar eller som inte har några indexeringstjänster med matchande taggar kommer att inaktiveras.**
{.is-info}

## HTTP Proxyinställningar

- Värd - Värdadressen för din proxyserver
- Port - Porten för din proxyserver
- Användarnamn - Användarnamnet för din proxyserver
- Lösenord - Lösenordet för din proxyserver

## Socks4 Proxyinställningar

- Värd - Värdadressen för din proxyserver
- Port - Porten för din proxyserver
- Användarnamn - Användarnamnet för din proxyserver
- Lösenord - Lösenordet för din proxyserver

## Socks5 Proxyinställningar

- Värd - Värdadressen för din proxyserver
- Port - Porten för din proxyserver
- Användarnamn - Användarnamnet för din proxyserver
- Lösenord - Lösenordet för din proxyserver

# Applikationer

> Information om stödda applikationer finns på sidan [Mer information (Stödda)](/prowlarr/supported#applications) för den här sektionen
{.is-info}

Här lägger du till applikationer som använder Prowlarr (Radarr, Sonarr, Lidarr, Readarr, etc.) och hur de håller sig synkroniserade med Prowlarr.

- Klicka på `Inställningar` => `Apps` och klicka sedan på <kb>+</kb> för att lägga till en app.
- Synkronisera appindexeringstjänster - Utlös en synkronisering av alla indexeringstjänster till alla applikationer
- Testa alla appar - Utlös ett test av alla applikationer
  
![addapps.png](/assets/prowlarr/addapps.png)

Alla program du kan lägga till listas. Du bör bara lägga till program som du redan har installerade, och om du har flera instanser av dem bör du lägga till var och en av dem separat.

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Observera: Indexeringstjänster synkroniseras baserat på de förmågor/kategorier de påstår sig stödja. Om en indexeringstjänst endast stöder `tv`-kategorier kommer den inte att synkroniseras med Lidarr, Radarr och Readarr. Den kommer bara att synkroniseras med Sonarr. "Stödda" kategorier kan väljas som en avancerad inställning per app. **Observera också att \*Arrs bara accepterar indexeringstjänster vars testförfrågningar returnerar resultat som innehåller minst en av de konfigurerade kategorierna.**
{.is-info}

## Applikationsinställningar

- Namn - Ange ett namn för denna app.
- Synknivå - Välj synknivå att använda
  - `Endast lägg till och ta bort` - När indexeringstjänster läggs till eller tas bort från Prowlarr kommer det att uppdatera denna fjärrapp. Om indexeringstjänsten är nere vid synkroniseringstillfället kommer den att inaktiveras i den fjärrapp.
  - `Fullständig synkronisering` - Fullständig synkronisering håller denna apps indexeringstjänster fullständigt synkroniserade. Ändringar som görs på indexeringstjänster i Prowlarr synkroniseras sedan till denna app. Eventuella ändringar som görs på inställningarna för dessa indexeringstjänster på FAQ-sidan inom denna app kommer att åsidosättas av Prowlarr vid nästa synkronisering. En lista över faktorer som används för att jämföra och avgöra om en synkronisering ska ske finns i [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Inaktiverad` - förhindrar att indexeringstjänster synkroniseras med programmet helt och hållet.

> `Fullständig synkronisering` innebär att Prowlarr kommer att åsidosätta de flesta inställningar, inklusive användarvalda kategorier som kan konfigureras i Prowlarr. Men inställningar som inte hanteras av Prowlarr kommer inte att beröras. Men [nästan alla andra ändringsfaktorer](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) kommer att utlösa en synkronisering och skriva över motsvarande inställningar i \*Arr
{.is-warning}

- Taggar - Om du har lagt till en tagg för din indexeringstjänst under installationen kommer endast indexeringstjänster med denna tagg att användas för den här programposten.
- Prowlarr-server - Ange Prowlarr-serverns URL (inklusive http, port och basurl om det behövs) som appen skulle komma åt här.

> Observera att om du använder en omvänd proxy måste du lägga till URL-basen här! Om du inte gör det kommer indexeringstjänsterna att bli trasiga när de synkroniseras, och om du har valt Endast lägg till och ta bort kommer de inte att bli fixade när du redigerar det!{.is-info}

- Appserver - Ange appserverns URL (inklusive http, port och basurl om det behövs) för ditt program här. Ange igen hela URL-basen om den används.
- API-nyckel - Ange API-nyckeln för ditt program här. För \*Arrs kan du hitta den här i Inställningar => Allmänt. Du kan få den från ditt program på fliken `Inställningar` => `Allmänt` och kopiera/klistra in den här.
- (Avancerad inställning) Synka kategorier - Välj de kategorier som ska synkroniseras med denna app. Indexeringstjänster som stöder dessa kategorier kommer att synkroniseras.
  - Indexeringstjänsternas anpassade kategorier kartläggs till standardiserade Torznab/Newznab-kategorier, så sökningar efter standardiserade kategorier inkluderar alla underliggande anpassade kategorier. Indexeringstjänsternas anpassade kategorier listas för finjustering om du inte vill ha dem alla på en gång.
  
## Testa applikationen

Testa din post. Om en grön bock visas kan du spara din post och upprepa vid behov för varje program du vill synkronisera med Prowlarr. Om det misslyckas måste du kontrollera loggen för felet (URL, API-nyckel, etc.).

## Synkroniseringsprofiler

Konfigurera synkroniseringsprofilerna att använda för (en) applikation(er)

> Du kan ha olika inställningar per app genom att skapa flera instanser av indexeringstjänsten
{.is-info}

- Namn - Unikt namn för synkroniseringsprofilen
- Aktivera RSS - För indexeringstjänster med denna profil, aktivera RSS-sökningar/förfrågningar för \*Arr-appen
- Aktivera interaktiv sökning - För indexeringstjänster med denna profil, aktivera interaktiva (manuella) sökningar för \*Arr-appen
- Aktivera automatisk sökning - För indexeringstjänster med denna profil, aktivera automatiska sökningar för \*Arr-appen
- Minsta seeders - För indexeringstjänster med denna profil, minsta antal seeders som krävs för att \*Arr ska hämta en torrent

# Nedladdningsklienter (Prowlarr-sökningar)

{#download-clients}

> Information om stödda nedladdningsklienter finns på sidan [Mer information (Stödda)](/prowlarr/supported#download-clients) för den här sektionen
{.is-info}

Om du avser att göra sökningar direkt inom Prowlarr måste du lägga till nedladdningsklienter. Annars behöver du inte lägga till dem här. För sökningar från dina appar används nedladdningsklienterna som konfigurerats där.

> Prowlarr synkroniserar inte nedladdningsklienter med applikationerna.
{.is-info}

Klicka på `Inställningar` => `Nedladdningsklienter` och klicka sedan på <kb>+</kb> för att lägga till en ny nedladdningsklient. Din nedladdningsklient bör redan vara konfigurerad enligt denna guide.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

Välj den nedladdningsklient du vill lägga till, och det kommer att visas en popupruta för att ange anslutningsinformation. Denna information är liknande för de flesta klienter. Vissa kommer att be om ett användarnamn eller lösenord, vissa kommer att fråga om du vill lägga till nya nedladdningar i ett pausat/startat tillstånd, osv.
  
> Klientprioritet spelar bara roll när 2 av samma typ (usenet eller torrent) läggs till. 1 är högsta prioritet, och om flera klienter av samma typ finns och har samma prioritet kommer Prowlarr att alternera mellan dem.
{.is-info}

## Usenet-klientinställningar

- Namn - Namnet på nedladdningsklienten inom Prowlarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en för din nedladdningsklient
- Port - Porten för din nedladdningsklient
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxyservrar.
- API-nyckel - API-nyckeln för att autentisera mot din klient
- Användarnamn - Användarnamnet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Lösenord - Lösenordet för att autentisera mot din klient (vanligtvis inte nödvändigt)
- Kategori - Kategorin inom din nedladdningsklient som Prowlarr kommer att använda
- Prioritet - nedladdningsklientens prioritet för tillagda objekt
- Klientprioritet - Prioritet för nedladdningsklienten inom Prowlarr. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet.

## Torrent-klientinställningar

- Namn - Namnet på nedladdningsklienten inom Prowlarr
- Aktivera - Aktivera denna nedladdningsklient
- Värd - URL:en för din nedladdningsklient
- Port - Porten för din nedladdningsklient; detta är vanligtvis webgui-porten
- Använd SSL - Använd en säker anslutning med din nedladdningsklient. Var medveten om detta vanliga misstag.
- URL-bas - Lägg till ett prefix i URL:en; detta behövs vanligtvis för omvända proxyservrar.
- Användarnamn - Användarnamnet för att autentisera mot din klient
- Lösenord - Lösenordet för att autentisera mot din klient
- Kategori - Kategorin inom din nedladdningsklient som Prowlarr kommer att använda
- Prioritet - nedladdningsklientens prioritet för tillagda objekt
- Initialt tillstånd - Inledande tillstånd för torrents (endast Qbittorrent: Tvingar förbigång av alla seed-trösklar)
- Klientprioritet - Prioritet för nedladdningsklienten inom Prowlarr. Round-Robin används för klienter av samma typ (torrent/usenet) som har samma prioritet.

## Testa nedladdningsklienten

Testa din post. Om en grön bock visas kan du spara din post och upprepa vid behov för varje nedladdningsklient du vill att Prowlarr ska använda. Om det misslyckas måste du kontrollera loggen för felet (anslutning, referenser, etc.).

# Notifieringar

> Information om stödda notifieringsleverantörer finns på sidan [Mer information (Stödda)](/prowlarr/supported#notifications) för den här sektionen
{.is-info}

## Anslutningar

Anslutningar är hur du vill att Prowlarr ska kommunicera med omvärlden.

- Genom att trycka på <kb>+</kb>-knappen kommer du att presenteras med ett nytt fönster som låter dig konfigurera många olika slutpunkter

- En lista över stödda notifieringar och anslutningar finns på [Mer information (Stödda)](/prowlarr/supported#notifications)

## Notifieringstriggers

- Vid hämtning av release - Få notifiering vid hämtning av release från Prowlarr eller från API:et
  - Inkludera manuella hämtningar - Få notifieringar vid manuella hämtningar som utlöses inom Prowlarr UI
- Vid hälsoproblem - Få notifieringar vid hälsokontrollfel
  - Inkludera hälsovarningar - Få notifieringar vid hälsovarningar i tillägg till fel.
- Vid programuppdatering - Få notifiering när Prowlarr uppdateras till en ny version

# Taggar

- Taggavsnittet i Prowlarr används för att koppla samman olika aspekter av Prowlarr.
- Taggar är särskilt användbara för:
  - Aktivering av Flaresolverr-proxy för användning med en indexeringstjänst; Observera att Flaresolverr-proxys är inaktiverade utan en tagg
  - Aktivering av en HTTP- eller SOCKS-proxy för användning med en indexeringstjänst
  - Specificera indexeringstjänster för vissa appar

# Allmänt

Här ändrar du allmänna applikationsinställningar som port och loggningsnivå.

Klicka på `Inställningar` => `Allmänt`.

> Många av alternativen här kan bara ses genom att klicka på "Visa avancerat" längst upp på skärmen. Alla menyalternativ i orange visas endast när "Visa avancerat" är aktiverat.
{.is-info}

## Värd

![general_host.png](/assets/prowlarr/general_host.png)

- (Avancerad inställning) Bindningsadress - Lämna detta som `*` om du inte behöver ändra det. IPv4-adress/värd på systemet som Prowlarr kommer att lyssna på. (standard: `*`)
  - Observera att `*` är alla adresser
- Portnummer - porten som Prowlarr körs på. Den måste vara unik. (standard: 9696)
- BasUrl - Ange en URL-bas här om du använder en omvänd proxy. (omstart krävs) (standard: tomt)
- (Avancerad inställning) Instansnamn - Namn att använda för webbläsarflik och SysLog (om aktiverat) (omstart krävs) (standard: Prowlarr)
- (Avancerad inställning) Använd SSL - Markera den här rutan om du använder en https-adress för att ansluta till Prowlarr. Om du använder `localhost` eller en IP-adress bör detta nästan ALDRIG vara markerat. (standard: false)
- Starta webbläsare (endast Windows) - Markera den här rutan om du vill att en webbläsarflik ska öppnas när Prowlarr startar. (standard: ja)

## Säkerhet

![general_security.png](/assets/prowlarr/general_security.png)

- Autentisering - Hur vill du autentisera för att komma åt din Prowlarr-instans
  - Ingen - Du har ingen autentisering för att komma åt din Prowlarr. Vanligtvis om du är den enda användaren i ditt nätverk, inte har någon på ditt nätverk som skulle vilja komma åt din Radarr eller om din Radarr inte är exponerad för webben
  - Grundläggande (webbläsarpopup) - Den här inställningen visar en liten popup när du går in på din Prowlarr och låter dig ange användarnamn och lösenord
  - Formulär (inloggningssida) - Den här inställningen har en bekant inloggningsskärm som liknar andra webbplatser och låter dig logga in på din Prowlarr
- API-nyckel - API-nyckeln används av externa appar som har åtkomst till Prowlarr. Den här nyckeln är hemlig och ska inte delas med någon. Om den delas bör du generera en ny nyckel och uppdatera dina appar.
- Certifikatvalidering - Ändra hur strikt HTTPS-certifikatvalidering är
  - Aktiverad - Validera alla HTTPS-certifikat (rekommenderas)
  - Inaktiverad för lokala adresser - Validera alla HTTPS-certifikat utom de på localhost och LAN
  - Inaktiverad - Validera inga HTTPS-certifikat

## Proxy

![general_proxy.png](/assets/prowlarr/general_proxy.png)

Proxy - Den här inställningen gör att du kan köra informationen som din Prowlarr hämtar och söker igenom via en proxy. Detta kan vara användbart om du befinner dig i ett land som inte tillåter nedladdning av torrentfiler.

- Använd proxy - Aktivera för att använda en proxy
- Proxytyp - Välj din proxytyp (HTTPS, Socks4 eller Socks5)
- Värdnamn - Ange ditt proxy-värdnamn (Inkludera inte http/https eller någon annan protokoll)
- Port - Ange din proxyport
- Användarnamn - Ange ditt proxy-användarnamn om det behövs
- Lösenord - Ange ditt proxy-lösenord om det behövs
- Ignorerade adresser - Ange en kommaseparerad lista över adresser som ska undantas från proxyt
- Bypassa proxy för lokala adresser - Markera rutan för att bypassa proxyt för lokala adresser.

## Loggning

![general_logging.png](/assets/prowlarr/general_logging.png)

Standardloggningen är `Info`. Detta är mycket grundläggande loggning. Du kan ändra den här för mer detaljerad loggning. Loggfilerna kommer att rotera, så det finns ingen risk att de tar för mycket plats.

- Loggnivå - Förmodligen ett av de mest användbara felsökningsverktygen
  - Info - Detta är det mest grundläggande sättet som Prowlarr samlar information på. Detta inkluderar en mycket minimal mängd information i loggarna. Denna loggfil innehåller fatala, fel, varningar och info-poster.
  - Debug - Debug kommer att inkludera all information som Info inkluderar plus mer information som kan vara användbar. Denna loggfil innehåller fatala, fel, varningar, info och debug-poster.
  - Trace - Den mest avancerade och detaljerade loggningen på Prowlarr, Trace kommer att inkludera all information som samlas in av Info och Debug och mer. Detta är den vanligaste typen av logg som kommer att begäras vid felsökning på Discord eller Reddit. Om du behöver hjälp, välj loggen till Trace och gör om uppgiften som gav dig problem för att fånga loggen. Denna loggfil innehåller fatala, fel, varningar, info, debug och trace-poster.

## Analys

![general_analytics.png](/assets/prowlarr/general_analytics.png)

- Analys - Skicka anonym användnings- och felinformation till Prowlarrs servrar (Servarr). Detta inkluderar information om din webbläsare, vilka Prowlarr WebUI-sidor du använder, felrapportering samt OS, runtime-version och relaterad information. Vi kommer att använda denna information för att prioritera funktioner och buggfixar.

## Uppdateringar

![general_updates.png](/assets/prowlarr/general_updates.png)

- (Avancerad inställning) Gren - Detta är grenen av Prowlarr som du kör på.
  - [Se detta FAQ-inlägg för mer information](/prowlarr/faq#how-do-i-update-prowlarr)
- Automatisk - Ladda ner och installera uppdateringar automatiskt. Du kommer fortfarande att kunna installera från System: Uppdateringar. Obs: Windows-användare uppdateras alltid automatiskt.
- Mekanism - Använd Prowlarrs inbyggda uppdaterare eller ett skript
  - Inbyggd - Använd Prowlarrs egna uppdaterare
  - Skript - Låt Prowlarr köra uppdateringsskriptet
  - Docker - Uppdatera inte Prowlarr från insidan av Docker, dra istället en helt ny bild med den nya uppdateringen
- Skript - Synlig endast när Mekanism är inställd på Skript - Sökväg till uppdateringsskriptet
- Uppdateringsprocess - Prowlarr kommer att ladda ner uppdateringsfilen, verifiera dess integritet och extrahera den till en temporär plats och anropa den valda metoden. Uppdateringsprocessen körs under samma användare som Prowlarr körs under, den behöver behörighet att uppdatera Prowlarr-filerna samt stoppa/starta Prowlarr.
- Inbyggd - Den inbyggda metoden kommer att säkerhetskopiera Prowlarr-filer och inställningar, stoppa Prowlarr, uppdatera installationen och starta Prowlarr igen. Om ditt system inte hanterar att stoppa Prowlarr och försöker starta om det automatiskt kan det vara bäst att använda ett skript istället. Vid eventuell felaktighet kommer den tidigare versionen av Prowlarr att startas om.
- Skript - Skriptet bör hantera samma saker som den inbyggda uppdateraren, om du behöver hantera stopp och start av tjänster (upstart/launchd/etc) måste du göra det här.

## Säkerhetskopior

![general_backups.png](/assets/prowlarr/general_backups.png)

- (Avancerad inställning) Mapp - Detta låter dig välja säkerhetskopieringsplatsen. I Docker kommer du att vara begränsad till vad du tillåter att behållaren ser. Sökvägar är relativa till appdata-mappen; om det behövs kan du ange en absolut sökväg för att säkerhetskopiera utanför appdata-mappen.
- (Avancerad inställning) Intervall - Hur ofta vill du att Prowlarr ska göra en säkerhetskopia
- (Avancerad inställning) Förvaring - Hur länge vill du att Prowlarr ska behålla varje säkerhetskopia. Efter att en ny säkerhetskopia har gjorts kommer den äldsta säkerhetskopian att tas bort

> Manuella säkerhetskopior behålls för evigt, lagras i samma mapp och har olika namn.
{.is-info}

# Användargränssnitt

## Datum

- Kort datumformat - Hur vill du att Prowlarr ska visa korta datum?
- Långt datumformat - Hur vill du att Prowlarr ska visa datum i långt format?
- Tidsformat - Vill du ha ett 12-timmars eller 24-timmars format?
- Visa relativa datum - Vill du att Prowlarr ska visa relativa (Idag/Igår/etc) eller absoluta datum?

## Stil

- Tema - Välj färgtema som Prowlarr ska använda, inspirerat av [Theme.Park](https://github.com/GilbN/theme.park)
- Aktivera färgsvagt läge - Ändrad stil för att färgsvaga användare bättre ska kunna skilja färgkodad information åt

## Språk

- Användargränssnittsspråk - Välj språk för Prowlarr att använda i applikationens användargränssnitt