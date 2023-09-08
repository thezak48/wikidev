---
title: Prowlarr Indekser
description: 
published: true
date: 2023-03-30T14:04:26.292Z
tags: 
editor: markdown
dateCreated: 2021-06-06T11:45:31.974Z
---

Denne siden vil beskrive hvordan du legger til og konfigurerer indekser i Prowlarr.

# Legge til en indekser

For å legge til en indekser, klikk først på `Indeksere` på venstre side, deretter <kb>+</kb> `Legg til indekser` øverst på siden.

![ind_1_addindexer.png](/assets/prowlarr/ind_1_addindexer.png)

Velg indekseren din fra listen, eller skriv inn et delvis navn i boksen for å finne indekseren din. Hvis indekseren din ikke er oppført, kan du prøve å bruke "Generic Newznab" (for Usenet) eller "Generic Torznab" (for torrents). Ellers kan du besøke vår [Indekseringsforespørsel-side](https://requests.prowlarr.com/).

> Bruk av `Generic Newznab` eller `Generic Torznab` forutsetter at indekseren din støtter standardiserte *znab-formater. Hvis den ikke gjør det, vil dette ikke fungere
{.is-info}

> Merk: nesten alle Usenet-nettsteder er kompatible med Generic Newznab.
{.is-warning}

> Hvis sporingen eller indekseren din ikke er oppført og ikke er på vår [liste over støttede indekserere](/prowlarr/supported-indexers), kan du be om å få den lagt til via vår [Indekseringsforespørsel-side](https://requests.prowlarr.com)
{.is-info}

# Redigere en indekser

For å redigere en indekser, klikk først på `Indeksere` på venstre side, deretter klikk på skiftenøkkelikonet helt til høyre for indekseren du ønsker å redigere.

# Se en indekser-ID eller URL

For å se detaljer om en indekser, klikk først på `Indeksere` på venstre side, deretter klikk på indekseringslenken i kolonnen for indeksernavn. (Tidligere ikonet (i) til høyre)

Tilgjengelige detaljer kan inkludere:

- ID i Prowlarr
- Beskrivelse
- Koding
- Språk
- Nettsted
- Newznab/Torznab Prowlarr-URL
- Nettstedsfunksjoner

# Indekseringsinnstillinger

Når du har valgt indekseren din, vil det vises en popup-vindu med ytterligere informasjon du trenger for å konfigurere den. Merk at de spesifikke innstillingene vil endre seg litt for hver indekser basert på deres påkrevde felt og typen indekser du konfigurerer.

![ind_3_indexer2.png](/assets/prowlarr/ind_3_indexer2.png)

- Navn - Velg et navn for denne indekseren. Når den synkroniseres med appene dine, vil den legge til `(Prowlarr)` bak.
- Aktiver - Merk av i boksen for å aktivere denne indekseren.
- Omdirigering - Merk av i boksen hvis omdirigering er nødvendig. Det er bare et par indekser der dette er nødvendig for å unngå å bli utestengt. Hvis det er aktivert, vil dette sende nedlastingslenken direkte til applikasjonen i stedet for å proxye den via Prowlarr.

> Omdirigering er vanligvis bare nødvendig for noen få svært spesifikke indekser
{.is-info}

- Synkroniseringsprofil - Velg synkroniseringsprofilen din her. Disse kan opprettes i [`Innstillinger` => `Apper`](/prowlarr/settings#applications). Standardprofilen, "Standard", eksisterer allerede og ser slik ut:

> Du kan ha forskjellige innstillinger per app ved å opprette flere instanser av indekseren
{.is-info}

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Velg URL-en som Prowlarr skal bruke. Hvis den er tom, brukes standard-/første URL.
- Nedlastingslenke - Hvis du legger til en torrent-indekser, kan du måtte velge hvilken type nedlastingslenke du vil bruke.
- (Avansert alternativ) API-sti - Sti til indekserens API. Vanligvis `/api`
- Påloggingsopplysninger - Mange indeksere og sporingssider krever at du autentiserer/logger inn på en eller annen måte. Du må kanskje oppgi en API-nøkkel, RSS-nøkkel, en økt-ID, en informasjonskapsel eller andre påloggingsopplysninger fra indekseren din (vanligvis funnet på profilsiden din eller under sikkerhet), velge søkeordre eller andre alternativer for den spesifikke indekseren din.
  - API-nøkkel
  - RSS-nøkkel
  - Økt-ID
  - Informasjonskapsel
  - Brukernavn/passord
  - osv.
- (Avansert alternativ) Tilleggsparametere - Tilleggsparametere som skal legges til forespørslene for denne indekseren.
- VIP-utløp - Skriv inn datoen i ISO-format (yyyy-MM-DD) for å bli varslet 1 uke før utløpet; ellers la det stå tomt
- Merker - Bruk merker for å angi standard nedlastingsklienter, angi indekserproksier, angi indekserer til applikasjoner eller bare for å organisere indekserne dine.
- (Avansert alternativ) Spørringsgrense - Hvis indekseren begrenser API-forespørslene dine per dag, kan du skrive inn det tallet her for å unngå å overskride grensen.
- (Avansert alternativ) Hentegrense - Hvis indekseren begrenser antall hentinger per dag, kan du skrive inn det tallet her for å unngå å overskride grensen. Når hentegrensen er nådd, vil ytterligere forespørsler utløse et uhåndtert unntak i \*Arr-apper. Andre apper kan variere.
- (Avansert alternativ) Seed-forhold - Kun for torrent-indekser: Forholdet en torrent skal nå før den stopper, tom er appens standard
- (Avansert alternativ) Seed-tid - Kun for torrent-indekser: Tiden en torrent skal være seedet før den stopper, tom er appens standard. Verdiene er i minutter.
- (Avansert alternativ) Indekseringsprioritet - Prioritet for denne indekseren for å foretrekke en indekser over en annen i utgivelsesavgjørende scenarier. 1 er høyeste prioritet og 50 er laveste prioritet. Disse prioritetene vil synkroniseres med \*Arr-apper.

- Test indekseren din, og hvis det vises et grønt hakeikon, er det greit å lagre den. Når du lagrer den, avhengig av synkroniseringsinnstillingene dine, vil den bli lagt til appene dine automatisk.

## Legge til en egendefinert YML-definisjon

- Merk at yml-definisjonen er mellomlagret i en kort periode, og hvis du gjør endringer av utviklingshensyn, må du vente til mellomlagringen utløper eller starte Prowlarr på nytt.
- Hvis du ønsker å legge til en egendefinert YML-definisjonsfil som er kompatibel med Cardigann for en indekser som ikke støttes, eller for å teste endringer i en eksisterende definisjon:
  - Naviger til (eller opprett) mappen for egendefinerte indekseringsdefinisjoner som heter `Custom` innenfor `Definitions`-mappen i [Prowlarrs App Data-mappen](/prowlarr/appdata-directory)
    - Eksempelstier:
      - Windows: `C:\ProgramData\Prowlarr\Definitions\Custom`
      - Linux: `/home/$USER/.config/Prowlarr/Definitions/Custom`
      - OSX: `/Users/$USER/.config/Prowlarr/Definitions/Custom`

  - Lagre [Cardigann-kompatibel YML-filen](/prowlarr/cardigann-yml-definition) i mappen og sørg for at Prowlarr har tillatelse til å få tilgang til den.

> Filnavnet og ID-en i definisjonen må være unik og kan ikke kollidere med noen andre eksisterende definisjoner. Det anbefales sterkt at navnet i definisjonen også er unikt.
{.is-info}

# Støttede indekserere

- [Se denne wikisiden for en liste over støttede indekserere per siste nattlige versjon.](/prowlarr/supported-indexers/)