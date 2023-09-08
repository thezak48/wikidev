---
title: Sonarr Mitwirken
description: 
published: true
date: 2023-09-03T13:55:05.394Z
tags: sonarr
editor: markdown
dateCreated: 2021-06-11T23:10:04.820Z
---

# Wie man mitwirken kann

Wir suchen immer nach Leuten, die Sonarr noch besser machen wollen. Es gibt verschiedene Möglichkeiten, wie du mitwirken kannst.

# Dokumentation

Einrichtungsanleitungen, [FAQ](/sonarr/faq), je mehr Informationen wir im [Wiki](https://wiki.servarr.com/sonarr) haben, desto besser.

# Entwicklung

Sonarr ist in C# (Backend) und JS (Frontend) geschrieben. Das Backend basiert auf dem .NET6-Framework, während das Frontend Reactjs verwendet.

## Benötigte Tools

- Visual Studio 2022 oder höher wird empfohlen (<https://www.visualstudio.com/vs/>). Die Community-Version ist kostenlos und funktioniert (<https://www.visualstudio.com/downloads/>).

> VS 2022 V17.0 oder höher wird empfohlen, da es das .NET6 SDK enthält
{.is-info}

- HTML/Javascript-Editor deiner Wahl (VS Code/Sublime Text/Webstorm/Atom/etc)
- [Git](https://git-scm.com/downloads)
- Die [Node.js](https://nodejs.org/) Runtime wird benötigt. Die folgenden Versionen werden unterstützt:
  - **12.0** oder höher
  - **14.0** oder höher
  - **16.0** oder höher
{.grid-list}

> Sonarr wird **NICHT** auf älteren Versionen wie `10.x`, `8.x`, `6.x` oder jeder Version unter 12.0 ausgeführt!
{.is-warning}

- [Yarn](https://yarnpkg.com/getting-started/install) wird benötigt, um das Frontend zu erstellen
  - Yarn ist standardmäßig in **Node 16.10**+ enthalten. Aktiviere es mit `corepack enable`
  - Für andere Node-Versionen installiere es mit `npm i -g corepack`

## Erste Schritte

1. Fork Sonarr
1. Klone das Repository auf deinen Entwicklungscomputer. [*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> Führe vor dem Committing von Frontend-Änderungen den Lint-Befehl `yarn lint --fix` für deinen Code aus.
Für CSS-Änderungen `yarn stylelint-windows --fix` ausführen {.is-info}

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

Die Backend-Lösung kann am einfachsten in Visual Studio oder Rider erstellt und ausgeführt werden. Wenn jedoch nur die Arbeit an der Frontend-Benutzeroberfläche Priorität hat, kann sie auch über die Befehlszeile erstellt werden, wenn das richtige SDK installiert ist.

#### Visual Studio

> Stelle sicher, dass das Startprojekt auf `Sonarr.Console` und das Framework auf `net6.0` eingestellt ist
{.is-info}

1. Baue die Lösung zuerst in Visual Studio. Dadurch werden alle Projekte korrekt erstellt und Abhängigkeiten wiederhergestellt.
1. Starte dann das Projekt in Visual Studio im Debug-Modus, um Sonarr zu starten.
1. Öffne <http://localhost:8989>

#### Befehlszeile

1. Lösche die Lösung

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. Stelle die Wiederherstellung und den Build der Debug-Konfiguration für die richtige Plattform (Posix oder Windows) wieder her

```shell
dotnet msbuild -restore src/Sonarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. Führe die erzeugte ausführbare Datei aus `/_output` aus

## Code beitragen

- Wenn du ein neues, bereits angefordertes Feature hinzufügst, kommentiere dies bitte in [GitHub Issues](https://github.com/Sonarr/Sonarr/issues), damit die Arbeit nicht dupliziert wird (Wenn du etwas hinzufügen möchtest, das noch nicht dort steht, sprich bitte zuerst mit uns)
- Rebase von Sonarr's Entwicklungsbranch, nicht mergen
- Mache aussagekräftige Commits oder squash sie
- Du kannst gerne einen Pull Request erstellen, bevor die Arbeit abgeschlossen ist. Dadurch können wir sehen, wo sie steht, und Kommentare abgeben/Verbesserungen vorschlagen
- Wende dich an uns im Discord, wenn du Fragen hast
- Füge Tests (Unit/Integration) hinzu
- Committe mit \*nix-Zeilenumbrüchen für Konsistenz (Wir überprüfen Windows und commiten \*nix)
- Ein Feature/Bugfix pro Pull Request, um die Dinge sauber und leicht verständlich zu halten
- Verwende 4 Leerzeichen anstelle von Tabs, dies ist die Standardeinstellung für VS 2022 und WebStorm

## Pull Request erstellen

- Erstelle Pull Requests nur für `develop`, niemals für `main`. Wenn du einen PR für `main` erstellst, werden wir darauf kommentieren und ihn schließen
- Du wirst wahrscheinlich einige Kommentare oder Fragen von uns erhalten, um Konsistenz und Wartbarkeit sicherzustellen
- Wir werden versuchen, auf Pull Requests so schnell wie möglich zu antworten. Wenn es ein oder zwei Tage gedauert hat, kontaktiere uns bitte im Discord, wir haben es möglicherweise übersehen
- Jeder PR sollte aus seinem eigenen [Feature-Branch](http://martinfowler.com/bliki/FeatureBranch.html) stammen, nicht aus `develop` in deinem Fork. Er sollte einen aussagekräftigen Branch-Namen haben (was wird hinzugefügt/behoben)
  - `new-feature` (Gut)
  - `fix-bug` (Gut)
  - `patch` (Schlecht)
  - `develop` (Schlecht)
- Commits sollten als `New:` oder `Fixed:` für Änderungen geschrieben werden, die nicht als `Wartungsrelease` betrachtet werden würden

## Unit Testing

Sonarr verwendet nunit für seine Unit-, Integrations- und Automatisierungstestsuite.

### Ausführen von Tests

Tests können einfach in VS mit dem mitgelieferten nunit3testadapter NuGet-Paket oder über die Befehlszeile mit dem mitgelieferten Bash-Skript `test.sh` ausgeführt werden.

In VS navigiere einfach zum Test Explorer und führe die Tests aus, die du untersuchen möchtest.

Tests können in VS alle auf einmal oder einzeln ausgeführt werden.

Über die Befehlszeile akzeptiert das `test.sh`-Skript 3 Parameter

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### Schreiben von Tests

Obwohl nicht immer spaßig, ermutigen wir das Schreiben von Unit-Tests für alle Backend-Code-Änderungen. Dadurch wird sichergestellt, dass die Änderung wie beabsichtigt funktioniert und dass zukünftige Änderungen das erwartete Verhalten nicht beeinträchtigen.

> Wir verlangen derzeit eine Abdeckung von 80% für neuen Code bei der Einreichung eines PRs
{.is-info}

Wenn du Fragen zu alldem hast, lass es uns bitte wissen.

# Übersetzung

Sonarr verwendet eine selbst gehostete Open-Access-[Weblate](https://translate.servarr.com)-Instanz zur Verwaltung seiner JSON-Übersetzungsdateien. Diese Dateien werden im Repository unter `src/NzbDrone.Core/Localization` gespeichert.

## Beitrag zu einer vorhandenen Übersetzung

Weblate kümmert sich um die Synchronisierung und Übersetzung von Zeichenketten für alle Sprachen außer Englisch. Die Bearbeitung von übersetzten Zeichenketten und die Übersetzung vorhandener Zeichenketten für unterstützte Sprachen sollten dort für das Sonarr-Projekt durchgeführt werden.

Die englische Übersetzung, `en.json`, dient als Quelle für alle anderen Übersetzungen und wird im GitHub-Repository verwaltet.

## Hinzufügen einer Sprache

Das Hinzufügen von Übersetzungen zu Sonarr erfordert zwei Schritte

- Hinzufügen der Sprache zu Weblate
- Hinzufügen der Sprache zum Sonarr-Codebase

## Hinzufügen von Übersetzungszeichenketten im Code

Die englische Übersetzung, `src/NzbDrone.Core/Localization/en.json`, dient als Quelle für alle anderen Übersetzungen und wird im GitHub-Repository verwaltet. Beim Hinzufügen einer neuen Zeichenkette zur Benutzeroberfläche oder zum Backend muss auch ein Schlüssel zu `en.json` hinzugefügt werden, zusammen mit dem Standardwert in Englisch. Dieser Schlüssel kann dann wie folgt verwendet werden:

> PRs für die Übersetzung von Protokollnachrichten werden nicht akzeptiert
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