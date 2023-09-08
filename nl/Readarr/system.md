# Status

## Gezondheid

- Deze pagina bevat een lijst met fouten bij gezondheidscontroles. Deze gezondheidscontroles worden periodiek uitgevoerd door Readarr en bij bepaalde gebeurtenissen. De resulterende waarschuwingen en fouten worden hier vermeld om advies te geven over hoe ze op te lossen.

### Systeemwaarschuwingen

#### Branch is geen geldige release-branch

- De branch die je hebt ingesteld is geen geldige release-branch. Je ontvangt geen updates. Verander deze naar een van de [huidige release-branches](/readarr/faq#hoe-update-ik-readarr).

#### Huidige geïnstalleerde SQLite-versie wordt niet ondersteund

- Readarr slaat zijn gegevens op in een SQLite-database. De geïnstalleerde SQLite3-bibliotheek op je systeem is te oud. Readarr vereist minimaal versie 3.9.0. Houd er rekening mee dat Readarr `libSQLite3.so` gebruikt, die al dan niet is opgenomen in een SQLite3-upgradepakket.

> Houd er rekening mee dat Readarr `libSQLite3.so` gebruikt, die al dan niet is opgenomen in een SQLite3-upgradepakket.
{.is-info}

#### Nieuwe update beschikbaar

Verheug je, de ontwikkelaars hebben een nieuwe update uitgebracht. Dit betekent over het algemeen geweldige nieuwe functies en opgeloste bugs (toch?). Blijkbaar heb je automatische updates niet ingeschakeld, dus je moet uitzoeken hoe je moet updaten op jouw platform. Het indrukken van de knop Installeren op de pagina Systeem => Updates is waarschijnlijk een goed startpunt.

> Deze waarschuwing verschijnt niet als je huidige versie minder dan 14 dagen oud is
{.is-info}

#### Kan update niet installeren omdat de opstartmap niet beschrijfbaar is door de gebruiker

- Dit betekent dat Readarr zichzelf niet kan updaten. Je moet Readarr handmatig updaten of de machtigingen op de opstartmap van Readarr (de installatiemap) instellen om Readarr in staat te stellen zichzelf bij te werken.

#### Updaten is niet mogelijk om het verwijderen van AppData bij een update te voorkomen

- Readarr heeft gedetecteerd dat de AppData-map voor je besturingssysteem zich bevindt in de map die de Readarr-binaries bevat. Normaal gesproken zou dit C:\ProgramData zijn voor Windows en ~/.config voor Linux.

- Kijk op Systeem => Info om de huidige AppData- en opstartmappen te zien.
- Dit betekent dat Readarr zichzelf niet kan updaten zonder het risico op gegevensverlies.
- Als je Linux gebruikt, moet je waarschijnlijk de home-directory voor de gebruiker die Readarr uitvoert wijzigen en de huidige inhoud van de map ~/.config/Readarr kopiëren om je database te behouden.

#### Branch is voor een vorige versie

- De update-branch die is ingesteld in Instellingen/Algemeen is voor een vorige versie van Readarr, daarom zal de instantie geen juiste update-informatie zien in de feed Systeem/Updates en mogelijk geen nieuwe updates ontvangen wanneer deze worden uitgebracht.

#### Kan geen verbinding maken met signalR

- signalR zorgt voor dynamische updates van de gebruikersinterface, dus als je browser geen verbinding kan maken met signalR op je server, zie je geen realtime updates in de gebruikersinterface.

- De meest voorkomende oorzaak hiervan is het gebruik van een omgekeerde proxy of Cloudflare.
- Cloudflare heeft websockets ingeschakeld nodig.

##### Nginx

- Nginx vereist de volgende toevoeging aan het locatieblok voor de app:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Zorg ervoor dat je niet proxy_set_header Connection "Upgrade"; opneemt zoals gesuggereerd door de nginx-documentatie. DIT WERKT NIET
> Zie <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

Voor Apache2 reverse proxy moet je de volgende modules inschakelen: proxy, proxy_http en proxy_wstunnel. Voeg vervolgens deze websocket-tunnelinstructie toe aan je vhost-configuratie:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8787/$1 [P,L]
```

Voor Caddy (V1) gebruik je dit:
Opmerking: je moet ook de websocket-instructie toevoegen aan je Readarr-configuratie

```none
 proxy /readarr 127.0.0.1:8787 {
     websocket
     transparent
 }
```

#### Kan het IP-adres voor de geconfigureerde proxyhost niet oplossen

- Controleer je proxy-instellingen en zorg ervoor dat ze juist zijn
- Zorg ervoor dat je proxy actief, actief en toegankelijk is

#### Proxytest mislukt

- Je geconfigureerde proxy is niet succesvol getest, controleer de verstrekte HTTP-fout en/of controleer de logs voor meer details.

#### Systeemtijd loopt meer dan 1 dag achter

- De systeemtijd loopt meer dan 1 dag achter. Geplande taken kunnen mogelijk niet correct worden uitgevoerd totdat de tijd is gecorrigeerd.
- Controleer je systeemtijd en zorg ervoor dat deze is gesynchroniseerd met een betrouwbare tijdserver en nauwkeurig is.

### Downloadclients

#### Geen downloadclient beschikbaar

- Een correct geconfigureerde en ingeschakelde downloadclient is vereist voor Readarr om media te kunnen downloaden. Aangezien Readarr verschillende downloadclients ondersteunt, moet je bepalen welke het beste bij je eisen past. Als je al een downloadclient hebt geïnstalleerd, moet je Readarr configureren om deze te gebruiken en een categorie aan te maken. Zie Instellingen => Downloadclient.

#### Kan niet communiceren met downloadclient

- Readarr kon niet communiceren met de geconfigureerde downloadclient. Controleer of de downloadclient operationeel is en controleer de URL. Dit kan ook duiden op een verificatiefout.
- Dit komt meestal door een verkeerd geconfigureerde downloadclient. Dingen die je meestal kunt controleren:
- Het IP-adres van je downloadclient, als deze op dezelfde fysieke machine staat, is dit meestal 127.0.0.1
- Het poortnummer dat je downloadclient gebruikt, deze zijn ingevuld met het standaard poortnummer, maar als je dit hebt gewijzigd, moet je hetzelfde nummer invoeren in Readarr.
- Zorg ervoor dat SSL-versleuteling niet is ingeschakeld als je zowel je Readarr-instantie als je downloadclient op een lokaal netwerk gebruikt. Zie de SSL-FAQ voor meer informatie.

#### Downloadclients zijn niet beschikbaar vanwege fouten

{#download-clients-zijn-niet-beschikbaar-vanwege-fouten}

- Een of meer van je downloadclients reageert niet op verzoeken van Readarr. Daarom heeft Readarr besloten om tijdelijk te stoppen met het bevragen van de downloadclient op de normale cyclus van 1 minuut, die normaal gesproken wordt gebruikt om actieve downloads bij te houden en voltooide downloads te importeren. Readarr zal echter blijven proberen om downloads naar de client te sturen, maar zal waarschijnlijk falen.
- Je moet Systeem => Logs inspecteren om te zien wat de reden is voor de fouten.
- Als je deze downloadclient niet meer gebruikt, schakel deze dan uit in Readarr om de fouten te voorkomen.

#### Voltooide downloadverwerking inschakelen

- Readarr vereist dat Voltooide downloadverwerking is ingeschakeld om bestanden te kunnen importeren die zijn gedownload door de downloadclient. Het wordt aanbevolen om Voltooide downloadverwerking in te schakelen.
- (Voltooide downloadverwerking is standaard ingeschakeld voor nieuwe gebruikers.)

#### Docker verkeerde externe padtoewijzing

- Deze fout wordt meestal geassocieerd met verkeerde Docker-paden binnen je downloadclient of Readarr.

- Een voorbeeld hiervan is:
  - Downloadclient: Downloadpad: /mnt/user/downloads:/downloads
  - Readarr: Downloadpad: /mnt/user/downloads:/data
- In dit voorbeeld plaatst de downloadclient zijn downloads in /downloads en vertelt Readarr wanneer het klaar is dat het voltooide boek zich in /downloads bevindt. Readarr komt dan langs en zegt "Oké, cool, laat me eens kijken in /downloads" Welnu, binnen Readarr heb je geen /downloads-pad toegewezen, je hebt een /data-pad toegewezen, dus gooit het deze fout.
- De gemakkelijkste oplossing hiervoor is CONSISTENTIE. Als je één schema gebruikt in je downloadclient, gebruik het dan overal.

- Team Readarr is een groot voorstander van het eenvoudigweg gebruiken van /data.
  - Downloadclient: /mnt/user/data/downloads:/data/downloads
  - Readarr: /mnt/user/data:/data

- Nu kun je binnen de downloadclient aangeven waar je je downloads in /data wilt plaatsen. Dit varieert afhankelijk van de client, maar je zou het moeten kunnen vertellen "Ja, downloadclient, plaats mijn bestanden in." /data/torrents (of usenet)/books en omdat je /data hebt gebruikt in Readarr, wanneer de downloadclient Readarr vertelt dat het klaar is, zal Readarr langskomen en zeggen "Geweldig, ik heb een /data en ik kan ook /torrents (of usenet)/books zien, alles is in orde in de wereld."
- Er zijn veel goede handleidingen: onze wiki [Docker-gids](/docker-guide) en TRaSH's [Hardlinks en Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Deze handleidingen leggen veel nadruk op Hardlinks en Atomic moves, maar het algemene concept van containers en hoe padtoewijzing werkt, is de kern van deze discussies.

- Als je besturingssystemen of native en Docker overschrijdt, heb je een externe padtoewijzing nodig. Zie [TRaSH's Remote Path Guide voor Radarr, maar het concept is hetzelfde voor alle \*Arrs](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) voor meer informatie.

- Als je deze fout krijgt met Calibre, kan Redarr geen toegang krijgen tot de Calibre-bibliotheek. De oplossing is hetzelfde: corrigeer de inconsistente koppelingen voor je containers. Maak anders een externe padtoewijzing om het pad van de Calibre-bibliotheek te koppelen aan het toegankelijke pad van Readarr. Een externe padtoewijzing is alleen nodig als je besturingssystemen of servers overschrijdt. Als alles in Docker staat, is het beter om je koppelingen te corrigeren.

#### Downloaden naar de rootmap

{#downloads-in-root-folder}

- Binnen de applicatie wordt een rootmap gedefinieerd als de geconfigureerde mediabibliotheekmap. Dit is niet de rootmap van een mount. Je downloadclient plaatst een onvolledige of voltooide download (of verplaatst voltooide downloads) naar je root (bibliotheek) map.
- Dit veroorzaakt vaak problemen - inclusief gegevensverlies - en mag niet worden gedaan. Om dit op te lossen, wijzig je downloadclient zodat deze geen downloads plaatst binnen je rootmap. Let op dat 'plaatsen' ook betekent dat je downloadclient-categorie is ingesteld op je rootmap of dat NZBGet/SABnzbd sorteren ingeschakeld heeft en sorteert naar je rootmap.
- Houd er rekening mee dat deze controle kijkt naar alle gedefinieerde/geconfigureerde rootmappen, niet alleen naar de momenteel gebruikte rootmappen. Met andere woorden, de map waarin je downloadclient downloads plaatst of voltooide downloads naartoe verplaatst, mag niet dezelfde map zijn die je hebt geconfigureerd als je root/bibliotheek/eindbestemmingsmap voor media in de *arr-toepassing.
- Geconfigureerde rootmappen (ook wel bibliotheekmappen genoemd) vind je in [Instellingen => Mediabeheer => Rootmappen](/readarr/settings/#root-folders)
- Een voorbeeld is als je downloads naar `\data\downloads` gaan en je een rootmap hebt ingesteld als `\data\downloads`.
- Het wordt aanbevolen om paden zoals `\data\media\` te gebruiken voor je rootmap/bibliotheek en `\data\downloads\` voor je downloads.
- Bekijk onze [Docker-gids](/docker-guide) en TRaSH's [Hardlinks en Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) voor meer informatie over de juiste en optimale padconfiguratie. Let op dat de concepten van toepassing zijn op zowel Docker als niet-Docker.

> Je downloadmap waar je downloadclient de downloads plaatst en je root/bibliotheekmap MOETEN gescheiden zijn. \*Arr importeert het bestand/de bestanden vanuit de downloadmap van je downloadclient naar je bibliotheek. De downloadclient mag niets verplaatsen of downloaden naar je bibliotheek.
{.is-warning}

#### Verkeerde instellingen voor downloadclient

- De locatie waar je downloadclient bestanden downloadt, veroorzaakt problemen. Controleer de logs voor meer informatie. Dit kan te maken hebben met machtigingen of een poging om van Windows naar Linux of van Linux naar Windows te gaan zonder een externe padtoewijzing.

#### Verkeerde externe padtoewijzing

- De locatie waar uw downloadclient bestanden downloadt, veroorzaakt problemen. Controleer de logboeken voor meer informatie. Dit kan te maken hebben met machtigingen of een poging om van Windows naar Linux te gaan of van Linux naar Windows zonder een externe padkoppeling. Zie [TRaSH's Remote Path Guide](https://trash-guides.info/Readarr/Readarr-remote-path-mapping/) voor meer informatie.

#### Machtigingsfout

- Readarr of de gebruiker waarop Readarr wordt uitgevoerd, kan geen toegang krijgen tot de locatie waar uw downloadclient bestanden downloadt. Dit is meestal een machtigingsprobleem.

#### Auteur-Mount is alleen-lezen

{#author-mount-ro}

- De mount die een auteurspad bevat, is alleen-lezen gemount. Controleer uw mountinstellingen en eigendom/machtigingen.

#### Externe bestand is verwijderd tijdens het verwerken

- Een bestand dat toegankelijk is via een externe padkoppeling lijkt te zijn verwijderd voordat de verwerking is voltooid.

#### Extern pad wordt gebruikt en importeren is mislukt

- Controleer uw logboeken voor meer informatie; Raadpleeg onze Probleemoplossingsgidsen

### Afhandeling van voltooide/mislukte downloads

#### Afhandeling van voltooide downloads is uitgeschakeld

- (Deze waarschuwing wordt alleen gegenereerd voor bestaande gebruikers vóór de implementatie van de functie Afhandeling van voltooide downloads. Deze functie is standaard uitgeschakeld om ervoor te zorgen dat het systeem blijft werken zoals verwacht voor huidige configuraties.)
- Het wordt aanbevolen om Afhandeling van voltooide downloads te gebruiken, omdat dit een betere compatibiliteit biedt voor de uitpak- en nabewerkingslogica van verschillende downloadclients. Met Afhandeling van voltooide downloads importeert Readarr een download pas nadat de downloadclient heeft gemeld dat deze gereed is.
- Als u Afhandeling van voltooide downloads wilt inschakelen, moet u het volgende verifiëren: * Waarschuwing: Afhandeling van voltooide downloads werkt alleen correct als de downloadclient en Readarr zich op dezelfde machine bevinden, omdat het het pad om te importeren rechtstreeks van de downloadclient krijgt, anders is een externe koppeling vereist.

### Indexers

#### Geen indexers beschikbaar met ingeschakelde automatische zoekopdracht, Readarr geeft geen automatische zoekresultaten

- Simpel gezegd heeft u geen van uw indexers ingesteld om automatische zoekopdrachten toe te staan
- Ga naar Instellingen => Indexers, selecteer een indexer die u automatische zoekopdrachten wilt toestaan en klik vervolgens op Opslaan.

#### Geen indexers beschikbaar met ingeschakelde RSS-synchronisatie, Readarr zal geen nieuwe releases automatisch ophalen

- Readarr gebruikt de RSS-feed om nieuwe releases op te pikken terwijl ze verschijnen. Meer informatie hierover vindt u hier
- Om dit probleem op te lossen, gaat u naar Instellingen => Indexers, selecteert u een indexer die u heeft en schakelt u RSS-synchronisatie in

#### Er zijn geen indexers ingeschakeld

- Readarr vereist indexers om nieuwe releases te kunnen ontdekken. Lees de wiki voor instructies over het toevoegen van indexers.

### Ingeschakelde indexers ondersteunen geen zoekopdrachten

- Geen van de ingeschakelde indexers ondersteunt zoekopdrachten. Dit betekent dat Readarr alleen nieuwe releases kan vinden via de RSS-feeds. Maar zoeken naar boeken (zowel automatisch zoeken als handmatig zoeken) zal nooit resultaten opleveren. De enige manier om dit te verhelpen is door een andere indexer toe te voegen.

#### Geen indexers beschikbaar met ingeschakelde interactieve zoekopdracht

- Geen van de ingeschakelde indexers ondersteunt interactief zoeken. Dit betekent dat de applicatie alleen nieuwe releases kan vinden via de RSS-feeds of een automatische zoekopdracht.

#### Indexers zijn niet beschikbaar vanwege fouten

- Er zijn fouten opgetreden terwijl Readarr probeerde een van uw indexers te gebruiken. Om het aantal herhalingspogingen te beperken, zal Readarr de indexer steeds langer niet gebruiken (tot 24 uur).
- Dit mechanisme wordt geactiveerd als Readarr geen reactie van de indexer kon krijgen (dit kan worden veroorzaakt door DNS, proxy/vpn-verbinding, verificatie of een indexerprobleem), of als Readarr het nzb/torrent-bestand niet kon ophalen van de indexer. Bekijk de logboeken om te bepalen welk soort fout het probleem veroorzaakt.
- U kunt de waarschuwing voorkomen door de betreffende indexer uit te schakelen.
- Voer de test uit op de indexer om Readarr te dwingen de indexer opnieuw te controleren, houd er rekening mee dat de waarschuwing voor de gezondheidscontrole niet altijd onmiddellijk verdwijnt.

#### Jackett All Endpoint gebruikt

- Het Jackett /all-eindpunt is handig, maar dat is het enige voordeel. Al het andere kan problemen veroorzaken, dus het is nu vereist om elke tracker afzonderlijk toe te voegen.
- [Zelfs de ontwikkelaars van Jackett zeggen dat het vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Het gebruik van het /all-eindpunt heeft geen voordelen, alleen nadelen:
  - u verliest de controle over specifieke instellingen van indexers (categorieën, zoekmodi, enz.)
  - het mixen van zoekmodi (IMDB, query, enz.) kan leiden tot resultaten van lage kwaliteit
  - specifieke categorieën van indexers (\>= 100000) kunnen niet worden gebruikt.
  - trage indexers vertragen het algehele resultaat
  - het totale aantal resultaten is beperkt tot 1000
  - als een van de trackers in /all een fout retourneert, schakelt \*Arr deze uit en krijgt u geen resultaten meer.

##### Oplossingen

- Voeg elke tracker in Jackett handmatig toe als een indexer in \*Arr
- Bekijk [Prowlarr](/prowlarr) dat indexers kan synchroniseren met \*Arr en afkomstig is van het Lidarr/Radarr/Readarr ontwikkelingsteam.
- Bekijk [NZBHydra2](https://github.com/theotherp/nzbhydra2) dat indexers kan synchroniseren met \*Arr. Gebruik echter niet hun enkele aggregaat-eindpunt en gebruik `multi` als synchronisatie wordt gebruikt.

### Boekmappen

#### Ontbrekende hoofdmap

- Deze fout wordt meestal geïdentificeerd als een auteur op zoek is naar een hoofdmap, maar die hoofdmap is niet meer beschikbaar.
- Deze fout kan ook optreden als een lijst nog steeds naar een hoofdmap wijst, maar die hoofdmap is niet meer beschikbaar.
- Als u deze waarschuwing wilt verwijderen, zoekt u eenvoudig het album dat nog steeds de oude hoofdmap gebruikt en bewerkt u deze naar de juiste hoofdmap.

- De gemakkelijkste manier om de probleemauteur te vinden, is als volgt:

  - Ga naar het tabblad Auteur (Bibliotheek)
  - Maak een aangepaste filter met het oude pad van de hoofdmap
  - Selecteer massa-bewerken in de bovenste balk en selecteer het nieuwe hoofdpad dat u wilt dat deze auteur naar wordt verplaatst in het vervolgkeuzemenu Hoofdpaden.
  - Vervolgens ontvangt u een pop-upvenster met de melding Wilt u de auteursmappen verplaatsen naar 'hoofdpad'? Hierin staat ook Dit hernoemt ook de auteursmap volgens het formaat van de auteursmap in de instellingen. Selecteer simpelweg Nee als u niet wilt dat Lidarr uw bestanden verplaatst.
  - Voer de taak Controleer gezondheid uit in Systeem => Taken

### Importlijsten

#### Importlijsten zijn niet beschikbaar vanwege fouten

- Dit betekent meestal dat Readarr niet langer kan communiceren via API of door in te loggen bij uw gekozen lijstprovider. Uw beste optie als het probleem aanhoudt, is om contact met hen op te nemen om ze uit te sluiten, omdat hun systemen soms overbelast kunnen zijn.

## Schijfruimte

- In dit gedeelte wordt de beschikbare schijfruimte weergegeven
- In Docker kan dit lastig zijn, omdat het meestal de beschikbare ruimte binnen uw Docker-image laat zien

## Over

- Hier vindt u informatie over uw huidige installatie van Readarr

## Meer informatie

- Startpagina: Startpagina van Readarr
- Wiki: U bent hier al
- Reddit: r/readarr
- Discord: Doe mee aan onze discord
- Donaties: Als u vrijgevig bent en wilt doneren, klik dan hier
- Donaties aan Sonarr: Als u vrijgevig bent en wilt doneren aan het project dat het allemaal is begonnen, klik dan hier
- Bron: GitHub
- Functieverzoeken: Heeft u een geweldig idee, laat het hier vallen

# Taken

## Gepland

- In dit gedeelte worden alle geplande taken weergegeven die Readarr uitvoert

- Toepassingsupdate controleren - Dit wordt uitgevoerd volgens het weergegeven schema in de gebruikersinterface en controleert of Readarr de meest recente versie heeft en activeert vervolgens het update-script om Readarr bij te werken. Instellingen => Update

> Opmerking: Als u Docker gebruikt, wordt uw container niet bijgewerkt, omdat er een nieuwe image moet worden gedownload.
{.is-warning}

- Back-up - Dit maakt een back-up van de database van uw Readarr volgens een vast schema. Meer informatie hierover vindt u hier. Meer informatie over back-ups vindt u in Systeem => Back-ups.
- Gezondheidscontrole - De gezondheidscontrole wordt uitgevoerd volgens het weergegeven schema in de gebruikersinterface en controleert de algehele gezondheid van uw Readarr. Raadpleeg de Wiki-invoer over Gezondheidscontroles voor een lijst met mogelijke gezondheidsproblemen.
- Schoonmaak - Volgens het weergegeven schema in de gebruikersinterface wordt dit gebruikt om alle spinnenwebben weg te halen, te vegen en te stofzuigen, te dweilen, te laten glanzen en zelfs netjes gevouwen briefjes voor u te maken. Maar het haalt het vuilnis niet weg. Daarvoor werd het gewoon niet genoeg betaald.
- Importlijst synchroniseren - Volgens het weergegeven schema in de gebruikersinterface worden uw lijsten uitgevoerd en worden eventuele nieuwe boeken geïmporteerd. Meer informatie over lijsten vindt u in Instellingen => Lijsten.
- Opruimen van berichten - Volgens het weergegeven schema in de gebruikersinterface worden de berichten die in de linkerbenedenhoek van Readarr verschijnen, opgeruimd
- Auteur vernieuwen - Hiermee worden alle auteurs in uw bibliotheek vernieuwd.
- Vernieuwen van bewaakte downloads - Hiermee wordt de downloadwachtrij vernieuwd die zich onder Activiteit bevindt. Het controleert in feite uw downloadclient om te controleren op voltooide downloads.
- Mappen opnieuw scannen - Hiermee worden alle boekmappen gescand om te controleren of een boek al dan niet bestaat en de status ervan dienovereenkomstig bij te werken.
- RSS-synchronisatie - Hiermee wordt de RSS-synchronisatie uitgevoerd. Dit kan worden gewijzigd in instellingen => opties. Meer informatie over de RSS-functie vindt u in onze FAQ
  
> Al deze taken kunnen handmatig worden uitgevoerd buiten hun geplande tijden door op het pictogram helemaal rechts van elke taak te klikken.
{.is-info}

## Wachtrij

De wachtrij toont lopende en geplande taken, evenals een geschiedenis van recent uitgevoerde taken en de duur van die taken.

# Back-up

> Als u wilt weten hoe u uw Readarr-instantie kunt back-uppen/herstellen, klik dan [hier](/readarr/faq).
{.is-info}

- In het gedeelte Back-up worden eerdere back-ups weergegeven (tenzij u een nieuwe installatie heeft gemaakt zonder back-ups te maken).
  
- Nu een back-up maken - Met deze optie wordt een handmatige back-up van de database van uw Readarr geactiveerd
- Back-up herstellen - Hiermee wordt een nieuw scherm geopend om te herstellen vanuit een eerdere back-up
  - Door Bestand kiezen te selecteren, wordt uw browser gevraagd om een dialoogvenster te openen om te herstellen vanuit een Readarr-zipback-up
  
- Als u eerdere back-ups heeft en deze van Readarr wilt downloaden om ze op een niet-standaard locatie te plaatsen, kunt u eenvoudig een van deze bestanden selecteren om ze te downloaden
- Aan de rechterkant van elke vorige download heeft u twee opties.
  - Herstellen (Klokpictogram) - Om te herstellen vanuit een eerdere back-up - Hiermee wordt een nieuw venster geopend om te bevestigen dat u wilt herstellen vanuit deze back-up
  - Verwijderen (Prullenbakpictogram) - Om een eerdere back-up te verwijderen

# Updates

- Het updatescherm toont de laatste 5 updates die zijn uitgevoerd, evenals de huidige versie waarop u zich bevindt.
- Op deze pagina worden ook de update-opmerkingen van de ontwikkelaars weergegeven, waarin wordt vermeld wat er is gerepareerd of toegevoegd aan Readarr (Verheug u!)
  
> Een onderhoudsrelease bevat bugfixes en andere verschillende verbeteringen. Bekijk de commitgeschiedenis voor details.
{.is-info}

# Gebeurtenissen

- Het tabblad Gebeurtenissen laat zien wat er is gebeurd in uw Readarr. Dit kan worden gebruikt om enkele lichte problemen te diagnosticeren. Dit vervangt echter niet de Trace Logs die worden besproken in Logging.

> Gebeurtenissen zijn het equivalent van INFO-logs. {.is-info}

- Componenten - Deze kolom geeft aan welk component binnen Readarr is geactiveerd
- Bericht - Deze kolom geeft aan welk bericht is verzonden door het component uit de vorige kolom.
- Tandwielpictogram - Met deze optie kunt u instellen hoeveel componenten/berichten per pagina worden weergegeven (standaard is 50)
- Opties bovenaan de pagina
  - Vernieuwen - Met deze optie wordt de huidige pagina vernieuwd en wordt er een nieuw gebeurtenissenlogboek opgehaald
  - Wissen - Hiermee wordt het huidige gebeurtenissenlogboek gewist, zodat u opnieuw kunt beginnen

# Logbestanden

- Op deze pagina kunt u de huidige logbestanden downloaden en bekijken die beschikbaar zijn voor Readarr

- Op de bovenste rij zijn er verschillende opties waarmee u uw logbestanden kunt beheren.

- Op de bovenste rij helemaal links is er een vervolgkeuzemenu waarmee u kunt schakelen tussen Logbestanden en Updater Logbestanden
  - Logbestanden - Het belangrijkste onderdeel van elk ondersteuningsprobleem, meer informatie over logbestanden vindt u hier.
  - Updater Logbestanden - Dit toont de logbestanden die horen bij het update-script van Readarr

> Als u Docker gebruikt, is dit leeg omdat u moet updaten door een nieuwe Docker-image te downloaden.
{.is-info}

- Vernieuwen - Hiermee wordt de huidige pagina vernieuwd en worden eventuele nieuwe logbestanden weergegeven
- Verwijderen - Hiermee worden alle logbestanden gewist, zodat u opnieuw kunt beginnen
- Bestandsnaam - Hier wordt de bestandsnaam weergegeven die bij het logbestand hoort
- Laatst geschreven - Dit is de lokale tijd waarop dit specifieke logbestand is geschreven.
  - Readarr gebruikt rollende logbestanden van maximaal 1 MB. Het huidige logbestand is altijd readarr.txt, voor de andere bestanden is readarr.0.txt het op een na nieuwste (hoe hoger het nummer, hoe ouder het is) tot maximaal 51 logbestanden in totaal. Dit logbestand bevat `fatal`, `error`, `warn` en `info` vermeldingen.
  - Wanneer het logniveau Debug is ingeschakeld, zijn er extra readarr.debug.txt rollende logbestanden aanwezig, tot maximaal 51 bestanden. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info` en `debug` vermeldingen. Het beslaat meestal een periode van ~40 uur.
  - Wanneer het logniveau Trace is ingeschakeld, zijn er extra readarr.trace.txt rollende logbestanden aanwezig, tot maximaal 51 bestanden. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info`, `debug` en `trace` vermeldingen. Vanwege de uitgebreide trace-informatie beslaat het meestal slechts een paar uur.