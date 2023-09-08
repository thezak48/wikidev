---
title: Dépannage de Prowlarr
description: 
published: true
date: 2023-08-20T00:20:04.841Z
tags: prowlarr, dépannage
editor: markdown
dateCreated: 2021-06-20T20:05:25.223Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Demander de l'aide](#demander-de-laide)
- [Journalisation et fichiers journaux](#journalisation-et-fichiers-journaux)
  - [Emplacement des journaux standard](#emplacement-des-journaux-standard)
  - [Emplacement des journaux de mise à jour](#emplacement-des-journaux-de-mise-à-jour)
  - [Partage des journaux](#partage-des-journaux)
  - [Journaux de trace/débogage](#journaux-de-tracedébogage)
  - [Effacement des journaux](#effacement-des-journaux)
- [Fichiers journaux multiples](#fichiers-journaux-multiples)
- [Récupération d'une mise à jour échouée](#récupération-dune-mise-à-jour-échouée)
  - [Déterminer le problème](#déterminer-le-problème)
    - [Problème de migration](#problème-de-migration)
    - [Problème de permission](#problème-de-permission)
  - [Résoudre le problème](#résoudre-le-problème)
    - [Problèmes de permissions](#problèmes-de-permissions)
    - [Mise à niveau manuelle](#mise-à-niveau-manuelle)
- [Erreurs NGINX](#erreurs-nginx)
- [Problèmes d'indexeur, d'application et de client de téléchargement](#problèmes-dindexeur-dapplication-et-de-client-de-téléchargement)
  - [Impossible de déterminer la taille de la trame ou une trame corrompue a été reçue](#impossible-de-déterminer-la-taille-de-la-trame-ou-une-trame-corrompue-a-été-reçue)
  - [Délai de connexion dépassé](#délai-de-connexion-dépassé)
  - [Erreurs HTTP 404 de Sonarr](#erreurs-http-404-de-sonarr)
  - [Erreurs HTTP 400 de \*Arr](#erreurs-http-400-de-arr)
  - [503 Service non disponible](#503-service-non-disponible)
  - [Torrents invalides](#torrents-invalides)
  - [Recherche, indexeurs et trackers](#recherche-indexeurs-et-trackers)

# Demander de l'aide

Vous avez besoin d'aide ? C'est normal, tout le monde a besoin d'aide parfois. Vous pouvez obtenir de l'aide en temps réel via le chat sur

- [<i class="fab fa-discord"></i>&emsp;Discord *Discord officiel de Prowlarr*](https://prowlarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Subreddit officiel de Prowlarr*](https://reddit.com/r/prowlarr)
{.links-list}

Mais avant d'y aller et de poster, assurez-vous que votre demande d'aide est la meilleure possible. Décrivez clairement le problème et décrivez brièvement votre configuration, y compris des éléments tels que votre système d'exploitation/distribution, la version de .NET, la version de Prowlarr, le client de téléchargement et sa version. **Si vous utilisez [Docker](https://www.docker.com/), veuillez suivre d'abord le [Guide Docker](/docker-guide) car cela résoudra les problèmes courants et fréquents de chemin/permissions. Sinon, veuillez avoir un [docker compose](/docker-guide#docker-compose) à portée de main. [Comment générer un Docker Compose](https://trash-guides.info/compose)** Parlez-nous de ce que vous avez déjà essayé, de ce que vous avez examiné. Utilisez la section [Journalisation et fichiers journaux](#journalisation-et-fichiers-journaux) pour augmenter le niveau de journalisation à la trace, recréer le problème, collez le contexte pertinent dans un pastebin et incluez un lien vers celui-ci dans votre message. Vous pouvez même inclure des captures d'écran pour mettre en évidence le problème.

Plus nous en savons, plus il est facile de vous aider.

# Journalisation et fichiers journaux

Il est également utile de consulter les [Problèmes courants des indexeurs, des applications et des clients de téléchargement](#problèmes-dindexeur-dapplication-et-de-client-de-téléchargement).

> Si on vous demande de fournir la réponse de l'indexeur à des fins de développement ou de débogage, lisez la section bleue ci-dessous... sinon, passez aux étapes ci-dessous. Pour le débogage des réponses de l'indexeur, il est probablement utile d'aller dans `settings/development` (page masquée) dans Prowlarr et d'activer temporairement l'enregistrement amélioré de l'indexeur pour enregistrer la réponse de l'indexeur. Il ne doit pas être activé en permanence
{.is-info}

Si on vous demande des journaux de débogage, vos journaux contiendront `debug` et si on vous demande des journaux de trace, vos journaux contiendront `trace`. Si les journaux que vous fournissez ne contiennent ni l'un ni l'autre, ce ne sont pas les journaux demandés.

- Évitez de partager l'intégralité du fichier journal à moins qu'on ne vous le demande.
- N'envoyez pas les journaux directement sur Discord ou ne les collez pas sous forme de murs de texte, sauf demande expresse.
- Ne partagez pas les journaux en tant que pièce jointe, archive zip ou tout autre format autre que du texte partagé via les services indiqués ci-dessous.

Pour fournir de bons et utiles journaux à partager :

> Assurez-vous qu'une tâche spammy ne s'exécute PAS, comme une actualisation RSS
{.is-warning}

1. [Augmentez le niveau de journalisation à Trace (Paramètres => Général => Niveau de journalisation ou modifiez le fichier de configuration)](#journaux-de-tracedébogage)
2. [Effacez les journaux (Système => Journaux => Effacer les journaux ou supprimez tous les journaux du dossier de journaux)](#effacement-des-journaux)
3. Reproduisez le problème (refaites ce qui pose problème)
4. [Ouvrez le fichier journal de trace (Lidarr.trace.txt) via l'interface utilisateur ou le fichier journal](#emplacement-des-journaux-standard) sur le système de fichiers et trouvez le contexte pertinent
5. Copiez une grande partie avant le problème, le problème lui-même et une grande partie après le problème.
6. Utilisez [Gist](https://gist.github.com/), [0bin (**Assurez-vous de désactiver la colorisation**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) ou des sites similaires - à l'exception de ceux mentionnés ci-dessous - pour partager les journaux copiés ci-dessus

**Avertissements :**
- **N'utilisez pas [pastebin.com](https://pastebin.com) car leurs filtres ont tendance à bloquer les journaux.
- N'utilisez pas [pastebin.pl](https://pastebin.pl) car leur site n'est souvent pas accessible.
- N'utilisez pas [JustPasteIt](https://justpaste.it/) car leur site ne facilite pas l'examen des journaux.
- Ne téléchargez pas votre journal en tant que fichier.
- Ne téléchargez pas et ne partagez pas vos journaux via Google Drive, Dropbox ou tout autre site non mentionné ci-dessus.
- N'archivez pas (zip, tar (tarball), 7zip, etc.) vos journaux.
- Ne partagez pas la sortie de la console, la sortie du conteneur Docker ou autre chose que les journaux d'application spécifiés

**Note importante :**
- Lors de l'utilisation de [0bin](https://0bin.net/), assurez-vous de désactiver la colorisation et de ne pas brûler après lecture.

- Alternativement, si vous recherchez une entrée spécifique dans un ancien fichier journal mais que vous n'êtes pas sûr duquel, vous pouvez utiliser N++. Vous pouvez utiliser la fonction "Rechercher dans les fichiers" de Notepad++ pour rechercher les anciens fichiers journaux selon vos besoins.
- **Unix uniquement :** Alternativement, si vous recherchez une entrée spécifique dans un ancien fichier journal mais que vous n'êtes pas sûr duquel, vous pouvez utiliser grep. Par exemple, si vous voulez trouver des informations sur le film/série/livre/chanson/indexeur "Shooter", vous pouvez exécuter la commande suivante `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Si votre [Répertoire Appdata](/prowlarr/appdata-directory) se trouve dans votre dossier personnel, vous exécuteriez : `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Les indicateurs ont les fonctions suivantes
    * -i : ignorer la casse
    * -n : afficher le numéro de ligne
    * -r : vérifier récursivement tous les fichiers dans le chemin
    * -C : fournir le nombre de lignes avant et après la ligne où il est trouvé
    * -e : le motif à rechercher

```

## Emplacement des journaux standard

Les fichiers journaux se trouvent dans le [Répertoire Appdata](/prowlarr/appdata-directory) de Prowlarr, à l'intérieur du dossier logs/. Vous pouvez également accéder aux fichiers journaux depuis l'interface utilisateur à Système => Journaux => Fichiers.

> Remarque : Le tableau des journaux ("Événements") dans l'interface utilisateur n'est pas identique aux fichiers journaux et n'est pas aussi utile. Si on vous demande des journaux, veuillez copier/coller à partir des fichiers journaux et non de la table.
{.is-info}

## Emplacement des journaux de mise à jour

Les fichiers journaux de mise à jour se trouvent dans le [Répertoire Appdata](/prowlarr/appdata-directory) de Prowlarr, à l'intérieur du dossier UpdateLogs/.

## Partage des journaux

Les journaux peuvent être longs et difficiles à lire dans un message sur un forum ou sur Reddit, et ils sont spammy sur Discord, alors veuillez utiliser [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) ou tout autre site similaire de pastebin. Le fichier entier n'est généralement pas nécessaire, seulement une bonne quantité de contexte avant et après le problème/erreur. N'oubliez pas d'attendre que les tâches spammy comme une synchronisation RSS ou une actualisation de la bibliothèque se terminent.

## Journaux de trace/débogage

Vous pouvez modifier le niveau de journalisation dans Paramètres => Général => Journalisation. Prowlarr n'a pas besoin d'être redémarré pour que le changement prenne effet. Ce changement n'affecte que les fichiers journaux, pas la base de données de journalisation. Les derniers fichiers journaux de débogage/traces sont nommés respectivement `prowlarr.debug.txt` et `prowlarr.trace.txt`.

Si vous ne pouvez pas accéder à l'interface utilisateur pour définir le niveau de journalisation, vous pouvez le faire en modifiant le fichier config.xml dans le répertoire AppData en définissant la valeur LogLevel sur Debug ou Trace au lieu de Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Effacement des journaux

Vous pouvez effacer les fichiers journaux et la base de données de journaux directement depuis l'interface utilisateur, sous `Système` => `Journaux` => `Fichiers` et `Système` => `Journaux` => `Supprimer` (icône de la corbeille).

# Fichiers journaux multiples

Prowlarr utilise des fichiers journaux roulants limités à 1 Mo chacun. Le fichier journal actuel est toujours Prowlarr.txt, pour les autres fichiers, Prowlarr.0.txt est le plus récent (plus le nombre est élevé, plus il est ancien). Ce fichier journal contient les entrées `fatal`, `error`, `warn` et `info`.

Lorsque le niveau de journalisation de débogage est activé, des fichiers journaux roulants supplémentaires `prowlarr.debug.txt` seront présents. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info` et `debug`. Ils couvrent généralement une période de 40 heures.

Lorsque le niveau de journalisation de trace est activé, des fichiers journaux roulants supplémentaires `prowlarr.trace.txt` seront présents. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info`, `debug` et `trace`. En raison de la verbosité de la trace, ils ne couvrent que quelques heures au maximum, et parfois moins d'une minute si vous effectuez une tâche intensive.

# Récupération d'une mise à jour échouée

Nous faisons tout notre possible pour éviter les problèmes lors de la mise à niveau, mais s'ils se produisent, nous vous guiderons dans les étapes à suivre pour récupérer votre installation.

## Déterminer le problème

- Le meilleur endroit où chercher lorsque l'application ne démarre pas après une mise à jour est de consulter les [journaux de mise à jour](#emplacement-des-journaux-de-mise-à-jour) et de voir si la mise à jour s'est terminée avec succès. Si cela ne pose pas de problème, la prochaine étape consiste à consulter vos fichiers journaux d'application habituels, avant de tenter de redémarrer, utilisez [Journalisation](/prowlarr/settings#journalisation) et [Fichiers journaux](/prowlarr/system#fichiers-journaux) pour les trouver et augmenter le niveau de journalisation.
- Le problème le plus fréquemment rencontré est que le système sur lequel l'application est installée a modifié le répertoire `/tmp` et a supprimé des fichiers \*Arr critiques lors de la mise à niveau, ce qui a entraîné l'échec de la mise à niveau et du retour en arrière. Dans ce cas, réinstallez simplement sur place par-dessus l'installation borked existante.

### Problème de migration

- Les erreurs de migration ne seront pas identiques, mais voici un exemple :

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Problème de permission

- Les problèmes de permissions sont dus à l'impossibilité pour l'application d'accéder aux dossiers temporaires pertinents et/ou au dossier binaire de l'application. Corrigez les permissions pour que l'utilisateur/le groupe sous lequel s'exécute l'application puisse accéder aux dossiers appropriés.

- Les utilisateurs de Synology peuvent rencontrer ce bug de Synology `Access to the path '/proc/{some number}/maps is denied`

- Les utilisateurs de Synology peuvent également rencontrer des problèmes d'espace dans `/tmp` sur certains NAS. Vous devrez spécifier un autre chemin `/tmp` pour l'application. Consultez SynoCommunity ou d'autres canaux de support Synology pour obtenir de l'aide à ce sujet.

## Résoudre le problème

En cas de problème de migration, il n'y a pas grand-chose que vous puissiez faire immédiatement, si le problème vous concerne spécifiquement (ou s'il n'y a pas encore de messages à ce sujet), veuillez créer un message sur [notre subreddit](https://reddit.com/r/prowlarr) ou passer sur notre [discord](https://prowlarr.com/discord). Si d'autres personnes ont le même problème, soyez assuré que nous y travaillons.

> Veuillez vous assurer de ne pas avoir essayé d'utiliser une base de données de `nightly` sur la version stable. Il est déconseillé de sauter de branche.{.is-info}

### Problèmes de permissions

- Corrigez les permissions pour que l'utilisateur/le groupe sous lequel s'exécute l'application puisse accéder (lecture et écriture) à la fois à `/tmp` et au répertoire d'installation de l'application.

- Pour les utilisateurs de Synology qui rencontrent des problèmes avec `/proc/###/maps` qui arrêtent Sonarr ou les autres applications \*Arr et mettent à jour devraient résoudre ce problème. Il s'agit d'un problème avec le package SynoCommunity.

### Mise à niveau manuelle

Téléchargez la dernière version depuis notre site web.

Installez la mise à jour (.exe) ou extrayez (.zip) le contenu par-dessus votre installation existante et exécutez à nouveau Prowlarr comme d'habitude.

# Erreurs NGINX

Dans votre configuration Prowlarr, vous aurez besoin de cette ligne :

`proxy_set_header Host $host;`

Si vous avez une autre `proxy_set_header`, vous devez la remplacer par la ligne ci-dessus.

# Problèmes d'indexeur, d'application et de client de téléchargement

- Fondamentalement, Prowlarr doit pouvoir communiquer avec vos indexeurs.
- Si vous utilisez la synchronisation des applications, Prowlarr doit également pouvoir communiquer avec vos applications et les applications doivent pouvoir communiquer avec Prowlarr.
- Si vous avez un client de téléchargement dans Prowlarr pour les téléchargements manuels dans Prowlarr, Prowlarr devra pouvoir communiquer avec votre client de téléchargement.

> Notez que les journaux indiquant la requête de l'indexeur ID 0 : L'ID 0 est un point de terminaison de test générique qui nous permet de tester si \*Arr peut rappeler et se connecter à Prowlarr sans dépendre réellement d'un indexeur fonctionnel.
{.is-info}

Voici quelques causes courantes

## Impossible de déterminer la taille de la trame ou une trame corrompue a été reçue

`Impossible de déterminer la taille de la trame ou une trame corrompue a été reçue.`

Prowlarr a eu un problème de sécurité lors de la connexion au site.

Cela est généralement dû à :

- des problèmes DNS locaux - Essayez de changer de fournisseur DNS

## Délai de connexion dépassé

`La requête a expiré`

Prowlarr ne reçoit aucune réponse du client. [Consultez notre guide de dépannage général du réseau et des permissions](/permissions-and-networking)

Cela est généralement dû à :

- une configuration incorrecte ou l'utilisation d'un VPN
- une configuration incorrecte ou l'utilisation d'un proxy
- des problèmes DNS locaux - Essayez de changer de fournisseur DNS
- des problèmes IPv6 locaux - généralement IPv6 est activé, mais non fonctionnel
- l'utilisation de Privoxy

## Erreurs HTTP 404 de Sonarr

- Cela est généralement dû à l'utilisation d'une version en fin de vie (EOL) de Sonarr qui n'a pas les points de terminaison de l'API v3
- Prowlarr ne prend pas en charge Sonarr v2
- Prowlarr ne prend en charge que Sonarr v3

## Erreurs HTTP 400 de \*Arr

- Voir cette entrée de FAQ : [Prowlarr ne synchronisera pas l'indexeur X avec l'application](/prowlarr/faq#prowlarr-will-not-sync-x-indexer-to-app)

## 503 Service non disponible

- Cela est généralement dû à votre tracker qui vous bloque via Cloudflare et qui nécessite [FlareSolverr](https://github.com/FlareSolverr/FlareSolverr)

## Torrents invalides

- Essayez de télécharger le lien via l'URL et les variables utilisées par Prowlarr.
- Essayez de télécharger le torrent via Prowlarr en utilisant le lien de l'application qui a récupéré le fichier.
- Assurez-vous que votre cookie ou vos autres identifiants pour votre indexeur ne sont pas expirés et sont valides.
- Si le problème est causé par Prowlarr, veuillez signaler un bogue.

## Recherches d'indexeurs et de trackers

- [Recherches et indexeurs Lidarr](/lidarr/troubleshooting#searches-indexers-and-trackers)
- [Recherches et indexeurs Radarr](/radarr/troubleshooting#searches-indexers-and-trackers)
- [Recherches et indexeurs Readarr](/readarr/troubleshooting#searches-indexers-and-trackers)
- [Recherches et indexeurs Sonarr](/sonarr/troubleshooting#searches-indexers-and-trackers)
{.links-list}