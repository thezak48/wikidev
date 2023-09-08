---
title: Radarr Probleemoplossing
description: Probleemoplossing voor Radarr, inclusief het verkrijgen van logbestanden, probleemoplossing en veelvoorkomende problemen bij het zoeken en downloaden/importeren.
published: true
date: 2023-08-12T09:40:45.369Z
tags: radarr, probleemoplossing
editor: markdown
dateCreated: 2021-08-03T21:05:52.988Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Hulp vragen](#hulp-vragen)
- [Logging en logbestanden](#logging-en-logbestanden)
  - [Standaardlocatie logbestanden](#standaardlocatie-logbestanden)
  - [Locatie update-logbestanden](#locatie-update-logbestanden)
  - [Logbestanden delen](#logbestanden-delen)
  - [Trace/Debug-logbestanden](#tracedebug-logbestanden)
  - [Logbestanden wissen](#logbestanden-wissen)
- [Meerdere logbestanden](#meerdere-logbestanden)
- [Herstellen na een mislukte update](#herstellen-na-een-mislukte-update)
  - [Het probleem vaststellen](#het-probleem-vaststellen)
    - [Database disk image is beschadigd](#database-disk-image-is-beschadigd)
    - [Migratieprobleem](#migratieprobleem)
    - [UI-migratieproblemen](#ui-migratieproblemen)
    - [Machtigingsprobleem](#machtigingsprobleem)
  - [Het probleem oplossen](#het-probleem-oplossen)
    - [Migratieproblemen](#migratieproblemen)
    - [Machtigingsproblemen](#machtigingsproblemen)
    - [Handmatig upgraden](#handmatig-upgraden)
- [Downloads en importeren](#downloads-en-importeren)
  - [Testen van de downloadclient](#testen-van-de-downloadclient)
  - [Testen van een download](#testen-van-een-download)
  - [Testen van een import](#testen-van-een-import)
  - [Veelvoorkomende problemen](#veelvoorkomende-problemen)
    - [WebUI van de downloadclient is niet ingeschakeld](#webui-van-de-downloadclient-is-niet-ingeschakeld)
    - [SSL in gebruik en verkeerd geconfigureerd](#ssl-in-gebruik-en-verkeerd-geconfigureerd)
    - [Kan gedeelde map niet zien op Windows](#kan-gedeelde-map-niet-zien-op-windows)
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
    - [Verbinding verbroken](#verbinding-verbroken)
  - [Probleem niet vermeld](#probleem-niet-vermeld)
- [Zoeken naar indexers en trackers](#zoeken-naar-indexers-en-trackers)
  - [Logging verhogen naar trace](#logging-verhogen-naar-trace)
  - [Testen van een indexer of tracker](#testen-van-een-indexer-of-tracker)
  - [Testen van een zoekopdracht](#testen-van-een-zoekopdracht)
  - [Veelvoorkomende problemen](#veelvoorkomende-problemen-1)
    - [Tracker heeft RawSearch-machtigingen nodig](#tracker-heeft-rawsearch-machtigingen-nodig)
    - [Media is niet gevolgd](#media-is-niet-gevolgd)
    - [Onjuiste categorieën](#onjuiste-categorieën)
    - [Query succesvol - geen resultaten](#query-succesvol-geen-resultaten)
    - [Onjuiste resultaten](#onjuiste-resultaten)
    - [Ontbrekende resultaten](#ontbrekende-resultaten)
    - [Certificaatvalidatie](#certificaatvalidatie)
    - [Rate limits bereikt](#rate-limits-bereikt)
    - [IP-blokkade](#ip-blokkade)
    - [Jaar komt niet overeen](#jaar-komt-niet-overeen)
    - [Jaar ontbreekt](#jaar-ontbreekt)
    - [Gebruik van de Jackett /all-eindpunt](#gebruik-van-de-jackett-all-eindpunt)
    - [Gebruik van NZBHydra2 als enkele invoer](#gebruik-van-nzbhydra2-als-enkele-invoer)
    - [Probleem niet vermeld](#probleem-niet-vermeld-1)
  - [Fouten](#fouten)
    - [De onderliggende verbinding is gesloten: er is een onverwachte fout opgetreden bij het verzenden](#de-onderliggende-verbinding-is-gesloten-er-is-een-onverwachte-fout-opgetreden-bij-het-verzenden)
    - [De aanvraag is verlopen](#de-aanvraag-is-verlopen)
    - [Probleem niet vermeld](#probleem-niet-vermeld-2)

# Hulp vragen

Heb je hulp nodig? Dat is prima, iedereen heeft soms hulp nodig. Je kunt realtime hulp krijgen via de chat op:

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiële Radarr Discord*](https://radarr.video/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiële Radarr Subreddit*](https://reddit.com/r/radarr)
{.links-list}

Maar voordat je daar naartoe gaat en een bericht plaatst, zorg ervoor dat je verzoek om hulp zo goed mogelijk is. Beschrijf duidelijk het probleem en geef een korte beschrijving van je setup, inclusief zaken zoals je besturingssysteem/distributie, versie van .NET, versie van Radarr, downloadclient en de versie ervan. **Als je [Docker](https://www.docker.com/) gebruikt, doorloop dan eerst de [Docker-handleiding](/docker-guide), omdat dit veelvoorkomende en frequente pad-/machtigingsproblemen oplost. Zorg er anders voor dat je een [docker compose](/docker-guide#docker-compose) bij de hand hebt. [Hoe genereer je een Docker Compose](https://trash-guides.info/compose)** Vertel ons wat je al hebt geprobeerd, waar je naar hebt gekeken. Gebruik de [Logging en logbestanden](#logging-en-logbestanden)-sectie om je logging naar trace te verhogen, het probleem opnieuw te reproduceren, plak de relevante context in een pastebin en voeg een link naar het bericht toe. Voeg misschien zelfs wat schermafbeeldingen toe om het probleem te verduidelijken.

Hoe meer we weten, hoe gemakkelijker het is om je te helpen.

# Logging en logbestanden

Het is waarschijnlijk ook nuttig om de veelvoorkomende probleemoplossingsproblemen te bekijken:
- [Veelvoorkomende problemen bij het downloaden en importeren](#veelvoorkomende-problemen)
- [Veelvoorkomende problemen bij het zoeken naar indexers en trackers](#veelvoorkomende-problemen-1)
{.links-list}

Als je wordt gevraagd om debuglogs, bevatten je logs het woord `debug` en als je wordt gevraagd om trace logs, bevatten je logs het woord `trace`. Als de logs die je verstrekt deze woorden niet bevatten, zijn het niet de gevraagde logs.

- Deel niet het volledige logbestand tenzij erom wordt gevraagd.
- Upload logs niet rechtstreeks naar Discord of plak ze niet als tekstblokken, tenzij erom wordt gevraagd.
- Deel de logs niet als bijlage, een zip-archief of iets anders dan tekst die wordt gedeeld via de hieronder genoemde services.

Om goede en bruikbare logs te verstrekken:

> Zorg ervoor dat er geen spamachtige taak wordt uitgevoerd, zoals een RSS-verversing
{.is-warning}

1. [Verhoog de logging naar trace (Instellingen => Algemeen => Logniveau of bewerk het configuratiebestand)](#tracedebug-logbestanden)
2. [Wis logs (Systeem => Logs => Logs wissen of verwijder alle logs in de logmap)](#logbestanden-wissen)
3. Reproduceer het probleem (Doe wat de dingen kapot maakt opnieuw)
4. [Open het trace-logbestand (radarr.trace.txt) via de UI of het logbestand](#standaardlocatie-logbestanden) op het bestandssysteem en zoek de relevante context op
5. Kopieer een groot stuk vóór het probleem, het probleem zelf en een groot stuk na het probleem.
6. Gebruik [Gist](https://gist.github.com/), [0bin (**Zorg ervoor dat kleurcodering is uitgeschakeld**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) of vergelijkbare sites - met uitzondering van de hieronder genoemde sites - om de gekopieerde logs hierboven te delen

**Waarschuwingen:**
- **Gebruik [pastebin.com](https://pastebin.com) niet, omdat hun filters de neiging hebben om de logs te blokkeren.
- Gebruik [pastebin.pl](https://pastebin.pl) niet, omdat hun site vaak niet toegankelijk is.
- Gebruik [JustPasteIt](https://justpaste.it/) niet, omdat hun site het bekijken van logs niet vergemakkelijkt.
- Upload je logbestand niet als bestand.
- Upload en deel je logs niet via Google Drive, Dropbox of een andere site die hierboven niet is genoemd.
- Archiveer je logs niet (zip, tar (tarball), 7zip, enz.).
- Deel geen console-uitvoer, uitvoer van dockercontainer of iets anders dan de gespecificeerde toepassingslogs.

**Belangrijke opmerking:**
- Als je [0bin](https://0bin.net/) gebruikt, zorg er dan voor dat kleurcodering is uitgeschakeld en dat je het bericht niet na het lezen verwijdert.

- Als alternatief, als je op zoek bent naar een specifieke invoer in een oud logbestand, maar niet zeker weet welke, kun je N++ gebruiken. Je kunt de functie "Zoeken in bestanden" van Notepad++ gebruiken om oude logbestanden te doorzoeken indien nodig.
- **Alleen Unix:** Als je op zoek bent naar een specifieke invoer in een oud logbestand, maar niet zeker weet welke, kun je grep gebruiken. Als je bijvoorbeeld informatie wilt vinden over de film/serie/boek/lied/indexer "Shooter", kun je het volgende commando uitvoeren: `grep -inr -C 100 -e 'Shooter' /pad/naar/logs/*.trace*.txt` Als je [Appdata Directory](/radarr/appdata-directory) zich in je home-map bevindt, voer je het volgende uit: `grep -inr -C 100 -e 'Shooter' /home/$Gebruiker/.config/logs/*.trace*.txt`

```none

    * De vlaggen hebben de volgende functies
    * -i: hoofdlettergevoeligheid negeren
    * -n: regelnummer weergeven
    *  -r: recursief alle bestanden in het pad controleren
    * -C: het aantal regels voor en na de gevonden regel opgeven
    * -e: het te zoeken patroon

```

## Standaardlocatie logbestanden

De logbestanden bevinden zich in de [Appdata Directory](/radarr/appdata-directory) van Radarr, in de map logs/. Je kunt ook toegang krijgen tot de logbestanden vanuit de UI via Systeem => Logs => Bestanden.

> Opmerking: De logtabel ("Gebeurtenissen") in de UI is niet hetzelfde als de logbestanden en is niet zo nuttig. Als je wordt gevraagd om logs, kopieer/plak dan uit de logbestanden en niet uit de tabel.
{.is-info}

## Locatie update-logbestanden

De update-logbestanden bevinden zich in de [Appdata Directory](/radarr/appdata-directory) van Radarr, in de map UpdateLogs/.

## Logbestanden delen

De logbestanden kunnen lang zijn en moeilijk te lezen als onderdeel van een forum- of Reddit-bericht en ze zijn spamachtig in Discord, dus gebruik alsjeblieft [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) of een andere vergelijkbare pastebin-site. Het hele bestand is meestal niet nodig, alleen een goede hoeveelheid context van vóór en na het probleem/fout. Vergeet niet te wachten tot spamachtige taken zoals een RSS-synchronisatie of bibliotheekverversing zijn voltooid.

## Trace/Debug-logbestanden

Je kunt het logniveau wijzigen via Instellingen => Algemeen => Logging. Radarr hoeft niet opnieuw te worden gestart voor de wijziging van kracht wordt. Deze wijziging heeft alleen invloed op de logbestanden, niet op de loggingsdatabase. De nieuwste debug/trace-logbestanden hebben respectievelijk de namen `radarr.debug.txt` en `radarr.trace.txt`.

Als je geen toegang hebt tot de UI om het logniveau in te stellen, kun je dit doen door config.xml in de AppData-directory te bewerken en de waarde van LogLevel in te stellen op Debug of Trace in plaats van Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Logbestanden wissen

Je kunt logbestanden en de loggingsdatabase rechtstreeks vanuit de UI wissen via Systeem => Logs => Logbestanden en Systeem => Logs => Verwijderen (Prullenbakpictogram)

# Meerdere logbestanden

Radarr maakt gebruik van rollende logbestanden die beperkt zijn tot 1 MB elk. Het huidige logbestand is altijd `radarr.txt`, voor de andere bestanden is `radarr.0.txt` de op een na nieuwste (hoe hoger het nummer, hoe ouder het bestand). Dit logbestand bevat `fatal`, `error`, `warn` en `info` vermeldingen.

Wanneer het debug-logniveau is ingeschakeld, zijn er extra `radarr.debug.txt` rollende logbestanden aanwezig. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info` en `debug` vermeldingen. Ze beslaan meestal een periode van 40 uur.

Wanneer het trace-logniveau is ingeschakeld, zijn er extra `radarr.trace.txt` rollende logbestanden aanwezig. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info`, `debug` en `trace` vermeldingen. Vanwege de uitgebreide traceerbaarheid beslaan ze meestal slechts een paar uur.

# Herstellen na een mislukte update

- We doen er alles aan om problemen bij het upgraden te voorkomen, maar als ze zich voordoen, doorloop dan de volgende stappen om je installatie te herstellen.
- In dit gedeelte worden ook veelvoorkomende problemen na een update behandeld.

## Het probleem vaststellen

- De beste plek om te kijken wanneer de toepassing niet start na een update, is het controleren van de [update-logbestanden](#locatie-update-logbestanden) en controleren of de update succesvol is voltooid. Als er geen problemen zijn, kijk dan naar je reguliere toepassingslogbestanden. Verhoog de logniveau eerst met behulp van [Logging](/radarr/settings#logging) en [Logbestanden](/radarr/system#logbestanden) om ze te vinden en verhoog het logniveau.
- Het meest voorkomende probleem is dat het systeem waarop de app is geïnstalleerd heeft geknoeid met de `/tmp`-map en kritieke \*Arr-bestanden heeft verwijderd tijdens de upgrade, waardoor zowel de upgrade als de rollback mislukken. In dit geval installeer je eenvoudigweg opnieuw op de bestaande defecte installatie.

### Database disk image is beschadigd

- Zie onze [FAQ-entry](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)

### Migratieprobleem

- Migratiefouten zijn niet identiek, maar hier is een voorbeeld:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### UI-migratieproblemen

- Als je schakelt tussen [niet-ondersteunde versies/takken](/radarr/faq#can-i-switch-between-branches), kun je een migratieprobleem ervaren dat er als volgt uitziet. De oplossing is om [terug te gaan naar de tak of hogere versie waarop je eerder zat](/radarr/faq#how-do-i-update-radarr), of [een back-up te herstellen](/radarr/faq#how-do-i-backuprestore-radarr) voor je huidige versie.

![radarr-migration-error-ui.png](/assets/radarr/radarr-migration-error-ui.png)

### Machtigingsprobleem

- Machtigingsproblemen ontstaan doordat de toepassing geen toegang heeft tot de relevante tijdelijke mappen en/of de map met de app-binaries. Los de machtigingsproblemen op, zodat de gebruiker/groep waarin de toepassing wordt uitgevoerd de juiste toegang heeft.

- Synology-gebruikers kunnen te maken krijgen met de Synology-bug `Toegang tot het pad '/proc/{some number}/maps is geweigerd'

- Synology-gebruikers kunnen ook te maken krijgen met een tekort aan ruimte in `/tmp` op bepaalde NAS-apparaten. U moet een ander `/tmp`-pad opgeven voor de app. Raadpleeg SynoCommunity of andere Synology-ondersteuningskanalen voor hulp hierbij.

## Het probleem oplossen

### Migratieproblemen

Bij een migratieprobleem kunt u niet veel doen op het moment zelf. Als het probleem specifiek voor u is (of er nog geen berichten zijn), maak dan een bericht aan op [onze subreddit](https://reddit.com/r/radarr) of kom langs op onze [discord](https://radarr.video/discord). Als er anderen zijn met hetzelfde probleem, wees dan gerust dat we eraan werken.

> Zorg ervoor dat u niet hebt geprobeerd een database van `nightly` te gebruiken in de stabiele versie. Het is niet verstandig om tussen verschillende versies te wisselen.{.is-info}

### Problemen met machtigingen

- Los de machtigingen op om ervoor te zorgen dat de gebruiker/groep waarin de applicatie wordt uitgevoerd zowel toegang heeft (lezen en schrijven) tot `/tmp` als tot de installatiemap van de applicatie.

- Voor Synology-gebruikers die problemen ondervinden met `/proc/###/maps` kan het stoppen van Sonarr of de andere \*Arr-applicaties en het bijwerken ervan dit probleem oplossen. Dit is een probleem met het SynoCommunity-pakket.

### Handmatig upgraden

Download de nieuwste release van onze website.

Installeer de update (.exe) of pak de inhoud uit (.zip) over uw bestaande installatie en voer Radarr opnieuw uit zoals u normaal zou doen.

# Downloads en importeren

Het downloaden en importeren is waar *de meeste* mensen problemen ondervinden. Vanuit een hoog niveau gezien moet Radarr kunnen communiceren met uw downloadclient en toegang hebben tot de bestanden die het downloadt. Er is een grote verscheidenheid aan ondersteunde downloadclients en nog een *grotere* verscheidenheid aan configuraties. Dit betekent dat hoewel er enkele *veelvoorkomende* configuraties zijn, er niet één *juiste* configuratie is en de configuratie van iedereen een beetje anders kan zijn.

> **De eerste stap is om de logboekregistratie te verhogen naar Trace, zie [Logging en logbestanden](#logging-en-logbestanden) voor details over het aanpassen van de logboekregistratie en het doorzoeken van logbestanden. U zult vervolgens het probleem reproduceren en de trace-level logs uit die tijdsperiode gebruiken om het probleem te onderzoeken.** Als iemand u helpt, plaats dan context van voor/na in een [pastebin](https://0bin.net), [Gist](https://gist.com) of een vergelijkbare site om het te laten zien. Het hoeft niet het hele bestand te zijn en het mag niet *alleen* de fout zijn. U moet het probleem ook reproduceren terwijl taken die het logbestand overspoelen niet worden uitgevoerd.
{.is-danger}

Wanneer u om hulp vraagt, zorg er dan voor dat u [om hulp vraagt](#om-hulp-vragen) zodat u ons de benodigde gegevens kunt verstrekken.

## Testen van de downloadclient

Zorg ervoor dat uw downloadclient(s) actief zijn. Begin met het testen van de downloadclient, als het niet werkt, kunt u details zien in de logboekregistratie op trace-niveau. U moet een URL vinden die u in uw browser kunt invoeren en controleren of deze werkt. Het kan een verbindingsprobleem zijn, wat kan duiden op een verkeerd IP-adres, hostname, poort of zelfs een firewall die de toegang blokkeert. Het kan ook voor de hand liggen, zoals een verificatieprobleem waarbij u de gebruikersnaam, het wachtwoord of de API-sleutel verkeerd hebt ingevoerd. Houd er rekening mee dat sommige seedboxes het gebruik van https, poort 443 en een URL-basis (geavanceerde opties) vereisen, in plaats van de werkelijke poort van uw downloadclient.

## Testen van een download

Nu gaan we een download proberen, kies een film en doe een handmatige zoekopdracht. Kies een van die bestanden en probeer het te downloaden. Wordt het naar de downloadclient gestuurd? Komt het terecht in de juiste categorie? Verschijnt het in Activiteit? Komt het voor in de logboekregistratie op trace-niveau tijdens de taken **Controleren op voltooide download** (Vernieuwen van gemonitorde downloads en Verwerken van gemonitorde downloads), die ongeveer elke minuut worden uitgevoerd? Wordt het correct verwerkt tijdens die taak? Heeft de in de wachtrij geplaatste download een redelijke naam? Omdat zoekopdrachten op basis van id worden uitgevoerd op sommige indexers/trackers, kan er een in de wachtrij worden geplaatst met een naam die niet herkend kan worden.

## Testen van een import

Importproblemen zouden bijna altijd zichtbaar moeten zijn als een item in Activiteit met een oranje pictogram waar u overheen kunt zweven om de fout te zien. Als ze niet verschijnen in Activiteit, moet u zich eerst op dit probleem concentreren en het oplossen. De meeste importfouten zijn *machtigings*problemen, onthoud dat lezen en schrijven mogelijk moet zijn in de map waarin de bibliotheek zich bevindt. Soms kunnen machtigingen in de bibliotheekmap ook de oorzaak zijn, dus controleer beide.

Problemen met onjuiste paden zijn ook mogelijk, maar minder vaak voorkomend in normale configuraties. Het sleutelwoord om padproblemen te begrijpen, is te weten dat de downloadclient het pad naar de download krijgt *van* de downloadclient via de API. Dit wordt een probleem in meer unieke gevallen, zoals wanneer de downloadclient op een ander systeem draait (misschien zelfs een ander besturingssysteem\!). Het kan ook voorkomen bij een Docker-configuratie wanneer volumes niet goed zijn geconfigureerd. Een externe padkoppeling is een goede oplossing wanneer u geen controle hebt, zoals bij een seedbox-configuratie. Bij een Docker-configuratie is het beter om de paden te corrigeren.

## Veelvoorkomende problemen

Hieronder staan enkele veelvoorkomende problemen.

### De webinterface van de downloadclient is niet ingeschakeld

Radarr communiceert met uw downloadclient via de API en heeft toegang tot de webinterface van de client nodig. Zorg ervoor dat de webinterface van de client is ingeschakeld en dat de poort die wordt gebruikt niet conflicteert met andere poorten die in gebruik zijn door andere clients of op uw systeem.

### SSL in gebruik en verkeerd geconfigureerd

Zorg ervoor dat SSL-versleuteling niet is ingeschakeld als u zowel uw instantie als uw downloadclient op een lokaal netwerk gebruikt. Zie [het SSL-FAQ-item](/radarr/faq#ongeldig-certificaat-en-andere-HTTPS-of-SSL-problemen) voor meer informatie.

### Kan gedeelde map niet zien op Windows

De standaardgebruiker voor een Windows-service is `LocalService`, die meestal geen toegang heeft tot uw gedeelde mappen. Bewerk de service en stel deze in om als uw eigen gebruiker uit te voeren, zie het FAQ-item [waarom kan ik mijn bestanden op een externe server niet zien](/radarr/faq#waarom-kan-ik-mijn-bestanden-op-een-externe-server-niet-zien) voor meer informatie.

### Mapped network drives zijn niet betrouwbaar

Hoewel gemapte netwerkstations zoals `X:\` handig zijn, zijn ze niet zo betrouwbaar als UNC-paden zoals `\\server\share` en ze zijn ook niet beschikbaar vóór het inloggen. Configureer uw downloadclient(s) zodat ze indien nodig UNC-paden gebruiken. Als uw bibliotheek zich op een gedeelde map bevindt, zorgt u ervoor dat uw hoofdmappen UNC-paden gebruiken. Als uw downloadclient naar een gedeelde map stuurt, moet u daar UNC-paden configureren, omdat het downloadpad wordt verkregen van de downloadclient. Het is prima om uw gemapte netwerkstations voor uzelf te gebruiken, maar gebruik ze niet voor automatisering.

### Docker en gebruiker, groep, eigendom, machtigingen en paden

Docker voegt een extra laag complexiteit toe die gemakkelijk verkeerd kan worden geconfigureerd, maar toch een setup oplevert die functioneert, maar verschillende problemen heeft. In plaats van ze hier te bespreken, lees dit wiki-artikel [voor deze automatiseringssoftware en Docker](/docker-guide) dat alles behandelt over gebruiker, groep, eigendom, machtigingen en paden. Het is niet specifiek voor een bepaald Docker-systeem, maar gaat in op de belangrijkste punten zodat u ze kunt implementeren in uw eigen omgeving.

### Extern pad koppelen

Als u Radarr in Docker hebt en de Download Client in niet-Docker (of andersom) hebt of als de programma's op verschillende servers staan, heeft u mogelijk een extern pad koppeling nodig.

De logboeken geven iets vergelijkbaars aan.

```none
2022-02-03 14:03:54.3|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /volume3/data/torrents/movies/The.Orville.2022.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Dus `/volume3/data` bestaat niet in de container van Radarr of is niet toegankelijk.

- [Instellingen => Downloadclients => Externe padkoppelingen](/radarr/settings#remote-path-mappings)
- Een externe padkoppeling wordt gebruikt wanneer uw downloadclient een pad rapporteert voor voltooide gegevens op een andere server of op een manier die \*Arr niet herkent.
- Over het algemeen is een externe padkoppeling alleen nodig als uw downloadclient op Linux draait terwijl \*Arr op Windows draait, of vice versa. Een externe padkoppeling is ook mogelijk nodig als u Docker- en native clients mixt, of als u een externe server gebruikt.
- Een externe padkoppeling is een DOMME zoek/vervang (waarbij het de WAARDE OP AFSTAND vindt en vervangt door de LOKALE waarde voor de opgegeven host).
- Als het foutbericht over een ongeldig pad de VERVANGEN waarde niet bevat, werkt de padkoppeling niet zoals u verwacht. De gebruikelijke oplossing is om de koppeling toe te voegen en te verwijderen.
- [Zie de tutorial van TRaSH voor aanvullende informatie over externe padkoppelingen](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Als zowel \*Arr als uw Download Client Docker-containers zijn, is een externe padkoppeling zelden nodig. Het wordt aanbevolen om [de Docker-handleiding](/docker-guide) te bekijken en/of [de tutorial van TRaSH](https://trash-guides.info/hardlinks) te volgen.
{.is-info}

#### Externe koppeling of externe synchronisatie (Syncthing)

- U moet ervoor zorgen dat het de hele tijd synchroniseert terwijl het aan het downloaden is. En u moet ervoor zorgen dat de lokale synchronisatiebestemming harde koppelingen kan maken wanneer \*Arr importeert, wat betekent dat het hetzelfde bestandssysteem moet zijn en er hetzelfde uit moet zien.
  - Synchroniseer op een lager, gemeenschappelijk map die zowel onvolledige als voltooide bestanden bevat.
  - Synchroniseer naar een locatie die lokaal hetzelfde bestandssysteem heeft als uw bibliotheek en er hetzelfde uitziet (Docker en netwerkshares maken het gemakkelijk om dit verkeerd te configureren).
  - U wilt de onvolledige en voltooide bestanden synchroniseren, zodat wanneer de torrentclient de verplaatsing uitvoert, dit lokaal wordt weergegeven en alle bestanden al "daar" zijn (zelfs als ze nog steeds worden gedownload). Vervolgens wilt u harde koppelingen gebruiken, omdat zelfs als het importeert voordat het klaar is, ze nog steeds worden voltooid.
  - Op deze manier wordt er de hele tijd gesynchroniseerd terwijl het wordt gedownload, vervolgens verplaatst de torrentclient naar de tv-submap en wordt dit weergegeven in de synchronisatie. Op deze manier zijn de downloads grotendeels aanwezig wanneer ze als voltooid worden beschouwd. En zelfs als ze nog niet helemaal klaar zijn, is het mogelijk om harde koppelingen te maken, wat nog steeds goed is.
  - (Optioneel - indien van toepassing en/of vereist (bijv. externe usenetclient)) Configureer een aangepast script dat wordt uitgevoerd bij importeren/downloaden/upgraden om het externe bestand te verwijderen.
- Als alternatief is een externe koppeling in plaats van een externe synchronisatieopstelling aanzienlijk minder gecompliceerd te configureren, maar meestal langzamer.
  - Koppel uw externe opslag aan met sshfs of een ander netwerkbestandssysteemprotocol.
  - Zorg ervoor dat de gebruiker en groep waarin \*Arr wordt uitgevoerd lees- of schrijftoegang hebben.
  - Configureer een externe padkoppeling om het EXTERNE pad te vinden en te vervangen door het LOKALE equivalent.

### Machtigingen op de bibliotheekmap

Logboeken zien er als volgt uit:

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/media/Movie Name (2010). Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Vergeet niet de machtigingen en eigendom van de *bestemming* te controleren. Het is gemakkelijk om gefixeerd te raken op de eigendom en machtigingen van de download en dat is *meestal* de oorzaak van machtigingsgerelateerde problemen, maar het *kan* ook de bestemming zijn. Controleer of de bestemmingsmap(pen) bestaan. Controleer of er al een bestaand *bestand* in de bestemming is of dat het niet kan worden verwijderd of verplaatst naar de prullenbak. Controleer of eigendom en machtigingen het kopiëren, harde koppelen of verplaatsen van het gedownloade bestand toestaan. De gebruiker of groep waarin \*Arr wordt uitgevoerd, moet de rootmap kunnen lezen en schrijven.

- Voor Windows-gebruikers kan dit te wijten zijn aan het draaien als een service:
  - de Windows-service wordt uitgevoerd onder het account 'Local Service', standaard heeft dit account geen toegang tot uw gebruikersmap, tenzij er handmatig machtigingen zijn toegewezen. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw gebruikersmap.
  - 'Local Service' heeft over het algemeen ook zeer beperkte machtigingen. Het is daarom raadzaam om de app als een systeemvaktoepassing te installeren als de gebruiker ingelogd kan blijven. Deze optie wordt tijdens de installatie aangeboden. Zie de FAQ voor instructies over het converteren van een service naar een systeemvaktoepassing.

- Voor Synology-gebruikers zie [het artikel over machtigingen van SynoCommunity voor hun pakketten](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Niet-Windows: als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
- Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.

### Machtigingen op de downloadmap

Logboeken zien er als volgt uit:

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/downloads/The.Movie. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Vergeet niet de machtigingen en eigendom van de *bron* te controleren. Het is gemakkelijk om gefixeerd te raken op de eigendom en machtigingen van de bestemming en dat is een *mogelijke* oorzaak van machtigingsgerelateerde problemen, maar meestal is het de bron. Controleer of de bronmap(pen) bestaan. Controleer of eigendom en machtigingen het kopiëren/hardlinken of kopiëren+verwijderen/verplaatsen van het gedownloade bestand toestaan. De gebruiker of groep waarin \*Arr wordt uitgevoerd, moet de downloadmap kunnen lezen en schrijven.

- Voor Windows-gebruikers kan dit te wijten zijn aan het draaien als een service:
  - de Windows-service wordt uitgevoerd onder het account 'Local Service', standaard heeft dit account geen toegang tot uw gebruikersmap, tenzij er handmatig machtigingen zijn toegewezen. Dit is met name relevant bij het gebruik van downloadclients die zijn geconfigureerd om te downloaden naar uw gebruikersmap.
  - 'Local Service' heeft over het algemeen ook zeer beperkte machtigingen. Het is daarom raadzaam om de app als een systeemvaktoepassing te installeren als de gebruiker ingelogd kan blijven. Deze optie wordt tijdens de installatie aangeboden. Zie de FAQ voor instructies over het converteren van een service naar een systeemvaktoepassing.

- Voor Synology-gebruikers zie [het artikel over machtigingen van SynoCommunity voor hun pakketten](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Niet-Windows: als u een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
- Als u een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.

### Downloadmap en bibliotheekmap zijn niet verschillende mappen

- De downloadclient moet downloaden naar een map die toegankelijk is voor \*Arr en die niet uw root/bibliotheekmap is; het moet importeren vanuit die aparte downloadmap naar uw bibliotheekmap.
- U moet nooit rechtstreeks downloaden naar uw rootmap. U moet ook uw rootmap niet gebruiken als de voltooide map of onvoltooide map van uw downloadclient.
- [**Dit veroorzaakt ook een gezondheidscontrole in Systeem**](/radarr/system#downloaden-in-rootmap)
- Binnen de applicatie wordt een rootmap gedefinieerd als de geconfigureerde mediabibliotheekmap. Dit is niet de rootmap van een mount. Uw downloadclient heeft een onvoltooide of voltooide map (of verplaatst voltooide downloads) naar uw root (bibliotheek) map. Dit veroorzaakt vaak problemen en wordt afgeraden. Om dit op te lossen, wijzigt u uw downloadclient zodat deze downloads niet in uw rootmap plaatst. Let op: 'plaatsen' omvat ook het geval waarin de categorie van uw downloadclient is ingesteld op uw rootmap of als NZBGet/SABnzbd sorteren ingeschakeld hebben en sorteren naar uw rootmap. Houd er rekening mee dat deze controle kijkt naar alle gedefinieerde/geconfigureerde rootmappen, niet alleen naar de rootmappen die momenteel in gebruik zijn. Met andere woorden, de map waarin uw downloadclient downloadt of voltooide downloads naartoe verplaatst, mag niet dezelfde map zijn die u hebt geconfigureerd als uw root/bibliotheek/definitieve mediabestemmingsmap in de \*Arr-applicatie.
- Geconfigureerde rootmappen (ook wel bibliotheekmappen genoemd) vindt u in [Instellingen => Media Management => Rootmappen](/radarr/settings/#root-folders)
- Een voorbeeld is als uw downloads worden geplaatst in `\data\downloads`, dan heeft u een rootmap ingesteld als `\data\downloads`.
- Het wordt aanbevolen om paden zoals `\data\media\` te gebruiken voor uw root/bibliotheekmap en `\data\downloads\` voor uw downloads.

> Uw downloadmap en uw root/bibliotheekmap MOETEN verschillende mappen zijn
{.is-warning}

### Onjuiste categorie

Radarr moet worden ingesteld om een categorie te gebruiken, zodat het alleen probeert zijn eigen downloads te verwerken. Het is zeldzaam dat een torrent die is ingediend door wordt toegevoegd zonder de juiste categorie, maar het kan gebeuren. Als u handmatig torrents toevoegt en ze wilt verwerken, moeten ze de juiste categorie hebben. Deze kan op elk moment worden ingesteld, omdat \*Arr downloads elke minuut probeert te verwerken.

### Ingepakte torrents

Logboeken geven fouten aan zoals

```none
No files found are eligible for import
```

Als uw torrent is ingepakt in `.rar`-bestanden, moet u de extractie instellen. We raden [Unpackerr](https://github.com/unpackerr/unpackerr) aan, omdat het uitpakken op de juiste manier doet: het voorkomt beschadigde gedeeltelijke imports en ruimt de uitgepakte bestanden op na import.

De fout kan ook optreden als er geen geldig mediabestand in de map aanwezig is.

### Herhaalde downloads

Er zijn verschillende oorzaken van herhaalde downloads, maar een daarvan heeft te maken met aangepaste indelingen. Het is mogelijk dat de naam van de release overeenkomt met een aangepaste indeling, maar de gedownloade bestanden niet. Dit zorgt ervoor dat je telkens opnieuw de items downloadt omdat het lijkt op een upgrade, maar dat is het niet, en dan verschijnt het opnieuw en lijkt het weer op een upgrade, maar dat is het niet. Afhankelijk van je aangepaste indeling kun je dit mogelijk omzeilen door de aangepaste indeling op te nemen in je hernoemingsschema. (Schakel de aangepaste indeling in om opgenomen te worden in de hernoeming en voeg vervolgens de aangepaste indeling toe aan je hernoemingsschema)

Dit kan ook te wijten zijn aan het feit dat de download nooit daadwerkelijk wordt geïmporteerd en vervolgens ontbreekt in de wachtrij, waardoor er telkens een nieuwe download wordt opgehaald en nooit geïmporteerd. Raadpleeg de verschillende andere veelvoorkomende problemen en probleemoplossingsstappen hiervoor.

### Usenet-download mist import

Radarr kijkt alleen naar de 60 meest recente downloads in SABnzbd en NZBGet, dus als je je geschiedenis *behoudt*, betekent dit dat tijdens grote wachtrijen met importproblemen downloads stilzwijgend kunnen worden gemist en niet worden geïmporteerd. De beste manier om dit te voorkomen is door je geschiedenis leeg te houden, zodat eventuele items die nog steeds verschijnen, onderzocht moeten worden. Dit kun je bereiken door Verwijderen in te schakelen onder Voltooide en Mislukte Downloadverwerker. In NZBGet worden items dan verplaatst naar de *verborgen* geschiedenis, wat geweldig is. Helaas heeft SABnzbd geen vergelijkbare functie. Het beste wat je daar kunt bereiken, is het gebruik van de nzb-back-upmap.

### Downloadclient verwijdert items

De downloadclient mag geen verantwoordelijkheid hebben voor het verwijderen van downloads. Usenet-clients moeten zo worden geconfigureerd dat ze downloads niet uit de geschiedenis verwijderen. Torrent-clients moeten worden ingesteld zodat ze torrents niet verwijderen wanneer ze klaar zijn met seeden (pauzeren of stoppen in plaats daarvan). Dit komt doordat Radarr communiceert met de downloadclient om te weten wat er moet worden geïmporteerd, dus als ze worden *verwijderd*, is er niets om te importeren... zelfs als er een map vol met bestanden is.

Voor SABnzbd wordt dit afgehandeld met de instelling Geschiedenisbehoud.

### Download kan niet worden gekoppeld aan een bibliotheekitem

Om verschillende redenen kunnen releases niet worden geparseerd nadat ze zijn gedownload en naar de downloadclient zijn gestuurd. Activiteit => Opties => Onbekend weergeven (dit is nu standaard ingeschakeld in recente versies) toont alle items die niet anders worden genegeerd / al zijn geïmporteerd binnen de downloadclientcategorie van \*Arr. Deze moeten meestal handmatig worden toegewezen en geïmporteerd.

Redenen hiervoor zijn onder andere:
- Filmtitel heeft een `:` op TMDb en TMDb heeft geen alternatieve titel met een `-` of met een spatie ter vervanging van de `:`
- Bestandsnaam mist het vereiste jaartal
- AKA of vreemde meerdere namen; Radarr heeft beperkte ondersteuning hiervoor
- Bestandsnaam komt overeen met meerdere films
- Releasenaam of releasenummer van de indexer komt niet overeen met de bestandsnaam

Dit kan ook voorkomen als je een release in je downloadclient hebt, maar dat mediabestand (film/aflevering/boek/liedje) bestaat niet in de applicatie.

### De onderliggende verbinding is gesloten: Er is een onverwachte fout opgetreden bij het verzenden

Dit wordt veroorzaakt doordat de indexer een SSL-protocol gebruikt dat niet wordt ondersteund door de huidige .NET-versie die wordt gevonden in [Radarr => Systeem => Status](/radarr/system#status).

### De aanvraag is verlopen

Radarr ontvangt geen reactie van de client.

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
- het gebruik van Privoxy en een onjuiste configuratie daarvan

## Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigings- en netwerkproblemen oplossen met behulp van de probleemoplossingsopdrachten [in onze handleiding](/permissions-and-networking). Bespreek het anders met het ondersteuningsteam op Discord. Als dit iets is dat mogelijk een veelvoorkomend probleem is, stel dan voor om het toe te voegen aan de wiki.

# Zoeken naar indexers en trackers

- Als je [Prowlarr](/prowlarr) gebruikt, kun je de [Geschiedenis](/prowlarr/history) bekijken van alle zoekopdrachten die Prowlarr heeft ontvangen en hoe ze naar de sites zijn verzonden. Zorg ervoor dat `Parameters` is ingeschakeld in Prowlarr Geschiedenis => Opties. Het (i)-pictogram biedt aanvullende details.

## Zet het loggen op trace-niveau

> **De eerste stap is om het loggen op trace-niveau te zetten, zie [Logging en logbestanden](#logging-en-logbestanden) voor details over het aanpassen van het loggen en het doorzoeken van logbestanden. Je zult vervolgens het probleem reproduceren en de logbestanden op trace-niveau van die tijdsperiode gebruiken om het probleem te onderzoeken.** Als iemand je helpt, plaats dan context van vóór/na in een [pastebin](https://0bin.net), [Gist](https://gist.com) of een vergelijkbare site om het te laten zien. Het hoeft niet het hele bestand te zijn en het mag niet *alleen* de fout zijn. Je moet het probleem ook reproduceren terwijl taken die het logbestand spammen niet worden uitgevoerd.
{.is-danger}

## Testen van een indexer of tracker

Bij het testen van een indexer of tracker kun je in debug- of trace-logs de gebruikte URL vinden. Hieronder staat een voorbeeld van een succesvolle test, je kunt zien dat het de indexer bevraagt via een specifieke URL met specifieke parameters en vervolgens de reactie. Je kunt deze URL in je browser testen door `apikey=(verwijderd)` te vervangen door de juiste apikey, bijvoorbeeld `apikey=123`. Je kunt experimenteren met de parameters als je een foutmelding van de indexer krijgt of kijken of je connectiviteitsproblemen hebt als het helemaal niet werkt. Nadat je het in je eigen browser hebt getest, moet je het testen vanaf het systeem waarop het draait *als* je dat nog niet hebt gedaan.

## Testen van een zoekopdracht

Net als bij de indexer/tracker-test hierboven, wanneer je een zoekopdracht start terwijl je logbestanden op Debug- of Trace-niveau staan, kun je de gebruikte URL uit de logbestanden halen. Bij het testen is het het beste om zo'n specifiek mogelijke zoekopdracht te gebruiken. Een handmatige zoekopdracht is goed omdat deze specifiek is en je de resultaten in de gebruikersinterface kunt zien terwijl je de logbestanden onderzoekt.

Bij deze test kijk je naar duidelijke fouten en voer je enkele eenvoudige tests uit. Je kunt zien dat de zoekopdracht de URL `https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(verwijderd)&q=O+Brother+Where+Art+Thou` gebruikte, die je zelf kunt proberen in een browser nadat je `(verwijderd)` hebt vervangen door je apikey voor die indexer. Werkt het? Zie je de verwachte resultaten? In die URL kun je zien dat het de specifieke categorie 2000 heeft ingesteld, dus als je de verwachte resultaten niet ziet, is dit een waarschijnlijke reden. Als de film niet correct is gecategoriseerd op de indexer, moet dit worden opgelost. Kijk bij Handmatige zoekopdracht XML-uitvoer hieronder voor een voorbeeld van de uitvoer van een werkende zoekopdracht.

- Handmatige zoekopdracht XML-uitvoer

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(verwijderd)&q=O+Brother+Where+Art+Thou" rel="self" type="application/rss+xml"/>
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
<newznab:response offset="0" total="17"/>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=e83b7ae75bca71e92367fab29b036731&apikey=(verwijderd)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(verwijderd)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=e83b7ae75bca71e92367fab29b036731</comments>
<pubDate>Sat, 10 Jul 2021 08:33:22 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(verwijderd)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="e83b7ae75bca71e92367fab29b036731"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=c00a92567863801ab1a4901458ae31ba&apikey=(verwijderd)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(verwijderd)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=c00a92567863801ab1a4901458ae31ba</comments>
<pubDate>Sun, 28 Mar 2021 10:50:38 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(verwijderd)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="c00a92567863801ab1a4901458ae31ba"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=75f5be8b4cd573c2359b638350689f73&apikey=(verwijderd)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(verwijderd)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=75f5be8b4cd573c2359b638350689f73</comments>
<pubDate>Sun, 28 Jul 2019 00:46:00 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(verwijderd)" length="936738000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="936738000"/>
<newznab:attr name="guid" value="75f5be8b4cd573c2359b638350689f73"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(verwijderd)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(verwijderd)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=a0fe801d9ba0a703db7d2164e996aa1f</comments>
<pubDate>Mon, 14 Aug 2017 15:34:36 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(verwijderd)" length="9746182000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="9746182000"/>
<newznab:attr name="guid" value="a0fe801d9ba0a703db7d2164e996aa1f"/>
</item>
</channel>
</rss>
```

***Afbeeldingen nodig***

![searches-indexers-and-trackers1.png](/assets/radarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/radarr/searches-indexers-and-trackers2.png)

- Fragment van Trace-logboek

```none
Fragment van Trace-logboek voor een handmatige zoekopdracht vereist
```

- Volledig Trace-logboek van een zoekopdracht

```none
Volledige sectie van Trace-logboek voor een handmatige zoekopdracht vereist
```

## Veelvoorkomende problemen

Hieronder staan enkele veelvoorkomende problemen.

### Tracker heeft RawSearch-caps nodig

- Radarr zoekt naar `Kikis Delivery Service`, maar je tracker heeft alleen resultaten voor `Kiki's Delivery Service`
- Dit komt doordat je tracker geen normale gestandaardiseerde zoekopdrachten ondersteunt.
- De oplossing is dat de zoekmogelijkheden van de definitie van je tracker moeten worden bijgewerkt om aan te geven dat deze [RawSearch vereist en ondersteunt](https://github.com/Radarr/Radarr/issues/4502#issuecomment-981143905)
- Jackett ondersteunt de vlag, maar de mogelijkheden moeten per indexer worden bijgewerkt. Open een functieverzoek voor Jackett om deze functionaliteit toe te voegen voor je indexer.
- Prowlarr ondersteunt de vlag, maar de mogelijkheden moeten per indexer worden bijgewerkt. Open een functieverzoek voor Prowlarr om deze functionaliteit toe te voegen voor je indexer.

### Media is niet gemonitord

De film(s) is(zijn) niet gemonitord.

### Verkeerde categorieën

Onjuiste categorieën zijn waarschijnlijk de meest voorkomende oorzaak van resultaten die worden weergegeven in handmatige zoekopdrachten van een indexer/tracker, maar *niet* in Radarr. De indexer/tracker *zou* de categorie moeten weergeven in de zoekresultaten, wat je zou moeten helpen om te achterhalen wat er ontbreekt. Als je Jackett of Prowlarr gebruikt, heeft elke tracker een lijst met specifiek ondersteunde categorieën. Zorg ervoor dat je de juiste categorieën gebruikt voor Radarr. Veel mensen vinden het handig om de lijst zichtbaar te hebben in een browser-venster terwijl ze de invoer bewerken.

### Succesvolle zoekopdracht - Geen resultaten geretourneerd

Je ontvangt een bericht vergelijkbaar met `Zoekopdracht succesvol, maar er zijn geen resultaten geretourneerd van je indexer. Dit kan een probleem zijn met de indexer of je indexer categorie-instellingen.`

Dit wordt veroorzaakt doordat je indexer geen resultaten retourneert die binnen de categorieën vallen die je hebt geconfigureerd voor de indexer.

### Verkeerde resultaten

Soms retourneren indexers volledig niet-gerelateerde resultaten. Radarr geeft parameters door om de zoekopdracht te beperken, maar de geretourneerde resultaten hebben niets met de zoekopdracht te maken. Of soms zijn de resultaten grotendeels gerelateerd met een paar onjuiste resultaten. Het eerste probleem is meestal een indexer-probleem en je kunt dit zien in de trace logs. Je kunt die indexer uitschakelen en het probleem melden. Het andere probleem heeft meestal te maken met verkeerd gecategoriseerde releases, die gemeld kunnen worden bij de indexer/tracker.

### Ontbrekende resultaten

Als je resultaten op de site kunt vinden die niet worden weergegeven in Radarr, dan is je probleem waarschijnlijk een van de volgende mogelijkheden:

- [Categorieën zijn onjuist - Zie hierboven](#wrong-categories)
- Er wordt een ID (IMDbId, TMDbId, enz.) gebaseerde zoekopdracht uitgevoerd en de indexer heeft de releases niet correct gekoppeld aan dat ID. Dit is iets wat alleen je indexer kan oplossen. Zij moeten ervoor zorgen dat de release correct wordt gekoppeld aan de juiste toepasselijke ID's.
- Je zoekt niet op dezelfde manier als Radarr zoekt; Het is zeer waarschijnlijk dat de termen die je op de indexer zoekt niet overeenkomen met de zoekopdracht van Radarr. Je kunt zien hoe Radarr zoekt in de Trace Logs. Tekstgebaseerde zoekopdrachten hebben meestal het formaat `q=woorden%20en%20dingen%20hier`. Deze string is HTTP-gecodeerd en kan eenvoudig worden gedecodeerd met behulp van een online HTML-decoderings/-coderingstool.
- [Zie de FAQ voor hoe Radarr omgaat met buitenlandse filmtitels en wanneer Radarr ze zou zoeken](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

### Certificaatvalidatie

Je zult verbinding maken met de meeste indexers/trackers via https, dus je hebt een correcte werking van SSL nodig op je systeem. Dat betekent dat je tijdzone en tijd beide *correct* moeten zijn ingesteld. Het betekent ook dat je systeemcertificaten up-to-date moeten zijn.

### Bereiken van limieten

Als je je verbinding maakt via een VPN of proxy, concurreer je mogelijk met 10s, 100s of 1000s andere mensen die allemaal proberen gebruik te maken van diensten zoals Radarr, theXEM en/of je indexers en trackers. Rate limiting en DDOS-bescherming worden vaak gedaan op basis van IP-adres en je VPN-/proxy-uitgangspunt is *één* IP-adres. Tenzij je je in een repressief land bevindt zoals China, Australië of Zuid-Afrika, heb je geen VPN/proxy nodig.

Rarbg heeft de neiging om enige vorm van rate limiting toe te passen binnen hun API en geeft dan geen resultaten terug.

### IP-blokkade

Vergelijkbaar met rate limits kan het voorkomen dat bepaalde indexers - zoals Nyaa - een IP-adres volledig blokkeren. Dit is meestal semi-permanent en de oplossing is om een nieuw IP-adres te krijgen van je internetprovider of VPN-provider.

### Jaar komt niet overeen

- [Zie deze FAQ-invoer](/radarr/faq#how-does-radarr-determine-the-year-of-a-movie)
  - Radarr haalt metadata op van TMDb
  - Radarr gebruikt het jaar van de oudste **Theatrical Release**-datum en het oudste **Premier**-jaar voor overeenkomsten
- In sommige gevallen is de film uitgesteld of verschoven en komt het jaar dat door de releasegroepen wordt gebruikt niet overeen met het oudste Premier-jaar of het oudste Theatrical-jaar. In deze situaties moet je de release handmatig downloaden en importeren.

### Ontbrekend jaar

Radarr zal geen release downloaden als de naam van de release geen jaar bevat. Dit is een slechte release en kan alleen handmatig worden gedownload. Dit is een veelvoorkomend iets dat over het hoofd wordt gezien bij het proberen te achterhalen waarom een film niet zoals verwacht is gedownload.

### Het gebruik van de Jackett /all-eindpunt

Het Jackett `/all`-eindpunt is handig, maar dat is het enige voordeel ervan. Alles daarna kan problemen veroorzaken, dus het toevoegen van elke tracker afzonderlijk is vereist. Als alternatief kun je overwegen om de Jackett & NZBHydra2-alternatief [Prowlarr](/prowlarr) te gebruiken.

[Zelfs Jackett zegt dat /all vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)

Het gebruik van het all-eindpunt heeft geen voordelen (behalve verminderd beheer), alleen nadelen:

- je verliest de controle over specifieke instellingen van indexers (categorieën, zoekmodi, enz.)
- het mixen van zoekmodi (IMDB, query, enz.) kan leiden tot resultaten van lage kwaliteit
- indexer-specifieke categorieën (\>= 100000) kunnen niet worden gebruikt.
- trage indexers vertragen het algehele resultaat
- het totale aantal resultaten is beperkt tot 1000

Door elke indexer afzonderlijk toe te voegen, kun je de categorieën per indexer nauwkeurig afstemmen, wat een probleem kan zijn met het `/all`-eindpunt als het gebruik van de verkeerde categorie fouten veroorzaakt op sommige trackers. In Jackett is elke indexer beperkt tot 1000 resultaten als paginering wordt ondersteund, of 100 als dit niet het geval is. Dit betekent dat naarmate je meer en meer trackers aan Jackett toevoegt, je steeds meer kans hebt om resultaten te missen. Ten slotte, als *één* van de trackers in `/all` een fout retourneert, schakelt Jackett deze uit en krijg je nu geen enkel resultaat meer.

### Het gebruik van NZBHydra2 als enkele invoer

Het gebruik van NZBHydra2 als enkele indexer-invoer (d.w.z. 1 NZBHydra2-invoer in Radarr voor veel indexers in NZBHydra2) in plaats van meerdere (d.w.z. veel NZBHydra2-invoeren in Radarr voor veel indexers in NZBHydra2) heeft dezelfde problemen als hierboven vermeld met het `/all`-eindpunt van Jackett.

### Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigingen en netwerkproblemen oplossen met behulp van opdrachten in onze handleiding. Anders kun je het probleem bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.

## Fouten

Dit zijn enkele veelvoorkomende fouten die je kunt tegenkomen bij het toevoegen van een indexer.

### De onderliggende verbinding is gesloten: Er is een onverwachte fout opgetreden bij het verzenden

Dit wordt veroorzaakt doordat de indexer een SSL-protocol gebruikt dat niet wordt ondersteund door de huidige .NET-versie die wordt gevonden in [Radarr => Systeem => Status](/radarr/system#status).

### De aanvraag is verlopen

Radarr ontvangt geen reactie van de indexer.

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

### Probleem niet vermeld

Je kunt ook enkele veelvoorkomende machtigingen en netwerkproblemen oplossen met behulp van opdrachten in onze handleiding. Anders kun je het probleem bespreken met het ondersteuningsteam op Discord. Als dit iets is dat een veelvoorkomend probleem kan zijn, stel dan voor om het toe te voegen aan de wiki.