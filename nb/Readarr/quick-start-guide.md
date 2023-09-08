---
title: Readarr Rask Start Guide
description: 
published: true
date: 2022-09-07T23:19:05.590Z
tags: readarr
editor: markdown
dateCreated: 2021-12-11T19:42:31.825Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Rask Start Oppsett Guide](#rask-start-oppsett-guide)
- [Oppstart](#oppstart)
- [Mediehåndtering](#mediehåndtering)
- [Boknavngivning](#boknavngivning)
- [Mapper](#mapper)
- [Importering](#importering)
- [Filhåndtering](#filhåndtering)
- [Rotmapper og Calibre-integrasjon](#rotmapper-og-calibre-integrasjon)
  - [Calibre Content Server (Valgfritt)](#calibre-content-server-valgfritt)
  - [Calibre-integrasjon](#calibre-integrasjon)
- [Nedlastingsklienter](#nedlastingsklienter)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Hvordan importere ditt eksisterende organiserte mediebibliotek](#hvordan-importere-ditt-eksisterende-organiserte-mediebibliotek)
  - [Importering av eksisterende medier](#importering-av-eksisterende-medier)
- [Legg til nye bøker](#legg-til-nye-bøker)

# Rask Start Oppsett Guide

> Denne siden er fortsatt under arbeid og er ikke fullført. Bidrag er velkomne.

> For en mer detaljert gjennomgang av alle innstillingene, sjekk [Readarr => Innstillinger](/readarr/settings)
{.is-info}

I denne guiden vil vi prøve å forklare det grunnleggende oppsettet du trenger å gjøre for å komme i gang med Readarr. Vi kommer til å hoppe over noen alternativer som du kan se på skjermen. Hvis du ønsker å gå dypere inn i disse, kan du se den relevante siden i FAQ og dokumentasjonen for en full forklaring.

> Vær oppmerksom på at innstillingene i `orange` i skjermbildene og GUI-innstillingene er avanserte alternativer, så du må klikke på `Vis avansert` øverst på siden for å gjøre dem synlige.
{.is-warning}

# Oppstart

Etter installasjon og oppstart åpner du en nettleser og går til `http://{din_ip_her}:8787`

![qs_startup.png](/assets/readarr/qs_startup.png)

# Mediehåndtering

Først skal vi se på innstillingene for `Mediehåndtering` der vi kan sette opp våre foretrukne navngivings- og filhåndteringsinnstillinger.

`Innstillinger` => `Mediehåndtering`

![mediamanagement.png](/assets/readarr/mediamanagement.png)

# Boknavngivning

![booknaming.png](/assets/readarr/booknaming.png)

- Aktiver/deaktiver omdøping av bøkene dine (i motsetning til å la navnene være som de er eller som de var da du lastet dem ned).
- Hvis du vil erstatte eller fjerne ulovlige tegn (`\ / : * ? " < > | ~ - % & + { }`).
- Her velger du navnekonvensjonen for de faktiske bokfilene. Merk at navnet på bokmappen er definert her også.
- `(Avansert alternativ) Her setter du navnekonvensjonen for forfattermappen.`

> Dette gjelder ikke hvis Calibre brukes, da Calibre håndterer fil-/mappenavn ved hjelp av sitt eget interne skjema.
{.is-info}

# Mapper

![folders.png](/assets/readarr/folders.png)

- (Avansert alternativ) Opprett tomme forfattermapper - Aktiver for å opprette tomme forfattermapper når en ny forfatter legges til i Readarr.
- (Avansert alternativ) Slett tomme mapper - Aktiver for å slette tomme forfattermapper når det ikke er flere bøker igjen for den forfatteren.

> Én av disse boksene kan være avkrysset, men BEGGE boksene skal ikke være avkrysset.
{.is-warning}

> Dette gjelder ikke hvis Calibre brukes, da Calibre håndterer fil-/mappenavn ved hjelp av sitt eget interne skjema.
{.is-info}

# Importering

![importing.png](/assets/readarr/importing.png)

- (Avansert alternativ) Hopp over sjekk av ledig plass - Hvis aktivert, hopp over sjekk av ledig plass før importering.
- (Avansert alternativ) Minimum ledig plass - Angi minimum ledig plass på disken før importeringen stopper.
- (Avansert alternativ) Bruk hardlenker i stedet for kopiering - Kryss av denne boksen for å bruke hardlenker i stedet for kopiering (for Torrents). Merk at dette er aktivert som standard.

> Du bør ideelt sett bruke dette hvor det er mulig. For at hardlenker skal kunne brukes, må kilden/målet være på samme filsystem (disk, partisjon) og monteringspunkter. [Se TRaSH's Hardlink Guide for mer informasjon](https://trash-guides.info/hardlinks/)
{.is-info}

- Importer ekstra filer - Hvis aktivert, importer spesifiserte ekstra filer som befinner seg i bokmappen når den importeres.
- (Avansert alternativ) Importer ekstra filer - Hvis "Importer ekstra filer" er aktivert, skriv inn en kommaseparert liste over filtyper som skal importeres.

> Hvis du bruker Readarr for lydbøker, bør du legge til .cue i denne listen, da den inneholder informasjon om kapitlene dine!
{.is-info}

# Filhåndtering

![filemanagement.png](/assets/readarr/filemanagement.png)

- Bøker som er slettet fra disken, blir automatisk overvåket som uovervåket i Readarr.

- Ignorer slettede bøker - Kryss av denne boksen for å uovervåke bøker som er oppdaget som slettet eller utilgjengelige fra Readarrs rotmappe.
- Last ned riktig og repacks - Om du automatisk skal oppgradere til riktige/repakker. Bruk `Ikke foretrekk` for å sortere etter foretrukket ordpoeng over riktige/repakker
  - Foretrekk og oppgrader - Ranger repakker og riktige høyere enn ikke-repakker og ikke-riktige. Behandle nye repakker og riktige som oppgradering til nåværende utgivelser.
  - Ikke oppgrader automatisk - Ranger repakker og riktige høyere enn ikke-repakker og ikke-riktige. Behandle ikke nye repakker og riktige som oppgradering til nåværende utgivelser.
  - Ikke foretrekk - Ignorer repakker og riktige. Du må håndtere eventuelle preferanser for disse med [Foretrukne ord](#utgivelsesprofiler).

> \* `RIKTIG` - betyr at det var et problem med den forrige utgivelsen. Nedlastinger merket som RIKTIG viser at problemene er løst i den utgivelsen. Dette er gjort av en gruppe som ikke slapp den opprinnelige utgivelsen.
> \* `REPACK` - betyr at det var et problem med den forrige utgivelsen og er rettet opp av den opprinnelige gruppen. Nedlastinger merket som REPACK viser at problemene er løst i den utgivelsen. Dette er gjort av en gruppe som slapp den opprinnelige utgivelsen.
{.is-info}

- (Avansert alternativ) Overvåk rotmapper for filendringer - Kryss av denne boksen for å utløse en ny skanning når det oppdages endringer i rotmappen.
- (Avansert alternativ) Skann forfattermappe på nytt etter oppdatering - Velg når du vil skanne forfattermappen på nytt etter oppdatering av forfatteren.
  - Alltid - Dette vil skanne forfattermapper basert på oppgaveplanen
  - Etter manuell oppdatering - Du må manuelt skanne disken på nytt
  - Aldri - Akkurat som det sier, aldri skanne forfattermapper på nytt.
- (Avansert alternativ) Tillat fingeravtrykk - Velg hvordan fingeravtrykk skal håndteres, noe som gir økt nøyaktighet for bokmatching, på bekostning av CPU-/disktid.
  - Alltid - Bruk alltid fingeravtrykk hvis mulig
  - Kun for nye importeringer - Bruk bare fingeravtrykk på nyimporterte utgivelser
  - Aldri - Akkurat som det sier, ikke bruk fingeravtrykk
- (Avansert alternativ) Endre filens dato - Endre filens dato ved import/skanning på nytt
  - Ingen - Readarr vil ikke endre datoen som vises i filutforskeren din
  - Bokutgivelsesdato - Datoen boken ble utgitt.
- (Avansert alternativ) Gjenvinningsbeholder - Bokfiler vil havne her når de slettes i stedet for å bli permanent slettet
- (Avansert alternativ) Rengjøring av gjenvinningsbeholder - Dette er hvor gammel en gitt fil kan være før den blir permanent slettet

> Det anbefales på det sterkeste å bruke en gjenvinningsbeholder. Det er enkelt å slette filer, og det er enkelt å gjenopprette dem hvis du bruker beholderen.
{.is-warning}

# Rotmapper og Calibre-integrasjon

![rootfolders1.png](/assets/readarr/rootfolders1.png)

Her legger vi til rotmappen som Readarr vil bruke for å importere ditt eksisterende organiserte mediebibliotek, og hvor Readarr vil importere (kopiere/hardlenke/flytte) mediet ditt etter at nedlastingsklienten din har lastet det ned.

> **Brukeren og gruppen du konfigurerte Readarr til å kjøre som, må ha lese- og skrivetilgang til dette stedet.** {.is-info}

Du kan også velge å bruke Calibre til å administrere biblioteket ditt på denne skjermen. Dette krever at du kjører Calibre Content Server. Dette er IKKE Calibre-Web.

> Brukere som ikke bruker Windows:
> \* Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
> \* Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.
{.is-warning}

> Hvis du skal bruke Calibre, må bøkene du vil at Readarr skal gjenkjenne ved den første biblioteksimporten **allerede være i Calibre**. Bøker i mappen som ikke er i Calibre, vil bli ignorert. Hardlenker brukes ikke når Calibre-integrasjon legges til.
> **Merk at du ikke kan legge til Calibre-integrasjon til en rotmappe etter at den er opprettet.**
{.is-danger}

> Nedlastingsklienten din laster ned til en nedlastingsmappe, og Readarr importerer det til mediemappen (endelig destinasjon) som medieserveren din bruker. Nedlastingsmappen og mediemappen kan ikke være samme plassering!
{.is-warning}

Ikke glem å lagre endringene dine.

## Calibre Content Server (Valgfritt)

Hvis du skal bruke Calibre til å administrere bøkene dine, må du sette opp Calibre Content Server. Igjen, dette er ikke Calibre-Web, men en del av Calibre selv. Du må kjøre Calibre, og du må sette opp Content Server.

> Hvis du velger å bruke Calibre, kan du ikke endre noe i Calibres database. Hvis du ikke følger denne advarselen, må du slette Readarr-databasen din og starte på nytt.
{.is-danger}

Hvis du bruker Docker, må den monterte bokmappen din i Calibre og den monterte bokmappen din i Readarr være den samme.

> Vær oppmerksom på at mens Readarr er i beta; hvis du bruker Calibre, anbefales det å deaktivere omdøping i Readarr, bare i tilfelle det glipper en utilsiktet feil.
{.is-info}

For å gjøre dette, åpne Calibre og klikk på `Innstillinger / Deling over nettet`

![calibreprefs.png](/assets/readarr/calibreprefs.png)

Først legger du til en brukerkonto. Kontoen MÅ ha tilgang til "gjøre endringer".

![calibreacct.png](/assets/readarr/calibreacct.png)

Deretter må du starte Calibre på nytt. Når du er tilbake, konfigurer og start opp innholdsserveren. Den skal vise at den kjører. Sett den til å kjøre automatisk ved oppstart. Etter at du har lagret, må du starte Calibre på nytt igjen. Sørg for at serveren er startet når den starter opp igjen, og deretter kan du gå videre til neste del.

> Du må velge "Krev brukernavn og passord for å få tilgang til innholdsserveren" for at Readarr skal fungere riktig. Hvis du ikke gjør det, får du en feilmelding som sier "Anonyme brukere har ikke lov til å gjøre endringer" når Readarr importerer en bok!
{.is-info}

![calibreserver.png](/assets/readarr/calibreserver.png)

## Calibre-integrasjon

![calibre1.png](/assets/readarr/calibre1.png)

Nedenfor er Calibre-spesifikke innstillinger og vises bare hvis `Bruk Calibre` er aktivert

- Bruk Calibre - Aktiver/deaktiver bruk av Calibre Content Server for å administrere rotmappen din.

> \* Merk at dette **ikke kan aktiveres på en eksisterende rotmappe**.
> \* Merk at dette **ikke kan deaktiveres på en eksisterende rotmappe med Calibre-integrasjon**.
> \* Merk at dette krever **Calibre Content Server** og fungerer ikke med Calibre Web eller Calibre.
> \* Merk at hardlenker ikke fungerer med Calibre-integrasjon.
> \* Merk at Calibre må ha `Krev brukernavn og passord for å få tilgang til innholdsserveren` aktivert.
> \* Hvis du ikke har `Krev brukernavn og passord for å få tilgang til innholdsserveren` aktivert i Calibre, får du en feilmelding som sier "Anonyme brukere har ikke lov til å gjøre endringer"
{.is-warning}

> Hvis du velger å bruke Calibre, kan du ikke endre noe i Calibres database. Hvis du ikke følger denne advarselen, må du slette Readarr-databasen din og starte på nytt.
{.is-danger}

- Calibre-vert - IP-/domenenavnet til verten for Calibre Content Server
- Calibre-port - Porten som Calibre Content Server lytter på
- (Avansert) Calibre URL-base - Legg til et prefiks til Calibre-URL-en, f.eks. `http://[vert]:[port]/[urlBase]`
- Calibre-brukernavn - Brukernavn for å få tilgang til Calibre Content Server
- Calibre-passord - Passord for å få tilgang til Calibre Content Server
- Calibre-bibliotek - Navn på Calibre Content Server-biblioteket. La være blankt for standardverdien
- Konverter til format - (Valgfritt) Be Calibre Content Server om å konvertere til andre formater med en kommaseparert liste.
  - Se (i)-ikonet i appen for en oppdatert liste over alternativer.
  - Alternativene er: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-utdataprofil - Velg utdataprofilen for Calibre Content Server som skal brukes
  - Utdataprofilen forteller Calibre Content Server-konverteringssystemet hvordan det skal optimalisere det opprettede dokumentet for den angitte enheten (for eksempel ved å endre størrelsen på bilder for enhetens skjermstørrelse). I noen tilfeller kan en utdataprofil brukes til å optimalisere utdataen for en bestemt enhet, men dette er sjelden nødvendig.
- Bruk SSL - Aktiver eller deaktiver bruk av SSL (HTTPS) for Calibre Content Server

> Hvis du legger til en individuell bok og velger `Ingen`\* for [metadataprofilen](/readarr/settings#metadata-profiles), vil bare den boken vises under forfatteren når den legges til. Hvis du vil legge til andre bøker for den forfatteren, velger du en passende metadataprofil.
> \* **Merk at `Ingen` ikke bruker noen metadatafiltre, og du kan få uønskede utenlandske utgaver. For å omgå dette [oppretter du en metadataprofil som beskrevet i FAQ-en](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Nedlastingsklienter

`Innstillinger` => `Nedlastingsklienter`

Nedlasting og importering er der de fleste opplever problemer. Fra et overordnet perspektiv må programvaren kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det finnes et stort utvalg av støttede nedlastingsklienter og en enda større variasjon av oppsett. Dette betyr at selv om det finnes noen vanlige oppsett, er det ikke én riktig oppsett, og hvert oppsett kan være litt annerledes. Men det finnes mange feilaktige oppsett.

> Se [innstillingssiden](/readarr/settings#download-clients), på siden [Mer informasjon (Støttet)](/readarr/supported#download-clients) for denne delen, og [TRaSH's Nedlastingsklientguider](https://trash-guides.info/Downloaders/) for mer informasjon.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Readarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Readarr vil overvåke nedlastingsklientens aktive nedlastinger som bruker det kategorinavnet. Den overvåker dette via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Readarr kjenne til den endelige filplasseringen som rapporteres av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediemappen din og tilgjengelig for Readarr.
- Readarr vil skanne denne fullførte filplasseringen etter filer som Readarr kan bruke. Den vil analysere filnavnet for å matche det med den forespurte medien. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til den angitte medielokasjonen.
- Atomiske flyttinger (umiddelbare flyttinger) er aktivert som standard. Filsystemet og monteringspunktene må være de samme for den fullførte nedlastingsmappen din og mediebiblioteket ditt. Hvis den atomiske flyttingen mislykkes eller oppsettet ditt ikke støtter hardlenker og atomiske flyttinger, vil Readarr falle tilbake og kopiere filen og deretter slette den fra kilden, noe som er IO-intensivt.
- Hvis alternativet "Behandling av fullførte nedlastinger - Fjern" er aktivert i Readarrs innstillinger, vil gjenværende filer fra nedlastingen bli sendt til papirkurven eller gjenvinningen via en forespørsel til klienten din om å slette/fjerne utgivelsen.

### BitTorrent

{#bittorrent}

- Readarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Readarr vil overvåke aktive nedlastinger i nedlastingsklienten som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan dele filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Readarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil Readarr opprette en hardlink til filen hvis det støttes av oppsettet ditt, eller kopiere hvis hardlink ikke støttes.
- Hardlink er aktivert som standard. [Et hardlink vil ikke bruke ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringspunktene må være de samme for den fullførte nedlastingsmappen og mediebiblioteket ditt. Hvis opprettelsen av hardlink mislykkes eller oppsettet ditt ikke støtter hardlink, vil Readarr falle tilbake og kopiere filen.
- Hvis alternativet "Fullført nedlastingshåndtering - Fjern" er aktivert i Readarrs innstillinger, vil Readarr slette torrenten fra klienten din og be klienten om å fjerne torrentdataene, men bare hvis klienten rapporterer at delingen er fullført og torrenten er stoppet (pauset ved fullføring).

# Hvordan importere ditt eksisterende organiserte mediebibliotek

> Merk at Readarr ikke søker regelmessig etter bøker. Se disse to FAQ-innleggene for detaljer om hvordan Readarr fungerer.
[Hvordan finner Readarr bøker?](/readarr/faq#hvordan-finner-readarr-bøker) og [Hvordan fungerer Readarr?](/readarr/faq#hvordan-fungerer-readarr)
{.is-info}

Etter at du har konfigurert profilene/den ønskede kvaliteten og lagt til indekseringsverktøy og nedlastingsklient(er), er det på tide å importere ditt eksisterende organiserte mediebibliotek.

Kommer snart - Bidrag ønskes

## Importere eksisterende medier

Kommer snart - Bidrag ønskes

# Legg til nye bøker

[Se bibliotekssiden for mer informasjon](/readarr/library#legg-til-nye)