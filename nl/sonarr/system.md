# Status

## Gezondheid

- Deze pagina bevat een lijst met fouten bij gezondheidscontroles. Deze gezondheidscontroles worden periodiek uitgevoerd door Sonarr en bij bepaalde gebeurtenissen. De resulterende waarschuwingen en fouten worden hier vermeld om advies te geven over hoe ze op te lossen.

### Systeemwaarschuwingen

#### Momenteel geïnstalleerde .NET Framework is oud en wordt niet ondersteund

- Sonarr maakt gebruik van het .NET Framework. We moeten Sonarr bouwen tegen de laagst ondersteunde versie die nog steeds door onze gebruikers wordt gebruikt. Af en toe verhogen we de versie waar we tegen bouwen om nieuwe functies te kunnen gebruiken. Blijkbaar hebt u al een tijdje geen geschikte Windows-updates toegepast en moet u .NET upgraden om nieuwere versies van Sonarr te kunnen gebruiken.

- Het upgraden van het .NET Framework is zeer eenvoudig op Windows, hoewel het vaak een herstart vereist.

#### Momenteel geïnstalleerde .NET Framework wordt ondersteund, maar een upgrade wordt aanbevolen

- Sonarr maakt gebruik van het .NET Framework. We moeten Sonarr bouwen tegen de laagst ondersteunde versie die nog steeds door onze gebruikers wordt gebruikt. Door te upgraden naar nieuwere versies kunnen we bouwen tegen nieuwere versies en nieuwe Framework-functies gebruiken.

- Het upgraden van het .NET Framework is zeer eenvoudig op Windows, hoewel het vaak een

#### Momenteel geïnstalleerde mono-versie is oud en wordt niet ondersteund

- Sonarr v4 is geschreven in .NET en v3 vereiste Mono. Mono 5.20 is het absolute minimum voor Sonarr.
- De upgradeprocedure voor Mono varieert per platform.

> Mono wordt niet langer ondersteund vanaf Sonarr versie 4.0
{.is-warning}

#### Momenteel geïnstalleerde SQLite-versie wordt niet ondersteund

- Sonarr slaat zijn gegevens op in een SQLite-database. De geïnstalleerde SQLite3-bibliotheek op uw systeem is te oud. Sonarr vereist minimaal versie 3.9.0.

> Houd er rekening mee dat Sonarr `libSQLite3.so` gebruikt, die mogelijk wel of niet is opgenomen in een SQLite3-upgradepakket.
{.is-info}

#### Bericht van pakketbeheerder

- Uw pakketbeheerder heeft een bericht voor u. Dit wordt beheerd door uw beheerder en niet door Sonarr.

#### Er is een nieuwe update beschikbaar

- Verheug u, de ontwikkelaars hebben een nieuwe update uitgebracht. Dit betekent meestal geweldige nieuwe functies en opgeloste bugs (toch?). Blijkbaar hebt u Automatisch bijwerken niet ingeschakeld, dus u moet zelf uitzoeken hoe u kunt bijwerken op uw platform. Het indrukken van de knop Installeren op de pagina Systeem => Updates is waarschijnlijk een goed startpunt.

> Deze waarschuwing verschijnt niet als uw huidige versie minder dan 14 dagen oud is
{.is-info}

#### Kan update niet installeren omdat de opstartmap en/of de UI-map niet beschrijfbaar zijn voor de gebruiker

