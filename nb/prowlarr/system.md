---
title: Prowlarr System
description: 
published: true
date: 2023-05-31T11:54:59.064Z
tags: prowlarr, system
editor: markdown
dateCreated: 2021-08-03T21:21:08.969Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Status](#status)
  - [Helse](#helse)
    - [Systemadvarsler](#systemadvarsler)
      - [Grenen er ikke en gyldig utgavegren](#grenen-er-ikke-en-gyldig-utgavegren)
      - [Den installerte SQLite-versjonen støttes ikke](#den-installerte-sqlite-versjonen-støttes-ikke)
      - [Ny oppdatering er tilgjengelig](#ny-oppdatering-er-tilgjengelig)
      - [Kan ikke installere oppdatering fordi oppstartsmappen ikke kan skrives til av brukeren](#kan-ikke-installere-oppdatering-fordi-oppstartsmappen-ikke-kan-skrives-til-av-brukeren)
      - [Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering](#oppdatering-vil-ikke-være-mulig-for-å-forhindre-sletting-av-appdata-ved-oppdatering)
      - [Grenen er for en tidligere versjon](#grenen-er-for-en-tidligere-versjon)
      - [Kunne ikke koble til signalR](#kunne-ikke-koble-til-signalr)
      - [Kunne ikke løse IP-adressen for konfigurert proxyvert](#kunne-ikke-løse-ip-adressen-for-konfigurert-proxyvert)
      - [Proxy mislyktes i test](#proxy-mislyktes-i-test)
      - [Systemtiden er mer enn 1 dag feil](#systemtiden-er-mer-enn-1-dag-feil)
    - [Nedlastingsklienter](#nedlastingsklienter)
      - [Ingen nedlastingsklient er tilgjengelig](#ingen-nedlastingsklient-er-tilgjengelig)
      - [Kan ikke kommunisere med nedlastingsklient](#kan-ikke-kommunisere-med-nedlastingsklient)
      - [Nedlastingsklienter er utilgjengelige på grunn av feil](#nedlastingsklienter-er-utilgjengelige-på-grunn-av-feil)
      - [Feil nedlastingsklientinnstillinger](#feil-nedlastingsklientinnstillinger)
    - [Indekser](#indekser)
      - [Indeksene har ingen definisjon](#indeksene-har-ingen-definisjon)
      - [Indeksene er utdaterte](#indeksene-er-utdaterte)
        - [Utdatert på grunn av kodeendringer](#utdatert-på-grunn-av-kodeendringer)
        - [Utdatert på grunn av fjerning av nettsteder](#utdatert-på-grunn-av-fjerning-av-nettsteder)
      - [Ingen indekser er aktivert](#ingen-indekser-er-aktivert)
      - [Indekser er utilgjengelige på grunn av feil](#indekser-er-utilgjengelige-på-grunn-av-feil)
      - [Indekser VIP utløper](#indekser-vip-utløper)
      - [Indekser VIP utløpt](#indekser-vip-utløpt)
    - [Applikasjoner](#applikasjoner)
      - [Applikasjonene er utilgjengelige på grunn av feil](#applikasjonene-er-utilgjengelige-på-grunn-av-feil)
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

Denne siden inneholder en liste over helsekontrollfeil. Disse helsekontrollene utføres periodisk av Prowlarr og ved visse hendelser. De resulterende advarslene og feilene er oppført her for å gi råd om hvordan du løser dem.

### Systemadvarsler

#### Grenen er ikke en gyldig utgavegren

- Grenen du har valgt er ikke en gyldig utgavegren. Du vil ikke motta oppdateringer. Vennligst endre til en av de [nåværende utgavegrenene](/prowlarr/faq#how-do-i-update-prowlarr).

#### Den installerte SQLite-versjonen støttes ikke

- Prowlarr lagrer dataene sine i en SQLite-database. SQLite3-biblioteket som er installert på systemet ditt, er for gammelt. Prowlarr krever minst versjon 3.9.0. Merk at Prowlarr bruker `libSQLite3.so`, som kan eller ikke kan være inkludert i en oppgraderingspakke for SQLite3.

#### Ny oppdatering er tilgjengelig

- Fryd deg, utviklerne har gitt ut en ny oppdatering. Dette betyr vanligvis fantastiske nye funksjoner og løste feil (ikke sant?). Tydeligvis har du ikke aktivert automatisk oppdatering, så du må finne ut hvordan du oppdaterer på plattformen din. Å trykke på Installer-knappen på siden System => Oppdateringer er sannsynligvis et godt utgangspunkt.

> Denne advarselen vises ikke hvis versjonen din er mindre enn 14 dager gammel
{.is-info}

#### Kan ikke installere oppdatering fordi oppstartsmappen ikke kan skrives til av brukeren

- Dette betyr at Prowlarr ikke vil kunne oppdatere seg selv. Du må oppdatere Prowlarr manuelt eller angi tillatelsene for Prowlarrs oppstartsmappen (installasjonsmappen) slik at Prowlarr kan oppdatere seg selv.

#### Oppdatering vil ikke være mulig for å forhindre sletting av AppData ved oppdatering

- Prowlarr har oppdaget at AppData-mappen for operativsystemet ditt er plassert inne i mappen som inneholder Prowlarr-binærene. Normalt sett vil det være C:\ProgramData for Windows og ~/.config for Linux.

- Se på System => Info for å se gjeldende AppData- og oppstartsmapper.
- Dette betyr at Prowlarr ikke vil kunne oppdatere seg selv uten å risikere tap av data.
- Hvis du bruker Linux, må du sannsynligvis endre hjemmemappen for brukeren som kjører Prowlarr, og kopiere innholdet i den gjeldende mappen ~/.config/Prowlarr for å bevare databasen din.

#### Grenen er for en tidligere versjon

- Oppdateringsgrenen som er konfigurert i Innstillinger/Generelt, er for en tidligere versjon av Prowlarr, derfor vil instansen ikke se riktig oppdateringsinformasjon i System/Oppdateringer og kan ikke motta nye oppdateringer når de blir utgitt.

#### Kunne ikke koble til signalR

- signalR driver de dynamiske brukergrensesnittoppdateringene, så hvis nettleseren din ikke kan koble til signalR på serveren din, vil du ikke se noen sanntidsoppdateringer i brukergrensesnittet.

- Den vanligste årsaken til dette er bruk av en omvendt proxy eller Cloudflare.
  - Cloudflare krever at websockets er aktivert.
  - Nginx krever følgende tillegg til plasseringsblokken for appen:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Pass på at du ikke inkluderer proxy_set_header Connection "Upgrade"; som foreslått av nginx-dokumentasjonen. DETTE VIL IKKE FUNGERE
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

- For Apache2 omvendt proxy må du aktivere følgende moduler: proxy, proxy_http og proxy_wstunnel. Deretter legger du til denne websockets-tunnel-direktivet i vhost-konfigurasjonen din:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:9696/$1 [P,L]
```

Hvis du har en omvendt proxy under en undermappe, bør RewriteRule inkludere basestien din, f.eks.

```none
RewriteRule /prowlarr/(.*) ws://127.0.0.1:9696/prowlarr/$1 [P,L]
```

Hvis Prowlarr ikke kjører på samme maskin som omvendt proxy. Erstatt 127.0.0.1 med riktig IP-adresse/DNS-navn for Prowlarr-appen din.

- For Caddy (V1) bruk dette:

> Merk: Du må også legge til websockets-direktivet i Prowlarr-konfigurasjonen din{.is-info}

```none
 proxy /prowlarr 127.0.0.1:9696 {
     websocket
     transparent
 }
```

#### Kunne ikke løse IP-adressen for konfigurert proxyvert

- Gjennomgå proxyinnstillingene dine og forsikre deg om at de er korrekte.
- Sørg for at proxyen din er oppe, kjører og tilgjengelig.

#### Proxy mislyktes i test

- Den konfigurerte proxyen mislyktes i testen, sjekk HTTP-feilen som ble oppgitt og/eller sjekk loggene for mer informasjon.

#### Systemtiden er mer enn 1 dag feil

- Systemtiden er mer enn 1 dag feil. Planlagte oppgaver kan ikke kjøre riktig før tiden er korrigert.
- Gjennomgå systemtiden din og forsikre deg om at den er synkronisert med en autoritativ tidsserver og er nøyaktig.

### Nedlastingsklienter

#### Ingen nedlastingsklient er tilgjengelig

- En riktig konfigurert og aktivert nedlastingsklient er nødvendig for at Prowlarr skal kunne laste ned medier. Siden Prowlarr støtter forskjellige nedlastingsklienter, bør du bestemme deg for hvilken som passer best for dine behov. Hvis du allerede har en nedlastingsklient installert, bør du konfigurere Prowlarr til å bruke den og opprette en kategori. Se Innstillinger => Nedlastingsklient.

#### Kan ikke kommunisere med nedlastingsklient

- Prowlarr kunne ikke kommunisere med den konfigurerte nedlastingsklienten. Vennligst bekreft om nedlastingsklienten er operativ og dobbeltsjekk URL-en. Dette kan også indikere en autentiseringsfeil.
- Dette skyldes vanligvis en feil konfigurert nedlastingsklient. Sjekk vanligvis følgende:
- IP-adressen til nedlastingsklienten din, hvis den er på samme fysiske maskin, er dette vanligvis 127.0.0.1
- Portnummeret for nedlastingsklienten din, disse er fylt ut med standard portnummer, men hvis du har endret det, må du angi det samme i Prowlarr.
- Forsikre deg om at SSL-kryptering ikke er aktivert hvis du bruker både Prowlarr-instansen og nedlastingsklienten din i et lokalt nettverk. Se SSL-FAQ-posten for mer informasjon.
- Bruk av rutorrent krever spesielle innstillingsendringer, da det krever https.

#### Nedlastingsklienter er utilgjengelige på grunn av feil

- En eller flere av nedlastingsklientene dine svarer ikke på forespørslene fra Prowlarr. Derfor har Prowlarr bestemt seg for å midlertidig slutte å spørre nedlastingsklienten på den normale 1-minutters syklusen, som vanligvis brukes til å spore aktive nedlastinger og importere ferdige nedlastinger. Imidlertid vil Prowlarr fortsette å prøve å sende nedlastinger til klienten, men vil mest sannsynlig mislykkes.
- Du bør inspisere System=>Loggfiler for å se hva årsaken er til feilene.
- Hvis du ikke lenger bruker denne nedlastingsklienten, deaktiver den i Prowlarr for å unngå feilene.

#### Feil nedlastingsklientinnstillinger

- Plasseringen der nedlastingsklienten din laster ned filer, forårsaker problemer. Sjekk loggene for mer informasjon. Dette kan være tillatelser eller forsøk på å gå fra Windows til Linux eller Linux til Windows uten en fjernbaneoversikt.

### Indekser

#### Indeksene har ingen definisjon

- Indekser(en) dine har ingen eksisterende definisjon(fil), dette skyldes vanligvis at indeksen din ikke lenger støttes og er fjernet, eller at Cardigann YML-definisjonen ikke lenger er tilgjengelig.

#### Indeksene er utdaterte

- Definisjonen til indeksene dine er utdatert. Dette har to årsaker som er beskrevet nedenfor

##### Utdatert på grunn av kodeendringer

- På grunn av kodeendringer er indeksen(e) merket som utdatert som konfigurert for øyeblikket. Fjern og legg til indeksen på nytt i Prowlarr for å løse problemet.
- Dette skyldes vanligvis konvertering av API-er eller fra YML til C# eller omvendt.

##### Utdatert på grunn av fjerning av nettsteder

- Visse nettsteder kan bli bedt om å bli fjernet fra Prowlarr eller Jackett. Disse kan da bli merket som utdaterte.
  - [TVVault](https://github.com/Prowlarr/Prowlarr/issues/573) i [Prowlarr #700](https://github.com/Prowlarr/Prowlarr/pull/700)
  - Audiobookbay har bedt om at Prowlarr ikke får tilgang til API-en deres
  - Ebookbay har bedt om at Prowlarr ikke får tilgang til API-en deres
  - Rarbg har [stengt ned fra og med 2023-05-31](https://torrentfreak.com/iconic-torrent-site-rarbg-shuts-down-all-content-releases-stop-230531/)

#### Ingen indekser er aktivert

- Prowlarr krever at indekser er aktivert for å kunne oppdage nye utgivelser. Les instruksjonene i wikien om hvordan du legger til indekser.

#### Indekser er utilgjengelige på grunn av feil

- (En) feil(e) oppstår når Prowlarr prøver å bruke en av indeksene dine. For å begrense antall forsøk vil ikke Prowlarr bruke indeksen i en økende tid (opptil 24 timer).
- Sjekk hendelser og filtrer etter advarsler for å få en rask oversikt over tidligere problemer
- Denne mekanismen utløses hvis Prowlarr ikke klarte å få et svar fra indeksen (kan skyldes DNS, proxy/vpn-tilkobling, autentisering eller en indeksfeil), eller ikke klarte å hente nzb-/torrent-filen fra indeksen. Inspiser loggene for å finne ut hvilken type feil som forårsaker problemet.
- Du kan forhindre advarselen ved å deaktivere den berørte indeksen.
- Kjør testen på indeksen for å tvinge Prowlarr til å sjekke indeksen på nytt, vær oppmerksom på at helsekontrolladvarselen ikke alltid vil forsvinne umiddelbart.

#### Indekser VIP utløper

- VIP-abonnementet eller fordelene dine for indeksen utløper innen de neste 7 dagene eller mindre basert på utløpsdatoen du konfigurerte for indeksen i Prowlarr.

#### Indekser VIP utløpt

- VIP-abonnementet eller fordelene dine for indeksen har utløpt basert på utløpsdatoen du konfigurerte for indeksen i Prowlarr.

### Applikasjoner

#### Applikasjonene er utilgjengelige på grunn av feil

- (En) feil(e) oppstår når Prowlarr prøver å bruke en av applikasjonene dine. For å begrense antall forsøk vil ikke Prowlarr bruke applikasjonen i en økende tid (opptil 24 timer).
- Denne mekanismen utløses hvis Prowlarr ikke klarte å få et svar fra applikasjonen (kan skyldes DNS, tilkobling, autentisering eller applikasjonsfeil). Inspiser loggene for å finne ut hvilken type feil som forårsaker problemet.
- Sjekk hendelser og filtrer etter advarsler for å få en rask oversikt over tidligere problemer
- Prowlarr vil ikke kunne synkronisere med applikasjonen, og det er mest sannsynlig at applikasjonen ikke vil kunne bruke Prowlarrs indekser.
- Du kan forhindre advarselen ved å deaktivere den berørte applikasjonen.
- Kjør testen på applikasjonen for å tvinge Prowlarr til å sjekke applikasjonen på nytt, vær oppmerksom på at helsekontrolladvarselen ikke alltid vil forsvinne umiddelbart.

## Diskplass

Denne delen viser tilgjengelig diskplass.
I Docker kan dette være vanskelig, da det vanligvis viser tilgjengelig plass innenfor Docker-bildet ditt.

## Om

Dette vil fortelle deg om den gjeldende installasjonen av Prowlarr.

## Mer informasjon

Hjemmeside: Prowlarrs hjemmeside
Wiki: Du er allerede her
Reddit: r/prowlarr
Discord: Bli med i vår discord
Donasjoner: Hvis du føler deg generøs og vil donere, klikk her
Donasjoner til Sonarr: Hvis du føler deg generøs og vil donere til prosjektet som startet det hele, klikk her
Kilde: GitHub
Funksjonsforespørsler: Har du en flott idé, legg den til her

# Oppgaver

## Planlagt

Denne siden viser alle planlagte oppgaver som Prowlarr kjører

- Sjekk oppdatering av applikasjon - Dette vil kjøre på den angitte planen i brukergrensesnittet, og sjekke om Prowlarr er på den nyeste versjonen, og deretter utløse oppdateringsskriptet for å oppdatere Prowlarr. Innstillinger => Oppdatering

> Merk: Hvis du bruker Docker, vil dette ikke oppdatere beholderen din, da det må lastes ned et nytt bilde.
{.is-warning}

- Sikkerhetskopi - Dette vil kjøre en sikkerhetskopi av Prowlarrs database på en angitt plan. Mer informasjon om dette finner du her. Mer informasjon om sikkerhetskopier finner du under System => Sikkerhetskopier.
- Sjekk helse - Sjekk helse vil kjøre på den angitte planen i brukergrensesnittet og sjekke den generelle helsen til Prowlarr. For å se en liste over mulige helseproblemer, se wikien om helsekontroller.
- Husarbeid - På den angitte planen i brukergrensesnittet vil dette støvsuge og vaske gulvene, skure og polere, og til og med lage fine, brettede notater bare for deg. Men det tar ikke ut søpla. Det ble bare ikke betalt nok for det.
- Rens opp meldinger - På den angitte planen i brukergrensesnittet rydder dette opp i meldingene som vises i nedre venstre hjørne av Prowlarr.
  
> Alle disse oppgavene kan kjøres manuelt utenfor planlagte tider ved å trykke på ikonet helt til høyre for hver av oppgavene.
{.is-info}

## Kø

Køen viser kommende oppgaver samt en historikk over nylig kjørte oppgaver og hvor lang tid de tok.

# Sikkerhetskopi



> Denne delen vil være mer tilpasset knappene og generelt formålet med siden.
> Hvis du imidlertid leter etter hvordan du sikkerhetskopierer/gjenoppretter Prowlarr-instansen din, [se vår FAQ](/prowlarr/faq).
{.is-info}

Innenfor Sikkerhetskopiering-seksjonen vil du bli presentert med tidligere sikkerhetskopier (med mindre du har en fersk installasjon som ikke har laget noen sikkerhetskopier).

Her har du to alternativer øverst på skjermen:

- Sikkerhetskopier nå - Dette alternativet vil utløse en manuell sikkerhetskopiering av Prowlarr-databasen din.
- Gjenopprett sikkerhetskopiering - Dette vil åpne en ny skjerm for å gjenopprette fra en tidligere sikkerhetskopiering.
Ved å velge Velg fil vil nettleseren din åpne en dialogboks for å gjenopprette fra en Prowlarr-zip-sikkerhetskopiering.

Til slutt, hvis du har tidligere sikkerhetskopier og ønsker å laste dem ned fra Prowlarr for å plassere dem på en ikke-standard plassering, kan du enkelt velge en av disse filene for å laste dem ned.
Til høyre for hver av de tidligere nedlastningene har du to alternativer.

- Ett - For å gjenopprette fra en tidligere sikkerhetskopiering - Dette vil åpne et nytt vindu for å bekrefte at du ønsker å gjenopprette fra denne sikkerhetskopieringen.
- To - For å slette en tidligere sikkerhetskopiering

# Oppdateringer

Oppdateringsskjermen vil vise de siste 5 oppdateringene som er gjort, samt den gjeldende versjonen du er på.
Denne siden vil også vise oppdateringsnotater fra utviklerne som forteller deg hva som er blitt fikset eller lagt til i Prowlarr (Jubel!)

> En vedlikeholdsutgivelse inneholder feilrettinger og andre forskjellige forbedringer. Ta en titt på commit-historikken for spesifikke detaljer.
{.is-info}

# Hendelser

Hendelsesfanen vil vise deg hva som har skjedd i Prowlarr. Dette kan brukes til å diagnostisere mindre problemer. Men dette erstatter ikke sporingslogger som diskuteres i Logging. Hendelser tilsvarer INFO-logger.

- Komponenter - Denne kolonnen vil fortelle deg hvilken komponent innenfor Prowlarr som har blitt utløst.
- Melding - Denne kolonnen vil fortelle deg hvilken melding som er sendt fra komponenten i forrige kolonne.
- Tannhjulikon - Dette alternativet lar deg endre hvor mange komponenter/meldinger som vises per side (Standard er 50).
- Alternativer øverst på siden
  - Oppdater - Dette alternativet vil oppdatere gjeldende side og hente en ny hendelseslogg.
  - Tøm - Dette vil tømme gjeldende hendelseslogg slik at du kan begynne på nytt.

# Loggfiler

Denne siden lar deg laste ned og se hvilke gjeldende loggfiler som er tilgjengelige for Prowlarr.

På toppraden er det flere alternativer som lar deg kontrollere loggfilene dine.

- På den øverste raden helt til venstre er det en rullegardinmeny som lar deg bytte mellom Loggfiler og Oppdateringsloggfiler.
  - Loggfiler - Kjernen i ethvert supportproblem, mer om loggfiler kan finnes her.
  - Oppdateringsloggfiler - Dette vil vise loggfilene som er tilknyttet Prowlarrs oppdateringsskript.

> Hvis du bruker Docker, vil dette være tomt da du bør oppdatere ved å laste ned et nytt Docker-bilde.
{.is-info}

- Oppdater - Dette vil oppdatere gjeldende side og vise eventuelt nyopprettede logger.
- Slett - Dette vil slette alle logger og la deg begynne på nytt.
- Filnavn - Dette vil vise filnavnet som er knyttet til loggen.
- Sist skrevet - Dette er lokal tid da denne bestemte loggfilen ble skrevet.
  - Prowlarr bruker rullerende loggfiler begrenset til 1 MB hver. Gjeldende loggfil er alltid prowlarr.txt, for de andre filene er prowlarr.0.txt den nest nyeste (jo høyere nummer, jo eldre er den) opp til totalt 51 loggfiler. Denne loggfilen inneholder `fatal`, `error`, `warn` og `info`-oppføringer.
  - Når Debug-loggnivå er aktivert, vil det være tilgjengelige prowlarr.debug.txt rullerende loggfiler, opptil 51 filer. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info` og `debug`-oppføringer. Den dekker vanligvis en periode på ~40 timer.
  - Når Trace-loggnivå er aktivert, vil det være tilgjengelige prowlarr.trace.txt rullerende loggfiler, opptil 51 filer. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-oppføringer. På grunn av sporingsnøyaktighet dekker den bare et par timer maksimalt.