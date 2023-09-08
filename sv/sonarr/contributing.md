---
title: Sonarr Bidragande
description: 
published: true
date: 2023-09-03T13:55:05.394Z
tags: sonarr
editor: markdown
dateCreated: 2021-06-11T23:10:04.820Z
---

# Hur man bidrar

Vi letar alltid efter personer som kan hjälpa till att göra Sonarr ännu bättre, och det finns flera sätt att bidra på.

# Dokumentation

Installationsguider, [FAQ](/sonarr/faq), ju mer information vi har på [wikin](https://wiki.servarr.com/sonarr), desto bättre.

# Utveckling

Sonarr är skrivet i C# (backend) och JS (frontend). Backend är byggt på .NET6-ramverket, medan frontend använder Reactjs.

## Verktyg som krävs

- Visual Studio 2022 eller senare rekommenderas (<https://www.visualstudio.com/vs/>). Community-versionen är gratis och fungerar (<https://www.visualstudio.com/downloads/>).

> VS 2022 V17.0 eller senare rekommenderas eftersom det inkluderar .NET6 SDK
{.is-info}

- HTML/Javascript-redigerare efter eget val (VS Code/Sublime Text/Webstorm/Atom/etc)
- [Git](https://git-scm.com/downloads)
- Körningsmiljön [Node.js](https://nodejs.org/) krävs. Följande versioner stöds:
  - **12.0** eller senare
  - **14.0** eller senare
  - **16.0** eller senare
{.grid-list}

> Sonarr kommer **INTE** att köras på äldre versioner som `10.x`, `8.x`, `6.x` eller någon version under 12.0!
{.is-warning}

- [Yarn](https://yarnpkg.com/getting-started/install) krävs för att bygga frontend
  - Yarn ingår som standard med **Node 16.10**+. Aktivera det med `corepack enable`
  - För andra Node-versioner, installera det med `npm i -g corepack`

## Komma igång

1. Forka Sonarr
1. Klona repositoryt till din utvecklingsmaskin. [*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> Se till att köra lint `yarn lint --fix` på din kod för eventuella ändringar i frontend innan du commitar.
För css-ändringar `yarn stylelint-windows --fix` {.is-info}

### Bygga frontend

- Navigera till den klonade mappen
- Installera de nödvändiga Node-paketen

     ```bash
     yarn install
     ```

- Starta webpack för att övervaka din utvecklingsmiljö för eventuella ändringar som behöver efterbehandlas med:

     ```bash
     yarn start
     ```

### Bygga backend

Backend-lösningen byggs och körs enklast i Visual Studio eller Rider, men om den enda prioriteringen är att arbeta med frontend-gränssnittet kan den byggas enkelt från kommandoraden när rätt SDK är installerat.

#### Visual Studio

> Se till att startprojektet är inställt på `Sonarr.Console` och ramverket på `net6.0`
{.is-info}

1. Bygg först lösningen i Visual Studio, detta kommer att se till att alla projekt byggs korrekt och att beroenden återställs
1. Kör sedan projektet i Visual Studio för att starta Sonarr
1. Öppna <http://localhost:8989>

#### Kommandorad

1. Rensa lösningen

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. Återställ och bygg debug-konfigurationen för rätt plattform (Posix eller Windows)

```shell
dotnet msbuild -restore src/Sonarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. Kör den producerade körbara filen från `/_output`

## Bidra med kod

- Om du lägger till en ny, redan begärd funktion, kommentera gärna på [GitHub Issues](https://github.com/Sonarr/Sonarr/issues) så att arbetet inte dupliceras (Om du vill lägga till något som inte redan finns där, prata med oss först)
- Rebase från Sonarrs utvecklingsgren, gör inte en merge
- Gör meningsfulla commits, eller squash dem
- Du är välkommen att göra en pull request innan arbetet är klart, detta låter oss se var det är och göra kommentarer/föreslå förbättringar
- Kontakta oss på Discord om du har några frågor
- Lägg till tester (enhet/integration)
- Commita med \*nix-radslut för konsekvens (Vi kollar ut Windows och commitar \*nix)
- En funktion/bugfix per pull request för att hålla det rent och lätt att förstå
- Använd 4 mellanslag istället för tabbar, detta är standardinställningen för VS 2022 och WebStorm

## Pull Request

- Gör bara pull requests till `develop`, aldrig till `main`, om du gör en PR till `main` kommer vi att kommentera på den och stänga den
- Du kommer förmodligen att få några kommentarer eller frågor från oss, de kommer att vara för att säkerställa konsekvens och underhållbarhet
- Vi försöker svara på pull requests så snart som möjligt, om det har gått en eller två dagar, kontakta oss på Discord, vi kanske har missat det
- Varje PR ska komma från sin egen [feature branch](http://martinfowler.com/bliki/FeatureBranch.html) inte från develop i din fork, den ska ha ett meningsfullt namn på branchen (vad som läggs till/fixas)
  - `new-feature` (Bra)
  - `fix-bug` (Bra)
  - `patch` (Dåligt)
  - `develop` (Dåligt)
- Commits ska skrivas som `New:` eller `Fixed:` för ändringar som inte skulle betraktas som en `maintenance release`

## Enhetstestning

Sonarr använder nunit för sina enhets-, integrations- och automatiseringstest.

### Körning av tester

Tester kan köras enkelt från VS med hjälp av den medföljande nunit3testadapter-nugetpaketet eller från kommandoraden med hjälp av den medföljande bash-skriptet `test.sh`.

I VS navigerar du helt enkelt till Test Explorer och kör eller debuggar de tester du vill undersöka.

I VS kan tester köras alla på en gång eller en i taget.

Från kommandoraden tar `test.sh`-skriptet emot 3 parametrar

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### Skrivning av tester

Även om det inte alltid är roligt, uppmuntrar vi att skriva enhetstester för alla ändringar i backend-koden. Detta kommer att säkerställa att ändringen fungerar som avsett och att framtida ändringar inte bryter förväntat beteende.

> Vi kräver för närvarande 80% täckning på ny kod vid inlämning av en PR
{.is-info}

Om du har några frågor om något av detta, låt oss veta.

# Översättning

Sonarr använder en självhostad öppen [Weblate](https://translate.servarr.com)-instans för att hantera sina json-översättningsfiler. Dessa filer lagras i repoet på `src/NzbDrone.Core/Localization`

## Bidra till en befintlig översättning

Weblate hanterar synkronisering och översättning av strängar för alla språk utom engelska. Redigering av översatta strängar och översättning av befintliga strängar för stödda språk bör utföras där för Sonarr-projektet.

Den engelska översättningen, `en.json`, fungerar som källan för alla andra översättningar och hanteras på GitHub-repot.

## Lägga till ett språk

Att lägga till översättningar till Sonarr kräver två steg

- Lägga till språket i weblate
- Lägga till språket i Sonarr-kodbasen

## Lägga till översättningssträngar i koden

Den engelska översättningen, `src/NzbDrone.Core/Localization/en.json`, fungerar som källan för alla andra översättningar och hanteras på GitHub-repot. När du lägger till en ny sträng i antingen gränssnittet eller backenden måste en nyckel också läggas till i `en.json` tillsammans med standardvärdet på engelska. Denna nyckel kan sedan användas på följande sätt:

> PR:er för översättning av loggmeddelanden kommer inte att accepteras
{.is-warning}

### Backend-strängar

Backend-strängar kan läggas till genom att använda lokaliseringsfunktionen `GetLocalizedString` i lokaliserings-tjänsten

```dotnet
private readonly ILocalizationService _localizationService;

public IndexerCheck(ILocalizationService localizationService)
{
  _localizationService = localizationService;
}
        
var translated = _localizationService.GetLocalizedString("IndexerHealthCheckNoIndexers")
```

### Frontend-strängar

Nya strängar kan läggas till i frontend genom att importera översättningsfunktionen och använda en nyckel som anges från `en.json`

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```