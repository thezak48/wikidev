# Markdown Syntax Guide

Markdown is a lightweight markup language that allows you to write formatted text using a plain text editor. It is widely used for writing documentation, creating web content, and even writing books.

## Headers

To create headers, use the `#` symbol followed by a space and the header text. The number of `#` symbols determines the level of the header, with one `#` being the highest level and six `#` symbols being the lowest level.

Example:

```markdown
# Heading 1
## Heading 2
### Heading 3
```

## Emphasis

To emphasize text, you can use either asterisks `*` or underscores `_`. Surround the text with a pair of asterisks or underscores to make it italic, and use two pairs to make it bold.

Example:

```markdown
*italic text*
_italic text_

**bold text**
__bold text__
```

## Lists

Markdown supports both ordered and unordered lists.

To create an unordered list, use the `-`, `+`, or `*` symbol followed by a space and the list item.

Example:

```markdown
- Item 1
- Item 2
- Item 3
```

To create an ordered list, use numbers followed by a period and a space.

Example:

```markdown
1. Item 1
2. Item 2
3. Item 3
```

## Links

To create a link, use square brackets `[]` to enclose the link text, followed by parentheses `()` containing the URL.

Example:

```markdown
[Google](https://www.google.com)
```

## Images

To insert an image, use an exclamation mark `!`, followed by square brackets `[]` containing the alt text, and parentheses `()` containing the image URL.

Example:

```markdown
![Alt Text](https://example.com/image.jpg)
```

## Code Blocks

To create a code block, indent the code by four spaces or one tab.

Example:

```markdown
    code block
```

## Blockquotes

To create a blockquote, use the `>` symbol followed by a space and the quoted text.

Example:

```markdown
> This is a blockquote.
```

## Horizontal Rules

To create a horizontal rule, use three or more hyphens `---`, asterisks `***`, or underscores `___` on a line by themselves.

Example:

```markdown
---
```

## Conclusion

This guide covers the basic syntax of Markdown. With these simple formatting rules, you can create well-structured and visually appealing documents. Markdown is a versatile and widely supported format, making it an excellent choice for writing content.

