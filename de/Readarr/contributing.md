---
title: Readarr Beitragende
description: 
published: true
date: 2022-09-26T15:56:42.368Z
tags: readarr, Entwicklung, Beitrag
editor: markdown
dateCreated: 2021-05-25T19:21:59.324Z
---

# Wie man beiträgt

Wir suchen immer nach Leuten, die Readarr noch besser machen möchten. Es gibt verschiedene Möglichkeiten, wie du einen Beitrag leisten kannst.

# Dokumentation

Einrichtungsanleitungen, [FAQ](/readarr/faq), je mehr Informationen wir im [Wiki](https://wiki.servarr.com/readarr) haben, desto besser.

# Entwicklung

Readarr ist in C# (Backend) und JS (Frontend) geschrieben. Das Backend basiert auf dem .NET6-Framework, während das Frontend Reactjs verwendet.

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

> Readarr wird **NICHT** auf älteren Versionen wie `10.x`, `8.x`, `6.x` oder einer Version unter 12.0 ausgeführt!
{.is-warning}

- [Yarn](https://yarnpkg.com/getting-started/install) wird zum Erstellen des Frontends benötigt
  - Yarn ist standardmäßig in **Node 16.10**+ enthalten. Aktiviere es mit `corepack enable`
  - Für andere Node-Versionen installiere es mit `npm i -g corepack`

## Erste Schritte

1. Fork Readarr
1. Klone das Repository auf deinen Entwicklungscomputer. [*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> Führe vor dem Committing von Frontend-Änderungen den Lint `yarn lint --fix` für deinen Code aus.
Für CSS-Änderungen `yarn stylelint-windows --fix` {.is-info}

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

Die Backend-Lösung lässt sich am einfachsten in Visual Studio oder Rider erstellen und ausführen. Wenn jedoch nur die Arbeit an der Frontend-Benutzeroberfläche im Vordergrund steht, kann sie auch problemlos über die Befehlszeile erstellt werden, wenn das richtige SDK installiert ist.

#### Visual Studio

> Stelle sicher, dass das Startprojekt auf `Readarr.Console` und das Framework auf `net6.0` eingestellt ist
{.is-info}

1. Baue die Lösung zuerst in Visual Studio. Dadurch werden alle Projekte korrekt erstellt und Abhängigkeiten wiederhergestellt.
1. Starte dann das Projekt in Visual Studio, um Readarr zu starten.
1. Öffne <http://localhost:8787>

#### Befehlszeile

1. Lösche die Lösung

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. Stelle die Wiederherstellung und den Build der Debug-Konfiguration für die richtige Plattform (Posix oder Windows) wieder her

```shell
dotnet msbuild -restore src/Readarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. Führe die erzeugte ausführbare Datei aus `/_output` aus

## Code beitragen

- Wenn du ein neues, bereits angefordertes Feature hinzufügst, kommentiere dies bitte in [GitHub Issues](https://github.com/Readarr/Readarr/issues), damit die Arbeit nicht doppelt gemacht wird (Wenn du etwas hinzufügen möchtest, das noch nicht dort steht, sprich bitte zuerst mit uns)
- Rebase von Readarr's Entwicklungsbranch, nicht mergen
- Mache aussagekräftige Commits oder squash sie
- Du kannst gerne einen Pull Request erstellen, bevor die Arbeit abgeschlossen ist. Dadurch können wir sehen, wo du stehst, und Kommentare machen/Verbesserungen vorschlagen
- Wende dich an uns im Discord, wenn du Fragen hast
- Füge Tests (Unit/Integration) hinzu
- Committe mit \*nix-Zeilenumbrüchen für Konsistenz (Wir checken Windows aus und commiten \*nix)
- Ein Feature/Bugfix pro Pull Request, um die Dinge sauber und leicht verständlich zu halten
- Verwende 4 Leerzeichen anstelle von Tabs, dies ist die Standardoption für VS 2022 und WebStorm

## Pull Request erstellen

- Erstelle Pull Requests nur für `develop`, niemals für `master`. Wenn du einen PR für `master` erstellst, werden wir darauf kommentieren und ihn schließen
- Du wirst wahrscheinlich einige Kommentare oder Fragen von uns erhalten, um Konsistenz und Wartbarkeit sicherzustellen
- Wir werden versuchen, so schnell wie möglich auf Pull Requests zu antworten. Wenn es einen Tag oder zwei gedauert hat, kontaktiere uns bitte, wir haben es möglicherweise übersehen
- Jeder PR sollte aus seinem eigenen [Feature-Branch](http://martinfowler.com/bliki/FeatureBranch.html) stammen, nicht aus dem develop-Zweig in deinem Fork. Er sollte einen aussagekräftigen Branch-Namen haben (was wird hinzugefügt/behoben)
  - `new-feature` (Gut)
  - `fix-bug` (Gut)
  - `patch` (Schlecht)
  - `develop` (Schlecht)
- Commits sollten als `New:` oder `Fixed:` für Änderungen geschrieben werden, die nicht als `Wartungsrelease` betrachtet werden würden

## Unit Testing

Readarr verwendet nunit für seine Unit-, Integrations- und Automatisierungstestsuite.

### Ausführen von Tests

Tests können einfach in VS mit dem enthaltenen nunit3testadapter NuGet-Paket oder über die Befehlszeile mit dem enthaltenen Bash-Skript `test.sh` ausgeführt werden.

In VS navigiere einfach zum Test Explorer und führe die Tests aus, die du untersuchen möchtest.

Tests können in VS alle auf einmal oder einzeln ausgeführt werden.

Über die Befehlszeile akzeptiert das `test.sh`-Skript 3 Parameter

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### Schreiben von Tests

Obwohl nicht immer spaßig, ermutigen wir das Schreiben von Unit-Tests für Backend-Code-Änderungen. Dadurch wird sichergestellt, dass die Änderung wie beabsichtigt funktioniert und dass zukünftige Änderungen das erwartete Verhalten nicht beeinträchtigen.

> Wir verlangen derzeit eine Abdeckung von 80% für neuen Code bei der Einreichung eines PRs
{.is-info}

Wenn du Fragen zu alldem hast, lass es uns bitte wissen.

# Übersetzung

Readarr verwendet eine selbst gehostete Open-Access-Instanz von [Weblate](https://translate.servarr.com), um seine JSON-Übersetzungsdateien zu verwalten. Diese Dateien werden im Repository unter `src/NzbDrone.Core/Localization` gespeichert.

## Beitrag zur bestehenden Übersetzung

Weblate übernimmt die Synchronisierung und Übersetzung von Zeichenketten für alle Sprachen außer Englisch. Die Bearbeitung von übersetzten Zeichenketten und die Übersetzung vorhandener Zeichenketten für unterstützte Sprachen sollten dort für das Readarr-Projekt durchgeführt werden.

Die englische Übersetzung, `en.json`, dient als Quelle für alle anderen Übersetzungen und wird im GitHub-Repository verwaltet.

## Hinzufügen einer Sprache

Das Hinzufügen von Übersetzungen zu Readarr erfordert zwei Schritte

- Hinzufügen der Sprache zu Weblate
- Hinzufügen der Sprache zum Readarr-Codebase

## Hinzufügen von Übersetzungszeichenketten im Code

Die englische Übersetzung, `src/NzbDrone.Core/Localization/en.json`, dient als Quelle für alle anderen Übersetzungen und wird im GitHub-Repository verwaltet. Beim Hinzufügen einer neuen Zeichenkette zur Benutzeroberfläche oder zum Backend muss auch ein Schlüssel zu `en.json` hinzugefügt werden, zusammen mit dem Standardwert in Englisch. Dieser Schlüssel kann dann wie folgt verwendet werden:

> Pull Requests für die Übersetzung von Protokollnachrichten werden nicht akzeptiert
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