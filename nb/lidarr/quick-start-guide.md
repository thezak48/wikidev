---
title: Lidarr Rask Start
description: 
published: true
date: 2022-07-14T14:10:13.343Z
tags: 
editor: markdown
dateCreated: 2021-06-13T06:14:53.615Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Rask Start Oppsettsguide](#rask-start-oppsettsguide)
- [Forbehold](#forbehold)
- [Konsept](#konsept)
  - [Utgivelser (Metadata)](#utgivelser-metadata)
  - [Artist (Metadata)](#artist-metadata)
- [Første Oppstart](#første-oppstart)
- [Innstillinger](#innstillinger)
  - [Mediehåndtering](#mediehåndtering)
  - [Profiler](#profiler)
  - [Kvalitet](#kvalitet)
  - [Indekser](#indekser)
  - [Nedlastingsklienter](#nedlastingsklienter)
    - [{.tabset}](#tabset)
      - [Usenet](#usenet)
      - [BitTorrent](#bittorrent)
- [Første Artist](#første-artist)
- [Første Nedlasting/Import](#første-nedlastingimport)
- [Rask Start - Avansert](#rask-start-avansert)
  - [Lidarr Brukstilfelle](#lidarr-brukstilfelle)
    - [Løse filer](#løse-filer)
    - [Spesialbiblioteker](#spesialbiblioteker)
  - [Importere eksisterende bibliotek eller filer](#importere-eksisterende-bibliotek-eller-filer)
    - [Forberede eksisterende filer](#forberede-eksisterende-filer)
      - [Mappesstruktur](#mappesstruktur)
      - [Tagging](#tagging)
    - [Forberedelser før import](#forberedelser-før-import)
    - [Start import](#start-import)

# Rask Start Oppsettsguide

> Denne siden er fortsatt under arbeid og er ikke komplett. Bidrag er velkomne.

> For en mer detaljert gjennomgang av alle innstillingene, sjekk [Lidarr => Innstillinger](/lidarr/settings)
{.is-info}

I denne guiden vil vi prøve å forklare det grunnleggende oppsettet du trenger å gjøre for å komme i gang med Lidarr. Vi vil hoppe over noen alternativer som du kan se på skjermen. Hvis du vil gå dypere inn i disse, kan du se den relevante siden i FAQ og dokumentasjonen for en full forklaring.

> Vær oppmerksom på at innstillingene som vises i skjermbildene og GUI-en i `orange` er avanserte alternativer, så du må klikke på `Vis avansert` øverst på siden for å gjøre dem synlige.
{.is-warning}

# Forbehold

I denne guiden vil vi forklare de grunnleggende trinnene for å begynne å jobbe med Lidarr. Denne guiden forutsetter at du allerede har installert applikasjonen. Installasjonsinstruksjoner finner du på følgende side [installasjon](/lidarr/installation). Vi vil fokusere på minimumsoppsettet og -alternativene for å få en fungerende konfigurasjon. Det er ytterligere oppsett og hensyn å ta hvis noen av følgende situasjoner gjelder:

- Eksisterende bibliotek eller filer
- Feil brukstilfelle
- Feil mappesstruktur
- Feil eller ekstremt komplisert tagging
- Løs samling av filer
- Spesialiserte musikkbiblioteker: Klassisk, Singler, Elektronisk

Hvis noen av de ovennevnte situasjonene gjelder, kan du se seksjonen Rask Start - Avansert.

Denne guiden er delt inn i seksjoner. Det anbefales å lese hele guiden for å få full forståelse, men du kan hoppe til spesifikke seksjoner for umiddelbare bekymringer. Bruk oversikten til venstre for å hoppe raskt.

# Konsept

For å bruke Lidarr riktig, må de underliggende konseptene forstås. På et overordnet nivå følger det prinsippene til de andre Arr-applikasjonene. Lidarr fungerer som et musikkbiblioteksstyringssystem, en dataaggregator og en automatiseringsplattform for å finne og laste ned medier.

Derfra er avviket ganske betydelig. Styring av musikkbibliotek er en svært komplisert prosess, da det er mange konkurrerende variabler som hindrer prosessen. I motsetning til styring av filmer eller TV-serier, er det ikke en konsistent sett med standarder for tagging, navngiving eller lagring av musikk. Dette har blitt ytterligere komplisert av endringene i musikkdistribusjonsmetoder fra fysiske medier til elektroniske. Til slutt er meningene om hvordan man skal håndtere denne styringen vidt forskjellige.

Lidarr bruker informasjon fra dataaggregasjonstjenester for å tagge og administrere musikkbiblioteket på riktig måte. Disse tredjepartsdataene representerer medier i definerte kategorier og typer.

> Hvis dataene ikke finnes i tredjepartstjenestene, kan de IKKE administreres av Lidarr.
Detaljer finner du nedenfor for å delta og bidra.
{.is-warning}

Den viktigste tjenesten som brukes er [MusicBrainz](https://musicbrainz.org/). Dette er en gratis tjeneste som drives av fellesskapet og eksisterer og overlever på bidragene og deltakelsen din. Opprettelse og bidrag til utgivelser er utenfor omfanget av denne guiden. Instruksjoner finner du her: [Hvordan bidra](https://musicbrainz.org/doc/How_to_Contribute)

Til syvende og sist er dataene definert av standardene til tredjepartsdataene. Hvis standardene ikke samsvarer med ditt brukstilfelle, kan **Lidarr være feil løsning**. Andre applikasjoner for styring av medier kan inkludere:

[Beets Media Management](https://beets.io/)
[MusicBrainz Picard](https://picard.musicbrainz.org/)
[Music Bee](https://getmusicbee.com/)

Disse implementeringene kan brukes sammen med Lidarr, men dette er utenfor omfanget av denne guiden.

## Utgivelser (Metadata)

Lidarr har valgt standarden `Utgivelse` for styring av musikkmedier. Dette betyr at for at systemet skal fungere ordentlig, må all media som behandles av systemet, være en `Utgivelse`.

Eksempler på utgivelser:

- Album
- EP
- Singel
- Kringkasting

Hver enhet som skal administreres, må ha en tilsvarende `Utgivelse` i tjenesten for tredjepartsdata.

> `Utgivelser` må eksistere i tredjepartstjenestene for å kunne administreres i Lidarr.

## Artist (Metadata)

Artister er akkurat det som forventes av `Utgivelsesartisten`. Dessverre har artistnavn, stilendringer over tid, brukerpreferanser og andre årsaker komplisert hva som utgjør denne `Utgivelsesartisten`.

Eksempler på riktige og feilaktige "Artister":

- Bob Dylan
- BOB DYLAN
- The Bob Dylan
- Bob Dylan, The
- Bob Dylan & the Band
- Bob Dylan feat. The Band
- The Band featuring Bob Dylan
- ...

Denne listen kan fortsette i det uendelige. Igjen er alle `Utgivelser` korrelert med en `Artist`. Du må finne (trinnene kommer senere i denne guiden) og bruke riktig `Artist` for å laste ned en `Utgivelse`.

> `Utgivelsesartister` må eksistere i tredjepartstjenestene for å kunne administreres i Lidarr.

# Første Oppstart

Etter installasjon og oppstart av Lidarr, får du tilgang ved å åpne en nettleser og gå til `http://{din_ip_her}:8686`

![lidarr_qs_startup.png](/assets/lidarr/quick-start-guide/lidarr_qs_startup.png)

Det vises to alternativer på oppstartsskjermen, men vi vil ikke bruke disse i utgangspunktet.

# Innstillinger

Vi vil bruke standardkonfigurasjonen av innstillingene for å konfigurere Lidarr. Dette vil bruke eksisterende profiler, kvalitet, tagger, osv.

> For en mer detaljert gjennomgang av alle innstillingene, sjekk [Lidarr > Innstillinger](/lidarr/settings)
{.is-info}

## Mediehåndtering

Først skal vi se på `Mediehåndtering`, der vi vil angi `Rotmappe`. Dette vil være plasseringen der mediefilene skal lagres.

> Ikke lagre Lidarr-medier på en skybasert lagringstjeneste! På grunn av måten Lidarr bruker tagger på, vil dette drepe eventuelle API-grenser og forårsake problemer. Hold biblioteket ditt på nettverket ditt.
{.is-warning}

Klikk på `Innstillinger` > `Mediehåndtering` i venstre meny.

![lidarr_qs_mediamanagement.png](/assets/lidarr/quick-start-guide/lidarr_qs_mediamanagement.png)

Klikk på `Legg til (+)` for `Rotmapper`.

Du blir presentert med følgende vindu:

![lidarr_qs_rootfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_rootfolder.png)

- **Navn** - Dette er det `Vennlige navnet` på lagringsplasseringen.
- **Sti** - Dette er den faktiske `Stien` til datalagringsplassen. Systemet/brukeren må ha de nødvendige tillatelsene til denne lagringsstien. Denne mappen kan ikke være nedlastingsplasseringen din!

La de andre alternativene være på standardverdiene.

> Hvis du bruker en `Rotmappe` med eksisterende filer, kan du se gjennom seksjonen Rask Start - Avansert for hensyn.
{.is-warning}

> \* Ikke-Windows: Hvis du bruker en NFS-montering, må `nolock` være aktivert.
> \* Hvis du bruker en SMB-montering, må `nobrl` være aktivert.
{.is-warning}

> **Brukeren og gruppen du konfigurerte Lidarr til å kjøre som, må ha lese- og skrivetilgang til denne plasseringen.** {.is-info}

> Nedlastingsklienten din laster ned til en nedlastingsmappe, og Lidarr importerer den til mediemappen (endelig destinasjon) som medieserveren din bruker.
{.is-info}

> **Nedlastingsmappen og mediemappen kan ikke være samme plassering**
{.is-danger}

## Profiler

`Innstillinger` > `Profiler`

Profilinnstillingene vil forbli med standardverdiene.

## Kvalitet

`Innstillinger` > `Kvalitet`

Kvalitetsinnstillingene vil forbli med standardverdiene.

## Indekser

`Innstillinger` > `Indekser`

Denne delen angir indekser/sporingsnettsteder som du vil bruke for å finne nedlastbare mediefiler.

Klikk på `Legg til (+)` for `Indekser`. Du blir presentert med et nytt vindu med mange forskjellige alternativer. Lidarr betrakter både Usenet-indekser og BitTorrent-sporingsnettsteder som `Indekser`.

Legg til minst én `Indeks` for at Lidarr skal kunne finne tilgjengelige filer.

Forståelsen av konfigurasjonen/konseptene bak `Indekser` er utenfor omfanget av denne guiden. Internett har mye informasjon om emnet.

## Nedlastingsklienter

`Innstillinger` => `Nedlastingsklienter`

![Lidarr-settings-download-clients.png](/assets/lidarr/Lidarr-settings-download-clients.png)

Nedlasting og import er der de fleste opplever problemer. Sett fra et overordnet perspektiv må programvaren kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det finnes mange forskjellige støttede nedlastingsklienter og enda flere forskjellige oppsett. Dette betyr at selv om det er noen vanlige oppsett, er det ikke én riktig oppsett, og hvert oppsett kan være litt annerledes. Men det er mange feilaktige oppsett.

> Se [innstillingssiden](/lidarr/settings#download-clients), siden [Mer informasjon (Støttet)](/lidarr/supported#download-clients) for denne delen, og [TRaSH's Nedlastingsklientguider](https://trash-guides.info/Downloaders/) for mer informasjon.
{.is-info}

### {.tabset}

#### Usenet

{#usenet}

- Lidarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Lidarr vil overvåke nedlastingsklientens aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Lidarr kjenne til den endelige filplasseringen som rapporteres av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediemappen din og tilgjengelig for Lidarr.
- Lidarr vil skanne denne fullførte filplasseringen etter filer som Lidarr kan bruke. Den vil analysere filnavnet for å matche det med den forespurte medien. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til den angitte medielokasjonen.
- Atomiske flyttinger (umiddelbare flyttinger) er aktivert som standard. Filsystemet og monteringene må være de samme for fullføringsmappen for nedlasting og mediebiblioteket ditt. Hvis den atomiske flyttingen mislykkes eller oppsettet ditt ikke støtter hardlenker og atomiske flyttinger, vil Lidarr falle tilbake og kopiere filen og deretter slette den fra kilden, noe som er I/O-intensivt.
- Hvis alternativet "Behandling av fullførte nedlastinger - Fjern" er aktivert i Lidarrs innstillinger, vil gjenværende filer fra nedlastingen bli sendt til papirkurven eller resirkuleringen via en forespørsel til klienten din om å slette/fjerne utgivelsen.

#### BitTorrent

{#bittorrent}

- Lidarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Lidarr vil overvåke nedlastingsklientens aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Lidarr under den spesifikke nedlastingsklienten). Når filene importeres til mediemappen din, vil Lidarr opprette en hardlenke til filen hvis det støttes av oppsettet ditt, eller kopiere den hvis hardlenker ikke støttes.
- Hardlenker er aktivert som standard. [En hardlenke vil ikke bruke noe ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringene må være de samme for fullføringsmappen for nedlasting og mediebiblioteket ditt. Hvis opprettelsen av hardlenken mislykkes eller oppsettet ditt ikke støtter hardlenker, vil Lidarr falle tilbake og kopiere filen.
- Hvis alternativet "Behandling av fullførte nedlastinger - Fjern" er aktivert i Lidarrs innstillinger, vil Lidarr slette torrenten fra klienten din og be klienten om å fjerne torrentdataene, men bare hvis klienten rapporterer at seeding er fullført og torrenten er stoppet (pauset ved fullføring).

# Første Artist

Hvis du følger denne guiden og `Rotmappen` din ikke hadde noen mediefiler, må du legge til en `Artist`.

`Bibliotek` > `Legg til ny`

![lidarr_qs_addnew.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnew.png)

Dette vil lenke til søkeskjermen for å finne en artist. Søk og velg `Artist` du vil legge til. Dette vil åpne vinduet "Legg til ny artist".

![lidarr_qs_addnewdylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnewdylan.png)

Vi vil bruke standardvalgene. Disse bør inkludere:

- Rotmappe - Mappen du opprettet
- Overvåk - Ingen
- Kvalitetsprofil - Hvilken som helst
- Tagger - (tom)
- Start søk etter manglende album - Ikke sjekket

Dette vil starte nedlastingen av `Artist`-metadata. Dette vil ta litt tid avhengig av mengden data som skal samles inn. Husk at denne informasjonen kommer fra tredjepartskilder og er bare så komplett som det fellesskapet har bidratt med.

Klikk på den nylig lagt til `Artisten`. (Bob Dylan i dette eksemplet)

> Standard `Metadataprofil` brukes, og bare `Utgivelser` av typen `Studioalbum` vises.

![lidarr_qs_dylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylan.png)

> Liker du ikke metadataen som ble lastet ned? - Bidra til å gjøre den bedre!
{.is-info}

# Første Nedlasting/Import

Endelig tid for å laste ned/importere din første `Utgivelse`!

Finn `Utgivelsen` du vil legge til i biblioteket ditt. Velg ikonet for manuell søk (menneske) ved siden av utgivelsen.

![lidarr_qs_dylanrelease.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanrelease.png)

Dette vil åpne vinduet for utvalg av `Utgivelse`. Dette vinduet viser resultatene av `Indekser`-forespørselen eller rett og slett søkeresultatene for tilgjengelige nedlastinger.

> Standard `Kvalitetsprofil` tillater alle filtyper. Standard `Utgivelsesprofil` tillater alle nedlastinger. For en detaljert gjennomgang av disse avanserte innstillingene, sjekk [Lidarr > Innstillinger](/lidarr/settings)

![lidarr_qs_dylandownload.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylandownload.png)

Gjennomgå nedlastingsvinduet for ulik informasjon som er gitt:

1. Tittel - Dette er navnet på nedlastingen som returneres av `Indekser`.
1. Kvalitet - Dette er kvaliteten som bestemmes av Lidarr ved hjelp av tittelen.
1. Advarselsindikatorene vil gi en beskrivelse av hvorfor nedlastingen har mislyktes i Lidarrs sjekker. I eksempelet returnerte søket "Feil album".

Når du har gjennomgått, velger du nedlastingsikonet (nummer 4) for å laste ned den tilgjengelige `Utgivelsen`.

Hvis alt er konfigurert riktig, blir nedlastingen sendt til din `Nedlastingsklient`.

Nedlastingen blir lagt til i `Køen` og vil gå gjennom de ulike tilstandene for din type `Nedlastingsklient`.

Til slutt blir nedlastingen importert til din `Rotmappe`. Hvis alt er vellykket, skal den vises som nedenfor.

![lidarr_qs_dylansucess.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylansuccess.png)

Du kan finne de nedlastede filene i din `Rotmappe` og kan bruke dem med mediespilleren du foretrekker.

![lidarr_qs_dylanfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanfolder.png)

# Rask Start - Avansert

Denne avanserte delen er ment for oppsett som kan ha spesielle hensyn. Gå gjennom hvis noen gjelder for konfigurasjonen din og potensielt spare deg for noen hodepine.

> De følgende avsnittene vil hjelpe med vanlige fallgruver og problemer.
{.is-warning}

## Lidarr Brukstilfelle

Som tidligere nevnt i Konsept-delen. Lidarr bør ikke brukes hvis bruken din ikke samsvarer med Lidarrs administrasjonssystem for `Releases`. Lidarr vil IKKE fungere med følgende bruksområder:

- Løse filer - Filer fra flere artister (ikke samlinger) eller flere `Releases`
- Spesialiserte musikkbiblioteker: Klassisk, Singler, Elektronisk

### Løse filer

Lite eller ingen organisering av løse filer vil ikke fungere med Lidarr. Det er best å ikke prøve å bruke disse filene med Lidarr.

### Spesialiserte biblioteker

Spesialiserte biblioteker skaper unike problemer for ethvert administrasjonssystem. Disse situasjonene kan fungere med Lidarr, men det kan kreve omfattende arbeid fra din side, og i stor grad fravike de innebygde automatiseringene. For eksempel:

- **Klassisk musikk** - Har vanligvis omfattende krav eller ønsker for tagging. `Releases`-metadata vil sannsynligvis ikke eksistere eller være feil.
- **Singler** - Singler kan ikke være faktiske `Releases`. Tredjeparts datakilder vil ikke returnere metadata. De vil ikke bli automatisert, og Lidarr vil ikke kunne administrere dem.
- **Elektronisk** - Dette gjelder IKKE for `Releases` i sjangeren Elektronisk. Dette gjelder biblioteker med mikser, beats, samples osv. (Beatport). Tredjeparts datakilder gjenkjenner ikke disse som `Releases`. De vil ikke bli automatisert, og Lidarr vil ikke kunne administrere dem.

## Importere eksisterende bibliotek eller filer

> Merk at Lidarr ikke søker regelmessig etter `Releases`. Se disse to FAQ-oppføringene for detaljer om hvordan Lidarr fungerer.
[Hvordan finner Lidarr `Releases`?](/lidarr/faq#hvordan-finner-lidarr-releases) og [Hvordan fungerer Lidarr?](/lidarr/faq#hvordan-fungerer-lidarr)
{.is-info}

> Automatisk import er en planlagt prosess og kan ikke stoppes når den er startet.
IKKE legg til en `Root Folder` med eksisterende filer før du har gjennomgått denne delen fullstendig.
{.is-warning}

Lidarr bruker et automatisert system for å legge til `Release Artists` og `Releases` som er plassert i rotmappen din.

Hvis Lidarrs brukstilfelle stemmer overens med din situasjon, og du ikke har unike eller spesialiserte biblioteker, kan du fortsette med å importere ditt eksisterende bibliotek.

Det er viktig at filene i ditt eksisterende bibliotek er strukturert og følger Lidarrs administrasjonssystem for `Releases`. Dette betyr at følgende ikke vil fungere:

- Feil mappestruktur - Filer plassert i en enkelt mappe - Se forberedelse>Mappestruktur-delen
- Feil eller ekstremt komplisert tagging - Se forberedelse>Tagging-delen

### Forberede eksisterende filer

For at den automatiserte prosessen skal fungere, må filene dine være klargjort slik at dette flyter effektivt eller fungerer i det hele tatt.

#### Mappestruktur

Det anbefales å følge standard mappestruktur:

\Rotmappe\Release Artist\Release\XX - Track

Dette, kombinert med riktige tags, vil tillate nesten 95% eller større gjenkjennelse av mediespillere.

#### Tagging

Tagging kan være en komplisert prosedyre. Antallet filer og hvordan de er tagget for øyeblikket, vil avgjøre hvor mye innsats som kreves.

De anbefalte metodene for tagging av filene dine inkluderer:

- MusicBrainz Picard
- Beets
- MusicBee, MediaMonkey, JRiver

Bruk av disse programmene er utenfor omfanget av denne veiledningen, men det er å foretrekke å knytte MusicBrainz Release ID-er som en del av tagging-prosessen.

> De fleste tagging-programvare kan strukturere mapper og gi filene riktige tags.
{.is-info}

### Forberedende hensyn

Når filene er riktig tagget og navngitt, bør følgende elementer verifiseres for å sikre at prosessen blir fullført vellykket:

- **Systemarkitektur** - Anbefalt x64 / 64-bit - Import av store biblioteker krever at systemet har tilgang til store mengder RAM og beregner mer effektivt. x86 / 32-bit støttes, men vil ikke være like effektivt og vil ta betydelig lengre tid.
- **Systemkrav til minne (RAM)** - Minimum 4 GB, anbefalt 8 GB - Importprosessen krever mye minne, og hvis Lidarr importerer og en nettleser er åpen, vil det resultere i betydelig bruk av RAM.
- **Begrensninger for `Release`-skive/spor** - `Releases` som har betydelige mengder spor eller skiver, bør fjernes fra importprosessen. De kan importeres manuelt ved hjelp av de innebygde prosedyrene. Det er ingen eksakt grense, men for å være på den sikre siden bør `Releases` med mer enn 25 skiver eller 250 spor fjernes.
- **`Release Artist` med mange `Releases`** - Lidarrs automatiserte prosess sammenligner `Releases` med filene dine. Selv om det ikke er sannsynlig at det vil mislykkes, vil disse filene gjennomgå den automatiserte prosedyren resultere i en betydelig økning i importtiden. Det finnes enkelte artister med tusenvis av `Releases`.
- **Tid** - Den automatiserte importprosedyren tar tid. Et rimelig estimat vil være 1 time for 500 riktig taggete `Releases`. Dette varierer sterkt basert på lagringsplassen din, internett-hastigheten og systemets ytelse.

### Start importering

//

Kommer snart

- Monitor * - Dette setter standardovervåkingsalternativet (`Releases`) for `Root Folder`.
- Quality Profile * - Dette setter standardkvalitetsalternativet for `Root Folder`.
- Metadata Profile * - Dette setter standardmetadataalternativet for `Root Folder`.