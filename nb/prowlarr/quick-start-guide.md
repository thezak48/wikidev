---
title: Prowlarr Rask Startveiledning
description: 
published: true
date: 2023-04-06T16:04:33.682Z
tags: 
editor: markdown
dateCreated: 2023-04-06T16:04:33.682Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Indekser](#indekser)
- [Apper](#apper)
  - [Appinnstillinger](#appinnstillinger)
- [Nedlastingsklienter](#nedlastingsklienter)
  - [Usenet-klientinnstillinger](#usenet-klientinnstillinger)
  - [Torrent-klientinnstillinger](#torrent-klientinnstillinger)
  - [Test av nedlastingsklienten](#test-av-nedlastingsklienten)
- [Oppsett fullført](#oppsett-fullført)

> Denne siden er fortsatt under arbeid og er ikke fullført.

> For en mer detaljert gjennomgang av alle innstillingene, sjekk [Prowlarr => Innstillinger](/prowlarr/settings)

I denne veiledningen vil vi prøve å forklare det grunnleggende oppsettet du trenger å gjøre for å komme i gang med Prowlarr. Vi vil hoppe over noen alternativer som du kan se på skjermen. Hvis du vil gå dypere inn i disse, kan du se den relevante siden i FAQ og dokumentasjonen for en fullstendig forklaring.

> Vær oppmerksom på at innenfor skjermbildene og GUI-innstillingene i `orange` er avanserte alternativer, så du må klikke på `Vis avansert` øverst på siden for å gjøre dem synlige.

# Indekser

Det første du må sette opp i Prowlarr er indekser. Du vil legge til hver indeks separat i Prowlarr.

Klikk på `Indekser`, og klikk deretter på + for å legge til en ny indeks.

![addindexer.png](/assets/prowlarr/addindexer.png)

Alle indekser du kan legge til (usenet og torrent) er oppført, og du kan skrive inn for å delvis matche en eksisterende oppføring. Hvis indeksen du vil legge til ikke finnes i listen, kan du legge til "Generic Newznab" (for usenet) eller "Generic Torznab" (for torrents).

![addgeneric.png](/assets/prowlarr/addgeneric.png)

Noen indekser har spesielle innstillinger, men de fleste er standard som vist.

![addnewindexer.png](/assets/prowlarr/addnewindexer.png)

- Navn - Velg et navn for denne indeksen. Når den synkroniseres med appene dine, vil den legge til `(Prowlarr)` bak.
- Aktiver - Merk av i boksen for å aktivere denne indeksen.
- Omdirigering - Merk av i boksen hvis omdirigering er nødvendig. Det er bare et par indekser der dette er nødvendig for å unngå å bli utestengt. Hvis det er aktivert, vil dette sende nedlastingslenken direkte til applikasjonen i stedet for å sende den via Prowlarr.

> Omdirigering er vanligvis bare nødvendig for et lite antall spesifikke indekser.

- Synkroniseringsprofil - Velg synkroniseringsprofilen din her. Disse kan opprettes i [`Innstillinger` => `Apper`](/prowlarr/settings#applications). Standardprofilen, Standard, eksisterer allerede og ser slik ut:

> Du kan ha forskjellige innstillinger per app ved å opprette flere instanser av indeksen

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Velg URL-en som Prowlarr skal bruke. Hvis den er tom, brukes standard-/første URL.
- Nedlastingslenke - Hvis du legger til en torrent-indeks, må du kanskje velge hvilken type nedlastingslenke du vil bruke.
- (Avansert alternativ) API-sti - Sti til indeksens API. Vanligvis `/api`
- Legitimasjon - Mange indekser og trackere krever at du autentiserer/logger inn på en eller annen måte. Du må kanskje legge inn en API-nøkkel, RSS-nøkkel, en økt-ID, en informasjonskapsel eller andre legitimasjonsopplysninger fra indeksen din (vanligvis funnet på profilsiden din eller under sikkerhet), velge søkeordre eller andre alternativer for den spesifikke indeksen din.
  - API-nøkkel
  - RSS-nøkkel
  - Økt-ID
  - Informasjonskapsel
  - Brukernavn/passord
  - osv.
- (Avansert alternativ) Tilleggsparametere - Tilleggsparametere som skal legges til forespørslene for denne indeksen.
- VIP-utløp - Skriv inn datoen i ISO-format (yyyy-MM-DD) for å bli varslet 1 uke før utløpet; ellers la det stå tomt
- Merker - Bruk merker for å angi standard nedlastingsklienter, angi indekser til applikasjoner eller bare for å organisere indeksene dine.
- (Avansert alternativ) Spørringsgrense - Hvis indeksen begrenser API-forespørslene dine per dag, kan du skrive inn dette tallet her for å unngå å overskride grensen.
- (Avansert alternativ) Hentegrense - Hvis indeksen begrenser antall hentinger per dag, kan du skrive inn dette tallet her for å unngå å overskride grensen. Når hentegrensen er nådd, vil ytterligere spørringer utløse et uhåndtert unntak i \*Arr-apper. Andre apper kan variere.
- (Avansert alternativ) Seed-forhold - Kun for torrent-indekser: Forholdet en torrent skal nå før den stopper, tom er appens standard
- (Avansert alternativ) Seed-tid - Kun for torrent-indekser: Tiden en torrent skal seedes før den stopper, tom er appens standard
- (Avansert alternativ) Indekserprioritet - Velg indekserprioriteten her fra 1-50 (1 er høyest). Disse prioritetene vil synkroniseres med appene dine.

Test oppføringen din. Hvis det vises et grønt hake-merke, kan du lagre oppføringen og gjenta etter behov for hver indeks du vil at Prowlarr skal bruke. Hvis det mislykkes, må du sjekke loggen din for feilen (URL, API-nøkkel osv.).

# Apper

Etter at du har lagt til indeksene dine, kobler vi deretter Prowlarr til de andre appene dine.

Klikk på `Innstillinger` => `Apper`, og klikk deretter på + for å legge til en støttet app.

![addapps.png](/assets/prowlarr/addapps.png)

Alle programmene du kan legge til, er oppført. Du bør bare legge til programmer du allerede har installert, og hvis du har flere instanser av dem, må du legge til hver av dem separat.

> For øyeblikket støttede apper finner du på siden [Mer informasjon (Støttet)](/prowlarr/supported#applications) for denne delen

Når du legger til en app, må du fylle ut verdier i popup-vinduet:

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Merk: Indekser synkroniseres basert på funksjonene/kategoriene de hevder å støtte. Hvis en indeks bare støtter `tv`-kategorier, vil den ikke bli synkronisert med Lidarr, Radarr og Readarr. Den vil bare bli synkronisert med Sonarr. "Støttede" kategorier kan velges som en avansert innstilling per app. **Merk også at \*Arr-ene bare godtar indekser hvis testspørringene deres returnerer resultater som inneholder minst en av de konfigurerte kategoriene.**

## Appinnstillinger

- Navn - Skriv inn et navn for denne appen.
- Synkroniseringsnivå - Velg synkroniseringsnivået som skal brukes
  - `Bare legg til og fjern` - Når indekser legges til eller fjernes fra Prowlarr, vil det oppdatere denne eksterne appen. Hvis indeksen er nede når synkroniseringen skjer, vil den bli deaktivert i den eksterne appen.
  - `Full synkronisering` - Full synkronisering vil holde denne appens indekser fullstendig synkronisert. Endringer som gjøres i indekser i Prowlarr, blir deretter synkronisert til denne appen. Eventuelle endringer som gjøres i innstillingene på FAQ-siden for disse indeksene eksternt i denne appen, vil bli overskrevet av Prowlarr ved neste synkronisering. En liste over faktorer som brukes til å sammenligne og avgjøre om en synkronisering skal skje, finner du i [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Deaktivert` - holder indekser fra å synkronisere med programmet i det hele tatt.

> `Full synkronisering` betyr at Prowlarr vil overskrive de fleste innstillingene, inkludert brukervalgte kategorier som kan konfigureres i Prowlarr. Imidlertid vil ikke innstillinger som ikke styres av Prowlarr bli berørt. Imidlertid vil [nesten alle andre endringer](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) utløse en synkronisering og overskrive de tilsvarende innstillingene i \*Arr
{.is-warning}

- Merker - Hvis du har lagt til et merke på indeksen under oppsettet, vil bare indekser med dette merket bli brukt for denne programoppføringen.
- Prowlarr-server - Skriv inn Prowlarr-serverens URL (inkludert http, port og baseurl hvis nødvendig) som appen ville bruke her.

> Merk at hvis du bruker en omvendt proxy, må du legge til URL-base her! Hvis du ikke gjør det, vil indeksene bli ødelagt når de synkroniseres, og hvis du har valgt Bare legg til og fjern, vil det ikke bli fikset når du redigerer det!

- Applikasjonsserver - Skriv inn appserverens URL (inkludert http, port og baseurl hvis nødvendig) for programmet ditt her. Skriv inn den fulle URL-basen hvis den brukes.
- API-nøkkel - Skriv inn API-nøkkelen for programmet ditt her. For \*Arr-ene finner du denne i Innstillinger => Generelt. Du kan få denne fra programmet ditt på fanen `Innstillinger` => `Generelt`, og kopiere/klippe ut og lime inn den her.
- (Avansert innstilling) Synkroniseringskategorier - Velg kategoriene som skal synkroniseres med denne appen. Indekser som støtter disse kategoriene, vil bli synkronisert.
  - Indekser med egendefinerte kategorier blir kartlagt til standard Torznab/Newznab-kategorier, slik at søk etter standardiserte kategorier inkluderer alle underliggende egendefinerte kategorier. Egendefinerte kategorier for indekser er oppført for finjustering hvis du ikke vil ha dem alle på en gang.

> Når du lagrer dette, vil det synkronisere indeksene dine med appen. De blir alle lagt til med navnet du har valgt for indeksen din pluss (Prowlarr) etter det. f.eks. `{Indeksnavn} (Prowlarr)`

![nzbgeek.png](/assets/prowlarr/nzbgeek.png)

Du bør deretter gå inn i programmet ditt og deaktivere den ikke-Prowlarr-versjonen av indeksen. Når alt går jevnt, kan du slette de oppføringene og bare la (Prowlarr)-versjonene være igjen.

Du kan ønske å gå inn i programmene dine og sjekke kategoriene for Prowlarr-indeksene. Standardkategorier som skal kartlegges til appen, kan konfigureres som en avansert innstilling for appen i Prowlarr.

> **Vær oppmerksom på at egendefinerte/ikke-standard indeksspesifikke kategorier blir kartlagt til standardkategorier, slik at søk etter standardkategorier inkluderer alle egendefinerte kategorier**

## Synkroniseringsprofiler

Konfigurer synkroniseringsprofilene for å bruke for (en) app(er)

- Navn - Unikt navn på synkroniseringsprofilen
- Aktiver RSS - For indekser med denne profilen, aktiver RSS-søk/spørringer for \*Arr-appen
- Aktiver interaktivt søk - For indekser med denne profilen, aktiver interaktive (manuelle) søk for \*Arr-appen
- Aktiver automatisk søk - For indekser med denne profilen, aktiver automatiske søk for \*Arr-appen
- Minimum seedere - For indekser med denne profilen, minimum antall seedere som kreves for at \*Arr skal laste ned en torrent

# Nedlastingsklienter (Prowlarr-søk)

> Hvis du har til hensikt å gjøre søk direkte i Prowlarr, må du legge til nedlastingsklienter. Ellers trenger du ikke å legge dem til her. For søk fra appene dine brukes nedlastingsklientene som er konfigurert der.

> Nedlastingsklienter er kun for Prowlarrs søk i appen og synkroniseres ikke med apper. Det er ingen planer om å legge til en slik funksjonalitet.

Klikk på `Innstillinger` => `Nedlastingsklienter`, og klikk deretter på + for å legge til en ny nedlastingsklient. Nedlastingsklienten din bør allerede være konfigurert i henhold til denne veiledningen.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

> For øyeblikket støttede nedlastingsklienter finner du på siden [Mer informasjon (Støttet)](/prowlarr/supported#downloadclient) for denne delen

Velg nedlastingsklienten du vil legge til, og det vil være en popup-boks der du kan fylle ut tilkoblingsdetaljer. Disse detaljene er like for de fleste klienter. Noen vil be om et brukernavn eller passord, noen vil spørre om du vil legge til nye nedlastinger i en pause/start-tilstand, osv.  
![nzbget.png](/assets/prowlarr/nzbget.png)

> Klientprioritet betyr bare noe når 2 av samme type (usenet eller torrent) er lagt til. 1 er høyeste prioritet, og hvis flere klienter av samme type eksisterer og har samme prioritet, vil Prowlarr veksle mellom dem.

## Usenet-klientinnstillinger

- Navn - Navnet på nedlastingsklienten i Prowlarr
- Aktiver - Aktiver denne nedlastingsklienten
- Vert - URL-en til nedlastingsklienten din
- Port - Porten til nedlastingsklienten din
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- URL-base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proxyer.
- API-nøkkel - API-nøkkelen for å autentisere mot klienten din
- Brukernavn - brukernavnet for å autentisere mot klienten din (vanligvis ikke nødvendig)
- Passord - passordet for å autentisere mot klienten din (vanligvis ikke nødvendig)
- Kategori - kategorien i nedlastingsklienten din som Prowlarr vil bruke
- Prioritet - nedlastingsklientprioritet for lagt til elementer
- Klientprioritet - Prioritet for nedlastingsklienten i Prowlarr. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet.

## Torrent-klientinnstillinger

- Navn - Navnet på nedlastingsklienten i Prowlarr
- Aktiver - Aktiver denne nedlastingsklienten
- Vert - URL-en til nedlastingsklienten din
- Port - Porten til nedlastingsklienten din
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- URL-base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proxyer.
- Brukernavn - brukernavnet for å autentisere mot klienten din
- Passord - passordet for å autentisere mot klienten din
- Kategori - kategorien i nedlastingsklienten din som Prowlarr vil bruke
- Prioritet - nedlastingsklientprioritet for lagt til elementer
- Initialtilstand - Innledende tilstand for torrents (kun Qbittorrent: Tvungen omgår alle seed-krav)
- Klientprioritet - Prioritet for nedlastingsklienten i Prowlarr. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet.

## Test av nedlastingsklienten

Test oppføringen din. Hvis det vises et grønt hake-merke, kan du lagre oppføringen og gjenta etter behov for hver nedlastingsklient du vil at Prowlarr skal bruke. Hvis det mislykkes, må du sjekke loggen din for feilen (tilkobling, legitimasjon osv.).

# Oppsett fullført

Det er alt for det grunnleggende! Du kan deretter legge til varsler og andre mer avanserte oppsettalternativer etter behov. Disse er dokumentert på den fulle innstillingssiden.