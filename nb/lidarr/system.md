# Getting Started with the Translation API

The Translation API allows you to easily integrate translation capabilities into your applications. This guide will walk you through the steps to get started with the Translation API.

## Prerequisites

Before you can start using the Translation API, you will need the following:

- A Google Cloud project with the Translation API enabled. You can create a new project or use an existing one.
- API credentials to authenticate your requests. You can create credentials by creating a service account or using an API key.

## Enable the Translation API

To enable the Translation API for your project, follow these steps:

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Select your project from the project dropdown.
3. In the sidebar, click on "APIs & Services" and then "Library".
4. In the search bar, type "Translation API" and select the API from the results.
5. Click on the "Enable" button to enable the Translation API for your project.

## Set up API Credentials

To authenticate your requests to the Translation API, you will need to set up API credentials. There are two types of credentials you can use: service account credentials or API key.

### Service Account Credentials

To create service account credentials, follow these steps:

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Select your project from the project dropdown.
3. In the sidebar, click on "APIs & Services" and then "Credentials".
4. Click on the "Create credentials" button and select "Service account".
5. Fill in the required information and click on the "Create" button.
6. Your service account credentials will be created. Download the JSON file containing your credentials.

### API Key

To create an API key, follow these steps:

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Select your project from the project dropdown.
3. In the sidebar, click on "APIs & Services" and then "Credentials".
4. Click on the "Create credentials" button and select "API key".
5. Your API key will be created. Make sure to keep it secure.

## Make a Translation Request

Now that you have enabled the Translation API and set up your API credentials, you can make a translation request. The Translation API supports translating text between thousands of language pairs.

To make a translation request, send a POST request to the following endpoint:

```
https://translation.googleapis.com/language/translate/v2
```

Include your API credentials in the request headers or query parameters. The request body should contain the text you want to translate, the source language, and the target language.

Here is an example request using cURL:

```bash
curl -X POST \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "q": "Hello, world!",
    "source": "en",
    "target": "fr"
  }' \
  "https://translation.googleapis.com/language/translate/v2"
```

Replace `YOUR_API_KEY` with your API key or the path to your service account JSON file.

## Next Steps

