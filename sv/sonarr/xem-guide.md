---
title: TheXEM Moderation Guide
description: Guide för hur man kartlägger olika scenarier i XEM för optimal användning med Sonarr och annan PVR-programvara.
published: true
date: 2021-11-24T19:26:31.972Z
tags: sonarr, xem
editor: markdown
dateCreated: 2021-10-03T16:48:28.241Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [TheXEM Moderation Guide](#thexem-moderation-guide)
- [Namngivning](#namngivning)
- [De olika entitetstyperna](#de-olika-entitetstyperna)
- [Kartläggningstyper](#kartläggningstyper)
  - [!SxxExx-kartläggning](#sxxexx-kartläggning)
  - [!Absolut kartläggning](#absolut-kartläggning)
  - [!Fullständig kartläggning](#fullständig-kartläggning)
  - [!Direkt kartläggning](#direkt-kartläggning)
- [Exempel](#exempel)
  - [Grundläggande kartläggning av anime](#grundläggande-kartläggning-av-anime)
  - [Komplex kartläggning av anime](#komplex-kartläggning-av-anime)
  - [Kortformat för västerländska tecknade serier](#kortformat-för-västerländska-tecknade-serier)
  - [Komplex individuell kartläggning](#komplex-individuell-kartläggning)
- [Begränsningar](#begränsningar)
  - [Endast ett numreringssystem per serie stöds](#endast-ett-numreringssystem-per-serie-stöds)
  - [Endast en huvudentitet stöds](#endast-en-huvudentitet-stöds)
  - [Ta bort huvudkolumnen eller enskilda säsonger i den](#ta-bort-huvudkolumnen-eller-enskilda-säsonger-i-den)
  - [Vissa saker kan helt enkelt inte kartläggas](#vissa-saker-kan-helt-enkelt-inte-kartläggas)
- [Behöver du hjälp?](#behöver-du-hjälp)

# TheXEM Moderation Guide

[TheXEM](https://thexem.info) är en tjänst som gör det möjligt att skapa kopplingar mellan andra tjänster/entiteter som använder olika numrering och namngivning för TV-serieutgåvor. Sonarr använder TVDB som datakälla för sin avsnittsinformation och ibland använder scenen och andra utgivargrupper en annan namngivnings- eller numreringsmetod. Med rätt kartläggning är det möjligt att se till att avsnitt 1 i säsong 1 enligt TVDB:s numrering matchar avsnitt 5 i säsong 1 enligt scenens numrering, så att Sonarr kan ladda ner rätt avsnitt trots att numreringen är annorlunda.

Denna guide är för personer med ett konto på TheXEM och kommer att guida dig genom några av de vanligare mönster som du kan använda. Men först går vi igenom några grundläggande saker.

# Namngivning

Som en konvention använder vi samma namn som TVDB använder för själva serien. Detta är särskilt intressant för internationella serier som anime och innebär i princip att vi använder det officiellt licensierade engelska namnet på serien.

Det är också möjligt att ange olika alias för seriens namn, vilket främst används för anime men ibland är användbart även för "vanlig" TV.

# De olika entitetstyperna

TheXEM har fyra olika datakällor eller entitetstyper som den för närvarande stöder och kan koppla samman med varandra vid behov. Dessa fyra typer är:

- Scen
- [TVDB](https://thetvdb.com)
- [AniDB](https://anidb.net)
- Huvud

En korrekt XEM-kartläggning för en specifik serie bör *minst* ha en post i scenkolumnen och en post i TVDB-kolumnen med den tillämpliga kartläggningstypen (se avsnittet *Kartläggningstyper* nedan) mellan dem.

> Serier som inte har minst en scenkolumn och en TVDB-kolumn är värdelösa och kan potentiellt tas bort. Samma sak gäller för serier där det inte finns någon direkt eller indirekt koppling mellan scenkolumnen och TVDB-kolumnen.
{.is-warning}

# Kartläggningstyper

TheXEM har tre olika automatiska alternativ för att koppla samman olika entiteter med varandra: SxxExx-kartläggning, absolut kartläggning och kombinationen av båda, fullständig kartläggning. Dessutom kan du också direkt koppla avsnitt till varandra med hjälp av direkt kartläggning. Var och en av dessa har sin egen användning och är användbar i specifika situationer.

## ![SxxExx-kartläggning](/assets/sonarr/xem-guide/mapping-sxxexx.svg) SxxExx-kartläggning

Denna typ av kartläggning fastställer att säsong- och avsnittsnumren är lika mellan de två entiteterna den kopplar samman, vilket innebär att S01E01 är samma avsnitt i båda entitetstyperna. Den absoluta numreringen behöver dock inte vara densamma.

## ![Absolut kartläggning](/assets/sonarr/xem-guide/mapping-abs.svg) Absolut kartläggning

Förutom några mycket specifika användningsfall är absolut kartläggning nästan uteslutande användbart för anime-serier. Anime-namngivningssystemet som används av de flesta utgivargrupper använder bara ett ökande avsnittsnummer istället för SxxExx-numrering, vilket vi kallar absolut numrering. Genom att markera kartläggningen mellan två entiteter som "absolut" informerar du tjänster som använder dessa data om att SxxExx-numreringen kan skilja sig eller inte, men att den absoluta numreringen åtminstone är densamma.

## ![Fullständig kartläggning](/assets/sonarr/xem-guide/mapping-full.svg) Fullständig kartläggning

Fullständig kartläggning informerar alla tjänster som använder TheXEM om att både den absoluta numreringen och SxxExx-kartläggningen är densamma mellan de två entiteterna, vilket innebär att numreringen är densamma mellan båda entiteterna.

> Detta innebär att om det enda du vill lägga till i din kartläggning är en scenkolumn och en TVDB-kolumn med fullständig kartläggning mellan dem, är din seriepost överflödig eftersom detta fungerar som standard utan en post på TheXEM.
{.is-info}

## ![Direkt kartläggning](/assets/sonarr/xem-guide/mapping-direct.svg) Direkt kartläggning

Direkt kartläggning är endast möjlig mellan huvudentitetstypen och entiteterna på vardera sidan om den. Du bör använda det så sparsamt som möjligt eftersom när du väl börjar använda direkta kopplingar måste du fortsätta använda dem åtminstone för resten av säsongen och i vissa fall för resten av hela serien.

Du kan aktivera direkt kartläggning genom att klicka på ikonen ovanför den automatiska kartläggningstypen. Du kommer att se att gränssnittet på sidan ändras lite för att ge plats åt de kopplingar du ska dra. För att koppla ett avsnitt till ett annat avsnitt klickar du helt enkelt på ett avsnitt på vänster sida av kopplingen och klickar sedan på det motsvarande avsnittet på höger sida. Om du gjorde det rätt kommer webbplatsen att be dig bekräfta kopplingen.

> Det är möjligt att koppla ett enskilt avsnitt på ena sidan till flera avsnitt på den andra sidan, till exempel om TVDB betraktar två avsnitt som separata avsnitt medan scenen kombinerar dem till ett nummer. Detta är särskilt intressant för västerländska tecknade serier.
{.is-info}

# Exempel

Det ovanstående är mycket att ta in, men sammanfattningsvis finns det bara några få användningsfall som täcker majoriteten av alla serier som du någonsin kommer att behöva lägga till i TheXEM. Följande är några mycket vanliga typer av kartläggning.

## Grundläggande kartläggning av anime

När du kartlägger en anime-serie använder vi alltid AniDB-kolumnen. När det är möjligt bör du *alltid* sträva efter att använda fullständig kartläggning mellan scenkolumnen och AniDB-kolumnen för den kartläggning du försöker uppnå.

De flesta anime-serier kan direkt kartläggas mellan scenkolumnen via AniDB och slutligen till TVDB. Ett enkelt exempel är serien [Ronia the Robber's Daughter](https://thexem.info/xem/show/1603). Den behöver kartläggning först och främst eftersom det japanska namnet som används av utgivargrupper inte matchar det engelska namnet som används av TVDB, men annars är kartläggningen enkel: numreringen är identisk mellan scenen och AniDB, så vi använder fullständig kartläggning mellan dessa, medan det enda vi vet säkert mellan AniDB och TVDB är att SxxExx-numreringen är identisk.

> AniDB återställer den absoluta numreringen mellan varje säsong eftersom den betraktar varje säsong som sin egen serie. När du lägger till en ny AniDB-säsong, se till att du anger dess ID-nummer och att du ställer in fältet "Ab. Start" för den nya säsongen till 1.
{.is-info}

För ett exempel på en anime-serie med flera säsonger, ta en titt på [Assassination Classroom](https://thexem.info/xem/show/2817). Observera de separata aliasen för den andra säsongen, som hjälper Sonarr att förstå att `[Utgivargrupp] Ansatsu Kyoushitsu - 01 (1080p)` kartläggs till S01E01 i TVDB medan `[Utgivargrupp] Ansatsu Kyoushitsu S2 - 01 (1080p)` kartläggs till S02E01.

## Komplex kartläggning av anime

Ibland stämmer inte TVDB:s uppfattning om en säsong överens med vad AniDB kallar en säsong. Detta händer särskilt när en anime släpps som en så kallad *split-cour*. Detta innebär att det är en grupp av avsnitt, följt av en kort paus efter vilken nästa grupp av avsnitt sänds. Split-cour-anime har vanligtvis en eller högst två anime-säsonger mellan sig och TVDB betraktar oftast en anime som split-cour när den andra gruppen av avsnitt annonseras under den första delens sändningstid.

Ett exempel på hur detta kan se ut är [That Time I Got Reincarnated as a Slime](https://thexem.info/xem/show/5241). Observera hur vad TVDB kallar säsong 2 faktiskt är uppdelat i säsongerna 2 och 3 enligt AniDB. Vi använder en länk till huvudentiteten här för att göra kartläggningen mindre komplex. I princip kombinerar huvudposten den absoluta numreringen som används på TVDB med SxxExx-numreringen som AniDB använder. Sedan länkar vi huvudkolumnen till TVDB med absolut kartläggning och till AniDB-kolumnen med SxxExx-kartläggning. Scenkolumnen kan länkas med fullständig kartläggning som vanligt.

## Kortformat för västerländska tecknade serier

Barnprogram erbjuder ofta en utmaning när det gäller kartläggning av avsnitt eftersom om ett 30-minuters avsnitt delas upp i två separata historier betraktar TVDB dessa som två olika avsnitt medan scenen generellt betraktar dem som ett enda avsnitt. Detta innebär att vi kommer att behöva mycket detaljerad direkt kartläggning mellan enskilda avsnitt.

Ett exempel på detta är serien [Paw Patrol](https://thexem.info/xem/show/4814). När du håller muspekaren över avsnitten i huvudkolumnen ser du att ett enskilt avsnitt på scenens sida är kopplat till ett eller två avsnitt på TVDB-sidan. Denna särskilda typ av kartläggning kräver kontinuerlig uppdatering när nya avsnitt av serien sänds.

> Kom ihåg att det kan vara meningsfullt att koppla ett avsnitt på ena sidan till flera avsnitt på den andra sidan, men att koppla flera avsnitt på ena sidan till flera avsnitt på den andra sidan gör det inte. Programvaran tillåter dig att göra det, men var snäll och gör det inte eftersom Sonarr inte kommer att kunna göra något med det.
{.is-warning}

## Komplex individuell kartläggning

I vissa (lyckligtvis mycket sällsynta!) fall kan kartläggning av avsnitt på varandra bli mycket komplex. TVDB betraktar sändningsdatum från seriens huvudnätverk som ledande när det gäller att bestämma avsnittsordningen. Det kan göra saker riktigt komplicerade i fall som Firefly eller [Transporter](https://thexem.info/xem/show/1653), som sändes av sina ursprungliga nätverk i en ordning som bryter mot den kronologiska ordningen. Scenen kompenserar ofta för detta genom att använda den kronologiska avsnittsordningen, vilket resulterar i att varje avsnitt behöver en komplex individuell kartläggning.

Observera att det inte finns någon automatisk kartläggning mellan huvudkolumnen och scenkolumnen för Transporter; all kartläggning uppnås genom direkta länkar mellan avsnitt.

# Begränsningar

TheXEM har för närvarande några begränsningar som vi kommer att försöka täcka här.

## Endast ett numreringssystem per serie stöds

Om flera utgivargrupper använder olika numreringssystem blir det komplicerat. I sådana fall finns det några riktlinjer för att hantera olika källor.

1. Scenens numrering har alltid företräde framför P2P-utgåvor.
2. Om det inte finns några scenutgåvor för en viss serie, välj den som verkar vara mest populär. Detta kommer vanligtvis att bero på vilken grupp som tenderar att släppa avsnitt snabbast i bra kvalitet.
3. I fallet med anime följer vi numreringen från SubsPlease/Erai-Raws om den är tillgänglig. Om inte gäller den tidigare riktlinjen även här.

## Endast en huvudentitet stöds

Du kommer att använda huvudentitetstypen i vissa relativt sällsynta fall för att göra direkta kopplingar *eller* för att undvika att behöva göra direkta kopplingar. Du kan dock bara använda en av dessa huvudentiteter för att koppla samman två andra entiteter. Eftersom målet är att se till att kartläggningen fungerar för huvudanvändningsfallet att koppla TVDB till scenen måste du se till att åtminstone *den* kartläggningen fungerar och om det kräver en huvudentitet är det där du bör prioritera att använda den.

## Ta bort huvudkolumnen eller enskilda säsonger i den

När du tar bort huvudkolumnen av någon anledning, se till att det inte finns några direkta kartläggningar på enskilda avsnitt i den. Om du tar bort säsongen medan kartläggningarna fortfarande finns där, **kommer kartläggningen att vara osynlig i gränssnittet men kommer fortfarande att finnas kvar!** Om du gör detta av misstag, lägg bara tillbaka säsongen du tog bort, ångra de enskilda länkarna och ta sedan bort säsongen igen.

## Vissa saker kan helt enkelt inte kartläggas

En sak att alltid komma ihåg är att ibland är en serie så förvirrad eller på annat sätt komplex att den inte kan kartläggas i TheXEM. Ibland kan du kartlägga ett av användningsfallen, ibland inte ens det. I dessa fall kan det ofta inte göras något åt det.

# Behöver du hjälp?

Slutligen, om du behöver hjälp med något eller om du helt enkelt inte har ett konto på TheXEM, gå med i Sonarrs Discord-server i kanalen [#xem](https://discord.gg/QzDaBmN2J3). Vi hjälper dig gärna. Tänk dock på att svarstiderna kan vara långsamma och mycket beroende av tidszonsskillnader.