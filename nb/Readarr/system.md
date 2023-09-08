---
title: Readarr System
description: 
published: true
date: 2022-05-05T12:52:16.242Z
tags: readarr, needs-love, system
editor: markdown
dateCreated: 2021-06-20T19:54:43.262Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Status](#status)
  - [Helse](#helse)
    - [Systemadvarsler](#systemadvarsler)
      - [Grenen er ikke en gyldig utgavegren](#grenen-er-ikke-en-gyldig-utgavegren)
      - [Gjeldende installert SQLite-versjon støttes ikke](#gjeldende-instalert-sqlite-versjon-støttes-ikke)
      - [Ny oppdatering er tilgjengelig](#ny-oppdatering-er-tilgjengelig)
      - [Kan ikke installere oppdatering fordi oppstartsmappen ikke kan skrives til av brukeren](#kan-ikke-installere-oppdatering-fordi-oppstartsmappen-ikke-kan-skrives-til-av-brukeren)
      - [Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering](#oppdatering-vil-ikke-være-mulig-for-å-forhindre-sletting-av-appdata-ved-oppdatering)
      - [Grenen er for en tidligere versjon](#grenen-er-for-en-tidligere-versjon)
      - [Kunne ikke koble til signalR](#kunne-ikke-koble-til-signalr)
        - [Nginx](#nginx)
      - [Klarte ikke å løse IP-adressen for konfigurert proxyvert](#klarte-ikke-å-løse-ip-adressen-for-konfigurert-proxyvert)
      - [Proxy mislyktes i test](#proxy-mislyktes-i-test)
      - [Systemtiden er mer enn 1 dag feil](#systemtiden-er-mer-enn-1-dag-feil)
    - [Nedlastingsklienter](#nedlastingsklienter)
      - [Ingen nedlastingsklient er tilgjengelig](#ingen-nedlastingsklient-er-tilgjengelig)
      - [Kan ikke kommunisere med nedlastingsklient](#kan-ikke-kommunisere-med-nedlastingsklient)
      - [Nedlastingsklienter er utilgjengelige på grunn av feil](#nedlastingsklienter-er-utilgjengelige-på-grunn-av-feil)
      - [Aktiver håndtering av fullførte nedlastinger](#aktiver-håndtering-av-fullførte-nedlastinger)
      - [Docker dårlig ekstern stiavbildning](#docker-dårlig-ekstern-stiavbildning)
      - [Laster ned til rotmappen](#laster-ned-til-rotmappen)
      - [Feil nedlastingsklientinnstillinger](#feil-nedlastingsklientinnstillinger)
      - [Feil ekstern stiavbildning](#feil-ekstern-stiavbildning)
      - [Tillatelsesfeil](#tillatelsesfeil)
      - [Forfattermonteringen er skrivebeskyttet](#forfattermonteringen-er-skrivebeskyttet)
      - [Ekstern fil ble fjernet under behandling](#ekstern-fil-ble-fjernet-under-behandling)
      - [Ekstern sti brukes og import mislyktes](#ekstern-sti-brukes-og-import-mislyktes)
    - [Fullførte/mislukte nedlastingshåndtering](#fullførtemislukte-nedlastingshåndtering)
      - [Fullført nedlastingshåndtering er deaktivert](#fullført-nedlastingshåndtering-er-deaktivert)
    - [Indekser](#indekser)
      - [Ingen indekser er tilgjengelige med automatisk søk aktivert, Readarr vil ikke gi noen automatiske søkeresultater](#ingen-indekser-er-tilgjengelige-med-automatisk-søk-aktivert-readarr-vil-ikke-gi-noen-automatiske-søkeresultater)
      - [Ingen indekser er tilgjengelige med RSS-synkronisering aktivert, Readarr vil ikke hente nye utgivelser automatisk](#ingen-indekser-er-tilgjengelige-med-rss-synkronisering-aktivert-readarr-vil-ikke-hente-nye-utgivelser-automatisk)
      - [Ingen indekser er aktivert](#ingen-indekser-er-aktivert)
    - [Aktiverte indekser støtter ikke søk](#aktiverte-indekser-støtter-ikke-søk)
      - [Ingen indekser er tilgjengelige med interaktivt søk aktivert](#ingen-indekser-er-tilgjengelige-med-interaktivt-søk-aktivert)
      - [Indekser er utilgjengelige på grunn av feil](#indekser-er-utilgjengelige-på-grunn-av-feil)
      - [Jackett All Endpoint Used](#jackett-all-endpoint-used)
        - [Løsninger](#løsninger)
    - [Bokmapper](#bokmapper)
      - [Mangler rotmappe](#mangler-rotmappe)
    - [Importlister](#importlister)
      - [Importlister er utilgjengelige på grunn av feil](#importlister-er-utilgjengelige-på-grunn-av-feil)
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

- Denne siden inneholder en liste over helsekontrollfeil. Disse helsekontrollene utføres periodisk av Readarr og ved visse hendelser. De resulterende advarslene og feilene er oppført her for å gi råd om hvordan du løser dem.

### Systemadvarsler

#### Grenen er ikke en gyldig utgavegren

- Grenen du har satt er ikke en gyldig utgavegren. Du vil ikke motta oppdateringer. Vennligst endre til en av de [nåværende utgavegrenene](/readarr/faq#how-do-i-update-readarr)

#### Gjeldende installert SQLite-versjon støttes ikke

- Readarr lagrer dataene sine i en SQLite-database. SQLite3-biblioteket som er installert på systemet ditt, er for gammelt. Readarr krever minst versjon 3.9.0. Merk at Readarr bruker `libSQLite3.so`, som kan eller ikke kan være inkludert i en SQLite3-oppgraderingspakke.

> Merk at Readarr bruker `libSQLite3.so`, som kan eller ikke kan være inkludert i en SQLite3-oppgraderingspakke.
{.is-info}

#### Ny oppdatering er tilgjengelig

Fryd deg, utviklerne har gitt ut en ny oppdatering. Dette betyr generelt sett fantastiske nye funksjoner og fikset hauger med feil (ikke sant?). Tydeligvis har du ikke aktivert automatisk oppdatering, så du må finne ut hvordan du oppdaterer på plattformen din. Å trykke på Installer-knappen på System => Oppdateringer-siden er sannsynligvis et godt utgangspunkt.

> Denne advarselen vises ikke hvis gjeldende versjon er mindre enn 14 dager gammel
{.is-info}

#### Kan ikke installere oppdatering fordi oppstartsmappen ikke kan skrives til av brukeren

- Dette betyr at Readarr ikke vil kunne oppdatere seg selv. Du må oppdatere Readarr manuelt eller angi tillatelsene for Readarrs oppstartsmappen (installasjonsmappen) for å tillate at Readarr oppdaterer seg selv.

#### Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering

- Readarr oppdaget at AppData-mappen for operativsystemet ditt er plassert inne i mappen som inneholder Readarr-binærene. Normalt sett ville det være C:\ProgramData for Windows og ~/.config for Linux.

- Se på System => Info for å se gjeldende AppData- og oppstartsmapper.
- Dette betyr at Readarr ikke vil kunne oppdatere seg selv uten å risikere tap av data.
- Hvis du bruker Linux, må du sannsynligvis endre hjemmemappen for brukeren som kjører Readarr, og kopiere innholdet i ~/.config/Readarr-mappen for å bevare databasen din.

#### Grenen er for en tidligere versjon

- Oppdateringsgrenen som er konfigurert i Innstillinger/Generelt, er for en tidligere versjon av Readarr, derfor vil instansen ikke se riktig oppdateringsinformasjon i System/Oppdateringer-strømmen og kan ikke motta nye oppdateringer når de blir utgitt.

#### Kunne ikke koble til signalR

- signalR driver de dynamiske brukergrensesnittoppdateringene, så hvis nettleseren din ikke kan koble til signalR på serveren din, vil du ikke se noen sanntidsoppdateringer i brukergrensesnittet.

- Den vanligste forekomsten av dette er bruk av en omvendt proxy eller Cloudflare
- Cloudflare trenger aktiverte websockets.

##### Nginx

- Nginx krever følgende tillegg til plasseringsblokken for appen:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Pass på at du ikke inkluderer proxy_set_header Connection "Upgrade"; som foreslått av nginx-dokumentasjonen. DETTE VIL IKKE FUNGERE
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

For Apache2 omvendt proxy må du aktivere følgende moduler: proxy, proxy_http og proxy_wstunnel. Deretter legger du til denne websocket-tunnelanvisningen i vhost-konfigurasjonen din:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8787/$1 [P,L]
```

For Caddy (V1) bruk dette:
Merk: Du må også legge til websocket-anvisningen i Readarr-konfigurasjonen din

```none
 proxy /readarr 127.0.0.1:8787 {
     websocket
     transparent
 }
```

#### Klarte ikke å løse IP-adressen for konfigurert proxyvert

- Gjennomgå proxyinnstillingene dine og forsikre deg om at de er korrekte
- Forsikre deg om at proxyen din er oppe, kjører og tilgjengelig

#### Proxy mislyktes i test

- Den konfigurerte proxyen mislyktes i testen, gjennomgå HTTP-feilen som ble oppgitt og/eller sjekk loggene for mer informasjon.

#### Systemtiden er mer enn 1 dag feil

- Systemtiden er mer enn 1 dag feil. Planlagte oppgaver kan ikke kjøre riktig før tiden er korrigert
- Gjennomgå systemtiden din og forsikre deg om at den er synkronisert med en autoritativ tidsserver og er nøyaktig

### Nedlastingsklienter

#### Ingen nedlastingsklient er tilgjengelig

- En riktig konfigurert og aktivert nedlastingsklient er nødvendig for at Readarr skal kunne laste ned medier. Siden Readarr støtter forskjellige nedlastingsklienter, bør du bestemme deg for hvilken som passer best for dine behov. Hvis du allerede har en nedlastingsklient installert, bør du konfigurere Readarr til å bruke den og opprette en kategori. Se Innstillinger => Nedlastingsklient.

#### Kan ikke kommunisere med nedlastingsklient

- Readarr kunne ikke kommunisere med den konfigurerte nedlastingsklienten. Vennligst verifiser om nedlastingsklienten er operativ og dobbeltsjekk URL-en. Dette kan også indikere en autentiseringsfeil.
- Dette skyldes vanligvis en feil konfigurert nedlastingsklient. Ting du vanligvis kan sjekke:
- IP-adressen til nedlastingsklienten din hvis den er på samme fysiske maskin, er dette vanligvis 127.0.0.1
- Portnummeret som nedlastingsklienten din bruker, disse er fylt ut med standard portnummer, men hvis du har endret det, må du ha det samme nummeret angitt i Readarr.
- Forsikre deg om at SSL-kryptering ikke er aktivert hvis du bruker både Readarr-instansen og nedlastingsklienten din i et lokalt nettverk. Se SSL-FAQ-innføringen for mer informasjon.

#### Nedlastingsklienter er utilgjengelige på grunn av feil

{#nedlastingsklienter-er-utilgjengelige-på-grunn-av-feil}

- En eller flere av nedlastingsklientene dine svarer ikke på forespørslene som Readarr sender. Derfor har Readarr bestemt seg for å midlertidig slutte å spørre nedlastingsklienten på sin normale 1-minutters syklus, som vanligvis brukes til å spore aktive nedlastinger og importere ferdige nedlastinger. Imidlertid vil Readarr fortsette å prøve å sende nedlastinger til klienten, men vil mest sannsynlig mislykkes.
- Du bør inspisere System=>Loggfiler for å se hva årsaken til feilene er.
- Hvis du ikke lenger bruker denne nedlastingsklienten, deaktiver den i Readarr for å forhindre feil.

#### Aktiver håndtering av fullførte nedlastinger

- Readarr krever at håndtering av fullførte nedlastinger er aktivert for å kunne importere filer som ble lastet ned av nedlastingsklienten. Det anbefales å aktivere håndtering av fullførte nedlastinger.
- (Håndtering av fullførte nedlastinger er aktivert som standard for nye brukere.)

#### Docker dårlig ekstern stiavbildning

- Denne feilen er vanligvis assosiert med dårlige Docker-stier i enten nedlastingsklienten eller Readarr

- Et eksempel på dette ville være:
  - Nedlastingsklient: Nedlastingssti: /mnt/user/downloads:/downloads
  - Readarr: Nedlastingssti: /mnt/user/downloads:/data
- I dette eksemplet plasserer nedlastingsklienten nedlastinger i /downloads og forteller deretter Readarr når den er ferdig at den ferdige boken er i /downloads. Readarr kommer deretter og sier "Ok, flott, la meg sjekke i /downloads" Vel, inne i Readarr har du ikke tildelt en /downloads-sti, du har tildelt en /data-sti, så det kastes denne feilen.
- Den enkleste løsningen på dette er KONSISTENS, hvis du bruker en ordning i nedlastingsklienten din, bruk den over hele linjen.

- Team Readarr er stor fan av å bare bruke /data.
  - Nedlastingsklient: /mnt/user/data/downloads:/data/downloads
  - Readarr: /mnt/user/data:/data

- Nå kan du innenfor nedlastingsklienten spesifisere hvor i /data du vil plassere nedlastingen din, dette varierer avhengig av klienten, men du bør kunne fortelle den "Ja, nedlastingsklient, plasser filene mine i." /data/torrents (eller usenet)/books og siden du brukte /data i Readarr når nedlastingsklienten forteller Readarr at den er ferdig, vil Readarr komme og si "Flott, jeg har en /data og jeg kan også se /torrents (eller usenet)/books alt er riktig i verden."
- Det er mange flotte skriveoppsett: vår wiki [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Disse veiledningene legger stor vekt på hardlenker og atombevegelser, men det generelle konseptet med containere og hvordan stiavbildning fungerer, er kjernen i disse diskusjonene.

- Hvis du krysser operativsystemer eller native og Docker, trenger du en ekstern stiavbildning. Se [TRaSH's Remote Path Guide for Radarr, men konseptet er det samme for alle \*Arrs](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mer informasjon.

- Hvis du får denne feilen med Calibre, kan ikke Redarr få tilgang til Calibres bibliotek. Løsningen er den samme - rett opp de inkonsekvente monteringene for kontainerne dine. Alternativt kan du opprette en ekstern stiavbildning for å avbilde Calibre Library-stien til den Readarr-tilgjengelige stien. En ekstern stiavbildning er bare nødvendig hvis du krysser operativsystemer eller servere. Hvis alt er i Docker, er det å foretrekke å rette opp monteringene dine i stedet.

#### Laster ned til rotmappen

{#downloads-in-root-folder}

- Innen applikasjonen defineres en rotmappe som den konfigurerte mediebibliotekmappen. Dette er ikke rotmappen til et monteringspunkt. Nedlastingsklienten din laster ned ufullstendige eller fullførte nedlastinger (eller flytter fullførte nedlastinger) til rotmappen (biblioteket) din.
- Dette forårsaker ofte problemer - inkludert tap av data - og bør ikke gjøres. For å løse dette, endre nedlastingsklienten slik at den ikke plasserer nedlastinger i rotmappen din. Merk at 'plassering' også inkluderer om nedlastingsklientens kategori er satt til rotmappen din eller om NZBGet/SABnzbd har sortering aktivert og sorterer til rotmappen din.
- Vær oppmerksom på at denne sjekken ser på alle definerte/konfigurerte rotmapper som er lagt til, ikke bare rotmapper som for øyeblikket er i bruk. Med andre ord, mappen nedlastingsklienten din laster ned til eller flytter fullførte nedlastinger til, bør ikke være den samme mappen du har konfigurert som rot-/biblioteks-/endelige mediamålmappe i *arr-applikasjonen.
- Konfigurerte rotmapper (også kjent som bibliotekmapper) finner du i [Innstillinger => Mediehåndtering => Rotmapper](/readarr/settings/#root-folders)
- Ett eksempel er hvis nedlastingen din går til `\data\downloads`, så har du en rotmappe satt som `\data\downloads`.
- Det anbefales å bruke stier som `\data\media\` for rotmappen/biblioteket ditt og `\data\downloads\` for nedlastingen din.
- Gjennomgå vår [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mer informasjon om riktig og optimal stikonfigurasjon. Merk at konseptene gjelder for både Docker og ikke-Docker

> Nedlastingsmappen der nedlastingsklienten din plasserer nedlastingene og rot-/bibliotekmappen din MÅ være separate. \*Arr vil importere filen(e) fra nedlastingsklientens mappe til biblioteket ditt. Nedlastingsklienten skal ikke flytte noe eller laste ned noe til biblioteket ditt.
{.is-warning}

#### Feil nedlastingsklientinnstillinger

- Plasseringen der nedlastingsklienten din laster ned filer, forårsaker problemer. Sjekk loggene for mer informasjon. Dette kan være tillatelsesproblemer eller forsøk på å gå fra Windows til Linux eller Linux til Windows uten en ekstern stiavbildning.

#### Feil ekstern stiavbildning

- Plasseringen der nedlastingsklienten din laster ned filer forårsaker problemer. Sjekk loggene for mer informasjon. Dette kan skyldes tillatelser eller forsøk på å gå fra Windows til Linux eller Linux til Windows uten en fjernbanekart. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Readarr/Readarr-remote-path-mapping/) for mer informasjon.

#### Tillatelsesfeil

- Readarr eller brukeren readarr kjører som har ikke tilgang til plasseringen der nedlastingsklienten din laster ned filer. Dette er vanligvis et tillatelsesproblem.

#### Forfattermonteringen er skrivebeskyttet

{#author-mount-ro}

- Monteringen som inneholder en forfatterbane er montert som skrivebeskyttet. Sjekk monteringsinnstillingene og eierskap/tilganger.

#### Ekstern fil ble fjernet under behandling

- En fil som er tilgjengelig via en ekstern banekart ser ut til å ha blitt fjernet før behandlingen var fullført.

#### Ekstern bane brukes og importen mislyktes

- Sjekk loggene for mer informasjon; Se våre feilsøkingsguider

### Behandling av fullførte/mislukkede nedlastinger

#### Behandling av fullførte nedlastinger er deaktivert

- (Denne advarselen genereres bare for eksisterende brukere før funksjonen for behandling av fullførte nedlastinger ble implementert. Denne funksjonen er deaktivert som standard for å sikre at systemet fortsetter å fungere som forventet for gjeldende konfigurasjoner.)
- Det anbefales å bruke behandling av fullførte nedlastinger, da det gir bedre kompatibilitet for pakking og etterbehandlingslogikk for forskjellige nedlastingsklienter. Med denne funksjonen vil Readarr bare importere en nedlasting når nedlastingsklienten rapporterer at den er klar.
- Hvis du ønsker å aktivere behandling av fullførte nedlastinger, bør du verifisere følgende: * Advarsel: Behandling av fullførte nedlastinger fungerer bare riktig hvis nedlastingsklienten og Readarr er på samme maskin, siden den får banen som skal importeres direkte fra nedlastingsklienten, ellers trengs det et eksternt kart.

### Indekser

#### Ingen indekser tilgjengelig med aktivert automatisk søk, Readarr vil ikke gi noen automatiske søkeresultater

- Enkelt sagt har du ingen av indeksene dine satt til å tillate automatisk søk
- Gå til Innstillinger => Indekser, velg en indeks du vil tillate automatisk søk og klikk deretter på Lagre.

#### Ingen indekser tilgjengelig med aktivert RSS-synkronisering, Readarr vil ikke hente nye utgivelser automatisk

- Så Readarr bruker RSS-feeden til å plukke opp nye utgivelser etter hvert som de kommer. Mer informasjon om dette finner du her
- For å rette opp dette problemet går du til Innstillinger => Indekser, velg en indeks du har og aktiver RSS-synkronisering

#### Ingen indekser er aktivert

- Readarr krever indekser for å kunne oppdage nye utgivelser. Vennligst les wikien for instruksjoner om hvordan du legger til indekser.

### Aktiverte indekser støtter ikke søk

- Ingen av de aktiverte indeksene dine støtter søk. Dette betyr at Readarr bare vil kunne finne nye utgivelser via RSS-feedene. Men søk etter bøker (enten automatisk søk eller manuelt søk) vil aldri gi noen resultater. Den eneste måten å rette det på er å legge til en annen indeks.

#### Ingen indekser tilgjengelig med aktivert interaktivt søk

- Ingen av de aktiverte indeksene dine støtter interaktivt søk. Dette betyr at programmet bare vil kunne finne nye utgivelser via RSS-feedene eller et automatisk søk.

#### Indeksene er utilgjengelige på grunn av feil

- Feil oppstod mens Readarr prøvde å bruke en av indeksene dine. For å begrense forsøkene vil ikke Readarr bruke indeksen i en økende mengde tid (opptil 24 timer).
- Denne mekanismen utløses hvis Readarr ikke kunne få et svar fra indeksen (kan skyldes DNS, proxy/vpn-tilkobling, autentisering eller en indeksfeil), eller ikke kunne hente nzb-/torrent-filen fra indeksen. Vennligst undersøk loggene for å finne ut hvilken type feil som forårsaker problemet.
- Du kan forhindre advarselen ved å deaktivere den berørte indeksen.
- Kjør testen på indeksen for å tvinge Readarr til å sjekke indeksen på nytt, vær oppmerksom på at helsekontrolladvarselen ikke alltid forsvinner umiddelbart.

#### Jackett All Endpoint brukes

- Jackett /all-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan føre til problemer, så det er nå nødvendig å legge til hver enkelt tracker separat.
- [Selv Jacketts utviklere sier at det bør unngås og ikke brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Å bruke /all-endepunktet har ingen fordeler, bare ulemper:
  - du mister kontrollen over indeksspesifikke innstillinger (kategorier, søkemåter, osv.)
  - blanding av søkemåter (IMDB, søk, osv.) kan føre til lavkvalitetsresultater
  - indeksspesifikke kategorier (\>= 100000) kan ikke brukes.
  - treg indekser vil bremse ned den totale resultatet
  - totalt antall resultater er begrenset til 1000
  - hvis en av trackerne i /all returnerer en feil, vil \*Arr deaktivere den og nå får du ingen resultater.

##### Løsninger

- Legg til hver enkelt tracker i Jackett manuelt som en indeks i \*Arr
- Sjekk ut [Prowlarr](/prowlarr) som kan synkronisere indekser til \*Arr og fra Lidarr/Radarr/Readarr-utviklingsteamet.
- Sjekk ut [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisere indekser til \*Arr. Men ikke bruk deres enkeltstående aggregatendepunkt, bruk `multi` hvis synkronisering skal brukes.

### Bokmapper

#### Manglende rotmappe

- Denne feilen identifiseres vanligvis hvis en forfatter leter etter en rotmappe, men den rotmappen er ikke lenger tilgjengelig.
- Denne feilen kan også oppstå hvis en liste fortsatt peker på en rotmappe, men den rotmappen ikke lenger er tilgjengelig.
- Hvis du vil fjerne denne advarselen, finn bare albumet som fortsatt bruker den gamle rotmappen og rediger det til riktig rotmappe.

- Enkelt måte å finne problemforfatteren på:

  - Gå til fanen Forfatter (Bibliotek)
  - Opprett et tilpasset filter med den gamle rotmappen
  - Velg masseendring i toppmenyen og velg den nye rotmappen du vil flytte disse forfatterne til fra rullegardinmenyen Rotstier.
  - Deretter får du en popup-melding som sier Vil du flytte forfattermappene til 'rotmappe'? Dette vil også si Dette vil også gi forfattermappen et nytt navn i henhold til formatet for forfattermappen i innstillingene. Velg bare Nei hvis du ikke vil at Readarr skal flytte filene dine
  - Kjør helsesjekkoppgaven i System => Oppgaver

### Importlister

#### Importlister er utilgjengelige på grunn av feil

- Dette betyr vanligvis at Readarr ikke lenger kan kommunisere via API eller ved å logge inn på den valgte listen. Hvis problemet vedvarer, bør du kontakte dem for å utelukke dem, da systemene deres kan være overbelastet fra tid til annen.

## Diskplass

- Denne delen viser tilgjengelig diskplass
- I Docker kan dette være litt komplisert, da det vanligvis viser tilgjengelig plass innenfor Docker-bildet ditt

## Om

- Dette vil fortelle deg om gjeldende installasjon av Readarr

## Mer informasjon

- Hjemmeside: Readarrs hjemmeside
- Wiki: Du er allerede her
- Reddit: r/readarr
- Discord: Bli med i vår discord
- Donasjoner: Hvis du føler deg generøs og vil donere, klikk her
- Donasjoner til Sonarr: Hvis du føler deg generøs og vil donere til prosjektet som startet det hele, klikk her
- Kilde: GitHub
- Funksjonsforespørsler: Har du en flott idé, legg den til her

# Oppgaver

## Planlagt

- Denne delen viser alle planlagte oppgaver som Readarr kjører

- Sjekk applikasjonsoppdatering - Dette vil kjøre på den angitte planen i brukergrensesnittet og sjekke om Readarr er på den nyeste versjonen, deretter utløse oppdateringsskriptet for å oppdatere Readarr. Innstillinger => Oppdatering

> Merk: Hvis du bruker Docker, vil ikke dette oppdatere beholderen din, da det må lastes ned et nytt bilde.
{.is-warning}

- Sikkerhetskopiering - Dette vil kjøre en sikkerhetskopi av Readarrs database etter en angitt plan. Mer informasjon om dette finner du her. Mer informasjon om sikkerhetskopiering finner du under System => Sikkerhetskopiering.
- Sjekk helse - Sjekk helsen vil kjøre på den angitte planen i brukergrensesnittet og sjekke den generelle helsen til Readarr. For å se en liste over mulige helseproblemer, se wikien om helsesjekker.
- Vedlikehold - På den angitte planen i brukergrensesnittet vil dette støvsuge, feie og støvsuge gulvene, vaske, skinne og til og med lage fine, ryddige små notater bare for deg. Men det tar ikke ut søpla. Det ble bare ikke betalt nok for det.
- Synkroniser importliste - På den angitte planen i brukergrensesnittet vil dette kjøre listene dine og importere eventuelle nye bøker. Mer informasjon om lister finner du under Innstillinger => Lister.
- Rens opp meldinger - På den angitte planen i brukergrensesnittet rydder dette opp i meldingene som vises i nedre venstre hjørne av Readarr
- Oppdater forfatter - Dette går gjennom og oppdaterer alle forfattere i biblioteket ditt.
- Oppdater overvåkede nedlastinger - Dette går gjennom og oppdaterer nedlastingskøen som ligger under Aktivitet. Det pinger i utgangspunktet nedlastingsklienten din for å sjekke ferdige nedlastinger.
- Skann mapper på nytt - Dette skanner alle bokmapper for å se om en bok eksisterer eller ikke, og oppdaterer statusen deretter.
- RSS-synkronisering - Dette vil kjøre RSS-synkroniseringen. Dette kan endres i innstillinger => alternativer. Mer informasjon om RSS-funksjonen finner du i vår FAQ
  
> Alle disse oppgavene kan kjøres manuelt utenom planlagte tider ved å klikke på ikonet helt til høyre for hver av oppgavene.
{.is-info}

## Kø

Køen viser kjørende og kommende oppgaver, samt en historikk over nylig kjørte oppgaver og hvor lang tid disse oppgavene tok.

# Sikkerhetskopi

> Hvis du vil vite hvordan du sikkerhetskopierer/gjenoppretter Readarr-instansen din, klikk [her](/readarr/faq).
{.is-info}

- Innenfor sikkerhetskopiseksjonen vil du få presentert tidligere sikkerhetskopier (med mindre du har en fersk installasjon som ikke har laget noen sikkerhetskopier ennå).
  
- Sikkerhetskopier nå - Denne muligheten vil utløse en manuell sikkerhetskopi av Readarrs database
- Gjenopprett sikkerhetskopi - Dette vil åpne en ny skjerm for å gjenopprette fra en tidligere sikkerhetskopi
  - Ved å velge Velg fil vil dette få nettleseren din til å åpne en dialogboks for å gjenopprette fra en Readarr-zipsikkerhetskopi
  
- Hvis du har noen tidligere sikkerhetskopier og vil laste dem ned fra Readarr for å plassere dem på en ikke-standard plassering, kan du bare velge en av disse filene for å laste dem ned
- Til høyre for hver av de tidligere nedlastingen har du to alternativer.
  - Gjenopprett (Klokkeikon) - For å gjenopprette fra en tidligere sikkerhetskopi - Dette vil åpne et nytt vindu for å bekrefte at du vil gjenopprette fra denne sikkerhetskopien
  - Slett (Søppelbøtte) - For å slette en tidligere sikkerhetskopi

# Oppdateringer

- Oppdateringsskjermen vil vise de siste 5 oppdateringene som er gjort, samt den gjeldende versjonen du er på.
- Denne siden vil også vise oppdateringsnotatene fra utviklerne som forteller deg hva som er blitt fikset eller lagt til i Readarr (Jubel!)
  
> En vedlikeholdsutgivelse inneholder feilrettinger og andre forskjellige forbedringer. Ta en titt på commit-historikken for spesifikke detaljer.
{.is-info}

# Hendelser

- Hendelsesfanen vil vise deg hva som har skjedd i Readarr. Dette kan brukes til å diagnostisere noen mindre problemer. Dette erstatter imidlertid ikke sporingslogger som diskuteres i Logging.

> Hendelser tilsvarer INFO-logger. {.is-info}

- Komponenter - Denne kolonnen vil fortelle deg hvilken komponent i Readarr som har blitt utløst
- Melding - Denne kolonnen vil fortelle deg hvilken melding som er sendt fra komponenten i forrige kolonne.
- Tannhjulikon - Dette alternativet lar deg endre hvor mange komponenter/meldinger som vises per side (Standard er 50)
- Alternativer øverst på siden
  - Oppdater - Dette alternativet vil oppdatere gjeldende side og hente en ny hendelseslogg
  - Tøm - Dette vil tømme gjeldende hendelseslogg slik at du kan begynne på nytt

# Loggfiler

- Denne siden lar deg laste ned og se hvilke loggfiler som er tilgjengelige for Readarr

- På toppraden er det flere alternativer som lar deg kontrollere loggfilene dine.

- Øverst til venstre på toppraden er det en rullegardinmeny som lar deg bytte mellom loggfiler og oppdateringsloggfiler
  - Loggfiler - Hoveddelen av ethvert støtteproblem, mer om loggfiler finner du her.
  - Oppdateringsloggfiler - Dette vil vise loggfilene som er knyttet til Readarrs oppdateringsskript

> Hvis du bruker Docker, vil dette være tomt, da du bør oppdatere ved å laste ned et nytt Docker-bilde
{.is-info}

- Oppdater - Dette vil oppdatere gjeldende side og vise eventuelt nyopprettede logger
- Slett - Dette vil slette alle logger og la deg begynne på nytt
- Filnavn - Dette vil vise filnavnet knyttet til loggen
- Sist skrevet - Dette er lokal tid da denne bestemte loggfilen ble skrevet til.
  - Readarr bruker rullerende loggfiler begrenset til 1 MB hver. Den gjeldende loggfilen er alltid readarr.txt, for de andre filene er readarr.0.txt den nest nyeste (jo høyere nummer, jo eldre er den) opp til totalt 51 loggfiler. Denne loggfilen inneholder `fatal`, `error`, `warn` og `info`-oppføringer.
  - Når feilsøkingslogg nivå er aktivert, vil det være tilgjengelige ekstra readarr.debug.txt rullerende loggfiler, opptil 51 filer. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info` og `debug`-oppføringer. Den dekker vanligvis en periode på ~40 timer.
  - Når sporingslogg nivå er aktivert, vil det være tilgjengelige ekstra readarr.trace.txt rullerende loggfiler, opptil 51 filer. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-oppføringer. På grunn av sporingsnøyaktighet dekker den bare et par timer maksimalt.