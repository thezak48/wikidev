---
title: Radarr System
description: 
published: true
date: 2022-10-19T22:59:06.531Z
tags: radarr, needs-love
editor: markdown
dateCreated: 2021-05-25T02:28:35.194Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Status](#status)
  - [Hälsa](#hälsa)
    - [Systemvarningar](#systemvarningar)
      - [Grenen är inte en giltig utgåvogren](#grenen-är-inte-en-giltig-utgåvogren)
      - [Uppdatera till .NET-version](#uppdatera-till-net-version)
        - [Fixa Docker-installationer](#fixa-docker-installationer)
        - [Fixa FreeBSD-installationer](#fixa-freebsd-installationer)
        - [Fixa fristående installationer](#fixa-fristående-installationer)
      - [För närvarande installerad mono-version är gammal och stöds inte](#för-närvarande-installerad-mono-version-är-gammal-och-stöds-inte)
      - [För närvarande installerad SQLite-version stöds inte](#för-närvarande-installerad-sqlite-version-stöds-inte)
      - [Databasen misslyckades med integritetskontroll](#databasen-misslyckades-med-integritetskontroll)
      - [Ny uppdatering finns tillgänglig](#ny-uppdatering-finns-tillgänglig)
      - [Kan inte installera uppdatering eftersom startmappen inte kan skrivas av användaren](#kan-inte-installera-uppdatering-eftersom-startmappen-inte-kan-skrivas-av-användaren)
      - [Uppdatering kommer inte att vara möjlig för att förhindra att AppData raderas vid uppdatering](#uppdatering-kommer-inte-att-vara-möjlig-för-att-förhindra-att-appdata-raderas-vid-uppdatering)
      - [Grenen är för en tidigare version](#grenen-är-för-en-tidigare-version)
      - [Kunde inte ansluta till signalR](#kunde-inte-ansluta-till-signalr)
        - [Nginx](#nginx)
        - [Apache2](#apache2)
        - [Caddy](#caddy)
      - [Misslyckades med att lösa IP-adressen för den konfigurerade proxyvärden](#misslyckades-med-att-lösa-ip-adressen-för-den-konfigurerade-proxyvärden)
      - [Proxy misslyckades med test](#proxy-misslyckades-med-test)
      - [Systemtiden är mer än 1 dag felaktig](#systemtiden-är-mer-än-1-dag-felaktig)
      - [PTP Indexer-inställningar är föråldrade](#ptp-indexer-inställningar-är-föråldrade)
      - [Mono- och x86-byggen upphör](#mono-och-x86-byggen-upphör)
    - [Nedladdningsklienter](#nedladdningsklienter)
      - [Ingen nedladdningsklient är tillgänglig](#ingen-nedladdningsklient-är-tillgänglig)
      - [Kan inte kommunicera med nedladdningsklient](#kan-inte-kommunicera-med-nedladdningsklient)
      - [Nedladdningsklienter är otillgängliga på grund av fel](#nedladdningsklienter-är-otillgängliga-på-grund-av-fel)
      - [Aktivera hantering av slutförda nedladdningar](#aktivera-hantering-av-slutförda-nedladdningar)
      - [Docker felaktig fjärrsökvägsmappning](#docker-felaktig-fjärrsökvägsmappning)
      - [Laddar ner till rotmappen](#laddar-ner-till-rotmappen)
      - [Felaktiga inställningar för nedladdningsklient](#felaktiga-inställningar-för-nedladdningsklient)
      - [Felaktig fjärrsökvägsmappning](#felaktig-fjärrsökvägsmappning)
      - [Behörighetsfel](#behörighetsfel)
      - [Fjärrfilen togs bort under pågående bearbetning](#fjärrfilen-togs-bort-under-pågående-bearbetning)
      - [Fjärrsökväg används och import misslyckades](#fjärrsökväg-används-och-import-misslyckades)
    - [Hantering av slutförda/misslyckade nedladdningar](#hantering-av-slutförda-misslyckade-nedladdningar)
      - [Hantering av slutförda nedladdningar är inaktiverad](#hantering-av-slutförda-nedladdningar-är-inaktiverad)
    - [Indexerare](#indexerare)
      - [Inga indexerare är tillgängliga med aktiverad automatisk sökning, Radarr kommer inte att ge några automatiska sökresultat](#inga-indexerare-är-tillgängliga-med-aktiverad-automatisk-sökning-radarr-kommer-inte-att-ge-några-automatiska-sökresultat)
      - [Inga indexerare är tillgängliga med aktiverad RSS-synkronisering, Radarr kommer inte att hämta nya utgåvor automatiskt](#inga-indexerare-är-tillgängliga-med-aktiverad-rss-synkronisering-radarr-kommer-inte-att-hämta-nya-utgåvor-automatiskt)
      - [Inga indexerare är aktiverade](#inga-indexerare-är-aktiverade)
    - [Aktiverade indexerare stöder inte sökning](#aktiverade-indexerare-stöder-inte-sökning)
      - [Inga indexerare är tillgängliga med aktiverad interaktiv sökning](#inga-indexerare-är-tillgängliga-med-aktiverad-interaktiv-sökning)
      - [Indexerare är otillgängliga på grund av fel](#indexerare-är-otillgängliga-på-grund-av-fel)
      - [Jackett Alla slutpunkter används](#jackett-alla-slutpunkter-används)
        - [Lösningar](#lösningar)
    - [Filmappar](#filmappar)
      - [Saknad rotmapp](#saknad-rotmapp)
    - [Filmer](#filmer)
      - [Filmen togs bort från TMDb](#filmen-togs-bort-från-tmdb)
      - [Listor är otillgängliga på grund av fel](#listor-är-otillgängliga-på-grund-av-fel)
    - [Aviseringar](#aviseringar)
    - [Discord som Slack-avisering](#discord-som-slack-avisering)
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

- Den här sidan innehåller en lista över fel vid hälsokontroller. Dessa hälsokontroller utförs regelbundet av Radarr och vid vissa händelser. De resulterande varningarna och felen listas här för att ge råd om hur man löser dem.

### Systemvarningar

#### Grenen är inte en giltig utgåvogren

- Den gren du har ställt in är inte en giltig utgåvogren. Du kommer inte att få uppdateringar. Ändra till en av de [aktuella utgåvogrenarna](/radarr/faq#how-do-i-update-radarr).

#### Uppdatera till .NET-version

{#update-to-net-core-version}

- Nyare versioner av Radarr är avsedda för .NET6 eller senare. Mono-byggen tillhandahålls inte och stöds inte från och med v4. v3.2.2 är den sista versionen av Radarr som stöder äldre mono-byggen. Du kör en av dessa äldre mono-byggen, men din plattform stöder .NET.

Se nedanstående avsnitt för hur du byter från äldre, inte längre stödda mono-versioner till dotnet.

- [Fixa Docker-installationer](#fixa-docker-installationer)
- [Fixa FreeBSD-installationer](#fixa-freebsd-installationer)
- [Fixa fristående installationer](#fixa-fristående-installationer)
{.links-list}

##### Fixa Docker-installationer

- Se till att din gren är korrekt för din Docker-underhållare och dra om din behållare

##### Fixa FreeBSD-installationer

- Uppdatera helt enkelt Radarr-porten med `pkg update && pkg upgrade`
- (Valfritt) Ta bort mono-paketet om du vill

##### Fixa fristående installationer

Fel som:

```none
Cannot open assembly '/opt/Radarr/Radarr': File does not contain a valid CIL image
```

- Säkerhetskopiera din befintliga konfiguration innan du går vidare till nästa steg.
- Detta bör bara hända på Linux-värdar. Installera inte .NET runtime eller SDK från Microsoft.
- För att åtgärda detta, ladda ner rätt bygg för din arkitektur och ersätt dina befintliga binärer (applikation)
- Kort sagt måste du ta bort dina befintliga binärer (innehållet eller mappen /opt/Radarr) och ersätta med innehållet i .tar.gz-filen du just laddade ner och sedan uppdatera din tjänstefil så att den inte använder mono.

> EXTRAHÖR INTE BARA NEDLADDNINGEN ÖVER DINA BEFINTLIGA BINÄRER.
> DU MÅSTE TA BORT DE GAMLA FÖRST.
{.is-warning}

- Nedan följer ett av communityn utvecklat skript för att ta bort din mono-installation och ersätta den med .NET-installationen. Bidrag och korrigeringar är välkomna.
- Detta antar att du är på Radarr-grenen `master`, så uppdatera variabeln om det behövs
- Detta antar att Radarr körs som användaren `radarr`, så uppdatera variablerna om det behövs
- Detta antar att Radarr är installerat i `/opt/Radarr`, så uppdatera variablerna om det behövs

```bash
#!/bin/bash
## Användarvariabler
installdir="/opt/Radarr"
APPUSER="radarr"
branch="master"
## /Användarvariabler
app="radarr"
ARCH=$(dpkg --print-architecture)
# Stoppa \*arr
sudo systemctl stop $app
# Hämta arkitektur
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "Arkitekturen stöds inte"
    exit 1
    ;;
esac
echo "Hämtar..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Installationen har hämtats och extraherats"
echo "Flyttar befintlig installation"
sudo mv "$installdir/" "$installdir.old/"
echo "Installerar..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "Appen har installerats"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### För närvarande installerad mono-version är gammal och stöds inte

- Radarr är skrivet i .NET och kräver Mono för att köras på mycket gamla ARM-processorer. Mono 5.20 är det absoluta minimum för Radarr.
- Uppgraderingsproceduren för Mono varierar beroende på plattform.

> Mono stöds inte längre från och med Radarr version 4.0
{.is-warning}

#### För närvarande installerad SQLite-version stöds inte

- Radarr lagrar sina data i en SQLite-databas. SQLite3-biblioteket som är installerat på ditt system är för gammalt. Radarr kräver minst version 3.9.0.

> Observera att Radarr använder `libSQLite3.so`, som kan eller inte kan ingå i ett uppgraderingspaket för SQLite3.
{.is-info}

#### Databasen misslyckades med integritetskontroll

- Dina databaser misslyckades med en [SQLite Pragma Integrity Check](https://www.sqlite.org/pragma.html#pragma_integrity_check) och har viss korruption.
- Om `Radarr.db` är korrupt [se detta FAQ-inlägg](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)
- Om `logs.db` är korrupt: Stoppa Radarr, ta bort `logs.db` och eventuella `logs.wal`-filer.
- Om båda är korrupta, granska de respektive processerna ovan.

#### Ny uppdatering finns tillgänglig

- Fira, utvecklarna har släppt en ny uppdatering. Detta innebär vanligtvis fantastiska nya funktioner och lösta buggar (eller hur?). Tydligen har du inte aktiverat automatisk uppdatering, så du måste lista ut hur du uppdaterar på din plattform. Att trycka på Installera-knappen på sidan System => Uppdateringar är förmodligen en bra startpunkt.

> Denna varning visas inte om din nuvarande version är mindre än 14 dagar gammal
{.is-info}

#### Kan inte installera uppdatering eftersom startmappen inte kan skrivas av användaren

- Detta innebär att Radarr inte kommer att kunna uppdatera sig själv. Du måste uppdatera Radarr manuellt eller ange behörigheterna för Radarrs startmapp (installationsmappen) så att Radarr kan uppdatera sig själv.

#### Uppdatering kommer inte att vara möjlig för att förhindra att AppData raderas vid uppdatering

- Radarr upptäckte att AppData-mappen för ditt operativsystem är placerad inuti mappen som innehåller Radarr-binärerna. Normalt sett skulle det vara C:\ProgramData för Windows och ~/.config för Linux.

- Titta på System => Info för att se de aktuella AppData- och startmapparna.
- Detta innebär att Radarr inte kommer att kunna uppdatera sig själv utan att riskera dataförlust.
- Om du använder Linux måste du förmodligen ändra hemmappen för användaren som kör Radarr och kopiera innehållet i den aktuella mappen ~/.config/Radarr för att bevara din databas.

#### Grenen är för en tidigare version

- Uppdateringsgrenen som är inställd i Inställningar/Allmänt är för en tidigare version av Radarr, vilket innebär att instansen inte kommer att se korrekt uppdateringsinformation i System/Uppdateringar och kanske inte får nya uppdateringar när de släpps.

#### Kunde inte ansluta till signalR

- signalR driver de dynamiska UI-uppdateringarna, så om din webbläsare inte kan ansluta till signalR på din server kommer du inte att se några uppdateringar i realtid i gränssnittet.
- Det vanligaste förekomsten av detta är användning av en omvänd proxy eller Cloudflare.
- Cloudflare kräver aktiverade websockets.

##### Nginx

- Nginx kräver följande tillägg till platsblocket för appen:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Se till att du inte inkluderar proxy_set_header Connection "Upgrade"; som föreslås i nginx-dokumentationen. DETTA KOMMER INTE ATT FUNGERA
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache2

För Apache2 omvänd proxy måste du aktivera följande moduler: proxy, proxy_http och proxy_wstunnel. Lägg sedan till denna direktiv för websockets-tunneln i din vhost-konfiguration:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:7878/$1 [P,L]
```

Om du har en omvänd proxy under en underkatalog bör RewriteRule inkludera din basbana, t.ex.

```none
RewriteRule /radarr/(.*) ws://127.0.0.1:7878/radarr/$1 [P,L]
```

Om Radarr inte körs på samma maskin som din omvända proxy. Ersätt 127.0.0.1 med rätt IP-adress/DNS-namn för din Radarr-app.

##### Caddy

För Caddy (V1) använd detta:
Observera: du måste också lägga till websocket-direktivet i din radarr-konfiguration

```none
 proxy /radarr 127.0.0.1:7878 {
     websocket
     transparent
 }
```

#### Misslyckades med att lösa IP-adressen för den konfigurerade proxyvärden

- Granska dina proxyinställningar och se till att de är korrekta
- Se till att din proxy är igång, fungerar och är tillgänglig

#### Proxy misslyckades med test

- Din konfigurerade proxy misslyckades med att testa framgångsrikt, granska det HTTP-fel som tillhandahålls och/eller kontrollera loggarna för mer information.

#### Systemtiden är mer än 1 dag felaktig

- Systemtiden är mer än 1 dag felaktig. Schemalagda uppgifter kan inte köras korrekt förrän tiden har korrigerats.
- Granska systemtiden och se till att den är synkroniserad med en auktoritativ tidsserver och är korrekt.

#### PTP Indexer-inställningar är föråldrade

- Följande PassThePopcorn-indexerare har föråldrade inställningar och bör uppdateras.

#### Mono- och x86-byggen upphör

- Mono- och x86-byggen kommer inte längre att stödjas med v4. Om du får detta felmeddelande kör du antingen mono-versionen av programmet eller x86-versionen. Tyvärr kommer vi att sluta stödja dessa äldre versioner på grund av ökande svårigheter med utvecklingsstöd för dessa äldre versioner. Det rekommenderas därför att du uppgraderar till ett stödd operativsystem som inte kräver varken x86 eller mono. Du kan också överväga att använda Docker för dina behov.

### Nedladdningsklienter

#### Ingen nedladdningsklient är tillgänglig

- En korrekt konfigurerad och aktiverad nedladdningsklient krävs för att Radarr ska kunna ladda ner media. Eftersom Radarr stöder olika nedladdningsklienter bör du bestämma vilken som bäst motsvarar dina krav. Om du redan har en nedladdningsklient installerad bör du konfigurera Radarr att använda den och skapa en kategori. Se Inställningar => Nedladdningsklient.

#### Kan inte kommunicera med nedladdningsklient

- Radarr kunde inte kommunicera med den konfigurerade nedladdningsklienten. Kontrollera om nedladdningsklienten är igång och dubbelkolla URL:en. Detta kan också indikera ett autentiseringsfel.
- Detta beror vanligtvis på en felaktigt konfigurerad nedladdningsklient. Saker du vanligtvis kan kontrollera:
  - IP-adressen för din nedladdningsklient, om den är på samma fysiska maskin är detta vanligtvis 127.0.0.1
  - Portnumret som din nedladdningsklient använder, dessa fylls i med standardportnumret men om du har ändrat det måste du ange samma nummer i Radarr.
  - Se till att SSL-kryptering inte är aktiverad om du använder både din Radarr-instans och din nedladdningsklient i ett lokalt nätverk. Se SSL-FAQ-inlägget för mer information.
  - Se till att IPv6 är inaktiverat på systemet om det inte fungerar
  - Se till att en DNS-server (t.ex. pihole) inte begränsar hastigheten för frågor

#### Nedladdningsklienter är otillgängliga på grund av fel

- En eller flera av dina nedladdningsklienter svarar inte på förfrågningar från Radarr. Därför har Radarr beslutat att tillfälligt sluta fråga nedladdningsklienten enligt dess normala 1-minuterscykel, som normalt används för att spåra aktiva nedladdningar och importera färdiga nedladdningar. Radarr kommer dock fortsätta att försöka skicka nedladdningar till klienten, men kommer med stor sannolikhet att misslyckas.
- Du bör inspektera System=>Loggar för att se vad orsaken till felen är.
- Om du inte längre använder denna nedladdningsklient bör du inaktivera den i Radarr för att förhindra felmeddelanden.

#### Aktivera hantering av slutförda nedladdningar

- Radarr kräver att hantering av slutförda nedladdningar är aktiverat för att kunna importera filer som laddats ner av nedladdningsklienten. Det rekommenderas att du aktiverar hantering av slutförda nedladdningar. (Hantering av slutförda nedladdningar är aktiverat som standard för nya användare.)

#### Docker felaktig fjärrsökvägsmappning

- Detta fel är vanligtvis förknippat med felaktiga Docker-sökvägar i antingen din nedladdningsklient eller Radarr.

- Ett exempel på detta skulle vara:
  - Nedladdningsklient: Nedladdningsväg: /mnt/user/downloads:/downloads
  - Radarr: Nedladdningsväg: /mnt/user/downloads:/data
- I detta exempel placerar nedladdningsklienten sina nedladdningar i /downloads och talar sedan om för Radarr när de är klara att den färdiga filmen finns i /downloads. Sedan kommer Radarr och säger "Okej, coolt, låt mig kolla i /downloads" Men i Radarr har du inte tilldelat en /downloads-sökväg, du har tilldelat en /data-sökväg, så det kastar detta fel.
- Det enklaste sättet att lösa detta är KONSISTENS. Om du använder ett system i din nedladdningsklient, använd det över hela linjen.

- Team Radarr gillar att helt enkelt använda /data.
  - Nedladdningsklient: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Nu kan du inom nedladdningsklienten ange var i /data du vill placera dina nedladdningar, detta varierar beroende på klienten men du bör kunna tala om för den "Ja, nedladdningsklient, placera mina filer i." /data/torrents (eller usenet)/movies och eftersom du använde /data i Radarr när nedladdningsklienten säger till Radarr att den är klar kommer Radarr att säga "Bra, jag har en /data och jag kan också se /torrents (eller usenet)/movies allt är rätt i världen."
- Det finns många bra guider: vår wiki [Docker Guide](/docker-guide) och TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Dessa guider lägger stor vikt vid hardlinks och atomic moves, men den allmänna principen för containrar och hur sökvägsmappning fungerar är kärnan i dessa diskussioner.

- Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) för mer information.

#### Laddar ner till rotmappen

{#downloads-in-root-folder}

- Inom applikationen definieras en rotmapp som den konfigurerade mediebiblioteksmappen. Detta är inte rotmappen för en montering. Din nedladdningsklient laddar ner ofullständiga eller kompletta (eller flyttar kompletta nedladdningar) till din rot (biblioteks) mapp.
- Detta orsakar ofta problem - inklusive dataförlust - och bör inte göras. För att åtgärda detta, ändra din nedladdningsklient så att den inte placerar nedladdningar inom din rotmapp. Observera att 'placering' även inkluderar om din nedladdningsklients kategori är inställd på din rotmapp eller om NZBGet/SABnzbd har sortering aktiverad och sorterar till din rotmapp.
- Observera att den här kontrollen tittar på alla definierade/konfigurerade rotmappar som har lagts till, inte bara rotmappar som för närvarande används. Med andra ord bör inte mappen där din nedladdningsklient laddar ner eller flyttar kompletta nedladdningar till vara samma mapp som du har konfigurerat som din rot/biblioteks/slutliga mediamålmapp i *arr-applikationen.
- Konfigurerade rotmappar (även kallade biblioteksmappar) finns i [Inställningar => Mediahantering => Rotmappar](/radarr/settings/#root-folders)
- Ett exempel är om dina nedladdningar går till `\data\downloads` och du har en rotmapp som är inställd på `\data\downloads`.
- Det rekommenderas att använda sökvägar som `\data\media\` för din rotmapp/bibliotek och `\data\downloads\` för dina nedladdningar.
- Granska vår [Docker Guide](/docker-guide) och TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) för mer information om korrekt och optimal sökvägskonfiguration. Observera att koncepten gäller både docker och icke-docker

> Din nedladdningsmapp där din nedladdningsklient placerar nedladdningarna och din rot/biblioteksmapp MÅSTE vara separata. \*Arr kommer att importera filen/filerna från din nedladdningsklients mapp till ditt bibliotek. Nedladdningsklienten bör inte flytta något eller ladda ner något till ditt bibliotek.
{.is-warning}

#### Felaktiga inställningar för nedladdningsklient

- Platsen där din nedladdningsklient laddar ner filer orsakar problem. Kontrollera loggarna för mer information. Detta kan bero på behörigheter eller försök att gå från Windows till Linux eller Linux till Windows utan fjärrsökvägsmappning.

#### Felaktig fjärrsökvägsmappning

- Platsen där din nedladdningsklient laddar ner filer orsakar problem. Kontrollera loggarna för mer information. Detta kan bero på behörigheter eller försök att gå från Windows till Linux eller Linux till Windows utan fjärrsökvägsmappning. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) för mer information.

#### Behörighetsfel

- Radarr eller användaren radarr som Radarr körs som kan inte komma åt platsen där din nedladdningsklient laddar ner filer. Detta beror vanligtvis på ett behörighetsproblem.

#### Fjärrfilen togs bort under pågående bearbetning

- En fil som är tillgänglig via en fjärrsökvägsmappning verkar ha tagits bort innan bearbetningen var klar.

#### Fjärrsökväg används och import misslyckades

- Kontrollera loggarna för mer information. Se våra felsökningsguider

### Hantering av slutförda/misslyckade nedladdningar

#### Hantering av slutförda nedladdningar är inaktiverad

- (Detta varningsmeddelande genereras endast för befintliga användare innan funktionen för hantering av slutförda nedladdningar implementerades. Denna funktion är inaktiverad som standard för att säkerställa att systemet fortsatte att fungera som förväntat för befintliga konfigurationer.)
- Det rekommenderas att du använder hantering av slutförda nedladdningar eftersom det ger bättre kompatibilitet för uppacknings- och efterbehandlingslogiken för olika nedladdningsklienter. Med det kommer Radarr bara att importera en nedladdning när nedladdningsklienten rapporterar att den är klar.
- Om du vill aktivera hantering av slutförda nedladdningar bör du verifiera följande: * Varning: Hantering av slutförda nedladdningar fungerar endast korrekt om nedladdningsklienten och Radarr är på samma maskin eftersom den får sökvägen att importera direkt från nedladdningsklienten, annars krävs en fjärrkarta.

### Indexerare

#### Inga indexerare är tillgängliga med aktiverad automatisk sökning, Radarr kommer inte att ge några automatiska sökresultat

- Helt enkelt sagt har du inte några indexerare inställda för att tillåta automatiska sökningar
- Gå till Inställningar => Indexerare, välj en indexerare du vill tillåta automatiska sökningar och klicka sedan på Spara.

#### Inga indexerare är tillgängliga med aktiverad RSS-synkronisering, Radarr kommer inte att hämta nya utgåvor automatiskt

- Radarr använder RSS-flödet för att plocka upp nya utgåvor allt eftersom de kommer. Mer information om det finns här
- För att åtgärda detta problem går du till Inställningar => Indexerare, välj en indexerare du har och aktivera RSS-synkronisering

#### Inga indexerare är aktiverade

- Radarr kräver indexerare för att kunna upptäcka nya utgåvor. Läs wikin för instruktioner om hur du lägger till indexerare.

#### Aktiverade indexerare stöder inte sökning

- Inga av de indexerare du har aktiverat stöder sökning. Det innebär att Radarr bara kommer att kunna hitta nya utgåvor via RSS-flödena. Men att söka efter filmer (antingen automatisk sökning eller manuell sökning) kommer aldrig att ge några resultat. Det enda sättet att åtgärda detta är att lägga till en annan indexerare.

#### Inga indexerare är tillgängliga med aktiverad interaktiv sökning

- Inga av de indexerare du har aktiverat stöder interaktiv sökning. Det innebär att programmet bara kommer att kunna hitta nya utgåvor via RSS-flöden eller automatisk sökning.

#### Indexerare är otillgängliga på grund av fel

- Fel inträffar när Radarr försökte använda en av dina indexerare. För att begränsa försöken kommer Radarr inte att använda indexeraren under en ökande tid (upp till 24 timmar).
- Denna mekanism utlöses om Radarr inte kunde få ett svar från indexeraren (kan bero på DNS, proxy/vpn-anslutning, autentisering eller indexerarproblem) eller om Radarr inte kunde hämta nzb/torrent-filen från indexeraren. Granska loggarna för att avgöra vilken typ av fel som orsakade problemet.
- Du kan förhindra varningen genom att inaktivera den berörda indexeraren.
- Kör testet på indexeraren för att tvinga Radarr att kontrollera indexeraren igen, observera att varningen för hälsokontrollen inte alltid försvinner omedelbart.

#### Jackett Alla slutpunkter används

- Jackett /all-slutpunkten är bekväm, men det är dess enda fördel. Allt annat är potentiella problem, så nu krävs det att varje spårare läggs till individuellt.
- [Även Jacketts utvecklare säger att det bör undvikas och inte användas.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Att använda /all-slutpunkten har inga fördelar, bara nackdelar:
  - du förlorar kontrollen över inställningar för specifika indexerare (kategorier, söklägen, etc.)
  - att blanda söklägen (IMDB, fråga, etc.) kan ge lågkvalitativa resultat
  - indexerarspecifika kategorier (\>= 100000) kan inte användas.
  - långsamma indexerare kommer att sakta ner det totala resultatet
  - totala resultat är begränsade till 1000
  - om en av spårarna i /all returnerar ett fel kommer \*Arr att inaktivera den och nu får du inga resultat.

##### Lösningar

- Lägg till varje spårare i Jackett manuellt som en indexerare i \*Arr
- Kolla in [Prowlarr](/prowlarr) som kan synkronisera indexerare till \*Arr och från Lidarr/Radarr/Readarr-utvecklingsteamet.
- Kolla in [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisera indexerare till \*Arr. Men använd inte deras enskilda samlade slutpunkt och använd `multi` om synkronisering kommer att användas.

### Filmappar

#### Saknad rotmapp

{#movie-collection-missing-root-folder}

- Detta fel identifieras vanligtvis om en film eller samling tilldelas en rotmapp, men den rotmappen är inte längre tillgänglig.
- Detta fel kan också uppstå om en lista fortfarande är kopplad till en rotmapp och den rotmappen inte längre är tillgänglig.
- Om du vill ta bort den här varningen, hitta helt enkelt filmerna eller samlingarna som fortfarande använder den gamla rotmappen och redigera dem till rätt rotmapp.

##### Filmöversiktstabell

1. Gå till fliken Filmer (Bibliotek)
1. Tabellvy och aktivera kolumnen Sökväg och sortera efter sökväg

##### Anpassat filter för filmer

1. Skapa ett anpassat filter med den gamla rotmappens sökväg
1. Välj massredigering i toppmenyn och välj den nya rotmappen som du vill flytta dessa filmer till från rullgardinsmenyn Rotmappar.
1. Nästa kommer du att få en popup som säger "Vill du flytta filmmapparna till 'rotmapp'?" Detta kommer också att säga Detta kommer också att döpa om filmmappen enligt filmmappens format i inställningarna. Välj helt enkelt Nej om du inte vill att Radarr ska flytta dina filer.
1. Kör uppgiften Kontrollera hälsa i System => Uppgifter

#### Anpassat filter för samlingar

1. Skapa ett anpassat filter i Samlingar med den gamla rotmappens sökväg
1. Välj samlingarna och välj den nya rotmappen som du vill att dessa samlingars framtida filmer ska tilldelas.
1. Kör uppgiften Kontrollera hälsa i System => Uppgifter

### Filmer

#### Filmen togs bort från TMDb

- Filmen är kopplad till ett TMDb

## Kö

- Köen visar dig körande och kommande uppgifter samt en historik över nyligen körda uppgifter och hur lång tid dessa uppgifter tog.

# Säkerhetskopiering

> Om du letar efter hur du säkerhetskopierar/återställer din Radarr-instans klicka [här](/radarr/faq).
{.is-info}

- Inom avsnittet Säkerhetskopiering kommer du att presenteras med tidigare säkerhetskopior (om du inte har en ny installation som inte har gjort några säkerhetskopior).
  
- Säkerhetskopiera nu - Detta alternativ kommer att utlösa en manuell säkerhetskopiering av din Radarr-databas.
- Återställ säkerhetskopia - Detta kommer att öppna en ny skärm för att återställa från en tidigare säkerhetskopia.
  - Genom att välja Välj fil kommer din webbläsare att öppna en dialogruta för att återställa från en Radarr-zip-säkerhetskopia.
  
- Om du har några tidigare säkerhetskopior och vill ladda ner dem från Radarr för att placera dem på en icke-standardplats kan du helt enkelt välja en av dessa filer för att ladda ner dem.
- Till höger om varje tidigare nedladdning har du två alternativ.
  - Återställ (Klockikon) - För att återställa från en tidigare säkerhetskopia - Detta kommer att öppna ett nytt fönster för att bekräfta att du vill återställa från denna säkerhetskopia.
  - Ta bort (Soptunna) - För att ta bort en tidigare säkerhetskopia.

# Uppdateringar

- Uppdateringsskärmen visar de senaste 5 uppdateringarna som har gjorts samt den nuvarande versionen du använder.
- På denna sida visas också uppdateringsanteckningarna från utvecklarna som berättar vad som har åtgärdats eller lagts till i Radarr (Fira!)

> En underhållsutgåva innehåller buggfixar och andra olika förbättringar. Ta en titt på ändringshistoriken för specifika detaljer.
{.is-info}

# Händelser

- Fliken Händelser visar vad som har hänt inom din Radarr. Detta kan användas för att diagnostisera vissa mindre problem. Observera att detta inte ersätter spårningsloggar som diskuteras i Loggning.

> Händelser motsvarar INFO-loggar. {.is-info}

- Komponenter - Denna kolumn visar vilken komponent inom Radarr som har utlösts.
- Meddelande - Denna kolumn visar vilket meddelande som har skickats från komponenten i föregående kolumn.
- Kugghjulsikon - Detta alternativ låter dig ändra hur många komponenter/meddelanden som visas per sida (standard är 50).
- Alternativ längst upp på sidan
  - Uppdatera - Detta alternativ kommer att uppdatera den aktuella sidan och hämta en ny händelselogg.
  - Rensa - Detta kommer att rensa den aktuella händelseloggen och låta dig börja om från början.

# Loggfiler

- Denna sida låter dig ladda ner och se vilka aktuella loggfiler som är tillgängliga för Radarr.

- På översta raden finns flera alternativ som låter dig kontrollera dina loggfiler.

- Längst till vänster på översta raden finns en rullgardinsmeny som låter dig växla mellan loggfiler och uppdateringsloggfiler.
  - Loggfiler - Grundläggande för alla supportärenden, mer information om loggfiler finns här.
  - Uppdateringsloggfiler - Detta visar loggfiler som är associerade med Radarrs uppdateringsskript.

> Om du använder Docker kommer detta vara tomt eftersom du bör uppdatera genom att ladda ner en ny Docker-bild.
{.is-info}

- Uppdatera - Detta kommer att uppdatera den aktuella sidan och visa eventuellt nyss skapade loggar.
- Ta bort - Detta kommer att rensa alla loggar och låta dig börja om från början.
- Filnamn - Detta kommer att visa filnamnet som är associerat med loggen.
- Senast skrivet - Detta är den lokala tiden då denna specifika loggfil skrevs.
  - Radarr använder rullande loggfiler som är begränsade till 1 MB var. Den aktuella loggfilen är alltid radarr.txt, för de andra filerna är radarr.0.txt den näst nyaste (ju högre nummer desto äldre är den) upp till totalt 51 loggfiler. Denna loggfil innehåller `fatal`, `error`, `warn` och `info`-poster.
  - När felsökningsloggning är aktiverad kommer ytterligare rullande loggfiler radarr.debug.txt att finnas, upp till 51 filer. Denna loggfil innehåller `fatal`, `error`, `warn`, `info` och `debug`-poster. Den täcker vanligtvis en ~40-timmarsperiod.
  - När spårningsloggning är aktiverad kommer ytterligare rullande loggfiler radarr.trace.txt att finnas, upp till 51 filer. Denna loggfil innehåller `fatal`, `error`, `warn`, `info`, `debug` och `trace`-poster. På grund av spårningsvolymen täcker den endast ett par timmar som mest.