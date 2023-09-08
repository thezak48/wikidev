---
title: Radarr Rask Start Guide
description: 
published: true
date: 2023-08-27T22:14:05.687Z
tags: radarr, quickstart
editor: markdown
dateCreated: 2021-06-20T20:05:44.814Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Rask Start Oppsettsguide](#rask-start-oppsettsguide)
- [Oppstart](#oppstart)
- [Mediehåndtering](#mediehåndtering)
  - [Filnavngivning for filmer](#filnavngivning-for-filmer)
  - [Importering](#importering)
  - [Filhåndtering](#filhåndtering)
  - [Rotmapper](#rotmapper)
- [Profiler](#profiler)
- [Kvalitet](#kvalitet)
- [Indekser](#indekser)
- [Nedlastingsklienter](#nedlastingsklienter)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Hvordan importere ditt eksisterende organiserte mediebibliotek](#hvordan-importere-ditt-eksisterende-organiserte-mediebibliotek)
  - [Importer filmer](#importer-filmer)
  - [Importering av eksisterende medier](#importering-av-eksisterende-medier)
    - [Ingen treff funnet](#ingen-treff-funnet)
    - [Fiks feilaktig mappenavn etter importering](#fiks-feilaktig-mappenavn-etter-importering)
  - [Hvordan legge til en film](#hvordan-legge-til-en-film)

# Rask Start Oppsettsguide

> Denne siden er fortsatt under arbeid og er ikke fullført. Bidrag er velkomne.

> For en mer detaljert gjennomgang av alle innstillingene, sjekk [Radarr => Innstillinger](/radarr/settings)
{.is-info}

I denne guiden vil vi prøve å forklare det grunnleggende oppsettet du trenger å gjøre for å komme i gang med Radarr. Vi vil hoppe over noen alternativer som du kan se på skjermen. Hvis du vil gå dypere inn i disse, kan du se den relevante siden i FAQ-en og dokumentasjonen for en full forklaring.

> Vær oppmerksom på at innstillingene og GUI-innstillingene i `orange` på skjermbildene er avanserte alternativer, så du må klikke på `Vis avansert` øverst på siden for å gjøre dem synlige.
{.is-warning}

# Oppstart

Etter installasjon og oppstart åpner du en nettleser og går til `http://{din_ip_her}:7878`

![Radarr-start.png](/assets/radarr/Radarr-start.png)

# Mediehåndtering

Først skal vi se på innstillingene for `Mediehåndtering` der vi kan sette opp våre foretrukne navngivings- og filhåndteringsinnstillinger.

`Innstillinger` => `Mediehåndtering`

![Radarr-settings-mm.png](/assets/radarr/Radarr-settings-mm.png)

## Filnavngivning for filmer

![Radarr-settings-mm-movie-naming.png](/assets/radarr/Radarr-settings-mm-movie-naming.png)

1. Aktiver/deaktiver omdøping av filmene dine (i motsetning til å la navnene være som de er eller som de var da du lastet dem ned).
2. Hvis du vil erstatte eller fjerne ulovlige tegn (`\ / : * ? " < > | ~ # % & + { }`).
3. Denne innstillingen bestemmer hvordan Radarr håndterer kolonner i filnavnet.
4. Her velger du navnekonvensjonen for de faktiske filene til filmen.
5. *(Avansert alternativ) Her setter du navnekonvensjonen for mappen som inneholder videofilen.*

> Hvis du vil ha en anbefalt navngivningsskjema og eksempler, kan du se på [TRaSH's anbefalte navngivningsskjemaer](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/).
{.is-info}

## Importering

![Radarr-settings-mm-importing.png](/assets/radarr/Radarr-settings-mm-importing.png)

1. *(Avansert alternativ) Aktiver `Bruk hardlenker i stedet for kopi` for mer informasjon om hvordan og hvorfor med eksempler, se [TRaSH's guide for hardlenker](https://trash-guides.info/hardlinks).
1. *(Avansert alternativ) Importer tilsvarende ekstra filer (undertekster, nfo, osv.) etter importering av en fil.*

## Filhåndtering

![Radarr-settings-mm-fm.png](/assets/radarr/Radarr-settings-mm-fm.png)

1. Filmer som er slettet fra disken, blir automatisk overvåket av Radarr.
    - Du kan ønske å slette en film, men ikke ønske at Radarr laster ned filmen på nytt. Du vil bruke denne innstillingen.
1. *(Avansert alternativ) Angi en plassering for slettede filer (i tilfelle du vil hente dem før søppelbøtten tømmes).*
1. *(Avansert alternativ) Dette er hvor gammel en fil kan være før den blir permanent slettet.*

## Rotmapper

![Radarr-settings-mm-root-folder.png](/assets/radarr/Radarr-settings-mm-root-folder.png)

Her legger vi til rotmappen som Radarr vil bruke for å importere ditt eksisterende organiserte mediebibliotek, og hvor Radarr vil importere (kopiere/hardlenke/flytte) medier etter at nedlastingsklienten din har lastet dem ned.

> \* Ikke-Windows: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
> \* Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.
{.is-warning}

> **Brukeren og gruppen du konfigurerte Radarr til å kjøre som, må ha lese- og skrivetilgang til denne plasseringen.** {.is-info}

> Nedlastingsklienten din laster ned til en nedlastingsmappe, og Radarr importerer den til mediamappen (endelig destinasjon) som medieserveren din bruker.
{.is-info}

> **Nedlastingsmappen din og mediamappen (bibliotek-/rotmappe) kan ikke være samme plassering**
{.is-danger}

Ikke glem å lagre endringene

# Profiler

`Innstillinger` => `Profiler`

![Radarr-settings-profiles.png](/assets/radarr/Radarr-settings-profiles.png)

Her kan du konfigurere profiler for kvalitet, foretrukket språk og tilpasset formatvurdering for en film du ønsker å laste ned.

Vi anbefaler at du oppretter dine egne profiler og bare velger kvalitetskilder og språk du faktisk ønsker.

For mer informasjon om utenlandske titler og språk, se [denne FAQ-oppføringen](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

Mange brukere finner [TRaSH's guide for tilpassede format og språk](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) nyttig for å spesifisere språkene til filmene de ønsker.

Profiler er også der tilpassede formatvurderinger konfigureres. Det anbefales sterkt å legge til følgende tilpassede formater fra [TRaSH's guider](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) for å unngå uønskede nedlastinger. Se TRaSHs guide for tilpassede formater og de 3 andre TRaSH-guider for tilpassede formater som er lenket øverst på siden for mer informasjon.

- [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) vil unngå å laste ned utgivelser med Dolby Vision (DV) som har en grønn fargetone hvis DV ikke støttes.
- [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) for å unngå å laste ned dårlig navngitte BR-DISK-er som ikke samsvarer med BR-DISK-kvalitetsanalyse.

> Mer informasjon på [Innstillinger => Profiler](/radarr/settings#profiles).
> For å se forskjellen mellom kvalitetskildene, se [våre definisjoner av kvalitet](/radarr/settings#qualities-defined).
{.is-info}

# Kvalitet

`Innstillinger` => `Kvalitet`

![Radarr-settings-quality.png](/assets/radarr/Radarr-settings-quality.png)

Her kan du endre/finjustere minste og største størrelse på ønskede mediefiler (når du bruker Usenet, må du huske på RAR/PAR2-filene)

> Hvis du trenger hjelp til hva du skal bruke for kvalitetsinnstillinger, kan du sjekke [TRaSH's anbefalte størrelser](https://trash-guides.info/Radarr/Radarr-Quality-Settings-File-Size/) for et testet eksempel.
{.is-info}

# Indekser

`Innstillinger` => `Indekser`

![Radarr-settings-indexers.png](/assets/radarr/Radarr-settings-indexers.png)

Her legger du til indekser/trackere som du vil bruke til å laste ned filene dine.

Når du har klikket på <kb>+</kb>-knappen for å legge til en ny indekser, får du opp et nytt vindu med mange forskjellige alternativer. For Radarr regnes både Usenet-indekser og torrent-trackere som "indekser".

Det er to seksjoner her: Usenet og Torrents. Basert på hvilken nedlastingsklient du vil bruke, må du velge hvilken type indekser du vil gå for.

For torrent-trackere - nesten alle krever bruk av [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett).

# Nedlastingsklienter

`Innstillinger` => `Nedlastingsklienter`

![Radarr-settings-download-clients.png](/assets/radarr/Radarr-settings-download-clients.png)

Nedlasting og importering er der de fleste opplever problemer. På et overordnet nivå må programvaren kunne kommunisere med nedlastingsklienten din og ha lese- og skrivetilgang til plasseringen klienten rapporterer at filene klienten laster ned befinner seg. Det er mange forskjellige støttede nedlastingsklienter og enda flere forskjellige oppsett. Dette betyr at selv om det er noen vanlige oppsett, er det ikke én riktig oppsett, og alle oppsett kan være litt forskjellige. Men det er mange feilaktige oppsett.

> Se [innstillingssiden](/radarr/settings#download-clients), [Mer informasjon (Støttet)](/radarr/supported#download-clients)-siden for denne delen, og [TRaSH's nedlastingsklientguider](https://trash-guides.info/Downloaders/) for mer informasjon.
{.is-info}

## Nedlastingsprotokoller {.tabset}

### Usenet

{#usenet}

- Radarr sender en nedlastingsforespørsel til klienten din og knytter den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Radarr overvåker dine nedlastingsklienters aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Radarr kjenne til den endelige filplasseringen som rapporteres av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din og tilgjengelig for Radarr.
- Radarr skanner denne fullførte filplasseringen etter filer som Radarr kan bruke. Den analyserer filnavnet for å matche det med forespurt media. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til den angitte medieplasseringen.
- Atomiske flyttinger (umiddelbare flyttinger) er aktivert som standard. Filsystemet og monteringene må være de samme for den fullførte nedlastingsmappen og mediebiblioteket ditt. Hvis den atomiske flyttingen mislykkes eller oppsettet ditt ikke støtter hardlenker og atomiske flyttinger, vil Radarr falle tilbake og kopiere filen og deretter slette den fra kilden, noe som er I/O-intensivt.
- Hvis alternativet "Behandling av fullførte nedlastinger - Fjern" er aktivert i Radarrs innstillinger, vil gjenværende filer fra nedlastingen bli sendt til papirkurven eller resirkuleringen via en forespørsel til klienten din om å slette/fjerne utgivelsen.

### BitTorrent

{#bittorrent}

- Radarr sender en nedlastingsforespørsel til klienten din og knytter den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Radarr overvåker dine nedlastingsklienters aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Fullførte nedlastinger som fortsatt seedes, vil filene bli liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Radarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen, vil Radarr opprette en hardlenke til filen hvis det støttes av oppsettet ditt, eller kopiere hvis hardlenker ikke støttes. Torrenter som er satt på pause og fullført seeding, vil bli atomisk flyttet hvis hardlenker støttes, eller kopiert og slettet hvis de ikke støttes.
- Hardlenker er aktivert som standard. [En hardlenke vil ikke bruke noe ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringene må være de samme for den fullførte nedlastingsmappen og mediebiblioteket ditt. Hvis opprettelsen av hardlenken mislykkes eller oppsettet ditt ikke støtter hardlenker, vil Radarr falle tilbake og kopiere filen.
- Hvis alternativet "Behandling av fullførte nedlastinger - Fjern" er aktivert i Radarrs innstillinger, vil Radarr slette torrenten fra klienten din og be klienten om å fjerne torrentdataene, men bare hvis klienten rapporterer at seeding er fullført og torrenten er stoppet (satt på pause etter fullføring).

# Hvordan importere ditt eksisterende organiserte mediebibliotek

> Merk at Radarr ikke søker regelmessig etter filmer. Se [Hvordan fungerer Radarr?](/radarr/faq#how-does-radarr-work) FAQ-oppføringen for detaljer om hvordan Radarr fungerer.
{.is-info}

Etter at du har satt opp profilene/den ønskede kvaliteten og lagt til indekser og nedlastingsklient(er), er det på tide å importere ditt eksisterende organiserte mediebibliotek.

`Filmer`

![Radarr-movies.png](/assets/radarr/Radarr-movies.png)

Velg `Importer eksisterende filmer` eller velg `Importer` fra sidepanelet.

## Importer filmer

![Radarr-movies-import.png](/assets/radarr/Radarr-movies-import.png)

Velg rotbanen du la til tidligere [i rotmappeseksjonen.](#rotmapper)

## Importering av eksisterende medier

![Radarr-importing-existing.png](/assets/radarr/Radarr-importing-existing.png)

Avhengig av hvor godt du har navngitt de eksisterende filmmappene dine, vil Radarr prøve å matche dem med riktig film som vist i nr. 5. Hvis alle filmene dine er i en enkelt mappe, følg denne [veiledningen](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

1. Navnet på filmappen din.
1. Overvåking - Hvordan du vil at filmen skal legges til i Radarr.

- Ingen - Overvåk verken filmen eller samlingen for nye utgivelser
- Kun film - Overvåk kun filmen for nye utgivelser
- Film og samling - Overvåk både filmen for nye utgivelser og legg til og overvåk eventuelle filmer i filmens samling (hvis den finnes)

1. Tilgjengelighet - Når vil Radarr anse en film som tilgjengelig.

- **Kunngjort**: Radarr vil anse filmer som tilgjengelige så snart de er lagt til i Radarr. Denne innstillingen er *anbefalt* hvis du har gode private trackere som ikke har falske utgivelser.
- **I kino**: Radarr vil anse filmer som tilgjengelige så snart de er på kino. Denne innstillingen er *ikke anbefalt*.
- **Utgitt**: Radarr vil anse filmer som tilgjengelige så snart Blu-ray-en er utgitt. Denne innstillingen er *anbefalt* hvis indekserne dine ofte inneholder falske utgivelser.

1. Kvalitetsprofil - Velg den foretrukne profilen du vil bruke.
1. Film - Hva Radarr tror filmen matcher. Det er viktig at du sjekker dette og redigerer/søker hvis kampen ikke er riktig. Feilaktige kamper skyldes ofte dårlig navngitte mapper.
1. Massevelg overvåkingsstatus.
1. Massevelg minimumstilgjengelighet.
1. Massevelg kvalitetsprofil.
1. Start importeringen av ditt eksisterende mediebibliotek.

Når en film er lagt til i Radarr, vil Radarr skanne filmens mappe og forsøke å matche en videofil i mappen med filmen. Den vanligste årsaken til at Radarr ikke matcher filen og filmen dermed har en Radarr-status som mangler, er at filnavnet ikke har året i seg. Radarr krever at året er inkludert i filnavnet for at det skal kunne analyseres.

### Ingen treff funnet

Hvis du får en feilmelding som dette

![Radarr-importing-existing-no-match.png](/assets/radarr/Radarr-importing-existing-no-match.png)

Har du sannsynligvis gjort en feil med navngivningen av filmappen din.

For å løse dette problemet kan du prøve følgende

Utvid feilmeldingen

![Radarr-importing-existing-no-match-expand.png](/assets/radarr/Radarr-importing-existing-no-match-expand.png)

og sjekk på [themoviedb](https://www.themoviedb.org/) om året eller tittelen stemmer. I dette eksempelet vil du legge merke til at året er feil, og du kan fikse det ved å endre året og klikke på oppdateringsikonet.

![radarr-importing-existing-no-match-expand-refresh.png](/assets/radarr/radarr-importing-existing-no-match-expand-refresh.png)

Eller så kan du bare bruke tmdb:id eller imdb:id (hvis tmdb er koblet til imdb) og deretter velge den funnete filmen hvis den er matchet.

![Radarr-importing-existing-no-match-expand-tmdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-tmdb.png)

![Radarr-importing-existing-no-match-expand-imdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-imdb.png)

### Fiks feilaktig mappenavn etter import

![Radarr-wrong-folder-name.png](/assets/radarr/Radarr-wrong-folder-name.png)

Du vil legge merke til etter at vi har fikset under importen at mappenavnet fortsatt har feil årstall i seg. For å fikse dette skal vi gjøre en liten magisk triks.

Gå til filmoversikten din

`Movies`

Klikk på `Movie Editor` øverst

![Radarr-movie-editor.png](/assets/radarr/Radarr-movie-editor.png)

Etter å ha aktivert det, velger du filmen(e) der du vil ha mappen(e) omdøpt.

![Radarr-movie-editor-select.png](/assets/radarr/Radarr-movie-editor-select.png)

1. Hvis du vil ha alle filmmappene dine omdøpt til ditt tidligere angitte mappenavningsformat [filmnavngivingsseksjonen](#movie-naming).
2. Velg filmen(e) der du vil ha mappen(e) omdøpt.
3. Velg samme `Root Folder`

En ny popup vil vises

![Radarr-movie-editor-move-files-yes.png](/assets/radarr/Radarr-movie-editor-move-files-yes.png)

Velg `Ja, flytt filene`

Så magi

![Radarr-correct-folder-name.png](/assets/radarr/Radarr-correct-folder-name.png)

Som du kan se, har mappen blitt omdøpt til riktig år i henhold til ditt navngivingsformat.

## Hvordan legge til en film

Etter at du har importert din eksisterende, godt organiserte mediebibliotek, er det på tide å legge til filmene du ønsker.

`Movies` => `Add New`

![Radarr-add-new.png](/assets/radarr/Radarr-add-new.png)

Skriv inn filmen du ønsker i boksen, eller bruk tmdb:id eller imdb:id.

Når du skriver inn filmnavnet, vil du se at det begynner å vise resultater.

![Radarr-movie-search.png](/assets/radarr/Radarr-movie-search.png)

Når du ser filmen du vil ha, klikker du på den.

![Radarr-movie-add.png](/assets/radarr/Radarr-movie-add.png)

1. Root Folder - Radarr vil legge til filmen i rotmappen du har satt opp [i rotmappeseksjonen](#root-folders)
1. Monitor - Hvordan du vil at filmen skal legges til i Radarr.

- Kun film = Radarr vil overvåke RSS-feeden etter filmer i biblioteket ditt som du ikke har (ennå) eller oppgradere den eksisterende filmen til bedre kvalitet.
- Film og samling = Radarr vil overvåke RSS-feeden etter filmer i biblioteket ditt som du ikke har (ennå) eller oppgradere den eksisterende filmen til bedre kvalitet. Den vil også legge til alle filmer i denne filmens samling (hvis det er noen) med dine valgte innstillinger.
- Ingen = Radarr vil ikke overvåke RSS-feeden, eventuelle oppgraderinger eller nye filmer vil bli ignorert og må gjøres manuelt. Alle søk etter uovervåkede filmer må være manuelt utløste søk eller interaktive søk.

1. Tilgjengelighet - Når Radarr skal anse en film som tilgjengelig.

> For mer informasjon om TMDBs datoer som påvirker tilgjengelighetene nedenfor, se [Hvordan bestemmer Radarr året for en film](#how-does-radarr-determine-the-year-of-a-movie)
{.is-info}

- **Kunngjort**: Radarr skal anse filmer som tilgjengelige så snart de er lagt til i Radarr. Denne innstillingen anbefales hvis du har gode private sporere (eller virkelig gode offentlige, f.eks. rarbg.to) som ikke har falske filmer.
- **På kino**: Radarr skal anse filmer som tilgjengelige så snart de vises på kino (Theatrical Date på TMDb). Denne innstillingen anbefales ikke.
- **Utgitt**: Radarr skal anse filmer som tilgjengelige så snart Blu-Ray- eller strømmingsversjonen er utgitt (Digitale og fysiske datoer på TMDb). Denne innstillingen anbefales og bør sannsynligvis kombineres med en tilgjengelighetsforsinkelse på `-14` eller `-21` dager.
  - Hvis TMDb ikke er fylt ut med en dato, antas det at 90 dager etter `Theatrical Date` (eldste dato for kinovisning) er filmen tilgjengelig på nettet eller fysiske tjenester.

1. Kvalitetsprofil - Velg profilen du vil bruke for denne filmen
1. Merkelapper - Her kan du legge til visse merkelapper for avansert bruk.
1. Søk ved tillegg - Sørg for at du aktiverer dette hvis du vil at Radarr skal søke etter den manglende filmen når den legges til i Radarr [mer informasjon](/radarr/faq#how-does-radarr-find-movies)
1. Klikk på `Add Movie` for å legge til filmen i Radarr.

- Hvis du får en feilmelding om "path is already configured" [se denne FAQ-oppføringen](/radarr/faq#path-is-already-configured-for-an-existing-movie)