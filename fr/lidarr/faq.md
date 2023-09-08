---
title: Lidarr FAQ
description: 
published: true
date: 2023-08-31T19:08:18.905Z
tags: lidarr, needs-love, faq
editor: markdown
dateCreated: 2021-06-14T14:33:41.344Z
---

# Table des matières

- [Table des matières](#table-des-matières)
  - [Comment fonctionne Lidarr ?](#comment-fonctionne-lidarr)
  - [Comment Lidarr trouve-t-il des sorties ?](#comment-lidarr-trouve-t-il-des-sorties)
  - [Authentification forcée](#authentification-forcée)
  - [Comment les téléchargements possibles sont-ils comparés ?](#comment-les-téléchargements-possibles-sont-ils-comparés)
  - [Lidarr a cessé de fonctionner après la mise à jour vers Ubuntu 22.04](#lidarr-a-cessé-de-fonctionner-après-la-mise-à-jour-vers-ubuntu-2204)
  - [Pourquoi ne puis-je pas ajouter une nouvelle sortie ou un nouvel artiste à Lidarr ?](#pourquoi-ne-puis-je-pas-ajouter-une-nouvelle-sortie-ou-un-nouvel-artiste-à-lidarr)
  - [Pourquoi ne puis-je pas ajouter un album d'artistes variés ?](#pourquoi-ne-puis-je-pas-ajouter-un-album-dartistes-variés)
  - [Pourquoi Lidarr ne montre-t-il que des albums studio ? Comment puis-je trouver des singles ou des EP ?](#pourquoi-lidarr-ne-montre-t-il-que-des-albums-studio-comment-puis-je-trouver-des-singles-ou-des-ep)
  - [Puis-je ajouter seulement un album ?](#puis-je-ajouter-seulement-un-album)
  - [Puis-je télécharger des pistes individuelles ?](#puis-je-télécharger-des-pistes-individuelles)
  - [Pourquoi l'artiste X n'apparaît-il pas dans la recherche ?](#pourquoi-lartiste-x-napparaît-il-pas-dans-la-recherche)
  - [Lidarr a associé un album avec trop de pistes. Comment puis-je changer l'album vers la sortie correcte ?](#lidarr-a-associé-un-album-avec-trop-de-pistes-comment-puis-je-changer-lalbum-vers-la-sortie-correcte)
  - [Je ne peux pas trouver une sortie dans Lidarr mais elle est sur MusicBrainz](#je-ne-peux-pas-trouver-une-sortie-dans-lidarr-mais-elle-est-sur-musicbrainz)
  - [À quelle fréquence les bases de données de Lidarr et de MusicBrainz se synchronisent-elles ?](#à-quelle-fréquence-les-bases-de-données-de-lidarr-et-de-musicbrainz-se-synchronisent-elles)
  - [Comment puis-je ajouter des images d'artiste manquantes ?](#comment-puis-je-ajouter-des-images-dartiste-manquantes)
  - [Comment puis-je obtenir des images d'album manquantes ? (Art de couverture)](#comment-puis-je-obtenir-des-images-dalbum-manquantes-art-de-couverture)
  - [J'ai des problèmes pour importer mes artistes, qu'est-ce que cela peut être ?](#jai-des-problèmes-pour-importer-mes-artistes-quest-ce-que-cela-peut-être)
  - [Comment puis-je renommer mes dossiers d'artistes ?](#comment-puis-je-renommer-mes-dossiers-dartistes)
  - [Comment puis-je supprimer en masse des artistes de la liste des souhaits ?](#comment-puis-je-supprimer-en-masse-des-artistes-de-la-liste-des-souhaits)
  - [Pourquoi Lidarr ne fonctionne-t-il pas derrière un proxy inverse ?](#pourquoi-lidarr-ne-fonctionne-t-il-pas-derrière-un-proxy-inverse)
  - [Comment mettre à jour Lidarr ?](#comment-mettre-à-jour-lidarr)
    - [Puis-je mettre à jour Lidarr à l'intérieur de mon conteneur Docker ?](#puis-je-mettre-à-jour-lidarr-à-lintérieur-de-mon-conteneur-docker)
    - [Installation d'une version plus récente](#installation-dune-version-plus-récente)
      - [Native](#native)
      - [Docker](#docker)
  - [Puis-je passer de `nightly` à `develop` ?](#puis-je-passer-de-nightly-à-develop)
  - [Puis-je passer d'une branche à une autre ?](#puis-je-passer-dune-branche-à-une-autre)
  - [Je reçois une erreur : L'image disque de la base de données est corrompue](#je-reçois-une-erreur-limage-disque-de-la-base-de-données-est-corrompue)
  - [Comment sauvegarder/restaurer mon Lidarr ?](#comment-sauvegarderrestaurer-mon-lidarr)
    - [Sauvegarde de Lidarr](#sauvegarde-de-lidarr)
      - [Utilisation de la sauvegarde intégrée](#utilisation-de-la-sauvegarde-intégrée)
      - [Utilisation du système de fichiers directement](#utilisation-du-système-de-fichiers-directement)
    - [Restauration à partir de la sauvegarde](#restauration-à-partir-de-la-sauvegarde)
      - [Utilisation de la sauvegarde au format zip](#utilisation-de-la-sauvegarde-au-format-zip)
      - [Utilisation de la sauvegarde du système de fichiers](#utilisation-de-la-sauvegarde-du-système-de-fichiers)
      - [Restauration du système de fichiers sur un NAS Synology](#restauration-du-système-de-fichiers-sur-un-nas-synology)
  - [J'utilise Lidarr sur un Mac et il a soudainement cessé de fonctionner. Que s'est-il passé ?](#jutilise-lidarr-sur-un-mac-et-il-a-soudainement-cessé-de-fonctionner-que-sest-il-passé)
  - [J'utilise un Raspberry Pi et Raspbian et Lidarr ne se lance pas](#jutilise-un-raspberry-pi-et-raspbian-et-lidarr-ne-se-lance-pas)
  - [Pourquoi les temps de synchronisation des listes sont-ils si longs et puis-je les modifier ?](#pourquoi-les-temps-de-synchronisation-des-listes-sont-ils-si-longs-et-puis-je-les-modifier)
  - [Puis-je désactiver la tâche de rafraîchissement des sorties ?](#puis-je-désactiver-la-tâche-de-rafraîchissement-des-sorties)
  - [Pourquoi Lidarr ne peut-il pas voir mes fichiers sur un serveur distant ?](#pourquoi-lidarr-ne-peut-il-pas-voir-mes-fichiers-sur-un-serveur-distant)
    - [Lidarr s'exécute sous le compte LocalService par défaut, qui n'a pas accès aux partages de fichiers distants protégés](#lidarr-sexécute-sous-le-compte-localservice-par-défaut-qui-na-pas-accès-aux-partages-de-fichiers-distantes-protégés)
    - [Vous utilisez un lecteur réseau mappé (pas un chemin UNC)](#vous-utilisez-un-lecteur-réseau-mappé-pas-un-chemin-unc)
  - [Aide, je me suis enfermé dehors](#aide-je-me-suis-enfermé-dehors)
  - [Comment empêcher le navigateur de se lancer au démarrage ?](#comment-empêcher-le-navigateur-de-se-lancer-au-démarrage)
  - [Problèmes d'interface utilisateur étranges](#problèmes-dinterface-utilisateur-étranges)
  - [VPNs, Jackett et les \*ARRs](#vpns-jackett-et-les-arrs)
  - [Point de terminaison /all de Jackett](#point-de-terminaison-all-de-jackett)
    - [Solutions Jackett /All](#solutions-jackett-all)
  - [Pourquoi y a-t-il deux fichiers ? | Pourquoi y a-t-il un fichier restant dans les téléchargements ?](#pourquoi-y-a-t-il-deux-fichiers--pourquoi-y-a-t-il-un-fichier-restant-dans-les-téléchargements)
  - [Je reçois constamment des avertissements de mon stockage cloud concernant les limites de l'API](#je-reçois-constamment-des-avertissements-de-mon-stockage-cloud-concernant-les-limites-de-lapi)

## Comment fonctionne Lidarr ?

- Lidarr s'appuie sur les flux RSS pour automatiser la récupération des sorties au fur et à mesure de leur publication, tant pour les nouvelles sorties que pour les sorties précédemment publiées qui sont publiées ou rééditées. Le flux RSS est composé des dernières sorties d'un site, généralement entre 50 et 100 sorties, bien que certains sites en fournissent plus et d'autres moins. Le flux RSS est constitué de toutes les sorties récemment disponibles, y compris les sorties pour les médias demandés que vous ne suivez pas. Si vous consultez les journaux de débogage, vous verrez ces sorties en cours de traitement, ce qui est tout à fait normal.
- Lidarr impose un intervalle de synchronisation RSS minimum de 10 minutes et un maximum de 2 heures. 15 minutes est le minimum recommandé par la plupart des indexeurs, bien que certains permettent des intervalles plus courts et 2 heures garantissent que Lidarr vérifie suffisamment fréquemment pour ne pas manquer une sortie (même s'il peut parcourir le flux RSS sur de nombreux indexeurs pour aider à cela). Certains indexeurs permettent aux clients d'effectuer une synchronisation RSS plus fréquemment que toutes les 10 minutes, dans ces scénarios, nous recommandons d'utiliser l'API Release-Push de Lidarr avec un canal d'annonce IRC pour envoyer les sorties à Lidarr pour le traitement, ce qui peut se faire en quasi temps réel et avec moins de surcharge sur l'indexeur et Lidarr, car Lidarr n'a pas besoin de demander le flux RSS trop fréquemment et de traiter les mêmes sorties encore et encore.

## Comment Lidarr trouve-t-il des sorties ?

- Lidarr ne recherche pas régulièrement les fichiers d'album manquants ou qui n'ont pas atteint leurs objectifs de qualité. Au lieu de cela, il interroge assez fréquemment vos indexeurs et trackers pour ''toutes'' les sorties nouvellement publiées, puis les compare avec sa liste de sorties manquantes ou à mettre à niveau. Toutes les correspondances sont téléchargées. Cela permet à Lidarr de couvrir une bibliothèque de ''n'importe quelle taille'' avec seulement 24 à 100 requêtes par jour (intervalle RSS de 15 à 60 minutes). Si vous comprenez cela, vous réaliserez qu'il ne couvre que le ''futur''.
- Alors comment gérer le présent et le passé ? Lorsque vous ajoutez un album, vous devez définir le chemin correct, le profil et l'état de surveillance, puis utiliser la case à cocher "Démarrer la recherche d'albums manquants". Si l'album n'a pas encore été publié, vous n'avez pas besoin de lancer une recherche.
- En d'autres termes, Lidarr ne trouvera que les sorties qui sont nouvellement téléchargées sur vos indexeurs. Il ne cherchera pas activement à trouver des sorties que vous souhaitez qui ont été téléchargées dans le passé.
- Si vous avez déjà ajouté l'album, mais que vous souhaitez maintenant le rechercher, vous avez plusieurs choix. Vous pouvez aller sur la page de l'album et utiliser le bouton de recherche, qui effectuera une recherche et choisira automatiquement l'un d'entre eux. Vous pouvez utiliser l'onglet Recherche et voir ''toutes'' les résultats, en choisissant celui que vous voulez. Ou vous pouvez utiliser les filtres "Manquant", "Souhaité" ou "Non atteint".
- Si Lidarr a été hors ligne pendant une période prolongée, Lidarr essaiera de revenir en arrière pour trouver la dernière sortie qu'il a traitée afin d'éviter de manquer une sortie. Tant que votre indexeur prend en charge le paginage et que cela n'a pas été trop long, Lidarr pourra traiter les sorties qu'il aurait manquées et éviter que vous ayez besoin de rechercher les sorties manquées.

## Authentification forcée

Si Lidarr est exposé de manière à ce que l'interface utilisateur puisse être accessible depuis l'extérieur de votre réseau local, vous devez avoir une forme d'authentification activée pour accéder à l'interface utilisateur. Cela est également de plus en plus requis par les trackers et les indexeurs.

À partir de Lidarr v2, l'authentification est obligatoire.

### Méthode d'authentification

- `Basic` (Pop-up du navigateur) - Cette option, lors de l'accès à votre Lidarr, affiche une petite fenêtre contextuelle vous permettant de saisir un nom d'utilisateur et un mot de passe.
- `Forms` (Page de connexion) - Cette option affiche un écran de connexion de type familier, comme le font d'autres sites web, pour vous permettre de vous connecter à votre Lidarr.
- `External` - Configurable uniquement via le fichier de configuration
  - Si vous utilisez une **authentification externe** telle que Authelia, Authetik, NGINX Basic auth, etc., vous pouvez éviter d'avoir à vous authentifier deux fois en arrêtant l'application, en définissant `<AuthenticationMethod>External</AuthenticationMethod>` dans le [fichier de configuration](/lidarr/appdata-directory) et en redémarrant l'application. **Notez que plusieurs entrées `AuthenticationMethod` dans le fichier ne sont pas prises en charge et seule la valeur la plus élevée sera utilisée**

### Authentification requise

- Si vous n'exposez pas l'application à l'extérieur et/ou si vous ne souhaitez pas que l'authentification soit requise pour l'accès local (par exemple, LAN), modifiez dans Paramètres => Sécurité générale => Authentification requise en `Désactivée pour les adresses locales`
  - L'équivalent du fichier de configuration est `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Comment les téléchargements possibles sont-ils comparés ?

> En général, la qualité prime sur tout. Si vous souhaitez que la qualité ne soit pas la priorité principale, vous pouvez fusionner vos qualités ensemble. [Voir le guide de TRaSH](https://trash-guides.info/merge-quality)***
{.is-info}

- La logique actuelle [peut être trouvée ici](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs).

- À partir du 23 janvier 2022, la logique est la suivante :

1. Qualité
1. Score de mot préféré
1. Protocole (tel que configuré dans le profil de retard correspondant)
1. Priorité de l'indexeur
1. Seeds/Peers (si Torrent)
1. Nombre d'albums
1. Âge (si Usenet)
1. Taille

## Lidarr a cessé de fonctionner après la mise à jour vers Ubuntu 22.04

- Lidarr v0.8 n'est pas compatible et n'est pas pris en charge sur Ubuntu 22.04
- Seule Lidarr v1 prend en charge Ubuntu 22.04
- [Voir cette entrée de FAQ pour les branches et les versions](#comment-mettre-à-jour-lidarr)

## Pourquoi ne puis-je pas ajouter une nouvelle sortie ou un nouvel artiste à Lidarr ?

- La sortie est probablement de type `inconnu` sur MusicBrainz

## Pourquoi ne puis-je pas ajouter un album d'artistes variés ?

- Les artistes variés et autres artistes méta sur Musicbrainz sont dus au nombre d'entrées qu'ils fournissent.

## Pourquoi Lidarr ne montre-t-il que des albums studio ? Comment puis-je trouver des singles ou des EP ?

- Lidarr est configuré par défaut pour n'importer que des albums studio pour chaque artiste. Cependant, vous pouvez étendre les types d'albums par artiste, ou pour l'ensemble de votre bibliothèque, en utilisant des profils de métadonnées.

## Puis-je ajouter seulement un album ?

- Pas pour le moment.

## Puis-je télécharger des pistes individuelles ?

- Lidarr fonctionne en recherchant et en téléchargeant des sorties complètes, donc les pistes individuelles ne peuvent pas être téléchargées à moins qu'elles ne soient sorties en tant que single par l'artiste.

## Pourquoi l'artiste X n'apparaît-il pas dans la recherche ?

- La recherche est encore en cours de développement. Les artistes qui n'apparaissent pas dans la recherche peuvent être ajoutés en recherchant `lidarr:mbid` où `mbid` est l'ID Musicbrainz de l'artiste.

## Lidarr a associé un album avec trop de pistes. Comment puis-je changer l'album vers la sortie correcte ?

- Ouvrez la page des détails de l'album et sélectionnez l'icône Modifier dans la barre de navigation supérieure. Vous y trouverez une liste déroulante de toutes les sorties liées à cet album.

## Je ne peux pas trouver une sortie dans Lidarr mais elle est sur MusicBrainz

- Cela est probablement dû au fait que la sortie a un statut de sortie `inconnu`. Mettez à jour MusicBrainz.

## À quelle fréquence les bases de données de Lidarr et de MusicBrainz se synchronisent-elles ?

- Toutes les heures, à 5 minutes après l'heure

## Comment puis-je ajouter des images d'artiste manquantes ?

- Ajoutez une image à fanart.tv et attendez ~7+ jours pour qu'elle soit effacée du cache. Ensuite, actualisez les métadonnées.

## Comment puis-je obtenir des images d'album manquantes ? (Art de couverture)

- Ajoutez une couverture à musicbrainz et attendez ~1h+ pour qu'elle soit effacée du cache. Ensuite, actualisez les métadonnées.

## J'ai des problèmes pour importer mes artistes, qu'est-ce que cela peut être ?

- Le processus d'importation des artistes importe uniquement les noms d'artistes et les emplacements de chemin, qui sont ensuite stockés dans la base de données afin que a) les métadonnées puissent être récupérées et b) le contenu téléchargé puisse être placé au même emplacement à l'avenir. À cette fin, le compte utilisateur sous lequel s'exécute Lidarr a besoin à la fois de la lecture et de l'écriture dans votre répertoire de données.

## Comment puis-je renommer mes dossiers d'artistes ?

{#rename-folders}

> Le même processus s'applique également pour déplacer/changer les chemins des artistes.
{.is-info}

1. Bibliothèque
1. Éditeur de masse
1. Sélectionnez les artistes dont vous souhaitez renommer le dossier
1. Changez le dossier racine pour le même dossier racine dans lequel les artistes se trouvent actuellement
1. Sélectionnez "Oui, déplacer les fichiers"

## Comment puis-je supprimer en masse des artistes de la liste des souhaits ?

- Utilisez l'Éditeur de masse => Sélectionnez les artistes que vous souhaitez supprimer => Supprimer

## Pourquoi Lidarr ne fonctionne-t-il pas derrière un proxy inverse

- Lidarr utilise .NET et un nouveau serveur web. Pour que SignalR fonctionne, pour que les boutons de l'interface utilisateur fonctionnent, pour que les modifications de la base de données soient prises en compte et pour d'autres éléments, il est nécessaire d'ajouter les éléments suivants au bloc de localisation pour Lidarr :
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;

- Assurez-vous de `ne pas` inclure `proxy_set_header Connection "Upgrade";` comme suggéré par la documentation de nginx. `CELA NE FONCTIONNERA PAS`
- [Voir ce problème ASP.NET Core](https://github.com/aspnet/AspNetCore/issues/17081)
- Si vous utilisez un CDN comme Cloudflare, assurez-vous que les websockets sont activés pour permettre les connexions websocket.

## Comment mettre à jour Lidarr ?

- Accédez à Paramètres, puis à l'onglet Général et affichez les paramètres avancés (utilisez le bascule près du bouton Enregistrer).

1. Dans la section Mises à jour, changez le nom de la branche en `master` ou `develop`
1. Enregistrez

*Cela n'installera pas immédiatement les éléments de cette branche, cela se produira lors de la prochaine mise à jour.*

- `master` - ![Maître actuel/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Maître&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) - (Par défaut/Stable) : Il a été testé par les utilisateurs sur les branches de développement et nocturnes et il n'est pas connu pour avoir de problèmes majeurs. Cette version recevra des mises à jour environ une fois par mois. Sur GitHub, il s'agit de la branche `master`.

- `develop` - ![Développement actuel/Bêta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Développement&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) - (Bêta) : Il s'agit de la version de test. Elle est publiée après avoir été testée en nocturne pour s'assurer qu'il n'y a pas de problèmes immédiats. Les nouvelles fonctionnalités et les corrections de bugs sont d'abord publiées ici après la nocturne. Elle peut être considérée comme semi-stable, mais reste en version `bêta`. Cette version recevra des mises à jour hebdomadaires ou bimensuelles en fonction du développement.

> **Attention : Vous pourriez ne pas pouvoir revenir à `master` après avoir basculé sur cette branche.** Sur GitHub, il s'agit d'un instantané de la branche `develop` à un moment précis.
{.is-warning}

- `nightly` - ![Nocturne actuel/Instable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nocturne&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) - (Alpha/Instable) : Il s'agit de la version la plus récente. Elle est publiée dès que le code est validé et passe tous les tests automatisés. Cette version peut ne pas avoir été utilisée par nous ou d'autres utilisateurs. Il n'y a aucune garantie qu'elle fonctionnera même dans certains cas. Cette branche est recommandée uniquement pour les utilisateurs avancés. Des problèmes et des enquêtes personnelles sont attendus dans cette branche. ***Utilisez cette branche uniquement si vous savez ce que vous faites et si vous êtes prêt à mettre les mains dans le cambouis pour récupérer une mise à jour échouée.*** Cette version est mise à jour immédiatement.

> **Attention : Vous pourriez ne pas pouvoir revenir à `master` après avoir basculé sur cette branche.** Sur GitHub, il s'agit de la branche `develop`.
{.is-danger}

- Note : Si vous utilisez Docker, ajoutez `:release`, `:latest`, `:testing` ou `:develop` à la fin de votre balise de conteneur en fonction de qui crée vos versions. Veuillez noter que les branches `nightly` ne sont intentionnellement pas répertoriées ci-dessous.

|                                                                    | `master` (stable) ![Maître actuel/Dernier](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Maître&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) | `develop` (bêta) ![Développement actuel/Bêta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Développement&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) | `nightly` (alpha) ![Nocturne actuel/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nocturne&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/lidarr)                       | `release`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-lidarr) | `latest`                                                                                                                                                                                                              | `develop`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |

### Puis-je mettre à jour Lidarr à l'intérieur de mon conteneur Docker ?

- *Techniquement, oui.* **Mais vous ne devriez absolument pas le faire.** C'est une philosophie fondamentale de Docker. Des problèmes de base de données peuvent survenir si vous mettez à niveau votre installation vers la version `nightly` la plus récente, puis mettez à jour le conteneur Docker lui-même (ce qui pourrait revenir à une version plus ancienne).

### Installation d'une version plus récente

#### Natif

1. Accédez à Système, puis à l'onglet Mises à jour.
1. Les versions plus récentes qui ne sont pas encore installées auront un bouton de mise à jour à côté d'elles. Cliquez sur ce bouton pour installer la mise à jour.

#### Docker

1. Répétez l'opération de récupération de votre balise et mettez à jour votre conteneur.

## Puis-je revenir de `nightly` à `develop` ?

## Puis-je passer d'une branche à une autre ?

- Si les versions sont identiques, vous pouvez passer d'une branche à l'autre. Sinon, vérifiez auprès de l'équipe de développement si vous pouvez passer de `nightly` à `master` ; `nightly` à `develop` ; ou `develop` à `master` pour votre version spécifique.
- Si vous ne suivez pas ces instructions, votre Lidarr risque de devenir inutilisable ou de générer des erreurs. Vous avez été prévenu.
  - L'erreur la plus courante est quelque chose comme `Error parsing column 45 (Language=31 - Int64)` ou d'autres erreurs de base de données similaires concernant des colonnes ou des tables manquantes.

## J'obtiens une erreur : Database disk image is malformed

- **Les erreurs de `Error creating log database` indiquent des problèmes avec logs.db**
  - Cela peut être rapidement résolu en renommant ou en supprimant la base de données. La base de données des journaux contient des informations non importantes concernant l'historique des commandes et l'historique des installations de mises à jour, ainsi que des entrées Info, Warn et Error.
- **Les erreurs de `Error creating main database` ou l'erreur générique `database disk image is malformed` sans base de données spécifiée indiquent des problèmes avec lidarr.db**
  - Poursuivez avec les étapes indiquées ci-dessous.
- Cela signifie que votre base de données SQLite qui stocke la plupart des informations de Lidarr est corrompue. Vos options sont d'essayer (un) sauvegarde(s), d'essayer de récupérer la base de données existante, d'essayer de récupérer les sauvegardes, ou si tout échoue, de recommencer avec une nouvelle base de données fraîche.
- Cette erreur peut apparaître si le fichier de base de données n'est pas accessible en écriture par l'utilisateur/groupe sous lequel \*Arr s'exécute. Les autorisations sont susceptibles de poser problème uniquement pour les nouvelles installations, les installations migrées vers un nouveau serveur, si vous avez récemment modifié les autorisations de votre répertoire appdata, ou si vous avez modifié l'utilisateur et le groupe sous lesquels \*Arr s'exécute.
- Votre meilleure et première option est d'essayer de [restaurer à partir d'une sauvegarde](#comment-faire-une-sauvegarderestauration-de-mon-lidarr)
- Vous pouvez également essayer de récupérer votre base de données. C'est généralement la seule option lorsque ce problème se produit après une mise à jour. Essayez la commande [sqlite3 `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Si votre sqlite n'a pas `.recover` ou si vous souhaitez une méthode plus conviviale pour l'interface utilisateur (par exemple, Windows), suivez [nos instructions sur ce wiki](/useful-tools#recovering-a-corrupt-db-ui).
- Une autre cause possible de l'erreur de base de données est que vous placez votre base de données sur un lecteur réseau (nfs ou smb ou autre chose non local). **SQLite est conçu pour des situations où les données et l'application coexistent sur la même machine.** Ainsi, votre dossier \*Arr AppData (/montage config pour Docker) DOIT être stocké localement. [SQLite et les lecteurs réseau ne fonctionnent pas bien ensemble et finiront par provoquer une base de données corrompue](https://www.sqlite.org/draft/useovernet.html).
- Si vous utilisez mergerFS, vous devez supprimer `direct_io` car SQLite utilise mmap, qui n'est pas pris en charge par `direct_io`, comme expliqué dans la documentation de mergerFS [ici](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Comment faire une sauvegarde/restauration de mon Lidarr ?

### Sauvegarde de Lidarr

#### Utilisation de la sauvegarde intégrée

- Accédez à Système => Sauvegarde dans l'interface utilisateur de Lidarr.
- Cliquez sur le bouton Sauvegarder.
- Téléchargez le fichier zip après la création de la sauvegarde pour le conserver en lieu sûr.

#### Utilisation du système de fichiers directement

- Trouvez l'emplacement du répertoire AppData de Lidarr.
  - Via l'interface utilisateur de Lidarr, accédez à Système => À propos.
  - [Répertoire AppData de Lidarr](/lidarr/appdata-directory)
- Arrêtez Lidarr - Cela empêchera la base de données de se corrompre.
- Copiez le contenu vers un emplacement sûr.

### Restauration à partir d'une sauvegarde

> La restauration sur un système d'exploitation qui utilise des chemins différents ne fonctionnera pas (Windows vers Linux, Linux vers Windows, Windows vers OS X ou OS X vers Windows). La migration entre OS X et Linux peut fonctionner, car les deux utilisent des chemins contenant `/` au lieu de `\` utilisé par Windows, mais cela n'est pas pris en charge. Vous devrez modifier manuellement tous les chemins dans la base de données.
{.is-warning}

#### Utilisation de la sauvegarde au format zip

- Réinstallez Lidarr (si applicable / non déjà installé).
- Lancez Lidarr.
- Accédez à Système => Sauvegarde.
- Sélectionnez Restaurer la sauvegarde.
- Sélectionnez Choisir le fichier.
- Sélectionnez votre fichier de sauvegarde au format zip.
- Sélectionnez Restaurer.

#### Utilisation de la sauvegarde du système de fichiers

- Réinstallez Lidarr (si applicable / non déjà installé).
- Trouvez l'emplacement du répertoire AppData de Lidarr.
  - Exécutez Lidarr une fois et accédez à Système => À propos via l'interface utilisateur.
  - [Répertoire AppData de Lidarr](/lidarr/appdata-directory)
- Arrêtez Lidarr.
- Supprimez le contenu du répertoire AppData **(y compris les fichiers .db-wal/.db-journal s'ils existent)**.
- Restaurez à partir de votre sauvegarde.
- Démarrez Lidarr.
- Tant que les chemins sont les mêmes, tout reprendra là où vous vous étiez arrêté.

#### Restauration du système de fichiers sur un NAS Synology

> ATTENTION : La restauration sur un Synology nécessite des connaissances en Linux et un accès SSH root à l'appareil Synology.
{.is-warning}

- Réinstallez Lidarr (si applicable / non déjà installé).
- Trouvez l'emplacement du répertoire AppData de Lidarr.
  - Exécutez Lidarr une fois et accédez à Système => À propos via l'interface utilisateur.
  - [Répertoire AppData de Lidarr](/lidarr/appdata-directory)
- Arrêtez Lidarr.
- Connectez-vous au NAS Synology via SSH et connectez-vous en tant que root.

> Sur certaines installations, l'utilisateur est différent des commandes ci-dessous : `chown -R sc-Lidarr:Lidarr *` {.is-info}

- Exécutez les commandes suivantes :

```shell
rm -r /usr/local/Lidarr/var/.config/Lidarr/Lidarr.db
cp -f /tmp/Lidarr_backup/* /usr/local/Lidarr/var/.config/Lidarr/
```

- Mettez à jour les autorisations sur les fichiers :

 ```shell
cd /usr/local/Lidarr/var/.config/Lidarr/
chown -R Lidarr:users *
chmod -R 0644 *
```

- Démarrez Lidarr

## J'utilise Lidarr sur un Mac et il a soudainement cessé de fonctionner. Que s'est-il passé ?

- Il s'agit très probablement d'un bogue de MacOS qui a provoqué la corruption de l'une des bases de données.

- Voir l'entrée ci-dessus "Database is malformed".

- Ensuite, essayez de le lancer et voyez s'il fonctionne. S'il ne fonctionne pas, vous aurez besoin d'un support supplémentaire. Postez sur notre [subreddit /r/lidarr](http://reddit.com/r/lidarr) ou rejoignez [notre discord](https://lidarr.audio/discord) pour obtenir de l'aide.

## J'utilise un Raspberry Pi et Raspbian et Lidarr ne se lance pas

Raspbian dispose d'une version de libseccomp2 trop ancienne pour prendre en charge l'exécution d'un conteneur Docker basé sur Ubuntu 20.04, que hotio et LinuxServer utilisent tous deux comme base. Vous devez soit utiliser `--privileged`, mettre à jour libseccomp2 à partir d'Ubuntu, soit obtenir un meilleur système d'exploitation (nous recommandons Ubuntu 20.04 arm64).

**Solution possible :**

J'ai réussi à résoudre le problème en installant le backport depuis le dépôt Debian. Il n'est généralement pas recommandé d'utiliser le backport en mode de mise à niveau général. L'installation d'un seul paquet peut être acceptable, mais peut également causer des problèmes. Il est donc important de comprendre ce que vous faites.

Voici les étapes pour résoudre le problème :

Assurez-vous d'exécuter Raspbian Buster, par exemple en utilisant `lsb_release -a`

> Distributor ID: Raspbian
> Description: Raspbian GNU/Linux 10 (buster)
> Release: 10
> Codename: buster

- Si vous utilisez Buster :
  - Exécutez la commande suivante pour ajouter les backports à vos sources

  ```shell
   echo "deb <http://deb.debian.org/debian> buster-backports main" | sudo tee /etc/apt/sources.list.d/buster-backports.list
   ```

  - Installez le backport de libseccomp2

  ```shell
  sudo apt update && sudo apt-get -t buster-backports install libseccomp2
  ```

## Pourquoi les temps de synchronisation des listes sont-ils si longs et puis-je les modifier ?

Les listes n'ont jamais été et ne sont pas censées être des outils de type "ajoutez-le maintenant", mais plutôt des outils de type "ajoutez-le éventuellement".

Vous pouvez déclencher une actualisation manuelle de la liste, la scripter et la déclencher via l'API, ou ajouter directement les versions à Lidarr.

Ce changement a été fait pour éviter que notre serveur ne soit surchargé par les mises à jour des listes toutes les 10 minutes.

## Puis-je désactiver la tâche de rafraîchissement des versions ?

Non, et vous ne devriez pas le faire en utilisant des manipulations SQL. La tâche de rafraîchissement des versions interroge le proxy Servarr en amont et vérifie si les métadonnées de chaque version (identifiants, casting, résumé, évaluation, traductions, titres alternatifs, etc.) ont été mises à jour par rapport à ce qui est actuellement dans Lidarr. Si nécessaire, elle mettra à jour les versions concernées.

Une plainte courante est que la tâche de rafraîchissement provoque une utilisation intensive des E/S. Un paramètre qui peut poser problème est "Rescan Artist Folder after Refresh". Si votre utilisation des E/S du disque augmente pendant un rafraîchissement, vous voudrez peut-être modifier le paramètre de rescan en `Manuel`. Ne le changez pas en `Jamais` à moins que toutes les modifications de votre bibliothèque (nouvelles versions, mises à niveau, suppressions, etc.) ne soient effectuées via Lidarr. Si vous supprimez manuellement des fichiers de version ou utilisez un programme tiers, ne définissez pas ce paramètre sur `Jamais`.

## Pourquoi Lidarr ne peut-il pas voir mes fichiers sur un serveur distant ?

- Pour tous les systèmes d'exploitation, assurez-vous que l'utilisateur/groupe avec lequel vous exécutez \*Arr dispose des droits de lecture et d'écriture sur le lecteur monté.
- Pour Linux, assurez-vous de :
  - Si vous utilisez un montage NFS, activez `nolock` pour votre montage.
  - Si vous utilisez un montage SMB, activez `nobrl` pour votre montage.
- Pour Windows : En bref, l'utilisateur avec lequel \*Arr s'exécute (s'il s'agit d'un service) ou sous lequel il s'exécute (s'il s'agit d'une application de la barre d'état système) ne peut pas accéder au chemin d'accès du fichier sur le serveur distant. Cela peut être dû à différentes raisons, mais la plus courante est que \*Arr s'exécute en tant que service, ce qui provoque les problèmes décrits ci-dessous.

### Lidarr s'exécute par défaut sous le compte LocalService qui n'a pas accès aux partages de fichiers distants protégés

- Exécutez le service Lidarr en tant qu'un autre utilisateur ayant accès à ce partage.
- Ouvrez la fenêtre "Outils d'administration" > "Services" sur votre serveur Windows.
- Arrêtez le service Lidarr.
- Ouvrez la boîte de dialogue "Propriétés" > "Connexion".
- Modifiez le compte utilisateur du service pour utiliser le compte utilisateur cible.
- Exécutez Lidarr.exe à l'aide du dossier de démarrage

### Vous utilisez un lecteur réseau mappé (et non un chemin UNC)

- Modifiez vos chemins d'accès en chemins UNC (`\\serveur\partage`)
- Exécutez Lidarr.exe via le dossier de démarrage

## Aide, je me suis verrouillé dehors

{#help-i-have-forgotten-my-password}

Pour désactiver l'authentification (pour réinitialiser votre nom d'utilisateur ou votre mot de passe oublié), vous devrez modifier `config.xml` qui se trouve dans le [répertoire des données de l'application Lidarr](/lidarr/appdata-directory).

1. Ouvrez config.xml dans un éditeur de texte.
2. Recherchez la ligne de méthode d'authentification qui sera `<AuthenticationMethod>Basic</AuthenticationMethod>` ou `<AuthenticationMethod>Forms</AuthenticationMethod>`.
3. Modifiez la ligne `AuthenticationMethod` en `<AuthenticationMethod>None</AuthenticationMethod>`.
4. Redémarrez Lidarr.
5. Lidarr sera maintenant accessible sans mot de passe. Vous devriez aller dans les `Paramètres : Général` de l'interface utilisateur et définir votre nom d'utilisateur et votre mot de passe.

## Comment empêcher le navigateur de se lancer au démarrage ?

Selon votre système d'exploitation, il existe plusieurs façons possibles.

- Dans `Paramètres` => `Général` sur certains systèmes d'exploitation, il y a une case à cocher pour lancer le navigateur au démarrage.
- Lorsque vous invoquez Lidarr, vous pouvez ajouter `-nobrowser` (*nix) ou `/nobrowser` (Windows) aux arguments.
- Arrêtez Lidarr, modifiez le fichier config.xml et changez `<LaunchBrowser>True</LaunchBrowser>` en `<LaunchBrowser>False</LaunchBrowser>`.

## Problèmes d'interface utilisateur étranges

- Si vous rencontrez des problèmes d'interface utilisateur étranges, comme l'absence de liste sur la page de la bibliothèque ou un affichage ou un tri spécifique qui ne fonctionne pas, essayez de visualiser dans une fenêtre de navigation privée Chrome ou une fenêtre privée Firefox. Si cela fonctionne correctement, videz le cache et les cookies de votre navigateur pour votre adresse IP/domaine spécifique. Pour plus d'informations, consultez l'article du wiki [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage).

## VPN, Jackett et les \*ARRs

- Sauf si vous vous trouvez dans un pays répressif comme la Chine, l'Australie ou l'Afrique du Sud, votre client torrent est généralement le seul élément qui doit être derrière un VPN. Étant donné que le point de terminaison VPN est partagé par de nombreux utilisateurs, vous pouvez rencontrer des limitations de débit, une protection contre les attaques par déni de service et des interdictions d'adresse IP de la part des différents services utilisés par chaque logiciel.
- En d'autres termes, mettre les \*Arrs (Lidarr, Prowlarr, Radarr, Readarr et Lidarr) derrière un VPN peut rendre les applications inutilisables dans certains cas en raison de l'inaccessibilité des services.

> **Pour être clair, il ne s'agit pas de savoir si les VPN vont causer des problèmes avec les \*Arrs, mais quand : les fournisseurs d'images vous bloqueront et Cloudflare est en face de la plupart des serveurs \*Arr (mises à jour, métadonnées, etc.) et peut également vous bloquer.**
{.is-warning}

- **De nombreux trackers privés vous interdiront d'utiliser ou d'accéder à leurs services (par exemple, en utilisant Jackett ou Prowlarr) via un VPN.**

### Utilisation d'un VPN

- Si un VPN est nécessaire et que Docker est utilisé, il est recommandé d'utiliser les conteneurs Hotio ou Binhex's Download Client + VPN.
- Si un VPN est nécessaire et que Docker n'est pas utilisé, votre client VPN ***doit*** prendre en charge le fractionnement du tunnel afin que seules les applications requises (client de téléchargement) soient derrière le VPN.
- De nombreux problèmes d'accès aux trackers peuvent être résolus en utilisant les serveurs DNS de Google ou de Cloudflare à la place des serveurs DNS de votre fournisseur d'accès Internet.
- Dans certains cas (par exemple, les fournisseurs de services Internet britanniques), vous devrez peut-être mettre votre client de téléchargement de torrents derrière un VPN et Jackett/Prowlarr de la manière suivante :
  - mettez Jackett derrière le VPN et assurez-vous que le fractionnement du tunnel permet l'accès local
  - pour Prowlarr, configurez votre client VPN pour fournir un proxy et ajoutez le proxy dans Paramètres => Indexeurs. Attribuez une étiquette au proxy et utilisez la même étiquette pour les indexeurs qui doivent l'utiliser.
    - Si nécessaire et si votre VPN ne permet pas de créer un proxy, vous pouvez mettre Prowlarr derrière le VPN et vous assurer que le fractionnement du tunnel permet l'accès local.

## Point de terminaison /all de Jackett

{#jackett-all-endpoint}

- Le point de terminaison `/all` de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc nécessaire d'ajouter chaque tracker individuellement. Vous pouvez également envisager d'utiliser l'alternative Jackett & NZBHydra2 [Prowlarr](/prowlarr).
- **Mise à jour d'avril 2022 : la prise en charge des \*Arr a été supprimée pour le point de terminaison `/all` de Jackett car il ne cause que des problèmes.**
- Le point de terminaison /all de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc désormais nécessaire d'ajouter chaque tracker individuellement.
- [Même les développeurs de Jackett disent qu'il faut l'éviter et ne pas l'utiliser.](https://github.com/Jackett/Jackett#aggregate-indexers)
- L'utilisation du point de terminaison /all n'a aucun avantage, seulement des inconvénients :
  - vous perdez le contrôle sur les paramètres spécifiques à chaque indexeur (catégories, modes de recherche, etc.)
  - mélanger les modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
  - les catégories spécifiques à chaque indexeur (\>= 100000) ne peuvent pas être utilisées.
  - les indexeurs lents ralentiront le résultat global
  - le nombre total de résultats est limité à 1000
  - si l'un des trackers dans /all renvoie une erreur, \*Arr le désactivera et vous n'obtiendrez aucun résultat.

### Solutions pour Jackett /All

- Ajoutez chaque tracker manuellement dans Jackett en tant qu'indexeur dans \*Arr.
- Consultez [Prowlarr](/prowlarr) qui peut synchroniser les indexeurs avec \*Arr et qui est développé par l'équipe de Lidarr/Radarr/Readarr.
- Consultez [NZBHydra2](https://github.com/theotherp/nzbhydra2) qui peut synchroniser les indexeurs avec \*Arr. Mais n'utilisez pas leur point de terminaison unique et utilisez `multi` si la synchronisation est utilisée.

## Pourquoi y a-t-il deux fichiers ? | Pourquoi reste-t-il un fichier dans les téléchargements ?

C'est normal. Avec une configuration prenant en charge les [liens physiques](https://trash-guides.info/hardlinks), aucun espace supplémentaire ne sera utilisé. Voici comment fonctionne le processus de torrent.

1. Lidarr envoie une demande de téléchargement à votre client et l'associe à un label ou à une catégorie que vous avez configuré dans les paramètres du client de téléchargement. Exemples : films, séries TV, musique, etc.
2. Lidarr surveille les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
3. Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de partager le fichier (le ratio ou la durée peuvent être ajustés dans les paramètres du client de téléchargement ou depuis Lidarr pour le téléchargement spécifique). Lorsque les fichiers sont importés dans votre dossier multimédia, ils sont liés physiquement s'ils sont pris en charge par votre configuration, sinon ils sont copiés.
4. Si l'option "Gestion des téléchargements terminés - Supprimer les téléchargements terminés" est activée dans les paramètres de Lidarr, Lidarr supprimera le fichier et le torrent d'origine de votre client de téléchargement, mais seulement si le client de téléchargement signale que le partage est terminé et que le torrent est arrêté (c'est-à-dire en pause). Consultez les [Guides des clients de téléchargement de TRaSH](https://trash-guides.info/Downloaders/) pour savoir comment configurer votre client de téléchargement de manière optimale.

> Les liens physiques sont activés par défaut. [Un lien physique ne nécessite pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien physique échoue ou si votre configuration ne prend pas en charge les liens physiques, une copie du fichier sera effectuée.
{.is-info}

## Je reçois constamment des avertissements de mon stockage cloud concernant les limites de l'API

Lidarr n'est pas comme les autres Arrs. Il utilise des balises au lieu des noms de fichiers pour fonctionner. Si vous conservez les fichiers Lidarr sur un stockage cloud, il doit télécharger le fichier pour lire les balises. Cela dépassera très rapidement les limites d'API que vous avez sur votre fournisseur de stockage. Nous vous déconseillons vivement de conserver votre bibliothèque Lidarr sur un fournisseur de stockage cloud, et les problèmes que vous rencontrez sont probablement dus à cette configuration.