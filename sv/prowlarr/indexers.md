---
title: Prowlarr Indexer
description: 
published: true
date: 2023-03-30T14:04:26.292Z
tags: 
editor: markdown
dateCreated: 2021-06-06T11:45:31.974Z
---

Denna sida beskriver hur du lägger till och konfigurerar indexeringar i Prowlarr.

# Lägga till en indexer

För att lägga till en indexer, klicka först på `Indexers` till vänster och sedan på <kb>+</kb> `Lägg till indexer` högst upp på sidan.

![ind_1_addindexer.png](/assets/prowlarr/ind_1_addindexer.png)

Välj din indexer från listan eller skriv in ett delvis namn i rutan för att hitta din indexer. Om din indexer inte finns med i listan kan du använda "Generic Newznab" (för Usenet) eller "Generic Torznab" (för torrents). Annars kan du besöka vår [Indexer Request site](https://requests.prowlarr.com/).

> Att använda `Generic Newznab` eller `Generic Torznab` förutsätter att din indexer stöder standardiserade *znab-format. Om den inte gör det kommer detta inte att fungera.
{.is-info}

> Observera: nästan alla Usenet-webbplatser är kompatibla med Generic Newznab.
{.is-warning}

> Om din tracker eller indexer inte finns med i listan och inte finns på vår [supported indexers](/prowlarr/supported-indexers)-sida kan du begära att den läggs till via vår [Indexer Requests Site](https://requests.prowlarr.com)
{.is-info}

# Redigera en indexer

För att redigera en indexer, klicka först på `Indexers` till vänster och klicka sedan på skiftnyckelikonen längst till höger för den indexer du vill redigera.

# Visa en indexer-ID eller URL

För att visa detaljer om en indexer, klicka först på `Indexers` till vänster och klicka sedan på indexerlänken i kolumnen för indexerens namn. (Tidigare (i)-ikonen till höger)

Tillgängliga detaljer kan inkludera:

- ID i Prowlarr
- Beskrivning
- Kodning
- Språk
- Webbplats
- Newznab/Torznab Prowlarr-URL
- Webbplatsfunktioner

# Indexerinställningar

När du har valt din indexer kommer det att visas en popupruta med ytterligare information som du behöver konfigurera. Observera att de specifika inställningarna kommer att variera något för varje indexer baserat på deras obligatoriska fält och typen av indexer du konfigurerar.

![ind_3_indexer2.png](/assets/prowlarr/ind_3_indexer2.png)

- Namn - Välj ett namn för denna indexer. När den synkroniseras med dina appar kommer den att lägga till "(Prowlarr)" efter namnet.
- Aktivera - Markera rutan för att aktivera denna indexer.
- Omdirigera - Markera rutan om en omdirigering är nödvändig. Det finns bara ett par indexeringar där detta krävs för att undvika att bli förbjuden. Om det är aktiverat kommer det att skicka länken direkt till applikationen istället för att använda Prowlarr som proxy.

> Omdirigering behövs vanligtvis bara för ett fåtal mycket specifika indexeringar.
{.is-info}

- Synkroniseringsprofil - Välj din synkroniseringsprofil här. Dessa kan skapas i [`Inställningar` => `Appar`](/prowlarr/settings#applications). Standardprofilen finns redan och ser ut så här:

> Du kan ha olika inställningar per app genom att skapa flera instanser av indexeringen.
{.is-info}

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Välj URL:en som Prowlarr ska använda. Om den är tom används standard-/första URL:en.
- Nedladdningslänk - Om du lägger till en torrentindexer kan det vara nödvändigt att välja vilken typ av nedladdningslänk som ska användas.
- (Avancerad inställning) API-sökväg - Sökväg till indexerens API. Vanligtvis `/api`
- Autentisering - Många indexeringar och trackers kräver att du autentiserar/loggar in på något sätt. Du kan behöva ange en API-nyckel, RSS-nyckel, session-ID, cookie eller andra autentiseringsuppgifter från din indexer (vanligtvis hittas på din profil eller under säkerhet), välja sökordning eller andra alternativ för din specifika indexer.
  - API-nyckel
  - RSS-nyckel
  - Session-ID
  - Cookie
  - Användarnamn/lösenord
  - osv.
- (Avancerad inställning) Ytterligare parametrar - Ytterligare parametrar att lägga till i förfrågningarna för denna indexer.
- VIP-utgångsdatum - Ange datumet i ISO-format (yyyy-MM-DD) för att få en påminnelse 1 vecka innan utgången; lämna annars tomt
- Taggar - Använd taggar för att ange standardnedladdningsklienter, ange indexerproxys, ange indexeringar för appar eller bara för att organisera dina indexeringar.
- (Avancerad inställning) Frågebegränsning - Om din indexer begränsar dina API-anrop per dag kan du ange det antalet här för att undvika att överskrida gränsen.
- (Avancerad inställning) Hämtgräns - Om din indexer begränsar dina hämtningar per dag kan du ange det antalet här för att undvika att överskrida gränsen. När hämtgränsen har nåtts kommer ytterligare förfrågningar att utlösa ett ohanterat undantag i \*Arr-appar. Andra appar kan variera.
- (Avancerad inställning) Seedningsförhållande - Endast för torrentindexeringar: Det förhållande som en torrent bör nå innan den stoppas, tom är appens standardinställning
- (Avancerad inställning) Seedningstid - Endast för torrentindexeringar: Tiden som en torrent bör vara seedad innan den stoppas, tom är appens standardinställning. Värden anges i minuter.
- (Avancerad inställning) Indexerprioritet - Prioritet för denna indexer för att föredra en indexer framför en annan i fall där flera släpp har samma tidpunkt. 1 är högsta prioritet och 50 är lägsta prioritet. Dessa prioriteringar synkroniseras med \*Arr-apparna.

- Testa din indexer och om en grön bock visas är det okej att spara den. När du sparar den kommer den, beroende på dina synkroniseringsinställningar, att läggas till automatiskt i dina appar.

## Lägga till en anpassad YML-definition

- Observera att yml-definitionen cachas under en kort period och om du gör ändringar för utvecklingsändamål måste du vänta ut cacheminnet eller starta om Prowlarr.
- Om du vill lägga till en anpassad YML-definition i Cardigann-format för en indexer som inte stöds eller för att testa ändringar i en befintlig definition:
  - Navigera till (eller skapa) mappen för anpassad indexerdefinition med namnet `Custom` inom mappen `Definitions` i [Prowlarrs App Data-mapp](/prowlarr/appdata-directory)
    - Exempel på sökvägar:
      - Windows: `C:\ProgramData\Prowlarr\Definitions\Custom`
      - Linux: `/home/$USER/.config/Prowlarr/Definitions/Custom`
      - OSX: `/Users/$USER/.config/Prowlarr/Definitions/Custom`

  - Spara [YML-filen i Cardigann-format](/prowlarr/cardigann-yml-definition) i mappen och se till att Prowlarr har behörighet att komma åt den.

> Filnamnet och ID:t i definitionen måste vara unika och får inte krocka med några andra befintliga definitioner. Det rekommenderas starkt att ha ett unikt namn i definitionen också.
{.is-info}

# Stödda indexeringar

- [Se denna wikisida för en lista över stödda indexeringar enligt den senaste nightly-versionen.](/prowlarr/supported-indexers/)