---
title: Radarr Hurtigstartsguide
description: 
published: true
date: 2023-08-27T22:14:05.687Z
tags: radarr, quickstart
editor: markdown
dateCreated: 2021-06-20T20:05:44.814Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Hurtigstartopsætningsguide](#hurtigstartopsætningsguide)
- [Opstart](#opstart)
- [Mediehåndtering](#mediehåndtering)
  - [Filnavngivning af film](#filnavngivning-af-film)
  - [Importering](#importering)
  - [Filhåndtering](#filhåndtering)
  - [Rodmapper](#rodmapper)
- [Profiler](#profiler)
- [Kvalitet](#kvalitet)
- [Indexere](#indexere)
- [Downloadklienter](#downloadklienter)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Sådan importerer du dit eksisterende organiserede mediebibliotek](#sådan-importerer-du-dit-eksisterende-organiserede-mediebibliotek)
  - [Importer film](#importer-film)
  - [Importering af eksisterende medier](#importering-af-eksisterende-medier)
    - [Ingen match fundet](#ingen-match-fundet)
    - [Ret fejlagtigt mappenavn efter import](#ret-fejlagtigt-mappenavn-efter-import)
  - [Sådan tilføjer du en film](#sådan-tilføjer-du-en-film)

# Hurtigstartopsætningsguide

> Denne side er stadig under udarbejdelse og er ikke fuldstændig. Bidrag er velkomne.

> Hvis du vil have en mere detaljeret gennemgang af alle indstillingerne, kan du se [Radarr => Indstillinger](/radarr/settings).
{.is-info}

I denne guide vil vi forsøge at forklare den grundlæggende opsætning, du skal gøre for at komme i gang med Radarr. Vi vil springe nogle af de muligheder over, som du måske ser på skærmen. Hvis du vil dykke dybere ned i disse, kan du se den relevante side i FAQ'en og dokumentationen for en fuld forklaring.

> Bemærk venligst, at inden for skærmbillederne og GUI-indstillingerne i `orange` er avancerede indstillinger, så du skal klikke på `Vis avanceret` øverst på siden for at gøre dem synlige.
{.is-warning}

# Opstart

Efter installation og opstart åbner du en browser og går til `http://{din_ip_her}:7878`

![Radarr-start.png](/assets/radarr/Radarr-start.png)

# Mediehåndtering

Først skal vi se på indstillingerne for `Mediehåndtering`, hvor vi kan konfigurere vores foretrukne navngivning og filhåndteringsindstillinger.

`Indstillinger` => `Mediehåndtering`

![Radarr-settings-mm.png](/assets/radarr/Radarr-settings-mm.png)

## Filnavngivning af film

![Radarr-settings-mm-movie-naming.png](/assets/radarr/Radarr-settings-mm-movie-naming.png)

1. Aktivér/deaktivér omdøbning af dine film (i modsætning til at lade navnene være som de er, eller som de var, da du downloadede dem).
2. Hvis du vil have ulovlige tegn erstattet eller fjernet (`\ / : * ? " < > | ~ # % & + { }`).
3. Denne indstilling bestemmer, hvordan Radarr håndterer kolonner i filnavnet.
4. Her vælger du navngivelseskonventionen for de faktiske filmfiler.
5. *(Avanceret indstilling) Her indstiller du navngivelseskonventionen for mappen, der indeholder videofilen.*

> Hvis du vil have en anbefalet navngivelsesordning og eksempler, kan du se [TRaSH's anbefalede navngivelsesordninger](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/).
{.is-info}

## Importering

![Radarr-settings-mm-importing.png](/assets/radarr/Radarr-settings-mm-importing.png)

1. *(Avanceret indstilling) Aktivér `Brug hardlinks i stedet for kopi` for mere information om, hvordan og hvorfor med eksempler, se [TRaSH's hardlink-guide](https://trash-guides.info/hardlinks).
1. *(Avanceret indstilling) Importer matchende ekstra filer (undertekster, nfo osv.) efter import af en fil.*

## Filhåndtering

![Radarr-settings-mm-fm.png](/assets/radarr/Radarr-settings-mm-fm.png)

1. Film, der er slettet fra disken, overvåges automatisk ikke i Radarr.
    - Du vil måske slette en film, men ønsker ikke, at Radarr skal downloade filmen igen. Du vil bruge denne indstilling.
1. *(Avanceret indstilling) Angiv en placering, hvor slettede filer skal placeres (bare hvis du vil hente dem, inden skraldespanden tømmes).*
1. *(Avanceret indstilling) Dette er, hvor gammel en given fil kan være, før den slettes permanent.*

## Rodmapper

![Radarr-settings-mm-root-folder.png](/assets/radarr/Radarr-settings-mm-root-folder.png)

Her tilføjer vi rodmappen, som Radarr vil bruge til at importere dit eksisterende organiserede mediebibliotek, og hvor Radarr vil importere (kopiere/hardlink/flytte) dine medier efter, at din downloadklient har downloadet dem.

> \* Ikke-Windows: Hvis du bruger et NFS-mount, skal du sørge for, at `nolock` er aktiveret.
> \* Hvis du bruger et SMB-mount, skal du sørge for, at `nobrl` er aktiveret.
{.is-warning}

> **Brugeren og gruppen, du har konfigureret Radarr til at køre som, skal have læse- og skriveadgang til denne placering.** {.is-info}

> Din downloadklient downloader til en downloadmappe, og Radarr importerer det til din mediemappe (endelig destination), som din medieserver bruger.
{.is-info}

> **Din downloadmappe og mediemappe (bibliotek / rodmappe) kan ikke være den samme placering**
{.is-danger}

Glem ikke at gemme dine ændringer

# Profiler

`Indstillinger` => `Profiler`

![Radarr-settings-profiles.png](/assets/radarr/Radarr-settings-profiles.png)

Her kan du konfigurere profiler, som du kan have for kvaliteten, foretrukne sprog og brugerdefineret formatvurdering af en film, du vil downloade.

Vi anbefaler, at du opretter dine egne profiler og kun vælger de kvalitetskilder og sprog, du rent faktisk ønsker.

For mere information om udenlandske titler og sprog, se [dette FAQ-indlæg](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles).

Mange brugere finder [TRaSH's guide til brugerdefinerede formatsprog](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) nyttig til at specificere sprogene for de film, de ønsker.

Profiler er også, hvor brugerdefinerede formatvurderinger konfigureres. Det anbefales kraftigt at tilføje følgende brugerdefinerede formater fra [TRaSH's guider](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) for at undgå uønskede downloads. Se den tilknyttede TRaSH-guide til brugerdefinerede formater og yderligere 3 TRaSH-guider til brugerdefinerede formater øverst på siden med brugerdefinerede formater for mere information.

- [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) undgår at downloade udgivelser med Dolby Vision (DV), der har en grøn farvetone, hvis DV ikke understøttes.
- [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) undgår at downloade dårligt navngivne BR-DISKs, der ikke matcher BR-DISK-kvalitetsanalyse.

> Mere information på [Indstillinger => Profiler](/radarr/settings#profiles).
> For at se forskellen mellem kvalitetskilderne, se [vores kvalitetsdefinitioner](/radarr/settings#qualities-defined).
{.is-info}

# Kvalitet

`Indstillinger` => `Kvalitet`

![Radarr-settings-quality.png](/assets/radarr/Radarr-settings-quality.png)

Her kan du ændre/finjustere den mindste og største størrelse på dine ønskede mediefiler (når du bruger Usenet, skal du huske på RAR/PAR2-filerne)

> Hvis du har brug for hjælp til, hvad du skal bruge til kvalitetsindstillinger, kan du se [TRaSH's størrelsesanbefalinger](https://trash-guides.info/Radarr/Radarr-Quality-Settings-File-Size/) for et testet eksempel.
{.is-info}

# Indexere

`Indstillinger` => `Indexere`

![Radarr-settings-indexers.png](/assets/radarr/Radarr-settings-indexers.png)

Her tilføjer du indexeren/trackeren, som du vil bruge til faktisk at downloade dine filer.

Når du har klikket på <kb>+</kb>-knappen for at tilføje en ny indexer, får du en ny vindue med mange forskellige indstillinger. I Radarr betragtes både Usenet-indexere og torrent-trackere som "indexere".

Der er to sektioner her: Usenet og Torrents. Afhængigt af hvilken downloadklient du vil bruge, skal du vælge den type indexer, du vil bruge.

For torrent-trackere - næsten alle kræver brug af [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett).

# Downloadklienter

`Indstillinger` => `Downloadklienter`

![Radarr-settings-download-clients.png](/assets/radarr/Radarr-settings-download-clients.png)

Download og import er det, hvor de fleste mennesker oplever problemer. Set fra et overordnet perspektiv skal softwaren kunne kommunikere med din downloadklient og have læse- og skriveadgang til den placering, som downloadklienten rapporterer, at klienten downloader filerne til. Der er mange understøttede downloadklienter og endnu flere forskellige opsætninger. Det betyder, at selvom der er nogle fælles opsætninger, er der ikke én rigtig opsætning, og alle opsætninger kan være lidt forskellige. Men der er mange forkerte opsætninger.

> Se [indstillingssiden](/radarr/settings#download-clients), [Mere info (Understøttet)](/radarr/supported#download-clients)-siden for denne sektion og [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for mere information.
{.is-info}

## Downloadprotokoller {.tabset}

### Usenet

{#usenet}

- Radarr sender en downloadanmodning til din klient og forbinder den med etiketten eller kategorinavnet, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Radarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er fuldført, kender Radarr den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et separat sted fra din mediemappe og kan tilgås af Radarr.
- Radarr scanner denne fuldførte filplacering for filer, som Radarr kan bruge. Den analyserer filnavnet for at matche det med det ønskede medie. Hvis det kan gøre det, omdøber den filen i henhold til dine specifikationer og flytter den til den angivne medieplacering.
- Atomiske flytninger (øjeblikkelige flytninger) er aktiveret som standard. Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis den atomiske flytning mislykkes, eller din opsætning ikke understøtter hardlinks og atomiske flytninger, vil Radarr falde tilbage og kopiere filen og derefter slette den fra kilden, hvilket er I/O-intensivt.
- Hvis indstillingen "Behandling af fuldførte downloads - Fjern" er aktiveret i Radarrs indstillinger, sendes resterende filer fra downloaden til papirkurven eller genbrugsstationen via en anmodning til din klient om at slette/fjerne udgivelsen.

### BitTorrent

{#bittorrent}

- Radarr sender en downloadanmodning til din klient og forbinder den med etiketten eller kategorinavnet, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Radarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Færdiggjorte downloads, der stadig seedes, efterlades i deres oprindelige placering, så du kan seede filen (ratio eller tid kan justeres i downloadklienten eller fra Radarr under den specifikke downloadklient). Når filer importeres til din mediemappe, opretter Radarr et hardlink til filen, hvis det understøttes af din opsætning, eller kopierer, hvis hardlinks ikke understøttes. Torrents, der er sat på pause og er færdige med at seede, flyttes atomisk, hvis hardlinks understøttes, eller kopieres og slettes, hvis de ikke understøttes.
- Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din opsætning ikke understøtter hardlinks, vil Radarr falde tilbage og kopiere filen.
- Hvis indstillingen "Behandling af fuldførte downloads - Fjern" er aktiveret i Radarrs indstillinger, sletter Radarr torrenten fra din klient og beder klienten om at fjerne torrentdataene, men kun hvis klienten rapporterer, at seeding er fuldført, og torrenten er stoppet (sat på pause efter fuldførelse).

# Sådan importerer du dit eksisterende organiserede mediebibliotek

> Bemærk, at Radarr ikke regelmæssigt søger efter film. Se [Hvordan fungerer Radarr?](/radarr/faq#how-does-radarr-work) FAQ-indlægget for detaljer om, hvordan Radarr fungerer.
{.is-info}

Efter at have konfigureret dine profiler/kvalitetsstørrelser og tilføjet dine indexere og downloadklient(er), er det tid til at importere dit eksisterende organiserede mediebibliotek.

`Film`

![Radarr-movies.png](/assets/radarr/Radarr-movies.png)

Vælg `Importer eksisterende film` eller vælg `Importer` fra sidepanelet.

## Importer film

![Radarr-movies-import.png](/assets/radarr/Radarr-movies-import.png)

Vælg den rodmappe, du tidligere har tilføjet [i afsnittet om rodmapper.](#rodmapper)

## Importering af eksisterende medier

![Radarr-importing-existing.png](/assets/radarr/Radarr-importing-existing.png)

Afhængigt af hvor godt du har navngivet dine eksisterende filmmapper, vil Radarr forsøge at matche dem med den korrekte film, som vist i nr. 5. Hvis alle dine film er i en enkelt mappe, skal du følge denne [guide](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

1. Navnet på din filmmappe.
1. Overvågning - Hvordan du vil have filmen tilføjet til Radarr.

- Ingen - Overvåg ikke filmen eller samlingen for nye udgivelser
- Kun film - Overvåg kun filmen for nye udgivelser
- Film og samling - Overvåg både filmen for nye udgivelser og tilføj og overvåg eventuelle film i filmens samling (hvis de findes)

1. Tilgængelighed - Hvornår vil Radarr betragte en film som tilgængelig.

- **Annonceret**: Radarr betragter film som tilgængelige, så snart de er tilføjet til Radarr. Denne indstilling anbefales, hvis du har gode private trackere, der ikke har falske udgivelser.
- **I biografen**: Radarr betragter film som tilgængelige, så snart de rammer biograferne. Denne indstilling anbefales ikke.
- **Udgivet**: Radarr betragter film som tilgængelige, så snart Blu-ray'en er udgivet. Denne indstilling anbefales, hvis dine indexere ofte indeholder falske udgivelser.

1. Kvalitetsprofil - Vælg din foretrukne profil.
1. Film - Hvad Radarr mener, filmen matcher. Det er vigtigt, at du gennemgår dette og redigerer/søger, hvis matchet ikke er korrekt. Forkerte match skyldes ofte dårligt navngivne mapper.
1. Massevælg overvågningsstatus.
1. Massevælg minimum tilgængelighed.
1. Massevælg kvalitetsprofil.
1. Start import af dit eksisterende mediebibliotek.

Når en film er tilføjet til Radarr, scanner Radarr filmens mappe og forsøger at matche en videofil i mappen med filmen. Den mest almindelige årsag til, at Radarr ikke matcher filen og filmen derfor har en Radarr-status som manglende, er, at filnavnet ikke indeholder året. Radarr kræver, at året er med i filnavnet for at kunne analysere det.  

### Ingen match fundet

Hvis du får en fejl som denne

![Radarr-importing-existing-no-match.png](/assets/radarr/Radarr-importing-existing-no-match.png)

Har du sandsynligvis lavet en fejl med navngivningen af din filmmappe.

For at løse dette problem kan du prøve følgende

Udvid fejlmeddelelsen

![Radarr-importing-existing-no-match-expand.png](/assets/radarr/Radarr-importing-existing-no-match-expand.png)

og tjek på [themoviedb](https://www.themoviedb.org/), om året eller titlen passer. I dette eksempel vil du bemærke, at året er forkert, og du kan rette det ved at ændre året og klikke på opdateringsikonet.

![radarr-importing-existing-no-match-expand-refresh.png](/assets/radarr/radarr-importing-existing-no-match-expand-refresh.png)

Eller du kan bare bruge tmdb:id eller imdb:id (hvis tmdb er linket til imdb) og derefter vælge den fundne film, hvis den matcher.

![Radarr-importing-existing-no-match-expand-tmdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-tmdb.png)

![Radarr-importing-existing-no-match-expand-imdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-imdb.png)

### Ret fejlagtigt mappenavn efter import

![Radarr-wrong-folder-name.png](/assets/radarr/Radarr-wrong-folder-name.png)

Du vil bemærke, at efter den rettelse, vi lavede under importen, har mappenavnet stadig det forkerte år i det. For at rette dette skal vi lave et lille magisk trick.

Gå til filmoversigten

`Film`

Klik øverst på `Filmredigering`

![Radarr-movie-editor.png](/assets/radarr/Radarr-movie-editor.png)

Efter aktivering vælger du filmen(e), hvor du vil have, at mapperne skal omdøbes.

![Radarr-movie-editor-select.png](/assets/radarr/Radarr-movie-editor-select.png)

1. Hvis du vil have alle dine filmmapper omdøbt til din tidligere indstillede mappestruktur [afsnit om filminavngivning](#filminavngivning).
2. Vælg filmen(e), hvor du vil have, at mapperne skal omdøbes.
3. Vælg den samme `Rodmappe`

Der vises en ny popup

![Radarr-movie-editor-move-files-yes.png](/assets/radarr/Radarr-movie-editor-move-files-yes.png)

Vælg `Ja, flyt filerne`

Så magi

![Radarr-correct-folder-name.png](/assets/radarr/Radarr-correct-folder-name.png)

Som du kan se, er mappen blevet omdøbt til det korrekte år i henhold til din mappestruktur.

## Sådan tilføjer du en film

Efter du har importeret din eksisterende, velorganiserede mediebibliotek, er det tid til at tilføje de film, du ønsker.

`Film` => `Tilføj ny`

![Radarr-add-new.png](/assets/radarr/Radarr-add-new.png)

Skriv filmen, du ønsker, i boksen, eller brug tmdb:id eller imdb:id.

Når du skriver filmnavnet, vil du se, at den begynder at vise resultater.

![Radarr-movie-search.png](/assets/radarr/Radarr-movie-search.png)

Når du ser den ønskede film, skal du klikke på den.

![Radarr-movie-add.png](/assets/radarr/Radarr-movie-add.png)

1. Rodmappe - Radarr vil tilføje filmen til den rodmappe, du har sat op [i afsnittet om rodmapper](#rodmapper)
1. Overvåg - Hvordan du vil have filmen tilføjet til Radarr.

- Kun film = Radarr vil overvåge RSS-feedet efter filmen i dit bibliotek, som du ikke har (endnu) eller opgradere den eksisterende film til en bedre kvalitet.
- Film og samling = Radarr vil overvåge RSS-feedet efter filmen i dit bibliotek, som du ikke har (endnu) eller opgradere den eksisterende film til en bedre kvalitet. Den vil også tilføje alle film i denne films samling (hvis der er nogen) med dine valgte indstillinger.
- Ingen = Radarr vil ikke overvåge RSS-feedet, eventuelle opgraderinger eller nye film vil blive ignoreret og skal gøres manuelt. Alle søgninger efter ikke-overvågede film skal være manuelt udløste søgninger eller interaktive søgninger.

1. Tilgængelighed - Hvornår Radarr skal betragte en film som tilgængelig.

> For mere information om TMDB's datoer, der påvirker de nedenstående tilgængeligheder, se [Hvordan bestemmer Radarr filmens år](#hvordan-bestemmer-radarr-filmens-ar)
{.is-info}

- **Annonceret**: Radarr vil betragte film som tilgængelige, så snart de er tilføjet til Radarr. Denne indstilling anbefales, hvis du har gode private trackere (eller virkelig gode offentlige, f.eks. rarbg.to), der ikke har falske film.
- **I biografen**: Radarr vil betragte film som tilgængelige, så snart de rammer biograferne (Teaterdato på TMDb). Denne indstilling anbefales ikke.
- **Udgivet**: Radarr vil betragte film som tilgængelige, så snart Blu-Ray- eller streamingversionen er udgivet (Digitale og fysiske datoer på TMDb). Denne indstilling anbefales, og den bør sandsynligvis kombineres med en tilgængelighedsforsinkelse på `-14` eller `-21` dage.
  - Hvis TMDb ikke er udfyldt med en dato, antages det, at filmen er tilgængelig 90 dage efter `Teaterdatoen` (Ældste dato for filmens biografpremiere) på web eller fysiske tjenester.

1. Kvalitetsprofil - Vælg din profil, der skal bruges til denne film
1. Tags - Her kan du tilføje visse tags til avanceret brug.
1. Søg ved tilføjelse - Sørg for at aktivere dette, hvis du vil have, at Radarr søger efter den manglende film, når den tilføjes til Radarr [mere info](/radarr/faq#how-does-radarr-find-movies)
1. Klik på `Tilføj film` for at tilføje filmen til Radarr.

- Hvis du får en fejl med "stien er allerede konfigureret" [se dette FAQ-indlæg](/radarr/faq#path-is-already-configured-for-an-existing-movie)