---
title: Prowlarr Indexers
description: 
published: true
date: 2023-03-30T14:04:26.292Z
tags: 
editor: markdown
dateCreated: 2021-06-06T11:45:31.974Z
---

Deze pagina beschrijft hoe je indexers kunt toevoegen en configureren in Prowlarr.

# Een Indexer toevoegen

Om een indexer toe te voegen, klik eerst op `Indexers` aan de linkerkant en klik vervolgens op <kb>+</kb> `Add Indexer` bovenaan de pagina.

![ind_1_addindexer.png](/assets/prowlarr/ind_1_addindexer.png)

Kies je indexer uit de lijst of typ een gedeeltelijke naam in het vak om je indexer te vinden. Als je indexer niet in de lijst staat, kun je mogelijk "Generic Newznab" (voor Usenet) of "Generic Torznab" (voor torrents) gebruiken. Bezoek anders onze [Indexer Request site](https://requests.prowlarr.com/).

> Het gebruik van `Generic Newznab` of `Generic Torznab` gaat ervan uit dat je indexer gestandaardiseerde *znab-formaten ondersteunt. Als dit niet het geval is, werkt dit niet.
{.is-info}

> Let op: bijna elke Usenet-site is compatibel met Generic Newznab.
{.is-warning}

> Als je tracker of indexer niet in de lijst staat en niet op onze [ondersteunde indexers](/prowlarr/supported-indexers) pagina staat, kun je een verzoek indienen om deze toe te voegen via onze [Indexer Requests Site](https://requests.prowlarr.com)
{.is-info}

# Een Indexer bewerken

Om een indexer te bewerken, klik eerst op `Indexers` aan de linkerkant en klik vervolgens op het moersleutel-icoon helemaal rechts van de indexer die je wilt bewerken.

# Het ID of de URL van een Indexer bekijken

Om details over een indexer te bekijken, klik eerst op `Indexers` aan de linkerkant en klik vervolgens op de Indexer Link in de Indexer Name-kolom. (Vroeger het (i)-icoon aan de rechterkant)

Beschikbare details kunnen zijn:

- Id in Prowlarr
- Beschrijving
- Codering
- Taal
- Site
- Newznab/Torznab Prowlarr URL
- Site-mogelijkheden

# Indexer-instellingen

Nadat je je indexer hebt geselecteerd, verschijnt er een pop-up met verdere informatie die je moet configureren. Houd er rekening mee dat de specifieke instellingen per indexer iets kunnen verschillen op basis van hun vereiste velden en het type indexer dat je configureert.

![ind_3_indexer2.png](/assets/prowlarr/ind_3_indexer2.png)

- Naam - Selecteer een naam voor deze indexer. Wanneer het synchroniseert met je apps, wordt er `(Prowlarr)` achter geplaatst.
- Inschakelen - Vink het vakje aan om deze indexer in te schakelen.
- Doorsturen - Vink het vakje aan als doorsturen nodig is. Er zijn slechts een paar indexers waarbij dit nodig is om een ban te voorkomen. Als dit is ingeschakeld, wordt de downloadlink rechtstreeks naar de applicatie doorgestuurd in plaats van via Prowlarr te worden geproxyd.

> Doorsturen is meestal alleen nodig voor een handvol zeer specifieke indexers
{.is-info}

- Synchronisatieprofiel - Selecteer hier je synchronisatieprofiel. Deze kunnen worden aangemaakt in [`Instellingen` => `Apps`](/prowlarr/settings#applications). Het standaardprofiel, "Standard", bestaat al en ziet er zo uit:

> Je kunt verschillende instellingen per app hebben door meerdere instanties van de indexer aan te maken
{.is-info}

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Selecteer de URL die Prowlarr moet gebruiken. Als dit leeg is, wordt de standaard/eerste URL gebruikt.
- Downloadlink - Als je een torrent-indexer toevoegt, moet je mogelijk kiezen welk soort downloadlink je wilt gebruiken.
- (Geavanceerde optie) API-pad - Pad naar de API van de indexer. Meestal `/api`
- Referenties - Veel indexers en trackers vereisen dat je op de een of andere manier authenticatie/inloggegevens invoert. Je moet mogelijk een API-sleutel, RSS-sleutel, een sessie-id, een cookie of andere referenties van je indexer invoeren (meestal te vinden op je profielpagina of onder Beveiliging), zoekvolgordes selecteren of andere opties voor je specifieke indexer.
  - API-sleutel
  - RSS-sleutel
  - Sessie-ID
  - Cookie
  - Gebruikersnaam/wachtwoord
  - etc.
- (Geavanceerde optie) Extra parameters - Extra parameters om toe te voegen aan de verzoeken voor deze indexer.
- VIP-verloopdatum - Voer de datum in ISO-formaat (jjjj-MM-dd) in om 1 week voor het verlopen een melding te ontvangen; laat anders leeg
- Tags - Gebruik tags om standaard downloadclients aan te geven, indexer-proxies aan te geven, indexers aan applicaties toe te wijzen of gewoon om je indexers te organiseren.
- (Geavanceerde optie) Querylimiet - Als je indexer je API-aanroepen per dag beperkt, kun je hier dat aantal invoeren om de limiet niet te overschrijden.
- (Geavanceerde optie) Grablimiet - Als je indexer je Grabs per dag beperkt, kun je hier dat aantal invoeren om de limiet niet te overschrijden. Zodra de grablimiet is bereikt, zal verdere zoekopdrachten een onbehandelde uitzondering in \*Arr-apps veroorzaken. Andere apps kunnen anders reageren.
- (Geavanceerde optie) Seed-verhouding - Alleen voor Torrent-indexers: de verhouding die een torrent moet bereiken voordat deze stopt, leeg is de standaardwaarde van de app
- (Geavanceerde optie) Seed-tijd - Alleen voor Torrent-indexers: de tijd dat een torrent moet worden geüpload voordat deze stopt, leeg is de standaardwaarde van de app. Waarden zijn in minuten.
- (Geavanceerde optie) Indexerprioriteit - Prioriteit van deze indexer om de ene indexer boven de andere te verkiezen in release-tiebreaker-scenario's. 1 is de hoogste prioriteit en 50 is de laagste prioriteit. Deze prioriteiten worden gesynchroniseerd met de \*Arr-apps.

- Test je indexer en als er een groen vinkje verschijnt, kun je het opslaan. Wanneer je het opslaat, wordt het, afhankelijk van je synchronisatie-instellingen, automatisch aan je apps toegevoegd.

## Een aangepaste YML-definitie toevoegen

- Houd er rekening mee dat de yml-definitie voor een korte periode in de cache wordt opgeslagen en als je wijzigingen wilt aanbrengen voor ontwikkelingsdoeleinden, moet je wachten tot de cache is verlopen of Prowlarr opnieuw opstarten.
- Als je een aangepast Cardigann-compatibel YML-definitiebestand wilt toevoegen voor een indexer die niet wordt ondersteund of om wijzigingen in een bestaande definitie te testen:
  - Ga naar (of maak) de map Custom Indexer Definition met de naam `Custom` binnen de map `Definitions` van de [App Data-map van Prowlarr](/prowlarr/appdata-directory)
    - Voorbeeldpaden:
      - Windows: `C:\ProgramData\Prowlarr\Definitions\Custom`
      - Linux: `/home/$USER/.config/Prowlarr/Definitions/Custom`
      - OSX: `/Users/$USER/.config/Prowlarr/Definitions/Custom`

  - Sla het [Cardigann-compatibele YML-bestand](/prowlarr/cardigann-yml-definition) op in de map en zorg ervoor dat Prowlarr toegangsrechten heeft om het te openen.

> De bestandsnaam en het id in de definitie moeten uniek zijn en mogen niet conflicteren met andere bestaande definities. Het is sterk aanbevolen om ook de naam in de definitie uniek te maken.
{.is-info}

# Ondersteunde Indexers

- [Zie deze wiki-pagina voor een lijst met ondersteunde indexers van de laatste nightly.](/prowlarr/supported-indexers/)