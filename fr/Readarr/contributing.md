---
title: Contribution à Readarr
description: 
published: true
date: 2022-09-26T15:56:42.368Z
tags: readarr, développement, contribution
editor: markdown
dateCreated: 2021-05-25T19:21:59.324Z
---

# Comment contribuer

Nous sommes toujours à la recherche de personnes pour aider à améliorer Readarr, et il existe plusieurs façons de contribuer.

# Documentation

Les guides d'installation, les [FAQ](/readarr/faq), plus nous avons d'informations sur le [wiki](https://wiki.servarr.com/readarr), mieux c'est.

# Développement

Readarr est écrit en C# (backend) et JS (frontend). Le backend est construit sur le framework .NET6, tandis que le frontend utilise Reactjs.

## Outils requis

- Visual Studio 2022 ou supérieur est recommandé (<https://www.visualstudio.com/vs/>). La version communautaire est gratuite et fonctionne (<https://www.visualstudio.com/downloads/>).

> VS 2022 V17.0 ou supérieur est recommandé car il inclut le SDK .NET6
{.is-info}

- Éditeur HTML/Javascript de votre choix (VS Code/Sublime Text/Webstorm/Atom/etc)
- [Git](https://git-scm.com/downloads)
- L'exécution de [Node.js](https://nodejs.org/) est requise. Les versions suivantes sont prises en charge :
  - **12.0** ou ultérieure
  - **14.0** ou ultérieure
  - **16.0** ou ultérieure
{.grid-list}

> Readarr ne fonctionnera **PAS** sur des versions plus anciennes telles que `10.x`, `8.x`, `6.x` ou toute version inférieure à 12.0 !
{.is-warning}

- [Yarn](https://yarnpkg.com/getting-started/install) est requis pour construire le frontend
  - Yarn est inclus avec **Node 16.10**+ par défaut. Activez-le avec `corepack enable`
  - Pour les autres versions de Node, installez-le avec `npm i -g corepack`

## Pour commencer

1. Fork Readarr
1. Clonez le dépôt sur votre machine de développement. [*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> Assurez-vous d'exécuter `yarn lint --fix` sur votre code pour tout changement du frontend avant de valider.
Pour les changements de CSS, exécutez `yarn stylelint-windows --fix` {.is-info}

### Construction du frontend

- Accédez au répertoire cloné
- Installez les packages Node requis

     ```bash
     yarn install
     ```

- Démarrez webpack pour surveiller votre environnement de développement et effectuer les modifications nécessitant un post-traitement :

     ```bash
     yarn start
     ```

### Construction du backend

La solution backend est plus facilement construite et exécutée dans Visual Studio ou Rider. Cependant, si la seule priorité est de travailler sur l'interface utilisateur frontend, elle peut également être construite facilement à partir de la ligne de commande lorsque le SDK correct est installé.

#### Visual Studio

> Assurez-vous que le projet de démarrage est défini sur `Readarr.Console` et le framework sur `net6.0`
{.is-info}

1. Commencez par `Build` la solution dans Visual Studio, cela garantira que tous les projets sont correctement construits et que les dépendances sont restaurées
1. Ensuite, `Debug/Run` le projet dans Visual Studio pour démarrer Readarr
1. Ouvrez <http://localhost:8787>

#### Ligne de commande

1. Nettoyez la solution

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. Restaurez et construisez la configuration de débogage pour la plateforme correcte (Posix ou Windows)

```shell
dotnet msbuild -restore src/Readarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. Exécutez l'exécutable produit à partir de `/_output`

## Contribution de code

- Si vous ajoutez une nouvelle fonctionnalité déjà demandée, veuillez commenter sur [GitHub Issues](https://github.com/Readarr/Readarr/issues) afin que le travail ne soit pas dupliqué (Si vous souhaitez ajouter quelque chose qui n'est pas déjà là, veuillez d'abord nous en parler)
- Faites un rebase à partir de la branche develop de Readarr, ne fusionnez pas
- Faites des commits significatifs, ou écrasez-les
- N'hésitez pas à faire une pull request avant que le travail ne soit terminé, cela nous permettra de voir où il en est et de faire des commentaires/suggérer des améliorations
- Contactez-nous sur Discord si vous avez des questions
- Ajoutez des tests (unitaires/intégration)
- Faites des commits avec des fins de ligne \*nix pour la cohérence (Nous utilisons Windows et commettons avec \*nix)
- Une fonctionnalité/correction de bogue par pull request pour que les choses restent propres et faciles à comprendre
- Utilisez 4 espaces au lieu des tabulations, c'est la valeur par défaut pour VS 2022 et WebStorm

## Faire une demande de pull

- Ne faites des demandes de pull que vers `develop`, jamais vers `master`, si vous faites une demande de pull vers `master`, nous commenterons et fermerons la demande
- Vous recevrez probablement des commentaires ou des questions de notre part, ils visent à assurer la cohérence et la maintenabilité
- Nous essaierons de répondre aux demandes de pull dès que possible, si cela fait un jour ou deux, veuillez nous contacter, nous avons peut-être manqué la demande
- Chaque demande de pull doit provenir de sa propre [branche de fonctionnalité](http://martinfowler.com/bliki/FeatureBranch.html) et non de develop dans votre fork, elle doit avoir un nom de branche significatif (ce qui est ajouté/corrigé)
  - `new-feature` (Bon)
  - `fix-bug` (Bon)
  - `patch` (Mauvais)
  - `develop` (Mauvais)
- Les commits doivent être écrits comme `New:` ou `Fixed:` pour les modifications qui ne seraient pas considérées comme une `maintenance release`

## Tests unitaires

Readarr utilise nunit pour sa suite de tests unitaires, d'intégration et d'automatisation.

### Exécution des tests

Les tests peuvent être exécutés facilement depuis Visual Studio en utilisant le package nuget nunit3testadapter inclus, ou depuis la ligne de commande en utilisant le script bash inclus `test.sh`.

Depuis Visual Studio, il suffit de naviguer vers l'Explorateur de tests et d'exécuter ou de déboguer les tests que vous souhaitez examiner.

Les tests peuvent être exécutés tous en une seule fois ou un par un dans Visual Studio.

Depuis la ligne de commande, le script `test.sh` accepte 3 paramètres

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### Rédaction des tests

Bien que cela ne soit pas toujours amusant, nous encourageons l'écriture de tests unitaires pour tout changement de code backend. Cela garantira que le changement fonctionne comme prévu et que les modifications futures ne compromettent pas le comportement attendu.

> Nous exigeons actuellement une couverture de 80 % sur le nouveau code lors de la soumission d'une demande de pull
{.is-info}

Si vous avez des questions à ce sujet, veuillez nous le faire savoir.

# Traduction

Readarr utilise une instance Weblate auto-hébergée en accès libre [Weblate](https://translate.servarr.com) pour gérer ses fichiers de traduction au format json. Ces fichiers sont stockés dans le dépôt à `src/NzbDrone.Core/Localization`

## Contribution à une traduction existante

Weblate gère la synchronisation et la traduction des chaînes pour toutes les langues autres que l'anglais. L'édition des chaînes traduites et la traduction des chaînes existantes pour les langues prises en charge doivent être effectuées sur Weblate pour le projet Readarr.

La traduction en anglais, `en.json`, sert de source pour toutes les autres traductions et est gérée sur le dépôt GitHub.

## Ajout d'une langue

L'ajout de traductions à Readarr nécessite deux étapes

- Ajout de la langue à Weblate
- Ajout de la langue à la base de code de Readarr

## Ajout de chaînes de traduction dans le code

La traduction en anglais, `src/NzbDrone.Core/Localization/en.json`, sert de source pour toutes les autres traductions et est gérée sur le dépôt GitHub. Lors de l'ajout d'une nouvelle chaîne à l'interface utilisateur ou au backend, une clé doit également être ajoutée à `en.json` avec la valeur par défaut en anglais. Cette clé peut ensuite être utilisée comme suit :

> Les demandes de traduction des messages de journal ne seront pas acceptées
{.is-warning}

### Chaînes du backend

Les chaînes du backend peuvent être ajoutées en utilisant la méthode `GetLocalizedString` du service de localisation

```dotnet
private readonly ILocalizationService _localizationService;

public IndexerCheck(ILocalizationService localizationService)
{
  _localizationService = localizationService;
}
        
var translated = _localizationService.GetLocalizedString("IndexerHealthCheckNoIndexers")
```

### Chaînes du frontend

Les nouvelles chaînes peuvent être ajoutées au frontend en important la fonction de traduction et en utilisant une clé spécifiée dans `en.json`

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```