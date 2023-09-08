---
title: Système Prowlarr
description: 
published: true
date: 2023-05-31T11:54:59.064Z
tags: prowlarr, système
editor: markdown
dateCreated: 2021-08-03T21:21:08.969Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Statut](#statut)
  - [Santé](#santé)
    - [Avertissements système](#avertissements-système)
      - [La branche n'est pas une branche de version valide](#la-branche-nest-pas-une-branche-de-version-valide)
      - [La version SQLite actuellement installée n'est pas prise en charge](#la-version-sqlite-actuellement-installée-nest-pas-prise-en-charge)
      - [Une nouvelle mise à jour est disponible](#une-nouvelle-mise-à-jour-est-disponible)
      - [Impossible d'installer la mise à jour car le dossier de démarrage n'est pas accessible en écriture par l'utilisateur](#impossible-dinstaller-la-mise-à-jour-car-le-dossier-de-démarrage-nest-pas-accessible-en-écriture-par-lutilisateur)
      - [La mise à jour ne sera pas possible pour éviter la suppression des données d'application lors de la mise à jour](#la-mise-à-jour-ne-sera-pas-possible-pour-éviter-la-suppression-des-données-dapplication-lors-de-la-mise-à-jour)
      - [La branche est pour une version précédente](#la-branche-est-pour-une-version-précédente)
      - [Impossible de se connecter à signalR](#impossible-de-se-connecter-à-signalr)
      - [Échec de résolution de l'adresse IP pour l'hôte proxy configuré](#échec-de-résolution-de-ladresse-ip-pour-lhôte-proxy-configuré)
      - [Échec du test du proxy](#échec-du-test-du-proxy)
      - [L'heure système est décalée de plus d'un jour](#lheure-système-est-décalée-de-plus-dun-jour)
    - [Clients de téléchargement](#clients-de-téléchargement)
      - [Aucun client de téléchargement n'est disponible](#aucun-client-de-téléchargement-nest-disponible)
      - [Impossible de communiquer avec le client de téléchargement](#impossible-de-communiquer-avec-le-client-de-téléchargement)
      - [Les clients de téléchargement ne sont pas disponibles en raison d'une défaillance](#les-clients-de-téléchargement-ne-sont-pas-disponibles-en-raison-dune-défaillance)
      - [Mauvais paramètres du client de téléchargement](#mauvais-paramètres-du-client-de-téléchargement)
    - [Indexeurs](#indexeurs)
      - [Les indexeurs n'ont pas de définition](#les-indexeurs-nont-pas-de-définition)
      - [Les indexeurs sont obsolètes](#les-indexeurs-sont-obsolètes)
        - [Obsolète en raison de modifications de code](#obsolète-en-raison-de-modifications-de-code)
        - [Obsolète en raison de la suppression de sites](#obsolète-en-raison-de-la-suppression-de-sites)
      - [Aucun indexeur n'est activé](#aucun-indexeur-nest-activé)
      - [Les indexeurs ne sont pas disponibles en raison de défaillances](#les-indexeurs-ne-sont-pas-disponibles-en-raison-de-défaillances)
      - [Expiration de l'abonnement VIP de l'indexeur](#expiration-de-labonnement-vip-de-lindexeur)
      - [L'abonnement VIP de l'indexeur a expiré](#labonnement-vip-de-lindexeur-a-expiré)
    - [Applications](#applications)
      - [Les applications ne sont pas disponibles en raison de défaillances](#les-applications-ne-sont-pas-disponibles-en-raison-de-défaillances)
  - [Espace disque](#espace-disque)
  - [À propos](#à-propos)
  - [Plus d'informations](#plus-dinformations)
- [Tâches](#tâches)
  - [Planifiées](#planifiées)
  - [File d'attente](#file-dattente)
- [Sauvegarde](#sauvegarde)
- [Mises à jour](#mises-à-jour)
- [Événements](#événements)
- [Fichiers journaux](#fichiers-journaux)

# Statut

## Santé

Cette page contient une liste des erreurs de vérification de santé. Ces vérifications de santé sont effectuées périodiquement par Prowlarr et lors de certains événements. Les avertissements et erreurs résultants sont répertoriés ici pour donner des conseils sur la façon de les résoudre.

### Avertissements système

#### La branche n'est pas une branche de version valide

- La branche que vous avez définie n'est pas une branche de version valide. Vous ne recevrez pas de mises à jour. Veuillez changer pour l'une des [branches de version actuelles](/prowlarr/faq#how-do-i-update-prowlarr).

#### La version SQLite actuellement installée n'est pas prise en charge

- Prowlarr stocke ses données dans une base de données SQLite. La bibliothèque SQLite3 installée sur votre système est trop ancienne. Prowlarr nécessite au moins la version 3.9.0. Notez que Prowlarr utilise `libSQLite3.so` qui peut être contenue ou non dans un package de mise à niveau SQLite3.

#### Une nouvelle mise à jour est disponible

- Réjouissez-vous, les développeurs ont publié une nouvelle mise à jour. Cela signifie généralement de nouvelles fonctionnalités géniales et des tas de bogues corrigés (n'est-ce pas ?). Apparemment, vous n'avez pas activé la mise à jour automatique, vous devrez donc trouver comment mettre à jour sur votre plateforme. Appuyer sur le bouton Installer sur la page Système => Mises à jour est probablement un bon point de départ.

> Cet avertissement n'apparaîtra pas si votre version actuelle a moins de 14 jours
{.is-info}

#### Impossible d'installer la mise à jour car le dossier de démarrage n'est pas accessible en écriture par l'utilisateur

- Cela signifie que Prowlarr ne pourra pas se mettre à jour automatiquement. Vous devrez mettre à jour Prowlarr manuellement ou définir les autorisations sur le répertoire de démarrage de Prowlarr (le répertoire d'installation) pour permettre à Prowlarr de se mettre à jour.

#### La mise à jour ne sera pas possible pour éviter la suppression des données d'application lors de la mise à jour

- Prowlarr a détecté que le dossier AppData de votre système d'exploitation est situé à l'intérieur du répertoire qui contient les binaires de Prowlarr. Normalement, il s'agirait de C:\ProgramData pour Windows et ~/.config pour Linux.

- Veuillez consulter Système => Info pour voir les répertoires AppData et de démarrage actuels.
- Cela signifie que Prowlarr ne pourra pas se mettre à jour sans risquer de perdre des données.
- Si vous êtes sous Linux, vous devrez probablement changer le répertoire personnel de l'utilisateur qui exécute Prowlarr et copier le contenu actuel du répertoire ~/.config/Prowlarr pour préserver votre base de données.

#### La branche est pour une version précédente

- La branche de mise à jour configurée dans Paramètres/Général est pour une version précédente de Prowlarr, par conséquent, l'instance ne verra pas les informations de mise à jour correctes dans le flux Mises à jour du système et ne recevra peut-être pas les nouvelles mises à jour lorsqu'elles seront publiées.

#### Impossible de se connecter à signalR

- signalR permet les mises à jour dynamiques de l'interface utilisateur, donc si votre navigateur ne peut pas se connecter à signalR sur votre serveur, vous ne verrez aucune mise à jour en temps réel dans l'interface utilisateur.

- Le cas le plus courant est l'utilisation d'un proxy inverse ou de Cloudflare
  - Cloudflare nécessite l'activation des websockets.
  - Nginx nécessite l'ajout suivant au bloc de localisation de l'application :

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Assurez-vous de ne pas inclure proxy_set_header Connection "Upgrade"; comme suggéré par la documentation de nginx. CELA NE FONCTIONNERA PAS
> Voir <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

- Pour Apache2 en tant que proxy inverse, vous devez activer les modules suivants : proxy, proxy_http et proxy_wstunnel. Ensuite, ajoutez cette directive de tunnel websocket à la configuration de votre hôte virtuel :

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:9696/$1 [P,L]
```

Si vous avez un proxy inverse dans un sous-répertoire, la RewriteRule doit inclure votre chemin de base, par exemple :

```none
RewriteRule /prowlarr/(.*) ws://127.0.0.1:9696/prowlarr/$1 [P,L]
```

Si Prowlarr ne s'exécute pas sur la même machine que votre proxy inverse, remplacez 127.0.0.1 par l'adresse IP/DNS appropriée de votre application Prowlarr.

- Pour Caddy (V1), utilisez ceci :

> Remarque : vous devrez également ajouter la directive websocket à votre configuration de prowlarr{.is-info}

```none
 proxy /prowlarr 127.0.0.1:9696 {
     websocket
     transparent
 }
```

#### Échec de résolution de l'adresse IP pour l'hôte proxy configuré

- Vérifiez vos paramètres de proxy et assurez-vous qu'ils sont corrects.
- Assurez-vous que votre proxy est actif, en cours d'exécution et accessible.

#### Échec du test du proxy

- Votre proxy configuré a échoué lors du test. Veuillez vérifier l'erreur HTTP fournie et/ou consulter les journaux pour plus de détails.

#### L'heure système est décalée de plus d'un jour

- L'heure système est décalée de plus d'un jour. Les tâches planifiées peuvent ne pas s'exécuter correctement tant que l'heure n'est pas corrigée.
- Vérifiez l'heure système et assurez-vous qu'elle est synchronisée avec un serveur de temps de référence et qu'elle est précise.

### Clients de téléchargement

#### Aucun client de téléchargement n'est disponible

- Un client de téléchargement correctement configuré et activé est requis pour que Prowlarr puisse télécharger des médias. Puisque Prowlarr prend en charge différents clients de téléchargement, vous devez déterminer celui qui correspond le mieux à vos besoins. Si vous avez déjà un client de téléchargement installé, vous devez le configurer pour l'utiliser avec Prowlarr et créer une catégorie. Voir Paramètres => Client de téléchargement.

#### Impossible de communiquer avec le client de téléchargement

- Prowlarr n'a pas pu communiquer avec le client de téléchargement configuré. Veuillez vérifier si le client de téléchargement est opérationnel et vérifier à nouveau l'URL. Cela peut également indiquer une erreur d'authentification.
- Cela est généralement dû à une mauvaise configuration du client de téléchargement. Voici quelques éléments que vous pouvez vérifier :
- L'adresse IP de vos clients de téléchargement, si elle est sur la même machine physique, il s'agit généralement de 127.0.0.1
- Le numéro de port que votre client de téléchargement utilise, ces champs sont remplis avec le numéro de port par défaut, mais si vous l'avez modifié, vous devrez entrer le même numéro dans Prowlarr.
- Assurez-vous que le chiffrement SSL n'est pas activé si vous utilisez à la fois votre instance Prowlarr et votre client de téléchargement sur un réseau local. Consultez la FAQ SSL pour plus d'informations.
- L'utilisation de rutorrent nécessite des modifications spéciales des paramètres car elle nécessite https.

#### Les clients de téléchargement ne sont pas disponibles en raison d'une défaillance

- Un ou plusieurs de vos clients de téléchargement ne répondent pas aux demandes de Prowlarr. Par conséquent, Prowlarr a décidé d'arrêter temporairement les requêtes au client de téléchargement selon son cycle normal d'une minute, qui est normalement utilisé pour suivre les téléchargements actifs et importer les téléchargements terminés. Cependant, Prowlarr continuera à essayer d'envoyer des téléchargements au client, mais il échouera très probablement.
- Vous devriez consulter Système => Journaux pour voir la raison des échecs.
- Si vous n'utilisez plus ce client de téléchargement, désactivez-le dans Prowlarr pour éviter les erreurs.

#### Mauvais paramètres du client de téléchargement

- L'emplacement où votre client de téléchargement télécharge les fichiers pose problème. Vérifiez les journaux pour plus d'informations. Cela peut être dû à des problèmes de permissions ou à une tentative de transfert de Windows à Linux ou de Linux à Windows sans mappage de chemin distant.

### Indexeurs

#### Les indexeurs n'ont pas de définition

- Votre(s) indexeur(s) n'a/n'ont pas de définition (fichier) existante, cela est généralement dû à la suppression de votre indexeur ou à l'inaccessibilité de la définition YAML de Cardigann.

#### Les indexeurs sont obsolètes

- La définition de votre/des indexeur(s) est obsolète et dépassée. Cela a deux causes possibles qui sont indiquées ci-dessous.

##### Obsolète en raison de modifications de code

- En raison de modifications de code, le(s) indexeur(s) noté(s) est/sont obsolète(s) tel(s) que configuré(s) actuellement. Supprimez et réajoutez l'indexeur à Prowlarr pour résoudre le problème.
- Cela est généralement causé par la conversion d'API ou du YML au C# ou vice versa.

##### Obsolète en raison de la suppression de sites

- Certains sites peuvent être demandés à être supprimés de Prowlarr ou Jackett. Ils peuvent alors être marqués comme obsolètes.
  - [TVVault](https://github.com/Prowlarr/Prowlarr/issues/573) dans [Prowlarr #700](https://github.com/Prowlarr/Prowlarr/pull/700)
  - Audiobookbay a demandé à ce que Prowlarr n'accède pas à leur API
  - Ebookbay a demandé à ce que Prowlarr n'accède pas à leur API
  - Rarbg a [fermé ses portes à partir du 2023-05-31](https://torrentfreak.com/iconic-torrent-site-rarbg-shuts-down-all-content-releases-stop-230531/)

#### Aucun indexeur n'est activé

- Prowlarr nécessite des indexeurs pour pouvoir découvrir de nouvelles sorties. Veuillez lire les instructions du wiki sur la façon d'ajouter des indexeurs.

#### Les indexeurs ne sont pas disponibles en raison de défaillances

- Une ou plusieurs erreurs se sont produites lorsque Prowlarr a essayé d'utiliser l'un de vos indexeurs. Pour limiter les nouvelles tentatives, Prowlarr n'utilisera pas l'indexeur pendant une durée de plus en plus longue (jusqu'à 24 heures).
- Consultez les événements et filtrez les avertissements pour avoir une idée rapide des problèmes survenus historiquement.
- Ce mécanisme est déclenché si Prowlarr n'a pas pu obtenir de réponse de l'indexeur (cela peut être dû à un problème DNS, de connexion proxy/VPN, d'authentification ou d'indexeur) ou s'il n'a pas pu récupérer le fichier nzb/torrent de l'indexeur. Veuillez consulter les journaux pour déterminer quel type d'erreur cause le problème.
- Vous pouvez éviter l'avertissement en désactivant l'indexeur concerné.
- Exécutez le test sur l'indexeur pour forcer Prowlarr à vérifier à nouveau l'indexeur, veuillez noter que l'avertissement de vérification de santé ne disparaîtra pas toujours immédiatement.

#### Expiration de l'abonnement VIP de l'indexeur

- Votre abonnement VIP ou les avantages de votre indexeur expirent dans les 7 prochains jours ou moins en fonction de la date d'expiration que vous avez configurée pour votre indexeur dans Prowlarr.

#### L'abonnement VIP de l'indexeur a expiré

- Votre abonnement VIP ou les avantages de votre indexeur ont expiré en fonction de la date d'expiration que vous avez configurée pour votre indexeur dans Prowlarr.

### Applications

#### Les applications ne sont pas disponibles en raison de défaillances

- Une ou plusieurs erreurs se sont produites lorsque Prowlarr a essayé d'utiliser l'une de vos applications. Pour limiter les nouvelles tentatives, Prowlarr n'utilisera pas l'application pendant une durée de plus en plus longue (jusqu'à 24 heures).
- Ce mécanisme est déclenché si Prowlarr n'a pas pu obtenir de réponse de l'application (cela peut être dû à un problème DNS, de connexion, d'authentification ou d'application). Veuillez consulter les journaux pour déterminer quel type d'erreur cause le problème.
- Consultez les événements et filtrez les avertissements pour avoir une idée rapide des problèmes survenus historiquement.
- Prowlarr ne pourra pas se synchroniser avec l'application et il est fort probable que l'application ne pourra pas utiliser les indexeurs de Prowlarr.
- Vous pouvez éviter l'avertissement en désactivant l'application concernée.
- Exécutez le test sur l'application pour forcer Prowlarr à vérifier à nouveau l'application, veuillez noter que l'avertissement de vérification de santé ne disparaîtra pas toujours immédiatement.

## Espace disque

Cette section vous montrera l'espace disque disponible.
Dans Docker, cela peut être délicat car il affiche généralement l'espace disponible dans votre image Docker.

## À propos

Cela vous donnera des informations sur votre installation actuelle de Prowlarr.

## Plus d'informations

Page d'accueil : Page d'accueil de Prowlarr
Wiki : Vous êtes déjà ici
Reddit : r/prowlarr
Discord : Rejoignez notre discord
Dons : Si vous vous sentez généreux et que vous souhaitez faire un don, cliquez ici
Dons à Sonarr : Si vous vous sentez généreux et que vous souhaitez faire un don au projet qui a tout commencé, cliquez ici
Source : GitHub
Demandes de fonctionnalités : Vous avez une excellente idée, partagez-la ici

# Tâches

## Planifiées

Cette page répertorie toutes les tâches planifiées exécutées par Prowlarr.

- Vérification de la mise à jour de l'application - Cette tâche s'exécute selon la planification affichée dans l'interface utilisateur, vérifiant si Prowlarr est à la version la plus récente, puis déclenchant le script de mise à jour pour mettre à jour Prowlarr. Paramètres => Mise à jour

> Remarque : Si vous utilisez Docker, cela ne mettra pas à jour votre conteneur car une nouvelle image devra être téléchargée.
{.is-warning}

- Sauvegarde - Cette tâche effectuera une sauvegarde de la base de données de votre Prowlarr selon une planification définie. Vous trouverez plus de détails à ce sujet ici. Vous trouverez plus d'informations sur les sauvegardes dans Système => Sauvegardes.
- Vérification de la santé - La vérification de la santé s'exécute selon la planification affichée dans l'interface utilisateur, vérifiant la santé globale de votre Prowlarr. Pour voir une liste des problèmes de santé possibles, consultez l'entrée du wiki sur les vérifications de santé.
- Entretien - Selon la planification affichée dans l'interface utilisateur, cela permet de dépoussiérer les toiles d'araignée, de balayer et d'aspirer les sols, de laver, de faire briller et même de faire de jolis petits plis juste pour vous. Mais il ne sort pas les poubelles. Il n'est tout simplement pas assez bien payé pour ça.
- Nettoyage des messages - Selon la planification affichée dans l'interface utilisateur, cela permet de nettoyer les messages qui apparaissent dans le coin inférieur gauche de Prowlarr.
  
> Toutes ces tâches peuvent être exécutées manuellement en dehors de leur planification en cliquant sur l'icône à l'extrême droite de chacune des tâches.
{.is-info}

## File d'attente

La file d'attente vous montrera les tâches à venir ainsi qu'un historique des tâches récemment exécutées ainsi que la durée de ces tâches.

# Sauvegarde

> Cette section sera plus adaptée aux boutons et à l'objectif général de la page.
> Cependant, si vous souhaitez savoir comment sauvegarder/restaurer votre instance Prowlarr, [consultez notre FAQ](/prowlarr/faq).
{.is-info}

Dans la section Sauvegarde, vous verrez les sauvegardes précédentes (sauf si vous venez d'installer Prowlarr et n'avez effectué aucune sauvegarde).

Vous aurez deux options en haut de l'écran :

- Sauvegarder maintenant : cette option déclenchera une sauvegarde manuelle de la base de données de Prowlarr.
- Restaurer une sauvegarde : cela ouvrira une nouvelle fenêtre pour restaurer à partir d'une sauvegarde précédente. En sélectionnant "Choisir un fichier", votre navigateur affichera une boîte de dialogue pour restaurer à partir d'une sauvegarde Zip de Prowlarr.

Enfin, si vous avez des sauvegardes précédentes et que vous souhaitez les télécharger depuis Prowlarr pour les placer dans un emplacement non standard, vous pouvez simplement sélectionner l'un de ces fichiers pour les télécharger.

À droite de chaque téléchargement précédent, vous avez deux options :

- Un - Pour restaurer à partir d'une sauvegarde précédente : cela ouvrira une nouvelle fenêtre pour confirmer que vous souhaitez restaurer à partir de cette sauvegarde.
- Deux - Pour supprimer une sauvegarde précédente.

# Mises à jour

L'écran des mises à jour affichera les 5 dernières mises à jour effectuées ainsi que la version actuelle que vous utilisez.
Cette page affichera également les notes de mise à jour des développeurs, vous indiquant ce qui a été corrigé ou ajouté à Prowlarr (Réjouissez-vous !).

> Une version de maintenance contient des corrections de bugs et diverses améliorations. Consultez l'historique des commits pour plus de détails.
{.is-info}

# Événements

L'onglet Événements vous montrera ce qui s'est passé dans votre Prowlarr. Cela peut être utilisé pour diagnostiquer certains problèmes mineurs. Cependant, cela ne remplace pas les journaux de trace discutés dans la section Journalisation. Les événements sont l'équivalent des journaux INFO.

- Composants : cette colonne vous indiquera quel composant de Prowlarr a été déclenché.
- Message : cette colonne vous indiquera quel message a été envoyé par le composant de la colonne précédente.
- Icône d'engrenage : cette option vous permettra de modifier le nombre de composants/messages affichés par page (par défaut : 50).
- Options en haut de la page :
  - Rafraîchir : cette option actualisera la page actuelle, en récupérant un nouveau journal des événements.
  - Effacer : cela effacera le journal des événements actuel, vous permettant de repartir à zéro.

# Fichiers journaux

Cette page vous permettra de télécharger et de voir quels fichiers journaux sont disponibles pour Prowlarr.

Sur la première ligne, vous trouverez plusieurs options pour contrôler vos fichiers journaux.

- Sur la première ligne, tout à gauche, il y a une liste déroulante qui vous permettra de passer des fichiers journaux aux fichiers journaux de mise à jour.
  - Fichiers journaux : l'essentiel de tout problème de support se trouve ici. Vous trouverez plus d'informations sur les fichiers journaux ici.
  - Fichiers journaux de mise à jour : cela affichera les fichiers journaux associés au script de mise à jour de Prowlarr.

> Si vous utilisez Docker, cette section sera vide car vous devriez effectuer la mise à jour en téléchargeant une nouvelle image Docker.
{.is-info}

- Rafraîchir : cela actualisera la page actuelle et affichera tous les journaux récemment créés.
- Supprimer : cela effacera tous les journaux, vous permettant de repartir à zéro.
- Nom du fichier : cela affichera le nom du fichier associé au journal.
- Dernière écriture : il s'agit de l'heure locale à laquelle ce fichier journal particulier a été écrit.
  - Prowlarr utilise des fichiers journaux en rotation limités à 1 Mo chacun. Le fichier journal actuel est toujours prowlarr.txt, pour les autres fichiers, prowlarr.0.txt est le plus récent (plus le nombre est élevé, plus le fichier est ancien), jusqu'à un total de 51 fichiers journaux. Ce fichier journal contient les entrées `fatal`, `error`, `warn` et `info`.
  - Lorsque le niveau de journalisation de débogage est activé, des fichiers journaux en rotation supplémentaires prowlarr.debug.txt seront présents, jusqu'à 51 fichiers. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info` et `debug`. Ils couvrent généralement une période d'environ 40 heures.
  - Lorsque le niveau de journalisation de trace est activé, des fichiers journaux en rotation supplémentaires prowlarr.trace.txt seront présents, jusqu'à 51 fichiers. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info`, `debug` et `trace`. En raison de la verbosité de la trace, ils ne couvrent que quelques heures au maximum.