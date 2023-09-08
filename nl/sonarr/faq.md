<!-- How do I change from the Windows Service to a Tray App? -->
## Hoe verander ik van de Windows-service naar een Tray-app?

- Als je Sonarr momenteel als een Windows-service gebruikt en wilt overschakelen naar een Tray-applicatie, volg dan de onderstaande stappen:

1. Stop de Sonarr-service. Dit kan worden gedaan door naar "Services" te gaan, de Sonarr-service te zoeken en deze te stoppen.
2. Open de Sonarr-toepassing en ga naar de instellingenpagina.
3. Ga naar het tabblad "General" (Algemeen).
4. Schakel de optie "Start Sonarr on boot" (Sonarr starten bij het opstarten) uit.
5. Klik op "Save" (Opslaan) om de wijzigingen op te slaan.
6. Sluit de Sonarr-toepassing af.
7. Start de Sonarr-toepassing opnieuw. Je zou nu de Tray-applicatie moeten zien in het systeemvak van Windows.

Opmerking: Als je de Tray-applicatie wilt sluiten, klik dan met de rechtermuisknop op het Sonarr-pictogram in het systeemvak en selecteer "Exit" (Afsluiten).

1. Sluit Sonarr af.
1. Voer serviceuninstall.exe uit die zich in de Sonarr-map bevindt.
1. Voer Sonarr.exe één keer uit als beheerder om het de juiste machtigingen te geven en de firewall te openen. Zodra dit is voltooid, kunt u het sluiten en normaal uitvoeren.
1. (Optioneel) Plaats een snelkoppeling naar Sonarr.exe in de opstartmap om automatisch op te starten bij het opstarten.

## Hoe maak ik een back-up/herstel ik mijn Sonarr?

### Een back-up maken van Sonarr

#### Gebruik de ingebouwde back-up

- Ga naar Systeem => Back-up in de Sonarr-UI.
- Klik op de knop Back-up.
- Download de zip nadat de back-up is gemaakt om deze veilig te bewaren.

#### Gebruik het bestandssysteem rechtstreeks

- Zoek de locatie van de AppData-map voor Sonarr op.
  - Ga via de Sonarr-UI naar Systeem => Over.
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Stop Sonarr - Hiermee wordt voorkomen dat de database wordt beschadigd.
- Kopieer de inhoud naar een veilige locatie.

### Herstellen vanaf een back-up

