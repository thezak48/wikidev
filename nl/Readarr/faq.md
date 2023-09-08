- No, you cannot disable the refresh books task in Readarr. The refresh books task is responsible for updating the metadata and status of your books, ensuring that Readarr has the most up-to-date information. Disabling this task would prevent Readarr from accurately tracking and managing your library.

- Nee, dat moet je ook niet doen via SQL-hackery. De taak 'Boeken vernieuwen' vraagt de upstream Servarr-proxy op en controleert of de metadata voor elk boek (ids, cast, samenvatting, beoordeling, vertalingen, alternatieve titels, enz.) is bijgewerkt in vergelijking met wat er momenteel in Readarr staat. Indien nodig zal het de betreffende boeken bijwerken.
- Een veelvoorkomende klacht is dat de vernieuwingstaak zorgt voor zware I/O-gebruik. Een instelling die problemen kan veroorzaken, is "Auteurmap opnieuw scannen na vernieuwen". Als uw schijf-I/O-gebruik stijgt tijdens een vernieuwing, wilt u mogelijk de instelling voor het opnieuw scannen wijzigen naar `Handmatig`. Verander dit niet naar `Nooit`, tenzij alle wijzigingen in uw bibliotheek (nieuwe boeken, upgrades, verwijderingen, enz.) via Readarr worden gedaan. Als u boekbestanden handmatig verwijdert of een programma van derden gebruikt, stel dit dan niet in op `Nooit`.

## Kan ik zowel een e-book als een luisterboekversie van hetzelfde boek hebben?

- Nee. Met een enkele Readarr-instantie kunt u slechts een van beide hebben, maar niet beide. Als u beide wilt, moet u twee afzonderlijke instanties van Readarr uitvoeren (net zoals sommige mensen 2 instanties van Sonarr of Radarr uitvoeren voor 1080p- en 4K-versies van hun media).

## Moet ik Calibre gebruiken?

- Nee. Over het algemeen biedt Calibre enkele verdere verbeteringen, zoals de mogelijkheid om e-books automatisch om te zetten naar een ander formaat dat specifiek is voor de mogelijkheden van uw e-reader, en ook om verbinding te maken met die e-reader. Maar als u Calibre niet gebruikte voordat u Readarr installeerde, is het waarschijnlijk van beperkt voordeel om het te installeren, en het is een zeer groot programma.

## Waarom kan Readarr mijn bestanden niet zien op een externe server?

- Zorg ervoor dat de gebruiker/groep waarmee u \*Arr uitvoert lees- en schrijftoegang heeft tot de gemounte schijf voor alle besturingssystemen.
- Voor Linux zorg ervoor dat:
  - Als u een NFS-mount gebruikt, zorg ervoor dat nolock is ingeschakeld voor uw mount.
  - Als u een SMB-mount gebruikt, zorg ervoor dat nobrl is ingeschakeld voor uw mount.
- Voor Windows: Kort gezegd kan de gebruiker waarmee \*Arr wordt uitgevoerd (als service) of onder (als tray-app) geen toegang krijgen tot het bestandspad op de externe server. Dit kan verschillende redenen hebben, maar de meest voorkomende is dat \*Arr wordt uitgevoerd als een service, wat de hieronder beschreven problemen veroorzaakt.

### Readarr wordt standaard uitgevoerd onder het LocalService-account dat geen toegang heeft tot beveiligde externe bestandsshares

- Voer de Readarr-service uit als een andere gebruiker die toegang heeft tot die share
- Open het venster Beheerprogramma's \> Services op uw Windows-server.
- Stop de Readarr-service.
- Open het dialoogvenster Eigenschappen \> Aanmelden.
- Wijzig het gebruikersaccount van de service naar het doelgebruikersaccount.
- Voer Readarr.exe uit via de map Opstarten

### U gebruikt een gekoppelde netwerkdrive (geen UNC-pad)

- Wijzig uw paden naar UNC-paden (`\\server\share`)
- Voer Readarr.exe uit via de map Opstarten

## Help, ik ben buitengesloten

