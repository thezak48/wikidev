---
title: Prowlarr Probleemoplossing
description: 
published: true
date: 2023-08-20T00:20:04.841Z
tags: prowlarr, probleemoplossing
editor: markdown
dateCreated: 2021-06-20T20:05:25.223Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Om hulp vragen](#om-hulp-vragen)
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
- [NGINX-fouten](#nginx-fouten)
- [Indexer-, applicatie- en downloadclientproblemen](#indexer-applicatie-en-downloadclientproblemen)
  - [Kan de framesize niet bepalen of een beschadigd frame is ontvangen](##kan-de-framesize-niet-bepalen-of-een-beschadigd-frame-is-ontvangen)
  - [Verbinding verbroken](#verbinding-verbroken)
  - [Sonarr HTTP 404-fouten](#sonarr-http-404-fouten)
  - [\*Arr HTTP 400-fouten](#arr-http-400-fouten)
  - [503 HTTP-service niet beschikbaar](#503-http-service-niet-beschikbaar)
  - [Ongeldige torrents](#ongeldige-torrents)
  - [Zoeken & indexers](#zoeken-indexers-en-trackers)

# Om hulp vragen

Heb je hulp nodig? Dat is prima, iedereen heeft soms hulp nodig. Je kunt realtime hulp krijgen via de chat op

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiële Prowlarr Discord*](https://prowlarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiële Prowlarr Subreddit*](https://reddit.com/r/prowlarr)
{.links-list}

Maar voordat je daar naartoe gaat en een bericht plaatst, zorg ervoor dat je verzoek om hulp zo goed mogelijk is. Beschrijf duidelijk het probleem en geef een korte beschrijving van je setup, inclusief zaken zoals je besturingssysteem/distributie, versie van .NET, versie van Prowlarr, downloadclient en de versie ervan. **Als je [Docker](https://www.docker.com/) gebruikt, doorloop dan eerst de [Docker-handleiding](/docker-guide), omdat dit veelvoorkomende en frequente pad/machtigingsproblemen oplost. Zorg er anders voor dat je een [docker compose](/docker-guide#docker-compose) bij de hand hebt. [Hoe je een Docker Compose genereert](https://trash-guides.info/compose)** Vertel ons wat je al hebt geprobeerd, waar je naar hebt gekeken. Gebruik de [Logging en logbestanden](#logging-en-logbestanden) sectie om je logging op te voeren naar trace, herhaal het probleem, plak de relevante context in een pastebin en voeg een link hiernaar toe in je bericht. Voeg misschien zelfs wat schermafbeeldingen toe om het probleem te verduidelijken.

Hoe meer we weten, hoe gemakkelijker het is om je te helpen.

# Logging en logbestanden

Het is waarschijnlijk ook nuttig om de [Indexer-, applicatie- en downloadclientproblemen Veelvoorkomende problemen](#indexer-applicatie-en-downloadclientproblemen) door te nemen.

> Als er wordt gevraagd om de indexerrespons te verstrekken voor ontwikkeling of debugging, lees dan verder in dit blauwe gedeelte...anders ga verder naar de onderstaande stappen. Voor het debuggen van indexerresponsen is het waarschijnlijk handig om naar `settings/development` (verborgen pagina) in Prowlarr te gaan en tijdelijk Enhanced Indexer Logging in te schakelen om de Indexer Response te loggen. Dit hoeft niet altijd aan te staan.
{.is-info}

Als er om debuglogs wordt gevraagd, bevatten je logs het woord `debug` en als er om trace-logs wordt gevraagd, bevatten je logs het woord `trace`. Als de logs die je verstrekt deze woorden niet bevatten, zijn het niet de gevraagde logs.

- Deel niet het volledige logbestand tenzij hierom wordt gevraagd.
- Upload logs niet rechtstreeks naar Discord of plak ze niet als tekstblokken, tenzij hierom wordt gevraagd.
- Deel de logs niet als bijlage, een zip-archief of iets anders dan tekst die wordt gedeeld via de hieronder genoemde services.

Om goede en bruikbare logs te verstrekken:

> Zorg ervoor dat er geen spamachtige taak wordt uitgevoerd, zoals een RSS-verversing.
{.is-warning}

1. [Verhoog de logging naar trace (Instellingen => Algemeen => Logniveau of bewerk het configuratiebestand)](#tracedebug-logs)
2. [Wis logs (Systeem => Logs => Logs wissen of verwijder alle logs in de logmap)](#logbestanden-wissen)
3. Reproduceer het probleem (Herhaal wat de dingen kapot maakt)
4. [Open het trace-logbestand (Lidarr.trace.txt) via de UI of het logbestand](#standaard-loglocatie) op het bestandssysteem en zoek de relevante context
5. Kopieer een groot stuk vóór het probleem, het probleem zelf en een groot stuk na het probleem.
6. Gebruik [Gist](https://gist.github.com/), [0bin (**Zorg ervoor dat kleurcodering is uitgeschakeld**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) of vergelijkbare sites - met uitzondering van de hieronder genoemde sites om te vermijden - om de gekopieerde logs hierboven te delen

**Waarschuwingen:**
- **Gebruik [pastebin.com](https://pastebin.com) niet, omdat hun filters de neiging hebben om de logs te blokkeren.
- Gebruik [pastebin.pl](https://pastebin.pl) niet, omdat hun site vaak niet toegankelijk is.
- Gebruik [JustPasteIt](https://justpaste.it/) niet, omdat hun site het bekijken van logs niet vergemakkelijkt.
- Upload je logbestand niet als bestand.
- Upload en deel je logs niet via Google Drive, Dropbox of een andere site die hierboven niet is genoemd.
- Archiveer je logs niet (zip, tar (tarball), 7zip, enz.).
- Deel geen console-uitvoer, docker-containeruitvoer of iets anders dan de specifieke applicatielogs

**Belangrijke opmerking:**
- Wanneer je [0bin](https://0bin.net/) gebruikt, zorg er dan voor dat kleurcodering is uitgeschakeld en dat je de logs niet verbrandt nadat je ze hebt gelezen.

- Als alternatief, als je op zoek bent naar een specifieke invoer in een oud logbestand, maar niet zeker weet welke, kun je N++ gebruiken. Je kunt de functie "Zoeken in bestanden" van Notepad++ gebruiken om oude logbestanden te doorzoeken indien nodig.
- **Alleen Unix:** Als je op zoek bent naar een specifieke invoer in een oud logbestand, maar niet zeker weet welke, kun je grep gebruiken. Als je bijvoorbeeld informatie wilt vinden over de film/serie/boek/lied/indexer "Shooter", kun je het volgende commando uitvoeren: `grep -inr -C 100 -e 'Shooter' /pad/naar/logs/*.trace*.txt` Als je [Appdata Directory](/prowlarr/appdata-directory) zich in je home-map bevindt, voer je het volgende uit: `grep -inr -C 100 -e 'Shooter' /home/$Gebruiker/.config/logs/*.trace*.txt`

```none

    * De vlaggen hebben de volgende functies
    * -i: hoofdletterongevoelig
    * -n: toon regelnummer
    *  -r: controleer recursief alle bestanden in het pad
    * -C: geef het aantal regels voor en na de gevonden regel
    * -e: het te zoeken patroon

```

## Standaard loglocatie

De logbestanden bevinden zich in de [Appdata Directory](/prowlarr/appdata-directory) van Prowlarr, in de map logs/. Je kunt ook toegang krijgen tot de logbestanden vanuit de UI via Systeem => Logs => Bestanden.

> Let op: De tabel Logs ("Gebeurtenissen") in de UI is niet hetzelfde als de logbestanden en is niet zo nuttig. Als er om logs wordt gevraagd, kopieer/plak dan uit de logbestanden en niet uit de tabel.
{.is-info}

## Update loglocatie

De update logbestanden bevinden zich in de [Appdata Directory](/prowlarr/appdata-directory) van Prowlarr, in de map UpdateLogs/.

## Logbestanden delen

De logbestanden kunnen lang zijn en moeilijk te lezen als onderdeel van een forum- of Reddit-bericht en ze zijn spamachtig in Discord, dus gebruik alsjeblieft [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) of een andere vergelijkbare pastebin-site. Het hele bestand is meestal niet nodig, alleen een goede hoeveelheid context van vóór en na het probleem/fout. Vergeet niet te wachten tot spamachtige taken zoals een RSS-synchronisatie of bibliotheekverversing zijn voltooid.

## Trace/Debug logs

Je kunt het logniveau wijzigen via Instellingen => Algemeen => Logging. Prowlarr hoeft niet opnieuw te worden gestart voor de wijziging van kracht wordt. Deze wijziging heeft alleen invloed op de logbestanden, niet op de loggingdatabase. De nieuwste debug/trace logbestanden hebben respectievelijk de namen `prowlarr.debug.txt` en `prowlarr.trace.txt`.

Als je geen toegang hebt tot de UI om het logniveau in te stellen, kun je dit doen door config.xml in de AppData-directory te bewerken en de waarde van LogLevel in te stellen op Debug of Trace in plaats van Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Logbestanden wissen

Je kunt logbestanden en de logdatabase rechtstreeks vanuit de UI wissen, onder `Systeem` => `Logs` => `Bestanden` en `Systeem` => `Logs` => `Verwijderen` (Prullenbakpictogram).

# Meerdere logbestanden

Prowlarr maakt gebruik van rollende logbestanden die beperkt zijn tot 1 MB elk. Het huidige logbestand is altijd Prowlarr.txt, voor de andere bestanden is Prowlarr.0.txt de op een na nieuwste (hoe hoger het nummer, hoe ouder het bestand). Dit logbestand bevat `fatal`, `error`, `warn` en `info` vermeldingen.

Wanneer het debuglogniveau is ingeschakeld, zijn er extra `prowlarr.debug.txt` rollende logbestanden aanwezig. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info` en `debug` vermeldingen. Ze beslaan meestal een periode van 40 uur.

Wanneer het tracelogniveau is ingeschakeld, zijn er extra `prowlarr.trace.txt` rollende logbestanden aanwezig. Deze logbestanden bevatten `fatal`, `error`, `warn`, `info`, `debug` en `trace` vermeldingen. Vanwege de uitgebreide trace-informatie beslaan ze meestal hooguit een paar uur, en soms minder dan een minuut als je iets intensiefs doet.

# Herstellen na een mislukte update

We doen er alles aan om problemen bij het upgraden te voorkomen, maar als ze toch optreden, leiden deze stappen je door de te nemen stappen om je installatie te herstellen.

## Het probleem vaststellen

- De beste plek om te kijken wanneer de applicatie niet start na een update, is het controleren van de [update logs](#update-loglocatie) en controleren of de update succesvol is voltooid. Als er geen probleem is gevonden, kijk dan naar je reguliere applicatielogbestanden voordat je opnieuw probeert te starten, gebruik [Logging](/prowlarr/settings#logging) en [Logbestanden](/prowlarr/system#logbestanden) om ze te vinden en het logniveau te verhogen.
- Het meest voorkomende probleem is dat het systeem waarop de app is geïnstalleerd heeft geknoeid met de `/tmp`-directory en kritieke \*Arr-bestanden heeft verwijderd tijdens de upgrade, waardoor zowel de upgrade als de rollback mislukken. In dit geval installeer je eenvoudigweg opnieuw op de bestaande beschadigde installatie.

### Migratieprobleem

- Migratiefouten zijn niet identiek, maar hier is een voorbeeld:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Machtigingsprobleem

- Machtigingsproblemen ontstaan doordat de applicatie geen toegang heeft tot de relevante tijdelijke mappen en/of de app-binmap. Los de machtigingen op, zodat de gebruiker/groep waarin de applicatie wordt uitgevoerd de juiste toegang heeft.

- Synology-gebruikers kunnen te maken krijgen met de Synology-bug `Toegang tot het pad '/proc/{some number}/maps is geweigerd`

- Synology-gebruikers kunnen ook te maken krijgen met een tekort aan ruimte in `/tmp` op bepaalde NAS-apparaten. Je moet een ander `/tmp`-pad opgeven voor de app. Raadpleeg SynoCommunity of andere Synology-ondersteuningskanalen voor hulp hierbij.

## Het probleem oplossen

Bij een migratieprobleem kun je op dit moment niet veel doen. Als het probleem specifiek voor jou is (of er nog geen berichten zijn), maak dan een bericht aan op [onze subreddit](https://reddit.com/r/prowlarr) of kom langs op onze [discord](https://prowlarr.com/discord). Als er anderen zijn met hetzelfde probleem, wees dan gerust dat we eraan werken.

> Zorg ervoor dat je niet hebt geprobeerd een database van `nightly` te gebruiken op de stabiele versie. Het wisselen van branches wordt afgeraden.{.is-info}

### Machtigingsproblemen

- Los de machtigingen op zodat de gebruiker/groep waarin de applicatie wordt uitgevoerd toegang heeft (lezen en schrijven) tot zowel `/tmp` als de installatiemap van de applicatie.

- Voor Synology-gebruikers die problemen ondervinden met `/proc/###/maps` kan het stoppen van Sonarr of de andere \*Arr-applicaties en het bijwerken ervan dit probleem oplossen. Dit is een probleem met het SynoCommunity-pakket.

### Handmatig upgraden

Download de nieuwste release van onze website.

Installeer de update (.exe) of pak de inhoud uit (.zip) over je bestaande installatie en voer Prowlarr op de normale manier opnieuw uit.

# NGINX-fouten

In je Prowlarr-setup heb je deze regel nodig:

`proxy_set_header Host $host;`

Als je een andere `proxy_set_header` hebt, moet je deze vervangen door de bovenstaande regel.

# Indexer-, applicatie- en downloadclientproblemen

- Op een basisniveau moet Prowlarr kunnen communiceren met je indexers.
- Als je applicatiesynchronisatie gebruikt, moet Prowlarr ook kunnen communiceren met je applicaties en moeten de applicaties kunnen communiceren met Prowlarr.
- Als je een downloadclient in Prowlarr hebt voor handmatige downloads in Prowlarr, moet Prowlarr kunnen communiceren met je downloadclient.

> Let op dat logs die aangeven dat indexer ID 0 wordt bevraagd: De ID 0 is een generiek test-eindpunt waarmee we kunnen testen of \*Arr kan terugbellen en verbinding kan maken met Prowlarr zonder daadwerkelijk afhankelijk te zijn van een werkende indexer.
{.is-info}

Hieronder staan enkele veelvoorkomende oorzaken

## Kan de framesize niet bepalen of een beschadigd frame is ontvangen

`Kan de framesize niet bepalen of een beschadigd frame is ontvangen.`

Prowlarr had een beveiligingsprobleem bij het verbinden met de site.

Dit wordt meestal veroorzaakt door:

- lokale DNS-problemen - Probeer over te schakelen naar een andere DNS-provider

## Verbinding verbroken

`De aanvraag is verlopen`

Prowlarr ontvangt geen reactie van de client. [Zie onze Algemene netwerk- en machtigingsproblemen Troubleshooting-gids](/permissions-and-networking)

Dit wordt meestal veroorzaakt door:

- onjuist geconfigureerde of gebruik van een VPN
- onjuist geconfigureerde of gebruik van een proxy
- lokale DNS-problemen - Probeer over te schakelen naar een andere DNS-provider
- lokale IPv6-problemen - meestal is IPv6 ingeschakeld, maar niet functioneel
- het gebruik van Privoxy

## Sonarr HTTP 404-fouten

- Dit wordt meestal veroorzaakt door het uitvoeren van een end-of-life (EOL) versie van Sonarr die niet de v3 API-eindpunten heeft
- Prowlarr ondersteunt Sonarr v2 niet
- Prowlarr ondersteunt alleen Sonarr v3

## \*Arr HTTP 400-fouten

- Zie deze FAQ-invoer: [Prowlarr synchroniseert X Indexer niet met App](/prowlarr/faq#prowlarr-will-not-sync-x-indexer-to-app)

## 503 HTTP-service niet beschikbaar

- Dit wordt meestal veroorzaakt doordat je tracker je blokkeert via Cloudflare en [FlareSolverr](https://github.com/FlareSolverr/FlareSolverr) vereist

## Ongeldige torrents

- Probeer de link te downloaden via de URL en variabelen die Prowlarr heeft gebruikt.
- Probeer de torrent te downloaden via Prowlarr (gebruik de Prowlarr-link die de app heeft gebruikt om het bestand te verkrijgen).
- Zorg ervoor dat je cookie of andere referenties voor je indexer niet verlopen zijn en geldig zijn.
- Als het probleem veroorzaakt wordt door Prowlarr, dien dan een bugrapport in.

## Zoeken in Indexers en Trackers

- [Lidarr Zoeken & Indexers](/lidarr/troubleshooting#searches-indexers-and-trackers)
- [Radarr Zoeken & Indexers](/radarr/troubleshooting#searches-indexers-and-trackers)
- [Readarr Zoeken & Indexers](/readarr/troubleshooting#searches-indexers-and-trackers)
- [Sonarr Zoeken & Indexers](/sonarr/troubleshooting#searches-indexers-and-trackers)
{.links-list}