> Herstellen naar een besturingssysteem met verschillende paden werkt niet (Windows naar Linux, Linux naar Windows, Windows naar macOS of macOS naar Windows). Het verplaatsen tussen macOS en Linux kan wel werken, omdat beide paden bevatten met `/` in plaats van `\` dat Windows gebruikt, maar dit wordt niet ondersteund. U moet alle paden in de database handmatig bewerken of [Toolbarr](https://github.com/Notifiarr/toolbarr) gebruiken.
{.is-warning}

#### Gebruik een zip-back-up

- Installeer Sonarr opnieuw (indien van toepassing / nog niet geïnstalleerd).
- Start Sonarr.
- Ga naar Systeem => Back-up.
- Selecteer Herstel back-up.
- Selecteer Kies bestand.
- Selecteer uw back-up-zipbestand.
- Selecteer Herstellen.

#### Gebruik een back-up van het bestandssysteem

- Installeer Sonarr opnieuw (indien van toepassing / nog niet geïnstalleerd).
- Zoek de locatie van de AppData-map voor Sonarr op.
  - Voer Sonarr één keer uit en ga via de UI naar Systeem => Over.
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Stop Sonarr.
- Verwijder de inhoud van de AppData-map **(inclusief de .db-wal/.db-journal-bestanden als ze bestaan)**.
- Herstel vanaf uw back-up.
- Start Sonarr.
- Zolang de paden hetzelfde zijn, zal alles doorgaan waar het gebleven was.

#### Bestandssysteemherstel op Synology NAS

> LET OP: Herstellen op een Synology vereist kennis van Linux en Root SSH-toegang tot het Synology-apparaat.
{.is-warning}

- Installeer Sonarr opnieuw (indien van toepassing / nog niet geïnstalleerd).
- Zoek de locatie van de AppData-map voor Sonarr op.
  - Voer Sonarr één keer uit en ga via de UI naar Systeem => Over.
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Stop Sonarr.
- Maak verbinding met de Synology NAS via SSH en log in als root.

> Op sommige installaties is de gebruiker anders dan de onderstaande opdrachten: `chown -R sc-Sonarr:Sonarr *` {.is-info}

- Voer de volgende opdrachten uit:

```shell
rm -r /usr/local/Sonarr/var/.config/Sonarr/Sonarr.db
cp -f /tmp/Sonarr_backup/* /usr/local/Sonarr/var/.config/Sonarr/
```

- Werk de machtigingen van de bestanden bij:

 ```shell
cd /usr/local/Sonarr/var/.config/Sonarr/
chown -R Sonarr:users *
chmod -R 0644 *
```

- Start Sonarr.

## Help, ik ben buitengesloten

{#help-i-have-forgotten-my-password}

> Als u Sonarr v4 gebruikt, is het type `None` voor `AuthenticationMethod` niet langer geldig - zie deze [FAQ](/sonarr/faq-v4) {.is-info}

Om authenticatie uit te schakelen (om uw vergeten gebruikersnaam of wachtwoord opnieuw in te stellen), moet u `config.xml` bewerken die zich bevindt in de [Sonarr Appdata Directory](/sonarr/appdata-directory).

1. Open config.xml in een teksteditor.
1. Zoek de regel met de authenticatiemethode:
   `<AuthenticationMethod>Basic</AuthenticationMethod>` of `<AuthenticationMethod>Forms</AuthenticationMethod>`.
1. Wijzig de regel `AuthenticationMethod` in `<AuthenticationMethod>None</AuthenticationMethod>`.
1. Start Sonarr opnieuw.
1. Sonarr is nu toegankelijk zonder wachtwoord. Ga naar `Instellingen: Algemeen` in de UI en stel uw gebruikersnaam en wachtwoord in.

## Waarom zijn er twee bestanden? \| Waarom blijft er een bestand achter in downloads?

Dit is normaal. Met een configuratie die [hardlinks](https://trash-guides.info/hardlinks) ondersteunt, wordt er geen dubbele ruimte gebruikt. Hieronder wordt beschreven hoe het torrentproces werkt.

1. Sonarr stuurt een downloadverzoek naar uw client en koppelt het aan een label of categorie die u hebt geconfigureerd in de instellingen van de downloadclient. Voorbeelden: films, tv, series, muziek, enz.
1. Sonarr controleert de actieve downloads van uw downloadclient die deze categorie gebruiken. Deze controle gebeurt via de API van uw downloadclient.
1. Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat u het bestand kunt seeden (de verhouding of tijd kan worden aangepast in de downloadclient of vanuit Sonarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar uw mediamap, wordt het bestand gekoppeld (hardlink) als dit wordt ondersteund door uw configuratie, anders wordt het gekopieerd als hardlinks niet worden ondersteund.
1. Als de optie "Voltooide downloadverwerking - Voltooide verwijderen" is ingeschakeld in de instellingen van Sonarr, zal Sonarr het oorspronkelijke bestand en de torrent verwijderen uit uw downloadclient, maar alleen als de downloadclient meldt dat het seeden is voltooid en de torrent is gestopt (gepauzeerd). Zie [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) voor het optimaliseren van de instellingen van uw downloadclient.

> Hardlinks zijn standaard ingeschakeld. [Een hardlink gebruikt geen extra schijfruimte](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/). Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediatheek. Als het maken van een hardlink mislukt of uw configuratie ondersteunt geen hardlinks, wordt er een kopie van het bestand gemaakt als fallback.{.is-info}

## Ik zie dat functie/fout X is opgelost, waarom kan ik het niet zien?

Sonarr bestaat uit twee hoofdtakken van code, `main` en `develop`.

- `main` wordt periodiek uitgebracht wanneer de `develop`-tak stabiel is.
- `develop` is bedoeld voor pre-release testen en gebruikers die graag op het randje leven. Wanneer een functie als "in ontwikkeling" is gemarkeerd, is deze alleen beschikbaar voor gebruikers die de `develop`-tak uitvoeren. Zodra deze is verplaatst naar de live-omgeving (in `main`), wordt deze officieel uitgebracht.

## Voortgang van afleveringen - Hoe wordt dit berekend?

- Er zijn twee delen van het afleveringentelling, namelijk het aantal afleveringen (Episode Count) en het aantal afleveringen met bestanden (Episode File Count). Elk deel gebruikt iets andere logica om de algehele voortgang van een serie of seizoen weer te geven.

  - Episode Count => Aflevering is al uitgezonden EN wordt gemonitord OF - Aflevering heeft een bestand
  - Episode File Count => Aflevering heeft een bestand

- Als een serie 10 afleveringen heeft die allemaal zijn uitgezonden en u geen bestanden ervoor heeft, heeft u 0/10 afleveringen. Als u alle afleveringen in die serie niet meer volgt, heeft u 0/0 en als u alle afleveringen voor die serie heeft, ongeacht of de afleveringen worden gevolgd of niet, heeft u 10/10 afleveringen.

## Hoe kan ik toegang krijgen tot Sonarr vanaf een andere computer?

- Standaard luistert Sonarr niet naar verzoeken van alle systemen (wanneer het niet als beheerder wordt uitgevoerd), het luistert alleen op localhost. Dit komt door de manier waarop de webserver die Sonarr gebruikt integreert met Windows (dit geldt ook voor huidige alternatieven). Als Sonarr als beheerder wordt uitgevoerd, wordt het correct geregistreerd bij Windows en wordt de firewallpoort geopend, zodat het vanaf andere systemen in uw netwerk kan worden benaderd. Het uitvoeren als beheerder hoeft slechts één keer te gebeuren (als u de poort wijzigt, moet deze opnieuw worden uitgevoerd).

## Waarom vernieuwt Sonarr zo vaak de serie-informatie?

- Sonarr vernieuwt de serie- en afleveringsinformatie naast het opnieuw scannen van de schijf op zoek naar bestanden elke 12 uur. Dit lijkt misschien agressief, maar het is een zeer belangrijk proces. De gegevensvernieuwing van onze TVDb-proxy is belangrijk omdat nieuwe afleveringsinformatie wordt gesynchroniseerd, zoals uitzenddata, aantal afleveringen, status (lopend/beëindigd). Zelfs shows die niet worden uitgezonden, worden bijgewerkt met nieuwe informatie.
- De schijfscan is minder belangrijk, maar wordt gebruikt om nieuwe bestanden te controleren die niet door Sonarr zijn gesorteerd en om verwijderde bestanden te detecteren.
- Het meest tijdrovende deel is de informatieverniewing (onder voorbehoud van redelijke schijftoegangssnelheid), grotere shows duren langer vanwege het aantal afleveringen dat moet worden verwerkt.

> Het is niet mogelijk om deze taak uit te schakelen. Als deze taak lang genoeg wordt uitgevoerd dat u denkt dat dit het probleem is, is er iets anders aan de hand dat moet worden opgelost in plaats van deze taak te stoppen.
{.is-warning}

## Waarom staat er een getal naast Activiteit?

- Dit getal geeft het aantal afleveringen weer in de wachtrij van uw downloadclient en de laatste 60 items in de geschiedenis die nog niet zijn geïmporteerd. Als het getal blauw is, werkt het normaal en worden afleveringen geïmporteerd zodra ze zijn voltooid. Geel betekent dat er een waarschuwing is voor een van de afleveringen. Rood betekent dat er een fout is opgetreden. In het geval van geel (waarschuwing) en rood (fout), moet u naar de wachtrij onder Activiteit kijken om te zien wat het probleem is (beweeg de muis over het pictogram voor meer details).
- U moet het item uit de wachtrij of geschiedenis van uw downloadclient verwijderen om ze uit de wachtrij van Sonarr te verwijderen.

## Wat zijn de verschillende soorten series?

- Het type serie heeft invloed op hoe Sonarr zoekt naar series. Een serie type is gebaseerd op hoe de serie wordt uitgebracht op indexers en is niet noodzakelijkerwijs het echte 'type' van de serie.
- De meeste shows moeten `Standaard` zijn. Voor dagelijkse shows die meestal worden uitgebracht met een datum, moet `Dagelijks` worden gebruikt. Ten slotte is er anime, waarbij `Anime` *meestal* de juiste keuze is, maar soms kan `Standaard` beter werken, dus probeer de *andere* als u problemen ondervindt.
- Houd er rekening mee dat als het serie type is ingesteld op anime en als geen van uw ingeschakelde indexers anime-categorieën heeft geconfigureerd, het effectief de indexer overslaat en het lijkt alsof er niet wordt gezocht.
- Houd er rekening mee dat het Anime-type geen concept heeft van seizoenspakketten of seizoenen en dat elke aflevering afzonderlijk wordt gezocht.
- Houd er rekening mee dat niet alle indexers zoeken naar seizoen/aflevering (standaard).
- Serie types kunnen worden gewijzigd vanuit de Massa-editor of vanuit `Bewerken` bij het bekijken van een serie. Merk op dat het serie type selecteerbaar is bij het importeren.

- Als het **Anime** serie type wordt gebruikt, is het [mogelijk om uw indexer ook te laten zoeken met het standaard type.](/sonarr/settings#indexers)

### Serie Types

- **Anime** - Afleveringen uitgebracht met een absoluut afleveringsnummer
- **Dagelijks** - Afleveringen die dagelijks of minder vaak worden uitgebracht en gebruikmaken van het formaat jaar-maand-dag (2017-05-25)
- **Standaard** - Afleveringen uitgebracht met het SxxEyy-patroon

### Voorbeelden van Serie Types

Hieronder staan enkele voorbeelden van releasenamen voor elk type show. Het specifieke onderscheidende element is vetgedrukt aangegeven.

> Als het **Anime** serie type wordt gebruikt, is het [mogelijk om uw indexer ook te laten zoeken met het standaard type.](/sonarr/settings#indexers)
{.is-info}

#### Dagelijks

Logs tonen `Zoeken in indexers voor [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standaard

Logs tonen `Zoeken in indexers voor [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Logs tonen `Zoeken in indexers voor [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

## Hoe kan ik mijn serie mappen hernoemen?

{#rename-folders}

> Hetzelfde proces geldt ook voor het verplaatsen/wijzigen van Series-paden{.is-info}

Als u uw serie naamnotatie heeft aangepast nadat Sonarr al enkele serie mappen heeft aangemaakt, zal Sonarr de bestaande mappen niet automatisch hernoemen. Om deze mappen te hernoemen, moeten de volgende stappen worden gevolgd:

1. Series
1. Massa-editor
1. Selecteer welke series hun mapnaam moeten worden hernoemd
1. Wijzig de hoofdmap naar dezelfde hoofdmap waarin de series momenteel bestaan
1. Selecteer "Ja, bestanden verplaatsen" om

> Als u Plex of Emby gebruikt, wordt hierdoor opnieuw detectie van intro's, miniaturen, hoofdstukken en voorbeeldmetadata geactiveerd.
{.is-warning}

## Hoe update ik Sonarr?

- Ga naar Instellingen en vervolgens het tabblad Algemeen en toon geavanceerde instellingen (gebruik de schakelaar bij de opslaan-knop).

1. Onder de sectie Updates wijzigt u de naam van de tak naar `main` of `develop`.
1. Opslaan

*Dit zal de bits van die tak niet onmiddellijk installeren, dit gebeurt tijdens de volgende update.*

- main - ![Huidige hoofd/stabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Standaard/Stabiel): Dit is getest door gebruikers op de nachtelijke (`develop`) tak en er zijn geen grote problemen bekend. Deze tak moet worden gebruikt door de meeste gebruikers. Op GitHub is dit de `main` tak.
- develop - ![Huidige ontwikkeling/nachtelijk](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alpha/Onstabiel): Dit is nu hetzelfde als main voor niet-Docker-gebruikers en waarschijnlijk de laatste v3-release.

> ~~**Waarschuwing: U kunt mogelijk niet teruggaan naar `main` nadat u naar deze tak bent overgeschakeld.** Op GitHub is dit de `develop` tak.~~
{.is-danger}

- v4 develop - ![Huidige v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alpha/Onstabiel): **Voor niet-Docker-gebruikers is de tak `develop` zodra v4 is geïnstalleerd. Voor Docker-gebruikers is dit waarschijnlijk het `develop`-label** Dit is de bleeding edge voor Sonarr v4 Beta. Het wordt uitgebracht zodra de code is geïmplementeerd en alle geautomatiseerde tests zijn geslaagd. Deze build is mogelijk nog niet door ons of andere gebruikers gebruikt. Er is geen garantie dat het in sommige gevallen zelfs zal werken. Deze tak wordt alleen aanbevolen voor gevorderde gebruikers. Problemen en zelfonderzoek worden verwacht in deze tak. Op GitHub is dit de `develop` tak.

> **Waarschuwing: U kunt niet teruggaan naar (v3) `main` of (v3) `develop` nadat u naar de v4-tak bent overgeschakeld zonder opnieuw te installeren en een v3-back-up te vinden.** Op GitHub is dit de `develop` tak.
{.is-danger}

> v3 **niet-Docker**-installaties kunnen **niet** rechtstreeks worden bijgewerkt naar v4 en vereisen het installeren van Sonarr v4
{.is-info}



|                                                                    | `main` (stabiel) ![Huidige Main/Laatste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v3) (beta) ![Huidige v3 Ontwikkeling/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Ontwikkeling&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v4) (v4 beta) ![Huidige v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) |
|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [hotio](https://hotio.dev/containers/sonarr)                       | `release`                                                                                                                                                                                             | `nightly`                                                                                                                                                                                                   | `v4`                                                                                                                                                                                                            |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-sonarr) | `latest`                                                                                                                                                                                              | `3.0.10`                                                                                                                                                                                                     | `develop`                                                                                                                                                                                                       |

### Het installeren van een nieuwere versie

#### Native

1. Ga naar Systeem en vervolgens naar het tabblad Updates
1. Nieuwere versies die nog niet zijn geïnstalleerd, hebben een updateknop naast zich. Door op die knop te klikken wordt de update geïnstalleerd.

> v3 kan niet worden bijgewerkt naar beta v4 en moet handmatig worden geïnstalleerd. Raadpleeg de [v4 Beta-aankondiging](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)
{.is-info}

#### Docker

1. Trek uw tag opnieuw en werk uw container bij

## Kan ik terugschakelen van `develop` naar `main`?

- Zie de onderstaande invoer

## Kan ik schakelen tussen branches?

> Je kunt (bijna) altijd je risico vergroten.{.is-info}

- `main` kan naar `develop`
- Zie hieronder of controleer anders bij het ontwikkelingsteam of je kunt overschakelen van `develop` naar `main` voor jouw specifieke build.
- Het niet volgen van deze instructies kan ertoe leiden dat je Sonarr onbruikbaar wordt of fouten genereert. Je bent gewaarschuwd. Als de onderstaande fouten zich voordoen, gebruik je een nieuwere database met een oudere \*Arr-versie die niet wordt ondersteund. Upgrade \*Arr naar de versie waarop je eerder zat of een nieuwere versie.
  - Voorbeeldfoutmeldingen:
    - `Fout bij het parseren van kolom 45 (Taal=31 - Int64)`
    - `De DataMapper kon het volgende veld niet laden: 'Talen' waarde`
    - `ID komt niet overeen met een bekende taal Parameter naam: id`
    - Andere soortgelijke databasefouten met ontbrekende kolommen of tabellen.
- **Update 7 augustus 2022**
  - `3.0.9.1549` is uitgebracht als main/stabiel
  - Voor degenen die zich in de ontwikkelingsfase bevinden en nog steeds op `3.0.9.1549` of lager zitten, kun je veilig downgraden naar main
  - Als je een nieuwere versie hebt, *zit je mogelijk vast* op nightly/develop totdat er een nieuwe stabiele release is. Als je een back-up hebt van vóór de upgrade naar de hierboven genoemde versie, kun je opnieuw installeren en de back-up herstellen. Controleer bij het ontwikkelingsteam of je veilig kunt downgraden.

# Sonarr en Series Problemen + Metadata

## Hoe gaat Sonarr om met problemen met scènenummering (American Dad!, etc)?

### Hoe Sonarr omgaat met problemen met scènenummering

- Sonarr vertrouwt op [TheXEM](http://thexem.info/), een door de community gedreven site waarmee gebruikers mappings kunnen maken van shows die de scène (de mensen die de bestanden posten) en TheTVDb (die meestal de nummering van het netwerk volgt). Er zijn al een aantal shows op de site, maar het is eenvoudig om er nog een toe te voegen en meestal worden de wijzigingen binnen een paar dagen geaccepteerd (als ze correct zijn). TheXEM wordt gebruikt om verschillen in afleveringsnummering (meningsverschil of een aflevering een speciale aflevering is of niet) en verschillen in seizoensnummering te corrigeren, zoals afleveringen die worden uitgebracht als S10E01, maar die door TheTVDb worden vermeld als S2017E01.
- XEM lost meestal de problemen op wanneer de nummering van releasegroepen (in de volksmond bekend als 'de scène') niet overeenkomt met de nummering van TVDb, zodat Sonarr niet werkt. Nou, daar komt [XEM](http://thexem.info) binnen, dat een kaart maakt waar Sonarr naar kan kijken.
- Releases bevatten dubbele afleveringen in één bestand, omdat dat is hoe ze worden uitgezonden, maar TVDb markeert elke aflevering afzonderlijk.
- Releasegroepen gebruiken een jaartal voor het seizoen S2010 en TVDb gebruikt S01.
- [XEM](http://thexem.info) werkt in de meeste gevallen en houdt alles soepel draaiende zonder dat je het ooit merkt. Maar zoals met de meeste dingen, zullen er altijd *probleemgevallen* zijn en in dit geval is er een lijst van hen.

> Bepaalde indexers of releasegroepen kunnen TVDb volgen in plaats van `Scene` (dwz XEM).
> Als dit wordt waargenomen, dien ze dan in via het formulier voor scènemapping.
{.is-info}

- [Services Requested Mappings *Controleer en zorg ervoor dat de alias en release nog niet zijn aangevraagd of toegevoegd*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Services Scene Mapping Request Form *Dien een nieuwe aanvraag in voor een alias. Zorg ervoor dat het formulier volledig is ingevuld*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

### Probleemshows

> Dit is geenszins een volledige lijst van shows met bekende problemen met scènemapping; dit zijn echter enkele veelvoorkomende gevallen.
{.is-info}

- Dit is een onvolledige lijst van de bekende shows en hoe/waarom ze problematisch zijn:
- American Dad {#problemshow-americandad}
  - Vanwege veranderingen in het seizoen van het netwerk, loopt American Dad meestal 1 seizoen achter tussen releases en TVDb. Raadpleeg de XEM-kaart voor details
  - [American Dad](https://thexem.info/xem/show/4948) is momenteel op S19 gebaseerd op TVDb of S18 gebaseerd op Scene op het moment van schrijven. Dus zoeken in Sonarr naar Seizoen 19 geeft **alleen** resultaten van Seizoen 18 vanwege de XEM-kaart.
  - Als je een indexer / releasegroep hebt met afleveringen van Seizoen 19, dien ze dan in via het formulier voor scènemapping en zorg ervoor dat ze nog niet zijn aangevraagd
    - [Services Requested Mappings *Controleer en zorg ervoor dat de alias en release nog niet zijn aangevraagd of toegevoegd*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Services Scene Mapping Request Form *Dien een nieuwe aanvraag in voor een alias. Zorg ervoor dat het formulier volledig is ingevuld*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- Paw Patrol {#problemshow-pawpatrol}
  - Dubbele afleveringsbestanden versus enkele aflevering TVDb, maar ook niet alle afleveringen zijn dubbel, dus de kaart kan verkeerd worden toegevoegd en aangeven welke afleveringen enkelvoudig en welke dubbel zijn
- Pokémon {#problemshow-pokemon}
  - Op TheXem volgt [Pokemon](http://thexem.info/xem/show/4638) *nagesynchroniseerde* afleveringen. Dus als je ondertitelde afleveringen wilt, heb je misschien pech. Als bepaalde releasegroepen TVDb volgen en geen XEM-mapping, dien ze dan in via het formulier voor scènemapping en zorg ervoor dat ze nog niet zijn aangevraagd
    - [Services Requested Mappings *Controleer en zorg ervoor dat de alias en release nog niet zijn aangevraagd of toegevoegd*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Services Scene Mapping Request Form *Dien een nieuwe aanvraag in voor een alias. Zorg ervoor dat het formulier volledig is ingevuld*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- La Casa de Papel / Money Heist  {#problemshow-moneyheist}
  - TVDb heeft de oorspronkelijke uitzendvolgorde van het Spaanse netwerk, maar Netflix heeft de rechten gekocht en de serie opnieuw gemonteerd tot een ander aantal afleveringen. Hierdoor wordt "seizoen 5" geïmporteerd over bestaande "seizoen 3" afleveringen. [Aanvullende informatie is te vinden in deze Reddit-thread](https://old.reddit.com/r/sonarr/comments/pdrr6l/money_heist_mess/)
- Kamen Rider {#problemshow-kamenrider}
  - De anthology entry ([TVDb ID 74096](https://thetvdb.com/series/kamen-rider)) moet worden gebruikt in Sonarr voor automatisering, omdat deze show zowel een anthology entry (waarin alle seizoenen worden verzameld) als de afzonderlijke seizoenen apart worden vermeld op TVDb. Vanwege de individuele seizoensnaammappings op [TheXEM](https://thexem.info/xem/show/5376) is het niet mogelijk om de individuele seizoensvermeldingen aan Sonarr toe te voegen zonder handmatig releases te downloaden en te importeren.
- Bleach: Thousand-Year Blood War {#problemshow-bleach}
  - Het nieuwste seizoen van Bleach: Thousand-Year Blood War wordt uitgebracht met verschillende benamingen, waardoor automatisering moeilijk wordt en mogelijk enkele van je bestaande afleveringen worden overschreven. Het kan alleen worden geautomatiseerd als je releasegroep:
    - De afleveringen uitbrengt met S17Exx-nummering, of
    - Ze uitbrengt met de juiste titel van seizoen 2 (te vinden op <https://thexem.info/xem/show/5476>) en dit nieuwe arc begint bij absolute afleveringsnummer 1.
- Great Asian Railway Journeys {#problemshow-greatasianrail}
  - Great Asian Railway Journeys werd eerst uitgezonden als 20 kleinere afleveringen, maar werd later opnieuw uitgezonden als 10 lange afleveringen. Deze langere gecombineerde afleveringen zijn toegevoegd als specials en moeten dienovereenkomstig worden genoemd. (S00E01, enz., ...)
- Horizon {#problemshow-horizon}
  - Een show die sinds 1964 sporadisch afleveringen uitzendt. Dit maakt het bijzonder moeilijk om te mappen, zoals te zien is op [TheXEM](https://thexem.info/xem/show/5495). Geïnteresseerden kunnen de oorspronkelijke discussie vinden op de Sonarr Discord [hier](https://discord.com/channels/383686866005917708/649018968559845376/1046898050909622312).
- Kaleidoscope (2023) {#problemshow-kaleidoscope}
  - Kaleidoscope (2023) werd op Netflix uitgebracht als een niet-lineaire show, wat betekent dat elke gebruiker een andere volgorde kreeg bij het bekijken van de serie. Dit zorgt voor een probleem voor Sonarr, omdat releasegroepen verschillende afleveringsvolgordes hebben voor de show. Om te voorkomen dat afleveringen verkeerd worden gemapt, zal Sonarr de afleveringen niet automatisch ophalen en moet je de afleveringen handmatig ophalen en importeren. Je kunt ze matchen op basis van de afleveringstitel, of door de eerste paar seconden te bekijken en te zien of de 'kleur' van de aflevering overeenkomt met de titel.

Enkele voorbeelden van andere shows die vaak problemen hebben, waarvan de meeste kunnen worden opgelost met TheXEM-mappings zijn: Arrested Development, Kitchen Nightmares (US), Mythbusters, Pawn Stars.

## Waarom kan Sonarr geen afleveringsbestanden importeren voor serie X? / Waarom kan Sonarr geen releases vinden voor serie X?

Er kunnen meerdere redenen zijn waarom Sonarr geen afleveringen kan vinden of importeren voor een bepaalde serie.

> Sonarr gebruikt geen aliassen of vertalingen (bijvoorbeeld titels in een andere taal) van TVDb.
{.is-warning}

> **Voor indexers die ID-gebaseerd zoeken ondersteunen**, worden de TVDbID of IMDbID van de serie gebruikt voor het zoeken. Serietitels en eventuele aliassen worden alleen gebruikt als ID-gebaseerd zoeken geen resultaten oplevert.
{.is-info}

- Sonarr vertrouwt op het kunnen matchen van titels, vaak gebruiken uploaders verschillende titels voor afleveringen, bijvoorbeeld `CSI: Crime Scene Investigation` wordt gepost als `CSI`, dus Sonarr kan de namen niet matchen zonder wat hulp. Deze worden behandeld door de Scene Mapping die het Sonarr-team onderhoudt.
- U kunt ook de [FAQ-invoer voor problematische shows en nummeringsproblemen van releasegroep versus TVDb](#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc) raadplegen.

> **Voor alle Japanse anime moeten aliassen worden toegevoegd aan [thexem.info](https://thexem.info)**, voor andere series om een nieuwe mapping aan te vragen, zie de onderstaande stappen. Meer informatie is te vinden bij enkele van de XEM-mensen die rondhangen in het #XEM-discordkanaal op de Sonarr Discord.
{.is-danger}

- [Services Requested Mappings *Controleer en zorg ervoor dat de alias en release nog niet zijn aangevraagd of toegevoegd*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Services Scene Mapping Request Form *Doe een nieuwe aanvraag voor een alias. Zorg ervoor dat het formulier volledig is ingevuld*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

> Gewoonlijk worden Services-aanvragen binnen 1-5 dagen toegevoegd
{.is-info}

> Vraag opnieuw geen mapping aan voor Japanse anime; gebruik daarvoor XEM.
> Meer informatie is te vinden bij enkele van de XEM-mensen die rondhangen in het [\#XEM-discordkanaal op de Sonarr Discord](https://discord.gg/Z3D6u5hBJb)
{.is-danger}

> Als een niet-Japanse serie een seizoensmapping vereist (bijvoorbeeld uitgebracht als S25E26 maar TVDB is S26E2), is een XEM-mapping vereist. Dit kan niet worden gedaan met Services-mapping.
{.is-info}

> De serie "Helt Perfekt" met TVDb-id's `343189` en `252077` is moeilijk te automatiseren vanwege TVDb die dezelfde naam heeft voor beide shows, waarmee de eigen regels van TVDb worden overtreden. De eerste vermelding voor de serie krijgt de naam. Eventuele toekomstige vermeldingen voor de serie moeten het jaar als onderdeel van de serienaam hebben. Er is echter een uitzondering voor de scene toegevoegd om releases te mappen (hoofdlettergevoelige mapping) Helt Perfekt-releases met `NORWEGIAN` -\> `252077` en met `SWEDISH` -\> `343189`
{.is-info}

## TVDb is bijgewerkt, waarom Sonarr niet?

{#tvdb}

- TVDb heeft een cache van 24 uur op hun API.
- De API van TVDb moet vervolgens worden gevuld via hun CDN-cache, wat enkele uren duurt.
- Skyhook van Sonarr heeft daarbovenop een veel kleinere cache van enkele uren.
- Bovendien voert Sonarr de taak 'Series vernieuwen' slechts elke 12 uur uit. Deze taak kan handmatig worden uitgevoerd vanuit Systeem => Taken; "Alles bijwerken" vanuit de Series Index, of handmatig worden uitgevoerd voor een specifieke serie op de pagina van die serie.

- Daarom duurt het meestal tussen de 36 en 48 uur (24 + ~3 + ~3 + 12) voordat een wijziging op TVDb automatisch in Sonarr wordt doorgevoerd.

- Als een serie of afleveringen ontbreken op TVDb, duurt het 36 tot 48 uur voordat ze worden toegevoegd aan uw Sonarr-instantie nadat ze zijn toegevoegd.

{#missing-episodes}

- Als u weet dat er meer dan 48 uur geleden een update is uitgevoerd op TVDb, bespreek dit dan op onze [Discord](https://discord.sonarr.tv/).

## Waarom kan ik geen serie toevoegen?

{#why-can-i-not-add-a-new-series}

- Als TheTVDb niet beschikbaar is, kan Sonarr geen zoekresultaten ophalen en kunt u geen nieuwe series toevoegen door te zoeken. U kunt mogelijk een nieuwe serie toevoegen via de TVDbID als u weet wat het is, de gebruikersinterface legt uit hoe u deze kunt toevoegen met behulp van een ID.
- Sonarr kan geen enkele serie toevoegen die geen Engelse titel heeft. Als u probeert een serie toe te voegen via TVDb ID die geen Engelse titel heeft. Als er geen Engelse titel bestaat voor die serie op TheTVDb, moet deze worden toegevoegd en vervolgens [moet u wachten tot de cache van TVDb is gewist](#tvdb).
- De show moet een tv-serie zijn en geen film. Het moet ook bestaan op TVDb. Als het op IMDB, TMDB of ergens anders staat, maar niet op TVDb, kunt u de show niet toevoegen.
- De serie moet bestaan op TVDb.
- Bepaalde series kunnen eigenlijk worden beschouwd als voortzettingen en seizoenen in hun primaire serie.
  - Enkele bekende series/seizoenen zijn:
  - [Dexter New Blood was seizoen 9](https://thetvdb.com/series/dexter/seasons/official/9) maar het is nu [een eigen serie](https://thetvdb.com/series/dexter-new-blood)

## Waarom kan ik geen serie toevoegen als ik het TVDb ID weet?

{#why-cant-i-add-a-new-series-when-i-know-the-tvdb-id}

- Sonarr kan geen enkele serie toevoegen die geen Engelse titel heeft. Als u probeert een serie toe te voegen via TVDb ID die geen Engelse titel heeft, wordt de serie niet gevonden. Als er geen Engelse titel bestaat voor die serie op TheTVDb, moet deze worden toegevoegd (indien beschikbaar).
- Controleer de URL/serie - Sonarr ondersteunt geen films; gebruik [Radarr](/radarr) voor films

## Titel Slug in gebruik

- Er zijn twee belangrijke oorzaken van deze fout die hieronder worden vermeld.

## Dubbele namen zonder jaartal

- Deze fout treedt vaak op wanneer twee series dezelfde titel hebben op TheTVDB, als dit het geval is, moet aan de tweede serie het jaartal worden toegevoegd aan de serietitel.
  - Serie A
  - Serie A (2021)
- Om dit te herstellen, wacht u tot iemand uiteindelijk (misschien) TVDb bijwerkt of werkt u TVDb zelf bij. Zodra dit is gecorrigeerd **en nadat het is goedgekeurd door de moderators van TVDb**, vanwege [de API-problemen van TVDb](#tvdb-is-updated-why-isnt-sonarr), moet u na de update minimaal 30 uur wachten voordat de gecorrigeerde titel in Sonarr kan worden gebruikt.

## Dubbele namen met leestekens

- Het kan ook gebeuren met twee series die qua naam op elkaar lijken en alleen verschillen in leestekens, als dit het geval is, meld dit dan op de [Sonarr Discord](https://discord.sonarr.tv/).
  - Joe's Show (2022)
  - Joes Show (2022)

## Aflevering heeft geen absoluut nummer

- De aflevering(en) op TVDb hebben geen absoluut nummer toegewezen gekregen. Werk de serie bij op TVDb indien nodig en wacht vervolgens 36-48 uur totdat de update de interne cache van TVDb heeft gewist en in Sonarr is geladen.

## Uitzendtijden van afleveringen

- Binnen Sonarr zijn de uitzenddatum en -tijd van afleveringen die in de browser worden weergegeven, gebaseerd op de tijd/tijdzone van de client, alle tijden worden van Sonarr naar de browser verzonden als UTC-tijden (ISO-8601 opgemaakt om precies te zijn)
- TVDb bepaalt - met uitzonderingen voor streamingdiensten - dat de uitzendtijd en -datum gebaseerd zijn op de lokale tijd van het primaire uitzendnetwerk in de populairste stad van het land. [Zie de FAQ-invoer van TVDb voor details](https://support.thetvdb.com/kb/faq.php?id=29)
- Afleveringsdatums en uitzendtijden op TVDb worden geconverteerd naar UTC en gebruiken de tijdzone van Sonarr die is toegewezen in Skyhook door het Sonarr-team voor het Network dat TVDb heeft voor de serie.
  - In het zeldzame geval dat een netwerk niet is toegewezen, wordt ervan uitgegaan dat de tijd in TVDb US EST (UTC-5) is. 
  - Als de uitzendtijd niet lijkt overeen te komen bij het omzetten van de uitzendtijd van de lokale tijdzone van het netwerk naar de tijdzone van uw browser, moet waarschijnlijk het netwerk worden toegewezen in Skyhook. [Neem contact op met het ontwikkelingsteam op Discord](https://discord.sonarr.tv/) voor ondersteuning bij het bijwerken van de tijdzone van het netwerk.  

# Veelvoorkomende problemen met Sonarr

## Pad is al geconfigureerd voor een bestaande serie

- Bibliotheek importeren toont "Bestaand" of u krijgt een foutmelding "Pad is geconfigureerd voor een bestaande serie"
- Dit gebeurt wanneer u probeert een serie toe te voegen of het pad van een bestaande serie te bewerken dat al is toegewezen aan een andere serie.
- Waarschijnlijk is dit veroorzaakt doordat een niet-overeenkomende serie niet is gecorrigeerd toen de gebruiker zijn bibliotheek importeerde.
- Zoek de film die al is toegewezen aan het pad van die serie.
  - Series Index
  - Tabelweergave
  - Opties => Voeg pad toe als kolom
  - Sorteer en zoek de film op het genoteerde problematische pad.
- Als alternatief kunt u de serie verwijderen die het bestaande pad gebruikt uit Sonarr

## Systeem en logs laden oneindig

- Het is de easy-privacy blocklist. Ze blokkeren in feite elke URL met /api/log? erin. Bekijk de lijst en vertel me of je denkt dat het blokkeren van alle urls in die lijst een verstandig idee is, er zijn tientallen urls in die lijst die mogelijk sites breken. Je hebt dat geselecteerd in je adblocker. De eenvoudige oplossing is om het domein waarop Sonarr draait op de whitelist te zetten. Maar ik raad nog steeds aan om de lijst te controleren.

## Vreemde UI-problemen

- Als u problemen ondervindt met de UI, zoals de pagina Bibliotheek die niets weergeeft of een bepaalde weergave of sortering die niet werkt, probeer dan te kijken in een Chrome Incognito-venster of Firefox Private Window. Als het daar goed werkt, verwijder dan de cache en cookies van uw browser voor uw specifieke IP/domein. Voor meer informatie, zie het [wiki-artikel Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage).

## Webinterface laadt alleen op localhost op Windows

- Als u alleen toegang heeft tot uw webinterface via <http://localhost:8989/> of <http://127.0.0.1:8989>, moet u Sonarr ten minste één keer als beheerder uitvoeren.

## Ik kreeg een pop-up met de melding dat config.xml beschadigd is, wat nu?

- Sonarr kon uw configuratiebestand niet lezen bij het opstarten omdat het op de een of andere manier beschadigd is geraakt. Om Sonarr weer online te krijgen, moet u `.xml` verwijderen in uw [AppData-map](/sonarr/appdata-directory) nadat u Sonarr hebt gestart en het zal starten op de standaardpoort (8989), u moet nu alle instellingen opnieuw configureren die u hebt geconfigureerd op de pagina Algemene instellingen.

## Ongeldig certificaat en andere HTTPS- of SSL-problemen

- Als u geen Windows gebruikt, zijn waarschijnlijk de certificaten van uw mono verouderd en moeten ze worden gesynchroniseerd. [Zie het gedeelte over mono ssl in het installatieartikel voor meer informatie](/sonarr/installation#mono-ssl-issues)
- Uw downloadclient werkt niet meer en u krijgt een foutmelding zoals `Localhost heeft een ongeldig certificaat`?
  - Sonarr valideert nu SSL-certificaten. Als er geen SSL-certificaat is ingesteld in de downloadclient, of als u een zelfondertekend https-certificaat gebruikt zonder het CA-certificaat toe te voegen aan uw lokale certificaatopslag, weigert Sonarr verbinding te maken. Gratis correct ondertekende certificaten zijn beschikbaar via [let's encrypt](https://letsencrypt.org/).
  - Als uw downloadclient en Sonarr zich op dezelfde machine bevinden, is er geen reden om HTTPS te gebruiken, dus de eenvoudigste oplossing is om SSL uit te schakelen voor de verbinding. De meeste mensen zijn het erover eens dat dit ook niet nodig is in een lokaal netwerk. Het is mogelijk om certificaatvalidatie uit te schakelen in geavanceerde instellingen als u een onveilige SSL-configuratie wilt behouden.

## Hoe voorkom ik dat de browser wordt geopend bij het opstarten?

Afhankelijk van uw besturingssysteem zijn er meerdere mogelijke manieren.

- In `Instellingen` => `Algemeen` op sommige besturingssystemen is er een selectievakje om de browser bij het opstarten te openen.
- Bij het starten van Sonarr kunt u `-nobrowser` (*nix) of `/nobrowser` (Windows) toevoegen aan de argumenten.
- Stop Sonarr en bewerk het config.xml-bestand en wijzig `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## VPN's, Jackett en de \*ARRs

- Tenzij u zich in een repressief land bevindt zoals China, Australië of Zuid-Afrika, is uw torrentclient meestal het enige dat achter een VPN moet staan. Omdat het VPN-eindpunt wordt gedeeld door veel gebruikers, kunt u te maken krijgen met snelheidsbeperkingen, DDOS-bescherming en IP-blokkades van verschillende services die elke software gebruikt.
- Met andere woorden, het achter een VPN plaatsen van de \*Arrs (Lidarr, Prowlarr, Radarr, Readarr en Lidarr) kan ervoor zorgen dat de applicaties in sommige gevallen onbruikbaar zijn vanwege de ontoegankelijkheid van de services.

> **Om duidelijk te zijn, het is niet de vraag of VPN's problemen zullen veroorzaken met de \*Arrs, maar wanneer: beeldleveranciers zullen u blokkeren en cloudflare staat voor de meeste \*Arr-servers (updates, metadata, enz.) en kan u ook blokkeren**
{.is-warning}

- **Veel privé-trackers zullen u verbannen als u ze gebruikt of er toegang toe krijgt (bijvoorbeeld via Jackett of Prowlarr) via een VPN.**

### Gebruik van een VPN

- Als een VPN vereist is en Docker wordt gebruikt, wordt het aanbevolen om Hotio of Binhex's Download Client + VPN Containers te gebruiken.
- Als een VPN vereist is en Docker niet wordt gebruikt, moet uw VPN-client ***split tunneling*** ondersteunen, zodat alleen de vereiste (Download Client) apps achter de VPN staan.
- Veel problemen met toegang tot trackers kunnen worden opgelost door Google of Cloudflare's DNS-servers te gebruiken in plaats van de DNS-servers van uw internetprovider.
- In sommige gevallen (bijvoorbeeld Britse internetproviders) moet u uw torrent-downloadclient achter een VPN plaatsen en Jackett/Prowlarr als volgt:
  - plaats Jackett achter de VPN en zorg ervoor dat split tunneling lokale toegang toestaat
  - voor Prowlarr configureert u uw vpn-client om een proxy te bieden en voegt u de proxy toe in Instellingen => Indexers. Geef de proxy een tag en geef dezelfde tag aan eventuele indexers die deze moeten gebruiken.
    - Als het absoluut noodzakelijk is en als uw vpn geen manier biedt om een proxy te maken, kunt u Prowlarr achter de VPN plaatsen en ervoor zorgen dat split tunneling lokale toegang toestaat.

## Ik zie logberichten voor shows die ik niet heb/niet wil

- Deze berichten zijn volkomen normaal en komen van de RSS-feeds die Sonarr controleert om te zien of er afleveringen zijn die u wel wilt, meestal verschijnen deze alleen in debug/trace logging, maar in het geval van een probleem bij het verwerken van een item kunt u een waarschuwing of foutmelding zien. Het is veilig om de waarschuwingen/fouten te negeren, aangezien ze betrekking hebben op shows die u niet wilt. Als het gaat om een show die u wel wilt, open dan een ondersteuningsthread op de forums.

## Seeds van torrents worden niet automatisch verwijderd

- Wanneer een torrent die nog steeds aan het seeden is wordt geïmporteerd, wordt deze gekopieerd of hard gelinkt (indien ingeschakeld en *mogelijk*) zodat de torrentclient kan blijven seeden. In een ideale setup bevinden de torrent-downloadmap en de bibliothekenmap zich op hetzelfde bestandssysteem en *lijken ze erop* (Docker en netwerkshares maken het gemakkelijk om dit verkeerd te doen), waardoor hard links mogelijk zijn en verspilde ruimte wordt geminimaliseerd.
- Bovendien kunt u uw seedtijd-/ratio-doelen configureren in Sonarr of uw downloadclient, uw downloadclient instellen om te *pauzeren* of *stoppen* wanneer deze zijn bereikt en Verwijderen inschakelen onder Voltooide en Mislukte Download Handler. Op die manier worden torrents die klaar zijn met seeden verwijderd uit de downloadclient door Sonarr.

## Help, mijn Mac zegt dat Sonarr niet kan worden geopend omdat de ontwikkelaar niet kan worden geverifieerd

- Dit is eenvoudig, zie deze link voor meer informatie [hier](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
[![Ontwikkelaar kan niet worden geverifieerd](/assets/general/faq_1_mac.png)]

## Help, mijn Mac zegt dat Sonarr.app beschadigd is en niet kan worden geopend

- Dat komt ofwel door een beschadigde download, dus probeer het opnieuw, of [beveiligingsproblemen, zie deze gerelateerde FAQ-invoer.](#help-my-mac-says-sonarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Ik krijg een foutmelding: Database disk image is malformed

> U kunt dit ontvangen na het upgraden van sqlite3 naar 3.41. Sonarr v3.0.9 ondersteunt sqlite3 3.41 niet vanwege een brekende standaardwijziging. [Details over het probleem zijn te vinden in Sonarr GHI #5464](https://github.com/Sonarr/Sonarr/issues/5464)
> Dit is opgelost met Sonarr v3.0.10 en gebruikers moeten Sonarr dienovereenkomstig upgraden.
{.is-warning}

- **Fouten van `Error creating log database` duiden op problemen met logs.db**
  - Dit kan snel worden opgelost door de database een andere naam te geven of te verwijderen. De logdatabase bevat onbelangrijke informatie over de geschiedenis van opdrachten en updates, evenals Info-, Warn- en Error-vermeldingen.
- **Fouten van `Error creating main database` of algemene `database disk image is malformed` zonder specifieke database duiden op problemen met sonarr.db**
  - Ga verder met de onderstaande stappen.
- Dit betekent dat uw SQLite-database die de meeste informatie voor Sonarr opslaat, beschadigd is. U kunt proberen (een) back-up(s) te maken, de bestaande database te herstellen, de back-up(s) te herstellen, of als laatste redmiddel opnieuw te beginnen met een nieuwe database.
- Deze fout kan optreden als het databasebestand niet beschrijfbaar is door de gebruiker/groep waar \*Arr als wordt uitgevoerd. Permissies zijn waarschijnlijk alleen een probleem bij nieuwe installaties, gemigreerde installaties naar een nieuwe server, als u onlangs de machtigingen van uw appdata-directory hebt gewijzigd, of als u de gebruiker en groep hebt gewijzigd waar \*Arr als wordt uitgevoerd.
- Uw beste en eerste optie is om [te proberen een back-up te herstellen](#how-do-i-backuprestore-my-sonarr)
- U kunt ook proberen uw database te herstellen. Dit is meestal de enige optie wanneer dit probleem optreedt na een update. Probeer het [sqlite3 `.recover`-commando](/useful-tools#recovering-a-corrupt-db)
  - Als uw sqlite niet over `.recover` beschikt of als u een meer GUI-vriendelijke (bijv. Windows) manier wilt, volg dan [onze instructies op deze wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- Een andere mogelijke oorzaak van een fout in uw database is dat u uw database op een netwerkstation plaatst (nfs of smb of iets anders niet lokaal). **SQLite is ontworpen voor situaties waarin de gegevens en de toepassing op dezelfde machine bestaan.** Daarom moet uw \*Arr AppData-map (/config mount voor docker) op lokale opslag staan. [SQLite en netwerkstations werken niet goed samen en zullen uiteindelijk een beschadigde database veroorzaken](https://www.sqlite.org/draft/useovernet.html).
- Als u mergerFS gebruikt, moet u `direct_io` verwijderen omdat SQLite mmap gebruikt, wat niet wordt ondersteund door `direct_io`, zoals uitgelegd in de mergerFS [documentatie hier](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Ik gebruik Sonarr op een Mac en het werkt plotseling niet meer. Wat is er gebeurd?

- Waarschijnlijk is dit te wijten aan een bug in MacOS waardoor een van de Sonarr-databases beschadigd is geraakt.
- [Volg deze stappen om het op te lossen](#i-am-getting-an-error-database-disk-image-is-malformed)
- Probeer vervolgens Sonarr te starten en kijk of het werkt. Als het niet werkt, heeft u verdere ondersteuning nodig. Plaats een bericht op onze [reddit](http://reddit.com/r/Sonarr) of ga naar [discord](https://discord.sonarr.tv/) voor hulp.

## Waarom kan Sonarr mijn bestanden op een externe server niet zien?

- Zorg ervoor dat de gebruiker/groep waarmee u \*Arr uitvoert lees- en schrijftoegang heeft tot het gemonteerde station.
- Voor Linux zorg ervoor dat:
  - Als u een NFS-mount gebruikt, zorg ervoor dat `nolock` is ingeschakeld voor uw mount.
  - Als u een SMB-mount gebruikt, zorg ervoor dat `nobrl` is ingeschakeld voor uw mount.
- Voor Windows: Kort gezegd kan de gebruiker waarmee \*Arr wordt uitgevoerd (als service) of onder (als tray-app) geen toegang krijgen tot het bestandspad op de externe server. Dit kan verschillende redenen hebben, maar de meest voorkomende is dat \*Arr wordt uitgevoerd als een service, wat de hieronder beschreven problemen veroorzaakt.

### Sonarr wordt standaard uitgevoerd onder het LocalService-account, dat geen toegang heeft tot beveiligde externe bestandsshare

- Voer de service van Sonarr uit als een andere gebruiker die toegang heeft tot die share
- Open het venster Beheer van computer \> Services op uw Windows-server.
- Stop de Sonarr-service.
- Open het dialoogvenster Eigenschappen \> Aanmelden.
- Wijzig het gebruikersaccount van de service naar het doelgebruikersaccount.
- Voer Sonarr.exe uit via de opstartmap

### U gebruikt een toegewezen netwerkstation (geen UNC-pad)

- Wijzig uw paden naar UNC-paden (`\\server\share`)
- Voer Sonarr.exe uit via de opstartmap

## Toegewezen netwerkstations versus UNC-paden

- Het gebruik van toegewezen netwerkstations werkt over het algemeen niet erg goed, vooral wanneer Sonarr is geconfigureerd om als service te worden uitgevoerd. De betere manier om shares in te stellen, is door UNC-paden te gebruiken. Dus in plaats van `X:\TV` gebruikt u `\\Server\TV`.

- Een belangrijk punt om te onthouden is dat Sonarr padinformatie krijgt van de downloader, dus u moet ook NZBGet, SABNzbd of een andere downloader instellen om ook UNC-paden te gebruiken.

## Sonarr werkt niet op Big Sur

Voer uit:

```shell
chmod +x /Applications/Sonarr.app/Contents/MacOS/Sonarr
```

## Mijn aangepaste script werkt niet meer na een upgrade van v2

- Waarschijnlijk gaf u argumenten door in uw verbinding... dat wordt niet ondersteund.
- Om dit te corrigeren:
  1. Wijzig uw argument zodat het uw pad is
  1. Zorg ervoor dat de shebang in uw script overeenkomt met uw pwsh-pad (als u geen shebang-definitie hebt, voeg deze dan toe)
  1. Zorg ervoor dat het pwsh-script uitvoerbaar is

# Veelvoorkomende problemen bij het zoeken en downloaden van Sonarr

## Succesvolle zoekopdracht - Geen resultaten teruggegeven

- [Zie dit probleemoplossingsitem](/sonarr/troubleshooting#query-successful-no-results-returned)

## Waarom heeft Sonarr een aflevering die ik verwachtte niet gepakt?

Zorg er eerst voor dat u het bovenstaande gedeelte genaamd ["Hoe vindt Sonarr afleveringen?](#how-does-sonarr-find-episodes) hebt gelezen en begrepen. Zorg er vervolgens voor dat ten minste een van uw indexers de aflevering heeft die u verwachtte te pakken.

1. Klik op het pictogram 'Handmatig zoeken' naast de afleveringsvermelding in Sonarr. Zijn er resultaten? Zo nee, dan heeft Sonarr mogelijk problemen met communiceren met uw indexers, hebben uw indexers de aflevering niet, of is de aflevering onjuist benoemd/gecategoriseerd op de indexer.
1. **Als er resultaten zijn van stap 1**, controleer dan naast deze resultaten op het rode uitroeptekenpictogram. Houd de muisaanwijzer boven het pictogram om te zien waarom die release geen kandidaat is voor automatische downloads. Als elk resultaat het pictogram heeft, zal er geen automatische download plaatsvinden.
1. **Als er ten minste één geldig handmatig zoekresultaat is uit stap 2**, zou er een automatische download moeten hebben plaatsgevonden. Als dit niet het geval is, is de meest waarschijnlijke reden een tijdelijk communicatieprobleem dat een RSS-synchronisatie van uw indexer voorkomt. Het wordt aanbevolen om meerdere indexers in te stellen voor de beste resultaten.
1. **Als er geen handmatig resultaat is van een show, maar u het kunt vinden wanneer u de website van uw indexer doorzoekt** - Dit kan verschillende redenen hebben, bijvoorbeeld de release is niet correct getagd op uw indexer, waardoor deze niet wordt teruggegeven aan Sonarr in een automatische zoekopdracht. Deze [probleemoplossingsinvoer](/sonarr/troubleshooting#searches-indexers-and-trackers) biedt enkele tips om de oorzaak te achterhalen. Het activeren van meerdere indexers kan dit probleem helpen oplossen door meer bronnen voor dezelfde inhoud te bieden.

## Er zijn overeenkomende series gevonden via de geschiedenis van het pakken, maar de release is gematcht met de serie op basis van ID. Automatische import is niet mogelijk

- Zie [dit probleemoplossingsitem](/sonarr/troubleshooting#found-matching-series-via-grab-history-but-series-was-matched-by-series-id-automatic-import-is-not-possible)

- Op TVDb worden afleveringsnamen als onbekend getiteld met TBA en er is een cache van 24 uur op de TVDb API. Veranderingen op de TVDb-website duren meestal 24-48 uur voordat ze Sonarr bereiken vanwege de TVDb-cache (24 uur), skyhook-cache (enkele uren) en de vernieuwingsinterval van de serie (elke 12 uur). De [instelling Vereiste afleveringstitel](/sonarr/settings#importing) in Sonarr bepaalt het importgedrag wanneer de titel TBA is, maar na 48 uur na de uitzending van de serie wordt de release geïmporteerd, zelfs als de titel nog steeds TBA is. Er is ook geen automatische hernoeming van bestanden met de titel TBA. Let op dat de TBA-timer wordt berekend vanaf de uitzenddatum en -tijd van de aflevering, niet vanaf het moment dat u deze hebt gedownload of geüpload.

## Sonarr geeft aan dat de serie onbekend is bij zoekopdrachten of importeren

- Zie de [Waarom kan Sonarr geen afleveringsbestanden importeren voor serie X? / Waarom kan Sonarr geen releases vinden voor serie X?](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x) invoer

## Jackett's /all-eindpunt

{#jackett-all-endpoint}

- Het Jackett `/all`-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan problemen veroorzaken, dus het is vereist om elke tracker afzonderlijk toe te voegen. Als alternatief kunt u de Jackett & NZBHydra2-alternatief [Prowlarr](/prowlarr) overwegen.

- **Update 5 februari 2022: \*Arr-ondersteuning is stopgezet voor het jackett `\all`-eindpunt. Het Jackett /all-eindpunt wordt niet langer ondersteund (bijv. waarschuwingen treden op) vanaf v3.0.6.1457 omdat het alleen maar problemen veroorzaakt.**

- Het Jackett /all-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan problemen veroorzaken, dus het is nu vereist om elke tracker afzonderlijk toe te voegen.
- [Zelfs de ontwikkelaars van Jackett zeggen dat het vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Het gebruik van het /all-eindpunt heeft geen voordelen, alleen nadelen:
  - u verliest de controle over specifieke instellingen van indexers (categorieën, zoekmodi, enz.)
  - het mengen van zoekmodi (IMDB, query, enz.) kan leiden tot resultaten van lage kwaliteit
  - specifieke indexer-categorieën (\>= 100000) kunnen niet worden gebruikt.
  - trage indexers vertragen het algehele resultaat
  - het totale aantal resultaten is beperkt tot 1000
  - als een van de trackers in /all een fout retourneert, schakelt \*Arr deze uit en krijgt u nu geen resultaten meer.

### Oplossingen voor Jackett /All

- Voeg elke tracker in Jackett handmatig toe als een indexer in \*Arr
- Bekijk [Prowlarr](/prowlarr), dat indexers kan synchroniseren met \*Arr en afkomstig is van het Lidarr/Radarr/Readarr-ontwikkelingsteam.
- Bekijk [NZBHydra2](https://github.com/theotherp/nzbhydra2), dat indexers kan synchroniseren met \*Arr. Gebruik echter niet hun enkele aggregate-eindpunt en gebruik `multi` als synchronisatie wordt gebruikt.

## Jackett toont meer resultaten dan Sonarr bij handmatig zoeken

- Controleer de geconfigureerde categorieën voor uw tracker in Sonarr
- Dit komt meestal doordat Sonarr op een andere manier naar Jackett zoekt dan u. [Zie dit probleemoplossingsartikel voor meer informatie](/sonarr/troubleshooting#searches-indexers-and-trackers).

## Het vinden van cookies

- Sommige sites kunnen niet automatisch worden ingelogd en vereisen dat u handmatig inlogt en vervolgens de cookies aan Sonarr geeft om te kunnen werken. [Raadpleeg dit artikel voor meer informatie.](/useful-tools#finding-cookies)

## Torrents uitpakken

- De meeste torrentclients hebben geen automatische verwerking van gecomprimeerde archieven zoals hun usenet-tegenhangers. We raden [unpackerr](https://github.com/unpackerr/unpackerr) aan.

## Machtigingen

- Sonarr moet bestanden verplaatsen van waar de downloader ze plaatst naar de uiteindelijke locatie, dus dit betekent dat Sonarr zowel lees- als schrijftoegang nodig heeft tot zowel de bron- als de doelmap en -bestanden.
- Op Linux, waar best practices voorschrijven dat services worden uitgevoerd als hun eigen gebruiker, betekent dit waarschijnlijk dat u een gedeelde groep moet gebruiken en de mapmachtigingen moet instellen op `775` en bestanden op `664` in zowel uw downloader als Sonarr. In umask-notatie zou dat `002` zijn.

## Gedwongen authenticatie

- In Sonarr v4 (bèta) is authenticatie verplicht. Zie de [Sonarr v4 FAQ - Gedwongen authenticatie](/sonarr/faq-v4#forced-authentication) voor details.