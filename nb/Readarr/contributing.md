---
title: Readarr Bidra til prosjektet
description: 
published: true
date: 2022-09-26T15:56:42.368Z
tags: readarr, utvikling, bidrag
editor: markdown
dateCreated: 2021-05-25T19:21:59.324Z
---

# Hvordan bidra

Vi er alltid på utkikk etter folk som kan hjelpe til med å gjøre Readarr enda bedre, og det finnes flere måter å bidra på.

# Dokumentasjon

Oppsettsguider, [FAQ](/readarr/faq), jo mer informasjon vi har på [wikien](https://wiki.servarr.com/readarr), jo bedre.

# Utvikling

Readarr er skrevet i C# (backend) og JS (frontend). Backend er bygget på .NET6-rammeverket, mens frontend bruker Reactjs.

## Nødvendige verktøy

- Visual Studio 2022 eller nyere anbefales (<https://www.visualstudio.com/vs/>). Community-versjonen er gratis og fungerer (<https://www.visualstudio.com/downloads/>).

> VS 2022 V17.0 eller nyere anbefales, da det inkluderer .NET6 SDK
{.is-info}

- HTML/Javascript-editor etter eget valg (VS Code/Sublime Text/Webstorm/Atom/etc)
- [Git](https://git-scm.com/downloads)
- Kjøretidsmiljøet [Node.js](https://nodejs.org/) er påkrevd. Følgende versjoner støttes:
  - **12.0** eller nyere
  - **14.0** eller nyere
  - **16.0** eller nyere
{.grid-list}

> Readarr vil **IKKE** kjøre på eldre versjoner som `10.x`, `8.x`, `6.x`, eller noen versjon under 12.0!
{.is-warning}

- [Yarn](https://yarnpkg.com/getting-started/install) er nødvendig for å bygge frontend
  - Yarn er inkludert med **Node 16.10**+ som standard. Aktiver det med `corepack enable`
  - For andre Node-versjoner, installer det med `npm i -g corepack`

## Komme i gang

1. Fork Readarr
1. Klon repositoriet til utviklingsmaskinen din. [*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> Sørg for å kjøre lint `yarn lint --fix` på koden din for eventuelle endringer i frontend før du committer.
For css-endringer `yarn stylelint-windows --fix` {.is-info}

### Bygge frontend

- Naviger til den klonede mappen
- Installer nødvendige Node-pakker

     ```bash
     yarn install
     ```

- Start webpack for å overvåke utviklingsmiljøet ditt for eventuelle endringer som trenger etterbehandling ved hjelp av:

     ```bash
     yarn start
     ```

### Bygge backend

Backend-løsningen bygges og kjøres enklest i Visual Studio eller Rider, men hvis det eneste fokuset er å jobbe med frontend-brukergrensesnittet, kan det også bygges enkelt fra kommandolinjen når riktig SDK er installert.

#### Visual Studio

> Sørg for at oppstartprosjektet er satt til `Readarr.Console` og rammeverket til `net6.0`
{.is-info}

1. Bygg løsningen i Visual Studio først. Dette vil sikre at alle prosjekter bygges riktig og avhengigheter gjenopprettes.
1. Start deretter prosjektet i Visual Studio for å starte Readarr.
1. Åpne <http://localhost:8787>

#### Kommandolinje

1. Rens løsningen

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. Gjenopprett og bygg debug-konfigurasjonen for riktig plattform (Posix eller Windows)

```shell
dotnet msbuild -restore src/Readarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. Kjør den produserte kjørbare filen fra `/_output`

## Bidra med kode

- Hvis du legger til en ny funksjon som allerede er forespurt, kan du kommentere det på [GitHub Issues](https://github.com/Readarr/Readarr/issues) slik at arbeidet ikke blir duplisert (Hvis du vil legge til noe som ikke allerede er der, kan du snakke med oss først)
- Rebase fra Readarrs utviklingsgren, ikke merge
- Gjør meningsfulle commits, eller squash dem
- Du kan gjerne lage en pull request før arbeidet er ferdig. Dette lar oss se hvor det er og gi kommentarer/forslag til forbedringer
- Ta kontakt med oss på Discord hvis du har spørsmål
- Legg til tester (enhet/integrasjon)
- Commit med \*nix linjeskift for konsistens (Vi sjekker ut Windows og committer \*nix)
- Én funksjon/feilretting per pull request for å holde ting ryddig og enkelt å forstå
- Bruk 4 mellomrom i stedet for tabulatorer, dette er standarden for VS 2022 og WebStorm

## Pull-forespørsler

- Lag kun pull-forespørsler til `develop`, aldri `master`. Hvis du lager en PR til `master`, vil vi kommentere det og lukke det
- Du vil sannsynligvis få noen kommentarer eller spørsmål fra oss, de vil være for å sikre konsistens og vedlikeholdbarhet
- Vi vil prøve å svare på pull-forespørslene så raskt som mulig. Hvis det har gått en dag eller to, ta gjerne kontakt med oss, vi kan ha oversett det
- Hver PR skal komme fra sin egen [feature-gren](http://martinfowler.com/bliki/FeatureBranch.html) og ikke fra develop i din egen fork. Den skal ha et meningsfylt grennavn (hva som blir lagt til/fikset)
  - `new-feature` (Bra)
  - `fix-bug` (Bra)
  - `patch` (Dårlig)
  - `develop` (Dårlig)
- Commits skal skrives som `New:` eller `Fixed:` for endringer som ikke ville bli betraktet som en `vedlikeholdsutgivelse`

## Enhetstesting

Readarr bruker nunit for sin enhets-, integrasjons- og automatiseringstest-suite.

### Kjøre tester

Tester kan kjøres enkelt fra VS ved hjelp av den inkluderte nunit3testadapter nuget-pakken eller fra kommandolinjen ved hjelp av den inkluderte bash-scriptet `test.sh`.

I VS kan du bare navigere til Testutforskeren og kjøre eller debugge testene du vil undersøke.

Testene kan kjøres alle sammen eller en om gangen i VS.

Fra kommandolinjen tar `test.sh`-skriptet imot 3 parametere

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### Skrive tester

Selv om det ikke alltid er gøy, oppfordrer vi til å skrive enhetstester for alle endringer i backend-koden. Dette vil sikre at endringen fungerer som tiltenkt og at fremtidige endringer ikke bryter forventet atferd.

> Vi krever for øyeblikket 80% dekning på ny kode ved innsending av en PR
{.is-info}

Hvis du har spørsmål om noe av dette, gi oss beskjed.

# Oversettelse

Readarr bruker en selvhostet åpen tilgang [Weblate](https://translate.servarr.com)-instans for å administrere sine json-oversettelsesfiler. Disse filene er lagret i repoet på `src/NzbDrone.Core/Localization`

## Bidra til en eksisterende oversettelse

Weblate håndterer synkronisering og oversettelse av strenger for alle språk bortsett fra engelsk. Redigering av oversatte strenger og oversettelse av eksisterende strenger for støttede språk bør utføres der for Readarr-prosjektet.

Den engelske oversettelsen, `en.json`, fungerer som kilden for alle andre oversettelser og administreres på GitHub-repoet.

## Legge til et språk

Å legge til oversettelser til Readarr krever to trinn

- Legge til språket i weblate
- Legge til språket i Readarr-kodebasen

## Legge til oversettelsesstrenger i koden

Den engelske oversettelsen, `src/NzbDrone.Core/Localization/en.json`, fungerer som kilden for alle andre oversettelser og administreres på GitHub-repoet. Når du legger til en ny streng i enten brukergrensesnittet eller backend, må det også legges til en nøkkel i `en.json` sammen med standardverdien på engelsk. Denne nøkkelen kan deretter brukes som følger:

> PR-er for oversettelse av loggmeldinger vil ikke bli akseptert
{.is-warning}

### Backend-strenger

Backend-strenger kan legges til ved å bruke lokaliserings-tjenesten `GetLocalizedString`-metoden

```dotnet
private readonly ILocalizationService _localizationService;

public IndexerCheck(ILocalizationService localizationService)
{
  _localizationService = localizationService;
}
        
var translated = _localizationService.GetLocalizedString("IndexerHealthCheckNoIndexers")
```

### Frontend-strenger

Nye strenger kan legges til i frontend ved å importere oversettelsesfunksjonen og bruke en nøkkel som er spesifisert fra `en.json`

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```