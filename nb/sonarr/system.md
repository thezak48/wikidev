---
title: Sonarr System
description: 
published: true
date: 2023-08-09T15:27:13.123Z
tags: 
editor: markdown
dateCreated: 2021-09-08T17:58:43.288Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Status](#status)
  - [Helse](#helse)
    - [Systemadvarsler](#systemadvarsler)
      - [For øyeblikket installert .NET Framework er gammelt og ikke støttet](#for-%C3%B8yeblikket-installert-net-framework-er-gammelt-og-ikke-st%C3%B8ttet)
      - [For øyeblikket installert .NET Framework er støttet, men oppgradering anbefales](#for-%C3%B8yeblikket-installert-net-framework-er-st%C3%B8ttet-men-oppgradering-anbefales)
      - [For øyeblikket installert mono-versjon er gammel og ikke støttet](#for-%C3%B8yeblikket-installert-mono-versjon-er-gammel-og-ikke-st%C3%B8ttet)
      - [Pakkevedlikeholdermelding](#pakkevedlikeholdermelding)
      - [Ny oppdatering er tilgjengelig](#ny-oppdatering-er-tilgjengelig)
      - [Kan ikke installere oppdatering fordi oppstartsmappen og/eller brukergrensesnittmappen ikke kan skrives til av brukeren](#kan-ikke-installere-oppdatering-fordi-oppstartsmappen-ogeller-brukergrensesnittmappen-ikke-kan-skrives-til-av-brukeren)
      - [Kan ikke installere oppdatering fordi oppstartsmappen er i en App Translocation-mappe](#kan-ikke-installere-oppdatering-fordi-oppstartsmappen-er-i-en-app-translocation-mappe)
      - [Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering](#oppdatering-vil-ikke-v%C3%A6re-mulig-for-%C3%A5-forhindre-sletting-av-appdata-ved-oppdatering)
      - [Klarte ikke å løse IP-adressen for den konfigurerte proxyverten](#klarte-ikke-%C3%A5-l%C3%B8se-ip-adressen-for-den-konfigurerte-proxyverten)
      - [Proxy mislyktes i testen](#proxy-mislyktes-i-testen)
      - [Systemtiden er mer enn 1 dag feil](#systemtiden-er-mer-enn-1-dag-feil)
      - [MediaInfo-biblioteket kunne ikke lastes](#mediainfo-biblioteket-kunne-ikke-lastes)
      - [Mono Legacy TLS er aktivert](#mono-legacy-tls-er-aktivert)
    - [Nedlastingsklienter](#nedlastingsklienter)
      - [Ingen nedlastingsklient er tilgjengelig](#ingen-nedlastingsklient-er-tilgjengelig)
      - [Kan ikke kommunisere med nedlastingsklienten](#kan-ikke-kommunisere-med-nedlastingsklienten)
      - [Nedlastingsklienter er utilgjengelige på grunn av feil](#nedlastingsklienter-er-utilgjengelige-p%C3%A5-grunn-av-feil)
      - [Aktiver håndtering av fullførte nedlastinger](#aktiver-h%C3%A5ndtering-av-fullf%C3%B8rte-nedlastinger)
      - [Laster ned til rotmappen](#laster-ned-til-rotmappen)
      - [Håndtering av fullførte nedlastinger er deaktivert](#h%C3%A5ndtering-av-fullf%C3%B8rte-nedlastinger-er-deaktivert)
    - [Indekser](#indekser)
      - [Ingen indekser er tilgjengelige med automatisk søk aktivert, Sonarr vil ikke gi noen automatiske søkeresultater](#ingen-indekser-er-tilgjengelige-med-automatisk-s%C3%B8k-aktivert-sonarr-vil-ikke-gi-noen-automatiske-s%C3%B8keresultater)
      - [Ingen indekser er tilgjengelige med RSS-synkronisering aktivert, Sonarr vil ikke hente nye utgivelser automatisk](#ingen-indekser-er-tilgjengelige-med-rss-synkronisering-aktivert-sonarr-vil-ikke-hente-nye-utgivelser-automatisk)
      - [Ingen indekser er aktivert](#ingen-indekser-er-aktivert)
      - [Aktiverte indekser støtter ikke søk](#aktiverte-indekser-st%C3%B8tter-ikke-s%C3%B8k)
      - [Ingen indekser er tilgjengelige med interaktivt søk aktivert](#ingen-indekser-er-tilgjengelige-med-interaktivt-s%C3%B8k-aktivert)
      - [Indekser er utilgjengelige på grunn av feil](#indekser-er-utilgjengelige-p%C3%A5-grunn-av-feil)
      - [Jackett All Endpoint Used](#jackett-all-endpoint-used)
        - [Løsninger](#l%C3%B8sninger)
    - [Media og lister](#media-og-lister)
      - [Serier fjernet fra TheTVDB](#serier-fjernet-fra-thetvdb)
      - [Lister er utilgjengelige på grunn av feil](#lister-er-utilgjengelige-p%C3%A5-grunn-av-feil)
      - [Importliste mangler rotmappe](#importliste-mangler-rotmappe)
      - [Mangler rotmappe](#mangler-rotmappe)
      - [Mangler rotmappe](#mangler-rotmappe-1)
      - [Seriesøkningsbane er skrivebeskyttet](#series%C3%B8kningsbane-er-skrivebeskyttet)
  - [Diskplass](#diskplass)
  - [Om](#om)
  - [Mer informasjon](#mer-informasjon)
- [Oppgaver](#oppgaver)
  - [Planlagt](#planlagt)
  - [Kø](#k%C3%B8)
- [Sikkerhetskopi](#sikkerhetskopi)
- [Oppdateringer](#oppdateringer)
- [Hendelser](#hendelser)
- [Loggfiler](#loggfiler)

# Status

## Helse

- Denne siden inneholder en liste over helsekontrollfeil. Disse helsekontrollene utføres periodisk av Sonarr og ved visse hendelser. De resulterende advarslene og feilene er oppført her for å gi råd om hvordan du løser dem.

### Systemadvarsler

#### For øyeblikket installert .NET Framework er gammelt og ikke støttet

- Sonarr bruker .NET Framework. Vi må bygge Sonarr mot den laveste støttede versjonen som fortsatt brukes av brukerne våre. Av og til øker vi versjonen vi bygger mot for å kunne bruke nye funksjoner. Tydeligvis har du ikke brukt de riktige Windows-oppdateringene på en stund og må oppgradere .NET for å kunne bruke nyere versjoner av Sonarr.

- Å oppgradere .NET Framework er veldig enkelt på Windows, selv om det ofte krever en omstart.

#### For øyeblikket installert .NET Framework er støttet, men oppgradering anbefales

- Sonarr bruker .NET Framework. Vi må bygge Sonarr mot den laveste støttede versjonen som fortsatt brukes av brukerne våre. Å oppgradere til nyere versjoner gjør det mulig for oss å bygge mot nyere versjoner og bruke nye rammeverksfunksjoner.

- Å oppgradere .NET Framework er veldig enkelt på Windows, selv om det ofte krever en

#### For øyeblikket installert mono-versjon er gammel og ikke støttet

- Sonarr v4 er skrevet i .NET og v3 krever Mono. Mono 5.20 er det absolutte minimum for Sonarr.
- Oppgraderingsprosedyren for Mono varierer per plattform.

> Mono støttes ikke lenger fra og med Sonarr versjon 4.0
{.is-warning}

#### For øyeblikket installert SQLite-versjon støttes ikke

- Sonarr lagrer dataene sine i en SQLite-database. SQLite3-biblioteket som er installert på systemet ditt, er for gammelt. Sonarr krever minst versjon 3.9.0.

> Merk at Sonarr bruker `libSQLite3.so`, som kan være inkludert eller ikke i en oppgraderingspakke for SQLite3.
{.is-info}

#### Pakkevedlikeholdermelding

- Pakkevedlikeholderen din har en melding til deg. Dette styres av vedlikeholderen din og ikke Sonarr.

#### Ny oppdatering er tilgjengelig

- Fryd deg, utviklerne har gitt ut en ny oppdatering. Dette betyr generelt sett fantastiske nye funksjoner og fikset hauger med feil (ikke sant?). Tydeligvis har du ikke aktivert automatisk oppdatering, så du må finne ut hvordan du oppdaterer på plattformen din. Å trykke på Installer-knappen på siden System => Oppdateringer er sannsynligvis et godt utgangspunkt.

> Denne advarselen vises ikke hvis gjeldende versjon er mindre enn 14 dager gammel
{.is-info}

#### Kan ikke installere oppdatering fordi oppstartsmappen og/eller brukergrensesnittmappen ikke kan skrives til av brukeren

{#kan-ikke-installere-oppdatering-fordi-brukergrensesnittmappen-ikke-kan-skrives-til-av-brukeren}

{#kan-ikke-installere-oppdatering-fordi-oppstartsmappen-ikke-kan-skrives-til-av-brukeren}

Dette betyr at Sonarr ikke vil kunne oppdatere seg selv. Du må oppdatere Sonarr manuelt eller angi tillatelsene for Sonarrs oppstartskatalog (installasjonskatalogen) for å tillate at Sonarr oppdaterer seg selv.

#### Kan ikke installere oppdatering fordi oppstartsmappen er i en App Translocation-mappe

I macOS Sierra la Apple til en merkelig sikkerhetsfunksjon kalt App Translocation (noen ganger kjent som Gatekeeper Path Randomization), som betyr at etter at du har lastet ned en applikasjon, hvis du ikke flytter den resulterende applikasjonen et sted (hvor som helst!), med Finder (du må bruke Finder!), vil applikasjonen kjøres som om den er plassert på en tilfeldig valgt bane av systemet.

#### Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering

Sonarr oppdaget at AppData-mappen for operativsystemet ditt er plassert inne i mappen som inneholder Sonarr-binærene. Normalt sett ville det være C:\ProgramData for Windows og ~/.config for Linux.

Se på System => Info for å se gjeldende AppData- og oppstartskataloger.
Dette betyr at Sonarr ikke vil kunne oppdatere seg selv uten å risikere tap av data.
Hvis du bruker Linux, må du sannsynligvis endre hjemmekatalogen for brukeren som kjører Sonarr, og kopiere innholdet i den gjeldende ~/.config/Sonarr-mappen for å bevare databasen din.

#### Klarte ikke å løse IP-adressen for den konfigurerte proxyverten

Gjennomgå proxyinnstillingene dine og forsikre deg om at de er nøyaktige
Sørg for at proxyen din er aktiv, kjører og tilgjengelig

#### Proxy mislyktes i testen

Den konfigurerte proxyen mislyktes i testen, gjennomgå HTTP-feilen som ble oppgitt og/eller sjekk loggene for mer informasjon.

#### Systemtiden er mer enn 1 dag feil

Systemtiden er mer enn 1 dag feil. Planlagte oppgaver kan ikke kjøre riktig før tiden er korrigert
Gjennomgå systemtiden din og forsikre deg om at den er synkronisert med en autoritativ tidsserver og er nøyaktig

#### MediaInfo-biblioteket kunne ikke lastes

MediaInfo-biblioteket kunne ikke lastes. Sonarr krever MediaInfo (`libmediainfo`) for å evaluere videoparametrene til filer.

#### Mono Legacy TLS er aktivert

{#sonarr-mono-4.x-tls-workaround-still-enabled-consider-removing-mono_tls_provider-legacy-environment-option}

Mono 4.x TLS-omgåelsen er fortsatt aktivert, vurder å fjerne MONO_TLS_PROVIDER=legacy-miljøalternativet.

### Nedlastingsklienter

#### Ingen nedlastingsklient er tilgjengelig

En riktig konfigurert og aktivert nedlastingsklient er nødvendig for at Sonarr skal kunne laste ned medier. Siden Sonarr støtter forskjellige nedlastingsklienter, bør du finne ut hvilken som passer best for dine behov. Hvis du allerede har en nedlastingsklient installert, bør du konfigurere Sonarr til å bruke den og opprette en kategori. Se Innstillinger => Nedlastingsklient.

#### Kan ikke kommunisere med nedlastingsklienten

Sonarr kunne ikke kommunisere med den konfigurerte nedlastingsklienten. Kontroller om nedlastingsklienten er operativ og dobbeltsjekk URL-en. Dette kan også indikere en autentiseringsfeil.
Dette skyldes vanligvis en feil konfigurert nedlastingsklient. Noen ting du vanligvis kan sjekke:
IP-adressen til nedlastingsklienten hvis den er på samme fysiske maskin, er dette vanligvis 127.0.0.1
Portnummeret som nedlastingsklienten bruker, disse er fylt ut med standard portnummer, men hvis du har endret det, må du ha det samme nummeret angitt i Sonarr.
Sørg for at SSL-kryptering ikke er slått på hvis du bruker både Sonarr-instansen og nedlastingsklienten på et lokalt nettverk. Se SSL-FAQ-en for mer informasjon.

#### Nedlastingsklienter er utilgjengelige på grunn av feil

En eller flere av nedlastingsklientene dine svarer ikke på forespørslene som Sonarr sender. Derfor har Sonarr bestemt seg for å midlertidig slutte å spørre nedlastingsklienten på sin normale 1-minutters syklus, som vanligvis brukes til å spore aktive nedlastinger og importere ferdige nedlastinger. Imidlertid vil Sonarr fortsette å prøve å sende nedlastinger til klienten, men vil mest sannsynlig mislykkes.
Du bør inspisere System => Loggfiler for å se hva årsaken til feilene er.
Hvis du ikke lenger bruker denne nedlastingsklienten, bør du deaktivere den i Sonarr for å unngå feilene.

#### Aktiver håndtering av fullførte nedlastinger

- Sonarr krever håndtering av fullførte nedlastinger for å kunne importere filer som ble lastet ned av nedlastingsklienten. Det anbefales å aktivere håndtering av fullførte nedlastinger.
(Håndtering av fullførte nedlastinger er aktivert som standard...)

#### Docker dårlig ekstern baneavbildning

- Denne feilen er vanligvis assosiert med dårlige Docker-baner i enten nedlastingsklienten eller Sonarr

- Et eksempel på dette ville være:
  - Nedlastingsklient: Nedlastingsbane: /mnt/user/downloads:/downloads
  - Radarr: Nedlastingsbane: /mnt/user/downloads:/data
- I dette eksemplet plasserer nedlastingsklienten nedlastingen i /downloads og forteller derfor Radarr når den er ferdig at den ferdige filmen er i /downloads. Sonarr kommer deretter og sier "Ok, flott, la meg sjekke i /downloads" Vel, inne i Radarr har du ikke tildelt en /downloads-bane, du har tildelt en /data-bane, så det kaster denne feilen.
- Den enkleste løsningen på dette er KONSISTENS, hvis du bruker en ordning i nedlastingsklienten din, bruk den over hele linjen.

- Team Sonarr er stor fan av å bare bruke /data.
  - Nedlastingsklient: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Nå kan du innenfor nedlastingsklienten spesifisere hvor i /data du vil plassere nedlastingen din, dette varierer avhengig av klienten, men du bør kunne fortelle den "Ja, nedlastingsklient, plasser filene mine i." /data/torrents (eller usenet)/movies og siden du brukte /data i Radarr når nedlastingsklienten forteller Radarr at den er ferdig, vil Radarr komme og si "Supert, jeg har en /data og jeg kan også se /torrents (eller usenet)/movies alt er riktig i verden."
- Det finnes mange gode veiledninger: vår wiki [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Disse veiledningene legger stor vekt på hardlenker og atombevegelser, men konseptet med containere og hvordan banekartlegging fungerer, er kjernen i disse diskusjonene.

- Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mer informasjon.

#### Laster ned til rotmappen

{#nedlastinger-i-rotmappen}

- Innen applikasjonen defineres en rotmappe som den konfigurerte mediebibliotekmappen. Dette er ikke rotmappen til et monteringspunkt. Nedlastingsklienten din laster ned ufullstendige eller fullførte nedlastinger (eller flytter fullførte nedlastinger) til rotmappen (biblioteket) din.
- Dette forårsaker ofte problemer - inkludert tap av data - og bør ikke gjøres. For å løse dette, endre nedlastingsklienten slik at den ikke plasserer nedlastinger i rotmappen din. Merk at 'plassering' også inkluderer om nedlastingsklientens kategori er satt til rotmappen din eller om NZBGet/SABnzbd har sortering aktivert og sorterer til rotmappen din.
- Vær oppmerksom på at denne sjekken ser på alle definerte/konfigurerte rotmapper som er lagt til, ikke bare rotmapper som for øyeblikket er i bruk. Med andre ord, bør ikke mappen der nedlastingsklienten din laster ned eller flytter fullførte nedlastinger til, være den samme mappen du har konfigurert som rot-/biblioteks-/endelig destinasjonsmappe for medier i *arr-applikasjonen.
- Konfigurerte rotmapper (også kjent som biblioteksmapper) finner du i [Innstillinger => Mediebehandling => Rotmapper](/sonarr/settings/#root-folders)
- Et eksempel er hvis nedlastingen din går til `/data/downloads`, så har du en rotmappe satt til `/data/downloads`.
- Det anbefales å bruke baner som `/data/media/` for rotmappen/biblioteket ditt og `/data/downloads/` for nedlastingen din.
- Gå gjennom vår [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mer informasjon om riktig og optimal oppsett av baner. Merk at konseptene gjelder for både Docker og ikke-Docker

> Nedlastingsmappen der nedlastingsklienten din plasserer nedlastningene og rot-/biblioteksmappen din MÅ være separate. \*Arr vil importere filen(e) fra nedlastingsklientens mappe til biblioteket ditt. Nedlastingsklienten skal ikke flytte noe eller laste ned noe til biblioteket ditt.
{.is-warning}

#### Dårlige innstillinger for nedlastingsklient

- Plasseringen der nedlastingsklienten din laster ned filer, forårsaker problemer. Sjekk loggene for mer informasjon. Dette kan være tillatelser eller forsøk på å gå fra Windows til Linux eller Linux til Windows uten en ekstern banekartlegging.

#### Dårlig ekstern baneavbildning

- Plasseringen der nedlastingsklienten din laster ned filer, forårsaker problemer. Sjekk loggene for mer informasjon. Dette kan være tillatelser eller forsøk på å gå fra Windows til Linux eller Linux til Windows uten en ekstern banekartlegging. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mer informasjon.

#### Tillatelsesfeil

- Sonarr eller brukeren sonarr kjører som, kan ikke få tilgang til plasseringen der nedlastingsklienten din laster ned filer. Dette er vanligvis et tillatelsesproblem.

#### Ekstern fil ble fjernet under behandling

- En fil som er tilgjengelig via en ekstern banekartlegging, ser ut til å ha blitt fjernet før behandlingen var fullført.

#### Bruker ekstern bane, og importen mislyktes

- Sjekk loggene for mer informasjon; Se våre feilsøkingsguider

### Laster ned til rotmappen

{#downloads-in-root-folder}

- Innenfor applikasjonen defineres en rotmappe som den konfigurerte mediebibliotekmappen. Dette er ikke rotmappen til et monteringspunkt. Nedlastingsklienten din har en ufullstendig eller fullstendig (eller flytter fullførte nedlastinger) til rotmappen (biblioteket) ditt.
- Dette forårsaker ofte problemer - inkludert tap av data - og bør ikke gjøres. For å løse dette, endre nedlastingsklienten din slik at den ikke plasserer nedlastinger i rotmappen din. Merk at 'plassering' også inkluderer om nedlastingsklienten din kategori er satt til rotmappen din, eller hvis NZBGet/SABnzbd har sortering aktivert og sorterer til rotmappen din.
- Vær oppmerksom på at denne sjekken ser på alle definerte/konfigurerte rotmapper som er lagt til, ikke bare rotmapper som for øyeblikket er i bruk. Med andre ord bør ikke mappen der nedlastingsklienten din laster ned eller flytter fullførte nedlastinger til, være den samme mappen du har konfigurert som rot-/bibliotek-/endelig mediamålmappe i *arr-applikasjonen.
- Konfigurerte rotmapper (også kjent som bibliotekmapper) finner du under [Innstillinger => Mediehåndtering => Rotmapper](/sonarr/settings/#root-folders)
- Et eksempel er hvis nedlastingen din går til `/data/downloads`, så har du en rotmappe satt som `/data/downloads`.
- Det anbefales å bruke stier som `/data/media/` for rotmappen/biblioteket ditt og `/data/downloads/` for nedlastingen din.
- Se gjennom vår [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mer informasjon om riktig og optimal oppsett av stier. Merk at konseptene gjelder både for docker og ikke-docker.

> Nedlastingsmappen der nedlastingsklienten din plasserer nedlastinger, og rot-/bibliotekmappen din MÅ være separate. \*Arr vil importere filene fra nedlastingsklientens mappe til biblioteket ditt. Nedlastingsklienten bør ikke flytte noe eller laste ned noe til biblioteket ditt.
{.is-warning}

#### Behandling av fullførte nedlastinger er deaktivert

{#completedfailed-download-handling}

- Det er nødvendig å bruke behandling av fullførte nedlastinger siden det gir bedre kompatibilitet for pakking og etterbehandlingslogikk for forskjellige nedlastingsklienter. Med dette vil Sonarr bare importere en nedlasting når nedlastingsklienten rapporterer at den er klar.
- Hvis behandling av fullførte nedlastinger er deaktivert:
  - Alle importeringer må håndteres manuelt
  - Denne helsesjekken vil vedvare og kan ikke avvises eller deaktiveres
  - Episoder vil alltid mangle i Sonarr og være tilgjengelige for å bli hentet i all evighet
    - Episoder som manuelt er flyttet og omdøpt av brukeren til seriens mappe i Sonarrs bibliotekmappe, vil muligens bli plukket opp av den to ganger daglige rescanen hvis de er riktig navngitt og dermed ikke mangle på det tidspunktet.
  - Brukeren må manuelt fjerne overvåkingen eller konfigurere et tilpasset skript for å fjerne overvåkingen av episoder.
  - FlexGet er sannsynligvis et bedre verktøy for ens brukstilfelle hvis de ikke ønsker å bruke Sonarrs funksjonalitet for mediebibliotekhåndtering og bare trenger noe for å analysere RSS-feeder og sende utgivelser til nedlastingsklienten

> \* Behandling av fullførte nedlastinger fungerer bare riktig hvis nedlastingsklienten og Sonarr er på samme maskin, siden den får banen som skal importeres direkte fra nedlastingsklienten, ellers trengs det en ekstern kartlegging.
> \* Behandling av fullførte nedlastinger krever at Sonarr har lese- og skrivetilgang til mappen for fullførte nedlastinger
{.is-warning}

### Indekser

#### Ingen indekser tilgjengelig med aktivert automatisk søk, Sonarr vil ikke gi noen automatiske søkeresultater

- Enkelt sagt har du ingen av indeksene dine satt til å tillate automatisk søk
Gå til Innstillinger > Indekser, velg en indeks du vil tillate automatisk søk og klikk deretter på Lagre.

#### Ingen indekser tilgjengelig med aktivert RSS-synkronisering, Sonarr vil ikke hente nye utgivelser automatisk

{#no-indexers-available-with-rss-sync-enabled,-sonarr-will-not-grab-new-releases-automatically}
{#all-rss-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Sonarr bruker RSS-feeden til å plukke opp nye utgivelser etter hvert som de kommer. [Se FAQen for mer informasjon](/sonarr/faq#how-does-sonarr-find-episodes)
- For å rette opp dette problemet går du til Innstillinger > Indekser, velg en indeks du har og aktiver RSS-synkronisering.

#### Ingen indekser er aktivert

- Sonarr krever at indekser er aktivert for å kunne oppdage nye utgivelser. Alle indeksene dine er deaktivert eller du har ikke lagt til noen indekser.

#### Aktiverte indekser støtter ikke søk

{#all-search-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Ingen av de aktiverte og tilgjengelige indeksene støtter søk. Dette betyr at Sonarr bare vil kunne finne nye utgivelser via RSS-feedene. Men søk etter serier (enten automatisk søk eller manuelt søk) vil aldri gi noen resultater. Den eneste måten å rette det på er å legge til en annen indeks.

#### Ingen indekser tilgjengelig med aktivert interaktivt søk

{#no-indexers-available-with-interactive-search-enabled-sonarr-will-not-provide-any-interactive-search-results}

- Ingen av de aktiverte og tilgjengelige indeksene støtter interaktivt søk. Dette betyr at applikasjonen bare vil kunne finne nye utgivelser via RSS-feedene eller en automatisk søk.

#### Indekser er utilgjengelige på grunn av feil

- Feil oppstod mens Sonarr prøvde å bruke en av indeksene dine. For å begrense forsøkene vil Sonarr ikke bruke indeksen i en økende tidsperiode (opptil 24 timer).
- Dette mekanismen utløses hvis Sonarr ikke klarte å få et svar fra indeksen (kan skyldes DNS, proxy/vpn-tilkobling, autentisering eller en indeksfeil), eller ikke klarte å hente nzb-/torrent-filen fra indeksen. Vennligst sjekk loggene for å finne ut hvilken type feil som forårsaket problemet.
- Du kan forhindre denne advarselen ved å deaktivere den berørte indeksen.
- Kjør en `Test` på indeksen for å tvinge Sonarr til å sjekke indeksen på nytt; vær oppmerksom på at helsesjekkadvarselen ikke alltid forsvinner umiddelbart, og du må kanskje kjøre oppgaven `Sjekk helse`

#### Jackett All Endpoint brukt

- Jackett /all-endepunktet er praktisk, men det er den eneste fordelen. Alt annet er potensielle problemer, så det er nå nødvendig å legge til hver enkelt tracker individuelt.
- [Selv Jacketts utviklere sier at det bør unngås og ikke brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Å bruke /all-endepunktet har ingen fordeler, bare ulemper:
  - du mister kontrollen over indeksspesifikke innstillinger (kategorier, søkemåter, osv.)
  - blanding av søkemåter (IMDB, søk, osv.) kan føre til resultater av lav kvalitet
  - indeksspesifikke kategorier (\>= 100000) kan ikke brukes.
  - treg indekser vil bremse ned den generelle ytelsen
  - totalt antall resultater er begrenset til 1000
  - hvis en av trackerne i /all returnerer en feil, vil \*Arr deaktivere den og nå får du ingen resultater.

##### Løsninger

- Legg til hver enkelt tracker i Jackett manuelt som en indeks i \*Arr
- Sjekk ut [Prowlarr](/prowlarr) som kan synkronisere indekser til \*Arr og er fra Lidarr/Radarr/Readarr-utviklingsteamet.
- Sjekk ut [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisere indekser til \*Arr. Men ikke bruk deres enkeltstående aggregerte endepunkt, bruk `multi` hvis synkronisering skal brukes.

### Medier og lister

#### Serier fjernet fra TheTVDB

- Den berørte serien/seriene ble fjernet fra [The TVDb](https://thetvdb.com). Dette skjer vanligvis fordi serien er en duplikat eller betraktes som en del av en annen serie. Alternativt kan TVDb behandle den som en serie; forhåpentligvis gjør også TMDb det slik at [Radarr](/radarr) kan brukes i stedet. For å rette opp dette må du fjerne den berørte serien og legge til riktig serie hvis det er aktuelt.

#### Lister er utilgjengelige på grunn av feil

{#import-lists-are-unavailable-due-to-failures}

- Dette betyr vanligvis at Sonarr ikke lenger kan kommunisere via API eller ved å logge inn på den valgte listeleverandøren. Hvis problemet vedvarer, er det best å kontakte dem for å utelukke dem, da systemene deres kan være overbelastet fra tid til annen.
- Gå gjennom System => Hendelser filtrert for Advarsel (Advarsler og Feil) for å se tidligere feil, eller sjekk loggene for detaljer.

#### Importliste mangler rotmappe

- En eller flere av importlistene dine er konfigurert til en rotmappe som ikke er tilgjengelig for Sonarr.
- Dette kan være problemer med tillatelser, manglende montering eller rett og slett behov for å oppdatere listene etter å ha reorganisert oppsettet ditt.

#### Manglende rotmappe

- En rotmappe er lagt til i Sonarr og eksisterer ikke eller er ikke tilgjengelig
- Denne feilen identifiseres vanligvis hvis en serie ser etter en rotmappe, men den rotmappen er ikke lenger tilgjengelig.
- Denne feilen kan også oppstå hvis en liste fremdeles peker på en rotmappe, men den rotmappen ikke lenger er tilgjengelig.
- Hvis du vil fjerne denne advarselen, finn bare serien som fortsatt bruker den gamle rotmappen, og rediger den til riktig rotmappe.

- Enkleste måten å finne problemserien på er å:

  - Gå til fanen for massebehandling
  - Opprett et tilpasset filter med den gamle rotmappen
  - Velg massebehandling i toppmenyen, og velg den nye rotbanen du vil flytte disse seriene til fra rullegardinmenyen for rotbaner.
  - Deretter får du en popup som sier Vil du flytte seriemappene til 'rotbane'? Dette vil også si Dette vil også omdøpe seriemappen i henhold til seriemappeformatet i innstillingene. Velg bare Nei hvis du ikke vil at Lidarr skal flytte filene dine
  - Kjør oppgaven Sjekk helse i System => Oppgaver

#### Seriemappe-monteringen er skrivebeskyttet

{#series-mount-ro}

En montering som inneholder en seriemappe er skrivebeskyttet og kan ikke skrives til av brukeren Sonarr kjører som.

## Diskplass

- Denne delen viser tilgjengelig diskplass
- I Docker kan dette være vanskelig, da det vanligvis viser tilgjengelig plass innenfor Docker-bildet ditt.

## Om

- Dette vil fortelle deg om den nåværende installasjonen av Sonarr.

## Mer informasjon

- Hjemmeside: Sonarrs [hjemmeside](https://www.sonarr.tv)
- Wiki: Du er allerede her.
- Reddit: [r/sonarr](https://www.reddit.com/r/sonarr)
- Discord: Bli med i vår [discord](https://discord.sonarr.tv/)
- Donasjoner: Hvis du føler deg generøs og vil donere, klikk [her](https://sonarr.tv/donate).
- Kildekode: [GitHub](https://www.github.com/sonarr/sonarr)
- Funksjonsforespørsler: Har du en flott idé, legg den til [her](https://www.github.com/sonarr/sonarr/issues).

# Oppgaver

## Planlagt

- Denne delen viser alle planlagte oppgaver som Sonarr kjører

- Sjekk applikasjonsoppdatering - Dette vil kjøre hver på den viste planen i brukergrensesnittet, sjekke om Sonarr er på den nyeste versjonen og deretter utløse oppdateringsskriptet for å oppdatere Sonarr. Innstillinger => Oppdatering

> Merk: Hvis du bruker Docker, vil dette ikke oppdatere beholderen din, da det må lastes ned et nytt bilde.
{.is-warning}

- Sikkerhetskopi - Dette vil kjøre en sikkerhetskopi av Sonarrs database etter en angitt plan. Mer informasjon om dette finner du her. Mer informasjon om sikkerhetskopier finner du under System => Sikkerhetskopier.
- Sjekk helse - Sjekk helse vil kjøre på den viste planen i brukergrensesnittet og sjekke den generelle helsen til Sonarr. For å se en liste over mulige helseproblemer, se Wiki-innlegget om helsesjekker.
- Rens opp i resirkuleringsbøtten - Resirkuleringsbøtten tømmes på den viste planen i brukergrensesnittet. Dette vil bare bli brukt hvis resirkuleringsbøtten er satt i Filbehandling
- Vedlikehold - På den viste planen i brukergrensesnittet vil dette støve av alle spindelvev, feie og støvsuge gulvene, vaske, skinne og til og med lage fine, pent brettede notater bare for deg. Men den tar ikke ut søpla. Den ble bare ikke betalt nok for det.
- Synkroniser importliste - På den viste planen i brukergrensesnittet vil dette kjøre listene dine og importere eventuelle nye serier. Mer informasjon om lister finner du under Innstillinger => Lister.
- Rens opp i meldinger - På den viste planen i brukergrensesnittet rydder dette opp i meldingene som vises i nedre venstre hjørne av Sonarr
- Oppdater overvåkede nedlastinger - Dette går gjennom og oppdaterer nedlastingskøen som ligger under Aktivitet. Det pinger i utgangspunktet nedlastingsklienten din for å sjekke ferdige nedlastinger.
- Oppdater serier - Dette går gjennom og oppdaterer all metadata for alle overvåkede og ikke-overvåkede serier
- RSS-synkronisering - Dette vil kjøre RSS-synkroniseringen. Dette kan endres under Innstillinger => Indekser => Alternativer. Mer informasjon om RSS-funksjonen finner du i vår [FAQ](/sonarr/faq)
  
> Alle disse oppgavene kan kjøres manuelt utenom planlagte tider ved å klikke på ikonet helt til høyre for hver av oppgavene.
{.is-info}

## Kø

Køen viser kjørende og kommende oppgaver, samt en historikk over nylig kjørte oppgaver og hvor lang tid de oppgavene tok.

# Sikkerhetskopi

> Hvis du vil vite hvordan du sikkerhetskopierer/gjenoppretter Sonarr-instansen din, klikk [her](/sonarr/faq).
{.is-info}

I sikkerhetskopiseksjonen blir du presentert med tidligere sikkerhetskopier (med mindre du har en fersk installasjon som ikke har laget noen sikkerhetskopier ennå).
  
- Sikkerhetskopier nå - Denne muligheten vil utløse en manuell sikkerhetskopi av Sonarrs database
- Gjenopprett sikkerhetskopi - Dette vil åpne en ny skjerm for å gjenopprette fra en tidligere sikkerhetskopi
  - Ved å velge Velg fil vil dette be nettleseren din om å åpne en dialogboks for å gjenopprette fra en Sonarr-zipsikkerhetskopi
  
- Hvis du har noen tidligere sikkerhetskopier og vil laste dem ned fra Sonarr for å plassere dem på en ikke-standard plassering, kan du bare velge en av disse filene for å laste dem ned
- Til høyre for hver av de tidligere nedlastingen har du to alternativer.

  - Gjenopprett (Klokkeikon) - For å gjenopprette fra en tidligere sikkerhetskopi - Dette vil åpne et nytt vindu for å bekrefte at du vil gjenopprette fra denne sikkerhetskopien
  - Slett (Søppelbøtte) - For å slette en tidligere sikkerhetskopi

# Oppdateringer

Oppdateringsskjermen vil vise de 5 siste oppdateringene som er gjort, samt den nåværende versjonen du er på.
Denne siden vil også vise oppdateringsnotatene fra utviklerne som forteller deg hva som er blitt fikset eller lagt til i Sonarr (Jubel!)

> En vedlikeholdsutgivelse inneholder feilrettinger og andre forskjellige forbedringer. Ta en titt på forpliktelser på Github for spesifikke detaljer.
{.is-info}

# Hendelser

Hendelsesfanen vil vise deg hva som har skjedd i Sonarr. Dette kan brukes til å diagnostisere noen mindre problemer. Dette erstatter imidlertid ikke sporingslogger som diskuteres i Logging.

> Hendelser tilsvarer INFO-logger. {.is-info}

- Komponenter - Denne kolonnen vil fortelle deg hvilken komponent innenfor Sonarr som har blitt utløst
- Melding - Denne kolonnen vil fortelle deg hvilken melding som er sendt fra komponenten fra forrige kolonne.
- Tannhjulikon - Dette alternativet lar deg endre hvor mange komponenter/meldinger som vises per side (Standard er 50)
- Alternativer øverst på siden
  - Oppdater - Dette alternativet vil oppdatere gjeldende side og hente en ny hendelseslogg
  - Tøm - Dette vil tømme gjeldende hendelseslogg og la deg starte på nytt

# Loggfiler

- Denne siden lar deg laste ned og se hvilke gjeldende loggfiler som er tilgjengelige for Sonarr.

- På den øverste raden er det flere alternativer som lar deg kontrollere loggfilene dine.

- Øverst til venstre på den øverste raden er det en rullegardinmeny som lar deg bytte mellom loggfiler og oppdateringsloggfiler
  - Loggfiler - Hoveddelen av ethvert supportproblem, mer om loggfiler finner du her.
  - Oppdateringsloggfiler - Dette vil vise loggfilene som er tilknyttet Sonarrs oppdateringsskript

> Hvis du bruker Docker, vil dette være tomt, da du bør oppdatere ved å laste ned et nytt Docker-bilde.
{.is-info}

- Oppdater - Dette vil oppdatere gjeldende side og vise eventuelt nyopprettede logger
- Slett - Dette vil slette alle logger og la deg starte på nytt
- Filnavn - Dette vil vise filnavnet som er tilknyttet loggen
- Sist skrevet - Dette er lokal tid da denne bestemte loggfilen ble skrevet.
  - Sonarr bruker rullerende loggfiler begrenset til 1 MB hver. Gjeldende loggfil er alltid sonarr.txt, for de andre filene er sonarr.0.txt den nest nyeste (jo høyere nummer, jo eldre er den) opptil totalt 51 loggfiler. Denne loggfilen inneholder `fatal`, `error`, `warn` og `info`-oppføringer.
  - Når feilsøkingslogg nivå er aktivert, vil det være tilgjengelige sonarr.debug.txt rullerende loggfiler, opptil 51 filer. Denne loggfilen inneholder `fatal`, `error`, `warn`, `info` og `debug`-oppføringer. Den dekker vanligvis en periode på ~40 timer.
  - Når sporingslogg nivå er aktivert, vil det være tilgjengelige sonarr.trace.txt rullerende loggfiler, opptil 51 filer. Denne loggfilen inneholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-oppføringer. På grunn av sporingsloggens omfang dekker den bare et par timer maksimalt.