{#help-i-have-forgotten-my-password}

Om authenticatie uit te schakelen (om uw vergeten gebruikersnaam of wachtwoord opnieuw in te stellen), moet u `config.xml` bewerken die zich bevindt in de [Readarr Appdata Directory](/readarr/appdata-directory)

1. Open config.xml in een teksteditor
1. Zoek de regel met de authenticatiemethode zal zijn
`<AuthenticationMethod>Basic</AuthenticationMethod>` of `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Wijzig de regel `AuthenticationMethod` naar `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Readarr opnieuw op
1. Readarr is nu toegankelijk zonder wachtwoord, u moet naar `Instellingen: Algemeen` in de UI gaan en uw gebruikersnaam en wachtwoord instellen

## Hoe voorkom ik dat de browser wordt geopend bij het opstarten?

Afhankelijk van uw besturingssysteem zijn er meerdere mogelijke manieren.

- In `Instellingen` => `Algemeen` op sommige besturingssystemen is er een selectievakje om de browser bij het opstarten te openen.
- Bij het starten van Readarr kunt u `-nobrowser` (*nix) of `/nobrowser` (Windows) toevoegen aan de argumenten.
- Stop Readarr en bewerk het config.xml-bestand en wijzig `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## Vreemde UI-problemen

- Als u vreemde UI-problemen ondervindt, zoals de bibliotheekpagina die niets vermeldt of een bepaalde weergave of sortering die niet werkt, probeer dan te kijken in een Chrome Incognito-venster of een Firefox Private Window. Als het daar goed werkt, wis dan uw browsercache en cookies voor uw specifieke IP/domein. Zie het artikel [Cache en cookies wissen](/useful-tools#clearing-cookies-and-local-storage) voor meer informatie.

## VPN's, Jackett en de \*ARRs

- Tenzij u zich in een onderdrukkend land bevindt zoals China, Australië of Zuid-Afrika, is uw torrentclient meestal het enige dat achter een VPN moet zitten. Omdat het VPN-eindpunt wordt gedeeld door veel gebruikers, kunt u te maken krijgen met snelheidsbeperkingen, DDOS-bescherming en IP-blokkades van verschillende services die elke software gebruikt.
- Met andere woorden, het achter een VPN plaatsen van de \*Arrs (Lidarr, Prowlarr, Radarr, Readarr en Lidarr) kan ervoor zorgen dat de applicaties in sommige gevallen onbruikbaar worden omdat de services niet toegankelijk zijn.

> **Om duidelijk te zijn, het is niet de vraag of VPN's problemen zullen veroorzaken met de \*Arrs, maar wanneer: beeldleveranciers zullen u blokkeren en cloudflare staat voor de meeste \*Arr-servers (updates, metadata, enz.) en kan u ook blokkeren**
{.is-warning}

- **Veel privé-trackers zullen u verbannen als u ze gebruikt of er toegang toe krijgt (bijv. met Jackett of Prowlarr) via een VPN.**

### Gebruik van een VPN

- Als een VPN vereist is en Docker wordt gebruikt, wordt het aanbevolen om Hotio of Binhex's Download Client + VPN Containers te gebruiken.
- Als een VPN vereist is en Docker niet wordt gebruikt, moet uw VPN-client ***split tunneling*** ondersteunen, zodat alleen de vereiste (Download Client) apps achter de VPN zitten.
- Veel problemen met het benaderen van trackers kunnen worden opgelost door Google of Cloudflare's DNS-servers te gebruiken in plaats van de DNS-servers van uw internetprovider.
- In sommige gevallen (bijv. Britse internetproviders) moet u uw torrent-downloadclient achter een VPN plaatsen en Jackett/Prowlarr als volgt:
  - plaats Jackett achter de VPN en zorg ervoor dat split tunneling lokale toegang toestaat
  - configureer voor Prowlarr uw VPN-client om een proxy te bieden en voeg de proxy toe in Instellingen => Indexers. Geef de proxy een tag en geef dezelfde tag aan eventuele indexers die deze moeten gebruiken.
    - Indien absoluut noodzakelijk en als uw VPN geen manier biedt om een proxy te maken, kunt u Prowlarr achter de VPN plaatsen en ervoor zorgen dat split tunneling lokale toegang toestaat.

## Jackett's /all-eindpunt

{#jackett-all-endpoint}

- Het Jackett `/all`-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan problemen veroorzaken, dus het is vereist om elke tracker afzonderlijk toe te voegen. Als alternatief kunt u overwegen om de Jackett & NZBHydra2-alternatief [Prowlarr](/prowlarr) te gebruiken.
- **Update 20 januari 2022: Het Jackett `/all`-eindpunt wordt niet langer ondersteund (bijv. waarschuwingen worden weergegeven) vanaf 0.1.0.1188 omdat het alleen maar problemen veroorzaakt.**
- Het Jackett /all-eindpunt is handig, maar dat is het enige voordeel ervan. Al het andere kan problemen veroorzaken, dus het is nu vereist om elke tracker afzonderlijk toe te voegen.
- [Zelfs de ontwikkelaars van Jackett zeggen dat het vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Het gebruik van het /all-eindpunt heeft geen voordelen, alleen nadelen:
  - u verliest de controle over specifieke instellingen van indexers (categorieën, zoekmodi, enz.)
  - het mixen van zoekmodi (IMDB, query, enz.) kan leiden tot resultaten van lage kwaliteit
  - specifieke categorieën van indexers (\>= 100000) kunnen niet worden gebruikt.
  - trage indexers vertragen het algehele resultaat
  - het totale aantal resultaten is beperkt tot 1000
  - als een van de trackers in /all een fout retourneert, schakelt \*Arr deze uit en krijgt u nu geen resultaten meer.

### Oplossingen voor Jackett /All

- Voeg elke tracker in Jackett handmatig toe als een indexer in \*Arr
- Bekijk [Prowlarr](/prowlarr), dat indexers kan synchroniseren met \*Arr en afkomstig is van het Lidarr/Radarr/Readarr-ontwikkelingsteam.
- Bekijk [NZBHydra2](https://github.com/theotherp/nzbhydra2), dat indexers kan synchroniseren met \*Arr. Gebruik echter niet hun enkele aggregatie-eindpunt en gebruik `multi` als synchronisatie wordt gebruikt.

## Waarom zijn er twee bestanden? | Waarom blijft er een bestand achter in de downloads?

Dit is normaal. Met een configuratie die [hardlinks](https://trash-guides.info/hardlinks) ondersteunt, wordt er geen dubbele ruimte gebruikt. Hieronder staat hoe het torrentproces werkt.

1. Readarr stuurt een downloadverzoek naar uw client en koppelt het aan een label of categorienaam die u heeft geconfigureerd in de instellingen van de downloadclient. Voorbeelden: films, tv, series, muziek, enz.
1. Readarr controleert uw actieve downloads in uw downloadclient die gebruikmaken van die categorienaam. Deze monitoring gebeurt via de API van uw downloadclient.
1. Voltooide bestanden blijven op hun oorspronkelijke locatie staan zodat u het bestand kunt seeden (ratio of tijd kan worden aangepast in de downloadclient of vanuit Readarr onder de specifieke downloadclient). Wanneer bestanden worden geïmporteerd naar uw mediamap, wordt het bestand gekoppeld (hardlink) als dit wordt ondersteund door uw configuratie, anders wordt het bestand gekopieerd als hardlinks niet worden ondersteund.
1. Als de optie "Voltooide downloadverwerking - Voltooide verwijderen" is ingeschakeld in de instellingen van Readarr, zal Readarr het oorspronkelijke bestand en de torrent verwijderen uit uw downloadclient, maar alleen als de downloadclient meldt dat het seeden is voltooid en de torrent is gestopt.

> Hardlinks zijn standaard ingeschakeld. [Een hardlink gebruikt geen extra schijfruimte.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Het bestandssysteem en de koppelingen moeten hetzelfde zijn voor uw voltooide downloadmap en uw mediatheek. Als het maken van een hardlink mislukt of uw configuratie geen hardlinks ondersteunt, wordt er overgeschakeld naar het kopiëren van het bestand.
{.is-info}

## Calibre geeft de melding "Calibre rejected duplicate book", maar dat is niet zo

Als u Calibre-integratie gebruikt, zal Calibre af en toe een boek afwijzen en zeggen dat het een duplicaat is. Het is waarschijnlijk geen echt duplicaat. Als dit gebeurt, kan Readarr niet veel doen en moet u dat boek niet meer volgen om te voorkomen dat Readarr blijft proberen het te pakken en naar Calibre te sturen. Dit is slechts een van de leuke nadelen van Calibre-integratie.