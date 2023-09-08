---
title: Lidarr Bidrag
description: 
published: true
date: 2022-09-26T15:56:35.364Z
tags: lidarr, bidrag
editor: markdown
dateCreated: 2021-05-26T02:28:31.770Z
---

# Sådan bidrager du

Vi leder altid efter folk, der kan hjælpe med at gøre Lidarr endnu bedre, og der er flere måder at bidrage på.

# Dokumentation

Opsætningsguider, [FAQ](/lidarr/faq), jo mere information vi har på [wikien](https://wiki.servarr.com/lidarr), jo bedre.

# Udvikling

Lidarr er skrevet i C# (backend) og JS (frontend). Backenden er bygget på .NET6-frameworket, mens frontenden bruger Reactjs.

## Nødvendige værktøjer

- Visual Studio 2022 eller nyere anbefales (<https://www.visualstudio.com/vs/>). Community-versionen er gratis og virker (<https://www.visualstudio.com/downloads/>).

> VS 2022 V17.0 eller nyere anbefales, da det inkluderer .NET6 SDK
{.is-info}

- HTML/Javascript-editor efter eget valg (VS Code/Sublime Text/Webstorm/Atom/etc)
- [Git](https://git-scm.com/downloads)
- Kørselstiden for [Node.js](https://nodejs.org/) er påkrævet. Følgende versioner understøttes:
  - **12.0** eller nyere
  - **14.0** eller nyere
  - **16.0** eller nyere
{.grid-list}

> Lidarr vil **IKKE** køre på ældre versioner som `10.x`, `8.x`, `6.x` eller nogen version under 12.0!
{.is-warning}

- [Yarn](https://yarnpkg.com/getting-started/install) er påkrævet for at bygge frontenden
  - Yarn er inkluderet som standard med **Node 16.10**+. Aktivér det med `corepack enable`
  - For andre Node-versioner skal du installere det med `npm i -g corepack`

## Kom godt i gang

1. Fork Lidarr
1. Klon repositoryet til din udviklingsmaskine. [*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> Sørg for at køre lint `yarn lint --fix` på din kode for eventuelle ændringer i frontenden, før du committer.
For css-ændringer `yarn stylelint-windows --fix` {.is-info}

### Byg frontend

- Gå til den klonede mappe
- Installer de nødvendige Node-pakker

     ```bash
     yarn install
     ```

- Start webpack for at overvåge dit udviklingsmiljø for eventuelle ændringer, der kræver efterbehandling ved hjælp af:

     ```bash
     yarn start
     ```

### Byg backend

Backend-løsningen bygges og køres nemmest i Visual Studio eller Rider, men hvis den eneste prioritet er at arbejde på frontend-brugergrænsefladen, kan den også bygges nemt fra kommandolinjen, når den korrekte SDK er installeret.

#### Visual Studio

> Sørg for, at startprojektet er indstillet til `Lidarr.Console` og ramme til `net6.0`
{.is-info}

1. Byg først løsningen i Visual Studio, dette sikrer, at alle projekter bygges korrekt, og afhængighederne gendannes
1. Kør derefter projektet i Visual Studio for at starte Lidarr
1. Åbn <http://localhost:8686>

#### Kommandolinje

1. Ryd løsningen

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. Gendan og byg debugkonfigurationen for den korrekte platform (Posix eller Windows)

```shell
dotnet msbuild -restore src/Lidarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. Kør den producerede eksekverbare fil fra `/_output`

## Bidrag med kode

- Hvis du tilføjer en ny, allerede anmodet funktion, skal du kommentere det på [GitHub Issues](https://github.com/Lidarr/Lidarr/issues), så arbejdet ikke duplikeres (Hvis du vil tilføje noget, der ikke allerede er der, skal du tale med os først)
- Rebase fra Lidarr's develop-branch, ikke merge
- Lav meningsfulde commits eller squash dem
- Du er velkommen til at lave en pull request, før arbejdet er færdigt. Dette vil lade os se, hvor det er, og give kommentarer/forslag til forbedringer
- Kontakt os på Discord, hvis du har spørgsmål
- Tilføj tests (enheds-/integrationstests)
- Commit med \*nix-linjeslutninger for konsistens (Vi checker ud på Windows og committer \*nix)
- Én funktion/bugfix pr. pull request for at holde tingene rene og nemme at forstå
- Brug 4 mellemrum i stedet for tabulering, dette er standarden for VS 2022 og WebStorm

## Pull-anmodninger

- Lav kun pull-anmodninger til `develop`, aldrig `master`. Hvis du laver en PR til `master`, vil vi kommentere på den og lukke den
- Du får sandsynligvis nogle kommentarer eller spørgsmål fra os, de vil være for at sikre konsistens og vedligeholdelighed
- Vi vil forsøge at svare på pull-anmodninger så hurtigt som muligt. Hvis der er gået en dag eller to, bedes du kontakte os, vi kan have overset det
- Hver PR skal komme fra sin egen [feature-branch](http://martinfowler.com/bliki/FeatureBranch.html) og ikke fra develop i din fork. Den skal have et meningsfuldt branchenavn (hvad der tilføjes/rettes)
  - `new-feature` (Godt)
  - `fix-bug` (Godt)
  - `patch` (Dårligt)
  - `develop` (Dårligt)
- Commits skal skrives som `New:` eller `Fixed:` for ændringer, der ikke ville blive betragtet som en `maintenance release`

## Enhedstestning

Lidarr bruger nunit til sin enheds-, integration- og automatiseringstest-suite.

### Kørsel af tests

Tests kan køres nemt fra VS ved hjælp af den medfølgende nunit3testadapter-nuget-pakke eller fra kommandolinjen ved hjælp af den medfølgende bash-script `test.sh`.

I VS skal du blot navigere til Test Explorer og køre eller debugge de tests, du gerne vil undersøge.

Tests kan køres alle på én gang eller en ad gangen i VS.

Fra kommandolinjen accepterer `test.sh`-scriptet 3 parametre

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### Skrivning af tests

Selvom det ikke altid er sjovt, opfordrer vi til at skrive enhedstests for eventuelle ændringer i backend-koden. Dette sikrer, at ændringen fungerer, som du har til hensigt, og at fremtidige ændringer ikke bryder den forventede adfærd.

> Vi kræver i øjeblikket 80% dækning af ny kode ved indsendelse af en PR
{.is-info}

Hvis du har spørgsmål til noget af dette, så lad os det vide.

# Oversættelse

Lidarr bruger en selvhostet åben adgang [Weblate](https://translate.servarr.com)-instans til at administrere sine json-oversættelsesfiler. Disse filer er gemt i repoet på `src/NzbDrone.Core/Localization`

## Bidrag til en eksisterende oversættelse

Weblate håndterer synkronisering og oversættelse af strenge for alle sprog undtagen engelsk. Redigering af oversatte strenge og oversættelse af eksisterende strenge til understøttede sprog skal udføres der for Lidarr-projektet.

Den engelske oversættelse, `en.json`, fungerer som kilden til alle andre oversættelser og administreres på GitHub-repoet.

## Tilføjelse af et sprog

Tilføjelse af oversættelser til Lidarr kræver to trin

- Tilføjelse af sproget til weblate
- Tilføjelse af sproget til Lidarr-kodebasen

## Tilføjelse af oversættelsesstrenge i koden

Den engelske oversættelse, `src/NzbDrone.Core/Localization/en.json`, fungerer som kilden til alle andre oversættelser og administreres på GitHub-repoet. Når der tilføjes en ny streng til enten brugergrænsefladen eller backenden, skal der også tilføjes en nøgle til `en.json` sammen med standardværdien på engelsk. Denne nøgle kan derefter bruges som følger:

> PR'er til oversættelse af logbeskeder accepteres ikke
{.is-warning}

### Backend-strenge

Backend-strenge kan tilføjes ved hjælp af lokalisationstjenestens `GetLocalizedString`-metode

```dotnet
private readonly ILocalizationService _localizationService;

public IndexerCheck(ILocalizationService localizationService)
{
  _localizationService = localizationService;
}
        
var translated = _localizationService.GetLocalizedString("IndexerHealthCheckNoIndexers")
```

### Frontend-strenge

Nye strenge kan tilføjes til frontenden ved at importere oversættelsesfunktionen og bruge en nøgle, der er specificeret fra `en.json`

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```