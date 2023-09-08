---
title: Readarr Probleemoplossing
description: 
published: true
date: 2023-07-24T19:54:33.343Z
tags: readarr, probleemoplossing
editor: markdown
dateCreated: 2021-06-20T20:06:25.552Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Hulp vragen](#hulp-vragen)
- [Logging en logbestanden](#logging-en-logbestanden)
  - [Standaard loglocatie](#standaard-loglocatie)
  - [Update loglocatie](#update-loglocatie)
  - [Logbestanden delen](#logbestanden-delen)
  - [Trace/Debug logs](#tracedebug-logs)
  - [Logbestanden wissen](#logbestanden-wissen)
- [Meerdere logbestanden](#meerdere-logbestanden)
- [Herstellen na een mislukte update](#herstellen-na-een-mislukte-update)
  - [Het probleem vaststellen](#het-probleem-vaststellen)
    - [Migratieprobleem](#migratieprobleem)
    - [Machtigingsprobleem](#machtigingsprobleem)
  - [Het probleem oplossen](#het-probleem-oplossen)
    - [Machtigingsproblemen](#machtigingsproblemen)
    - [Handmatig upgraden](#handmatig-upgraden)
- [Downloads en importeren](#downloads-en-importeren)
  - [De downloadclient testen](#de-downloadclient-testen)
  - [Een download testen](#een-download-testen)
  - [Een import testen](#een-import-testen)
  - [Veelvoorkomende problemen](#veelvoorkomende-problemen)
    - [Je hebt een voorkeursformaat, maar er is een ander formaat geïmporteerd](#je-hebt-een-voorkeursformaat-maar-er-is-een-ander-formaat-geïmporteerd)
    - [De webinterface van de downloadclient is niet ingeschakeld](#de-webinterface-van-de-downloadclient-is-niet-ingeschakeld)
    - [SSL wordt gebruikt en is verkeerd geconfigureerd](#ssl-wordt-gebruikt-en-is-verkeerd-geconfigureerd)
    - [Kan gedeelde map niet zien op Windows](#kan-gedeelde-map-niet-zien-op-windows)
    - [Toegewezen netwerkstations zijn niet betrouwbaar](#toegewezen-netwerkstations-zijn-niet-betrouwbaar)
    - [Docker en gebruiker, groep, eigendom, machtigingen en paden](#docker-en-gebruiker-groep-eigendom-machtigingen-en-paden)
    - [Externe padtoewijzing](#externe-padtoewijzing)
      - [Externe koppeling of externe synchronisatie (Syncthing)](#externe-koppeling-of-externe-synchronisatie-syncthing)
    - [Machtigingen voor de bibliotheekmap](#machtigingen-voor-de-bibliotheekmap)
    - [Machtigingen voor de downloadmap](#machtigingen-voor-de-downloadmap)
    - [Downloadmap en bibliotheekmap zijn niet verschillende mappen](#downloadmap-en-bibliotheekmap-zijn-niet-verschillende-mappen)
    - [Onjuiste categorie](#onjuiste-categorie)
    - [Ingepakte torrents](#ingepakte-torrents)
    - [Herhaalde downloads](#herhaalde-downloads)
    - [Usenet-download mist import](#usenet-download-mist-import)
    - [Downloadclient wist items](#downloadclient-wist-items)
    - [Download kan niet worden gekoppeld aan een bibliotheekitem](#download-kan-niet-worden-gekoppeld-aan-een-bibliotheekitem)
    - [Verbinding verbroken](#verbinding-verbroken)
  - [Probleem niet vermeld](#probleem-niet-vermeld)
- [Zoeken naar indexers en trackers](#zoeken-naar-indexers-en-trackers)
  - [Logging verhogen naar trace](#logging-verhogen-naar-trace)
  - [Een indexer of tracker testen](#een-indexer-of-tracker-testen)
  - [Een zoekopdracht testen](#een-zoekopdracht-testen)
  - [Veelvoorkomende problemen](#veelvoorkomende-problemen-1)
    - [Media is niet gemonitord](#media-is-niet-gemonitord)
    - [Verkeerde categorieën](#verkeerde-categorieën)
    - [Verkeerde resultaten](#verkeerde-resultaten)
    - [Zoekopdracht succesvol - geen resultaten teruggegeven](#zoekopdracht-succesvol-geen-resultaten-teruggegeven)
    - [Ontbrekende resultaten](#ontbrekende-resultaten)
    - [Certificaatvalidatie](#certificaatvalidatie)
    - [Rate limits bereikt](#rate-limits-bereikt)
    - [IP-blokkade](#ip-blokkade)
    - [De Jackett /all-eindpunt gebruiken](#de-jackett-all-eindpunt-gebruiken)
    - [NZBHydra2 als enkele invoer gebruiken](#nzbhydra2-als-enkele-invoer-gebruiken)
    - [Probleem niet vermeld](#probleem-niet-vermeld-1)
  - [Fouten](#fouten)
    - [De onderliggende verbinding is gesloten: er is een onverwachte fout opgetreden bij het verzenden](#de-onderliggende-verbinding-is-gesloten-er-is-een-onverwachte-fout-opgetreden-bij-het-verzenden)
    - [De aanvraag is verlopen](#de-aanvraag-is-verlopen)
    - [Probleem niet vermeld](#probleem-niet-vermeld-2)

# Hulp vragen

Heb je hulp nodig? Dat is prima, iedereen heeft soms hulp nodig. Je kunt realtime hulp krijgen via de chat op

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiële Readarr Discord*](https://readarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiële Readarr Subreddit*](https://reddit.com/r/readarr)
{.links-list}

Maar voordat je daar naartoe gaat en een bericht plaatst, zorg ervoor dat je verzoek om hulp zo goed mogelijk is. Beschrijf duidelijk het probleem en geef een korte beschrijving van je setup, inclusief zaken zoals je besturingssysteem/distributie, versie van .NET, versie van Readarr, downloadclient en de versie ervan. **Als je [Docker](https://www.docker.com/) gebruikt, doorloop dan eerst de [Docker-gids](/docker-guide), omdat dit veelvoorkomende en frequente pad/machtigingsproblemen oplost. Zorg er anders voor dat je een [docker compose](/docker-guide#docker-compose) bij de hand hebt. [Hoe genereer je een Docker Compose](https://trash-guides.info/compose)** Vertel ons wat je al hebt geprobeerd, waar je naar hebt gekeken. Gebruik de [Logging en logbestanden sectie](#logging-en-logbestanden) om je logging te verhogen naar trace, herhaal het probleem, plak de relevante context in een pastebin en voeg een link naar de pastebin toe in je bericht. Voeg misschien zelfs wat schermafbeeldingen toe om het probleem te verduidelijken.

Hoe meer we weten, hoe gemakkelijker het is om je te helpen.

# Logging en logbestanden

Het is waarschijnlijk ook nuttig om de veelvoorkomende probleemoplossingsproblemen te bekijken:
- [Veelvoorkomende problemen bij downloads en importeren](#veelvoorkomende-problemen)
- [Veelvoorkomende problemen bij het zoeken naar indexers en trackers](#veelvoorkomende-problemen-1)
{.links-list}

Als er om debuglogs wordt gevraagd, bevatten je logs het woord `debug` en als er om trace logs wordt gevraagd, bevatten je logs het woord `trace`. Als de logs die je verstrekt deze woorden niet bevatten, zijn het niet de gevraagde logs.

- Deel niet het volledige logbestand tenzij hierom wordt gevraagd.
- Upload logs niet rechtstreeks naar Discord of plak ze niet als lappen tekst, tenzij hierom wordt gevraagd.
- Deel de logs niet als bijlage, een zip-archief of iets anders dan tekst die wordt gedeeld via de hieronder genoemde services.

Om goede en bruikbare logs te verstrekken:

> Zorg ervoor dat er geen spamtaken worden uitgevoerd, zoals een RSS-verversing
{.is-warning}

1. [Verhoog de logging naar trace (Instellingen => Algemeen => Logniveau of bewerk het configuratiebestand)](#tracedebug-logs)
2. [Wis logs (Systeem => Logs => Logs wissen of verwijder alle logs in de logmap)](#logbestanden-wissen)
3. Reproduceer het probleem (Doe wat het probleem veroorzaakt)
4. [Open het trace logbestand (readarr.trace.txt) via de UI of het logbestand](#standaard-loglocatie) op het bestandssysteem en zoek de relevante context op
5. Kopieer een groot stuk vóór het probleem, het probleem zelf en een groot stuk na het probleem.
6. Gebruik [Gist](https://gist.github.com/), [0bin (**Zorg ervoor dat kleurcodering is uitgeschakeld**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) of vergelijkbare sites - met uitzondering van de hieronder genoemde sites om te vermijden - om de gekopieerde logs hierboven te delen

**Waarschuwingen:**
- **Gebruik [pastebin.com](https://pastebin.com) niet, omdat hun filters de neiging hebben om de logs te blokkeren.
- Gebruik [pastebin.pl](https://pastebin.pl) niet, omdat hun site vaak niet toegankelijk is.
- Gebruik [JustPasteIt](https://justpaste.it/) niet, omdat hun site het bekijken van logs niet vergemakkelijkt.
- Upload je log niet als een bestand.
- Upload en deel je logs niet via Google Drive, Dropbox of een andere site die hierboven niet is genoemd.
- Archiveer je logs niet (zip, tar (tarball), 7zip, enz.).
- Deel geen console-uitvoer, uitvoer van dockercontainers of iets anders dan de gespecificeerde toepassingslogs.

**Belangrijke opmerking:**
- Als je [0bin](https://0bin.net/) gebruikt, zorg er dan voor dat kleurcodering is uitgeschakeld en dat je het bericht niet na het lezen verwijdert.
- Als je op zoek bent naar een specifieke invoer in een oud logbestand, maar niet zeker weet welke, kun je N++ gebruiken. Je kunt de functie "Zoeken in bestanden" van Notepad++ gebruiken om oude logbestanden te doorzoeken indien nodig.
- **Alleen Unix:** Als je op zoek bent naar een specifieke invoer in een oud logbestand, maar niet zeker weet welke, kun je grep gebruiken. Als je bijvoorbeeld informatie wilt vinden over de film/serie/boek/lied/indexer "Shooter", kun je het volgende commando uitvoeren: `grep -inr -C 100 -e 'Shooter' /pad/naar/logs/*.trace*.txt` Als je [Appdata Directory](/readarr/appdata-directory) zich in je home-map bevindt, voer je het volgende uit: `grep -inr -C 100 -e 'Shooter' /home/$Gebruiker/.config/logs/*.trace*.txt`

```none

    * De vlaggen hebben de volgende functies
    * -i: hoofdlettergevoeligheid negeren
    * -n: regelnummer weergeven
    *  -r: recursief alle bestanden in het pad controleren
    * -C: het aantal regels voor en na de gevonden regel opgeven
    * -e: het te zoeken patroon

```

## Standaard loglocatie

De logbestanden bevinden zich in de [Appdata Directory](/readarr/appdata-directory) van Readarr, in de map logs/. Je kunt ook toegang krijgen tot de logbestanden vanuit de UI via Systeem => Logs => Bestanden.

> Let op: De logtabel ("Gebeurtenissen") in de UI is niet hetzelfde als de logbestanden en is niet zo nuttig. Als er om logs wordt gevraagd, kopieer/plak dan uit de logbestanden en niet uit de tabel.
{.is-info}

## Update loglocatie

De update logbestanden bevinden zich in de [Appdata Directory](/readarr/appdata-directory) van Readarr, in de map UpdateLogs/.

## Logbestanden delen

De logbestanden kunnen lang zijn en moeilijk te lezen als onderdeel van een forum- of Reddit-bericht en ze zijn spammy in Discord, dus gebruik alsjeblieft [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) of een andere vergelijkbare pastebin-site. Het hele bestand is meestal niet nodig, alleen een goede hoeveelheid context van vóór en na het probleem/fout. Vergeet niet te wachten tot spamtaken zoals een RSS-synchronisatie of bibliotheekverversing zijn voltooid.

## Trace/Debug logs

Je kunt het logniveau wijzigen via Instellingen => Algemeen => Logging. Readarr hoeft niet opnieuw te worden gestart voor de wijziging van kracht wordt. Deze wijziging heeft alleen invloed op de logbestanden, niet op de loggingdatabase. De nieuwste debug/trace logbestanden hebben respectievelijk de namen `readarr.debug.txt` en `readarr.trace.txt`.

Als je geen toegang hebt tot de UI om het logniveau in te stellen, kun je dit doen door config.xml in de AppData-directory te bewerken en de waarde van LogLevel in te stellen op Debug of Trace in plaats van Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Logbestanden wissen

Je kunt logbestanden en de logdatabase rechtstreeks vanuit de UI wissen, onder Systeem => Logs => Bestanden en Systeem => Logs => Verwijderen (Prullenbakpictogram)

# Meerdere logbestanden

Readarr maakt gebruik van rollende logbestanden met een limiet van 1 MB per stuk. Het huidige logbestand is altijd `readarr.txt`, voor de andere bestanden is `readarr.0.txt` de op een na nieuwste (hoe hoger het nummer, hoe ouder het bestand). Dit logbestand bevat `fatal`, `error`, `warn` en `info` vermeldingen.

Wanneer het debuglogniveau is ingeschakeld, zijn er extra rollende logbestanden aanwezig met de naam `readarr.debug.txt`. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info` en `debug` vermeldingen. Ze beslaan meestal een periode van 40 uur.

Wanneer het tracelogniveau is ingeschakeld, zijn er extra rollende logbestanden aanwezig met de naam `readarr.trace.txt`. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info`, `debug` en `trace` vermeldingen. Vanwege de uitgebreide trace-informatie beslaan ze meestal hooguit een paar uur.

# Herstellen na een mislukte update

We doen er alles aan om problemen bij het upgraden te voorkomen, maar als ze zich voordoen, doorloop dan de volgende stappen om je installatie te herstellen.

## Het probleem vaststellen

- De beste plek om te kijken wanneer de toepassing niet start na een update, is het controleren van de [update logs](#update-loglocatie) en zien of de update succesvol is voltooid. Als er geen probleem is met die logs, kijk dan naar je reguliere toepassingslogbestanden voordat je opnieuw probeert te starten, gebruik [Logging](/readarr/settings#logging) en [Logbestanden](/readarr/system#logbestanden) om ze te vinden en verhoog het logniveau.
- Het meest voorkomende probleem is dat het systeem waarop de app is geïnstalleerd heeft geknoeid met de `/tmp`-map en kritieke \*Arr-bestanden heeft verwijderd tijdens de upgrade, waardoor zowel de upgrade als de rollback zijn mislukt. In dit geval installeer je eenvoudigweg opnieuw op de bestaande beschadigde installatie.

### Migratieprobleem

- Migratiefouten zijn niet identiek, maar hier is een voorbeeld:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Machtigingsprobleem

- Machtigingsproblemen zijn te wijten aan het feit dat de toepassing geen toegang heeft tot de relevante tijdelijke mappen en/of de map met de app-binaries. Los de machtigingen op, zodat de gebruiker/groep waarin de toepassing wordt uitgevoerd de juiste toegang heeft.

- Synology-gebruikers kunnen te maken krijgen met de Synology-bug `Toegang tot het pad '/proc/{een getal}/maps is geweigerd`

- Synology-gebruikers kunnen ook te maken krijgen met een tekort aan ruimte in `/tmp` op bepaalde NAS-apparaten. Je moet een ander pad voor `/tmp` opgeven voor de app. Raadpleeg SynoCommunity of andere Synology-ondersteuningskanalen voor hulp hierbij.

## Het probleem oplossen

Bij een migratieprobleem kun je op dit moment niet veel doen. Als het probleem specifiek voor jou is (of er nog geen berichten zijn), maak dan een bericht aan op [onze subreddit](https://reddit.com/r/readarr) of kom langs in onze [discord](https://readarr.com/discord). Als er anderen zijn met hetzelfde probleem, wees dan gerust dat we eraan werken.

> Zorg ervoor dat je niet hebt geprobeerd een database van `nightly` te gebruiken op de stabiele versie. Het wisselen van branches wordt afgeraden.{.is-info}

### Machtigingsproblemen

- Los de machtigingen op om ervoor te zorgen dat de gebruiker/groep waarin de toepassing wordt uitgevoerd toegang heeft (lezen en schrijven) tot zowel `/tmp` als de installatiemap van de toepassing.

- Voor Synology-gebruikers die problemen ondervinden met `/proc/###/maps` kan het stoppen van Sonarr of de andere \*Arr-toepassingen en het bijwerken ervan dit probleem oplossen. Dit is een probleem met het SynoCommunity-pakket.

### Handmatig upgraden

Download de nieuwste release van onze website.

# Downloads en importeren

Het downloaden en importeren is waar de meeste mensen problemen ervaren. Vanuit een hoog niveau gezien moet Readarr kunnen communiceren met uw downloadclient en toegang hebben tot de bestanden die het downloadt. Er is een grote verscheidenheid aan ondersteunde downloadclients en nog veel meer verschillende configuraties. Dit betekent dat hoewel er enkele veelvoorkomende configuraties zijn, er geen enkele juiste configuratie is en de configuratie van iedereen een beetje anders kan zijn.

> **De eerste stap is om de logboekregistratie te verhogen naar Trace, zie [Logging en logbestanden](#logging-en-logbestanden) voor details over het aanpassen van de logboekregistratie en het doorzoeken van logbestanden. U zult vervolgens het probleem reproduceren en de trace level logs uit die tijdsperiode gebruiken om het probleem te onderzoeken.** Als iemand u helpt, plaats dan de context van voor/na in een [pastebin](https://0bin.net), [Gist](https://gist.com) of een vergelijkbare site om het aan hen te tonen. Het hoeft niet het hele bestand te zijn en het mag niet *alleen* de fout zijn. U moet het probleem ook reproduceren terwijl taken die het logbestand spammen niet worden uitgevoerd.
{.is-danger}

Wanneer u om hulp vraagt, zorg er dan voor dat u [om hulp vraagt](#om-hulp-vragen) zodat u ons kunt voorzien van de benodigde details.

## Testen van de downloadclient

Zorg ervoor dat uw downloadclient(s) actief zijn. Begin met het testen van de downloadclient, als dit niet werkt kunt u gedetailleerde informatie vinden in de logbestanden op trace niveau. U zou een URL moeten vinden die u in uw browser kunt invoeren om te zien of het werkt. Het kan een verbindingsprobleem zijn, wat kan duiden op een verkeerd IP-adres, hostnaam, poort of zelfs een firewall die de toegang blokkeert. Het kan ook voor de hand liggend zijn, zoals een verificatieprobleem waarbij u de gebruikersnaam, het wachtwoord of de API-sleutel verkeerd heeft ingevoerd.

## Testen van een download

Nu gaan we een download proberen, kies een boek en doe een handmatige zoekopdracht. Kies een van die bestanden en probeer het te downloaden. Wordt het naar de downloadclient gestuurd? Komt het terecht in de juiste categorie? Verschijnt het in Activiteit? Komt het terecht in de logbestanden op trace niveau tijdens de taak **Controleren op voltooide download** die ongeveer elke minuut wordt uitgevoerd? Wordt het correct geparseerd tijdens die taak? Heeft de in de wachtrij geplaatste download een redelijke naam? Omdat zoekopdrachten op basis van id worden uitgevoerd op sommige indexers/trackers, kan het er een in de wachtrij plaatsen met een naam die het niet kan herkennen.

## Testen van een import

Importproblemen moeten bijna altijd zichtbaar zijn als een item in Activiteit met een oranje pictogram waarop u kunt hoveren om de fout te zien. Als ze niet verschijnen in Activiteit, moet u zich eerst op dit probleem concentreren en dit oplossen. De meeste importfouten zijn *rechten* problemen, onthoud dat Readarr lees- en schrijfrechten moet hebben in de downloadmap. Soms kunnen ook de rechten in de bibliothekenmap de oorzaak zijn, dus controleer beide.

Onjuiste padproblemen zijn ook mogelijk, maar minder vaak voorkomend in normale configuraties. De sleutel tot het begrijpen van padproblemen is weten dat Readarr het pad naar de download krijgt *van* de downloadclient, via de API ervan. Dit wordt een probleem in meer unieke gevallen, zoals wanneer de downloadclient op een ander systeem draait (misschien zelfs een ander besturingssysteem\!). Het kan ook voorkomen bij een Docker-configuratie, wanneer volumes niet goed zijn geconfigureerd. Een externe padtoewijzing is een goede oplossing wanneer u geen controle heeft, zoals bij een seedbox-configuratie. Bij een Docker-configuratie is het beter om de paden te corrigeren.

## Veelvoorkomende problemen

Hieronder staan enkele veelvoorkomende problemen.

### U geeft de voorkeur aan een bepaald formaat, maar er wordt een ander formaat geïmporteerd

Wanneer Readarr importeert, importeert het op basis van uw prioriteiten in uw kwaliteitsprofiel, ongeacht of ze zijn aangevinkt of niet. Om dit probleem op te lossen, moet u uw aangevinkte formaten naar de bovenkant van de kwaliteitslijst slepen. Bijvoorbeeld, in de onderstaande opties, ook al is alleen EPUB gewenst, als de download een AZW3 bevat samen met de EPUB, zal deze met prioriteit boven de EPUB worden geïmporteerd, waardoor ongewenste formaten worden geïmporteerd.

![qualities.png](/assets/readarr/qualities.png)

### De webinterface van de downloadclient is niet ingeschakeld

Readarr communiceert met uw downloadclient via de API en heeft toegang tot de webinterface van de client. U moet ervoor zorgen dat de webinterface van de client is ingeschakeld en dat de poort die wordt gebruikt niet conflicteert met andere poorten die in gebruik zijn door andere clients of op uw systeem.

### SSL wordt gebruikt en verkeerd geconfigureerd

Zorg ervoor dat SSL-encryptie niet is ingeschakeld als u zowel uw instantie als uw downloadclient op een lokaal netwerk gebruikt. Zie [het SSL FAQ-item](/readarr/faq#ongeldig-certificaat-en-andere-HTTPS-of-SSL-problemen) voor meer informatie.

### Kan gedeelde mappen niet zien op Windows

De standaardgebruiker voor een Windows-service is `LocalService`, die meestal geen toegang heeft tot uw gedeelde mappen. Bewerk de service en stel deze in om als uw eigen gebruiker uit te voeren, zie het FAQ-item [waarom kan ik mijn bestanden op een externe server niet zien](/readarr/faq#waarom-kan-ik-mijn-bestanden-op-een-externe-server-niet-zien) voor meer informatie.

### Toegewezen netwerkstations zijn niet betrouwbaar

Hoewel toegewezen netwerkstations zoals `X:\` handig zijn, zijn ze niet zo betrouwbaar als UNC-paden zoals `\\server\share` en ze zijn ook niet beschikbaar vóór het inloggen. Configureer uw downloadclient(s) zodat ze indien nodig UNC-paden gebruiken. Als uw bibliotheek zich op een gedeelde map bevindt, moet u ervoor zorgen dat uw hoofdmappen UNC-paden gebruiken. Als uw downloadclient naar een gedeelde map stuurt, moet u daar UNC-paden configureren, omdat Readarr het downloadpad van de downloadclient krijgt. Het is prima om uw toegewezen netwerkstations voor uzelf te gebruiken, maar gebruik ze niet voor automatisering.

### Docker en gebruiker, groep, eigendom, rechten en paden

Docker voegt een extra laag complexiteit toe die gemakkelijk verkeerd kan worden geconfigureerd, maar toch eindigt met een configuratie die functioneert, maar verschillende problemen heeft. In plaats van ze hier te bespreken, lees dit wiki-artikel [voor deze automatiseringssoftware en Docker](/docker-guide) dat alles te maken heeft met gebruiker, groep, eigendom, rechten en paden. Het is niet specifiek voor een specifiek Docker-systeem, maar het gaat over zaken op een hoog niveau, zodat u ze in uw eigen omgeving kunt implementeren.

### Extern pad toewijzen

Als u Readarr in Docker heeft en de Download Client in non-Docker (of vice versa) heeft of de programma's op verschillende servers heeft, heeft u mogelijk een extern pad toewijzing nodig.

Logboeken zien er als volgt uit

```none
2022-02-03 14:03:54.3|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /volume3/data/torrents/audiobooks/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Dus `/volume3/data` bestaat niet in de container van Readarr of is niet toegankelijk.

- [Instellingen => Downloadclients => Externe padtoewijzingen](/readarr/settings#remote-path-mappings)
- Een externe padtoewijzing wordt gebruikt wanneer uw downloadclient een pad rapporteert voor voltooide gegevens, hetzij op een andere server, hetzij op een manier die \*Arr niet adresseert naar die map.
- Over het algemeen is een externe padtoewijzing alleen nodig als uw downloadclient op Linux draait terwijl \*Arr op Windows draait of vice versa. Een externe padtoewijzing is mogelijk ook nodig als u Docker- en Native-clients mengt of als u een externe server gebruikt.
- Een externe padtoewijzing is een DOMME zoek/vervang (waarbij het de REMOTE-waarde vindt en vervangt door de LOCAL-waarde voor de opgegeven host).
- Als het foutbericht over een ongeldig pad de VERVANGEN waarde niet bevat, werkt de padtoewijzing niet zoals u verwacht. De gebruikelijke oplossing is om de toewijzing toe te voegen en te verwijderen.
- [Zie TRaSH's handleiding voor aanvullende informatie over externe padtoewijzing](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Als zowel \*Arr als uw Download Client Docker-containers zijn, is een externe padtoewijzing zelden nodig. Het wordt aanbevolen om [de Docker-handleiding](/docker-guide) te bekijken en/of [TRaSH's handleiding](https://trash-guides.info/hardlinks) te volgen.
{.is-info}

#### Externe koppeling of externe synchronisatie (Syncthing)

- U moet ervoor zorgen dat het de hele tijd synchroniseert terwijl het aan het downloaden is. En u moet ervoor zorgen dat de lokale synchronisatiebestemming hardlinks kan zijn wanneer \*Arr importeert, wat betekent dat het hetzelfde bestandssysteem moet zijn en er zo uit moet zien.
  - Synchroniseer op een lager, gemeenschappelijk map die zowel onvolledige als voltooide bestanden bevat.
  - Synchroniseer naar een locatie die lokaal hetzelfde bestandssysteem heeft als uw bibliotheek en er zo uitziet (Docker en netwerkshares maken het gemakkelijk om dit verkeerd te configureren).
  - U wilt de onvolledige en voltooide bestanden synchroniseren, zodat wanneer de torrentclient de verplaatsing uitvoert, dit lokaal wordt weergegeven en alle bestanden al "daar" zijn (zelfs als ze nog steeds worden gedownload). Vervolgens wilt u hardlinks gebruiken, omdat zelfs als het importeert voordat het klaar is, ze nog steeds worden voltooid.
  - Op deze manier wordt er de hele tijd gesynchroniseerd terwijl het wordt gedownload, vervolgens verplaatst de torrentclient naar de tv-submap en wordt de synchronisatie weergegeven. Op deze manier zijn de downloads grotendeels aanwezig wanneer ze als voltooid worden beschouwd. En zelfs als ze nog niet helemaal klaar zijn, betekent de mogelijkheid van de hardlink dat dit nog steeds in orde is.
  - (Optioneel - indien van toepassing en/of vereist (bijv. externe usenetclient)) Configureer een aangepast script dat wordt uitgevoerd bij import/download/upgrade om het externe bestand te verwijderen.
- Een externe koppeling in plaats van een externe synchronisatieopstelling is aanzienlijk minder gecompliceerd te configureren, maar meestal langzamer.
  - Koppel uw externe opslag aan met sshfs of een ander netwerkbestandssysteemprotocol.
  - Zorg ervoor dat de gebruiker en groep waarin \*Arr is geconfigureerd om uit te voeren lees- of schrijftoegang hebben.
  - Configureer een externe padtoewijzing om het REMOTE-pad te vinden en te vervangen door het bijbehorende LOKALE pad.

### Rechten op de bibliotheekmap

Logboeken zien er als volgt uit

```none
2022-02-28 18:51:01.1|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /data/media/books/Jasmine Guillory/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Vergeet niet de rechten en eigendom van de *bestemming* te controleren. Het is gemakkelijk om gefixeerd te raken op de eigendom en rechten van de download en dat is *meestal* de oorzaak van problemen met betrekking tot rechten, maar het *kan* ook de bestemming zijn. Controleer of de bestemmingsmap(pen) bestaan. Controleer of een bestemming *bestand* al bestaat of niet kan worden verwijderd of verplaatst naar de prullenbak. Controleer of eigendom en rechten het kopiëren, hardlinken of verplaatsen van het gedownloade bestand toestaan. De gebruiker of groep die wordt uitgevoerd, moet de rootmap kunnen lezen en schrijven.

- Voor Windows-gebruikers kan dit te wijten zijn aan het draaien als een service:
  - de Windows-service wordt uitgevoerd onder het account 'Local Service', standaard heeft dit account geen toegang tot uw gebruikersmap tenzij er handmatig machtigingen zijn toegewezen. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw gebruikersmap.
  - 'Local Service' heeft over het algemeen ook zeer beperkte rechten. Het is daarom raadzaam om de app als een systeemvaktoepassing te installeren als de gebruiker ingelogd kan blijven. De optie hiervoor wordt tijdens de installatie aangeboden. Zie de FAQ voor instructies over het converteren van een service naar een systeemvaktoepassing.

- Voor Synology-gebruikers zie [SynoCommunity's artikel over machtigingen voor hun pakketten](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Niet-Windows: als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
- Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.

### Rechten op de downloadmap

Logboeken zien er als volgt uit

```none
2022-02-28 18:51:01.1|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /data/torrents/books/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Vergeet niet de rechten en eigendom van de *bron* te controleren. Het is gemakkelijk om gefixeerd te raken op de eigendom en rechten van de bestemming en dat is een *mogelijke* oorzaak van problemen met betrekking tot rechten, maar meestal is het de bron. Controleer of de bronmap(pen) bestaan. Controleer of eigendom en rechten het kopiëren/hardlinken of kopiëren+verwijderen/verplaatsen van het gedownloade bestand toestaan. De gebruiker of groep die wordt uitgevoerd, moet de downloadmap kunnen lezen en schrijven.

- Voor Windows-gebruikers kan dit te wijten zijn aan het draaien als een service:
  - de Windows-service wordt uitgevoerd onder het account 'Local Service', standaard heeft dit account geen toegang tot uw gebruikersmap tenzij er handmatig machtigingen zijn toegewezen. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw gebruikersmap.
  - 'Local Service' heeft over het algemeen ook zeer beperkte rechten. Het is daarom raadzaam om de app als een systeemvaktoepassing te installeren als de gebruiker ingelogd kan blijven. De optie hiervoor wordt tijdens de installatie aangeboden. Zie de FAQ voor instructies over het converteren van een service naar een systeemvaktoepassing.

- Voor Synology-gebruikers zie [SynoCommunity's artikel over machtigingen voor hun pakketten](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Niet-Windows: als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
- Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.

### Downloadmap en bibliotheekmap zijn niet verschillende mappen

De downloadclient moet downloaden naar een map die toegankelijk is voor \*Arr en die niet uw root/bibliotheekmap is; het moet importeren vanuit die aparte downloadmap naar uw bibliotheekmap.

U moet nooit rechtstreeks downloaden naar uw rootmap. U moet uw rootmap ook niet gebruiken als de voltooide map of onvoltooide map van de downloadclient.

[**Dit zal ook een gezondheidscontrole in Systeem veroorzaken**](/readarr/system#downloaden-in-rootmap)

Binnen de applicatie wordt een rootmap gedefinieerd als de geconfigureerde mediabibliotheekmap. Dit is niet de rootmap van een mount. Uw downloadclient heeft een onvoltooide of voltooide map (of verplaatst voltooide downloads) naar uw root (bibliotheek) map. Dit veroorzaakt vaak problemen en wordt afgeraden. Om dit op te lossen, wijzigt u uw downloadclient zodat deze downloads niet plaatst binnen uw rootmap. Let op: 'plaatsen' omvat ook het geval waarin de categorie van uw downloadclient is ingesteld op uw rootmap of als NZBGet/SABnzbd sorteren ingeschakeld heeft en sorteert naar uw rootmap. Houd er rekening mee dat deze controle kijkt naar alle gedefinieerde/geconfigureerde rootmappen, niet alleen naar de rootmappen die momenteel in gebruik zijn. Met andere woorden, de map waarin uw downloadclient downloadt of voltooide downloads verplaatst, mag niet dezelfde map zijn die u heeft geconfigureerd als uw root/bibliotheek/eindbestemmingsmap in de \*Arr-applicatie.

Geconfigureerde rootmappen (ook wel bibliotheekmappen genoemd) kunnen worden gevonden in [Instellingen => Mediabeheer => Rootmappen](/readarr/settings/#root-folders)

Een voorbeeld is als uw downloads naar `\data\downloads` gaan, dan heeft u een rootmap ingesteld als `\data\downloads`.

Het wordt aanbevolen om paden zoals `\data\media\` te gebruiken voor uw root/bibliotheekmap en `\data\downloads\` voor uw downloads.

> Uw downloadmap en uw root/bibliotheekmap MOETEN verschillende mappen zijn.
{.is-warning}

### Onjuiste categorie

Readarr moet worden ingesteld om een categorie te gebruiken, zodat het alleen probeert zijn eigen downloads te verwerken. Het is zeldzaam dat een torrent die door wordt toegevoegd zonder de juiste categorie wordt toegevoegd, maar het kan gebeuren. Als u handmatig torrents toevoegt en ze wilt verwerken, moeten ze de juiste categorie hebben. Dit kan op elk moment worden ingesteld, omdat Readarr probeert downloads elke minuut te verwerken.

### Ingepakte torrents

Logboeken geven fouten aan zoals

```none
No files found are eligible for import
```

Als uw torrent is ingepakt in `.rar`-bestanden, moet u de extractie instellen. We raden [Unpackerr](https://github.com/unpackerr/unpackerr) aan, omdat het uitpakken op de juiste manier doet: het voorkomt beschadigde gedeeltelijke imports en ruimt de uitgepakte bestanden op na import.

De fout kan ook optreden als er geen geldig mediabestand in de map aanwezig is.

### Herhaalde downloads

Er zijn een paar oorzaken van herhaalde downloads, maar een daarvan heeft te maken met de indexerbeperking in Releaseprofielen. Omdat de indexer *niet* wordt opgeslagen bij de gegevens, zijn alle voorkeurswoordscores *nul* voor media in uw bibliotheek, maar tijdens "RSS" en zoeken worden ze toegepast. Dit zorgt ervoor dat u steeds opnieuw de items downloadt omdat het eruitziet als een upgrade, dan niet, dan verschijnt het opnieuw en lijkt het op een upgrade, dan niet. Beperk uw releaseprofiel niet tot een indexer.

Dit kan ook te wijten zijn aan het feit dat de download nooit daadwerkelijk wordt geïmporteerd en vervolgens ontbreekt in de wachtrij, waardoor er steeds opnieuw een nieuwe download wordt gepakt en nooit geïmporteerd. Raadpleeg de verschillende andere veelvoorkomende problemen en probleemoplossingsstappen hiervoor.

### Usenet-download mist import

Readarr kijkt alleen naar de 60 meest recente downloads in SABnzbd en NZBGet, dus als je je geschiedenis *behoudt*, betekent dit dat tijdens grote wachtrijen met importproblemen downloads stilzwijgend kunnen worden gemist en niet geïmporteerd. De beste manier om dit te voorkomen is door je geschiedenis leeg te houden, zodat eventuele items die nog steeds verschijnen, onderzocht moeten worden. Dit kun je bereiken door 'Verwijderen' in te schakelen onder 'Voltooide en mislukte downloadverwerker'. In NZBGet worden items dan verplaatst naar de *verborgen* geschiedenis, wat geweldig is. Helaas heeft SABnzbd geen vergelijkbare functie. Het beste wat je daar kunt bereiken, is het gebruik van de nzb-back-upmap.

### Verwijderen van items door de downloadclient

De downloadclient moet *niet* verantwoordelijk zijn voor het verwijderen van downloads. Usenet-clients moeten zo worden geconfigureerd dat ze downloads *niet* uit de geschiedenis verwijderen. Torrent-clients moeten worden ingesteld zodat ze torrents *niet* verwijderen wanneer ze klaar zijn met seeden (pauzeren of stoppen in plaats daarvan). Dit komt doordat Readarr communiceert met de downloadclient om te weten wat er geïmporteerd moet worden, dus als ze worden *verwijderd*, is er niets om te importeren... zelfs als er een map vol met bestanden is.

Voor SABnzbd wordt dit afgehandeld met de instelling Geschiedenisbehoud.

### Download kan niet worden gekoppeld aan een bibliotheekitem

Om verschillende redenen kunnen releases niet worden geparseerd nadat ze zijn gedownload en naar de downloadclient zijn gestuurd. Activity => Options => Show Unknown (dit is nu standaard ingeschakeld in recente builds) toont alle items die niet anders worden genegeerd / al zijn geïmporteerd binnen de downloadclientcategorie van \*Arr. Deze moeten meestal handmatig worden toegewezen en geïmporteerd.

Dit kan ook voorkomen als je een release in je downloadclient hebt, maar dat mediabestand (film/aflevering/boek/liedje) niet bestaat in de applicatie.

### De onderliggende verbinding is gesloten: Er is een onverwachte fout opgetreden bij het verzenden

Dit wordt veroorzaakt doordat de indexer een SSL-protocol gebruikt dat niet wordt ondersteund door de huidige .NET-versie die wordt gevonden in [Readarr => Systeem => Status](/readarr/system#status).

### De aanvraag is verlopen

Readarr ontvangt geen reactie van de client.

```none
    System.NET.WebException: De aanvraag is verlopen: ’https://example.org/api?t=caps&apikey=(verwijderd) —> System.NET.WebException: De aanvraag is verlopen
```

```none
2022-11-01 10:16:54.3|Waarschuwing|Newznab|Kan geen verbinding maken met indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Een taak is geannuleerd.
```

Dit kan ook worden veroorzaakt door:

- onjuist geconfigureerde of het gebruik van een VPN
- onjuist geconfigureerde of het gebruik van een proxy
- lokale DNS-problemen
- lokale IPv6-problemen - meestal is IPv6 ingeschakeld, maar niet functioneel
- het gebruik van Privoxy en een onjuiste configuratie daarvan

## Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigingen en netwerkproblemen oplossen met behulp van opdrachten [in onze handleiding](/permissions-and-networking). Anders kun je dit bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.

# Zoeken in indexers en trackers

- Als je [Prowlarr](/prowlarr) gebruikt, kun je de [Geschiedenis](/prowlarr/history) van alle zoekopdrachten bekijken die Prowlarr heeft ontvangen en hoe ze naar de sites zijn verzonden. Zorg ervoor dat 'Parameters' is ingeschakeld in Prowlarr History => Options. Het (i)-pictogram biedt aanvullende details.

## Zet logging op trace-niveau

> **De eerste stap is om de logging op trace-niveau te zetten, zie [Logging en logbestanden](#logging-en-logbestanden) voor details over het aanpassen van de logging en het doorzoeken van logs. Je zult vervolgens het probleem reproduceren en de trace-niveau logs uit die tijdsperiode gebruiken om het probleem te onderzoeken.** Als iemand je helpt, plaats dan context van vóór/na in een [pastebin](https://0bin.net), [Gist](https://gist.com) of een vergelijkbare site om het te laten zien. Het hoeft niet het hele bestand te zijn en het mag niet *alleen* de fout zijn. Je moet het probleem ook reproduceren terwijl taken die het logbestand spammen niet worden uitgevoerd.
{.is-danger}

## Testen van een indexer of tracker

Bij het testen van een indexer of tracker kun je in debug- of trace-logs de gebruikte URL vinden. Hieronder staat een voorbeeld van een succesvolle test, waarin je kunt zien dat er een query naar de indexer wordt gestuurd via een specifieke URL met specifieke parameters en vervolgens de respons. Je kunt deze URL in je browser testen door `apikey=(verwijderd)` te vervangen door de juiste apikey, bijvoorbeeld `apikey=123`. Je kunt experimenteren met de parameters als je een foutmelding van de indexer krijgt of controleren of je connectiviteitsproblemen hebt als het helemaal niet werkt. Nadat je het in je eigen browser hebt getest, moet je het testen vanaf het systeem waarop Readarr wordt uitgevoerd *als* je dat nog niet hebt gedaan.

## Testen van een zoekopdracht

Net als bij de indexer/tracker-test hierboven, kun je bij het starten van een zoekopdracht tijdens het loggen op debug- of trace-niveau de gebruikte URL uit de logbestanden halen. Bij het testen is het het beste om zo'n specifiek mogelijke zoekopdracht te gebruiken. Een handmatige zoekopdracht is goed omdat deze specifiek is en je de resultaten in de gebruikersinterface kunt zien terwijl je de logs onderzoekt.

Bij deze test kijk je naar duidelijke fouten en voer je enkele eenvoudige tests uit. Je kunt zien dat de zoekopdracht de URL ***BIJGEWERKTE URL SPECIFIEK VOOR BOEK NODIG - DIT IS EEN VOORBEELD VAN EEN SONARR-URL*** `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(verwijderd)&offset=0&limit=100&tvdbid=354629&season=1&ep=1` heeft gebruikt, die je zelf kunt proberen in een browser nadat je (verwijderd) hebt vervangen door je apikey voor die indexer. Werkt het? Zie je de verwachte resultaten? Is deze FAQ-vermelding van toepassing? In die URL kun je zien dat er specifieke categorieën zijn ingesteld met `cat=5030,5040,5045,5080`, dus als je niet de verwachte resultaten ziet, is dit waarschijnlijk de reden. Je kunt ook zien dat er wordt gezocht op tvdbid met `tvdbid=354629`, dus als de aflevering niet correct is gecategoriseerd op de indexer, moet dit worden opgelost. Je kunt ook zien dat er wordt gezocht op een specifiek seizoen en aflevering met season=1 en ep=1, dus als dat niet correct is op de indexer, zie je die resultaten niet. Kijk naar de XML-uitvoer van handmatige zoekopdrachten hieronder om een voorbeeld te zien van de uitvoer van een werkende query.

- XML-uitvoer van handmatige zoekopdracht

```xml
VOORBEELD VAN INDEXER ZOEKRESPONS NODIG
```

***Afbeeldingen nodig***

![searches-indexers-and-trackers1.png](/assets/readarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/readarr/searches-indexers-and-trackers2.png)

- Fragment van trace-log

```none
Fragment van trace-log voor een handmatige zoekopdracht nodig
```

- Volledig trace-log van een zoekopdracht

```none
Volledige sectie van trace-log voor een handmatige zoekopdracht nodig
```

## Veelvoorkomende problemen

Hieronder staan enkele veelvoorkomende problemen.

### Media is niet gemonitord

Het boek/de boeken is/zijn niet gemonitord.

### Onjuiste categorieën

Onjuiste categorieën zijn waarschijnlijk de meest voorkomende oorzaak van resultaten die worden weergegeven in handmatige zoekopdrachten van een indexer/tracker, maar *niet* in . De indexer/tracker *zou* de categorie moeten weergeven in de zoekresultaten, wat je zou moeten helpen om te achterhalen wat er ontbreekt. Als je Jackett of Prowlarr gebruikt, heeft elke tracker een lijst met specifiek ondersteunde categorieën. Zorg ervoor dat je de juiste categorieën gebruikt voor Categorieën. Veel mensen vinden het handig om de lijst zichtbaar te hebben in één browservenster terwijl ze de invoer in de andere bewerken.

### Onjuiste resultaten

Soms geven indexers volledig niet-gerelateerde resultaten terug, Readarr voert parameters in om de zoekopdracht te beperken, maar de resultaten die worden teruggegeven zijn volledig niet-gerelateerd. Of soms grotendeels gerelateerd met een paar onjuiste resultaten. Het eerste is meestal een probleem met de indexer en je kunt aan de hand van de trace-logs zien welke indexer dit veroorzaakt. Je kunt die indexer uitschakelen en het probleem melden. Het andere probleem heeft meestal te maken met gecategoriseerde releases die moeten worden gemeld bij de indexer/tracker.

### Query succesvol - Geen resultaten teruggegeven

Je ontvangt een bericht vergelijkbaar met `Query succesvol, maar er zijn geen resultaten teruggegeven door je indexer. Dit kan een probleem zijn met de indexer of je indexer-categorie-instellingen.`

Dit wordt veroorzaakt doordat je indexer geen resultaten retourneert die binnen de categorieën vallen die je hebt geconfigureerd voor de indexer.

### Ontbrekende resultaten

Als je resultaten op de site kunt vinden die niet worden weergegeven in Readarr, is het probleem waarschijnlijk een van de volgende mogelijkheden:

- [Categorieën zijn onjuist - zie hierboven](#onjuiste-categorieën)
- Er wordt een zoekopdracht op basis van ID uitgevoerd en de indexer heeft de releases niet correct gekoppeld aan dat ID. Dit is iets wat alleen je indexer kan oplossen. Ze moeten ervoor zorgen dat de release correct wordt gekoppeld aan de juiste toepasselijke id's.
- Je zoekt niet op dezelfde manier als Readarr zoekt; Het is zeer waarschijnlijk dat de termen die je op de indexer zoekt niet overeenkomen met de manier waarop Readarr het doorzoekt. Je kunt zien hoe Readarr zoekt aan de hand van de Trace Logs. Tekstgebaseerde zoekopdrachten hebben over het algemeen het formaat `q=woorden%20en%20dingen%20hier`, deze string is HTTP-gecodeerd en kan eenvoudig worden gedecodeerd met behulp van een online HTML-decoderings/coderingstool.

### Certificaatvalidatie

Je zult verbinding maken met de meeste indexers/trackers via https, dus je hebt dat correct werkend op je systeem nodig. Dat betekent dat je tijdzone en tijd *correct* moeten zijn ingesteld. Het betekent ook dat je systeemcertificaten up-to-date moeten zijn.

### Bereiken van snelheidslimieten

Als je je via een VPN of proxy verbindt, concurreer je mogelijk met 10s of 100s of 1000s andere mensen die allemaal proberen gebruik te maken van diensten zoals , theXEM en/of je indexers en trackers. Snelheidslimieten en DDOS-bescherming worden vaak gedaan op basis van IP-adres en het VPN-/proxy-uitgangspunt is *één* IP-adres. Tenzij je in een repressief land woont zoals China, Australië of Zuid-Afrika, hoef je geen VPN/proxy te gebruiken .

Rarbg heeft de neiging om enige vorm van snelheidslimiet in hun API te hebben en geeft aan dat er geen resultaten zijn.

### IP-blokkade

Vergelijkbaar met snelheidslimieten kan een bepaalde indexer - zoals Nyaa - een IP-adres volledig blokkeren. Dit is meestal semi-permanent en de oplossing is om een nieuw IP-adres van je ISP of VPN-provider te krijgen.

### Het gebruik van de Jackett /all-eindpunt

Het Jackett `/all`-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan problemen veroorzaken, dus het toevoegen van elke tracker afzonderlijk is vereist. Als alternatief kun je kijken naar de Jackett & NZBHydra2-alternatief [Prowlarr](/prowlarr).

[Zelfs Jackett zegt dat /all vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)

Het gebruik van het all-eindpunt heeft geen voordelen (behalve verminderd beheer), alleen nadelen:

- je verliest de controle over specifieke instellingen van indexers (categorieën, zoekmodi, etc.)
- het mixen van zoekmodi (IMDB, query, etc.) kan leiden tot resultaten van lage kwaliteit
- specifieke categorieën van indexers (\>= 100000) kunnen niet worden gebruikt.
- trage indexers vertragen het algehele resultaat
- het totale aantal resultaten is beperkt tot 1000

Door elke indexer afzonderlijk toe te voegen, kun je de categorieën per indexer nauwkeurig afstemmen, wat een probleem kan zijn met het `/all`-eindpunt als het gebruik van de verkeerde categorie fouten veroorzaakt op sommige trackers. In , is elke indexer beperkt tot 1000 resultaten als paginering wordt ondersteund, of 100 als dit niet het geval is, wat betekent dat naarmate je meer en meer trackers aan Jackett toevoegt, je steeds meer kans hebt om resultaten te missen. Ten slotte, als *één* van de trackers in `/all` een fout retourneert, schakelt  deze uit en krijg je nu geen resultaten meer.

### Het gebruik van NZBHydra2 als enkele invoer

Het gebruik van NZBHydra2 als enkele indexer-invoer (bijv. 1 NZBHydra2-invoer in Readarr voor veel indexers in NZBHydra2) in plaats van meerdere (bijv. veel NZBHydra2-invoeren in Readarr voor veel indexers in NZBHydra2) heeft dezelfde problemen als hierboven opgemerkt met het `/all`-eindpunt van Jackett.

### Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigingen en netwerkproblemen oplossen met behulp van opdrachten [in onze handleiding](/permissions-and-networking). Anders kun je dit bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.

## Fouten

Dit zijn enkele veelvoorkomende fouten die je kunt zien bij het toevoegen van een indexer.

### De onderliggende verbinding is gesloten: Er is een onverwachte fout opgetreden bij het verzenden

Dit wordt veroorzaakt doordat de indexer een SSL-protocol gebruikt dat niet wordt ondersteund door de huidige .NET-versie die wordt gevonden in [Readarr => Systeem => Status](/readarr/system#status).

### De aanvraag is verlopen

Readarr ontvangt geen reactie van de indexer.

```none
    System.NET.WebException: De aanvraag is verlopen: ’https://example.org/api?t=caps&apikey=(verwijderd) —> System.NET.WebException: De aanvraag is verlopen
```

```none
2022-11-01 10:16:54.3|Waarschuwing|Newznab|Kan geen verbinding maken met indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Een taak is geannuleerd.
```

Dit kan ook worden veroorzaakt door:

- onjuist geconfigureerde of het gebruik van een VPN
- onjuist geconfigureerde of het gebruik van een proxy
- lokale DNS-problemen
- lokale IPv6-problemen - meestal is IPv6 ingeschakeld, maar niet functioneel
- het gebruik van Privoxy en een onjuiste configuratie daarvan

### Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigingen en netwerkproblemen oplossen met behulp van opdrachten [in onze handleiding](/permissions-and-networking). Anders kun je dit bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.