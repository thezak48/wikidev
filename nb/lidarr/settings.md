---
title: Lidarr Innstillinger
description: 
published: true
date: 2022-07-24T14:21:19.994Z
tags: lidarr, needs-love, settings
editor: markdown
dateCreated: 2021-06-14T21:36:07.513Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Innstillinger](#innstillinger)
- [Nedlastingsklienter](#nedlastingsklienter)
  - [Oversikt](#oversikt)
  - [Nedlastingsklientprosesser](#nedlastingsklientprosesser)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Nedlastingsklienter](#nedlastingsklienter-1)
    - [Støttede nedlastingsklienter](#støttede-nedlastingsklienter)
    - [Innstillinger for Usenet-klient](#innstillinger-for-usenet-klient)
    - [Innstillinger for Torrent-klient](#innstillinger-for-torrent-klient)
    - [Kompatibilitet for fjerning av nedlastinger i Torrent-klient](#kompatibilitet-for-fjerning-av-nedlastinger-i-torrent-klient)
  - [Behandling av fullførte nedlastinger](#behandling-av-fullførte-nedlastinger)
    - [Fjern fullførte nedlastinger](#fjern-fullførte-nedlastinger)
    - [Behandling av mislykkede nedlastinger](#behandling-av-mislykkede-nedlastinger)
  - [Fjernstyrte stiavbildninger](#fjernstyrte-stiavbildninger)
- [Importlister](#importlister)
  - [Importlister](#importlister-1)
  - [Ekskludering av importlister](#ekskludering-av-importlister)
  - [Legge til en importliste](#legge-til-en-importliste)
- [Tilkoblinger](#tilkoblinger)
- [Tags](#tags)
- [Generelt](#generelt)
  - [Oppdateringer](#oppdateringer)

# Innstillinger

Denne siden er under utvikling, og bidrag - basert på andre \*Arr-sider - er både velkomne og sterkt oppfordret.

# Nedlastingsklienter

> Informasjon om støttede nedlastingsklienter finner du på siden [Mer informasjon (Støttet)](/lidarr/supported#nedlastingsklienter) for denne delen
{.is-info}

## Oversikt

- Nedlasting og importering er der de fleste opplever problemer. Fra et overordnet perspektiv må programvaren kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det finnes et stort utvalg av støttede nedlastingsklienter og enda flere forskjellige oppsett. Dette betyr at selv om det finnes noen vanlige oppsett, er det ikke én riktig oppsett, og alle oppsett kan være litt forskjellige. Men det finnes mange feilaktige oppsett.

## Nedlastingsklientprosesser

## Usenet

- Lidarr vil sende en nedlastingsforespørsel til klienten din og tilknytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Lidarr vil overvåke dine nedlastingsklienters aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Lidarr kjenne den endelige filplasseringen som rapporteres av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din og tilgjengelig for Lidarr.
- Lidarr vil skanne denne fullførte filplasseringen etter filer som Lidarr kan bruke. Den vil analysere filnavnet for å matche det med forespurt media. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til den angitte medielokasjonen.
- Atomiske flyttinger (umiddelbare flyttinger) er aktivert som standard. Filsystemet og monteringspunktene må være de samme for mappen der nedlastingen er fullført, og mediebiblioteket ditt. Hvis den atomiske flyttingen mislykkes eller oppsettet ditt ikke støtter hardlenker og atomiske flyttinger, vil Lidarr falle tilbake og kopiere filen og deretter slette den fra kilden, noe som er IO-intensivt.
- Hvis alternativet "Fullført nedlastingsbehandling - Fjern" er aktivert i Lidarrs innstillinger, vil gjenværende filer fra nedlastingen bli sendt til papirkurven eller resirkuleringen via en forespørsel til klienten din om å slette/fjerne utgivelsen.

## BitTorrent

- Lidarr vil sende en nedlastingsforespørsel til klienten din og tilknytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Lidarr vil overvåke dine nedlastingsklienters aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Lidarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil Lidarr opprette en hardlenke til filen hvis det støttes av oppsettet ditt, eller kopiere den hvis hardlenker ikke støttes.
- Hardlenker er aktivert som standard. [En hardlenke vil ikke bruke noe ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringspunktene må være de samme for mappen der nedlastingen er fullført, og mediebiblioteket ditt. Hvis opprettelsen av hardlenken mislykkes eller oppsettet ditt ikke støtter hardlenker, vil Lidarr falle tilbake og kopiere filen.
- Hvis alternativet "Fullført nedlastingsbehandling - Fjern" er aktivert i Lidarrs innstillinger, vil Lidarr slette torrenten fra klienten din og be klienten om å fjerne torrentdataene, men bare hvis klienten rapporterer at seeding er fullført og torrenten er stoppet (pauset ved fullføring).

## Nedlastingsklienter

Klikk på `Innstillinger => Nedlastingsklienter`, og klikk deretter på <kb>+</kb> for å legge til en ny nedlastingsklient. Nedlastingsklienten din bør allerede være konfigurert og kjøre.

### Støttede nedlastingsklienter

- En liste over støttede nedlastingsklienter finnes på siden [Mer informasjon (Støttet)](/lidarr/supported#nedlastingsklient) for denne delen

Velg nedlastingsklienten du ønsker å legge til, og det vil vises en popup-boks der du kan legge inn tilkoblingsdetaljer. Disse detaljene er lik for de fleste klienter. Noen vil be om et brukernavn eller passord, noen vil spørre om du vil legge til nye nedlastinger i en pauset/startet tilstand, osv.

### Innstillinger for Usenet-klient

- Navn - Navnet på nedlastingsklienten i Lidarr
- Aktiver - Aktiver denne nedlastingsklienten
- Vert - URL-en til nedlastingsklienten din
- Port - Porten til nedlastingsklienten din
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- (Avansert alternativ) URL-base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proxyer.
- API-nøkkel - API-nøkkelen for å autentisere mot klienten din
- Brukernavn - brukernavnet for å autentisere mot klienten din (typisk ikke nødvendig)
- Passord - passordet for å autentisere mot klienten din (typisk ikke nødvendig)
- Kategori - kategorien i nedlastingsklienten din som \*Arr vil bruke. For å unngå at irrelevante nedlastinger vises i aktiviteten, anbefales det sterkt å angi en kategori.
- Nylig prioritet - nedlastingsklientprioritet for nylig utgitte medier
- Eldre prioritet - nedlastingsklientprioritet for medier som ikke nylig er utgitt
- (Avansert alternativ) Klientprioritet - Prioritet for nedlastingsklienten. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet. 1 er høyeste prioritet, og 50 er laveste prioritet

### Innstillinger for Torrent-klient

- Navn - Navnet på nedlastingsklienten i Lidarr
- Aktiver - Aktiver denne nedlastingsklienten
- Vert - URL-en til nedlastingsklienten din
- Port - Porten til nedlastingsklienten din; dette er vanligvis webgui-porten
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- (Avansert alternativ) URL-base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proxyer.
- Brukernavn - brukernavnet for å autentisere mot klienten din
- Passord - passordet for å autentisere mot klienten din
- Kategori - kategorien i nedlastingsklienten din som \*Arr vil bruke. For å unngå at irrelevante nedlastinger vises i aktiviteten, anbefales det sterkt å angi en kategori.
- Kategori etter import - kategorien som skal angis etter at utgivelsen er lastet ned og importert. Vær oppmerksom på at dette bryter med fjerning av fullførte nedlastinger.
- Nylig prioritet - nedlastingsklientprioritet for nylig utgitte medier
- Eldre prioritet - nedlastingsklientprioritet for medier som ikke nylig er utgitt
- Innledende tilstand - Innledende tilstand for torrents (bare Qbittorrent: Tvinger forbi alle seed-krav)
- (Avansert alternativ) - Prioritet for nedlastingsklienten. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet. 1 er høyeste prioritet, og 50 er laveste prioritet

### Kompatibilitet for fjerning av nedlastinger i Torrent-klient

- Lidarr kan bare angi forholdet mellom seed og tid på klienter som støtter å angi denne verdien via API-en når torrenten legges til. Seed-mål kan settes globalt i klienten selv eller per tracker i \*Arr-innstillingene for hver indekser. Se tabellen nedenfor for klientkompatibilitet.

|      Klient       |                                Forhold                                |                                  Tid                                   |
| :---------------: | :------------------------------------------------------------------: | :--------------------------------------------------------------------: |
|       Aria2       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
|      Deluge       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
| Download Station  | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
|       Flood       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|     Hadouken      | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
|    qBittorrent    |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|     rTorrent      |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
| Torrent Blackhole | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
|   Transmission    |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Støttet-Idle%20Limit*-blue) |
|     uTorrent      |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|       Vuze        |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |

> ![Idle Limit](https://img.shields.io/badge/Støttet-Idle%20Limit*-blue) - Transmission har internt en sjekk for ledig tid, men Lidarr sammenligner den med seedetiden hvis ledighetsgrensen er satt per torrent. Dette gjøres som en løsning på Transmission's API-begrensninger.{.is-info}

## Behandling av fullførte nedlastinger

- Behandling av fullførte nedlastinger er hvordan Lidarr importerer media fra nedlastingsklienten din til seriemappene dine.

- Aktiver (Avansert global innstilling) - Importer fullførte nedlastinger automatisk fra nedlastingsklienten
- Fjern (Innstilling per klient) - Fjern fullførte nedlastinger når de er ferdige (usenet) eller stoppet/fullført (torrenter)
  - For torrenter krever dette at nedlastingsklienten din pauser når seedmålene er nådd. Det krever også at seedmålene støttes av Lidarr i henhold til tabellen ovenfor. Torrenter må også være i samme kategori.

### Fjern fullførte nedlastinger

- Lidarr vil sende en nedlastingsforespørsel til klienten din og tilknytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
- Lidarr vil overvåke dine nedlastingsklienters aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Lidarr kjenne den endelige filplasseringen som rapporteres av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din.
- Lidarr vil skanne denne fullførte filplasseringen etter videofiler. Den vil analysere videofilnavnet for å matche det med en episode. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til den angitte bibliotekmappen.
- Gjenværende filer fra nedlastingen vil bli sendt til papirkurven eller resirkuleringen.

Hvis du laster ned ved hjelp av en BitTorrent-klient, er prosessen litt annerledes:

- Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede. Når filene importeres til den angitte bibliotekmappen, vil Lidarr forsøke å opprette en hardlenke til filen eller falle tilbake til å kopiere (bruk dobbel plass) hvis hardlenker ikke støttes.
- Hvis alternativet "Fullført nedlastingsbehandling - Fjern" er aktivert i innstillingene, vil Lidarr be torrentklienten om å slette den opprinnelige filen og torrenten, men dette vil bare skje hvis klienten rapporterer at seeding er fullført, torrenten er i samme kategori (dvs. ikke bruker en post-import-kategori), seedmålet som er nådd, støttes av Lidarr, og torrenten er pauset (stoppet).

### Behandling av mislykkede nedlastinger

- Behandling av mislykkede nedlastinger er bare kompatibel med SABnzbd og NZBGet.
- Behandling av mislykkede nedlastinger gjelder ikke for torrenter, og det er heller ingen planer om å legge til en slik funksjonalitet.

- Det er flere komponenter som utgjør prosessen for behandling av mislykkede nedlastinger:

- Sjekk nedlaster:
  - Kø - Sjekk nedlasterens kø for passordbeskyttede (krypterte) utgivelser som er merket som mislykket
  - Historikk - Sjekk nedlasterens historikk for mislykkede nedlastinger (f.eks. ikke nok blokker til reparasjon, eller utpakking mislyktes)
- Når Lidarr finner en mislykket nedlasting, starter den behandlingen og gjør noen ting:
  - Legger til en mislykket hendelse i Lidarrs historikk
  - Fjerner den mislykkede nedlastingen fra nedlastingsklienten for å frigjøre plass og fjerne nedlastede filer (valgfritt)
  - Begynner å søke etter en erstatningsfil (valgfritt)
  - Blokkeringsliste (tidligere kjent som 'Blacklisting') tillater automatisk hopping over nzbs når de mislykkes, dette betyr at nzb-en ikke vil bli lastet ned automatisk av Lidarr igjen (du kan fortsatt tvinge nedlastingen via et manuelt søk).
  - Det er 2 avanserte alternativer (på siden for 'Nedlastingsklient'-innstillinger) som kontrollerer oppførselen til mislykkede nedlastinger i Lidarr, for øyeblikket er de alle aktivert som standard.

- Last ned på nytt - Kontrollerer om Lidarr skal søke etter samme fil etter en feil
- (Avansert alternativ) Fjern - Om nedlastingen automatisk skal fjernes fra nedlastingsklienten når feilen oppdages

## Fjernstyrte stiavbildninger

- Fjernstyrt stiavbildning fungerer som en enkel søk-og-erstatt-funksjon for fjernsti og lokalsti. Dette brukes primært for enten sammenslåtte lokale/fjernoppsett ved bruk av mergerfs eller lignende, eller når applikasjonen og nedlastingsklienten ikke er på samme server.
- En fjernstyrt stiavbildning brukes når nedlastingsklienten din rapporterer en sti for fullførte data enten på en annen server eller på en måte som \*Arr ikke adresserer den mappen.
- Generelt sett er en fjernstyrt stiavbildning bare nødvendig hvis nedlastingsklienten din kjører på Linux når \*Arr kjører på Windows eller omvendt. En fjernstyrt stiavbildning kan også være nødvendig hvis du blander Docker- og Native-klienter eller hvis du bruker en fjernserver.
- En fjernstyrt stiavbildning er en ENKEL søk/erstatt (der den finner VERDIEN FOR FJERNSTYRT, erstatter den med VERDIEN FOR LOKAL for den angitte Verten).
- Hvis feilmeldingen om en ugyldig sti ikke inneholder VERDIEN SOM ER ERSTATTET, fungerer ikke stiavbildningen som forventet. Den vanlige løsningen er å legge til og fjerne avbildningen.
- [Se TRaSH's veiledning for ytterligere informasjon om fjernstyrt stiavbildning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og nedlastingsklienten din er Docker-containere, er det sjelden behov for en ekstern stiavbildning. Det anbefales at du [gjennomgår Docker-guiden](/docker-guide) og/eller [følger TRaSH's opplæring](https://trash-guides.info/hardlinks)
{.is-info}

# Importlister

> Informasjon om støttede listetyper finner du på siden [Mer informasjon (Støttet)](/lidarr/supported#lists) for denne delen
{.is-info}

Importlister lar deg legge til elementer i Lidarr fra Spotify eller Last.fm. Dette kan potensielt legge til mange uventede elementer i Lidarr-databasen din, så bruk det med forsiktighet.

<!-- ![importlists.png](/assets/readarr/importlists.png) -->

## Importlister

Dette viser deg hvilke lister du har for øyeblikket, og lar deg legge til nye lister. Å legge til lister blir dekket mer detaljert nedenfor.

## Importlisteutelatelser

Alt som er oppført her, er utelatt fra å bli lagt til av lister, og vil aldri bli lagt til fra noen liste. Du kan fjerne elementer fra dette ved å klikke på det.

## Legge til en importliste

Etter å ha klikket på <kb>+</kb>, velg hvilken type liste du vil legge til:

<!-- ![addlist.png](/assets/readarr/addlist.png) -->

I dette tilfellet skal vi legge til en Spotify-lagrede albumliste.

<!-- ![bookshelflist.png](/assets/readarr/bookshelflist.png) -->

- Navn - Skriv inn et navn for denne listen.
- Aktiver automatisk tillegg - Hvis aktivert, vil alt på listen automatisk legges til i Lidarr.

> Dette vil legge til ALLE ALBUM fra den artisten i Lidarr!

- Overvåkning - Velg overvåkningsnivået for ting som blir lagt til. Gyldige alternativer er `Ingen`, `Spesifikt album` og `Alle artistalbum`. Alle album legges til i Lidarr, men vil bli overvåket eller ikke overvåket basert på dette valget.
- Rotmappe - Velg rotmappen for artister som blir lagt til fra denne listen.
- Overvåk nye album - Velg hva Lidarr skal gjøre med fremtidige album fra den lagte artisten. Gyldige alternativer er `Alle album`, `Ingen`, `Nye`.
- Kvalitetsprofil - Velg kvalitetsprofilen for artister som blir lagt til fra denne listen.
- Metadataprofil - Velg metadataprofilen for artister som blir lagt til fra denne listen.
- Lidarr-tagger - Velg hvilke tagger som gjelder for artister som blir lagt til fra denne listen.

> Det anbefales på det sterkeste at du legger til en beskrivende tagg her. Ellers vil du ikke vite hvilken liste som la til disse elementene i Lidarr, og når de er lagt til, kan du aldri få denne informasjonen igjen! Denne informasjonen blir ikke loggført!

Lister synkroniseres som standard hver 24. time, men kan utløses manuelt fra siden `System` => `Oppgaver`. Du kan ikke automatisere denne prosessen raskere enn det.

# Tilkoblinger

> Informasjon om støttede tilkoblingstyper finner du på siden [Mer informasjon (Støttet)](/lidarr/supported#notifications) for denne delen
{.is-info}

# Tagger

- Tag-seksjonen i Lidarr brukes til å koble forskjellige aspekter av Lidarr sammen.
- Tagger er spesielt nyttige for:

  - Forsinkelsesprofiler
  - Utgivelsesprofiler
  - Indekser

- Tagger kan brukes til å koble Forsinkelsesprofiler, Utgivelsesprofiler, Indekser og Artister/Album sammen.
- For eksempel:
  - Du vil at en bestemt Artist/Album bare skal bruke en bestemt indeks. Du ville opprette en tagg og tilordne Artist/Album og indeksen den taggen.
  - Du vil at en bestemt Utgivelsesprofil bare skal bruke en bestemt Forsinkelsesprofil. Du ville opprette en tagg og tilordne Utgivelsesprofilen og Forsinkelsesprofilen den taggen.

> Merk: Tagger påvirker ikke noen "Kvalitetsprofiler", "Metadataprofiler" eller andre aspekter som ikke er nevnt ovenfor.
{.is-info}

# Generelt

## Oppdateringer

- (Avansert alternativ) Gren - Dette er grenen av Lidarr som du kjører på.
  - [Se denne FAQ-posten for mer informasjon](/lidarr/faq#how-do-i-update-lidarr)
- Automatisk - Last ned og installer oppdateringer automatisk. Du vil fortsatt kunne installere fra System: Oppdateringer. Merk: Windows-brukere blir alltid oppdatert automatisk.
- Mekanisme - Bruk Lidarrs innebygde oppdaterer eller et skript
  - Innebygd - Bruk Lidarrs egen oppdaterer
  - Skript - La Lidarr kjøre oppdateringsskriptet
  - Docker - Oppdater ikke Lidarr fra innsiden av Docker, i stedet dra inn et helt nytt bilde med den nye oppdateringen
- Skript - Synlig bare når Mekanisme er satt til Skript - Sti til oppdateringsskript
- Oppdateringsprosess - Lidarr vil laste ned oppdateringsfilen, verifisere integriteten og pakke den ut til en midlertidig plassering og kalle den valgte metoden. Oppdateringsprosessen vil bli kjørt under samme bruker som Lidarr kjører under, den vil trenge tillatelser til å oppdatere Lidarr-filene samt stoppe/starte Lidarr.
- Innebygd - Den innebygde metoden vil sikkerhetskopiere Lidarr-filer og -innstillinger, stoppe Lidarr, oppdatere installasjonen og starte Lidarr igjen. Hvis systemet ditt ikke takler å stoppe Lidarr og prøver å starte det på nytt automatisk, kan det være best å bruke et skript i stedet. Hvis oppdateringen mislykkes, vil forrige versjon av Lidarr bli startet på nytt.
- Skript - Skriptet skal håndtere det samme som den innebygde oppdatereren. Hvis du trenger å stoppe og starte tjenester (upstart/launchd/etc), må du gjøre det her.