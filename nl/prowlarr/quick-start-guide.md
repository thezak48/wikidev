---
title: Prowlarr Snelstartgids
description: 
published: true
date: 2023-04-06T16:04:33.682Z
tags: 
editor: markdown
dateCreated: 2023-04-06T16:04:33.682Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Indexers](#indexers)
- [Apps](#apps)
  - [App-instellingen](#app-instellingen)
- [Downloadclients](#downloadclients)
  - [Usenet-clientinstellingen](#usenet-clientinstellingen)
  - [Torrent-clientinstellingen](#torrent-clientinstellingen)
  - [Testen van de downloadclient](#testen-van-de-downloadclient)
- [Installatie voltooid](#installatie-voltooid)

> Deze pagina is nog in ontwikkeling en niet compleet.

> Voor een gedetailleerdere uitleg van alle instellingen, bekijk [Prowlarr => Instellingen](/prowlarr/settings)

In deze handleiding proberen we de basisconfiguratie uit te leggen die je moet doen om aan de slag te gaan met Prowlarr. We zullen enkele opties overslaan die je op het scherm kunt zien. Als je dieper op deze opties wilt ingaan, raadpleeg dan de juiste pagina in de FAQ en documentatie voor een volledige uitleg.

> Houd er rekening mee dat geavanceerde opties binnen de schermafbeeldingen en GUI-instellingen in `oranje` zijn, dus je moet op `Toon geavanceerd` bovenaan de pagina klikken om ze zichtbaar te maken.

# Indexers

Het eerste wat je moet instellen in Prowlarr zijn indexers. Je voegt elke indexer afzonderlijk toe aan Prowlarr.

Klik op `Indexers` en klik vervolgens op het + -teken om een nieuwe indexer toe te voegen.

![addindexer.png](/assets/prowlarr/addindexer.png)

Alle indexers die je kunt toevoegen (usenet en torrent) worden vermeld en je kunt typen om gedeeltelijk overeen te komen met een bestaande invoer. Als de indexer die je wilt toevoegen niet in de lijst staat, kun je "Generic Newznab" (voor usenet) of "Generic Torznab" (voor torrents) toevoegen.

![addgeneric.png](/assets/prowlarr/addgeneric.png)

Sommige indexers hebben speciale instellingen, maar de meeste zijn standaard zoals getoond.

![addnewindexer.png](/assets/prowlarr/addnewindexer.png)

- Naam - Selecteer een naam voor deze indexer. Wanneer deze wordt gesynchroniseerd met je apps, wordt er `(Prowlarr)` achter geplaatst.
- Inschakelen - Vink het vakje aan om deze indexer in te schakelen.
- Doorsturen - Vink het vakje aan als er een doorsturing nodig is. Er zijn slechts een paar indexers waar dit nodig is om te voorkomen dat je wordt verbannen. Als dit is ingeschakeld, wordt de downloadlink rechtstreeks naar de applicatie doorgestuurd in plaats van via Prowlarr te worden geproxyd.

> Doorsturen is meestal alleen nodig voor een handvol zeer specifieke indexers.

- Synchronisatieprofiel - Selecteer hier je synchronisatieprofiel. Deze kunnen worden aangemaakt in [`Instellingen` => `Apps`](/prowlarr/settings#applications). Het standaardprofiel, "Standard", bestaat al en ziet er zo uit:

> Je kunt verschillende instellingen per app hebben door meerdere instanties van de indexer te maken.

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Selecteer de URL die Prowlarr moet gebruiken. Als dit leeg is, wordt de standaard/eerste URL gebruikt.
- Downloadlink - Als je een torrent-indexer toevoegt, moet je mogelijk kiezen welk soort downloadlink je wilt gebruiken.
- (Geavanceerde optie) API-pad - Pad naar de API van de indexer. Meestal `/api`
- Referenties - Veel indexers en trackers vereisen dat je op de een of andere manier inlogt of authenticatie verleent. Je moet mogelijk een API-sleutel, RSS-sleutel, een sessie-id, een cookie of andere referenties van je indexer invoeren (meestal te vinden op je profielpagina of onder Beveiliging), zoekvolgordes selecteren of andere opties voor je specifieke indexer.
  - API-sleutel
  - RSS-sleutel
  - Sessie-ID
  - Cookie
  - Gebruikersnaam/wachtwoord
  - enz.
- (Geavanceerde optie) Extra parameters - Extra parameters om toe te voegen aan de verzoeken voor deze indexer.
- VIP-verloopdatum - Voer de datum in ISO-indeling (jjjj-MM-dd) in om 1 week voor het verlopen een melding te ontvangen; laat anders leeg
- Tags - Gebruik tags om standaard downloadclients op te geven, indexer-proxies op te geven, indexers aan applicaties toe te wijzen of gewoon om je indexers te organiseren.
- (Geavanceerde optie) Querylimiet - Als je indexer je API-aanroepen per dag beperkt, kun je hier dat aantal invoeren om te voorkomen dat je de limiet overschrijdt.
- (Geavanceerde optie) Grablimiet - Als je indexer je Grabs per dag beperkt, kun je hier dat aantal invoeren om te voorkomen dat je de limiet overschrijdt. Zodra de grablimiet is bereikt, veroorzaken verdere zoekopdrachten een onverwerkte uitzondering in \*Arr-apps. Andere apps kunnen anders reageren.
- (Geavanceerde optie) Seed-verhouding - Alleen voor torrent-indexers: de verhouding die een torrent moet bereiken voordat deze wordt gestopt, leeg is de standaardwaarde van de app
- (Geavanceerde optie) Seedtijd - Alleen voor torrent-indexers: de tijd dat een torrent moet worden gezaaid voordat deze wordt gestopt, leeg is de standaardwaarde van de app
- (Geavanceerde optie) Indexerprioriteit - Selecteer hier de indexerprioriteit van 1-50 (1 is het hoogst). Deze prioriteiten worden gesynchroniseerd met je apps.

Test je invoer. Als er een groen vinkje verschijnt, kun je je invoer opslaan en herhalen indien nodig voor elke indexer die je wilt gebruiken met Prowlarr. Als het mislukt, moet je je logboek controleren op de fout (URL, API-sleutel, enz.).

# Apps

Nadat je je indexers hebt toegevoegd, verbinden we Prowlarr met je andere apps.

Klik op `Instellingen` => `Apps` en klik vervolgens op het + -teken om een ondersteunde app toe te voegen.

![addapps.png](/assets/prowlarr/addapps.png)

Alle programma's die je kunt toevoegen, worden vermeld. Je moet alleen programma's toevoegen die je momenteel hebt geïnstalleerd, en als je er meerdere exemplaren van hebt, moet je ze afzonderlijk toevoegen.

> Momenteel ondersteunde apps vind je op de [Meer informatie (Ondersteund)](/prowlarr/supported#applications) pagina voor dit gedeelte

Bij het toevoegen van een app moet je waarden invoeren in het pop-upscherm:

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Opmerking: Indexers worden gesynchroniseerd op basis van de mogelijkheden/categorieën die ze beweren te ondersteunen. Als een indexer alleen `tv`-categorieën ondersteunt, wordt deze niet gesynchroniseerd met Lidarr, Radarr en Readarr. Het wordt alleen gesynchroniseerd met Sonarr. "Ondersteunde" categorieën kunnen worden geselecteerd als een geavanceerde instelling op app-basis. **Let ook op dat de \*Arrs alleen indexers accepteren waarvan de testquery's resultaten retourneren die ten minste een van de geconfigureerde categorieën bevatten.**

## App-instellingen

- Naam - Voer een naam in voor deze app.
- Synchronisatieniveau - Selecteer het synchronisatieniveau dat moet worden gebruikt
  - `Alleen toevoegen en verwijderen` - Wanneer indexers aan Prowlarr worden toegevoegd of verwijderd, wordt dit bijgewerkt in deze externe app. Als de indexer op het moment van synchronisatie niet beschikbaar is, wordt deze uitgeschakeld in de externe app.
  - `Volledige synchronisatie` - Volledige synchronisatie houdt de indexers van deze app volledig in sync. Wijzigingen die in Prowlarr worden aangebracht aan indexers worden vervolgens gesynchroniseerd met deze app. Elke wijziging die in de instellingen op de FAQ voor deze indexers op afstand binnen deze app wordt aangebracht, wordt overschreven door Prowlarr bij de volgende synchronisatie. Een lijst met factoren die worden gebruikt om te bepalen of een synchronisatie moet plaatsvinden, vind je in de [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Uitgeschakeld` - voorkomt dat indexers worden gesynchroniseerd met het programma.

> `Volledige synchronisatie` betekent dat Prowlarr de meeste instellingen overschrijft, inclusief door de gebruiker geselecteerde categorieën die configureerbaar zijn in Prowlarr. Niet door Prowlarr beheerde instellingen worden echter niet gewijzigd. Echter, [bijna elke andere wijziging](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) zal een synchronisatie activeren en de overeenkomstige instellingen in \*Arr overschrijven.
{.is-warning}

- Tags - Als je een tag hebt toegevoegd aan je indexer tijdens de installatie, worden alleen indexers met deze tag gebruikt voor deze programma-invoer.
- Prowlarr-server - Voer hier de URL van de Prowlarr-server in (inclusief http, poort en baseurl indien nodig) zoals de app er toegang toe zou hebben.

> Houd er rekening mee dat als je een omgekeerde proxy gebruikt, je de URL-basis hieraan moet toevoegen! Als je dit niet doet, worden de indexers verbroken wanneer ze worden gesynchroniseerd en als je Alleen toevoegen en verwijderen hebt geselecteerd, wordt dit niet hersteld wanneer je het bewerkt!

- App-server - Voer hier de URL van de app-server in (inclusief http, poort en baseurl indien nodig). Voer indien nodig de volledige URL-basis in.
- API-sleutel - Voer hier de API-sleutel van je programma in. Voor \*Arrs kun je deze vinden in Instellingen => Algemeen. Je kunt deze verkrijgen van je programma in het tabblad `Instellingen` => `Algemeen` en hier kopiëren/plakken.
- (Geavanceerde instelling) Synchronisatiecategorieën - Selecteer de categorieën die moeten worden gesynchroniseerd met deze app. Indexers die deze categorieën ondersteunen, worden gesynchroniseerd.
  - Indexer-aangepaste categorieën worden toegewezen aan de standaard Torznab/Newznab-categorieën, dus zoeken naar de gestandaardiseerde categorieën omvat alle onderliggende aangepaste categorieën. Indexer-aangepaste categorieën worden vermeld voor fijnafstemming als je ze niet allemaal tegelijk wilt hebben.

> Wanneer je dit opslaat, worden je indexers gesynchroniseerd met de app. Ze worden allemaal toegevoegd met de naam die je hebt gekozen voor je indexer plus (Prowlarr) erachter. bijv. `{Indexernaam} (Prowlarr)`

![nzbgeek.png](/assets/prowlarr/nzbgeek.png)

Ga vervolgens naar je programma en schakel de niet-Prowlarr-versie van de indexer uit. Zodra alles soepel verloopt, kun je die invoeren verwijderen en alleen de (Prowlarr)-versies behouden.

Je kunt de categorieën voor de Prowlarr-indexers controleren in je programma's. Standaardcategorieën die worden toegewezen aan de app kunnen worden geconfigureerd als een geavanceerde instelling voor de app in Prowlarr.

> **Houd er rekening mee dat aangepaste/niet-standaard indexer-specifieke categorieën worden toegewezen aan standaardcategorieën, dus zoeken naar standaardcategorieën omvat alle aangepaste categorieën**

## Synchronisatieprofielen

Configureer de synchronisatieprofielen voor (een) app(s)

- Naam - Unieke naam van het synchronisatieprofiel
- RSS inschakelen - Voor indexers met dit profiel, RSS-zoekopdrachten inschakelen voor de \*Arr-app
- Interactief zoeken inschakelen - Voor indexers met dit profiel, interactieve (handmatige) zoekopdrachten inschakelen voor de \*Arr-app
- Automatisch zoeken inschakelen - Voor indexers met dit profiel, automatische zoekopdrachten inschakelen voor de \*Arr-app
- Minimum aantal seeders - Voor indexers met dit profiel, het minimum aantal seeders dat vereist is voor \*Arr om een torrent te downloaden

# Downloadclients (Prowlarr-zoekopdrachten)

> Als je van plan bent om rechtstreeks in Prowlarr te zoeken, moet je Downloadclients toevoegen. Anders hoef je ze hier niet toe te voegen. Voor zoekopdrachten vanuit je apps worden de daar geconfigureerde downloadclients gebruikt.

> Downloadclients zijn alleen voor Prowlarr-zoekopdrachten in de app en worden niet gesynchroniseerd met apps. Er zijn geen plannen om een dergelijke functionaliteit toe te voegen.

Klik op `Instellingen` => `Downloadclients` en klik vervolgens op het + -teken om een nieuwe downloadclient toe te voegen. Je downloadclient moet al zijn geconfigureerd volgens deze handleiding.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

> Momenteel ondersteunde downloadclients vind je op de [Meer informatie (Ondersteund)](/prowlarr/supported#downloadclient) pagina voor dit gedeelte

Selecteer de downloadclient die je wilt toevoegen en er verschijnt een pop-upvenster om de verbindingsgegevens in te voeren. Deze gegevens zijn vergelijkbaar voor de meeste clients. Sommige vragen om een gebruikersnaam of wachtwoord, sommige vragen of nieuwe downloads in een gepauzeerde/starttoestand moeten worden toegevoegd, enz.
![nzbget.png](/assets/prowlarr/nzbget.png)

> De prioriteit van de client is alleen van belang wanneer er 2 van hetzelfde type (usenet of torrent) zijn toegevoegd. 1 heeft de hoogste prioriteit en als er meerdere clients van hetzelfde type zijn en dezelfde prioriteit hebben, zal Prowlarr er tussen schakelen.

## Usenet-clientinstellingen

- Naam - De naam van de downloadclient binnen Prowlarr
- Inschakelen - Deze downloadclient inschakelen
- Host - De URL van je downloadclient
- Poort - De poort van je downloadclient
- SSL gebruiken - Een beveiligde verbinding gebruiken met je downloadclient. Let op deze veelgemaakte fout.
- URL-basis - Voeg een voorvoegsel toe aan de URL; dit is vaak nodig voor omgekeerde proxies.
- API-sleutel - de API-sleutel om je client te authenticeren
- Gebruikersnaam - de gebruikersnaam om je client te authenticeren (meestal niet nodig)
- Wachtwoord - het wachtwoord om je client te authenticeren (meestal niet nodig)
- Categorie - de categorie binnen je downloadclient die Prowlarr zal gebruiken
- Prioriteit - prioriteit van de downloadclient voor toegevoegde items
- Clientprioriteit - Prioriteit van de downloadclient binnen Prowlarr. Round-robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) die dezelfde prioriteit hebben.

## Torrent-clientinstellingen

- Naam - De naam van de downloadclient binnen Prowlarr
- Inschakelen - Deze downloadclient inschakelen
- Host - De URL van je downloadclient
- Poort - De poort van je downloadclient
- SSL gebruiken - Een beveiligde verbinding gebruiken met je downloadclient. Let op deze veelgemaakte fout.
- URL-basis - Voeg een voorvoegsel toe aan de URL; dit is vaak nodig voor omgekeerde proxies.
- Gebruikersnaam - de gebruikersnaam om je client te authenticeren
- Wachtwoord - het wachtwoord om je client te authenticeren
- Categorie - de categorie binnen je downloadclient die Prowlarr zal gebruiken
- Prioriteit - prioriteit van de downloadclient voor toegevoegde items
- Initiële status - Initiële status voor torrents (alleen Qbittorrent: Geforceerd omzeilt alle seeddrempels)
- Clientprioriteit - Prioriteit van de downloadclient binnen Prowlarr. Round-robin wordt gebruikt voor clients van hetzelfde type (torrent/usenet) die dezelfde prioriteit hebben.

## Testen van de downloadclient

Test je invoer. Als er een groen vinkje verschijnt, kun je je invoer opslaan en herhalen indien nodig voor elke downloadclient die je met Prowlarr wilt gebruiken. Als het mislukt, moet je je logboek controleren op de fout (verbinding, referenties, enz.).

# Installatie voltooid

Dat is het voor de basis! Je kunt vervolgens meldingen en andere geavanceerde instellingsopties toevoegen indien nodig. Deze worden gedocumenteerd op de volledige instellingenpagina.