---
title: Prowlarr Contributing
description: 
published: true
date: 2022-11-16T19:35:23.515Z
tags: prowlarr, development, contributing
editor: markdown
dateCreated: 2021-12-11T19:42:15.627Z
---

# Wie man beiträgt

Wir suchen immer nach Leuten, die helfen, Prowlarr noch besser zu machen. Es gibt verschiedene Möglichkeiten, wie du beitragen kannst.

# Dokumentation

Einrichtungsanleitungen, [FAQ](/prowlarr/faq), je mehr Informationen wir im [Wiki](https://wiki.servarr.com/prowlarr) haben, desto besser.

# Entwicklung

Prowlarr ist in C# (Backend) und JS (Frontend) geschrieben. Das Backend basiert auf dem .NET6-Framework, während das Frontend Reactjs verwendet.

## Benötigte Tools

- Visual Studio 2022 oder höher wird empfohlen (<https://www.visualstudio.com/vs/>). Die Community-Version ist kostenlos und funktioniert (<https://www.visualstudio.com/downloads/>).

> VS 2022 V17.0 oder höher wird empfohlen, da es das .NET6 SDK enthält
{.is-info}

- HTML/Javascript-Editor deiner Wahl (VS Code/Sublime Text/Webstorm/Atom/etc)
- [Git](https://git-scm.com/downloads)
- Die [Node.js](https://nodejs.org/) Runtime ist erforderlich. Die folgenden Versionen werden unterstützt:
  - **12.0** oder höher
  - **14.0** oder höher
  - **16.0** oder höher
{.grid-list}

> Prowlarr wird **NICHT** auf älteren Versionen wie `10.x`, `8.x`, `6.x` oder einer Version unter 12.0 ausgeführt!
{.is-warning}

- [Yarn](https://yarnpkg.com/getting-started/install) wird benötigt, um das Frontend zu erstellen
  - Yarn ist standardmäßig in **Node 16.10**+ enthalten. Aktiviere es mit `corepack enable`
  - Für andere Node-Versionen installiere es mit `npm i -g corepack`

## Erste Schritte

1. Fork Prowlarr
1. Klone das Repository auf deinen Entwicklungscomputer. [*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> Führe vor dem Committing von Frontend-Änderungen den Lint-Befehl `yarn lint --fix` für deinen Code aus.
Für CSS-Änderungen `yarn stylelint-windows --fix`
{.is-info}

### Erstellen des Frontends

- Navigiere zum geklonten Verzeichnis
- Installiere die erforderlichen Node-Pakete

     ```bash
     yarn install
     ```

- Starte Webpack, um deine Entwicklungsumgebung auf Änderungen zu überwachen, die eine Nachverarbeitung erfordern:

     ```bash
     yarn start
     ```

### Erstellen des Backends

Die Backend-Lösung kann am einfachsten in Visual Studio oder Rider erstellt und ausgeführt werden. Wenn jedoch nur die Arbeit an der Frontend-Benutzeroberfläche Priorität hat, kann sie auch über die Befehlszeile einfach erstellt werden, wenn das richtige SDK installiert ist.

#### Visual Studio

> Stelle sicher, dass das Startprojekt auf `Prowlarr.Console` und das Framework auf `net6.0` eingestellt ist
{.is-info}

1. Baue die Lösung in Visual Studio, um sicherzustellen, dass alle Projekte korrekt erstellt und Abhängigkeiten wiederhergestellt werden
1. Starte das Projekt in Visual Studio, um Prowlarr zu starten
1. Öffne <http://localhost:9696>

#### Befehlszeile

1. Lösche die Lösung

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. Stelle die Wiederherstellung und den Build der Debug-Konfiguration für die richtige Plattform (Posix oder Windows) wieder her

```shell
dotnet msbuild -restore src/Prowlarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. Führe die erstellbare Datei aus dem Verzeichnis `/_output` aus

## Code beitragen

- Wenn du ein neues, bereits angefordertes Feature hinzufügst, kommentiere bitte auf [GitHub Issues](https://github.com/Prowlarr/Prowlarr/issues), damit die Arbeit nicht dupliziert wird (Wenn du etwas hinzufügen möchtest, das noch nicht dort steht, sprich bitte zuerst mit uns)
- Rebase von Prowlarr's develop-Zweig, nicht mergen
- Mache aussagekräftige Commits oder squash sie
- Du kannst gerne einen Pull Request erstellen, bevor die Arbeit abgeschlossen ist. Dadurch können wir sehen, wo sie steht, und Kommentare abgeben/Verbesserungen vorschlagen
- Wende dich an uns im Discord, wenn du Fragen hast
- Füge Tests (Unit/Integration) hinzu
- Committe mit \*nix-Zeilenumbrüchen für Konsistenz (Wir checken Windows aus und commiten \*nix)
- Ein Feature/Bugfix pro Pull Request, um die Dinge sauber und leicht verständlich zu halten
- Verwende 4 Leerzeichen anstelle von Tabs, dies ist die Standardeinstellung für VS 2022 und WebStorm

### Indexer beitragen

### C# Indexer

- C# Indexer sollten als Pull Request an das [Prowlarr App Repository](https://github.com/prowlarr/prowlarr) gegen den `develop`-Zweig gestellt werden
- Wenn du einen C# Indexer beiträgst, formuliere deinen Commit bitte wie folgt: `New: (Indexer) {Indexer Name}`, `New: (Indexer) {Usenet|Torrent} {Indexer Name}`, `New: (Indexer) {Torznab|Newznab} {Indexer Name}`
- Wenn du einen C# Indexer aktualisierst, formuliere deinen Commit bitte wie folgt: `Fixed: (Indexer) {Indexer Name} {Änderungen}` z.B. `Fixed: (Indexer) Changed BHD to use API`

### Cardigann (YML) Indexer

- Cardigann- und YML-Indexer sollten als Pull Request an das [Prowlarr Indexer Repository](https://github.com/prowlarr/indexers) gegen den `master`-Zweig gestellt werden
- Für Cardigann/YML-Indexer-Details siehe [die Definition und Beschreibung des Prowlarr Cardigann yml-Formats](/prowlarr/cardigann-yml-definition)
- Für das Testen von benutzerdefinierten yml-Definitionen siehe [den Abschnitt Benutzerdefinierte yml in der Indexer-Seite](/prowlarr/indexers#adding-a-custom-yml-definition)

## Pull Request erstellen

- Mache Pull Requests nur an `develop`, niemals an `master`. Wenn du einen PR an `master` erstellst, werden wir darauf kommentieren und ihn schließen
- Du wirst wahrscheinlich einige Kommentare oder Fragen von uns bekommen, um Konsistenz und Wartbarkeit sicherzustellen
- Wir werden versuchen, auf Pull Requests so schnell wie möglich zu antworten. Wenn es ein oder zwei Tage gedauert hat, kontaktiere uns bitte, wir haben es möglicherweise übersehen
- Jeder PR sollte aus seinem eigenen [Feature-Zweig](http://martinfowler.com/bliki/FeatureBranch.html) in deinem Fork stammen, er sollte einen aussagekräftigen Branch-Namen haben (was wird hinzugefügt/behoben)
  - `new-feature` (Gut)
  - `fix-bug` (Gut)
  - `patch` (Schlecht)
  - `develop` (Schlecht)
- Commits sollten als `New:` oder `Fixed:` für Änderungen geschrieben werden, die nicht als `Wartungsrelease` betrachtet werden würden

## Unit Testing

Prowlarr verwendet nunit für seine Unit-, Integration- und Automatisierungstestsuite.

### Tests ausführen

Tests können einfach von Visual Studio aus mit dem enthaltenen nunit3testadapter NuGet-Paket oder von der Befehlszeile aus mit dem enthaltenen Bash-Skript `test.sh` ausgeführt werden.

In Visual Studio navigiere einfach zum Test Explorer und führe die Tests aus, die du untersuchen möchtest.

Tests können in Visual Studio alle auf einmal oder einzeln ausgeführt werden.

Von der Befehlszeile aus akzeptiert das `test.sh`-Skript 3 Parameter

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### Tests schreiben

Obwohl nicht immer spaßig, ermutigen wir das Schreiben von Unit-Tests für alle Backend-Code-Änderungen. Dadurch wird sichergestellt, dass die Änderung wie beabsichtigt funktioniert und dass zukünftige Änderungen das erwartete Verhalten nicht beeinträchtigen.

> Wir verlangen derzeit eine Testabdeckung von 80% für neuen Code bei der Einreichung eines PRs
{.is-info}

Wenn du Fragen zu alldem hast, lass es uns bitte wissen.

# Übersetzung

Prowlarr verwendet eine selbst gehostete Open-Access-[Weblate](https://translate.servarr.com)-Instanz zur Verwaltung seiner JSON-Übersetzungsdateien. Diese Dateien werden im Repository unter `src/NzbDrone.Core/Localization` gespeichert.

## Beitrag zu einer vorhandenen Übersetzung

Weblate übernimmt die Synchronisierung und Übersetzung von Zeichenketten für alle Sprachen außer Englisch. Die Bearbeitung von übersetzten Zeichenketten und die Übersetzung vorhandener Zeichenketten für unterstützte Sprachen sollten dort für das Prowlarr-Projekt durchgeführt werden.

Die englische Übersetzung, `en.json`, dient als Quelle für alle anderen Übersetzungen und wird im GitHub-Repository verwaltet.

## Hinzufügen einer Sprache

Das Hinzufügen von Übersetzungen zu Prowlarr erfordert zwei Schritte

- Hinzufügen der Sprache zu Weblate
- Hinzufügen der Sprache zum Prowlarr-Codebase

## Hinzufügen von Übersetzungszeichenketten im Code

Die englische Übersetzung, `src/NzbDrone.Core/Localization/en.json`, dient als Quelle für alle anderen Übersetzungen und wird im GitHub-Repository verwaltet. Wenn du eine neue Zeichenkette sowohl für die Benutzeroberfläche als auch für das Backend hinzufügst, muss auch ein Schlüssel zu `en.json` hinzugefügt werden, zusammen mit dem Standardwert in Englisch. Dieser Schlüssel kann dann wie folgt verwendet werden:

> PRs für die Übersetzung von Protokollmeldungen werden nicht akzeptiert
{.is-warning}

### Backend-Zeichenketten

Backend-Zeichenketten können mit der Methode `GetLocalizedString` des Localization Service hinzugefügt werden

```dotnet
private readonly ILocalizationService _localizationService;

public IndexerCheck(ILocalizationService localizationService)
{
  _localizationService = localizationService;
}
        
var translated = _localizationService.GetLocalizedString("IndexerHealthCheckNoIndexers")
```

### Frontend-Zeichenketten

Neue Zeichenketten können im Frontend hinzugefügt werden, indem die Übersetzungsfunktion importiert und ein Schlüssel aus `en.json` verwendet wird

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```