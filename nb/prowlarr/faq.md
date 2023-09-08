---
title: Prowlarr FAQ
description: Prowlarr FAQ
published: true
date: 2023-08-28T19:29:30.585Z
tags: prowlarr, faq
editor: markdown
dateCreated: 2021-11-03T03:01:18.079Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
  - [Tvungen autentisering](#tvungen-autentisering)
  - [Hvordan tilbakestiller jeg statistikk?](#hvordan-tilbakestiller-jeg-statistikk)
  - [Kategori ikke tilgjengelig eller mangler](#kategori-ikke-tilgjengelig-eller-mangler)
  - [Kan jeg legge til en hvilken som helst (generisk) Torznab- eller Newznab-indeks?](#kan-jeg-legge-til-en-hvilken-som-helst-generisk-torznab-eller-newznab-indeks)
  - [Kan jeg legge til en hvilken som helst (generisk) Torrent RSS-feed?](#kan-jeg-legge-til-en-hvilken-som-helst-generisk-torrent-rss-feed)
  - [Kan jeg bruke flaresolverr-indekser?](#kan-jeg-bruke-flaresolverr-indekser)
  - [Hvordan kan jeg legge til en indekser som er nede eller ikke fungerer?](#hvordan-kan-jeg-legge-til-en-indekser-som-er-nede-eller-ikke-fungerer)
  - [Prowlarr synkroniseres ikke med Sonarr](#prowlarr-synkroniseres-ikke-med-sonarr)
  - [Prowlarr synkroniserer ikke X-indeks med appen](#prowlarr-synkroniserer-ikke-x-indeks-med-appen)
  - [Hvilke \*Arr-indeksinnstillinger sammenlignes for full synkronisering av appen?](#hvilke-arr-indeksinnstillinger-sammenlignes-for-full-synkronisering-av-appen)
  - [Hvordan oppdaterer jeg Prowlarr?](#hvordan-oppdaterer-jeg-prowlarr)
    - [Kan jeg oppdatere Prowlarr inne i Docker-containeren min?](#kan-jeg-oppdatere-prowlarr-inne-i-docker-containeren-min)
    - [Installere en nyere versjon](#installere-en-nyere-versjon)
      - [Lokal installasjon](#lokal-installasjon)
      - [Docker](#docker)
  - [Kan jeg bytte fra `nightly` til `develop`?](#kan-jeg-bytte-fra-nightly-til-develop)
  - [Kan jeg bytte mellom grener?](#kan-jeg-bytte-mellom-grener)
  - [Hjelp, Mac-en min sier at Prowlarr ikke kan åpnes fordi utvikleren ikke kan verifiseres](#hjelp-mac-en-min-sier-at-prowlarr-ikke-kan-åpnes-fordi-utvikleren-ikke-kan-verifiseres)
  - [Hjelp, Mac-en min sier at Prowlarr.app er skadet og kan ikke åpnes](#hjelp-mac-en-min-sier-at-prowlarrapp-er-skadet-og-kan-ikke-åpnes)
  - [Hvordan kan jeg be om en funksjon for Prowlarr?](#hvordan-kan-jeg-be-om-en-funksjon-for-prowlarr)
  - [Jeg får en feilmelding: Database disk image is malformed](#jeg-får-en-feilmelding-database-disk-image-is-malformed)
  - [Jeg bruker Prowlarr på en Mac, og den sluttet plutselig å fungere. Hva skjedde?](#jeg-bruker-prowlarr-på-en-mac-og-den-sluttet-plutselig-å-fungere-hva-skjedde)
  - [Hvordan bytter jeg fra Windows-tjenesten til en Tray App?](#hvordan-bytter-jeg-fra-windows-tjenesten-til-en-tray-app)
  - [Hvordan sikkerhetskopierer/gjenoppretter jeg Prowlarr?](#hvordan-sikkerhetskopierergjenoppretter-jeg-prowlarr)
    - [Sikkerhetskopiering av Prowlarr](#sikkerhetskopiering-av-prowlarr)
      - [Bruke innebygd sikkerhetskopiering](#bruke-innebygd-sikkerhetskopiering)
      - [Bruke filsystemet direkte](#bruke-filsystemet-direkte)
    - [Gjenoppretting fra sikkerhetskopi](#gjenoppretting-fra-sikkerhetskopi)
      - [Bruke zip-sikkerhetskopi](#bruke-zip-sikkerhetskopi)
      - [Bruke filsystem-sikkerhetskopi](#bruke-filsystem-sikkerhetskopi)
      - [Gjenoppretting av filsystem på Synology NAS](#gjenoppretting-av-filsystem-på-synology-nas)
  - [WebUI lastes bare på localhost på Windows](#webui-lastes-bare-på-localhost-på-windows)
  - [Finner ikke informasjonskapsler](#finner-ikke-informasjonskapsler)
  - [uTorrent fungerer ikke lenger](#utorrent-fungerer-ikke-lenger)
  - [Jeg fikk en popup som sa at config.xml var ødelagt, hva nå?](#jeg-fikk-en-popup-som-sa-at-configxml-var-ødelagt-hva-nå)
  - [Ugyldig sertifikat og andre HTTPS- eller SSL-problemer](#ugyldig-sertifikat-og-andre-https-eller-ssl-problemer)
  - [Hjelp, jeg har låst meg ute](#hjelp-jeg-har-låst-meg-ute)
  - [Rare UI-problemer](#rare-ui-problemer)
  - [VPN-er, Prowlarr og \*ARR-ene](#vpn-er-prowlarr-og-arr-ene)
  - [Hvordan stopper jeg nettleseren fra å starte ved oppstart?](#hvordan-stopper-jeg-nettleseren-fra-å-starte-ved-oppstart)
  - [Kan jeg enkelt legge til alle indekser samtidig?](#kan-jeg-enkelt-legge-til-alle-indekser-samtidig)
  
## Tvungen autentisering

Hvis Prowlarr er eksponert slik at brukergrensesnittet kan nås utenfor det lokale nettverket ditt, bør du ha en form for autentiseringsmetode aktivert for å få tilgang til brukergrensesnittet. Dette kreves også i økende grad av sporingsenheter og indekser.

Fra og med Prowlarr v1 er autentisering obligatorisk.

### Autentiseringsmetode

- `Basic` (Nettleser popup) - Denne opsjonen vil vise en liten popup når du åpner Prowlarr, som lar deg skrive inn brukernavn og passord.
- `Forms` (Innloggingsside) - Denne opsjonen vil ha et kjent innloggingsgrensesnitt som ligner på andre nettsteder, som lar deg logge på Prowlarr.
- `External` - Konfigurerbart via konfigurasjonsfilen
  - Hvis du bruker en **ekstern autentisering** som Authelia, Authetik, NGINX Basic auth, osv., kan du unngå dobbel autentisering ved å lukke ned appen, sette `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurasjonsfilen](/prowlarr/appdata-directory) og starte appen på nytt. **Merk at flere `AuthenticationMethod`-oppføringer i filen ikke støttes, og bare verdien øverst vil bli brukt.**

### Påkrevd autentisering

- Hvis du ikke eksponerer appen eksternt og/eller ikke ønsker autentisering for lokal (f.eks. LAN) tilgang, kan du endre innstillingen i Innstillinger => Generell sikkerhet => Påkrevd autentisering til `Deaktivert for lokale adresser`
  - Den tilsvarende konfigurasjonsfilen for dette er `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`
  
## Hvordan tilbakestiller jeg statistikk?

- For å tilbakestille statistikken og slette historikken, gjør følgende:

1. Historikk => Alternativer
1. Sett Historikkopprydding til `1`. Dette vil beholde historikk og statistikk frem til i går
1. Gå til System => Oppgaver
1. Kjør oppgaven "Rydd opp i historikken"
1. Kjør oppgaven "Vedlikehold"
1. Gå tilbake til Historikk => Alternativer
1. Sett Historikkopprydding til ønsket periode for å beholde historikk og statistikk

## Kategori ikke tilgjengelig eller mangler

- Vær oppmerksom på at egendefinerte/ikke-standard indeksspesifikke kategorier er kartlagt til standardkategorier, så søk i standardkategorier vil inkludere alle egendefinerte kategorier. Gå gjennom den spesifikke indeksens kategorikartleggingsdefinisjon for detaljer.

## Kan jeg legge til en hvilken som helst (generisk) Torrent RSS-feed?

Ja. Bruk "TorrentRSS".

Følgende attributter er obligatoriske:

- guid
- title
- infohash
- enclosure eller link

Følgende attributter er valgfrie, men anbefales:

- size
- pubDate

## Kan jeg legge til en hvilken som helst (generisk) Torznab- eller Newznab-indeks?

- Ja.
- Gå til `Indekser` => `Legg til indeks` (<kb>+</kb>) => `Generisk Torznab` eller `Generisk Newznab`

## Kan jeg bruke flaresolverr-indekser?

- Ja.

1. Konfigurer flaresolverr-instansen ved å legge den til som en proxy i [Innstillinger => Indekser](/prowlarr/settings#indexer-proxies)
1. Legg til en tagg på den opprettede flaresovlerr-proxien
1. Legg til samme tagg på [Indekseren](/prowlarr/indexers) din

> Taggene må være like, og Cloudflare må oppdages for at Flaresolverr skal brukes. En Flaresolverr-proxy er deaktivert hvis ingen tagger brukes.
{.is-warning}

> [Se TRaSH's veiledning om "Hvordan sette opp Flaresolverr"](https://trash-guides.info/Prowlarr/prowlarr-setup-flaresolverr/) for mer informasjon
{.is-info}

## Hvordan kan jeg legge til en indekser som er nede eller ikke fungerer?

- Følg de vanlige trinnene for å legge til indeksen, men merk følgende endringer.
- Fjern merket (Deaktiver) for boksen "Aktivert"
- Trykk "Lagre"
- Trykk "Lagre" igjen for å tvinge en lagring
- Rediger indeksen (Skiftenøkkelikon)
- Merk av (Aktiver) for boksen "Aktivert"
- Trykk "Lagre"
- Trykk "Lagre" igjen for å tvinge en lagring

## Prowlarr synkroniseres ikke med Sonarr

- Prowlarr støtter bare Sonarr v3+
- Sonarr v2 (tidligere nzbdrone) støttes ikke av Prowlarr eller generelt, og har vært avsluttet siden mars 2021

## Prowlarr synkroniserer ikke X-indeks med appen

- Prowlarr synkroniserer bare hvis "Legg til og fjern" eller "Full synkronisering" er aktivert for appen.
- Bare i tilfeller der en app og en indekser har samsvarende tagger eller ingen tagger i det hele tatt, vil en indekser bli synkronisert med en app.
- Indekser synkroniseres basert på funksjoner/kategorier de hevder å støtte.
  - Hvis en indekser bare støtter TV-kategorier, vil den ikke bli synkronisert med Lidarr, Radarr og Readarr.
- En gitt indekser vil bare bli synkronisert med Sonarr hvis "Støttede" kategorier kan velges som en avansert innstilling for hver app.
- Indekser vil ikke bli forsøkt synkronisert hvis de spesifikke kategoriene som støttes av indeksen, ikke er valgt i Innstillinger => Applikasjon => {App} => Synkroniseringskategorier (Avanserte innstillinger), og logger vil ikke vise noen indikasjon på et synkroniseringsforsøk.
- Den vanligste årsaken til dette er at \*Arrs bare godtar indekser hvis testforespørslene deres returnerer resultater som inneholder minst en av de konfigurerte kategoriene. Med andre ord, hvis du synkroniserer med en app og indeksens tomme forespørsel ikke returnerer resultater med noen utgivelse innenfor kategoriene som er konfigurert for appen, vil den ikke kunne legge til indeksen i \*Arr.
- Den spesifikke feilmeldingen vil være en HTTP 400 fra \*Arr som sier `Query successful, but no results in the configured categories were returned from your indexer. This may be an issue with the indexer or your indexer category settings.` (Forespørselen var vellykket, men ingen resultater i de konfigurerte kategoriene ble returnert fra indeksen din. Dette kan være et problem med indeksen eller indekskategoriinnstillingene dine.)
  - Det kan hende at indeksen rett og slett ikke kan brukes med den \*Arr-appen. Dette er vanlig når du prøver å bruke offentlige trackere eller usenet-indekser med Readarr og Lidarr.
  - Juster kategoriene som synkroniseres i de avanserte innstillingene for \*Arr-applikasjonen i Prowlarr.
    - Merk at visse trackere - hovedsakelig "dårlige" offentlige trackere - krever at du velger og synkroniserer kategorien "8000 - Annet". Dette er ofte - men ikke alltid - angitt i trackerens detaljer i Prowlarr.
  - Prøv igjen senere
  - Hvis problemet vedvarer, kan du ha en korrupt database. Sjekk loggene for forekomster av `Database disk image is malformed` eller `Error creating main database`. Se [denne overskriften](https://wiki.servarr.com/prowlarr/faq#i-am-getting-an-error-database-disk-image-is-malformed) for mulige løsninger.

## Hvilke \*Arr-indeksinnstillinger sammenlignes for full synkronisering av appen?

- App/Prowlarr: Indeksernavn
- App/Prowlarr: Aktiver/deaktiver RSS
- App/Prowlarr: Aktiver/deaktiver automatisk søk
- App/Prowlarr: Aktiver/deaktiver interaktivt søk
- App/Prowlarr: Indekserprioritet
- App/Prowlarr: API-nøkkel
- App/Prowlarr: URL
- App/Prowlarr: Base-URL
- App/Prowlarr: Port
- App/Prowlarr: Kategorier
- App/Prowlarr: Seed-forhold og seed-tid
- App/Prowlarr: Minimum antall seedere
- App/Prowlarr: *Alle andre innstillinger som kan konfigureres/kontrolleres i Prowlarr*
- Prowlarr: Implementering (f.eks. YML eller C#)

Med full synkronisering aktivert, hvis noen av de ovennevnte endres mellom \*Arr-appen og Prowlarr, vil indeksen bli synkronisert og oppdatert i \*Arr.

## Hvordan oppdaterer jeg Prowlarr?

- Gå til Innstillinger og deretter fanen Generelt og vis avanserte innstillinger (bruk veksleknappen ved siden av lagre-knappen).

1. Under Oppdateringer-seksjonen endrer du grennavnet til `master`, `develop` eller `nightly`
1. Lagre

*Dette vil ikke installere bitene fra den grenen umiddelbart, det vil skje under neste oppdatering.*

- `master` - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) -    (Standard/Stabil): Denne versjonen er testet av brukere på utviklings- og nightly-grenene, og det er ikke kjent noen større problemer. På GitHub er dette `master`-grenen.

- `develop` - ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) -  (Beta): Dette er den eksperimentelle grenen. Den utgis etter testing i nightly for å sikre at det ikke er umiddelbare problemer. Nye funksjoner og feilrettinger utgis her først etter nightly. Den kan betraktes som halvstabil, men er fortsatt `beta`.

> På GitHub er dette et øyeblikksbilde av `develop`-grenen på et bestemt tidspunkt.
{.is-warning}

- `nightly` - ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) -  (Alpha/Ustabil): Dette er den nyeste versjonen. Den utgis så snart koden er bekreftet og består alle automatiserte tester. Denne bygningen er kanskje ikke brukt av oss eller andre brukere ennå. Det er ingen garanti for at den vil kjøre i noen tilfeller. Denne grenen anbefales bare for avanserte brukere. Problemer og egen feilsøking forventes i denne grenen. ***Bruk denne grenen bare hvis du vet hva du gjør og er villig til å ta i bruk tiltak for å gjenopprette en mislykket oppdatering.*** Denne versjonen oppdateres umiddelbart.

> **Advarsel: Du kan kanskje ikke gå tilbake til `develop` etter å ha byttet til denne grenen.** På GitHub er dette `develop`-grenen.
{.is-danger}

- Merk: Hvis du bruker Docker, legg til `:latest`, `:testing`, `:develop` eller `:nightly` på slutten av kontainerkoden, avhengig av hvem som lager byggene dine.

|                                                                      | `master` (stabil) ![Nåværende Master/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Nåværende Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) | `nightly` (ustabil) ![Nåværende Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/prowlarr)                       | `latest`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-prowlarr) | `latest`                                                                                                                                                                                                             | `develop`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |

### Kan jeg oppdatere Prowlarr inne i Docker-containeren min?

- *Teknisk sett, ja.* **Men du bør absolutt ikke gjøre det.** Det er en hovedfilosofi i Docker. Problemer med databasen kan oppstå hvis du oppgraderer installasjonen din til den nyeste `nightly`-versjonen, men deretter oppdaterer Docker-containeren selv (og muligens nedgraderer til en eldre versjon).

### Installere en nyere versjon

#### Native

1. Gå til System og deretter fanen Oppdateringer.
1. Nyere versjoner som ikke er installert ennå, vil ha en oppdateringsknapp ved siden av dem. Klikk på den knappen for å installere oppdateringen.

#### Docker

1. Dra taggen din på nytt og oppdater containeren din.

## Kan jeg bytte fra `nightly` tilbake til `develop`?

## Kan jeg bytte mellom grener?

- Hvis versjonen er identisk, kan du bytte, ellers sjekk med utviklingsteamet for å se om du kan bytte fra `nightly` til `develop`; eller `develop` til `nightly` for bygget ditt.
- Hvis du ikke følger disse instruksjonene, kan Prowlarr bli ubrukelig eller kaste feil. Du er advart
  - De vanligste feilene er databasefeil knyttet til manglende kolonner eller tabeller.

## Hjelp, Mac-en min sier at Prowlarr ikke kan åpnes fordi utvikleren ikke kan verifiseres

- Dette er enkelt, se denne lenken for mer informasjon [her](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
- Alternativt kan du måtte selv-signere Prowlarr `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine`

![faq_1_mac.png](/assets/general/faq_1_mac.png)

## Hjelp, Mac-en min sier at Prowlarr.app er skadet og kan ikke åpnes

Dette skyldes enten en korrupt nedlasting (så prøv igjen), eller sikkerhetsproblemer som er besvart rett over dette.

## Hvordan kan jeg be om en funksjon for Prowlarr?

For å be om en funksjon for Prowlarr, søk først på GitHub for å forsikre deg om at det ikke allerede finnes en lignende forespørsel, og deretter [klikk her](https://github.com/Prowlarr/Prowlarr/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=) for å legge til forespørselen din.

## Jeg får en feilmelding: Database disk image is malformed

- **Feil som `Error creating log database` indikerer problemer med logs.db**
  - Dette kan raskt løses ved å omdøpe eller fjerne databasen. Logs-databasen inneholder uviktig informasjon om kommandohistorikk og oppdateringsinstallasjonshistorikk, samt Info-, Warn- og Error-oppføringer.
- **Feil som `Error creating main database` eller generell `database disk image is malformed` uten spesifisert database indikerer problemer med prowlarr.db**
  - Fortsett med trinnene nedenfor
- Dette betyr at SQLite-databasen som lagrer mesteparten av informasjonen for Prowlarr er korrupt. Du har muligheten til å prøve (en) sikkerhetskopi(er), prøve å gjenopprette den eksisterende databasen, prøve å gjenopprette sikkerhetskopiene, eller hvis alt annet mislykkes, starte på nytt med en helt ny database.
- Denne feilen kan vises hvis databasefilen ikke kan skrives av bruker/gruppe som \*Arr kjører som. Tillatelsesproblemer vil sannsynligvis bare være et problem for nye installasjoner, migrerte installasjoner til en ny server, hvis du nylig har endret tillatelsene for appdata-katalogen din, eller hvis du har endret brukeren og gruppen \*Arr kjører som.
- Ditt beste og første alternativ er å [prøve å gjenopprette fra en sikkerhetskopi](#hvordan-sikkerhetskopierer-gjenoppretter-jeg-prowlarr)
- Du kan også prøve å gjenopprette databasen din. Dette er vanligvis det eneste alternativet når dette problemet oppstår etter en oppdatering. Prøv [sqlite3 `.recover`-kommandoen](/useful-tools#recovering-a-corrupt-db)
  - Hvis sqlite ikke har `.recover` eller du ønsker en mer GUI-vennlig måte (f.eks. Windows), følg [instruksjonene våre på denne wikien.](/useful-tools#recovering-a-corrupt-db-ui)
- En annen mulig årsak til at du får en feil med databasen din er at du plasserer databasen din på en nettverksstasjon (nfs eller smb eller noe annet som ikke er lokalt). **SQLite er designet for situasjoner der data og applikasjonen eksisterer på samme maskin.** Derfor må \*Arr AppData-mappen din (/config mount for docker) være på lokal lagring. [SQLite og nettverksstasjoner fungerer ikke bra sammen og vil til slutt føre til en korrupt database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruker mergerFS, må du fjerne `direct_io` siden SQLite bruker mmap som ikke støttes av `direct_io`, som forklart i mergerFS [dokumentasjonen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jeg bruker Prowlarr på en Mac, og den sluttet plutselig å fungere. Hva skjedde?

Mest sannsynlig skyldes dette en MacOS-feil som førte til at Prowlarr-databasen ble korrupt. Sjekk FAQ-innlegget for å gjenopprette en korrupt database.

## Hvordan bytter jeg fra Windows-tjenesten til en Tray App?

- Stopp Prowlarr
- Kjør serviceuninstall.exe som er i Prowlarr-mappen
- Kjør Prowlarr.exe som administrator én gang for å gi den riktige tillatelser og åpne brannmuren. Når det er fullført, kan du lukke det og kjøre det normalt.
- (Valgfritt) Legg til en snarvei til Prowlarr.exe i oppstartsmappen for å starte automatisk ved oppstart.

## Hvordan sikkerhetskopierer/gjenoppretter jeg Prowlarr?

### Sikkerhetskopiering av Prowlarr

#### Bruke innebygd sikkerhetskopi

- Gå til System => Backup i Prowlarr UI-en
- Klikk på Sikkerhetskopier-knappen
- Last ned zip-filen etter at sikkerhetskopien er opprettet for å lagre den på et trygt sted

#### Bruke filsystemet direkte

- Finn plasseringen til AppData-katalogen for Prowlarr
  - Gå til System => Om i Prowlarr UI-en
  - [Prowlarr Appdata-katalog](/prowlarr/appdata-directory)
- Stopp Prowlarr - Dette forhindrer at databasen blir korrupt
- Kopier innholdet til et trygt sted

### Gjenoppretting fra sikkerhetskopi

> Å gjenopprette til et operativsystem som bruker forskjellige stier vil ikke fungere (Windows til Linux, Linux til Windows, Windows til OS X eller OS X til Windows), overføring mellom OS X og Linux kan fungere, siden begge bruker stier som inneholder `/` i stedet for `\` som Windows bruker, men det støttes ikke. Du må manuelt redigere alle stier i databasen.
{.is-warning}

#### Bruke zip-sikkerhetskopi

- Installer Prowlarr på nytt (hvis aktuelt / ikke allerede installert)
- Kjør Prowlarr
- Gå til System => Backup
- Velg Gjenopprett sikkerhetskopi
- Velg Velg fil
- Velg sikkerhetskopien din som zip-fil
- Velg Gjenopprett

#### Bruke filsystem-sikkerhetskopi

- Installer Prowlarr på nytt (hvis aktuelt / ikke allerede installert)
- Finn plasseringen til AppData-katalogen for Prowlarr
  - Kjør Prowlarr én gang og gå til System => Om i UI-en
  - [Prowlarr Appdata-katalog](/prowlarr/appdata-directory)
- Stopp Prowlarr
- Slett innholdet i AppData-katalogen **(inkludert .db-wal/.db-journal-filene hvis de eksisterer)**
- Gjenopprett fra sikkerhetskopien din
- Start Prowlarr
- Så lenge stiene er de samme, vil alt fortsette der det slapp

#### Gjenoppretting av filsystem på Synology NAS

> ADVARSEL: Gjenoppretting på en Synology krever kunnskap om Linux og Root SSH-tilgang til Synology-enheten.
{.is-warning}

- Installer Prowlarr på nytt (hvis aktuelt / ikke allerede installert)
- Finn plasseringen til AppData-katalogen for Prowlarr
  - Kjør Prowlarr én gang og gå til System => Om i UI-en
  - [Prowlarr Appdata-katalog](/prowlarr/appdata-directory)
- Stopp Prowlarr
- Koble til Synology NAS via SSH og logg inn som root

> På noen installasjoner er brukeren annerledes enn kommandoene nedenfor: `chown -R sc-Prowlarr:Prowlarr *` {.is-info}

- Kjør følgende kommandoer:

    ```shell
        rm -r /usr/local/Prowlarr/var/.config/Prowlarr/Prowlarr.db
        cp -f /tmp/Prowlarr_backup/* /usr/local/Prowlarr/var/.config/Prowlarr/
    ```

- Oppdater tillatelsene på filene:

    ```shell
        cd /usr/local/Prowlarr/var/.config/Prowlarr/
        chown -R Prowlarr:users *
        chmod -R 0644 *
    ```

- Start Prowlarr

## WebUI lastes bare på localhost på Windows

Hvis du bare kan nå brukergrensesnittet ditt på `http://localhost:9696/` eller `http://127.0.0.1:9696`, må du kjøre Prowlarr som administrator minst én gang, kanskje til og med alltid.

## Finn informasjonskapsler

Noen nettsteder kan ikke logges inn automatisk og krever at du logger inn manuelt og deretter gir informasjonskapslene til Prowlarr for at det skal fungere. [Se denne artikkelen for detaljer.](/useful-tools#finding-cookies)

## uTorrent fungerer ikke lenger

- Sørg for at Web UI er aktivert

![faq_4_utorrent.png](/assets/general/faq_4_utorrent.png)

- Slå på Web UI

![faq_5_utorrent.png](/assets/general/faq_5_utorrent.png)

- Sørg for at alternativ lytteport (Avansert => Web UI) ikke er den samme som lytteporten (Tilkoblinger). Vi anbefaler å endre alternativ lytteport for Web UI for å unngå å påvirke portvideresending for tilkoblinger.

![faq_6_utorrent.png](/assets/general/faq_6_utorrent.png)

## Jeg fikk en popup-melding som sa at config.xml var korrupt, hva gjør jeg nå?

Prowlarr klarte ikke å lese konfigurasjonsfilen din ved oppstart fordi den ble på en eller annen måte korrupt. For å få Prowlarr tilbake på nettet, må du slette `.xml` i AppData-mappen din. Når du har slettet den, starter du Prowlarr og den vil starte på standardporten (9696). Du bør nå konfigurere eventuelle innstillinger du konfigurerte på siden for generelle innstillinger.

## Ugyldig sertifikat og andre HTTPS- eller SSL-problemer

Nedlastingsklienten din sluttet å fungere, og du får en feilmelding som "Localhost er et ugyldig sertifikat"?

Prowlarr validerer SSL-sertifikater. Hvis det ikke er satt opp et SSL-sertifikat i nedlastingsklienten, eller hvis du bruker et selvsignert HTTPS-sertifikat uten at CA-sertifikatet er lagt til i den lokale sertifikatbutikken din, vil Prowlarr nekte å koble til. Gratis, riktig signerte sertifikater er tilgjengelige fra Let's Encrypt.

Hvis nedlastingsklienten din og Prowlarr er på samme maskin, er det ingen grunn til å bruke HTTPS, så den enkleste løsningen er å deaktivere SSL for tilkoblingen. De fleste vil være enige i at det heller ikke er nødvendig i et lokalt nettverk. Det er mulig å deaktivere validering av sertifikater i avanserte innstillinger hvis du ønsker å beholde en usikker SSL-konfigurasjon.

## Hjelp, jeg har låst meg ute

{#help-i-have-forgotten-my-password}

Hvis du vil deaktivere autentisering (for å tilbakestille brukernavnet eller passordet du har glemt), må du redigere `config.xml`, som vil være inne i [Prowlarr Appdata Directory](/prowlarr/appdata-directory)

1. Åpne config.xml i en teksteditor
1. Finn linjen for autentiseringsmetode, som vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Endre linjen for `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Prowlarr på nytt
1. Prowlarr vil nå være tilgjengelig uten passord. Du bør gå til `Innstillinger: Generelt` i brukergrensesnittet og angi brukernavnet og passordet ditt

## Rare UI-problemer

- Hvis du opplever rare UI-problemer eller at visse visninger eller sorteringsfunksjoner ikke fungerer, kan du prøve å se det i et Chrome Inkognitovindu eller Firefox Privat vindu. Hvis det fungerer fint der, kan du tømme nettleserens hurtigbuffer og informasjonskapsler for din spesifikke IP/domene. For mer informasjon, se artikkelen [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage) i wikien.

## VPN-er, Jackett og \*ARR-ene

- Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, er det vanligvis bare torrentklienten din som trenger å være bak en VPN. Fordi VPN-tilkoblingspunktet deles av mange brukere, kan du oppleve begrensning av hastighet, DDOS-beskyttelse og IP-blokkering fra ulike tjenester som hver programvare bruker.
- Med andre ord kan det å sette \*ARR-ene (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bak en VPN gjøre applikasjonene ubrukelige i noen tilfeller på grunn av at tjenestene ikke er tilgjengelige.

> **For å være tydelig, det handler ikke om hvorvidt VPN-er vil forårsake problemer med \*ARR-ene, men når: bildetilbydere vil blokkere deg, og Cloudflare er foran de fleste \*ARR-servere (oppdateringer, metadata osv.) og kan også blokkere deg**
{.is-warning}

- **Mange private sporere vil utestenge deg for å bruke eller få tilgang til dem (f.eks. ved å bruke Jackett eller Prowlarr) via en VPN.**

### Bruk av en VPN

- Hvis en VPN er nødvendig og Docker brukes, anbefales det å bruke Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er nødvendig og Docker ikke brukes, må VPN-klienten din ***støtte*** delt tunnelering slik at bare de nødvendige (nedlastingsklient)appene er bak VPN-en.
- Mange problemer med å få tilgang til sporere kan løses ved å bruke Google eller Cloudflares DNS-servere i stedet for ISP-ens DNS-servere.
- I noen tilfeller (f.eks. britiske internettleverandører) kan du trenge å sette torrentnedlastingsklienten din bak en VPN og Jackett/Prowlarr som følger:
  - Sett Jackett bak VPN-en og sørg for at delt tunnelering tillater lokal tilgang
  - For Prowlarr konfigurerer du VPN-klienten din til å gi en proxy og legger til proxyen i Innstillinger => Indekserere. Gi proxyen en tagg, og gi alle indekserere som trenger å bruke den samme taggen.
    - Hvis det absolutt er nødvendig, og hvis VPN-en din ikke gir en måte å opprette en proxy på, kan du sette Prowlarr bak VPN-en og sørge for at delt tunnelering tillater lokal tilgang.

## Hvordan hindrer jeg at nettleseren starter ved oppstart?

Avhengig av operativsystemet ditt, er det flere mulige måter.

- I `Innstillinger` => `Generelt` på noen operativsystemer er det en avmerkingsboks for å starte nettleseren ved oppstart.
- Når du starter Prowlarr, kan du legge til `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumentene.
- Stopp Prowlarr og rediger config.xml-filen, og endre `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Kan jeg enkelt legge til alle indekserere samtidig?

Nei. Dette ville ikke være en god ting å gjøre, og denne funksjonaliteten vil ikke bli lagt til. Det er mye bedre å velge indekserere med omhu, være oppmerksom på statistikken for å fjerne indekserere som er for treg eller ikke gir treff. Riktig beskjæring og vedlikehold av indeksererne dine vil gi mye bedre resultater generelt, og raskere resultater ved søk fra appene dine.