Congratulations! You have successfully set up the Translation API and made your first translation request. You can now explore the [Translation API documentation](https://cloud.google.com/translate/docs) to learn more about the available features and options.

{/*examples*/}

---
title: Lidarr System
description: 
published: true
date: 2022-10-31T04:35:13.645Z
tags: lidarr, needs-love, system
editor: markdown
dateCreated: 2021-06-14T21:36:28.225Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Status](#status)
  - [Helse](#helse)
    - [Systemadvarsler](#systemadvarsler)
      - [Grensen er ikke en gyldig utgavegren](#grensen-er-ikke-en-gyldig-utgavegren)
      - [Oppdater til .NET-versjon](#oppdater-til-net-versjon)
        - [Fikse Docker-installasjoner](#fikse-docker-installasjoner)
        - [Fikse frittstående installasjoner](#fikse-frittstående-installasjoner)
      - [Gjeldende installert mono-versjon er gammel og ikke støttet](#gjeldende-installert-mono-versjon-er-gammel-og-ikke-støttet)
      - [Gjeldende installert SQLite-versjon støttes ikke](#gjeldende-installert-sqlite-versjon-støttes-ikke)
      - [Ny oppdatering er tilgjengelig](#ny-oppdatering-er-tilgjengelig)
      - [Kan ikke installere oppdatering fordi oppstartsmappen ikke kan skrives til av brukeren](#kan-ikke-installere-oppdatering-fordi-oppstartsmappen-ikke-kan-skrives-til-av-brukeren)
      - [Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering](#oppdatering-vil-ikke-være-mulig-for-å-forhindre-sletting-av-appdata-ved-oppdatering)
      - [Grensen er for en tidligere versjon](#grensen-er-for-en-tidligere-versjon)
      - [Kunne ikke koble til signalR](#kunne-ikke-koble-til-signalr)
        - [NGINX](#nginx)
        - [Apache](#apache)
        - [Caddy](#caddy)
      - [Kunne ikke løse IP-adressen for konfigurert proxyvert](#kunne-ikke-løse-ip-adressen-for-konfigurert-proxyvert)
      - [Proxy mislyktes test](#proxy-mislyktes-test)
      - [Systemklokken er mer enn 1 dag feil](#systemklokken-er-mer-enn-1-dag-feil)
      - [Mono Legacy TLS er aktivert](#mono-legacy-tls-er-aktivert)
      - [Mono og x86-bygg avsluttes](#mono-og-x86-bygg-avsluttes)
      - [FPcalc må oppdateres](#fpcalc-må-oppdateres)
    - [Nedlastingsklienter](#nedlastingsklienter)
      - [Ingen nedlastingsklient er tilgjengelig](#ingen-nedlastingsklient-er-tilgjengelig)
      - [Kan ikke kommunisere med nedlastingsklient](#kan-ikke-kommunisere-med-nedlastingsklient)
      - [Nedlastingsklienter er utilgjengelige på grunn av feil](#nedlastingsklienter-er-utilgjengelige-på-grunn-av-feil)
      - [Aktiver håndtering av fullførte nedlastinger](#aktiver-håndtering-av-fullførte-nedlastinger)
      - [Docker dårlig ekstern stioppkobling](#docker-dårlig-ekstern-stioppkobling)
      - [Nedlasting til rotmappen](#nedlasting-til-rotmappen)
      - [Feil nedlastingsklientinnstillinger](#feil-nedlastingsklientinnstillinger)
      - [Feil ekstern stioppkobling](#feil-ekstern-stioppkobling)
      - [Tillatelsesfeil](#tillatelsesfeil)
      - [Ekstern fil ble fjernet under behandling](#ekstern-fil-ble-fjernet-under-behandling)
      - [Brukte fjernsti og import mislyktes](#brukte-fjernsti-og-import-mislyktes)
    - [Fullførte/mislukte nedlastingshåndtering](#fullførtemislukte-nedlastingshåndtering)
      - [Fullført nedlastingshåndtering er deaktivert](#fullført-nedlastingshåndtering-er-deaktivert)
    - [Indekser](#indekser)
      - [Ingen indekser er tilgjengelige med automatisk søk aktivert, Lidarr vil ikke gi noen automatisk søkresultater](#ingen-indekser-er-tilgjengelige-med-automatisk-søk-aktivert-lidarr-vil-ikke-gi-noen-automatisk-søkresultater)
      - [Ingen indekser er tilgjengelige med RSS-synkronisering aktivert, Lidarr vil ikke hente nye utgivelser automatisk](#ingen-indekser-er-tilgjengelige-med-rss-synkronisering-aktivert-lidarr-vil-ikke-hente-nye-utgivelser-automatisk)
      - [Ingen indekser er aktivert](#ingen-indekser-er-aktivert)
    - [Aktiverte indekser støtter ikke søk](#aktiverte-indekser-støtter-ikke-søk)
      - [Ingen indekser er tilgjengelige med interaktivt søk aktivert](#ingen-indekser-er-tilgjengelige-med-interaktivt-søk-aktivert)
      - [Indekser er utilgjengelige på grunn av feil](#indekser-er-utilgjengelige-på-grunn-av-feil)
      - [Jackett bruker alle endepunkter](#jackett-bruker-alle-endepunkter)
        - [Løsninger](#løsninger)
    - [Artistmapper](#artistmapper)
      - [Mangler rotmappe](#mangler-rotmappe)
      - [Lister er utilgjengelige på grunn av feil](#lister-er-utilgjengelige-på-grunn-av-feil)
  - [Diskplass](#diskplass)
  - [Om](#om)
  - [Mer informasjon](#mer-informasjon)
- [Oppgaver](#oppgaver)
  - [Planlagt](#planlagt)
  - [Kø](#kø)
- [Sikkerhetskopi](#sikkerhetskopi)
- [Oppdateringer](#oppdateringer)
- [Hendelser](#hendelser)
- [Loggfiler](#loggfiler)

> Advarsel: Denne siden er under utvikling og er for øyeblikket et utkast basert på Readarr
{.is-danger}

# Status

## Helse

Denne siden inneholder en liste over helsekontrollfeil. Disse helsekontrollene utføres periodisk av Lidarr og ved visse hendelser. Advarsler og feil som oppstår, vises her for å gi råd om hvordan du løser dem.

### Systemadvarsler

#### Grensen er ikke en gyldig utgavegren

Grensen du har satt er ikke en gyldig utgavegren. Du vil ikke motta oppdateringer. Vennligst endre til en av de [nåværende utgavegrenene](/lidarr/faq#how-do-i-update-lidarr)

#### Oppdater til .NET-versjon

{#update-to-net-core-version}

- Nyere versjoner av Lidarr er rettet mot .NET6 eller nyere. Vi vil ikke lenger tilby eldre mono-bygg etter at 1.0 er utgitt. Du kjører en av disse eldre byggene, men plattformen din støtter .NET.

##### Fikse Docker-installasjoner

- Trekk inn beholderen på nytt

##### Fikse frittstående installasjoner

- Sikkerhetskopier konfigurasjonen din før neste trinn.
- Dette bør bare skje på Linux-verter. Ikke installer .NET runtime eller SDK fra Microsoft.
- For å rette opp, last ned riktig bygg for arkitekturen din og erstatt de eksisterende binærene (programmet)
- Kort sagt må du slette de eksisterende binærene (innholdet eller mappen /opt/Lidarr) og erstatte med innholdet i .tar.gz du nettopp lastet ned.

> IKKE BARE PAKK UT NEDLASTINGEN OVER DE EKSISTERENDE BINÆRENE.
> DU MÅ FØRST SLETTE DE GAMLE.
{.is-warning}

- Nedenfor er et fellesskapsutviklet skript for å fjerne mono-installasjonen og erstatte den med .NET-installasjonen. Bidrag og rettelser er velkomne.
- Dette antar at du er på `master` Lidarr-grenen, oppdater variabelen om nødvendig
- Dette antar at Lidarr kjører som brukeren `lidarr`, oppdater variablene om nødvendig
- Dette antar at Lidarr er installert på `/opt/Lidarr`, oppdater variablene om nødvendig

```bash
#!/bin/bash
## Brukervariabler
installdir="/opt/Lidarr"
APPUSER="lidarr"
gren="master"
## /Brukervariabler
app="lidarr"
ARCH=$(dpkg --print-architecture)
# Stopp \*arr
sudo systemctl stop $app
# få ark
dlbase="https://$app.servarr.com/v1/update/$gren/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "Arkitektur støttes ikke"
    exit 1
    ;;
esac
echo "Laster ned..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Installasjonsfiler lastet ned og utpakket"
echo "Flytter eksisterende installasjon"
sudo mv "$installdir/" "$installdir.old/"
echo "Installerer..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "App installert"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### Gjeldende installert mono-versjon er gammel og ikke støttet

- Lidarr er skrevet i .NET og krever Mono for å kjøre på veldig gamle ARM-prosessorer. Vær oppmerksom på at Mono-bygg ikke lenger støttes etter v1.0
- Mono 5.20 er det absolutte minimum for Lidarr.
- Oppgraderingsprosedyren for Mono varierer per plattform.

#### Gjeldende installert SQLite-versjon støttes ikke

- Lidarr lagrer dataene sine i en SQLite-database. SQLite3-biblioteket installert på systemet ditt er for gammelt. Lidarr krever minst versjon 3.9.0. Merk at Lidarr bruker `libSQLite3.so`, som kan være inkludert eller ikke i en oppgraderingspakke for SQLite3.

#### Ny oppdatering er tilgjengelig

- Fryd deg, utviklerne har gitt ut en ny oppdatering. Dette betyr generelt sett fantastiske nye funksjoner og løste feil (ikke sant?). Tydeligvis har du ikke aktivert automatisk oppdatering, så du må finne ut hvordan du oppdaterer på plattformen din. Å trykke på Install-knappen på siden `System => Oppdateringer` er sannsynligvis et godt utgangspunkt.

> Denne advarselen vises ikke hvis gjeldende versjon er mindre enn 14 dager gammel
{.is-info}

#### Kan ikke installere oppdatering fordi oppstartsmappen ikke kan skrives til av brukeren

- Dette betyr at Lidarr ikke vil kunne oppdatere seg selv. Du må oppdatere Lidarr manuelt eller angi tillatelsene for Lidarrs oppstartsmappe (installasjonsmappen) slik at Lidarr kan oppdatere seg selv.

#### Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering

- Lidarr oppdaget at AppData-mappen for operativsystemet ditt er plassert inne i mappen som inneholder Lidarr-binærene. Normalt sett ville det være `C:\ProgramData` for Windows og `~/.config` for Linux.

- Se på `System => Info` for å se gjeldende AppData- og oppstartsmapper.
- Dette betyr at Lidarr ikke vil kunne oppdatere seg selv uten å risikere tap av data.
- Hvis du bruker Linux, må du sannsynligvis endre hjemmemappen for brukeren som kjører Lidarr, og kopiere innholdet i den gjeldende `~/.config/Lidarr`-mappen for å bevare databasen din.

#### Grensen er for en tidligere versjon

- Oppdateringsgrensen som er satt i `Innstillinger => Generelt`, er for en tidligere versjon av Lidarr, og derfor vil instansen ikke se riktig oppdateringsinformasjon i strømmen `System => Oppdateringer` og kan ikke motta nye oppdateringer når de er tilgjengelige.

#### Kunne ikke koble til signalR

- signalR driver dynamiske oppdateringer av brukergrensesnittet, så hvis nettleseren din ikke kan koble til signalR på serveren din, vil du ikke se noen sanntidsoppdateringer i brukergrensesnittet.

- Den vanligste forekomsten av dette er bruk av en omvendt proxy eller Cloudflare
- Cloudflare trenger aktiverte websockets.

##### NGINX

- Nginx krever følgende tillegg til plasseringen for appen:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Pass på at du ikke inkluderer `proxy_set_header Connection "Upgrade";` som foreslått av nginx-dokumentasjonen. DETTE VIL IKKE FUNGERE
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache

- For Apache2 omvendt proxy må du aktivere følgende moduler: proxy, proxy_http og proxy_wstunnel. Deretter legger du til denne direktivet for websockets i vhost-konfigurasjonen din:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8686/$1 [P,L]
```

##### Caddy

- For Caddy (V1) bruk dette:
- Merk: Du må også legge til websockets-direktivet i Lidarr-konfigurasjonen

```none
 proxy /lidarr 127.0.0.1:8686 {
     websocket
     transparent
 }
```

#### Kunne ikke løse IP-adressen for konfigurert proxyvert

- Gjennomgå proxyinnstillingene dine og sørg for at de er nøyaktige
- Sørg for at proxyen din er aktiv, kjører og tilgjengelig

#### Proxy mislyktes test

- Den konfigurerte proxyen mislyktes i å teste vellykket, gjennomgå HTTP-feilen som ble oppgitt og/eller sjekk loggene for mer informasjon.

#### Systemklokken er mer enn 1 dag feil

- Systemklokken er mer enn 1 dag feil. Planlagte oppgaver kan ikke kjøre riktig før tiden er korrigert
- Gjennomgå systemklokken og sørg for at den er synkronisert med en autoritativ tidsserver og er nøyaktig

#### Mono Legacy TLS er aktivert

- Mono 4.x tls-omgåelse er fortsatt aktivert, vurder å fjerne miljøalternativet `MONO_TLS_PROVIDER=legacy`

#### Mono og x86-bygg avsluttes

- Mono- og x86-bygg vil ikke lenger støttes i neste bygg av programmet. Hvis du får denne feilen, kjører du enten mono-versjonen av programmet eller x86-versjonen. Dessverre, på grunn av økende vanskeligheter med utviklingsstøtte for disse eldre versjonene, vil vi avslutte støtten for dem og dermed utgivelser for dem i fremtiden. Det anbefales derfor å oppgradere til et støttet operativsystem som ikke krever verken x86 eller mono. Du kan også vurdere å bruke Docker for dine behov.

#### FPcalc må oppdateres

{#fpcalc-upgrade}

- Lidarr bruker chromaprint lydfingeravtrykk for å identifisere spor. Dette avhenger av en ekstern binær `fpcalc`, som distribueres med Lidarr v1 for Windows, Linux og macOS, men må leveres uavhengig på freeBSD.
- Sørg for at den medfølgende fpcalc-binæren som følger med Lidarr, er kjørbar (755 tillatelser). Denne finnes i Lidarrs installasjonsmappe (f.eks. `/opt/Lidarr/fpcalc`). Hvis den ikke er kjørbar, rett opp tillatelsene med følgende kommando og start deretter Lidarr på nytt.
  - Merk at `sudo` kan være nødvendig for å fikse dette, eller banen til Lidarrs binærmappe kan være annerledes avhengig av miljøet og oppsettet ditt.

```bash
chmod +x /opt/Lidarr/fpcalc
```

> Informasjonen nedenfor gjelder bare for eldre v0.8.0-bygg.
{.is-info}

- For å fikse dette på en nativ Linux-instans, installer den passende pakken ved hjelp av pakkehåndtereren din, og sørg for at fpcalc er i PATH (dette kan sjekkes ved å bruke kommandoen `which fpcalc` og verifisere at riktig plassering for fpcalc returneres):

| Distribusjon  |       Pakke        |
| :-----------: | :------------------: |
| Debian/Ubuntu | libchromaprint-tools |
| Fedora/CentOS |  chromaprint-tools   |
|     Arch      |     chromaprint      |
|   OpenSUSE    |  chromaprint-fpcalc  |
|   Synology    |     chromaprint      |

### Nedlastingsklienter

#### Ingen nedlastingsklient er tilgjengelig

- En riktig konfigurert og aktivert nedlastingsklient er nødvendig for at Lidarr skal kunne laste ned medier. Siden Lidarr støtter forskjellige nedlastingsklienter, bør du bestemme hvilken som passer best for dine behov. Hvis du allerede har en nedlastingsklient installert, bør du konfigurere Lidarr til å bruke den og opprette en kategori. Se `Innstillinger => Nedlastingsklient`.

#### Kan ikke kommunisere med nedlastingsklient

- Lidarr kunne ikke kommunisere med den konfigurerte nedlastingsklienten. Vennligst bekreft at nedlastingsklienten er operativ og dobbeltsjekk URLen. Dette kan også indikere en autentiseringsfeil.
- Dette skyldes vanligvis en feil konfigurert nedlastingsklient. Ting du vanligvis kan sjekke:
  - IP-adressen til nedlastingsklienten din - hvis alt er på samme fysiske maskin, er dette vanligvis `127.0.0.1`
  - Portnummeret som nedlastingsklienten din bruker - disse er fylt ut med standardportnummeret, men hvis du har endret det, må du ha det samme nummeret skrevet inn i Lidarr.
  - Sørg for at SSL-kryptering ikke er aktivert hvis du bruker både Lidarr-instansen og nedlastingsklienten din i et lokalt nettverk (dvs. over vanlig HTTP). Se SSL-FAQ-en for mer informasjon.

#### Nedlastingsklienter er utilgjengelige på grunn av feil

- En eller flere av nedlastingsklientene dine svarer ikke på forespørslene som blir sendt av Lidarr. Derfor har Lidarr bestemt seg for å midlertidig slutte å spørre nedlastingsklienten på den normale 1-minutters syklusen, som vanligvis brukes til å spore aktive nedlastinger og importere ferdige nedlastinger. Imidlertid vil Lidarr fortsette å prøve å sende nedlastinger til klienten, men vil mest sannsynlig mislykkes.
- Du bør inspisere `System => Logger` for å se hva årsaken er til feilene.
- Hvis du ikke lenger bruker denne nedlastingsklienten, deaktiver den i Lidarr for å unngå feilene.

#### Aktiver håndtering av fullførte nedlastinger

- Lidarr krever at håndtering av fullførte nedlastinger er aktivert for å kunne importere filer som ble lastet ned av nedlastingsklienten. Det anbefales å aktivere håndtering av fullførte nedlastinger. (Håndtering av fullførte nedlastinger er aktivert som standard for nye brukere.)

#### Docker dårlig ekstern stioppkobling

- Denne feilen er vanligvis knyttet til dårlige Docker-stier i enten nedlastingsklienten eller Lidarr.

- Et eksempel på dårlige (inkonsekvente) stier kan være:
  - Nedlastingsklient: `/mnt/user/downloads:/downloads`
  - Lidarr:   `/mnt/user/downloads:/data`
- I dette eksemplet plasserer nedlastingsklienten nedlastinger i `/downloads` og forteller Lidarr når det er ferdig at den ferdige boken er i `/downloads`. Lidarr kommer deretter og sier "Ok, flott, la meg sjekke i `/downloads`." Vel, inne i Lidarr har du ikke tildelt en `/downloads`-sti, du har tildelt en `/data`-sti, så det kaster denne feilen.
- Den enkleste løsningen på dette er KONSISTENS - hvis du bruker en ordning i nedlastingsklienten din, bruk den over hele linjen.

- Team Lidarr er veldig glad i å bare bruke /data.

  - Nedlastingsklient: `/mnt/user/data/downloads:/data/downloads`
  - Lidarr: `/mnt/user/data:/data`

- Nå kan du innenfor nedlastingsklienten angi hvor i `/data` du vil plassere nedlastingen din, dette varierer avhengig av klienten, men du bør kunne fortelle den "Ja, nedlastingsklient, plasser filene mine i `/data/downloads/movies`", og siden du brukte `/data` i Lidarr, når nedlastingsklienten forteller Lidarr at den er ferdig, vil Lidarr komme og si "Flott, jeg har en `/data` og jeg kan også se `/data/downloads/movies`, alt er bra i verden."
- Det er mange flotte veiledninger: vår wiki [Docker Guide](/docker-guide) og TRaSHs [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Disse veiledningene legger stor vekt på hardlinker og atomiske flyttinger, men det generelle konseptet med containere og hvordan stibasering fungerer, er kjernen i disse diskusjonene.
- Hvis du krysser operativsystemer eller bruker native og Docker, trenger du en ekstern stioppkobling. Se [TRaSHs Remote Path Guide for Radarr](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) og [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/) for mer informasjon.

#### Nedlasting til rotmappen

{#downloads-in-root-folder}

- Innenfor applikasjonen defineres en rotmappe som den konfigurerte mediebibliotekmappen. Dette er ikke rotmappen til et monteringspunkt. Nedlastingsklienten din laster ned ufullstendige eller fullførte nedlastinger (eller flytter fullførte nedlastinger) til rotmappen (biblioteket) din.
- Dette forårsaker ofte problemer - inkludert tap av data - og bør ikke gjøres. For å løse dette, endre nedlastingsklienten slik at den ikke plasserer nedlastinger i rotmappen din. Merk at 'plassering' også inkluderer om nedlastingsklientens kategori er satt til rotmappen din, eller om NZBGet/SABnzbd har sortering aktivert og sorterer til rotmappen din.
- Vær oppmerksom på at denne sjekken ser på alle definerte/konfigurerte rotmapper som er lagt til, ikke bare rotmapper som for øyeblikket er i bruk. Med andre ord, mappen der nedlastingsklienten din laster ned eller flytter fullførte nedlastinger til, bør ikke være den samme mappen du har konfigurert som rot-/biblioteks-/endelig destinasjonsmappe for medier i *arr-applikasjonen.
- Konfigurerte rotmapper (også kjent som biblioteksmapper) finner du i [Innstillinger => Mediebehandling => Rotmapper](/lidarr/settings/#root-folders)
- Et eksempel er hvis nedlastingen din går til `\data\downloads`, så har du en rotmappe satt som `\data\downloads`.
- Det anbefales å bruke stier som `\data\media\` for rotmappen/biblioteket ditt og `\data\downloads\` for nedlastingen din.
- Gjennomgå vår [Docker Guide](/docker-guide) og TRaSHs [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mer informasjon om riktig og optimal stikonfigurasjon. Merk at konseptene gjelder både Docker og ikke-Docker

> Nedlastingsmappen der nedlastingsklienten din plasserer nedlastingen og rotmappen/biblioteket ditt MÅ være separate. \*Arr vil importere filen(e) fra nedlastingsklientens mappe til biblioteket ditt. Nedlastingsklienten skal ikke flytte eller laste ned noe til biblioteket ditt.
{.is-warning}

#### Feil nedlastingsklientinnstillinger

- Plasseringen der nedlastingsklienten din laster ned filer, forårsaker problemer. Sjekk loggene for mer informasjon. Dette kan være tillatelser eller forsøk på å gå fra Windows til Linux eller Linux til Windows uten en ekstern stioppkobling.

#### Feil ekstern stioppkobling

- Plasseringen der nedlastingsklienten din laster ned filer, forårsaker problemer. Sjekk loggene for mer informasjon. Dette kan være tillatelser eller forsøk på å gå fra Windows til Linux eller Linux til Windows uten en ekstern stioppkobling. Se [TRaSHs Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mer informasjon.

#### Tillatelsesfeil

- Lidarr (eller brukeren Lidarr kjører som) kan ikke få tilgang til plasseringen der nedlastingsklienten din laster ned filer. Dette er vanligvis et tillatelsesproblem.

#### Ekstern fil ble fjernet under behandling

- En fil som er tilgjengelig via en ekstern stioppkobling, ser ut til å ha blitt fjernet før behandlingen var fullført.

#### Brukte fjernsti og import mislyktes

- Sjekk loggene for mer informasjon. Se vår [Feilsøkingsguide](/lidarr/troubleshooting).

### Fullførte/mislukte nedlastingshåndtering

#### Fullført nedlastingshåndtering er deaktivert

- Lidarr krever at `Fullført nedlastingshåndtering` er aktivert for å kunne importere filer som ble lastet ned av nedlastingsklienten. Det anbefales å aktivere `Fullført nedlastingshåndtering`. (Det er aktivert som standard for nye brukere.)

### Indekser

#### Ingen indekser er tilgjengelige med automatisk søk aktivert, Lidarr vil ikke gi noen automatisk søkresultater

- Enkelt sagt har du ikke noen av indeksene dine satt til å tillate automatisk søk
- Gå til `Innstillinger => Indekser`, velg en indeks du vil tillate automatisk søk, og klikk deretter på Lagre.

#### Ingen indekser er tilgjengelige med RSS-synkronisering aktivert, Lidarr vil ikke hente nye utgivelser automatisk

- Lidarr bruker RSS-feeden til å plukke opp nye utgivelser etter hvert som de kommer. Mer informasjon om dette finner du her
- For å rette opp dette problemet går du til `Innstillinger => Indekser`, velger en indeks du har og aktiverer RSS-synkronisering

#### Ingen indekser er aktivert

- Lidarr krever indekser for å kunne oppdage nye utgivelser. Les wikien for instruksjoner om hvordan du legger til indekser.

### Aktiverte indekser støtter ikke søk

- Ingen av indeksene du har aktivert, støtter søk. Dette betyr at Lidarr bare vil kunne finne nye utgivelser via RSS-feedene. Men søk etter bøker (enten automatisk søk eller manuelt søk) vil aldri gi noen resultater. Den eneste måten å rette det på er å legge til en annen indeks.

#### Ingen indekser er tilgjengelige med interaktivt søk aktivert

- Ingen av indeksene du har aktivert, støtter interaktivt søk. Dette betyr at applikasjonen bare vil kunne finne nye utgivelser via RSS-feedene eller et automatisk søk.

#### Indekser er utilgjengelige på grunn av feil

- Feil oppstod mens Lidarr prøvde å bruke en av indeksene dine. For å begrense forsøkene, vil Lidarr ikke bruke indeksen i en økende tidsperiode (opptil 24 timer).
- Denne mekanismen utløses hvis Lidarr ikke klarte å få et svar fra indeksen (kan skyldes DNS, proxy/VPN-tilkobling, autentisering eller en indeksfeil), eller klarte ikke å hente nzb-/torrent-filen fra indeksen.
- Inspiser loggene for å finne ut hvilken type feil som forårsaker problemet.
- Du kan forhindre advarselen ved å deaktivere den berørte indeksen.
- Kjør testen på indeksen for å tvinge Lidarr til å sjekke indeksen på nytt, vær oppmerksom på at helsekontrolladvarselen ikke alltid forsvinner umiddelbart.

#### Jackett bruker alle endepunkter

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet er potensielle problemer, så det er nå nødvendig å legge til hver enkelt tracker individuelt.
- [Selv Jacketts utviklere sier at det bør unngås og ikke bør brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Bruk av `/all`-endepunktet har ingen fordeler, bare ulemper:
  - du mister kontrollen over indeksspesifikke innstillinger (kategorier, søkemåter, osv.)
  - blanding av søkemåter (IMDB, spørring, osv.) kan gi dårlige resultater
  - indeksspesifikke kategorier (>= 100000) kan ikke brukes.
  - treg indekser vil bremse ned den generelle resultatet
  - totalt antall resultater er begrenset til 1000
  - hvis en av sporerne returnerer en feil, vil \*Arr deaktivere den, og nå får du ingen resultater.

##### Løsninger

- Legg til hver sporer manuelt i Jackett som en indeks i \*Arr
- Sjekk ut [Prowlarr](/prowlarr), som kan synkronisere indekser til \*Arr, og fra Lidarr/Radarr/Readarr-utviklingsteamet.
- Sjekk ut [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indekser til \*Arr. Men ikke bruk deres enkeltstående aggregatendepunkt, bruk `multi` hvis synkroniseringen skal brukes.

### Artistmapper

#### Mangler rotmappe

- Denne feilen identifiseres vanligvis hvis en artist leter etter en rotmappe, men den rotmappen er ikke lenger tilgjengelig.
- Denne feilen kan også oppstå hvis en liste fremdeles peker på en rotmappe, men den rotmappen ikke lenger er tilgjengelig.
- Hvis du vil fjerne denne advarselen, finn bare albumet som fremdeles bruker den gamle rotmappen, og rediger det til riktig rotmappe.

- En enkel måte å finne problemartisten på er å:

  - Gå til fanen Artist (Bibliotek)
  - Opprett et tilpasset filter med den gamle rotmappen
  - Velg masseendring i toppmenyen, og velg den nye rotbanen du vil flytte disse artistene til fra rullegardinmenyen Rotbaner.
  - Deretter får du en popup som sier Vil du flytte artistmappene til 'rotbanen'? Dette vil også si Dette vil også gi nytt navn til artistmappen i henhold til artistmappens format i innstillingene. Velg bare Nei hvis du ikke vil at Lidarr skal flytte filene dine.
  - Kjør helsekontrolloppgaven i System => Oppgaver

#### Lister er utilgjengelige på grunn av feil

- Dette betyr vanligvis at Lidarr ikke lenger kan kommunisere via API eller ved å logge inn på den valgte listeleverandøren. Hvis problemet vedvarer, er det beste alternativet å kontakte dem for å utelukke dem, da systemene deres kan være overbelastet fra tid til annen.
- Gjennomgå System => Hendelser filtrert for advarsel (advarsel og feil) for å se de historiske feilene eller sjekk loggene for detaljer.
- Gjennomgå System => Hendelser filtrert for advarsel (advarsel og feil) for å se de historiske feilene eller sjekk loggene for detaljer.

## Diskplass

- Denne delen viser tilgjengelig diskplass
- I Docker kan dette