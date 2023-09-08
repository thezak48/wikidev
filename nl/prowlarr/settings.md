# Prowlarr-instellingen

Deze pagina gaat door alle beschikbare instellingen in Prowlarr en hoe ze werken. Dit is niet bedoeld als een uitgebreide "hoe Prowlarr in te stellen". Als je dat wilt, gebruik dan in plaats daarvan de [Snelstartgids](/prowlarr/quick-start-guide) pagina.

# Menu-opties

Om naar de instellingenpagina te gaan, kies je Instellingen in het linker menu. De volgende submenu-opties zijn beschikbaar:

![settings_1_menu.png](/assets/prowlarr/settings_1_menu.png)

Merk ook op dat voor elke individuele instellingenpagina enkele opties bovenaan het menu staan:

![settings_2_topmenu.png](/assets/prowlarr/settings_2_topmenu.png)

- Verbergen/tonen van geavanceerde opties is belangrijk voor items die hieronder zijn gemarkeerd als `(Geavanceerde optie)`, anders worden ze niet weergegeven. Deze menu-items worden weergegeven in het oranje op de schermafbeeldingen.

- Je moet je wijzigingen opslaan voordat je het scherm verlaat. Dit doe je door op het schijf-icoon te klikken. Als je geen wijzigingen hebt aangebracht, wordt "Geen wijzigingen" weergegeven en is het grijs, zoals hierboven getoond.

# Indexer-proxies

