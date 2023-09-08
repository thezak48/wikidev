---
title: Sonarr FAQ
description: Vanlige spørsmål om Sonarr
published: true
date: 2023-08-28T19:31:41.131Z
tags: 
editor: markdown
dateCreated: 2021-06-09T18:39:33.208Z
---

<!-- # Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Grunnleggende om Sonarr](#grunnleggende-om-sonarr)
  - [Hvordan finner Sonarr episoder?](#hvordan-finner-sonarr-episoder)
  - [Hvordan sammenlignes mulige nedlastinger?](#hvordan-sammenlignes-mulige-nedlastinger)
  - [Vanlige spørsmål om foretrukne ord](#vanlige-spørsmål-om-foretrukne-ord)
  - [Hvordan bytter jeg fra Windows-tjenesten til en brettapp?](#hvordan-bytter-jeg-fra-windows-tjenesten-til-en-brettapp)
  - [Hvordan sikkerhetskopierer/gjenoppretter jeg Sonarr?](#hvordan-sikkerhetskopierer-gjenoppretter-jeg-sonarr)
    - [Sikkerhetskopiering av Sonarr](#sikkerhetskopiering-av-sonarr)
      - [Bruke innebygd sikkerhetskopiering](#bruke-innebygd-sikkerhetskopiering)
      - [Bruke filsystemet direkte](#bruke-filsystemet-direkte)
    - [Gjenoppretting fra sikkerhetskopi](#gjenoppretting-fra-sikkerhetskopi)
      - [Bruke zip-sikkerhetskopi](#bruke-zip-sikkerhetskopi)
      - [Bruke filsystem-sikkerhetskopi](#bruke-filsystem-sikkerhetskopi)
      - [Gjenoppretting av filsystem på Synology NAS](#gjenoppretting-av-filsystem-på-synology-nas)
  - [Hjelp, jeg har låst meg ute](#hjelp-jeg-har-låst-meg-ute)
  - [Hvorfor er det to filer? \| Hvorfor er det en fil igjen i nedlastinger?](#hvorfor-er-det-to-filer-hvorfor-er-det-en-fil-igjen-i-nedlastinger)
  - [Jeg ser at funksjon/feil X ble fikset, hvorfor kan jeg ikke se det?](#jeg-ser-at-funksjonfeil-x-ble-fikset-hvorfor-kan-jeg-ikke-se-det)
  - [Episodestatus - Hvordan beregnes den?](#episodestatus-hvordan-beregnes-den)
  - [Hvordan får jeg tilgang til Sonarr fra en annen datamaskin?](#hvordan-får-jeg-tilgang-til-sonarr-fra-en-annen-datamaskin)
  - [Hvorfor oppdaterer Sonarr seriedata så ofte?](#hvorfor-oppdaterer-sonarr-seriedata-så-ofte)
  - [Hvorfor er det et tall ved siden av Aktivitet?](#hvorfor-er-det-et-tall-ved-siden-av-aktivitet)
  - [Hva er forskjellige serietyper?](#hva-er-forskjellige-serietyper)
    - [Serietyper](#serietyper)
    - [Eksempler på serietyper](#eksempler-på-serietyper)
      - [Daglig](#daglig)
      - [Standard](#standard)
      - [Anime](#anime)
  - [Hvordan kan jeg endre navn på seriemappene mine?](#hvordan-kan-jeg-endre-navn-på-seriemappene-mine)
  - [Hvordan oppdaterer jeg Sonarr?](#hvordan-oppdaterer-jeg-sonarr)
    - [Installerer en nyere versjon](#installerer-en-nyere-versjon)
      - [Nativ](#nativ)
      - [Docker](#docker)
  - [Kan jeg bytte fra `develop` tilbake til `main`?](#kan-jeg-bytte-fra-develop-tilbake-til-main)
  - [Kan jeg bytte mellom grener?](#kan-jeg-bytte-mellom-grener)
- [Sonarr og serier - problemer + metadata](#sonarr-og-serier---problemer-metadata)
  - [Hvordan håndterer Sonarr nummereringsproblemer i scener (American Dad!, osv)?](#hvordan-håndterer-sonarr-nummereringsproblemer-i-scener-american-dad-osv)
    - [Hvordan Sonarr håndterer nummereringsproblemer i scener](#hvordan-sonarr-håndterer-nummereringsproblemer-i-scener)
    - [Problematiske serier](#problematiske-serier)
  - [Hvorfor kan ikke Sonarr importere episodfiler for serie X? / Hvorfor kan ikke Sonarr finne utgivelser for serie X?](#hvorfor-kan-ikke-sonarr-importere-episodfiler-for-serie-x-hvorfor-kan-ikke-sonarr-finne-utgivelser-for-serie-x)
  - [TVDb er oppdatert, hvorfor er ikke Sonarr det?](#tvdb-er-oppdatert-hvorfor-er-ikke-sonarr-det)
  - [Hvorfor kan jeg ikke legge til en serie?](#hvorfor-kan-jeg-ikke-legge-til-en-serie)
  - [Hvorfor kan jeg ikke legge til en serie når jeg kjenner TVDb-IDen?](#hvorfor-kan-jeg-ikke-legge-til-en-serie-når-jeg-kjenner-tvdb-iden)
  - [Tittelsnutt i bruk](#tittelsnutt-i-bruk)
  - [Episoden har ikke et absolutt nummer](#episoden-har-ikke-et-absolutt-nummer)
  - [Episodetider](#episodetider)
- [Vanlige problemer med Sonarr](#vanlige-problemer-med-sonarr)
  - [Stien er allerede konfigurert for en eksisterende serie](#stien-er-allerede-konfigurert-for-en-eksisterende-serie)
  - [Episoden har ikke en evighet](#systemlogger-laster-forever)
  - [Rare UI-problemer](#rare-ui-problemer)
  - [Nettlesergrensesnittet lastes bare på localhost på Windows](#nettlesergrensesnittet-lastes-bare-på-localhost-på-windows)
  - [uTorrent fungerer ikke lenger](#utorrent-fungerer-ikke-lenger)
  - [Krever Sonarr en SABnzbd-postbehandlingskript for å importere nedlastede episoder?](#krever-sonarr-en-sabnzbd-postbehandlingskript-for-å-importere-nedlastede-episoder)
  - [Jeg fikk en popup som sa at config.xml var ødelagt, hva nå?](#jeg-fikk-en-popup-som-sa-at-configxml-var-ødelagt-hva-nå)
  - [Sonarr på Synology sluttet å fungere (SSL)](#sonarr-på-synology-sluttet-å-fungere-ssl)
  - [Ugyldig sertifikat og andre HTTPS- eller SSL-problemer](#ugyldig-sertifikat-og-andre-https-eller-ssl-problemer)
  - [Hvordan stopper jeg nettleseren fra å starte ved oppstart?](#hvordan-stopper-jeg-nettleseren-fra-å-starte-ved-oppstart)
  - [VPNs, Jackett og \*ARRs](#vpns-jackett-og-arrs)
  - [Jeg ser loggmeldinger for serier jeg ikke har/ikke vil ha](#jeg-ser-loggmeldinger-for-serier-jeg-ikke-harikke-vil-ha)
  - [Seeder-torrenter blir ikke slettet automatisk](#seeder-torrenter-blir-ikke-slettet-automatisk)
  - [Hjelp, Macen min sier at Sonarr ikke kan åpnes fordi utvikleren ikke kan verifiseres](#hjelp-macen-min-sier-at-sonarr-ikke-kan-åpnes-fordi-utvikleren-ikke-kan-verifiseres)
  - [Hjelp, Macen min sier at Sonarr.app er skadet og kan ikke åpnes](#hjelp-macen-min-sier-at-sonarrapp-er-skadet-og-kan-ikke-åpnes)
  - [Jeg får en feilmelding: Database disk image is malformed](#jeg-får-en-feilmelding-database-disk-image-is-malformed)
  - [Jeg bruker Sonarr på en Mac og den sluttet plutselig å fungere. Hva skjedde?](#jeg-bruker-sonarr-på-en-mac-og-den-sluttet-plutselig-å-fungere-hva-skjedde)
  - [Hvorfor kan ikke Sonarr se filene mine på en ekstern server?](#hvorfor-kan-ikke-sonarr-se-filene-mine-på-en-ekstern-server)
    - [Sonarr kjører som standard under LocalService-kontoen, som ikke har tilgang til beskyttede eksterne filområder](#sonarr-kjører-som-standard-under-localservice-kontoen-som-ikke-har-tilgang-til-beskyttede-eksterne-filområder)
    - [Du bruker et kartet nettverksstasjon (ikke en UNC-sti)](#du-bruker-et-kartet-nettverksstasjon-ikke-en-unc-sti)
  - [Kartede nettverksstasjoner vs. UNC-stier](#kartede-nettverksstasjoner-vs-unc-stier)
  - [Sonarr fungerer ikke på Big Sur](#sonarr-fungerer-ikke-på-big-sur)
  - [Mitt egendefinerte skript sluttet å fungere etter oppgradering fra v2](#mitt-egendefinerte-skript-sluttet-å-fungere-etter-oppgradering-fra-v2)
- [Vanlige problemer med søk og nedlasting i Sonarr](#vanlige-problemer-med-søk-og-nedlasting-i-sonarr)
  - [Spørringen var vellykket - ingen resultater returnert](#spørringen-var-vellykket-ingen-resultater-returnert)
  - [Hvorfor hentet ikke Sonarr en episode jeg forventet?](#hvorfor-hentet-ikke-sonarr-en-episode-jeg-forventet)
  - [Fant samsvarende serie via nedlastingshistorikk, men utgivelsen ble matchet til serien etter ID. Automatisk import er ikke mulig](#fant-samsvarende-serie-via-nedlastingshistorikk-men-utgivelsen-ble-matchet-til-serien-etter-id-automatisk-import-er-ikke-mulig)
  - [Hvorfor importerer ikke Sonarr en TBA-episode?](#hvorfor-importerer-ikke-sonarr-en-tba-episode)
  - [Sonarr sier ukjent serie ved søk eller import](#sonarr-sier-ukjent-serie-ved-søk-eller-import)
  - [Jacketts /all-endepunkt](#jacketts-all-endepunkt)
    - [Løsninger for Jackett /All](#løsninger-for-jackett-all)
  - [Jackett viser flere resultater enn Sonarr ved manuell søk](#jackett-viser-flere-resultater-enn-sonarr-ved-manuell-søk)
  - [Finn informasjonskapsler](#finn-informasjonskapsler)
  - [Pakk ut torrents](#pakk-ut-torrents)
  - [Tillatelser](#tillatelser)
-->
# Sonarr Basics

## Hvordan finner Sonarr episoder?

- Sonarr søker *ikke* regelmessig etter episodfiler som mangler eller ikke har oppnådd kvalitetsmålene. I stedet spør den ganske ofte indekserne og sporingssystemene dine om *alle* de nylig publiserte episodene/nylig opplastede utgivelsene, og sammenligner deretter dette med listen over episoder som mangler eller trenger oppgradering. Eventuelle samsvarende utgivelser lastes ned. Dette gjør at Sonarr kan dekke en bibliotek av *hvilken som helst størrelse* med bare 24-100 spørringer per dag (RSS-intervall på 15-60 minutter). Hvis du forstår dette, vil du innse at det bare dekker *fremtiden*.
- Hvordan håndterer du nåtiden og fortiden? Når du legger til en serie, må du angi riktig sti, profil og overvåkingsstatus, og deretter bruke avmerkingsboksen Start søk etter manglende. Hvis serien ikke har hatt noen episoder og ikke har blitt utgitt ennå, trenger du ikke å starte et søk.
- Med andre ord, Sonarr finner bare utgivelser som nylig er lastet opp til indekserne dine. Den prøver ikke aktivt å finne utgivelser som ble lastet opp i fortiden.
- Hvis du allerede har lagt til serien, men nå vil søke etter den, har du noen valg. Du kan gå til seriens side og bruke søkeknappen, som vil utføre et søk og deretter automatisk velge episode(r). Du kan søke etter individuelle episoder eller sesonger automatisk eller manuelt. Eller du kan gå til [Ønsket](/sonarr/wanted)-fanen og søke derfra.
- Hvis Sonarr har vært frakoblet i lang tid, vil Sonarr forsøke å bla tilbake for å finne den siste utgivelsen den behandlet, for å unngå å gå glipp av en utgivelse. Så lenge indekseren din støtter blading og det ikke har gått for lang tid, vil Sonarr kunne behandle utgivelsene den ville ha gått glipp av, og du slipper å søke etter de manglende episodene.

### Tilfeller der automatisk søk forekommer

Automatisk søk (via indekserens API) utføres bare i følgende situasjoner. Merk at de samme reglene som normalt gjelder: serien + episoden må være overvåket, og episoder uten sendetidspunkt blir hoppet over.

- Utløst automatisk eller manuelt søk
  - Bruker- eller API-utløst søk. Vanligvis utført ved å klikke på knappene for automatisk eller manuelt søk på en bestemt episode, sesong eller serie.
- Legge til en serie ved hjelp av knappen Legg til og søk
- Bruke Ønsket => Mangler eller Ønsket => Avkortet uoppfylt for å gjøre ett eller flere søk
- Nylig sendte episoder lagt til etter sending
  - Hvis en ny episode blir lagt til i Sonarr som ble sendt de siste 14 dagene eller innen 1 dag i fremtiden (for å dekke de episodene som kan bli utgitt litt tidlig), vil Sonarr **søke** etter disse episodene etter at seriemappen er skannet på nytt (for å fange opp ting som er importert utenfor Sonarr)

## Hvordan sammenlignes mulige nedlastinger?

> Generelt sett er kvalitet viktigst. Hvis du ikke ønsker at kvalitet skal være hovedprioritet, kan du slå sammen kvalitetene dine. [Se TRaSHs guide](https://trash-guides.info/merge-quality)
{.is-info}

- Den nåværende logikken [kan alltid finnes her](https://github.com/Sonarr/Sonarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs#L31-L40s).

- Fra og med 2022-01-23 er logikken som følger:

1. Kvalitet
1. Språk
1. Foretrukket ordpoengsum\*
1. Protokoll (som konfigurert i den relevante forsinkelsesprofilen)
1. Antall episoder\*
1. Episodenummer
1. Indekserprioritet
1. Seeder/jevnaldrende (hvis torrent)
1. Alder (hvis Usenet)
1. Størrelse

> REPACKS og PROPERs er v2 av kvaliteter og rangerer derfor over en ikke-repack av samme kvalitet. [Sett Media Management => File Management `Last ned Proper & Repacks` til "Do Not Prefer"](/sonarr/settings#file-management) og bruk et foretrukket ord regex av `/\b(repack|proper)\b/i` med en positiv poengsum som foreslått av [TRaSHs guider](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#p2p-groups-repackproper)
{.is-warning}

> \* Foretrukne ord oppgraderer alltid en utgivelse, selv om kvalitets- og/eller språkgrensen er oppnådd. Dette gjelder også hvis profilen har deaktivert oppgraderinger.
> \* Foretrukne ord overstyrer standard sesongpakkepreferanse. Dette er [Sonarr Github Issue #3562](https://github.com/Sonarr/Sonarr/issues/3562). Hvis du vil foretrekke sesongpakker når du bruker foretrukne ord, må du [legge til en sesongpakkepreferanse også](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs)
{.is-info}

## Vanlige spørsmål om foretrukne ord

- For poengsummen til filen på disken: Det eksisterende navnet på filen og "originalt scenenavn" for utgivelsen blir vurdert for foretrukne ord. Den høyeste poengsummen av de to blir tatt.

- Hvordan inkluderes foretrukne ord i navngivningen?

  - For Sonarr kan du bruke `{Preferred Words}`-variabelen i navngivningsskjemaet ditt og også aktivere `Inkluder foretrukne ved navngivning` i utgivelsesprofilen. Se [TRaSHs anbefalte navngivningsskjema](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/) for eksempler på anbefalte navngivningsskjemaer for Sonarr. Bruk av variablene i navngivningsskjemaet ditt kan hjelpe med nedlastingsløkkeproblemer.

- Fra og med v3.0.7 kan du nå også inkludere foretrukne ord på en utgivelsesprofilbasis `{Preferred Words:<Utgivelsesprofilnavn>}`

- Foretrukne ord oppgraderer alltid en utgivelse, selv om kvalitets- og/eller språkgrensen er oppnådd. Dette gjelder også hvis profilen har deaktivert oppgraderinger.

> Foretrukne ord overstyrer standard sesongpakkepreferanse. Dette er [Sonarr Github Issue #3562](https://github.com/Sonarr/Sonarr/issues/3562). Hvis du vil foretrekke sesongpakker når du bruker foretrukne ord, må du [legge til en sesongpakkepreferanse også](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs)
{.is-info}

- Merker kan brukes til å kontrollere hvilke serier en utgivelsesprofil gjelder for; se innstillingene for utgivelsesprofiler for mer informasjon

- For ytterligere informasjon om foretrukne ord og utgivelsesprofiler, [se innstillingssiden](/sonarr/settings#release-profiles)

## Hvordan bytter jeg fra Windows-tjenesten til en brettapp?

1. Slå av Sonarr
1. Kjør serviceuninstall.exe som ligger i Sonarr-mappen
1. Kjør Sonarr.exe som administrator én gang for å gi den riktige tillatelser og åpne brannmuren. Når det er fullført, kan du lukke det og kjøre det normalt.
1. (Valgfritt) Legg til en snarvei til Sonarr.exe i oppstartsmappen for å starte automatisk ved oppstart.

## Hvordan sikkerhetskopierer/gjenoppretter jeg Sonarr?

### Sikkerhetskopiering av Sonarr

#### Bruke innebygd sikkerhetskopiering

- Gå til System => Backup i Sonarr-grensesnittet
- Klikk på Sikkerhetskopier-knappen
- Last ned zip-filen etter at sikkerhetskopieringen er opprettet for å lagre den på et trygt sted

#### Bruke filsystemet direkte

- Finn plasseringen til AppData-mappen for Sonarr
  - Gå til System => Om i Sonarr-grensesnittet
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Stopp Sonarr - Dette forhindrer at databasen blir ødelagt
- Kopier innholdet til et trygt sted

### Gjenoppretting fra sikkerhetskopiering

> Gjenoppretting til et operativsystem som bruker forskjellige stier vil ikke fungere (Windows til Linux, Linux til Windows, Windows til OS X eller OS X til Windows). Flytting mellom OS X og Linux kan fungere, siden begge bruker stier som inneholder `/` i stedet for `\` som Windows bruker, men det støttes ikke. Du må manuelt redigere alle stier i databasen eller bruke [Toolbarr](https://github.com/Notifiarr/toolbarr).
{.is-warning}

#### Bruke zip-sikkerhetskopiering

- Installer Sonarr på nytt (hvis aktuelt / ikke allerede installert)
- Kjør Sonarr
- Gå til System => Backup
- Velg Gjenopprett sikkerhetskopi
- Velg Velg fil
- Velg sikkerhetskopien din som zip-fil
- Velg Gjenopprett

#### Bruke filsystem-sikkerhetskopiering

- Installer Sonarr på nytt (hvis aktuelt / ikke allerede installert)
- Finn plasseringen til AppData-mappen for Sonarr
  - Kjør Sonarr én gang og gå til System => Om i grensesnittet
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Stopp Sonarr
- Slett innholdet i AppData-mappen **(inkludert .db-wal/.db-journal-filene hvis de eksisterer)**
- Gjenopprett fra sikkerhetskopien din
- Start Sonarr
- Så lenge stiene er de samme, vil alt fortsette der det slapp

#### Gjenoppretting av filsystem på Synology NAS

> ADVARSEL: Gjenoppretting på en Synology krever kunnskap om Linux og rot-SSH-tilgang til Synology-enheten.
{.is-warning}

- Installer Sonarr på nytt (hvis aktuelt / ikke allerede installert)
- Finn plasseringen til AppData-mappen for Sonarr
  - Kjør Sonarr én gang og gå til System => Om i grensesnittet
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Stopp Sonarr
- Koble til Synology NAS via SSH og logg inn som root

> På noen installasjoner er brukeren annerledes enn i kommandoene nedenfor: `chown -R sc-Sonarr:Sonarr *` {.is-info}

- Utfør følgende kommandoer:

```shell
rm -r /usr/local/Sonarr/var/.config/Sonarr/Sonarr.db
cp -f /tmp/Sonarr_backup/* /usr/local/Sonarr/var/.config/Sonarr/
```

- Oppdater tillatelser på filene:

 ```shell
cd /usr/local/Sonarr/var/.config/Sonarr/
chown -R Sonarr:users *
chmod -R 0644 *
```

- Start Sonarr

## Hjelp, jeg har låst meg ute

{#help-i-have-forgotten-my-password}

> Hvis du bruker v4 av Sonarr, er ikke `AuthenticationMethod`-typen `None` lenger gyldig - se denne [FAQ-en](/sonarr/faq-v4) {.is-info}

Hvis du vil deaktivere autentisering (for å tilbakestille brukernavnet eller passordet du har glemt), må du redigere `config.xml` som vil være inne i [Sonarr Appdata Directory](/sonarr/appdata-directory)

1. Åpne config.xml i en tekstredigerer
1. Finn linjen for autentiseringsmetode som vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Endre linjen for `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Sonarr på nytt
1. Sonarr vil nå være tilgjengelig uten passord. Du bør gå til `Innstillinger: Generelt` i grensesnittet og angi brukernavnet og passordet ditt

## Hvorfor er det to filer? \| Hvorfor er det en fil igjen i nedlastinger?

Dette er forventet. Med en konfigurasjon som støtter [hardlinker](https://trash-guides.info/hardlinks), vil ikke dobbelt plass bli brukt. Her er hvordan torrentprosessen fungerer:

1. Sonarr sender en nedlastingsforespørsel til klienten din og tilordner den etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten. Eksempler: filmer, tv, serier, musikk, osv.
1. Sonarr overvåker de aktive nedlastingene dine i nedlastingsklienten som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
1. Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra selve klienten under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil de enten bli hardlinket hvis støttet av konfigurasjonen din, eller kopiert hvis hardlinker ikke støttes.
1. Hvis alternativet "Fullført nedlastingshåndtering - Fjern fullførte" er aktivert i Sonarr-innstillingene, vil Sonarr slette den opprinnelige filen og torrenten fra nedlastingsklienten din, men bare hvis nedlastingsklienten rapporterer at seeding er fullført og torrenten er stoppet (dvs. satt på pause). Se [TRaSH's veiledninger for nedlastingsklienter](https://trash-guides.info/Downloaders/) for hvordan du konfigurerer nedlastingsklienten optimalt.

> Hardlinker er aktivert som standard. [En hardlink bruker ikke noe ekstra diskplass](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/). Filsystemet og monteringspunktene må være de samme for mappen der de fullførte nedlastingene dine er og mediebiblioteket ditt. Hvis opprettelsen av hardlinken mislykkes eller konfigurasjonen din ikke støtter hardlinker, vil den falle tilbake og kopiere filen.{.is-info}

## Jeg ser at funksjonen/feilen X er fikset, hvorfor kan jeg ikke se den?

Sonarr består av to hovedkoder, `main` og `develop`.

- `main` blir utgitt periodisk når `develop`-grenen er stabil
- `develop` er for pre-release-testing og personer som er villige til å være på forkanten. Når en funksjon er merket som i `develop`, vil den bare være tilgjengelig for brukere som kjører `develop`-grenen, når den er flyttet til live (i `main`), er den offisielt utgitt.

## Episodestatus - Hvordan beregnes den?

- Det er to deler av episodetellingen, en er antall episoder (Episode Count) og den andre er antall episoder med filer (Episode File Count), hver bruker litt forskjellig logikk for å gi deg den generelle fremgangen for en serie eller sesong.

  - Episode Count => Episoden har allerede blitt sendt OG er overvåket ELLER - Episoden har en fil
  - Episode File Count => Episoden har en fil

- Hvis en serie har 10 episoder som allerede har blitt sendt, og du ikke har noen filer for dem, vil du ha 0/10 episoder. Hvis du ikke overvåker noen av episodene i den serien, vil du ha 0/0, og hvis du får alle episodene for den serien, uavhengig av om episodene er overvåket eller ikke, vil du ha 10/10 episoder.

## Hvordan får jeg tilgang til Sonarr fra en annen datamaskin?

- Som standard lytter ikke Sonarr til forespørsler fra alle systemer (når det ikke kjøres som administrator), det vil bare lytte på localhost. Dette skyldes hvordan webserveren Sonarr bruker integreres med Windows (dette gjelder også for nåværende alternativer). Hvis Sonarr kjøres som administrator, vil det registrere seg riktig med Windows og åpne brannmurens port slik at det kan nås fra andre systemer i nettverket ditt. Kjøring som administrator trenger bare å gjøres én gang (hvis du endrer porten, må den kjøres på nytt).

## Hvorfor oppdaterer Sonarr serieninformasjon så ofte?

- Sonarr oppdaterer serier og episodinformasjon i tillegg til å skanne disken for filer hver 12. time. Dette kan virke aggressivt, men det er en veldig viktig prosess. Dataoppdateringen fra vår TVDb-proxy er viktig fordi ny episodinformasjon synkroniseres ned, sendetidspunkter, antall episoder, status (fortsetter/avsluttet). Selv show som ikke sendes, blir oppdatert med ny informasjon.
- Diskskanningen er mindre viktig, men brukes til å sjekke etter nye filer som ikke ble sortert av Sonarr og for å oppdage slettede filer.
- Den mest tidkrevende delen er informasjonsoppdateringen (forutsatt at disktilgangshastigheten er rimelig), større show tar lengre tid på grunn av antall episoder som skal behandles.

> Det er ikke mulig å deaktivere denne oppgaven. Hvis denne oppgaven kjører lenge nok til at du føler at den er et problem, er det noe annet som skjer som må løses i stedet for å stoppe denne oppgaven.
{.is-warning}

## Hvorfor er det et tall ved siden av Aktivitet?

- Dette tallet viser antallet episoder i køen til nedlastingsklienten din og de siste 60 elementene i historikken som ennå ikke er importert. Hvis tallet er blått, fungerer det normalt og bør importere episoder når de er ferdige. Gult betyr at det er en advarsel for en av episodene. Rødt betyr at det har oppstått en feil. I tilfelle gult (advarsel) og rødt (feil), må du se på køen under Aktivitet for å se hva problemet er (hold musepekeren over ikonet for å få mer informasjon).
- Du må fjerne elementet fra nedlastingsklientens kø eller historikk for å fjerne dem fra Sonarrs kø.

## Hva er forskjellige serietyper?

- Serietype påvirker hvordan Sonarr søker etter serier. En serietype er basert på hvordan serien blir utgitt på indekseringsnettstedene og er ikke nødvendigvis den sanne 'typen' til serien.
- De fleste show skal være `Standard`. For daglige show som vanligvis blir utgitt med en dato, bør `Daily` brukes. Til slutt er det anime, der bruk av `Anime` er *vanligvis* riktig, men noen ganger kan `Standard` fungere bedre, så prøv den *andre* hvis du har problemer.
- Vær oppmerksom på at hvis serietypen er satt til anime og ingen av de aktiverte indekseringsnettstedene har noen anime-kategorier konfigurert, vil det effektivt hoppe over indekseringsnettstedet og det kan virke som om det ikke søker.
- Vær oppmerksom på at Anime-typen ikke har noen konsept om sesongpakker eller sesonger, og hver episode blir søkt individuelt.
- Vær oppmerksom på at ikke alle indekseringsnettsteder støtter sesong/episodesøk (standard).
- Serietyper kan endres fra Masseredigerer eller fra `Rediger` når du ser på en serie. Merk at serietypen kan velges ved import.

- Hvis **Anime**-serietypen brukes, er det [mulig å også søke på indekseringsnettstedet med standardtypen.](/sonarr/settings#indexers)

### Serietyper

- **Anime** - Episoder utgitt med absolutt episodenummer
- **Daily** - Episoder utgitt daglig eller sjeldnere som bruker år-måned-dag (2017-05-25)
- **Standard** - Episoder utgitt med SxxEyy-mønster

### Eksempler på serietyper

Nedenfor er noen eksempler på utgivelsesnavn for hver serietype. Den spesifikke forskjellen er merket med fet skrift.

> Hvis **Anime**-serietypen brukes, er det [mulig å også søke på indekseringsnettstedet med standardtypen.](/sonarr/settings#indexers)
{.is-info}

#### Daily

Loggene vil vise `Søker indekseringsnettsteder for [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Loggene vil vise `Søker indekseringsnettsteder for [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Loggene vil vise `Søker indekseringsnettsteder for [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

## Hvordan kan jeg endre navn på seriemappene mine?

{#rename-folders}

> Samme prosess gjelder også for å flytte/endre seriestier{.is-info}

Hvis du har justert formatet for serienavnet ditt etter at Sonarr allerede har opprettet noen seriemapper, vil ikke Sonarr automatisk endre navn på eksisterende mapper. For å utløse en endring av disse mappene, bør følgende trinn følges:

1. Serier
1. Masseredigerer
1. Velg hvilke serier som trenger at mappen deres blir omdøpt
1. Endre rotmappen til samme rotmappe som serien allerede eksisterer i
1. Velg "Ja, flytt filer" for å få

> Hvis du bruker Plex eller Emby, vil dette utløse ny gjenkjenning av intros, miniatyrbilder, kapitler og forhåndsvisningsmetadata.
{.is-warning}

## Hvordan oppdaterer jeg Sonarr?

- Gå til Innstillinger og deretter fanen Generelt og vis avanserte innstillinger (bruk vippebryteren ved siden av lagre-knappen).

1. Under Oppdateringer-seksjonen endrer du grennavnet til `main` eller `develop`
1. Lagre

*Dette vil ikke installere bitene fra den grenen umiddelbart, det vil skje under neste oppdatering.*

- main - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Standard/Stabil): Dette er testet av brukere på nattlig (`develop`) gren og det er ikke kjent for å ha noen større problemer. Denne grenen bør brukes av flertallet av brukerne. På GitHub er dette `main`-grenen.
- develop - ![Current Develop/Nightly](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alfa/Ustabil): Dette er nå det samme som main for ikke-Docker-brukere og sannsynligvis den siste v3-utgivelsen.

> ~~**Advarsel: Du kan kanskje ikke gå tilbake til `main` etter å ha byttet til denne grenen.** På GitHub er dette `develop`-grenen.~~
{.is-danger}

- v4 develop - ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alfa/Ustabil): **For ikke-Docker-brukere er grenen `develop` når v4 er installert. For Docker-brukere er dette sannsynligvis `develop`-taggen** Dette er det nyeste for Sonarr v4 Beta. Det utgis så snart koden er bekreftet og bestått alle automatiserte tester. Denne bygningen er kanskje ikke brukt av oss eller andre brukere ennå. Det er ingen garanti for at den vil kjøre i noen tilfeller. Denne grenen anbefales bare for avanserte brukere. Problemer og egen feilsøking forventes i denne grenen. På GitHub er dette `develop`-grenen.

> **Advarsel: Du kan ikke gå tilbake til (v3) `main` eller (v3) `develop` etter å ha byttet til v4-grenen uten å reinstallere og finne en v3-sikkerhetskopi.** På GitHub er dette `develop`-grenen.
{.is-danger}

> v3 **ikke-Docker**-installasjoner **kan ikke** oppgraderes direkte til v4 og krever installasjon av Sonarr v4
{.is-info}

- Merk: Hvis installasjonen din er via Docker, legg til `:release`, `:latest`, `:nightly` eller `:develop` på slutten av kontainermerket, avhengig av hvem som lager byggene dine.

|                                                                    | `main` (stabil) ![Current Main/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v3) (beta) ![Current v3 Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v4) (v4 beta) ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) |
|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [hotio](https://hotio.dev/containers/sonarr)                       | `release`                                                                                                                                                                                             | `nightly`                                                                                                                                                                                                   | `v4`                                                                                                                                                                                                            |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-sonarr) | `latest`                                                                                                                                                                                              | `3.0.10`                                                                                                                                                                                                     | `develop`                                                                                                                                                                                                       |

### Installere en nyere versjon

#### Lokal

1. Gå til System og deretter til fanen Oppdateringer
1. Nyere versjoner som ikke er installert ennå, vil ha en oppdateringsknapp ved siden av dem. Klikk på denne knappen for å installere oppdateringen.

> v3 kan ikke oppdateres til beta v4 og må installeres manuelt. Se [v4 Beta-annonsering](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)
{.is-info}

#### Docker

1. Last ned taggen på nytt og oppdater beholderen din

## Kan jeg bytte fra `develop` tilbake til `main`?

- Se oppføringen nedenfor

## Kan jeg bytte mellom grener?

> Du kan (nesten) alltid øke risikoen.{.is-info}

- `main` kan bytte til `develop`
- Se nedenfor eller sjekk med utviklingsteamet for å se om du kan bytte fra `develop` til `main` for den gitte byggingen din.
- Hvis du ikke følger disse instruksjonene, kan Sonarr bli ubrukelig eller kaste feil. Du er advart. Hvis følgende feilmeldinger oppstår, bruker du en nyere database med en eldre \*Arr-versjon som ikke støttes. Oppgrader \*Arr til versjonen du tidligere var på eller nyere.
  - Eksempel på feilmeldinger:
    - `Feil ved analyse av kolonne 45 (Language=31 - Int64)`
    - `DataMapper kunne ikke laste inn følgende felt: 'Languages' verdi`
    - `ID samsvarer ikke med et kjent språk Parameter name: id`
    - Andre lignende databasefeil om manglende kolonner eller tabeller.
- **Oppdatering 7. august 2022**
  - `3.0.9.1549` er utgitt som hoved/stabil
  - For de som er på develop og fortsatt er på `3.0.9.1549` eller lavere, kan du trygt nedgradere til main
  - Hvis du er på en nyere versjon, *kan du bli sittende fast* på nightly/develop til en ny stabil utgivelse er klar. Hvis du har en sikkerhetskopi fra før du oppgraderte forbi versjonen nevnt ovenfor, kan du reinstallere og gjenopprette sikkerhetskopien. Sjekk med utviklingsteamet for å se om du kan nedgradere på en trygg måte.

# Sonarr og problemer med serier + metadata

## Hvordan håndterer Sonarr nummereringsproblemer med scener (American Dad!, osv)?

### Hvordan Sonarr håndterer nummereringsproblemer med scener

- Sonarr er avhengig av [TheXEM](http://thexem.info/), et samfunnsdrevet nettsted som lar brukere opprette kartlegginger av serier mellom scener (de som legger ut filene) og TheTVDb (som vanligvis følger nettverkets nummerering). Det er allerede en rekke serier der, men det er enkelt å legge til en ny serie, og endringene blir vanligvis akseptert innen et par dager (hvis de er korrekte). TheXEM brukes til å korrigere forskjeller i episodenummerering (uoverensstemmelse om en episode er en spesialepisode eller ikke) samt forskjeller i sesongnummerering, for eksempel at episoder blir utgitt som S10E01, men TheTVDb lister den samme episoden som S2017E01.
- XEM fikser vanligvis problemene når nummereringen til utgivelsesgruppene (populært kjent som 'scenen') ikke samsvarer med TVDb-nummereringen, slik at Sonarr ikke fungerer. Her kommer [XEM](http://thexem.info) inn i bildet, som oppretter et kart for Sonarr å se på.
- Utgivelsesgrupper dobbeltepisoder i en enkelt fil, siden det er slik de sendes, men TVDb merker hver episode individuelt.
- Utgivelsesgrupper bruker et år for sesongen S2010, og TVDb bruker S01.
- [XEM](http://thexem.info) fungerer i de fleste tilfeller og holder alt i gang uten at du merker det. Men som med de fleste ting, vil det alltid være noen *problematiske unntak*, og i dette tilfellet er det en liste over dem.

> Visse indekseringsverktøy eller utgivelsesgrupper kan følge TVDb i stedet for `Scene` (dvs. XEM).
> Hvis dette observeres, kan du sende dem inn via skjemamappingen for scenen.
{.is-info}

- [Tjenester som er etterspurt kartlegging *Gjennomgå og forsikre deg om at aliaset og utgivelsen ikke allerede er forespurt eller lagt til*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Skjemamapping for scenen *Lag en ny forespørsel for et alias. Forsikre deg om at skjemaet er fylt ut fullstendig*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

### Problematiske serier

> Dette er på ingen måte en fullstendig liste over serier som har kjente problemer med scenemapping; men dette er noen vanlige.

- Dette er en ufullstendig liste over kjente serier og hvordan/hvorfor de er problematiske:
- American Dad {#problemshow-americandad}
  - På grunn av endringer i sesongene på nettverket, er American Dad vanligvis en sesong unna mellom utgivelser og TVDb. Se XEM-kartet for detaljer
  - [American Dad](https://thexem.info/xem/show/4948) er for øyeblikket på S19 basert på TVDb eller S18 basert på Scene på tidspunktet for denne skrivingen. Så å søke i Sonarr etter sesong 19 vil **bare** gi resultater for sesong 18 på grunn av XEM-kartet.
  - Hvis du har en indekseringsverktøy / utgivelsesgrupper med episoder fra sesong 19, kan du sende dem inn via skjemamappingen for scenen og forsikre deg om at de ikke allerede er forespurt
    - [Tjenester som er etterspurt kartlegging *Gjennomgå og forsikre deg om at aliaset og utgivelsen ikke allerede er forespurt eller lagt til*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Skjemamapping for scenen *Lag en ny forespørsel for et alias. Forsikre deg om at skjemaet er fylt ut fullstendig*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- Paw Patrol {#problemshow-pawpatrol}
  - Dobbeltepisodefiler vs. enkeltepisodefiler på TVDb, men ikke alle episoder er dobbelt, så kartet kan bli feil og peke på hvilke som er enkelt og hvilke som er dobbelt
- Pokémon {#problemshow-pokemon}
  - På TheXem sporer [Pokemon](http://thexem.info/xem/show/4638) *dubbet* episoder. Så hvis du vil ha tekstede episoder, kan du være uheldig. Hvis visse utgivelsesgrupper følger TVDb og ikke XEM-kartleggingen, kan du sende dem inn via skjemamappingen for scenen og forsikre deg om at de ikke allerede er forespurt
    - [Tjenester som er etterspurt kartlegging *Gjennomgå og forsikre deg om at aliaset og utgivelsen ikke allerede er forespurt eller lagt til*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Skjemamapping for scenen *Lag en ny forespørsel for et alias. Forsikre deg om at skjemaet er fylt ut fullstendig*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- La Casa de Papel / Money Heist  {#problemshow-moneyheist}
  - TVDb har den opprinnelige sendeordenen fra det spanske nettverket, men Netflix kjøpte rettighetene og klippet om serien til en annen antall episoder. Dette fører til at "sesong 5" blir importert over eksisterende "sesong 3"-episoder. [Mer informasjon finner du i denne Reddit-tråden](https://old.reddit.com/r/sonarr/comments/pdrr6l/money_heist_mess/)
- Kamen Rider {#problemshow-kamenrider}
  - Antologien ([TVDb ID 74096](https://thetvdb.com/series/kamen-rider)) skal brukes i Sonarr for automatisering, siden denne serien har både en antologioppføring (som samler alle sesongene) og de individuelle sesongene som er oppført som separate oppføringer på TVDb. På grunn av at antologien har individuelle sesongnavnmappinger på [TheXEM](https://thexem.info/xem/show/5376), er det ikke mulig å legge til de individuelle sesongoppføringene i Sonarr uten å laste ned og importere utgivelser manuelt.
- Bleach: Thousand-Year Blood War {#problemshow-bleach}
  - Den nyeste sesongen av Bleach: Thousand-Year Blood War blir utgitt med forskjellige navneskjemaer, noe som gjør det vanskelig å automatisere og potensielt overskrive noen av de eksisterende episodene dine. Den kan bare automatiseres hvis utgivelsesgruppen din enten:
    - Utgir episodene som S17Exx-nummerering, eller
    - Utgir dem med riktig serietittel for sesong 2 (funnet her <https://thexem.info/xem/show/5476>) og har begynt denne nye bue ved absolutt episodenummer 1.
- Great Asian Railway Journeys {#problemshow-greatasianrail}
  - Great Asian Railway Journeys ble først sendt som 20 mindre episoder, men ble senere sendt på nytt som 10 lange episoder. Disse lengre kombinerte episodene ble lagt til som spesialepisoder og bør navngis deretter. (S00E01, osv., ...)
- Horizon {#problemshow-horizon}
  - En serie som sporadisk sender episoder siden 1964. Dette gjør kartleggingen spesielt vanskelig, som du kan se på [TheXEM](https://thexem.info/xem/show/5495). De interesserte kan finne den opprinnelige diskusjonen på Sonarr Discord [her](https://discord.com/channels/383686866005917708/649018968559845376/1046898050909622312).
- Kaleidoscope (2023) {#problemshow-kaleidoscope}
  - Kaleidoscope (2023) ble utgitt på Netflix som en ikke-lineær serie, noe som betyr at hver bruker fikk en annen rekkefølge når de så serien. Dette skaper et problem for Sonarr, ettersom utgivelsesgruppene har forskjellige episoderekkefølger for serien. For å unngå feilaktig kartlegging av episoder vil ikke Sonarr automatisk laste ned episoder, og du må laste ned og importere episodene manuelt. Du kan matche dem basert på episodetittel, eller ved å forhåndsvise de første sekundene og se om episoden 'farge' samsvarer med tittelen.

Noen eksempler på andre programmer som ofte har problemer, hvor de fleste kan løses ved hjelp av TheXEM-mapping, er: Arrested Development, Kitchen Nightmares (US), Mythbusters, Pawn Stars.

## Hvorfor kan ikke Sonarr importere episodfiler for serie X? / Hvorfor kan ikke Sonarr finne utgivelser for serie X?

Det kan være flere grunner til at Sonarr ikke kan finne eller importere episoder for en bestemt serie.

> Sonarr bruker ikke aliaser eller oversettelser (dvs. utenlandske tittler) fra TVDb.
{.is-warning}

> **For indekser som støtter søk basert på ID**, brukes TVDbID eller IMDbID for å søke. Serietitler og eventuelle aliaser brukes bare hvis søk basert på ID ikke gir resultater.
{.is-info}

- Sonarr er avhengig av å kunne matche titler, ofte bruker opplasterne forskjellige titler for episoder, f.eks. blir `CSI: Crime Scene Investigation` postet som bare `CSI`, slik at Sonarr ikke kan matche navnene uten litt hjelp. Dette håndteres av Scene Mapping som Sonarr-teamet vedlikeholder.
- Du kan også se gjennom [FAQ-inngangen for problematiske programmer og nummerering av utgivelsesgrupper vs. TVDb](#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)

> **For all japansk anime må aliaser legges til [thexem.info](https://thexem.info)**, for andre serier for å be om en ny kartlegging, se trinnene nedenfor. Mer informasjon finnes hos noen av XEM-folkene som henger i #XEM discord-kanalen på Sonarr Discord.
{.is-danger}

- [Tjenester som er etterspurt kartlegging *Gjennomgå og forsikre deg om at aliaset og utgivelsen ikke allerede er forespurt eller lagt til*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Tjenester Scene Mapping Request Form *Lag en ny forespørsel om et alias. Sørg for at skjemaet er fylt ut fullstendig*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

> Typisk blir tjenesteforespørsler lagt til innen 1-5 dager
{.is-info}

> Be ikke om en kartlegging for japansk anime; bruk XEM for det.
> Mer informasjon finnes hos noen av XEM-folkene som henger i [\#XEM discord-kanalen på Sonarr Discord](https://discord.gg/Z3D6u5hBJb)
{.is-danger}

> Hvis en ikke-japansk serie krever sesongkartlegging (f.eks. utgitt som S25E26, men TVDB er S26E2, så vil det være nødvendig med en XEM-kartlegging. Dette kan ikke gjøres med tjenestekartlegging.
{.is-info}

> Serien "Helt Perfekt" med TVDb-ID-ene `343189` og `252077` er vanskelig å automatisere på grunn av at TVDb har samme navn for begge showene, noe som bryter med TVDb sine egne regler. Den første oppføringen for serien får navnet. Eventuelle fremtidige oppføringer for serien må ha året som en del av serienavnet. Imidlertid er det lagt til et unntak for å kartlegge utgivelser (følsom kartlegging) av Helt Perfekt-utgivelser som inneholder `NORWEGIAN` -\> `252077` og som inneholder `SWEDISH` -\> `343189`
{.is-info}

## TVDb er oppdatert, hvorfor er ikke Sonarr det?

{#tvdb}

- TVDb har en 24-timers hurtigbuffer på API-en sin.
- TVDb sin API må deretter fylles gjennom CDN-hurtigbufferen, noe som tar flere timer.
- Sonarrs Skyhook har en mye mindre hurtigbuffer på noen få timer i tillegg.
- I tillegg kjører Sonarr bare oppgaven "Oppdater serier" hver 12. time. Denne oppgaven kan kjøres manuelt fra System => Oppgaver; "Oppdater alle" fra Serieindeksen, eller manuelt for en bestemt serie på den seriens side.

- Derfor vil det vanligvis ta mellom 36 og 48 timer (24 + ~3 + ~3 + 12) for en endring på TVDb å bli automatisk oppdatert i Sonarr.

- Hvis en serie eller episoder mangler på TVDb, vil det ta 36 til 48 timer fra de blir lagt til for å bli tilgjengelige i Sonarr-instansen din.

{#missing-episodes}

- Hvis du vet at en oppdatering på TVDb ble gjort for mer enn 48 timer siden, kan du diskutere det på [Discord](https://discord.sonarr.tv/).

## Hvorfor kan jeg ikke legge til en serie?

{#why-can-i-not-add-a-new-series}

- Hvis TheTVDb er utilgjengelig, kan ikke Sonarr få søkeresultater, og du vil ikke kunne legge til noen nye serier ved å søke. Du kan kanskje legge til en ny serie ved hjelp av TVDbID hvis du vet hva det er, brukergrensesnittet forklarer hvordan du legger den til ved hjelp av en ID.
- Sonarr kan ikke legge til noen serier som ikke har en engelsk tittel. Hvis du prøver å legge til en serie via TVDb ID som ikke har en engelsk tittel. Hvis det ikke finnes noen engelsk tittel for den serien på TheTVDb, må den legges til, og deretter [må man vente på at TVDb sin hurtigbuffer skal tømmes](#tvdb).
- Showet må være en TV-serie, ikke en film. Det må også eksistere på TVDb. Hvis det er på IMDB, TMDB eller et annet sted, men ikke på TVDb, kan du ikke legge til showet.
- Serien må eksistere på TVDb
- Visse serier kan faktisk betraktes som fortsettelser og sesonger i sin primære serie.
  - Noen kjente serier/sesonger er:
  - [Dexter New Blood var sesong 9](https://thetvdb.com/series/dexter/seasons/official/9), men det er nå [sin egen serie](https://thetvdb.com/series/dexter-new-blood)

## Hvorfor kan jeg ikke legge til en serie når jeg kjenner TVDb-ID-en?

{#why-cant-i-add-a-new-series-when-i-know-the-tvdb-id}

- Sonarr kan ikke legge til noen serier som ikke har en engelsk tittel. Hvis du prøver å legge til en serie via TVDb ID som ikke har en engelsk tittel, vil ikke serien bli funnet. Hvis det ikke finnes noen engelsk tittel for den serien på TheTVDb, må den legges til (hvis tilgjengelig).
- Sjekk URLen / serien - Sonarr støtter ikke filmer; bruk [Radarr](/radarr) for filmer

## Tittel Slug i bruk

- Det er to hovedårsaker til denne feilen som er oppført nedenfor.

## Dupliserte navn uten år

- Denne feilen oppstår ofte når to serier har samme navn på TheTVDB, hvis dette er tilfelle, bør det andre showet ha året lagt til seriens tittel.
  - Serie A
  - Serie A (2021)
- For å rette opp dette, vent på at noen til slutt (kanskje) oppdaterer TVDb eller oppdater TVDb selv. Når det er rettet opp **og når det er godkjent av TVDb sine moderatorer**, på grunn av [TVDb sine API-problemer](#tvdb-is-updated-why-isnt-sonarr), når det er oppdatert, må du vente i 30+ timer før den korrigerte tittelen kan brukes i Sonarr.

## Dupliserte navn med tegnsetting

- Det vil også skje med to lignende navngitte serier som bare kan skille seg med tegnsetting, hvis dette er tilfelle, vennligst rapporter dette på [Sonarr Discord](https://discord.sonarr.tv/).
  - Joe's Show (2022)
  - Joes Show (2022)

## Episoden har ikke et absolutt nummer

- Episodene på TVDb har ikke fått tildelt et absolutt nummer. Oppdater serien på TVDb om nødvendig, og vent deretter 36-48 timer for at oppdateringen skal tømme TVDb sin interne hurtigbuffer og laste inn i Sonarr

## Sendetider for episoder

- Innenfor Sonarr er sendetid og -dato for episoder som vises i nettleseren basert på klientens tid/tidssone, alle tider sendes fra Sonarr til nettleseren som UTC-tider (ISO-8601 formatert for å være nøyaktig)
- TVDb bestemmer - med unntak for strømmetjenester - at sendetiden og -datoen er basert på hovedsendenettverkets lokale tid i landets mest populære by. [Se TVDb sin FAQ-inngang for detaljer](https://support.thetvdb.com/kb/faq.php?id=29)
- Sendetid og -dato for episoder på TVDb konverteres til UTC og bruker Sonarrs tidssone som er kartlagt i Skyhook av Sonarr-teamet for nettverket TVDb har for serien.
  - I sjeldne tilfeller der et nettverk ikke er kartlagt, vil tiden i TVDb antas å være US EST (UTC-5).
  - Hvis sendetiden ikke ser ut til å stemme når man konverterer fra sendetidspunktet i nettverkets lokale tidssone til nettleserens tidssone, er det sannsynlig at nettverket må kartlegges i Skyhook. [Kontakt utviklingsteamet på Discord](https://discord.sonarr.tv/) for hjelp med å oppdatere nettverkets tidssone.  

# Vanlige problemer med Sonarr

## Stien er allerede konfigurert for en eksisterende serie

- Bibliotekimport viser "Eksisterende" eller du får en feilmelding om at "Stien er konfigurert for en eksisterende serie"
- Dette skjer når du prøver å legge til en serie eller redigere stien til en eksisterende serie som allerede er tilordnet en annen serie.
- Dette ble sannsynligvis forårsaket av at du ikke rettet opp en serie som ikke stemte da brukeren importerte biblioteket sitt.
- Finn og rett opp filmen som allerede er tilordnet den seriens sti.
  - Serieindeks
  - Tabellvisning
  - Alternativer => Legg til sti som en kolonne
  - Sorter og finn filmen på den merkede problematiske stien.
- Alternativt kan du slette serien som bruker den eksisterende stien fra Sonarr

## System og logger lastes inn for alltid

- Det er easy-privacy blocklist. De blokkerer i utgangspunktet alle URL-er med /api/log? i seg. Se gjennom listen og vurder om du synes det er en fornuftig idé å blokkere alle URL-ene i den listen, det er dusinvis av URL-er der som potensielt kan ødelegge nettsteder. Du valgte det i annonseblokkereren din. En enkel løsning er å legge domenet Sonarr kjører på i hvitelisten. Men jeg anbefaler fortsatt å sjekke listen.

## Rare UI-problemer

- Hvis du opplever rare UI-problemer som at bibliotekssiden ikke viser noe eller at en bestemt visning eller sortering ikke fungerer, prøv å se det i et Chrome Inkognitovindu eller Firefox Privat vindu. Hvis det fungerer fint der, kan du tømme nettleserens hurtigbuffer og informasjonskapsler for din spesifikke IP/domene. For mer informasjon, se [Tøm hurtigbuffer, informasjonskapsler og lokal lagring](/useful-tools#clearing-cookies-and-local-storage) wiki-artikkelen.

## Webgrensesnitt lastes bare inn på localhost på Windows

- Hvis du bare kan nå webgrensesnittet ditt på <http://localhost:8989/> eller <http://127.0.0.1:8989>, må du kjøre Sonarr som administrator minst én gang.

## Jeg fikk en popup som sa at config.xml var ødelagt, hva nå?

- Sonarr kunne ikke lese konfigurasjonsfilen ved oppstart fordi den ble ødelagt på en eller annen måte. For å få Sonarr tilbake på nett, må du slette `.xml` i [AppData-mappen](/sonarr/appdata-directory), når den er slettet, start Sonarr, og den vil starte på standardporten (8989), du må nå konfigurere eventuelle innstillinger du konfigurerte på siden for generelle innstillinger.

## Ugyldig sertifikat og andre HTTPS- eller SSL-problemer

- Hvis du ikke bruker Windows, er det mest sannsynlig at mono-sertifikatene dine er utdaterte og må synkroniseres. [Se delen om mono ssl i installasjonsartikkelen for detaljer](/sonarr/installation#mono-ssl-issues)
- Nedlastingsklienten din sluttet å fungere, og du får en feilmelding som "Localhost is an invalid certificate"?
  - Sonarr validerer nå SSL-sertifikater. Hvis det ikke er satt opp et SSL-sertifikat i nedlastingsklienten, eller hvis du bruker et selvsignert https-sertifikat uten at CA-sertifikatet er lagt til i den lokale sertifikatbutikken din, vil Sonarr nekte å koble til. Gratis riktig signerte sertifikater er tilgjengelige fra [let's encrypt](https://letsencrypt.org/).
  - Hvis nedlastingsklienten din og Sonarr er på samme maskin, er det ingen grunn til å bruke HTTPS, så den enkleste løsningen er å deaktivere SSL for tilkoblingen. De fleste vil være enige i at det ikke er nødvendig i et lokalt nettverk heller. Det er mulig å deaktivere sertifikatvalidering i avanserte innstillinger hvis du vil beholde en usikker SSL-oppsett.

## Hvordan stopper jeg at nettleseren starter ved oppstart?

Avhengig av operativsystemet ditt, er det flere mulige måter.

- I `Innstillinger` => `Generelt` på noen operativsystemer er det en avmerkingsboks for å starte nettleseren ved oppstart.
- Når du starter Sonarr, kan du legge til `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumentene.
- Stopp Sonarr og rediger config.xml-filen, og endre `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## VPN-er, Jackett og \*ARR-ene

- Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, er torrentklienten din vanligvis det eneste som trenger å være bak en VPN. Fordi VPN-endepunktet deles av mange brukere, kan du oppleve hastighetsbegrensninger, DDOS-beskyttelse og IP-blokkering fra ulike tjenester som hver programvare bruker.
- Med andre ord kan det å sette \*Arr-ene (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bak en VPN gjøre applikasjonene ubrukelige i noen tilfeller på grunn av at tjenestene ikke er tilgjengelige.

> **For å være tydelig, det handler ikke om hvorvidt VPN-er vil forårsake problemer med \*Arr-ene, men når: bildeleverandører vil blokkere deg, og cloudflare er foran de fleste \*Arr-servere (oppdateringer, metadata osv.) og kan også blokkere deg**
{.is-warning}

- **Mange private trackere vil utestenge deg for å bruke eller få tilgang til dem (dvs. bruke Jackett eller Prowlarr) via en VPN.**

### Bruk av en VPN

- Hvis en VPN er nødvendig, og Docker brukes, anbefales det å bruke Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er nødvendig, og Docker ikke brukes, må VPN-klienten din ***støtte delt tunnelering, slik at bare de nødvendige (nedlastingsklient) appene er bak VPN-en.
- Mange problemer med å få tilgang til trackere kan løses ved å bruke Googles eller Cloudflares DNS-servere i stedet for ISP-ens DNS-servere.
- I noen tilfeller (f.eks. britiske internettleverandører) kan du trenge å sette torrentnedlastingsklienten bak en VPN og Jackett/Prowlarr som følger:
  - sett Jackett bak VPN-en og sørg for at delt tunnelering tillater lokal tilgang
  - for Prowlarr konfigurer VPN-klienten din til å gi en proxy og legg til proxyen i Innstillinger => Indekser. Gi proxyen en tagg, og gi alle indekser som trenger å bruke den samme taggen.

## Jeg ser loggmeldinger for show jeg ikke har/ikke vil ha

- Disse meldingene er helt normale og kommer fra RSS-strømmene som Sonarr sjekker for å se om det er episoder du vil ha, vanligvis vises disse bare i debug/trace logging, men i tilfelle det oppstår et problem med å behandle et element, kan du se en advarsel eller feil. Det er trygt å ignorere advarslene/feilene også, siden de gjelder show du ikke vil ha, hvis det er for et show du vil ha, åpne en støttetråd på forumene.

## Seeder-torrenter blir ikke slettet automatisk

- Når en torrent som fortsatt seedes, blir importert, blir den kopiert eller hardlinket (hvis aktivert og *mulig*) slik at torrentklienten kan fortsette å seede. I en ideell oppsett vil torrentnedlastingsmappen og biblioteksmappen være på samme filsystem og *se ut som det* (Docker og nettverksdelinger gjør det enkelt å gjøre feil), noe som gjør hardlinking mulig og minimerer bortkastet plass.
- I tillegg kan du konfigurere målene for seedetid/forhold i Sonarr eller nedlastingsklienten din, konfigurere nedlastingsklienten til å *pause* eller *stoppe* når de er oppfylt, og aktivere Fjern under Fullførte og Mislykkede Nedlastingshåndterer. På den måten vil torrenter som er ferdig med å seede bli fjernet fra nedlastingsklienten av Sonarr.

## Hjelp, Mac-en min sier at Sonarr ikke kan åpnes fordi utvikleren ikke kan verifiseres

- Dette er enkelt, se denne lenken for mer informasjon [her](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
[![Utvikler kan ikke verifiseres](/assets/general/faq_1_mac.png)]

## Hjelp, Mac-en min sier at Sonarr.app er skadet og kan ikke åpnes

- Det skyldes enten en korrupt nedlasting, så prøv igjen, eller [sikkerhetsproblemer, se denne relaterte FAQ-inngangen.](#help-my-mac-says-sonarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Jeg får en feilmelding: Database disk image is malformed

> Du kan motta denne etter å ha oppgradert sqlite3 til 3.41. Sonarr v3.0.9 støtter ikke sqlite3 3.41 på grunn av en breaking default-endring. [Detaljer om problemet finner du i Sonarr GHI #5464](https://github.com/Sonarr/Sonarr/issues/5464)
> Dette er løst med Sonarr v3.0.10, og brukere bør oppgradere Sonarr deretter.
{.is-warning}

- **Feil med `Error creating log database` indikerer problemer med logs.db**
  - Dette kan løses raskt ved å endre navn på eller fjerne databasen. Logs-databasen inneholder uviktig informasjon om kommandohistorikk, oppdateringsinstallasjonshistorikk og Info-, Warn- og Error-oppføringer.
- **Feil med `Error creating main database` eller generisk `database disk image is malformed` uten spesifisert database indikerer problemer med sonarr.db**
  - Fortsett med trinnene nedenfor.
- Dette betyr at SQLite-databasen som lagrer mesteparten av informasjonen for Sonarr er korrupt. Du kan prøve å bruke (en) sikkerhetskopi(er), prøve å gjenopprette den eksisterende databasen, prøve å gjenopprette sikkerhetskopi(en), eller hvis alt annet mislykkes, starte på nytt med en helt ny database.
- Denne feilen kan vises hvis databasefilen ikke kan skrives av bruker/gruppe som \*Arr kjører som. Tillatelser som årsak vil sannsynligvis bare være et problem for nye installasjoner, migrerte installasjoner til en ny server, hvis du nylig har endret tillatelsene for appdata-katalogen din, eller hvis du har endret brukeren og gruppen \*Arr kjører som.
- Ditt beste og første alternativ er å [prøve å gjenopprette fra en sikkerhetskopi](#how-do-i-backuprestore-my-sonarr)
- Du kan også prøve å gjenopprette databasen din. Dette er vanligvis det eneste alternativet når dette problemet oppstår etter en oppdatering. Prøv [sqlite3 `.recover`-kommandoen](/useful-tools#recovering-a-corrupt-db)
  - Hvis sqlite ikke har `.recover` eller du ønsker en mer GUI-vennlig (f.eks. Windows) måte, følg [instruksjonene våre på denne wikien.](/useful-tools#recovering-a-corrupt-db-ui)
- En annen mulig årsak til at du får en feil med databasen din er at du plasserer databasen din på en nettverksstasjon (nfs eller smb eller noe annet som ikke er lokalt). **SQLite er designet for situasjoner der data og applikasjon eksisterer på samme maskin.** Derfor må \*Arr AppData-mappen din (/config montert for docker) VÆRE på lokal lagring. [SQLite og nettverksstasjoner fungerer ikke bra sammen og vil til slutt føre til en feilformet database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruker mergerFS, må du fjerne `direct_io` siden SQLite bruker mmap som ikke støttes av `direct_io`, som forklart i mergerFS [dokumentasjonen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jeg bruker Sonarr på en Mac, og den sluttet plutselig å fungere. Hva skjedde?

- Dette skyldes mest sannsynlig en MacOS-feil som førte til at en av Sonarr-databasene ble korrupt.
- [Følg disse trinnene for å løse problemet](#i-am-getting-an-error-database-disk-image-is-malformed)
- Prøv deretter å starte Sonarr og se om det fungerer. Hvis det ikke fungerer, trenger du ytterligere støtte. Legg ut på [reddit](http://reddit.com/r/Sonarr) eller bli med på [discord](https://discord.sonarr.tv/) for hjelp.

## Hvorfor kan ikke Sonarr se filene mine på en ekstern server?

- For alle operativsystemer må du sørge for at bruker/gruppe som \*Arr kjører som, har lese- og skrivetilgang til den monterte stasjonen.
- For Linux, sørg for:
  - Hvis du bruker en NFS-montering, må du aktivere `nolock` for monteringen din.
  - Hvis du bruker en SMB-montering, må du aktivere `nobrl` for monteringen din.
- For Windows: Kort sagt, brukeren \*Arr kjører som (hvis tjeneste) eller under (hvis bakgrunnsapp) kan ikke få tilgang til filbanen på den eksterne serveren. Dette kan skyldes forskjellige årsaker, men det vanligste er at \*Arr kjører som en tjeneste, noe som forårsaker problemene som beskrives nedenfor.

### Sonarr kjører som standard under LocalService-kontoen, som ikke har tilgang til beskyttede eksterne filområder

- Kjør Sonarr-tjenesten som en annen bruker som har tilgang til den delte mappen
- Åpne vinduet Administrative Tools \> Services på Windows-serveren din.
- Stopp Sonarr-tjenesten.
- Åpne dialogboksen Properties \> Log On.
- Endre brukerkontoen for tjenesten til målkontoen.
- Kjør Sonarr.exe ved hjelp av Startup-mappen

### Du bruker en kartlagt nettverksstasjon (ikke en UNC-bane)

- Endre banene dine til UNC-baner (`\\server\share`)
- Kjør Sonarr.exe via Startup-mappen

## Kartlagte nettverksstasjoner vs. UNC-baner

- Bruk av kartlagte nettverksstasjoner fungerer generelt ikke så bra, spesielt når Sonarr er konfigurert til å kjøre som en tjeneste. Den beste måten å sette opp delinger på er å bruke UNC-baner. Så i stedet for `X:\TV`, bruk `\\Server\TV`.

- Et viktig poeng å huske er at Sonarr får baninformasjon fra nedlasteren, så du må *også* sette opp NZBGet, SABNzbd eller en annen nedlaster til å bruke UNC-baner.

## Sonarr vil ikke fungere på Big Sur

Kjør

```shell
chmod +x /Applications/Sonarr.app/Contents/MacOS/Sonarr
```

## Skriptet mitt tilpasset sluttet å fungere etter oppgradering fra v2

- Du sendte sannsynligvis argumenter i tilkoblingen din... dette støttes ikke.
- For å rette dette:
  1. Endre argumentet ditt til å være banen din
  1. Sørg for at shebang i skriptet ditt peker på riktig pwsh-bane (hvis du ikke har en shebang-definisjon der, legg den til)
  1. Sørg for at pwsh-skriptet er kjørbart

# Vanlige problemer med Sonarr-søk og -nedlasting

## Spørring vellykket - Ingen resultater returnert

- [Se denne feilsøkingsoppføringen](/sonarr/troubleshooting#query-successful-no-results-returned)

## Hvorfor hentet ikke Sonarr en episode jeg forventet?

Først må du forsikre deg om at du har lest og forstått avsnittet ovenfor kalt ["Hvordan finner Sonarr episoder?](#how-does-sonarr-find-episodes) Sørg deretter for at minst en av indekserne dine har episoden du forventet å få tak i.

1. Klikk på ikonet for "Manuell søk" ved siden av episodelisten i Sonarr. Er det noen resultater? Hvis ikke, har enten Sonarr problemer med å kommunisere med indekserne dine, eller indekserne dine har ikke episoden, eller episoden er feil navngitt/kategorisert på indeksen.
1. **Hvis det er resultater fra trinn 1**, sjekk ved siden av dem etter et rødt utropstegn-ikon. Hold musepekeren over ikonet for å se hvorfor den utgivelsen ikke er en kandidat for automatisk nedlasting. Hvis alle resultatene har ikonet, vil ingen automatisk nedlasting skje.
1. **Hvis det er minst ett gyldig manuelt søkeresultat fra trinn 2**, skal en automatisk nedlasting ha skjedd. Hvis det ikke skjedde, er den mest sannsynlige årsaken et midlertidig kommunikasjonsproblem som hindrer en RSS-synkronisering fra indeksen din. Det anbefales å ha flere indekser satt opp for best resultat.
1. **Hvis det ikke er noe manuelt resultat fra en serie, men du kan finne den når du blar gjennom indeksens nettsted** - Dette kan skyldes forskjellige årsaker, for eksempel at utgivelsen ikke er riktig merket på indeksen din, noe som forhindrer at den returneres til Sonarr i en automatisk søk. Denne [feilsøkingsoppføringen](/sonarr/troubleshooting#searches-indexers-and-trackers) gir noen tips om hvordan du kan finne årsaken. Å ha flere aktive indekser kan bidra til å løse dette ved å gi flere kilder til samme innhold.

## Fant matchende serier via grabbhistorikk, men utgivelsen ble matchet til serien etter ID. Automatisk import er ikke mulig

- Se [denne feilsøkingsoppføringen](/sonarr/troubleshooting#found-matching-series-via-grab-history-but-series-was-matched-by-series-id-automatic-import-is-not-possible)

- På TVDb, når episodetitler er ukjente, vil de bli kalt TBA, og det er en 24-timers hurtigbuffer på TVDb API-en. Vanligvis tar endringer på TVDb-nettstedet 24-48 timer å nå Sonarr på grunn av TVDb-cache (24 timer), skyhook-cache (noen timer) og serieoppdateringsintervallet (hver 12. time). [Innstillingen Episode Title Required](/sonarr/settings#importing) i Sonarr kontrollerer importoppførselen når tittelen er TBA, men etter 48 timer fra seriens sending vil utgivelsen bli importert selv om tittelen fortsatt er TBA. Det er heller ingen automatisk påfølgende omdøping av filer med TBA-tittel. Merk at TBA-timeren beregnes fra episodens sendetidspunkt, ikke fra når du har lastet den ned eller opplastingstidspunktet.

## Sonarr sier Ukjent serie ved søk eller import

- Se [Hvorfor kan ikke Sonarr importere episodfiler for serie X? / Hvorfor kan ikke Sonarr finne utgivelser for serie X?](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x) oppføringen

## Jacketts /all-endepunkt

{#jackett-all-endpoint}

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan føre til problemer, så det er nødvendig å legge til hver enkelt tracker separat. Alternativt kan du sjekke ut Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

- **Oppdatering 5. februar 2022: Støtten for \*Arr har blitt avviklet for jackett `\all`-endepunktet. Jackett /all-endepunktet støttes ikke lenger (f.eks. advarsler vil vises) fra v3.0.6.1457 på grunn av at det bare forårsaker problemer.**

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan føre til problemer, så det er nå nødvendig å legge til hver enkelt tracker.
- [Selv Jacketts utviklere sier at det bør unngås og ikke brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Bruk av /all-endepunktet har ingen fordeler, bare ulemper:
  - du mister kontrollen over innstillingene for hver enkelt indeks (kategorier, søkemåter, osv.)
  - blanding av søkemåter (IMDB, spørring, osv.) kan føre til lavkvalitetsresultater
  - indeksspesifikke kategorier (\>= 100000) kan ikke brukes.
  - treg indekser vil bremse ned det totale resultatet
  - totalt antall resultater er begrenset til 1000
  - hvis en av trackerne i /all returnerer en feil, vil \*Arr deaktivere den, og nå får du ingen resultater.

### Løsninger for Jackett /All

- Legg til hver enkelt tracker i Jackett manuelt som en indeks i \*Arr
- Sjekk ut [Prowlarr](/prowlarr), som kan synkronisere indekser med \*Arr og er utviklet av Lidarr/Radarr/Readarr-utviklingsteamet.
- Sjekk ut [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indekser med \*Arr. Men ikke bruk deres enkeltstående aggregerte endepunkt, bruk `multi` hvis synkronisering skal brukes.

## Jackett viser flere resultater enn Sonarr ved manuelt søk

- Sjekk de konfigurerte kategoriene for trackeren din i Sonarr
- Dette skyldes vanligvis at Sonarr søker i Jackett på en annen måte enn du gjør. [Se denne feilsøkingsartikkelen for mer informasjon](/sonarr/troubleshooting#searches-indexers-and-trackers).

## Finn informasjonskapsler

- Noen nettsteder kan ikke logges inn automatisk og krever at du logger inn manuelt og deretter gir informasjonskapslene til Sonarr for at det skal fungere. [Se denne artikkelen for detaljer.](/useful-tools#finding-cookies)

## Pakk ut torrents

- De fleste torrentklienter har ikke automatisk håndtering av komprimerte arkiver som deres Usenet-motparter. Vi anbefaler [unpackerr](https://github.com/unpackerr/unpackerr).

## Tillatelser

- Sonarr må flytte filer fra der nedlasteren legger dem til den endelige plasseringen, så dette betyr at Sonarr må lese/skrive til både kildekatalogen og destinasjonskatalogen og filene.
- På Linux, der beste praksis er at tjenester kjører som sin egen bruker, vil dette sannsynligvis bety å bruke en delt gruppe og sette mappe- og filtillatelser til `775` og `664` både i nedlasteren din og Sonarr. I umask-notasjon vil det være `002`.

## Påtvunget autentisering

- I Sonarr v4 (beta) er autentisering obligatorisk. Se [Sonarr v4 FAQ - Forced Authentication](/sonarr/faq-v4#forced-authentication) for detaljer.