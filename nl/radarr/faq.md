## Kan ik al mijn filmbestanden opslaan in één map?

- Ja, je kunt ervoor kiezen om al je filmbestanden op te slaan in één map. Dit kan handig zijn als je een overzicht wilt hebben van al je films op één locatie. Om dit in te stellen, ga je naar de instellingen van Radarr en navigeer je naar het tabblad "Media Management". Onder het gedeelte "Bestandsbeheer" kun je de optie "Basismap" vinden. Hier kun je de gewenste map selecteren waarin je al je filmbestanden wilt opslaan. Zorg ervoor dat je de juiste machtigingen hebt ingesteld, zodat Radarr toegang heeft tot deze map en bestanden kan maken en verplaatsen zoals vereist.

- Nee, dit is niet mogelijk. Radarr is een afsplitsing van [Sonarr](/sonarr), waarbij elke serie een aparte map heeft. Deze beperking is een bekend pijnpunt voor veel gebruikers en zal mogelijk in een toekomstige versie worden opgelost. Houd er rekening mee dat dit geen eenvoudige wijziging is en dat het feitelijk een volledige herschrijving van de backend vereist.
- Het [Custom Folder GitHub Issue](https://github.com/Radarr/Radarr/issues/153) behandelt technisch gezien dit verzoek, maar dit betekent niet dat het implementeren van alle filmbestanden in één map op dat moment zal gebeuren.
- Een mogelijke oplossing is om een aangepast script te gebruiken. 
  - Het script moet worden geactiveerd bij het importeren van een film.
  - Het script moet zo worden ontworpen dat het het bestand verplaatst wanneer je dat wilt.
  - Vervolgens moet het script de Radarr API aanroepen en de film als onbewaakt markeren.
- Als je al je films wilt verplaatsen van één map naar individuele mappen, bekijk dan het artikel [Tips en trucs => Maak een map voor elke film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie).

## Kan ik al mijn films in één map plaatsen in mijn bibliotheek?

- Nee, zie hierboven.

## Hoe update ik Radarr?

- Ga naar Instellingen en vervolgens het tabblad Algemeen en toon geavanceerde instellingen (gebruik de schakelaar naast de opslaan knop).

1. Onder de sectie Updates wijzig je de branchnaam naar `master` of `develop`.
1. Opslaan.

*Dit zal de bits van die branch niet onmiddellijk installeren, dit gebeurt tijdens de volgende update.*

- ![Huidige Master/Stabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (Standaard/Stabiel): Het is getest door gebruikers op de ontwikkel- en nachtelijke branches en er zijn geen grote problemen bekend. Deze versie ontvangt ongeveer maandelijks updates. Op GitHub is dit de `master` branch.

- ![Huidige Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (Bèta): Dit is de testversie. Uitgebracht na getest te zijn in de nachtelijke versie om ervoor te zorgen dat er geen onmiddellijke problemen zijn. Nieuwe functies en bugfixes worden hier als eerste uitgebracht na de nachtelijke versie. Het kan als semi-stabiel worden beschouwd, maar het is nog steeds `bèta`. Deze versie ontvangt wekelijks of tweewekelijks updates, afhankelijk van de ontwikkeling.

> **Waarschuwing: Je kunt mogelijk niet teruggaan naar `master` nadat je naar deze branch bent overgeschakeld.** Op GitHub is dit een momentopname van de `develop` branch op een specifiek moment.
{.is-warning}

- ![Huidige Nightly/Onstabiel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (Alpha/Onstabiel): Dit is de meest recente versie. Het wordt uitgebracht zodra de code is toegevoegd en alle geautomatiseerde tests zijn geslaagd. Deze build is mogelijk nog niet door ons of andere gebruikers gebruikt. Er is geen garantie dat het in sommige gevallen zelfs zal werken. Deze branch wordt alleen aanbevolen voor gevorderde gebruikers. Problemen en zelfonderzoek worden verwacht in deze branch. ***Gebruik deze branch alleen als je weet wat je doet en bereid bent om je handen vuil te maken om een mislukte update te herstellen.*** Deze versie wordt onmiddellijk bijgewerkt.

> **Waarschuwing: Je kunt mogelijk niet teruggaan naar `master` nadat je naar deze branch bent overgeschakeld.** Op GitHub is dit de `develop` branch.
{.is-danger}

- Opmerking: Als je Radarr via Docker hebt geïnstalleerd, voeg dan `:release`, `:latest`, `:testing` of `:develop` toe aan het einde van je container tag, afhankelijk van wie je builds maakt.

|                                                                    | ![Huidige Master/Laatste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Huidige Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Huidige Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Kan ik Radarr updaten binnen mijn Docker-container?

- *Technisch gezien wel.* **Maar je moet dit absoluut niet doen.** Dit is een fundamenteel principe van Docker. Er kunnen problemen met de database ontstaan als je je installatie binnenin bijwerkt naar de meest recente `nightly` en vervolgens de Docker-container zelf bijwerkt (mogelijk terug naar een oudere versie).

### Het installeren van een nieuwere versie

#### Native

1. Ga naar Systeem en vervolgens het tabblad Updates.
1. Nieuwere versies die nog niet zijn geïnstalleerd, hebben een updateknop naast zich. Klik op die knop om de update te installeren.

#### Docker

1. Haal je tag opnieuw op en werk je container bij.

## Kan ik terugschakelen van `nightly` naar `develop`?

## Kan ik schakelen tussen branches?

- Als de versie identiek is, kun je overschakelen. Controleer anders bij het ontwikkelingsteam of je kunt overschakelen van `nightly` naar `master`; `nightly` naar `develop`; of `develop` naar `master` voor jouw specifieke build.
- Als je deze instructies niet volgt, kan je Radarr onbruikbaar worden of fouten veroorzaken. Je bent gewaarschuwd. Als de onderstaande fouten zich voordoen, gebruik je een nieuwere database met een oudere \*Arr-versie die niet wordt ondersteund. Upgrade \*Arr naar de versie waarop je eerder zat of een nieuwere versie.
  - Voorbeeldfoutmeldingen:
    - `Fout bij het analyseren van kolom 45 (Language=31 - Int64)`
    - `De DataMapper kon het volgende veld niet laden: 'Languages' waarde`
    - `ID komt niet overeen met een bekende taal Parameter naam: id`
    - Andere soortgelijke databasefouten met ontbrekende kolommen of tabellen.

## Hoe maak ik een back-up/herstel ik Radarr?

### Een back-up maken van Radarr

#### Gebruik van de ingebouwde back-up

- Ga naar Systeem => Back-up in de Radarr-UI.
- Klik op de knop Back-up.
- Download de zip nadat de back-up is gemaakt om deze veilig te bewaren.

#### Gebruik van het bestandssysteem rechtstreeks

- Zoek de locatie van de AppData-map voor Radarr op.
  - Ga via de Radarr-UI naar Systeem => Over.
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Stop Radarr - Dit voorkomt beschadiging van de database.
- Kopieer de inhoud naar een veilige locatie.

### Herstellen vanaf een back-up

> Het herstellen naar een besturingssysteem met verschillende paden werkt niet (Windows naar Linux, Linux naar Windows, Windows naar macOS of macOS naar Windows). Het verplaatsen tussen macOS en Linux kan wel werken, omdat beide paden met `/` in plaats van `\` werken, dat Windows gebruikt, maar dit wordt niet ondersteund. Je moet alle paden in de database handmatig bewerken of [Toolbarr](https://github.com/Notifiarr/toolbarr) gebruiken.
{.is-warning}

#### Gebruik van een zip-back-up

- Installeer Radarr opnieuw (indien van toepassing / nog niet geïnstalleerd).
- Start Radarr.
- Ga naar Systeem => Back-up.
- Selecteer Herstel back-up.
- Selecteer Kies bestand.
- Selecteer je back-up-zipbestand.
- Selecteer Herstellen.

#### Gebruik van een back-up van het bestandssysteem

- Installeer Radarr opnieuw (indien van toepassing / nog niet geïnstalleerd).
- Zoek de locatie van de AppData-map voor Radarr op.
  - Start Radarr eenmaal en ga via de UI naar Systeem => Over.
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Stop Radarr.
- Verwijder de inhoud van de AppData-map **(inclusief de .db-wal/.db-journal-bestanden als ze bestaan)**.
- Herstel vanaf je back-up.
- Start Radarr.
- Zolang de paden hetzelfde zijn, zal alles doorgaan waar het gebleven was.

#### Bestandssysteemherstel op Synology NAS

> LET OP: Herstellen op een Synology vereist kennis van Linux en root SSH-toegang tot het Synology-apparaat.
{.is-warning}

- Installeer Radarr opnieuw (indien van toepassing / nog niet geïnstalleerd).
- Zoek de locatie van de AppData-map voor Radarr op.
  - Start Radarr eenmaal en ga via de UI naar Systeem => Over.
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Stop Radarr.
- Maak verbinding met de Synology NAS via SSH en log in als root.

> Bij sommige installaties is de gebruiker anders dan de onderstaande opdrachten: `chown -R sc-Radarr:Radarr *` {.is-info}

- Voer de volgende opdrachten uit:

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- Werk de rechten van de bestanden bij:

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- Start Radarr

# Veelvoorkomende problemen met Radarr

## Een taak is geannuleerd

- Radarr heeft geen reactie ontvangen van de server waar het verzoek naartoe is gestuurd na 100 seconden.
- De logs bevatten `System.Threading.Tasks.TaskCanceledException: A task was canceled.`.
- Dit wordt vaak veroorzaakt door:
  - een verkeerde configuratie of het gebruik van een VPN
  - een verkeerde configuratie of het gebruik van een proxy
  - lokale DNS-problemen - Probeer over te schakelen naar een andere DNS-provider
  - lokale IPv6-problemen - *meest voorkomend* - meestal is IPv6 ingeschakeld op het host-systeem, maar niet functioneel
  - het gebruik van Privoxy en een verkeerde configuratie daarvan
  - PiHole [Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit) verzoeken
- Je kunt het probleem oplossen met DNS `nslookup <domein.tld uit trace logs>` en IPv6 met `curl -sv -6 "<url uit trace logs>"` / alle andere connectiviteit met `curl -sv -4 "<url uit trace logs>"`

## Het pad is al geconfigureerd voor een bestaande film

![existing-movie.png](/assets/radarr/existing-movie.png)

- De bibliotheekimport toont "Bestaand" of je krijgt een foutmelding "Het pad is geconfigureerd voor een bestaande film".
- Dit gebeurt wanneer je probeert een film toe te voegen of het pad van een bestaande film te bewerken dat al is toegewezen aan een andere film.
- Waarschijnlijk is dit veroorzaakt doordat je een verkeerde film niet hebt gecorrigeerd toen je je bibliotheek importeerde.
- Zoek de film die al is toegewezen aan het pad van die film en corrigeer deze.
  - Filmindex
  - Tabelweergave
  - Opties => Voeg pad toe als kolom
  - Sorteer en zoek de film met het genoteerde problematische pad.
- Als alternatief kun je de film verwijderen die het bestaande pad gebruikt in Radarr.

## Hoe kan ik de mappen van mijn films hernoemen?

{#rename-folders}

> Hetzelfde proces geldt ook voor het verplaatsen/wijzigen van de paden van films. Als je alleen de paden in Radarr bijwerkt en de bestanden niet hoeft te verplaatsen, selecteer dan geen "Ja, bestanden verplaatsen" in Stap 5.
{.is-info}

1. Films
1. Film-editor
1. Selecteer welke films hun mapnaam moeten wijzigen
1. Wijzig de hoofdmap naar dezelfde hoofdmap waarin de films zich momenteel bevinden
1. Selecteer "Ja, bestanden verplaatsen"

> Als je Plex gebruikt, wordt hierdoor de herkenning van intro's, miniaturen, hoofdstukken en voorbeeldmetadata opnieuw geactiveerd.
{.is-warning}

## Naamgeving van filmbestanden en -mappen

- Momenteel vereist Radarr dat elke film zich in een map bevindt met het formaat `Filmnaam (Jaar)/`, optioneel zijn `_` of `.` geldige scheidingstekens. Om correcte kwaliteits- en resolutie-identificatie tijdens het importeren te vergemakkelijken, is een bestandsnaam zoals `Filmnaam (Jaar) [Kwaliteit-Resolutie].ext` het beste, opnieuw zijn `_` of `.` geldige scheidingstekens.

  - Een handige tool om deze wijzigingen in je collectie aan te brengen is [filebot](http://www.filebot.net/#download), dat een betaalde versie heeft in zowel de Apple als Windows stores, maar gratis te vinden is op hun legacy [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download) site. Het heeft zowel een GUI als CLI, dus je kunt gebruiken wat je prettig vindt. Voor het bovenstaande voorbeeld breidt `{ny}` uit naar `Naam (Jaar)` en `{vf}` geeft de resolutie zoals `1080p`. Er is niets om de kwaliteit af te leiden, dus je kunt het vervalsen met behulp van `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`, wat alles lager dan 720p zal noemen als `[DVD-572p]` en gelijk aan of groter dan 720p als `[Bluray-1080p]`.

- Zie [Tips en trucs sectie => Maak een map voor elke film](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie) voor meer details.

## Filmmappen verkeerd genoemd

- De naamgeving van de filmmappen is gebaseerd op de metadata (naam/jaar) op het moment dat de film werd toegevoegd. Als je een film hebt toegevoegd voordat deze werd uitgebracht, moet je mogelijk de truc met het hernoemen van de map gebruiken zoals hierboven vermeld om de naamgeving van de filmmap bij te werken zodat deze overeenkomt met de nieuwe huidige gegevens.
- Zelfs als je films al in mappen staan, kunnen de mappen mogelijk niet correct zijn genoemd. De mapnaam moet `Filmnaam (Jaar)` zijn, het hebben van de titel en het jaar in de naam van de map is momenteel essentieel.

  - Voorbeelden die goed werken:
    - `/mnt/Films/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Kinderfilms/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - Voorbeelden die werken, maar handmatig beheer vereisen:
    - Op alfabet: `/mnt/Films/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Op beoordeling: `/mnt/Films/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Op genre: `/mnt/Films/Crime, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Deze voorbeelden vereisen handmatig beheer wanneer de film wordt toegevoegd. Elk van de voorbeelden heeft veel hoofdmappen, zoals `A-D` en `E-G` in het voorbeeld met de eerste letter, `R` en `PG-13` in het voorbeeld met de beoordeling, en je kunt raden naar de verscheidenheid aan genre-mappen. Bij het toevoegen van een nieuwe film moet de juiste basismap worden geselecteerd voor dit formaat om te werken.
  - Voorbeelden die niet werken:
    - Enkele map: `/mnt/Kinderfilms/Frozen (2013) [Bluray-1080p].mkv`
      - Op dit moment moeten films gewoon in een map staan met de naam van de film. Er is geen manier om dit te omzeilen totdat er ontwikkelingswerk is gedaan om deze functie toe te voegen.
    - **Film** Naamgevingsindelingen vanaf v0.2 die **Bestand** eigenschappen bevatten in de naam van de **filmmap** zoals ``{Film.Titel}.{Jaar van uitgave}.{Kwaliteit.Volledig}-{MediaInfo.Eenvoudig}{`Release.Groep}`` werken niet in v3.
      - Mappen hebben betrekking op de film en zijn onafhankelijk van het bestand. Bovendien zal dit breken met de geplande ondersteuning voor meerdere bestanden per film.
      - De andere reden waarom dit is verwijderd, is dat het vaak voor verwarring zorgde, databasecorruptie veroorzaakte en over het algemeen maar halfbakken was.
  - De [Tips en trucs sectie => Maak een map voor elke film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) is een geweldige bron om ervoor te zorgen dat je bestands- en mapstructuur goed werkt.

## Kan ik de taak 'films vernieuwen' uitschakelen?

- Nee, en dat zou je ook niet moeten doen via enige SQL-hack. De taak 'films vernieuwen' vraagt de upstream Servarr-proxy op en controleert of de metadata voor elke film (ids, cast, samenvatting, beoordeling, vertalingen, alternatieve titels, enz.) is bijgewerkt in vergelijking met wat er momenteel in Radarr staat. Indien nodig zal het de betreffende films bijwerken.
- Een veelvoorkomende klacht is dat de vernieuwingstaak zorgt voor zware I/O-gebruik.
- De belangrijkste instelling is "Filmmap opnieuw scannen na vernieuwen". Als je schijf-I/O-gebruik piekt tijdens een vernieuwing, wil je mogelijk de scaninstelling wijzigen naar `Handmatig`.
  - Verander dit niet in `Nooit`, tenzij alle wijzigingen in je bibliotheek (nieuwe films, upgrades, verwijderingen, enz.) via Radarr worden gedaan.
  - Als je filmbestanden handmatig of via Plex of een ander programma van derden verwijdert, stel dit dan niet in op `Nooit`.
- De andere instelling die kan worden gewijzigd, is "Video's analyseren", wat wordt aanbevolen als je tdarr gebruikt of je bestanden op een andere manier extern wijzigt. Als je dit niet doet, kun je "Video's analyseren" veilig uitschakelen om wat I/O te verminderen.

## Hoe kan ik een functie aanvragen voor Radarr?

- Dit is gemakkelijk [klik hier](https://github.com/Radarr/Radarr/issues)

## Help, mijn Mac zegt dat Radarr niet kan worden geopend omdat de ontwikkelaar niet kan worden geverifieerd

- Dit is eenvoudig, zie deze link voor meer informatie [hier](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Ontwikkelaar kan niet worden geverifieerd](developer-cannot-be-verified.png "Ontwikkelaar kan niet worden geverifieerd")
- Mogelijk moet je Radarr zelf ondertekenen met `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## Help, mijn Mac zegt dat Radarr.app beschadigd is en niet kan worden geopend

- Dat komt ofwel door een beschadigde download, dus probeer het opnieuw, of [beveiligingsproblemen, zie deze gerelateerde FAQ-entry.](#help-my-mac-says-radarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Ik krijg een foutmelding: Database disk image is malformed

> \* Voor Radarr-gebruikers die dit ervaren na het upgraden naar v4.X-versies. v4-versies voeren verschillende verreikende migraties uit omdat als je database eerder op enige plaats beschadigd was (wat mogelijk niet detecteerbaar was tijdens het uitvoeren van Radarr), de migratie zal mislukken. Hierdoor kan Radarr niet starten. Waarschijnlijk zijn al je back-ups ook beschadigd, dus het simpelweg herstellen ervan zal waarschijnlijk het probleem niet oplossen.
> \* Als de na migratie gegenereerde database niet kan worden geopend of niet kan worden hersteld, maak dan een kopie van de database vanuit een recente back-up en pas het databaseherstelproces toe op dat bestand en probeer Radarr te starten met het herstelde back-upbestand. Het zou dan zonder problemen moeten migreren.
{.is-warning}

- **Fouten van `Error creating log database` geven problemen aan met logs.db**
  - Dit kan snel worden opgelost door de database te hernoemen of te verwijderen. De logboekdatabase bevat onbelangrijke informatie over de geschiedenis van opdrachten en installatiegeschiedenis van updates, en Info-, Warn- en Error-vermeldingen.
- **Fouten van `Error creating main database` of algemene `database disk image is malformed` zonder specifieke database geven problemen aan met radarr.db**
  - Ga verder met de hieronder genoemde stappen
- Dit betekent dat je SQLite-database die de meeste informatie voor Radarr opslaat, beschadigd is. Je opties zijn om (een) back-up(s) te proberen, de bestaande database te herstellen, de back-up(s) te herstellen, of als niets anders werkt opnieuw te beginnen met een nieuwe database.
- Deze fout kan optreden als het databasebestand niet beschrijfbaar is door de gebruiker/groep waarin \*Arr wordt uitgevoerd. Permissies als oorzaak zullen waarschijnlijk alleen een probleem zijn bij nieuwe installaties, gemigreerde installaties naar een nieuwe server, als je onlangs de machtigingen van je appdata-directory hebt gewijzigd, of als je de gebruiker en groep \*Arr hebt gewijzigd.
- Je beste en eerste optie is om [te proberen te herstellen vanuit een back-up](#how-do-i-backuprestore-my-radarr). Voor gebruikers die deze foutmelding ontvangen na het upgraden naar v4 is het echter zeer onwaarschijnlijk dat de back-up zelf zal werken en moet je de andere genoemde herstelmethoden proberen.
- Je kunt ook proberen je database te herstellen. Dit is meestal de enige optie wanneer dit probleem optreedt na een update. Probeer het [sqlite3 `.recover`-commando](/useful-tools#recovering-a-corrupt-db)
  - Als je sqlite niet over `.recover` beschikt of als je een meer GUI-vriendelijke (bijv. Windows) manier wilt, volg dan [onze instructies op deze wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- Een andere mogelijke oorzaak van het krijgen van een foutmelding met je database is dat je je database op een netwerkstation plaatst (nfs of smb of iets anders niet lokaal). **SQLite is ontworpen voor situaties waarin de gegevens en de toepassing op dezelfde machine bestaan.** Daarom moet je \*Arr AppData-map (/config-mount voor docker) op lokale opslag staan. [SQLite en netwerkstations werken niet goed samen en zullen uiteindelijk leiden tot een beschadigde database](https://www.sqlite.org/draft/useovernet.html).
- Als je mergerFS gebruikt, moet je `direct_io` verwijderen omdat SQLite mmap gebruikt, wat niet wordt ondersteund door `direct_io`, zoals uitgelegd in de mergerFS [documentatie hier](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Ik gebruik Radarr op een Mac en het werkt plotseling niet meer. Wat is er gebeurd?

- Waarschijnlijk is dit te wijten aan een bug in MacOS waardoor een van de databases beschadigd is geraakt.
- Zie de bovenstaande vermelding over een beschadigde database.
- Probeer het vervolgens opnieuw te starten en kijk of het werkt. Als het niet werkt, heb je verdere ondersteuning nodig. Plaats een bericht op onze [subreddit /r/radarr](http://reddit.com/r/radarr) of kom naar [onze discord](https://radarr.video/discord) voor hulp.

## Waarom kan Radarr mijn bestanden op een externe server niet zien?

- Zorg ervoor dat de gebruiker/groep waarmee je \*Arr uitvoert lees- en schrijftoegang heeft tot de gemounte schijf.
- Voor Linux zorg je ervoor dat:
  - Als je een NFS-mount gebruikt, zorg dan dat `nolock` is ingeschakeld voor je mount.
  - Als je een SMB-mount gebruikt, zorg dan dat `nobrl` is ingeschakeld voor je mount.
- Voor Windows: in het kort: de gebruiker waarmee \*Arr wordt uitgevoerd (als service) of onder wie \*Arr wordt uitgevoerd (als tray-app) heeft geen toegang tot het bestandspad op de externe server. Dit kan verschillende redenen hebben, maar de meest voorkomende is dat \*Arr wordt uitgevoerd als een service, wat de hieronder beschreven problemen veroorzaakt.

### Radarr wordt standaard uitgevoerd onder het LocalService-account, dat geen toegang heeft tot beveiligde externe bestandsshare

- Voer de service van Radarr uit als een andere gebruiker die toegang heeft tot die share
- Open het venster 'Administratieve hulpmiddelen' \> 'Services' op je Windows-server.
- Stop de Radarr-service.
- Open het dialoogvenster 'Eigenschappen' \> 'Aanmelden'.
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
1. Zoek de regel met de authenticatiemethode, deze zal zijn
`<AuthenticationMethod>Basic</AuthenticationMethod>` of `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Wijzig de regel `AuthenticationMethod` naar `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Radarr opnieuw op
1. Radarr is nu toegankelijk zonder wachtwoord, je moet naar de pagina 'Instellingen: Algemeen' gaan in de UI en je gebruikersnaam en wachtwoord instellen

## Hoe voorkom ik dat de browser wordt geopend bij het opstarten?

Afhankelijk van je besturingssysteem zijn er meerdere mogelijke manieren.

- In `Instellingen` => `Algemeen` op sommige besturingssystemen is er een selectievakje om de browser bij het opstarten te openen.
- Bij het starten van Radarr kun je `-nobrowser` (*nix) of `/nobrowser` (Windows) toevoegen aan de argumenten.
- Stop Radarr en bewerk het config.xml-bestand en wijzig `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## Vreemde UI-problemen

- Als je vreemde UI-problemen ondervindt, zoals de pagina 'Bibliotheek' die niets vermeldt of een bepaalde weergave of sortering die niet werkt, probeer dan te kijken in een Chrome Incognito-venster of Firefox Private Window. Als het daar goed werkt, wis dan je browsercache en cookies voor je specifieke IP/domein. Zie het artikel [Cache, cookies en lokale opslag wissen](/useful-tools#clearing-cookies-and-local-storage) voor meer informatie.

## Webinterface laadt alleen op localhost op Windows

- Als je alleen toegang hebt tot je webinterface op <http://localhost:7878/> of <http://127.0.0.1:7878/>, moet je minstens één keer als beheerder uitvoeren.

## Machtigingen

- Radarr moet bestanden verplaatsen van waar de downloader ze plaatst naar de uiteindelijke locatie, dus dit betekent dat het zowel lees- als schrijftoegang nodig heeft tot zowel de bron- als de doelmap en -bestanden.
- Op Linux, waar best practices services laten draaien als hun eigen gebruiker, betekent dit waarschijnlijk het gebruik van een gedeelde groep en het instellen van mapmachtigingen op `775` en bestanden op `664` zowel in je downloader als in \*Arr. In umask-notatie zou dat `002` zijn.

## Systeem en logs laden eindeloos

- Het is de easy-privacy blocklist. Ze blokkeren in feite elke URL met /api/log? erin. Bekijk de lijst en bepaal zelf of het blokkeren van alle URL's in die lijst een verstandig idee is, er zijn tientallen URL's in die lijst die mogelijk sites breken. Je hebt deze geselecteerd in je adblocker. De eenvoudige oplossing is om het domein waarop Radarr wordt uitgevoerd op de whitelist te zetten. Maar ik raad nog steeds aan om de lijst te controleren.

## Torrents uitpakken

- De meeste torrentclients hebben geen automatische verwerking van gecomprimeerde archieven zoals hun usenet-tegenhangers. We raden [unpackerr](https://github.com/unpackerr/unpackerr) aan.

## uTorrent werkt niet meer

- Zorg ervoor dat de web-UI is ingeschakeld
- Zorg ervoor dat de alternatieve luisterpoort voor de web-UI (Geavanceerd => Web-UI) niet hetzelfde is als de luisterpoort (Verbindingen)
- We raden aan de alternatieve luisterpoort voor de web-UI te wijzigen om geen problemen te veroorzaken met het doorsturen van poorten voor verbindingen.

## Ik kreeg een pop-up dat config.xml beschadigd is, wat nu?

- Radarr kon je configuratiebestand bij het opstarten niet lezen omdat het op de een of andere manier beschadigd is geraakt. Om weer online te gaan, moet je `.xml` verwijderen in je [appdata-directory](/radarr/appdata-directory), nadat je dit hebt verwijderd, start het op en het zal starten op de standaardpoort (7878), je moet nu alle instellingen opnieuw configureren die je hebt geconfigureerd op de pagina Algemene instellingen.

## Ongeldig certificaat en andere HTTPS- of SSL-problemen

- Je downloadclient werkt niet meer en je krijgt een foutmelding zoals `Localhost is een ongeldig certificaat`?
  - Radarr valideert SSL-certificaten. Als er geen SSL-certificaat is ingesteld in de downloadclient, of als je een zelfondertekend https-certificaat gebruikt zonder het CA-certificaat toe te voegen aan je lokale certificaatopslag, zal Radarr weigeren verbinding te maken. Gratis correct ondertekende certificaten zijn beschikbaar via [Let's Encrypt](https://letsencrypt.org/).
  - Als je downloadclient en je computer op dezelfde machine staan, is er geen reden om HTTPS te gebruiken. De eenvoudigste oplossing is om SSL uit te schakelen voor de verbinding. De meeste mensen zijn het erover eens dat dit ook niet nodig is in een lokaal netwerk. Het is mogelijk om certificaatvalidatie uit te schakelen in de geavanceerde instellingen als je een onveilige SSL-configuratie wilt behouden.

## VPN's, Jackett en de \*ARRs

- Tenzij je je in een onderdrukkend land bevindt zoals China, Australië of Zuid-Afrika, is je torrentclient meestal het enige dat achter een VPN moet staan. Omdat het VPN-eindpunt wordt gedeeld door veel gebruikers, kun je te maken krijgen met snelheidsbeperkingen, DDOS-bescherming en IP-blokkades van verschillende services die elke software gebruikt.
- Met andere woorden, het achter een VPN plaatsen van de \*ARRs (Lidarr, Prowlarr, Radarr, Readarr en Lidarr) kan ervoor zorgen dat de applicaties in sommige gevallen onbruikbaar zijn omdat de services niet toegankelijk zijn.

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

- Dit komt meestal doordat je op een andere manier zoekt in Jackett dan normaal. Raadpleeg ons [probleemoplossingsartikel](/radarr/troubleshooting) voor meer informatie.

## Hoe bepaalt Radarr het jaartal van een film?

- Radarr haalt metadata op van [TMDb](https://www.themoviedb.org/)
- Radarr gebruikt het jaartal van de oudste **theatervoorstelling** en de oudste **première** voor het matchen.
  - Let op: als er geen theatervoorstelling bestaat, zal de logica terugvallen op de oudste fysieke of digitale releasedatum.
- Als een film ontbreekt aan een digitale, fysieke, theatervoorstelling of première-datum, moet TMDb worden bijgewerkt.
- [De bijdragegids van TMDb](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013) vermeldt het volgende over hun releasedatatypes.
  - **Première** - Een premièrevertoning kan de vorm aannemen van een festivalvertoning (bijv. TIFF) of een première-evenement met de cast en crew in een grote stad (bijv. LA, Londen, Toronto).
  - **Theatervoorstelling** - Kan worden gebruikt voor de oorspronkelijke release en alle volgende officiële releases. Gebruikt voor brede of saturatie-releases. In de Verenigde Staten wordt 600-1.999 schermen beschouwd als een brede release en 2000+ als een saturatie-release.
  - **Theatervoorstelling (beperkt)** - Een beperkte theatervoorstelling is een distributiestrategie waarbij een nieuwe film in een paar theaters in een land wordt uitgebracht, meestal in grote steden. In de Verenigde Staten zijn er minder dan 600 theaters.
  - **Fysiek** - Omvat alle VHS-, DVD- en Blu-ray-releases.
  - **Digitaal** - Alle relevante releases kunnen worden toegevoegd, inclusief streamingplatforms, VOD-verhuur of -aankoop. Digitale vertoningen, inclusief online filmfestivals en virtuele bioscoopreleases, worden ook beschouwd als digitale releases.

## Hoe gaat Radarr om met buitenlandse films of buitenlandse titels?

> [TRaSH's Custom Format Language Guide](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) kan nuttig zijn om films in de gewenste taal(en) te krijgen.{.is-info}

> Vanaf 12 februari 2023 zal de metadatacache van Radarr de oorspronkelijke taal van een film beschouwen als de gesproken taal van TMDb als er slechts één gesproken taal bestaat voor de film op TMDb; anders wordt de oorspronkelijke TMDb-taal van de film gebruikt.
{.is-warning}

## Zoeken op ID

- **Indexers die zoeken op basis van ID ondersteunen** - Zoeken op indexers en trackers die zoeken op basis van ID (TMDbId, IMDbId, enz.) - zoals veel Usenet-indexers en veel privé-torrent-trackers - worden tekstzoekopdrachten niet gebruikt als er resultaten worden geretourneerd voor een zoekopdracht op basis van ID. Als er resultaten worden geretourneerd, wordt er niet teruggevallen op een naam/tekstzoekopdracht. Als je resultaten mist van je indexer, komt dit doordat de releases zijn gekoppeld aan het verkeerde film-ID.
  - De taal van de release kan ook worden afgeleid van de taal van de release van de indexer of tracker in het resultaat, indien opgegeven, in plaats van uit de naam te worden geanalyseerd.

## Tekstzoekopdrachten

- **Indexers die geen zoekopdrachten op basis van ID ondersteunen of waarvoor geen resultaten worden geretourneerd voor zoekopdrachten op basis van ID** - Zoeken op zal de oorspronkelijke titel van de film, de Engelse titel en de vertaalde titel gebruiken in de talen die je hebt ingesteld in het kwaliteitsprofiel van de film en eventuele aangepaste formaten met scores in het kwaliteitsprofiel groter dan nul.
- Bij het importeren wordt er gezocht naar een overeenkomst in alle vertalingen en alternatieve titels.
  - De taal van de release kan ook worden afgeleid van de taal van de release van de indexer of tracker in het resultaat, indien opgegeven, in plaats van uit de naam te worden geanalyseerd.

## Buitenlandse films krijgen

- Om een film in een vreemde taal te krijgen, stel je de taal van het kwaliteitsprofiel van je film in op Original (de oorspronkelijke taal van de film\*), een specifieke taal voor dat profiel, of `Any` en maak en scoor aangepaste formaten met taalvoorwaarden groter dan 0 om te bepalen welke taal je wilt hebben.
- Let op dat dit geen indexer-talen omvat die zijn geconfigureerd in de instellingen van de indexer als `multi`.
  - Let op dat vanaf [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c) van Radarr `multi` niet langer wordt verondersteld Engels te omvatten
  - Gebruikers kunnen hun instellingen per indexer aanpassen om aan te geven welke taal(talen) `multi` aangeeft

## Hoe gaat Radarr om met "multi" in namen?

- Met Radarr v4.1+ gaat Radarr ervan uit dat
`multi` alleen de taal van de film is en **NIET** Engels, zoals in eerdere versies.
  - Gebruikers kunnen hun instellingen per indexer aanpassen om aan te geven welke taal(talen) `multi` aangeeft
- Let op dat `multi`-definities alleen helpen bij het parsen van releases en niet bij buitenlandse titels of filmzoekopdrachten.

## Help, film toegevoegd, maar niet gezocht

- Radarr zoekt niet *actief* automatisch naar ontbrekende films. In plaats daarvan wordt periodiek een query uitgevoerd op nieuwe berichten naar alle indexers die zijn geconfigureerd voor RSS. Wanneer een gewenste film of een film waarvan de cutoff niet is gehaald in die lijst verschijnt, wordt deze gedownload. Dit betekent dat een film pas wordt gedownload wanneer deze wordt gepost (of opnieuw wordt gepost).
- Als je een film toevoegt die je nu wilt hebben, is de beste optie om het vakje "Start zoekopdracht naar ontbrekende film" aan te vinken, links van de knop *Film toevoegen* (**1**). Je kunt ook naar de pagina van een film gaan die je hebt toegevoegd en op het vergrootglas "Zoeken" (**2**) klikken of de Wanted-weergave gebruiken om te zoeken naar ontbrekende of niet-geknipte films.

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
- Bekijk [NZBHydra2](https://github.com/theotherp/nzbhydra2), dat indexers kan synchroniseren met \*Arr. Gebruik echter niet hun enkele aggregatie-eindpunt en gebruik `multi` als synchronisatie wordt gebruikt.

## Waarom zijn er twee bestanden? | Waarom blijft er een bestand achter in downloads?

Dit is normaal. Met een configuratie die [hardlinks](https://trash-guides.info/hardlinks) ondersteunt, wordt er geen dubbele ruimte gebruikt. Hieronder staat hoe het torrentproces werkt.

1. Radarr stuurt een downloadverzoek naar je client en koppelt het aan een label of categorienaam die je hebt geconfigureerd in de instellingen van de downloadclient. Voorbeelden: films, tv, series, muziek, enz.
1. Radarr houdt de actieve downloads van je downloadclient in de gaten die gebruikmaken van die categorienaam. Deze monitoring gebeurt via de API van je downloadclient.
1. Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat je het bestand kunt seeden (de verhouding of tijd kan worden aangepast in de downloadclient of vanuit Radarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar je mediamap, wordt het bestand gekoppeld (hardlink) als dit wordt ondersteund door je configuratie, anders wordt het gekopieerd als hardlinks niet worden ondersteund.
1. Als de optie "Voltooide downloadverwerking - Voltooide verwijderen" is ingeschakeld in de instellingen van Radarr, zal Radarr het oorspronkelijke bestand en de torrent verwijderen uit je downloadclient, maar alleen als de downloadclient meldt dat het seeden is voltooid en de torrent is gestopt (bijvoorbeeld gepauzeerd). Zie [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) voor hoe je je downloadclient optimaal kunt configureren.

> Hardlinks zijn standaard ingeschakeld. [Een hardlink gebruikt geen extra schijfruimte.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor je voltooide downloadmap en je mediamap. Als het maken van een hardlink mislukt of je configuratie geen hardlinks ondersteunt, wordt er overgeschakeld naar kopiëren van het bestand.
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