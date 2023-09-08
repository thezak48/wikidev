---
title: Sonarr Probleemoplossing
description: 
published: true
date: 2023-07-24T19:54:54.368Z
tags: sonarr, probleemoplossing
editor: markdown
dateCreated: 2021-06-20T19:13:01.108Z
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
    - [Eén of meer verwachte afleveringen in de release zijn niet geïmporteerd of ontbreken](#één-of-meer-verwachte-afleveringen-in-de-release-zijn-niet-geïmporteerd-of-ontbreken)
    - [Gebruik van Sonarr v2](#gebruik-van-sonarr-v2)
    - [WebUI van de downloadclient is niet ingeschakeld](#webui-van-de-downloadclient-is-niet-ingeschakeld)
    - [SSL in gebruik en verkeerd geconfigureerd](#ssl-in-gebruik-en-verkeerd-geconfigureerd)
    - [Kan share niet zien op Windows](#kan-share-niet-zien-op-windows)
    - [Toegewezen netwerkstations zijn niet betrouwbaar](#toegewezen-netwerkstations-zijn-niet-betrouwbaar)
    - [Docker en gebruiker, groep, eigendom, machtigingen en paden](#docker-en-gebruiker-groep-eigendom-machtigingen-en-paden)
    - [Externe padkoppeling](#externe-padkoppeling)
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
      - [Gevonden overeenkomende serie via grab-geschiedenis, maar serie werd gekoppeld op basis van serie-ID. Automatische import is niet mogelijk](#gevonden-overeenkomende-serie-via-grab-geschiedenis-maar-serie-werd-gekoppeld-op-basis-van-serie-id-automatische-import-is-niet-mogelijk)
    - [Afleveringsnaam is TBA](#afleveringsnaam-is-tba)
    - [Verbindingstime-out](#verbindingstime-out)
  - [Probleem niet vermeld](#probleem-niet-vermeld)
- [Zoeken naar indexers en trackers](#zoeken-naar-indexers-en-trackers)
  - [Logging verhogen naar trace](#logging-verhogen-naar-trace)
  - [Een indexer of tracker testen](#een-indexer-of-tracker-testen)
  - [Een zoekopdracht testen](#een-zoekopdracht-testen)
  - [Veelvoorkomende problemen](#veelvoorkomende-problemen-1)
    - [Indexers worden niet doorzocht](#indexers-worden-niet-doorzocht)
    - [Slecht genoemde releases](#slecht-genomede-releases)
    - [Tracker heeft RawSearch-mogelijkheden nodig](#tracker-heeft-rawsearch-mogelijkheden-nodig)
    - [Serie heeft een alias nodig](#serie-heeft-een-alias-nodig)
    - [Serie heeft een XEM-koppeling nodig](#serie-heeft-een-xem-koppeling-nodig)
    - [Onjuist serie-type](#onjuist-serie-type)
      - [Dagelijks](#dagelijks)
      - [Standaard](#standaard)
      - [Anime](#anime)
    - [Media is niet gemonitord](#media-is-niet-gemonitord)
    - [Zoekopdracht succesvol - geen resultaten geretourneerd](#zoekopdracht-succesvol-geen-resultaten-geretourneerd)
    - [Onjuiste categorieën](#onjuiste-categorieën)
    - [Onjuiste resultaten](#onjuiste-resultaten)
    - [Ontbrekende resultaten](#ontbrekende-resultaten)
    - [Certificaatvalidatie](#certificaatvalidatie)
    - [Limieten bereikt](#limieten-bereikt)
    - [IP-blokkade](#ip-blokkade)
    - [De Jackett /all-eindpunt gebruiken](#de-jackett-all-eindpunt-gebruiken)
    - [NZBHydra2 gebruiken als enkele invoer](#nzbhydra2-gebruiken-als-enkele-invoer)
    - [Indexer wordt niet doorzocht](#indexer-wordt-niet-doorzocht)
    - [Jackett handmatige zoekopdracht vindt meer resultaten](#jackett-handmatige-zoekopdracht-vindt-meer-resultaten)
    - [Releaseprofielen worden niet gerespecteerd](#releaseprofielen-worden-niet-gerespecteerd)
    - [Probleem niet vermeld](#probleem-niet-vermeld-1)
  - [Fouten](#fouten)
    - [De onderliggende verbinding is gesloten: Er is een onverwachte fout opgetreden bij het verzenden](#de-onderliggende-verbinding-is-gesloten-er-is-een-onverwachte-fout-opgetreden-bij-het-verzenden)
    - [De aanvraag is verlopen](#de-aanvraag-is-verlopen)
    - [Probleem niet vermeld](#probleem-niet-vermeld-2)

# Hulp vragen

Heb je hulp nodig? Dat is prima, iedereen heeft soms hulp nodig. Je kunt realtime hulp krijgen via de chat op

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiële Sonarr Discord*](https://discord.sonarr.tv/)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiële Sonarr Subreddit*](https://reddit.com/r/sonarr)
{.links-list}

Maar voordat je daar naartoe gaat en een bericht plaatst, zorg ervoor dat je verzoek om hulp zo goed mogelijk is. Beschrijf duidelijk het probleem en geef een korte beschrijving van je setup, inclusief zaken zoals je besturingssysteem/distributie, versie van .net/Mono, versie van Sonarr, downloadclient en de versie ervan. **Als je [Docker](https://www.docker.com/) gebruikt, doorloop dan eerst de [Docker-gids](/docker-guide), omdat dit veelvoorkomende en frequente pad/machtigingsproblemen oplost. Zorg er anders voor dat je een [docker compose](/docker-guide#docker-compose) bij de hand hebt. [Hoe genereer je een Docker Compose](https://trash-guides.info/compose)** Vertel ons wat je al hebt geprobeerd, waar je naar hebt gekeken. Gebruik de [Logging en logbestanden sectie](#logging-en-logbestanden) om je logging te verhogen naar trace, herhaal het probleem, plak de relevante context in een pastebin en voeg een link hiernaar toe in je bericht. Voeg misschien zelfs wat schermafbeeldingen toe om het probleem te verduidelijken.

Hoe meer we weten, hoe gemakkelijker het is om je te helpen.

# Logging en logbestanden

Het is waarschijnlijk ook nuttig om de veelvoorkomende probleemoplossingsproblemen te bekijken:
- [Veelvoorkomende problemen bij downloads en importeren](#veelvoorkomende-problemen)
- [Veelvoorkomende problemen bij het zoeken naar indexers en trackers](#veelvoorkomende-problemen-1)
{.links-list}

Als je wordt gevraagd om debuglogs, bevatten je logs het woord `debug` en als je wordt gevraagd om trace logs, bevatten je logs het woord `trace`. Als de logs die je verstrekt deze woorden niet bevatten, zijn het niet de gevraagde logs.

- Deel niet het volledige logbestand tenzij hierom wordt gevraagd.
- Upload logs niet rechtstreeks naar Discord of plak ze niet als grote lappen tekst, tenzij hierom wordt gevraagd.
- Deel de logs niet als bijlage, een zip-archief of iets anders dan tekst die wordt gedeeld via de hieronder genoemde services.

Om goede en bruikbare logs te verstrekken:

> Zorg ervoor dat er geen spamachtige taak wordt uitgevoerd, zoals een RSS-verversing
{.is-warning}

1. [Verhoog de logging naar trace (Instellingen => Algemeen => Logniveau of bewerk het configuratiebestand)](#tracedebug-logs)
2. [Wis logs (Systeem => Logs => Logs wissen of verwijder alle logs in de logmap)](#logbestanden-wissen)
3. Reproduceer het probleem (Herhaal wat de problemen veroorzaakt)
4. [Open het trace logbestand (sonarr.trace.txt) via de UI of het logbestand](#standaard-loglocatie) op het bestandssysteem en zoek de relevante context op
5. Kopieer een groot stuk vóór het probleem, het probleem zelf en een groot stuk na het probleem.
6. Gebruik [Gist](https://gist.github.com/), [0bin (**Zorg ervoor dat kleurcodering is uitgeschakeld**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) of vergelijkbare sites - met uitzondering van de hieronder genoemde sites om te vermijden - om de gekopieerde logs hierboven te delen

**Waarschuwingen:**
- **Gebruik [pastebin.com](https://pastebin.com) niet, omdat hun filters de neiging hebben om de logs te blokkeren.
- Gebruik [pastebin.pl](https://pastebin.pl) niet, omdat hun site vaak niet toegankelijk is.
- Gebruik [JustPasteIt](https://justpaste.it/) niet, omdat hun site het bekijken van logs niet vergemakkelijkt.
- Upload je log niet als een bestand
- Upload en deel je logs niet via Google Drive, Dropbox of een andere site die hierboven niet is genoemd.
- Archiveer je logs niet (zip, tar (tarball), 7zip, enz.).
- Deel geen console-uitvoer, uitvoer van een dockercontainer of iets anders dan de specifieke applicatielogs

**Belangrijke opmerking:**
- Als je [0bin](https://0bin.net/) gebruikt, zorg er dan voor dat kleurcodering is uitgeschakeld en dat het bericht niet wordt verwijderd na het lezen.

- Als alternatief, als je op zoek bent naar een specifieke vermelding in een oud logbestand, maar niet zeker weet welke, kun je N++ gebruiken. Je kunt de functie "Zoeken in bestanden" van Notepad++ gebruiken om oude logbestanden te doorzoeken indien nodig.
- **Alleen Unix:** Als je op zoek bent naar een specifieke vermelding in een oud logbestand, maar niet zeker weet welke, kun je grep gebruiken. Als je bijvoorbeeld informatie wilt vinden over de film/serie/boek/lied/indexer "Shooter", kun je het volgende commando uitvoeren: `grep -inr -C 100 -e 'Shooter' /pad/naar/logs/*.trace*.txt` Als je [Appdata Directory](/sonarr/appdata-directory) zich in je home-map bevindt, voer je het volgende uit: `grep -inr -C 100 -e 'Shooter' /home/$Gebruiker/.config/logs/*.trace*.txt`

```none

    * De vlaggen hebben de volgende functies
    * -i: hoofdlettergevoeligheid negeren
    * -n: regelnummer weergeven
    *  -r: recursief alle bestanden in het pad controleren
    * -C: het aantal regels voor en na de gevonden regel opgeven
    * -e: het te zoeken patroon

```

## Standaard loglocatie

De logbestanden bevinden zich in de [Appdata Directory](/sonarr/appdata-directory) van Sonarr, in de map logs/. Je kunt ook toegang krijgen tot de logbestanden vanuit de UI via Systeem => Logs => Bestanden.

> Let op: De logtabel ("Gebeurtenissen") in de UI is niet hetzelfde als de logbestanden en is niet zo nuttig. Als je wordt gevraagd om logs, kopieer/plak dan uit de logbestanden en niet uit de tabel.
{.is-info}

## Update loglocatie

De update logbestanden bevinden zich in de [Appdata Directory](/sonarr/appdata-directory) van Sonarr, in de map UpdateLogs/.

## Logbestanden delen

De logbestanden kunnen lang zijn en moeilijk te lezen als onderdeel van een forum- of Reddit-bericht en ze zijn spamachtig in Discord, dus gebruik alsjeblieft [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) of een andere vergelijkbare pastebin-site. Het hele bestand is meestal niet nodig, alleen een goede hoeveelheid context van vóór en na het probleem/fout. Vergeet niet te wachten tot spamachtige taken zoals een RSS-synchronisatie of bibliotheekverversing zijn voltooid.

## Trace/Debug logs

Je kunt het logniveau wijzigen bij Instellingen => Algemeen => Logging. Sonarr hoeft niet opnieuw te worden gestart voor de wijziging van kracht wordt. Deze wijziging heeft alleen invloed op de logbestanden, niet op de logdatabase. De nieuwste debug/trace logbestanden hebben respectievelijk de namen `sonarr.debug.txt` en `sonarr.trace.txt`.

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

Sonarr maakt gebruik van rollende logbestanden die beperkt zijn tot 1 MB elk. Het huidige logbestand is altijd `sonarr.txt`, voor de andere bestanden is `sonarr.0.txt` de op een na nieuwste (hoe hoger het nummer, hoe ouder het bestand). Dit logbestand bevat `fatal`, `error`, `warn` en `info` vermeldingen.

Wanneer het debug-logniveau is ingeschakeld, zijn er extra `sonarr.debug.txt` rollende logbestanden aanwezig. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info` en `debug` vermeldingen. Ze beslaan meestal een periode van 40 uur.

Wanneer het trace-logniveau is ingeschakeld, zijn er extra `sonarr.trace.txt` rollende logbestanden aanwezig. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info`, `debug` en `trace` vermeldingen. Vanwege de uitgebreide traceerbaarheid beslaan ze meestal hooguit een paar uur.

# Herstellen na een mislukte update

We doen er alles aan om problemen bij het upgraden te voorkomen, maar als ze zich voordoen, leiden deze stappen je door de stappen om je installatie te herstellen.

## Het probleem vaststellen

De beste plek om te kijken wanneer de applicatie niet start na een update, is het controleren van de [update logs](#update-loglocatie) en controleren of de update succesvol is voltooid. Als er geen problemen zijn in die logs, is de volgende stap om je reguliere applicatielogbestanden te bekijken. Voordat je opnieuw probeert te starten, gebruik je [Logging](/sonarr/settings#logging) en [Logbestanden](/sonarr/system#log-files) om ze te vinden en het logniveau te verhogen.

### Migratieprobleem

- Migratiefouten zijn niet identiek, maar hier is een voorbeeld:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Machtigingsprobleem

- Machtigingsproblemen worden veroorzaakt doordat de applicatie geen toegang heeft tot de relevante tijdelijke mappen en/of de app-binmap. Los de machtigingen op, zodat de gebruiker/groep waarin de applicatie wordt uitgevoerd de juiste toegang heeft.

- Synology-gebruikers kunnen de volgende Synology-bug tegenkomen: `Toegang tot het pad '/proc/{some number}/maps is geweigerd`.

- Synology-gebruikers kunnen ook tegen het probleem aanlopen dat `/tmp` vol is op bepaalde NAS-apparaten. U moet een andere `/tmp`-pad opgeven voor de app. Raadpleeg SynoCommunity of andere Synology-ondersteuningskanalen voor hulp hierbij.

## Het probleem oplossen

Bij een migratieprobleem is er niet veel dat u onmiddellijk kunt doen. Als het probleem specifiek voor u is (of er nog geen berichten zijn), maak dan een bericht aan op [onze subreddit](https://reddit.com/r/sonarr) of kom langs op onze [discord](https://discord.sonarr.tv/). Als er anderen zijn met hetzelfde probleem, wees dan gerust dat we eraan werken.

> Zorg ervoor dat u niet hebt geprobeerd een database van `develop` te gebruiken in de stabiele versie. Het is onverstandig om tussen branches te wisselen.{.is-info}

### Problemen met machtigingen

- Los de machtigingen op om ervoor te zorgen dat de gebruiker/groep waarin de applicatie wordt uitgevoerd zowel toegang heeft (lezen en schrijven) tot `/tmp` als tot de installatiemap van de applicatie.

- Voor Synology-gebruikers die problemen ondervinden met `/proc/###/maps` die Sonarr of de andere \*Arr-applicaties stoppen, zou het updaten van de applicaties dit probleem moeten oplossen. Dit is een probleem met het SynoCommunity-pakket.

### Handmatig upgraden

Download de nieuwste release van onze website.

Installeer de update (.exe) of pak de inhoud uit (.zip) over uw bestaande installatie en voer Sonarr opnieuw uit zoals u normaal zou doen.

# Downloads en importeren

Het downloaden en importeren is waar de meeste mensen problemen ondervinden. Vanuit een hoog niveau gezien moet Sonarr kunnen communiceren met uw downloadclient en toegang hebben tot de bestanden die het downloadt. Er is een grote verscheidenheid aan ondersteunde downloadclients en nog veel meer verschillende configuraties. Dit betekent dat hoewel er enkele veelvoorkomende configuraties zijn, er geen enkele juiste configuratie is en dat de configuratie van iedereen een beetje anders kan zijn.

> **De eerste stap is om de logboekregistratie te verhogen naar Trace, zie [Logging en logbestanden](#logging-en-logbestanden) voor details over het aanpassen van de logboekregistratie en het doorzoeken van logbestanden. Vervolgens herhaalt u het probleem en gebruikt u de logboeken op trace-niveau uit die tijdsperiode om het probleem te onderzoeken.**
> Als iemand u helpt, plaats dan context van voor/na in een [pastebin](https://0bin.net), [Gist](https://gist.com) of een vergelijkbare site om het aan hen te laten zien.
> Het hoeft niet het hele bestand te zijn en het mag niet alleen de fout zijn. U moet het probleem ook reproduceren terwijl taken die het logbestand overspoelen niet worden uitgevoerd.
{.is-danger}

Wanneer u om hulp vraagt, zorg er dan voor dat u [om hulp vraagt](#om-hulp-vragen) zodat u ons kunt voorzien van de benodigde details.

## Testen van de downloadclient

Zorg ervoor dat uw downloadclient(s) actief zijn. Begin met het testen van de downloadclient. Als het niet werkt, kunt u gedetailleerde informatie vinden in de logboeken op trace-niveau. U moet een URL vinden die u in uw browser kunt invoeren om te zien of het werkt. Het kan een verbindingsprobleem zijn, wat kan duiden op een verkeerd IP-adres, hostname, poort of zelfs een firewall die de toegang blokkeert. Het kan ook voor de hand liggen, zoals een verificatieprobleem waarbij u de gebruikersnaam, het wachtwoord of de API-sleutel verkeerd hebt ingevoerd.

## Testen van een download

Nu gaan we een download proberen. Kies een aflevering van een serie en doe een handmatige zoekopdracht. Kies een van die bestanden en probeer het te downloaden. Wordt het naar de downloadclient gestuurd? Komt het terecht in de juiste categorie? Verschijnt het in Activiteit? Komt het voor in de logboeken op trace-niveau tijdens de taken **Controleren op voltooide download** (Taken voor het vernieuwen van gemonitorde downloads en taken voor het verwerken van gemonitorde downloads) die ongeveer elke minuut worden uitgevoerd? Wordt het correct geparseerd tijdens die taak? Heeft de in de wachtrij geplaatste download een redelijke naam? Omdat zoekopdrachten op basis van id worden uitgevoerd op sommige indexers/trackers, kan er een download in de wachtrij worden geplaatst met een naam die niet herkend kan worden.

## Testen van een import

Importproblemen moeten bijna altijd zichtbaar zijn als een item in Activiteit met een oranje pictogram waarop u kunt hoveren om de fout te zien. Als ze niet in Activiteit worden weergegeven, moet u zich eerst op dit probleem concentreren en dit oplossen. De meeste importfouten zijn machtigingsproblemen. Onthoud dat Sonarr lees- en schrijftoegang moet hebben tot de downloadmap. Soms kunnen ook machtigingsproblemen in de bibliotheekmap de oorzaak zijn, dus controleer beide.

Problemen met onjuiste paden zijn ook mogelijk, maar minder gebruikelijk in normale configuraties. Het belangrijkste om te begrijpen bij padproblemen is dat Sonarr het pad naar de download krijgt van de downloadclient via de API. Dit kan een probleem zijn in meer unieke gevallen, zoals wanneer de downloadclient op een ander systeem draait (misschien zelfs een ander besturingssysteem!). Het kan ook voorkomen in een Docker-configuratie wanneer volumes niet goed zijn geconfigureerd. Een externe padtoewijzing is een goede oplossing wanneer u geen controle hebt, zoals bij een seedbox-configuratie. Bij een Docker-configuratie is het beter om de paden te corrigeren.

## Veelvoorkomende problemen

Hieronder staan enkele veelvoorkomende problemen.

### Een of meer verwachte afleveringen zijn niet geïmporteerd of ontbreken

- Als alle afleveringen zijn geïmporteerd, is de meest voorkomende oorzaak dat er een seizoenspakket is gedownload, maar dat dit niet alle afleveringen van het seizoen bevat. Klik op `X` om de release te verwijderen en te negeren.
- Voor alle andere problemen zijn een of meer afleveringen niet geïmporteerd. Bekijk de informatie in de gebruikersinterface en andere veelvoorkomende problemen.

### Gebruik van Sonarr v2

Sonarr v2 is niet meer ondersteund sinds 3/2021. Het is niet compatibel met qBittorrent v4.3.0 of nieuwer. Upgrade naar Sonarr v3.

### WebUI van de downloadclient is niet ingeschakeld

Sonarr communiceert met uw downloadclient via de API en heeft toegang tot de webinterface van de client. Zorg ervoor dat de webinterface van de client is ingeschakeld en dat de poort die wordt gebruikt niet conflicteert met andere poorten die door andere clients of uw systeem worden gebruikt.

### Onjuiste configuratie van SSL

Zorg ervoor dat SSL-encryptie niet is ingeschakeld als u zowel uw instantie als uw downloadclient op een lokaal netwerk gebruikt. Zie [het SSL FAQ-item](/sonarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) voor meer informatie.

### Kan share niet zien op Windows

De standaardgebruiker voor een Windows-service is `LocalService`, die meestal geen toegang heeft tot uw shares. Bewerk de service en stel deze in om als uw eigen gebruiker uit te voeren. Zie het FAQ-item [waarom kan ik mijn bestanden op een externe server niet zien](/sonarr/faq#why-cant-i-see-my-files-on-a-remote-server) voor meer informatie.

### Mapped network drives zijn niet betrouwbaar

Hoewel gekoppelde netwerkstations zoals `X:\` handig zijn, zijn ze niet zo betrouwbaar als UNC-paden zoals `\\server\share` en ze zijn ook niet beschikbaar vóór het inloggen. Configureer uw downloadclient(s) zodat ze UNC-paden gebruiken indien nodig. Als uw bibliotheek zich op een share bevindt, zorgt u ervoor dat uw hoofdmappen UNC-paden gebruiken. Als uw downloadclient naar een share stuurt, moet u daar UNC-paden configureren, omdat Sonarr het downloadpad van de downloadclient krijgt. Het is prima om uw gekoppelde netwerkstations voor uzelf te gebruiken, maar gebruik ze niet voor automatisering.

### Docker en gebruiker, groep, eigendom, machtigingen en paden

Docker voegt een extra laag complexiteit toe die gemakkelijk verkeerd kan worden geconfigureerd, maar toch een setup oplevert die functioneert, maar verschillende problemen heeft. In plaats van ze hier te bespreken, leest u dit wiki-artikel [voor deze automatiseringssoftware en Docker](/docker-guide) dat alles te maken heeft met gebruiker, groep, eigendom, machtigingen en paden. Het is niet specifiek voor een bepaald Docker-systeem, maar gaat in op zaken op een hoog niveau, zodat u ze in uw eigen omgeving kunt implementeren.

### Externe padtoewijzing

Als u Sonarr in Docker heeft en de Download Client niet in Docker (of vice versa) heeft of als de programma's op verschillende servers staan, heeft u mogelijk een externe padtoewijzing nodig.

De logboeken zien er als volgt uit:

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/torrents/tv/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Dus `/volume3/data` bestaat niet binnen de container van Sonarr of is niet toegankelijk.

- [Instellingen => Downloadclients => Externe padtoewijzingen](/sonarr/settings#remote-path-mappings)
- Een externe padtoewijzing wordt gebruikt wanneer uw downloadclient een pad rapporteert voor voltooide gegevens, hetzij op een andere server, hetzij op een manier die \*Arr niet adresseert naar die map.
- Over het algemeen is een externe padtoewijzing alleen nodig als uw downloadclient op Linux draait terwijl \*Arr op Windows draait, of vice versa. Een externe padtoewijzing is ook mogelijk nodig als u Docker- en native clients mixt, of als u een externe server gebruikt.
- Een externe padtoewijzing is een DOMME zoek/vervang (waarbij het de WAARDE VAN DE EXTERNE locatie vindt en vervangt door de WAARDE VAN DE LOKALE locatie voor de opgegeven host).
- Als het foutbericht over een ongeldig pad de VERVANGENDE waarde niet bevat, werkt de padtoewijzing niet zoals u verwacht. De gebruikelijke oplossing is om de toewijzing toe te voegen en te verwijderen.
- [Zie de tutorial van TRaSH voor aanvullende informatie over externe padtoewijzing](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Als zowel \*Arr als uw Download Client Docker-containers zijn, is een externe padtoewijzing zelden nodig. Het wordt aanbevolen om [de Docker-gids](/docker-guide) te bekijken en/of [de tutorial van TRaSH](https://trash-guides.info/hardlinks) te volgen.
{.is-info}

#### Externe koppeling of externe synchronisatie (Syncthing)

- U moet ervoor zorgen dat het de hele tijd synchroniseert terwijl het aan het downloaden is. En u moet ervoor zorgen dat de lokale synchronisatiebestemming harde koppelingen kan maken wanneer \*Arr importeert, wat betekent dat het hetzelfde bestandssysteem moet zijn en er hetzelfde uit moet zien.
  - Synchroniseer naar een lager, gemeenschappelijke map die zowel onvolledige als voltooide bestanden bevat.
  - Synchroniseer naar een locatie die lokaal op hetzelfde bestandssysteem staat als uw bibliotheek en er hetzelfde uitziet (Docker en netwerkshares maken het gemakkelijk om dit verkeerd te configureren).
  - U wilt de onvolledige en voltooide bestanden synchroniseren, zodat wanneer de torrentclient de verplaatsing uitvoert, dit lokaal wordt weergegeven en alle bestanden al "daar" zijn (zelfs als ze nog steeds worden gedownload). Vervolgens wilt u harde koppelingen gebruiken, omdat zelfs als het importeert voordat het klaar is, ze nog steeds worden voltooid.
  - Op deze manier wordt de hele tijd dat het downloadt, gesynchroniseerd, vervolgens verplaatst de torrentclient naar de tv-submap en wordt dit weergegeven in de synchronisatie. Op die manier zijn de downloads grotendeels aanwezig wanneer ze als voltooid worden beschouwd. En zelfs als ze nog niet helemaal klaar zijn, is het mogelijk om harde koppelingen te maken, wat nog steeds prima is.
  - (Optioneel - indien van toepassing en/of vereist (bijv. externe usenetclient)) Configureer een aangepast script dat wordt uitgevoerd bij importeren/downloaden/upgraden om het externe bestand te verwijderen.
- Als alternatief is een externe koppeling in plaats van een externe synchronisatieopstelling aanzienlijk minder gecompliceerd te configureren, maar meestal langzamer.
  - Koppel uw externe opslag aan met sshfs of een ander netwerkbestandssysteemprotocol.
  - Zorg ervoor dat de gebruiker en groep waarin \*Arr is geconfigureerd om uit te voeren, lees- of schrijftoegang hebben.
  - Configureer een externe padtoewijzing om het EXTERNE pad te vinden en te vervangen door het LOKALE equivalent.

### Machtigingen op de bibliotheekmap

De logboeken zien er als volgt uit:

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/tv/The Orville/Season 03/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Vergeet niet om de machtigingen en eigendom van de *bestemming* te controleren. Het is gemakkelijk om gefixeerd te raken op de eigendom en machtigingen van de download en dat is meestal de oorzaak van machtigingsgerelateerde problemen, maar het *kan* ook de bestemming zijn. Controleer of de bestemmingsmap(pen) bestaan. Controleer of er al een bestaand *bestand* in de bestemming staat of niet kan worden verwijderd of verplaatst naar de prullenbak. Controleer of de eigendom en machtigingen het kopiëren, hardlinken of verplaatsen van het gedownloade bestand toestaan. De gebruiker of groep waarin wordt uitgevoerd, moet lees- en schrijftoegang hebben tot de hoofdmap.

- Voor Windows-gebruikers kan dit te wijten zijn aan het uitvoeren als een service:
  - de Windows-service wordt uitgevoerd onder het account 'Local Service', standaard heeft dit account geen toegang tot uw gebruikersmap, tenzij er handmatig machtigingen zijn toegewezen. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw gebruikersmap.
  - 'Local Service' heeft over het algemeen ook zeer beperkte machtigingen. Het is daarom raadzaam om de app als een systeemvaktoepassing te installeren als de gebruiker ingelogd kan blijven. De optie hiervoor wordt tijdens de installatie aangeboden. Zie de FAQ voor instructies over hoe u kunt overschakelen van een service naar een systeemvaktoepassing.

- Voor Synology-gebruikers raadpleegt u [het artikel over machtigingen van SynoCommunity voor hun pakketten](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Niet-Windows: Als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
- Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.

### Machtigingen op de downloadmap

U ziet een foutmelding die lijkt op het volgende:

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES.1/a4187f6c3c4445f98e85da52b83c84e8.mkv. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

of

```none
2022-02-03 10:40:41.8|Warn|Sabnzbd|[Resident.Alien.S02E02.720p.WEB.H264-CAKES] Error occurred while trying to delete data from '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES/'.
 
[v3.0.6.1342] System.UnauthorizedAccessException: Access to the path '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES' is denied.
```

Vergeet niet om de machtigingen en eigendom van de *bron* te controleren. Het is gemakkelijk om gefixeerd te raken op de eigendom en machtigingen van de bestemming en dat is een *mogelijke* oorzaak van machtigingsgerelateerde problemen, maar meestal is het de bron. Controleer of de bronmap(pen) bestaan. Controleer of de eigendom en machtigingen het kopiëren/hardlinken of kopiëren+verwijderen/verplaatsen van het gedownloade bestand toestaan. De gebruiker of groep waarin Sonarr wordt uitgevoerd, moet lees- en schrijftoegang hebben tot de downloadbestanden.

- Voor Windows-gebruikers kan dit te wijten zijn aan het uitvoeren als een service:
  - de Windows-service wordt uitgevoerd onder het account 'Local Service', standaard heeft dit account geen toegang tot uw gebruikersmap, tenzij er handmatig machtigingen zijn toegewezen. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw gebruikersmap.
  - 'Local Service' heeft over het algemeen ook zeer beperkte machtigingen. Het is daarom raadzaam om de app als een systeemvaktoepassing te installeren als de gebruiker ingelogd kan blijven. De optie hiervoor wordt tijdens de installatie aangeboden. Zie de FAQ voor instructies over hoe u kunt overschakelen van een service naar een systeemvaktoepassing.

- Voor Synology-gebruikers raadpleegt u [het artikel over machtigingen van SynoCommunity voor hun pakketten](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Niet-Windows: Als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
- Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.

### Downloadmap en bibliotheekmap zijn niet verschillende mappen

- De downloadclient moet downloaden naar een map die toegankelijk is voor \*Arr en die niet je root/bibliotheekmap is; je moet importeren vanuit die aparte downloadmap naar je bibliotheekmap.
- Je moet nooit rechtstreeks downloaden naar je rootmap. Je moet ook je rootmap niet gebruiken als de voltooide map of onvoltooide map van de downloadclient.
- [**Dit zal ook een gezondheidscontrole in het systeem veroorzaken**](/sonarr/system#downloading-into-root-folder)
- Binnen de applicatie wordt een rootmap gedefinieerd als de geconfigureerde mediabibliotheekmap. Dit is niet de rootmap van een mount. Je downloadclient heeft een onvoltooide of voltooide map (of verplaatst voltooide downloads) naar je root (bibliotheek) map. Dit veroorzaakt vaak problemen en wordt afgeraden. Om dit op te lossen, wijzig je downloadclient zodat deze downloads niet in je rootmap plaatst. Let op dat 'plaatsen' ook inhoudt dat je downloadclientcategorie is ingesteld op je rootmap of dat NZBGet/SABnzbd sorteren ingeschakeld heeft en sorteert naar je rootmap. Houd er rekening mee dat deze controle kijkt naar alle gedefinieerde/geconfigureerde rootmappen die zijn toegevoegd, niet alleen naar de rootmappen die momenteel in gebruik zijn. Met andere woorden, de map waarin je downloadclient downloadt of voltooide downloads naartoe verplaatst, mag niet dezelfde map zijn die je hebt geconfigureerd als je root/bibliotheek/eindbestemmingsmap in de \*Arr-applicatie.
- Geconfigureerde rootmappen (ook wel bibliotheekmappen genoemd) kunnen worden gevonden in [Instellingen => Mediabeheer => Rootmappen](/sonarr/settings/#root-folders)
- Een voorbeeld is als je downloads naar `\data\downloads` gaan, dan heb je een rootmap ingesteld als `\data\downloads`.
- Het wordt aanbevolen om paden zoals `\data\media\` te gebruiken voor je rootmap/bibliotheek en `\data\downloads\` voor je downloads.

> Je downloadmap en je root/bibliotheekmap MOETEN gescheiden zijn
{.is-warning}

### Onjuiste categorie

Sonarr moet worden ingesteld om een categorie te gebruiken, zodat het alleen probeert zijn eigen downloads te verwerken. Het is zeldzaam dat een torrent die handmatig is toegevoegd zonder de juiste categorie wordt toegevoegd, maar het kan gebeuren. Als je handmatig torrents toevoegt en ze wilt verwerken, moeten ze de juiste categorie hebben. Deze kan op elk moment worden ingesteld, omdat Sonarr elke minuut probeert downloads te verwerken.

### Ingepakte torrents

Logs geven fouten aan zoals

```none
Geen geschikte bestanden gevonden om te importeren
```

Als je torrent is ingepakt in `.rar`-bestanden, moet je uitpakken instellen. We raden [Unpackerr](https://github.com/unpackerr/unpackerr) aan, omdat het uitpakken correct doet: het voorkomt beschadigde gedeeltelijke imports en ruimt de uitgepakte bestanden op na import.

De fout kan ook optreden als er geen geldig mediabestand in de map aanwezig is.

### Herhaalde downloads

Er zijn verschillende oorzaken van herhaalde downloads, maar een daarvan heeft te maken met de indexerbeperking in Releaseprofielen. Omdat de indexer *niet* wordt opgeslagen met de gegevens, zijn alle scores voor `voorkeurswoord` *nul* voor media in je bibliotheek, maar tijdens "RSS" en zoeken worden ze toegepast. Op dezelfde manier gelden de beperkingen voor `moet bevatten` of `mag niet bevatten` alleen voor die indexer; alles wat daarbuiten valt, is eerlijk spel. Hierdoor kom je in een lus terecht waarin je de items steeds opnieuw downloadt omdat het eruitziet als een upgrade, dan niet is, dan weer verschijnt en eruitziet als een upgrade, dan niet is. Beperk je releaseprofiel niet tot een indexer.

Dit kan ook te wijten zijn aan het feit dat de download nooit daadwerkelijk wordt geïmporteerd en vervolgens ontbreekt in de wachtrij, dus er wordt voortdurend een nieuwe download opgehaald en nooit geïmporteerd. Raadpleeg de verschillende andere veelvoorkomende problemen en probleemoplossingsstappen hiervoor.

### Usenet-download mist import

Sonarr kijkt alleen naar de 60 meest recente downloads in SABnzbd en NZBGet, dus als je je geschiedenis *behoudt*, betekent dit dat tijdens grote wachtrijen met importproblemen downloads stilzwijgend kunnen worden gemist en niet geïmporteerd. De beste manier om dit te voorkomen, is door je geschiedenis leeg te houden, zodat eventuele items die nog steeds verschijnen, onderzocht moeten worden. Dit kun je bereiken door Verwijderen in te schakelen onder Voltooide en Mislukte Downloadverwerking. In NZBGet worden items dan verplaatst naar de *verborgen* geschiedenis, wat geweldig is. Helaas heeft SABnzbd geen vergelijkbare functie. Het beste wat je daar kunt bereiken, is het gebruik van de nzb-back-upmap.

### Downloadclient verwijdert items

De downloadclient moet geen downloads verwijderen. Usenet-clients moeten zo worden geconfigureerd dat ze downloads niet uit de geschiedenis verwijderen. Torrent-clients moeten zo worden ingesteld dat ze torrents niet verwijderen wanneer ze klaar zijn met seeden (pauzeren of stoppen in plaats daarvan). Dit komt doordat Sonarr communiceert met de downloadclient om te weten wat er moet worden geïmporteerd, dus als ze worden *verwijderd*, is er niets om te importeren, zelfs als er een map vol met bestanden is.

Voor SABnzbd wordt dit afgehandeld met de instelling Geschiedenisbehoud.

### Download kan niet worden gekoppeld aan een bibliotheekitem

Om verschillende redenen kunnen releases niet worden geparseerd nadat ze zijn gedownload en naar de downloadclient zijn gestuurd. Activity => Opties => Onbekend weergeven (dit is nu standaard ingeschakeld in recente builds) toont alle items die niet anders worden genegeerd / al zijn geïmporteerd binnen de downloadclientcategorie van \*Arr. Deze moeten meestal handmatig worden toegewezen en geïmporteerd.

Dit kan ook voorkomen als je een release in je downloadclient hebt, maar dat mediabestand (film/aflevering/boek/lied) niet bestaat in de applicatie.

#### Overeenkomende serie gevonden via geschiedenis ophalen, maar serie werd gekoppeld via serie-ID. Automatische import is niet mogelijk

- Deze importfout is vergelijkbaar met de bovenstaande fout die niet kan worden gekoppeld.
- Sonarr heeft de release gedownload omdat je indexer of tracker heeft gemeld dat de release de TVDb-ID (of IMDb-ID) had voor een serie die je wilde.
- De serie van het gedownloade bestand komt niet overeen met de gemelde ID, dus Sonarr zal het bestand niet importeren.
- Afhankelijk van de serietitel en de releasenaam - ervan uitgaande dat de release correct is voor de bijbehorende serie-ID - heeft Sonarr waarschijnlijk een alias nodig, [deze FAQ-vermelding bevat meer informatie](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x) over het aanvragen van een alias.
- Als alternatief is de release verkeerd gelabeld en niet voor de gemelde serie-ID. Dit moet worden gemeld aan je indexer, zodat zij corrigerende maatregelen kunnen nemen.
- Om deze fout af te handelen:
  1. Verifieer de serie van het bestand.
  1. Vraag een alias aan (indien van toepassing).
  1. Importeer het bestand handmatig (menselijk pictogram aan de rechterkant) vanuit Activity => Wachtrij OF klik op `X` in de wachtrij om de release in je client te negeren en optioneel op de blokkeerlijst te plaatsen / optioneel te verwijderen uit de client.

### Afleveringsnaam is TBA

Op TVDB worden afleveringsnamen als onbekend getiteld als TBA en er is een cache van 24 uur op de API. Gewoonlijk duurt het 24-48 uur voordat wijzigingen op de TVDB-website in Sonarr worden weergegeven vanwege de TVDB-cache, Skyhook-cache en de verversingsinterval van de serie.

De instelling [Vereiste afleveringstitel](/sonarr/settings#importing) in Sonarr bepaalt het importgedrag wanneer de titel TBA is, maar na 24 uur vanaf de uitzenddatum van de aflevering wordt de release geïmporteerd, zelfs als de titel nog steeds TBA is. Er is ook geen automatische hernoeming van bestanden met de titel TBA.

### De onderliggende verbinding is gesloten: Er is een onverwachte fout opgetreden bij het verzenden

Dit wordt veroorzaakt doordat de indexer een SSL-protocol gebruikt dat niet wordt ondersteund door de huidige .NET-versie die wordt gevonden in [Sonarr => Systeem => Status](/sonarr/system#status).

### De aanvraag is verlopen

Sonarr ontvangt geen reactie van de client.

```none
    System.NET.WebException: De aanvraag is verlopen: ’https://example.org/api?t=caps&apikey=(verwijderd) —> System.NET.WebException: De aanvraag is verlopen
```

```none
2022-11-01 10:16:54.3|Waarschuwing|Newznab|Kan geen verbinding maken met indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Een taak is geannuleerd.
```

Dit kan ook worden veroorzaakt door:

- onjuiste configuratie of gebruik van een VPN
- onjuiste configuratie of gebruik van een proxy
- lokale DNS-problemen - Probeer over te schakelen naar een andere DNS-provider
- lokale IPv6-problemen - meestal is IPv6 ingeschakeld, maar niet functioneel
- het gebruik van Privoxy en een onjuiste configuratie daarvan

## Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigings- en netwerkproblemen oplossen met behulp van opdrachten [in onze handleiding](/permissions-and-networking). Bespreek anders het probleem met het ondersteuningsteam op Discord. Als dit iets is dat mogelijk een veelvoorkomend probleem is, stel dan voor om het toe te voegen aan de wiki.

# Zoeken in indexers en trackers

- De [Waarom heeft Sonarr een aflevering die ik verwachtte niet gedownload?](/sonarr/faq#why-didnt-sonarr-grab-an-episode-i-was-expecting) FAQ-vermelding is waarschijnlijk ook nuttig.
- Als je [Prowlarr](/prowlarr) gebruikt, kun je de [Geschiedenis](/prowlarr/history) van alle query's bekijken die Prowlarr heeft ontvangen en hoe ze naar de sites zijn verzonden. Zorg ervoor dat `Parameters` is ingeschakeld in Prowlarr Geschiedenis => Opties. Het (i)-pictogram biedt aanvullende details.
- De probleemoplossingsstappen staan hieronder

## Zet logging op trace

> **De eerste stap is om logging op Trace te zetten, zie [Logging en logbestanden](#logging-and-log-files) voor details over het aanpassen van logging en het doorzoeken van logs. Je zult vervolgens het probleem reproduceren en de trace-level logs uit die tijdsperiode gebruiken om het probleem te onderzoeken.** Als iemand je helpt, plaats dan context van vóór/na in een [pastebin](https://0bin.net), [Gist](https://gist.com) of een vergelijkbare site om het te laten zien. Het hoeft niet het hele bestand te zijn en het mag niet *alleen* de fout zijn. Je moet het probleem ook reproduceren terwijl taken die het logbestand spammen niet worden uitgevoerd.
{.is-danger}

## Testen van een indexer of tracker

Bij het testen van een indexer of tracker kun je in debug- of trace-logs de gebruikte URL vinden. Hieronder staat een voorbeeld van een succesvolle test, je kunt zien dat het de indexer bevraagt via een specifieke URL met specifieke parameters en vervolgens de reactie. Je kunt deze URL in je browser testen door `apikey=(verwijderd)` te vervangen door de juiste apikey, zoals `apikey=123`. Je kunt experimenteren met de parameters als je een foutmelding van de indexer krijgt of controleren of je connectiviteitsproblemen hebt als het helemaal niet werkt. Nadat je het in je eigen browser hebt getest, moet je testen vanaf het systeem waarop het draait *als* je dat nog niet hebt gedaan.

## Testen van een zoekopdracht

Net als bij de indexer/tracker-test hierboven, wanneer je een zoekopdracht start terwijl je logbestanden op Debug- of Trace-niveau staan, kun je de gebruikte URL uit de logbestanden halen. Bij het testen is het het beste om zo'n smal mogelijke zoekopdracht te gebruiken. Een handmatige (interactieve) zoekopdracht voor een enkele aflevering of seizoen is goed omdat het specifiek is en je de resultaten in de gebruikersinterface kunt zien terwijl je de logbestanden onderzoekt. Handmatige (interactieve) zoekopdrachten worden geactiveerd door naar een serie te gaan en op het menselijke pictogram te klikken voor een aflevering of seizoen.

Bij deze test kijk je naar duidelijke fouten en voer je enkele eenvoudige tests uit. Je kunt zien dat de zoekopdracht de URL `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(verwijderd)&offset=0&limit=100&tvdbid=354629&season=1&ep=1` gebruikte, die je zelf kunt proberen in een browser nadat je (verwijderd) hebt vervangen door je apikey voor die indexer. Werkt het? Zie je de verwachte resultaten? Is deze FAQ-vermelding van toepassing? In die URL kun je zien dat het specifieke categorieën heeft ingesteld met `cat=5030,5040,5045,5080`, dus als je de verwachte resultaten niet ziet, is dit een waarschijnlijke reden. Je kunt ook zien dat er is gezocht op tvdbid met `tvdbid=354629`, dus als de aflevering niet correct is gecategoriseerd op de indexer, moet dit worden opgelost. Je kunt ook zien dat er is gezocht op specifiek seizoen en aflevering met season=1 en ep=1, dus als dat niet correct is op de indexer, zie je die resultaten niet. Kijk naar Voorbeeld van XML-uitvoer van handmatige zoekopdracht hieronder om een voorbeeld te zien van de uitvoer van een werkende query.

- Voorbeeld van XML-uitvoer van handmatige zoekopdracht

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1" rel="self" type="application/rss+xml"/>
<title>api.nzbgeek.info</title>
<description>NZBgeek API</description>
<link>http://api.nzbgeek.info/</link>
<language>en-gb</language>
<webMaster>info@nzbgeek.info (NZBgeek)</webMaster>
<category/>
<image>
<url>https://api.nzbgeek.info/covers/nzbgeek.png</url>
<title>api.nzbgeek.info</title>
<link>http://api.nzbgeek.info/</link>
<description>NZBgeek</description>
</image>
<newznab:response offset="0" total="2"/>
<item>
<title>The.Fix.S01E01.1080p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/358e0f946f953771c7688864b0334ba1
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=358e0f946f953771c7688864b0334ba1
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:32 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.1080p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)" length="3810861000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="3810861000"/>
<newznab:attr name="guid" value="358e0f946f953771c7688864b0334ba1"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="55"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:54:15 +0000"/>
</item>
<item>
<title>The.Fix.S01E01.720p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/f7e4ac2875b6a1ce45bae91ab19e9699
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=f7e4ac2875b6a1ce45bae91ab19e9699
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:33 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.720p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)" length="1195794000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="1195794000"/>
<newznab:attr name="guid" value="f7e4ac2875b6a1ce45bae91ab19e9699"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="14"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:51:45 +0000"/>
</item>
</channel>
</rss>
```

![searches-indexers-and-trackers1.png](/assets/sonarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/sonarr/searches-indexers-and-trackers2.png)

- Trace Log Fragment

```none
2021-03-20 13:15:23.6|Info|NzbSearchService|Zoeken in 1 indexers voor [The Fix : S01E01]
2021-03-20 13:15:23.6|Debug|Newznab|Feed downloaden https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
2021-03-20 13:15:23.6|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
```

- Volledige Trace Log van een zoekopdracht

```none
2022-04-24 20:14:26.7|Info|NzbSearchService|Searching 1 indexers for [Fairy Tail : S02E91 (91)]
2022-04-24 20:14:26.7|Debug|Newznab|Downloading Feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91
2022-04-24 20:14:26.7|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'proxyenabled' defaultValue:'False'
2022-04-24 20:14:27.2|Trace|HttpClient|Res: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91: 200.OK (505 ms)
2022-04-24 20:14:27.2|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|NzbSearchService|Total of 2 reports were found for [Fairy Tail : S02E91 (91)] from 1 indexers
2022-04-24 20:14:27.2|Debug|NzbSearchService|Setting last search time to: 11/20/2019 13:15:24
2022-04-24 20:14:27.2|Info|DownloadDecisionMaker|Processing 2 releases
2022-04-24 20:14:27.2|Trace|DownloadDecisionMaker|Processing release 1/2
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.2|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.2|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.2|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.2|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.2|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|Parser|Quality parsed: WEBDL-1080p v1
2022-04-24 20:14:27.2|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.2|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.2|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-1080p v1
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.1080p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.2|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.2|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.2|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.2|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] WEBDL-1080p is not wanted in profile
2022-04-24 20:14:27.2|Trace|DownloadDecisionMaker|Processing release 2/2
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.2|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.2|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.2|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.2|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.2|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|Parser|Quality parsed: WEBDL-720p v1
2022-04-24 20:14:27.2|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.720p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.2|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.2|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-720p v1
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.720p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.2|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.2|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.2|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.2|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'autounmonitorpreviouslydownloadedepisodes' defaultValue:'False'
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Release accepted
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'downloadpropersandrepacks' defaultValue:'PreferAndUpgrade'
2022-04-24 20:14:27.2|Trace|Http|Res: 66 [GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
2022-04-24 20:14:27.2|Debug|Api|[GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
```

## Veelvoorkomende problemen

Hieronder staan enkele veelvoorkomende problemen die de oplossing bieden voor bijna alle problemen die zich voordoen.

### Indexers worden niet doorzocht

- Logs zien er als volgt uit:

```none
2022-04-24 20:14:26.7|Info|ReleaseSearchService|Zoeken naar indexers voor [Fairy Tail : S02E91 (91)]. 0 actieve indexers
2022-04-24 20:14:26.7|Debug|ReleaseSearchService|Er zijn in totaal 0 rapporten gevonden voor [Fairy Tail : S02E91 (91)] van 0 indexers
2022-04-24 20:14:26.7|Info|DownloadDecisionMaker|Geen resultaten gevonden
```

- Let op dat in het bovenstaande geval 0 indexers worden doorzocht. Dit aantal kan variëren afhankelijk van uw specifieke configuratie. Als het aantal niet overeenkomt met het aantal geconfigureerde indexers, zijn de volgende waarschijnlijke oorzaken:
  - [Health Checks (Systeem => Status)](/sonarr/system#health)
    - [Geen indexers beschikbaar met automatisch zoeken ingeschakeld, Sonarr geeft geen automatische zoekresultaten](/sonarr/system#no-indexers-available-with-automatic-search-enabled-sonarr-will-not-provide-any-automatic-search-results)
    - [Er zijn geen indexers ingeschakeld](/sonarr/system#no-indexers-are-enabled)
    - [Ingeschakelde indexers ondersteunen geen zoeken](/sonarr/system#enabled-indexers-do-not-support-searching)
    - [Geen indexers beschikbaar met interactief zoeken ingeschakeld](/sonarr/system#no-indexers-available-with-interactive-search-enabled)
    - [Indexers zijn niet beschikbaar vanwege fouten](/sonarr/system#indexers-are-unavailable-due-to-failures)
  - Het zoeken naar een serie van het type Anime en er zijn geen anime-categorieën geconfigureerd voor uw tracker(s). Indexers hebben [twee verschillende configureerbare categorieën](/sonarr/settings#indexers).
  - Het zoeken naar een serie van het type Dagelijks of Standaard en er zijn geen standaard (niet-anime) categorieën geconfigureerd voor uw tracker(s)
    - Categorieën - Standaardcategorieën worden gebruikt tenzij ze zijn bewerkt. Het is waarschijnlijk dat deze standaardcategorieën suboptimaal zijn. Bij het bewerken van deze instelling vraagt Sonarr de indexer om de beschikbare categorieën en toont ze in een selecteerbare lijst. De verouderde standaardwaarden worden gewist zodra een categorie wordt omgeschakeld.
  - Anime-categorieën - De categorieën die Sonarr zal gebruiken voor Anime-zoekopdrachten. Er worden geen categorieën gebruikt tenzij ze zijn bewerkt. Bij het bewerken van deze instelling vraagt Sonarr de indexer om de beschikbare categorieën en toont ze in een selecteerbare lijst. De verouderde standaardwaarden worden gewist zodra een categorie wordt omgeschakeld.
  - De mogelijkheden van de indexer ondersteunen het querytype niet (bijv. Seizoen/aflevering, enz.):
    - Binnen Prowlarr kunnen de mogelijkheden van een indexer worden gevonden in het (I)-pictogram voor de indexer
    - Jackett toont de mogelijkheden van een tracker niet binnen zijn UI.
  - Trace logs geven informatie weer over waarom indexers worden genegeerd als er na het ***herstarten van Sonarr*** een zoekopdracht wordt uitgevoerd.

### Slecht genoemde releases

- Series Packs worden niet ondersteund
- Meerdere Season Packs worden niet ondersteund
- In veel gevallen kan Sonarr de geretourneerde resultaten niet koppelen aan een bekende serie. In deze gevallen zullen uw logboeken er als volgt uitzien. Deze moeten handmatig worden gedownload en waarschijnlijk geïmporteerd. De sleutelzin om in de logboeken te zien is `|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings`

```none
2022-02-23 14:11:09.7|Debug|Parser|Parsing string 'Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR'
2022-02-23 14:11:09.7|Trace|Parser|^(?<title>.+?)[-_. ]+?(?:S|Season|Saison|Series)[-_. ]?(?<season>\d{1,2}(?![-_. ]?\d+))(\W+|_|$)(?<extras>EXTRAS|SUBPACK)?(?!\\)
2022-02-23 14:11:09.7|Debug|Parser|Episode Parsed. Johnny Bravo 1997 Season 1 4 - Season 01 
2022-02-23 14:11:09.7|Debug|Parser|Language parsed: English
2022-02-23 14:11:09.7|Debug|QualityParser|Trying to parse quality for Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR
2022-02-23 14:11:09.7|Debug|Parser|Quality parsed: SDTV v1
2022-02-23 14:11:09.7|Debug|Parser|Release Group parsed: 
2022-02-23 14:11:09.8|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings
```

### Tracker heeft RawSearch Caps nodig

- Sonarr zoekt naar `9 1 1`, maar uw tracker heeft alleen resultaten voor `9-1-1` of `John s Show` en `John's Show`
- Dit komt doordat uw tracker geen normale gestandaardiseerde zoekopdrachten ondersteunt.
- De oplossing is dat de zoekmogelijkheden van de definitie van uw tracker moeten worden bijgewerkt om aan te geven dat deze [RawSearch vereist en ondersteunt](https://github.com/Sonarr/Sonarr/issues/1225#issuecomment-981153943)
- Jackett ondersteunt de vlag, maar de mogelijkheden moeten per indexer worden bijgewerkt. Open een functieverzoek voor Jackett om deze functionaliteit toe te voegen voor uw indexer.
- Prowlarr ondersteunt de vlag, maar de mogelijkheden moeten per indexer worden bijgewerkt. Open een functieverzoek voor Prowlarr om deze functionaliteit toe te voegen voor uw indexer.

### Serie heeft een alias nodig

Releases kunnen worden geüpload als `The Series Name`, maar TVDB heeft de serie als `Series Name` of soortgelijke naamverschillen. Zie [deze FAQ-entry](/sonarr/faq#why-cannot-sonarr-import-episode-files-for-series-x-why-cannot-sonarr-find-releases-for-series-x) voor meer informatie.

### Serie heeft een XEM-mapping nodig

Releases kunnen worden geüpload als `Series Title S02E45` of `Other Series Title S2022E42`, maar TVDB heeft deze aflevering als `Series Title S03E01` of `Other Series Title S03E42`. Zie [deze FAQ-entry](/sonarr/faq#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc) voor meer informatie.

### Verkeerd serie type

Het serie type heeft invloed op hoe Sonarr zoekt. Het serie type moet worden geselecteerd op basis van hoe de serie wordt uitgebracht op de indexers.
[Zie deze FAQ-entry voor meer details](/sonarr/faq#whats-the-different-series-types)

> Als het **Anime** serie type wordt gebruikt, is het [mogelijk om ook uw indexer te doorzoeken met het standaard type.](/sonarr/settings#indexers)
{.is-info}

#### Dagelijks

Logboeken tonen `Zoeken in indexers voor [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standaard

Logboeken tonen `Zoeken in indexers voor [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Logboeken tonen `Zoeken in indexers voor [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

### Media is niet gemonitord

Logboeken tonen iets vergelijkbaars als

```none
2022-03-30 13:46:03.0|Debug|MonitoredEpisodeSpecification|No episodes in the release are monitored. Rejecting
2022-03-30 13:46:03.0|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] One or more episodes is not monitored
```

De serie/season/aflevering(en) worden niet gemonitord. Controleer de monitorstatus van de serie, het seizoen en de aflevering(en).

> Season Packs worden alleen gedownload als alle afleveringen in het seizoen worden gemonitord en het seizoenspakket alle bestaande afleveringen upgrade of als alle afleveringen ontbreken.
{.is-info}

### Succesvolle zoekopdracht - Geen resultaten geretourneerd

U ontvangt een bericht vergelijkbaar met `Query successful, but no results were returned from your indexer. This may be an issue with the indexer or your indexer category settings.`

Dit wordt veroorzaakt doordat uw indexer geen resultaten retourneert die binnen de door u geconfigureerde categorieën vallen.

### Verkeerde categorieën

Onjuiste categorieën zijn waarschijnlijk de meest voorkomende oorzaak van resultaten die worden weergegeven in handmatige zoekopdrachten van een indexer/tracker, maar *niet* in \*Arr. De indexer/tracker *zou* de categorie in de zoekresultaten moeten weergeven, wat u zou moeten helpen om te achterhalen wat er ontbreekt. Als u Jackett of Prowlarr gebruikt, heeft elke tracker een lijst met specifiek ondersteunde categorieën. Zorg ervoor dat u de juiste categorieën gebruikt. Veel mensen vinden het handig om de lijst zichtbaar te hebben in één browservenster terwijl ze de invoer in Sonarr bewerken.

> Let op dat als u `Anime Categories` leeg laat in uw indexerinstellingen, de indexer niet wordt gebruikt voor zoekopdrachten van het Anime serie type.
> Op dezelfde manier, als u `Categories` leeg laat in uw indexerinstellingen, wordt de indexer niet gebruikt voor zoekopdrachten van het Standaard of Dagelijks serie type.
{.is-info}

### Verkeerde resultaten

Soms retourneren indexers volledig niet-gerelateerde resultaten; Sonarr geeft parameters door om de zoekopdracht te beperken tot een serie. Soms zijn de geretourneerde resultaten volledig niet-gerelateerd. Of soms voornamelijk gerelateerd met een paar onjuiste resultaten. Het eerste is meestal een probleem met de indexer en u kunt dit zien aan de hand van de trace-logboeken die het veroorzaken. U kunt die indexer uitschakelen en het probleem melden. Het andere is meestal gecategoriseerde releases die kunnen worden gemeld bij de indexer/tracker.

Bepaalde trackers - zoals EZTV en andere publieke trackers - retourneren willekeurige resultaten als ze geen exacte overeenkomst hebben voor de gezochte serie/season/aflevering. Hier is geen oplossing voor.

### Ontbrekende resultaten

Als u resultaten op de site kunt vinden die niet worden weergegeven in Sonarr, is uw probleem waarschijnlijk een van de volgende mogelijkheden:

- [Categorieën zijn onjuist - zie hierboven](#wrong-categories)
- Er wordt een ID (IMDbId, TVDBId, enz.) gebaseerde zoekopdracht uitgevoerd en de indexer heeft de releases niet correct gekoppeld aan dat ID. Dit is iets wat alleen uw indexer kan oplossen. Zij moeten ervoor zorgen dat de release correct wordt gekoppeld aan de juiste toepasselijke id's.
- U zoekt niet op dezelfde manier als Sonarr zoekt; Het is zeer waarschijnlijk dat de termen die u op de indexer zoekt niet overeenkomen met hoe Sonarr het doorzoekt. U kunt zien hoe Sonarr zoekt in de Trace Logs. Tekstgebaseerde zoekopdrachten zullen over het algemeen in het formaat `q=woorden%20en%20dingen%20hier` zijn, deze string is HTTP-gecodeerd en kan eenvoudig worden gedecodeerd met behulp van een online HTML-decoderings/-coderingstool.
- Gemiste delen van de RSS-feed van nieuwe uploads. Logboeken worden als volgt weergegeven en er wordt een waarschuwingsevenement genoteerd.

```none
2022-02-22 08:03:38.7|Debug|Torznab|Downloading Feed http://jackett:9117/api/v2.0/indexers/torrentdownloads/results/torznab?t=tvsearch&cat=5000,100008&extended=1&apikey=(removed)&offset=2900&limit=100
2022-02-22 08:03:40.7|Warn|Torznab|Indexer TorrentDownloads rss sync didn't cover the period between 2/21/2022 8:32:06 PM and 2/21/2022 9:02:42 PM UTC. Search may be required.
```

### Certificaatvalidatie

U zult verbinding maken met de meeste indexers/trackers via https, dus u moet ervoor zorgen dat dit correct werkt op uw systeem. Dat betekent dat uw tijdzone en tijd beide *correct* moeten zijn ingesteld. Het betekent ook dat uw systeemcertificaten up-to-date moeten zijn.

### Bereiken van snelheidslimieten

Als u uw systeem via een VPN of proxy laat lopen, concurreert u mogelijk met 10s of 100s of 1000s andere mensen die allemaal proberen gebruik te maken van diensten zoals , theXEM en/of uw indexers en trackers. Snelheidsbeperkingen en DDOS-bescherming worden vaak gedaan op basis van IP-adres en uw VPN-/proxy-uitgangspunt is *één* IP-adres. Tenzij u zich in een repressief land bevindt zoals China, Australië of Zuid-Afrika, heeft u geen VPN-/proxy nodig.

Rarbg heeft de neiging om een soort snelheidsbeperking te hebben binnen hun API en geeft aan dat er geen resultaten zijn.

### IP-blokkade

Vergelijkbaar met snelheidsbeperkingen kan een bepaalde indexer - zoals Nyaa - een IP-adres volledig blokkeren. Dit is meestal semi-permanent en de oplossing is om een nieuw IP-adres van uw ISP of VPN-provider te krijgen.

### Het gebruik van de Jackett /all-eindpunt

Het Jackett `/all`-eindpunt is handig, maar dat is het enige voordeel. Al het andere kan problemen veroorzaken, dus het toevoegen van elke tracker afzonderlijk is vereist. Als alternatief kunt u overwegen om de Jackett & NZBHydra2-alternatief [Prowlarr](/prowlarr) te gebruiken.

[Zelfs Jackett zegt dat /all vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)

Het gebruik van het all-eindpunt heeft geen voordelen (behalve verminderd beheer), alleen nadelen:

- u verliest de controle over specifieke instellingen van indexers (categorieën, zoekmodi, enz.)
- het mixen van zoekmodi (IMDB, query, enz.) kan leiden tot lage kwaliteit resultaten
- indexer-specifieke categorieën (\>= 100000) kunnen niet worden gebruikt.
- trage indexers vertragen het algehele resultaat
- het totale aantal resultaten is beperkt tot 1000
- niet-gerelateerde resultaten
- ontbrekende resultaten

Het toevoegen van elke indexer afzonderlijk maakt fijnafstemming van categorieën mogelijk op basis van de indexer, wat een probleem kan zijn met het `/all`-eindpunt als het gebruik van de verkeerde categorie fouten veroorzaakt op sommige trackers. In Sonarr is elke indexer beperkt tot 1000 resultaten als paginering wordt ondersteund, of 100 als dit niet het geval is, wat betekent dat naarmate u meer trackers aan Jackett toevoegt, u steeds meer kans hebt om resultaten te missen. Ten slotte, als *één* van de trackers in `/all` een fout retourneert, zal Jackett deze uitschakelen en krijgt u nu geen resultaten meer.

### Het gebruik van NZBHydra2 als enkele invoer

Het gebruik van NZBHydra2 als enkele indexerinvoer (dwz 1 NZBHydra2-invoer in Sonarr voor veel indexers in NZBHydra2) in plaats van meerdere (dwz veel NZBHydra2-invoeren in Sonarr voor veel indexers in NZBHydra2) heeft dezelfde problemen als hierboven vermeld met het `/all`-eindpunt van Jackett.

### Indexer wordt niet doorzocht

- Als een indexer niet lijkt te worden doorzocht, komt dit waarschijnlijk doordat de indexer het zoektype niet ondersteunt. Het meest voorkomende geval is dat Nyaa alleen query-zoekopdrachten ondersteunt en geen Season/Episode-zoekopdrachten. De Trace-logboeken geven na een herstart bij de eerste zoekopdracht aan welke mogelijkheden een indexer heeft of niet heeft.

### Jackett handmatige zoekopdracht vindt meer resultaten

- [Zie deze FAQ-entry](/sonarr/faq#jackett-shows-more-results-than-sonarr-when-manually-searching)

### Releaseprofielen worden niet gerespecteerd

Er zijn een paar oorzaken waarom het lijkt alsof uw profielen worden genegeerd. De meest voorkomende is gerelateerd aan de Indexer-beperking in Releaseprofielen. Omdat de indexer *niet* wordt opgeslagen bij de gegevens, zijn alle scores voor `preferred word` *nul* voor media in uw bibliotheek, *maar* tijdens "RSS" en zoekopdrachten worden ze toegepast. Op dezelfde manier geldt voor eventuele beperkingen van `must contain` of `must-not` dat deze alleen van toepassing zijn op die indexer; alles wat daarbuiten valt, is eerlijk spel. Dit kan ertoe leiden dat releaseprofielen lijken te worden genegeerd of dat er upgrade-lussen optreden.

### Probleem niet vermeld

U kunt ook enkele veelvoorkomende machtigings- en netwerkproblemen oplossen met behulp van [onze handleiding](/permissions-and-networking). Anders kunt u dit bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.

## Fouten

Dit zijn enkele veelvoorkomende fouten die u kunt zien bij het toevoegen van een indexer

### De onderliggende verbinding is gesloten: Er is een onverwachte fout opgetreden bij het verzenden

Dit wordt veroorzaakt doordat de indexer een SSL-protocol gebruikt dat niet wordt ondersteund door de huidige .NET-versie die wordt gevonden in [Sonarr => Systeem => Status](/sonarr/system#status).

### De aanvraag is verlopen

Sonarr ontvangt geen reactie van de indexer.

```none
    System.NET.WebException: De aanvraag is verlopen: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: De aanvraag is verlopen
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Kan geen verbinding maken met indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Een taak is geannuleerd.
```

Dit kan ook worden veroorzaakt door:

- onjuist geconfigureerde of gebruikte VPN
- onjuist geconfigureerde of gebruikte proxy
- lokale DNS-problemen - Probeer over te schakelen naar een andere DNS-provider
- lokale IPv6-problemen - meestal is IPv6 ingeschakeld, maar niet functioneel
- het gebruik van Privoxy en een onjuiste configuratie ervan

### Probleem niet vermeld

U kunt ook enkele veelvoorkomende machtigings- en netwerkproblemen oplossen met behulp van [onze handleiding](/permissions-and-networking). Anders kunt u dit bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.