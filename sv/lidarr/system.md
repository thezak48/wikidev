Jag översätter dokumentationen för att hjälpa användare. Översätt Markdown-innehållet jag kommer att klistra in senare till svenska. Du måste strikt följa reglerna nedan. - Ändra aldrig Markdown-märkningsstrukturen. Lägg inte till eller ta bort länkar. Ändra inte någon URL. - Ändra aldrig innehållet i kodblock även om de verkar ha en bugg. - Bevara alltid de ursprungliga radbrytningarna. Lägg inte till eller ta bort blanka rader. - Rör inte permalänken som `{/*exempel*/}` i slutet av varje rubrik. - Rör inte HTML-liknande taggar som `<Notes>`.

---
title: Lidarr System
description: 
published: true
date: 2022-10-31T04:35:13.645Z
tags: lidarr, needs-love, system
editor: markdown
dateCreated: 2021-06-14T21:36:28.225Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Status](#status)
  - [Hälsa](#hälsa)
    - [Systemvarningar](#systemvarningar)
      - [Grenen är inte en giltig utgåvogren](#grenen-är-inte-en-giltig-utgåvogren)
      - [Uppdatera till .NET-version](#uppdatera-till-net-version)
        - [Fixa Docker-installationer](#fixa-docker-installationer)
        - [Fixa fristående installationer](#fixa-fristående-installationer)
      - [För närvarande installerad mono-version är gammal och stöds inte](#för-närvarande-installerad-mono-version-är-gammal-och-stöds-inte)
      - [För närvarande installerad SQLite-version stöds inte](#för-närvarande-installerad-sqlite-version-stöds-inte)
      - [Ny uppdatering finns tillgänglig](#ny-uppdatering-finns-tillgänglig)
      - [Kan inte installera uppdatering eftersom startmappen inte kan skrivas av användaren](#kan-inte-installera-uppdatering-eftersom-startmappen-inte-kan-skrivas-av-användaren)
      - [Uppdatering kommer inte att vara möjlig för att förhindra att AppData raderas vid uppdatering](#uppdatering-kommer-inte-att-vara-möjlig-för-att-förhindra-att-appdata-raderas-vid-uppdatering)
      - [Grenen är för en tidigare version](#grenen-är-för-en-tidigare-version)
      - [Kunde inte ansluta till signalR](#kunde-inte-ansluta-till-signalr)
        - [NGINX](#nginx)
        - [Apache](#apache)
        - [Caddy](#caddy)
      - [Misslyckades med att lösa IP-adressen för den konfigurerade proxyvärden](#misslyckades-med-att-lösa-ip-adressen-för-den-konfigurerade-proxyvärden)
      - [Proxy misslyckades test](#proxy-misslyckades-test)
      - [Systemtiden är mer än 1 dag felaktig](#systemtiden-är-mer-än-1-dag-felaktig)
      - [Mono Legacy TLS aktiverat](#mono-legacy-tls-aktiverat)
      - [Mono och x86-byggen upphör](#mono-och-x86-byggen-upphör)
      - [FPcalc behöver uppdateras](#fpcalc-behöver-uppdateras)
    - [Nedladdningsklienter](#nedladdningsklienter)
      - [Ingen nedladdningsklient är tillgänglig](#ingen-nedladdningsklient-är-tillgänglig)
      - [Kan inte kommunicera med nedladdningsklient](#kan-inte-kommunicera-med-nedladdningsklient)
      - [Nedladdningsklienter är otillgängliga på grund av fel](#nedladdningsklienter-är-otillgängliga-på-grund-av-fel)
      - [Aktivera hantering av slutförda nedladdningar](#aktivera-hantering-av-slutförda-nedladdningar)
      - [Docker felaktig fjärrsökvägsmappning](#docker-felaktig-fjärrsökvägsmappning)
      - [Laddar ner till rotmapp](#laddar-ner-till-rotmapp)
      - [Felaktiga inställningar för nedladdningsklient](#felaktiga-inställningar-för-nedladdningsklient)
      - [Felaktig fjärrsökvägsmappning](#felaktig-fjärrsökvägsmappning)
      - [Behörighetsfel](#behörighetsfel)
      - [Fjärrfilen togs bort under bearbetning](#fjärrfilen-togs-bort-under-bearbetning)
      - [Fjärrsökväg används och importen misslyckades](#fjärrsökväg-används-och-importen-misslyckades)
    - [Hantering av slutförda/misslyckade nedladdningar](#hantering-av-slutförda-misslyckade-nedladdningar)
      - [Hantering av slutförda nedladdningar är inaktiverad](#hantering-av-slutförda-nedladdningar-är-inaktiverad)
    - [Indexerare](#indexerare)
      - [Inga indexerare är tillgängliga med aktiverad automatisk sökning, Lidarr kommer inte att ge några automatiska sökresultat](#inga-indexerare-är-tillgängliga-med-aktiverad-automatisk-sökning-lidarr-kommer-inte-att-ge-några-automatiska-sökresultat)
      - [Inga indexerare är tillgängliga med aktiverad RSS-synkronisering, Lidarr kommer inte att hämta nya utgåvor automatiskt](#inga-indexerare-är-tillgängliga-med-aktiverad-rss-synkronisering-lidarr-kommer-inte-att-hämta-nya-utgåvor-automatiskt)
      - [Inga indexerare är aktiverade](#inga-indexerare-är-aktiverade)
    - [Aktiverade indexerare stöder inte sökning](#aktiverade-indexerare-stöder-inte-sökning)
      - [Inga indexerare är tillgängliga med aktiverad interaktiv sökning](#inga-indexerare-är-tillgängliga-med-aktiverad-interaktiv-sökning)
      - [Indexerare är otillgängliga på grund av fel](#indexerare-är-otillgängliga-på-grund-av-fel)
      - [Jackett används för alla slutpunkter](#jackett-används-för-alla-slutpunkter)
        - [Lösningar](#lösningar)
    - [Artistmappar](#artistmappar)
      - [Saknad rotmapp](#saknad-rotmapp)
      - [Listor är otillgängliga på grund av fel](#listor-är-otillgängliga-på-grund-av-fel)
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

> Varning: Denna sida är under arbete och är för närvarande ett utkast baserat på Readarr
{.is-danger}

# Status

## Hälsa

Denna sida innehåller en lista över fel vid hälsokontroller. Dessa hälsokontroller utförs periodvis av Lidarr och vid vissa händelser. De resulterande varningarna och felen listas här för att ge råd om hur man löser dem.

### Systemvarningar

#### Grenen är inte en giltig utgåvogren

Den gren du har ställt in är inte en giltig utgåvogren. Du kommer inte att få uppdateringar. Ändra till en av de [aktuella utgåvogrenarna](/lidarr/faq#how-do-i-update-lidarr)

#### Uppdatera till .NET-version

{#update-to-net-core-version}

- Nyare versioner av Lidarr är avsedda för .NET6 eller senare. Vi kommer inte längre att tillhandahålla äldre mono-versioner efter att 1.0 har släppts. Du kör en av dessa äldre versioner men din plattform stöder .NET.

##### Fixa Docker-installationer

- Dra om din behållare

##### Fixa fristående installationer

- Säkerhetskopiera din befintliga konfiguration innan du går vidare till nästa steg.
- Detta bör bara hända på Linux-värdar. Installera inte .NET-runtime eller SDK från Microsoft.
- För att åtgärda, ladda ner rätt version för din arkitektur och ersätt dina befintliga binärer (program)
- Kort sagt måste du ta bort dina befintliga binärer (innehåll eller mapp i /opt/Lidarr) och ersätta med innehållet i .tar.gz-filen du just laddade ner.

> TA INTE BARA UT PAKETET ÖVER DINA BEFINTLIGA BINÄRER.
> DU MÅSTE TA BORT DE GAMLA FÖRST.
{.is-warning}

- Nedan följer ett skript som utvecklats av gemenskapen för att ta bort din mono-installation och ersätta den med .NET-installationen. Bidrag och korrigeringar är välkomna.
- Detta antar att du är på Lidarr-grenen `master`, uppdatera variabeln om det behövs
- Detta antar att Lidarr körs som användaren `lidarr`, uppdatera variablerna om det behövs
- Detta antar att Lidarr är installerat i `/opt/Lidarr`, uppdatera variablerna om det behövs

```bash
#!/bin/bash
## Användarvariabler
installdir="/opt/Lidarr"
APPUSER="lidarr"
branch="master"
## /Användarvariabler
app="lidarr"
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
    echo_error "Arkitektur stöds inte"
    exit 1
    ;;
esac
echo "Hämtar..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Installationsfiler hämtade och extraherade"
echo "Flyttar befintlig installation"
sudo mv "$installdir/" "$installdir.old/"
echo "Installerar..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "App installerad"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### För närvarande installerad mono-version är gammal och stöds inte

- Lidarr är skrivet i .NET och kräver Mono för att köras på mycket gamla ARM-processorer. Observera att Mono-versioner inte längre stöds efter v1.0
- Mono 5.20 är det absoluta minimum för Lidarr.
- Uppgraderingsproceduren för Mono varierar beroende på plattform.

#### För närvarande installerad SQLite-version stöds inte

- Lidarr lagrar sina data i en SQLite-databas. SQLite3-biblioteket som är installerat på ditt system är för gammalt. Lidarr kräver minst version 3.9.0. Observera att Lidarr använder `libSQLite3.so` som kan finnas i en uppgraderingspaket för SQLite3.

#### Ny uppdatering finns tillgänglig

- Fira, utvecklarna har släppt en ny uppdatering. Detta innebär vanligtvis fantastiska nya funktioner och lösta buggar (eller hur?). Tydligen har du inte aktiverat automatisk uppdatering, så du måste lista ut hur du uppdaterar på din plattform. Att trycka på Installera-knappen på sidan `System => Uppdateringar` är förmodligen en bra startpunkt.

> Denna varning visas inte om din nuvarande version är mindre än 14 dagar gammal
{.is-info}

#### Kan inte installera uppdatering eftersom startmappen inte kan skrivas av användaren

- Detta innebär att Lidarr inte kommer att kunna uppdatera sig själv. Du måste uppdatera Lidarr manuellt eller ange behörigheterna för Lidarrs startmapp (installationsmappen) så att Lidarr kan uppdatera sig själv.

#### Uppdatering kommer inte att vara möjlig för att förhindra att AppData raderas vid uppdatering

- Lidarr upptäckte att AppData-mappen för ditt operativsystem är placerad inuti mappen som innehåller Lidarr-binärerna. Normalt skulle det vara `C:\ProgramData` för Windows och `~/.config` för Linux.

- Titta på `System => Info` för att se aktuella AppData- och startmappar.
- Detta innebär att Lidarr inte kommer att kunna uppdatera sig själv utan att riskera dataförlust.
- Om du använder Linux måste du förmodligen ändra hemmappen för användaren som kör Lidarr och kopiera innehållet i den aktuella mappen `~/.config/Lidarr` för att bevara din databas.

#### Grenen är för en tidigare version

- Uppdateringsgrenen som är inställd i `Inställningar => Allmänt` är för en tidigare version av Lidarr, därför kommer instansen inte att se korrekt uppdateringsinformation i flödet `System => Uppdateringar` och kanske inte får nya uppdateringar vid släpp.

#### Kunde inte ansluta till signalR

- signalR driver dynamiska UI-uppdateringar, så om din webbläsare inte kan ansluta till signalR på din server kommer du inte att se några uppdateringar i realtid i användargränssnittet.

- Det vanligaste förekomsten av detta är användning av en omvänd proxy eller Cloudflare
- Cloudflare behöver aktiverade websockets.

##### NGINX

- Nginx kräver följande tillägg till platsblocket för appen:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Se till att du inte inkluderar `proxy_set_header Connection "Upgrade";` som föreslås i nginx-dokumentationen. DETTA KOMMER INTE ATT FUNGERA
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache

- För Apache2 omvänd proxy måste du aktivera följande moduler: proxy, proxy_http och proxy_wstunnel. Lägg sedan till denna websocket-tunnelanvisning i din vhost-konfiguration:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8686/$1 [P,L]
```

##### Caddy

- För Caddy (V1) använd detta:
- Observera att du också måste lägga till websocket-anvisningen i din Lidarr-konfiguration

```none
 proxy /lidarr 127.0.0.1:8686 {
     websocket
     transparent
 }
```

#### Misslyckades med att lösa IP-adressen för den konfigurerade proxyvärden

- Granska dina proxyinställningar och se till att de är korrekta
- Se till att din proxy är igång, fungerande och tillgänglig

#### Proxy misslyckades test

- Din konfigurerade proxy misslyckades med att testa framgångsrikt, granska det HTTP-fel som tillhandahålls och/eller kontrollera loggarna för mer information.

#### Systemtiden är mer än 1 dag felaktig

- Systemtiden är mer än 1 dag felaktig. Schemalagda uppgifter kan inte köras korrekt förrän tiden har korrigerats
- Granska systemtiden och se till att den är synkroniserad med en auktoritativ tidsserver och är korrekt

#### Mono Legacy TLS aktiverat

- Mono 4.x tls-åtgärd är fortfarande aktiverad, överväg att ta bort miljöalternativet `MONO_TLS_PROVIDER=legacy`

#### Mono och x86-byggen upphör

- Mono- och x86-byggen kommer inte längre att stödjas i nästa version av programmet. Om du får detta felmeddelande kör du antingen mono-versionen av programmet eller x86-versionen. Tyvärr kommer vi att sluta stödja dessa äldre versioner på grund av ökande svårigheter med utvecklingsstöd för dessa äldre versioner. Därför rekommenderas att du uppgraderar till ett stödsystem som inte kräver vare sig x86 eller mono. Du kan också överväga att använda Docker för dina behov.

#### FPcalc behöver uppdateras

{#fpcalc-upgrade}

- Lidarr använder ljudfingeravtryck med chromaprint för att identifiera spår. Detta beror på en extern binär `fpcalc`, som distribueras med Lidarr v1 för Windows, Linux och macOS, men måste tillhandahållas separat på freeBSD.
- Se till att den fpcalc-binär som medföljer Lidarr är körbar (755-behörigheter). Den finns i Lidarrs installationsmapp (t.ex. `/opt/Lidarr/fpcalc`). Om den inte är körbar, korrigera dess behörigheter med följande kommando och starta om Lidarr.
  - Observera att `sudo` kan krävas för att fixa detta eller att sökvägen till Lidarrs binärmapp kan vara annorlunda beroende på din miljö och konfiguration.

```bash
chmod +x /opt/Lidarr/fpcalc
```

> Följande information gäller endast för äldre v0.8.0-versioner.
{.is-info}

- För att åtgärda detta på en nativ Linux-instans, installera den lämpliga paketet med hjälp av din pakethanterare och se till att fpcalc finns i din PATH (detta kan kontrolleras med kommandot `which fpcalc` och verifiera att rätt plats för fpcalc returneras):

| Distribution  |       Paket        |
| :-----------: | :------------------: |
| Debian/Ubuntu | libchromaprint-tools |
| Fedora/CentOS |  chromaprint-tools   |
|     Arch      |     chromaprint      |
|   OpenSUSE    |  chromaprint-fpcalc  |
|   Synology    |     chromaprint      |

### Nedladdningsklienter

#### Ingen nedladdningsklient är tillgänglig

- En korrekt konfigurerad och aktiverad nedladdningsklient krävs för att Lidarr ska kunna ladda ner media. Eftersom Lidarr stöder olika nedladdningsklienter bör du bestämma vilken som bäst passar dina behov. Om du redan har en nedladdningsklient installerad bör du konfigurera Lidarr att använda den och skapa en kategori. Se `Inställningar => Nedladdningsklient`.

#### Kan inte kommunicera med nedladdningsklient

- Lidarr kunde inte kommunicera med den konfigurerade nedladdningsklienten. Kontrollera att nedladdningsklienten är igång och dubbelkolla URL:en. Detta kan också indikera ett autentiseringsfel.
- Detta beror vanligtvis på en felaktigt konfigurerad nedladdningsklient. Saker du vanligtvis kan kontrollera:
  - IP-adressen för din nedladdningsklient - om allt är på samma fysiska maskin är detta vanligtvis `127.0.0.1`
  - Portnumret som din nedladdningsklient använder - dessa fylls i med standardportnumret, men om du har ändrat det måste du ange samma nummer i Lidarr.
  - Se till att SSL-kryptering inte är aktiverad om du använder både din Lidarr-instans och din nedladdningsklient i ett lokalt nätverk (dvs över vanlig HTTP). Se SSL-FAQ:n för mer information.

#### Nedladdningsklienter är otillgängliga på grund av fel

- En eller flera av dina nedladdningsklienter svarar inte på förfrågningar från Lidarr. Därför har Lidarr beslutat att tillfälligt sluta fråga nedladdningsklienten på sin normala 1-minuterscykel, som normalt används för att spåra aktiva nedladdningar och importera färdiga. Lidarr kommer dock att fortsätta försöka skicka nedladdningar till klienten, men kommer med stor sannolikhet att misslyckas.
- Du bör inspektera `System => Loggar` för att se vad orsaken till felen är.
- Om du inte längre använder denna nedladdningsklient kan du inaktivera den i Lidarr för att förhindra fel.

#### Aktivera hantering av slutförda nedladdningar

- Lidarr kräver att hantering av slutförda nedladdningar är aktiverat för att kunna importera filer som har laddats ner av nedladdningsklienten. Det rekommenderas att du aktiverar hantering av slutförda nedladdningar. (Hantering av slutförda nedladdningar är aktiverat som standard för nya användare.)

#### Docker felaktig fjärrsökvägsmappning

- Detta fel är vanligtvis associerat med felaktiga Docker-sökvägar antingen i din nedladdningsklient eller Lidarr

- Ett exempel på felaktiga (inkonsekventa) sökvägar skulle vara:
  - Nedladdningsklient: `/mnt/user/downloads:/downloads`
  - Lidarr:   `/mnt/user/downloads:/data`
- I detta exempel placerar nedladdningsklienten sina nedladdningar i `/downloads` och meddelar Lidarr när det är klart att den färdiga boken finns i `/downloads`. Lidarr kommer sedan och säger "Okej, bra, låt mig kolla i `/downloads`." När Lidarr kommer dit har du inte allokerat en `/downloads`-sökväg, du har allokerat en `/data`-sökväg, så det här felet uppstår.
- Det enklaste sättet att åtgärda detta är KONSEKVENS - om du använder en metod i din nedladdningsklient, använd den över hela linjen.

- Team Lidarr föredrar helt enkelt att använda /data.

  - Nedladdningsklient: `/mnt/user/data/downloads:/data/downloads`
  - Lidarr: `/mnt/user/data:/data`

- Nu kan du i nedladdningsklienten ange var i `/data` du vill placera dina nedladdningar, detta varierar beroende på klienten men du bör kunna tala om för den "Ja, nedladdningsklient, placera mina filer i `/data/downloads/movies`" och eftersom du använde `/data` i Lidarr när nedladdningsklienten meddelar Lidarr att den är klar kommer Lidarr att säga "Bra, jag har en `/data` och jag kan också se `/data/downloads/movies`, allt är rätt i världen."
- Det finns många bra skrivna guider: vår wiki [Docker Guide](/docker-guide) och TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Dessa guider lägger stor vikt vid hardlinks och atomic moves, men själva konceptet med containrar och hur sökvägsmappning fungerar är kärnan i dessa diskussioner.
- Om du korsar operativsystem eller använder nativ och Docker behöver du en fjärrsökvägsmappning. Se [TRaSH's Remote Path Guide för Radarr](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) och [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/) för mer information.

#### Laddar ner till rotmapp

{#downloads-in-root-folder}

- Inom applikationen definieras en rotmapp som den konfigurerade mediebiblioteksmappen. Detta är inte rotmappen för en montering. Din nedladdningsklient laddar ner ofullständiga eller slutförda nedladdningar (eller flyttar slutförda nedladdningar) till din rot (biblioteks) mapp.
- Detta orsakar ofta problem - inklusive dataförlust - och bör inte göras. För att åtgärda detta, ändra din nedladdningsklient så att den inte placerar nedladdningar inom din rotmapp. Observera att 'placering' även inkluderar om din nedladdningsklients kategori är inställd på din rotmapp eller om NZBGet/SABnzbd har sorteringsfunktionen aktiverad och sorterar till din rotmapp.
- Observera att denna kontroll tittar på alla definierade/konfigurerade rotmappar som har lagts till, inte bara rotmappar som för närvarande används. Med andra ord bör inte mappen där din nedladdningsklient laddar ner eller flyttar slutförda nedladdningar till vara samma mapp som du har konfigurerat som din rot/biblioteks/slutliga destinationsmapp för media i *arr-applikationen.
- Konfigurerade rotmappar (även kallade biblioteksmappar) finns i [Inställningar => Mediehantering => Rotmappar](/lidarr/settings/#root-folders)
- Ett exempel är om dina nedladdningar går till `\data\downloads` och du har en rotmapp som är inställd på `\data\downloads`.
- Det rekommenderas att använda sökvägar som `\data\media\` för din rotmapp/bibliotek och `\data\downloads\` för dina nedladdningar.
- Granska vår [Docker Guide](/docker-guide) och TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) för mer information om korrekt och optimal sökvägskonfiguration. Observera att koncepten gäller både Docker och icke-Docker

> Din nedladdningsmapp där din nedladdningsklient placerar nedladdningarna och din rot/biblioteksmapp MÅSTE vara separata. \*Arr kommer att importera filen/filerna från din nedladdningsklients mapp till ditt bibliotek. Nedladdningsklienten bör inte flytta eller ladda ner något till ditt bibliotek.
{.is-warning}

#### Felaktiga inställningar för nedladdningsklient

- Platsen där din nedladdningsklient laddar ner filer orsakar problem. Kontrollera loggarna för mer information. Detta kan bero på behörigheter eller försök att gå från Windows till Linux eller Linux till Windows utan fjärrsökvägsmappning.

#### Felaktig fjärrsökvägsmappning

- Platsen där din nedladdningsklient laddar ner filer orsakar problem. Kontrollera loggarna för mer information. Detta kan bero på behörigheter eller försök att gå från Windows till Linux eller Linux till Windows utan fjärrsökvägsmappning. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) för mer information.

#### Behörighetsfel

- Lidarr (eller användaren som Lidarr körs som) kan inte komma åt platsen där din nedladdningsklient laddar ner filer. Detta beror vanligtvis på ett behörighetsproblem.

#### Fjärrfilen togs bort under bearbetning

- En fil som är tillgänglig via en fjärrsökvägsmappning verkar ha tagits bort innan bearbetningen var klar.

#### Fjärrsökväg används och importen misslyckades

- Kontrollera loggarna för mer information. Se våra [Felsökningsguider](/lidarr/troubleshooting).

### Hantering av slutförda/misslyckade nedladdningar

#### Hantering av slutförda nedladdningar är inaktiverad

- Lidarr kräver att `Hantering av slutförda nedladdningar` är aktiverad för att kunna importera filer som har laddats ner av nedladdningsklienten. Det rekommenderas att du aktiverar `Hantering av slutförda nedladdningar`. (Det är aktiverat som standard för nya användare.)

### Indexerare

#### Inga indexerare är tillgängliga med aktiverad automatisk sökning, Lidarr kommer inte att ge några automatiska sökresultat

- Helt enkelt sagt har du inte några indexerare inställda för att tillåta automatiska sökningar
- Gå till `Inställningar => Indexerare`, välj en indexerare du vill tillåta automatiska sökningar och klicka sedan på Spara.

#### Inga indexerare är tillgängliga med aktiverad RSS-synkronisering, Lidarr kommer inte att hämta nya utgåvor automatiskt

- Lidarr använder RSS-flödet för att hämta nya utgåvor allt eftersom de kommer. Mer information om detta finns här
- För att åtgärda detta problem går du till `Inställningar => Indexerare`, väljer en indexerare du har och aktiverar RSS-synkronisering

#### Inga indexerare är aktiverade

- Lidarr kräver indexerare för att kunna upptäcka nya utgåvor. Läs wikin för instruktioner om hur du lägger till indexerare.

### Aktiverade indexerare stöder inte sökning

- Ingen av de indexerare du har aktiverat stöder sökning. Det innebär att Lidarr endast kommer att kunna hitta nya utgåvor via RSS-flödena. Men att söka efter filmer (antingen automatisk sökning eller manuell sökning) kommer aldrig att ge några resultat. Det enda sättet att åtgärda detta är att lägga till en annan indexerare.

#### Inga indexerare är tillgängliga med aktiverad interaktiv sökning

- Ingen av de indexerare du har aktiverat stöder interaktiv sökning. Det innebär att programmet endast kommer att kunna hitta nya utgåvor via RSS-flödena eller en automatisk sökning.

#### Indexerare är otillgängliga på grund av fel

- Fel inträffar när Lidarr försökte använda en av dina indexerare. För att begränsa försöken kommer Lidarr inte att använda indexeraren under en ökande tid (upp till 24 timmar).
- Detta mekanism utlöses om Lidarr inte kunde få ett svar från indexeraren (kan bero på DNS, proxy/VPN-anslutning, autentisering eller indexerarproblem) eller inte kunde hämta nzb/torrent-filen från indexeraren.
- Granska loggarna för att avgöra vilken typ av fel som orsakar problemet.
- Du kan förhindra varningen genom att inaktivera den berörda indexeraren.
- Kör testet på indexeraren för att tvinga Lidarr att kontrollera indexeraren igen, observera att varningen om hälsokontrollen inte alltid försvinner omedelbart.

#### Jackett används för alla slutpunkter

- Jackett `/all`-slutpunkten är bekväm, men det är dess enda fördel. Allt annat är potentiella problem, så det krävs nu att varje spårare läggs till individuellt.
- [Även Jacketts utvecklare säger att det bör undvikas och inte användas.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Att använda `/all`-slutpunkten har inga fördelar, bara nackdelar:
  - du förlorar kontrollen över inställningar för specifika indexerare (kategorier, söklägen, etc.)
  - att blanda söklägen (IMDB, fråga, etc.) kan ge lågkvalitativa resultat
  - indexerarspecifika kategorier (>= 100000) kan inte användas.
  - långsamma indexerare kommer att sakta ner det totala resultatet
  - totala resultat är begränsade till 1000
  - om en av spårarna returnerar ett fel kommer \*Arr att inaktivera den och nu får du inga resultat.

##### Lösningar

- Lägg till varje spårare i Jackett manuellt som en indexerare i \*Arr
- Kolla in [Prowlarr](/prowlarr) som kan synkronisera indexerare till \*Arr och från Lidarr/Radarr/Readarr-utvecklingsteamet.
- Kolla in [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisera indexerare till \*Arr. Använd inte deras enskilda samlade slutpunkt och använd `multi` om synkronisering kommer att användas.

### Artistmappar

#### Saknad rotmapp

- Detta fel identifieras vanligtvis om en artist letar efter en rotmapp men den rotmappen är inte längre tillgänglig.
- Detta fel kan också uppstå om en lista fortfarande är kopplad till en rotmapp men den rotmappen inte längre är tillgänglig.
- Om du vill ta bort denna varning kan du helt enkelt hitta albumet som fortfarande använder den gamla rotmappen och redigera det till rätt rotmapp.

- Det enklaste sättet att hitta problemartisten är att:

  - Gå till fliken Artist (Bibliotek)
  - Skapa ett anpassat filter med den gamla sökvägen till rotmappen
  - Välj massredigering i den översta menyn och välj den nya rotmappen i rullgardinsmenyn Rotmappar.
  - Därefter får du en popupruta som frågar om du vill flytta artistmapparna till 'rotmapp' ? Detta kommer också att säga Detta kommer också att döpa om artistmappen enligt artistmappens format i inställningarna. Välj helt enkelt Nej om du inte vill att Lidarr ska flytta dina filer
  - Kör hälsokontrolluppgiften i System => Uppgifter

### Diskutrymme

- Den