---
title: Readarr Bidragande
description: 
published: true
date: 2022-09-26T15:56:42.368Z
tags: readarr, utveckling, bidragande
editor: markdown
dateCreated: 2021-05-25T19:21:59.324Z
---

# Hur man bidrar

Vi letar alltid efter människor som kan hjälpa till att göra Readarr ännu bättre, och det finns flera sätt att bidra på.

# Dokumentation

Installationsguider, [FAQ](/readarr/faq), ju mer information vi har på [wikin](https://wiki.servarr.com/readarr), desto bättre.

# Utveckling

Readarr är skrivet i C# (backend) och JS (frontend). Backend är byggt på .NET6-ramverket, medan frontend använder Reactjs.

## Verktyg som krävs

- Visual Studio 2022 eller senare rekommenderas (<https://www.visualstudio.com/vs/>). Community-versionen är gratis och fungerar (<https://www.visualstudio.com/downloads/>).

> VS 2022 V17.0 eller senare rekommenderas eftersom det inkluderar .NET6 SDK
{.is-info}

- HTML/Javascript-redigerare (VS Code/Sublime Text/Webstorm/Atom/etc)
- [Git](https://git-scm.com/downloads)
- Körningsmiljön [Node.js](https://nodejs.org/) krävs. Följande versioner stöds:
  - **12.0** eller senare
  - **14.0** eller senare
  - **16.0** eller senare
{.grid-list}

> Readarr kommer **INTE** att köras på äldre versioner som `10.x`, `8.x`, `6.x` eller någon version under 12.0!
{.is-warning}

- [Yarn](https://yarnpkg.com/getting-started/install) krävs för att bygga frontend
  - Yarn ingår som standard med **Node 16.10**+. Aktivera det med `corepack enable`
  - För andra Node-versioner, installera det med `npm i -g corepack`

## Komma igång

1. Forka Readarr
1. Klona repositoryt till din utvecklingsmaskin. [*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> Se till att köra lint `yarn lint --fix` på din kod för eventuella ändringar i frontend innan du gör en commit.
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

> Se till att startprojektet är inställt på `Readarr.Console` och ramverket på `net6.0`
{.is-info}

1. Bygg först lösningen i Visual Studio, detta kommer att se till att alla projekt byggs korrekt och att beroenden återställs
1. Kör sedan projektet i Visual Studio för att starta Readarr
1. Öppna <http://localhost:8787>

#### Kommandorad

1. Rensa lösningen

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. Återställ och bygg debug-konfigurationen för rätt plattform (Posix eller Windows)

```shell
dotnet msbuild -restore src/Readarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. Kör den genererade körbara filen från `/_output`

## Bidra med kod

- Om du lägger till en ny, redan begärd funktion, kommentera gärna på [GitHub Issues](https://github.com/Readarr/Readarr/issues) så att arbetet inte dupliceras (Om du vill lägga till något som inte redan finns där, prata gärna med oss först)
- Rebase från Readarrs utvecklingsgren, gör inte en merge
- Gör meningsfulla commits, eller squasha dem
- Du är välkommen att göra en pull request innan arbetet är klart, detta låter oss se var det är och göra kommentarer/föreslå förbättringar
- Kontakta oss på Discord om du har några frågor
- Lägg till tester (enhet/integration)
- Commita med \*nix-radslut för konsekvens (Vi checkar ut Windows och commitar \*nix)
- En funktion/bugfix per pull request för att hålla det rent och lätt att förstå
- Använd 4 mellanslag istället för tabbar, detta är standard för VS 2022 och WebStorm

## Pull-begäran

- Gör bara pull-begäran till `develop`, aldrig till `master`, om du gör en PR till `master` kommer vi att kommentera och stänga den
- Du kommer förmodligen att få några kommentarer eller frågor från oss, de kommer att vara för att säkerställa konsekvens och underhållbarhet
- Vi försöker svara på pull-begäran så snart som möjligt, om det har gått en eller två dagar, kontakta oss, vi kanske har missat det
- Varje PR ska komma från sin egen [feature branch](http://martinfowler.com/bliki/FeatureBranch.html) inte från develop i din fork, den ska ha ett meningsfullt namn på branchen (vad som läggs till/fixas)
  - `new-feature` (Bra)
  - `fix-bug` (Bra)
  - `patch` (Dåligt)
  - `develop` (Dåligt)
- Commits ska skrivas som `New:` eller `Fixed:` för ändringar som inte skulle betraktas som en `maintenance release`

## Enhetstestning

Readarr använder nunit för sina enhets-, integrations- och automatiseringstest.

### Körning av tester

Tester kan köras enkelt från VS med hjälp av det medföljande nunit3testadapter-nuget-paketet eller från kommandoraden med hjälp av den medföljande bash-skriptet `test.sh`.

I VS navigerar du helt enkelt till Test Explorer och kör eller debuggar de tester du vill undersöka.

Testerna kan köras alla på en gång eller en i taget i VS.

Från kommandoraden tar `test.sh`-skriptet emot 3 parametrar

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### Skrivning av tester

Även om det inte alltid är roligt, uppmuntrar vi att skriva enhetstester för alla ändringar i backend-koden. Detta kommer att säkerställa att ändringen fungerar som avsett och att framtida ändringar inte bryter den förväntade beteendet.

> Vi kräver för närvarande 80% täckning på ny kod vid inlämning av en PR
{.is-info}

Om du har några frågor om något av detta, låt oss veta.

# Översättning

Readarr använder en självhostad öppen tillgång [Weblate](https://translate.servarr.com)-instans för att hantera sina json-översättningsfiler. Dessa filer lagras i repot på `src/NzbDrone.Core/Localization`

## Bidra till en befintlig översättning

Weblate hanterar synkronisering och översättning av strängar för alla språk utom engelska. Redigering av översatta strängar och översättning av befintliga strängar för stödda språk bör utföras där för Readarr-projektet.

Den engelska översättningen, `en.json`, fungerar som källan för alla andra översättningar och hanteras på GitHub-repot.

## Lägga till ett språk

Att lägga till översättningar till Readarr kräver två steg

- Lägga till språket i weblate
- Lägga till språket i Readarr-kodbasen

## Lägga till översättningssträngar i koden

Den engelska översättningen, `src/NzbDrone.Core/Localization/en.json`, fungerar som källan för alla andra översättningar och hanteras på GitHub-repot. När du lägger till en ny sträng i antingen gränssnittet eller backenden måste en nyckel också läggas till i `en.json` tillsammans med standardvärdet på engelska. Denna nyckel kan sedan användas på följande sätt:

> PR:er för översättning av loggmeddelanden kommer inte att accepteras
{.is-warning}

### Backend-strängar

Backend-strängar kan läggas till genom att använda lokaliserings-tjänstens `GetLocalizedString`-metod

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