---
title: Lidarr Probleemoplossing
description: 
published: true
date: 2023-07-24T19:53:24.970Z
tags: lidarr, needs-love, troubleshooting
editor: markdown
dateCreated: 2021-06-14T21:36:46.193Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Hulp vragen](#hulp-vragen)
- [Logging en logbestanden](#logging-en-logbestanden)
  - [Standaard locatie van logbestanden](#standaard-locatie-van-logbestanden)
  - [Locatie van update-logbestanden](#locatie-van-update-logbestanden)
  - [Logbestanden delen](#logbestanden-delen)
  - [Trace/Debug-logbestanden](#tracedebug-logbestanden)
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
    - [Gepakte torrents](#gepakte-torrents)
    - [Herhaalde downloads](#herhaalde-downloads)
    - [Usenet-download mist import](#usenet-download-mist-import)
    - [Downloadclient wist items](#downloadclient-wist-items)
    - [Download kan niet worden gekoppeld aan een bibliotheekitem](#download-kan-niet-worden-gekoppeld-aan-een-bibliotheekitem)
    - [Verbinding verbroken](#verbinding-verbroken)
  - [Probleem niet vermeld](#probleem-niet-vermeld)
- [Zoeken, indexers en trackers](#zoeken-indexers-en-trackers)
  - [Logniveau verhogen naar trace](#logniveau-verhogen-naar-trace)
  - [Een indexer of tracker testen](#een-indexer-of-tracker-testen)
  - [Een zoekopdracht testen](#een-zoekopdracht-testen)
  - [Veelvoorkomende problemen](#veelvoorkomende-problemen-1)
    - [Media is niet gecontroleerd](#media-is-niet-gecontroleerd)
    - [Tracker heeft RawSearch-machtigingen nodig](#tracker-heeft-rawsearch-machtigingen-nodig)
    - [Onjuiste categorieën](#onjuiste-categorieën)
    - [Onjuiste resultaten](#onjuiste-resultaten)
    - [Query succesvol - geen resultaten geretourneerd](#query-succesvol-geen-resultaten-geretourneerd)
    - [Ontbrekende resultaten](#ontbrekende-resultaten)
    - [Certificaatvalidatie](#certificaatvalidatie)
    - [Limieten bereikt](#limieten-bereikt)
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

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiële Lidarr Discord*](https://lidarr.audio/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiële Lidarr Subreddit*](https://reddit.com/r/lidarr)
{.links-list}

Maar voordat je daar naartoe gaat en een bericht plaatst, zorg ervoor dat je verzoek om hulp zo goed mogelijk is. Beschrijf duidelijk het probleem en geef een korte beschrijving van je setup, inclusief zaken zoals je besturingssysteem/distributie, versie van .NET, versie van Lidarr, downloadclient en de versie ervan. **Als je [Docker](https://www.docker.com/) gebruikt, doorloop dan eerst de [Docker-handleiding](/docker-guide), omdat dit veelvoorkomende en frequente pad-/machtigingsproblemen oplost. Zorg er anders voor dat je een [docker compose](/docker-guide#docker-compose) bij de hand hebt. [Hoe je een Docker Compose genereert](https://trash-guides.info/compose)** Vertel ons wat je al hebt geprobeerd, waar je naar hebt gekeken. Gebruik de [Logging en logbestanden sectie](#logging-en-logbestanden) om je logniveau te verhogen naar trace, herhaal het probleem, plak de relevante context in een pastebin en voeg een link naar deze toe in je bericht. Voeg misschien zelfs wat schermafbeeldingen toe om het probleem te verduidelijken.

Hoe meer we weten, hoe gemakkelijker het is om je te helpen.

# Logging en logbestanden

Het is waarschijnlijk ook nuttig om de veelvoorkomende probleemoplossingsproblemen te bekijken:
- [Veelvoorkomende problemen bij downloads en importeren](#veelvoorkomende-problemen)
- [Veelvoorkomende problemen bij zoeken, indexers en trackers](#veelvoorkomende-problemen-1)
{.links-list}

Als je wordt gevraagd om debuglogboeken, bevatten je logboeken `debug` en als je wordt gevraagd om trace-logboeken, bevatten je logboeken `trace`. Als de logboeken die je verstrekt geen van beide bevatten, zijn het niet de gevraagde logboeken.

- Deel niet het volledige logbestand tenzij hierom wordt gevraagd.
- Upload logboeken niet rechtstreeks naar Discord of plak ze niet als tekstblokken, tenzij hierom wordt gevraagd.
- Deel de logboeken niet als bijlage, zip-archief of iets anders dan tekst die wordt gedeeld via de hieronder genoemde services.

Om goede en bruikbare logboeken te verstrekken:

> Zorg ervoor dat er geen spamachtige taak wordt uitgevoerd, zoals een RSS-verversing
{.is-warning}

1. [Verhoog het logniveau naar trace (Instellingen => Algemeen => Logniveau of bewerk het configuratiebestand)](#tracedebug-logbestanden)
2. [Wis logboeken (Systeem => Logboeken => Logboeken wissen of verwijder alle logboeken in de logmap)](#logbestanden-wissen)
3. Reproduceer het probleem (Doe wat het probleem veroorzaakt)
4. [Open het trace-logbestand (Lidarr.trace.txt) via de UI of het logbestand](#standaard-locatie-van-logbestanden) op het bestandssysteem en zoek de relevante context op
5. Kopieer een groot stuk vóór het probleem, het probleem zelf en een groot stuk na het probleem.
6. Gebruik [Gist](https://gist.github.com/), [0bin (**Zorg ervoor dat kleurcodering is uitgeschakeld**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) of vergelijkbare sites - met uitzondering van de hieronder genoemde - om de gekopieerde logboeken hierboven te delen

**Waarschuwingen:**
- **Gebruik [pastebin.com](https://pastebin.com) niet, omdat hun filters de neiging hebben om de logboeken te blokkeren.
- Gebruik [pastebin.pl](https://pastebin.pl) niet, omdat hun site vaak niet toegankelijk is.
- Gebruik [JustPasteIt](https://justpaste.it/) niet, omdat hun site het bekijken van logboeken niet vergemakkelijkt.
- Upload je logboek niet als bestand.
- Upload en deel je logboeken niet via Google Drive, Dropbox of een andere site die hierboven niet is genoemd.
- Archiveer je logboeken niet (zip, tar (tarball), 7zip, enz.).
- Deel geen console-uitvoer, uitvoer van dockercontainer of iets anders dan de gespecificeerde toepassingslogboeken.

**Belangrijke opmerking:**
- Bij gebruik van [0bin](https://0bin.net/) moet je kleurcodering uitschakelen en moet je de logboeken niet na het lezen vernietigen.

- Als alternatief, als je op zoek bent naar een specifieke vermelding in een oud logboekbestand, maar niet zeker weet welke, kun je N++ gebruiken. Je kunt de functie "Zoeken in bestanden" van Notepad++ gebruiken om oude logboekbestanden te doorzoeken indien nodig.
- **Alleen Unix:** Als je op zoek bent naar een specifieke vermelding in een oud logboekbestand, maar niet zeker weet welke, kun je grep gebruiken. Als je bijvoorbeeld informatie wilt vinden over de film/serie/boek/lied/indexer "Shooter", kun je het volgende commando uitvoeren: `grep -inr -C 100 -e 'Shooter' /pad/naar/logboeken/*.trace*.txt` Als je [Appdata Directory](/lidarr/appdata-directory) zich in je home-map bevindt, voer je het volgende uit: `grep -inr -C 100 -e 'Shooter' /home/$Gebruiker/.config/logs/*.trace*.txt`

```none

    * De vlaggen hebben de volgende functies
    * -i: hoofdlettergevoeligheid negeren
    * -n: regelnummer weergeven
    *  -r: recursief alle bestanden in het pad controleren
    * -C: het aantal regels voor en na de gevonden regel opgeven
    * -e: het te zoeken patroon

```

## Standaard locatie van logbestanden

De logbestanden bevinden zich in de [Appdata Directory](/lidarr/appdata-directory) van Lidarr, in de map logs/. Je kunt ook toegang krijgen tot de logbestanden vanuit de UI via Systeem => Logboeken => Bestanden.

> Opmerking: De logboektabel ("Gebeurtenissen") in de UI is niet hetzelfde als de logbestanden en is niet zo nuttig. Als je wordt gevraagd om logboeken, kopieer/plak dan uit de logbestanden en niet uit de tabel.
{.is-info}

## Locatie van update-logbestanden

De update-logbestanden bevinden zich in de [Appdata Directory](/lidarr/appdata-directory) van Lidarr, in de map UpdateLogs/.

## Logbestanden delen

De logboeken kunnen lang zijn en moeilijk te lezen als onderdeel van een forum- of Reddit-bericht en ze zijn spamachtig in Discord, dus gebruik alsjeblieft [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) of een andere vergelijkbare pastebin-site. Het hele bestand is meestal niet nodig, alleen een goede hoeveelheid context van vóór en na het probleem/fout. Vergeet niet te wachten tot spamachtige taken zoals een RSS-synchronisatie of bibliotheekverversing zijn voltooid.

## Trace/Debug-logbestanden

Je kunt het logniveau wijzigen bij Instellingen => Algemeen => Loggen. Lidarr hoeft niet opnieuw te worden gestart voor de wijziging van kracht wordt. Deze wijziging heeft alleen invloed op de logbestanden, niet op de loggingsdatabase. De nieuwste debug/trace-logbestanden hebben respectievelijk de namen `lidarr.debug.txt` en `lidarr.trace.txt`.

Als je geen toegang hebt tot de UI om het logniveau in te stellen, kun je dit doen door config.xml in de AppData-directory te bewerken en de waarde van LogLevel in te stellen op Debug of Trace in plaats van Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Logbestanden wissen

Je kunt logbestanden en de loggingsdatabase rechtstreeks vanuit de UI wissen, onder Systeem => Logboeken => Bestanden en Systeem => Logboeken => Verwijderen (Prullenbakpictogram)

# Meerdere logbestanden

Lidarr maakt gebruik van rollende logbestanden die beperkt zijn tot 1 MB elk. Het huidige logbestand is altijd `lidarr.txt`, voor de andere bestanden is `.0.txt` de op een na nieuwste (hoe hoger het nummer, hoe ouder het bestand). Dit logbestand bevat `fatal`, `error`, `warn` en `info` vermeldingen.

Wanneer het debuglogniveau is ingeschakeld, zijn er extra rollende logbestanden aanwezig met de naam `lidarr.debug.txt`. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info` en `debug` vermeldingen. Ze beslaan meestal een periode van 40 uur.

Wanneer het tracelogniveau is ingeschakeld, zijn er extra rollende logbestanden aanwezig met de naam `lidarr.trace.txt`. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info`, `debug` en `trace` vermeldingen. Vanwege de uitgebreide traceerbaarheid beslaan ze meestal slechts een paar uur.

# Herstellen na een mislukte update

We doen er alles aan om problemen bij het upgraden te voorkomen, maar als ze zich voordoen, leiden deze stappen je door de stappen om je installatie te herstellen.

## Het probleem vaststellen

- De beste plek om te kijken wanneer de toepassing niet start na een update, is het controleren van de [update-logbestanden](#locatie-van-update-logbestanden) en controleren of de update succesvol is voltooid. Als er geen probleem is met de logbestanden, kijk dan naar je reguliere toepassingslogbestanden voordat je opnieuw probeert te starten, gebruik [Logging](/lidarr/settings#logging) en [Logbestanden](/lidarr/system#logbestanden) om ze te vinden en het logniveau te verhogen.
- Het meest voorkomende probleem is dat het systeem waarop de app is geïnstalleerd heeft geknoeid met de `/tmp`-directory en kritieke \*Arr-bestanden heeft verwijderd tijdens de upgrade, waardoor zowel de upgrade als de rollback mislukken. In dit geval hoef je alleen maar opnieuw te installeren op de bestaande defecte installatie.

### Migratieprobleem

- Migratiefouten zijn niet identiek, maar hier is een voorbeeld:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Machtigingsprobleem

- Machtigingsproblemen zijn te wijten aan het feit dat de toepassing geen toegang heeft tot de relevante tijdelijke mappen en/of de app-binmap. Los de machtigingen op, zodat de gebruiker/groep waarin de toepassing wordt uitgevoerd de juiste toegang heeft.

- Synology-gebruikers kunnen te maken krijgen met de Synology-bug `Toegang tot het pad '/proc/{een nummer}/maps is geweigerd`

- Synology-gebruikers kunnen ook te maken krijgen met een tekort aan ruimte in `/tmp` op bepaalde NAS-apparaten. Je moet een ander pad voor `/tmp` opgeven voor de app. Raadpleeg SynoCommunity of andere Synology-ondersteuningskanalen voor hulp hierbij.

## Het probleem oplossen

Bij een migratieprobleem kun je op dit moment niet veel doen. Als het probleem specifiek voor jou is (of er nog geen berichten zijn), maak dan een bericht aan op [onze subreddit](https://reddit.com/r/lidarr) of kom langs op onze [discord](https://lidarr.audio/discord), als er anderen zijn met hetzelfde probleem, wees dan gerust dat we eraan werken.

> Zorg ervoor dat je niet hebt geprobeerd een database van `nightly` te gebruiken op de stabiele versie. Het wisselen van branches wordt afgeraden.{.is-info}

### Machtigingsproblemen

- Los de machtigingen op om ervoor te zorgen dat de gebruiker/groep waarin de toepassing wordt uitgevoerd toegang heeft (lezen en schrijven) tot zowel `/tmp` als de installatiemap van de toepassing.

- Voor Synology-gebruikers die problemen ondervinden met `/proc/###/maps` kan het stoppen van Sonarr of de andere \*Arr-toepassingen en het bijwerken ervan dit probleem oplossen. Dit is een probleem met het SynoCommunity-pakket.

### Handmatig upgraden

Download de nieuwste release van onze website.

# Downloads en importeren

Het downloaden en importeren is waar de meeste mensen problemen ervaren. Vanuit een hoog niveau gezien moet Lidarr kunnen communiceren met uw downloadclient en toegang hebben tot de bestanden die het downloadt. Er is een grote verscheidenheid aan ondersteunde downloadclients en nog veel meer verschillende configuraties. Dit betekent dat hoewel er enkele veelvoorkomende configuraties zijn, er geen enkele juiste configuratie is en de configuratie van iedereen een beetje anders kan zijn.

> **De eerste stap is om de logboekregistratie op te voeren naar Trace, zie [Logging en logbestanden](#logging-en-logbestanden) voor details over het aanpassen van de logboekregistratie en het doorzoeken van logbestanden. U zult vervolgens het probleem reproduceren en de logboekregistratie op trace-niveau van die tijdsperiode gebruiken om het probleem te onderzoeken.** Als iemand u helpt, plaats dan de context van voor/na in een [pastebin](https://0bin.net), [Gist](https://gist.com) of een vergelijkbare site om het te laten zien. Het hoeft niet het hele bestand te zijn en het mag niet *alleen* de fout zijn. U moet het probleem ook reproduceren terwijl taken die het logbestand overspoelen niet worden uitgevoerd.
{.is-danger}

Wanneer u hulp zoekt, zorg er dan voor dat u [hulp vragen](#hulp-vragen) leest, zodat u ons kunt voorzien van de benodigde details.

## Testen van de downloadclient

Zorg ervoor dat uw downloadclient(s) actief zijn. Begin met het testen van de downloadclient. Als het niet werkt, kunt u gedetailleerde informatie vinden in de logboekregistratie op trace-niveau. U zou een URL moeten vinden die u in uw browser kunt invoeren om te zien of het werkt. Het kan een verbindingsprobleem zijn, wat kan duiden op een verkeerd IP-adres, hostname, poort of zelfs een firewall die de toegang blokkeert. Het kan ook voor de hand liggen, zoals een verificatieprobleem waarbij u de gebruikersnaam, het wachtwoord of de API-sleutel verkeerd hebt ingevoerd.

## Testen van een download

Nu gaan we een download proberen. Kies een nummer en doe een handmatige zoekopdracht. Kies een van die bestanden en probeer het te downloaden. Wordt het naar de downloadclient gestuurd? Komt het terecht in de juiste categorie? Verschijnt het in Activiteit? Komt het voor in de logboekregistratie op trace-niveau tijdens de taken **Controleren op voltooide download** (Taken voor het vernieuwen van gemonitorde downloads en het verwerken van gemonitorde downloads) die ongeveer elke minuut worden uitgevoerd? Wordt het correct geparseerd tijdens die taak? Heeft de in de wachtrij geplaatste download een redelijke naam? Omdat zoekopdrachten op basis van id worden uitgevoerd op sommige indexers/trackers, kan het een download in de wachtrij plaatsen met een naam die het niet kan herkennen.

## Testen van een import

Importproblemen moeten bijna altijd zichtbaar zijn als een item in Activiteit met een oranje pictogram waar u overheen kunt zweven om de fout te zien. Als ze niet in Activiteit worden weergegeven, moet u zich eerst op dit probleem concentreren en het oplossen. De meeste importfouten zijn *machtigings*problemen. Onthoud dat Lidarr lees- en schrijftoegang moet hebben tot de downloadmap. Soms kunnen ook machtigingsproblemen in de bibliothekenmap de oorzaak zijn, dus controleer beide.

Onjuiste padproblemen zijn ook mogelijk, maar minder gebruikelijk in normale configuraties. Het sleutelwoord bij het begrijpen van padproblemen is weten dat Lidarr het pad naar de download krijgt *van* de downloadclient, via de API ervan. Dit kan een probleem worden in meer unieke gevallen, zoals wanneer de downloadclient op een ander systeem draait (misschien zelfs een ander besturingssysteem\!). Het kan ook voorkomen bij een Docker-configuratie wanneer de volumes niet goed zijn ingesteld. Een externe padtoewijzing is een goede oplossing wanneer u geen controle hebt, zoals bij een seedbox-configuratie. Bij een Docker-configuratie is het beter om de paden te corrigeren.

## Veelvoorkomende problemen

Hieronder staan enkele veelvoorkomende problemen.

### De webinterface van de downloadclient is niet ingeschakeld

Lidarr communiceert met uw downloadclient via de API en heeft toegang tot de webinterface van de client nodig. Zorg ervoor dat de webinterface van de client is ingeschakeld en dat de poort die wordt gebruikt niet conflicteert met andere poorten die in gebruik zijn door andere clients of op uw systeem.

### SSL wordt gebruikt en is onjuist geconfigureerd

Zorg ervoor dat SSL-versleuteling niet is ingeschakeld als u zowel uw instantie als uw downloadclient op een lokaal netwerk gebruikt. Zie [het SSL-FAQ-item](/lidarr/faq#ongeldig-certificaat-en-andere-https-of-ssl-problemen) voor meer informatie.

### Kan gedeelde mappen niet zien op Windows

De standaardgebruiker voor een Windows-service is `LocalService`, die meestal geen toegang heeft tot uw gedeelde mappen. Bewerk de service en stel deze in om als uw eigen gebruiker uit te voeren, zie het FAQ-item [waarom kan ik mijn bestanden op een externe server niet zien](/lidarr/faq#waarom-kan-ik-mijn-bestanden-op-een-externe-server-niet-zien) voor meer informatie.

### Toegewezen netwerkstations zijn niet betrouwbaar

Hoewel toegewezen netwerkstations zoals `X:\` handig zijn, zijn ze niet zo betrouwbaar als UNC-paden zoals `\\server\share` en ze zijn ook niet beschikbaar vóór het inloggen. Configureer uw downloadclient(s) zodat ze indien nodig UNC-paden gebruiken. Als uw bibliotheek zich op een gedeelde map bevindt, moet u ervoor zorgen dat uw hoofdmappen UNC-paden gebruiken. Als uw downloadclient naar een gedeelde map stuurt, moet u daar UNC-paden configureren, omdat Lidarr het downloadpad van de downloadclient krijgt. Het is prima om uw toegewezen netwerkstations voor uzelf te gebruiken, maar gebruik ze niet voor automatisering.

### Docker en gebruiker, groep, eigendom, machtigingen en paden

Docker voegt een extra laag complexiteit toe die gemakkelijk verkeerd kan worden geconfigureerd, maar toch een functionerende setup oplevert met verschillende problemen. In plaats van ze hier te bespreken, leest u dit wiki-artikel [voor deze automatiseringssoftware en Docker](/docker-guide) dat alles te maken heeft met gebruiker, groep, eigendom, machtigingen en paden. Het is niet specifiek voor een bepaald Docker-systeem, maar het gaat over zaken op een hoog niveau, zodat u ze in uw eigen omgeving kunt implementeren.

### Externe padtoewijzing

Als u Lidarr in Docker heeft en de Downloadclient niet in Docker (of andersom) heeft, of als de programma's op verschillende servers staan, heeft u mogelijk een externe padtoewijzing nodig.

De logboekregistratie ziet er als volgt uit:

```none
2022-02-03 14:03:54.3|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /volume3/data/torrents/music/Five Finger Death Punch - F8 (2020) FLAC. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Dus `/volume3/data` bestaat niet in de container van Lidarr of is niet toegankelijk.

- [Instellingen => Downloadclients => Externe padtoewijzingen](/lidarr/settings#remote-path-mappings)
- Een externe padtoewijzing wordt gebruikt wanneer uw downloadclient een pad rapporteert voor voltooide gegevens op een andere server of op een manier die \*Arr niet behandelt.
- Over het algemeen is een externe padtoewijzing alleen nodig als uw downloadclient op Linux draait terwijl \*Arr op Windows draait, of andersom. Een externe padtoewijzing is ook mogelijk nodig als u Docker- en native clients mixt, of als u een externe server gebruikt.
- Een externe padtoewijzing is een DOMME zoek/vervang (waarbij het de WAARDE OP AFSTAND vindt en vervangt door de LOKALE waarde voor de opgegeven host).
- Als het foutbericht over een ongeldig pad de VERVANGEN waarde niet bevat, werkt de padtoewijzing niet zoals u verwacht. De gebruikelijke oplossing is om de toewijzing toe te voegen en te verwijderen.
- [Zie TRaSH's handleiding voor aanvullende informatie over externe padtoewijzing](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Als zowel \*Arr als uw Downloadclient Docker-containers zijn, is een externe padtoewijzing zelden nodig. Het wordt aanbevolen om [de Docker-handleiding](/docker-guide) te bekijken en/of [TRaSH's handleiding](https://trash-guides.info/hardlinks) te volgen.
{.is-info}

#### Externe koppeling of externe synchronisatie (Syncthing)

- U moet ervoor zorgen dat het de hele tijd synchroniseert terwijl het aan het downloaden is. En u moet ervoor zorgen dat de lokale synchronisatiebestemming harde koppelingen kan zijn wanneer \*Arr importeert, wat betekent dat het hetzelfde bestandssysteem moet zijn en er hetzelfde uit moet zien.
  - Synchroniseer op een lager, gemeenschappelijk mapniveau dat zowel onvolledige als voltooide bestanden bevat.
  - Synchroniseer naar een locatie die lokaal hetzelfde bestandssysteem heeft als uw bibliotheek en er hetzelfde uitziet (Docker en netwerkshares maken het gemakkelijk om dit verkeerd te configureren).
  - U wilt de onvolledige en voltooide bestanden synchroniseren, zodat wanneer de torrentclient de verplaatsing uitvoert, dit lokaal wordt weergegeven en alle bestanden al "daar" zijn (zelfs als ze nog steeds worden gedownload). Vervolgens wilt u harde koppelingen gebruiken, omdat zelfs als ze worden geïmporteerd voordat ze klaar zijn, ze nog steeds worden voltooid.
  - Op deze manier wordt er de hele tijd gesynchroniseerd terwijl er wordt gedownload, vervolgens verplaatst de torrentclient naar de tv-submap en wordt dit weergegeven in de synchronisatie. Op deze manier zijn de downloads grotendeels aanwezig wanneer ze als voltooid worden beschouwd. En zelfs als ze nog niet helemaal klaar zijn, betekent de mogelijkheid van de harde koppeling dat dit nog steeds in orde is.
  - (Optioneel - indien van toepassing en/of vereist (bijv. externe usenetclient)) Configureer een aangepast script dat wordt uitgevoerd bij importeren/downloaden/upgraden om het externe bestand te verwijderen.
- Een externe koppeling in plaats van een externe synchronisatieopstelling is aanzienlijk minder gecompliceerd om te configureren, maar meestal langzamer.
  - Koppel uw externe opslag aan met sshfs of een ander netwerkbestandssysteemprotocol.
  - Zorg ervoor dat de gebruiker en groep waar \*Arr is geconfigureerd om als te worden uitgevoerd lees- of schrijftoegang hebben.
  - Configureer een externe padtoewijzing om het EXTERNE pad te vinden en te vervangen door het LOKALE equivalent.

### Machtigingen op de bibliotheekmap

Logboekregistraties zien er als volgt uit:

```none
2022-02-28 18:51:01.1|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /data/media/music/Jasmine Guillory/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Vergeet niet de machtigingen en eigendom van de *bestemming* te controleren. Het is gemakkelijk om gefixeerd te raken op de eigendom en machtigingen van de download en dat is meestal de oorzaak van machtigingsproblemen, maar het *kan* ook de bestemming zijn. Controleer of de doelfolder(s) bestaan. Controleer of er al een doelbestand bestaat of niet kan worden verwijderd of verplaatst naar de prullenbak. Controleer of de eigendom en machtigingen het kopiëren, harde koppelen of verplaatsen van het gedownloade bestand toestaan. De gebruiker of groep die wordt uitgevoerd, moet de rootmap kunnen lezen en schrijven.

- Voor Windows-gebruikers kan dit te wijten zijn aan het uitvoeren als een service:
  - de Windows-service wordt uitgevoerd onder het account 'Local Service', standaard heeft dit account geen toegang tot uw gebruikersmap, tenzij er handmatig machtigingen zijn toegewezen. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw gebruikersmap.
  - 'Local Service' heeft over het algemeen ook zeer beperkte machtigingen. Het is daarom raadzaam om de app als een systeemvaktoepassing te installeren als de gebruiker ingelogd kan blijven. De optie hiervoor wordt tijdens de installatie aangeboden. Zie de FAQ voor instructies over het converteren van een service naar een systeemvaktoepassing.

- Voor Synology-gebruikers raadpleegt u [het artikel over machtigingen van SynoCommunity voor hun pakketten](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Niet-Windows: als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
- Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.

### Machtigingen op de downloadmap

Logboekregistraties zien er als volgt uit:

```none
2022-02-28 18:51:01.1|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /data/downloads/music/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Vergeet niet de machtigingen en eigendom van de *bron* te controleren. Het is gemakkelijk om gefixeerd te raken op de eigendom en machtigingen van de bestemming en dat is een *mogelijke* oorzaak van machtigingsproblemen, maar meestal is het de bron. Controleer of de bronmap(pen) bestaan. Controleer of de eigendom en machtigingen het kopiëren/hardlinken of kopiëren+verwijderen/verplaatsen van het gedownloade bestand toestaan. De gebruiker of groep die wordt uitgevoerd, moet de downloadmap kunnen lezen en schrijven.

- Voor Windows-gebruikers kan dit te wijten zijn aan het uitvoeren als een service:
  - de Windows-service wordt uitgevoerd onder het account 'Local Service', standaard heeft dit account geen toegang tot uw gebruikersmap, tenzij er handmatig machtigingen zijn toegewezen. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw gebruikersmap.
  - 'Local Service' heeft over het algemeen ook zeer beperkte machtigingen. Het is daarom raadzaam om de app als een systeemvaktoepassing te installeren als de gebruiker ingelogd kan blijven. De optie hiervoor wordt tijdens de installatie aangeboden. Zie de FAQ voor instructies over het converteren van een service naar een systeemvaktoepassing.

- Voor Synology-gebruikers raadpleegt u [het artikel over machtigingen van SynoCommunity voor hun pakketten](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Niet-Windows: als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
- Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.

### Downloadmap en bibliotheekmap zijn dezelfde mappen

De downloadclient moet downloaden naar een map die toegankelijk is voor \*Arr en die niet uw root/bibliotheekmap is; het moet importeren vanuit die aparte downloadmap naar uw bibliotheekmap.

U moet nooit rechtstreeks downloaden naar uw rootmap. U moet uw rootmap ook niet gebruiken als de voltooide map of onvoltooide map van de downloadclient.

[**Dit veroorzaakt ook een gezondheidscontrole in Systeem**](/lidarr/system#downloaden-in-rootmap)

Binnen de applicatie wordt een rootmap gedefinieerd als de geconfigureerde mediabibliotheekmap. Dit is niet de rootmap van een mount. Uw downloadclient heeft een onvoltooide of voltooide map (of verplaatst voltooide downloads) naar uw root (bibliotheek) map. Dit veroorzaakt vaak problemen en wordt afgeraden. Los dit op door uw downloadclient zo te wijzigen dat deze downloads niet in uw rootmap plaatst. Let op: 'plaatsen' omvat ook het geval waarin de categorie van uw downloadclient is ingesteld op uw rootmap of als NZBGet/SABnzbd sorteren ingeschakeld hebben en sorteren naar uw rootmap. Houd er rekening mee dat deze controle kijkt naar alle gedefinieerde/geconfigureerde rootmappen, niet alleen naar de rootmappen die momenteel in gebruik zijn. Met andere woorden, de map waarin uw downloadclient downloadt of voltooide downloads naartoe verplaatst, mag niet dezelfde map zijn die u hebt geconfigureerd als uw root/bibliotheek/eindbestemmingsmap in de \*Arr-applicatie.

Geconfigureerde rootmappen (ook wel bibliotheekmappen genoemd) vindt u in [Instellingen => Mediabeheer => Rootmappen](/lidarr/settings/#root-folders)

Een voorbeeld is als uw downloads naar `\data\downloads` gaan en u een rootmap heeft ingesteld als `\data\downloads`.

Het wordt aanbevolen om paden zoals `\data\media\` te gebruiken voor uw root/bibliotheekmap en `\data\downloads\` voor uw downloads.

> Uw downloadmap en uw root/bibliotheekmap MOETEN apart zijn
{.is-warning}

### Onjuiste categorie

Lidarr moet worden ingesteld om een categorie te gebruiken, zodat het alleen probeert zijn eigen downloads te verwerken. Het is zeldzaam dat een torrent die wordt toegevoegd door \*Arr wordt toegevoegd zonder de juiste categorie, maar het kan voorkomen. Als u handmatig torrents toevoegt en ze wilt verwerken, moeten ze de juiste categorie hebben. Dit kan op elk moment worden ingesteld, omdat \*Arr elke minuut probeert downloads te verwerken.

### Ingepakte torrents

Logboekregistraties geven fouten aan zoals

```none
No files found are eligible for import
```

Als uw torrent is ingepakt in `.rar`-bestanden, moet u de extractie instellen. We raden [Unpackerr](https://github.com/unpackerr/unpackerr) aan, omdat het uitpakken op de juiste manier doet: het voorkomt beschadigde gedeeltelijke imports en ruimt de uitgepakte bestanden op na import.

De fout kan ook optreden als er geen geldig mediabestand in de map aanwezig is.

### Herhaalde downloads

Er zijn verschillende oorzaken van herhaalde downloads, maar een daarvan heeft te maken met de indexeringsbeperking in Releaseprofielen. Omdat de indexer *niet* wordt opgeslagen bij de gegevens, zijn alle voorkeurswoordscores *nul* voor media in uw bibliotheek, maar tijdens "RSS" en zoeken worden ze toegepast. Dit zorgt ervoor dat u steeds opnieuw items downloadt omdat het eruitziet als een upgrade, dan niet, dan verschijnt het opnieuw en lijkt het op een upgrade, dan is het dat niet. Beperk uw releaseprofiel niet tot een indexer.

Dit kan ook te wijten zijn aan het feit dat de download nooit daadwerkelijk wordt geïmporteerd en vervolgens ontbreekt in de wachtrij, waardoor een nieuwe download voortdurend wordt opgepakt en nooit wordt geïmporteerd. Raadpleeg de verschillende andere veelvoorkomende problemen en probleemoplossingsstappen hiervoor.

### Usenet-download wordt niet geïmporteerd

Lidarr kijkt alleen naar de 60 meest recente downloads in SABnzbd en NZBGet, dus als u uw geschiedenis *behoudt*, betekent dit dat tijdens grote wachtrijen met importproblemen downloads stilzwijgend kunnen worden gemist en niet worden geïmporteerd. De beste manier om dat te voorkomen, is door uw geschiedenis leeg te houden, zodat eventuele items die nog steeds verschijnen, moeten worden onderzocht. U kunt dit bereiken door Verwijderen in te schakelen onder Voltooide en mislukte downloadverwerking. In NZBGet worden items dan verplaatst naar de *verborgen* geschiedenis, wat geweldig is. Helaas heeft SABnzbd geen vergelijkbare functie. Het beste wat u daar kunt doen, is de nzb-back-upmap gebruiken.

### Downloadclient wist items

De downloadclient moet *niet* verantwoordelijk zijn voor het verwijderen van downloads. Usenet-clients moeten zo worden geconfigureerd dat ze downloads niet uit de geschiedenis verwijderen. Torrent-clients moeten zo worden ingesteld dat ze torrents niet verwijderen wanneer ze klaar zijn met seeden (pauzeren of stoppen in plaats daarvan). Dit komt doordat Lidarr communiceert met de downloadclient om te weten wat er geïmporteerd moet worden, dus als ze worden *verwijderd*, is er niets om te importeren... zelfs als er een map vol met bestanden is.

Voor SABnzbd wordt dit afgehandeld met de instelling Geschiedenisbehoud.

### Download kan niet worden gekoppeld aan een bibliotheekitem

Om verschillende redenen kunnen releases niet worden geparseerd nadat ze zijn gedownload en naar de downloadclient zijn gestuurd. Activiteit => Opties => Onbekend weergeven (dit is nu standaard ingeschakeld in recente builds) toont alle items die niet anders worden genegeerd / al zijn geïmporteerd binnen de downloadclientcategorie van Lidarr. Deze moeten meestal handmatig worden toegewezen en geïmporteerd.

Dit kan ook voorkomen als je een release in je downloadclient hebt, maar dat mediabestand (film/aflevering/boek/liedje) niet bestaat in de applicatie.

### De onderliggende verbinding is gesloten: Er is een onverwachte fout opgetreden bij het verzenden

Dit wordt veroorzaakt doordat de indexer een SSL-protocol gebruikt dat niet wordt ondersteund door de huidige .NET-versie die wordt gevonden in [Lidarr => Systeem => Status](/lidarr/system#status).

### De aanvraag is verlopen

Lidarr ontvangt geen reactie van de client.

```none
    System.NET.WebException: De aanvraag is verlopen: ’https://example.org/api?t=caps&apikey=(verwijderd) —> System.NET.WebException: De aanvraag is verlopen
```

```none
2022-11-01 10:16:54.3|Waarschuwing|Newznab|Kan geen verbinding maken met indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Een taak is geannuleerd.
```

Dit kan ook worden veroorzaakt door:

- onjuist geconfigureerde of gebruikte VPN
- onjuist geconfigureerde of gebruikte proxy
- lokale DNS-problemen - Probeer over te schakelen naar een andere DNS-provider
- lokale IPv6-problemen - meestal is IPv6 ingeschakeld, maar niet functioneel
- het gebruik van Privoxy en onjuiste configuratie ervan

## Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigings- en netwerkproblemen oplossen met behulp van de opdrachten in onze handleiding. Anders kun je het probleem bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.

# Zoeken in indexers en trackers

- Als je [Prowlarr](/prowlarr) gebruikt, kun je de [Geschiedenis](/prowlarr/history) van alle query's bekijken die Prowlarr heeft ontvangen en hoe ze naar de sites zijn verzonden. Zorg ervoor dat `Parameters` is ingeschakeld in Prowlarr Geschiedenis => Opties. Het (i)-pictogram biedt aanvullende details.

## Zet het loggen op trace-niveau

> **De eerste stap is om het loggen op trace-niveau te zetten, zie [Logging en logbestanden](#logging-en-logbestanden) voor details over het aanpassen van het loggen en het doorzoeken van logbestanden. Je zult dan het probleem reproduceren en de logbestanden op trace-niveau uit die tijdsperiode gebruiken om het probleem te onderzoeken.** Als iemand je helpt, plaats dan context van vóór/na in een [pastebin](https://0bin.net), [Gist](https://gist.com) of een vergelijkbare site om het te laten zien. Het hoeft niet het hele bestand te zijn en het mag niet *alleen* de fout zijn. Je moet het probleem ook reproduceren terwijl taken die het logbestand spammen niet worden uitgevoerd.
{.is-danger}

## Testen van een indexer of tracker

Bij het testen van een indexer of tracker kun je in debug- of trace-logs de gebruikte URL vinden. Hieronder staat een voorbeeld van een succesvolle test, waarin je kunt zien dat er een query naar de indexer wordt gestuurd via een specifieke URL met specifieke parameters en vervolgens de reactie. Je kunt deze URL in je browser testen door `apikey=(verwijderd)` te vervangen door de juiste apikey, bijvoorbeeld `apikey=123`. Je kunt experimenteren met de parameters als je een foutmelding van de indexer krijgt of controleren of je connectiviteitsproblemen hebt als het helemaal niet werkt. Nadat je het in je eigen browser hebt getest, moet je het testen vanaf het systeem waarop Lidarr wordt uitgevoerd *als* je dat nog niet hebt gedaan.

## Testen van een zoekopdracht

Net als bij de indexer/tracker-test hierboven, wanneer je een zoekopdracht start terwijl je logbestanden op debug- of trace-niveau hebt ingesteld, kun je de gebruikte URL uit de logbestanden halen. Bij het testen is het het beste om zo'n specifiek mogelijke zoekopdracht te gebruiken. Een handmatige zoekopdracht is goed omdat deze specifiek is en je de resultaten in de gebruikersinterface kunt zien terwijl je de logbestanden bekijkt.

Bij deze test kijk je naar duidelijke fouten en voer je enkele eenvoudige tests uit. Je kunt zien dat de zoekopdracht de URL ***BIJGEWERKTE URL VOOR MUZIEK NODIG - DIT IS EEN VOORBEELD VAN EEN SONARR-URL*** `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(verwijderd)&offset=0&limit=100&tvdbid=354629&season=1&ep=1` heeft gebruikt, die je zelf kunt proberen in een browser nadat je (verwijderd) hebt vervangen door je apikey voor die indexer. Werkt het? Zie je de verwachte resultaten? Is deze FAQ van toepassing? In die URL kun je zien dat er specifieke categorieën zijn ingesteld met `cat=5030,5040,5045,5080`, dus als je de verwachte resultaten niet ziet, is dit waarschijnlijk de reden. Je kunt ook zien dat er wordt gezocht op tvdbid met `tvdbid=354629`, dus als de aflevering niet correct is gecategoriseerd op de indexer, moet dit worden opgelost. Je kunt ook zien dat er wordt gezocht op een specifiek seizoen en aflevering met season=1 en ep=1, dus als dat niet correct is op de indexer, zie je die resultaten niet. Kijk bij Handmatige zoekopdracht XML-uitvoer hieronder voor een voorbeeld van de uitvoer van een werkende query.

- Handmatige zoekopdracht XML-uitvoer

```xml
VOORBEELD VAN INDEXER ZOEKRESULTAAT NODIG
```

***Afbeeldingen nodig***

![searches-indexers-and-trackers1.png](/assets/lidarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/lidarr/searches-indexers-and-trackers2.png)

- Fragment van trace-logboek

```none
Fragment van trace-logboek voor een handmatige zoekopdracht nodig
```

- Volledig trace-logboek van een zoekopdracht

```none
Volledige sectie van trace-logboek voor een handmatige zoekopdracht nodig
```

## Veelvoorkomende problemen

Hieronder staan enkele veelvoorkomende problemen.

### Media is niet gevolgd

Het nummer(s) is/zijn niet gevolgd.

### Tracker heeft RawSearch-caps nodig

- Lidarr zoekt naar `Kikis Delivery Service`, maar je tracker heeft alleen resultaten voor `Kiki's Delivery Service`.
- Dit komt doordat je tracker geen normale gestandaardiseerde zoekopdrachten ondersteunt.
- De oplossing is dat de zoekmogelijkheden van de definitie van je tracker moeten worden bijgewerkt om aan te geven dat het `RawSearch` vereist en ondersteunt.
- Jackett ondersteunt de vlag, maar de mogelijkheden moeten per indexer worden bijgewerkt. Dien een functieverzoek in bij Jackett om deze functionaliteit toe te voegen voor je indexer.
- Prowlarr ondersteunt de vlag, maar de mogelijkheden moeten per indexer worden bijgewerkt. Dien een functieverzoek in bij Prowlarr om deze functionaliteit toe te voegen voor je indexer.

### Verkeerde categorieën

Onjuiste categorieën zijn waarschijnlijk de meest voorkomende oorzaak van resultaten die worden weergegeven in handmatige zoekopdrachten van een indexer/tracker, maar *niet* in Lidarr. De indexer/tracker *zou* de categorie moeten tonen in de zoekresultaten, wat je zou moeten helpen om te achterhalen wat er ontbreekt. Als je Jackett of Prowlarr gebruikt, heeft elke tracker een lijst met specifiek ondersteunde categorieën. Zorg ervoor dat je de juiste categorieën gebruikt. Veel mensen vinden het handig om de lijst zichtbaar te hebben in één browservenster terwijl ze de invoer in een ander venster bewerken.

### Verkeerde resultaten

Soms geven indexers volledig niet-gerelateerde resultaten terug, terwijl Lidarr parameters doorgeeft om de zoekopdracht te beperken. Of soms gedeeltelijk gerelateerde resultaten met een paar onjuiste resultaten. Het eerste is meestal een probleem met de indexer en je kunt aan de hand van de trace-logboeken zien welke indexer dit veroorzaakt. Je kunt die indexer uitschakelen en het probleem melden. Het andere probleem heeft meestal te maken met gecategoriseerde releases die moeten worden gemeld bij de indexer/tracker.

### Query succesvol - Geen resultaten teruggegeven

Je ontvangt een bericht vergelijkbaar met `Query succesvol, maar er zijn geen resultaten teruggegeven door je indexer. Dit kan een probleem zijn met de indexer of je indexer-categorie-instellingen.`

Dit wordt veroorzaakt doordat je indexer geen resultaten retourneert die binnen de categorieën vallen die je hebt geconfigureerd voor de indexer.

### Ontbrekende resultaten

Als je resultaten op de site kunt vinden die niet worden weergegeven in Lidarr, is het probleem waarschijnlijk een van de volgende mogelijkheden:

- [Categorieën zijn onjuist - zie hierboven](#verkeerde-categorieën)
- Er wordt een ID-gebaseerde zoekopdracht uitgevoerd en de indexer heeft de releases niet correct gekoppeld aan die ID. Dit is iets wat alleen je indexer kan oplossen. Ze moeten ervoor zorgen dat de release correct wordt gekoppeld aan de juiste toepasselijke id's.
- Je zoekt niet op dezelfde manier als Lidarr zoekt; Het is zeer waarschijnlijk dat de termen die je op de indexer zoekt niet overeenkomen met de manier waarop Lidarr het doorzoekt. Je kunt zien hoe Lidarr het doorzoekt in de trace-logboeken. Tekstgebaseerde zoekopdrachten hebben over het algemeen het formaat `q=woorden%20en%20dingen%20hier`, deze string is HTTP-gecodeerd en kan eenvoudig worden gedecodeerd met behulp van een online HTML-decoderings/coderingstool.

### Certificaatvalidatie

Je zult verbinding maken met de meeste indexers/trackers via https, dus je hebt dat correct nodig op je systeem. Dat betekent dat je tijdzone en tijd *correct* moeten zijn ingesteld. Het betekent ook dat je systeemcertificaten up-to-date moeten zijn.

### Overschrijding van de limiet

Als je je via een VPN of proxy verbindt, concurreer je mogelijk met 10s, 100s of 1000s andere mensen die allemaal proberen gebruik te maken van diensten zoals Lidarr, theXEM en/of je indexers en trackers. Beperking van de snelheid en DDoS-bescherming worden vaak gedaan op basis van IP-adres en het uitgangspunt van je VPN/proxy is *één* IP-adres. Tenzij je in een repressief land woont zoals China, Australië of Zuid-Afrika, hoef je geen VPN/proxy te gebruiken.

Rarbg heeft de neiging om enige vorm van snelheidsbeperking in hun API te hebben en geeft aan dat er geen resultaten zijn.

### IP-blokkade

Vergelijkbaar met snelheidslimieten kan een bepaalde indexer - zoals Nyaa - een IP-adres volledig blokkeren. Dit is meestal semi-permanent en de oplossing is om een nieuw IP-adres van je internetprovider of VPN-provider te krijgen.

### Het gebruik van de Jackett /all-eindpunt

Het Jackett `/all`-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan problemen veroorzaken, dus het toevoegen van elke tracker afzonderlijk is vereist. Als alternatief kun je overwegen om de alternatieve combinatie van Jackett & NZBHydra2 [Prowlarr](/prowlarr) te gebruiken.

[Zelfs Jackett zegt dat /all vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)

Het gebruik van het all-eindpunt heeft geen voordelen (behalve verminderd beheer), alleen nadelen:

- je verliest de controle over specifieke instellingen van de indexer (categorieën, zoekmodi, enz.)
- het mixen van zoekmodi (IMDB, query, enz.) kan leiden tot resultaten van lage kwaliteit
- indexer-specifieke categorieën (\>= 100000) kunnen niet worden gebruikt.
- trage indexers vertragen het algehele resultaat
- het totale aantal resultaten is beperkt tot 1000

Door elke indexer afzonderlijk toe te voegen, kun je de categorieën per indexer nauwkeurig afstemmen, wat een probleem kan zijn met het `/all`-eindpunt als het gebruik van de verkeerde categorie fouten veroorzaakt op sommige trackers. In , is elke indexer beperkt tot 1000 resultaten als paginering wordt ondersteund, of 100 als dit niet het geval is, wat betekent dat naarmate je meer en meer trackers aan Jackett toevoegt, je steeds meer kans hebt om resultaten te missen. Ten slotte, als *één* van de trackers in `/all` een fout retourneert, schakelt Lidarr deze uit en krijg je nu geen resultaten meer.

### Het gebruik van NZBHydra2 als enkele invoer

Het gebruik van NZBHydra2 als enkele indexer-invoer (d.w.z. 1 NZBHydra2-invoer in Lidarr voor veel indexers in NZBHydra2) in plaats van meerdere (d.w.z. veel NZBHydra2-invoeren in Lidarr voor veel indexers in NZBHydra2) heeft dezelfde problemen als hierboven opgemerkt met het `/all`-eindpunt van Jackett.

### Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigings- en netwerkproblemen oplossen met behulp van de opdrachten in onze handleiding. Anders kun je het probleem bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.

## Fouten

Dit zijn enkele veelvoorkomende fouten die je kunt zien bij het toevoegen van een indexer.

### De onderliggende verbinding is gesloten: Er is een onverwachte fout opgetreden bij het verzenden

Dit wordt veroorzaakt doordat de indexer een SSL-protocol gebruikt dat niet wordt ondersteund door de huidige .NET-versie die wordt gevonden in [Lidarr => Systeem => Status](/lidarr/system#status).

### De aanvraag is verlopen

Lidarr ontvangt geen reactie van de indexer.

```none
    System.NET.WebException: De aanvraag is verlopen: ’https://example.org/api?t=caps&apikey=(verwijderd) —> System.NET.WebException: De aanvraag is verlopen
```

```none
2022-11-01 10:16:54.3|Waarschuwing|Newznab|Kan geen verbinding maken met indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Een taak is geannuleerd.
```

Dit kan ook worden veroorzaakt door:

- onjuist geconfigureerde of gebruikte VPN
- onjuist geconfigureerde of gebruikte proxy
- lokale DNS-problemen - Probeer over te schakelen naar een andere DNS-provider
- lokale IPv6-problemen - meestal is IPv6 ingeschakeld, maar niet functioneel
- het gebruik van Privoxy en onjuiste configuratie ervan

### Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigings- en netwerkproblemen oplossen met behulp van de opdrachten in onze handleiding. Anders kun je het probleem bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.