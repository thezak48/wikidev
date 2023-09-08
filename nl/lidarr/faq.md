# Lidarr FAQ

## Inhoudsopgave

- [Hoe werkt Lidarr?](#hoe-werkt-lidarr)
- [Hoe vindt Lidarr releases?](#hoe-vindt-lidarr-releases)
- [Gedwongen authenticatie](#gedwongen-authenticatie)
- [Hoe worden mogelijke downloads vergeleken?](#hoe-worden-mogelijke-downloads-vergeleken)
- [Lidarr werkt niet meer na het updaten naar Ubuntu 22.04](#lidarr-werkt-niet-meer-na-het-updaten-naar-ubuntu-2204)
- [Waarom kan ik geen nieuwe release of artiest toevoegen aan Lidarr?](#waarom-kan-ik-geen-nieuwe-release-of-artiest-toevoegen-aan-lidarr)
- [Waarom kan ik geen album van verschillende artiesten toevoegen?](#waarom-kan-ik-geen-album-van-verschillende-artiesten-toevoegen)
- [Waarom toont Lidarr alleen studioalbums? Hoe vind ik singles of EP's?](#waarom-toont-lidarr-alleen-studioalbums-hoe-vind-ik-singles-of-eps)
- [Kan ik alleen een album toevoegen?](#kan-ik-alleen-een-album-toevoegen)
- [Kan ik individuele tracks downloaden?](#kan-ik-individuele-tracks-downloaden)
- [Waarom wordt artiest X niet weergegeven in de zoekresultaten?](#waarom-wordt-artiest-x-niet-weergegeven-in-de-zoekresultaten)
- [Lidarr heeft een album gevonden met te veel tracks. Hoe kan ik het album wijzigen naar de juiste release?](#lidarr-heeft-een-album-gevonden-met-te-veel-tracks-hoe-kan-ik-het-album-wijzigen-naar-de-juiste-release)
- [Ik kan een release niet vinden in Lidarr, maar het staat op MusicBrainz](#ik-kan-een-release-niet-vinden-in-lidarr-maar-het-staat-op-musicbrainz)
- [Hoe vaak synchroniseren de databases van Lidarr en MusicBrainz?](#hoe-vaak-synchroniseren-de-databases-van-lidarr-en-musicbrainz)
- [Hoe kan ik ontbrekende artiestenafbeeldingen toevoegen?](#hoe-kan-ik-ontbrekende-artiestenafbeeldingen-toevoegen)
- [Hoe kan ik ontbrekende albumafbeeldingen krijgen? (Cover Art)](#hoe-kan-ik-ontbrekende-albumafbeeldingen-krijgen-cover-art)
- [Ik heb problemen met het importeren van mijn artiesten, wat kan het zijn?](#ik-heb-problemen-met-het-importeren-van-mijn-artiesten-wat-kan-het-zijn)
- [Hoe kan ik mijn mappen met artiesten hernoemen?](#hoe-kan-ik-mijn-mappen-met-artiesten-hernoemen)
- [Hoe kan ik artiesten massaal verwijderen uit de gewenste lijst?](#hoe-kan-ik-artiesten-massaal-verwijderen-uit-de-gewenste-lijst)
- [Waarom werkt Lidarr niet achter een omgekeerde proxy?](#waarom-werkt-lidarr-niet-achter-een-omgekeerde-proxy)
- [Hoe update ik Lidarr?](#hoe-update-ik-lidarr)
  - [Kan ik Lidarr updaten binnen mijn Docker-container?](#kan-ik-lidarr-updaten-binnen-mijn-docker-container)
  - [Het installeren van een nieuwere versie](#het-installeren-van-een-nieuwere-versie)
    - [Native](#native)
    - [Docker](#docker)
- [Kan ik overschakelen van 'nightly' naar 'develop'?](#kan-ik-overschakelen-van-nightly-naar-develop)
- [Kan ik schakelen tussen branches?](#kan-ik-schakelen-tussen-branches)
- [Ik krijg een foutmelding: Database disk image is malformed](#ik-krijg-een-foutmelding-database-disk-image-is-malformed)
- [Hoe maak ik een back-up/herstel ik mijn Lidarr?](#hoe-maak-ik-een-back-upherstel-ik-mijn-lidarr)
  - [Een back-up maken van Lidarr](#een-back-up-maken-van-lidarr)
    - [Gebruik de ingebouwde back-up](#gebruik-de-ingebouwde-back-up)
    - [Gebruik het bestandssysteem rechtstreeks](#gebruik-het-bestandssysteem-rechtstreeks)
  - [Herstellen van een back-up](#herstellen-van-een-back-up)
    - [Gebruik een zip-back-up](#gebruik-een-zip-back-up)
    - [Gebruik een back-up van het bestandssysteem](#gebruik-een-back-up-van-het-bestandssysteem)
    - [Bestandssysteemherstel op Synology NAS](#bestandssysteemherstel-op-synology-nas)
- [Ik gebruik Lidarr op een Mac en het werkt plotseling niet meer. Wat is er gebeurd?](#ik-gebruik-lidarr-op-een-mac-en-het-werkt-plotseling-niet-meer-wat-is-er-gebeurd)
- [Ik gebruik een Pi en Raspbian en Lidarr start niet op](#ik-gebruik-een-pi-en-raspbian-en-lidarr-start-niet-op)
- [Waarom duren de synchronisatietijden van lijsten zo lang en kan ik dit wijzigen?](#waarom-duren-de-synchronisatietijden-van-lijsten-zo-lang-en-kan-ik-dit-wijzigen)
- [Kan ik de taak voor het vernieuwen van releases uitschakelen?](#kan-ik-de-taak-voor-het-vernieuwen-van-releases-uitschakelen)
- [Waarom kan Lidarr mijn bestanden op een externe server niet zien?](#waarom-kan-lidarr-mijn-bestanden-op-een-externe-server-niet-zien)
  - [Lidarr wordt standaard uitgevoerd onder het LocalService-account, dat geen toegang heeft tot beveiligde externe bestandsshares](#lidarr-wordt-standaard-uitgevoerd-onder-het-localservice-account-dat-geen-toegang-heeft-tot-beveiligde-externe-bestandsshares)
  - [U gebruikt een toegewezen netwerkstation (geen UNC-pad)](#u-gebruikt-een-toegewezen-netwerkstation-geen-unc-pad)
- [Help, ik ben buitengesloten](#help-ik-ben-buitengesloten)
- [Hoe voorkom ik dat de browser wordt geopend bij het opstarten?](#hoe-voorkom-ik-dat-de-browser-wordt-geopend-bij-het-opstarten)
- [Vreemde UI-problemen](#vreemde-ui-problemen)
- [VPNs, Jackett en de \*ARRs](#vpns-jackett-en-de-arrs)
- [Jackett's /all Endpoint](#jacketts-all-endpoint)
  - [Jackett /All-oplossingen](#jackett-all-oplossingen)
- [Waarom zijn er twee bestanden? | Waarom blijft er een bestand achter in downloads?](#waarom-zijn-er-twee-bestanden--waarom-blijft-er-een-bestand-achter-in-downloads)
- [Ik krijg steeds waarschuwingen van mijn cloudopslag over API-limieten](#ik-krijg-steeds-waarschuwingen-van-mijn-cloudopslag-over-api-limieten)

## Hoe werkt Lidarr?

- Lidarr maakt gebruik van RSS-feeds om automatisch releases te verzamelen zodra ze worden gepost, zowel nieuwe releases als eerder uitgebrachte releases die opnieuw worden uitgebracht. De RSS-feed bevat de nieuwste releases van een site, meestal tussen de 50 en 100 releases, hoewel sommige sites meer en andere minder bieden. De RSS-feed bestaat uit alle recent beschikbare releases, inclusief releases voor gevraagde media die je niet volgt. Als je naar debuglogs kijkt, zie je dat deze releases worden verwerkt, wat volkomen normaal is.
- Lidarr vereist een minimum van 10 minuten voor het synchroniseren van de RSS en een maximum van 2 uur. 15 minuten is het aanbevolen minimum voor de meeste indexers, hoewel sommige lagere intervallen toestaan en 2 uur ervoor zorgt dat Lidarr vaak genoeg controleert om geen release te missen (ook al kan het door de RSS-feed bladeren op veel indexers om daarbij te helpen). Sommige indexers staan toe dat clients vaker dan elke 10 minuten een RSS-synchronisatie uitvoeren. In die gevallen raden we aan om de Release-Push API-eindpunt van Lidarr te gebruiken in combinatie met een IRC-aankondigingskanaal om releases naar Lidarr te sturen voor verwerking. Dit kan vrijwel in realtime gebeuren en met minder overhead op de indexer en Lidarr, omdat Lidarr de RSS-feed niet te vaak hoeft op te vragen en dezelfde releases steeds opnieuw hoeft te verwerken.

## Hoe vindt Lidarr releases?

- Lidarr zoekt ''niet'' regelmatig naar ontbrekende albumbestanden of bestanden die niet aan hun kwaliteitsdoelen voldoen. In plaats daarvan vraagt het vrij vaak je indexers en trackers om ''alle'' nieuw geposte releases, en vergelijkt dat met de lijst van releases die ontbreken of moeten worden geüpgraded. Eventuele overeenkomsten worden gedownload. Hierdoor kan Lidarr een bibliotheek van ''elke omvang'' bestrijken met slechts 24-100 queries per dag (RSS-interval van 15-60 minuten). Als je dit begrijpt, zul je beseffen dat het alleen de ''toekomst'' bestrijkt.
- Hoe ga je dan om met het heden en het verleden? Bij het toevoegen van een album moet je het juiste pad, profiel en bewakingsstatus instellen en vervolgens het selectievakje Start zoeken naar ontbrekend album gebruiken. Als het album nog niet is uitgebracht, hoef je geen zoekopdracht te starten.
- Met andere woorden, Lidarr vindt alleen releases die nieuw zijn geüpload naar je indexers. Het zal niet actief proberen releases te vinden die je wilt en die in het verleden zijn geüpload.
- Als je het album al hebt toegevoegd, maar nu wilt zoeken, heb je een paar keuzes. Je kunt naar de pagina van het album gaan en de zoekknop gebruiken, die een zoekopdracht uitvoert en automatisch een keuze maakt. Je kunt het tabblad Zoeken gebruiken en ''alle'' resultaten bekijken en handmatig degene kiezen die je wilt. Of je kunt de filters Missing, Wanted of Cut-off Unmet gebruiken.
- Als Lidarr gedurende een langere periode offline is geweest, zal Lidarr proberen terug te bladeren om de laatste release te vinden die het heeft verwerkt om te voorkomen dat er een release wordt gemist. Zolang je indexer paging ondersteunt en het niet te lang geleden is, kan Lidarr de releases verwerken die het zou hebben gemist en hoef je geen zoekopdracht uit te voeren voor de gemiste releases.

## Gedwongen authenticatie

Als Lidarr zo is ingesteld dat de gebruikersinterface van buiten je lokale netwerk toegankelijk is, moet je een vorm van authenticatie inschakelen om toegang te krijgen tot de gebruikersinterface. Dit is ook steeds vaker vereist door trackers en indexers.

Vanaf Lidarr v2 is authenticatie verplicht.

### Authenticatiemethode

- `Basic` (Browser pop-up) - Deze optie toont bij het openen van Lidarr een klein pop-upvenster waarin je een gebruikersnaam en wachtwoord kunt invoeren.
- `Forms` (Aanmeldpagina) - Deze optie toont een aanmeldscherm dat lijkt op de aanmeldschermen van andere websites, zodat je kunt inloggen op Lidarr.
- `External` - Configuratie alleen mogelijk via het configuratiebestand
  - Als je een **externe authenticatie** zoals Authelia, Authetik, NGINX Basic auth, enz. gebruikt, kun je dubbele authenticatie voorkomen door de app af te sluiten, `<AuthenticationMethod>External</AuthenticationMethod>` in het [configuratiebestand](/lidarr/appdata-directory) in te stellen en de app opnieuw te starten. **Let op dat meerdere `AuthenticationMethod`-vermeldingen in het bestand niet worden ondersteund en alleen de bovenste waarde wordt gebruikt.**

### Vereiste authenticatie

- Als je de app niet extern beschikbaar stelt en/of geen authenticatie vereist voor lokaal (bijv. LAN) toegang, wijzig je in Instellingen => Algemene beveiliging => Vereiste authenticatie naar `Uitgeschakeld voor lokale adressen`
  - Het equivalent in het configuratiebestand is `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Hoe worden mogelijke downloads vergeleken?

> Over het algemeen heeft kwaliteit voorrang. Als je wilt dat kwaliteit niet de belangrijkste prioriteit is, kun je je kwaliteiten samenvoegen. [Zie de gids van TRaSH](https://trash-guides.info/merge-quality)***
{.is-info}

- De huidige logica [is hier te vinden](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs).

- Vanaf 2022-01-23 is de logica als volgt:

1. Kwaliteit
1. Voorkeurswoord-score
1. Protocol (zoals geconfigureerd in het relevante vertragingsprofiel)
1. Indexerprioriteit
1. Seeds/Peers (bij torrents)
1. Aantal albums
1. Leeftijd (bij Usenet)
1. Grootte

## Lidarr werkt niet meer na het updaten naar Ubuntu 22.04

- Lidarr v0.8 is niet compatibel en wordt niet ondersteund op Ubuntu 22.04
- Alleen Lidarr v1 ondersteunt Ubuntu 22.04
- [Zie deze FAQ-entry voor de branches en versies](#hoe-update-ik-lidarr)

## Waarom kan ik geen nieuwe release of artiest toevoegen aan Lidarr?

- De release heeft waarschijnlijk een `onbekend` type op MusicBrainz

## Waarom kan ik geen album van verschillende artiesten toevoegen?

- Verschillende artiesten en andere meta-artiesten op MusicBrainz zijn te wijten aan het aantal vermeldingen dat ze bieden.

## Waarom toont Lidarr alleen studioalbums? Hoe vind ik singles of EP's?

- Lidarr toont standaard alleen studioalbums voor elke artiest. Je kunt echter de albumtypen per artiest uitbreiden, of voor je hele bibliotheek door gebruik te maken van Metadata-profielen.

## Kan ik alleen een album toevoegen?

- Op dit moment niet.

## Kan ik individuele tracks downloaden?

- Lidarr werkt door te zoeken naar en het downloaden van volledige releases, daarom kunnen individuele tracks niet worden gedownload, tenzij ze als single zijn uitgebracht door de artiest.

## Waarom wordt artiest X niet weergegeven in de zoekresultaten?

- Zoeken is nog in ontwikkeling. Artiesten die niet worden weergegeven in de zoekresultaten kunnen worden toegevoegd door te zoeken naar `lidarr:mbid`, waarbij `mbid` de MusicBrainz-ID van de artiest is.

## Lidarr heeft een album gevonden met te veel tracks. Hoe kan ik het album wijzigen naar de juiste release?

- Open de pagina met albumdetails en selecteer het bewerkingspictogram in de bovenste navigatiebalk. Daar vind je een vervolgkeuzemenu met alle releases die aan dat album zijn gekoppeld.

## Ik kan een release niet vinden in Lidarr, maar het staat op MusicBrainz

- Dit komt waarschijnlijk doordat de release een `onbekende` status heeft. Werk MusicBrainz bij.

## Hoe vaak synchroniseren de databases van Lidarr en MusicBrainz?

- Elke uur op 5 minuten na het uur

## Hoe kan ik ontbrekende artiestenafbeeldingen toevoegen?

- Voeg kunst toe aan fanart.tv en wacht ~7+ dagen totdat het is gewist uit de cache. Vernieuw vervolgens de metadata.

## Hoe kan ik ontbrekende albumafbeeldingen krijgen? (Cover Art)

- Voeg coverart toe aan musicbrainz en wacht ~1 uur+ totdat het is gewist uit de cache. Vernieuw vervolgens de metadata.

## Ik heb problemen met het importeren van mijn artiesten, wat kan het zijn?

- Het importeerproces van de artiest importeert alleen de namen van de artiesten en de locaties van de mappen, die vervolgens worden opgeslagen in de database zodat a) metadata kan worden opgehaald en b) gedownloade inhoud in de toekomst op dezelfde locatie kan worden geplaatst. Om dit te kunnen doen, heeft het gebruikersaccount waar Lidarr onder draait zowel lees- als schrijfrechten nodig voor je gegevensdirectory.

## Hoe kan ik mijn mappen met artiesten hernoemen?

{#rename-folders}

> Dezelfde procedure geldt ook voor het verplaatsen/wijzigen van paden van artiesten.
{.is-info}

1. Bibliotheek
1. Massa-editor
1. Selecteer de artiesten waarvan je de map wilt hernoemen
1. Wijzig de hoofdmap naar dezelfde hoofdmap waarin de artiesten zich momenteel bevinden
1. Selecteer "Ja, verplaats bestanden"

## Hoe kan ik artiesten massaal verwijderen uit de gewenste lijst?

- Gebruik de Massa-editor => Selecteer de artiesten die je wilt verwijderen => Verwijderen

## Waarom werkt Lidarr niet achter een omgekeerde proxy?

- Lidarr maakt gebruik van .NET en een nieuwe webserver. Om ervoor te zorgen dat SignalR werkt, de UI-knoppen werken, database-wijzigingen worden doorgevoerd en andere zaken, is de volgende toevoeging vereist aan het locatieblok voor Lidarr:
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;

- Zorg ervoor dat je `proxy_set_header Connection "Upgrade";` **niet** opneemt, zoals wordt voorgesteld in de nginx-documentatie. `DIT WERKT NIET`
- [Zie dit ASP.NET Core-probleem](https://github.com/aspnet/AspNetCore/issues/17081)
- Als je een CDN zoals Cloudflare gebruikt, zorg er dan voor dat websockets zijn ingeschakeld om websocket-verbindingen toe te staan.

## Hoe update ik Lidarr?

- Ga naar Instellingen en vervolgens het tabblad Algemeen en toon geavanceerde instellingen (gebruik de schakelaar bij de opslaan-knop).

1. Wijzig onder de sectie Updates de naam van de branch naar `master` of `develop`
1. Opslaan

*Dit zal de bits van die branch niet onmiddellijk installeren, dit gebeurt tijdens de volgende update.*

- `master` - ![Huidige Master/Stabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) - (Standaard/Stabiel): Het is getest door gebruikers op de ontwikkel- en nachtelijke takken en er zijn geen grote problemen bekend. Deze versie ontvangt ongeveer maandelijks updates. Op GitHub is dit de `master`-tak.

- `develop` - ![Huidige Ontwikkel/Bèta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Ontwikkel&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) - (Bèta): Dit is de testomgeving. Uitgebracht na getest te zijn in de nachtelijke tak om te zorgen dat er geen directe problemen zijn. Nieuwe functies en bugfixes worden hier als eerste uitgebracht na de nachtelijke tak. Het kan als semi-stabiel worden beschouwd, maar het is nog steeds `bèta`. Deze versie ontvangt updates wekelijks of tweewekelijks, afhankelijk van de ontwikkeling.

> **Waarschuwing: Mogelijk kunt u niet teruggaan naar `master` nadat u naar deze tak bent overgeschakeld.** Op GitHub is dit een momentopname van de `develop`-tak op een specifiek moment.
{.is-warning}

- `nightly` - ![Huidige Nachtelijk/Onstabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nachtelijk&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) - (Alfa/Onstabiel): Dit is de meest recente versie. Het wordt uitgebracht zodra de code is ingediend en alle geautomatiseerde tests zijn geslaagd. Deze build is mogelijk nog niet door ons of andere gebruikers gebruikt. Er is geen garantie dat het in sommige gevallen zelfs zal werken. Deze tak wordt alleen aanbevolen voor gevorderde gebruikers. Problemen en zelfonderzoek worden verwacht in deze tak. ***Gebruik deze tak alleen als u weet wat u doet en bereid bent om uw handen vuil te maken om een mislukte update te herstellen.*** Deze versie wordt onmiddellijk bijgewerkt.

> **Waarschuwing: Mogelijk kunt u niet teruggaan naar `master` nadat u naar deze tak bent overgeschakeld.** Op GitHub is dit de `develop`-tak.
{.is-danger}

- Opmerking: Als u Lidarr installeert via Docker, voeg dan `:release`, `:latest`, `:testing` of `:develop` toe aan het einde van uw containerlabel, afhankelijk van wie uw builds maakt. Houd er rekening mee dat `nightly`-takken opzettelijk niet hieronder worden vermeld.

|                                                                    | `master` (stabiel) ![Huidige Master/Laatste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) | `develop` (bèta) ![Huidige Ontwikkel/Bèta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Ontwikkel&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) | `nightly` (alfa) ![Huidige Nachtelijk/Alfa](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nachtelijk&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/lidarr)                       | `release`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-lidarr) | `latest`                                                                                                                                                                                                              | `develop`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |

### Kan ik Lidarr bijwerken in mijn Docker-container?

- *Technisch gezien wel.* **Maar dat zou je absoluut niet moeten doen.** Het is een fundamentele filosofie van Docker. Er kunnen problemen met de database ontstaan als je je installatie bijwerkt naar de meest recente `nightly` en vervolgens de Docker-container zelf bijwerkt (mogelijk naar een oudere versie).

### Het installeren van een nieuwere versie

#### Native

1. Ga naar Systeem en vervolgens het tabblad Updates
1. Nieuwere versies die nog niet zijn geïnstalleerd, hebben een updateknop naast zich. Door op die knop te klikken, wordt de update geïnstalleerd.

#### Docker

1. Trek uw tag opnieuw en werk uw container bij

## Kan ik terugschakelen van `nightly` naar `develop`?

## Kan ik schakelen tussen takken?

- Als de versie identiek is, kunt u overschakelen, anders controleert u bij het ontwikkelingsteam of u kunt overschakelen van `nightly` naar `master`; `nightly` naar `develop`; of `develop` naar `master` voor uw specifieke build.
- Als u deze instructies niet opvolgt, kan uw Lidarr onbruikbaar worden of fouten veroorzaken. U bent gewaarschuwd.
  - De meest voorkomende fout is iets als `Error parsing column 45 (Language=31 - Int64)` of andere vergelijkbare databasefouten met ontbrekende kolommen of tabellen.

## Ik krijg een foutmelding: Database disk image is malformed

- **Fouten van `Error creating log database` geven problemen aan met logs.db**
  - Dit kan snel worden opgelost door de database een andere naam te geven of te verwijderen. De logboekdatabase bevat onbelangrijke informatie over de geschiedenis van opdrachten en installatiegeschiedenis van updates, en Info-, Warn- en Error-vermeldingen.
- **Fouten van `Error creating main database` of algemene `database disk image is malformed` zonder gespecificeerde database geven problemen aan met lidarr.db**
  - Ga verder met de hieronder genoemde stappen.
- Dit betekent dat uw SQLite-database die de meeste informatie voor Lidarr opslaat, beschadigd is. Uw opties zijn om (een) back-up(s) te proberen, de bestaande database te herstellen, de back-up(s) te herstellen, of als niets anders lukt, opnieuw te beginnen met een nieuwe database.
- Deze fout kan optreden als het databasebestand niet beschrijfbaar is door de gebruiker/groep waarin \*Arr wordt uitgevoerd. Permissies als oorzaak zullen waarschijnlijk alleen een probleem zijn bij nieuwe installaties, gemigreerde installaties naar een nieuwe server, als u onlangs de machtigingen van uw appdata-directory hebt gewijzigd, of als u de gebruiker en groep \*Arr hebt gewijzigd waarmee het wordt uitgevoerd.
- Uw beste en eerste optie is om [te proberen een back-up te herstellen](#hoe-maak-ik-een-back-upherstel-van-mijn-lidarr).
- U kunt ook proberen uw database te herstellen. Dit is meestal de enige optie wanneer dit probleem optreedt na een update. Probeer het [sqlite3-commando `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Als uw sqlite geen `.recover` heeft of als u een meer GUI-vriendelijke manier wilt (bijv. Windows), volg dan [onze instructies op deze wiki](/useful-tools#recovering-a-corrupt-db-ui).
- Een andere mogelijke oorzaak van de fout met uw database is dat u uw database op een netwerkstation plaatst (nfs of smb of iets anders dat niet lokaal is). **SQLite is ontworpen voor situaties waarin de gegevens en de toepassing op dezelfde machine bestaan.** Daarom moet uw \*Arr AppData-map (/config mount voor docker) zich op lokale opslag bevinden. [SQLite en netwerkstations werken niet goed samen en zullen uiteindelijk een beschadigde database veroorzaken](https://www.sqlite.org/draft/useovernet.html).
- Als u mergerFS gebruikt, moet u `direct_io` verwijderen omdat SQLite mmap gebruikt, wat niet wordt ondersteund door `direct_io`, zoals uitgelegd in de mergerFS [documentatie hier](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Hoe maak ik een back-up/herstel van mijn Lidarr?

### Lidarr back-uppen

#### Gebruik van ingebouwde back-up

- Ga naar Systeem => Backup in de Lidarr-UI
- Klik op de knop Backup
- Download de zip nadat de back-up is gemaakt om deze veilig te bewaren

#### Gebruik van het bestandssysteem rechtstreeks

- Zoek de locatie van de AppData-map voor Lidarr op
  - Ga via de Lidarr-UI naar Systeem => Over
  - [Lidarr Appdata Directory](/lidarr/appdata-directory)
- Stop Lidarr - Dit voorkomt dat de database beschadigd raakt
- Kopieer de inhoud naar een veilige locatie

### Herstellen van een back-up

> Herstellen naar een besturingssysteem met andere paden werkt niet (Windows naar Linux, Linux naar Windows, Windows naar OS X of OS X naar Windows), het verplaatsen tussen OS X en Linux kan werken, omdat beide paden bevatten `/` in plaats van `\` dat Windows gebruikt, maar wordt niet ondersteund. U moet alle paden in de database handmatig bewerken.
{.is-warning}

#### Gebruik van zip-back-up

- Installeer Lidarr opnieuw (indien van toepassing / nog niet geïnstalleerd)
- Start Lidarr
- Ga naar Systeem => Backup
- Selecteer Herstel Backup
- Selecteer Kies bestand
- Selecteer uw back-up-zipbestand
- Selecteer Herstellen

#### Gebruik van bestandssysteemback-up

- Installeer Lidarr opnieuw (indien van toepassing / nog niet geïnstalleerd)
- Zoek de locatie van de AppData-map voor Lidarr op
  - Voer Lidarr eenmaal uit en ga via de UI naar Systeem => Over
  - [Lidarr Appdata Directory](/lidarr/appdata-directory)
- Stop Lidarr
- Verwijder de inhoud van de AppData-map **(Inclusief de .db-wal/.db-journal-bestanden als ze bestaan)**
- Herstel vanuit uw back-up
- Start Lidarr
- Zolang de paden hetzelfde zijn, wordt alles opgepakt waar het was gebleven

#### Bestandssysteemherstel op Synology NAS

> LET OP: Herstellen op een Synology vereist kennis van Linux en Root SSH-toegang tot het Synology-apparaat.
{.is-warning}

- Installeer Lidarr opnieuw (indien van toepassing / nog niet geïnstalleerd)
- Zoek de locatie van de AppData-map voor Lidarr op
  - Voer Lidarr eenmaal uit en ga via de UI naar Systeem => Over
  - [Lidarr Appdata Directory](/lidarr/appdata-directory)
- Stop Lidarr
- Maak verbinding met de Synology NAS via SSH en log in als root

> Op sommige installaties is de gebruiker anders dan de onderstaande opdrachten: `chown -R sc-Lidarr:Lidarr *` {.is-info}

- Voer de volgende opdrachten uit:

```shell
rm -r /usr/local/Lidarr/var/.config/Lidarr/Lidarr.db
cp -f /tmp/Lidarr_backup/* /usr/local/Lidarr/var/.config/Lidarr/
```

- Werk de machtigingen van de bestanden bij:

 ```shell
cd /usr/local/Lidarr/var/.config/Lidarr/
chown -R Lidarr:users *
chmod -R 0644 *
```

- Start Lidarr

## Ik gebruik Lidarr op een Mac en het werkt plotseling niet meer. Wat is er gebeurd?

- Waarschijnlijk is dit te wijten aan een bug in MacOS waardoor een van de databases beschadigd is geraakt.

- Zie de bovenstaande vermelding over een beschadigde database.

- Probeer vervolgens op te starten en kijk of het werkt. Als het niet werkt, heeft u verdere ondersteuning nodig. Plaats een bericht op onze [subreddit /r/lidarr](http://reddit.com/r/lidarr) of kom naar [onze discord](https://lidarr.audio/discord) voor hulp.

## Ik gebruik een Pi en Raspbian en Lidarr start niet op

Raspbian heeft een versie van libseccomp2 die te oud is om een Docker-container te draaien op basis van Ubuntu 20.04, waar zowel hotio als LinuxServer gebruik van maken als hun basis. Je moet ofwel `--privileged` gebruiken, libseccomp2 updaten vanuit Ubuntu, of een beter besturingssysteem gebruiken (we raden Ubuntu 20.04 arm64 aan).

**Mogelijke oplossing:**

Het probleem is opgelost door de backport van het debian-repo te installeren. Het wordt over het algemeen niet aanbevolen om de backport in de upgrade-modus te gebruiken. Het installeren van een enkel pakket kan wel oké zijn, maar kan ook problemen veroorzaken. Dus begrijp wat je doet.

Stappen om het op te lossen:

Zorg er eerst voor dat je Raspbian Buster gebruikt, bijvoorbeeld met behulp van `lsb_release -a`

> Distributor ID: Raspbian
> Description: Raspbian GNU/Linux 10 (buster)
> Release: 10
> Codename: buster

- Als je Buster gebruikt:
  - Voer het volgende uit om de backports aan je bronnen toe te voegen

  ```shell
   echo "deb <http://deb.debian.org/debian> buster-backports main" | sudo tee /etc/apt/sources.list.d/buster-backports.list
   ```

  - Installeer de backport van libseccomp2

  ```shell
  sudo apt update && sudo apt-get -t buster-backports install libseccomp2
  ```

## Waarom duren synchronisatietijden van lijsten zo lang en kan ik dit veranderen?

Lijsten waren nooit bedoeld om direct toe te voegen, het zijn tools om te zeggen "ik wil dit, voeg het uiteindelijk toe".

Je kunt handmatig een lijstverversing starten, een script maken en het via de API starten, of de releases rechtstreeks aan Lidarr toevoegen.

Deze verandering is doorgevoerd om te voorkomen dat onze server wordt overbelast door mensen die elke 10 minuten lijsten bijwerken.

## Kan ik de taak voor het vernieuwen van releases uitschakelen?

Nee, en je moet dit ook niet proberen via SQL-hacks. De taak voor het vernieuwen van releases controleert de upstream Servarr-proxy en controleert of de metadata voor elke release (ids, cast, samenvatting, beoordelingen, vertalingen, alternatieve titels, etc.) is bijgewerkt ten opzichte van wat er momenteel in Lidarr staat. Indien nodig zal het de toepasselijke releases bijwerken.

Een veelvoorkomende klacht is dat de vernieuwingstaak zorgt voor zware I/O-gebruik. Een instelling die problemen kan veroorzaken is "Rescan Artist Folder after Refresh". Als je schijf-I/O-gebruik pieken vertoont tijdens een vernieuwing, wil je mogelijk de instelling voor het opnieuw scannen wijzigen naar `Handmatig`. Verander dit niet naar `Nooit`, tenzij alle wijzigingen in je bibliotheek (nieuwe releases, upgrades, verwijderingen, etc.) via Lidarr worden gedaan. Als je releasebestanden handmatig verwijdert of met een programma van derden, stel dit dan niet in op `Nooit`.

## Waarom kan Lidarr mijn bestanden op een externe server niet zien?

- Zorg ervoor dat de gebruiker/groep waarmee je \*Arr uitvoert lees- en schrijftoegang heeft tot de gemounte schijf.
- Voor Linux zorg je ervoor dat:
  - Als je een NFS-mount gebruikt, zorg ervoor dat `nolock` is ingeschakeld voor je mount.
  - Als je een SMB-mount gebruikt, zorg ervoor dat `nobrl` is ingeschakeld voor je mount.
- Voor Windows: In het kort: de gebruiker waarmee \*Arr wordt uitgevoerd (als service) of onder (als tray-app) heeft geen toegang tot het bestandspad op de externe server. Dit kan verschillende redenen hebben, maar de meest voorkomende is dat \*Arr wordt uitgevoerd als een service, wat de hieronder beschreven problemen veroorzaakt.

### Lidarr wordt standaard uitgevoerd onder het LocalService-account, dat geen toegang heeft tot beveiligde externe bestandsshare

- Voer de service van Lidarr uit als een andere gebruiker die toegang heeft tot die share
- Open het venster "Administrative Tools" > "Services" op je Windows-server.
- Stop de Lidarr-service.
- Open het dialoogvenster "Properties" > "Log On".
- Wijzig het gebruikersaccount van de service naar het doelgebruikersaccount.
- Voer Lidarr.exe uit via de opstartmap

### Je gebruikt een toegewezen netwerkstation (geen UNC-pad)

- Verander je paden naar UNC-paden (`\\server\share`)
- Voer Lidarr.exe uit via de opstartmap

## Help, ik ben buitengesloten

{#help-i-have-forgotten-my-password}

Om authenticatie uit te schakelen (om je vergeten gebruikersnaam of wachtwoord te resetten), moet je `config.xml` bewerken, die zich bevindt in de [Lidarr Appdata Directory](/lidarr/appdata-directory)

1. Open config.xml in een teksteditor
1. Zoek de regel met de authenticatiemethode, deze zal zijn
`<AuthenticationMethod>Basic</AuthenticationMethod>` of `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Verander de regel `AuthenticationMethod` naar `<AuthenticationMethod>None</AuthenticationMethod>`
1. Herstart Lidarr
1. Lidarr is nu toegankelijk zonder wachtwoord, je moet naar "Settings: General" in de UI gaan en je gebruikersnaam en wachtwoord instellen

## Hoe voorkom ik dat de browser wordt geopend bij het opstarten?

Afhankelijk van je besturingssysteem zijn er meerdere mogelijke manieren.

- In `Settings` => `General` op sommige besturingssystemen is er een selectievakje om de browser bij het opstarten te openen.
- Bij het starten van Lidarr kun je `-nobrowser` (*nix) of `/nobrowser` (Windows) toevoegen aan de argumenten.
- Stop Lidarr en bewerk het config.xml-bestand en verander `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## Vreemde UI-problemen

- Als je vreemde UI-problemen ervaart, zoals de bibliotheekpagina die niets weergeeft of een bepaalde weergave of sortering die niet werkt, probeer dan te kijken in een Chrome Incognito-venster of Firefox Private Window. Als het daar goed werkt, wis dan je browsercache en cookies voor je specifieke IP/domein. Zie het [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage) wiki-artikel voor meer informatie.

## VPN's, Jackett en de \*ARRs

Tenzij je je in een onderdrukkend land bevindt zoals China, Australië of Zuid-Afrika, is je torrentclient meestal het enige dat achter een VPN moet zitten. Omdat het VPN-eindpunt wordt gedeeld door veel gebruikers, kun je te maken krijgen met snelheidsbeperkingen, DDOS-bescherming en IP-blokkades van verschillende services die elke software gebruikt.
Met andere woorden, het achter een VPN plaatsen van de \*Arrs (Lidarr, Prowlarr, Radarr, Readarr en Lidarr) kan ervoor zorgen dat de toepassingen in sommige gevallen onbruikbaar worden omdat de services niet toegankelijk zijn.

> **Om duidelijk te zijn, het is niet de vraag of VPN's problemen zullen veroorzaken met de \*Arrs, maar wanneer: afbeeldingsproviders zullen je blokkeren en cloudflare staat voor de meeste \*Arr-servers (updates, metadata, etc.) en kan je ook blokkeren**
{.is-warning}

- **Veel privé-trackers zullen je verbannen als je ze gebruikt of er toegang toe hebt (bijv. via Jackett of Prowlarr) via een VPN.**

### Gebruik van een VPN

- Als een VPN vereist is en Docker wordt gebruikt, wordt het aanbevolen om Hotio of Binhex's Download Client + VPN Containers te gebruiken.
- Als een VPN vereist is en Docker niet wordt gebruikt, moet je VPN-client ***split tunneling*** ondersteunen, zodat alleen de vereiste (Download Client) apps achter de VPN zitten.
- Veel problemen met het benaderen van trackers kunnen worden opgelost door Google of Cloudflare's DNS-servers te gebruiken in plaats van de DNS-servers van je internetprovider.
- In sommige gevallen (bijv. Britse internetproviders) moet je je torrent-downloadclient achter een VPN plaatsen en Jackett/Prowlarr als volgt:
  - Plaats Jackett achter de VPN en zorg ervoor dat split tunneling lokale toegang toestaat.
  - Voor Prowlarr configureer je je VPN-client om een proxy te bieden en voeg je de proxy toe in Settings => Indexers. Geef de proxy een tag en geef dezelfde tag aan eventuele indexers die deze moeten gebruiken.
    - Als het absoluut noodzakelijk is en als je VPN geen manier biedt om een proxy te maken, kun je Prowlarr achter de VPN plaatsen en ervoor zorgen dat split tunneling lokale toegang toestaat.

## Jackett's /all-eindpunt

{#jackett-all-endpoint}

- Het Jackett `/all`-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan problemen veroorzaken, dus het is vereist om elke tracker afzonderlijk toe te voegen. Als alternatief kun je overwegen om de Jackett & NZBHydra2-alternatief [Prowlarr](/prowlarr) te gebruiken.
- **Update april 2022: \*Arr-ondersteuning is verwijderd voor het Jackett `/all`-eindpunt omdat het alleen maar problemen veroorzaakt.**
- Het Jackett /all-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan problemen veroorzaken, dus het is nu vereist om elke tracker afzonderlijk toe te voegen.
- [Zelfs de ontwikkelaars van Jackett zeggen dat het vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Het gebruik van het /all-eindpunt heeft geen voordelen, alleen nadelen:
  - je verliest de controle over specifieke instellingen van indexers (categorieën, zoekmodi, etc.)
  - het mixen van zoekmodi (IMDB, query, etc.) kan leiden tot lage kwaliteit resultaten
  - specifieke indexer-categorieën (\>= 100000) kunnen niet worden gebruikt.
  - trage indexers vertragen het algehele resultaat
  - het totale aantal resultaten is beperkt tot 1000
  - als een van de trackers in /all een foutmelding geeft, schakelt \*Arr deze uit en krijg je geen resultaten meer.

### Oplossingen voor Jackett /All

- Voeg elke tracker in Jackett handmatig toe als een indexer in \*Arr
- Bekijk [Prowlarr](/prowlarr), dat indexers kan synchroniseren met \*Arr en afkomstig is van het Lidarr/Radarr/Readarr-ontwikkelingsteam.
- Bekijk [NZBHydra2](https://github.com/theotherp/nzbhydra2), dat indexers kan synchroniseren met \*Arr. Gebruik echter niet hun enkele aggregatie-eindpunt en gebruik `multi` als synchronisatie wordt gebruikt.

## Waarom zijn er twee bestanden? | Waarom blijft er een bestand achter in de downloads?

Dit is normaal. Met een configuratie die [hardlinks](https://trash-guides.info/hardlinks) ondersteunt, wordt er geen dubbele ruimte gebruikt. Hieronder staat hoe het torrentproces werkt.

1. Lidarr stuurt een downloadverzoek naar je client en koppelt het aan een label of categorienaam die je hebt geconfigureerd in de instellingen van de downloadclient. Voorbeelden: films, tv, series, muziek, etc.
1. Lidarr houdt de actieve downloads van je downloadclients in de gaten die die categorienaam gebruiken. Deze monitoring gebeurt via de API van je downloadclient.
1. Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat je het bestand kunt seeden (ratio of tijd kan worden aangepast in de downloadclient of vanuit Lidarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar je mediamap, wordt het bestand gekoppeld (hardlink) als dit wordt ondersteund door je configuratie, anders wordt het gekopieerd als hardlinks niet worden ondersteund.
1. Als de optie "Voltooide downloadverwerking - Voltooide verwijderen" is ingeschakeld in de instellingen van Lidarr, zal Lidarr het oorspronkelijke bestand en de torrent verwijderen uit je downloadclient, maar alleen als de downloadclient meldt dat het seeden is voltooid en de torrent is gestopt (bijv. gepauzeerd). Zie [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) voor hoe je je downloadclient optimaal kunt configureren.

> Hardlinks zijn standaard ingeschakeld. [Een hardlink gebruikt geen extra schijfruimte.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de mounts moeten hetzelfde zijn voor je voltooide downloadmap en je mediatheek. Als het maken van een hardlink mislukt of je configuratie geen hardlinks ondersteunt, wordt er een kopie van het bestand gemaakt.
{.is-info}

## Ik krijg steeds waarschuwingen van mijn cloudopslag over API-limieten

Lidarr is anders dan de andere Arrs. Het gebruikt tags in plaats van bestandsnamen voor de werking. Als je Lidarr-bestanden op cloudopslag bewaart, moet het het bestand downloaden om de tags te lezen. Dit zal zeer snel door alle API-limieten van je opslagprovider heen gaan. We raden ten zeerste af om je Lidarr-bibliotheek op een cloudopslagprovider te bewaren, en eventuele problemen die je ondervindt zijn waarschijnlijk te wijten aan die configuratie.