# Status

## Health

Deze pagina bevat een lijst met fouten bij gezondheidscontroles. Deze gezondheidscontroles worden periodiek uitgevoerd door Prowlarr en bij bepaalde gebeurtenissen. De resulterende waarschuwingen en fouten worden hier vermeld om advies te geven over hoe ze op te lossen.

### Systeemwaarschuwingen

#### Branch is geen geldige release branch

- De branch die je hebt ingesteld is geen geldige release branch. Je ontvangt geen updates. Verander deze naar een van de [huidige release branches](/prowlarr/faq#hoe-update-ik-prowlarr).

#### Huidige geïnstalleerde SQLite-versie wordt niet ondersteund

- Prowlarr slaat zijn gegevens op in een SQLite-database. De geïnstalleerde SQLite3-bibliotheek op je systeem is te oud. Prowlarr vereist minimaal versie 3.9.0. Let op dat Prowlarr `libSQLite3.so` gebruikt, die al dan niet is opgenomen in een SQLite3-upgradepakket.

#### Nieuwe update beschikbaar

- Verheug je, de ontwikkelaars hebben een nieuwe update uitgebracht. Dit betekent meestal geweldige nieuwe functies en opgeloste bugs (toch?). Blijkbaar heb je automatische updates niet ingeschakeld, dus je moet zelf uitzoeken hoe je moet updaten op jouw platform. Het indrukken van de knop Installeren op de pagina Systeem => Updates is waarschijnlijk een goed startpunt.

> Deze waarschuwing verschijnt niet als je huidige versie minder dan 14 dagen oud is
{.is-info}

#### Kan update niet installeren omdat de opstartmap niet beschrijfbaar is door de gebruiker

- Dit betekent dat Prowlarr zichzelf niet kan updaten. Je moet Prowlarr handmatig updaten of de machtigingen op de opstartmap van Prowlarr (de installatiemap) instellen om Prowlarr in staat te stellen zichzelf bij te werken.

#### Updaten is niet mogelijk om het verwijderen van AppData bij een update te voorkomen

- Prowlarr heeft gedetecteerd dat de AppData-map voor je besturingssysteem zich bevindt in de map die de Prowlarr-binaries bevat. Normaal gesproken zou dit C:\ProgramData zijn voor Windows en ~/.config voor Linux.

- Kijk naar Systeem => Info om de huidige AppData- en opstartmappen te zien.
- Dit betekent dat Prowlarr zichzelf niet kan updaten zonder het risico op gegevensverlies.
- Als je Linux gebruikt, moet je waarschijnlijk de home-directory voor de gebruiker die Prowlarr uitvoert wijzigen en de huidige inhoud van de map ~/.config/Prowlarr kopiëren om je database te behouden.

#### Branch is voor een vorige versie

- De update-branch die is ingesteld in Instellingen/Algemeen is voor een vorige versie van Prowlarr, daarom zal de instantie geen juiste update-informatie zien in de feed Systeem/Updates en mogelijk geen nieuwe updates ontvangen wanneer deze worden uitgebracht.

#### Kan geen verbinding maken met signalR

- signalR zorgt voor dynamische updates van de gebruikersinterface, dus als je browser geen verbinding kan maken met signalR op je server, zie je geen realtime updates in de gebruikersinterface.

- De meest voorkomende oorzaak hiervan is het gebruik van een omgekeerde proxy of Cloudflare.
  - Cloudflare heeft websockets ingeschakeld nodig.
  - Nginx vereist de volgende toevoeging aan het locatieblok voor de app:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Zorg ervoor dat je proxy_set_header Connection "Upgrade"; niet opneemt, zoals voorgesteld in de nginx-documentatie. DIT WERKT NIET
> Zie <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

- Voor een omgekeerde proxy van Apache2 moet je de volgende modules inschakelen: proxy, proxy_http en proxy_wstunnel. Voeg vervolgens deze websocket-tunnelinstructie toe aan je vhost-configuratie:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:9696/$1 [P,L]
```

Als je een omgekeerde proxy hebt onder een subdirectory, moet de RewriteRule je basispad bevatten, bijvoorbeeld:

```none
RewriteRule /prowlarr/(.*) ws://127.0.0.1:9696/prowlarr/$1 [P,L]
```

Als Prowlarr niet op dezelfde machine als je omgekeerde proxy wordt uitgevoerd, vervang je 127.0.0.1 door het juiste IP-adres/DNS-naam van je Prowlarr-app.

- Voor Caddy (V1) gebruik je dit:

> Opmerking: je moet ook de websocket-instructie toevoegen aan je prowlarr-configuratie{.is-info}

```none
 proxy /prowlarr 127.0.0.1:9696 {
     websocket
     transparent
 }
```

#### Kan het IP-adres voor de geconfigureerde proxyhost niet oplossen

- Controleer je proxy-instellingen en zorg ervoor dat ze juist zijn.
- Zorg ervoor dat je proxy actief, draaiend en toegankelijk is.

#### Proxytest mislukt

- Je geconfigureerde proxy is niet succesvol getest. Controleer de verstrekte HTTP-fout en/of controleer de logs voor meer details.

#### Systeemtijd loopt meer dan 1 dag achter

- De systeemtijd loopt meer dan 1 dag achter. Geplande taken kunnen mogelijk niet correct worden uitgevoerd totdat de tijd is gecorrigeerd.
- Controleer je systeemtijd en zorg ervoor dat deze is gesynchroniseerd met een betrouwbare tijdserver en nauwkeurig is.

### Downloadclients

#### Geen downloadclient beschikbaar

- Een correct geconfigureerde en ingeschakelde downloadclient is vereist voor Prowlarr om media te kunnen downloaden. Aangezien Prowlarr verschillende downloadclients ondersteunt, moet je bepalen welke het beste bij je eisen past. Als je al een downloadclient hebt geïnstalleerd, moet je Prowlarr configureren om deze te gebruiken en een categorie aan te maken. Zie Instellingen => Downloadclient.

#### Kan niet communiceren met downloadclient

- Prowlarr kon niet communiceren met de geconfigureerde downloadclient. Controleer of de downloadclient operationeel is en controleer de URL. Dit kan ook duiden op een verificatiefout.
- Dit wordt meestal veroorzaakt door een onjuist geconfigureerde downloadclient. Dingen die je meestal kunt controleren:
- Het IP-adres van je downloadclient, als deze op dezelfde fysieke machine staat, is dit meestal 127.0.0.1
- Het poortnummer dat je downloadclient gebruikt, deze zijn ingevuld met het standaard poortnummer, maar als je dit hebt gewijzigd, moet je hetzelfde nummer invoeren in Prowlarr.
- Zorg ervoor dat SSL-versleuteling niet is ingeschakeld als je zowel je Prowlarr-instantie als je downloadclient op een lokaal netwerk gebruikt. Zie de SSL-FAQ voor meer informatie.
- Voor rutorrent zijn speciale instellingenwijzigingen vereist, omdat het https vereist.

#### Downloadclients zijn niet beschikbaar vanwege een storing

- Een of meer van je downloadclients reageren niet op verzoeken van Prowlarr. Daarom heeft Prowlarr besloten om tijdelijk te stoppen met het bevragen van de downloadclient op de normale cyclus van 1 minuut, die normaal gesproken wordt gebruikt om actieve downloads bij te houden en voltooide downloads te importeren. Prowlarr zal echter blijven proberen om downloads naar de client te sturen, maar zal waarschijnlijk falen.
- Je moet Systeem => Logs controleren om te zien wat de reden is voor de fouten.
- Als je deze downloadclient niet meer gebruikt, schakel deze dan uit in Prowlarr om de fouten te voorkomen.

#### Slechte instellingen voor downloadclient

- De locatie waar je downloadclient bestanden downloadt, veroorzaakt problemen. Controleer de logs voor meer informatie. Dit kan te maken hebben met machtigingen of een poging om van Windows naar Linux te gaan of van Linux naar Windows zonder een externe padkoppeling.

### Indexers

#### Indexers hebben geen definitie

- Je indexer(s) hebben geen bestaande definitie (bestand). Dit komt meestal doordat je indexer niet langer wordt ondersteund en is verwijderd of de Cardigann YML-definitie niet langer toegankelijk is.

#### Indexers zijn verouderd

- De definitie van je indexer(s) is verouderd en niet up-to-date. Dit heeft twee mogelijke oorzaken die hieronder worden vermeld.

##### Verouderd door codeveranderingen

- Vanwege codeveranderingen is de definitie van de indexer(s) verouderd zoals momenteel geconfigureerd. Verwijder de indexer uit Prowlarr en voeg deze opnieuw toe om het probleem op te lossen.
- Dit wordt meestal veroorzaakt door het converteren van API's of van YML naar C# of vice versa.

##### Verouderd door verwijdering van sites

- Bepaalde sites kunnen worden verzocht om uit Prowlarr of Jackett te worden verwijderd. Deze kunnen dan als verouderd worden gemarkeerd.
  - [TVVault](https://github.com/Prowlarr/Prowlarr/issues/573) in [Prowlarr #700](https://github.com/Prowlarr/Prowlarr/pull/700)
  - Audiobookbay heeft verzocht dat Prowlarr geen toegang heeft tot hun API
  - Ebookbay heeft verzocht dat Prowlarr geen toegang heeft tot hun API
  - Rarbg is [gestopt met ingang van 2023-05-31](https://torrentfreak.com/iconic-torrent-site-rarbg-shuts-down-all-content-releases-stop-230531/)

#### Geen indexers ingeschakeld

- Prowlarr vereist indexers om nieuwe releases te kunnen ontdekken. Lees de instructies in de wiki over hoe je indexers kunt toevoegen.

#### Indexers zijn niet beschikbaar vanwege fouten

- Er zijn fouten opgetreden bij het gebruik van een van je indexers. Om het aantal herhalingspogingen te beperken, zal Prowlarr de indexer gedurende steeds langere tijd niet gebruiken (tot 24 uur).
- Controleer Evenementen en filter op Waarschuwingen om snel een idee te krijgen van welke problemen zich historisch hebben voorgedaan.
- Dit mechanisme wordt geactiveerd als Prowlarr geen reactie van de indexer kon krijgen (dit kan worden veroorzaakt door DNS, proxy/vpn-verbinding, verificatie of een indexerprobleem), of als Prowlarr het nzb-/torrentbestand niet kon ophalen van de indexer. Bekijk de logs om te bepalen wat voor soort fout het probleem veroorzaakt.
- Je kunt de waarschuwing voorkomen door de betreffende indexer uit te schakelen.
- Voer de test op de indexer uit om Prowlarr te dwingen de indexer opnieuw te controleren, houd er rekening mee dat de waarschuwing van de gezondheidscontrole niet altijd onmiddellijk verdwijnt.

#### Indexer VIP-abonnement verloopt binnen 7 dagen

- Je VIP-abonnement of voordelen bij je indexer verlopen binnen de komende 7 dagen of minder op basis van de vervaldatum die je hebt geconfigureerd voor je indexer in Prowlarr.

#### Indexer VIP-abonnement verlopen

- Je VIP-abonnement of voordelen bij je indexer zijn verlopen op basis van de vervaldatum die je hebt geconfigureerd voor je indexer in Prowlarr.

### Applicaties

#### Applicaties zijn niet beschikbaar vanwege fouten

- Er zijn fouten opgetreden bij het gebruik van een van je applicaties. Om het aantal herhalingspogingen te beperken, zal Prowlarr de applicatie gedurende steeds langere tijd niet gebruiken (tot 24 uur).
- Dit mechanisme wordt geactiveerd als Prowlarr geen reactie van de applicatie kon krijgen (dit kan worden veroorzaakt door DNS, verbinding, verificatie of een applicatieprobleem). Bekijk de logs om te bepalen wat voor soort fout het probleem veroorzaakt.
- Controleer Evenementen en filter op Waarschuwingen om snel een idee te krijgen van welke problemen zich historisch hebben voorgedaan.
- Prowlarr kan geen synchronisatie met de applicatie uitvoeren en het is zeer waarschijnlijk dat de applicatie de indexers van Prowlarr niet kan gebruiken.
- Je kunt de waarschuwing voorkomen door de betreffende applicatie uit te schakelen.
- Voer de test op de applicatie uit om Prowlarr te dwingen de applicatie opnieuw te controleren, houd er rekening mee dat de waarschuwing van de gezondheidscontrole niet altijd onmiddellijk verdwijnt.

## Schijfruimte

In dit gedeelte wordt de beschikbare schijfruimte weergegeven. In Docker kan dit lastig zijn, omdat het meestal de beschikbare ruimte binnen je Docker-image laat zien.

## Over

Hier vind je informatie over je huidige installatie van Prowlarr.

## Meer informatie

Homepagina: Prowlarr's homepagina
Wiki: Je bent hier al
Reddit: r/prowlarr
Discord: Doe mee aan onze Discord
Donaties: Als je vrijgevig bent en wilt doneren, klik dan hier
Donaties aan Sonarr: Als je vrijgevig bent en wilt doneren aan het project dat het allemaal is begonnen, klik dan hier
Broncode: GitHub
Functieverzoeken: Heb je een geweldig idee, deel het hier

# Taken

## Gepland

Deze pagina toont alle geplande taken die Prowlarr uitvoert.

- Toepassingsupdate controleren - Dit wordt uitgevoerd volgens het weergegeven schema in de gebruikersinterface en controleert of Prowlarr de meest recente versie heeft. Vervolgens wordt het update-script geactiveerd om Prowlarr bij te werken. Instellingen => Update

> Opmerking: als je Docker gebruikt, wordt je container niet bijgewerkt, omdat er een nieuwe image moet worden gedownload.
{.is-warning}

- Backup - Dit maakt een back-up van de database van Prowlarr volgens een vast schema. Meer informatie hierover vind je hier. Meer informatie over back-ups vind je bij Systeem => Back-ups.
- Gezondheid controleren - De gezondheidscontrole wordt uitgevoerd volgens het weergegeven schema in de gebruikersinterface en controleert de algehele gezondheid van Prowlarr. Zie de Wiki-invoer over gezondheidscontroles voor een lijst met mogelijke gezondheidsproblemen.
- Onderhoud - Volgens het weergegeven schema in de gebruikersinterface wordt er schoongemaakt, geveegd, gestofzuigd, gedweild, gepoetst en zelfs worden er netjes gevouwen briefjes gemaakt speciaal voor jou. Maar het afval wordt niet weggegooid. Daarvoor wordt gewoon niet genoeg betaald.
- Opruimen van berichten - Volgens het weergegeven schema in de gebruikersinterface worden de berichten die in de linkerbenedenhoek van Prowlarr verschijnen opgeruimd.
  
> Al deze taken kunnen handmatig worden uitgevoerd buiten hun geplande tijden door op het pictogram helemaal rechts van elke taak te klikken.
{.is-info}

## Wachtrij

De wachtrij toont aanstaande taken en een geschiedenis van recent uitgevoerde taken, evenals de duur van die taken.

# Backup

> Deze sectie is meer gericht op de knoppen en het algemene doel van de pagina.
> Als je echter wilt weten hoe je je Prowlarr-instantie kunt back-uppen/herstellen, [zie onze FAQ](/prowlarr/faq).
{.is-info}

Binnen de Back-up sectie krijg je eerdere back-ups te zien (tenzij je een nieuwe installatie hebt gedaan zonder back-ups te maken).

Hier heb je twee opties bovenaan het scherm:

- Nu back-uppen - Deze optie zal een handmatige back-up van de database van Prowlarr triggeren.
- Back-up herstellen - Dit opent een nieuw scherm om te herstellen vanuit een eerdere back-up.
Door "Kies bestand" te selecteren, wordt je browser gevraagd om een dialoogvenster te openen om te herstellen vanuit een Prowlarr Zip-back-up.

Als je eerdere back-ups hebt en ze wilt downloaden van Prowlarr om ze op een niet-standaard locatie te plaatsen, kun je eenvoudig een van deze bestanden selecteren om ze te downloaden.
Aan de rechterkant van elke vorige download heb je twee opties:

- Een - Om te herstellen vanuit een eerdere back-up - Dit opent een nieuw venster om te bevestigen dat je wilt herstellen vanuit deze back-up.
- Twee - Om een eerdere back-up te verwijderen

# Updates

Het update-scherm toont de laatste 5 updates die zijn uitgevoerd, evenals de huidige versie waarop je zit.
Op deze pagina worden ook de update-opmerkingen van de ontwikkelaars weergegeven, waarin wordt vermeld wat er is gerepareerd of toegevoegd aan Prowlarr (Verheug je!)

> Een onderhoudsrelease bevat bugfixes en andere verbeteringen. Bekijk de commitgeschiedenis voor details.
{.is-info}

# Gebeurtenissen

Het tabblad Gebeurtenissen laat zien wat er is gebeurd binnen jouw Prowlarr. Dit kan worden gebruikt om enkele kleine problemen te diagnosticeren. Dit vervangt echter niet de Trace Logs die worden besproken in Logging. Gebeurtenissen zijn het equivalent van INFO-logs.

- Componenten - Deze kolom geeft aan welke component binnen Prowlarr is geactiveerd.
- Bericht - Deze kolom geeft aan welk bericht is verzonden door de component uit de vorige kolom.
- Tandwielicoon - Deze optie stelt je in staat om het aantal componenten/berichten per pagina weer te geven (standaard is 50).
- Opties bovenaan de pagina:
  - Vernieuwen - Deze optie vernieuwt de huidige pagina en haalt een nieuw gebeurtenissenlogboek op.
  - Wissen - Hiermee wordt het huidige gebeurtenissenlogboek gewist, zodat je opnieuw kunt beginnen.

# Logbestanden

Op deze pagina kun je logbestanden downloaden en bekijken die beschikbaar zijn voor Prowlarr.

Op de bovenste rij zijn er verschillende opties om je logbestanden te beheren.

- Op de uiterst linkse positie van de bovenste rij is er een dropdown-menu waarmee je kunt schakelen tussen Logbestanden en Updater Logbestanden.
  - Logbestanden - De essentie van elk ondersteuningsprobleem is hier te vinden.
  - Updater Logbestanden - Dit toont de logbestanden die verband houden met het updater-script van Prowlarr.

> Als je Docker gebruikt, zal dit leeg zijn, omdat je zou moeten updaten door een nieuwe Docker-image te downloaden.
{.is-info}

- Vernieuwen - Hiermee wordt de huidige pagina vernieuwd en worden eventuele nieuw gemaakte logbestanden weergegeven.
- Verwijderen - Hiermee worden alle logbestanden gewist, zodat je opnieuw kunt beginnen.
- Bestandsnaam - Hier wordt de bestandsnaam van het logbestand weergegeven.
- Laatst geschreven - Dit is de lokale tijd waarop dit specifieke logbestand is geschreven.
  - Prowlarr maakt gebruik van roterende logbestanden met een limiet van 1 MB per stuk. Het huidige logbestand is altijd prowlarr.txt, voor de andere bestanden is prowlarr.0.txt de op een na nieuwste (hoe hoger het nummer, hoe ouder het is), totaal maximaal 51 logbestanden. Dit logbestand bevat `fatal`, `error`, `warn` en `info` vermeldingen.
  - Wanneer het debug-logniveau is ingeschakeld, zijn er extra prowlarr.debug.txt roterende logbestanden aanwezig, tot maximaal 51 bestanden. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info` en `debug` vermeldingen. Het beslaat meestal een periode van ongeveer 40 uur.
  - Wanneer het trace-logniveau is ingeschakeld, zijn er extra prowlarr.trace.txt roterende logbestanden aanwezig, tot maximaal 51 bestanden. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info`, `debug` en `trace` vermeldingen. Vanwege de uitgebreide traceerbaarheid beslaat het meestal slechts een paar uur.