---
title: Radarr System
description: 
published: true
date: 2022-10-19T22:59:06.531Z
tags: radarr, needs-love
editor: markdown
dateCreated: 2021-05-25T02:28:35.194Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Status](#status)
  - [Helse](#helse)
    - [Systemadvarsler](#systemadvarsler)
      - [Grenen er ikke en gyldig utgavegren](#grenen-er-ikke-en-gyldig-utgavegren)
      - [Oppdater til .NET-versjon](#oppdater-til-net-versjon)
        - [Fikse Docker-installasjoner](#fikse-docker-installasjoner)
        - [Fikse FreeBSD-installasjoner](#fikse-freebsd-installasjoner)
        - [Fikse frittstående installasjoner](#fikse-frittstående-installasjoner)
      - [Gjeldende installert mono-versjon er gammel og ikke støttet](#gjeldende-instalert-mono-versjon-er-gammel-og-ikke-støttet)
      - [Gjeldende installert SQLite-versjon støttes ikke](#gjeldende-instalert-sqlite-versjon-støttes-ikke)
      - [Database mislyktes integritetssjekk](#database-mislyktes-integritetssjekk)
      - [Ny oppdatering er tilgjengelig](#ny-oppdatering-er-tilgjengelig)
      - [Kan ikke installere oppdatering fordi oppstartsmappen ikke kan skrives til av brukeren](#kan-ikke-installere-oppdatering-fordi-oppstartsmappen-ikke-kan-skrives-til-av-brukeren)
      - [Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering](#oppdatering-vil-ikke-være-mulig-for-å-forhindre-sletting-av-appdata-ved-oppdatering)
      - [Grenen er for en tidligere versjon](#grenen-er-for-en-tidligere-versjon)
      - [Kunne ikke koble til signalR](#kunne-ikke-koble-til-signalr)
        - [Nginx](#nginx)
        - [Apache2](#apache2)
        - [Caddy](#caddy)
      - [Kunne ikke løse IP-adressen for konfigurert proxyvert](#kunne-ikke-løse-ip-adressen-for-konfigurert-proxyvert)
      - [Proxy mislyktes test](#proxy-mislyktes-test)
      - [Systemtiden er mer enn 1 dag feil](#systemtiden-er-mer-enn-1-dag-feil)
      - [PTP-indeksinnstillinger er utdaterte](#ptp-indeksinnstillinger-er-utdaterte)
      - [Mono- og x86-bygg avsluttes](#mono-og-x86-bygg-avsluttes)
    - [Nedlastingsklienter](#nedlastingsklienter)
      - [Ingen nedlastingsklient er tilgjengelig](#ingen-nedlastingsklient-er-tilgjengelig)
      - [Kan ikke kommunisere med nedlastingsklient](#kan-ikke-kommunisere-med-nedlastingsklient)
      - [Nedlastingsklienter er utilgjengelige på grunn av feil](#nedlastingsklienter-er-utilgjengelige-på-grunn-av-feil)
      - [Aktiver håndtering av fullførte nedlastinger](#aktiver-håndtering-av-fullførte-nedlastinger)
      - [Docker dårlig ekstern stioppføring](#docker-dårlig-ekstern-stioppføring)
      - [Nedlasting til rotmappen](#nedlasting-til-rotmappen)
      - [Dårlige innstillinger for nedlastingsklient](#dårlige-innstillinger-for-nedlastingsklient)
      - [Dårlig ekstern stioppføring](#dårlig-ekstern-stioppføring)
      - [Tillatelsesfeil](#tillatelsesfeil)
      - [Ekstern fil ble fjernet under behandling](#ekstern-fil-ble-fjernet-under-behandling)
      - [Brukte fjernsti og import mislyktes](#brukte-fjernsti-og-import-mislyktes)
    - [Fullførte/mislukte nedlastingshåndtering](#fullførtemislukte-nedlastingshåndtering)
      - [Fullført nedlastingshåndtering er deaktivert](#fullført-nedlastingshåndtering-er-deaktivert)
    - [Indekser](#indekser)
      - [Ingen indekser er tilgjengelige med automatisk søk aktivert, Radarr vil ikke gi noen automatiske søkeresultater](#ingen-indekser-er-tilgjengelige-med-automatisk-søk-aktivert-radarr-vil-ikke-gi-noen-automatiske-søkeresultater)
      - [Ingen indekser er tilgjengelige med RSS-synkronisering aktivert, Radarr vil ikke hente nye utgivelser automatisk](#ingen-indekser-er-tilgjengelige-med-rss-synkronisering-aktivert-radarr-vil-ikke-hente-nye-utgivelser-automatisk)
      - [Ingen indekser er aktivert](#ingen-indekser-er-aktivert)
    - [Aktiverte indekser støtter ikke søk](#aktiverte-indekser-støtter-ikke-søk)
      - [Ingen indekser er tilgjengelige med interaktivt søk aktivert](#ingen-indekser-er-tilgjengelige-med-interaktivt-søk-aktivert)
      - [Indekser er utilgjengelige på grunn av feil](#indekser-er-utilgjengelige-på-grunn-av-feil)
      - [Jackett bruker alle endepunkter](#jackett-bruker-alle-endepunkter)
        - [Løsninger](#løsninger)
    - [Filmapper](#filmapper)
      - [Mangler rotmappe](#mangler-rotmappe)
    - [Filmer](#filmer)
      - [Film ble fjernet fra TMDb](#film-ble-fjernet-fra-tmdb)
      - [Lister er utilgjengelige på grunn av feil](#lister-er-utilgjengelige-på-grunn-av-feil)
    - [Varsler](#varsler)
    - [Discord som Slack-varsling](#discord-som-slack-varsling)
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

# Status

## Helse

- Denne siden inneholder en liste over helsekontrollfeil. Disse helsekontrollene utføres periodisk av Radarr og ved visse hendelser. Advarslene og feilene som oppstår, vises her for å gi råd om hvordan du løser dem.

### Systemadvarsler

#### Grenen er ikke en gyldig utgavegren

- Grenen du har satt er ikke en gyldig utgavegren. Du vil ikke motta oppdateringer. Vennligst endre til en av de [nåværende utgavegrenene](/radarr/faq#how-do-i-update-radarr).

#### Oppdater til .NET-versjon

{#update-to-net-core-version}

- Nyere versjoner av Radarr er rettet mot .NET6 eller nyere. Mono-bygg leveres ikke lenger og støttes ikke fra og med v4. v3.2.2 er den siste versjonen av Radarr som støtter eldre mono-bygg. Du kjører en av disse eldre mono-byggene, men plattformen din støtter .NET.

Se de følgende oppføringene for hvordan du bytter fra ikke-støttede, utdaterte mono-versjoner til dotnet.

- [Fikse Docker-installasjoner](#fikse-docker-installasjoner)
- [Fikse FreeBSD-installasjoner](#fikse-freebsd-installasjoner)
- [Fikse frittstående installasjoner](#fikse-frittstående-installasjoner)
{.links-list}

##### Fikse Docker-installasjoner

- Sørg for at grenen din er riktig for vedlikeholderen av Docker og trekk inn kontaineren på nytt

##### Fikse FreeBSD-installasjoner

- Oppdater enkelt Radarr-porten med `pkg update && pkg upgrade`
- (Valgfritt) Fjern mono-pakken hvis du ønsker det

##### Fikse frittstående installasjoner

Feil som:

```none
Cannot open assembly '/opt/Radarr/Radarr': File does not contain a valid CIL image
```

- Sikkerhetskopier konfigurasjonen din før neste trinn.
- Dette skal bare skje på Linux-verter. Ikke installer .NET runtime eller SDK fra Microsoft.
- For å rette opp dette, last ned riktig bygg for arkitekturen din og erstatt de eksisterende binærene dine (programmet)
- Kort sagt må du slette de eksisterende binærene dine (innholdet eller mappen /opt/Radarr) og erstatte med innholdet i .tar.gz du nettopp lastet ned, og deretter oppdatere tjenestefilen din for å ikke bruke mono.

> IKKE BARE PAKK UT NEDLASTINGEN OVER DE EKSISTERENDE BINÆRENE DINE.
> DU MÅ FØRST SLETTE DE GAMLE.
{.is-warning}

- Nedenfor er et skript utviklet av fellesskapet for å fjerne mono-installasjonen og erstatte den med .NET-installasjonen. Bidrag og rettelser er velkomne.
- Dette antar at du er på `master` Radarr-grenen, så oppdater variabelen om nødvendig
- Dette antar at Radarr kjører som brukeren `radarr`, så oppdater variablene om nødvendig
- Dette antar at Radarr er installert på `/opt/Radarr`, så oppdater variablene om nødvendig

```bash
#!/bin/bash
## Brukervariabler
installdir="/opt/Radarr"
APPUSER="radarr"
branch="master"
## /Brukervariabler
app="radarr"
ARCH=$(dpkg --print-architecture)
# Stopp \*arr
sudo systemctl stop $app
# Hent arkitektur
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
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
echo "Nedlastingsfiler er lastet ned og pakket ut"
echo "Flytter eksisterende installasjon"
sudo mv "$installdir/" "$installdir.old/"
echo "Installerer..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "Appen er installert"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### Gjeldende installert mono-versjon er gammel og ikke støttet

- Radarr er skrevet i .NET og krever Mono for å kjøre på veldig gamle ARM-prosessorer. Mono 5.20 er det absolutte minimumet for Radarr.
- Oppgraderingsprosedyren for Mono varierer per plattform.

> Mono støttes ikke lenger fra og med Radarr versjon 4.0
{.is-warning}

#### Gjeldende installert SQLite-versjon støttes ikke

- Radarr lagrer dataene sine i en SQLite-database. SQLite3-biblioteket installert på systemet ditt er for gammelt. Radarr krever minst versjon 3.9.0.

> Merk at Radarr bruker `libSQLite3.so`, som kan eller ikke kan være inkludert i en oppgraderingspakke for SQLite3.
{.is-info}

#### Database mislyktes integritetssjekk

- Databasen(e) dine mislyktes en [SQLite Pragma Integrity Check](https://www.sqlite.org/pragma.html#pragma_integrity_check) og har noe korrupt data.
- Hvis `Radarr.db` er korrupt, [se denne FAQ-oppføringen](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)
- Hvis `logs.db` er korrupt: Stopp Radarr, slett `logs.db` og eventuelle `logs.wal`-filer.
- Hvis begge er korrupte, gjennomgå de respektive prosessene ovenfor.

#### Ny oppdatering er tilgjengelig

- Jippi, utviklerne har gitt ut en ny oppdatering. Dette betyr vanligvis fantastiske nye funksjoner og fikset hauger med feil (ikke sant?). Tydeligvis har du ikke aktivert automatisk oppdatering, så du må finne ut hvordan du oppdaterer på plattformen din. Å trykke på Install-knappen på siden System => Oppdateringer er sannsynligvis et godt utgangspunkt.

> Denne advarselen vises ikke hvis nåværende versjon er mindre enn 14 dager gammel
{.is-info}

#### Kan ikke installere oppdatering fordi oppstartsmappen ikke kan skrives til av brukeren

- Dette betyr at Radarr ikke vil kunne oppdatere seg selv. Du må oppdatere Radarr manuelt eller angi tillatelser for Radarrs oppstartsmappe (installasjonsmappen) slik at Radarr kan oppdatere seg selv.

#### Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering

- Radarr oppdaget at AppData-mappen for operativsystemet ditt er plassert inne i mappen som inneholder Radarr-binærene. Normalt sett ville det være C:\ProgramData for Windows og ~/.config for Linux.

- Se på System => Info for å se gjeldende AppData- og oppstartsmapper.
- Dette betyr at Radarr ikke vil kunne oppdatere seg selv uten å risikere tap av data.
- Hvis du bruker Linux, må du sannsynligvis endre hjemmemappen for brukeren som kjører Radarr, og kopiere innholdet i den eksisterende mappen ~/.config/Radarr for å bevare databasen din.

#### Grenen er for en tidligere versjon

- Oppdateringsgrenen som er konfigurert i Innstillinger/Generelt, er for en tidligere versjon av Radarr, og derfor vil instansen ikke se riktig oppdateringsinformasjon i System/Oppdateringer, og kan ikke motta nye oppdateringer når de blir utgitt.

#### Kunne ikke koble til signalR

- signalR driver de dynamiske oppdateringene i brukergrensesnittet, så hvis nettleseren din ikke kan koble til signalR på serveren din, vil du ikke se noen sanntidsoppdateringer i brukergrensesnittet.
- Den vanligste forekomsten av dette er bruk av en omvendt proxy eller Cloudflare.
- Cloudflare trenger aktiverte websockets.

##### Nginx

- Nginx krever følgende tillegg til plasseringen for appen:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Pass på at du ikke inkluderer proxy_set_header Connection "Upgrade"; som foreslått av nginx-dokumentasjonen. DETTE VIL IKKE FUNGERE
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache2

For Apache2 omvendt proxy må du aktivere følgende moduler: proxy, proxy_http og proxy_wstunnel. Deretter legger du til denne direktivet for websockets i vhost-konfigurasjonen din:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:7878/$1 [P,L]
```

Hvis du har en omvendt proxy under en undermappe, bør RewriteRule inkludere basebanen din, f.eks.

```none
RewriteRule /radarr/(.*) ws://127.0.0.1:7878/radarr/$1 [P,L]
```

Hvis Radarr ikke kjører på samme maskin som omvendt proxy. Erstatt 127.0.0.1 med riktig IP-adresse/DNS-navn for Radarr-appen.

##### Caddy

For Caddy (V1) bruk dette:
Merk: Du må også legge til websocket-direktivet i Radarr-konfigurasjonen din

```none
 proxy /radarr 127.0.0.1:7878 {
     websocket
     transparent
 }
```

#### Kunne ikke løse IP-adressen for konfigurert proxyvert

- Gjennomgå proxyinnstillingene dine og forsikre deg om at de er riktige
- Sørg for at proxyen din er oppe, kjører og tilgjengelig

#### Proxy mislyktes test

- Den konfigurerte proxyen mislyktes i å teste vellykket, gjennomgå HTTP-feilen som ble oppgitt og/eller sjekk loggene for mer informasjon.

#### Systemtiden er mer enn 1 dag feil

- Systemtiden er mer enn 1 dag feil. Planlagte oppgaver kan ikke kjøre riktig før tiden er korrigert.
- Gjennomgå systemtiden din og forsikre deg om at den er synkronisert med en autoritativ tidsserver og er nøyaktig.

#### PTP-indeksinnstillinger er utdaterte

- Følgende PassThePopcorn-indekser har utdaterte innstillinger og bør oppdateres.

#### Mono- og x86-bygg avsluttes

- Mono- og x86-bygg støttes ikke lenger med v4. Hvis du får denne feilen, kjører du sannsynligvis mono-versjonen av programmet eller x86-versjonen. Dessverre, på grunn av økende vanskeligheter med utviklingsstøtte for disse eldre versjonene, vil vi avslutte støtten for dem og dermed utgivelser for dem i fremtiden. Derfor anbefales det å oppgradere til et støttet operativsystem som ikke krever verken x86 eller mono. Du kan også vurdere å bruke Docker for dine behov.

### Nedlastingsklienter

#### Ingen nedlastingsklient er tilgjengelig

- En riktig konfigurert og aktivert nedlastingsklient er nødvendig for at Radarr skal kunne laste ned medier. Siden Radarr støtter forskjellige nedlastingsklienter, bør du bestemme hvilken som passer best for dine behov. Hvis du allerede har en nedlastingsklient installert, bør du konfigurere Radarr til å bruke den og opprette en kategori. Se Innstillinger => Nedlastingsklient.

#### Kan ikke kommunisere med nedlastingsklient

- Radarr kunne ikke kommunisere med den konfigurerte nedlastingsklienten. Kontroller om nedlastingsklienten er operativ og dobbeltsjekk URL-en. Dette kan også indikere en autentiseringsfeil.
- Dette skyldes vanligvis en feil konfigurert nedlastingsklient. Ting du vanligvis kan sjekke:
  - IP-adressen til nedlastingsklienten din, hvis den er på samme fysiske maskin, er dette vanligvis 127.0.0.1
  - Portnummeret som nedlastingsklienten din bruker, disse er fylt ut med standard portnummer, men hvis du har endret det, må du ha det samme nummeret i Radarr.
  - Sørg for at SSL-kryptering ikke er aktivert hvis du bruker både Radarr-instansen og nedlastingsklienten din i et lokalt nettverk. Se SSL-FAQ-innføringen for mer informasjon.
  - Sørg for at IPv6 er deaktivert på systemet hvis det ikke fungerer
  - Sørg for at en DNS-server (f.eks. pihole) ikke begrenser hastigheten på spørringer

#### Nedlastingsklienter er utilgjengelige på grunn av feil

- En eller flere av nedlastingsklientene dine svarer ikke på forespørslene som Radarr sender. Derfor har Radarr bestemt seg for å midlertidig slutte å spørre nedlastingsklienten i sin normale 1-minutters syklus, som vanligvis brukes til å spore aktive nedlastinger og importere ferdige nedlastinger. Imidlertid vil Radarr fortsette å prøve å sende nedlastinger til klienten, men vil mest sannsynlig mislykkes.
- Du bør inspisere System=>Logg for å se hva årsaken er til feilene.
- Hvis du ikke lenger bruker denne nedlastingsklienten, deaktiver den i Radarr for å unngå feilene.

#### Aktiver håndtering av fullførte nedlastinger

- Radarr krever at håndtering av fullførte nedlastinger er aktivert for å kunne importere filer som ble lastet ned av nedlastingsklienten. Det anbefales å aktivere håndtering av fullførte nedlastinger. (Håndtering av fullførte nedlastinger er aktivert som standard for nye brukere.)

#### Docker dårlig ekstern stioppføring

- Denne feilen er vanligvis knyttet til dårlige Docker-stier i enten nedlastingsklienten eller Radarr

- Et eksempel på dette ville være:
  - Nedlastingsklient: Nedlastingssti: /mnt/user/downloads:/downloads
  - Radarr: Nedlastingssti: /mnt/user/downloads:/data
- I dette eksemplet plasserer nedlastingsklienten nedlastinger i /downloads og forteller deretter Radarr når det er ferdig at den ferdige filmen er i /downloads. Radarr kommer deretter og sier "Ok, flott, la meg sjekke i /downloads" Vel, inne i Radarr har du ikke tildelt en /downloads-sti, du har tildelt en /data-sti, så det kaster denne feilen.
- Den enkleste løsningen på dette er KONSISTENS, hvis du bruker en ordning i nedlastingsklienten din, bruk den over hele linjen.

- Team Radarr er veldig glad i å bare bruke /data.
  - Nedlastingsklient: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Nå kan du innenfor nedlastingsklienten spesifisere hvor i /data du vil plassere nedlastingen din, dette varierer avhengig av klienten, men du bør kunne fortelle den "Ja, nedlastingsklient, plasser filene mine i." /data/torrents (eller usenet)/movies og siden du brukte /data i Radarr når nedlastingsklienten forteller Radarr at den er ferdig, vil Radarr komme og si "Flott, jeg har en /data og jeg kan også se /torrents (eller usenet)/movies alt er riktig i verden."
- Det er mange flotte artikler: vår wiki [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Disse guidene legger stor vekt på hardlinker og atombevegelser, men det generelle konseptet med containere og hvordan stioppføring fungerer, er kjernen i disse diskusjonene.

- Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mer informasjon.

#### Nedlasting til rotmappen

{#downloads-in-root-folder}

- Innen applikasjonen defineres en rotmappe som den konfigurerte mediebibliotekmappen. Dette er ikke rotmappen til et monteringspunkt. Nedlastingsklienten din har en ufullstendig eller fullført (eller flytter fullførte nedlastinger) til rotmappen din (biblioteket).
- Dette forårsaker ofte problemer - inkludert datatap - og bør ikke gjøres. For å løse dette, endre nedlastingsklienten slik at den ikke plasserer nedlastinger i rotmappen din. Merk at 'plassering' også inkluderer om nedlastingsklientens kategori er satt til rotmappen din eller om NZBGet/SABnzbd har sortering aktivert og sorterer til rotmappen din.
- Vær oppmerksom på at denne sjekken ser på alle definerte/konfigurerte rotmapper som er lagt til, ikke bare rotmapper som for øyeblikket er i bruk. Med andre ord, mappen der nedlastingsklienten din laster ned eller flytter fullførte nedlastinger til, bør ikke være den samme mappen du har konfigurert som rot-/bibliotek-/endelig destinasjonsmappe for medier i *arr-applikasjonen.
- Konfigurerte rotmapper (også kjent som bibliotekmapper) finner du i [Innstillinger => Mediebehandling => Rotmapper](/radarr/settings/#root-folders)
- Ett eksempel er hvis nedlastingen din går til `\data\downloads` og du har en rotmappe satt til `\data\downloads`.
- Det anbefales å bruke stier som `\data\media\` for rotmappen/biblioteket ditt og `\data\downloads\` for nedlastingene dine.
- Gjennomgå vår [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mer informasjon om riktig og optimal oppsett av stier. Merk at konseptene gjelder for både Docker og ikke-Docker

> Nedlastingsmappen der nedlastingsklienten din plasserer nedlastinger og rotmappen/biblioteket ditt MÅ være separate. \*Arr vil importere filen(e) fra nedlastingsklientens mappe til biblioteket ditt. Nedlastingsklienten skal ikke flytte noe eller laste ned noe til biblioteket ditt.
{.is-warning}

#### Dårlige innstillinger for nedlastingsklient

- Plasseringen der nedlastingsklienten din laster ned filer, forårsaker problemer. Sjekk loggene for mer informasjon. Dette kan være tillatelser eller forsøk på å gå fra Windows til Linux eller Linux til Windows uten en ekstern stioppføring.

#### Dårlig ekstern stioppføring

- Plasseringen der nedlastingsklienten din laster ned filer, forårsaker problemer. Sjekk loggene for mer informasjon. Dette kan være tillatelser eller forsøk på å gå fra Windows til Linux eller Linux til Windows uten en ekstern stioppføring. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mer informasjon.

#### Tillatelsesfeil

- Radarr eller brukeren radarr kjører som, kan ikke få tilgang til plasseringen der nedlastingsklienten din laster ned filer. Dette er vanligvis et tillatelsesproblem.

#### Ekstern fil ble fjernet under behandling

- En fil som er tilgjengelig via en ekstern stioppføring, ser ut til å ha blitt fjernet før behandlingen var fullført.

#### Brukte fjernsti og import mislyktes

- Sjekk loggene for mer informasjon; Se våre feilsøkingsguider

### Fullførte/mislukte nedlastingshåndtering

#### Fullført nedlastingshåndtering er deaktivert

- (Denne advarselen genereres bare for eksisterende brukere før funksjonen for fullført nedlastingshåndtering ble implementert. Denne funksjonen er deaktivert som standard for å sikre at systemet fortsatte å fungere som forventet for gjeldende konfigurasjoner.)
- Det anbefales å bruke fullført nedlastingshåndtering, da det gir bedre kompatibilitet for pakking og etterbehandling av forskjellige nedlastingsklienter. Med dette vil Radarr bare importere en nedlasting når nedlastingsklienten rapporterer at den er klar.
- Hvis du ønsker å aktivere fullført nedlastingshåndtering, bør du bekrefte følgende: * Advarsel: Fullført nedlastingshåndtering fungerer bare riktig hvis nedlastingsklienten og Radarr er på samme maskin, siden den får banen som skal importeres direkte fra nedlastingsklienten, ellers trengs en ekstern kartlegging.

### Indekser

#### Ingen indekser er tilgjengelige med automatisk søk aktivert, Radarr vil ikke gi noen automatiske søkeresultater

- Enkelt sagt har du ikke noen av indeksene dine satt til å tillate automatisk søk
- Gå til Innstillinger => Indekser, velg en indeks du vil tillate automatisk søk og klikk deretter på Lagre.

#### Ingen indekser er tilgjengelige med RSS-synkronisering aktivert, Radarr vil ikke hente nye utgivelser automatisk

- Radarr bruker RSS-feeden til å plukke opp nye utgivelser etter hvert som de kommer. Mer informasjon om det finner du her
- For å rette opp dette problemet går du til Innstillinger => Indekser, velger en indeks du har og aktiverer RSS-synkronisering

#### Ingen indekser er aktivert

- Radarr krever indekser for å kunne oppdage nye utgivelser. Les wikien for instruksjoner om hvordan du legger til indekser.

#### Aktiverte indekser støtter ikke søk

- Ingen av de aktiverte indeksene dine støtter søk. Dette betyr at Radarr bare vil kunne finne nye utgivelser via RSS-feedene. Men søk etter filmer (enten automatisk søk eller manuelt søk) vil aldri gi noen resultater. Den eneste måten å rette det på er å legge til en annen indeks.

#### Ingen indekser er tilgjengelige med interaktivt søk aktivert

- Ingen av de aktiverte indeksene dine støtter interaktivt søk. Dette betyr at applikasjonen bare vil kunne finne nye utgivelser via RSS-feedene eller et automatisk søk.

#### Indekser er utilgjengelige på grunn av feil

- Feil oppstår når Radarr prøvde å bruke en av indeksene dine. For å begrense forsøkene, vil Radarr ikke bruke indeksen i en økende mengde tid (opptil 24 timer).
- Denne mekanismen utløses hvis Radarr ikke kunne få et svar fra indeksen (kan skyldes DNS, proxy/vpn-tilkobling, autentisering eller en indeksfeil), eller ikke kunne hente nzb/torrent-filen fra indeksen. Se på loggene for å finne ut hvilken type feil som forårsaket problemet.
- Du kan forhindre advarselen ved å deaktivere den berørte indeksen.
- Kjør testen på indeksen for å tvinge Radarr til å sjekke indeksen på nytt, vær oppmerksom på at helsekontrolladvarselen ikke alltid vil forsvinne umiddelbart.

#### Jackett bruker alle endepunkter

- Jackett /all-endepunktet er praktisk, men det er den eneste fordelen. Alt annet er potensielle problemer, så nå kreves det at hver tracker legges til individuelt.
- [Selv Jacketts utviklere sier at det bør unngås og ikke brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Bruk av /all-endepunktet har ingen fordeler, bare ulemper:
  - du mister kontrollen over indeksspesifikke innstillinger (kategorier, søkemåter, osv.)
  - blanding av søkemåter (IMDB, spørring, osv.) kan føre til lavkvalitetsresultater
  - indeksspesifikke kategorier (\>= 100000) kan ikke brukes.
  - treg indekser vil bremse ned den generelle resultatet
  - totalt antall resultater er begrenset til 1000
  - hvis en av trackerne i /all returnerer en feil, vil \*Arr deaktivere den og nå får du ingen resultater.

##### Løsninger

- Legg til hver tracker i Jackett manuelt som en indeks i \*Arr
- Sjekk ut [Prowlarr](/prowlarr) som kan synkronisere indekser til \*Arr og fra Lidarr/Radarr/Readarr-utviklingsteamet.
- Sjekk ut [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisere indekser til \*Arr. Men ikke bruk deres enkeltstående aggregat-endepunkt og bruk `multi` hvis synkroniseringen skal brukes.

### Filmapper

#### Mangler rotmappe

{#movie-collection-missing-root-folder}

- Denne feilen identifiseres vanligvis hvis en film eller samling er tildelt en rotmappe, men den rotmappen er ikke lenger tilgjengelig.
- Denne feilen kan også oppstå hvis en liste fremdeles peker på en rotmappe og den rotmappen ikke lenger er tilgjengelig.
- Hvis du vil fjerne denne advarselen, finn bare filmene eller samlingene som fortsatt bruker den gamle rotmappen, og rediger dem til riktig rotmappe.

##### Tabellvisning av filmer

1. Gå til fanen Filmer (Bibliotek)
1. Tabellvisning og aktiver kolonnen Path, og sorter etter path

##### Egendefinert filter for filmer

1. Opprett et egendefinert filter med den gamle rotmappen
1. Velg masseendring i toppmenyen og velg den nye rotmappen du vil flytte disse filmene til fra rullegardinmenyen Root Paths.
1. Deretter får du en popup som sier "Vil du flytte filmmappene til 'rotmappe'?" Dette vil også si at dette vil også gi nytt navn til filmappen i henhold til filmappenformatet i innstillingene. Velg bare Nei hvis du ikke vil at Radarr skal flytte filene dine.
1. Kjør helsekontrolloppgaven i System => Oppgaver

#### Egendefinert filter for samlinger

1. Opprett et egendefinert filter i Samlinger med den gamle rotmappen
1. Velg samlingene og fra rullegardinmenyen Root Paths velger du den nye rotmappen du vil at fremtidige filmer i disse samlingene skal tilordnes.
1. Kjør helsekontrolloppgaven i System => Oppgaver

### Filmer

#### Film ble fjernet fra TMDb

- Filmen er koblet til en TMDb-ID som ble slettet fra TMDb, vanligvis fordi det var en duplikat, ikke var en film eller endret ID av en annen grunn. Slettede filmer vil ikke motta oppdateringer og bør rettes av brukeren for å sikre fortsatt funksjonalitet. Fjern filmen fra Radarr uten å slette filene, og prøv å legge den til på nytt. Hvis den ikke vises i et søk, sjekk Sonarr, fordi det kan være en TV-miniserie som Stephen Kings It.

- Du kan finne og redigere slettede filmer ved å opprette et egendefinert filter ved å følge disse trinnene:

  1. Klikk på Filmer i venstremenyen
  1. Klikk på rullegardinmenyen for Filter og velg "Egendefinert filter"
  1. Skriv inn en etikett, for eksempel "Slettede filmer"
  1. Lag

## Kø

- Køen vil vise deg kjørende og kommende oppgaver, samt en historikk over nylig kjørte oppgaver og hvor lang tid disse oppgavene tok.

# Sikkerhetskopi

> Hvis du vil vite hvordan du sikkerhetskopierer/gjenoppretter Radarr-instansen din, klikk [her](/radarr/faq).
{.is-info}

- Innenfor Sikkerhetskopi-seksjonen vil du bli presentert med tidligere sikkerhetskopier (med mindre du har en fersk installasjon som ikke har laget noen sikkerhetskopier ennå).
  
- Sikkerhetskopier nå - Denne muligheten vil utløse en manuell sikkerhetskopi av Radarr-databasen din.
- Gjenopprett sikkerhetskopi - Dette vil åpne et nytt skjermbilde for å gjenopprette fra en tidligere sikkerhetskopi.
  - Ved å velge Velg fil vil dette be nettleseren din om å åpne en dialogboks for å gjenopprette fra en Radarr-zip-sikkerhetskopi.
  
- Hvis du har noen tidligere sikkerhetskopier og ønsker å laste dem ned fra Radarr for å plassere dem på en ikke-standard plassering, kan du enkelt velge en av disse filene for å laste dem ned.
- Til høyre for hver av de tidligere nedlastningene har du to alternativer.
  - Gjenopprett (Klokkeikon) - For å gjenopprette fra en tidligere sikkerhetskopi - Dette vil åpne et nytt vindu for å bekrefte at du ønsker å gjenopprette fra denne sikkerhetskopien.
  - Slett (Søppelbøtte) - For å slette en tidligere sikkerhetskopi.

# Oppdateringer

- Oppdateringsskjermen vil vise de fem siste oppdateringene som er gjort, samt den nåværende versjonen du er på.
- Denne siden vil også vise oppdateringsnotater fra utviklerne som forteller deg hva som er blitt fikset eller lagt til i Radarr (Jubel!)

> En vedlikeholdsutgivelse inneholder feilrettinger og andre forskjellige forbedringer. Ta en titt på endringsloggen for spesifikke detaljer.
{.is-info}

# Hendelser

- Hendelsesfanen vil vise deg hva som har skjedd i Radarr. Dette kan brukes til å diagnostisere mindre problemer. Men dette erstatter ikke sporingslogger som diskuteres i Logging.

> Hendelser tilsvarer INFO-logger. {.is-info}

- Komponenter - Denne kolonnen vil fortelle deg hvilken komponent innenfor Radarr som har blitt utløst.
- Melding - Denne kolonnen vil fortelle deg hvilken melding som er sendt fra komponenten i forrige kolonne.
- Tannhjulikon - Dette alternativet lar deg endre hvor mange komponenter/meldinger som vises per side (Standard er 50).
- Alternativer øverst på siden
  - Oppdater - Dette alternativet vil oppdatere gjeldende side og hente en ny hendelseslogg.
  - Tøm - Dette vil tømme gjeldende hendelseslogg og la deg starte på nytt.

# Loggfiler

- Denne siden lar deg laste ned og se hvilke gjeldende loggfiler som er tilgjengelige for Radarr.

- På toppraden er det flere alternativer som lar deg kontrollere loggfilene dine.

- På toppraden helt til venstre er det en nedtrekksliste som lar deg bytte mellom loggfiler og oppdateringsloggfiler.
  - Loggfiler - Hoveddelen av ethvert supportproblem, mer om loggfiler kan finnes her.
  - Oppdateringsloggfiler - Dette vil vise loggfilene som er knyttet til Radarrs oppdateringsskript.

> Hvis du bruker Docker, vil dette være tomt, da du bør oppdatere ved å laste ned et nytt Docker-bilde.
{.is-info}

- Oppdater - Dette vil oppdatere gjeldende side og vise eventuelt nyopprettede logger.
- Slett - Dette vil slette alle logger og la deg starte på nytt.
- Filnavn - Dette vil vise filnavnet som er knyttet til loggen.
- Sist skrevet - Dette er lokal tid da denne bestemte loggfilen ble skrevet.
  - Radarr bruker rullerende loggfiler begrenset til 1 MB hver. Den gjeldende loggfilen er alltid radarr.txt, for de andre filene er radarr.0.txt den nest nyeste (jo høyere nummer, jo eldre er den) opp til totalt 51 loggfiler. Denne loggfilen inneholder `fatal`, `error`, `warn` og `info`-oppføringer.
  - Når feilsøkingslogg-nivået er aktivert, vil det være tilgjengelige radarr.debug.txt-rullerende loggfiler, opptil 51 filer. Denne loggfilen inneholder `fatal`, `error`, `warn`, `info` og `debug`-oppføringer. Den dekker vanligvis en periode på ~40 timer.
  - Når sporingslogg-nivået er aktivert, vil det være tilgjengelige radarr.trace.txt-rullerende loggfiler, opptil 51 filer. Denne loggfilen inneholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-oppføringer. På grunn av sporingsnøyaktighet dekker den bare et par timer.