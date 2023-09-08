---
title: Readarr System
description: 
published: true
date: 2022-05-05T12:52:16.242Z
tags: readarr, needs-love, system
editor: markdown
dateCreated: 2021-06-20T19:54:43.262Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Status](#status)
  - [Hälsa](#hälsa)
    - [Systemvarningar](#systemvarningar)
      - [Grenen är inte en giltig utgåvogren](#grenen-är-inte-en-giltig-utgåvogren)
      - [Installerad SQLite-version stöds inte](#installerad-sqlite-version-stöds-inte)
      - [Ny uppdatering finns tillgänglig](#ny-uppdatering-finns-tillgänglig)
      - [Kan inte installera uppdatering eftersom startmappen inte kan skrivas av användaren](#kan-inte-installera-uppdatering-eftersom-startmappen-inte-kan-skrivas-av-användaren)
      - [Uppdatering kommer inte att vara möjlig för att förhindra att AppData raderas vid uppdatering](#uppdatering-kommer-inte-att-vara-möjlig-för-att-förhindra-att-appdata-raderas-vid-uppdatering)
      - [Grenen är för en tidigare version](#grenen-är-för-en-tidigare-version)
      - [Kunde inte ansluta till signalR](#kunde-inte-ansluta-till-signalr)
        - [Nginx](#nginx)
      - [Misslyckades med att lösa IP-adressen för den konfigurerade proxyvärden](#misslyckades-med-att-lösa-ip-adressen-för-den-konfigurerade-proxyvärden)
      - [Proxytest misslyckades](#proxytest-misslyckades)
      - [Systemtiden är mer än 1 dag felaktig](#systemtiden-är-mer-än-1-dag-felaktig)
    - [Nedladdningsklienter](#nedladdningsklienter)
      - [Ingen nedladdningsklient är tillgänglig](#ingen-nedladdningsklient-är-tillgänglig)
      - [Kan inte kommunicera med nedladdningsklienten](#kan-inte-kommunicera-med-nedladdningsklienten)
      - [Nedladdningsklienter är otillgängliga på grund av fel](#nedladdningsklienter-är-otillgängliga-på-grund-av-fel)
      - [Aktivera hantering av slutförda nedladdningar](#aktivera-hantering-av-slutförda-nedladdningar)
      - [Docker felaktig fjärrsökvägsmappning](#docker-felaktig-fjärrsökvägsmappning)
      - [Nedladdning till rotmappen](#nedladdning-till-rotmappen)
      - [Felaktiga inställningar för nedladdningsklient](#felaktiga-inställningar-för-nedladdningsklient)
      - [Felaktig fjärrsökvägsmappning](#felaktig-fjärrsökvägsmappning)
      - [Behörighetsfel](#behörighetsfel)
      - [Författarmontage är skrivskyddat](#författarmontage-är-skrivskyddat)
      - [Fjärrfilen togs bort under bearbetning](#fjärrfilen-togs-bort-under-bearbetning)
      - [Fjärrsökväg används och importen misslyckades](#fjärrsökväg-används-och-importen-misslyckades)
    - [Hantering av slutförda/misslyckade nedladdningar](#hantering-av-slutförda-misslyckade-nedladdningar)
      - [Hantering av slutförda nedladdningar är inaktiverad](#hantering-av-slutförda-nedladdningar-är-inaktiverad)
    - [Indexerare](#indexerare)
      - [Inga indexerare är tillgängliga med automatisk sökning aktiverad, Readarr kommer inte att ge några automatiska sökresultat](#inga-indexerare-är-tillgängliga-med-automatisk-sökning-aktiverad-readarr-kommer-inte-att-ge-några-automatiska-sökresultat)
      - [Inga indexerare är tillgängliga med RSS-synkronisering aktiverad, Readarr kommer inte att hämta nya utgåvor automatiskt](#inga-indexerare-är-tillgängliga-med-rss-synkronisering-aktiverad-readarr-kommer-inte-att-hämta-nya-utgåvor-automatiskt)
      - [Inga indexerare är aktiverade](#inga-indexerare-är-aktiverade)
    - [Aktiverade indexerare stöder inte sökning](#aktiverade-indexerare-stöder-inte-sökning)
      - [Inga indexerare är tillgängliga med interaktiv sökning aktiverad](#inga-indexerare-är-tillgängliga-med-interaktiv-sökning-aktiverad)
      - [Indexerare är otillgängliga på grund av fel](#indexerare-är-otillgängliga-på-grund-av-fel)
      - [Jackett används för alla slutpunkter](#jackett-används-för-alla-slutpunkter)
        - [Lösningar](#lösningar)
    - [Bokmappar](#bokmappar)
      - [Saknad rotmapp](#saknad-rotmapp)
    - [Importlistor](#importlistor)
      - [Importlistor är otillgängliga på grund av fel](#importlistor-är-otillgängliga-på-grund-av-fel)
  - [Diskutrymme](#diskutrymme)
  - [Om](#om)
  - [Mer information](#mer-information)
- [Uppgifter](#uppgifter)
  - [Schemalagda](#schemalagda)
  - [Kö](#kö)
- [Säkerhetskopiering](#säkerhetskopiering)
- [Uppdateringar](#uppdateringar)
- [Händelser](#händelser)
- [Loggfiler](#loggfiler)

# Status

## Hälsa

- Den här sidan innehåller en lista över felkontroller för hälsa. Dessa hälsokontroller utförs periodvis av Readarr och vid vissa händelser. De resulterande varningarna och felen listas här för att ge råd om hur man löser dem.

### Systemvarningar

#### Grenen är inte en giltig utgåvogren

- Den gren du har ställt in är inte en giltig utgåvogren. Du kommer inte att få uppdateringar. Ändra till en av de [aktuella utgåvogrenarna](/readarr/faq#how-do-i-update-readarr).

#### Installerad SQLite-version stöds inte

- Readarr lagrar sina data i en SQLite-databas. Den installerade SQLite3-biblioteket på ditt system är för gammalt. Readarr kräver minst version 3.9.0. Observera att Readarr använder `libSQLite3.so` som kan finnas eller inte finnas i ett SQLite3-uppgraderingspaket.

> Observera att Readarr använder `libSQLite3.so` som kan finnas eller inte finnas i ett SQLite3-uppgraderingspaket.
{.is-info}

#### Ny uppdatering finns tillgänglig

Fira, utvecklarna har släppt en ny uppdatering. Detta innebär vanligtvis fantastiska nya funktioner och lösta buggar (eller hur?). Tydligen har du inte aktiverat automatisk uppdatering, så du måste ta reda på hur du uppdaterar på din plattform. Att trycka på Installera-knappen på sidan System => Uppdateringar är förmodligen en bra startpunkt.

> Den här varningen visas inte om din nuvarande version är mindre än 14 dagar gammal
{.is-info}

#### Kan inte installera uppdatering eftersom startmappen inte kan skrivas av användaren

- Detta innebär att Readarr inte kommer att kunna uppdatera sig själv. Du måste uppdatera Readarr manuellt eller ange behörigheterna för Readarrs startmapp (installationsmappen) så att Readarr kan uppdatera sig själv.

#### Uppdatering kommer inte att vara möjlig för att förhindra att AppData raderas vid uppdatering

- Readarr upptäckte att AppData-mappen för ditt operativsystem är placerad inuti mappen som innehåller Readarr-binärerna. Normalt skulle det vara C:\ProgramData för Windows och ~/.config för Linux.

- Titta på System => Info för att se de aktuella AppData- och startmapparna.
- Detta innebär att Readarr inte kommer att kunna uppdatera sig själv utan att riskera dataförlust.
- Om du använder Linux måste du förmodligen ändra hemmappen för användaren som kör Readarr och kopiera innehållet i den aktuella mappen ~/.config/Readarr för att bevara din databas.

#### Grenen är för en tidigare version

- Uppdateringsgrenen som är inställd i Inställningar/Allmänt är för en tidigare version av Readarr, därför kommer instansen inte att se korrekt uppdateringsinformation i System/Uppdateringar och kanske inte får nya uppdateringar när de släpps.

#### Kunde inte ansluta till signalR

- signalR driver de dynamiska UI-uppdateringarna, så om din webbläsare inte kan ansluta till signalR på din server kommer du inte att se några uppdateringar i realtid i gränssnittet.

- Det vanligaste förekomsten av detta är användning av en omvänd proxy eller Cloudflare.
- Cloudflare kräver aktiverade websockets.

##### Nginx

- Nginx kräver följande tillägg till platsblocket för appen:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Se till att du inte inkluderar proxy_set_header Connection "Upgrade"; som föreslås i nginx-dokumentationen. DETTA KOMMER INTE ATT FUNGERA
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

För Apache2 omvänd proxy måste du aktivera följande moduler: proxy, proxy_http och proxy_wstunnel. Lägg sedan till denna websocket-tunnelanvisning i din vhost-konfiguration:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8787/$1 [P,L]
```

För Caddy (V1) använd detta:
Obs: du måste också lägga till websocket-anvisningen i din Readarr-konfiguration

```none
 proxy /readarr 127.0.0.1:8787 {
     websocket
     transparent
 }
```

#### Misslyckades med att lösa IP-adressen för den konfigurerade proxyvärden

- Granska dina proxyinställningar och se till att de är korrekta.
- Se till att din proxy är igång, fungerar och är tillgänglig.

#### Proxytest misslyckades

- Din konfigurerade proxy misslyckades med att testa framgångsrikt, granska den HTTP-felinformation som tillhandahålls och/eller kontrollera loggarna för mer information.

#### Systemtiden är mer än 1 dag felaktig

- Systemtiden är mer än 1 dag felaktig. Schemalagda uppgifter kan inte köras korrekt förrän tiden har korrigerats.
- Granska din systemtid och se till att den är synkroniserad med en auktoritativ tidsserver och är korrekt.

### Nedladdningsklienter

#### Ingen nedladdningsklient är tillgänglig

- En korrekt konfigurerad och aktiverad nedladdningsklient krävs för att Readarr ska kunna ladda ner media. Eftersom Readarr stöder olika nedladdningsklienter bör du bestämma vilken som bäst motsvarar dina krav. Om du redan har en nedladdningsklient installerad bör du konfigurera Readarr att använda den och skapa en kategori. Se Inställningar => Nedladdningsklient.

#### Kan inte kommunicera med nedladdningsklienten

- Readarr kunde inte kommunicera med den konfigurerade nedladdningsklienten. Kontrollera om nedladdningsklienten är igång och dubbelkolla URL:en. Detta kan också indikera ett autentiseringsfel.
- Detta beror vanligtvis på en felaktigt konfigurerad nedladdningsklient. Saker du vanligtvis kan kontrollera:
- IP-adressen för dina nedladdningsklienter, om de finns på samma fysiska maskin är detta vanligtvis 127.0.0.1
- Portnumret som din nedladdningsklient använder, dessa fylls i med standardportnumret men om du har ändrat det måste du ange samma nummer i Readarr.
- Se till att SSL-kryptering inte är aktiverad om du använder både din Readarr-instans och din nedladdningsklient i ett lokalt nätverk. Se SSL-FAQ-posten för mer information.

#### Nedladdningsklienter är otillgängliga på grund av fel

{#nedladdningsklienter-är-otillgängliga-på-grund-av-fel}

- En eller flera av dina nedladdningsklienter svarar inte på förfrågningar från Readarr. Därför har Readarr beslutat att tillfälligt sluta fråga nedladdningsklienten på sin normala 1-minuterscykel, som normalt används för att spåra aktiva nedladdningar och importera färdiga nedladdningar. Men Readarr kommer fortsätta försöka skicka nedladdningar till klienten, men kommer med stor sannolikhet misslyckas.
- Du bör inspektera System=>Loggar för att se vad orsaken till felen är.
- Om du inte längre använder denna nedladdningsklient bör du inaktivera den i Readarr för att förhindra fel.

#### Aktivera hantering av slutförda nedladdningar

- Readarr kräver att hantering av slutförda nedladdningar är aktiverat för att kunna importera filer som har laddats ner av nedladdningsklienten. Det rekommenderas att du aktiverar hantering av slutförda nedladdningar.
- (Hantering av slutförda nedladdningar är aktiverat som standard för nya användare.)

#### Docker felaktig fjärrsökvägsmappning

- Det här felet är vanligtvis associerat med felaktiga Docker-sökvägar antingen i din nedladdningsklient eller Readarr.

- Ett exempel på detta skulle vara:
  - Nedladdningsklient: Nedladdningsmapp: /mnt/user/downloads:/downloads
  - Readarr: Nedladdningsmapp: /mnt/user/downloads:/data
- I det här exemplet placerar nedladdningsklienten sina nedladdningar i /downloads och berättar sedan för Readarr när de är klara att den färdiga boken finns i /downloads. Readarr kommer då och säger "Okej, bra, låt mig kolla i /downloads" När det gäller Readarr har du inte tilldelat en /downloads-sökväg, du har tilldelat en /data-sökväg, så det här felet kastas.
- Det enklaste sättet att åtgärda detta är KONCISTENS om du använder ett system i din nedladdningsklient, använd det överallt.

- Team Readarr gillar att helt enkelt använda /data.
  - Nedladdningsklient: /mnt/user/data/downloads:/data/downloads
  - Readarr: /mnt/user/data:/data

- Nu kan du inom nedladdningsklienten ange var i /data du vill placera dina nedladdningar, detta varierar beroende på klienten men du bör kunna säga "Ja, nedladdningsklient, placera mina filer i." /data/torrents (eller usenet)/books och eftersom du använde /data i Readarr när nedladdningsklienten berättar för Readarr att den är klar kommer Readarr att säga "Bra, jag har en /data och jag kan också se /torrents (eller usenet)/books allt är rätt i världen."
- Det finns många bra skrivuppgifter: vår wiki [Docker Guide](/docker-guide) och TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Dessa guider lägger stor vikt vid hårdlänkar och atomiska flyttningar, men själva konceptet med containrar och hur sökvägsmappning fungerar är kärnan i dessa diskussioner.

- Om du korsar operativsystem eller nativt och Docker behöver du en fjärrsökvägsmappning. Se [TRaSH's Remote Path Guide för Radarr men konceptet är detsamma för alla \*Arrs](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) för mer information.

- Om du får detta fel med Calibre kan inte Redarr komma åt Calibres bibliotek. Lösningen är densamma - korrigera de inkonsekventa monteringspunkterna för dina containrar. Alternativt kan du skapa en fjärrsökvägsmappning för att koppla Calibre-bibliotekets sökväg till den sökväg som Readarr kan komma åt. En fjärrsökvägsmappning behövs bara om du korsar operativsystem eller servrar. Om allt är i Docker är det bättre att korrigera dina monteringspunkter istället.

#### Nedladdning till rotmappen

{#nedladdningar-i-rotmappen}

- Inom applikationen definieras en rotmapp som den konfigurerade mediebiblioteksmappen. Detta är inte rotmappen för en montering. Din nedladdningsklient laddar ner ofullständiga eller slutförda nedladdningar (eller flyttar slutförda nedladdningar) till din rot (biblioteks) mapp.
- Detta orsakar ofta problem - inklusive dataförlust - och bör inte göras. För att åtgärda detta, ändra din nedladdningsklient så att den inte placerar nedladdningar inom din rotmapp. Observera att 'placera' även inkluderar om din nedladdningsklients kategori är inställd på din rotmapp eller om NZBGet/SABnzbd har sorteringsfunktionen aktiverad och sorterar till din rotmapp.
- Observera att den här kontrollen tittar på alla definierade/konfigurerade rotmappar som har lagts till, inte bara rotmappar som för närvarande används. Med andra ord bör inte mappen där din nedladdningsklient laddar ner eller flyttar slutförda nedladdningar till vara samma mapp som du har konfigurerat som din rot/biblioteks/finala mediedestinationsmapp i *arr-applikationen.
- Konfigurerade rotmappar (även kallade biblioteksmappar) finns i [Inställningar => Mediehantering => Rotmappar](/readarr/settings/#root-folders)
- Ett exempel är om dina nedladdningar går till `\data\downloads` och du har en rotmapp inställd som `\data\downloads`.
- Det rekommenderas att använda sökvägar som `\data\media\` för din rotmapp/bibliotek och `\data\downloads\` för dina nedladdningar.
- Granska vår [Docker Guide](/docker-guide) och TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) för mer information om korrekt och optimal sökvägsinställning. Observera att koncepten gäller både Docker och icke-Docker.

> Din nedladdningsmapp där din nedladdningsklient placerar nedladdningarna och din rot/biblioteksmapp MÅSTE vara separata. \*Arr kommer att importera filen/filerna från din nedladdningsklients mapp till ditt bibliotek. Nedladdningsklienten bör inte flytta något eller ladda ner något till ditt bibliotek.
{.is-warning}

#### Felaktiga inställningar för nedladdningsklient

- Platsen där din nedladdningsklient laddar ner filer orsakar problem. Kontrollera loggarna för mer information. Detta kan bero på behörigheter eller försök att gå från Windows till Linux eller Linux till Windows utan en fjärrsökvägsmappning.

#### Felaktig fjärrsökvägsmappning

- Platsen där din nedladdningsklient laddar ner filer orsakar problem. Kontrollera loggarna för mer information. Detta kan bero på behörigheter eller försök att gå från Windows till Linux eller Linux till Windows utan en fjärrsökvägskarta. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Readarr/Readarr-remote-path-mapping/) för mer information.

#### Behörighetsfel

- Readarr eller användaren readarr körs som kan inte komma åt platsen där din nedladdningsklient laddar ner filer. Detta är vanligtvis ett behörighetsproblem.

#### Författarmontering är skrivskyddad

{#author-mount-ro}

- Montering som innehåller en författarsökväg är monterad som skrivskyddad. Kontrollera dina monteringsinställningar och ägande/behörigheter.

#### Fjärrfilen togs bort mitt under bearbetning

- En fil som är åtkomlig via en fjärrsökvägskarta verkar ha tagits bort innan bearbetningen var klar.

#### Fjärrsökvägen används och importen misslyckades

- Kontrollera dina loggar för mer information; Se våra felsökningsguider

### Hantering av slutförda/misslyckade nedladdningar

#### Hantering av slutförda nedladdningar är inaktiverad

- (Denna varning genereras endast för befintliga användare innan funktionen för hantering av slutförda nedladdningar implementerades. Denna funktion är inaktiverad som standard för att säkerställa att systemet fortsatte att fungera som förväntat för befintliga konfigurationer.)
- Det rekommenderas att använda hantering av slutförda nedladdningar eftersom det ger bättre kompatibilitet för uppacknings- och efterbearbetningslogik för olika nedladdningsklienter. Med den kommer Readarr bara att importera en nedladdning när nedladdningsklienten rapporterar att den är klar.
- Om du vill aktivera hantering av slutförda nedladdningar bör du verifiera följande: * Varning: Hantering av slutförda nedladdningar fungerar endast korrekt om nedladdningsklienten och Readarr är på samma maskin eftersom den får sökvägen som ska importeras direkt från nedladdningsklienten, annars behövs en fjärrkarta.

### Indexerare

#### Inga indexerare är tillgängliga med aktiverad automatisk sökning, Readarr kommer inte att ge några automatiska sökresultat

- Helt enkelt sagt har du inte några indexerare inställda för att tillåta automatiska sökningar
- Gå till Inställningar => Indexerare, välj en indexerare du vill tillåta automatiska sökningar och klicka sedan på spara.

#### Inga indexerare är tillgängliga med aktiverad RSS-synkronisering, Readarr kommer inte att hämta nya utgåvor automatiskt

- Så Readarr använder RSS-flödet för att plocka upp nya utgåvor när de kommer. Mer information om det finns här
- För att åtgärda detta problem går du till Inställningar => Indexerare, välj en indexerare du har och aktivera RSS-synkronisering

#### Inga indexerare är aktiverade

- Readarr kräver indexerare för att kunna upptäcka nya utgåvor. Läs wikin för instruktioner om hur du lägger till indexerare.

### Aktiverade indexerare stöder inte sökning

- Ingen av de indexerare du har aktiverat stöder sökning. Detta innebär att Readarr bara kommer att kunna hitta nya utgåvor via RSS-flödena. Men att söka efter böcker (antingen automatisk sökning eller manuell sökning) kommer aldrig att ge några resultat. Det enda sättet att åtgärda det är att lägga till en annan indexerare.

#### Inga indexerare är tillgängliga med aktiverad interaktiv sökning

- Ingen av de indexerare du har aktiverat stöder interaktiv sökning. Detta innebär att programmet bara kommer att kunna hitta nya utgåvor via RSS-flöden eller en automatisk sökning.

#### Indexerare är otillgängliga på grund av fel

- Fel uppstår när Readarr försökte använda en av dina indexerare. För att begränsa försöken kommer Readarr inte att använda indexeraren under en ökande tid (upp till 24 timmar).
- Detta mekanism utlöses om Readarr inte kunde få ett svar från indexeraren (kan bero på DNS, proxy/vpn-anslutning, autentisering eller indexeringsproblem) eller inte kunde hämta nzb/torrent-filen från indexeraren. Granska loggarna för att avgöra vilken typ av fel som orsakar problemet.
- Du kan förhindra varningen genom att inaktivera den berörda indexeraren.
- Kör testet på indexeraren för att tvinga Readarr att kontrollera indexeraren igen, observera att varningen för hälsokontrollen inte alltid försvinner omedelbart.

#### Jackett All Endpoint används

- Jackett /all-endpointen är bekväm, men det är dess enda fördel. Allt annat kan orsaka problem, så det krävs nu att varje spårare läggs till individuellt.
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

### Bokmappar

#### Saknad rotmapp

- Detta fel identifieras vanligtvis om en författare letar efter en rotmapp men den rotmappen är inte längre tillgänglig.
- Detta fel kan också uppstå om en lista fortfarande pekar på en rotmapp men den rotmappen inte längre är tillgänglig.
- Om du vill ta bort denna varning kan du helt enkelt hitta albumet som fortfarande använder den gamla rotmappen och redigera det till rätt rotmapp.

- Det enklaste sättet att hitta problemförfattaren är att:

  - Gå till fliken Författare (Bibliotek)
  - Skapa ett anpassat filter med den gamla sökvägen till rotmappen
  - Välj massredigering i den översta menyn och välj den nya rotmappen som du vill flytta dessa författare till från rullgardinsmenyn Rotmappar.
  - Nästa kommer du att få en popup som frågar Vill du flytta författarmapparna till 'rotmapp' ? Detta kommer också att ange Detta kommer också att döpa om författarmappen enligt författarmappens format i inställningarna. Välj helt enkelt Nej om du inte vill att Lidarr ska flytta dina filer
  - Kör Hälsokontrolluppgiften i System => Uppgifter

### Importlistor

#### Importlistor är otillgängliga på grund av fel

- Vanligtvis betyder detta helt enkelt att Readarr inte längre kan kommunicera via API eller genom att logga in på din valda listtjänst. Om problemet kvarstår är det bästa alternativet att kontakta dem för att utesluta dem, eftersom deras system kan vara överbelastade från tid till annan.

## Diskutrymme

- I det här avsnittet visas tillgängligt diskutrymme
- I Docker kan detta vara knepigt eftersom det vanligtvis visar det tillgängliga utrymmet inom din Docker-bild

## Om

- Detta kommer att berätta om din nuvarande installation av Readarr

## Mer information

- Hemssida: Readarrs startsida
- Wiki: Du är redan här
- Reddit: r/readarr
- Discord: Gå med i vår discord
- Donationer: Om du känner dig generös och vill donera klicka här
- Donationer till Sonarr: Om du känner dig generös och vill donera till projektet som startade allt klicka här
- Källa: GitHub
- Funktionsförfrågningar: Har du en bra idé, lägg fram den här

# Uppgifter

## Schemalagda

- Detta avsnitt listar alla schemalagda uppgifter som Readarr kör

- Kontrollera uppdatering - Detta körs enligt den schemalagda tiden i gränssnittet och kontrollerar om Readarr är på den senaste versionen och utlöser sedan uppdateringsskriptet för att uppdatera Readarr. Inställningar => Uppdatera

> Observera: Om du använder Docker kommer detta inte att uppdatera din behållare eftersom en ny bild måste laddas ner.
{.is-warning}

- Säkerhetskopiering - Detta körs en säkerhetskopiering av din Readarr-databas enligt en inställd tidtabell, mer information om detta finns här. Mer information om säkerhetskopieringar finns under System => Säkerhetskopior.
- Kontrollera hälsa - Kontrollera hälsa körs enligt den schemalagda tiden i gränssnittet och kontrollerar den övergripande hälsan för din Readarr. För att se en lista över möjliga hälsorelaterade problem, se wikin om hälsokontroller.
- Städning - Enligt den schemalagda tiden i gränssnittet kommer detta att dammsuga bort spindelväv, sopa och dammsuga golven, moppa, polera och till och med göra fina små vikta anteckningar bara för dig. Men det tar inte ut soporna. Det fick helt enkelt inte tillräckligt med betalt.
- Synkronisera importlista - Enligt den schemalagda tiden i gränssnittet körs detta dina listor och importerar eventuella nya böcker. Mer information om listor finns under Inställningar => Listor.
- Rensa meddelanden - Enligt den schemalagda tiden i gränssnittet rensar detta upp de meddelanden som visas i det nedre vänstra hörnet av Readarr
- Uppdatera författare - Detta går igenom och uppdaterar alla författare i ditt bibliotek.
- Uppdatera övervakade nedladdningar - Detta går igenom och uppdaterar nedladdningskön som finns under Aktivitet. Det pingar helt enkelt din nedladdningsklient för att kontrollera färdiga nedladdningar.
- Skanna mappar igen - Detta skannar alla bokmappar för att se om en bok finns eller inte och uppdaterar statusen för den på lämpligt sätt.
- RSS-synkronisering - Detta kommer att köra RSS-synkroniseringen. Detta kan ändras i inställningar => alternativ. Mer information om RSS-funktionen finns i vår FAQ
  
> Alla dessa uppgifter kan köras manuellt utanför sina schemalagda tider genom att klicka på ikonen längst till höger för varje uppgift.
{.is-info}

## Kö

Kön visar pågående och kommande uppgifter samt en historik över nyligen körda uppgifter och hur lång tid dessa uppgifter tog.

# Säkerhetskopiering

> Om du vill veta hur du säkerhetskopierar/återställer din Readarr-instans klicka [här](/readarr/faq).
{.is-info}

- Inom säkerhetskopieringsavsnittet presenteras tidigare säkerhetskopior (om du inte har en nyinstallation som inte har gjort några säkerhetskopior).
  
- Säkerhetskopiera nu - Denna alternativ kommer att utlösa en manuell säkerhetskopiering av din Readarr-databas
- Återställ säkerhetskopia - Detta öppnar en ny skärm för att återställa från en tidigare säkerhetskopia
  - Genom att välja Välj fil kommer din webbläsare att öppna en dialogruta för att återställa från en Readarr-zip-säkerhetskopia
  
- Om du har några tidigare säkerhetskopior och vill ladda ner dem från Readarr för att placera dem på en icke-standardplats kan du helt enkelt välja en av dessa filer för att ladda ner dem
- Till höger om varje tidigare nedladdning har du två alternativ.
  - Återställ (Klockikon) - För att återställa från en tidigare säkerhetskopia - Detta öppnar ett nytt fönster för att bekräfta att du vill återställa från denna säkerhetskopia
  - Ta bort (Sopkorg) - För att ta bort en tidigare säkerhetskopia

# Uppdateringar

- Uppdateringsskärmen visar de senaste 5 uppdateringarna som har gjorts samt den nuvarande versionen du använder.
- På denna sida visas också uppdateringsanteckningarna från utvecklarna som berättar vad som har åtgärdats eller lagts till i Readarr (Fira!)
  
> En underhållsversion innehåller buggfixar och andra olika förbättringar. Ta en titt på commit-historiken för specifika detaljer.
{.is-info}

# Händelser

- Fliken Händelser visar vad som har hänt i din Readarr. Detta kan användas för att diagnostisera vissa mindre problem. Detta ersätter dock inte spårloggar som diskuteras i Loggning.

> Händelser motsvarar INFO-loggar. {.is-info}

- Komponenter - Denna kolumn visar vilken komponent inom Readarr som har utlösts
- Meddelande - Denna kolumn visar vilket meddelande som har skickats från komponenten i föregående kolumn.
- Kugghjulsikon - Detta alternativ låter dig ändra hur många komponenter/meddelanden som visas per sida (Standard är 50)
- Alternativ längst upp på sidan
  - Uppdatera - Detta alternativ kommer att uppdatera den aktuella sidan och hämta en ny händelselogg
  - Rensa - Detta kommer att rensa den aktuella händelseloggen och låta dig börja om

# Loggfiler

- Denna sida låter dig ladda ner och se vilka loggfiler som är tillgängliga för Readarr

- På översta raden finns flera alternativ som låter dig kontrollera dina loggfiler.

- Översta raden längst till vänster finns en rullgardinsmeny som låter dig växla mellan loggfiler och uppdateringsloggfiler
  - Loggfiler - Grunden för alla supportfrågor, mer om loggfiler finns här.
  - Uppdateringsloggfiler - Detta visar loggfiler som är associerade med Readarrs uppdateringsskript

> Om du använder Docker kommer detta att vara tomt eftersom du bör uppdatera genom att ladda ner en ny Docker-bild
{.is-info}

- Uppdatera - Detta kommer att uppdatera den aktuella sidan och visa eventuellt nya skapade loggar
- Ta bort - Detta kommer att rensa alla loggar och låta dig börja om
- Filnamn - Detta kommer att visa filnamnet som är associerat med loggen
- Senast skrivet - Detta är den lokala tiden då denna specifika loggfil skrevs.
  - Readarr använder rullande loggfiler som är begränsade till 1 MB var. Den aktuella loggfilen är alltid readarr.txt, för de andra filerna är readarr.0.txt den näst nyaste (ju högre nummer desto äldre är den) upp till totalt 51 loggfiler. Denna loggfil innehåller `fatal`, `error`, `warn` och `info`-poster.
  - När felsökningsloggnivån är aktiverad kommer ytterligare readarr.debug.txt rullande loggfiler att finnas, upp till 51 filer. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info` och `debug`-poster. Den täcker vanligtvis en ~40-timmarsperiod.
  - När spårningsloggnivån är aktiverad kommer ytterligare readarr.trace.txt rullande loggfiler att finnas, upp till 51 filer. Dessa loggfiler innehåller `fatal`, `error`, `warn`, `info`, `debug` och `trace`-poster. På grund av spårningsverbositet täcker den bara ett par timmar som mest.