> Informatie over ondersteunde proxytypen is te vinden op de [Meer informatie (Ondersteund)](/prowlarr/supported#indexer-proxies) pagina voor dit gedeelte
{.is-info}

Hier kun je proxies of Flaresolverr-configuraties toevoegen voor indexers die deze vereisen.

Ga naar `Instellingen` => `Indexer-proxies` en klik vervolgens op het <kb>+</kb> om een proxy toe te voegen.

![proxies.png](/assets/prowlarr/proxies.png)

## Proxy-instellingen

- Naam - Naam van de proxy in Prowlarr
- Tags - De tags voor deze proxy. Proxies zijn van toepassing op alle overeenkomende (dezelfde tag) indexers. Als dit leeg is, is deze proxy van toepassing op alle indexers.

## FlareSolverr-proxy-instellingen

- Host - het volledige hostpad (inclusief http en poort) naar je FlareSolverr-instantie
- (Geavanceerde instelling) Time-out voor aanvraag (seconden) - de [FlareSolver Request `maxTimeout` waarde](https://github.com/FlareSolverr/FlareSolverr#-requestget) die Prowlarr moet gebruiken voor FlareSolverr-aanvragen. Moet tussen `1` seconde en `180` seconden zijn (standaard: `60` seconden)

> \* Een FlareSolverr-proxy wordt alleen gebruikt voor aanvragen als en alleen als Cloudflare wordt gedetecteerd door Prowlarr
> \* Een FlareSolverr-proxy wordt alleen gebruikt voor aanvragen als en alleen als de proxy en de indexer overeenkomende tags hebben
> \* **Een Flaresolverr-proxy geconfigureerd zonder tags of zonder indexers met overeenkomende tags wordt uitgeschakeld.**
{.is-info}

## HTTP-proxy-instellingen

- Host - het hostadres van je proxy
- Poort - de poort van je proxy
- Gebruikersnaam - de gebruikersnaam van je proxy
- Wachtwoord - het wachtwoord van je proxy

## Socks4-proxy-instellingen

- Host - het hostadres van je proxy
- Poort - de poort van je proxy
- Gebruikersnaam - de gebruikersnaam van je proxy
- Wachtwoord - het wachtwoord van je proxy

## Socks5-proxy-instellingen

- Host - het hostadres van je proxy
- Poort - de poort van je proxy
- Gebruikersnaam - de gebruikersnaam van je proxy
- Wachtwoord - het wachtwoord van je proxy

# Applicaties

> Informatie over ondersteunde applicaties is te vinden op de [Meer informatie (Ondersteund)](/prowlarr/supported#applications) pagina voor dit gedeelte
{.is-info}

Hier voeg je de applicaties toe die Prowlarr gebruikt (Radarr, Sonarr, Lidarr, Readarr, enz.) en hoe ze gesynchroniseerd blijven met Prowlarr.

- Klik op `Instellingen` => `Apps` en klik vervolgens op het <kb>+</kb> om een app toe te voegen.
- Sync App Indexers - Start een synchronisatie van alle indexers naar alle applicaties
- Test All Apps - Start een test van alle applicaties

![addapps.png](/assets/prowlarr/addapps.png)

Alle programma's die je kunt toevoegen, worden vermeld. Je moet alleen programma's toevoegen die je momenteel hebt geïnstalleerd, en als je er meerdere exemplaren van hebt, moet je ze afzonderlijk toevoegen.

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Opmerking: Indexers worden gesynchroniseerd op basis van de mogelijkheden/categorieën die ze beweren te ondersteunen. Als een indexer alleen `tv`-categorieën ondersteunt, wordt deze niet gesynchroniseerd met Lidarr, Radarr en Readarr. Het wordt alleen gesynchroniseerd met Sonarr. "Ondersteunde" categorieën kunnen worden geselecteerd als een geavanceerde instelling op basis van de app. **Merk ook op dat de \*Arrs alleen indexers accepteren waarvan de testquery's resultaten retourneren die ten minste een van de geconfigureerde categorieën bevatten.**
{.is-info}

## Applicatie-instellingen

- Naam - Voer een naam in voor deze app.
- Synchronisatieniveau - Selecteer het synchronisatieniveau dat moet worden gebruikt
  - `Alleen toevoegen en verwijderen` - Wanneer indexers worden toegevoegd of verwijderd uit Prowlarr, wordt dit bijgewerkt in deze externe app. Als de indexer op het moment van synchronisatie niet beschikbaar is, wordt deze uitgeschakeld in de externe app.
  - `Volledige synchronisatie` - Volledige synchronisatie houdt de indexers van deze app volledig in sync. Wijzigingen die in Prowlarr worden aangebracht aan indexers worden gesynchroniseerd met deze app. Elke wijziging die in de instellingen op de FAQ voor deze indexers op afstand binnen deze app wordt aangebracht, wordt overschreven door Prowlarr bij de volgende synchronisatie. Een lijst met factoren die worden gebruikt om te bepalen of een synchronisatie moet plaatsvinden, is te vinden in de [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Uitgeschakeld` - voorkomt dat indexers worden gesynchroniseerd met het programma.

> `Volledige synchronisatie` betekent dat Prowlarr de meeste instellingen overschrijft, inclusief door de gebruiker geselecteerde categorieën die configureerbaar zijn in Prowlarr. Niet door Prowlarr beheerde instellingen worden echter niet aangeraakt. Echter, [bijna elke andere verandering](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) zal een synchronisatie activeren en de overeenkomstige instellingen in \*Arr overschrijven.
{.is-warning}

- Tags - Als je een tag aan je indexer hebt toegevoegd tijdens de installatie, worden alleen indexers met deze tag gebruikt voor deze programma-invoer.
- Prowlarr-server - Voer hier de URL van de Prowlarr-server in (inclusief http, poort en baseurl indien nodig) zoals de app er toegang toe zou hebben.

> Houd er rekening mee dat als je een omgekeerde proxy gebruikt, je de URL-basis hieraan moet toevoegen! Als je dit niet doet, worden de indexers verbroken wanneer ze worden gesynchroniseerd, en als je Alleen toevoegen en verwijderen hebt geselecteerd, wordt dit niet gerepareerd wanneer je het bewerkt!{.is-info}

- Applicatieserver - Voer hier de URL van de app-server in (inclusief http, poort en baseurl indien nodig) van je programma. Voer indien nodig de volledige URL-basis in.
- API-sleutel - Voer hier de API-sleutel van je programma in. Voor \*Arrs is deze te vinden in Instellingen => Algemeen. Je kunt deze krijgen van je programma in het tabblad `Instellingen` => `Algemeen` en hier kopiëren/plakken.
- (Geavanceerde instelling) Synchroniseer categorieën - Selecteer de categorieën die moeten worden gesynchroniseerd met deze app. Indexers die deze categorieën ondersteunen, worden gesynchroniseerd.
  - Indexer-aangepaste categorieën worden toegewezen aan de standaard Torznab/Newznab-categorieën, zodat zoeken naar de gestandaardiseerde categorieën alle onderliggende aangepaste categorieën omvat. Indexer-aangepaste categorieën worden vermeld voor fijnafstemming als je ze niet allemaal tegelijk wilt hebben.

## Test de applicatie

Test je invoer. Als er een groen vinkje verschijnt, kun je je invoer opslaan en herhalen indien nodig voor elk programma dat je wilt synchroniseren met Prowlarr. Als het mislukt, moet je je logboek controleren op de fout (URL, API-sleutel, enz.).

## Synchronisatieprofielen

Configureer de synchronisatieprofielen voor (een) applicatie(s)

> Je kunt verschillende instellingen per app hebben door meerdere exemplaren van de indexer te maken
{.is-info}

- Naam - Unieke naam van het synchronisatieprofiel
- RSS inschakelen - Voor indexers met dit profiel, RSS-zoekopdrachten inschakelen voor de \*Arr-app
- Interactief zoeken inschakelen - Voor indexers met dit profiel, interactieve (handmatige) zoekopdrachten inschakelen voor de \*Arr-app
- Automatisch zoeken inschakelen - Voor indexers met dit profiel, automatische zoekopdrachten inschakelen voor de \*Arr-app
- Minimum Seeders - Voor indexers met dit profiel, het minimum aantal seeders dat vereist is voor \*Arr om een torrent te downloaden

# Downloadclients (Prowlarr-zoekopdrachten)

{#download-clients}

> Informatie over ondersteunde downloadclients is te vinden op de [Meer informatie (Ondersteund)](/prowlarr/supported#download-clients) pagina voor dit gedeelte
{.is-info}

Als je van plan bent om rechtstreeks in Prowlarr te zoeken, moet je Downloadclients toevoegen. Anders hoef je ze hier niet toe te voegen. Voor zoekopdrachten vanuit je apps worden de daar geconfigureerde downloadclients gebruikt.

> Prowlarr synchroniseert geen downloadclients met de applicaties.
{.is-info}

Klik op `Instellingen` => `Downloadclients` en klik vervolgens op het <kb>+</kb> om een nieuwe downloadclient toe te voegen. Je downloadclient moet al zijn geconfigureerd volgens deze handleiding.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

Selecteer de downloadclient die je wilt toevoegen en er verschijnt een pop-upvenster om de verbindingsgegevens in te voeren. Deze gegevens zijn vergelijkbaar voor de meeste clients. Sommige vragen om een gebruikersnaam of wachtwoord, sommige vragen of nieuwe downloads in een gepauzeerde/startstatus moeten worden toegevoegd, enz.

> Clientprioriteit is alleen van belang wanneer er 2 van hetzelfde type (usenet of torrent) zijn toegevoegd. 1 is de hoogste prioriteit en als er meerdere clients van hetzelfde type zijn en dezelfde prioriteit hebben, zal Prowlarr er tussen wisselen.
{.is-info}

## Usenet-clientinstellingen

- Naam - De naam van de downloadclient in Prowlarr
- Inschakelen - Deze downloadclient inschakelen
- Host - De URL van je downloadclient
- Poort - De poort van je downloadclient
- SSL gebruiken - Een beveiligde verbinding gebruiken met je downloadclient. Let op deze veelvoorkomende fout.
- URL-basis - Voeg een voorvoegsel toe aan de URL; dit is vaak nodig voor omgekeerde proxies.
- API-sleutel - de API-sleutel om je client te authenticeren
- Gebruikersnaam - de gebruikersnaam om je client te authenticeren (meestal niet nodig)
- Wachtwoord - het wachtwoord om je client te authenticeren (meestal niet nodig)
- Categorie - de categorie binnen je downloadclient die Prowlarr zal gebruiken
- Prioriteit - downloadclientprioriteit voor toegevoegde items
- Clientprioriteit - Prioriteit van de downloadclient binnen Prowlarr. Round-Robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) die dezelfde prioriteit hebben.

## Torrent-clientinstellingen

- Naam - De naam van de downloadclient in Prowlarr
- Inschakelen - Deze downloadclient inschakelen
- Host - De URL van je downloadclient
- Poort - De poort van je downloadclient; dit is meestal de webgui-poort
- SSL gebruiken - Een beveiligde verbinding gebruiken met je downloadclient. Let op deze veelvoorkomende fout.
- URL-basis - Voeg een voorvoegsel toe aan de URL; dit is vaak nodig voor omgekeerde proxies.
- Gebruikersnaam - de gebruikersnaam om je client te authenticeren
- Wachtwoord - het wachtwoord om je client te authenticeren
- Categorie - de categorie binnen je downloadclient die Prowlarr zal gebruiken
- Prioriteit - downloadclientprioriteit voor toegevoegde items
- Initiële status - Initiële status voor torrents (alleen Qbittorrent: Gedwongen omzeilt alle seeddrempels)
- Clientprioriteit - Prioriteit van de downloadclient binnen Prowlarr. Round-Robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) die dezelfde prioriteit hebben.

## Test de downloadclient

Test je invoer. Als er een groen vinkje verschijnt, kun je je invoer opslaan en herhalen indien nodig voor elke downloadclient die je wilt gebruiken in Prowlarr. Als het mislukt, moet je je logboek controleren op de fout (verbinding, referenties, enz.).

# Meldingen

> Informatie over ondersteunde meldingsproviders is te vinden op de [Meer informatie (Ondersteund)](/prowlarr/supported#notifications) pagina voor dit gedeelte
{.is-info}

## Verbindingen

Verbindingen bepalen hoe Prowlarr met de buitenwereld communiceert.

- Door op de <kb>+</kb>-knop te drukken, wordt een nieuw venster geopend waarin je veel verschillende eindpunten kunt configureren.

- Een lijst met ondersteunde meldingen en verbindingen is te vinden op de [Meer informatie (Ondersteund)](/prowlarr/supported#notifications) pagina.

## Meldingstriggers

- Bij vrijgave vastleggen - Word op de hoogte gesteld van vrijgavevastleggingen vanuit Prowlarr of via de API
  - Handmatige vastleggingen opnemen - Word op de hoogte gesteld van handmatige vastleggingen die binnen de Prowlarr-UI zijn geactiveerd
- Bij gezondheidsprobleem - Word op de hoogte gesteld van mislukte gezondheidscontroles
  - Gezondheidswaarschuwingen opnemen - Word op de hoogte gesteld van gezondheidswaarschuwingen naast fouten.
- Bij applicatie-update - Word op de hoogte gesteld wanneer Prowlarr wordt bijgewerkt naar een nieuwe versie

# Tags

- Het tag-gedeelte in Prowlarr wordt gebruikt om verschillende aspecten van Prowlarr te koppelen.
- Tags zijn met name handig voor:
  - Het inschakelen van Flaresolverr-proxy voor gebruik met een indexer; Let op: Flaresolverr-proxies zijn uitgeschakeld zonder een tag
  - Het inschakelen van een HTTP- of SOCKS-proxy voor gebruik met een indexer
  - Het specificeren van indexers voor bepaalde apps

# Algemeen

Hier kun je algemene applicatie-instellingen wijzigen, zoals poort en logniveau.

Klik op `Instellingen` => `Algemeen`.

> Veel van de opties hier zijn alleen zichtbaar door op "Geavanceerd weergeven" te klikken bovenaan het scherm. Menu-items in het oranje worden alleen weergegeven wanneer geavanceerd weergeven is ingeschakeld.
{.is-info}

## Host

![general_host.png](/assets/prowlarr/general_host.png)

- (Geavanceerde optie) Bindadres - Laat dit als `*` staan tenzij je het moet wijzigen. Het IPv4-adres/host op het systeem waarop Prowlarr luistert. (standaard: `*`)
  - Let op dat `*` elk/adres is
- Poortnummer - de poort waarop Prowlarr wordt uitgevoerd. Het moet uniek zijn. (standaard: 9696)
- URL-basis - Voer hier een URL-basis in als je een omgekeerde proxy gebruikt. (herstart vereist) (standaard: leeg)
- (Geavanceerde optie) Instantienaam - Naam om te gebruiken voor browser-tabblad en SysLog (indien ingeschakeld) (herstart vereist) (standaard: Prowlarr)
- (Geavanceerde optie) SSL gebruiken - Vink dit vakje aan als je een https-adres gebruikt om verbinding te maken met Prowlarr. Als je `localhost` of een IP-adres gebruikt, moet dit bijna NOOIT worden aangevinkt. (standaard: false)
- Browser starten (alleen Windows) - Vink dit vakje aan als je wilt dat er een browser-venster wordt geopend wanneer Prowlarr start. (standaard: ja)

## Beveiliging

![general_security.png](/assets/prowlarr/general_security.png)

- Authenticatie - Hoe wilt u zich authenticeren om toegang te krijgen tot uw Prowlarr-instantie
  - Geen - U heeft geen authenticatie nodig om toegang te krijgen tot uw Prowlarr. Dit is meestal het geval als u de enige gebruiker van uw netwerk bent, niemand op uw netwerk heeft toegang tot uw Radarr nodig of uw Radarr is niet blootgesteld aan het web.
  - Basis (Browser pop-up) - Deze optie toont een klein pop-upvenster wanneer u toegang krijgt tot uw Prowlarr, waarin u een gebruikersnaam en wachtwoord kunt invoeren.
  - Formulieren (Aanmeldingspagina) - Deze optie heeft een vertrouwd uitziend aanmeldingsscherm, vergelijkbaar met andere websites, waarmee u kunt inloggen op uw Prowlarr.
- API-sleutel - De API-sleutel wordt gebruikt door externe apps die toegang hebben tot Prowlarr. Dit is geheim en mag niet worden gedeeld met anderen. Als het wordt gedeeld, moet u het opnieuw genereren en uw apps bijwerken.
- Certificaatvalidatie - Wijzig hoe strikt de validatie van HTTPS-certificaten is
  - Ingeschakeld - Valideer alle HTTPS-certificaten (aanbevolen)
  - Uitgeschakeld voor lokale adressen - Valideer alle HTTPS-certificaten behalve die op localhost en het LAN
  - Uitgeschakeld - Valideer geen enkel HTTPS-certificaat

## Proxy

![general_proxy.png](/assets/prowlarr/general_proxy.png)

Proxy - Met deze optie kunt u de informatie die uw Prowlarr ophaalt en doorzoekt via een proxy laten lopen. Dit kan handig zijn als u zich in een land bevindt waar het downloaden van torrentbestanden niet is toegestaan.

- Proxy gebruiken - Inschakelen om een proxy te gebruiken
- Proxytype - Selecteer uw proxytype (HTTPS, Socks4 of Socks5)
- Hostnaam - Voer de hostnaam van uw proxy in (inclusief http/https of een ander protocol)
- Poort - Voer de poort van uw proxy in
- Gebruikersnaam - Voer uw proxygebruikersnaam in, indien van toepassing
- Wachtwoord - Voer uw proxys wachtwoord in, indien van toepassing
- Genegeerde adressen - Voer een lijst met adressen gescheiden door komma's in die de proxy moeten omzeilen
- Proxy omzeilen voor lokale adressen - Vink het vakje aan om de proxy voor lokale adressen over te slaan.

## Logging

![general_logging.png](/assets/prowlarr/general_logging.png)

Het standaard logniveau is `Info`. Dit is zeer eenvoudige logging. U kunt het hier wijzigen voor meer gedetailleerde logging. Logbestanden worden geroteerd, dus er is geen gevaar dat er te veel ruimte wordt ingenomen.

- Logniveau - Waarschijnlijk een van de meest nuttige probleemoplossingstools
  - Info - Dit is de meest basale manier waarop Prowlarr informatie verzamelt. Dit bevat een zeer minimale hoeveelheid informatie in de logs. Dit logbestand bevat fatale, fout-, waarschuwings- en infovermeldingen.
  - Debug - Debug bevat alle informatie die Info bevat, plus meer informatie die nuttig kan zijn. Dit logbestand bevat fatale, fout-, waarschuwings-, info- en debugvermeldingen.
  - Trace - De meest geavanceerde en gedetailleerde logging op Prowlarr, Trace bevat alle informatie die is verzameld door Info en Debug en meer. Dit is het meest voorkomende type log dat wordt gevraagd bij het oplossen van problemen op Discord of Reddit. Als u hulp nodig heeft, selecteer dan uw logboek op Trace en herhaal de taak die u problemen gaf om het logboek vast te leggen. Dit logbestand bevat fatale, fout-, waarschuwings-, info-, debug- en tracevermeldingen.

## Analytics

![general_analytics.png](/assets/prowlarr/general_analytics.png)

- Analytics - Stuur anonieme gebruiks- en foutinformatie naar de servers van Prowlarr (Servarr). Dit omvat informatie over uw browser, welke Prowlarr WebUI-pagina's u gebruikt, foutenrapportage, evenals informatie over het besturingssysteem, runtime-versie en gerelateerde informatie. We zullen deze informatie gebruiken om functies en bugfixes te prioriteren.

## Updates

![general_updates.png](/assets/prowlarr/general_updates.png)

- (Geavanceerde optie) Branch - Dit is de branch van Prowlarr die u gebruikt.
  - [Zie deze FAQ voor meer informatie](/prowlarr/faq#how-do-i-update-prowlarr)
- Automatisch - Updates automatisch downloaden en installeren. U kunt nog steeds installeren via Systeem: Updates. Opmerking: Windows-gebruikers worden altijd automatisch bijgewerkt.
- Mechanisme - Gebruik de ingebouwde updater van Prowlarr of een script
  - Ingebouwd - Gebruik de eigen updater van Prowlarr
  - Script - Laat Prowlarr het update-script uitvoeren
  - Docker - Werk Prowlarr niet bij vanuit de Docker, maar haal een gloednieuwe image op met de nieuwe update
- Script - Alleen zichtbaar wanneer Mechanisme is ingesteld op Script - Pad naar update-script
- Updateproces - Prowlarr zal het updatebestand downloaden, de integriteit ervan controleren en het naar een tijdelijke locatie extraheren en de gekozen methode aanroepen. Het updateproces wordt uitgevoerd onder dezelfde gebruiker als waar Prowlarr onder wordt uitgevoerd, het heeft toestemming nodig om de Prowlarr-bestanden bij te werken en Prowlarr te stoppen/starten.
- Ingebouwd - De ingebouwde methode zal Prowlarr-bestanden en -instellingen back-uppen, Prowlarr stoppen, de installatie bijwerken en Prowlarr starten. Als uw systeem het stoppen van Prowlarr niet aankan en automatisch probeert te herstarten, is het misschien beter om in plaats daarvan een script te gebruiken. Bij een mislukking wordt de vorige versie van Prowlarr opnieuw gestart.
- Script - Het script moet hetzelfde behandelen als de ingebouwde updater. Als u services wilt stoppen en starten (upstart/launchd/etc), moet u dat hier doen.

## Back-ups

![general_backups.png](/assets/prowlarr/general_backups.png)

- (Geavanceerde optie) Map - Hiermee kunt u de back-uplocatie selecteren. In Docker bent u beperkt tot wat de container kan zien. Padnamen zijn relatief ten opzichte van de appdata-map; indien nodig kunt u een absoluut pad instellen om buiten de appdata-map een back-up te maken.
- (Geavanceerde optie) Interval - Hoe vaak wilt u dat Prowlarr een back-up maakt
- (Geavanceerde optie) Retentie - Hoe lang wilt u dat Prowlarr elke back-up bewaart. Nadat er een nieuwe back-up is gemaakt, wordt de oudste back-up verwijderd.

> Handmatige back-ups worden voor altijd bewaard, opgeslagen in dezelfde map en hebben een andere naam.
{.is-info}

# UI

## Datums

- Korte datumnotatie - Hoe wilt u dat Prowlarr korte datums weergeeft?
- Lange datumnotatie - Hoe wilt u dat Prowlarr lange datums weergeeft?
- Tijdnotatie - Wilt u een 12-uurs of 24-uurs notatie?
- Relatieve datums weergeven - Wilt u dat Prowlarr relatieve (Vandaag/Gisteren/etc) of absolute datums weergeeft?

## Stijl

- Thema - Selecteer het kleurenthema dat Prowlarr moet gebruiken, geïnspireerd door [Theme.Park](https://github.com/GilbN/theme.park)
- Kleurenblindmodus inschakelen - Gewijzigde stijl om kleurenblinde gebruikers in staat te stellen kleurgecodeerde informatie beter te onderscheiden

## Taal

- UI-taal - Selecteer de taal die Prowlarr moet gebruiken in de applicatie-UI