{#cannot-install-update-because-UI-folder-is-not-writable-by-the-user}

{#cannot-install-update-because-startup-folder-is-not-writable-by-the-user}

Dit betekent dat Sonarr zichzelf niet kan bijwerken. U moet Sonarr handmatig bijwerken of de machtigingen op de opstartmap van Sonarr (de installatiemap) instellen om Sonarr in staat te stellen zichzelf bij te werken.

#### Kan update niet installeren omdat de opstartmap zich in een App Translocation-map bevindt

In macOS Sierra heeft Apple een vreemde beveiligingsfunctie toegevoegd genaamd App Translocation (soms bekend als Gatekeeper Path Randomization), wat betekent dat na het downloaden van een applicatie, als u de resulterende applicatie niet ergens verplaatst (overal!), met de Finder (u moet de Finder gebruiken!), de applicatie wordt uitgevoerd alsof deze zich op een willekeurig gekozen pad bevindt door het systeem.

#### Bijwerken is niet mogelijk om het verwijderen van AppData bij bijwerken te voorkomen

Sonarr heeft gedetecteerd dat de AppData-map voor uw besturingssysteem zich bevindt in de map die de Sonarr-binaries bevat. Normaal gesproken zou dit C:\ProgramData zijn voor Windows en ~/.config voor Linux.

Kijk op Systeem => Info om de huidige AppData- en opstartmappen te zien.
Dit betekent dat Sonarr zichzelf niet kan bijwerken zonder het risico van gegevensverlies.
Als u Linux gebruikt, moet u waarschijnlijk de thuisdirectory wijzigen voor de gebruiker die Sonarr uitvoert en de huidige inhoud van de map ~/.config/Sonarr kopiëren om uw database te behouden.

#### Kan het IP-adres voor de geconfigureerde proxyhost niet oplossen

Controleer uw proxy-instellingen en zorg ervoor dat ze correct zijn
Zorg ervoor dat uw proxy actief, actief en toegankelijk is

#### Proxy-test mislukt

Uw geconfigureerde proxy is niet geslaagd voor de test, controleer de verstrekte HTTP-fout en/of controleer de logboeken voor meer details.

#### Systeemtijd loopt meer dan 1 dag achter

De systeemtijd loopt meer dan 1 dag achter. Geplande taken kunnen mogelijk niet correct worden uitgevoerd totdat de tijd is gecorrigeerd
Controleer uw systeemtijd en zorg ervoor dat deze is gesynchroniseerd met een betrouwbare tijdserver en nauwkeurig is

#### Mediabibliotheek kan niet worden geladen

De mediabibliotheek kan niet worden geladen. Sonarr vereist MediaInfo (`libmediainfo`) om de videokenmerken van bestanden te evalueren.

#### Mono Legacy TLS ingeschakeld

{#sonarr-mono-4.x-tls-workaround-still-enabled-consider-removing-mono_tls_provider-legacy-environment-option}

Mono 4.x TLS-omweg is nog steeds ingeschakeld, overweeg de MONO_TLS_PROVIDER=legacy omgevingsoptie te verwijderen.

### Downloadclients

#### Geen downloadclient beschikbaar

Er is een correct geconfigureerde en ingeschakelde downloadclient vereist voor Sonarr om media te kunnen downloaden. Aangezien Sonarr verschillende downloadclients ondersteunt, moet u bepalen welke het beste bij uw eisen past. Als u al een downloadclient hebt geïnstalleerd, moet u Sonarr configureren om deze te gebruiken en een categorie te maken. Zie Instellingen => Downloadclient.

#### Kan niet communiceren met downloadclient

Sonarr kon niet communiceren met de geconfigureerde downloadclient. Controleer of de downloadclient operationeel is en controleer de URL dubbel. Dit kan ook duiden op een verificatiefout.
Dit wordt meestal veroorzaakt door een onjuist geconfigureerde downloadclient. Dingen die u meestal kunt controleren:
Het IP-adres van uw downloadclient als deze zich op dezelfde fysieke machine bevindt, is dit meestal 127.0.0.1
Het poortnummer dat uw downloadclient gebruikt, deze zijn ingevuld met het standaard poortnummer, maar als u het hebt gewijzigd, moet u hetzelfde nummer invoeren in Sonarr.
Zorg ervoor dat SSL-versleuteling niet is ingeschakeld als u zowel uw Sonarr-instantie als uw downloadclient op een lokaal netwerk gebruikt. Zie de SSL FAQ voor meer informatie.

#### Downloadclients zijn niet beschikbaar vanwege een storing

Een of meer van uw downloadclients reageert niet op verzoeken van Sonarr. Daarom heeft Sonarr besloten om tijdelijk te stoppen met het bevragen van de downloadclient op de normale cyclus van 1 minuut, die normaal wordt gebruikt om actieve downloads bij te houden en voltooide downloads te importeren. Sonarr zal echter blijven proberen downloads naar de client te sturen, maar zal naar alle waarschijnlijkheid falen.
U moet Systeem => Logboeken controleren om de reden voor de fouten te zien.
Als u deze downloadclient niet meer gebruikt, schakel deze dan uit in Sonarr om de fouten te voorkomen.

#### Voltooide downloadverwerking inschakelen

- Sonarr vereist voltooide downloadverwerking om bestanden te kunnen importeren die zijn gedownload door de downloadclient. Het wordt aanbevolen om voltooide downloadverwerking in te schakelen.
(Voltooide downloadverwerking is standaard ingeschakeld...)

#### Slechte externe padkoppeling in Docker

- Deze fout wordt meestal geassocieerd met onjuiste docker-paden binnen uw downloadclient of Sonarr

- Een voorbeeld hiervan zou zijn:
  - Downloadclient: Downloadpad: /mnt/user/downloads:/downloads
  - Radarr: Downloadpad: /mnt/user/downloads:/data
- In dit voorbeeld plaatst de downloadclient zijn downloads in /downloads en vertelt het aan Radarr wanneer het klaar is dat de voltooide film zich in /downloads bevindt. Sonarr komt dan langs en zegt "Oké, cool, laat me in /downloads kijken" Welnu, binnen Radarr heb je geen /downloads-pad toegewezen, je hebt een /data-pad toegewezen, dus gooit het deze fout.
- De gemakkelijkste oplossing hiervoor is CONSISTENTIE, als je één schema gebruikt in je downloadclient, gebruik het dan overal.

- Team Sonarr is een groot voorstander van het eenvoudigweg gebruiken van /data.
  - Downloadclient: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Nu kunt u binnen de downloadclient aangeven waar u uw downloads in /data wilt plaatsen, dit varieert afhankelijk van de client, maar u zou het moeten kunnen vertellen "Ja, downloadclient plaats mijn bestanden in." /data/torrents (of usenet)/movies en omdat je /data hebt gebruikt in Radarr wanneer de downloadclient aan Radarr vertelt dat het klaar is, zal Radarr langskomen en zeggen "Geweldig, ik heb een /data en ik kan ook /torrents (of usenet)/movies zien, alles is in orde in de wereld."
- Er zijn veel goede handleidingen: onze wiki [Docker-gids](/docker-guide) en TRaSH's [Hardlinks en Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Deze handleidingen leggen veel nadruk op Hardlinks en Atomic moves, maar het algemene concept van containers en hoe het padmapping werkt, is de kern van deze discussies.

- Zie [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) voor meer informatie.

#### Downloaden naar rootmap

{#downloads-in-root-folder}

- Binnen de applicatie wordt een rootmap gedefinieerd als de geconfigureerde mediabibliotheekmap. Dit is niet de rootmap van een mount. Uw downloadclient plaatst een onvolledige of voltooide download (of verplaatst voltooide downloads) naar uw root (bibliotheek) map.
- Dit veroorzaakt vaak problemen - inclusief gegevensverlies - en mag niet worden gedaan. Om dit op te lossen, wijzigt u uw downloadclient zodat deze geen downloads plaatst binnen uw rootmap. Let op: 'plaatsen' omvat ook als uw downloadclient-categorie is ingesteld op uw rootmap of als NZBGet/SABnzbd sorteren ingeschakeld heeft en sorteert naar uw rootmap.
- Houd er rekening mee dat deze controle kijkt naar alle gedefinieerde/geconfigureerde rootmappen die zijn toegevoegd, niet alleen naar rootmappen die momenteel in gebruik zijn. Met andere woorden, de map waarin uw downloadclient downloads plaatst of voltooide downloads naartoe verplaatst, mag niet dezelfde map zijn die u hebt geconfigureerd als uw root/bibliotheek/eindbestemmingsmap voor media in de *arr-toepassing.
- Geconfigureerde rootmappen (ook wel bibliotheekmappen genoemd) vindt u in [Instellingen => Mediabeheer => Rootmappen](/sonarr/settings/#root-folders)
- Een voorbeeld is als uw downloads naar `/data/downloads` gaan en u een rootmap heeft ingesteld als `/data/downloads`.
- Het wordt aanbevolen om paden zoals `/data/media/` te gebruiken voor uw rootmap/bibliotheek en `/data/downloads/` voor uw downloads.
- Bekijk onze [Docker-gids](/docker-guide) en TRaSH's [Hardlinks en Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) voor meer informatie over de juiste en optimale padconfiguratie. Let op: de concepten zijn van toepassing op zowel docker als niet-docker

> Uw downloadmap waar uw downloadclient de downloads plaatst en uw root/bibliotheekmap MOETEN gescheiden zijn. \*Arr importeert het bestand/de bestanden vanuit de map van uw downloadclient naar uw bibliotheek. De downloadclient mag niets verplaatsen of downloaden naar uw bibliotheek.
{.is-warning}

#### Slechte instellingen voor downloadclient

- De locatie waar uw downloadclient bestanden downloadt, veroorzaakt problemen. Controleer de logboeken voor meer informatie. Dit kan te maken hebben met machtigingen of een poging om van Windows naar Linux te gaan of van Linux naar Windows zonder een externe padkoppeling.

#### Slechte externe padkoppeling

- De locatie waar uw downloadclient bestanden downloadt, veroorzaakt problemen. Controleer de logboeken voor meer informatie. Dit kan te maken hebben met machtigingen of een poging om van Windows naar Linux te gaan of van Linux naar Windows zonder een externe padkoppeling. Zie [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) voor meer informatie.

#### Machtigingsfout

- Sonarr of de gebruiker waarop Sonarr wordt uitgevoerd, heeft geen toegang tot de locatie waar uw downloadclient bestanden downloadt. Dit is meestal een machtigingsprobleem.

#### Extern bestand is verwijderd tijdens het verwerken

- Een bestand dat toegankelijk is via een externe padkoppeling lijkt te zijn verwijderd voordat de verwerking is voltooid.

#### Extern pad wordt gebruikt en import is mislukt

- Controleer uw logboeken voor meer informatie; Raadpleeg onze probleemoplossingsgidsen

### Downloaden naar rootmap

{#downloads-in-root-folder}

- Binnen de applicatie wordt een rootmap gedefinieerd als de geconfigureerde mediabibliotheekmap. Dit is niet de rootmap van een mount. Uw downloadclient plaatst onvolledige of voltooide downloads (of verplaatst voltooide downloads) naar uw root (bibliotheek) map.
- Dit veroorzaakt vaak problemen - inclusief gegevensverlies - en mag niet worden gedaan. Om dit op te lossen, wijzigt u uw downloadclient zodat deze downloads niet in uw rootmap worden geplaatst. Houd er rekening mee dat 'plaatsen' ook inhoudt dat uw downloadclient-categorie is ingesteld op uw rootmap of dat NZBGet/SABnzbd sorteren ingeschakeld heeft en sorteert naar uw rootmap.
- Houd er rekening mee dat deze controle kijkt naar alle gedefinieerde/geconfigureerde rootmappen, niet alleen naar de momenteel gebruikte rootmappen. Met andere woorden, de map waar uw downloadclient downloads naar downloadt of voltooide downloads naartoe verplaatst, mag niet dezelfde map zijn die u hebt geconfigureerd als uw root/bibliotheek/eindbestemmingsmap voor media in de *arr-applicatie.
- Geconfigureerde rootmappen (ook wel bibliotheekmappen genoemd) kunnen worden gevonden in [Instellingen => Mediabeheer => Rootmappen](/sonarr/settings/#root-folders)
- Een voorbeeld is als uw downloads naar `/data/downloads` gaan, dan heeft u een rootmap ingesteld als `/data/downloads`.
- Het wordt aanbevolen om paden zoals `/data/media/` te gebruiken voor uw rootmap/bibliotheek en `/data/downloads/` voor uw downloads.
- Bekijk onze [Docker-gids](/docker-guide) en TRaSH's [Hardlinks en Instant Moves (Atomic-Moves) Gids](https://trash-guides.info/hardlinks/) voor meer informatie over de juiste en optimale configuratie van paden. Houd er rekening mee dat de concepten van toepassing zijn op zowel Docker als niet-Docker.

> Uw downloadmap waar uw downloadclient de downloads plaatst en uw root/bibliotheekmap MOET gescheiden zijn. \*Arr importeert het bestand/de bestanden van de downloadmap van uw downloadclient naar uw bibliotheek. De downloadclient mag niets verplaatsen of downloaden naar uw bibliotheek.
{.is-warning}

#### Voltooide downloadverwerking is uitgeschakeld

{#completedfailed-download-handling}

- Het is vereist om Voltooide Downloadverwerking te gebruiken, omdat dit betere compatibiliteit biedt voor het uitpakken en post-processing logica van verschillende downloadclients. Met Voltooide Downloadverwerking importeert Sonarr een download pas nadat de downloadclient deze als gereed heeft gemeld.
- Als voltooide downloadverwerking is uitgeschakeld:
  - Moeten alle imports handmatig worden afgehandeld
  - Deze gezondheidscontrole blijft bestaan en kan niet worden genegeerd of uitgeschakeld
  - Afleveringen zullen altijd ontbreken in Sonarr en in aanmerking komen om voor altijd te worden opgepikt
    - Afleveringen die handmatig door de gebruiker zijn verplaatst en hernoemd naar de map van de serie in de bibliotheekmap van Sonarr worden mogelijk opgepikt door de tweemaandelijkse rescan als ze op dat moment correct zijn genoemd.
  - De gebruiker moet handmatig de monitoring van afleveringen stopzetten of een aangepast script voor On Grab configureren om afleveringen niet te monitoren.
  - FlexGet is waarschijnlijk een beter hulpmiddel voor uw gebruikssituatie als u de mediabibliotheekbeheerfunctionaliteiten van Sonarr niet wilt gebruiken en gewoon iets nodig heeft om RSS-feeds te verwerken en releases naar de downloadclient te sturen.

> \* Voltooide Downloadverwerking werkt alleen correct als de downloadclient en Sonarr zich op dezelfde machine bevinden, omdat het het pad om te importeren rechtstreeks van de downloadclient krijgt. Anders is een externe mapping nodig.
> \* Voltooide Downloadverwerking vereist dat Sonarr lees- en schrijftoegang heeft tot de map met voltooide downloads.
{.is-warning}

### Indexers

#### Geen indexers beschikbaar met automatisch zoeken ingeschakeld, Sonarr zal geen automatische zoekresultaten geven

- Simpel gezegd heb je geen van je indexers ingesteld om automatisch zoeken toe te staan.
Ga naar Instellingen > Indexers, selecteer een indexer die je automatisch zoeken wilt toestaan en klik vervolgens op Opslaan.

#### Geen indexers beschikbaar met RSS-synchronisatie ingeschakeld, Sonarr zal geen nieuwe releases automatisch ophalen

{#no-indexers-available-with-rss-sync-enabled,-sonarr-will-not-grab-new-releases-automatically}
{#all-rss-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Sonarr gebruikt de RSS-feed om nieuwe releases op te pikken terwijl ze binnenkomen. [Zie de FAQ voor meer informatie](/sonarr/faq#how-does-sonarr-find-episodes)
- Om dit probleem op te lossen, ga naar Instellingen > Indexers, selecteer een indexer die je hebt en schakel RSS-synchronisatie in.

#### Geen indexers ingeschakeld

- Sonarr vereist indexers om nieuwe releases te kunnen ontdekken. Al uw indexers zijn uitgeschakeld of u hebt geen indexers toegevoegd.

#### Ingeschakelde indexers ondersteunen geen zoeken

{#all-search-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Geen van de ingeschakelde en beschikbare indexers ondersteunt zoeken. Dit betekent dat Sonarr alleen nieuwe releases kan vinden via de RSS-feeds. Maar zoeken naar series (zowel automatisch zoeken als handmatig zoeken) zal nooit resultaten opleveren. De enige manier om dit te verhelpen is door een andere indexer toe te voegen.

#### Geen indexers beschikbaar met interactief zoeken ingeschakeld

{#no-indexers-available-with-interactive-search-enabled-sonarr-will-not-provide-any-interactive-search-results}

- Geen van de ingeschakelde en beschikbare indexers ondersteunt interactief zoeken. Dit betekent dat de applicatie alleen nieuwe releases kan vinden via de RSS-feeds of een automatische zoekopdracht.

#### Indexers zijn niet beschikbaar vanwege fouten

- Er zijn fouten opgetreden terwijl Sonarr probeerde een van uw indexers te gebruiken. Om het aantal herhalingspogingen te beperken, zal Sonarr de indexer steeds langer niet gebruiken (tot 24 uur).
- Dit mechanisme wordt geactiveerd als Sonarr geen reactie van de indexer kon krijgen (dit kan worden veroorzaakt door DNS, proxy/vpn-verbinding, authenticatie of een indexerprobleem), of als Sonarr het nzb/torrent-bestand niet kon ophalen van de indexer. Bekijk de logboeken om te bepalen wat voor soort fout het probleem heeft veroorzaakt.
- U kunt deze waarschuwing voorkomen door de betreffende indexer uit te schakelen.
- Voer een `Test` uit op de indexer om Sonarr te dwingen de indexer opnieuw te controleren; houd er rekening mee dat de waarschuwing van de gezondheidscontrole niet altijd onmiddellijk verdwijnt en dat u mogelijk de taak `Check Health` moet uitvoeren

#### Jackett All Endpoint Gebruikt

- Het Jackett /all-eindpunt is handig, maar dat is het enige voordeel. Al het andere kan problemen veroorzaken, dus het is nu vereist om elke tracker afzonderlijk toe te voegen.
- [Zelfs de ontwikkelaars van Jackett zeggen dat het vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Het gebruik van het /all-eindpunt heeft geen voordelen, alleen nadelen:
  - u verliest de controle over specifieke instellingen van indexers (categorieën, zoekmodi, etc.)
  - het mengen van zoekmodi (IMDB, query, etc.) kan leiden tot resultaten van lage kwaliteit
  - indexer-specifieke categorieën (\>= 100000) kunnen niet worden gebruikt.
  - trage indexers vertragen het algehele resultaat
  - het totale aantal resultaten is beperkt tot 1000
  - als een van de trackers in /all een fout retourneert, schakelt \*Arr deze uit en krijgt u geen resultaten meer.

##### Oplossingen

- Voeg elke tracker in Jackett handmatig toe als een indexer in \*Arr
- Bekijk [Prowlarr](/prowlarr), dat indexers kan synchroniseren met \*Arr en afkomstig is van het Lidarr/Radarr/Readarr-ontwikkelingsteam.
- Bekijk [NZBHydra2](https://github.com/theotherp/nzbhydra2), dat indexers kan synchroniseren met \*Arr. Gebruik echter niet hun enkele aggregatie-eindpunt en gebruik `multi` als synchronisatie wordt gebruikt.

### Media & Lijsten

#### Series verwijderd uit TheTVDB

- De betreffende serie(s) is/zijn verwijderd uit [The TVDb](https://thetvdb.com). Dit gebeurt meestal omdat de serie een duplicaat is of als onderdeel van een andere serie wordt beschouwd. Mogelijk behandelt TMDb het ook als een serie; hopelijk kan [Radarr](/radarr) dan worden gebruikt. Om dit te corrigeren, moet u de betreffende serie verwijderen en indien van toepassing de juiste serie toevoegen.

#### Lijsten zijn niet beschikbaar vanwege fouten

{#import-lists-are-unavailable-due-to-failures}

- Dit betekent meestal dat Sonarr niet langer kan communiceren via API of via het inloggen bij uw gekozen lijstprovider. Als het probleem aanhoudt, kunt u het beste contact met hen opnemen om ze uit te sluiten, omdat hun systemen soms overbelast kunnen zijn.
- Bekijk Systeem => Gebeurtenissen gefilterd op Waarschuwing (Waarschuwingen en Fouten) om de historische fouten te zien of controleer de logboeken voor details.

#### Importlijst mist rootmap

- Een of meer van uw importlijsten zijn geconfigureerd naar een rootmap die niet toegankelijk is voor Sonarr.
- Dit kan te maken hebben met machtigingsproblemen, een ontbrekende mount of simpelweg de lijsten bijwerken nadat u uw setup opnieuw hebt georganiseerd.

#### Ontbrekende rootmap

- Er is een rootmap toegevoegd aan Sonarr die niet bestaat of niet toegankelijk is.
- Deze fout wordt meestal geïdentificeerd als een serie op zoek is naar een rootmap, maar die rootmap is niet meer beschikbaar.
- Deze fout kan ook optreden als een lijst nog steeds naar een rootmap wijst, maar die rootmap is niet meer beschikbaar.
- Als u deze waarschuwing wilt verwijderen, zoekt u eenvoudigweg de serie die nog steeds de oude rootmap gebruikt en bewerkt u deze naar de juiste rootmap.

- De gemakkelijkste manier om de probleemserie te vinden is:

  - Ga naar het tabblad Massa-editor
  - Maak een aangepaste filter met het pad van de oude rootmap
  - Selecteer massa-bewerken in de bovenste balk en selecteer in het vervolgkeuzemenu Rootpaden het nieuwe rootpad waar u deze series naartoe wilt verplaatsen.
  - Vervolgens krijgt u een pop-upvenster met de melding Wilt u de serie-mappen verplaatsen naar 'root pad'? Hierin staat ook Dit hernoemt ook de map van de serie volgens het mapformaat van de serie in de instellingen. Selecteer eenvoudigweg Nee als u niet wilt dat Lidarr uw bestanden verplaatst.
  - Voer de taak Check Health uit in Systeem => Taken

#### Seriespad-mount is alleen-lezen

{#series-mount-ro}

Een mount met een seriespad is alleen-lezen en kan niet worden beschreven door de gebruiker waarop Sonarr wordt uitgevoerd.

## Schijfruimte

- In dit gedeelte wordt de beschikbare schijfruimte weergegeven.
- In Docker kan dit lastig zijn, omdat het meestal de beschikbare ruimte binnen uw Docker-image laat zien.

## Over

- Hier vindt u informatie over uw huidige installatie van Sonarr.

## Meer informatie

- Startpagina: Sonarr's [startpagina](https://www.sonarr.tv)
- Wiki: U bent hier al.
- Reddit: [r/sonarr](https://www.reddit.com/r/sonarr)
- Discord: Doe mee aan onze [discord](https://discord.sonarr.tv/)
- Donaties: Als u vrijgevig bent en wilt doneren, klik dan [hier](https://sonarr.tv/donate).
- Broncode: [GitHub](https://www.github.com/sonarr/sonarr)
- Functieverzoeken: Heeft u een geweldig idee, laat het [hier](https://www.github.com/sonarr/sonarr/issues) weten.

# Taken

## Gepland

- In dit gedeelte worden alle geplande taken weergegeven die Sonarr uitvoert.

- Applicatie Update Controleren - Dit wordt uitgevoerd volgens het weergegeven schema in de gebruikersinterface en controleert of Sonarr de meest recente versie heeft en activeert vervolgens het update-script om Sonarr bij te werken. Instellingen => Update

> Opmerking: Als u Docker gebruikt, wordt uw container niet bijgewerkt, omdat er een nieuwe image gedownload moet worden.
{.is-warning}

- Backup - Dit maakt een back-up van de database van Sonarr volgens een vast schema. Meer informatie over back-ups vindt u in Systeem => Back-ups.
- Gezondheid controleren - Deze taak controleert de algehele gezondheid van Sonarr volgens het weergegeven schema in de gebruikersinterface. Raadpleeg de Wiki-pagina over Gezondheidscontroles voor een lijst met mogelijke gezondheidsproblemen.
- Prullenbak opruimen - De prullenbak wordt op het weergegeven schema in de gebruikersinterface leeggemaakt. Dit wordt alleen gebruikt als de prullenbak is ingesteld in Bestandsbeheer.
- Huishouding - Op het weergegeven schema in de gebruikersinterface worden alle spinnenwebben weggehaald, wordt er geveegd en gestofzuigd, wordt er gedweild en gepoetst, en worden er zelfs netjes gevouwen briefjes gemaakt alleen voor jou. Maar het afval wordt niet weggegooid. Daarvoor wordt gewoon niet genoeg betaald.
- Importlijst synchroniseren - Op het weergegeven schema in de gebruikersinterface worden uw lijsten uitgevoerd en worden eventuele nieuwe series geïmporteerd. Meer informatie over lijsten vindt u in Instellingen => Lijsten.
- Opruimen van berichten - Op het weergegeven schema in de gebruikersinterface worden de berichten opgeruimd die in de linkerbenedenhoek van Sonarr verschijnen.
- Vernieuwen van gemonitorde downloads - Hiermee wordt de downloadwachtrij vernieuwd die te vinden is onder Activiteit. Hiermee wordt in feite uw downloadclient gepinged om te controleren op voltooide downloads.
- Vernieuwen van series - Hiermee wordt alle metadata voor alle gemonitorde en niet-gemonitorde series vernieuwd.
- RSS-synchronisatie - Hiermee wordt de RSS-synchronisatie uitgevoerd. Dit kan worden gewijzigd in Instellingen => Indexers => Opties. Meer informatie over de RSS-functie vindt u in onze [FAQ](/sonarr/faq)
  
> Al deze taken kunnen handmatig worden uitgevoerd buiten hun geplande tijden door op het pictogram helemaal rechts van elke taak te klikken.
{.is-info}

## Wachtrij

De wachtrij toont lopende en geplande taken, evenals een geschiedenis van recent uitgevoerde taken en hoe lang die taken hebben geduurd.

# Backup

> Als u wilt weten hoe u uw Sonarr-instantie kunt back-uppen/herstellen, klik dan [hier](/sonarr/faq).
{.is-info}

In het gedeelte Backup worden eerdere back-ups weergegeven (tenzij u een nieuwe installatie hebt die geen back-ups heeft gemaakt).
  
- Nu een back-up maken - Hiermee wordt handmatig een back-up van de database van Sonarr gemaakt
- Back-up herstellen - Hiermee wordt een nieuw scherm geopend om te herstellen vanuit een eerdere back-up
  - Door Bestand kiezen te selecteren, wordt uw browser gevraagd om een dialoogvenster te openen om te herstellen vanuit een Sonarr-zipback-up
  
- Als u eerdere back-ups hebt en deze van Sonarr wilt downloaden om ze op een niet-standaard locatie te plaatsen, kunt u eenvoudig een van deze bestanden selecteren om ze te downloaden
- Aan de rechterkant van elk van de vorige downloads heeft u twee opties.

  - Herstellen (Klokpictogram) - Om te herstellen vanuit een eerdere back-up - Dit opent een nieuw venster om te bevestigen dat u wilt herstellen vanuit deze back-up
  - Verwijderen (Prullenbakpictogram) - Om een eerdere back-up te verwijderen

# Updates

Het updatescherm toont de laatste 5 updates die zijn uitgevoerd, evenals de huidige versie waarop u zich bevindt.
Op deze pagina worden ook de update-opmerkingen van de ontwikkelaars weergegeven waarin wordt beschreven wat er is gerepareerd of toegevoegd aan Sonarr (Verheug u!)
  
> Een onderhoudsrelease bevat bugfixes en andere verbeteringen. Bekijk de commitgeschiedenis op Github voor details.
{.is-info}

# Gebeurtenissen

Het tabblad Gebeurtenissen toont wat er is gebeurd in uw Sonarr. Dit kan worden gebruikt om enkele lichte problemen te diagnosticeren. Dit vervangt echter niet de Trace Logs die worden besproken in Logging.

> Gebeurtenissen zijn het equivalent van INFO-logs. {.is-info}

- Componenten - Deze kolom geeft aan welk component binnen Sonarr is geactiveerd
- Bericht - Deze kolom geeft aan welk bericht is verzonden door het component uit de vorige kolom.
- Tandwielpictogram - Met deze optie kunt u instellen hoeveel componenten/berichten per pagina worden weergegeven (standaard is 50)
- Opties bovenaan de pagina
  - Vernieuwen - Hiermee wordt de huidige pagina vernieuwd en wordt er een nieuwe gebeurtenissenlog weergegeven
  - Wissen - Hiermee wordt de huidige gebeurtenissenlog gewist, zodat u opnieuw kunt beginnen

# Logbestanden

- Op deze pagina kunt u de huidige logbestanden van Sonarr downloaden en bekijken.

- Bovenaan de pagina zijn er verschillende opties om uw logbestanden te beheren.

- In de bovenste rij helemaal links is er een vervolgkeuzemenu waarmee u kunt schakelen tussen Logbestanden en Updater Logbestanden
  - Logbestanden - Het belangrijkste onderdeel bij elk ondersteuningsprobleem, meer informatie over logbestanden vindt u hier.
  - Updater Logbestanden - Dit toont de logbestanden die horen bij het update-script van Sonarr

> Als u Docker gebruikt, is dit leeg omdat u moet updaten door een nieuwe Docker-image te downloaden.
{.is-info}

- Vernieuwen - Hiermee wordt de huidige pagina vernieuwd en worden eventuele nieuwe logbestanden weergegeven
- Verwijderen - Hiermee worden alle logbestanden gewist, zodat u opnieuw kunt beginnen
- Bestandsnaam - Hier wordt de bestandsnaam van het logbestand weergegeven
- Laatst geschreven - Dit is de lokale tijd waarop dit specifieke logbestand is geschreven.
  - Sonarr gebruikt rollende logbestanden met een limiet van 1 MB per stuk. Het huidige logbestand is altijd sonarr.txt, voor de andere bestanden is sonarr.0.txt de op een na nieuwste (hoe hoger het nummer, hoe ouder het is) tot in totaal 51 logbestanden. Dit logbestand bevat `fatal`, `error`, `warn` en `info` vermeldingen.
  - Wanneer het debug-logniveau is ingeschakeld, zijn er extra sonarr.debug.txt rollende logbestanden aanwezig, tot 51 bestanden. Dit logbestand bevat `fatal`, `error`, `warn`, `info` en `debug` vermeldingen. Het beslaat meestal een periode van ~40 uur.
  - Wanneer het trace-logniveau is ingeschakeld, zijn er extra sonarr.trace.txt rollende logbestanden aanwezig, tot 51 bestanden. Dit logbestand bevat `fatal`, `error`, `warn`, `info`, `debug` en `trace` vermeldingen. Vanwege de uitgebreide trace-informatie beslaat het meestal slechts een paar uur.