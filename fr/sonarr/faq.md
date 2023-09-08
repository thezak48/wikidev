---
title: FAQ Sonarr
description: 
published: true
date: 2023-08-28T19:31:41.131Z
tags: 
editor: markdown
dateCreated: 2021-06-09T18:39:33.208Z
---

<!-- # Table des matières

- [Table des matières](#table-des-matières)
- [Principes de base de Sonarr](#principes-de-base-de-sonarr)
  - [Comment Sonarr trouve-t-il les épisodes ?](#comment-sonarr-trouve-t-il-les-épisodes)
  - [Comment les téléchargements possibles sont-ils comparés ?](#comment-les-téléchargements-possibles-sont-ils-comparés)
  - [FAQ sur les mots préférés](#faq-sur-les-mots-préférés)
  - [Comment passer du service Windows à une application en arrière-plan ?](#comment-passer-du-service-windows-à-une-application-en-arrière-plan)
  - [Comment sauvegarder/restaurer mon Sonarr ?](#comment-sauvegarderrestaurer-mon-sonarr)
    - [Sauvegarde de Sonarr](#sauvegarde-de-sonarr)
      - [Utilisation de la sauvegarde intégrée](#utilisation-de-la-sauvegarde-intégrée)
      - [Utilisation du système de fichiers directement](#utilisation-du-système-de-fichiers-directement)
    - [Restauration à partir d'une sauvegarde](#restauration-à-partir-dune-sauvegarde)
      - [Utilisation de la sauvegarde au format zip](#utilisation-de-la-sauvegarde-au-format-zip)
      - [Utilisation de la sauvegarde du système de fichiers](#utilisation-de-la-sauvegarde-du-système-de-fichiers)
      - [Restauration du système de fichiers sur un NAS Synology](#restauration-du-système-de-fichiers-sur-un-nas-synology)
  - [Aide, je me suis bloqué !](#aide-je-me-suis-bloqué-)
  - [Pourquoi y a-t-il deux fichiers ? \| Pourquoi y a-t-il un fichier restant dans les téléchargements ?](#pourquoi-y-a-t-il-deux-fichiers--pourquoi-y-a-t-il-un-fichier-restant-dans-les-téléchargements-)
  - [Je vois que la fonctionnalité/le bogue X a été corrigé(e), pourquoi ne puis-je pas le voir ?](#je-vois-que-la-fonctionnalitéle-bogue-x-a-été-corrigée-pourquoi-ne-puis-je-pas-le-voir-)
  - [Progression de l'épisode - Comment est-elle calculée ?](#progression-de-lépisode---comment-est-elle-calculée-)
  - [Comment accéder à Sonarr depuis un autre ordinateur ?](#comment-accéder-à-sonarr-depuis-un-autre-ordinateur-)
  - [Pourquoi Sonarr actualise-t-il si fréquemment les informations sur les séries ?](#pourquoi-sonarr-actualise-t-il-si-fréquemment-les-informations-sur-les-séries-)
  - [Pourquoi y a-t-il un nombre à côté de l'activité ?](#pourquoi-y-a-t-il-un-nombre-à-côté-de-lactivité-)
  - [Quels sont les différents types de séries ?](#quels-sont-les-différents-types-de-séries-)
    - [Types de séries](#types-de-séries)
    - [Exemples de types de séries](#exemples-de-types-de-séries)
      - [Quotidien](#quotidien)
      - [Standard](#standard)
      - [Anime](#anime)
  - [Comment puis-je renommer mes dossiers de séries ?](#comment-puis-je-renommer-mes-dossiers-de-séries-)
  - [Comment mettre à jour Sonarr ?](#comment-mettre-à-jour-sonarr-)
    - [Installation d'une version plus récente](#installation-dune-version-plus-récente)
      - [Native](#native)
      - [Docker](#docker)
  - [Puis-je passer de `develop` à `main` ?](#puis-je-passer-de-develop-à-main-)
  - [Puis-je passer d'une branche à une autre ?](#puis-je-passer-dune-branche-à-une-autre-)
- [Problèmes courants de Sonarr et des séries + métadonnées](#problèmes-courants-de-sonarr-et-des-séries--métadonnées)
  - [Comment Sonarr gère-t-il les problèmes de numérotation des scènes (American Dad!, etc.) ?](#comment-sonarr-gère-t-il-les-problèmes-de-numérotation-des-scènes-american-dad-etc-)
    - [Comment Sonarr gère-t-il les problèmes de numérotation des scènes](#comment-sonarr-gère-t-il-les-problèmes-de-numérotation-des-scènes)
    - [Séries problématiques](#séries-problématiques)
  - [Pourquoi Sonarr ne peut-il pas importer les fichiers d'épisodes pour la série X ? / Pourquoi Sonarr ne peut-il pas trouver de versions pour la série X ?](#pourquoi-sonarr-ne-peut-il-pas-importer-les-fichiers-dépisodes-pour-la-série-x--pourquoi-sonarr-ne-peut-il-pas-trouver-de-versions-pour-la-série-x-)
  - [TVDb est mis à jour, pourquoi Sonarr ne l'est-il pas ?](#tvdb-est-mis-à-jour-pourquoi-sonarr-ne-lest-il-pas-)
  - [Pourquoi ne puis-je pas ajouter une série ?](#pourquoi-ne-puis-je-pas-ajouter-une-série-)
  - [Pourquoi ne puis-je pas ajouter une série lorsque je connais l'ID TVDb ?](#pourquoi-ne-puis-je-pas-ajouter-une-série-lorsque-je-connais-lid-tvdb-)
  - [Slug de titre déjà utilisé](#slug-de-titre-déjà-utilisé)
  - [L'épisode n'a pas de numéro absolu](#lépisode-na-pas-de-numéro-absolu)
  - [Horaires de diffusion des épisodes](#horaires-de-diffusion-des-épisodes)
- [Problèmes courants de Sonarr](#problèmes-courants-de-sonarr)
  - [Le chemin est déjà configuré pour une série existante](#le-chemin-est-déjà-configuré-pour-une-série-existante)
  - [L'épisode n'a pas de durée](#les-logs-du-système-se-chargent-indéfiniment)
  - [Problèmes d'interface utilisateur étranges](#problèmes-dinterface-utilisateur-étranges)
  - [L'interface Web ne se charge qu'en local sur Windows](#linterface-web-ne-se-charge-quen-local-sur-windows)
  - [uTorrent ne fonctionne plus](#utorrent-ne-fonctionne-plus)
  - [Sonarr nécessite-t-il un script de post-traitement SABnzbd pour importer les épisodes téléchargés ?](#sonarr-nécessite-t-il-un-script-de-post-traitement-sabnzbd-pour-importer-les-épisodes-téléchargés-)
  - [J'ai reçu une fenêtre contextuelle indiquant que config.xml était corrompu, que dois-je faire maintenant ?](#jai-reçu-une-fenêtre-contextuelle-indiquant-que-configxml-était-corrompu-que-dois-je-faire-maintenant-)
  - [Sonarr sur Synology a cessé de fonctionner (SSL)](#sonarr-sur-synology-a-cessé-de-fonctionner-ssl)
  - [Certificat invalide et autres problèmes HTTPS ou SSL](#certificat-invalide-et-autres-problèmes-https-ou-ssl)
  - [Comment empêcher le navigateur de se lancer au démarrage ?](#comment-empêcher-le-navigateur-de-se-lancer-au-démarrage-)
  - [VPNs, Jackett et les \*ARRs](#vpns-jackett-et-les-arrs)
  - [Je vois des messages de journal pour des émissions que je n'ai pas/que je ne veux pas](#je-vois-des-messages-de-journal-pour-des-émissions-que-je-nai-pasque-je-ne-veux-pas)
  - [Les torrents en cours de partage ne sont pas supprimés automatiquement](#les-torrents-en-cours-de-partage-ne-sont-pas-supprimés-automatiquement)
  - [Aide, mon Mac dit que Sonarr ne peut pas être ouvert car le développeur ne peut pas être vérifié](#aide-mon-mac-dit-que-sonarr-ne-peut-pas-être-ouvert-car-le-développeur-ne-peut-pas-être-vérifié)
  - [Aide, mon Mac dit que Sonarr.app est endommagé et ne peut pas être ouvert](#aide-mon-mac-dit-que-sonarrapp-est-endommagé-et-ne-peut-pas-être-ouvert)
  - [J'obtiens une erreur : L'image disque de la base de données est corrompue](#jobtiens-une-erreur-limage-disque-de-la-base-de-données-est-corrompue)
  - [J'utilise Sonarr sur un Mac et il a soudainement cessé de fonctionner. Que s'est-il passé ?](#jutilise-sonarr-sur-un-mac-et-il-a-soudainement-cessé-de-fonctionner-que-sest-il-passé-)
  - [Pourquoi Sonarr ne peut-il pas voir mes fichiers sur un serveur distant ?](#pourquoi-sonarr-ne-peut-il-pas-voir-mes-fichiers-sur-un-serveur-distant-)
    - [Sonarr s'exécute par défaut sous le compte LocalService qui n'a pas accès aux partages de fichiers distants protégés](#sonarr-sexécute-par-défaut-sous-le-compte-localservice-qui-na-pas-accès-aux-partages-de-fichiers-distants-protégés)
    - [Vous utilisez un lecteur réseau mappé (pas un chemin UNC)](#vous-utilisez-un-lecteur-réseau-mappé-pas-un-chemin-unc)
  - [Lecteurs réseau mappés vs chemins UNC](#lecteurs-réseau-mappés-vs-chemins-unc)
  - [Sonarr ne fonctionnera pas sur Big Sur](#sonarr-ne-fonctionnera-pas-sur-big-sur)
  - [Mon script personnalisé a cessé de fonctionner après la mise à niveau depuis la version 2](#mon-script-personnalisé-a-cessé-de-fonctionner-après-la-mise-à-niveau-depuis-la-version-2)
- [Problèmes courants de recherche et de téléchargement de Sonarr](#problèmes-courants-de-recherche-et-de-téléchargement-de-sonarr)
  - [Requête réussie - Aucun résultat renvoyé](#requête-réussie---aucun-résultat-renvoyé)
  - [Pourquoi Sonarr n'a-t-il pas récupéré un épisode que j'attendais ?](#pourquoi-sonarr-na-t-il-pas-récupéré-un-épisode-que-jattendais-)
  - [Série correspondante trouvée via l'historique des téléchargements, mais la version a été associée à la série par ID. L'importation automatique n'est pas possible](#série-correspondante-trouvée-via-lhistorique-des-téléchargements-mais-la-version-a-été-associée-à-la-série-par-id-limportation-automatique-nest-pas-possible)
  - [Pourquoi Sonarr n'importe-t-il pas un épisode TBA ?](#pourquoi-sonarr-nimporte-t-il-pas-un-épisode-tba-)
  - [Sonarr indique "Série inconnue" lors des recherches ou des importations](#sonarr-indique-série-inconnue-lors-des-recherches-ou-des-importations)
  - [Point de terminaison /all de Jackett](#point-de-terminaison-all-de-jackett)
    - [Solutions Jackett /All](#solutions-jackett-all)
  - [Jackett affiche plus de résultats que Sonarr lors de la recherche manuelle](#jackett-affiche-plus-de-résultats-que-sonarr-lors-de-la-recherche-manuelle)
  - [Recherche de cookies](#recherche-de-cookies)
  - [Décompresser les torrents](#décompresser-les-torrents)
  - [Autorisations](#autorisations)
-->
# Principes de base de Sonarr

## Comment Sonarr trouve-t-il les épisodes ?

- Sonarr ne recherche pas régulièrement les fichiers d'épisodes manquants ou qui n'ont pas atteint leurs objectifs de qualité. Au lieu de cela, il interroge assez fréquemment vos indexeurs et trackers pour tous les épisodes nouvellement publiés/nouvelles versions téléchargées, puis les compare avec sa liste d'épisodes manquants ou devant être améliorés. Toutes les correspondances sont téléchargées. Cela permet à Sonarr de couvrir une bibliothèque de n'importe quelle taille avec seulement 24 à 100 requêtes par jour (intervalle RSS de 15 à 60 minutes). Si vous comprenez cela, vous réaliserez qu'il ne couvre que le futur.
- Comment faire face au présent et au passé ? Lorsque vous ajoutez une émission, vous devez définir le chemin correct, le profil et l'état de surveillance, puis utiliser la case à cocher "Démarrer la recherche des épisodes manquants". Si l'émission n'a pas eu d'épisodes et n'a pas encore été diffusée, vous n'avez pas besoin de lancer une recherche.
- En d'autres termes, Sonarr ne trouvera que les versions téléchargées récemment sur vos indexeurs. Il ne cherchera pas activement les versions téléchargées dans le passé.
- Si vous avez déjà ajouté l'émission, mais que vous souhaitez maintenant la rechercher, vous avez plusieurs choix. Vous pouvez vous rendre sur la page de l'émission et utiliser le bouton de recherche, qui effectuera une recherche puis choisira automatiquement l'épisode (ou les épisodes). Vous pouvez rechercher des épisodes ou des saisons individuellement de manière automatique ou manuelle. Ou vous pouvez vous rendre à l'onglet [Recherchés](/sonarr/wanted) et effectuer une recherche à partir de là.
- Si Sonarr a été hors ligne pendant une période prolongée, Sonarr tentera de revenir en arrière pour trouver la dernière version qu'il a traitée afin d'éviter de manquer une version. Tant que votre indexeur prend en charge le retour en arrière et que cela n'a pas été trop long, Sonarr pourra traiter les versions qu'il aurait manquées et vous éviter d'avoir à effectuer une recherche pour les épisodes manqués.

### Cas où la recherche automatique se produit

La recherche active (via l'API de l'indexeur) n'est effectuée que dans les situations suivantes. Notez que les mêmes règles que d'habitude s'appliquent : la série + l'épisode doivent être surveillés et les épisodes sans date de diffusion sont ignorés.

- Recherche automatique ou manuelle déclenchée
  - Recherche déclenchée par l'utilisateur ou l'API. Généralement exécutée en cliquant sur les boutons de recherche automatique ou manuelle sur un épisode, une saison ou une série spécifique.
- Ajout d'une émission à l'aide du bouton Ajouter et rechercher
- Utilisation de Recherchés => Manquants ou Recherchés => Coupure non atteinte pour effectuer une ou plusieurs recherches
- Épisodes récemment diffusés ajoutés après la diffusion
  - Si un nouvel épisode est ajouté à Sonarr et qu'il a été diffusé au cours des 14 derniers jours ou dans le futur immédiat (pour couvrir les épisodes qui peuvent être diffusés un peu plus tôt), Sonarr **recherchera** ces épisodes après que le dossier de la série ait été analysé à nouveau (pour détecter les éléments importés en dehors de Sonarr)

## Comment les téléchargements possibles sont-ils comparés ?

> En général, la qualité prime sur tout le reste. Si vous ne souhaitez pas que la qualité soit la priorité principale, vous pouvez fusionner vos qualités ensemble. [Voir le guide de TRaSH](https://trash-guides.info/merge-quality)
{.is-info}

- La logique actuelle [peut toujours être trouvée ici](https://github.com/Sonarr/Sonarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs#L31-L40s).

- À partir du 23 janvier 2022, la logique est la suivante :

1. Qualité
1. Langue
1. Score des mots préférés\*
1. Protocole (tel que configuré dans le profil de retard correspondant)
1. Nombre d'épisodes\*
1. Numéro d'épisode
1. Priorité de l'indexeur
1. Seeds/Peers (si Torrent)
1. Âge (si Usenet)
1. Taille

> Les REPACKS et PROPERs sont la v2 des Qualités et sont donc classés au-dessus d'une version non repack de la même qualité. [Définissez Gestion des supports => Gestion des fichiers `Télécharger les versions Repack & Proper` sur "Ne pas préférer"](/sonarr/settings#file-management) et utilisez une expression régulière de mots préférés `/\b(repack|proper)\b/i` avec un score positif comme suggéré par [les guides de TRaSH](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#p2p-groups-repackproper)
{.is-warning}

> \* Les mots préférés mettent toujours à niveau une version même si la qualité et/ou la coupure de langue ont été atteintes. Cela inclut si le profil a les mises à niveau désactivées.
> \* Les mots préférés remplacent la préférence standard des packs de saisons. Il s'agit de [l'issue Github de Sonarr n°3562](https://github.com/Sonarr/Sonarr/issues/3562). Pour préférer les packs de saisons lors de l'utilisation de mots préférés, vous devez [ajouter une préférence de pack de saisons également](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs)
{.is-info}

## FAQ sur les mots préférés

- Pour le score du fichier sur le disque : le nom existant du fichier et le "nom de scène original" de la version sont évalués pour les mots préférés. Le score le plus élevé des deux est retenu.

- Comment les mots préférés sont-ils inclus dans le renommage ?

  - Pour Sonarr, vous pouvez utiliser le jeton `{Mots préférés}` dans votre schéma de renommage et également activer `Inclure les préférés lors du renommage` dans le profil de version. Consultez [le schéma de renommage recommandé par TRaSH](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/) pour des exemples de schémas de renommage recommandés pour Sonarr. L'utilisation des jetons dans votre schéma de renommage peut aider à résoudre les problèmes de boucle de téléchargement.

- À partir de la version 3.0.7, vous pouvez également inclure les mots préférés sur la base d'un profil de version `{Mots préférés:<Nom du profil de version>}`

- Les mots préférés mettent toujours à niveau une version même si la qualité et/ou la coupure de langue ont été atteintes. Cela inclut si le profil a les `Mises à niveau` désactivées.

> Les mots préférés remplacent la préférence standard des packs de saisons. Il s'agit de [l'issue Github de Sonarr n°3562](https://github.com/Sonarr/Sonarr/issues/3562). Pour préférer les packs de saisons lors de l'utilisation de mots préférés, vous devez [ajouter une préférence de pack de saisons également](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs)
{.is-info}

- Les balises peuvent être utilisées pour contrôler à quelles séries un profil de version s'applique ; consultez l'entrée des paramètres pour les profils de version pour plus d'informations

- Pour plus d'informations sur les mots préférés et les profils de version, [consultez la page des paramètres](/sonarr/settings#release-profiles)

## Comment passer du service Windows à une application en arrière-plan ?

1. Arrêtez Sonarr.
1. Exécutez serviceuninstall.exe qui se trouve dans le répertoire de Sonarr.
1. Exécutez Sonarr.exe en tant qu'administrateur une fois pour lui donner les autorisations appropriées et ouvrir le pare-feu. Une fois terminé, vous pouvez le fermer et l'exécuter normalement.
1. (Facultatif) Ajoutez un raccourci vers Sonarr.exe dans le dossier de démarrage pour le démarrer automatiquement au démarrage.

## Comment sauvegarder/restaurer mon Sonarr ?

### Sauvegarde de Sonarr

#### Utilisation de la sauvegarde intégrée

- Accédez à Système => Sauvegarde dans l'interface utilisateur de Sonarr.
- Cliquez sur le bouton Sauvegarder.
- Téléchargez le fichier zip après la création de la sauvegarde pour le conserver en lieu sûr.

#### Utilisation du système de fichiers directement

- Trouvez l'emplacement du répertoire AppData de Sonarr.
  - Via l'interface utilisateur de Sonarr, accédez à Système => À propos.
  - [Répertoire AppData de Sonarr](/sonarr/appdata-directory)
- Arrêtez Sonarr - Cela empêchera la corruption de la base de données.
- Copiez le contenu vers un emplacement sûr.

### Restauration à partir d'une sauvegarde

> La restauration sur un système d'exploitation utilisant des chemins différents ne fonctionnera pas (Windows vers Linux, Linux vers Windows, Windows vers macOS ou macOS vers Windows). Le passage entre macOS et Linux peut fonctionner, car les deux utilisent des chemins contenant `/` au lieu de `\` utilisé par Windows, mais cela n'est pas pris en charge. Vous devrez modifier manuellement tous les chemins dans la base de données ou utiliser [Toolbarr](https://github.com/Notifiarr/toolbarr).
{.is-warning}

#### Utilisation de la sauvegarde au format zip

- Réinstallez Sonarr (si applicable / non déjà installé).
- Exécutez Sonarr.
- Accédez à Système => Sauvegarde.
- Sélectionnez Restaurer la sauvegarde.
- Sélectionnez Choisir le fichier.
- Sélectionnez votre fichier zip de sauvegarde.
- Sélectionnez Restaurer.

#### Utilisation de la sauvegarde du système de fichiers

- Réinstallez Sonarr (si applicable / non déjà installé).
- Trouvez l'emplacement du répertoire AppData de Sonarr.
  - Exécutez Sonarr une fois et accédez à Système => À propos via l'interface utilisateur.
  - [Répertoire AppData de Sonarr](/sonarr/appdata-directory)
- Arrêtez Sonarr.
- Supprimez le contenu du répertoire AppData **(y compris les fichiers .db-wal/.db-journal s'ils existent)**.
- Restaurez à partir de votre sauvegarde.
- Démarrez Sonarr.
- Tant que les chemins sont les mêmes, tout reprendra là où cela s'était arrêté.

#### Restauration du système de fichiers sur un NAS Synology

> ATTENTION : La restauration sur un Synology nécessite des connaissances en Linux et un accès SSH root à l'appareil Synology.
{.is-warning}

- Réinstallez Sonarr (si applicable / non déjà installé).
- Trouvez l'emplacement du répertoire AppData de Sonarr.
  - Exécutez Sonarr une fois et accédez à Système => À propos via l'interface utilisateur.
  - [Répertoire AppData de Sonarr](/sonarr/appdata-directory)
- Arrêtez Sonarr.
- Connectez-vous au NAS Synology via SSH et connectez-vous en tant que root.

> Sur certaines installations, l'utilisateur est différent des commandes ci-dessous : `chown -R sc-Sonarr:Sonarr *` {.is-info}

- Exécutez les commandes suivantes :

```shell
rm -r /usr/local/Sonarr/var/.config/Sonarr/Sonarr.db
cp -f /tmp/Sonarr_backup/* /usr/local/Sonarr/var/.config/Sonarr/
```

- Mettez à jour les autorisations sur les fichiers :

 ```shell
cd /usr/local/Sonarr/var/.config/Sonarr/
chown -R Sonarr:users *
chmod -R 0644 *
```

- Démarrez Sonarr.

## J'ai perdu mon mot de passe, comment puis-je retrouver l'accès ?

{#help-i-have-forgotten-my-password}

> Si vous utilisez la version 4 de Sonarr, le type `None` de `AuthenticationMethod` n'est plus valide - veuillez consulter cette [FAQ](/sonarr/faq-v4) {.is-info}

Pour désactiver l'authentification (pour réinitialiser votre nom d'utilisateur ou votre mot de passe oublié), vous devrez modifier le fichier `config.xml` qui se trouve dans le [répertoire AppData de Sonarr](/sonarr/appdata-directory).

1. Ouvrez config.xml dans un éditeur de texte.
1. Recherchez la ligne de méthode d'authentification qui sera
   `<AuthenticationMethod>Basic</AuthenticationMethod>` ou `<AuthenticationMethod>Forms</AuthenticationMethod>`.
1. Modifiez la ligne `AuthenticationMethod` en `<AuthenticationMethod>None</AuthenticationMethod>`.
1. Redémarrez Sonarr.
1. Sonarr sera maintenant accessible sans mot de passe. Vous devriez aller dans les `Paramètres : Général` dans l'interface utilisateur et définir votre nom d'utilisateur et votre mot de passe.

## Pourquoi y a-t-il deux fichiers ? \| Pourquoi y a-t-il un fichier restant dans les téléchargements ?

C'est normal. Avec une configuration prenant en charge les [liens physiques](https://trash-guides.info/hardlinks), l'espace double ne sera pas utilisé. Voici comment fonctionne le processus de torrent :

1. Sonarr envoie une demande de téléchargement à votre client et l'associe à un label ou à une catégorie que vous avez configuré dans les paramètres du client de téléchargement. Exemples : films, émissions de télévision, séries, musique, etc.
1. Sonarr surveille les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
1. Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de partager le fichier (le ratio ou le temps peut être ajusté dans le client de téléchargement ou depuis l'interface spécifique du client de téléchargement). Lorsque les fichiers sont importés dans votre dossier multimédia, le fichier est lié physiquement s'il est pris en charge par votre configuration ou copié s'il n'est pas pris en charge par les liens physiques.
1. Si l'option "Gestion des téléchargements terminés - Supprimer les téléchargements terminés" est activée dans les paramètres de Sonarr, Sonarr supprimera le fichier et le torrent d'origine de votre client de téléchargement, mais seulement si le client de téléchargement signale que le partage est terminé et que le torrent est arrêté (c'est-à-dire en pause). Consultez les [Guides des clients de téléchargement de TRaSH](https://trash-guides.info/Downloaders/) pour savoir comment configurer votre client de téléchargement de manière optimale.

> Les liens physiques sont activés par défaut. [Un lien physique n'utilisera pas d'espace disque supplémentaire](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/). Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création de liens physiques échoue ou si votre configuration ne prend pas en charge les liens physiques, le fichier sera copié en dernier recours.{.is-info}

## Je vois que la fonctionnalité/le bogue X a été corrigé(e), pourquoi ne puis-je pas le voir ?

Sonarr est composé de deux branches principales de code, `main` et `develop`.

- `main` est publié périodiquement, lorsque la branche `develop` est stable.
- `develop` est destiné aux tests de pré-version et aux personnes prêtes à prendre des risques. Lorsqu'une fonctionnalité est marquée comme étant dans `develop`, elle ne sera disponible que pour les utilisateurs exécutant la branche `develop`, une fois qu'elle aura été déplacée en direct (dans `main`), elle sera officiellement publiée.

## Progression de l'épisode - Comment est-elle calculée ?

- Il y a deux parties dans le décompte des épisodes, l'une étant le nombre d'épisodes (Episode Count) et l'autre étant le nombre d'épisodes avec des fichiers (Episode File Count), chacune utilisant une logique légèrement différente pour vous donner la progression globale d'une série ou d'une saison.

  - Episode Count => L'épisode a déjà été diffusé ET est surveillé OU - L'épisode a un fichier
  - Episode File Count => L'épisode a un fichier

- Si une série a 10 épisodes qui ont tous été diffusés et que vous n'avez aucun fichier pour eux, vous aurez 0/10 épisodes. Si vous désactivez la surveillance de tous les épisodes de cette série, vous aurez 0/0, et si vous obtenez tous les épisodes de cette série, qu'ils soient surveillés ou non, vous aurez 10/10 épisodes.

## Comment accéder à Sonarr depuis un autre ordinateur ?

- Par défaut, Sonarr n'écoute pas les demandes provenant de tous les systèmes (lorsqu'il n'est pas exécuté en tant qu'administrateur), il n'écoute que sur localhost, cela est dû à la façon dont le serveur Web utilisé par Sonarr s'intègre à Windows (cela s'applique également aux alternatives actuelles). Si Sonarr est exécuté en tant qu'administrateur, il s'enregistrera correctement auprès de Windows et ouvrira le port du pare-feu afin qu'il puisse être accessible depuis d'autres systèmes de votre réseau. L'exécution en tant qu'administrateur ne doit se faire qu'une seule fois (si vous modifiez le port, vous devrez le réexécuter).

## Pourquoi Sonarr actualise-t-il si fréquemment les informations sur les séries ?

- Sonarr actualise les informations sur les séries et les épisodes en plus de rescanner le disque à la recherche de fichiers toutes les 12 heures. Cela peut sembler agressif, mais c'est un processus très important. La mise à jour des données depuis notre proxy TVDb est importante, car de nouvelles informations sur les épisodes sont synchronisées, les dates de diffusion, le nombre d'épisodes, le statut (en cours/terminé). Même les émissions qui ne sont pas diffusées sont mises à jour avec de nouvelles informations.
- La numérisation du disque est moins importante, mais elle est utilisée pour vérifier les nouveaux fichiers qui n'ont pas été triés par Sonarr et détecter les fichiers supprimés.
- La partie la plus chronophage est la mise à jour des informations (en supposant une vitesse d'accès au disque raisonnable), les séries plus volumineuses prennent plus de temps en raison du nombre d'épisodes à traiter.

> Il n'est pas possible de désactiver cette tâche. Si cette tâche s'exécute suffisamment longtemps pour que vous pensiez que c'est le problème, autre chose se passe et doit être résolu au lieu d'arrêter cette tâche.
{.is-warning}

## Pourquoi y a-t-il un nombre à côté de l'activité ?

- Ce nombre indique le nombre d'épisodes dans la file d'attente de votre client de téléchargement et les 60 derniers éléments de son historique qui n'ont pas encore été importés. Si le nombre est bleu, tout fonctionne normalement et les épisodes seront importés lorsqu'ils seront terminés. Le jaune signifie qu'il y a un avertissement sur l'un des épisodes. Le rouge signifie qu'il y a eu une erreur. En cas de jaune (avertissement) et de rouge (erreur), vous devrez consulter la file d'attente sous Activité pour voir quel est le problème (passez la souris sur l'icône pour obtenir plus de détails).
- Vous devez supprimer l'élément de la file d'attente ou de l'historique de votre client de téléchargement pour les supprimer de la file d'attente de Sonarr.

## Quels sont les différents types de séries ?

- Le type de série a un impact sur la façon dont Sonarr recherche les séries. Un type de série est basé sur la façon dont la série est publiée sur les indexeurs et ne correspond pas nécessairement au véritable "type" de la série.
- La plupart des émissions devraient être de type `Standard`. Pour les émissions quotidiennes qui sont généralement diffusées avec une date, `Daily` doit être utilisé. Enfin, il y a les animes où l'utilisation de `Anime` est *généralement* correcte, mais parfois `Standard` peut fonctionner mieux, donc essayez l'autre si vous rencontrez des problèmes.
- Veuillez noter que si le type de série est défini sur anime et si aucun de vos indexeurs activés n'a de catégories d'anime configurées, cela contourne effectivement l'indexeur et il peut sembler qu'il ne recherche pas.
- Veuillez noter que le type Anime n'a aucune notion de packs de saisons ou de saisons et fera en sorte que chaque épisode soit recherché individuellement.
- Veuillez noter que tous les indexeurs ne prennent pas en charge les recherches par saison/épisode (standard).
- Les types de séries peuvent être modifiés depuis l'Éditeur de masse ou depuis `Modifier` lors de la visualisation d'une série. Notez que le type de série est sélectionnable lors de l'importation.

- Si le type de série **Anime** est utilisé, il est [possible de rechercher également sur votre indexeur avec le type standard](/sonarr/settings#indexers)

### Types de séries

- **Anime** - Épisodes publiés en utilisant un numéro d'épisode absolu
- **Daily** - Épisodes publiés quotidiennement ou moins fréquemment qui utilisent l'année-mois-jour (2017-05-25)
- **Standard** - Épisodes publiés avec le modèle SxxEyy

### Exemples de types de séries

Voici quelques exemples de noms de sortie pour chaque type de série. La partie spécifique de différenciation est mise en gras.

> Si le type de série **Anime** est utilisé, il est [possible de rechercher également sur votre indexeur avec le type standard](/sonarr/settings#indexers)
{.is-info}

#### Daily

Les journaux afficheront `Recherche d'indexeurs pour [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Les journaux afficheront `Recherche d'indexeurs pour [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Les journaux afficheront `Recherche d'indexeurs pour [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

## Comment puis-je renommer mes dossiers de séries ?

{#rename-folders}

> Le même processus s'applique également pour déplacer/changer les chemins des séries{.is-info}

Si vous avez ajusté le format du nom de vos séries après que Sonarr ait déjà créé certains dossiers de séries, Sonarr ne renommera pas automatiquement les dossiers existants. Pour déclencher le renommage de ces dossiers, suivez les étapes suivantes :

1. Séries
1. Éditeur de masse
1. Sélectionnez les séries dont le dossier doit être renommé
1. Modifiez le dossier racine pour qu'il soit identique au dossier racine dans lequel les séries existent actuellement
1. Sélectionnez "Oui, déplacer les fichiers" pour que

> Si vous utilisez Plex ou Emby, cela déclenchera la redétection des intros, des vignettes, des chapitres et des métadonnées de prévisualisation.
{.is-warning}

## Comment mettre à jour Sonarr ?

- Accédez aux Paramètres, puis à l'onglet Général et affichez les paramètres avancés (utilisez le bouton bascule près du bouton Enregistrer).

1. Dans la section Mises à jour, changez le nom de la branche en `main` ou `develop`.
1. Enregistrez.

*Cela n'installera pas immédiatement les éléments de cette branche, cela se fera lors de la prochaine mise à jour.*

- main - ![Version actuelle principale/stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Par défaut/Stable) : Cela a été testé par des utilisateurs sur la branche nightly (`develop`) et il n'est pas connu pour avoir de problèmes majeurs. Cette branche devrait être utilisée par la majorité des utilisateurs. Sur GitHub, il s'agit de la branche `main`.
- develop - ![Version actuelle develop/nightly](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alpha/Instable) : C'est maintenant la même chose que main pour les utilisateurs non-Docker et probablement la dernière version v3.

> ~~**Attention : Vous ne pourrez peut-être pas revenir à `main` après avoir basculé vers cette branche.** Sur GitHub, il s'agit de la branche `develop`.~~
{.is-danger}

- v4 develop - ![Version bêta actuelle v4](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alpha/Instable) : **Pour les utilisateurs non-Docker, la branche est `develop` une fois v4 installé. Pour les utilisateurs Docker, il s'agit probablement de l'étiquette `develop`** Il s'agit de la pointe de l'épée pour la version bêta de Sonarr v4. Elle est publiée dès que le code est validé et passe tous les tests automatisés. Cette version n'a peut-être pas encore été utilisée par nous ou d'autres utilisateurs. Il n'y a aucune garantie qu'elle fonctionnera même dans certains cas. Cette branche est uniquement recommandée pour les utilisateurs avancés. Des problèmes et des investigations personnelles sont attendus dans cette branche. Sur GitHub, il s'agit de la branche `develop`.

> **Attention : Vous ne pouvez pas revenir à (v3) `main` ou (v3) `develop` après avoir basculé vers la branche v4 sans réinstaller et localiser une sauvegarde v3.** Sur GitHub, il s'agit de la branche `develop`.
{.is-danger}

> Les installations v3 **non-Docker** ne peuvent pas être mises à niveau directement vers v4 et nécessitent l'installation de Sonarr v4.
{.is-info}

- Remarque : Si votre installation se fait via Docker, ajoutez `:release`, `:latest`, `:nightly` ou `:develop` à la fin de votre balise de conteneur en fonction de qui crée vos versions.

|                                                                    | `main` (stable) ![Current Main/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v3) (beta) ![Current v3 Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v4) (v4 beta) ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) |
|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [hotio](https://hotio.dev/containers/sonarr)                       | `release`                                                                                                                                                                                             | `nightly`                                                                                                                                                                                                   | `v4`                                                                                                                                                                                                            |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-sonarr) | `latest`                                                                                                                                                                                              | `3.0.10`                                                                                                                                                                                                     | `develop`                                                                                                                                                                                                       |

### Installation d'une version plus récente

#### Native

1. Accédez à Système, puis à l'onglet Mises à jour.
1. Les versions plus récentes qui ne sont pas encore installées auront un bouton de mise à jour à côté d'elles. En cliquant sur ce bouton, vous installerez la mise à jour.

> La version 3 ne peut pas être mise à jour vers la version bêta 4 et nécessite une installation manuelle. Reportez-vous à l'[annonce de la version bêta 4](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)
{.is-info}

#### Docker

1. Re-téléchargez votre balise et mettez à jour votre conteneur.

## Puis-je passer de `develop` à `main` ?

- Voir l'entrée ci-dessous

## Puis-je passer d'une branche à une autre ?

> Vous pouvez (presque) toujours augmenter votre risque.{.is-info}

- `main` peut passer à `develop`
- Voir ci-dessous ou vérifiez avec l'équipe de développement pour voir si vous pouvez passer de `develop` à `main` pour votre version donnée.
- Ne pas suivre ces instructions peut rendre votre Sonarr inutilisable ou provoquer des erreurs. Vous avez été prévenu. Si les erreurs suivantes se produisent, cela signifie que vous utilisez une base de données plus récente avec une ancienne version de \*Arr, ce qui n'est pas pris en charge. Mettez à niveau \*Arr vers la version précédente ou plus récente sur laquelle vous étiez.
  - Exemples de messages d'erreur :
    - `Erreur d'analyse de la colonne 45 (Language=31 - Int64)`
    - `Le DataMapper n'a pas pu charger le champ suivant : 'Languages' value`
    - `ID ne correspond pas à une langue connue Nom du paramètre : id`
    - Autres erreurs de base de données similaires concernant des colonnes ou des tables manquantes.
- **Mise à jour du 7 août 2022**
  - `3.0.9.1549` a été publié en tant que version principale/stable
  - Pour ceux qui utilisent develop et qui sont toujours sur `3.0.9.1549` ou une version inférieure, vous pouvez revenir en toute sécurité à main
  - Si vous utilisez une version plus récente, vous *pourriez être bloqué* sur nightly/develop jusqu'à ce qu'une nouvelle version stable soit publiée. Si vous disposez d'une sauvegarde antérieure à la mise à niveau de la version mentionnée ci-dessus, vous pouvez la réinstaller et restaurer la sauvegarde. Vérifiez avec l'équipe de développement pour voir si vous pouvez revenir en toute sécurité à une version antérieure.

# Problèmes de Sonarr et de séries + métadonnées

## Comment Sonarr gère-t-il les problèmes de numérotation des épisodes (American Dad!, etc) ?

### Comment Sonarr gère les problèmes de numérotation des épisodes

- Sonarr s'appuie sur [TheXEM](http://thexem.info/), un site communautaire qui permet aux utilisateurs de créer des correspondances entre les émissions de la scène (les personnes qui publient les fichiers) et TheTVDb (qui suit généralement la numérotation du réseau). Il existe déjà un certain nombre d'émissions sur ce site, mais il est facile d'en ajouter une autre et généralement les modifications sont acceptées dans les deux jours (si elles sont correctes). TheXEM est utilisé pour corriger les différences de numérotation des épisodes (différence d'opinion sur le fait qu'un épisode est spécial ou non) ainsi que les différences de numérotation des saisons, comme des épisodes publiés en tant que S10E01, mais TheTVDb répertorie le même épisode en tant que S2017E01.
- XEM corrige généralement les problèmes lorsque la numérotation des groupes de sortie (communément appelés "la scène") ne correspond pas à la numérotation de TVDb, de sorte que Sonarr ne fonctionne pas. Eh bien, entrez [XEM](http://thexem.info), qui crée une carte que Sonarr peut consulter.
- Les groupes de sortie diffusent des épisodes doubles dans un seul fichier, car c'est ainsi qu'ils sont diffusés, mais TVDb marque chaque épisode individuellement.
- Les groupes de sortie utilisent une année pour la saison S2010 et TVDb utilise S01.
- [XEM](http://thexem.info) fonctionne dans la plupart des cas et permet de maintenir un fonctionnement fluide sans que vous ne le sachiez jamais. Cependant, comme pour la plupart des choses, il y aura toujours des *exceptions problématiques* et dans ce cas, il y en a une liste.

> Certains indexeurs ou groupes de sortie peuvent suivre TVDb plutôt que `Scene` (c'est-à-dire XEM).
> Si cela est observé, veuillez les soumettre via le formulaire de correspondance de la scène.
{.is-info}

- [Correspondances demandées pour les services *Vérifiez et assurez-vous que l'alias et la version n'ont pas déjà été demandés ou ajoutés*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Formulaire de demande de correspondance de la scène des services *Faites une nouvelle demande pour un alias. Assurez-vous de remplir le formulaire en entier*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

### Émissions problématiques

> Ceci n'est en aucun cas une liste exhaustive des émissions ayant des problèmes connus avec la correspondance de la scène ; cependant, ce sont quelques-unes des plus courantes.
{.is-info}

- Il s'agit d'une liste incomplète des émissions connues et de la manière dont/pourquoi elles posent problème :
- American Dad {#problemshow-americandad}
  - En raison des changements de saison du réseau, American Dad a généralement un décalage d'une saison entre les sorties et TVDb. Reportez-vous à la carte XEM pour plus de détails.
  - [American Dad](https://thexem.info/xem/show/4948) est actuellement en S19 selon TVDb ou en S18 selon la scène au moment de la rédaction de cet article. Ainsi, si vous recherchez la saison 19 dans Sonarr, vous n'obtiendrez **que** les résultats de la saison 18 en raison de la carte XEM.
  - Si vous disposez d'un indexeur/groupes de sortie avec des épisodes de la saison 19, veuillez les soumettre via le formulaire de correspondance de la scène et assurez-vous qu'ils ne sont pas déjà demandés
    - [Correspondances demandées pour les services *Vérifiez et assurez-vous que l'alias et la version n'ont pas déjà été demandés ou ajoutés*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Formulaire de demande de correspondance de la scène des services *Faites une nouvelle demande pour un alias. Assurez-vous de remplir le formulaire en entier*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- Paw Patrol {#problemshow-pawpatrol}
  - Fichiers d'épisodes doubles par rapport à des épisodes simples sur TVDb, mais tous les épisodes ne sont pas doubles, de sorte que la carte peut être ajoutée de manière incorrecte en indiquant lesquels sont simples et lesquels sont doubles.
- Pokémon {#problemshow-pokemon}
  - Sur TheXem, [Pokemon](http://thexem.info/xem/show/4638) suit les épisodes *doublés*. Donc, si vous voulez des épisodes sous-titrés, vous pourriez être malchanceux. Si certains groupes de sortie suivent TVDb et non la correspondance XEM, veuillez les soumettre via le formulaire de correspondance de la scène et assurez-vous qu'ils ne sont pas déjà demandés
    - [Correspondances demandées pour les services *Vérifiez et assurez-vous que l'alias et la version n'ont pas déjà été demandés ou ajoutés*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Formulaire de demande de correspondance de la scène des services *Faites une nouvelle demande pour un alias. Assurez-vous de remplir le formulaire en entier*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- La Casa de Papel / Money Heist  {#problemshow-moneyheist}
  - TVDb a l'ordre de diffusion original du réseau espagnol, mais Netflix a acheté les droits et a recoupé la série en un nombre d'épisodes différent. Cela fait que "saison 5" est importée par-dessus les épisodes "saison 3" existants. [Des informations supplémentaires peuvent être trouvées dans ce fil Reddit](https://old.reddit.com/r/sonarr/comments/pdrr6l/money_heist_mess/)
- Kamen Rider {#problemshow-kamenrider}
  - L'entrée de l'anthologie ([ID TVDb 74096](https://thetvdb.com/series/kamen-rider)) doit être utilisée dans Sonarr pour l'automatisation, car cette émission a à la fois une entrée d'anthologie (regroupant toutes les saisons) et les saisons individuelles répertoriées comme des entrées distinctes sur TVDb. En raison des correspondances de noms de saison individuelles de l'entrée d'anthologie sur [TheXEM](https://thexem.info/xem/show/5376), il n'est pas possible d'ajouter les entrées de saison individuelles à Sonarr sans télécharger et importer manuellement les sorties.
- Bleach: Thousand-Year Blood War {#problemshow-bleach}
  - La nouvelle saison de Bleach: Thousand-Year Blood War est diffusée avec une variété de schémas de dénomination différents, ce qui rend difficile l'automatisation et peut écraser certains de vos épisodes existants. Elle ne peut être automatisée que si votre groupe de sortie :
    - Publie les épisodes avec la numérotation S17Exx, ou
    - Les publie avec le titre correct de la saison 2 (trouvé ici <https://thexem.info/xem/show/5476>) et a commencé cette nouvelle arc au numéro d'épisode absolu 1.
- Great Asian Railway Journeys {#problemshow-greatasianrail}
  - Great Asian Railway Journeys a d'abord été diffusé en 20 épisodes plus courts, puis a été rediffusé en 10 épisodes plus longs. Ces épisodes combinés plus longs ont été ajoutés en tant qu'épisodes spéciaux et doivent être nommés en conséquence (S00E01, etc.).
- Horizon {#problemshow-horizon}
  - Une émission qui diffuse sporadiquement des épisodes depuis 1964. Cela rend la correspondance particulièrement difficile, comme vous pouvez le voir sur [TheXEM](https://thexem.info/xem/show/5495). Ceux qui sont intéressés peuvent trouver la discussion originale sur le discord de Sonarr [ici](https://discord.com/channels/383686866005917708/649018968559845376/1046898050909622312).
- Kaleidoscope (2023) {#problemshow-kaleidoscope}
  - Kaleidoscope (2023) a été diffusé sur Netflix sous la forme d'une émission non linéaire, ce qui signifie que chaque utilisateur obtenait un ordre différent en regardant la série. Cela pose un problème pour Sonarr car les groupes de sortie ont différents ordres d'épisodes pour l'émission. Afin d'éviter une correspondance incorrecte des épisodes, Sonarr ne téléchargera pas automatiquement les épisodes et vous devrez les télécharger et les importer manuellement. Vous pouvez les faire correspondre en fonction du titre de l'épisode ou en prévisualisant les premières secondes et en vérifiant que la "couleur" de l'épisode correspond au titre.

Quelques exemples d'autres émissions qui ont souvent des problèmes, dont la plupart peuvent être résolus grâce aux correspondances TheXEM, sont : Arrested Development, Kitchen Nightmares (US), Mythbusters, Pawn Stars.

## Pourquoi Sonarr ne peut-il pas importer les fichiers d'épisodes de la série X ? / Pourquoi Sonarr ne peut-il pas trouver de versions pour la série X ?

Il peut y avoir plusieurs raisons pour lesquelles Sonarr ne parvient pas à trouver ou à importer des épisodes pour une série particulière.

> Sonarr n'utilise pas les alias ni les traductions (c'est-à-dire les titres étrangers) de TVDb.
{.is-warning}

> **Pour les indexeurs qui prennent en charge les recherches basées sur l'ID**, l'ID TVDb ou l'ID IMDb de la série est utilisé pour la recherche. Les titres de la série et les alias ne sont utilisés que si les recherches basées sur l'ID ne donnent aucun résultat.
{.is-info}

- Sonarr compte sur la correspondance des titres, souvent les uploaders nomment les épisodes avec des titres différents, par exemple `CSI: Crime Scene Investigation` est publié simplement `CSI`, donc Sonarr ne peut pas faire correspondre les noms sans un peu d'aide. Ces cas sont gérés par la correspondance de scène que l'équipe Sonarr maintient.
- Vous pouvez également consulter la [FAQ sur les problèmes d'émissions problématiques et les problèmes de numérotation des groupes de diffusion par rapport à TVDb](#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc).

> **Pour tous les animes japonais, des alias doivent être ajoutés à [thexem.info](https://thexem.info)**, pour demander une nouvelle correspondance pour d'autres séries, suivez les étapes ci-dessous. Vous trouverez plus d'informations auprès de certains membres de XEM qui se trouvent dans le canal #XEM sur le serveur Discord de Sonarr.
{.is-danger}

- [Demandes de correspondance de services *Vérifiez et assurez-vous que l'alias et la version n'ont pas déjà été demandés ou ajoutés*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Formulaire de demande de correspondance de services *Faites une nouvelle demande pour un alias. Assurez-vous de remplir le formulaire en entier*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

> Les demandes de services sont généralement ajoutées dans un délai de 1 à 5 jours
{.is-info}

> Encore une fois, ne demandez pas de correspondance pour les animes japonais ; utilisez XEM pour cela.
> Vous trouverez plus d'informations auprès de certains membres de XEM qui se trouvent dans le canal [\#XEM sur le serveur Discord de Sonarr](https://discord.gg/Z3D6u5hBJb)
{.is-danger}

> Si une série non japonaise nécessite une correspondance de saison (par exemple, si elle est publiée en tant que S25E26 mais que TVDB est S26E2), une correspondance XEM sera nécessaire. Cela ne peut pas être fait avec une correspondance de services.
{.is-info}

> La série "Helt Perfekt" avec les identifiants TVDb `343189` et `252077` est difficile à automatiser car TVDb a le même nom pour les deux émissions, ce qui viole les propres règles de TVDb. La première entrée pour la série obtient le nom. Toutes les entrées futures pour la série doivent avoir l'année comme partie du nom de la série. Cependant, une exception de scène a été ajoutée pour mapper les versions (correspondance sensible à la casse) Helt Perfekt contenant `NORWEGIAN` -\> `252077` et contenant `SWEDISH` -\> `343189`
{.is-info}

## TVDb est mis à jour, pourquoi Sonarr ne l'est-il pas ?

{#tvdb}

- TVDb a un cache de 24 heures sur son API.
- L'API de TVDb doit ensuite se propager à travers son cache CDN, ce qui prend plusieurs heures.
- Skyhook de Sonarr a un cache beaucoup plus petit de quelques heures en plus de cela.
- De plus, Sonarr ne lance la tâche de rafraîchissement des séries que toutes les 12 heures. Cette tâche peut être exécutée manuellement depuis Système => Tâches ; "Tout mettre à jour" depuis l'Index des séries, ou exécutée manuellement pour une série spécifique sur la page de cette série.

- Par conséquent, pour qu'un changement sur TVDb soit automatiquement pris en compte par Sonarr, il faut généralement entre 36 et 48 heures (24 + ~3 + ~3 + 12)

- Si une série ou des épisodes manquent sur TVDb, ils prendront entre 36 et 48 heures à partir de leur ajout pour apparaître dans votre instance Sonarr.

{#missing-episodes}

- Si vous savez qu'une mise à jour de TVDb a été effectuée il y a plus de 48 heures, veuillez en discuter sur notre [Discord](https://discord.sonarr.tv/).

## Pourquoi ne puis-je pas ajouter une série ?

{#why-can-i-not-add-a-new-series}

- Si TheTVDb est indisponible, Sonarr ne peut pas obtenir de résultats de recherche et vous ne pourrez pas ajouter de nouvelles séries par recherche. Vous pourrez peut-être ajouter une nouvelle série en utilisant l'ID TVDb si vous le connaissez, l'interface utilisateur explique comment l'ajouter par un ID.
- Sonarr ne peut pas ajouter de série qui n'a pas de titre en anglais. Si vous essayez d'ajouter une série via l'ID TVDb qui n'a pas de titre en anglais. Si aucun titre en anglais n'existe pour cette série sur TheTVDb, il faudra l'ajouter, puis [attendre que le cache de TVDb se vide](#tvdb).
- L'émission doit être une série télévisée, et non un film. Elle doit également exister sur TVDb. Si elle est sur IMDB, TMDB ou ailleurs, mais pas sur TVDb, vous ne pouvez pas ajouter l'émission.
- La série doit exister sur TVDb.
- Certaines séries peuvent en réalité être considérées comme des continuations et des saisons de leur série principale.
  - Certaines séries/saisons connues sont :
  - [Dexter New Blood était la saison 9](https://thetvdb.com/series/dexter/seasons/official/9) mais c'est maintenant [sa propre série](https://thetvdb.com/series/dexter-new-blood)

## Pourquoi ne puis-je pas ajouter une série lorsque je connais l'ID TVDb ?

{#why-cant-i-add-a-new-series-when-i-know-the-tvdb-id}

- Sonarr ne peut pas ajouter de série qui n'a pas de titre en anglais. Si vous essayez d'ajouter une série via l'ID TVDb qui n'a pas de titre en anglais, la série ne sera pas trouvée. Si aucun titre en anglais n'existe pour cette série sur TheTVDb, il faudra l'ajouter (si disponible).
- Vérifiez l'URL / la série - Sonarr ne prend pas en charge les films ; utilisez [Radarr](/radarr) pour les films.

## Titre Slug déjà utilisé

- Il y a deux causes principales de cette erreur, qui sont énumérées ci-dessous.

## Noms en double sans année

- Cette erreur se produit souvent lorsque deux séries portent le même titre sur TheTVDB, dans ce cas, la deuxième série doit avoir l'année ajoutée au titre de la série.
  - Série A
  - Série A (2021)
- Pour remédier à cela, attendez que quelqu'un mette éventuellement à jour TVDb ou mette à jour TVDb vous-même. Une fois corrigé **et une fois approuvé par les modérateurs de TVDb**, en raison des [problèmes d'API de TVDb](#tvdb-is-updated-why-isnt-sonarr), une fois mis à jour, vous devrez attendre plus de 30 heures avant que le titre corrigé puisse être utilisé dans Sonarr.

## Noms en double avec ponctuation

- Cela se produira également avec deux séries de noms similaires qui ne diffèrent peut-être que par la ponctuation, dans ce cas, veuillez signaler cela sur le [Discord de Sonarr](https://discord.sonarr.tv/).
  - L'émission de Joe (2022)
  - L'émission de Joes (2022)

## L'épisode n'a pas de numéro absolu

- Les épisode(s) sur TVDb n'ont pas de numéro absolu attribué. Mettez à jour la série sur TVDb si nécessaire, puis attendez 36 à 48 heures pour que la mise à jour se propage dans le cache interne de TVDb et se charge dans Sonarr.

## Horaires de diffusion des épisodes

- Dans Sonarr, les dates et heures de diffusion des épisodes affichées dans le navigateur sont basées sur l'heure/le fuseau horaire du client, toutes les heures sont envoyées de Sonarr au navigateur sous forme d'heures UTC (formatées selon la norme ISO-8601)
- TVDb indique - avec des exceptions pour les services de streaming - que l'heure et la date de diffusion sont basées sur l'heure locale du réseau de diffusion principal dans la ville la plus populaire du pays. [Consultez l'entrée FAQ de TVDb pour plus de détails](https://support.thetvdb.com/kb/faq.php?id=29)
- Les dates et heures de diffusion des épisodes sur TVDb sont converties en UTC et utilisent le fuseau horaire de Sonarr qui est mappé dans Skyhook par l'équipe Sonarr pour le réseau que TVDb a pour la série.
  - Dans le cas rare où un réseau n'est pas mappé, l'heure dans TVDb sera supposée être US EST (UTC-5).
  - Si l'heure de diffusion ne semble pas correspondre lors de la conversion de l'heure de diffusion du fuseau horaire local du réseau vers le fuseau horaire de votre navigateur, il est probable que le réseau doit être mappé dans Skyhook. [Contactez l'équipe de développement sur Discord](https://discord.sonarr.tv/) pour obtenir de l'aide pour mettre à jour le fuseau horaire du réseau.

# Problèmes courants de Sonarr

## Le chemin est déjà configuré pour une série existante

- L'importation de la bibliothèque affiche "Existante" ou vous obtenez une erreur "Le chemin est configuré pour une série existante"
- Cela se produit lorsque vous essayez d'ajouter une série ou de modifier le chemin d'une série existante qui est déjà attribué à une autre série.
- Cela est probablement dû au fait de ne pas avoir corrigé une série non correspondante lorsque l'utilisateur a importé sa bibliothèque.
- Localisez et corrigez le film qui est déjà attribué au chemin de cette série.
  - Index des séries
  - Vue en tableau
  - Options => Ajouter le chemin en tant que colonne
  - Triez et trouvez le film au chemin problématique noté.
- Alternativement, supprimez la série utilisant le chemin existant de Sonarr

## Le système et les journaux se chargent indéfiniment

- C'est à cause de la liste de blocage easy-privacy. Ils bloquent essentiellement toutes les URL contenant "/api/log?" dedans. Examinez la liste et dites-moi si vous pensez que bloquer toutes les URL de cette liste est une idée sensée, il y a des dizaines d'URL qui peuvent potentiellement casser des sites. Vous l'avez sélectionné dans votre bloqueur de publicités. La solution simple est d'ajouter le domaine sur lequel Sonarr s'exécute à la liste blanche. Mais je recommande quand même de vérifier la liste.

## Problèmes d'interface utilisateur étranges

- Si vous rencontrez des problèmes d'interface utilisateur étranges, comme la page de la bibliothèque qui ne liste rien ou une certaine vue ou un certain tri qui ne fonctionne pas, essayez de voir dans une fenêtre de navigation privée Chrome ou une fenêtre privée Firefox. Si cela fonctionne correctement là-bas, videz le cache et les cookies de votre navigateur pour votre adresse IP/domaine spécifique. Pour plus d'informations, consultez l'article du wiki sur [la suppression du cache, des cookies et du stockage local](/useful-tools#clearing-cookies-and-local-storage).

## L'interface Web ne se charge qu'en local sur Windows

- Si vous ne pouvez accéder à votre interface Web qu'à l'adresse <http://localhost:8989/> ou <http://127.0.0.1:8989>, vous devez exécuter Sonarr en tant qu'administrateur au moins une fois.

## J'ai eu une fenêtre contextuelle indiquant que config.xml était corrompu, que faire maintenant ?

- Sonarr n'a pas pu lire votre fichier de configuration au démarrage car il est devenu corrompu d'une manière ou d'une autre. Pour remettre Sonarr en ligne, vous devrez supprimer le fichier `.xml` dans votre [dossier AppData](/sonarr/appdata-directory), une fois supprimé, lancez Sonarr et il démarrera sur le port par défaut (8989), vous devrez maintenant reconfigurer les paramètres que vous avez configurés sur la page des paramètres généraux.

## Certificat invalide et autres problèmes HTTPS ou SSL

- Si vous n'êtes pas sous Windows, il est très probable que les certificats de votre mono soient obsolètes et doivent être synchronisés. [Consultez la section sur le SSL mono dans l'article d'installation pour plus de détails](/sonarr/installation#mono-ssl-issues)
- Votre client de téléchargement a cessé de fonctionner et vous obtenez une erreur du type `Localhost is an invalid certificate` ?
  - Sonarr valide désormais les certificats SSL. Si aucun certificat SSL n'est défini dans le client de téléchargement, ou si vous utilisez un certificat https auto-signé sans le certificat CA ajouté à votre magasin de certificats local, alors Sonarr refusera de se connecter. Des certificats correctement signés et gratuits sont disponibles sur [let's encrypt](https://letsencrypt.org/).
  - Si votre client de téléchargement et Sonarr sont sur la même machine, il n'y a aucune raison d'utiliser HTTPS, donc la solution la plus simple est de désactiver SSL pour la connexion. La plupart des gens conviennent que ce n'est pas nécessaire sur un réseau local non plus. Il est possible de désactiver la validation des certificats dans les paramètres avancés si vous souhaitez conserver une configuration SSL non sécurisée.

## Comment empêcher le navigateur de se lancer au démarrage ?

Selon votre système d'exploitation, il existe plusieurs façons possibles.

- Dans `Paramètres` => `Général` sur certains systèmes d'exploitation, il y a une case à cocher pour lancer le navigateur au démarrage.
- Lorsque vous invoquez Sonarr, vous pouvez ajouter `-nobrowser` (*nix) ou `/nobrowser` (Windows) aux arguments.
- Arrêtez Sonarr, éditez le fichier config.xml et changez `<LaunchBrowser>True</LaunchBrowser>` en `<LaunchBrowser>False</LaunchBrowser>`.

## VPN, Jackett et les \*ARRs

- À moins que vous ne soyez dans un pays répressif comme la Chine, l'Australie ou l'Afrique du Sud, votre client torrent est généralement le seul élément qui doit être derrière un VPN. Étant donné que le point de terminaison VPN est partagé par de nombreux utilisateurs, vous pouvez rencontrer des limites de débit, une protection contre les DDOS et des interdictions d'IP de divers services utilisés par chaque logiciel.
- En d'autres termes, mettre les \*Arrs (Lidarr, Prowlarr, Radarr, Readarr et Lidarr) derrière un VPN peut rendre les applications inutilisables dans certains cas en raison de l'inaccessibilité des services.

> **Pour être clair, il ne s'agit pas de savoir si les VPN causeront des problèmes avec les \*Arrs, mais quand : les fournisseurs d'images vous bloqueront et Cloudflare est devant la plupart des serveurs \*Arr (mises à jour, métadonnées, etc.) et est susceptible de vous bloquer également**
{.is-warning}

- **De nombreux trackers privés vous banniront si vous les utilisez ou y accédez (c'est-à-dire en utilisant Jackett ou Prowlarr) via un VPN.**

### Utilisation d'un VPN

- Si un VPN est nécessaire et que Docker est utilisé, il est recommandé d'utiliser les conteneurs Hotio ou Binhex's Download Client + VPN.
- Si un VPN est nécessaire et que Docker n'est pas utilisé, votre client VPN ***doit*** prendre en charge le fractionnement du tunnel afin que seules les applications requises (client de téléchargement) soient derrière le VPN.
- De nombreux problèmes d'accès aux trackers peuvent être résolus en utilisant les serveurs DNS de Google ou de Cloudflare à la place des serveurs DNS de votre fournisseur d'accès Internet.
- Dans certains cas (par exemple, les fournisseurs d'accès Internet britanniques), vous devrez mettre votre client de téléchargement de torrents derrière un VPN et Jackett/Prowlarr comme suit :
  - mettez Jackett derrière le VPN et assurez-vous que le fractionnement du tunnel permet l'accès local
  - pour Prowlarr, configurez votre client VPN pour fournir un proxy et ajoutez le proxy dans Paramètres => Indexeurs. Donnez au proxy une étiquette et attribuez la même étiquette aux indexeurs qui doivent l'utiliser.
    - Si cela est absolument nécessaire et si votre VPN ne permet pas de créer un proxy, vous pouvez mettre Prowlarr derrière le VPN et vous assurer que le fractionnement du tunnel permet l'accès local.

## Je vois des messages de journal pour des émissions que je n'ai pas/que je ne veux pas

- Ces messages sont tout à fait normaux et proviennent des flux RSS que Sonarr vérifie pour voir s'il y a des épisodes que vous voulez, généralement ils n'apparaissent que dans les journaux de débogage/traces, mais en cas de problème de traitement d'un élément, vous pouvez voir un avertissement ou une erreur. Il est sûr d'ignorer les avertissements/erreurs car ils concernent des émissions que vous ne voulez pas, dans le cas où il s'agit d'une émission que vous voulez, ouvrez un fil de support sur les forums.

## Les torrents en cours de partage ne sont pas supprimés automatiquement

- Lorsqu'un torrent qui est encore en partage est importé, il est copié ou lié en dur (si activé et *possible*) afin que le client torrent puisse continuer à partager. Dans une configuration idéale, le dossier de téléchargement des torrents et le dossier de la bibliothèque seront sur le même système de fichiers et *auront l'air de l'être* (Docker et les partages réseau facilitent les erreurs à ce sujet), ce qui rend les liens durs possibles et minimise l'espace gaspillé.
- De plus, vous pouvez configurer vos objectifs de temps/de ratio de partage dans Sonarr ou votre client de téléchargement, configurer votre client de téléchargement pour *mettre en pause* ou *arrêter* lorsque ces objectifs sont atteints et activer la suppression dans le gestionnaire de téléchargement terminés et échoués. Ainsi, les torrents qui ont fini de partager seront supprimés du client de téléchargement par Sonarr.

## Aide, mon Mac dit que Sonarr ne peut pas être ouvert car le développeur ne peut pas être vérifié

- C'est simple, veuillez consulter ce lien pour plus d'informations [ici](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
[![Le développeur ne peut pas être vérifié](/assets/general/faq_1_mac.png)]

## Aide, mon Mac dit que Sonarr.app est endommagé et ne peut pas être ouvert

- Cela est dû soit à un téléchargement corrompu, alors essayez à nouveau, soit à des problèmes de sécurité, veuillez consulter cette FAQ connexe [ici](#help-my-mac-says-sonarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## J'obtiens une erreur : Database disk image is malformed

> Vous pouvez recevoir cette erreur après avoir mis à jour sqlite3 vers 3.41. Sonarr v3.0.9 ne prend pas en charge sqlite3 3.41 en raison d'un changement par défaut cassant. [Les détails sur le problème peuvent être trouvés dans Sonarr GHI #5464](https://github.com/Sonarr/Sonarr/issues/5464)
> Cela est résolu avec Sonarr v3.0.10 et les utilisateurs doivent mettre à jour Sonarr en conséquence.
{.is-warning}

- **Les erreurs de `Erreur lors de la création de la base de données de journal` indiquent des problèmes avec logs.db**
  - Cela peut être rapidement résolu en renommant ou en supprimant la base de données. La base de données des journaux contient des informations non importantes concernant l'historique des commandes et l'historique des installations de mises à jour, ainsi que des entrées Info, Warn et Error.
- **Les erreurs de `Erreur lors de la création de la base de données principale` ou `l'image disque de la base de données est corrompue` sans base de données spécifiée indiquent des problèmes avec sonarr.db**
  - Poursuivez avec les étapes indiquées ci-dessous.
- Cela signifie que votre base de données SQLite qui stocke la plupart des informations pour Sonarr est corrompue. Vos options sont d'essayer de sauvegarder, de récupérer la base de données existante, de récupérer les sauvegardes, ou si tout échoue, de recommencer avec une nouvelle base de données.
- Cette erreur peut apparaître si le fichier de base de données n'est pas accessible en écriture par l'utilisateur/groupe sous lequel \*Arr s'exécute. Les autorisations étant la cause, cela ne posera probablement problème que pour les nouvelles installations, les installations migrées vers un nouveau serveur, si vous avez récemment modifié les autorisations de votre répertoire appdata, ou si vous avez modifié l'utilisateur et le groupe sous lesquels \*Arr s'exécute.
- Votre meilleure et première option est d'essayer de [restaurer à partir d'une sauvegarde](#how-do-i-backuprestore-my-sonarr)
- Vous pouvez également essayer de récupérer votre base de données. C'est généralement la seule option lorsque ce problème survient après une mise à jour. Essayez la commande [sqlite3 `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Si votre sqlite ne dispose pas de `.recover` ou si vous souhaitez une méthode plus conviviale pour l'interface graphique (par exemple, Windows), suivez [nos instructions sur ce wiki](/useful-tools#recovering-a-corrupt-db-ui).
- Une autre cause possible de l'erreur de votre base de données est que vous placez votre base de données sur un lecteur réseau (nfs ou smb ou autre chose non local). **SQLite est conçu pour des situations où les données et l'application coexistent sur la même machine.** Ainsi, votre dossier \*Arr AppData (/montage de configuration pour Docker) DOIT être stocké localement. [SQLite et les lecteurs réseau ne fonctionnent pas bien ensemble et finiront par provoquer une base de données corrompue](https://www.sqlite.org/draft/useovernet.html).
- Si vous utilisez mergerFS, vous devez supprimer `direct_io` car SQLite utilise mmap qui n'est pas pris en charge par `direct_io`, comme expliqué dans la documentation de mergerFS [ici](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## J'utilise Sonarr sur un Mac et il a soudainement cessé de fonctionner. Que s'est-il passé ?

- Il s'agit très probablement d'un bogue de MacOS qui a provoqué la corruption d'une des bases de données de Sonarr.
- [Suivez ces étapes pour résoudre le problème](#i-am-getting-an-error-database-disk-image-is-malformed)
- Ensuite, essayez de lancer Sonarr et voyez s'il fonctionne. S'il ne fonctionne pas, vous aurez besoin d'un support supplémentaire. Postez sur notre [reddit](http://reddit.com/r/Sonarr) ou rejoignez notre [discord](https://discord.sonarr.tv/) pour obtenir de l'aide.

## Pourquoi Sonarr ne peut-il pas voir mes fichiers sur un serveur distant ?

- Pour tous les systèmes d'exploitation, assurez-vous que l'utilisateur/groupe sous lequel vous exécutez \*Arr ait les droits de lecture et d'écriture sur le lecteur monté.
- Pour Linux, assurez-vous de :
  - Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé pour votre montage.
  - Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé pour votre montage.
- Pour Windows : En bref, l'utilisateur sous lequel \*Arr s'exécute (s'il s'agit d'un service) ou en dessous (s'il s'agit d'une application de la barre d'état système) ne peut pas accéder au chemin d'accès du fichier sur le serveur distant. Cela peut être dû à diverses raisons, mais la plus courante est que \*Arr s'exécute en tant que service, ce qui provoque les problèmes décrits ci-dessous.

### Sonarr s'exécute par défaut sous le compte LocalService qui n'a pas accès aux partages de fichiers distants protégés

- Exécutez le service Sonarr sous un autre utilisateur qui a accès à ce partage.
- Ouvrez la fenêtre Outils d'administration \> Services sur votre serveur Windows.
- Arrêtez le service Sonarr.
- Ouvrez la boîte de dialogue Propriétés \> Connexion.
- Changez le compte utilisateur du service pour le compte utilisateur cible.
- Exécutez Sonarr.exe à l'aide du dossier de démarrage

### Vous utilisez un lecteur réseau mappé (pas un chemin UNC)

- Modifiez vos chemins d'accès en chemins UNC (`\\serveur\partage`)
- Exécutez Sonarr.exe via le dossier de démarrage

## Lecteurs réseau mappés vs chemins UNC

- L'utilisation de lecteurs réseau mappés ne fonctionne généralement pas très bien, surtout lorsque Sonarr est configuré pour s'exécuter en tant que service. La meilleure façon de configurer les partages est d'utiliser des chemins UNC. Ainsi, au lieu de `X:\TV`, utilisez `\\Serveur\TV`.

- Un point clé à retenir est que Sonarr obtient des informations de chemin d'accès à partir du téléchargeur, vous devrez donc *également* configurer NZBGet, SABNzbd ou tout autre téléchargeur pour utiliser des chemins UNC.

## Sonarr ne fonctionnera pas sur Big Sur

Exécutez la commande suivante :

```shell
chmod +x /Applications/Sonarr.app/Contents/MacOS/Sonarr
```

## Mon script personnalisé a cessé de fonctionner après la mise à niveau depuis la version 2

- Il est probable que vous passiez des arguments dans votre connexion... ce qui n'est pas pris en charge.
- Pour corriger cela :
  1. Modifiez votre argument pour qu'il soit votre chemin d'accès
  1. Assurez-vous que le shebang dans votre script correspond à votre chemin d'accès pwsh (si vous n'avez pas de définition de shebang, ajoutez-la)
  1. Assurez-vous que le script pwsh est exécutable

# Problèmes courants de recherche et de téléchargement de Sonarr

## Requête réussie - Aucun résultat renvoyé

- [Consultez cette entrée de dépannage](/sonarr/troubleshooting#query-successful-no-results-returned)

## Pourquoi Sonarr n'a-t-il pas récupéré un épisode que j'attendais ?

Tout d'abord, assurez-vous de lire et de comprendre la section ci-dessus intitulée "Comment Sonarr trouve-t-il les épisodes ?". Ensuite, assurez-vous qu'au moins l'un de vos indexeurs possède l'épisode que vous attendiez.

1. Cliquez sur l'icône "Recherche manuelle" à côté de la liste des épisodes dans Sonarr. Y a-t-il des résultats ? Si non, alors soit Sonarr a du mal à communiquer avec vos indexeurs, soit vos indexeurs n'ont pas l'épisode, soit l'épisode est mal nommé/catégorisé sur l'indexeur.
1. **S'il y a des résultats à l'étape 1**, vérifiez à côté d'eux l'icône du point d'exclamation rouge. Passez le curseur sur l'icône pour voir pourquoi cette version n'est pas éligible pour les téléchargements automatiques. Si chaque résultat a l'icône, aucun téléchargement automatique ne se produira.
1. **S'il y a au moins un résultat de recherche manuelle valide à l'étape 2**, alors un téléchargement automatique aurait dû se produire. S'il ne s'est pas produit, la raison la plus probable est un problème de communication temporaire empêchant une synchronisation RSS depuis votre indexeur. Il est recommandé d'avoir plusieurs indexeurs configurés pour de meilleurs résultats.
1. **S'il n'y a aucun résultat manuel pour une émission, mais que vous pouvez le trouver lorsque vous parcourez le site de votre indexeur** - Cela peut être dû à plusieurs raisons, par exemple la version n'est pas correctement étiquetée sur votre indexeur, ce qui fait qu'elle n'est pas renvoyée à Sonarr lors d'une recherche automatique. Cette [entrée de dépannage](/sonarr/troubleshooting#searches-indexers-and-trackers) fournit quelques conseils pour déterminer la cause. Avoir plusieurs indexeurs actifs peut aider à résoudre ce problème en fournissant plus de sources pour le même contenu.

## Des séries correspondantes ont été trouvées via l'historique des téléchargements, mais la version a été associée à la série par ID. L'importation automatique n'est pas possible.

- Voir [cette entrée de dépannage](/sonarr/troubleshooting#found-matching-series-via-grab-history-but-series-was-matched-by-series-id-automatic-import-is-not-possible)

- Sur TVDb, lorsque les noms des épisodes sont inconnus, ils sont intitulés TBA et il y a un cache de 24 heures sur l'API de TVDb. En général, les modifications apportées au site de TVDb mettent 24 à 48 heures pour atteindre Sonarr en raison du cache de TVDb (24 heures), du cache de skyhook (quelques heures) et de l'intervalle de rafraîchissement des séries (toutes les 12 heures). Le paramètre [Titre de l'épisode requis](/sonarr/settings#importing) dans Sonarr contrôle le comportement de l'importation lorsque le titre est TBA, mais après 48 heures à partir de la diffusion de la série, la version sera importée même si le titre est toujours TBA. Il n'y a également aucune renommage automatique des fichiers intitulés TBA. Notez que le minuteur TBA est calculé à partir de la date et de l'heure de diffusion de l'épisode, et non à partir du moment où vous l'avez téléchargé ou de l'heure de mise en ligne.

## Sonarr indique "Série inconnue" lors des recherches ou des importations

- Voir l'entrée [Pourquoi Sonarr ne peut-il pas importer les fichiers d'épisodes pour la série X ? / Pourquoi Sonarr ne peut-il pas trouver les versions pour la série X ?](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x)

## L'endpoint /all de Jackett

{#jackett-all-endpoint}

- L'endpoint `/all` de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc nécessaire d'ajouter chaque tracker individuellement. Alternativement, vous pouvez envisager d'utiliser l'alternative Jackett & NZBHydra2 [Prowlarr](/prowlarr)

- **Mise à jour du 5 février 2022 : Le support de \*Arr pour l'endpoint `\all` de Jackett a été abandonné. L'endpoint Jackett /all n'est plus pris en charge (par exemple, des avertissements apparaîtront) à partir de la version 3.0.6.1457 car il ne cause que des problèmes.**

- L'endpoint /all de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc désormais nécessaire d'ajouter chaque tracker individuellement.
- [Même les développeurs de Jackett disent qu'il faut l'éviter et ne pas l'utiliser.](https://github.com/Jackett/Jackett#aggregate-indexers)
- L'utilisation de l'endpoint /all n'a aucun avantage, seulement des inconvénients :
  - vous perdez le contrôle sur les paramètres spécifiques de l'indexeur (catégories, modes de recherche, etc.)
  - mélanger les modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
  - les catégories spécifiques de l'indexeur (\>= 100000) ne peuvent pas être utilisées.
  - les indexeurs lents ralentiront le résultat global
  - le nombre total de résultats est limité à 1000
  - si l'un des trackers dans /all renvoie une erreur, \*Arr le désactivera et vous n'obtiendrez plus aucun résultat.

### Solutions pour l'endpoint /all de Jackett

- Ajoutez chaque tracker dans Jackett manuellement en tant qu'indexeur dans \*Arr
- Consultez [Prowlarr](/prowlarr) qui peut synchroniser les indexeurs avec \*Arr et qui provient de l'équipe de développement de Lidarr/Radarr/Readarr.
- Consultez [NZBHydra2](https://github.com/theotherp/nzbhydra2) qui peut synchroniser les indexeurs avec \*Arr. Mais n'utilisez pas leur endpoint agrégé unique et utilisez `multi` si la synchronisation est utilisée.

## Jackett affiche plus de résultats que Sonarr lors d'une recherche manuelle

- Vérifiez les catégories configurées pour votre tracker dans Sonarr
- Cela est généralement dû au fait que Sonarr recherche Jackett différemment de vous. [Consultez cet article de dépannage pour plus d'informations](/sonarr/troubleshooting#searches-indexers-and-trackers).

## Trouver des cookies

- Certains sites ne peuvent pas être connectés automatiquement et vous obligent à vous connecter manuellement, puis à donner les cookies à Sonarr pour qu'il fonctionne. [Veuillez consulter cet article pour plus de détails.](/useful-tools#finding-cookies)

## Décompresser les torrents

- La plupart des clients torrent ne disposent pas de la gestion automatique des archives compressées comme leurs homologues Usenet. Nous recommandons [unpackerr](https://github.com/unpackerr/unpackerr).

## Autorisations

- Sonarr devra déplacer les fichiers du répertoire où le téléchargeur les place vers l'emplacement final, ce qui signifie que Sonarr devra lire/écrire à la fois dans le répertoire source et dans le répertoire et les fichiers de destination.
- Sur Linux, où les bonnes pratiques consistent à exécuter les services en tant qu'utilisateur distinct, cela signifiera probablement l'utilisation d'un groupe partagé et la configuration des autorisations de dossier sur `775` et des fichiers sur `664` à la fois dans votre téléchargeur et Sonarr. En notation umask, cela serait `002`.

## Authentification obligatoire

- Dans Sonarr v4 (bêta), l'authentification est obligatoire. Veuillez consulter la [FAQ de Sonarr v4 - Authentification obligatoire](/sonarr/faq-v4#forced-authentication) pour plus de détails.