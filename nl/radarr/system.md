---
title: Radarr Systeem
description: 
published: true
date: 2022-10-19T22:59:06.531Z
tags: radarr, needs-love
editor: markdown
dateCreated: 2021-05-25T02:28:35.194Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Status](#status)
  - [Gezondheid](#gezondheid)
    - [Systeemwaarschuwingen](#systeemwaarschuwingen)
      - [Branch is geen geldige release-branch](#branch-is-geen-geldige-release-branch)
      - [Update naar .NET-versie](#update-naar-net-versie)
        - [Problemen met Docker-installaties oplossen](#problemen-met-docker-installaties-oplossen)
        - [Problemen met FreeBSD-installaties oplossen](#problemen-met-freebsd-installaties-oplossen)
        - [Problemen met zelfstandige installaties oplossen](#problemen-met-zelfstandige-installaties-oplossen)
      - [Huidige geïnstalleerde mono-versie is oud en wordt niet ondersteund](#huidige-geïnstalleerde-mono-versie-is-oud-en-wordt-niet-ondersteund)
      - [Huidige geïnstalleerde SQLite-versie wordt niet ondersteund](#huidige-geïnstalleerde-sqlite-versie-wordt-niet-ondersteund)
      - [Database mislukte integriteitscontrole](#database-mislukte-integriteitscontrole)
      - [Nieuwe update beschikbaar](#nieuwe-update-beschikbaar)
      - [Kan update niet installeren omdat de opstartmap niet beschrijfbaar is door de gebruiker](#kan-update-niet-installeren-omdat-de-opstartmap-niet-beschrijfbaar-is-door-de-gebruiker)
      - [Bijwerken is niet mogelijk om het verwijderen van AppData bij te werken te voorkomen](#bijwerken-is-niet-mogelijk-om-het-verwijderen-van-appdata-bij-te-werken-te-voorkomen)
      - [Branch is voor een vorige versie](#branch-is-voor-een-vorige-versie)
      - [Kan geen verbinding maken met signalR](#kan-geen-verbinding-maken-met-signalr)
        - [Nginx](#nginx)
        - [Apache2](#apache2)
        - [Caddy](#caddy)
      - [Kan het IP-adres voor de geconfigureerde proxyhost niet oplossen](#kan-het-ip-adres-voor-de-geconfigureerde-proxyhost-niet-oplossen)
      - [Proxytest mislukt](#proxytest-mislukt)
      - [Systeemtijd loopt meer dan 1 dag achter](#systeemtijd-loopt-meer-dan-1-dag-achter)
      - [PTP-indexerinstellingen zijn verouderd](#ptp-indexerinstellingen-zijn-verouderd)
      - [Mono- en x86-builds worden beëindigd](#mono-en-x86-builds-worden-beëindigd)
    - [Downloadclients](#downloadclients)
      - [Er is geen downloadclient beschikbaar](#er-is-geen-downloadclient-beschikbaar)
      - [Kan geen verbinding maken met downloadclient](#kan-geen-verbinding-maken-met-downloadclient)
      - [Downloadclients zijn niet beschikbaar vanwege een storing](#downloadclients-zijn-niet-beschikbaar-vanwege-een-storing)
      - [Voltooide downloadverwerking inschakelen](#voltooide-downloadverwerking-inschakelen)
      - [Slechte externe padkoppeling in Docker](#slechte-externe-padkoppeling-in-docker)
      - [Downloaden naar hoofdmap](#downloaden-naar-hoofdmap)
      - [Slechte instellingen voor downloadclient](#slechte-instellingen-voor-downloadclient)
      - [Slechte externe padkoppeling](#slechte-externe-padkoppeling)
      - [Machtigingsfout](#machtigingsfout)
      - [Extern bestand is halverwege het verwerkingsproces verwijderd](#extern-bestand-is-halverwege-het-verwerkingsproces-verwijderd)
      - [Extern pad wordt gebruikt en import is mislukt](#extern-pad-wordt-gebruikt-en-import-is-mislukt)
    - [Voltooide/mislukte downloadverwerking](#voltooide-mislukte-downloadverwerking)
      - [Voltooide downloadverwerking is uitgeschakeld](#voltooide-downloadverwerking-is-uitgeschakeld)
    - [Indexers](#indexers)
      - [Er zijn geen indexers beschikbaar met automatisch zoeken ingeschakeld, Radarr geeft geen automatische zoekresultaten](#er-zijn-geen-indexers-beschikbaar-met-automatisch-zoeken-ingeschakeld-radarr-geeft-geen-automatische-zoekresultaten)
      - [Er zijn geen indexers beschikbaar met RSS-synchronisatie ingeschakeld, Radarr haalt geen nieuwe releases automatisch op](#er-zijn-geen-indexers-beschikbaar-met-rss-synchronisatie-ingeschakeld-radarr-haalt-geen-nieuwe-releases-automatisch-op)
      - [Er zijn geen indexers ingeschakeld](#er-zijn-geen-indexers-ingeschakeld)
    - [Ingeschakelde indexers ondersteunen geen zoeken](#ingeschakelde-indexers-ondersteunen-geen-zoeken)
      - [Er zijn geen indexers beschikbaar met interactief zoeken ingeschakeld](#er-zijn-geen-indexers-beschikbaar-met-interactief-zoeken-ingeschakeld)
      - [Indexers zijn niet beschikbaar vanwege storingen](#indexers-zijn-niet-beschikbaar-vanwege-storingen)
      - [Jackett gebruikt alle eindpunten](#jackett-gebruikt-alle-eindpunten)
        - [Oplossingen](#oplossingen)
    - [Film mappen](#film-mappen)
      - [Ontbrekende hoofdmap](#ontbrekende-hoofdmap)
    - [Films](#films)
      - [Film is verwijderd uit TMDb](#film-is-verwijderd-uit-tmdb)
      - [Lijsten zijn niet beschikbaar vanwege storingen](#lijsten-zijn-niet-beschikbaar-vanwege-storingen)
    - [Meldingen](#meldingen)
    - [Discord als Slack-melding](#discord-als-slack-melding)
  - [Schijfruimte](#schijfruimte)
  - [Over](#over)
  - [Meer informatie](#meer-informatie)
- [Taken](#taken)
  - [Gepland](#gepland)
  - [Wachtrij](#wachtrij)
- [Back-up](#back-up)
- [Updates](#updates)
- [Gebeurtenissen](#gebeurtenissen)
- [Logbestanden](#logbestanden)

# Status

## Gezondheid

- Deze pagina bevat een lijst met fouten bij gezondheidscontroles. Deze gezondheidscontroles worden periodiek uitgevoerd door Radarr en bij bepaalde gebeurtenissen. De resulterende waarschuwingen en fouten worden hier vermeld om advies te geven over hoe ze op te lossen.

### Systeemwaarschuwingen

#### Branch is geen geldige release-branch

- De branch die je hebt ingesteld is geen geldige release-branch. Je ontvangt geen updates. Verander dit naar een van de [huidige release-branches](/radarr/faq#hoe-werk-ik-radarr-bij).

#### Update naar .NET-versie

{#update-to-net-core-version}

- Nieuwere versies van Radarr zijn gericht op .NET6 of nieuwer. Mono-builds worden niet meer geleverd of ondersteund vanaf v4. v3.2.2 is de laatste versie van Radarr die legacy mono-builds ondersteunt. Je gebruikt een van deze legacy mono-builds, maar je platform ondersteunt .NET.

Zie de onderstaande items voor hoe je kunt overschakelen van niet-ondersteunde, verouderde mono-versies naar dotnet.

- [Problemen met Docker-installaties oplossen](#problemen-met-docker-installaties-oplossen)
- [Problemen met FreeBSD-installaties oplossen](#problemen-met-freebsd-installaties-oplossen)
- [Problemen met zelfstandige installaties oplossen](#problemen-met-zelfstandige-installaties-oplossen)
{.links-list}

##### Problemen met Docker-installaties oplossen

- Zorg ervoor dat je branch correct is voor je Docker-beheerder en trek je container opnieuw.

##### Problemen met FreeBSD-installaties oplossen

- Werk eenvoudigweg de Radarr-poort bij met `pkg update && pkg upgrade`
- (Optioneel) Verwijder het mono-pakket als je dat wilt

##### Problemen met zelfstandige installaties oplossen

Fouten zoals:

```none
Kan de assembly '/opt/Radarr/Radarr' niet openen: het bestand bevat geen geldige CIL-afbeelding
```

- Maak een back-up van je bestaande configuratie voordat je de volgende stap uitvoert.
- Dit zou alleen moeten gebeuren op Linux-hosts. Installeer geen .NET-runtime of -SDK van Microsoft.
- Om dit te verhelpen, download je de juiste build voor je architectuur en vervang je je bestaande binaries (toepassing)
- Kort gezegd moet je je bestaande binaries (inhoud of map van /opt/Radarr) verwijderen en vervangen door de inhoud van de zojuist gedownloade .tar.gz en vervolgens je servicebestand bijwerken om geen mono te gebruiken.

> PAK DE DOWNLOAD NIET GEWOON UIT OVER JE BESTAANDE BINARIES.
> JE MOET EERST DE OUDE VERWIJDEREN.
{.is-warning}

- Hieronder staat een door de community ontwikkeld script om je mono-installatie te verwijderen en te vervangen door de .NET-installatie. Bijdragen en correcties zijn welkom.
- Dit gaat ervan uit dat je op de `master` Radarr-branch zit, dus update de variabele indien nodig
- Dit gaat ervan uit dat Radarr wordt uitgevoerd als de gebruiker `radarr`, dus update de variabelen indien nodig
- Dit gaat ervan uit dat Radarr is geïnstalleerd in `/opt/Radarr`, dus update de variabelen indien nodig

```bash
#!/bin/bash
## Gebruikersvariabelen
installdir="/opt/Radarr"
APPUSER="radarr"
branch="master"
## /Gebruikersvariabelen
app="radarr"
ARCH=$(dpkg --print-architecture)
# Stop \*arr
sudo systemctl stop $app
# krijg arch
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "Arch wordt niet ondersteund"
    exit 1
    ;;
esac
echo "Downloaden..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Installatiebestanden gedownload en uitgepakt"
echo "Bestaande installatie verplaatsen"
sudo mv "$installdir/" "$installdir.old/"
echo "Installeren..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "App geïnstalleerd"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### Huidige geïnstalleerde mono-versie is oud en wordt niet ondersteund

- Radarr is geschreven in .NET en vereist Mono om te draaien op zeer oude ARM-processors. Mono 5.20 is het absolute minimum voor Radarr.
- De upgradeprocedure voor Mono verschilt per platform.

> Mono wordt niet langer ondersteund vanaf Radarr versie 4.0
{.is-warning}

#### Huidige geïnstalleerde SQLite-versie wordt niet ondersteund

- Radarr slaat zijn gegevens op in een SQLite-database. De geïnstalleerde SQLite3-bibliotheek op je systeem is te oud. Radarr vereist minimaal versie 3.9.0.

> Merk op dat Radarr `libSQLite3.so` gebruikt, die al dan niet is opgenomen in een SQLite3-upgradepakket.
{.is-info}

#### Database mislukte integriteitscontrole

- Je database(s) zijn niet geslaagd voor een [SQLite Pragma Integrity Check](https://www.sqlite.org/pragma.html#pragma_integrity_check) en bevatten enige corruptie.
- Als `Radarr.db` corrupt is, [raadpleeg dan deze FAQ-entry](/radarr/faq#ik-krijg-een-foutmelding-database-disk-image-is-malformed)
- Als `logs.db` corrupt is: Stop Radarr, verwijder `logs.db` en eventuele `logs.wal`-bestanden.
- Als beide corrupt zijn, bekijk dan de respectieve processen hierboven.

#### Nieuwe update beschikbaar

- Verheug je, de ontwikkelaars hebben een nieuwe update uitgebracht. Dit betekent meestal geweldige nieuwe functies en opgeloste bugs (toch?). Blijkbaar heb je automatische updates niet ingeschakeld, dus je moet zelf uitzoeken hoe je moet updaten op je platform. Het indrukken van de knop Installeren op de pagina Systeem => Updates is waarschijnlijk een goed startpunt.

> Deze waarschuwing verschijnt niet als je huidige versie minder dan 14 dagen oud is
{.is-info}

#### Kan update niet installeren omdat de opstartmap niet beschrijfbaar is door de gebruiker

- Dit betekent dat Radarr zichzelf niet kan updaten. Je moet Radarr handmatig bijwerken of de machtigingen op de opstartmap van Radarr (de installatiemap) instellen om Radarr in staat te stellen zichzelf bij te werken.

#### Bijwerken is niet mogelijk om het verwijderen van AppData bij te werken te voorkomen

- Radarr heeft gedetecteerd dat de AppData-map voor je besturingssysteem zich bevindt in de map die de Radarr-binaries bevat. Normaal gesproken zou dit C:\ProgramData zijn voor Windows en ~/.config voor Linux.

- Kijk naar Systeem => Info om de huidige AppData- en opstartmappen te zien.
- Dit betekent dat Radarr zichzelf niet kan bijwerken zonder het risico van gegevensverlies.
- Als je Linux gebruikt, moet je waarschijnlijk de home-directory voor de gebruiker die Radarr uitvoert wijzigen en de huidige inhoud van de ~/.config/Radarr-map kopiëren om je database te behouden.

#### Branch is voor een vorige versie

- De update-branch die is ingesteld in Instellingen/Algemeen is voor een vorige versie van Radarr, daarom zal de instantie geen juiste update-informatie zien in de Systeem/Updates-feed en mogelijk geen nieuwe updates ontvangen wanneer deze worden uitgebracht.

#### Kan geen verbinding maken met signalR

- signalR zorgt voor dynamische updates van de gebruikersinterface, dus als je browser geen verbinding kan maken met signalR op je server, zie je geen realtime updates in de gebruikersinterface.
- De meest voorkomende oorzaak hiervan is het gebruik van een omgekeerde proxy of Cloudflare.
- Cloudflare heeft websockets ingeschakeld nodig.

##### Nginx

- Nginx vereist de volgende toevoeging aan het locatieblok voor de app:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Zorg ervoor dat je niet proxy_set_header Connection "Upgrade"; opneemt zoals voorgesteld door de nginx-documentatie. DIT WERKT NIET
> Zie <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache2

Voor een omgekeerde proxy van Apache2 moet je de volgende modules inschakelen: proxy, proxy_http en proxy_wstunnel. Voeg vervolgens deze websocket-tunnelinstructie toe aan je vhost-configuratie:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:7878/$1 [P,L]
```

Als je een omgekeerde proxy onder een submap hebt, moet de RewriteRule je basispad bevatten, bijvoorbeeld:

```none
RewriteRule /radarr/(.*) ws://127.0.0.1:7878/radarr/$1 [P,L]
```

Als Radarr niet op dezelfde machine als je omgekeerde proxy wordt uitgevoerd, vervang je 127.0.0.1 door het juiste IP-adres/DNS-naam van je Radarr-app.

##### Caddy

Voor Caddy (V1) gebruik je het volgende:
Opmerking: je moet ook de websocket-instructie toevoegen aan je Radarr-configuratie

```none
 proxy /radarr 127.0.0.1:7878 {
     websocket
     transparent
 }
```

#### Kan het IP-adres voor de geconfigureerde proxyhost niet oplossen

- Controleer je proxy-instellingen en zorg ervoor dat ze correct zijn
- Zorg ervoor dat je proxy actief, draaiend en toegankelijk is

#### Proxytest mislukt

- Je geconfigureerde proxy is niet geslaagd voor de test. Bekijk de verstrekte HTTP-fout en/of controleer de logboeken voor meer details.

#### Systeemtijd loopt meer dan 1 dag achter

- De systeemtijd loopt meer dan 1 dag achter. Geplande taken kunnen mogelijk niet correct worden uitgevoerd totdat de tijd is gecorrigeerd.
- Controleer je systeemtijd en zorg ervoor dat deze is gesynchroniseerd met een betrouwbare tijdserver en nauwkeurig is.

#### PTP-indexerinstellingen zijn verouderd

- De volgende PassThePopcorn-indexers hebben verouderde instellingen en moeten worden bijgewerkt.

#### Mono- en x86-builds worden beëindigd

- Mono- en x86-builds worden niet langer ondersteund vanaf v4. Als je deze foutmelding krijgt, gebruik je de mono-versie van de toepassing of de x86-versie. Helaas zullen wegens de toenemende moeilijkheid bij de ontwikkelingsondersteuning voor deze verouderde versies hun ondersteuning en daarmee ook de releases ervan worden stopgezet. Daarom wordt aangeraden om over te stappen naar een ondersteund besturingssysteem dat geen x86 of mono vereist. Je kunt ook overwegen om Docker te gebruiken voor je behoeften.

### Downloadclients

#### Er is geen downloadclient beschikbaar

- Een correct geconfigureerde en ingeschakelde downloadclient is vereist voor Radarr om media te kunnen downloaden. Aangezien Radarr verschillende downloadclients ondersteunt, moet je bepalen welke het beste aansluit bij je eisen. Als je al een downloadclient hebt geïnstalleerd, moet je Radarr configureren om deze te gebruiken en een categorie aan te maken. Zie Instellingen => Downloadclient.

#### Kan geen verbinding maken met downloadclient

- Radarr kon geen verbinding maken met de geconfigureerde downloadclient. Controleer of de downloadclient operationeel is en controleer de URL. Dit kan ook duiden op een verificatiefout.
- Dit wordt meestal veroorzaakt door een verkeerd geconfigureerde downloadclient. Dingen die je meestal kunt controleren:
  - Het IP-adres van je downloadclient als deze op dezelfde fysieke machine staat, is meestal 127.0.0.1
  - Het poortnummer dat je downloadclient gebruikt, deze is ingevuld met het standaard poortnummer, maar als je dit hebt gewijzigd, moet je hetzelfde nummer invoeren in Radarr.
  - Zorg ervoor dat SSL-versleuteling niet is ingeschakeld als je zowel je Radarr-instantie als je downloadclient op een lokaal netwerk gebruikt. Zie de SSL-FAQ voor meer informatie.
  - Zorg ervoor dat IPv6 is uitgeschakeld op het systeem als het niet functioneel is.
  - Zorg ervoor dat een DNS-server (bijv. pihole) geen querylimiet heeft

#### Downloadclients zijn niet beschikbaar vanwege een storing

- Een of meer van je downloadclients reageert niet op verzoeken van Radarr. Daarom heeft Radarr besloten om tijdelijk te stoppen met het bevragen van de downloadclient op de normale cyclus van 1 minuut, die normaal gesproken wordt gebruikt om actieve downloads bij te houden en voltooide downloads te importeren. Radarr zal echter blijven proberen om downloads naar de client te sturen, maar zal hoogstwaarschijnlijk falen.
- Je moet System=>Logs controleren om de reden voor de fouten te zien.
- Als je deze downloadclient niet meer gebruikt, schakel deze dan uit in Radarr om de fouten te voorkomen.

#### Voltooide downloadverwerking inschakelen

- Radarr vereist voltooide downloadverwerking om bestanden te kunnen importeren die zijn gedownload door de downloadclient. Het wordt aanbevolen om voltooide downloadverwerking in te schakelen. (Voltooide downloadverwerking is standaard ingeschakeld voor nieuwe gebruikers.)

#### Slechte externe padkoppeling in Docker

- Deze fout wordt meestal geassocieerd met slechte Docker-paden binnen je downloadclient of Radarr.

- Een voorbeeld hiervan is:
  - Downloadclient: Downloadpad: /mnt/user/downloads:/downloads
  - Radarr: Downloadpad: /mnt/user/downloads:/data
- In dit voorbeeld plaatst de downloadclient zijn downloads in /downloads en vertelt het Radarr wanneer het klaar is dat de voltooide film zich in /downloads bevindt. Radarr komt dan langs en zegt "Oké, cool, laat me in /downloads kijken" Nou, binnen Radarr heb je geen /downloads-pad toegewezen, maar je hebt een /data-pad toegewezen, dus gooit het deze foutmelding.
- De gemakkelijkste oplossing hiervoor is CONSISTENTIE: als je één schema gebruikt in je downloadclient, gebruik het dan overal.

- Team Radarr is een groot voorstander van het eenvoudigweg gebruiken van /data.
  - Downloadclient: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Nu kun je binnen de downloadclient aangeven waar je je downloads wilt plaatsen, bijvoorbeeld /data/torrents (of usenet)/movies en omdat je /data in Radarr hebt gebruikt, wanneer de downloadclient aan Radarr vertelt dat deze klaar is, zal Radarr langskomen en zeggen "Geweldig, ik heb een /data en ik kan ook /torrents (of usenet)/movies zien, alles is in orde in de wereld."
- Er zijn veel goede handleidingen: onze wiki [Docker-gids](/docker-guide) en TRaSH's [Hardlinks en Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Deze handleidingen leggen sterk de nadruk op Hardlinks en Atomic moves, maar het algemene concept van containers en hoe het padkoppeling werkt, is de kern van deze discussies.

- Zie [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) voor meer informatie.

#### Downloaden naar hoofdmap

{#downloads-in-root-folder}

- In de toepassing wordt een hoofdmap gedefinieerd als de geconfigureerde mediabibliotheekmap. Dit is niet de hoofdmap van een koppeling. Je downloadclient heeft een onvolledige of voltooide (of verplaatst voltooide downloads) naar je hoofd (bibliotheek)map.
- Dit veroorzaakt vaak problemen, inclusief gegevensverlies, en mag niet worden gedaan. Om dit op te lossen, wijzig je downloadclient zodat deze geen downloads plaatst binnen je hoofdmap. Let op dat 'plaatsen' ook betekent dat als de categorie van je downloadclient is ingesteld op je hoofdmap of als NZBGet/SABnzbd sorteren ingeschakeld heeft en sorteert naar je hoofdmap.
- Houd er rekening mee dat deze controle kijkt naar alle gedefinieerde/geconfigureerde hoofdmappen die zijn toegevoegd, niet alleen de momenteel gebruikte hoofdmappen. Met andere woorden, de map waarin je downloadclient downloads plaatst of voltooide downloads naartoe verplaatst, mag niet dezelfde map zijn die je hebt geconfigureerd als je hoofd/bibliotheek/eindbestemmingsmap voor media in de *arr-toepassing.
- Geconfigureerde hoofdmappen (ook wel bibliotheekmappen genoemd) vind je in [Instellingen => Mediabeheer => Hoofdmappen](/radarr/settings/#root-folders)
- Een voorbeeld is als je downloads naar `\data\downloads` gaan en je een hoofdmap hebt ingesteld als `\data\downloads`.
- Het wordt aanbevolen om paden zoals `\data\media\` te gebruiken voor je hoofdmap/bibliotheek en `\data\downloads\` voor je downloads.
- Bekijk onze [Docker-gids](/docker-guide) en TRaSH's [Hardlinks en Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) voor meer informatie over de juiste en optimale padconfiguratie. Let op dat de concepten van toepassing zijn op zowel Docker als niet-Docker

> Je downloadmap waar je downloadclient de downloads plaatst en je hoofd/bibliotheekmap MOETEN gescheiden zijn. \*Arr importeert het bestand/de bestanden vanuit de downloadmap van je downloadclient naar je bibliotheek. De downloadclient mag niets verplaatsen of downloaden naar je bibliotheek.
{.is-warning}

#### Slechte instellingen voor downloadclient

- De locatie waar je downloadclient bestanden downloadt, veroorzaakt problemen. Controleer de logboeken voor meer informatie. Dit kan te maken hebben met machtigingen of een poging om van Windows naar Linux of van Linux naar Windows te gaan zonder een externe padkoppeling.

#### Slechte externe padkoppeling

- De locatie waar je downloadclient bestanden downloadt, veroorzaakt problemen. Controleer de logboeken voor meer informatie. Dit kan te maken hebben met machtigingen of een poging om van Windows naar Linux of van Linux naar Windows te gaan zonder een externe padkoppeling. Zie [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) voor meer informatie.

#### Machtigingsfout

- Radarr of de gebruiker radarr waarop het wordt uitgevoerd, kan de locatie waar je downloadclient bestanden downloadt, niet openen. Dit is meestal een machtigingsprobleem.

#### Extern bestand is halverwege het verwerkingsproces verwijderd

- Een bestand dat toegankelijk is via een externe padkoppeling lijkt te zijn verwijderd voordat de verwerking is voltooid.

#### Extern pad wordt gebruikt en import is mislukt

- Controleer je logboeken voor meer informatie; raadpleeg onze probleemoplossingsgidsen

### Voltooide/mislukte downloadverwerking

#### Voltooide downloadverwerking is uitgeschakeld

- (Deze waarschuwing wordt alleen gegenereerd voor bestaande gebruikers vóór de implementatie van de functie Voltooide Downloadverwerking. Deze functie is standaard uitgeschakeld om ervoor te zorgen dat het systeem blijft werken zoals verwacht voor huidige configuraties.)
- Het wordt aanbevolen om Voltooide Downloadverwerking te gebruiken, omdat dit betere compatibiliteit biedt voor de uitpak- en nabewerkingslogica van verschillende downloadclients. Met Voltooide Downloadverwerking importeert Radarr een download pas nadat de downloadclient heeft gemeld dat deze gereed is.
- Als je Voltooide Downloadverwerking wilt inschakelen, moet je het volgende controleren: * Waarschuwing: Voltooide Downloadverwerking werkt alleen correct als de downloadclient en Radarr op dezelfde machine staan, omdat het het pad om te importeren rechtstreeks van de downloadclient krijgt, anders is een externe koppeling nodig.

### Indexers

#### Er zijn geen indexers beschikbaar met automatisch zoeken ingeschakeld, Radarr geeft geen automatische zoekresultaten

- Simpel gezegd heb je geen van je indexers ingesteld om automatisch zoeken toe te staan
- Ga naar Instellingen => Indexers, selecteer een indexer die je automatisch zoeken wilt toestaan en klik vervolgens op Opslaan.

#### Er zijn geen indexers beschikbaar met RSS-synchronisatie ingeschakeld, Radarr haalt geen nieuwe releases automatisch op

- Radarr gebruikt de RSS-feed om nieuwe releases op te pikken terwijl ze binnenkomen. Meer informatie daarover vind je hier
- Om dit probleem op te lossen, ga je naar Instellingen => Indexers, selecteer een indexer die je hebt en schakel RSS-synchronisatie in

#### Er zijn geen indexers ingeschakeld

- Radarr vereist indexers om nieuwe releases te kunnen ontdekken. Lees de wiki voor instructies over het toevoegen van indexers.

#### Ingeschakelde indexers ondersteunen geen zoeken

- Geen van de ingeschakelde indexers ondersteunt zoeken. Dit betekent dat Radarr alleen nieuwe releases kan vinden via de RSS-feeds. Maar zoeken naar films (zowel automatisch zoeken als handmatig zoeken) zal nooit resultaten opleveren. De enige manier om dit te verhelpen, is door een andere indexer toe te voegen.

#### Er zijn geen indexers beschikbaar met interactief zoeken ingeschakeld

- Geen van de ingeschakelde indexers ondersteunt interactief zoeken. Dit betekent dat de toepassing alleen nieuwe releases kan vinden via de RSS-feeds of een automatische zoekopdracht.

#### Indexers zijn niet beschikbaar vanwege storingen

- Er zijn fouten opgetreden terwijl Radarr probeerde een van je indexers te gebruiken. Om het aantal herhalingen te beperken, zal Radarr de indexer gedurende steeds langere tijd niet gebruiken (tot 24 uur).
- Dit mechanisme wordt geactiveerd als Radarr geen reactie van de indexer kon krijgen (dit kan worden veroorzaakt door DNS, proxy/vpn-verbinding, verificatie of een indexerprobleem) of als Radarr het nzb/torrent-bestand niet kon ophalen van de indexer. Raadpleeg de logboeken om te bepalen wat voor soort fout het probleem heeft veroorzaakt.
- Je kunt de waarschuwing voorkomen door de betreffende indexer uit te schakelen.
- Voer de test op de indexer uit om Radarr te dwingen de indexer opnieuw te controleren, houd er rekening mee dat de waarschuwing van de gezondheidscontrole niet altijd onmiddellijk verdwijnt.

#### Jackett gebruikt alle eindpunten

- Het Jackett /all-eindpunt is handig, maar dat is het enige voordeel. Al het andere kan problemen veroorzaken, dus het is nu vereist om elke tracker afzonderlijk toe te voegen.
- [Zelfs de ontwikkelaars van Jackett zeggen dat het moet worden vermeden en niet moet worden gebruikt.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Het gebruik van het /all-eindpunt heeft geen voordelen, alleen nadelen:
  - je verliest de controle over indexer-specifieke instellingen (categorieën, zoekmodi, enz.)
  - het mixen van zoekmodi (IMDB, query, enz.) kan leiden tot resultaten van lage kwaliteit
  - indexer-specifieke categorieën (\>= 100000) kunnen niet worden gebruikt.
  - trage indexers vertragen het algehele resultaat
  - het totale aantal resultaten is beperkt tot 1000
  - als een van de trackers in /all een fout retourneert, schakelt \*Arr deze uit en krijg je nu geen resultaten meer.

##### Oplossingen

- Voeg elke tracker in Jackett handmatig toe als een indexer in \*Arr
- Bekijk [Prowlarr](/prowlarr), dat indexers kan synchroniseren met \*Arr en afkomstig is van het Lidarr/Radarr/Readarr-ontwikkelingsteam.
- Bekijk [NZBHydra2](https://github.com/theotherp/nzbhydra2), dat indexers kan synchroniseren met \*Arr. Gebruik echter niet hun enkele aggregatie-eindpunt en gebruik `multi` als synchronisatie wordt gebruikt.

### Film mappen

#### Ontbrekende hoofdmap

{#movie-collection-missing-root-folder}

- Deze fout wordt meestal geïdentificeerd als een film of collectie is toegewezen aan een hoofdmap, maar die hoofdmap is niet meer beschikbaar.
- Deze fout kan ook optreden als een lijst nog steeds is gericht op een hoofdmap die niet meer beschikbaar is.
- Als je deze waarschuwing wilt verwijderen, zoek dan gewoon de film(s) of collectie(s) die nog steeds de oude hoofdmap gebruiken en bewerk deze naar de juiste hoofdmap.

##### Weergave van de tabel Films

1. Ga naar het tabblad Films (Bibliotheek)
1. Schakel de kolom Pad in voor de tabelweergave en sorteer op pad

##### Aangepaste filter voor films

1. Maak een aangepast filter met het oude pad van de hoofdmap
1. Selecteer massabewerking in de bovenste balk en selecteer in het vervolgkeuzemenu Hoofdpaden het nieuwe hoofdpad waar je wilt dat deze films naartoe worden verplaatst.
1. Vervolgens krijg je een pop-up met de melding "Wil je de filmmappen verplaatsen naar 'hoofdpad'?" Hierin staat ook dat dit de filmaper mapindeling in de instellingen zal hernoemen. Selecteer gewoon Nee als je niet wilt dat Radarr je bestanden verplaatst.
1. Voer de taak Controleer gezondheid uit in Systeem => Taken

#### Aangepaste filter voor collecties

1. Maak een aangepast filter in Collecties met het oude pad van de hoofdmap
1. Selecteer de collecties en selecteer in het vervolgkeuzemenu Hoofdpaden het nieuwe hoofdpad waar je wilt dat de toekomstige films van deze collecties aan worden toegewezen.
1. Voer de taak Controleer gezondheid uit in Systeem => Taken

### Films

#### Film is verwijderd uit TMDb

- De film is gekoppeld aan een TMDb-ID dat is verwijderd uit TMDb, meestal omdat het een duplicaat was, geen film was of om een andere reden van ID is veranderd. Verwijderde films ontvangen geen updates en moeten door de gebruiker worden gecorrigeerd om de functionaliteit te behouden. Verwijder de film uit Radarr zonder de bestanden te verwijderen en probeer deze opnieuw toe te voegen. Als deze niet verschijnt in een zoekopdracht, controleer dan Sonarr, want het kan een tv-miniserie zijn zoals Stephen King's It.

- Je kunt verwijderde films vinden en bewerken door een aangepast filter te maken met de volgende stappen:

  1. Klik op Films in het linkermenu
  1. Klik op het vervolgkeuzemenu Filter en selecteer "Aangepast filter"
  1. Voer een label in, bijvoorbeeld "Verwijderde films"
  1. Maak de filter als volgt: `Release Status` is `Verwijderd`
  1. Klik op Opslaan en selecteer het zojuist gemaakte filter in het vervolgkeuzemenu Filter

#### Lijsten zijn niet beschikbaar vanwege storingen

- Meestal betekent dit gewoon dat Radarr niet langer kan communiceren via API of door in te loggen bij je gekozen lijstprovider. Als het probleem aanhoudt, kun je het beste contact met hen opnemen om ze uit te sluiten, omdat hun systemen soms overbelast kunnen zijn.
- Bekijk Systeem => Gebeurtenissen gefilterd op Waarschuwing (Waarschuwingen en Fouten) om de historische storingen te zien of controleer de logboeken voor details.

### Meldingen

### Discord als Slack-melding

- Je hebt Discord geconfigureerd om een Slack-webhook te gebruiken. Dit wordt niet aanbevolen en de native Discord-functionaliteit moet in plaats daarvan worden gebruikt. Als je deze melding ontvangt, betekent dit waarschijnlijk dat je dit zojuist hebt geconfigureerd door een verouderde handleiding te volgen. Laat de auteur van de handleiding weten dat deze moet worden bijgewerkt.

## Schijfruimte

- In dit gedeelte

## Wachtrij

- De wachtrij laat lopende en aankomende taken zien, evenals een geschiedenis van recent uitgevoerde taken en hoe lang die taken hebben geduurd.

# Back-up

> Als je wilt weten hoe je je Radarr-instantie kunt back-uppen/herstellen, klik dan [hier](/radarr/faq).
{.is-info}

- In het gedeelte Back-up worden eerdere back-ups weergegeven (tenzij je een nieuwe installatie hebt waarbij nog geen back-ups zijn gemaakt).
  
- Nu back-uppen - Met deze optie kun je handmatig een back-up van de database van Radarr maken.
- Back-up herstellen - Hiermee wordt een nieuw scherm geopend om te herstellen vanuit een eerdere back-up.
  - Door Bestand kiezen te selecteren, wordt je browser gevraagd om een dialoogvenster te openen om te herstellen vanuit een Radarr-zipback-up.
  
- Als je eerdere back-ups hebt en ze vanuit Radarr wilt downloaden om ze op een niet-standaardlocatie te plaatsen, kun je eenvoudig een van deze bestanden selecteren om ze te downloaden.
- Aan de rechterkant van elke vorige download heb je twee opties.
  - Herstellen (Klokpictogram) - Om te herstellen vanuit een eerdere back-up - Dit opent een nieuw venster om te bevestigen dat je wilt herstellen vanuit deze back-up.
  - Verwijderen (Prullenbak) - Om een eerdere back-up te verwijderen

# Updates

- Het updatescherm laat de laatste 5 updates zien die zijn uitgevoerd, evenals de huidige versie waarop je zit.
- Op deze pagina worden ook de update-opmerkingen van de ontwikkelaars weergegeven, waarin wordt vermeld wat er is gerepareerd of toegevoegd aan Radarr (Verheug je!)

> Een onderhoudsrelease bevat bugfixes en andere verbeteringen. Bekijk de commitgeschiedenis voor details.
{.is-info}

# Gebeurtenissen

- Het tabblad Gebeurtenissen laat zien wat er gaande is in je Radarr. Dit kan worden gebruikt om enkele kleine problemen te diagnosticeren. Dit vervangt echter niet de Trace Logs die worden besproken in Logging.

> Gebeurtenissen zijn het equivalent van INFO-logs. {.is-info}

- Componenten - Deze kolom geeft aan welke component binnen Radarr is geactiveerd.
- Bericht - Deze kolom geeft aan welk bericht is verzonden door het component uit de vorige kolom.
- Tandwielpictogram - Met deze optie kun je instellen hoeveel componenten/berichten per pagina worden weergegeven (standaard is 50).
- Opties bovenaan de pagina
  - Vernieuwen - Met deze optie wordt de huidige pagina vernieuwd en wordt er een nieuw gebeurtenissenlogboek opgehaald.
  - Wissen - Hiermee wordt het huidige gebeurtenissenlogboek gewist, zodat je opnieuw kunt beginnen.

# Logbestanden

- Op deze pagina kun je de huidige logbestanden van Radarr downloaden en bekijken.

- Op de bovenste rij zijn er verschillende opties waarmee je je logbestanden kunt beheren.

- Op de bovenste rij helemaal links is er een vervolgkeuzemenu waarmee je kunt schakelen tussen Logbestanden en Updater Logbestanden.
  - Logbestanden - Het belangrijkste onderdeel bij elk ondersteuningsprobleem, meer informatie over logbestanden is hier te vinden.
  - Updater Logbestanden - Dit toont de logbestanden die zijn gekoppeld aan het updaterscript van Radarr.

> Als je Docker gebruikt, is dit leeg omdat je zou moeten updaten door een nieuwe Docker-image te downloaden.
{.is-info}

- Vernieuwen - Hiermee wordt de huidige pagina vernieuwd en worden eventuele nieuw gemaakte logbestanden weergegeven.
- Verwijderen - Hiermee worden alle logbestanden gewist, zodat je opnieuw kunt beginnen.
- Bestandsnaam - Hier wordt de bestandsnaam weergegeven die is gekoppeld aan het logbestand.
- Laatst geschreven - Dit is de lokale tijd waarop dit specifieke logbestand is geschreven.
  - Radarr maakt gebruik van rollende logbestanden met een limiet van 1 MB per stuk. Het huidige logbestand is altijd radarr.txt, voor de andere bestanden is radarr.0.txt de op een na nieuwste (hoe hoger het nummer, hoe ouder het is) tot een totaal van 51 logbestanden. Dit logbestand bevat `fatal`, `error`, `warn` en `info` vermeldingen.
  - Wanneer het debug-logniveau is ingeschakeld, zijn er extra radarr.debug.txt rollende logbestanden aanwezig, tot 51 bestanden. Dit logbestand bevat `fatal`, `error`, `warn`, `info` en `debug` vermeldingen. Het beslaat meestal een periode van ~40 uur.
  - Wanneer het trace-logniveau is ingeschakeld, zijn er extra radarr.trace.txt rollende logbestanden aanwezig, tot 51 bestanden. Dit logbestand bevat `fatal`, `error`, `warn`, `info`, `debug` en `trace` vermeldingen. Vanwege de uitgebreide traceerbaarheid beslaat het meestal slechts een paar uur.