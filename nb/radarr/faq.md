---
title: Radarr FAQ
description: Radarr FAQ
published: true
date: 2023-09-08T04:24:10.540Z
tags: radarr, needs-love, troubleshooting, faq
editor: markdown
dateCreated: 2021-05-16T20:44:27.778Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Grunnleggende om Radarr](#grunnleggende-om-radarr)
  - [Hvordan fungerer Radarr?](#hvordan-fungerer-radarr)
  - [Hvordan finner Radarr filmer?](#hvordan-finner-radarr-filmer)
  - [Hvordan får jeg tilgang til Radarr fra en annen datamaskin?](#hvordan-får-jeg-tilgang-til-radarr-fra-en-annen-datamaskin)
  - [Tvungen autentisering](#tvungen-autentisering)
  - [Hva er minimum tilgjengelighet?](#hva-er-minimum-tilgjengelighet)
  - [Hvordan sammenlignes mulige nedlastinger?](#hvordan-sammenlignes-mulige-nedlastinger)
  - [Hva er lister og hva kan de gjøre for meg?](#hva-er-lister-og-hva-kan-de-gjøre-for-meg)
  - [Hvorfor tar det så lang tid å synkronisere lister, og kan jeg endre det?](#hvorfor-tar-det-så-lang-tid-å-synkronisere-lister-og-kan-jeg-endre-det)
  - [Kan alle filmfilene mine lagres i én mappe?](#kan-alle-filmfilene-mine-lagres-i-én-mappe)
  - [Kan jeg legge alle filmene mine i biblioteket i én mappe?](#kan-jeg-legge-alle-filmene-mine-i-biblioteket-i-én-mappe)
  - [Hvordan oppdaterer jeg Radarr?](#hvordan-oppdaterer-jeg-radarr)
    - [Kan jeg oppdatere Radarr inne i Docker-containeren min?](#kan-jeg-oppdatere-radarr-inne-i-docker-containeren-min)
    - [Installere en nyere versjon](#installere-en-nyere-versjon)
      - [Lokal installasjon](#lokal-installasjon)
      - [Docker](#docker)
  - [Kan jeg bytte fra `nightly` tilbake til `develop`?](#kan-jeg-bytte-fra-nightly-tilbake-til-develop)
  - [Kan jeg bytte mellom grener?](#kan-jeg-bytte-mellom-grener)
  - [Hvordan sikkerhetskopierer/gjenoppretter jeg Radarr?](#hvordan-sikkerhetskopierer-gjenoppretter-jeg-radarr)
    - [Sikkerhetskopiering av Radarr](#sikkerhetskopiering-av-radarr)
      - [Bruke innebygd sikkerhetskopiering](#bruke-innebygd-sikkerhetskopiering)
      - [Bruke filsystemet direkte](#bruke-filsystemet-direkte)
    - [Gjenoppretting fra sikkerhetskopi](#gjenoppretting-fra-sikkerhetskopi)
      - [Bruke zip-sikkerhetskopi](#bruke-zip-sikkerhetskopi)
      - [Bruke sikkerhetskopi fra filsystemet](#bruke-sikkerhetskopi-fra-filsystemet)
      - [Gjenoppretting av filsystem på Synology NAS](#gjenoppretting-av-filsystem-på-synology-nas)
- [Vanlige problemer med Radarr](#vanlige-problemer-med-radarr)
  - [Feil - en oppgave ble avbrutt](#feil---en-oppgave-ble-avbrutt)
  - [Sti er allerede konfigurert for en eksisterende film](#sti-er-allerede-konfigurert-for-en-eksisterende-film)
  - [Hvordan kan jeg endre navn på filmmappene mine?](#hvordan-kan-jeg-endre-navn-på-filmmappene-mine)
  - [Navngivning av filer og mapper for filmer](#navngivning-av-filer-og-mapper-for-filmer)
  - [Feil navngivning av filmmapper](#feil-navngivning-av-filmmapper)
  - [Kan jeg deaktivere oppdatering av filmer?](#kan-jeg-deaktivere-oppdatering-av-filmer)
  - [Hvordan kan jeg be om en ny funksjon for Radarr?](#hvordan-kan-jeg-be-om-en-ny-funksjon-for-radarr)
  - [Hjelp, Mac-en min sier at Radarr ikke kan åpnes fordi utvikleren ikke kan verifiseres](#hjelp-mac-en-min-sier-at-radarr-ikke-kan-åpnes-fordi-utvikleren-ikke-kan-verifiseres)
  - [Hjelp, Mac-en min sier at Radarr.app er skadet og kan ikke åpnes](#hjelp-mac-en-min-sier-at-radarrapp-er-skadet-og-kan-ikke-åpnes)
  - [Jeg får en feilmelding: Database disk image is malformed](#jeg-får-en-feilmelding-database-disk-image-is-malformed)
  - [Jeg bruker Radarr på en Mac, og den sluttet plutselig å fungere. Hva skjedde?](#jeg-bruker-radarr-på-en-mac-og-den-sluttet-plutselig-å-fungere-hva-skjedde)
  - [Hvorfor kan ikke Radarr se filene mine på en ekstern server?](#hvorfor-kan-ikke-radarr-se-filene-mine-på-en-ekstern-server)
    - [Radarr kjører som standard under LocalService-kontoen, som ikke har tilgang til beskyttede eksterne filområder](#radarr-kjører-som-standard-under-localservice-kontoen-som-ikke-har-tilgang-til-beskyttede-eksterne-filområder)
    - [Du bruker et kartlagt nettverksstasjon (ikke en UNC-sti)](#du-bruker-et-kartlagt-nettverksstasjon-ikke-en-unc-sti)
  - [Hvordan bytter jeg fra Windows-tjenesten til en skuffeapp?](#hvordan-bytter-jeg-fra-windows-tjenesten-til-en-skuffeapp)
  - [Hjelp, jeg har låst meg ute](#hjelp-jeg-har-låst-meg-ute)
  - [Hvordan stopper jeg nettleseren fra å starte ved oppstart?](#hvordan-stopper-jeg-nettleseren-fra-å-starte-ved-oppstart)
  - [Rare problemer med brukergrensesnittet](#rare-problemer-med-brukergrensesnittet)
  - [Nettlesergrensesnittet lastes bare på localhost på Windows](#nettlesergrensesnittet-lastes-bare-på-localhost-på-windows)
  - [Tillatelser](#tillatelser)
  - [System og logger lastes inn for alltid](#system-og-logger-lastes-inn-for-alltid)
  - [Finn informasjonskapsler](#finn-informasjonskapsler)
  - [Pakk ut torrents](#pakk-ut-torrents)
  - [uTorrent fungerer ikke lenger](#utorrent-fungerer-ikke-lenger)
  - [Jeg fikk en popup-melding som sa at config.xml var ødelagt, hva nå?](#jeg-fikk-en-popup-melding-som-sa-at-configxml-var-ødelagt-hva-nå)
  - [Ugyldig sertifikat og andre HTTPS- eller SSL-problemer](#ugyldig-sertifikat-og-andre-https-eller-ssl-problemer)
  - [VPNs, Jackett og \*ARRene](#vpns-jackett-og-arrene)
- [Vanlige problemer med søk og nedlasting i Radarr](#vanlige-problemer-med-søk-og-nedlasting-i-radarr)
  - [Hvorfor kan jeg ikke legge til en ny film i Radarr?](#hvorfor-kan-jeg-ikke-legge-til-en-ny-film-i-radarr)
  - [Hvordan bestemmer Radarr året for en film?](#hvordan-bestemmer-radarr-året-for-en-film)
  - [Jackett viser flere resultater enn ved manuell søk](#jackett-viser-flere-resultater-enn-ved-manuell-søk)
  - [Hvordan håndterer Radarr utenlandske filmer eller utenlandske titler?](#hvordan-håndterer-radarr-utenlandske-filmer-eller-utenlandske-titler)
  - [Hvordan håndterer Radarr "multi" i navn?](#hvordan-håndterer-radarr-multi-i-navn)
  - [Hjelp, filmen ble lagt til, men ikke søkt etter](#hjelp-filmen-ble-lagt-til-men-ikke-søkt-etter)
  - [Jacketts /all-endepunkt](#jacketts-all-endepunkt)
    - [Løsninger for Jackett /All](#løsninger-for-jackett-all)
  - [Hvorfor er det to filer? | Hvorfor er det en fil igjen i nedlastinger?](#hvorfor-er-det-to-filer-hvorfor-er-det-en-fil-igjen-i-nedlastinger)
  - [Hvorfor fungerer ikke Radarr bak en omvendt proxy](#hvorfor-fungerer-ikke-radarr-bak-en-omvendt-proxy)

# Grunnleggende om Radarr

## Hvordan fungerer Radarr?

- Radarr søker *ikke* regelmessig etter filer som mangler eller ikke oppfyller kvalitetsmålene. I stedet spør den ganske ofte indekserne og sporingssystemene dine etter *alle* de nylig publiserte filmene, og sammenligner det med listen over filmer som mangler eller trenger oppgradering. Eventuelle treff blir lastet ned. Dette gjør at Radarr kan dekke et bibliotek av *hvilken som helst størrelse* med bare 24-100 spørringer per dag (RSS-intervall på 15-60 minutter). Hvis du forstår dette, vil du innse at det bare dekker *fremtiden*.
- Så hvordan håndterer du nåtiden og fortiden? Når du legger til en film, må du angi riktig sti, profil og overvåkingsstatus, og deretter bruke avmerkingsboksen "Start søk etter manglende film". Hvis filmen ikke er utgitt ennå, trenger du ikke å starte et søk.
- Med andre ord vil Radarr bare finne filmer som nylig er lastet opp til indekserne dine. Den vil ikke aktivt prøve å finne filmer du ønsker som ble lastet opp i fortiden.
- Hvis du allerede har lagt til filmen, men nå vil søke etter den, har du noen valg. Du kan gå til filmens side og bruke søkeknappen, som vil gjøre et søk og deretter automatisk velge en. Du kan bruke fanen Søk og se *alle* resultatene, og velge den du vil ha. Eller du kan bruke filtrene `Mangler`, `Ønsket` eller `Kuttet ikke oppfylt`.
- Hvis Radarr har vært frakoblet i lang tid, vil Radarr forsøke å bla tilbake for å finne den siste utgivelsen den behandlet, for å unngå å gå glipp av en utgivelse. Så lenge indeksen din støtter blading og det ikke har gått for lang tid, vil Radarr kunne behandle utgivelsene den ville ha gått glipp av, og du trenger ikke å utføre et søk etter de tapte filmene.

## Hvordan finner Radarr filmer?

> Dette FAQ-elementet er en tidligere FAQ-innføring. Se [Hvordan fungerer Radarr?](#hvordan-fungerer-radarr)
{.is-info}

## Hvordan får jeg tilgang til Radarr fra en annen datamaskin?

- Som standard lytter ikke Radarr til forespørsler fra alle systemer (når det ikke kjøres som administrator), det vil bare lytte på localhost. Dette skyldes hvordan webserveren Radarr bruker integreres med Windows (dette gjelder også for nåværende alternativer). Hvis Radarr kjøres som administrator, vil det registrere seg riktig med Windows og åpne brannmurens port slik at det kan nås fra andre systemer i nettverket ditt. Kjøring som administrator trenger bare å skje én gang (hvis du endrer porten, må den kjøres på nytt).

## Tvungen autentisering

Hvis Radarr er eksponert slik at brukergrensesnittet kan nås utenfor det lokale nettverket, bør du ha en form for autentiseringsmetode aktivert for å få tilgang til brukergrensesnittet. Dette kreves også i økende grad av sporings- og indekssystemer.

Fra og med Radarr v5 er autentisering obligatorisk.

### Autentiseringsmetode

- `Basic` (nettleser-popup) - Denne alternativet viser en liten popup når du får tilgang til Radarr, slik at du kan skrive inn brukernavn og passord.
- `Forms` (innloggingsside) - Dette alternativet har en innloggingsskjerm som ligner på innloggingsskjermen på andre nettsteder, slik at du kan logge på Radarr.
- `External` - Konfigurerbart via konfigurasjonsfilen
  - Hvis du bruker **ekstern autentisering** som Authelia, Authetik, NGINX Basic auth, osv., kan du unngå dobbel autentisering ved å lukke ned appen, angi `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurasjonsfilen](/radarr/appdata-directory) og starte appen på nytt. **Merk at flere `AuthenticationMethod`-oppføringer i filen ikke støttes, og bare verdien øverst vil bli brukt.**

### Påkrevd autentisering

- Hvis du ikke eksponerer appen eksternt og/eller ikke ønsker å kreve autentisering for lokal (f.eks. LAN) tilgang, kan du endre dette i Innstillinger => Generell sikkerhet => Påkrevd autentisering til `Deaktivert for lokale adresser`.
  - Tilsvarende konfigurasjon i konfigurasjonsfilen er `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Hva er minimum tilgjengelighet?

> For mer informasjon om TMDBs datoer som påvirker de nedenfor nevnte tilgjengelighetene, se [Hvordan bestemmer Radarr året for filmen](#hvordan-bestemmer-radarr-året-for-en-film)
{.is-info}

- **Kunngjort**: Radarr vil anse filmer som tilgjengelige så snart de er lagt til i Radarr. Denne innstillingen anbefales hvis du har gode private indekser (eller virkelig gode offentlige, f.eks. rarbg.to) som ikke har falske filmer.
- **I kinoene**: Radarr vil anse filmer som tilgjengelige så snart de kommer på kino (teaterdato på TMDb). Denne innstillingen anbefales ikke.
- **Utgitt**: Radarr vil anse filmer som tilgjengelige så snart Blu-Ray- eller strømmingsversjonen er utgitt (digitale og fysiske datoer på TMDb). Denne innstillingen anbefales og bør sannsynligvis kombineres med en tilgjengelighetsforsinkelse på `-14` eller `-21` dager.
  - Hvis TMDb ikke har en dato, antas det at filmen er tilgjengelig på nettet eller i fysiske tjenester 90 dager etter `Theatrical Date` (eldste dato for teaterets visning).

## Hvordan sammenlignes mulige nedlastinger?

> Generelt sett har kvalitet høyest prioritet. Hvis du ønsker at kvalitet ikke skal være hovedprioritet, kan du slå sammen kvalitetene dine. [Se TRaSHs guide](https://trash-guides.info/merge-quality)
{.is-info}

- Den nåværende logikken [kan alltid finnes her](https://github.com/Radarr/Radarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs).

- Fra og med 2022-01-23 er logikken som følger:

1. Kvalitet\*
1. Poeng for tilpasset format
1. Protokoll (som konfigurert i den relevante forsinkelsesprofilen)
1. Indekserprioritet
1. Indekserflagg
1. Seeder/jevnaldrende (hvis torrent)
1. Alder (hvis Usenet)
1. Størrelse

> Denne rangeringen gjelder både utgivelser som ville vært oppgraderinger av kvalitet og/eller tilpasset format.
{.is-info}

> \*REPACKS og PROPERs er v2 av kvaliteter og rangerer derfor over en ikke-repack av samme kvalitet. [Sett Mediahåndtering => Filhåndtering `Last ned Proper & Repacks` til "Ikke foretrekk"](/radarr/settings#file-management) og bruk [Repack/Proper tilpasset format](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#repack-proper).{.is-warning}

## Hva er lister og hva kan de gjøre for meg?

- Lister er en del av Radarr som lar deg følge en bestemt liste fra forskjellige kilder, inkludert Plex.
- Lister er ikke ment å være en "legg til nå" -funksjonalitet, men er heller en funksjonalitet for å legge til filmer på denne listen etter hvert.
- La oss si at du følger en bestemt listeoppretter på Trakt/TMDb og virkelig liker deres seksjon for Marvel Cinematic Universe-filmer og vil se hver film på listen deres. Du ser i Radarr at du ikke har disse filmene. I stedet for å søke én etter én og legge til disse listene og deretter søke indekserne etter disse filmene, kan du gjøre alt dette samtidig med en liste. Listene kan settes til å importere alle filmene på den kuratorens liste, samt automatisk tilordne en kvalitetsprofil, automatisk legge til og automatisk overvåke den filmen.
- Lister kan også brukes til å synkronisere Radarr med en annen Radarr-instans eller importere en eller flere av Plex-brukernes avspillingslister.

> **FORSIKTIG:** Hvis listene brukes feil, kan de skape kaos i biblioteket ditt ved å legge til mange filmer du ikke har til hensikt å se. Sørg for at du er kjent med listen før du klikker på Lagre.
{.is-warning}

- Det anbefales å se på listen fysisk før du går til Radarr.

### Hvorfor tar det så lang tid å synkronisere lister, og kan jeg endre det?

- Lister var aldri ment å være "legg til nå", de er verktøy for "hei, jeg vil ha dette, legg det til etter hvert".
- Du kan utløse en manuell oppdatering av listen ved å teste den, legge til filmene i Radarr, bruke Ombi, Petio, Overseer eller en lignende app som legger dem til med en gang.
- Denne begrensningen er for å unngå at serveren vår og listeleverandørene våre blir overbelastet av personer som oppdaterer lister hvert 10. minutt.
- I Radarr før v4.7 kan intervallet konfigureres i [Innstillinger => Lister](/radarr/settings#lists) for mellom 6-24 timer. Standardverdien er 24 timer.
- I Radarr v4.7 er disse verdiene nå hardkodet og ikke konfigurerbare. Tidene er basert på listetypen for å minimere påvirkningen på tredjepartstjenester og tillate at Radarrs funksjonalitet med dem fortsetter.

## Kan alle filmfilene mine lagres i én mappe?

- Nei, og grunnen er at Radarr er en forgrening av [Sonarr](/sonarr), der hver serie har en mappe. Denne begrensningen er et kjent problem for mange brukere og kan kanskje bli løst i en fremtidig versjon. Vær oppmerksom på at dette ikke er en enkel endring og faktisk krever en fullstendig omskriving av bakenden.
- [GitHub-problemet for tilpassede mapper](https://github.com/Radarr/Radarr/issues/153) dekker teknisk sett denne forespørselen, men det er ingen garanti for at alle filmfiler i én mappe vil bli implementert på det tidspunktet.
- En liten "hack-ish" løsning er beskrevet nedenfor. Vær oppmerksom på at du ikke må starte en ny skanning i Radarr, da vil den vises som manglende, og uansett vil filmen aldri bli oppgradert.
  - Bruk et tilpasset skript
    - Skriptet skal aktiveres ved import
    - Det skal være designet for å flytte filen når du ønsker det
    - Deretter må det kalle Radarr API-en og endre filmen til "ikke overvåket".
- Hvis du vil flytte alle filmene dine fra én mappe til individuelle mapper, kan du se artikkelen [Tips og triks => Opprett en mappe for hver film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

## Kan jeg legge alle filmene mine i biblioteket i én mappe?

- Nei, se ovenfor.

## Hvordan oppdaterer jeg Radarr?

- Gå til Innstillinger og deretter til fanen Generelt og vis avanserte innstillinger (bruk bryteren ved siden av lagre-knappen).

1. Under Oppdateringer-seksjonen endrer du grennavnet til `master` eller `develop`
1. Lagre

*Dette vil ikke installere bitene fra den grenen umiddelbart, det vil skje under neste oppdatering.*

- ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Den er testet av brukere på utviklings- og nattlige grener, og det er ikke kjent at den har noen større problemer. Denne versjonen vil motta oppdateringer omtrent månedlig. På GitHub er dette `master`-grenen.

- ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (Beta): Dette er kanten for testing. Utgitt etter testing i nattlige for å sikre at det ikke er umiddelbare problemer. Nye funksjoner og feilrettinger utgis her først etter nattlige. Den kan betraktes som halvstabil, men er fortsatt `beta`. Denne versjonen vil motta oppdateringer enten ukentlig eller annenhver uke, avhengig av utvikling.

> **Advarsel: Du kan kanskje ikke gå tilbake til `master` etter å ha byttet til denne grenen.** På GitHub er dette et øyeblikksbilde av `develop`-grenen på et bestemt tidspunkt.
{.is-warning}

- ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (Alfa/Ustabil): Dette er den aller nyeste versjonen. Den utgis så snart koden er bekreftet og består alle automatiserte tester. Denne bygningen er kanskje ikke brukt av oss eller andre brukere ennå. Det er ingen garanti for at den vil kjøre i noen tilfeller. Denne grenen anbefales bare for avanserte brukere. Problemer og egen undersøkelse forventes i denne grenen. ***Bruk denne grenen bare hvis du vet hva du gjør og er villig til å bli skitten på hendene for å gjenopprette en mislykket oppdatering.*** Denne versjonen oppdateres umiddelbart.

> **Advarsel: Du kan kanskje ikke gå tilbake til `master` etter å ha byttet til denne grenen.** På GitHub er dette `develop`-grenen.
{.is-danger}

- Merk: Hvis du har installert via Docker, legg til `:release`, `:latest`, `:testing` eller `:develop` på slutten av kontainermerket, avhengig av hvem som lager byggene dine.

|                                                                    | ![Current Master/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Current Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Kan jeg oppdatere Radarr inne i Docker-kontaineren min?

- *Teknisk sett, ja.* **Men du bør absolutt ikke gjøre det.** Det er en grunnleggende filosofi i Docker. Databaseproblemer kan oppstå hvis du oppgraderer installasjonen din til den nyeste `nightly`-versjonen, men deretter oppdaterer Docker-kontaineren selv (og muligens nedgraderer til en eldre versjon).

### Installere en nyere versjon

#### Native

1. Gå til System og deretter til fanen Oppdateringer
1. Nyere versjoner som ikke er installert ennå, vil ha en oppdateringsknapp ved siden av dem. Klikk på den knappen for å installere oppdateringen.

#### Docker

1. Dra taggen på nytt og oppdater kontaineren din

## Kan jeg bytte fra `nightly` tilbake til `develop`?

## Kan jeg bytte mellom grener?

- Hvis versjonen er identisk, kan du bytte, ellers sjekk med utviklingsteamet for å se om du kan bytte fra `nightly` til `master`; `nightly` til `develop`; eller `develop` til `master` for ditt spesifikke bygg.
- Hvis du ikke følger disse instruksjonene, kan Radarr bli ubrukelig eller kaste feil. Du er advart. Hvis du støter på feilmeldingene nedenfor, bruker du en nyere database med en eldre \*Arr-versjon som ikke støttes. Oppgrader \*Arr til versjonen du tidligere hadde eller nyere.
  - Eksempel på feilmeldinger:
    - `Error parsing column 45 (Language=31 - Int64)`
    - `The DataMapper was unable to load the following field: 'Languages' value`
    - `ID does not match a known language Parameter name: id`
    - Andre lignende databasefeil som manglende kolonner eller tabeller.

## Hvordan sikkerhetskopierer/gjenoppretter jeg Radarr?

### Sikkerhetskopiering av Radarr

#### Bruke innebygd sikkerhetskopiering

- Gå til System => Sikkerhetskopiering i Radarr-brukergrensesnittet
- Klikk på Sikkerhetskopier-knappen
- Last ned zip-filen etter at sikkerhetskopieringen er opprettet for å lagre den på et trygt sted

#### Bruke filsystemet direkte

- Finn plasseringen til AppData-mappen for Radarr
  - Gå til System => Om i Radarr-brukergrensesnittet
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Stopp Radarr - Dette forhindrer at databasen blir ødelagt
- Kopier innholdet til et trygt sted

### Gjenoppretting fra sikkerhetskopiering

> Å gjenopprette til et operativsystem som bruker forskjellige stier vil ikke fungere (Windows til Linux, Linux til Windows, Windows til OS X eller OS X til Windows), det kan fungere å flytte mellom OS X og Linux, siden begge bruker stier som inneholder `/` i stedet for `\` som Windows bruker, men det støttes ikke. Du må manuelt redigere alle stier i databasen eller bruke [Toolbarr](https://github.com/Notifiarr/toolbarr).
{.is-warning}

#### Bruke zip-sikkerhetskopiering

- Installer Radarr på nytt (hvis aktuelt / ikke allerede installert)
- Kjør Radarr
- Gå til System => Sikkerhetskopiering
- Velg Gjenopprett sikkerhetskopiering
- Velg Velg fil
- Velg sikkerhetskopierings-zip-filen din
- Velg Gjenopprett

#### Bruke filsystem-sikkerhetskopiering

- Installer Radarr på nytt (hvis aktuelt / ikke allerede installert)
- Finn plasseringen til AppData-mappen for Radarr
  - Kjør Radarr én gang og gå til System => Om i brukergrensesnittet
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Stopp Radarr
- Slett innholdet i AppData-mappen **(inkludert .db-wal/.db-journal-filene hvis de eksisterer)**
- Gjenopprett fra sikkerhetskopien din
- Start Radarr
- Så lenge stiene er de samme, vil alt fortsette der det slapp

#### Gjenoppretting av filsystem på Synology NAS

> ADVARSEL: Gjenoppretting på en Synology krever kunnskap om Linux og rot-SSH-tilgang til Synology-enheten.
{.is-warning}

- Installer Radarr på nytt (hvis aktuelt / ikke allerede installert)
- Finn plasseringen til AppData-mappen for Radarr
  - Kjør Radarr én gang og gå til System => Om i brukergrensesnittet
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Stopp Radarr
- Koble til Synology NAS via SSH og logg inn som root

> På noen installasjoner er brukeren annerledes enn i kommandoene nedenfor: `chown -R sc-Radarr:Radarr *` {.is-info}

- Utfør følgende kommandoer:

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- Oppdater tillatelser på filene:

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- Start Radarr

# Vanlige problemer med Radarr

## En oppgave ble avbrutt

- Radarr mottok ingen respons fra serveren forespørselen ble sendt til etter 100 sekunder.
- Loggene vil inneholde `System.Threading.Tasks.TaskCanceledException: A task was canceled.`
- Dette skyldes ofte:
  - feil konfigurert eller bruk av VPN
  - feil konfigurert eller bruk av proxy
  - lokale DNS-problemer - Prøv å bytte til en annen DNS-leverandør
  - lokale IPv6-problemer - *mest vanlig* - vanligvis er IPv6 aktivert på vertsoperativsystemet, men fungerer ikke
  - bruk av Privoxy og feil konfigurering av det
  - PiHole [Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit) forespørsler
- Du kan feilsøke med DNS `nslookup <domene.tld fra sporingsloggene>` og ipv6 med `curl -sv -6 "<url fra sporingsloggene>"` / all annen tilkobling med `curl -sv -4 "<url fra sporingsloggene>"`

## Stien er allerede konfigurert for en eksisterende film

![existing-movie.png](/assets/radarr/existing-movie.png)

- Bibliotekimport viser "Eksisterende" eller du får en feil som sier "Stien er konfigurert for en eksisterende film"
- Dette skjer når du prøver å legge til en film eller redigere stien til en eksisterende film som allerede er tilordnet en annen film.
- Sannsynligvis skyldes dette at du ikke rettet opp en feilaktig tilordnet film da du importerte biblioteket ditt.
- Finn og rett opp filmen som allerede er tilordnet den aktuelle filmens sti.
  - Filindeks
  - Tabellvisning
  - Alternativer => Legg til sti som en kolonne
  - Sorter og finn filmen med den merkede problematiske stien.
- Alternativt kan du slette filmen som bruker den eksisterende stien fra Radarr

## Hvordan kan jeg endre navn på filmmappe?

{#rename-folders}

> Den samme prosessen gjelder også for å flytte/endre stier for filmer. Hvis du bare oppdaterer stiene i Radarr og ikke trenger å flytte filene, må du ikke velge "Ja, flytt filer" i trinn 5.
{.is-info}

1. Filmer
1. Filmredigerer
1. Velg hvilke filmer som trenger å få mappen sin omdøpt
1. Endre rotmappen til samme rotmappe som filmene allerede eksisterer i
1. Velg "Ja, flytt filer"

> Hvis du bruker Plex, vil dette utløse ny deteksjon av intros, miniatyrbilder, kapitler og forhåndsvisningsmetadata.
{.is-warning}

## Navngivning av filmfiler og mapper

- For øyeblikket krever Radarr at hver film er i en mappe med formatet `Filmnavn (År)/`, valgfritt er `_` eller `.` gyldige skilletegn. For å lette riktig identifisering av kvalitet og oppløsning under import, er det best med et filnavn som `Filmnavn (År) [Kvalitet-oppløsning].ext`, igjen er `_` eller `.` gyldige skilletegn.

  - Et nyttig verktøy for å gjøre disse endringene i samlingen din er [filebot](http://www.filebot.net/#download), som har en betalt versjon i både Apple og Windows-butikkene, men kan finnes gratis på deres eldre [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download) nettsted. Det har både et GUI og CLI, så du kan bruke det du er komfortabel med. For det ovennevnte eksempelet vil `{ny}` utvides til `Navn (År)` og `{vf}` gir oppløsningen som `1080p`. Det er ingenting å slutte seg til kvaliteten, så du kan jukse ved å bruke `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`, som vil navngi alt lavere enn 720p til `[DVD-572p]` og større eller lik 720p som `[Bluray-1080p]`.

- Se [Tips and Tricks Section => Create a Folder for Each Movie](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie) for mer informasjon.

## Mapper for filmer er navngitt feil

- Navngivningen av filmmapper er basert på metadataen (navn/år) på tidspunktet da filmen ble lagt til. Hvis du la til en film før den ble utgitt, kan du måtte bruke trikset med å omdøpe mappen som er nevnt ovenfor for å oppdatere navngivningen av filmmappen for å gjenspeile de nye nåværende dataene.
- Selv om filmene dine allerede er i mapper, kan mappene være navngitt feil. Mappenavnet skal være `Filmnavn (År)`, og å ha tittel og år i mappens navn er kritisk akkurat nå.

  - Eksempler som vil fungere bra:
    - `/mnt/Filmer/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Barnas Filmer/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - Eksempler som vil fungere, men vil kreve manuell administrasjon:
    - Etter bokstaver: `/mnt/Filmer/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Etter rangering: `/mnt/Filmer/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Etter sjanger: `/mnt/Filmer/Crime, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Disse eksemplene vil kreve manuell administrasjon når filmen legges til. Hver av eksemplene vil ha mange rotmapper, som `A-D` og `E-G` i eksemplet med første bokstav, `R` og `PG-13` i eksemplet med rangering, og du kan gjette variasjonen av sjangermapper. Når du legger til en ny film, må riktig grunnmappe velges for at dette formatet skal fungere.
  - Eksempler som ikke vil fungere:
    - Enkeltmappe: `/mnt/Barnas Filmer/Frozen (2013) [Bluray-1080p].mkv`
      - For øyeblikket må filmene bare være i en mappe med navn etter filmen. Det er ingen måte å omgå dette på før utviklingsarbeidet er gjort for å legge til denne funksjonen.
    - **Film** Navngivningsformater fra v0.2 som inkluderer **Fil** egenskaper i **filmmappe** navnet som ``{Film.Tittel}.{Utgivelsesår}.{Kvalitet.Full}-{MediaInfo.Enkel}{`Utgivelsesgruppe}`` vil ikke fungere i v3.
      - Mapper er relatert til filmen og uavhengig av filen. I tillegg vil dette bryte med den planlagte støtten for flere filer per film.
      - Den andre grunnen til at det ble fjernet var at det forårsaket hyppig forvirring, databasekorruptering og generelt sett var det bare halvveis implementert.
  - [Tips and Tricks Section => Create a Folder for Each Movie](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) er en flott kilde for å sikre at fil- og mappstrukturen din fungerer bra.

## Kan jeg deaktivere oppgaven for oppdatering av filmer?

- Nei, og du bør heller ikke gjøre det gjennom noen SQL-hack. Oppgaven for oppdatering av filmer spør den oppstrøms Servarr-proxyen og sjekker om metadataen for hver film (ID-er, rollebesetning, sammendrag, rangering, oversettelser, alternative titler osv.) har blitt oppdatert sammenlignet med det som er i Radarr for øyeblikket. Hvis det er nødvendig, vil den deretter oppdatere de aktuelle filmene.
- En vanlig klage er at oppgaven for oppdatering forårsaker tung I/O-bruk.
- Hovedinnstillingen er "Skann filmmappe etter oppdatering". Hvis disk I/O-bruken øker under en oppdatering, kan du endre skanneinnstillingen til `Manuell`.
  - Ikke endre dette til `Aldri` med mindre alle endringer i biblioteket ditt (nye filmer, oppgraderinger, slettinger osv.) gjøres gjennom Radarr.
  - Hvis du sletter filmfiler manuelt eller via Plex eller et annet tredjepartsprogram, må du ikke sette dette til `Aldri`.
- Den andre innstillingen som kan endres, er "Analyser videofiler", som anbefales å være aktivert hvis du bruker tdarr eller på annen måte endrer filene dine eksternt. Hvis du ikke gjør det, kan du trygt deaktivere "Analyser videofiler" for å redusere noe I/O.

## Hvordan kan jeg be om en funksjon for Radarr?

- Dette er enkelt [klikk her](https://github.com/Radarr/Radarr/issues)

## Hjelp, Macen min sier at Radarr ikke kan åpnes fordi utvikleren ikke kan verifiseres

- Dette er enkelt, se denne lenken for mer informasjon [her](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Utvikler kan ikke verifiseres](developer-cannot-be-verified.png "Utvikler kan ikke verifiseres")
- Alternativt kan du måtte selv-signere Radarr `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## Hjelp, Macen min sier at Radarr.app er skadet og kan ikke åpnes

- Det skyldes enten en korrupt nedlasting, så prøv igjen, eller [sikkerhetsproblemer, se denne relaterte FAQ-oppføringen.](#hjelp-mac-sier-at-radarr-ikke-kan-åpnes-for-diagnose)

## Jeg får en feilmelding: Database disk image is malformed

> \* For Radarr-brukere som opplever dette etter oppgradering til v4.X-versjoner. v4-versjoner gjør flere omfattende migreringer fordi hvis databasen din hadde tidligere korrupte steder (som kanskje ikke var påvisbare tidligere kjøring av Radarr), vil migreringen mislykkes. Dette vil føre til at Radarr ikke starter. Det er sannsynlig at alle sikkerhetskopiene dine også er korrupte, så det å gjenopprette dem vil sannsynligvis ikke løse problemet.
> \* Hvis den migrerte databasen ikke kan åpnes eller ikke kan gjenopprettes, må du lage en kopi av databasen fra en nylig sikkerhetskopi og bruke databasens gjenopprettingsprosess på den filen, og deretter prøve å starte Radarr med den gjenopprettede sikkerhetskopifilen. Den skal da migrere uten problemer.
{.is-warning}

- **Feilene "Error creating log database" indikerer problemer med logs.db**
  - Dette kan raskt løses ved å omdøpe eller fjerne databasen. Logs-databasen inneholder uvesentlig informasjon om kommandohistorikk og oppdateringsinstallasjonshistorikk, samt Info-, Warn- og Error-oppføringer.
- **Feilene "Error creating main database" eller generelle "database disk image is malformed" uten spesifisert database indikerer problemer med radarr.db**
  - Fortsett med trinnene nedenfor
- Dette betyr at SQLite-databasen som lagrer mesteparten av informasjonen for Radarr, er korrupt. Du har muligheten til å prøve (en) sikkerhetskopi(er), prøve å gjenopprette den eksisterende databasen, prøve å gjenopprette sikkerhetskopi(er), eller hvis alt annet mislykkes, starte på nytt med en helt ny database.
- Denne feilen kan vises hvis databasefilen ikke kan skrives av brukeren/gruppen \*Arr kjører som. Tillatelser som årsak vil sannsynligvis bare være et problem for nye installasjoner, migrerte installasjoner til en ny server, hvis du nylig har endret tillatelsene for appdata-katalogen din, eller hvis du har endret brukeren og gruppen \*Arr kjører som.
- Ditt beste og første alternativ er å [prøve å gjenopprette fra en sikkerhetskopi](#hvordan-sikkerhetskopierer-gjenoppretter-jeg-radarr). Imidlertid er det svært usannsynlig at sikkerhetskopien i seg selv vil fungere, og du må prøve de andre gjenopprettingsmetodene som er nevnt.
- Du kan også prøve å gjenopprette databasen din. Dette er vanligvis det eneste alternativet når dette problemet oppstår etter en oppdatering. Prøv [sqlite3 `.recover`-kommandoen](/useful-tools#recovering-a-corrupt-db)
  - Hvis sqlite ikke har `.recover` eller du ønsker en mer GUI-vennlig (f.eks. Windows) måte, følg [instruksjonene våre på denne wikien.](/useful-tools#recovering-a-corrupt-db-ui)
- En annen mulig årsak til at du får en feil med databasen din, er at du plasserer databasen din på en nettverksstasjon (nfs eller smb eller noe annet som ikke er lokalt). **SQLite er designet for situasjoner der data og programvare eksisterer på samme maskin.** Derfor må \*Arr AppData-mappen din (/config-monteringspunkt for Docker) være på lokal lagring. [SQLite og nettverksstasjoner fungerer ikke bra sammen og vil til slutt føre til en ødelagt database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruker mergerFS, må du fjerne `direct_io` siden SQLite bruker mmap, som ikke støttes av `direct_io`, som forklart i mergerFS [dokumentasjonen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jeg bruker Radarr på en Mac, og den sluttet plutselig å fungere. Hva skjedde?

- Mest sannsynlig skyldes dette en MacOS-feil som førte til at en av databasene ble korrupt.
- Se oppføringen om at databasen er korrupt ovenfor.
- Prøv deretter å starte og se om det fungerer. Hvis det ikke fungerer, trenger du ytterligere støtte. Legg ut i [subredditen vår /r/radarr](http://reddit.com/r/radarr) eller bli med på [discord-serveren vår](https://radarr.video/discord) for hjelp.

## Hvorfor kan ikke Radarr se filene mine på en ekstern server?

- For alle operativsystemer må du sørge for at brukeren/gruppen du kjører \*Arr som, har lese- og skrivetilgang til den monterte disken.
- For Linux, sørg for:
  - Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert for monteringen din.
  - Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert for monteringen din.
- For Windows: Kort sagt, brukeren \*Arr kjører som (hvis tjeneste) eller under (hvis skuffeprogram) kan ikke få tilgang til filbanen på den eksterne serveren. Dette kan skyldes forskjellige årsaker, men det vanligste er at \*Arr kjører som en tjeneste, noe som forårsaker problemene som beskrives nedenfor.

### Radarr kjører som standard under LocalService-kontoen, som ikke har tilgang til beskyttede eksterne filområder

- Kjør Radarr-tjenesten som en annen bruker som har tilgang til den delte mappen
- Åpne vinduet Administrative Tools \> Services på Windows-serveren din.
- Stopp Radarr-tjenesten.
- Åpne dialogboksen Properties \> Log On.
- Endre brukerkontoen for tjenesten til målbrukerkontoen.
- Kjør Radarr.exe ved hjelp av Startup-mappen

### Du bruker en kartlagt nettverksstasjon (ikke en UNC-bane)

- Endre banene dine til UNC-baner (`\\server\share`)
- Kjør Radarr.exe via Startup-mappen

## Hvordan kan jeg bytte fra Windows-tjenesten til et skuffeprogram?

1. Stopp Radarr
1. Kjør serviceuninstall.exe som er i Radarr-mappen
1. Kjør `Radarr.exe` som administrator én gang for å gi den riktige tillatelser og åpne brannmuren. Når det er fullført, kan du lukke det og kjøre det normalt.
1. (Valgfritt) Legg til en snarvei til .exe-filen i oppstartsmappen for å starte automatisk ved oppstart.

## Hjelp, jeg har låst meg ute

{#help-i-have-forgotten-my-password}

For å deaktivere autentisering (for å tilbakestille glemt brukernavn eller passord), må du redigere `config.xml`, som vil være inne i [Radarr Appdata-katalogen](/radarr/appdata-directory)

1. Åpne config.xml i en tekstredigerer
1. Finn linjen for autentiseringsmetode, som vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Endre linjen `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Radarr på nytt
1. Radarr vil nå være tilgjengelig uten passord, du bør gå til `Innstillinger: Generelt` i brukergrensesnittet og angi brukernavnet og passordet ditt

## Hvordan kan jeg forhindre at nettleseren åpnes ved oppstart?

Avhengig av operativsystemet ditt, er det flere mulige måter.

- I `Innstillinger` => `Generelt` på noen operativsystemer er det en avmerkingsboks for å åpne nettleseren ved oppstart.
- Når du starter Radarr, kan du legge til `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumentene.
- Stopp Radarr og rediger config.xml-filen, og endre `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Rar brukergrensesnittproblemer

- Hvis du opplever rare brukergrensesnittproblemer som at bibliotekssiden ikke viser noe eller at en bestemt visning eller sortering ikke fungerer, kan du prøve å se i en Chrome Inkognitovindu eller Firefox Privat vindu. Hvis det fungerer fint der, kan du tømme nettleserens hurtigbuffer og informasjonskapsler for din spesifikke IP/domene. For mer informasjon, se artikkelen [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage) på wikien vår.

## Nettgrensesnittet lastes bare på localhost på Windows

- Hvis du bare kan nå nettgrensesnittet ditt på <http://localhost:7878/> eller <http://127.0.0.1:7878/>, må du kjøre som administrator minst én gang.

## Tillatelser

- Radarr må flytte filer fra der nedlasteren legger dem til den endelige plasseringen, så dette betyr at den må lese/skrive til både kildekatalogen og destinasjonskatalogen og filene.
- På Linux, der beste praksis er at tjenester kjører som sin egen bruker, vil dette sannsynligvis bety å bruke en delt gruppe og sette mappe tillatelser til `775` og filer til `664` både i nedlasteren din og . I umask-notasjon vil det være `002`.

## System og logger lastes inn for alltid

- Det er easy-privacy blokkeringslisten. De blokkerer i utgangspunktet alle URL-er med /api/log? i dem. Se gjennom listen og fortell meg om du synes det er fornuftig å blokkere alle URL-ene i den, det er dusinvis av URL-er der som potensielt ødelegger nettsteder. Du valgte det i annonseblokkereren din. En enkel løsning er å legge domenet Radarr kjører på i hvitelisten. Men jeg anbefaler likevel å sjekke listen.

## Pakk ut torrenter

- De fleste torrentklienter har ikke automatisk håndtering av komprimerte arkiver som deres Usenet-motparter. Vi anbefaler [unpackerr](https://github.com/unpackerr/unpackerr).

## uTorrent fungerer ikke lenger

- Sørg for at Web UI er aktivert
- Sørg for at alternativ lytteport (Avansert => Web UI) ikke er den samme som lytteporten (Tilkoblinger)
- Vi anbefaler å endre alternativ lytteport for Web UI slik at det ikke påvirker portvideresending for tilkoblinger.

## Jeg fikk en popup-melding som sa at config.xml var korrupt, hva nå?

- Radarr kunne ikke lese konfigurasjonsfilen ved oppstart fordi den ble på en eller annen måte korrupt. For å komme tilbake på nettet, må du slette `.xml` i [appdata-katalogen](/radarr/appdata-directory), når den er slettet, starter den på standardporten (7878), du bør nå konfigurere eventuelle innstillinger du konfigurerte på siden for generelle innstillinger.

## Ugyldig sertifikat og andre HTTPS- eller SSL-problemer

- Din nedlastingsklient sluttet å fungere, og du får en feilmelding som "Localhost is an invalid certificate"?
  - Radarr validerer SSL-sertifikater. Hvis det ikke er satt opp et SSL-sertifikat i nedlastingsklienten, eller hvis du bruker et selvsignert https-sertifikat uten at CA-sertifikatet er lagt til i den lokale sertifikatbutikken din, vil Radarr nekte å koble til. Gratis, riktig signerte sertifikater er tilgjengelige fra [let's encrypt](https://letsencrypt.org/).
  - Hvis nedlastingsklienten din og Radarr kjører på samme maskin, er det ingen grunn til å bruke HTTPS, så den enkleste løsningen er å deaktivere SSL for tilkoblingen. De fleste vil være enige i at det heller ikke er nødvendig i et lokalt nettverk. Det er mulig å deaktivere sertifikatvalidering i avanserte innstillinger hvis du ønsker å beholde en usikker SSL-konfigurasjon.

## VPN-er, Jackett og \*ARR-ene

- Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, er det vanligvis bare torrentklienten din som trenger å være bak en VPN. Fordi VPN-endepunktet deles av mange brukere, kan du oppleve begrensninger i hastigheten, DDOS-beskyttelse og IP-blokkering fra ulike tjenester som hver programvare bruker.
- Med andre ord kan det å sette \*ARR-ene (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bak en VPN gjøre programmene ubrukelige i noen tilfeller på grunn av at tjenestene ikke er tilgjengelige.

> **For å være tydelig, det er ikke et spørsmål om VPN-er vil forårsake problemer med \*ARR-ene, men når: bildeleverandører vil blokkere deg, og Cloudflare er foran de fleste \*ARR-servere (oppdateringer, metadata osv.) og kan også blokkere deg**
{.is-warning}

- **Mange private trackere vil utestenge deg hvis du bruker eller får tilgang til dem (f.eks. ved å bruke Jackett eller Prowlarr) via en VPN.**

### Bruk av VPN

- Hvis en VPN er nødvendig og Docker brukes, anbefales det å bruke Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er nødvendig og Docker ikke brukes, må VPN-klienten din ***støtte delt tunnelering slik at bare de nødvendige (nedlastingsklient) appene er bak VPN-en.
- Mange problemer med å få tilgang til trackere kan løses ved å bruke Googles eller Cloudflares DNS-servere i stedet for ISP-ens DNS-servere.
- I noen tilfeller (f.eks. britiske internettleverandører) kan du måtte sette torrentnedlastingsklienten bak en VPN og Jackett/Prowlarr som følger:
  - Sett Jackett bak VPN-en og sørg for at delt tunnelering tillater lokal tilgang.
  - For Prowlarr kan du konfigurere VPN-klienten din til å gi en proxy og legge til proxyen i Innstillinger => Indekser. Gi proxyen en tagg, og gi alle indekser som trenger å bruke den samme taggen.
    - Hvis det absolutt er nødvendig, og hvis VPN-en din ikke gir en måte å opprette en proxy på, kan du sette Prowlarr bak VPN-en og sørge for at delt tunnelering tillater lokal tilgang.

# Vanlige problemer med søk og nedlasting i Radarr

## Hvorfor kan jeg ikke legge til en ny film i Radarr?

{#why-cant-i-add-a-new-movie-to-radarr}

- Radarr bruker [The Movie Database (TMDb)](http://themoviedb.org) for filminformasjon og bilder som fanart, bannere og bakgrunner. Generelt sett er det noen grunner til at du kanskje ikke kan legge til en film:
  - TMDb liker ikke at spesialtegn brukes når du søker etter filmer via API-en (som Radarr bruker), så prøv å søke med et oversatt navn og/eller uten spesialtegn.
  - Du kan også legge til ved hjelp av TMDb-ID eller, hvis TMDb har det, IMDb-ID-en.
  - Filmen er ikke lagt til i TMDb ennå, følg deres [veiledning](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006) for å få den lagt til.

## Jackett viser flere resultater enn manuelt søk

- Dette skyldes vanligvis at du søker i Jackett på en annen måte enn du gjør manuelt. Se vår [feilsøkingsartikkel](/radarr/troubleshooting) for mer informasjon.

## Hvordan bestemmer Radarr året for en film?

- Radarr henter metadata fra [TMDb](https://www.themoviedb.org/)
- Radarr bruker året for den eldste **kinopremieren** og den eldste **premieren** for å finne riktig film.
  - Merk at hvis det ikke finnes en kinopremiere, vil logikken falle tilbake på den eldste fysiske eller digitale utgivelsesdatoen.
- Hvis en film mangler en digital, fysisk, kinopremiere eller premiere-dato, bør TMDb oppdateres.
- [TMDb's Contribution Bible](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013) nevner følgende om utgivelsestypene deres.
  - **Premiere** - En premierevisning kan være en festivalvisning (f.eks. TIFF) eller en premierehendelse med skuespillere og mannskap i en storby (f.eks. LA, London, Toronto).
  - **Kinopremiere** - Kan brukes for den opprinnelige utgivelsen og eventuelle påfølgende offisielle utgivelser. Brukes for bred eller mettet utgivelse. I USA regnes 600-1 999 skjermer som bred utgivelse, og 2000+ regnes som mettet utgivelse.
  - **Kinopremiere (begrenset)** - Begrenset kinopremiere er en distribusjonsstrategi for filmer der en ny film slippes i noen få kinoer over hele landet, vanligvis i større storbyområder. I USA er antallet kinoer færre enn 600.
  - **Fysisk** - Inkluderer alle VHS-, DVD- og Blu-ray-utgivelser.
  - **Digital** - Alle relevante utgivelser kan legges til, inkludert strømmetjenester, VOD-utleie eller -kjøp. Digitale visninger, inkludert online filmfestivaler og virtuelle kinoutgivelser, regnes også som digitale utgivelser.

## Hvordan håndterer Radarr utenlandske filmer eller utenlandske titler?

> [TRaSH's Custom Format Language Guide](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) kan være nyttig for å hjelpe deg med å få filmer på det språket (eller de språkene) du ønsker.{.is-info}

> Fra og med 12. februar 2023 vil Radarrs metadata-cache begynne å bruke en films opprinnelige språk som TMDb's talespråk bare hvis det bare finnes ett talespråk for filmen på TMDb; ellers vil filmens opprinnelige TMDb-språk bli brukt.
{.is-warning}

## Søk etter ID

- **Indekser som støtter søk basert på ID** - Søk på indekser og trackere som støtter søk basert på ID (TMDbId, IMDbId osv.) - som mange Usenet-indekser og mange private torrent-trackere - tekstforespørsler brukes ikke hvis det returneres resultater for et ID-basert søk. Hvis det returneres resultater, vil det ikke falle tilbake til et navn-/tekstsøk. Hvis du mangler resultater fra indeksen din, skyldes det at utgivelsen(e) er knyttet til feil film-ID.
  - Utgivelsens språk kan også hentes fra indeksen eller trackernes utgivelsesspråk i resultatet hvis det er oppgitt, i stedet for å parses fra navnet.

## Tekstsøk

- **Indekser som ikke støtter ID-baserte søk eller ID-baserte søk uten resultater** - Søk på vil bruke filmens opprinnelige tittel, engelske tittel og oversatt tittel fra [hvilke språk du har valgt i filmens kvalitetsprofil og eventuelle tilpassede formater med poengsum større enn null](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/).
- Parsing (dvs. importering) ser etter en match i alle oversettelser og alternative titler.
  - Utgivelsens språk kan også hentes fra indeksen eller trackernes utgivelsesspråk i resultatet hvis det er oppgitt, i stedet for å parses fra navnet.

## Få utenlandske filmer

- For å få en film på et fremmed språk, sett filmens kvalitetsprofil-språk til Original (Filmens opprinnelige språk\*), et spesifikt språk for den profilen eller `Any`, og opprett og gi en poengsum større enn 0 [Tilpassede formater med språkbetingelser for å bestemme hvilket språk som skal lastes ned - se TRaSH's Guide for detaljer](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/).
- Merk at dette ikke inkluderer noen indeksspråk som er konfigurert som `multi` i indeksens innstillinger.
  - Merk at fra [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c) antas det ikke lenger at `multi` inkluderer engelsk.
  - Brukere kan justere innstillingene per indeks for å definere hvilket språk `multi` indikerer.

## Hvordan håndterer Radarr "multi" i navn?

- Med Radarr v4.1+ antar Radarr at
`multi` bare er filmens språk og **IKKE** engelsk som i tidligere versjoner.
  - Brukere kan justere innstillingene per indeks for å definere hvilket språk `multi` indikerer.
- Merk at `multi`-definisjoner bare hjelper for utgivelsesparsing og ikke for utenlandske titler eller filmsøk.

## Hjelp, filmen er lagt til, men ikke søkt etter

- Radarr søker ikke *aktivt* etter manglende filmer automatisk. I stedet gjøres det en periodisk forespørsel om nye innlegg til alle indekser som er konfigurert for RSS. Når en ønsket film eller en film som ikke oppfyller kuttet dukker opp i den listen, blir den lastet ned. Dette betyr at en film ikke blir lastet ned før den blir lagt ut (eller lagt ut på nytt).
- Hvis du legger til en film som du vil ha nå, er det beste alternativet å merke av for "Start søk etter manglende film" -boksen til venstre for *Legg til film* (**1**) -knappen. Du kan også gå til siden for en film du har lagt til og klikke på forstørrelsesglasset "Søk" (**2**) -knappen eller bruke Wanted-visningen for å søke etter manglende eller ikke oppfylte kutt-filmer.

  - Legg til og søk etter film når du legger til en film
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - Søk etter en eksisterende film
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jacketts /all-endepunkt

{#jackett-all-endpoint}

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan potensielt føre til problemer, så det er nødvendig å legge til hver tracker individuelt. Alternativt kan du vurdere Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

- **Oppdatering 1. januar 2022: Jackett `/all`-endepunktet støttes ikke lenger (dvs. advarsler vil vises) fra og med 4.0.0.5730 på grunn av at det bare skaper problemer.**

- Jackett /all-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan potensielt føre til problemer, så det er nå nødvendig å legge til hver tracker individuelt.
- [Selv Jacketts utviklere sier at det bør unngås og ikke bør brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Å bruke /all-endepunktet har ingen fordeler, bare ulemper:
  - du mister kontrollen over innstillingene for hver enkelt indeks (kategorier, søkemåter osv.)
  - blanding av søkemåter (IMDB, søk, osv.) kan føre til resultater av lav kvalitet
  - indeksspesifikke kategorier (\>= 100000) kan ikke brukes.
  - treg indekser vil bremse ned den totale resultatet
  - totalt antall resultater er begrenset til 1000
  - hvis en av trackerne i /all returnerer en feil, vil \*Arr deaktivere den, og nå får du ingen resultater.

### Løsninger for Jackett /all

- Legg til hver tracker i Jackett manuelt som en indekser i \*Arr
- Sjekk ut [Prowlarr](/prowlarr), som kan synkronisere indekser med \*Arr og er utviklet av Lidarr/Radarr/Readarr-utviklingsteamet.
- Sjekk ut [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indekser med \*Arr. Men ikke bruk deres enkeltstående aggregerte endepunkt, og bruk `multi` hvis synkronisering skal brukes.

## Hvorfor er det to filer? | Hvorfor er det en fil igjen i nedlastinger?

Dette er forventet. Med en konfigurasjon som støtter [hardlinker](https://trash-guides.info/hardlinks), vil ikke dobbelt plass bli brukt. Her er hvordan torrentprosessen fungerer.

1. Radarr sender en nedlastingsforespørsel til klienten din og knytter den til en merkelapp eller kategorinavn som du har konfigurert i innstillingene for nedlastingsklienten. Eksempler: filmer, tv, serier, musikk, osv.
1. Radarr overvåker de aktive nedlastingene i nedlastingsklienten som bruker det kategorinavnet. Denne overvåkingen skjer via nedlastingsklientens API.
1. Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Radarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil de bli hardlinket hvis det støttes av oppsettet ditt, eller kopiert hvis hardlinker ikke støttes.
1. Hvis alternativet "Behandling av fullførte nedlastinger - Fjern fullførte" er aktivert i Radarrs innstillinger, vil Radarr slette den opprinnelige filen og torrenten fra nedlastingsklienten, men bare hvis nedlastingsklienten rapporterer at seeding er fullført og torrenten er stoppet (dvs. satt på pause). Se [TRaSH's nedlastingsklientguider](https://trash-guides.info/Downloaders/) for hvordan du konfigurerer nedlastingsklienten din optimalt.

> Hardlinker er aktivert som standard. [En hardlink vil ikke bruke ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringspunktene må være de samme for den fullførte nedlastingsmappen og mediebiblioteket ditt. Hvis opprettelsen av hardlinken mislykkes eller oppsettet ditt ikke støtter hardlinker, vil det falle tilbake og kopiere filen.
{.is-info}

## Hvorfor fungerer ikke Radarr bak en omvendt proxy?

- Fra og med v3 har Radarr byttet til .NET og en ny webserver. For at SignalR skal fungere, at knappene i brukergrensesnittet skal fungere, at databasendringer skal ta effekt og andre elementer. Kreves følgende tillegg til location-blokken for Radarr:

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- Pass på at du **ikke** inkluderer `proxy_set_header Connection "Upgrade";` som foreslått av nginx-dokumentasjonen. **Dette VIL IKKE FUNGERE**
- [Se dette ASP.NET Core-problemet](https://github.com/aspnet/AspNetCore/issues/17081)
- Hvis du bruker en CDN som Cloudflare, må du sørge for at websockets er aktivert for å tillate websocket-tilkoblinger.
- Hvis du opplever uventede omdirigeringer, må du sørge for at vertshodet ditt videresendes.