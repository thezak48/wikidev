---
title: Prowlarr FAQ
description: Prowlarr FAQ
published: true
date: 2023-08-28T19:29:30.585Z
tags: prowlarr, faq
editor: markdown
dateCreated: 2021-11-03T03:01:18.079Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
  - [Gedwongen authenticatie](#gedwongen-authenticatie)
  - [Hoe kan ik statistieken resetten?](#hoe-kan-ik-statistieken-resetten)
  - [Categorie niet beschikbaar of ontbreekt](#categorie-niet-beschikbaar-of-ontbreekt)
  - [Kan ik een (generieke) Torznab- of Newznab-indexer toevoegen?](#kan-ik-een-generieke-torznab-of-newznab-indexer-toevoegen)
  - [Kan ik een (generieke) Torrent RSS-feed toevoegen?](#kan-ik-een-generieke-torrent-rss-feed-toevoegen)
  - [Kan ik flaresolverr-indexers gebruiken?](#kan-ik-flaresolverr-indexers-gebruiken)
  - [Hoe kan ik een indexer toevoegen die niet werkt of niet functioneert?](#hoe-kan-ik-een-indexer-toevoegen-die-niet-werkt-of-niet-functioneert)
  - [Prowlarr synchroniseert niet met Sonarr](#prowlarr-synchroniseert-niet-met-sonarr)
  - [Prowlarr synchroniseert X Indexer niet met de app](#prowlarr-synchroniseert-x-indexer-niet-met-de-app)
  - [Welke \*Arr Indexer-instellingen worden vergeleken voor volledige app-synchronisatie?](#welke-arr-indexer-instellingen-worden-vergeleken-voor-volledige-app-synchronisatie)
  - [Hoe update ik Prowlarr?](#hoe-update-ik-prowlarr)
    - [Kan ik Prowlarr updaten binnen mijn Docker-container?](#kan-ik-prowlarr-updaten-binnen-mijn-docker-container)
    - [Het installeren van een nieuwere versie](#het-installeren-van-een-nieuwere-versie)
      - [Native](#native)
      - [Docker](#docker)
  - [Kan ik terugschakelen van 'nightly' naar 'develop'?](#kan-ik-terugschakelen-van-nightly-naar-develop)
  - [Kan ik schakelen tussen branches?](#kan-ik-schakelen-tussen-branches)
  - [Help, mijn Mac zegt dat Prowlarr niet kan worden geopend omdat de ontwikkelaar niet kan worden geverifieerd](#help-mijn-mac-zegt-dat-prowlarr-niet-kan-worden-geopend-omdat-de-ontwikkelaar-niet-kan-worden-geverifieerd)
  - [Help, mijn Mac zegt dat Prowlarr.app beschadigd is en niet kan worden geopend](#help-mijn-mac-zegt-dat-prowlarrapp-beschadigd-is-en-niet-kan-worden-geopend)
  - [Hoe kan ik een functie aanvragen voor Prowlarr?](#hoe-kan-ik-een-functie-aanvragen-voor-prowlarr)
  - [Ik krijg een foutmelding: Database disk image is malformed](#ik-krijg-een-foutmelding-database-disk-image-is-malformed)
  - [Ik gebruik Prowlarr op een Mac en het werkt plotseling niet meer. Wat is er gebeurd?](#ik-gebruik-prowlarr-op-een-mac-en-het-werkt-plotseling-niet-meer-wat-is-er-gebeurd)
  - [Hoe schakel ik over van de Windows-service naar een Tray-app?](#hoe-schakel-ik-over-van-de-windows-service-naar-een-tray-app)
  - [Hoe maak ik een back-up/herstel ik Prowlarr?](#hoe-maak-ik-een-back-upherstel-ik-prowlarr)
    - [Een back-up maken van Prowlarr](#een-back-up-maken-van-prowlarr)
      - [Gebruik van ingebouwde back-up](#gebruik-van-ingebouwde-back-up)
      - [Gebruik van het bestandssysteem rechtstreeks](#gebruik-van-het-bestandssysteem-rechtstreeks)
    - [Herstellen van een back-up](#herstellen-van-een-back-up)
      - [Gebruik van zip-back-up](#gebruik-van-zip-back-up)
      - [Gebruik van back-up van het bestandssysteem](#gebruik-van-back-up-van-het-bestandssysteem)
      - [Bestandssysteemherstel op Synology NAS](#bestandssysteemherstel-op-synology-nas)
  - [WebUI laadt alleen op localhost op Windows](#webui-laadt-alleen-op-localhost-op-windows)
  - [Het vinden van cookies](#het-vinden-van-cookies)
  - [uTorrent werkt niet meer](#utorrent-werkt-niet-meer)
  - [Ik kreeg een pop-up dat config.xml beschadigd is, wat nu?](#ik-kreeg-een-pop-up-dat-configxml-beschadigd-is-wat-nu)
  - [Ongeldig certificaat en andere HTTPS- of SSL-problemen](#ongeldig-certificaat-en-andere-https-of-ssl-problemen)
  - [Help, ik ben buitengesloten](#help-ik-ben-buitengesloten)
  - [Vreemde UI-problemen](#vreemde-ui-problemen)
  - [VPNs, Prowlarr en de \*ARRs](#vpns-prowlarr-en-de-arrs)
  - [Hoe voorkom ik dat de browser wordt gestart bij het opstarten?](#hoe-voorkom-ik-dat-de-browser-wordt-gestart-bij-het-opstarten)
  - [Kan ik in één keer alle indexers toevoegen?](#kan-ik-in-één-keer-alle-indexers-toevoegen)

## Gedwongen authenticatie

Als Prowlarr zo is ingesteld dat de gebruikersinterface van buiten uw lokale netwerk toegankelijk is, moet u een vorm van authenticatie inschakelen om toegang te krijgen tot de gebruikersinterface. Dit is ook steeds vaker vereist door trackers en indexers.

Vanaf Prowlarr v1 is authenticatie verplicht.

### Authenticatiemethode

- `Basic` (Browser pop-up) - Deze optie toont een klein pop-upvenster wanneer u Prowlarr opent, waarin u een gebruikersnaam en wachtwoord kunt invoeren.
- `Forms` (Inlogpagina) - Deze optie toont een inlogscherm dat lijkt op de inlogschermen van andere websites, waarmee u kunt inloggen op Prowlarr.
- `External` - Configuratie alleen mogelijk via configuratiebestand
  - Als u een **externe authenticatie** gebruikt, zoals Authelia, Authetik, NGINX Basic auth, enzovoort, kunt u dubbele authenticatie voorkomen door de app af te sluiten, `<AuthenticationMethod>External</AuthenticationMethod>` in het [configuratiebestand](/prowlarr/appdata-directory) in te stellen en de app opnieuw te starten. **Let op dat meerdere `AuthenticationMethod`-vermeldingen in het bestand niet worden ondersteund en alleen de bovenste waarde wordt gebruikt**.

### Vereiste authenticatie

- Als u de app niet extern blootstelt en/of geen authenticatie vereist voor lokale (bijv. LAN) toegang, wijzig dan in Instellingen => Algemene beveiliging => Vereiste authenticatie naar `Uitgeschakeld voor lokale adressen`
  - Het equivalent hiervan in het configuratiebestand is `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Hoe kan ik statistieken resetten?

- Om uw statistieken te resetten en de geschiedenis te wissen, volgt u de volgende stappen:

1. Ga naar Geschiedenis => Opties
1. Stel Geschiedenisopruiming in op `1`. Hierdoor blijft alleen de geschiedenis en statistieken van gisteren behouden.
1. Ga naar Systeem => Taken
1. Voer de taak 'Geschiedenis opruimen' uit
1. Voer de taak 'Housekeeping' uit
1. Ga terug naar Geschiedenis => Opties
1. Stel Geschiedenisopruiming in op de gewenste bewaarperiode voor geschiedenis en statistieken

## Categorie niet beschikbaar of ontbreekt

- Houd er rekening mee dat aangepaste/niet-standaard indexer-specifieke categorieën worden toegewezen aan standaardcategorieën, zodat zoeken in standaardcategorieën alle aangepaste categorieën omvat. Bekijk de definitie van de categorie-toewijzing van uw specifieke indexer voor meer informatie.

## Kan ik een (generieke) Torrent RSS-feed toevoegen?

Ja. Gebruik "TorrentRSS".

De volgende attributen zijn verplicht:

- guid
- title
- infohash
- enclosure of link

De volgende attributen zijn optioneel, maar aanbevolen:

- size
- pubDate

## Kan ik een (generieke) Torznab- of Newznab-indexer toevoegen?

- Ja.
- Ga naar `Indexers` => `Indexer toevoegen` (<kb>+</kb>) => `Generieke Torznab` of `Generieke Newznab`

## Kan ik flaresolverr-indexers gebruiken?

- Ja.

1. Configureer uw flaresolverr-instantie door deze toe te voegen als proxy in [Instellingen => Indexers](/prowlarr/settings#indexer-proxies)
1. Voeg een tag toe aan de gemaakte flaresovlerr-proxy
1. Voeg dezelfde tag toe aan uw [Indexer](/prowlarr/indexers)

> De tags moeten overeenkomen en Cloudflare moet worden gedetecteerd om Flaresolverr te kunnen gebruiken. Een Flaresolverr-proxy is uitgeschakeld als er geen tags worden gebruikt.
{.is-warning}

> [Zie TRaSH's handleidingen over "Hoe Flaresolverr in te stellen"](https://trash-guides.info/Prowlarr/prowlarr-setup-flaresolverr/) voor meer informatie.
{.is-info}

## Hoe kan ik een indexer toevoegen die niet werkt of niet functioneert?

- Volg de standaardstappen om de indexer toe te voegen, maar let op de volgende wijzigingen.
- Schakel het selectievakje 'Ingeschakeld' uit
- Druk op 'Opslaan'
- Druk nogmaals op 'Opslaan' om een geforceerde opslag te activeren
- Bewerk de indexer (sleutelpictogram)
- Schakel het selectievakje 'Ingeschakeld' in
- Druk op 'Opslaan'
- Druk nogmaals op 'Opslaan' om een geforceerde opslag te activeren

## Prowlarr synchroniseert niet met Sonarr

- Prowlarr ondersteunt alleen Sonarr v3+
- Sonarr v2 (voorheen nzbdrone) wordt niet ondersteund door Prowlarr en ook niet in het algemeen. Het is sinds maart 2021 buiten gebruik gesteld.

## Prowlarr synchroniseert X Indexer niet met de app

- Prowlarr synchroniseert alleen als 'Toevoegen en verwijderen' of 'Volledige synchronisatie' is ingeschakeld voor de app.
- Alleen in gevallen waarin een app en indexer overeenkomende tags hebben of helemaal geen tags hebben, wordt een indexer gesynchroniseerd met een app.
- Indexers worden gesynchroniseerd op basis van de mogelijkheden/categorieën die ze beweren te ondersteunen.
  - Als een indexer alleen tv-categorieën ondersteunt, wordt deze niet gesynchroniseerd met Lidarr, Radarr en Readarr.
- Een bepaalde indexer wordt alleen gesynchroniseerd met Sonarr als "Ondersteunde" categorieën kunnen worden geselecteerd als een geavanceerde instelling op app-niveau.
- Indexers worden niet gesynchroniseerd als de specifieke categorieën die door de indexer worden ondersteund niet zijn geselecteerd in Instellingen => Toepassing => {App} => Synchronisatiecategorieën (Geavanceerde instellingen) en er worden geen logboekmeldingen weergegeven van een synchronisatiepoging.
- De meest voorkomende oorzaak hiervan is dat de \*Arrs alleen indexers accepteren waarvan de testquery's resultaten retourneren die ten minste één van de geconfigureerde categorieën bevatten. Met andere woorden, als u synchroniseert met een app en de lege query van uw indexer retourneert geen resultaten met een release binnen de categorieën die geconfigureerd zijn voor de app, dan kan de indexer niet aan \*Arr worden toegevoegd.
- De specifieke foutmelding zal een HTTP 400 van \*Arr zijn met de melding `Query successful, but no results in the configured categories were returned from your indexer. This may be an issue with the indexer or your indexer category settings.` (Query succesvol, maar er zijn geen resultaten geretourneerd in de geconfigureerde categorieën van uw indexer. Dit kan een probleem zijn met de indexer of uw indexer-categorie-instellingen.)
  - Mogelijk kan die indexer eenvoudigweg niet worden gebruikt met die \*Arr. Dit komt vaak voor bij pogingen om openbare trackers of usenet-indexers te gebruiken met Readarr en Lidarr.
  - Pas de gesynchroniseerde categorieën aan in de geavanceerde instellingen voor de \*Arr-toepassing binnen Prowlarr aan.
    - Let op dat bepaalde trackers - voornamelijk "slechte" openbare trackers - vereisen dat u de categorie '8000 - Overig' selecteert en synchroniseert. Dit wordt vaak - maar niet altijd - vermeld in de details van de tracker in Prowlarr.
  - Probeer het later opnieuw.
  - Als het probleem aanhoudt, heeft u mogelijk een beschadigde database. Controleer uw logboeken op meldingen van `Database disk image is malformed` of `Error creating main database`. Zie [deze sectie](https://wiki.servarr.com/prowlarr/faq#i-am-getting-an-error-database-disk-image-is-malformed) voor mogelijke oplossingen.

## Welke \*Arr Indexer-instellingen worden vergeleken voor volledige app-synchronisatie?

- App/Prowlarr: Indexernaam
- App/Prowlarr: RSS in-/uitschakelen
- App/Prowlarr: Automatisch zoeken in-/uitschakelen
- App/Prowlarr: Interactief zoeken in-/uitschakelen
- App/Prowlarr: Indexerprioriteit
- App/Prowlarr: API-sleutel
- App/Prowlarr: URL
- App/Prowlarr: Basis-URL
- App/Prowlarr: Poort
- App/Prowlarr: Categorieën
- App/Prowlarr: Seedratio en seedtijd
- App/Prowlarr: Minimale seeders
- App/Prowlarr: *Alle andere instellingen die configureerbaar/zelf te beheren zijn in Prowlarr*
- Prowlarr: Implementatie (bijv. YML of C#)

Met volledige synchronisatie worden indexers gesynchroniseerd en bijgewerkt in \*Arr als een van de bovenstaande instellingen verandert tussen de \*Arr-app en Prowlarr.

## Hoe update ik Prowlarr?

- Ga naar Instellingen en vervolgens het tabblad Algemeen en toon geavanceerde instellingen (gebruik de schakelaar bij de opslaan-knop).

1. Wijzig in de sectie Updates de naam van de branch naar `master`, `develop` of `nightly`
1. Sla op

*Dit zal de bits van die branch niet onmiddellijk installeren, dit gebeurt tijdens de volgende update.*

- `master` - ![Huidige Master/Stabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) -    (Standaard/Stabiel): Het is getest door gebruikers op de develop- en nightly-branches en er zijn geen grote problemen bekend. Op GitHub is dit de `master`-branch.

- `develop` - ![Huidige Develop/Bèta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) -  (Bèta): Dit is de testversie. Uitgebracht na getest te zijn in nightly om ervoor te zorgen dat er geen onmiddellijke problemen zijn. Nieuwe functies en bugfixes worden hier als eerste uitgebracht na nightly. Het kan als semi-stabiel worden beschouwd, maar het is nog steeds `bèta`.

> Op GitHub is dit een momentopname van de `develop`-branch op een specifiek moment.
{.is-warning}

- `nightly` - ![Huidige Nightly/Onstabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) -  (Alpha/Onstabiel): Dit is de allernieuwste versie. Het wordt uitgebracht zodra de code is toegevoegd en alle geautomatiseerde tests zijn geslaagd. Deze build is mogelijk nog niet door ons of andere gebruikers gebruikt. Er is geen garantie dat het in sommige gevallen zelfs zal werken. Deze branch wordt alleen aanbevolen voor gevorderde gebruikers. Problemen en zelfonderzoek worden verwacht in deze branch. ***Gebruik deze branch alleen als u weet wat u doet en bereid bent om uw handen vuil te maken om een mislukte update te herstellen.*** Deze versie wordt onmiddellijk bijgewerkt.

> **Waarschuwing: U kunt mogelijk niet terugschakelen naar `develop` nadat u naar deze branch hebt geschakeld.** Op GitHub is dit de `develop`-branch.
{.is-danger}

- Opmerking: Als u Prowlarr via Docker installeert, voegt u `:latest`, `:testing`, `:develop` of `:nightly` toe aan het einde van uw container-tag, afhankelijk van wie uw builds maakt.

|                                                                      | `master` (stabiel) ![Huidige Master/Stabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Huidige Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) | `nightly` (onstabiel) ![Huidige Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/prowlarr)                       | `latest`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-prowlarr) | `latest`                                                                                                                                                                                                             | `develop`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |

### Kan ik Prowlarr bijwerken in mijn Docker-container?

- *Technisch gezien wel.* **Maar dat zou je absoluut niet moeten doen.** Het is een belangrijk principe van Docker. Er kunnen databaseproblemen ontstaan als je je installatie bijwerkt naar de meest recente `nightly` en vervolgens de Docker-container zelf bijwerkt (mogelijk naar een oudere versie).

### Het installeren van een nieuwere versie

#### Native

1. Ga naar Systeem en vervolgens het tabblad Updates
1. Nieuwere versies die nog niet zijn geïnstalleerd, hebben een updateknop naast zich. Door op die knop te klikken, wordt de update geïnstalleerd.

#### Docker

1. Haal je tag opnieuw op en werk je container bij

## Kan ik overschakelen van `nightly` naar `develop`?

## Kan ik wisselen tussen branches?

- Als de versie identiek is, kun je overschakelen. Controleer anders bij het ontwikkelingsteam of je kunt overschakelen van `nightly` naar `develop`; of van `develop` naar `nightly` voor jouw specifieke build.
- Als je deze instructies niet opvolgt, kan je Prowlarr onbruikbaar worden of fouten veroorzaken. Je bent gewaarschuwd.
  - De meest voorkomende fouten zijn databasefouten met ontbrekende kolommen of tabellen.

## Help, mijn Mac zegt dat Prowlarr niet kan worden geopend omdat de ontwikkelaar niet kan worden geverifieerd

- Dit is eenvoudig, zie deze link voor meer informatie [hier](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
- Als alternatief moet je Prowlarr mogelijk zelf ondertekenen `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine`

![faq_1_mac.png](/assets/general/faq_1_mac.png)

## Help, mijn Mac zegt dat Prowlarr.app beschadigd is en niet kan worden geopend

Dat komt ofwel door een beschadigde download (dus probeer het opnieuw), of door de hierboven beantwoorde beveiligingsproblemen.

## Hoe kan ik een functie aanvragen voor Prowlarr?

Om een functie aan te vragen voor Prowlarr, zoek je eerst op GitHub om er zeker van te zijn dat er geen vergelijkbaar verzoek bestaat, klik dan [hier](https://github.com/Prowlarr/Prowlarr/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=) om je verzoek toe te voegen.

## Ik krijg een foutmelding: Database disk image is malformed

- **Fouten van `Error creating log database` duiden op problemen met logs.db**
  - Dit kan snel worden opgelost door de database een andere naam te geven of te verwijderen. De logdatabase bevat onbelangrijke informatie over de geschiedenis van opdrachten en installatiegeschiedenis van updates, en Info-, Warn- en Error-vermeldingen.
- **Fouten van `Error creating main database` of algemene `database disk image is malformed` zonder specifieke database duiden op problemen met prowlarr.db**
  - Ga verder met de onderstaande stappen
- Dit betekent dat je SQLite-database, waarin de meeste informatie voor Prowlarr wordt opgeslagen, beschadigd is. Je hebt de optie om te proberen (een) back-up(s) te herstellen, de bestaande database te herstellen, de back-up(s) te herstellen, of als niets anders werkt, opnieuw te beginnen met een nieuwe database.
- Deze fout kan optreden als het databasebestand niet beschrijfbaar is door de gebruiker/groep waarin \*Arr wordt uitgevoerd. Problemen met machtigingen zullen waarschijnlijk alleen optreden bij nieuwe installaties, gemigreerde installaties naar een nieuwe server, als je onlangs de machtigingen van je appdata-directory hebt gewijzigd, of als je de gebruiker en groep \*Arr hebt gewijzigd.
- Je beste en eerste optie is om [te proberen een back-up te herstellen](#hoe-back-up-ik-mijn-prowlarr).
- Je kunt ook proberen je database te herstellen. Dit is meestal de enige optie wanneer dit probleem optreedt na een update. Probeer het [sqlite3-commando `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Als je sqlite geen `.recover` heeft of als je een meer GUI-vriendelijke (bijv. Windows) methode wilt, volg dan [onze instructies op deze wiki](/useful-tools#recovering-a-corrupt-db-ui).
- Een andere mogelijke oorzaak van een fout met je database is dat je je database op een netwerkstation plaatst (nfs of smb of iets anders dat niet lokaal is). **SQLite is ontworpen voor situaties waarin de gegevens en de toepassing op dezelfde machine bestaan.** Daarom moet je \*Arr AppData-map (/config mount voor docker) zich op lokale opslag bevinden. [SQLite en netwerkstations werken niet goed samen en zullen uiteindelijk een beschadigde database veroorzaken](https://www.sqlite.org/draft/useovernet.html).
- Als je mergerFS gebruikt, moet je `direct_io` verwijderen, omdat SQLite mmap gebruikt dat niet wordt ondersteund door `direct_io`, zoals uitgelegd in de mergerFS [documentatie hier](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Ik gebruik Prowlarr op een Mac en het werkt plotseling niet meer. Wat is er gebeurd?

Dit komt waarschijnlijk door een bug in MacOS waardoor de Prowlarr-database beschadigd is geraakt. Raadpleeg de FAQ-invoer voor het herstellen van een beschadigde database.

## Hoe schakel ik over van de Windows-service naar een systeemvaktoepassing?

- Sluit Prowlarr af
- Voer serviceuninstall.exe uit in de Prowlarr-map
- Voer Prowlarr.exe eenmaal uit als beheerder om de juiste machtigingen te geven en de firewall te openen. Zodra dit is voltooid, kun je het sluiten en normaal uitvoeren.
- (Optioneel) Plaats een snelkoppeling naar Prowlarr.exe in de opstartmap om automatisch op te starten bij het opstarten.

## Hoe maak ik een back-up/herstel ik Prowlarr?

### Een back-up maken van Prowlarr

#### Gebruik de ingebouwde back-up

- Ga naar Systeem => Backup in de Prowlarr-UI
- Klik op de knop Backup
- Download de zip nadat de back-up is gemaakt om deze veilig te bewaren

#### Gebruik het bestandssysteem rechtstreeks

- Zoek de locatie van de AppData-map voor Prowlarr op  
  - Ga via de Prowlarr-UI naar Systeem => Over  
  - [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- Stop Prowlarr - Dit voorkomt dat de database beschadigd raakt
- Kopieer de inhoud naar een veilige locatie

### Herstellen van een back-up

> Herstellen naar een besturingssysteem met andere paden werkt niet (Windows naar Linux, Linux naar Windows, Windows naar OS X of OS X naar Windows), overschakelen tussen OS X en Linux kan werken, omdat beide paden bevatten `/` in plaats van `\` dat Windows gebruikt, maar dit wordt niet ondersteund. Je moet alle paden in de database handmatig bewerken.
{.is-warning}

#### Gebruik de zip-back-up

- Installeer Prowlarr opnieuw (indien van toepassing / nog niet geïnstalleerd)
- Voer Prowlarr uit
- Ga naar Systeem => Backup
- Selecteer Herstel Backup
- Selecteer Kies bestand
- Selecteer je back-up-zipbestand
- Selecteer Herstellen

#### Gebruik de back-up van het bestandssysteem

- Installeer Prowlarr opnieuw (indien van toepassing / nog niet geïnstalleerd)
- Zoek de locatie van de AppData-map voor Prowlarr op  
  - Voer Prowlarr eenmaal uit en ga via de UI naar Systeem => Over  
  - [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- Stop Prowlarr
- Verwijder de inhoud van de AppData-map **(Inclusief de .db-wal/.db-journal-bestanden als ze bestaan)**
- Herstel vanuit je back-up
- Start Prowlarr
- Zolang de paden hetzelfde zijn, wordt alles opgepakt waar het was gebleven

#### Bestandssysteemherstel op Synology NAS

> LET OP: Herstellen op een Synology vereist kennis van Linux en Root SSH-toegang tot het Synology-apparaat.
{.is-warning}

- Installeer Prowlarr opnieuw (indien van toepassing / nog niet geïnstalleerd)
- Zoek de locatie van de AppData-map voor Prowlarr op  
  - Voer Prowlarr eenmaal uit en ga via de UI naar Systeem => Over  
  - [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- Stop Prowlarr
- Maak verbinding met de Synology NAS via SSH en log in als root  

> Bij sommige installaties is de gebruiker anders dan de onderstaande opdrachten: `chown -R sc-Prowlarr:Prowlarr *` {.is-info}

- Voer de volgende opdrachten uit:

    ```shell
        rm -r /usr/local/Prowlarr/var/.config/Prowlarr/Prowlarr.db
        cp -f /tmp/Prowlarr_backup/* /usr/local/Prowlarr/var/.config/Prowlarr/
    ```

- Werk de machtigingen van de bestanden bij:

    ```shell
        cd /usr/local/Prowlarr/var/.config/Prowlarr/
        chown -R Prowlarr:users *
        chmod -R 0644 *
    ```

- Start Prowlarr

## De WebUI laadt alleen op localhost op Windows

Als je alleen toegang hebt tot je webinterface via `http://localhost:9696/` of `http://127.0.0.1:9696`, moet je Prowlarr minstens één keer als beheerder uitvoeren, misschien zelfs altijd.

## Het vinden van cookies

Sommige sites kunnen niet automatisch worden ingelogd en vereisen dat je handmatig inlogt en vervolgens de cookies aan Prowlarr geeft om te kunnen werken. [Zie dit artikel voor meer informatie.](/useful-tools#finding-cookies)

## uTorrent werkt niet meer

- Zorg ervoor dat de Web UI is ingeschakeld

![faq_4_utorrent.png](/assets/general/faq_4_utorrent.png)

- Schakel de Web UI in

![faq_5_utorrent.png](/assets/general/faq_5_utorrent.png)

- Zorg ervoor dat de alternatieve luisterpoort (Geavanceerd => Web UI) niet hetzelfde is als de luisterpoort (Verbindingen). We raden aan om de alternatieve luisterpoort voor de Web UI te wijzigen om geen problemen te veroorzaken met port forwarding voor verbindingen.

![faq_6_utorrent.png](/assets/general/faq_6_utorrent.png)

## Ik kreeg een pop-up met de melding dat config.xml beschadigd is, wat nu?

Prowlarr kon uw configuratiebestand niet lezen bij het opstarten omdat het op de een of andere manier beschadigd is geraakt. Om Prowlarr weer online te krijgen, moet u `.xml` verwijderen in uw AppData-map. Start vervolgens Prowlarr opnieuw en het zal starten op de standaardpoort (9696). U moet nu alle instellingen opnieuw configureren die u hebt geconfigureerd op de pagina Algemene instellingen.

## Ongeldig certificaat en andere HTTPS- of SSL-problemen

Uw downloadclient werkt niet meer en u krijgt een foutmelding zoals `Localhost heeft een ongeldig certificaat`?

Prowlarr valideert SSL-certificaten. Als er geen SSL-certificaat is ingesteld in de downloadclient, of als u een zelfondertekend https-certificaat gebruikt zonder het CA-certificaat toe te voegen aan uw lokale certificaatopslag, weigert Prowlarr verbinding te maken. Gratis correct ondertekende certificaten zijn beschikbaar bij Let's Encrypt.

Als uw downloadclient en Prowlarr zich op dezelfde machine bevinden, is er geen reden om HTTPS te gebruiken, dus de gemakkelijkste oplossing is om SSL uit te schakelen voor de verbinding. De meeste mensen zullen het erover eens zijn dat dit ook niet nodig is in een lokaal netwerk. Het is mogelijk om certificaatvalidatie uit te schakelen in de geavanceerde instellingen als u een onveilige SSL-configuratie wilt behouden.

## Help, ik ben buitengesloten

{#help-i-have-forgotten-my-password}

Om authenticatie uit te schakelen (om uw vergeten gebruikersnaam of wachtwoord opnieuw in te stellen), moet u `config.xml` bewerken die zich bevindt in de [Prowlarr Appdata Directory](/prowlarr/appdata-directory)

1. Open config.xml in een teksteditor
1. Zoek de regel met de authenticatiemethode
`<AuthenticationMethod>Basic</AuthenticationMethod>` of `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Wijzig de regel `AuthenticationMethod` naar `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Prowlarr opnieuw op
1. Prowlarr is nu toegankelijk zonder wachtwoord, u moet naar `Instellingen: Algemeen` gaan in de gebruikersinterface en uw gebruikersnaam en wachtwoord instellen

## Vreemde UI-problemen

- Als u vreemde UI-problemen ondervindt of een bepaalde weergave of sortering niet werkt, probeer dan te kijken in een Chrome Incognito-venster of Firefox Private Window. Als het daar goed werkt, wis dan uw browsercache en cookies voor uw specifieke IP/domein. Voor meer informatie, zie het [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage) wiki-artikel.

## VPN's, Jackett en de \*ARRs

- Tenzij u zich in een onderdrukkend land bevindt zoals China, Australië of Zuid-Afrika, is uw torrentclient meestal het enige dat achter een VPN moet worden geplaatst. Omdat het VPN-eindpunt wordt gedeeld door veel gebruikers, kunt u te maken krijgen met snelheidsbeperkingen, DDOS-bescherming en IP-blokkades van verschillende services die elke software gebruikt.
- Met andere woorden, het achter een VPN plaatsen van de \*ARRs (Lidarr, Prowlarr, Radarr, Readarr en Lidarr) kan ervoor zorgen dat de applicaties in sommige gevallen onbruikbaar zijn omdat de services niet toegankelijk zijn.

> **Om duidelijk te zijn, het is niet de vraag of VPN's problemen zullen veroorzaken met de \*ARRs, maar wanneer: beeldleveranciers zullen u blokkeren en cloudflare staat voor de meeste \*ARR-servers (updates, metadata, enz.) en kan u ook blokkeren**
{.is-warning}

- **Veel privé-trackers zullen u verbannen als u ze gebruikt of er toegang toe hebt (bijvoorbeeld via Jackett of Prowlarr) via een VPN.**

### Gebruik van een VPN

- Als een VPN vereist is en Docker wordt gebruikt, wordt het aanbevolen om Hotio of Binhex's Download Client + VPN Containers te gebruiken.
- Als een VPN vereist is en Docker niet wordt gebruikt, moet uw VPN-client ***split tunneling*** ondersteunen, zodat alleen de vereiste (Download Client) apps achter de VPN worden geplaatst.
- Veel problemen met het openen van trackers kunnen worden opgelost door Google of Cloudflare's DNS-servers te gebruiken in plaats van de DNS-servers van uw internetprovider.
- In sommige gevallen (bijvoorbeeld Britse internetproviders) moet u uw torrent-downloadclient achter een VPN plaatsen en Jackett/Prowlarr als volgt:
  - plaats Jackett achter de VPN en zorg ervoor dat split tunneling lokale toegang toestaat
  - voor Prowlarr configureert u uw VPN-client om een proxy te bieden en voegt u de proxy toe in Instellingen => Indexers. Geef de proxy een tag en geef dezelfde tag aan eventuele indexers die deze moeten gebruiken.
    - Indien absoluut noodzakelijk en als uw VPN geen manier biedt om een proxy te maken, kunt u Prowlarr achter de VPN plaatsen en ervoor zorgen dat split tunneling lokale toegang toestaat.

## Hoe voorkom ik dat de browser wordt geopend bij het opstarten?

Afhankelijk van uw besturingssysteem zijn er meerdere mogelijke manieren.

- In `Instellingen` => `Algemeen` op sommige besturingssystemen is er een selectievakje om de browser bij het opstarten te openen.
- Bij het starten van Prowlarr kunt u `-nobrowser` (*nix) of `/nobrowser` (Windows) toevoegen aan de argumenten.
- Stop Prowlarr en bewerk het bestand config.xml en wijzig `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## Kan ik alle indexers in één keer toevoegen?

Nee. Dit zou geen goed idee zijn om te doen, en deze functionaliteit zal niet worden toegevoegd. Het is veel beter om uw indexers verstandig te kiezen, let op de statistieken om indexers die te traag zijn of geen resultaten opleveren te verwijderen. Het goed snoeien en onderhouden van uw indexers zal over het algemeen veel betere resultaten opleveren en snellere resultaten bij zoekopdrachten van uw apps.