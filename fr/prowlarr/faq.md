---
title: FAQ de Prowlarr
description: FAQ de Prowlarr
published: true
date: 2023-08-28T19:29:30.585Z
tags: prowlarr, faq
editor: markdown
dateCreated: 2021-11-03T03:01:18.079Z
---

# Table des matières

- [Table des matières](#table-des-matières)
  - [Authentification forcée](#authentification-forcée)
  - [Comment réinitialiser les statistiques ?](#comment-réinitialiser-les-statistiques)
  - [Catégorie non disponible ou manquante](#catégorie-non-disponible-ou-manquante)
  - [Puis-je ajouter n'importe quel indexeur Torznab ou Newznab (générique) ?](#puis-je-ajouter-nimporte-quel-indexeur-torznab-ou-newznab-générique)
  - [Puis-je ajouter n'importe quel flux RSS de torrent (générique) ?](#puis-je-ajouter-nimporte-quel-flux-rss-de-torrent-générique)
  - [Puis-je utiliser des indexeurs flaresolverr ?](#puis-je-utiliser-des-indexeurs-flaresolverr)
  - [Comment ajouter un indexeur qui est hors ligne ou non fonctionnel ?](#comment-ajouter-un-indexeur-qui-est-hors-ligne-ou-non-fonctionnel)
  - [Prowlarr ne se synchronise pas avec Sonarr](#prowlarr-ne-se-synchronise-pas-avec-sonarr)
  - [Prowlarr ne synchronise pas l'indexeur X avec l'application](#prowlarr-ne-synchronise-pas-lindexeur-x-avec-lapplication)
  - [Quels paramètres d'indexeur \*Arr sont comparés pour une synchronisation complète de l'application ?](#quels-paramètres-dindexeur-arr-sont-comparés-pour-une-synchronisation-complète-de-lapplication)
  - [Comment mettre à jour Prowlarr ?](#comment-mettre-à-jour-prowlarr)
    - [Puis-je mettre à jour Prowlarr à l'intérieur de mon conteneur Docker ?](#puis-je-mettre-à-jour-prowlarr-à-lintérieur-de-mon-conteneur-docker)
    - [Installation d'une version plus récente](#installation-dune-version-plus-récente)
      - [Native](#native)
      - [Docker](#docker)
  - [Puis-je passer de `nightly` à `develop` ?](#puis-je-passer-de-nightly-à-develop)
  - [Puis-je passer d'une branche à une autre ?](#puis-je-passer-dune-branche-à-une-autre)
  - [Aide, mon Mac dit que Prowlarr ne peut pas être ouvert car le développeur ne peut pas être vérifié](#aide-mon-mac-dit-que-prowlarr-ne-peut-pas-être-ouvert-car-le-développeur-ne-peut-pas-être-vérifié)
  - [Aide, mon Mac dit que Prowlarr.app est endommagé et ne peut pas être ouvert](#aide-mon-mac-dit-que-prowlarrapp-est-endommagé-et-ne-peut-pas-être-ouvert)
  - [Comment demander une fonctionnalité pour Prowlarr ?](#comment-demander-une-fonctionnalité-pour-prowlarr)
  - [Je reçois une erreur : Database disk image is malformed](#je-reçois-une-erreur-database-disk-image-is-malformed)
  - [J'utilise Prowlarr sur un Mac et il a soudainement cessé de fonctionner. Que s'est-il passé ?](#jutilise-prowlarr-sur-un-mac-et-il-a-soudainement-cessé-de-fonctionner-que-sest-il-passé)
  - [Comment passer du service Windows à une application de la barre d'état système ?](#comment-passer-du-service-windows-à-une-application-de-la-barre-détat-système)
  - [Comment sauvegarder/restaurer Prowlarr ?](#comment-sauvegarderrestaurer-prowlarr)
    - [Sauvegarde de Prowlarr](#sauvegarde-de-prowlarr)
      - [Utilisation de la sauvegarde intégrée](#utilisation-de-la-sauvegarde-intégrée)
      - [Utilisation du système de fichiers directement](#utilisation-du-système-de-fichiers-directement)
    - [Restauration à partir de la sauvegarde](#restauration-à-partir-de-la-sauvegarde)
      - [Utilisation de la sauvegarde au format zip](#utilisation-de-la-sauvegarde-au-format-zip)
      - [Utilisation de la sauvegarde du système de fichiers](#utilisation-de-la-sauvegarde-du-système-de-fichiers)
      - [Restauration du système de fichiers sur un NAS Synology](#restauration-du-système-de-fichiers-sur-un-nas-synology)
  - [L'interface Web ne se charge qu'en local sur Windows](#linterface-web-ne-se-charge-quen-local-sur-windows)
  - [Comment trouver les cookies ?](#comment-trouver-les-cookies)
  - [uTorrent ne fonctionne plus](#utorrent-ne-fonctionne-plus)
  - [J'ai reçu une fenêtre contextuelle indiquant que config.xml était corrompu, que faire maintenant ?](#jai-reçu-une-fenêtre-contextuelle-indiquant-que-configxml-était-corrompu-que-faire-maintenant)
  - [Certificat invalide et autres problèmes HTTPS ou SSL](#certificat-invalide-et-autres-problèmes-https-ou-ssl)
  - [Aide, je me suis enfermé dehors](#aide-je-me-suis-enfermé-dehors)
  - [Problèmes d'interface utilisateur étranges](#problèmes-dinterface-utilisateur-étranges)
  - [VPNs, Prowlarr et les \*ARRs](#vpns-prowlarr-et-les-arrs)
  - [Comment empêcher le navigateur de se lancer au démarrage ?](#comment-empêcher-le-navigateur-de-se-lancer-au-démarrage)
  - [Puis-je ajouter facilement tous les indexeurs en une seule fois ?](#puis-je-ajouter-facilement-tous-les-indexeurs-en-une-seule-fois)
  
## Authentification forcée

Si Prowlarr est exposé de manière à ce que l'interface utilisateur puisse être accessible depuis l'extérieur de votre réseau local, vous devez avoir une méthode d'authentification activée pour accéder à l'interface utilisateur. Cela est également de plus en plus requis par les trackers et les indexeurs.

À partir de Prowlarr v1, l'authentification est obligatoire.

### Méthode d'authentification

- `Basic` (fenêtre contextuelle du navigateur) - Cette option, lors de l'accès à votre Prowlarr, affiche une petite fenêtre contextuelle vous permettant de saisir un nom d'utilisateur et un mot de passe.
- `Forms` (page de connexion) - Cette option affiche un écran de connexion familier, similaire à celui des autres sites web, vous permettant de vous connecter à votre Prowlarr.
- `External` - Configurable uniquement via le fichier de configuration
  - Si vous utilisez une **authentification externe** telle que Authelia, Authetik, NGINX Basic auth, etc., vous pouvez éviter de devoir vous authentifier deux fois en arrêtant l'application, en définissant `<AuthenticationMethod>External</AuthenticationMethod>` dans le [fichier de configuration](/prowlarr/appdata-directory) et en redémarrant l'application. **Notez que plusieurs entrées `AuthenticationMethod` dans le fichier ne sont pas prises en charge et seule la valeur la plus haute sera utilisée**.

### Authentification requise

- Si vous n'exposez pas l'application à l'extérieur et/ou si vous ne souhaitez pas que l'authentification soit requise pour l'accès local (par exemple, LAN), modifiez les paramètres dans Paramètres => Sécurité générale => Authentification requise en `Désactivée pour les adresses locales`.
  - L'équivalent dans le fichier de configuration est `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`.
  
## Comment réinitialiser les statistiques ?

- Pour réinitialiser vos statistiques et effacer l'historique, procédez comme suit :

1. Historique => Options
1. Définissez le nettoyage de l'historique sur `1`. Cela conservera uniquement l'historique et les statistiques jusqu'à hier.
1. Accédez à Système => Tâches
1. Exécutez la tâche "Nettoyer l'historique"
1. Exécutez la tâche "Entretien"
1. Revenez à Historique => Options
1. Définissez le nettoyage de l'historique sur la période de rétention souhaitée pour l'historique et les statistiques.

## Catégorie non disponible ou manquante

- Veuillez noter que les catégories personnalisées/spécifiques à un indexeur sont mappées sur des catégories standard, de sorte que la recherche dans les catégories standard inclura toutes les catégories personnalisées. Consultez la définition de mappage des catégories de votre indexeur spécifique pour plus de détails.

## Puis-je ajouter n'importe quel flux RSS de torrent (générique) ?

Oui. Utilisez "TorrentRSS".

Les attributs suivants sont obligatoires :

- guid
- title
- infohash
- enclosure ou link

Les attributs suivants sont facultatifs, mais recommandés :

- size
- pubDate

## Puis-je ajouter n'importe quel indexeur Torznab ou Newznab (générique) ?

- Oui.
- Allez dans `Indexeurs` => `Ajouter un indexeur` (<kb>+</kb>) => `Torznab générique` ou `Newznab générique`

## Puis-je utiliser des indexeurs flaresolverr ?

- Oui.

1. Configurez votre instance flaresolverr en l'ajoutant en tant que proxy dans [Paramètres => Indexeurs](/prowlarr/settings#indexer-proxies)
1. Ajoutez une étiquette au proxy flaresovlerr créé
1. Ajoutez la même étiquette à votre [Indexeur](/prowlarr/indexers)

> Les étiquettes doivent correspondre et Cloudflare doit être détecté pour que Flaresolverr soit utilisé. Un proxy Flaresolverr est désactivé s'il n'y a pas d'étiquettes utilisées.
{.is-warning}

> [Consultez les guides de TRaSH sur "Comment configurer Flaresolverr"](https://trash-guides.info/Prowlarr/prowlarr-setup-flaresolverr/) pour plus de détails.
{.is-info}

## Comment ajouter un indexeur qui est hors ligne ou non fonctionnel ?

- Suivez les étapes standard pour ajouter l'indexeur en notant les modifications suivantes.
- Décochez (Désactiver) la case "Activé"
- Appuyez sur "Enregistrer"
- Appuyez à nouveau sur "Enregistrer" pour déclencher une sauvegarde forcée
- Modifiez l'indexeur (icône de clé à molette)
- Cochez (Activer) la case "Activé"
- Appuyez sur "Enregistrer"
- Appuyez à nouveau sur "Enregistrer" pour déclencher une sauvegarde forcée

## Prowlarr ne se synchronise pas avec Sonarr

- Prowlarr ne prend en charge que Sonarr v3+
- Sonarr v2 (anciennement nzbdrone) n'est pas pris en charge par Prowlarr ni en général et a été abandonné depuis mars 2021.

## Prowlarr ne synchronise pas l'indexeur X avec l'application

- Prowlarr ne se synchronise que si l'ajout et la suppression ou la synchronisation complète sont activés pour l'application.
- Seuls dans les cas où une application et un indexeur ont des étiquettes correspondantes ou aucune étiquette du tout, un indexeur sera synchronisé avec une application.
- Les indexeurs sont synchronisés en fonction des capacités/catégories qu'ils prétendent prendre en charge.
  - Si un indexeur ne prend en charge que des catégories TV, il ne sera pas synchronisé avec Lidarr, Radarr et Readarr.
- Un indexeur donné ne sera synchronisé qu'avec les catégories "Prises en charge" de Sonarr, qui peuvent être sélectionnées comme paramètre avancé pour chaque application.
- Les indexeurs ne seront pas synchronisés s'ils ne retournent pas de résultats contenant au moins l'une des catégories configurées lors des requêtes de test. Les journaux ne montreront aucune indication de tentative de synchronisation.
- La cause la plus courante de ce problème est que les \*Arr n'acceptent que les indexeurs dont les requêtes de test renvoient des résultats contenant au moins l'une des catégories configurées. En d'autres termes, si vous synchronisez une application et que la requête vide de votre indexeur ne renvoie pas de résultats avec une sortie dans les catégories configurées pour l'application, il ne pourra pas ajouter l'indexeur à \*Arr.
- L'erreur spécifique sera un HTTP 400 de \*Arr indiquant `Query successful, but no results in the configured categories were returned from your indexer. This may be an issue with the indexer or your indexer category settings.` (Requête réussie, mais aucun résultat dans les catégories configurées n'a été renvoyé par votre indexeur. Cela peut être un problème avec l'indexeur ou vos paramètres de catégorie de l'indexeur.)
  - Il est possible que cet indexeur ne puisse tout simplement pas être utilisé avec cet \*Arr. C'est courant lorsque l'on essaie d'utiliser des trackers publics ou des indexeurs Usenet avec Readarr et Lidarr.
  - Ajustez les catégories synchronisées dans les paramètres avancés de l'application \*Arr dans Prowlarr.
    - Notez que certains trackers - principalement les trackers publics "médiocres" - nécessitent de sélectionner et de synchroniser la catégorie `8000 - Autre`. Cela est souvent - mais pas toujours - indiqué dans les détails du tracker dans Prowlarr.
  - Réessayez plus tard.
  - Si le problème persiste, vous pouvez avoir une base de données corrompue. Vérifiez vos journaux pour des instances de `Database disk image is malformed` (Image disque de base de données corrompue) ou `Error creating main database` (Erreur lors de la création de la base de données principale). Consultez [cette section](https://wiki.servarr.com/prowlarr/faq#i-am-getting-an-error-database-disk-image-is-malformed) pour des solutions possibles.

## Quels paramètres d'indexeur \*Arr sont comparés pour une synchronisation complète de l'application ?

- Application/Prowlarr : Nom de l'indexeur
- Application/Prowlarr : Activer/Désactiver le flux RSS
- Application/Prowlarr : Activer/Désactiver la recherche automatique
- Application/Prowlarr : Activer/Désactiver la recherche interactive
- Application/Prowlarr : Priorité de l'indexeur
- Application/Prowlarr : Clé API
- Application/Prowlarr : URL
- Application/Prowlarr : URL de base
- Application/Prowlarr : Port
- Application/Prowlarr : Catégories
- Application/Prowlarr : Ratio de partage et temps de partage
- Application/Prowlarr : Nombre minimum de sources
- Application/Prowlarr : *Tout autre paramètre configurable/contrôlé dans Prowlarr*
- Prowlarr : Implémentation (par exemple, YML ou C#)

Avec la synchronisation complète activée, si l'un des éléments ci-dessus change entre l'application \*Arr et Prowlarr, l'indexeur sera synchronisé et mis à jour dans \*Arr.

## Comment mettre à jour Prowlarr ?

- Allez dans Paramètres, puis l'onglet Général et affichez les paramètres avancés (utilisez le bouton bascule près du bouton Enregistrer).

1. Dans la section Mises à jour, changez le nom de la branche en `master`, `develop` ou `nightly`.
1. Enregistrez.

*Cela n'installera pas immédiatement les éléments de cette branche, cela se produira lors de la prochaine mise à jour.*

- `master` - ![Version actuelle stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) - (Par défaut/Stable) : Il a été testé par les utilisateurs des branches develop et nightly et il n'est pas connu pour avoir de problèmes majeurs. Sur GitHub, il s'agit de la branche `master`.

- `develop` - ![Version actuelle bêta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) - (Bêta) : Il s'agit de la version de test. Elle est publiée après avoir été testée en nightly pour s'assurer qu'il n'y a pas de problèmes immédiats. Les nouvelles fonctionnalités et les corrections de bugs sont d'abord publiées ici après la version nightly. Elle peut être considérée comme semi-stable, mais reste une version `bêta`.

> Sur GitHub, il s'agit d'un instantané de la branche `develop` à un moment précis.
{.is-warning}

- `nightly` - ![Version actuelle instable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) - (Alpha/Instable) : Il s'agit de la version la plus récente. Elle est publiée dès que le code est validé et passe tous les tests automatisés. Cette version n'a peut-être pas encore été utilisée par nous ou d'autres utilisateurs. Il n'y a aucune garantie qu'elle fonctionnera même dans certains cas. Cette branche est uniquement recommandée pour les utilisateurs avancés. Des problèmes et des investigations personnelles sont attendus dans cette branche. ***Utilisez cette branche uniquement si vous savez ce que vous faites et êtes prêt à mettre les mains dans le cambouis pour récupérer une mise à jour échouée.*** Cette version est mise à jour immédiatement.

> **Attention : Vous pourriez ne pas pouvoir revenir à `develop` après avoir basculé vers cette branche.** Sur GitHub, il s'agit de la branche `develop`.
{.is-danger}

- Remarque : Si vous utilisez Docker, ajoutez `:latest`, `:testing`, `:develop` ou `:nightly` à la fin de votre balise de conteneur en fonction de celui qui crée vos versions.

|                                                                      | `master` (stable) ![Master/Stable actuel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Develop/Beta actuel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) | `nightly` (instable) ![Nightly/Alpha actuel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/prowlarr)                       | `latest`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-prowlarr) | `latest`                                                                                                                                                                                                             | `develop`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |

### Puis-je mettre à jour Prowlarr à l'intérieur de mon conteneur Docker ?

- *Techniquement, oui.* **Mais vous ne devriez absolument pas le faire.** C'est une philosophie fondamentale de Docker. Des problèmes de base de données peuvent survenir si vous mettez à niveau votre installation vers la version `nightly` la plus récente, puis mettez à jour le conteneur Docker lui-même (éventuellement en revenant à une version plus ancienne).

### Installation d'une version plus récente

#### Natif

1. Accédez à Système, puis à l'onglet Mises à jour.
1. Les versions plus récentes qui ne sont pas encore installées auront un bouton de mise à jour à côté d'elles. En cliquant sur ce bouton, vous installerez la mise à jour.

#### Docker

1. Re-téléchargez votre balise et mettez à jour votre conteneur.

## Puis-je passer de `nightly` à `develop` ?

## Puis-je passer d'une branche à une autre ?

- Si la version est identique, vous pouvez passer d'une branche à l'autre. Sinon, vérifiez avec l'équipe de développement si vous pouvez passer de `nightly` à `develop` ; ou de `develop` à `nightly` pour votre version donnée.
- Si vous ne suivez pas ces instructions, votre Prowlarr risque de devenir inutilisable ou de générer des erreurs. Vous êtes prévenu
  - Les erreurs les plus courantes sont des erreurs de base de données concernant des colonnes ou des tables manquantes.

## Aide, mon Mac dit que Prowlarr ne peut pas être ouvert car le développeur ne peut pas être vérifié

- C'est simple, veuillez consulter ce lien pour plus d'informations [ici](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
- Alternativement, vous devrez peut-être auto-signer Prowlarr `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine`

![faq_1_mac.png](/assets/general/faq_1_mac.png)

## Aide, mon Mac dit que Prowlarr.app est endommagé et ne peut pas être ouvert

Cela est dû soit à un téléchargement corrompu (essayez à nouveau), soit à des problèmes de sécurité expliqués juste avant cela.

## Comment puis-je demander une fonctionnalité pour Prowlarr ?

Pour demander une fonctionnalité pour Prowlarr, recherchez d'abord sur GitHub pour vous assurer qu'aucune demande similaire n'existe, puis [cliquez ici](https://github.com/Prowlarr/Prowlarr/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=) pour ajouter votre demande.

## J'obtiens une erreur : L'image disque de la base de données est corrompue

- **Les erreurs de `Error creating log database` indiquent des problèmes avec logs.db**
  - Cela peut être rapidement résolu en renommant ou en supprimant la base de données. La base de données des journaux contient des informations non importantes concernant l'historique des commandes et l'historique des installations de mises à jour, ainsi que des entrées Info, Warn et Error.
- **Les erreurs de `Error creating main database` ou les erreurs génériques `database disk image is malformed` sans base de données spécifiée indiquent des problèmes avec prowlarr.db**
  - Continuez avec les étapes indiquées ci-dessous
- Cela signifie que votre base de données SQLite qui stocke la plupart des informations de Prowlarr est corrompue. Vos options sont d'essayer de sauvegarder votre (vos) base(s) de données, d'essayer de récupérer la base de données existante, d'essayer de récupérer la (les) sauvegarde(s), ou si tout échoue, de recommencer avec une nouvelle base de données fraîche.
- Cette erreur peut apparaître si le fichier de base de données n'est pas accessible en écriture par l'utilisateur/groupe sous lequel \*Arr s'exécute. Les autorisations étant la cause, cela ne posera probablement problème que pour les nouvelles installations, les installations migrées vers un nouveau serveur, si vous avez récemment modifié les autorisations de votre répertoire appdata, ou si vous avez modifié l'utilisateur et le groupe sous lesquels \*Arr s'exécute.
- Votre meilleure et première option est d'[essayer de restaurer à partir d'une sauvegarde](#how-do-i-backuprestore-my-prowlarr)
- Vous pouvez également essayer de récupérer votre base de données. C'est généralement la seule option lorsque ce problème se produit après une mise à jour. Essayez la commande [sqlite3 `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Si votre version de sqlite ne dispose pas de la commande `.recover` ou si vous souhaitez une méthode plus conviviale pour l'interface graphique (par exemple sous Windows), suivez [nos instructions sur ce wiki](/useful-tools#recovering-a-corrupt-db-ui).
- Une autre cause possible de l'erreur de base de données est que vous placez votre base de données sur un lecteur réseau (nfs ou smb ou autre chose non local). **SQLite est conçu pour des situations où les données et l'application coexistent sur la même machine.** Ainsi, votre dossier \*Arr AppData (/montage de configuration pour Docker) DOIT être stocké sur un stockage local. [SQLite et les lecteurs réseau ne fonctionnent pas bien ensemble et finiront par provoquer une base de données corrompue](https://www.sqlite.org/draft/useovernet.html).
- Si vous utilisez mergerFS, vous devez supprimer `direct_io` car SQLite utilise mmap qui n'est pas pris en charge par `direct_io`, comme expliqué dans la [documentation de mergerFS ici](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## J'utilise Prowlarr sur un Mac et il a soudainement cessé de fonctionner. Que s'est-il passé ?

- Il s'agit très probablement d'un bogue de MacOS qui a provoqué la corruption de la base de données de Prowlarr. Veuillez consulter l'entrée de la FAQ pour restaurer une base de données corrompue.

## Comment passer du service Windows à une application de la barre d'état système ?

- Arrêtez Prowlarr
- Exécutez serviceuninstall.exe qui se trouve dans le répertoire Prowlarr
- Exécutez Prowlarr.exe en tant qu'administrateur une fois pour lui donner les autorisations appropriées et ouvrir le pare-feu. Une fois terminé, vous pouvez le fermer et l'exécuter normalement.
- (Facultatif) Ajoutez un raccourci vers Prowlarr.exe dans le dossier de démarrage pour le démarrer automatiquement au démarrage.

## Comment sauvegarder/restaurer Prowlarr ?

### Sauvegarde de Prowlarr

#### Utilisation de la sauvegarde intégrée

- Accédez à Système => Sauvegarde dans l'interface utilisateur de Prowlarr
- Cliquez sur le bouton Sauvegarder
- Téléchargez le fichier zip après la création de la sauvegarde pour le mettre en lieu sûr

#### Utilisation du système de fichiers directement

- Trouvez l'emplacement du répertoire AppData de Prowlarr  
  - Via l'interface utilisateur de Prowlarr, accédez à Système => À propos  
  - [Répertoire AppData de Prowlarr](/prowlarr/appdata-directory)
- Arrêtez Prowlarr - Cela empêchera la corruption de la base de données
- Copiez le contenu vers un emplacement sûr

### Restauration à partir d'une sauvegarde

> La restauration sur un système d'exploitation qui utilise des chemins différents ne fonctionnera pas (Windows vers Linux, Linux vers Windows, Windows vers OS X ou OS X vers Windows), le passage entre OS X et Linux peut fonctionner, car les deux utilisent des chemins contenant `/` au lieu de `\` utilisé par Windows, mais cela n'est pas pris en charge. Vous devrez modifier manuellement tous les chemins dans la base de données.
{.is-warning}

#### Utilisation de la sauvegarde au format zip

- Réinstallez Prowlarr (si applicable / non déjà installé)
- Exécutez Prowlarr
- Accédez à Système => Sauvegarde
- Sélectionnez Restaurer la sauvegarde
- Sélectionnez Choisir le fichier
- Sélectionnez votre fichier de sauvegarde au format zip
- Sélectionnez Restaurer

#### Utilisation de la sauvegarde du système de fichiers

- Réinstallez Prowlarr (si applicable / non déjà installé)
- Trouvez l'emplacement du répertoire AppData de Prowlarr  
  - Exécutez Prowlarr une fois et via l'interface utilisateur, accédez à Système => À propos  
  - [Répertoire AppData de Prowlarr](/prowlarr/appdata-directory)
- Arrêtez Prowlarr
- Supprimez le contenu du répertoire AppData **(y compris les fichiers .db-wal/.db-journal s'ils existent)**
- Restaurez à partir de votre sauvegarde
- Démarrez Prowlarr
- Tant que les chemins sont les mêmes, tout reprendra là où vous vous étiez arrêté

#### Restauration du système de fichiers sur un NAS Synology

> ATTENTION : La restauration sur un Synology nécessite des connaissances en Linux et un accès SSH root à l'appareil Synology.
{.is-warning}

- Réinstallez Prowlarr (si applicable / non déjà installé)
- Trouvez l'emplacement du répertoire AppData de Prowlarr  
  - Exécutez Prowlarr une fois et via l'interface utilisateur, accédez à Système => À propos  
  - [Répertoire AppData de Prowlarr](/prowlarr/appdata-directory)
- Arrêtez Prowlarr
- Connectez-vous au NAS Synology via SSH et connectez-vous en tant que root  

> Sur certaines installations, l'utilisateur est différent des commandes ci-dessous : `chown -R sc-Prowlarr:Prowlarr *` {.is-info}

- Exécutez les commandes suivantes :

    ```shell
        rm -r /usr/local/Prowlarr/var/.config/Prowlarr/Prowlarr.db
        cp -f /tmp/Prowlarr_backup/* /usr/local/Prowlarr/var/.config/Prowlarr/
    ```

- Mettez à jour les autorisations sur les fichiers :

    ```shell
        cd /usr/local/Prowlarr/var/.config/Prowlarr/
        chown -R Prowlarr:users *
        chmod -R 0644 *
    ```

- Démarrez Prowlarr

## L'interface WebUI ne se charge qu'en local sur Windows

Si vous ne pouvez accéder à votre interface web qu'à l'adresse `http://localhost:9696/` ou `http://127.0.0.1:9696`, vous devez exécuter Prowlarr en tant qu'administrateur au moins une fois, voire toujours.

## Recherche de cookies

Certains sites ne peuvent pas être connectés automatiquement et nécessitent une connexion manuelle, puis vous devez fournir les cookies à Prowlarr pour qu'il fonctionne. [Veuillez consulter cet article pour plus de détails.](/useful-tools#finding-cookies)

## uTorrent ne fonctionne plus

- Assurez-vous que l'interface Web est activée

![faq_4_utorrent.png](/assets/general/faq_4_utorrent.png)

- Activez l'interface Web

![faq_5_utorrent.png](/assets/general/faq_5_utorrent.png)

- Assurez-vous que le port d'écoute alternatif (Avancé => Interface Web) n'est pas le même que le port d'écoute (Connexions). Nous vous suggérons de modifier le port d'écoute alternatif de l'interface Web afin de ne pas perturber la redirection de port pour les connexions.

![faq_6_utorrent.png](/assets/general/faq_6_utorrent.png)

## J'ai reçu une fenêtre contextuelle indiquant que config.xml était corrompu, que dois-je faire maintenant ?

Prowlarr n'a pas pu lire votre fichier de configuration au démarrage car il est devenu corrompu d'une manière ou d'une autre. Pour remettre Prowlarr en ligne, vous devrez supprimer le fichier `.xml` dans votre dossier AppData, une fois supprimé, lancez Prowlarr et il démarrera sur le port par défaut (9696), vous devrez maintenant reconfigurer tous les paramètres que vous avez configurés sur la page Paramètres généraux.

## Certificat invalide et autres problèmes HTTPS ou SSL

Votre client de téléchargement ne fonctionne plus et vous obtenez une erreur comme `Localhost est un certificat invalide` ?

Prowlarr valide les certificats SSL. Si aucun certificat SSL n'est défini dans le client de téléchargement, ou si vous utilisez un certificat https auto-signé sans le certificat CA ajouté à votre magasin de certificats local, alors Prowlarr refusera de se connecter. Des certificats correctement signés et gratuits sont disponibles auprès de Let's Encrypt.

Si votre client de téléchargement et Prowlarr sont sur la même machine, il n'y a aucune raison d'utiliser HTTPS, donc la solution la plus simple est de désactiver SSL pour la connexion. La plupart des gens conviendraient que ce n'est pas nécessaire non plus sur un réseau local. Il est possible de désactiver la validation du certificat dans les paramètres avancés si vous souhaitez conserver une configuration SSL non sécurisée.

## Aide, je me suis verrouillé dehors

{#help-i-have-forgotten-my-password}

Pour désactiver l'authentification (pour réinitialiser votre nom d'utilisateur ou votre mot de passe oublié), vous devrez modifier `config.xml` qui se trouve à l'intérieur du [répertoire des données d'application Prowlarr](/prowlarr/appdata-directory)

1. Ouvrez config.xml dans un éditeur de texte
1. Trouvez la ligne de méthode d'authentification qui sera
`<AuthenticationMethod>Basic</AuthenticationMethod>` ou `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Changez la ligne `AuthenticationMethod` en `<AuthenticationMethod>None</AuthenticationMethod>`
1. Redémarrez Prowlarr
1. Prowlarr sera maintenant accessible sans mot de passe, vous devriez aller dans `Paramètres : Général` dans l'interface utilisateur et définir votre nom d'utilisateur et votre mot de passe

## Problèmes d'interface utilisateur étranges

- Si vous rencontrez des problèmes d'interface utilisateur étranges ou si une certaine vue ou un certain tri ne fonctionne pas, essayez de voir dans une fenêtre de navigation privée Chrome ou une fenêtre privée Firefox. Si cela fonctionne correctement là-bas, effacez le cache et les cookies de votre navigateur pour votre adresse IP/domaine spécifique. Pour plus d'informations, consultez l'article du wiki [Effacer le cache, les cookies et le stockage local](/useful-tools#clearing-cookies-and-local-storage).

## VPN, Jackett et les \*ARRs

- À moins que vous ne soyez dans un pays répressif comme la Chine, l'Australie ou l'Afrique du Sud, votre client torrent est généralement la seule chose qui doit être derrière un VPN. Étant donné que le point de terminaison VPN est partagé par de nombreux utilisateurs, vous pouvez et rencontrerez des limites de débit, une protection contre les attaques DDOS et des interdictions IP de divers services utilisés par chaque logiciel.
- En d'autres termes, mettre les \*Arrs (Lidarr, Prowlarr, Radarr, Readarr et Lidarr) derrière un VPN peut rendre les applications inutilisables dans certains cas en raison de l'inaccessibilité des services.

> **Pour être clair, il ne s'agit pas de savoir si les VPN causeront des problèmes avec les \*Arrs, mais quand : les fournisseurs d'images vous bloqueront et Cloudflare est devant la plupart des serveurs \*Arr (mises à jour, métadonnées, etc.) et peut également vous bloquer**
{.is-warning}

- **De nombreux trackers privés vous interdiront d'utiliser ou d'accéder à eux (c'est-à-dire en utilisant Jackett ou Prowlarr) via un VPN.**

### Utilisation d'un VPN

- Si un VPN est requis et que Docker est utilisé, il est recommandé d'utiliser les conteneurs Hotio ou Binhex's Download Client + VPN.
- Si un VPN est requis et que Docker n'est pas utilisé, votre client VPN ***doit*** prendre en charge le fractionnement du tunnel afin que seules les applications requises (client de téléchargement) soient derrière le VPN.
- De nombreux problèmes d'accès aux trackers peuvent être résolus en utilisant les serveurs DNS de Google ou de Cloudflare à la place des serveurs DNS de votre fournisseur d'accès Internet.
- Dans certains cas (par exemple, les fournisseurs de services Internet au Royaume-Uni), vous devrez peut-être mettre votre client de téléchargement de torrents derrière un VPN et Jackett/Prowlarr comme suit :
  - mettez Jackett derrière le VPN et assurez-vous que le fractionnement du tunnel permet l'accès local
  - pour Prowlarr, configurez votre client VPN pour fournir un proxy et ajoutez le proxy dans Paramètres => Indexeurs. Donnez au proxy une étiquette et attribuez la même étiquette à tous les indexeurs qui doivent l'utiliser.
    - Si absolument nécessaire et si votre VPN ne propose pas de moyen de créer un proxy, vous pouvez mettre Prowlarr derrière le VPN et vous assurer que le fractionnement du tunnel permet l'accès local.

## Comment empêcher le navigateur de se lancer au démarrage ?

Selon votre système d'exploitation, il existe plusieurs façons possibles.

- Dans `Paramètres` => `Général` sur certains systèmes d'exploitation, il y a une case à cocher pour lancer le navigateur au démarrage.
- Lorsque vous invoquez Prowlarr, vous pouvez ajouter `-nobrowser` (*nix) ou `/nobrowser` (Windows) aux arguments.
- Arrêtez Prowlarr, modifiez le fichier config.xml et changez `<LaunchBrowser>True</LaunchBrowser>` en `<LaunchBrowser>False</LaunchBrowser>`.

## Puis-je ajouter facilement tous les indexeurs en une seule fois ?

Non. Ce ne serait pas une bonne chose à faire, et cette fonctionnalité ne sera pas ajoutée. Il est beaucoup mieux de choisir judicieusement vos indexeurs, de prêter attention aux statistiques pour supprimer les indexeurs trop lents ou qui ne produisent pas de résultats. Une bonne élagage et maintenance de vos indexeurs donnera de bien meilleurs résultats dans l'ensemble, et des résultats plus rapides lors des recherches à partir de vos applications.