---
title: Lidarr Systeem
description: 
published: true
date: 2022-10-31T04:35:13.645Z
tags: lidarr, needs-love, systeem
editor: markdown
dateCreated: 2021-06-14T21:36:28.225Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [Status](#status)
  - [Gezondheid](#gezondheid)
    - [Systeemwaarschuwingen](#systeemwaarschuwingen)
      - [Branch is geen geldige release branch](#branch-is-geen-geldige-release-branch)
      - [Update naar .NET-versie](#update-naar-net-versie)
        - [Problemen oplossen bij Docker-installaties](#problemen-oplossen-bij-docker-installaties)
        - [Problemen oplossen bij Standalone-installaties](#problemen-oplossen-bij-standalone-installaties)
      - [Huidige geïnstalleerde mono-versie is oud en wordt niet ondersteund](#huidige-geïnstalleerde-mono-versie-is-oud-en-wordt-niet-ondersteund)
      - [Huidige geïnstalleerde SQLite-versie wordt niet ondersteund](#huidige-geïnstalleerde-sqlite-versie-wordt-niet-ondersteund)
      - [Nieuwe update beschikbaar](#nieuwe-update-beschikbaar)
      - [Kan update niet installeren omdat de opstartmap niet beschrijfbaar is door de gebruiker](#kan-update-niet-installeren-omdat-de-opstartmap-niet-beschrijfbaar-is-door-de-gebruiker)
      - [Update is niet mogelijk om het verwijderen van AppData bij te werken](#update-is-niet-mogelijk-om-het-verwijderen-van-appdata-bij-te-werken)
      - [Branch is voor een vorige versie](#branch-is-voor-een-vorige-versie)
      - [Kan geen verbinding maken met signalR](#kan-geen-verbinding-maken-met-signalr)
        - [NGINX](#nginx)
        - [Apache](#apache)
        - [Caddy](#caddy)
      - [Kan het IP-adres voor de geconfigureerde proxyhost niet oplossen](#kan-het-ip-adres-voor-de-geconfigureerde-proxyhost-niet-oplossen)
      - [Proxytest mislukt](#proxytest-mislukt)
      - [Systeemtijd loopt meer dan 1 dag achter](#systeemtijd-loopt-meer-dan-1-dag-achter)
      - [Mono Legacy TLS ingeschakeld](#mono-legacy-tls-ingeschakeld)
      - [Mono- en x86-builds worden beëindigd](#mono-en-x86-builds-worden-beëindigd)
      - [FPcalc moet worden bijgewerkt](#fpcalc-moet-worden-bijgewerkt)
    - [Downloadclients](#downloadclients)
      - [Er is geen downloadclient beschikbaar](#er-is-geen-downloadclient-beschikbaar)
      - [Kan niet communiceren met downloadclient](#kan-niet-communiceren-met-downloadclient)
      - [Downloadclients zijn niet beschikbaar vanwege een storing](#downloadclients-zijn-niet-beschikbaar-vanwege-een-storing)
      - [Voltooide downloadverwerking inschakelen](#voltooide-downloadverwerking-inschakelen)
      - [Docker verkeerde externe padtoewijzing](#docker-verkeerde-externe-padtoewijzing)
      - [Downloaden naar hoofdmap](#downloaden-naar-hoofdmap)
      - [Foutieve instellingen voor downloadclient](#foutieve-instellingen-voor-downloadclient)
      - [Foutieve externe padtoewijzing](#foutieve-externe-padtoewijzing)
      - [Toestemmingsfout](#toestemmingsfout)
      - [Extern bestand is tijdens de verwerking gedeeltelijk verwijderd](#extern-bestand-is-tijdens-de-verwerking-gedeeltelijk-verwijderd)
      - [Extern pad wordt gebruikt en importeren is mislukt](#extern-pad-wordt-gebruikt-en-importeren-is-mislukt)
    - [Voltooide/mislukte downloadverwerking](#voltooide-mislukte-downloadverwerking)
      - [Voltooide downloadverwerking is uitgeschakeld](#voltooide-downloadverwerking-is-uitgeschakeld)
    - [Indexers](#indexers)
      - [Geen indexers beschikbaar met automatisch zoeken ingeschakeld, Lidarr geeft geen automatische zoekresultaten](#geen-indexers-beschikbaar-met-automatisch-zoeken-ingeschakeld-lidarr-geeft-geen-automatische-zoekresultaten)
      - [Geen indexers beschikbaar met RSS-synchronisatie ingeschakeld, Lidarr haalt nieuwe releases niet automatisch op](#geen-indexers-beschikbaar-met-rss-synchronisatie-ingeschakeld-lidarr-haalt-nieuwe-releases-niet-automatisch-op)
      - [Er zijn geen indexers ingeschakeld](#er-zijn-geen-indexers-ingeschakeld)
    - [Ingeschakelde indexers ondersteunen geen zoeken](#ingeschakelde-indexers-ondersteunen-geen-zoeken)
      - [Geen indexers beschikbaar met interactief zoeken ingeschakeld](#geen-indexers-beschikbaar-met-interactief-zoeken-ingeschakeld)
      - [Indexers zijn niet beschikbaar vanwege storingen](#indexers-zijn-niet-beschikbaar-vanwege-storingen)
      - [Jackett All Endpoint gebruikt](#jackett-all-endpoint-gebruikt)
        - [Oplossingen](#oplossingen)
    - [Artiestmappen](#artiestmappen)
      - [Ontbrekende hoofdmap](#ontbrekende-hoofdmap)
      - [Lijsten zijn niet beschikbaar vanwege storingen](#lijsten-zijn-niet-beschikbaar-vanwege-storingen)
  - [Schijfruimte](#schijfruimte)
  - [Over](#over)
  - [Meer informatie](#meer-informatie)
- [Taken](#taken)
  - [Gepland](#gepland)
  - [Wachtrij](#wachtrij)
- [Back-up](#back-up)
- [Updates](#updates)
- [Gebeurtenissen](#gebeurtenissen)
- [Logbestanden](#logbestanden)

> Waarschuwing: Deze pagina is nog in ontwikkeling en is momenteel een ruwe schets op basis van Readarr
{.is-danger}

# Status

## Gezondheid

Deze pagina bevat een lijst met fouten bij gezondheidscontroles. Deze gezondheidscontroles worden periodiek uitgevoerd door Lidarr en bij bepaalde gebeurtenissen. De resulterende waarschuwingen en fouten worden hier vermeld om advies te geven over hoe ze op te lossen.

### Systeemwaarschuwingen

#### Branch is geen geldige release branch

De branch die je hebt ingesteld is geen geldige release branch. Je ontvangt geen updates. Verander dit naar een van de [huidige release branches](/lidarr/faq#hoe-update-ik-lidarr)

#### Update naar .NET-versie

{#update-to-net-core-version}

- Nieuwere versies van Lidarr zijn gericht op .NET6 of nieuwer. We zullen geen legacy mono builds meer leveren na de release van 1.0. Je gebruikt een van deze legacy builds, maar je platform ondersteunt .NET.

##### Problemen oplossen bij Docker-installaties

- Trek je container opnieuw

##### Problemen oplossen bij Standalone-installaties

- Maak een back-up van je bestaande configuratie voordat je de volgende stap uitvoert.
- Dit zou alleen moeten gebeuren op Linux-hosts. Installeer geen .NET-runtime of -SDK van Microsoft.
- Download de juiste build voor je architectuur en vervang je bestaande binaries (toepassing)
- Kort gezegd moet je je bestaande binaries (inhoud of map van /opt/Lidarr) verwijderen en vervangen door de inhoud van de .tar.gz die je zojuist hebt gedownload.

> EXTRACT DE DOWNLOAD NIET GEWOON OVER JE BESTAANDE BINARIES.
> JE MOET EERST DE OUDE VERWIJDEREN.
{.is-warning}

- Hieronder staat een door de community ontwikkeld script om je mono-installatie te verwijderen en te vervangen door de .NET-installatie. Bijdragen en correcties zijn welkom.
- Dit gaat ervan uit dat je op de `master` Lidarr-branch zit, pas de variabelen indien nodig aan.
- Dit gaat ervan uit dat Lidarr wordt uitgevoerd als de gebruiker `lidarr`, pas de variabelen indien nodig aan.
- Dit gaat ervan uit dat Lidarr is geïnstalleerd in `/opt/Lidarr`, pas de variabelen indien nodig aan

```bash
#!/bin/bash
## Gebruikersvariabelen
installdir="/opt/Lidarr"
APPUSER="lidarr"
branch="master"
## /Gebruikersvariabelen
app="lidarr"
ARCH=$(dpkg --print-architecture)
# Stop \*arr
sudo systemctl stop $app
# krijg arch
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "Arch wordt niet ondersteund"
    exit 1
    ;;
esac
echo "Downloaden..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Installatiebestanden gedownload en uitgepakt"
echo "Huidige installatie verplaatsen"
sudo mv "$installdir/" "$installdir.old/"
echo "Installeren..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "App geïnstalleerd"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### Huidige geïnstalleerde mono-versie is oud en wordt niet ondersteund

- Lidarr is geschreven in .NET en vereist Mono om te kunnen draaien op zeer oude ARM-processors. Houd er rekening mee dat Mono-builds niet langer worden ondersteund na v1.0
- Mono 5.20 is het absolute minimum voor Lidarr.
- De upgradeprocedure voor Mono verschilt per platform.

#### Huidige geïnstalleerde SQLite-versie wordt niet ondersteund

- Lidarr slaat zijn gegevens op in een SQLite-database. De geïnstalleerde SQLite3-bibliotheek op je systeem is te oud. Lidarr vereist minimaal versie 3.9.0. Houd er rekening mee dat Lidarr `libSQLite3.so` gebruikt, die al dan niet is opgenomen in een SQLite3-upgradepakket.

#### Nieuwe update beschikbaar

- Verheug je, de ontwikkelaars hebben een nieuwe update uitgebracht. Dit betekent meestal geweldige nieuwe functies en opgeloste problemen (toch?). Blijkbaar heb je automatische updates niet ingeschakeld, dus je moet zelf uitzoeken hoe je moet updaten op jouw platform. Het indrukken van de knop Installeren op de pagina `Systeem => Updates` is waarschijnlijk een goed startpunt.

> Deze waarschuwing verschijnt niet als je huidige versie minder dan 14 dagen oud is
{.is-info}

#### Kan update niet installeren omdat de opstartmap niet beschrijfbaar is door de gebruiker

- Dit betekent dat Lidarr zichzelf niet kan updaten. Je moet Lidarr handmatig bijwerken of de machtigingen op de opstartmap van Lidarr (de installatiemap) instellen om Lidarr in staat te stellen zichzelf bij te werken.

#### Update is niet mogelijk om het verwijderen van AppData bij te werken

- Lidarr heeft gedetecteerd dat de AppData-map voor je besturingssysteem zich bevindt in de map die de Lidarr-binaries bevat. Normaal gesproken zou dit `C:\ProgramData` zijn voor Windows en `~/.config` voor Linux.

- Kijk naar `System => Info` om de huidige AppData- en opstartmappen te zien.
- Dit betekent dat Lidarr zichzelf niet kan bijwerken zonder het risico van gegevensverlies.
- Als je Linux gebruikt, moet je waarschijnlijk de home-directory voor de gebruiker die Lidarr uitvoert wijzigen en de huidige inhoud van de map `~/.config/Lidarr` kopiëren om je database te behouden.

#### Branch is voor een vorige versie

- De update-branch die is ingesteld in `Instellingen => Algemeen` is voor een vorige versie van Lidarr, daarom zal de instantie geen juiste update-informatie zien in de `Systeem => Updates` feed en mogelijk geen nieuwe updates ontvangen wanneer deze worden uitgebracht.

#### Kan geen verbinding maken met signalR

- signalR zorgt voor dynamische UI-updates, dus als je browser geen verbinding kan maken met signalR op je server, zie je geen realtime updates in de UI.

- De meest voorkomende oorzaak hiervan is het gebruik van een omgekeerde proxy of Cloudflare.
- Cloudflare heeft websockets ingeschakeld nodig.

##### NGINX

- Nginx vereist de volgende toevoeging aan het locatieblok voor de app:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Zorg ervoor dat je `proxy_set_header Connection "Upgrade";` niet opneemt zoals voorgesteld door de nginx-documentatie. DIT WERKT NIET
> Zie <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache

- Voor een omgekeerde proxy van Apache2 moet je de volgende modules inschakelen: proxy, proxy_http en proxy_wstunnel. Voeg vervolgens deze websocket tunnelinstructie toe aan je vhost-configuratie:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8686/$1 [P,L]
```

##### Caddy

- Voor Caddy (V1) gebruik je dit:
- Let op: je moet ook de websocket-instructie toevoegen aan je Lidarr-configuratie

```none
 proxy /lidarr 127.0.0.1:8686 {
     websocket
     transparent
 }
```

#### Kan het IP-adres voor de geconfigureerde proxyhost niet oplossen

- Controleer je proxy-instellingen en zorg ervoor dat ze correct zijn
- Zorg ervoor dat je proxy actief, draaiend en toegankelijk is

#### Proxytest mislukt

- Je geconfigureerde proxy is niet succesvol getest, controleer de HTTP-fout en/of controleer de logs voor meer details.

#### Systeemtijd loopt meer dan 1 dag achter

- De systeemtijd loopt meer dan 1 dag achter. Geplande taken kunnen mogelijk niet correct worden uitgevoerd totdat de tijd is gecorrigeerd.
- Controleer je systeemtijd en zorg ervoor dat deze is gesynchroniseerd met een betrouwbare tijdserver en nauwkeurig is.

#### Mono Legacy TLS ingeschakeld

- Mono 4.x TLS-workaround is nog steeds ingeschakeld, overweeg het verwijderen van de `MONO_TLS_PROVIDER=legacy` omgevingsoptie

#### Mono- en x86-builds worden beëindigd

- Mono- en x86-builds worden niet langer ondersteund in de volgende versie van de applicatie. Als je deze foutmelding ontvangt, gebruik je de mono-versie van de applicatie of de x86-versie. Helaas zullen wegens de toenemende moeilijkheden bij de ontwikkelingsondersteuning voor deze legacy-versies hun ondersteuning en daarmee ook de releases ervoor worden stopgezet. Het wordt daarom aangeraden om te upgraden naar een ondersteund besturingssysteem dat geen x86 of mono vereist. Je kunt ook overwegen om Docker te gebruiken voor je behoeften.

#### FPcalc moet worden bijgewerkt

{#fpcalc-upgrade}

- Lidarr gebruikt chromaprint audio fingerprinting om tracks te identificeren. Dit is afhankelijk van een externe binair bestand `fpcalc`, dat wordt gedistribueerd met Lidarr v1 voor Windows, Linux en macOS, maar onafhankelijk moet worden geleverd op freeBSD.
- Zorg ervoor dat het fpcalc-binair dat wordt meegeleverd met Lidarr uitvoerbaar is (755-machtigingen). Dit bestand bevindt zich in de installatiemap van Lidarr (bijv. `/opt/Lidarr/fpcalc`). Als het niet uitvoerbaar is, corrigeer dan de machtigingen met de onderstaande opdracht en start vervolgens Lidarr opnieuw op.
  - Houd er rekening mee dat voor de fix mogelijk `sudo` vereist is of dat je pad naar de bin-map van Lidarr mogelijk verschilt, afhankelijk van je omgeving en configuratie.

```bash
chmod +x /opt/Lidarr/fpcalc
```

> De onderstaande informatie is alleen van toepassing op legacy v0.8.0-builds.
{.is-info}

- Om dit op een native Linux-instantie op te lossen, installeer je het juiste pakket met behulp van je pakketbeheerder en zorg je ervoor dat fpcalc beschikbaar is in je PATH (dit kun je controleren met `which fpcalc` en controleren of de juiste locatie van fpcalc wordt geretourneerd):

| Distributie  |       Pakket        |
| :-----------: | :------------------: |
| Debian/Ubuntu | libchromaprint-tools |
| Fedora/CentOS |  chromaprint-tools   |
|     Arch      |     chromaprint      |
|   OpenSUSE    |  chromaprint-fpcalc  |
|   Synology    |     chromaprint      |

### Downloadclients

#### Er is geen downloadclient beschikbaar

- Een correct geconfigureerde en ingeschakelde downloadclient is vereist voor Lidarr om media te kunnen downloaden. Aangezien Lidarr verschillende downloadclients ondersteunt, moet je bepalen welke het beste bij je eisen past. Als je al een downloadclient hebt geïnstalleerd, moet je Lidarr configureren om deze te gebruiken en een categorie aan te maken. Zie `Instellingen => Downloadclient`.

#### Kan niet communiceren met downloadclient

- Lidarr kon niet communiceren met de geconfigureerde downloadclient. Controleer of de downloadclient operationeel is en controleer de URL. Dit kan ook duiden op een verificatiefout.
- Dit wordt meestal veroorzaakt door een verkeerd geconfigureerde downloadclient. Dingen die je meestal kunt controleren:
  - Het IP-adres van je downloadclient - als alles op dezelfde fysieke machine staat, is dit meestal `127.0.0.1`
  - Het poortnummer dat je downloadclient gebruikt - deze zijn ingevuld met het standaard poortnummer, maar als je dit hebt gewijzigd, moet je hetzelfde nummer invoeren in Lidarr.
  - Zorg ervoor dat SSL-versleuteling niet is ingeschakeld als je zowel je Lidarr-instantie als je downloadclient op een lokaal netwerk gebruikt (d.w.z. via gewoon HTTP). Zie de SSL FAQ voor meer informatie.

#### Downloadclients zijn niet beschikbaar vanwege een storing

- Een of meer van je downloadclients reageert niet op verzoeken van Lidarr. Daarom heeft Lidarr besloten om tijdelijk te stoppen met het bevragen van de downloadclient op zijn normale cyclus van 1 minuut, die normaal wordt gebruikt om actieve downloads bij te houden en voltooide downloads te importeren. Lidarr zal echter doorgaan met het proberen te verzenden van downloads naar de client, maar zal hoogstwaarschijnlijk falen.
- Je moet `System=>Logs` inspecteren om te zien wat de reden is voor de fouten.
- Als je deze downloadclient niet meer gebruikt, schakel deze dan uit in Lidarr om de fouten te voorkomen.

#### Voltooide downloadverwerking inschakelen

- Lidarr vereist dat `Voltooide downloadverwerking` is ingeschakeld om bestanden te kunnen importeren die zijn gedownload door de downloadclient. Het wordt aanbevolen om `Voltooide downloadverwerking` in te schakelen. (Het is standaard ingeschakeld voor nieuwe gebruikers.)

#### Docker verkeerde externe padtoewijzing

- Deze fout wordt meestal geassocieerd met verkeerde docker-paden binnen je downloadclient of Lidarr.

- Een voorbeeld van verkeerde (inconsistente) paden zou zijn:
  - Downloadclient:  `/mnt/user/downloads:/downloads`
  - Lidarr:   `/mnt/user/downloads:/data`
- In dit voorbeeld plaatst de downloadclient zijn downloads in `/downloads` en vertelt Lidarr wanneer het klaar is dat het voltooide boek zich in `/downloads` bevindt. Lidarr komt dan langs en zegt "Oké, cool, laat me eens kijken in `/downloads`." Welnu, binnen Lidarr heb je geen `/downloads`-pad toegewezen, maar je hebt een `/data`-pad toegewezen, dus gooit het deze foutmelding.
- De gemakkelijkste oplossing hiervoor is CONSISTENTIE - als je één schema gebruikt in je downloadclient, gebruik het dan overal.

- Team Lidarr is een groot voorstander van het eenvoudigweg gebruiken van /data.

  - Downloadclient: `/mnt/user/data/downloads:/data/downloads`
  - Lidarr: `/mnt/user/data:/data`

- Nu kun je binnen de downloadclient aangeven waar je je downloads wilt plaatsen in `/data/downloads/movies`. Aangezien je `/data` hebt gebruikt in Lidarr, wanneer de downloadclient aan Lidarr vertelt dat het klaar is, zal Lidarr langskomen en zeggen "Mooi, ik heb een `/data` en ik kan ook `/data/downloads/movies` zien, alles is in orde."
- Er zijn veel goede handleidingen: onze wiki [Docker Guide](/docker-guide) en TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Deze handleidingen leggen veel nadruk op Hardlinks en Atomic moves, maar het algemene concept van containers en hoe padtoewijzing werkt, is de kern van deze discussies.
- Als je besturingssystemen of native en docker combineert, heb je een externe padtoewijzing nodig. Zie [TRaSH's Remote Path Guide voor Radarr](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) en [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/) voor meer informatie.

#### Downloaden naar hoofdmap

{#downloads-in-root-folder}

- Binnen de applicatie wordt een hoofdmap gedefinieerd als de geconfigureerde mediabibliotheekmap. Dit is niet de hoofdmap van een mount. Je downloadclient plaatst een onvolledige of voltooide download (of verplaatst voltooide downloads) naar je hoofd (bibliotheek) map.
- Dit veroorzaakt vaak problemen - inclusief gegevensverlies - en mag niet worden gedaan. Om dit op te lossen, wijzig je downloadclient zodat deze geen downloads plaatst binnen je hoofdmap. Let op: 'plaatsen' omvat ook als je downloadclient-categorie is ingesteld op je hoofdmap of als NZBGet/SABnzbd sorteren ingeschakeld heeft en sorteert naar je hoofdmap.
- Houd er rekening mee dat deze controle kijkt naar alle gedefinieerde/geconfigureerde hoofdmappen die zijn toegevoegd, niet alleen de hoofdmappen die momenteel in gebruik zijn. Met andere woorden, de map waarin je downloadclient downloads plaatst of voltooide downloads naartoe verplaatst, mag niet dezelfde map zijn die je hebt geconfigureerd als je hoofd/bibliotheek/eindbestemmingsmap voor media in de *arr-toepassing.
- Geconfigureerde hoofdmappen (ook wel bibliotheekmappen genoemd) vind je in [Instellingen => Mediabeheer => Hoofdmappen](/lidarr/settings/#root-folders)
- Een voorbeeld is als je downloads naar `\data\downloads` gaan en je hebt een hoofdmap ingesteld als `\data\downloads`.
- Het wordt aanbevolen om paden als `\data\media\` te gebruiken voor je hoofdmap/bibliotheek en `\data\downloads\` voor je downloads.
- Bekijk onze [Docker Guide](/docker-guide) en TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) voor meer informatie over de juiste en optimale padconfiguratie. Let op: de concepten zijn van toepassing op zowel docker als niet-docker

> Je downloadmap waar je downloadclient de downloads plaatst en je hoofd/bibliotheekmap MOETEN gescheiden zijn. \*Arr importeert het bestand/de bestanden van de downloadmap van je downloadclient naar je bibliotheek. De downloadclient mag niets verplaatsen of downloaden naar je bibliotheek.
{.is-warning}

#### Foutieve instellingen voor downloadclient

- De locatie waar je downloadclient bestanden downloadt, veroorzaakt problemen. Controleer de logs voor meer informatie. Dit kan te maken hebben met machtigingen of een poging om van Windows naar Linux of van Linux naar Windows te gaan zonder een externe padtoewijzing.

#### Foutieve externe padtoewijzing

- De locatie waar je downloadclient bestanden downloadt, veroorzaakt problemen. Controleer de logs voor meer informatie. Dit kan te maken hebben met machtigingen of een poging om van Windows naar Linux of van Linux naar Windows te gaan zonder een externe padtoewijzing. Zie [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) voor meer informatie.

#### Toestemmingsfout

- Lidarr (of de gebruiker waarop Lidarr wordt uitgevoerd) kan de locatie waar je downloadclient bestanden downloadt, niet openen. Dit is meestal een machtigingsprobleem.

#### Extern bestand is tijdens de verwerking gedeeltelijk verwijderd

- Een bestand dat toegankelijk is via een externe padtoewijzing lijkt te zijn verwijderd voordat de verwerking is voltooid.

#### Extern pad wordt gebruikt en importeren is mislukt

- Controleer je logs voor meer informatie. Raadpleeg onze [Troubleshooting Guides](/lidarr/troubleshooting).

### Voltooide/mislukte downloadverwerking

#### Voltooide downloadverwerking is uitgeschakeld

- Lidarr vereist `Voltooide downloadverwerking` om bestanden te kunnen importeren die zijn gedownload door de downloadclient. Het wordt aanbevolen om `Voltooide downloadverwerking` in te schakelen. (Het is standaard ingeschakeld voor nieuwe gebruikers.)

### Indexers

#### Geen indexers beschikbaar met automatisch zoeken ingeschakeld, Lidarr geeft geen automatische zoekresultaten

- Simpel gezegd heb je geen van je indexers ingesteld om automatisch zoeken toe te staan
- Ga naar `Instellingen => Indexers`, selecteer een indexer die je automatisch zoeken wilt toestaan en klik vervolgens op Opslaan.

#### Geen indexers beschikbaar met RSS-synchronisatie ingeschakeld, Lidarr haalt nieuwe releases niet automatisch op

- Lidarr gebruikt de RSS-feed om nieuwe releases op te pikken wanneer ze beschikbaar komen. Meer informatie hierover vind je hier
- Om dit probleem op te lossen, ga je naar `Instellingen => Indexers`, selecteer een indexer die je hebt en schakel RSS-synchronisatie in

#### Er zijn geen indexers ingeschakeld

- Lidarr vereist indexers om nieuwe releases te kunnen ontdekken. Lees de wiki voor instructies over het toevoegen van indexers.

### Ingeschakelde indexers ondersteunen geen zoeken

- Geen van de ingeschakelde indexers ondersteunt zoeken. Dit betekent dat Lidarr alleen nieuwe releases kan vinden via de RSS-feeds. Maar zoeken naar films (zowel automatisch zoeken als handmatig zoeken) zal nooit resultaten opleveren. De enige manier om dit te verhelpen, is door een andere indexer toe te voegen.

#### Geen indexers beschikbaar met interactief zoeken ingeschakeld

- Geen van de ingeschakelde indexers ondersteunt interactief zoeken. Dit betekent dat de applicatie alleen nieuwe releases kan vinden via de RSS-feeds of een automatische zoekopdracht.

#### Indexers zijn niet beschikbaar vanwege storingen

- Er zijn fouten opgetreden tijdens het gebruik van een van je indexers. Om het aantal herhalingspogingen te beperken, zal Lidarr de indexer gedurende steeds langere tijd niet gebruiken (tot 24 uur).
- Dit mechanisme wordt geactiveerd als Lidarr geen reactie van de indexer kon krijgen (dit kan worden veroorzaakt door DNS, proxy/VPN-verbinding, verificatie of een indexerprobleem) of als Lidarr het nzb/torrent-bestand niet kon ophalen van de indexer.
- Raadpleeg de logs om te bepalen wat voor soort fout het probleem veroorzaakt.
- Je kunt de waarschuwing voorkomen door de betreffende indexer uit te schakelen.
- Voer de test op de indexer uit om Lidarr te dwingen de indexer opnieuw te controleren. Houd er rekening mee dat de waarschuwing van de gezondheidscontrole niet altijd onmiddellijk verdwijnt.

#### Jackett All Endpoint gebruikt

- Het Jackett `/all` endpoint is handig, maar dat is het enige voordeel. Al het andere kan problemen veroorzaken, dus het is nu vereist om elke tracker afzonderlijk toe te voegen.
- [Zelfs de ontwikkelaars van Jackett zeggen dat het vermeden moet worden en niet gebruikt moet worden.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Het gebruik van het `/all` endpoint heeft geen voordelen, alleen nadelen:
  - je verliest de controle over specifieke indexerinstellingen (categorieën, zoekmodi, enz.)
  - het mixen van zoekmodi (IMDB, query, enz.) kan leiden tot lage kwaliteit resultaten
  - specifieke indexer-categorieën (>= 100000) kunnen niet worden gebruikt.
  - trage indexers vertragen het algehele resultaat
  - het totale aantal resultaten is beperkt tot 1000
  - als een van de trackers een fout retourneert, schakelt \*Arr deze uit en krijg je nu geen resultaten meer.

##### Oplossingen

- Voeg elke tracker handmatig toe in Jackett als een indexer in \*Arr
- Bekijk [Prowlarr](/prowlarr), dat indexers kan synchroniseren met \*Arr en afkomstig is van het Lidarr/Radarr/Readarr-ontwikkelingsteam.
- Bekijk [NZBHydra2](https://github.com/theotherp/nzbhydra2), dat indexers kan synchroniseren met \*Arr. Gebruik echter niet hun enkele aggregaatendpoint en gebruik `multi` als synchronisatie wordt gebruikt.

### Artiestmappen

#### Ontbrekende hoofdmap

- Deze fout wordt meestal geïdentificeerd als een artiest die op zoek is naar een hoofdmap, maar die hoofdmap is niet meer beschikbaar.
- Deze fout kan ook optreden als een lijst nog steeds naar een hoofdmap verwijst, maar die hoofdmap is niet meer beschikbaar.
- Als je deze waarschuwing wilt verwijderen, zoek dan het album dat nog steeds de oude hoofdmap gebruikt en bewerk het naar de juiste hoofdmap.

- De gemakkelijkste manier om de probleemartiest te vinden is:

  - Ga naar het tabblad Artiest (Bibliotheek)
  - Maak een aangepaste filter met het oude pad van de hoofdmap
  - Selecteer Massa bewerken in de bovenste balk en selecteer in het vervolgkeuzemenu Hoofdpaden het nieuwe hoofdpad waar je deze artiesten naartoe wilt verplaatsen.
  - Vervolgens krijg je een pop-up met de melding Wil je de mappen van de artiest verplaatsen naar 'hoofdpad'? Hierin staat ook Dit hernoemt ook de artiestmap volgens het artiestmapformaat in de instellingen. Selecteer gewoon Nee als je niet wilt dat Lidarr je bestanden verplaatst.
  - Voer de taak Check Health uit in Systeem => Taken

#### Lijsten zijn niet beschikbaar vanwege storingen

- Meestal betekent dit dat Lidarr niet langer via API of door in te loggen bij je gekozen lijstprovider kan communiceren. Je beste optie als het probleem aanhoudt, is om contact met hen op te nemen om ze uit te sluiten, omdat hun systemen soms overbelast kunnen zijn.
- Bekijk Systeem => Gebeurtenissen gefilterd op Waarschuwing (Waarschuwingen en Fouten) om de historische storingen te zien of controleer de logs voor details.
- Bekijk Systeem => Gebeurtenissen gefilterd op Waarschuwing (Waarschuwingen en Fouten) om de historische storingen te zien of controleer de logs voor details.

## Schijfruimte

- Deze sectie toont je beschikbare schijfruimte
- In Docker kan dit lastig zijn, omdat het meestal de beschikbare ruimte binnen je Docker-image laat zien

## Over

- Hier vind je informatie over je huidige installatie van Lidarr

## Meer informatie

- Startpagina: De startpagina van Lidarr
- Wiki: Je bent hier al
- Reddit: r/lidarr
- Discord: Doe mee aan onze discord
- Donaties: Als je vrijgevig bent en wilt doneren, klik dan hier
- Donaties aan Sonarr: Als je vrijgevig bent en wilt doneren aan het project dat het allemaal is begonnen, klik dan hier
- Bron: GitHub
- Functieverzoeken: Heb je een geweldig idee, laat het hier weten

# Taken

## Gepland

- Deze pagina toont alle geplande taken die Lidarr uitvoert

  - Toepassingscontrole-update - Dit wordt uitgevoerd volgens het weergegeven schema in de UI en controleert of Lidarr de meest recente versie heeft en activeert het update-script om Lidarr bij te werken. Instellingen => Update

  > Opmerking: Als je Docker gebruikt, wordt je container niet bijgewerkt, omdat er een nieuwe image moet worden gedownload.
{.is-warning}

  - Back-up - Dit maakt een back-up van de database van Lidarr volgens een vast schema. Meer informatie over back-ups vind je hier. Meer informatie over back-ups vind je in Systeem => Back-ups.
  - Controleer gezondheid - Controleer gezondheid wordt uitgevoerd volgens het weergegeven schema in de UI en controleert de algehele gezondheid van Lidarr. Zie de Wiki-entry