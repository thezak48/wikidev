## Kan ik al mijn filmbestanden in één map opslaan?

- Ja, je kunt ervoor kiezen om al je filmbestanden in één map op te slaan. Dit kan handig zijn als je een overzicht wilt hebben van al je films op één plek. Om dit in te stellen, ga je naar de instellingen van Radarr en navigeer je naar het tabblad "Media Management". Onder het gedeelte "Bestandsbeheer" kun je de optie "Filmopslag" vinden. Hier kun je de gewenste map selecteren waarin je al je filmbestanden wilt opslaan. Zorg ervoor dat je de juiste machtigingen hebt om bestanden in deze map op te slaan en te openen.

> Opmerking: Het is belangrijk om te onthouden dat het opslaan van al je filmbestanden in één map gevolgen kan hebben voor de organisatie en het beheer van je bibliotheek. Zorg ervoor dat je een gestructureerde bestandsnaamconventie gebruikt om je films gemakkelijk te kunnen vinden en identificeren.

- Nee, dat is niet mogelijk. Radarr is een afsplitsing van [Sonarr](/sonarr), waarbij elke show een aparte map heeft. Deze beperking is een bekend pijnpunt voor veel gebruikers en zal misschien in een toekomstige versie worden opgelost. Houd er rekening mee dat dit geen eenvoudige wijziging is en effectief een volledige herschrijving van de backend vereist.
- Het [Custom Folder GitHub Issue](https://github.com/Radarr/Radarr/issues/153) behandelt technisch gezien dit verzoek, maar er is geen garantie dat het implementeren van alle filmbestanden in één map op dat moment zal gebeuren.
- Een mogelijke oplossing is als volgt. Let op dat je geen rescan in Radarr mag activeren, anders wordt de film als ontbrekend weergegeven en wordt de film nooit geüpgraded.
  - Gebruik een aangepast script
    - Het script moet worden geactiveerd bij importeren
    - Het moet zo worden ontworpen dat het het bestand verplaatst wanneer je dat wilt
    - Vervolgens moet het de Radarr API aanroepen en de film als onbewaakt markeren.
- Als je al je films van één map naar individuele mappen wilt verplaatsen, bekijk dan het artikel [Tips en trucs => Maak een map voor elke film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

## Kan ik al mijn films in één map in mijn bibliotheek plaatsen?

- Nee, zie hierboven.

## Hoe update ik Radarr?

- Ga naar Instellingen en vervolgens het tabblad Algemeen en toon geavanceerde instellingen (gebruik de schakelaar naast de opslaan knop).

1. Onder de sectie Updates wijzig je de branche naam naar `master` of `develop`
1. Opslaan

*Dit zal de bits van die branche niet onmiddellijk installeren, dit gebeurt tijdens de volgende update.*

- ![Huidige Master/Stabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (Standaard/Stabiel): Het is getest door gebruikers op de ontwikkel- en nachtelijke takken en er zijn geen grote problemen bekend. Deze versie ontvangt ongeveer maandelijks updates. Op GitHub is dit de `master` tak.

- ![Huidige Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (Bèta): Dit is de testversie. Uitgebracht na getest te zijn in de nachtelijke versie om ervoor te zorgen dat er geen onmiddellijke problemen zijn. Nieuwe functies en bugfixes worden hier als eerste uitgebracht na de nachtelijke versie. Het kan als semi-stabiel worden beschouwd, maar het is nog steeds `bèta`. Deze versie ontvangt wekelijks of tweewekelijks updates, afhankelijk van de ontwikkeling.

> **Waarschuwing: Het kan zijn dat je niet kunt teruggaan naar `master` nadat je naar deze tak bent overgeschakeld.** Op GitHub is dit een momentopname van de `develop` tak op een specifiek moment.
{.is-warning}

- ![Huidige Nightly/Onstabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (Alpha/Onstabiel): Dit is de allernieuwste versie. Het wordt uitgebracht zodra de code is toegevoegd en alle geautomatiseerde tests zijn geslaagd. Deze build is mogelijk nog niet door ons of andere gebruikers gebruikt. Er is geen garantie dat het in sommige gevallen zelfs zal werken. Deze tak wordt alleen aanbevolen voor gevorderde gebruikers. Problemen en zelfonderzoek worden verwacht in deze tak. ***Gebruik deze tak alleen als je weet wat je doet en bereid bent om je handen vuil te maken om een mislukte update te herstellen.*** Deze versie wordt onmiddellijk bijgewerkt.

> **Waarschuwing: Het kan zijn dat je niet kunt teruggaan naar `master` nadat je naar deze tak bent overgeschakeld.** Op GitHub is dit de `develop` tak.
{.is-danger}

- Opmerking: Als je installatie via Docker verloopt, voeg dan `:release`, `:latest`, `:testing` of `:develop` toe aan het einde van je container tag, afhankelijk van wie je builds maakt.

|                                                                    | ![Huidige Master/Laatste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Huidige Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Huidige Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Kan ik Radarr bijwerken binnen mijn Docker-container?

- *Technisch gezien wel.* **Maar dat zou je absoluut niet moeten doen.** Het is een fundamenteel principe van Docker. Er kunnen problemen met de database ontstaan als je je installatie binnenin bijwerkt naar de meest recente `nightly`, maar vervolgens de Docker-container zelf bijwerkt (mogelijk naar een oudere versie).

### Het installeren van een nieuwere versie

#### Native

1. Ga naar Systeem en vervolgens het tabblad Updates
1. Nieuwere versies die nog niet zijn geïnstalleerd, hebben een updateknop naast zich. Klik op die knop om de update te installeren.

#### Docker

1. Haal je tag opnieuw op en werk je container bij

## Kan ik terugschakelen van `nightly` naar `develop`?

## Kan ik schakelen tussen takken?

- Als de versie identiek is, kun je overschakelen, anders controleer je bij het ontwikkelingsteam of je kunt overschakelen van `nightly` naar `master`; `nightly` naar `develop`; of `develop` naar `master` voor jouw specifieke build.
- Als je deze instructies niet opvolgt, kan je Radarr onbruikbaar worden of fouten veroorzaken. Je bent gewaarschuwd. Als de onderstaande fouten zich voordoen, gebruik je een nieuwere database met een oudere \*Arr-versie die niet wordt ondersteund. Upgrade \*Arr naar de versie waarop je eerder zat of een nieuwere versie.
  - Voorbeeldfoutmeldingen:
    - `Fout bij het analyseren van kolom 45 (Language=31 - Int64)`
    - `De DataMapper kon het volgende veld niet laden: 'Languages' waarde`
    - `ID komt niet overeen met een bekende taal Parameter naam: id`
    - Andere soortgelijke databasefouten met ontbrekende kolommen of tabellen.

## Hoe maak ik een back-up/herstel ik Radarr?

### Een back-up maken van Radarr

#### Gebruik van ingebouwde back-up

- Ga naar Systeem => Back-up in de Radarr-UI
- Klik op de knop Back-up
- Download de zip nadat de back-up is gemaakt om deze veilig te bewaren

#### Gebruik van het bestandssysteem rechtstreeks

- Zoek de locatie van de AppData-map voor Radarr op
  - Ga via de Radarr-UI naar Systeem => Over
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Stop Radarr - Dit voorkomt beschadiging van de database
- Kopieer de inhoud naar een veilige locatie

### Herstellen van een back-up

> Het herstellen naar een besturingssysteem met verschillende paden werkt niet (Windows naar Linux, Linux naar Windows, Windows naar macOS of macOS naar Windows), het verplaatsen tussen macOS en Linux kan wel werken, omdat beide paden met `/` in plaats van `\` werken zoals Windows, maar dit wordt niet ondersteund. Je moet alle paden in de database handmatig bewerken of [Toolbarr](https://github.com/Notifiarr/toolbarr) gebruiken.
{.is-warning}

#### Gebruik van een zip-back-up

- Installeer Radarr opnieuw (indien van toepassing / nog niet geïnstalleerd)
- Start Radarr
- Ga naar Systeem => Back-up
- Selecteer Herstel back-up
- Selecteer Kies bestand
- Selecteer je back-up-zipbestand
- Selecteer Herstellen

#### Gebruik van een back-up van het bestandssysteem

- Installeer Radarr opnieuw (indien van toepassing / nog niet geïnstalleerd)
- Zoek de locatie van de AppData-map voor Radarr op
  - Start Radarr eenmaal en ga via de UI naar Systeem => Over
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Stop Radarr
- Verwijder de inhoud van de AppData-map **(inclusief de .db-wal/.db-journal-bestanden als ze bestaan)**
- Herstel vanuit je back-up
- Start Radarr
- Zolang de paden hetzelfde zijn, zal alles doorgaan waar het gebleven was

#### Bestandssysteemherstel op Synology NAS

> LET OP: Herstellen op een Synology vereist kennis van Linux en root SSH-toegang tot het Synology-apparaat.
{.is-warning}

- Installeer Radarr opnieuw (indien van toepassing / nog niet geïnstalleerd)
- Zoek de locatie van de AppData-map voor Radarr op
  - Start Radarr eenmaal en ga via de UI naar Systeem => Over
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Stop Radarr
- Maak verbinding met de Synology NAS via SSH en log in als root

> Bij sommige installaties is de gebruiker anders dan de onderstaande opdrachten: `chown -R sc-Radarr:Radarr *` {.is-info}

- Voer de volgende opdrachten uit:

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- Werk de machtigingen van de bestanden bij:

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- Start Radarr

# Veelvoorkomende problemen met Radarr

## Een taak is geannuleerd

- Radarr heeft geen reactie ontvangen van de server waar het verzoek naartoe is gestuurd na 100 seconden.
- De logs bevatten `System.Threading.Tasks.TaskCanceledException: A task was canceled.`
- Dit wordt vaak veroorzaakt door:
  - een verkeerde configuratie of het gebruik van een VPN
  - een verkeerde configuratie of het gebruik van een proxy
  - lokale DNS-problemen - Probeer over te schakelen naar een andere DNS-provider
  - lokale IPv6-problemen - *meest voorkomend* - meestal is IPv6 ingeschakeld op het host-systeem, maar niet functioneel
  - het gebruik van Privoxy en een verkeerde configuratie daarvan
  - PiHole [Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit) verzoeken
- Je kunt problemen oplossen met DNS `nslookup <domein.tld uit trace logs>` en ipv6 met `curl -sv -6 "<url uit trace logs>"` / alle andere connectiviteit met `curl -sv -4 "<url uit trace logs>"`

## Pad is al geconfigureerd voor een bestaande film

![existing-movie.png](/assets/radarr/existing-movie.png)

- Bibliotheekimport toont "Bestaand" of je krijgt een foutmelding "Pad is geconfigureerd voor een bestaande film"
- Dit gebeurt wanneer je een film probeert toe te voegen of het pad van een bestaande film probeert te bewerken dat al is toegewezen aan een andere film.
- Waarschijnlijk is dit veroorzaakt doordat je een niet-overeenkomende film niet hebt gecorrigeerd toen je je bibliotheek importeerde.
- Zoek de film die al is toegewezen aan dat pad en corrigeer deze.
  - Filmindex
  - Tabelweergave
  - Opties => Voeg pad toe als kolom
  - Sorteer en zoek de film met het genoteerde problematische pad.
- Als alternatief kun je de film verwijderen die het bestaande pad gebruikt uit Radarr

## Hoe kan ik de mappen van mijn films hernoemen?

{#rename-folders}

> Hetzelfde proces geldt ook voor het verplaatsen/wijzigen van de paden van films. Als je alleen de paden in Radarr bijwerkt en de bestanden niet hoeft te verplaatsen, selecteer dan "Ja, bestanden verplaatsen" niet in stap 5.
{.is-info}

1. Films
1. Film Editor
1. Selecteer welke films hun mapnaam moeten wijzigen
1. Wijzig de hoofdmap naar dezelfde hoofdmap waarin de films zich momenteel bevinden
1. Selecteer "Ja, bestanden verplaatsen"

> Als je Plex gebruikt, wordt hierdoor opnieuw detectie van intro's, miniaturen, hoofdstukken en voorbeeldmetadata geactiveerd.
{.is-warning}

## Bestands- en mapnaamgeving van films

- Momenteel vereist Radarr dat elke film zich in een map bevindt met het formaat dat ten minste `Film Titel (Jaar)/` bevat, optioneel zijn `_` of `.` geldige scheidingstekens. Om correcte kwaliteits- en resolutie-identificatie tijdens import mogelijk te maken, is een bestandsnaam zoals `Film Titel (Jaar) [Kwaliteit-Resolutie].ext` het beste, opnieuw zijn `_` of `.` geldige scheidingstekens.

  - Een handige tool om deze wijzigingen in je collectie aan te brengen is [filebot](http://www.filebot.net/#download), dat een betaalde versie heeft in zowel de Apple als Windows stores, maar gratis te vinden is op hun oude [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download) site. Het heeft zowel een GUI als CLI, dus je kunt gebruiken wat je prettig vindt. Voor het bovenstaande voorbeeld breidt `{ny}` uit naar `Naam (Jaar)` en `{vf}` geeft de resolutie zoals `1080p`. Er is niets om de kwaliteit af te leiden, dus je kunt het vervalsen met behulp van `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`, wat alles lager dan 720p de naam `[DVD-572p]` zal geven en gelijk aan of groter dan 720p zoals `[Bluray-1080p]`.

- Zie [Tips en trucs sectie => Maak een map voor elke film](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie) voor meer details.

## Film Mappen Verkeerd Genoemd

- De naamgeving van de map van de film is gebaseerd op de metadata (naam/jaar) op het moment dat de film werd toegevoegd. Als je een film hebt toegevoegd voordat deze werd uitgebracht, moet je mogelijk de truc met het hernoemen van de map gebruiken die hierboven is vermeld om de naamgeving van de filmmap bij te werken om de nieuwe huidige gegevens weer te geven.
- Zelfs als je films al in mappen staan, kunnen de mappen mogelijk niet correct zijn genoemd. De mapnaam moet `Film Titel (Jaar)` zijn, waarbij de titel en het jaar in de naam van de map essentieel zijn op dit moment.

  - Voorbeelden die goed werken:
    - `/mnt/Films/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Kinderfilms/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - Voorbeelden die werken, maar handmatig beheer vereisen:
    - Op alfabet: `/mnt/Films/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Op beoordeling: `/mnt/Films/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Op genre: `/mnt/Films/Crime, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Deze voorbeelden vereisen handmatig beheer wanneer de film wordt toegevoegd. Elk van de voorbeelden heeft veel hoofdmappen, zoals `A-D` en `E-G` in het eerste voorbeeld met de eerste letter, `R` en `PG-13` in het voorbeeld met de beoordeling, en je kunt raden naar de verscheidenheid aan genre-mappen. Bij het toevoegen van een nieuwe film moet de juiste hoofdmap worden geselecteerd voor dit formaat om te werken.
  - Voorbeelden die niet werken:
    - Enkele map: `/mnt/Kinderfilms/Frozen (2013) [Bluray-1080p].mkv`
      - Op dit moment moeten films gewoon in een map staan met de naam van de film. Er is geen manier om dit te omzeilen totdat er ontwikkelingswerk is gedaan om deze functie toe te voegen.
    - **Film** Naamgevingsindelingen van v0.2 die **Bestand** eigenschappen bevatten in de naam van de **filmmap** zoals ``{Film.Titel}.{Jaar van Uitgave}.{Kwaliteit.Volledig}-{MediaInfo.Eenvoudig}{`Release.Groep}`` werken niet in v3.
      - Mappen hebben betrekking op de film en zijn onafhankelijk van het bestand. Bovendien zal dit niet werken met de geplande ondersteuning voor meerdere bestanden per film.
      - De andere reden waarom dit is verwijderd, is dat het vaak tot verwarring leidde, databasecorruptie veroorzaakte en over het algemeen maar halfbakken was.
  - De [Tips en trucs sectie => Maak een map voor elke film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) is een geweldige bron om ervoor te zorgen dat je bestands- en mapstructuur goed werkt.

## Kan ik de taak voor het vernieuwen van films uitschakelen?

- Nee, en dat zou je ook niet moeten doen via enige SQL-hack. De taak voor het vernieuwen van films vraagt de upstream Servarr-proxy om te controleren of de metadata voor elke film (ids, cast, samenvatting, beoordeling, vertalingen, alternatieve titels, enz.) is bijgewerkt in vergelijking met wat er momenteel in Radarr staat. Indien nodig worden de toepasselijke films vervolgens bijgewerkt.
- Een veelvoorkomende klacht is dat de vernieuwingstaak zorgt voor zwaar I/O-gebruik.
- De belangrijkste instelling is "Filmmap opnieuw scannen na vernieuwen". Als je schijf-I/O-gebruik piekt tijdens een vernieuwing, wil je mogelijk de instelling voor het opnieuw scannen wijzigen in `Handmatig`.
  - Verander dit niet in `Nooit`, tenzij alle wijzigingen in je bibliotheek (nieuwe films, upgrades, verwijderingen, enz.) via Radarr worden gedaan.
  - Als je filmbestanden handmatig of via Plex of een ander programma van derden verwijdert, stel dit dan niet in op `Nooit`.
- De andere instelling die kan worden gewijzigd, is "Video's analyseren", wat wordt aanbevolen als je tdarr gebruikt of je bestanden op een andere manier extern wijzigt. Als je dit niet doet, kun je "Video's analyseren" veilig uitschakelen om wat I/O te verminderen.

## Hoe kan ik een functie aanvragen voor Radarr?

- Dit is gemakkelijk [klik hier](https://github.com/Radarr/Radarr/issues)

## Help, mijn Mac zegt dat Radarr niet kan worden geopend omdat de ontwikkelaar niet kan worden geverifieerd

- Dit is eenvoudig, zie deze link voor meer informatie [hier](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Developer Cannot be verified](developer-cannot-be-verified.png "Developer Cannot be verified")
- Als alternatief moet je Radarr zelf ondertekenen `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## Help, mijn Mac zegt dat Radarr.app beschadigd is en niet kan worden geopend

- Dat komt ofwel door een beschadigde download, dus probeer het opnieuw, of [beveiligingsproblemen, zie deze gerelateerde FAQ-invoer.](#help-my-mac-says-radarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Ik krijg een foutmelding: Database disk image is malformed

> \* Voor Radarr-gebruikers die dit ervaren na het upgraden naar v4.X-versies. v4-versies voeren verschillende verreikende migraties uit omdat als je database eerder op enige plaats beschadigd was (wat eerder draaiende Radarr mogelijk niet detecteerbaar was), de migratie zal mislukken. Dit zorgt ervoor dat Radarr niet kan starten. Het is waarschijnlijk dat al je back-ups ook beschadigd zijn, dus het simpelweg herstellen daarvan zal waarschijnlijk het probleem niet oplossen.
> \* Als de na de migratie gegenereerde database niet kan worden geopend of niet kan worden hersteld, maak dan een kopie van de database vanuit een recente back-up en pas het databaseherstelproces toe op dat bestand en probeer Radarr te starten met het herstelde back-upbestand. Het zou dan zonder problemen moeten migreren.
{.is-warning}

- **Fouten van `Error creating log database` geven problemen aan met logs.db**
  - Dit kan snel worden opgelost door de database te hernoemen of te verwijderen. De logboekdatabase bevat onbelangrijke informatie over de geschiedenis van opdrachten en installatiegeschiedenis van updates, en Info-, Warn- en Error-vermeldingen.
- **Fouten van `Error creating main database` of algemene `database disk image is malformed` zonder specifieke database geven problemen aan met radarr.db**
  - Ga verder met de hieronder genoemde stappen
- Dit betekent dat je SQLite-database die de meeste informatie voor Radarr opslaat, beschadigd is. Je opties zijn om (een) back-up(s) te proberen, de bestaande database te herstellen, de back-up(s) te herstellen, of als niets anders werkt, opnieuw te beginnen met een nieuwe, frisse database.
- Deze fout kan optreden als het databasebestand niet beschrijfbaar is voor de gebruiker/groep waarin \*Arr wordt uitgevoerd. Permissies als oorzaak zullen waarschijnlijk alleen een probleem zijn bij nieuwe installaties, gemigreerde installaties naar een nieuwe server, als je onlangs de machtigingen van je appdata-directory hebt gewijzigd, of als je de gebruiker en groep hebt gewijzigd waarin \*Arr wordt uitgevoerd.
- Je beste en eerste optie is om [te proberen te herstellen vanuit een back-up](#how-do-i-backuprestore-my-radarr). Voor gebruikers die deze foutmelding ontvangen na het upgraden naar v4, is het echter zeer onwaarschijnlijk dat de back-up zelf zal werken en moet je de andere genoemde herstelmethoden proberen.
- Je kunt ook proberen je database te herstellen. Dit is meestal de enige optie wanneer dit probleem optreedt na een update. Probeer het [sqlite3 `.recover` commando](/useful-tools#recovering-a-corrupt-db)
  - Als je sqlite niet over `.recover` beschikt of als je een meer GUI-vriendelijke manier (bijv. Windows) wilt, volg dan [onze instructies op deze wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- Een andere mogelijke oorzaak van het krijgen van een foutmelding met je database is dat je je database op een netwerkstation plaatst (nfs of smb of iets anders niet lokaal). **SQLite is ontworpen voor situaties waarin de gegevens en de toepassing op dezelfde machine bestaan.** Daarom moet je \*Arr AppData-map (/config-mount voor docker) zich op lokale opslag bevinden. [SQLite en netwerkstations werken niet goed samen en zullen uiteindelijk een beschadigde database veroorzaken](https://www.sqlite.org/draft/useovernet.html).
- Als je mergerFS gebruikt, moet je `direct_io` verwijderen omdat SQLite mmap gebruikt, dat niet wordt ondersteund door `direct_io`, zoals uitgelegd in de mergerFS [documentatie hier](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Ik gebruik Radarr op een Mac en het werkt plotseling niet meer. Wat is er gebeurd?

- Waarschijnlijk is dit te wijten aan een bug in MacOS waardoor een van de databases beschadigd is geraakt.
- Zie de bovenstaande invoer over een beschadigde database.
- Probeer vervolgens op te starten en kijk of het werkt. Als het niet werkt, heb je verdere ondersteuning nodig. Plaats in onze [subreddit /r/radarr](http://reddit.com/r/radarr) of kom naar [onze discord](https://radarr.video/discord) voor hulp.

## Waarom kan Radarr mijn bestanden op een externe server niet zien?

- Zorg ervoor dat de gebruiker/groep waarmee je \*Arr uitvoert lees- en schrijftoegang heeft tot de aangekoppelde schijf.
- Voor Linux zorg je ervoor dat:
  - Als je een NFS-aankoppeling gebruikt, zorg dan dat `nolock` is ingeschakeld voor je aankoppeling.
  - Als je een SMB-aankoppeling gebruikt, zorg dan dat `nobrl` is ingeschakeld voor je aankoppeling.
- Voor Windows: In het kort: de gebruiker waarmee \*Arr wordt uitgevoerd (als service) of onder (als tray-app) heeft geen toegang tot het bestandspad op de externe server. Dit kan verschillende redenen hebben, maar de meest voorkomende is dat \*Arr wordt uitgevoerd als een service, wat de hieronder beschreven problemen veroorzaakt.

### Radarr wordt standaard uitgevoerd onder het LocalService-account, dat geen toegang heeft tot beveiligde externe bestandsshare

- Voer de service van Radarr uit als een andere gebruiker die toegang heeft tot die share
- Open het venster `Administrative Tools` \> `Services` op je Windows-server.
- Stop de Radarr-service.
- Open het dialoogvenster `Properties` \> `Log On`.
- Wijzig het gebruikersaccount van de service naar het doelgebruikersaccount.
- Voer Radarr.exe uit met behulp van de opstartmap

### Je gebruikt een toegewezen netwerkstation (geen UNC-pad)

- Wijzig je paden naar UNC-paden (`\\server\share`)
- Voer Radarr.exe uit via de opstartmap

## Hoe schakel ik over van de Windows-service naar een tray-app?

1. Sluit Radarr af
1. Voer serviceuninstall.exe uit die zich in de Radarr-map bevindt
1. Voer `Radarr.exe` eenmaal uit als beheerder om het de juiste machtigingen te geven en de firewall te openen. Zodra dit is voltooid, kun je het sluiten en normaal uitvoeren.
1. (Optioneel) Plaats een snelkoppeling naar .exe in de opstartmap om automatisch op te starten bij het opstarten.

## Help, ik ben buitengesloten

{#help-i-have-forgotten-my-password}

Om authenticatie uit te schakelen (om je vergeten gebruikersnaam of wachtwoord opnieuw in te stellen), moet je `config.xml` bewerken, die zich bevindt in de [Radarr Appdata Directory](/radarr/appdata-directory)

1. Open config.xml in een teksteditor
1. Zoek de regel met de authenticatiemethode, dit zal zijn
`<AuthenticationMethod>Basic</AuthenticationMethod>` of `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Wijzig de regel `AuthenticationMethod` naar `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Radarr opnieuw op
1. Radarr is nu toegankelijk zonder wachtwoord, je moet naar `Instellingen: Algemeen` in de UI gaan en je gebruikersnaam en wachtwoord instellen

## Hoe voorkom ik dat de browser wordt geopend bij het opstarten?

Afhankelijk van je besturingssysteem zijn er meerdere mogelijke manieren.

- In `Instellingen` => `Algemeen` op sommige besturingssystemen is er een selectievakje om de browser bij het opstarten te openen.
- Bij het starten van Radarr kun je `-nobrowser` (*nix) of `/nobrowser` (Windows) toevoegen aan de argumenten.
- Stop Radarr en bewerk het configuratiebestand config.xml en wijzig `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## Vreemde UI-problemen

- Als je vreemde UI-problemen ondervindt, zoals de bibliotheekpagina die niets vermeldt of een bepaalde weergave of sortering die niet werkt, probeer dan te kijken in een Chrome Incognito-venster of Firefox Private Window. Als het daar goed werkt, wis dan je browsercache en cookies voor je specifieke IP/domein. Zie voor meer informatie het wiki-artikel [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage).

## Webinterface laadt alleen op localhost op Windows

- Als je alleen toegang hebt tot je webinterface op <http://localhost:7878/> of <http://127.0.0.1:7878/>, moet je minstens één keer als beheerder uitvoeren.

## Machtigingen

- Radarr moet bestanden verplaatsen van waar de downloader ze plaatst naar de uiteindelijke locatie, dit betekent dat het zowel lees- als schrijftoegang nodig heeft tot zowel de bron- als de doelmap en -bestanden.
- Op Linux, waar best practices services laten draaien als hun eigen gebruiker, betekent dit waarschijnlijk het gebruik van een gedeelde groep en het instellen van mapmachtigingen op `775` en bestanden op `664` zowel in je downloader als in \*Arr. In umask-notatie zou dat `002` zijn.

## Systeem & Logs laadt eindeloos

- Het is de easy-privacy blocklist. Ze blokkeren in feite elke URL met /api/log? erin. Bekijk de lijst en vertel me of je denkt dat het blokkeren van alle URL's in die lijst een verstandig idee is, er zijn tientallen URL's in die lijst die mogelijk sites breken. Je hebt dat geselecteerd in je adblocker. De eenvoudige oplossing is om het domein waarop Radarr wordt uitgevoerd op de whitelist te zetten. Maar ik raad nog steeds aan om de lijst te controleren.

## Torrents uitpakken

- De meeste torrentclients hebben geen automatische verwerking van gecomprimeerde archieven zoals hun usenet-tegenhangers. We raden [unpackerr](https://github.com/unpackerr/unpackerr) aan.

## uTorrent werkt niet meer

- Zorg ervoor dat de web-UI is ingeschakeld
- Zorg ervoor dat de alternatieve luisterpoort voor de web-UI (Geavanceerd => Web-UI) niet hetzelfde is als de luisterpoort (Verbindingen)
- We raden aan de alternatieve luisterpoort voor de web-UI te wijzigen om geen problemen te veroorzaken met het doorsturen van poorten voor verbindingen.

## Ik kreeg een pop-up dat config.xml beschadigd is, wat nu?

- Radarr kon je configuratiebestand bij het opstarten niet lezen omdat het op de een of andere manier beschadigd is geraakt. Om weer online te gaan, moet je `.xml` verwijderen in je [appdata-directory](/radarr/appdata-directory), zodra het is verwijderd, start het op en het zal starten op de standaardpoort (7878), je moet nu alle instellingen opnieuw configureren die je hebt geconfigureerd op de pagina Algemene instellingen.

## Ongeldig certificaat en andere HTTPS- of SSL-problemen

- Je downloadclient werkt niet meer en je krijgt een foutmelding zoals `Localhost is een ongeldig certificaat`?
  - Radarr valideert SSL-certificaten. Als er geen SSL-certificaat is ingesteld in de downloadclient, of als je een zelfondertekend https-certificaat gebruikt zonder het CA-certificaat toe te voegen aan je lokale certificaatopslag, zal Radarr weigeren verbinding te maken. Gratis correct ondertekende certificaten zijn beschikbaar via [Let's Encrypt](https://letsencrypt.org/).
  - Als je downloadclient en je machine op dezelfde computer staan, is er geen reden om HTTPS te gebruiken. De eenvoudigste oplossing is om SSL uit te schakelen voor de verbinding. De meeste mensen zijn het erover eens dat dit ook niet nodig is in een lokaal netwerk. Het is mogelijk om certificaatvalidatie uit te schakelen in de geavanceerde instellingen als je een onveilige SSL-configuratie wilt behouden.

## VPN's, Jackett en de \*ARRs

- Tenzij je je in een onderdrukkend land bevindt zoals China, Australië of Zuid-Afrika, is je torrentclient meestal het enige dat achter een VPN moet staan. Omdat het VPN-eindpunt wordt gedeeld door veel gebruikers, kun je te maken krijgen met snelheidsbeperkingen, DDOS-bescherming en IP-blokkades van verschillende services die elke software gebruikt.
- Met andere woorden, het achter een VPN plaatsen van de \*ARRs (Lidarr, Prowlarr, Radarr, Readarr en Lidarr) kan ervoor zorgen dat de applicaties in sommige gevallen onbruikbaar worden omdat de services niet toegankelijk zijn.

> **Om duidelijk te zijn, het is niet de vraag of VPN's problemen zullen veroorzaken met de \*ARRs, maar wanneer: beeldleveranciers zullen je blokkeren en Cloudflare staat voor de meeste \*ARR-servers (updates, metadata, enz.) en kan je ook blokkeren**
{.is-warning}

- **Veel privé-trackers zullen je verbannen als je ze gebruikt of er toegang toe hebt (bijvoorbeeld via Jackett of Prowlarr) via een VPN.**

### Gebruik van een VPN

- Als een VPN vereist is en Docker wordt gebruikt, wordt het aanbevolen om Hotio of Binhex's Download Client + VPN Containers te gebruiken.
- Als een VPN vereist is en Docker niet wordt gebruikt, moet je VPN-client ***split tunneling*** ondersteunen, zodat alleen de vereiste (Download Client) apps achter de VPN staan.
- Veel problemen met het openen van trackers kunnen worden opgelost door Google of Cloudflare's DNS-servers te gebruiken in plaats van de DNS-servers van je internetprovider.
- In sommige gevallen (bijvoorbeeld bij Britse internetproviders) moet je je torrent-downloadclient achter een VPN plaatsen en Jackett/Prowlarr als volgt:
  - plaats Jackett achter de VPN en zorg ervoor dat split tunneling lokale toegang toestaat
  - voor Prowlarr configureer je je VPN-client om een proxy te bieden en voeg je de proxy toe in Instellingen => Indexers. Geef de proxy een tag en geef dezelfde tag aan eventuele indexers die deze moeten gebruiken.
    - Indien absoluut noodzakelijk en als je VPN geen manier biedt om een proxy te maken, kun je Prowlarr achter de VPN plaatsen en ervoor zorgen dat split tunneling lokale toegang toestaat.

# Veelvoorkomende problemen bij het zoeken en downloaden in Radarr

## Waarom kan ik geen nieuwe film toevoegen aan Radarr?

{#waarom-kan-ik-geen-nieuwe-film-toevoegen-aan-radarr}

- Radarr gebruikt [The Movie Database (TMDb)](http://themoviedb.org) voor filminformatie en afbeeldingen zoals fanart, banners en achtergronden. Over het algemeen zijn er een paar redenen waarom je mogelijk geen film kunt toevoegen:
  - TMDb houdt niet van speciale tekens bij het zoeken naar films via de API (die Radarr gebruikt), dus probeer te zoeken naar een vertaalde naam en/of zonder speciale tekens.
  - Je kunt ook zoeken op TMDb ID of, als TMDb het heeft, de IMDb ID.
  - De film is nog niet toegevoegd aan TMDb, volg hun [handleiding](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006) om deze toe te voegen.

## Jackett toont meer resultaten dan bij handmatig zoeken

- Dit komt meestal doordat je op een andere manier zoekt in Jackett dan je normaal doet. Zie ons [probleemoplossingsartikel](/radarr/troubleshooting) voor meer informatie.

## Hoe bepaalt Radarr het jaartal van een film?

- Radarr haalt metadata op van [TMDb](https://www.themoviedb.org/)
- Radarr gebruikt het jaartal van de oudste **Theatrical Release**-datum en de oudste **Premier**-datum voor het matchen.
  - Let op: als er geen Theatrical Release bestaat, zal de logica terugvallen op de oudste fysieke of digitale releasedatum.
- Als een film ontbreekt aan een digitale, fysieke, theatervoorstelling of première-datum, moet TMDb worden bijgewerkt.
- [De Contribution Bible van TMDb](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013) vermeldt het volgende over hun release-types.
  - **Premiere** - Een premiere screening kan de vorm aannemen van een festivalvertoning (bijv. TIFF) of een premiere-evenement met de cast en crew in een grote stad (bijv. LA, Londen, Toronto).
  - **Theatrical** - Kan worden gebruikt voor de oorspronkelijke release en alle volgende officiële releases. Gebruikt voor brede of saturatie-releases. In de Verenigde Staten wordt 600-1.999 schermen beschouwd als een brede release en 2000+ als een saturatie-release.
  - **Theatrical (limited)** - Een beperkte theatervoorstelling is een distributiestrategie waarbij een nieuwe film in een paar theaters in een land wordt uitgebracht, meestal in grote steden. In de Verenigde Staten zijn er minder dan 600 theaters.
  - **Physical** - Omvat alle VHS-, DVD- en Blu-ray-releases.
  - **Digital** - Alle relevante releases kunnen worden toegevoegd, inclusief streamingplatforms, VOD-verhuur of -aankoop. Digitale vertoningen, inclusief online filmfestivals en virtuele bioscoopreleases, worden ook beschouwd als digitale releases.

## Hoe gaat Radarr om met buitenlandse films of buitenlandse titels?

> [De gids voor de aangepaste taalindeling van TRaSH](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) kan nuttig zijn om films in de gewenste taal(en) te krijgen.{.is-info}

> Vanaf 12 februari 2023 zal de metadatacache van Radarr bij het bepalen van de taal van een film de oorspronkelijke taal van TMDb beschouwen als de gesproken taal van TMDb, maar alleen als er slechts één gesproken taal bestaat voor de film op TMDb; anders wordt de oorspronkelijke TMDb-taal van de film gebruikt.
{.is-warning}

## Zoeken op ID

- **Indexers die zoeken op basis van ID ondersteunen** - Zoeken op indexers en trackers die zoeken op basis van ID (TMDbId, IMDbId, enz.) - zoals veel Usenet-indexers en veel privé-torrent-trackers - worden tekstzoekopdrachten niet gebruikt als er resultaten worden geretourneerd voor een zoekopdracht op basis van ID. Als er resultaten worden geretourneerd, wordt er niet teruggevallen op een naam/tekstzoekopdracht. Als je resultaten mist van je indexer, komt dit doordat de releases zijn gekoppeld aan het verkeerde film-ID.
  - De taal van de release kan ook worden afgeleid van de taal van de release van de indexer of tracker in het resultaat, indien opgegeven, in plaats van uit de naam te worden geparseerd.

## Tekstzoekopdrachten

- **Indexers die geen zoekopdrachten op basis van ID ondersteunen of geen resultaten retourneren voor zoekopdrachten op basis van ID** - Zoeken op zal de oorspronkelijke titel van de film, de Engelse titel en de vertaalde titel gebruiken van [welke talen je hebt ingesteld in het kwaliteitsprofiel van de film en eventuele aangepaste formaten met scores in het kwaliteitsprofiel groter dan nul](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/).
- Bij het parsen (d.w.z. importeren) wordt gezocht naar een overeenkomst in alle vertalingen en alternatieve titels.
  - De taal van de release kan ook worden afgeleid van de taal van de release van de indexer of tracker in het resultaat, indien opgegeven, in plaats van uit de naam te worden geparseerd.

## Buitenlandse films krijgen

- Om een film in een vreemde taal te krijgen, stel je de taal van het kwaliteitsprofiel van je film in op Original (Originele taal van de film\*), een specifieke taal voor dat profiel, of `Any` en maak je aangepaste formaten met een score groter dan 0 [met taalvoorwaarden om te bepalen welke taal moet worden gedownload - zie de gelinkte gids van TRaSH voor details](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/).
- Houd er rekening mee dat dit geen indexer-talen omvat die zijn geconfigureerd in de instellingen van de indexer als `multi`.
  - Let op dat vanaf [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c) `multi` niet langer wordt verondersteld Engels te omvatten
  - Gebruikers kunnen hun instellingen per indexer aanpassen om aan te geven welke taal(talen) `multi` aangeeft

## Hoe gaat Radarr om met "multi" in namen?

- Met Radarr v4.1+ gaat Radarr ervan uit dat
`multi` alleen de taal van de film is en **NIET** Engels, zoals in eerdere versies.
  - Gebruikers kunnen hun instellingen per indexer aanpassen om aan te geven welke taal(talen) `multi` aangeeft
- Let op dat `multi`-definities alleen helpen bij het parsen van releases en niet bij buitenlandse titels of filmzoekopdrachten.

## Help, film toegevoegd, maar niet gezocht

- Radarr zoekt niet *actief* automatisch naar ontbrekende films. In plaats daarvan wordt periodiek een query uitgevoerd op nieuwe berichten naar alle indexers die zijn geconfigureerd voor RSS. Wanneer een gewenste film of een film waarvan de snijvoorwaarden niet zijn voldaan in die lijst verschijnt, wordt deze gedownload. Dit betekent dat een film pas wordt gedownload als deze wordt gepost (of opnieuw wordt gepost).
- Als je een film toevoegt die je nu wilt hebben, is de beste optie om het vakje "Start zoekopdracht naar ontbrekende film" aan te vinken, links van de knop *Film toevoegen* (**1**). Je kunt ook naar de pagina van een film gaan die je hebt toegevoegd en op het vergrootglas "Zoeken" (**2**) klikken of de Gewenste weergave gebruiken om te zoeken naar ontbrekende of niet voldane films.

  - Film toevoegen en zoeken bij het toevoegen van een film
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - Zoeken naar een bestaande film
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jackett's /all-eindpunt

{#jackett-all-endpoint}

- Het Jackett `/all`-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan potentiële problemen veroorzaken, dus het is vereist om elke tracker afzonderlijk toe te voegen. Als alternatief kun je overwegen om de Jackett & NZBHydra2-alternatief [Prowlarr](/prowlarr) te gebruiken.

- **Update 1 januari 2022: Het Jackett `/all`-eindpunt wordt niet langer ondersteund (bijv. waarschuwingen worden weergegeven) vanaf 4.0.0.5730 omdat het alleen maar problemen veroorzaakt.**

- Het Jackett /all-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan potentiële problemen veroorzaken, dus het is nu vereist om elke tracker afzonderlijk toe te voegen.
- [Zelfs de ontwikkelaars van Jackett zeggen dat het vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Het gebruik van het /all-eindpunt heeft geen voordelen, alleen nadelen:
  - je verliest de controle over specifieke instellingen van indexers (categorieën, zoekmodi, enz.)
  - het mixen van zoekmodi (IMDB, query, enz.) kan leiden tot resultaten van lage kwaliteit
  - specifieke categorieën van indexers (\>= 100000) kunnen niet worden gebruikt.
  - trage indexers vertragen het algehele resultaat
  - het totale aantal resultaten is beperkt tot 1000
  - als een van de trackers in /all een fout retourneert, schakelt \*Arr deze uit en krijg je geen resultaten meer.

### Oplossingen voor Jackett /All

- Voeg elke tracker in Jackett handmatig toe als een indexer in \*Arr
- Bekijk [Prowlarr](/prowlarr), dat indexers kan synchroniseren met \*Arr en afkomstig is van het Lidarr/Radarr/Readarr-ontwikkelingsteam.
- Bekijk [NZBHydra2](https://github.com/theotherp/nzbhydra2), dat indexers kan synchroniseren met \*Arr. Gebruik echter niet hun enkele aggregate-eindpunt en gebruik `multi` als synchronisatie wordt gebruikt.

## Waarom zijn er twee bestanden? | Waarom blijft er een bestand achter in de downloads?

Dit is normaal. Met een setup die [hardlinks](https://trash-guides.info/hardlinks) ondersteunt, wordt er geen dubbele ruimte gebruikt. Hieronder wordt uitgelegd hoe het torrentproces werkt.

1. Radarr stuurt een downloadverzoek naar je client en koppelt het aan een label of categorienaam die je hebt geconfigureerd in de instellingen van de downloadclient. Voorbeelden: films, tv, series, muziek, enz.
1. Radarr houdt de actieve downloads bij van je downloadclients die deze categorienaam gebruiken. Deze monitoring gebeurt via de API van je downloadclient.
1. Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat je het bestand kunt seeden (de ratio of tijd kan worden aangepast in de downloadclient of vanuit Radarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar je mediamap, wordt het bestand gekoppeld met een hardlink als dit wordt ondersteund door je setup, anders wordt het bestand gekopieerd als hardlinks niet worden ondersteund.
1. Als de optie "Voltooide downloadverwerking - Voltooide verwijderen" is ingeschakeld in de instellingen van Radarr, zal Radarr het oorspronkelijke bestand en de torrent verwijderen uit je downloadclient, maar alleen als de downloadclient meldt dat het seeden is voltooid en de torrent is gestopt (d.w.z. gepauzeerd). Zie [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) voor hoe je je downloadclient optimaal kunt configureren.

> Hardlinks zijn standaard ingeschakeld. [Een hardlink gebruikt geen extra schijfruimte.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor je voltooide downloadmap en je mediamap. Als het maken van een hardlink mislukt of je setup geen hardlinks ondersteunt, wordt er teruggevallen op het kopiëren van het bestand.
{.is-info}

## Waarom werkt Radarr niet achter een omgekeerde proxy?

- Vanaf v3 is Radarr overgestapt op .NET en een nieuwe webserver. Om ervoor te zorgen dat SignalR werkt, de UI-knoppen werken, database-wijzigingen worden doorgevoerd en andere zaken. Is de volgende toevoeging vereist aan het location-blok voor Radarr:

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- Zorg ervoor dat je **niet** `proxy_set_header Connection "Upgrade";` toevoegt zoals wordt voorgesteld in de nginx-documentatie. **DIT WERKT NIET**
- [Zie dit ASP.NET Core-probleem](https://github.com/aspnet/AspNetCore/issues/17081)
- Als je een CDN zoals Cloudflare gebruikt, zorg er dan voor dat websockets zijn ingeschakeld om websocket-verbindingen toe te staan.
- Als je onverwachte omleidingen hebt, zorg er dan voor dat je hostheader wordt doorgestuurd.