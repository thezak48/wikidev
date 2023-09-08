---
title: Prowlarr Innstillinger
description: 
published: true
date: 2023-03-30T14:07:39.851Z
tags: 
editor: markdown
dateCreated: 2021-06-06T15:04:48.057Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Menyalternativer](#menyalternativer)
- [Indexer Proxies](#indexer-proxies)
  - [Proxyinnstillinger](#proxyinnstillinger)
  - [FlareSolverr Proxyinnstillinger](#flaresolverr-proxyinnstillinger)
  - [HTTP Proxyinnstillinger](#http-proxyinnstillinger)
  - [Socks4 Proxyinnstillinger](#socks4-proxyinnstillinger)
  - [Socks5 Proxyinnstillinger](#socks5-proxyinnstillinger)
- [Applikasjoner](#applikasjoner)
  - [Applikasjonsinnstillinger](#applikasjonsinnstillinger)
  - [Test applikasjonen](#test-applikasjonen)
- [Nedlastingsklienter (Prowlarr-søk)](#nedlastingsklienter-prowlarr-søk)
  - [Usenet-klientinnstillinger](#usenet-klientinnstillinger)
  - [Torrent-klientinnstillinger](#torrent-klientinnstillinger)
  - [Test nedlastingsklienten](#test-nedlastingsklienten)
- [Varsler](#varsler)
  - [Tilkoblinger](#tilkoblinger)
  - [Varselutløsere](#varselutløsere)
- [Tags](#tags)
- [Generelt](#generelt)
  - [Vert](#vert)
  - [Sikkerhet](#sikkerhet)
  - [Proxy](#proxy)
  - [Logging](#logging)
  - [Analyse](#analyse)
  - [Oppdateringer](#oppdateringer)
  - [Sikkerhetskopier](#sikkerhetskopier)
- [UI](#ui)
  - [Datoer](#datoer)
  - [Stil](#stil)
  - [Språk](#språk)
  
Denne siden vil gå gjennom alle tilgjengelige innstillinger i Prowlarr og hvordan de fungerer. Dette er ikke ment å være en omfattende "hvordan sette opp Prowlarr" guide. Hvis du ønsker det, vennligst bruk [Quick Start](/prowlarr/quick-start-guide) siden i stedet.

# Menyalternativer

For å komme til innstillingssiden, velg Innstillinger fra venstremenyen. Følgende undermenyalternativer vil være tilgjengelige:

![settings_1_menu.png](/assets/prowlarr/settings_1_menu.png)

Merk også at for hver enkelt innstillingsside er det noen alternativer øverst i menyen:

![settings_2_topmenu.png](/assets/prowlarr/settings_2_topmenu.png)

- Skjul/Vis avansert er viktig for alle elementer som er merket som `(Avansert alternativ)` nedenfor, ellers vil de ikke vises. Disse menyelementene vises i oransje på skjermbildene.

- Du må lagre endringene før du forlater skjermen. Dette gjør du ved å klikke på diskikonet. Hvis du ikke har gjort noen endringer, vil det stå "Ingen endringer" og være grået ut, som vist ovenfor.

# Indexer Proxies

> Informasjon om støttede proxytyper finner du på [Mer informasjon (Støttet)](/prowlarr/supported#indexer-proxies) siden for denne seksjonen
{.is-info}

Her kan du legge til proxyer eller Flaresolverr-konfigurasjoner for de indexerne som krever dem.

Gå til `Innstillinger` => `Indexer Proxies`, og klikk deretter på <kb>+</kb> for å legge til en proxy.

![proxies.png](/assets/prowlarr/proxies.png)

## Proxyinnstillinger
  
- Navn - Navnet på proxyen i Prowlarr
- Tags - Taggene for denne proxyen. Proxyer gjelder for alle indexer som matcher (samme tagg). Hvis det er tomt, gjelder denne proxyen for alle indexer.

## FlareSolverr Proxyinnstillinger

- Vert - full vertssti (inkluder http og port) til FlareSolverr-instansen din
- (Avansert innstilling) Timeout for forespørsel (sekunder) - [FlareSolver Request `maxTimeout` verdi](https://github.com/FlareSolverr/FlareSolverr#-requestget) som Prowlarr skal bruke for FlareSolverr-forespørsler. Må være mellom `1` sekund og `180` sekunder (Standard: `60` sekunder)

> \* En FlareSolverr-proxy vil bare bli brukt for forespørsler hvis og bare hvis Cloudflare blir oppdaget av Prowlarr
> \* En FlareSolverr-proxy vil bare bli brukt for forespørsler hvis og bare hvis proxyen og indexerne har samsvarende tagger
> \* **En Flaresolverr-proxy konfigurert uten noen tagger eller uten indexer med samsvarende tagger vil bli deaktivert.**
{.is-info}

## HTTP Proxyinnstillinger

- Vert - vertadressen til proxyen din
- Port - porten til proxyen din
- Brukernavn - brukernavnet til proxyen din
- Passord - passordet til proxyen din

## Socks4 Proxyinnstillinger

- Vert - vertadressen til proxyen din
- Port - porten til proxyen din
- Brukernavn - brukernavnet til proxyen din
- Passord - passordet til proxyen din

## Socks5 Proxyinnstillinger

- Vert - vertadressen til proxyen din
- Port - porten til proxyen din
- Brukernavn - brukernavnet til proxyen din
- Passord - passordet til proxyen din

# Applikasjoner

> Informasjon om støttede applikasjoner finner du på [Mer informasjon (Støttet)](/prowlarr/supported#applications) siden for denne seksjonen
{.is-info}

Her legger du til applikasjonene som bruker Prowlarr (Radarr, Sonarr, Lidarr, Readarr, osv.) og hvordan de holder seg synkronisert med Prowlarr.

- Klikk på `Innstillinger` => `Apps`, og klikk deretter på <kb>+</kb> for å legge til en app.
- Synkroniser appindekser - Utløs en synkronisering av alle indekser til alle applikasjoner
- Test alle apper - Utløs en test av alle applikasjoner
  
![addapps.png](/assets/prowlarr/addapps.png)

Alle programmene du kan legge til, er oppført. Du bør bare legge til programmer du allerede har installert, og hvis du har flere instanser av dem, bør du legge til hver av dem separat.

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Merk: Indekser synkroniseres basert på funksjoner/kategorier de hevder å støtte. Hvis en indeks bare støtter `tv`-kategorier, vil den ikke bli synkronisert til Lidarr, Radarr og Readarr. Den vil bare bli synkronisert til Sonarr. "Støttede" kategorier kan velges som en avansert innstilling per app. **Merk også at \*Arrs bare godtar indekser hvis testforespørslene deres returnerer resultater som inneholder minst en av de konfigurerte kategoriene.**
{.is-info}

## Applikasjonsinnstillinger

- Navn - Skriv inn et navn for denne appen.
- Synkroniseringsnivå - Velg synkroniseringsnivået som skal brukes
  - `Bare legg til og fjern` - Når indekser legges til eller fjernes fra Prowlarr, vil det oppdatere denne eksterne appen. Hvis indeksen er nede på tidspunktet for synkroniseringen, vil den bli deaktivert i den eksterne appen.
  - `Full synkronisering` - Full synkronisering vil holde denne appens indekser fullstendig synkronisert. Endringer som gjøres i indekser i Prowlarr blir deretter synkronisert til denne appen. Eventuelle endringer som gjøres i innstillingene på FAQ-siden for disse indeksene eksternt i denne appen, vil bli overskrevet av Prowlarr ved neste synkronisering. En liste over faktorer som brukes til å sammenligne og avgjøre om en synkronisering skal skje, finnes i [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Deaktivert` - forhindrer at indekser synkroniseres med programmet.

> `Full synkronisering` betyr at Prowlarr vil overskrive de fleste innstillingene, inkludert brukervalgte kategorier som kan konfigureres i Prowlarr. Imidlertid vil innstillinger som ikke styres av Prowlarr ikke bli berørt. Imidlertid vil [nesten alle andre endringer](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) utløse en synkronisering og overskrive de tilsvarende innstillingene i \*Arr
{.is-warning}

- Tags - Hvis du har lagt til en tagg for indeksen under oppsettet, vil bare indekser med denne taggen bli brukt for denne programoppføringen.
- Prowlarr-server - Skriv inn Prowlarr-serverens URL (inkludert http, port og baseurl hvis nødvendig) som appen vil bruke her.

> Merk at hvis du bruker en omvendt proxy, må du legge til URL Base her! Hvis du ikke gjør det, vil indeksene bli ødelagt når de synkroniseres, og hvis du har valgt Bare legg til og fjern, vil det ikke bli fikset når du redigerer det!{.is-info}

- Applikasjonsserver - Skriv inn URL-en til appserveren (inkludert http, port og baseurl hvis nødvendig) for programmet ditt her. Skriv inn full URL Base hvis det brukes.
- API-nøkkel - Skriv inn API-nøkkelen for programmet ditt her. For \*Arrs finner du denne i Innstillinger => Generelt. Du kan få denne fra programmet ditt på `Innstillinger` => `Generelt`-fanen, og kopiere/lim inn den her.
- (Avansert innstilling) Synkroniseringskategorier - Velg kategoriene som skal synkroniseres til denne appen. Indekser som støtter disse kategoriene, vil bli synkronisert.
  - Indekser med egendefinerte kategorier blir kartlagt til standardiserte Torznab/Newznab-kategorier, slik at søk etter standardiserte kategorier inkluderer alle underliggende egendefinerte kategorier. Egendefinerte kategorier for indekser er oppført for finjustering hvis du ikke ønsker dem alle på en gang.
  
## Test applikasjonen

Test oppføringen din. Hvis det vises et grønt hake-merke, kan du lagre oppføringen din og gjenta etter behov for hver app du vil synkronisere med Prowlarr. Hvis det mislykkes, må du sjekke loggen for feilen (URL, API-nøkkel, osv.).

## Synkroniseringsprofiler

Konfigurer synkroniseringsprofilene som skal brukes for (en) applikasjon(er)

> Du kan ha forskjellige innstillinger per app ved å opprette flere instanser av indeksen
{.is-info}

- Navn - Unikt navn på synkroniseringsprofilen
- Aktiver RSS - For indekser med denne profilen, aktiver RSS-søk/spørringer for \*Arr-appen
- Aktiver interaktivt søk - For indekser med denne profilen, aktiver interaktive (manuelle) søk for \*Arr-appen
- Aktiver automatisk søk - For indekser med denne profilen, aktiver automatiske søk for \*Arr-appen
- Minimum seedere - For indekser med denne profilen, minimum antall seedere som kreves for at \*Arr skal laste ned en torrent

# Nedlastingsklienter (Prowlarr-søk)

{#download-clients}

> Informasjon om støttede nedlastingsklienter finner du på [Mer informasjon (Støttet)](/prowlarr/supported#download-clients) siden for denne seksjonen
{.is-info}

Hvis du har til hensikt å gjøre søk direkte i Prowlarr, må du legge til nedlastingsklienter. Ellers trenger du ikke å legge dem til her. For søk fra appene dine brukes nedlastingsklientene som er konfigurert der.

> Prowlarr synkroniserer ikke nedlastingsklienter til applikasjonene.
{.is-info}

Klikk på `Innstillinger` => `Nedlastingsklienter`, og klikk deretter på <kb>+</kb> for å legge til en ny nedlastingsklient. Nedlastingsklienten din bør allerede være konfigurert i henhold til denne veiledningen.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

Velg nedlastingsklienten du ønsker å legge til, og det vil vises en popup-boks der du kan legge inn tilkoblingsdetaljer. Disse detaljene er like for de fleste klienter. Noen vil be om et brukernavn eller passord, noen vil spørre om du vil legge til nye nedlastinger i en pauset/startet tilstand, osv.
  
> Klientprioritet betyr bare noe når 2 av samme type (usenet eller torrent) er lagt til. 1 er høyeste prioritet, og hvis det finnes flere klienter av samme type med samme prioritet, vil Prowlarr veksle mellom dem.
{.is-info}

## Usenet-klientinnstillinger

- Navn - Navnet på nedlastingsklienten i Prowlarr
- Aktiver - Aktiver denne nedlastingsklienten
- Vert - URL-en til nedlastingsklienten din
- Port - Porten til nedlastingsklienten din
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- URL Base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proxyer.
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
- Port - Porten til nedlastingsklienten din; dette er vanligvis webgui-porten
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- URL Base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proxyer.
- Brukernavn - brukernavnet for å autentisere mot klienten din
- Passord - passordet for å autentisere mot klienten din
- Kategori - kategorien i nedlastingsklienten din som Prowlarr vil bruke
- Prioritet - nedlastingsklientprioritet for lagt til elementer
- Initial State - Starttilstand for torrents (kun Qbittorrent: Tvungen omgår alle seed-krav)
- Klientprioritet - Prioritet for nedlastingsklienten i Prowlarr. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet.

## Test nedlastingsklienten

Test oppføringen din. Hvis det vises et grønt hake-merke, kan du lagre oppføringen din og gjenta etter behov for hver nedlastingsklient du vil at Prowlarr skal bruke. Hvis det mislykkes, må du sjekke loggen for feilen (tilkobling, legitimasjon, osv.).

# Varsler

> Informasjon om støttede varslingsleverandører finner du på [Mer informasjon (Støttet)](/prowlarr/supported#notifications) siden for denne seksjonen
{.is-info}

## Tilkoblinger

Tilkoblinger er hvordan du ønsker at Prowlarr skal kommunisere med omverdenen.

- Ved å trykke på <kb>+</kb>-knappen vil du få opp et nytt vindu som lar deg konfigurere mange forskjellige endepunkter

- En liste over støttede varsler og tilkoblinger finnes på [Mer informasjon (Støttet)](/prowlarr/supported#notifications)

## Varselutløsere

- Ved utgivelse - Få varsel når det gjøres en utgivelse i Prowlarr eller via API-en
  - Inkluder manuelle utgivelser - Få varsel når utgivelser utløses manuelt i Prowlarr-brukergrensesnittet
- Ved helseproblem - Få varsel ved helsekontrollfeil
  - Inkluder helseadvarsler - Få varsel om helseadvarsler i tillegg til feil.
- Ved programoppdatering - Få varsel når Prowlarr blir oppdatert til en ny versjon

# Tags

- Tag-seksjonen i Prowlarr brukes til å koble forskjellige aspekter av Prowlarr.
- Tags er spesielt nyttige for:
  - Aktivering av Flaresolverr-proxy for bruk med en indeks; Merk at Flaresolverr-proxier er deaktivert uten en tagg
  - Aktivering av en HTTP- eller SOCKS-proxy for bruk med en indeks
  - Spesifisering av indekser for visse apper

# Generelt

Her endrer du generelle applikasjonsinnstillinger som port og loggingnivå.

Klikk på `Innstillinger` => `Generelt`.

> Mange av alternativene her kan bare sees ved å klikke på "Vis avansert" øverst på skjermen. Eventuelle menyelementer i oransje vises bare når vis avansert er aktivert.
{.is-info}

## Vert

![general_host.png](/assets/prowlarr/general_host.png)

- (Avansert alternativ) Bind-adresse - La denne være `*` med mindre du trenger å endre den. IPv4-adressen/verten på systemet Prowlarr vil lytte på. (standard: `*`)
  - Merk at `*` er alle adresser
- Portnummer - porten som Prowlarr kjører på. Den må være unik. (standard: 9696)
- BaseUrl - Skriv inn en URL-base her hvis du bruker en omvendt proxy. (krever omstart) (standard: blank)
- (Avansert alternativ) Instansnavn - Navn som skal brukes for nettlesertab og SysLog (hvis aktivert) (krever omstart) (standard: Prowlarr)
- (Avansert alternativ) Bruk SSL - Merk av denne boksen hvis du bruker en https-adresse for å koble til Prowlarr. Hvis du bruker `localhost` eller en IP-adresse, bør denne nesten ALDRI være merket av. (standard: false)
- Start nettleser (kun Windows) - Merk av denne boksen hvis du vil at en nettleservindu skal åpnes når Prowlarr starter. (standard: ja)

## Sikkerhet

![general_security.png](/assets/prowlarr/general_security.png)

- Autentisering - Hvordan vil du autentisere for å få tilgang til Prowlarr-instansen din
  - Ingen - Du har ingen autentisering for å få tilgang til Prowlarr. Dette er vanligvis hvis du er den eneste brukeren på nettverket ditt, ikke har noen på nettverket ditt som ønsker å få tilgang til Radarr, eller hvis Radarr ikke er tilgjengelig på nettet
  - Grunnleggende (nettleser pop-up) - Denne alternativet vil vise en liten pop-up når du får tilgang til Prowlarr, som lar deg skrive inn brukernavn og passord
  - Skjema (innloggingsside) - Dette alternativet vil ha en kjent innloggingsrute som ligner på andre nettsteder, som lar deg logge på Prowlarr

- API-nøkkel - API-nøkkelen brukes av eksterne apper som får tilgang til Prowlarr. Denne er hemmelig og bør ikke deles med noen. Hvis den blir delt, bør du generere en ny og oppdatere appene dine.

- Sertifikatvalidering - Endre hvor streng HTTPS-sertifikatvalidering er
  - Aktivert - Valider alle HTTPS-sertifikater (anbefalt)
  - Deaktivert for lokale adresser - Valider alle HTTPS-sertifikater unntatt de på localhost og LAN
  - Deaktivert - Ikke valider noen HTTPS-sertifikater

## Proxy

![general_proxy.png](/assets/prowlarr/general_proxy.png)

Proxy - Dette alternativet lar deg kjøre informasjonen Prowlarr henter og søker etter gjennom en proxy. Dette kan være nyttig hvis du er i et land som ikke tillater nedlasting av torrent-filer.

- Bruk proxy - Aktiver for å bruke en proxy
- Proxytype - Velg proxytype (HTTPS, Socks4 eller Socks5)
- Vertsnavn - Skriv inn vertsnavnet for proxyen din (Ikke inkluder http/https eller noen annen protokoll)
- Port - Skriv inn proxyporten din
- Brukernavn - Skriv inn proxybrukernavnet ditt hvis relevant
- Passord - Skriv inn proxypassordet ditt hvis relevant
- Ignorerte adresser - Skriv inn en kommaseparert liste over adresser som skal omgå proxyen
- Omgå proxy for lokale adresser - Merk av for å omgå proxyen for lokale adresser

## Logging

![general_logging.png](/assets/prowlarr/general_logging.png)

Standardlogg nivået er `Info`. Dette er veldig grunnleggende logging. Du kan endre det her for mer detaljert logging. Loggfilene vil rotere, så det er ingen fare for å ta opp for mye plass.

- Loggnivå - Sannsynligvis et av de mest nyttige feilsøkingsverktøyene
  - Info - Dette er den mest grunnleggende måten Prowlarr samler informasjon på. Denne vil inkludere minimal mengde informasjon i loggene. Denne loggfilen inneholder fatal, feil, advarsel og info-oppføringer.
  - Debug - Debug vil inkludere all informasjonen som Info inkluderer, pluss mer informasjon som kan være nyttig. Denne loggfilen inneholder fatal, feil, advarsel, info og debug-oppføringer.
  - Trace - Den mest avanserte og detaljerte loggingen på Prowlarr. Trace vil inkludere all informasjonen som er samlet inn av Info og Debug, og mer. Dette er den vanligste typen logg som blir bedt om når man feilsøker på Discord eller Reddit. Hvis du trenger hjelp, velg loggen din til Trace og gjenta oppgaven som ga deg problemer for å fange loggen. Denne loggfilen inneholder fatal, feil, advarsel, info, debug og trace-oppføringer.

## Analyse

![general_analytics.png](/assets/prowlarr/general_analytics.png)

- Analyse - Send anonym bruker- og feilinformasjon til Prowlarrs servere (Servarr). Dette inkluderer informasjon om nettleseren din, hvilke Prowlarr WebUI-sider du bruker, feilrapportering samt OS, runtime-versjon og relatert informasjon. Vi vil bruke denne informasjonen til å prioritere funksjoner og feilretting.

## Oppdateringer

![general_updates.png](/assets/prowlarr/general_updates.png)

- (Avansert alternativ) Gren - Dette er grenen av Prowlarr som du kjører på.
  - [Se denne FAQ-innføringen for mer informasjon](/prowlarr/faq#how-do-i-update-prowlarr)
- Automatisk - Last ned og installer oppdateringer automatisk. Du vil fortsatt kunne installere fra System: Oppdateringer. Merk: Windows-brukere blir alltid oppdatert automatisk.
- Mekanisme - Bruk Prowlarrs innebygde oppdaterer eller et skript
  - Innebygd - Bruk Prowlarrs egen oppdaterer
  - Skript - La Prowlarr kjøre oppdateringsskriptet
  - Docker - Ikke oppdater Prowlarr fra innsiden av Docker, i stedet dra inn et helt nytt bilde med den nye oppdateringen
- Skript - Synlig bare når mekanismen er satt til Skript - Sti til oppdateringsskriptet
- Oppdateringsprosess - Prowlarr vil laste ned oppdateringsfilen, verifisere integriteten og pakke den ut til en midlertidig plassering og kalle den valgte metoden. Oppdateringsprosessen vil bli kjørt under samme bruker som Prowlarr kjører under, den vil trenge tillatelser til å oppdatere Prowlarr-filene samt stoppe/starte Prowlarr.
- Innebygd - Den innebygde metoden vil sikkerhetskopiere Prowlarr-filer og innstillinger, stoppe Prowlarr, oppdatere installasjonen og starte Prowlarr. Hvis systemet ditt ikke takler å stoppe Prowlarr og prøver å starte det på nytt automatisk, kan det være best å bruke et skript i stedet. Hvis oppdateringen mislykkes, vil forrige versjon av Prowlarr bli startet på nytt.
- Skript - Skriptet skal håndtere det samme som den innebygde oppdatereren. Hvis du trenger å stoppe og starte tjenester (upstart/launchd/etc), må du gjøre det her.

## Sikkerhetskopier

![general_backups.png](/assets/prowlarr/general_backups.png)

- (Avansert alternativ) Mappe - Dette lar deg velge sikkerhetskopieringsplasseringen. I Docker vil du være begrenset til hva containeren kan se. Stier er relative til appdata-mappen; om nødvendig kan du angi en absolutt sti for å sikkerhetskopiere utenfor appdata-mappen.
- (Avansert alternativ) Intervall - Hvor ofte vil du at Prowlarr skal ta en sikkerhetskopi
- (Avansert alternativ) Oppbevaring - Hvor lenge vil du at Prowlarr skal beholde hver sikkerhetskopi. Etter at en ny sikkerhetskopi er opprettet, vil den eldste sikkerhetskopien bli fjernet

> Manuelle sikkerhetskopier beholdes for alltid, lagres i samme mappe og har forskjellige navn.
{.is-info}

# Brukergrensesnitt

## Datoer

- Kort datoformat - Hvordan vil du at Prowlarr skal vise korte datoer?
- Langt datoformat - Hvordan vil du at Prowlarr skal vise lange datoer?
- Tidsformat - Vil du ha et 12-timers eller 24-timers format?
- Vis relative datoer - Vil du at Prowlarr skal vise relative (I dag/I går/osv.) eller absolutte datoer?

## Stil

- Tema - Velg fargetemaet Prowlarr skal bruke, inspirert av [Theme.Park](https://github.com/GilbN/theme.park)
- Aktiver fargeblindmodus - Endret stil for å la fargeblinde brukere bedre skille fargekodet informasjon

## Språk

- Brukergrensesnittspråk - Velg språket som Prowlarr skal bruke i brukergrensesnittet til applikasjonen