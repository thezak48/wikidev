# Series

De pagina Series toont je volledige bibliotheek en stelt je in staat om individuele series te selecteren (hoewel zoeken efficiënter kan zijn in grote bibliotheken) en zoekopdrachten uit te voeren voor specifieke series, evenals het bewerken ervan. Het stelt je ook in staat om je series te filteren.

# Filters

De filteropties stellen je in staat om je series te verfijnen en zijn ontzettend handig. Je kunt ze gebruiken om releasedata, namen, afleveringentellingen, schijfgroottetellingen en nog veel meer te zien, inclusief aangepaste filters die aan al je behoeften voldoen. Deze kunnen ook worden gebruikt in de massabewerker.

# Nieuwe toevoegen

Met de functie Nieuwe toevoegen kun je een nieuwe serie toevoegen die Sonarr kan volgen en downloaden.

- Hoofdmap - De geselecteerde [hoofdmap/bibliotheekmap](/sonarr/settings#root-folders) in Sonarr die deze serie moet gebruiken
- Monitoren - Hoe wil je dat de serie in eerste instantie wordt gemonitord?
  - Alle afleveringen - Alle afleveringen monitoren, behalve specials
  - Toekomstige afleveringen - Afleveringen monitoren die nog niet zijn uitgezonden
  - Ontbrekende afleveringen - Afleveringen monitoren die geen bestanden hebben of nog niet zijn uitgezonden
  - Bestaande afleveringen - Afleveringen monitoren die bestanden hebben
  - Eerste seizoen - Alle afleveringen van het eerste seizoen monitoren; alle andere seizoenen worden genegeerd
  - Laatste seizoen - Alle afleveringen van het laatste seizoen en toekomstige seizoenen monitoren
  - Geen - Er worden geen afleveringen gemonitord
- Kwaliteitsprofiel - Het [kwaliteitsprofiel](/sonarr/settings#quality-profiles) dat moet worden gebruikt voor deze serie
- Serietype - Welk serietype moet worden gebruikt voor deze serie; dit verandert hoe zoekopdrachten worden uitgevoerd [Zie de FAQ voor meer informatie](/sonarr/faq#whats-the-different-series-types)
- Seizoensmap - In- of uitschakelen van het maken en gebruiken van seizoensmappen voor deze serie
- Tags - Gebruikt om series toe te wijzen aan releaseprofielen, vertragingsprofielen, indexers, of gewoon om je series te organiseren
- [ ] Zoeken naar ontbrekende afleveringen starten - op basis van je geselecteerde monitorinstellingen, zoeken naar alle ontbrekende en gemonitorde afleveringen in deze serie
- [ ] Zoeken naar afleveringen die niet aan de cutoff voldoen starten - op basis van je geselecteerde monitorinstellingen en alleen van toepassing als je bestanden hebt voor je afleveringen in de map van de serie, zoeken naar alle bestaande en gemonitorde afleveringen in deze serie die niet aan je kwaliteitsprofiel's cutoff voldoen of deze overschrijden

# Bibliotheek importeren

Met Bibliotheek importeren kun je bestaande, georganiseerde series en afleveringsbestanden importeren in Sonarr via bestaande bestanden in de map van het pad. Dit is vooral handig wanneer je een nieuwe Sonarr-instantie maakt en je bestaande series wilt behouden.

- Bibliotheek importeren is bedoeld voor het toevoegen en importeren van een bestaande georganiseerde bibliotheek van series in Sonarr.

- Bibliotheek importeren kan niet worden gebruikt voor:
  - Het importeren van bestanden uit een downloadmap
  - Het toevoegen of importeren van één of meer bestanden die niet correct zijn benoemd en georganiseerd in hun eigen map van de serie binnen je hoofdmap of een map die je als hoofdmap wilt toevoegen
  - Andere toepassingen dan het toevoegen van een serie of aflevering aan Sonarr en het importeren van de serie en de bijbehorende bestand(en) vanuit de hoofdmap (bibliotheekmap) die is ingevoerd in Bibliotheek importeren

> \* Niet-Windows: Als je een NFS-mount gebruikt, zorg er dan voor dat `nolock` is ingeschakeld.
> \* Als je een SMB-mount gebruikt, zorg er dan voor dat `nobrl` is ingeschakeld.
{.is-warning}

> **De gebruiker en groep die je hebt geconfigureerd om Sonarr uit te voeren, moeten lees- en schrijftoegang hebben tot deze locatie.** {.is-info}

> Je downloadclient downloadt naar een downloadmap en Sonarr importeert het naar je mediamap (eindbestemming) die je mediaserver gebruikt.
{.is-info}

> **Je downloadmap en mediamap kunnen niet dezelfde locatie zijn**
{.is-danger}

# Massabewerker

De massabewerker stelt je in staat om series massaal te bewerken. Je kunt alle eerdere instellingen wijzigen die zijn gemaakt toen je de serie toevoegde.

# Seizoenspas

Dit toont informatie over hoeveel seizoenen elke serie heeft en hoeveel afleveringen er in elk seizoen ontbreken.