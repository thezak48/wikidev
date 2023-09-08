---
title: Dépannage de Sonarr
description: 
published: true
date: 2023-07-24T19:54:54.368Z
tags: sonarr, dépannage
editor: markdown
dateCreated: 2021-06-20T19:13:01.108Z
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
- [Récupération après une mise à jour échouée](#récupération-après-une-mise-à-jour-échouée)
  - [Déterminer le problème](#déterminer-le-problème)
    - [Problème de migration](#problème-de-migration)
    - [Problème de permission](#problème-de-permission)
  - [Résoudre le problème](#résoudre-le-problème)
    - [Problèmes de permissions](#problèmes-de-permissions)
    - [Mise à niveau manuelle](#mise-à-niveau-manuelle)
- [Téléchargements et importation](#téléchargements-et-importation)
  - [Tester le client de téléchargement](#tester-le-client-de-téléchargement)
  - [Tester un téléchargement](#tester-un-téléchargement)
  - [Tester une importation](#tester-une-importation)
  - [Problèmes courants](#problèmes-courants)
    - [Un ou plusieurs épisodes attendus dans la version n'ont pas été importés ou sont manquants](#un-ou-plusieurs-épisodes-attendus-dans-la-version-nont-pas-été-importés-ou-sont-manquants)
    - [Utilisation de Sonarr v2](#utilisation-de-sonarr-v2)
    - [L'interface Web du client de téléchargement n'est pas activée](#linterface-web-du-client-de-téléchargement-nest-pas-activée)
    - [SSL utilisé et mal configuré](#ssl-utilisé-et-mal-configuré)
    - [Impossible de voir le partage sur Windows](#impossible-de-voir-le-partage-sur-windows)
    - [Les lecteurs réseau mappés ne sont pas fiables](#les-lecteurs-réseau-mappés-ne-sont-pas-fiables)
    - [Docker et utilisateur, groupe, propriété, permissions et chemins](#docker-et-utilisateur-groupe-propriété-permissions-et-chemins)
    - [Mapping de chemin distant](#mapping-de-chemin-distant)
      - [Montage distant ou synchronisation distante (Syncthing)](#montage-distant-ou-synchronisation-distant-syncthing)
    - [Permissions sur le dossier de la bibliothèque](#permissions-sur-le-dossier-de-la-bibliothèque)
    - [Permissions sur le dossier de téléchargements](#permissions-sur-le-dossier-de-téléchargements)
    - [Le dossier de téléchargement et le dossier de la bibliothèque ne sont pas différents](#le-dossier-de-téléchargement-et-le-dossier-de-la-bibliothèque-ne-sont-pas-différents)
    - [Catégorie incorrecte](#catégorie-incorrecte)
    - [Torrents compressés](#torrents-compressés)
    - [Téléchargements répétés](#téléchargements-répétés)
    - [Téléchargement Usenet manqué lors de l'importation](#téléchargement-usenet-manqué-lors-de-limportation)
    - [Le client de téléchargement efface les éléments](#le-client-de-téléchargement-efface-les-éléments)
    - [Le téléchargement ne peut pas être associé à un élément de la bibliothèque](#le-téléchargement-ne-peut-pas-être-associé-à-un-élément-de-la-bibliothèque)
      - [Série correspondante trouvée via l'historique de capture, mais la série a été associée par ID de série. L'importation automatique n'est pas possible](#série-correspondante-trouvée-via-lhistorique-de-capture-mais-la-série-a-été-associée-par-id-de-série-limportation-automatique-nest-pas-possible)
    - [Le nom de l'épisode est TBA](#le-nom-de-lépisode-est-tba)
    - [Temps d'attente de la connexion dépassé](#temps-dattente-de-la-connexion-dépassé)
  - [Problème non répertorié](#problème-non-répertorié)
- [Recherches, indexeurs et trackers](#recherches-indexeurs-et-trackers)
  - [Augmenter le niveau de journalisation](#augmenter-le-niveau-de-journalisation)
  - [Tester un indexeur ou un tracker](#tester-un-indexeur-ou-un-tracker)
  - [Tester une recherche](#tester-une-recherche)
  - [Problèmes courants](#problèmes-courants-1)
    - [Indexeurs non recherchés](#indexeurs-non-recherchés)
    - [Versions mal nommées](#versions-mal-nommées)
    - [Le tracker nécessite des capacités de recherche brute](#le-tracker-nécessite-des-capacités-de-recherche-brute)
    - [La série a besoin d'un alias](#la-série-a-besoin-dun-alias)
    - [La série a besoin d'une correspondance XEM](#la-série-a-besoin-dune-correspondance-xem)
    - [Mauvais type de série](#mauvais-type-de-série)
      - [Quotidien](#quotidien)
      - [Standard](#standard)
      - [Anime](#anime)
    - [Le média n'est pas surveillé](#le-média-nest-pas-surveillé)
    - [Requête réussie - Aucun résultat retourné](#requête-réussie---aucun-résultat-retourné)
    - [Catégories incorrectes](#catégories-incorrectes)
    - [Résultats incorrects](#résultats-incorrects)
    - [Résultats manquants](#résultats-manquants)
    - [Validation du certificat](#validation-du-certificat)
    - [Atteinte des limites de taux](#atteinte-des-limites-de-taux)
    - [Interdiction IP](#interdiction-ip)
    - [Utilisation de l'endpoint /all de Jackett](#utilisation-de-lendpoint-all-de-jackett)
    - [Utilisation de NZBHydra2 comme entrée unique](#utilisation-de-nzbhydra2-comme-entrée-unique)
    - [Indexeur non recherché](#indexeur-non-recherché)
    - [Recherche manuelle de Jackett trouvant plus de résultats](#recherche-manuelle-de-jackett-trouvant-plus-de-résultats)
    - [Les profils de version ne sont pas respectés](#les-profils-de-version-ne-sont-pas-respectés)
    - [Problème non répertorié](#problème-non-répertorié-1)
  - [Erreurs](#erreurs)
    - [La connexion sous-jacente a été fermée : une erreur inattendue s'est produite lors de l'envoi](#la-connexion-sous-jacente-a-été-fermée-une-erreur-inattendue-sest-produite-lors-de-lenvoi)
    - [La demande a expiré](#la-demande-a-expiré)
    - [Problème non répertorié](#problème-non-répertorié-2)

# Demander de l'aide

Vous avez besoin d'aide ? C'est normal, tout le monde a besoin d'aide parfois. Vous pouvez obtenir de l'aide en temps réel via le chat sur

- [<i class="fab fa-discord"></i>&emsp;Discord *Discord officiel de Sonarr*](https://discord.sonarr.tv/)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Subreddit officiel de Sonarr*](https://reddit.com/r/sonarr)
{.links-list}

Mais avant d'y aller et de poster, assurez-vous que votre demande d'aide est la meilleure possible. Décrivez clairement le problème et décrivez brièvement votre configuration, y compris des éléments tels que votre système d'exploitation/distribution, la version de .net/Mono, la version de Sonarr, le client de téléchargement et sa version. **Si vous utilisez [Docker](https://www.docker.com/), veuillez suivre d'abord le [Guide Docker](/docker-guide) car cela résoudra les problèmes courants et fréquents de chemin/permissions. Sinon, veuillez avoir un [docker compose](/docker-guide#docker-compose) à portée de main. [Comment générer un Docker Compose](https://trash-guides.info/compose)** Parlez-nous de ce que vous avez déjà essayé, de ce que vous avez examiné. Utilisez la section [Journalisation et fichiers journaux](#journalisation-et-fichiers-journaux) pour augmenter le niveau de journalisation, recréer le problème, collez le contexte pertinent sur un service de partage de code et incluez un lien vers celui-ci dans votre message. Vous pouvez même inclure des captures d'écran pour mettre en évidence le problème.

Plus nous en savons, plus il est facile de vous aider.

# Journalisation et fichiers journaux

Il est probablement utile de consulter également les problèmes courants de dépannage :
- [Problèmes courants de téléchargements et d'importation](#problèmes-courants)
- [Problèmes courants de recherches, indexeurs et trackers](#problèmes-courants-1)
{.links-list}

Si on vous demande des journaux de débogage, vos journaux contiendront `debug` et si on vous demande des journaux de trace, vos journaux contiendront `trace`. Si les journaux que vous fournissez ne contiennent ni l'un ni l'autre, ce ne sont pas les journaux demandés.

- Évitez de partager l'intégralité du fichier journal à moins qu'on ne vous le demande.
- N'envoyez pas les journaux directement sur Discord ou ne les collez pas sous forme de murs de texte, sauf si on vous le demande.
- Ne partagez pas les journaux en tant que pièce jointe, archive zip ou autre que du texte partagé via les services indiqués ci-dessous.

Pour fournir de bons et utiles journaux à partager :

> Assurez-vous qu'une tâche de spam N'EST PAS en cours d'exécution, comme une actualisation RSS
{.is-warning}

1. [Augmentez le niveau de journalisation à Trace (Paramètres => Général => Niveau de journalisation ou modifiez le fichier de configuration)](#journaux-de-tracedébogage)
2. [Effacez les journaux (Système => Journaux => Effacer les journaux ou supprimez tous les journaux du dossier des journaux)](#effacement-des-journaux)
3. Reproduisez le problème (Refaites ce qui pose problème)
4. [Ouvrez le fichier journal de trace (sonarr.trace.txt) via l'interface utilisateur ou le fichier journal](#emplacement-des-journaux-standard) sur le système de fichiers et trouvez le contexte pertinent
5. Copiez une grande partie avant le problème, le problème lui-même et une grande partie après le problème.
6. Utilisez [Gist](https://gist.github.com/), [0bin (**Assurez-vous de désactiver la colorisation**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Pastebin d'Ubuntu](https://pastebin.ubuntu.com/) ou des sites similaires - à l'exception de ceux mentionnés ci-dessous - pour partager les journaux copiés ci-dessus

**Avertissements :**
- **N'utilisez pas [pastebin.com](https://pastebin.com) car leurs filtres ont tendance à bloquer les journaux.
- N'utilisez pas [pastebin.pl](https://pastebin.pl) car leur site n'est souvent pas accessible.
- N'utilisez pas [JustPasteIt](https://justpaste.it/) car leur site ne facilite pas l'examen des journaux.
- N'envoyez pas votre journal en tant que fichier
- N'envoyez pas et ne partagez pas vos journaux via Google Drive, Dropbox ou tout autre site non mentionné ci-dessus.
- N'archivez pas (zip, tar (tarball), 7zip, etc.) vos journaux.
- Ne partagez pas de sortie de console, de sortie de conteneur Docker ou autre chose que les journaux d'application spécifiés

**Note importante :**
- Lors de l'utilisation de [0bin](https://0bin.net/), assurez-vous de désactiver la colorisation et de ne pas brûler après lecture.

- Alternativement, si vous recherchez une entrée spécifique dans un ancien fichier journal mais que vous n'êtes pas sûr duquel, vous pouvez utiliser N++. Vous pouvez utiliser la fonction "Rechercher dans les fichiers" de Notepad++ pour rechercher les anciens fichiers journaux selon vos besoins.
- **Unix uniquement :** Alternativement, si vous recherchez une entrée spécifique dans un ancien fichier journal mais que vous n'êtes pas sûr duquel, vous pouvez utiliser grep. Par exemple, si vous souhaitez trouver des informations sur le film/émission/livre/chanson/indexeur "Shooter", vous pouvez exécuter la commande suivante `grep -inr -C 100 -e 'Shooter' /chemin/vers/les/journaux/*.trace*.txt` Si votre [Répertoire Appdata](/sonarr/appdata-directory) se trouve dans votre dossier personnel, vous exécuteriez : `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Les indicateurs ont les fonctions suivantes
    * -i : ignorer la casse
    * -n : afficher le numéro de ligne
    * -r : vérifier récursivement tous les fichiers dans le chemin
    * -C : fournir le nombre de lignes avant et après la ligne où il est trouvé
    * -e : le motif à rechercher

```

## Emplacement des journaux standard

Les fichiers journaux se trouvent dans le [Répertoire Appdata](/sonarr/appdata-directory) de Sonarr, à l'intérieur du dossier logs/. Vous pouvez également accéder aux fichiers journaux depuis l'interface utilisateur à Système => Journaux => Fichiers.

> Remarque : Le tableau des journaux ("Événements") dans l'interface utilisateur n'est pas identique aux fichiers journaux et n'est pas aussi utile. Si on vous demande des journaux, veuillez copier/coller à partir des fichiers journaux et non de la table.
{.is-info}

## Emplacement des journaux de mise à jour

Les fichiers journaux de mise à jour se trouvent dans le [Répertoire Appdata](/sonarr/appdata-directory) de Sonarr, à l'intérieur du dossier UpdateLogs/.

## Partage des journaux

Les journaux peuvent être longs et difficiles à lire dans un message sur un forum ou sur Reddit, et ils sont encombrants sur Discord, veuillez donc utiliser [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) ou tout autre site similaire de partage de code. Le fichier entier n'est généralement pas nécessaire, seulement une bonne quantité de contexte avant et après le problème/erreur. N'oubliez pas d'attendre que des tâches de spam comme une synchronisation RSS ou une actualisation de la bibliothèque se terminent.

## Journaux de trace/débogage

Vous pouvez modifier le niveau de journalisation dans Paramètres => Général => Journalisation. Sonarr n'a pas besoin d'être redémarré pour que le changement prenne effet. Ce changement n'affecte que les fichiers journaux, pas la base de données de journalisation. Les derniers fichiers journaux de débogage/trace sont nommés respectivement `sonarr.debug.txt` et `sonarr.trace.txt`.

Si vous ne pouvez pas accéder à l'interface utilisateur pour définir le niveau de journalisation, vous pouvez le faire en modifiant config.xml dans le répertoire AppData en définissant la valeur LogLevel sur Debug ou Trace au lieu de Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Effacement des journaux

Vous pouvez effacer les fichiers journaux et la base de données de journaux directement depuis l'interface utilisateur, sous Système => Journaux => Fichiers et Système => Journaux => Supprimer (icône de corbeille)

# Fichiers journaux multiples

Sonarr utilise des fichiers journaux roulants limités à 1 Mo chacun. Le fichier journal actuel est toujours `sonarr.txt`, pour les autres fichiers `sonarr.0.txt` est le plus récent (plus le nombre est élevé, plus il est ancien). Ce fichier journal contient les entrées `fatal`, `error`, `warn` et `info`.

Lorsque le niveau de journalisation de débogage est activé, des fichiers journaux roulants supplémentaires `sonarr.debug.txt` seront présents. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info` et `debug`. Ils couvrent généralement une période de 40 heures.

Lorsque le niveau de journalisation de trace est activé, des fichiers journaux roulants supplémentaires `sonarr.trace.txt` seront présents. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info`, `debug` et `trace`. En raison de la verbosité de la trace, ils ne couvrent que quelques heures au maximum.

# Récupération après une mise à jour échouée

Nous faisons tout notre possible pour éviter les problèmes lors de la mise à niveau, mais s'ils se produisent, voici les étapes à suivre pour récupérer votre installation.

## Déterminer le problème

Le meilleur endroit où chercher lorsque l'application ne démarre pas après une mise à jour est de consulter les [journaux de mise à jour](#emplacement-des-journaux-de-mise-à-jour) et de voir si la mise à jour s'est terminée avec succès. Si ceux-ci ne présentent aucun problème, la prochaine étape consiste à consulter vos fichiers journaux d'application habituels, avant de tenter de redémarrer, utilisez [Journalisation](/sonarr/settings#journalisation) et [Fichiers journaux](/sonarr/system#fichiers-journaux) pour les trouver et augmenter le niveau de journalisation.

### Problème de migration

- Les erreurs de migration ne seront pas identiques, mais voici un exemple :

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Problème de permission

- Les problèmes de permissions sont dus à l'incapacité de l'application à accéder aux dossiers temporaires pertinents et/ou au dossier binaire de l'application. Corrigez les permissions afin que l'utilisateur/le groupe sous lequel s'exécute l'application ait les autorisations appropriées.

- Les utilisateurs de Synology peuvent rencontrer le bug Synology `Access to the path '/proc/{some number}/maps is denied`

- Les utilisateurs de Synology peuvent également rencontrer des problèmes d'espace dans `/tmp` sur certains NAS. Vous devrez spécifier un chemin `/tmp` différent pour l'application. Consultez la communauté SynoCommunity ou d'autres canaux de support Synology pour obtenir de l'aide à ce sujet.

## Résolution du problème

En cas de problème de migration, il n'y a pas grand-chose que vous puissiez faire immédiatement. Si le problème vous concerne spécifiquement (ou s'il n'y a pas encore de publications à ce sujet), veuillez créer une publication sur [notre subreddit](https://reddit.com/r/sonarr) ou passer sur notre [discord](https://discord.sonarr.tv/). Si d'autres personnes rencontrent le même problème, soyez assuré que nous travaillons dessus.

> Assurez-vous de ne pas avoir essayé d'utiliser une base de données de `develop` sur la version stable. Il est déconseillé de passer d'une branche à l'autre.{.is-info}

### Problèmes de permissions

- Corrigez les permissions pour vous assurer que l'utilisateur/groupe sous lequel l'application s'exécute peut accéder (lecture et écriture) à la fois à `/tmp` et au répertoire d'installation de l'application.

- Pour les utilisateurs de Synology qui rencontrent des problèmes avec `/proc/###/maps` qui arrêtent Sonarr ou les autres applications \*Arr, la mise à jour devrait résoudre ce problème. Il s'agit d'un problème avec le package SynoCommunity.

### Mise à niveau manuelle

Téléchargez la dernière version depuis notre site web.

Installez la mise à jour (.exe) ou extrayez (.zip) le contenu par-dessus votre installation existante et exécutez Sonarr comme d'habitude.

# Téléchargements et importation

Le téléchargement et l'importation sont les étapes où *la plupart* des utilisateurs rencontrent des problèmes. D'un point de vue général, Sonarr doit être en mesure de communiquer avec votre client de téléchargement et d'avoir accès aux fichiers qu'il télécharge. Il existe une grande variété de clients de téléchargement pris en charge et une encore *plus grande* variété de configurations. Cela signifie qu'il existe quelques configurations *courantes*, mais il n'y a pas une seule configuration *correcte* et la configuration de chacun peut être légèrement différente.

> **La première étape consiste à augmenter le niveau de journalisation à Trace, consultez [Logging and Log Files](#logging-and-log-files) pour plus de détails sur l'ajustement de la journalisation et la recherche dans les journaux. Vous reproduirez ensuite le problème et utiliserez les journaux de niveau trace de cette période pour examiner le problème.**
> Si quelqu'un vous aide, mettez le contexte avant/après dans un [pastebin](https://0bin.net), [Gist](https://gist.com) ou un site similaire pour le lui montrer.
> Il n'est pas nécessaire de fournir l'intégralité du fichier et il ne doit pas se limiter à l'erreur. Vous devez également reproduire le problème lorsque des tâches qui encombrent le fichier journal ne sont pas en cours d'exécution.
{.is-danger}

Lorsque vous demandez de l'aide, assurez-vous de lire [demander de l'aide](#asking-for-help) afin de pouvoir nous fournir les détails dont nous aurons besoin.

## Test du client de téléchargement

Assurez-vous que votre client(s) de téléchargement est en cours d'exécution. Commencez par tester le client de téléchargement, s'il ne fonctionne pas, vous pourrez voir les détails dans les journaux de niveau trace. Vous devriez trouver une URL que vous pouvez entrer dans votre navigateur pour voir si cela fonctionne. Il peut s'agir d'un problème de connexion, ce qui pourrait indiquer une mauvaise adresse IP, un nom d'hôte incorrect, un port incorrect ou même un pare-feu bloquant l'accès. Cela peut être évident, comme un problème d'authentification où vous avez mal saisi le nom d'utilisateur, le mot de passe ou la clé API.

## Test d'un téléchargement

Maintenant, nous allons essayer un téléchargement, choisissez un épisode d'une série et effectuez une recherche manuelle. Choisissez l'un de ces fichiers et essayez de le télécharger. Est-il envoyé au client de téléchargement ? Apparaît-il dans la catégorie correcte ? Apparaît-il dans l'activité ? Apparaît-il dans les journaux de niveau trace pendant les tâches **Vérifier les téléchargements terminés** (tâches Rafraîchir les téléchargements surveillés et Traiter les téléchargements surveillés) qui s'exécutent environ toutes les minutes ? Est-il correctement analysé pendant cette tâche ? Le téléchargement en attente a-t-il un nom raisonnable ? Étant donné que les recherches se font par ID sur certains indexeurs/trackers, il peut mettre en file d'attente un téléchargement avec un nom qu'il ne peut pas reconnaître.

## Test d'une importation

Les problèmes d'importation se manifestent presque toujours par un élément dans l'activité avec une icône orange sur laquelle vous pouvez survoler pour voir l'erreur. S'ils n'apparaissent pas dans l'activité, c'est le problème sur lequel vous devez vous concentrer en premier, alors revenez en arrière et résolvez-le. La plupart des erreurs d'importation sont des problèmes de *permissions*, n'oubliez pas que Sonarr doit pouvoir lire et écrire dans le dossier de téléchargement. Parfois, les permissions dans le dossier de la bibliothèque peuvent également être en cause, alors assurez-vous de vérifier les deux.

Des problèmes de chemin incorrect sont également possibles, bien que moins courants dans les configurations normales. La clé pour comprendre les problèmes de chemin est de savoir que récupère le chemin du téléchargement *à partir* du client de téléchargement, via son API. Cela pose problème dans des cas d'utilisation plus spécifiques, comme lorsque le client de téléchargement s'exécute sur un système différent (voire même un système d'exploitation différent\!). Cela peut également se produire dans une configuration Docker, lorsque les volumes ne sont pas bien configurés. Une correspondance de chemin distant est une bonne solution lorsque vous n'avez pas le contrôle, comme dans une configuration de seedbox. Dans une configuration Docker, corriger les chemins est une meilleure option.

## Problèmes courants

Voici quelques problèmes courants.

### Un ou plusieurs épisodes attendus dans la version n'ont pas été importés ou sont manquants

- Si tous les épisodes ont été importés, la cause la plus courante est qu'un pack de saison a été téléchargé, mais ne contient pas tous les épisodes de la saison. Cliquez sur `X` pour supprimer et ignorer la version.
- Pour tous les autres problèmes, un ou plusieurs épisodes n'ont pas pu être importés. Vérifiez les informations dans l'interface utilisateur et les autres problèmes courants.

### Utilisation de Sonarr v2

Sonarr v2 a atteint sa fin de vie et n'est plus pris en charge depuis 3/2021. Il n'est pas compatible avec qBittorrent v4.3.0 ou une version ultérieure. Mettez à niveau vers Sonarr v3.

### L'interface Web du client de téléchargement n'est pas activée

Sonarr communique avec votre client de téléchargement via son API et y accède via l'interface web du client. Vous devez vous assurer que l'interface web du client est activée et que le port utilisé ne entre pas en conflit avec d'autres ports utilisés par d'autres clients ou par votre système.

### SSL utilisé et mal configuré

Assurez-vous que le chiffrement SSL n'est pas activé si vous utilisez à la fois votre instance et votre client de téléchargement sur un réseau local. Consultez [l'entrée FAQ sur les certificats invalides et autres problèmes HTTPS ou SSL](/sonarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) pour plus d'informations.

### Impossible de voir le partage sur Windows

L'utilisateur par défaut pour un service Windows est `LocalService`, qui n'a généralement pas accès à vos partages. Modifiez le service et configurez-le pour qu'il s'exécute en tant qu'utilisateur, consultez l'entrée FAQ [pourquoi je ne peux pas voir mes fichiers sur un serveur distant](/sonarr/faq#why-cant-i-see-my-files-on-a-remote-server) pour plus de détails.

### Les lecteurs réseau mappés ne sont pas fiables

Bien que les lecteurs réseau mappés comme `X:\` soient pratiques, ils ne sont pas aussi fiables que les chemins UNC comme `\\serveur\partage` et ils ne sont pas disponibles avant la connexion. Configurez votre client de téléchargement et vos clients de téléchargement de manière à utiliser les chemins UNC si nécessaire. Si votre bibliothèque se trouve sur un partage, assurez-vous que vos dossiers racines utilisent des chemins UNC. Si votre client de téléchargement envoie vers un partage, c'est là que vous devrez configurer des chemins UNC, car récupère le chemin de téléchargement à partir du client de téléchargement. Il est possible de conserver vos lecteurs réseau mappés pour votre propre utilisation, mais ne les utilisez pas pour l'automatisation.

### Docker et utilisateur, groupe, propriété, permissions et chemins

Docker ajoute une autre couche de complexité qui est facile à mal configurer, mais qui peut quand même fonctionner, mais avec divers problèmes. Au lieu de les passer en revue ici, lisez cet article du wiki [pour ces logiciels d'automatisation et Docker](/docker-guide) qui traite de l'utilisateur, du groupe, de la propriété, des permissions et des chemins. Il n'est pas spécifique à un système Docker particulier, mais il passe en revue les choses de manière générale afin que vous puissiez les mettre en œuvre dans votre propre environnement.

### Correspondance de chemin distant

Si vous avez Sonarr dans Docker et le client de téléchargement en dehors de Docker (ou vice versa) ou si les programmes sont sur différents serveurs, vous devrez peut-être utiliser une correspondance de chemin distant.

Les journaux ressembleront à ceci

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/torrents/tv/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Ainsi, `/volume3/data` n'existe pas dans le conteneur de Sonarr ou n'est pas accessible.

- [Paramètres => Clients de téléchargement => Correspondances de chemin distant](/sonarr/settings#remote-path-mappings)
- Une correspondance de chemin distant est utilisée lorsque votre client de téléchargement signale un chemin pour les données terminées, soit sur un autre serveur, soit d'une manière que \*Arr n'adresse pas ce dossier.
- En général, une correspondance de chemin distant n'est nécessaire que si votre client de téléchargement est sous Linux lorsque \*Arr est sous Windows, ou vice versa. Une correspondance de chemin distant peut également être nécessaire si vous mélangez des clients Docker et natifs ou si vous utilisez un serveur distant.
- Une correspondance de chemin distant est une recherche/remplacement SIMPLE (où elle trouve la valeur DISTANTE, la remplace par la valeur LOCALE pour l'hôte spécifié).
- Si le message d'erreur concernant un mauvais chemin ne contient pas la valeur REMPLACÉE, alors la correspondance de chemin ne fonctionne pas comme vous le souhaitez. La solution typique consiste à ajouter et supprimer la correspondance.
- [Consultez le tutoriel de TRaSH pour des informations supplémentaires sur la correspondance de chemin distant](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Si à la fois \*Arr et votre client de téléchargement sont des conteneurs Docker, il est rare qu'une correspondance de chemin distant soit nécessaire. Il est recommandé de [revoir le guide Docker](/docker-guide) et/ou de [suivre le tutoriel de TRaSH](https://trash-guides.info/hardlinks)
{.is-info}

#### Montage distant ou synchronisation distante (Syncthing)

- Vous devez le synchroniser pendant toute la durée du téléchargement. Et vous devez vous assurer que la destination de synchronisation locale peut être liée en dur lorsque \*Arr importe, ce qui signifie qu'elle doit être sur le même système de fichiers et y ressembler.
  - Synchronisez dans un dossier inférieur et commun qui contient à la fois les fichiers incomplets et les fichiers complets.
  - Synchronisez vers un emplacement qui se trouve sur le même système de fichiers localement que votre bibliothèque et qui y ressemble (les conteneurs Docker et les partages réseau facilitent la mauvaise configuration).
  - Vous voulez synchroniser les fichiers incomplets et complets afin que lorsque le client torrent effectue le déplacement, cela soit reflété localement et que tous les fichiers soient déjà "là" (même s'ils sont toujours en cours de téléchargement). Ensuite, vous voulez utiliser des liens durs, car même s'ils sont importés avant d'être terminés, ils finiront quand même.
  - De cette façon, pendant toute la durée du téléchargement, il est synchronisé, puis le client torrent déplace vers le sous-dossier tv et la synchronisation le reflète. De cette façon, les téléchargements sont presque terminés lorsqu'ils sont déclarés terminés. Et même s'ils ne sont pas totalement terminés, le fait que le lien dur soit possible signifie que c'est quand même acceptable.
  - (Facultatif - si applicable et/ou requis (par exemple, client usenet distant)) Configurez un script personnalisé à exécuter lors de l'importation/téléchargement/mise à niveau pour supprimer le fichier distant.
- Alternativement, un montage distant plutôt qu'une configuration de synchronisation distante est beaucoup moins compliqué à configurer, mais généralement plus lent.
  - Montez votre stockage distant avec sshfs ou un autre protocole de système de fichiers réseau.
  - Assurez-vous que l'utilisateur et le groupe sous lesquels \*Arr est configuré pour s'exécuter ont un accès en lecture ou en écriture.
  - Configurez une correspondance de chemin distant pour trouver le chemin DISTANT et le remplacer par l'équivalent LOCAL

### Permissions sur le dossier de la bibliothèque

Les journaux ressembleront à ceci

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/tv/The Orville/Season 03/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

N'oubliez pas de vérifier les permissions et la propriété de la *destination*. Il est facile de se concentrer sur la propriété et les permissions du téléchargement et c'est *généralement* la cause des problèmes liés aux permissions, mais cela *pourrait* être aussi la destination. Vérifiez que le(s) dossier(s) de destination existe(nt). Vérifiez qu'un fichier de destination n'existe pas déjà ou ne peut pas être supprimé ou déplacé vers la corbeille. Vérifiez que la propriété et les permissions permettent de copier, de créer un lien dur ou de déplacer le fichier téléchargé. L'utilisateur ou le groupe qui s'exécute doit pouvoir lire et écrire dans le dossier racine.

- Pour les utilisateurs de Windows, cela peut être dû à l'exécution en tant que service :
  - le service Windows s'exécute sous le compte 'Local Service', par défaut ce compte n'a pas les permissions pour accéder au répertoire personnel de votre utilisateur à moins que les permissions n'aient été attribuées manuellement. Cela est particulièrement pertinent lorsque vous utilisez des clients de téléchargement configurés pour télécharger dans votre répertoire personnel.
  - 'Local Service' a également généralement des permissions très limitées. Il est donc conseillé d'installer l'application en tant qu'application de la barre d'état système si l'utilisateur peut rester connecté. L'option pour le faire est fournie lors de l'installation. Consultez la FAQ pour savoir comment passer d'un service à une application de la barre d'état système.

- Pour les utilisateurs de Synology, consultez [l'article sur les permissions de SynoCommunity pour leurs packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Non-Windows : Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
- Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.

### Permissions sur le dossier de téléchargement

Vous verrez une erreur similaire à celle-ci

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES.1/a4187f6c3c4445f98e85da52b83c84e8.mkv. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

ou

```none
2022-02-03 10:40:41.8|Warn|Sabnzbd|[Resident.Alien.S02E02.720p.WEB.H264-CAKES] Error occurred while trying to delete data from '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES/'.
 
[v3.0.6.1342] System.UnauthorizedAccessException: Access to the path '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES' is denied.
```

N'oubliez pas de vérifier les permissions et la propriété de la *source*. Il est facile de se concentrer sur la propriété et les permissions de la destination et c'est une *cause possible* de problèmes liés aux permissions, mais c'est généralement la source. Vérifiez que le(s) dossier(s) source existe(nt). Vérifiez que la propriété et les permissions permettent de copier, de créer un lien dur ou de copier+supprimer/déplacer le fichier. L'utilisateur ou le groupe sous lequel Sonarr s'exécute doit pouvoir lire et écrire les fichiers de téléchargement.

- Pour les utilisateurs de Windows, cela peut être dû à l'exécution en tant que service :
  - le service Windows s'exécute sous le compte 'Local Service', par défaut ce compte n'a pas les permissions pour accéder au répertoire personnel de votre utilisateur à moins que les permissions n'aient été attribuées manuellement. Cela est particulièrement pertinent lorsque vous utilisez des clients de téléchargement configurés pour télécharger dans votre répertoire personnel.
  - 'Local Service' a également généralement des permissions très limitées. Il est donc conseillé d'installer l'application en tant qu'application de la barre d'état système si l'utilisateur peut rester connecté. L'option pour le faire est fournie lors de l'installation. Consultez la FAQ pour savoir comment passer d'un service à une application de la barre d'état système.

- Pour les utilisateurs de Synology, consultez [l'article sur les permissions de SynoCommunity pour leurs packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Non-Windows : Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
- Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.

### Dossier de téléchargement et dossier de la bibliothèque ne sont pas des dossiers différents

- Le client de téléchargement doit télécharger dans un dossier accessible par \*Arr et qui n'est pas votre dossier racine/bibliothèque ; il doit importer à partir de ce dossier de téléchargement séparé dans votre dossier Bibliothèque.
- Vous ne devez jamais télécharger directement dans votre dossier racine. Vous ne devez pas non plus utiliser votre dossier racine comme dossier complet ou dossier incomplet du client de téléchargement.
- [**Cela provoquera également une vérification de l'état du système**](/sonarr/system#downloading-into-root-folder)
- Dans l'application, un dossier racine est défini comme le dossier de bibliothèque multimédia configuré. Ce n'est pas le dossier racine d'un montage. Votre client de téléchargement a un dossier incomplet ou complet (ou déplace les téléchargements terminés) dans votre dossier racine (bibliothèque). Cela cause fréquemment des problèmes et n'est pas recommandé. Pour résoudre ce problème, modifiez votre client de téléchargement afin qu'il ne place pas les téléchargements dans votre dossier racine. Notez que 'placer' inclut également si la catégorie de votre client de téléchargement est définie sur votre dossier racine ou si NZBGet/SABnzbd ont activé le tri et trient vers votre dossier racine. Veuillez noter que cette vérification examine tous les dossiers racines définis/configurés ajoutés, pas seulement les dossiers racines actuellement utilisés. En d'autres termes, le dossier dans lequel votre client de téléchargement télécharge ou déplace les téléchargements terminés ne doit pas être le même dossier que celui que vous avez configuré comme dossier de destination multimédia racine/bibliothèque/final dans l'application \*Arr.
- Les dossiers racines configurés (alias dossiers de bibliothèque) peuvent être trouvés dans [Paramètres => Gestion des médias => Dossiers racines](/sonarr/settings/#root-folders)
- Un exemple est si vos téléchargements vont dans `\data\downloads`, alors vous avez un dossier racine défini comme `\data\downloads`.
- Il est recommandé d'utiliser des chemins comme `\data\media\` pour votre dossier racine/bibliothèque et `\data\downloads\` pour vos téléchargements.

> Votre dossier de téléchargement et votre dossier racine/bibliothèque DOIVENT être séparés
{.is-warning}

### Catégorie incorrecte

Sonarr doit être configuré pour utiliser une catégorie afin qu'il ne tente de traiter que ses propres téléchargements. Il est rare qu'un torrent soumis soit ajouté sans la catégorie correcte, mais cela peut arriver. Si vous ajoutez manuellement des torrents et que vous souhaitez les traiter, ils doivent avoir la catégorie correcte. Elle peut être définie à tout moment, car Sonarr tente de traiter les téléchargements toutes les minutes.

### Torrents compressés

Les journaux indiqueront des erreurs telles que

```none
Aucun fichier éligible à l'importation n'a été trouvé
```

Si votre torrent est compressé dans des fichiers `.rar`, vous devrez configurer l'extraction. Nous recommandons [Unpackerr](https://github.com/unpackerr/unpackerr) car il effectue le déballage correctement : il empêche les imports partiels corrompus et nettoie les fichiers déballés après l'importation.

L'erreur peut également être observée s'il n'y a aucun fichier multimédia valide dans le dossier.

### Téléchargements répétés

Il existe plusieurs causes de téléchargements répétés, mais l'une d'entre elles est liée à la restriction de l'indexeur dans les profils de publication. Étant donné que l'indexeur n'est pas stocké avec les données, tous les scores de `mot préféré` sont *nuls* pour les médias de votre bibliothèque, mais pendant la recherche "RSS" et la recherche, ils seront appliqués. De même pour les restrictions de `doit contenir` ou `ne doit pas contenir`, elles s'appliquent uniquement à cet indexeur ; tout le reste est autorisé. Cela vous fait entrer dans une boucle où vous téléchargez les éléments encore et encore parce qu'ils ressemblent à une mise à niveau, puis ne le sont pas, puis réapparaissent et ressemblent à une mise à niveau, puis ne le sont pas. Ne restreignez pas votre profil de publication à un indexeur.

Cela peut également être dû au fait que le téléchargement n'est jamais importé réellement, puis est manquant de la file d'attente, de sorte qu'un nouveau téléchargement est constamment récupéré et jamais importé. Veuillez consulter les autres problèmes courants et les étapes de dépannage pour cela.

### Échec de l'importation du téléchargement Usenet

Sonarr ne regarde que les 60 téléchargements les plus récents dans SABnzbd et NZBGet, donc si vous gardez votre historique, cela signifie que pendant les files d'attente importantes avec des problèmes d'importation, les téléchargements peuvent être manqués silencieusement et non importés. La meilleure façon d'éviter cela est de garder votre historique clair, de sorte que tous les éléments qui apparaissent encore nécessitent une enquête. Vous pouvez y parvenir en activant la suppression dans les gestionnaires de téléchargement terminés et échoués. Dans NZBGet, cela déplacera les éléments vers l'historique *caché*, ce qui est génial. Malheureusement, SABnzbd n'a pas de fonctionnalité similaire. Le mieux que vous puissiez réaliser est d'utiliser le dossier de sauvegarde nzb.

### Le client de téléchargement supprime les éléments

Le client de téléchargement ne doit pas être responsable de la suppression des téléchargements. Les clients Usenet doivent être configurés pour ne pas supprimer les téléchargements de l'historique. Les clients torrent doivent être configurés pour ne pas supprimer les torrents lorsqu'ils ont fini de partager (les mettre en pause ou les arrêter à la place). C'est parce que Sonarr communique avec le client de téléchargement pour savoir quoi importer, donc s'ils sont *supprimés*, il n'y a rien à importer, même s'il y a un dossier rempli de fichiers.

Pour SABnzbd, cela est géré avec le paramètre de rétention de l'historique.

### Le téléchargement ne peut pas être associé à un élément de bibliothèque

Pour diverses raisons, les publications ne peuvent pas être analysées une fois récupérées et envoyées au client de téléchargement. L'activité => Options => Afficher les inconnus (ceci est maintenant activé par défaut dans les versions récentes) affiche tous les éléments non ignorés / déjà importés dans la catégorie du client de téléchargement de \*Arr. Ils devront généralement être mappés et importés manuellement.

Cela peut également se produire si vous avez une publication dans votre client de téléchargement mais que cet élément multimédia (film/épisode/livre/chanson) n'existe pas dans l'application.

#### Correspondance de séries trouvée via l'historique de récupération, mais la série a été associée par ID de série. L'importation automatique n'est pas possible

- Cette erreur d'importation est similaire à l'erreur de correspondance ci-dessus.
- Sonarr a récupéré la publication en raison de votre indexeur ou tracker signalant que la publication avait l'ID TVDb (ou IMDb) d'une série que vous vouliez.
- La série du fichier téléchargé ne correspond pas à l'ID signalé, donc Sonarr n'importera pas le fichier.
- Selon le titre de la série et le nom de la publication - en supposant que la publication est correcte pour l'ID de série auquel elle est associée - Sonarr aura probablement besoin d'un alias ajouté, [cette entrée FAQ contient plus d'informations](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x) sur la demande d'ajout d'un alias.
- Alternativement, la publication est mal étiquetée et ne correspond pas à l'ID de série qui a été signalé. Cela doit être signalé à votre indexeur afin qu'il puisse prendre des mesures correctives.
- Pour gérer cette erreur :
  1. Vérifiez la série du fichier
  1. Demandez un alias (si applicable)
  1. Importez manuellement le fichier (icône humaine à droite) depuis l'activité => File d'attente OU cliquez sur `X` dans la file d'attente pour ignorer la publication dans votre client et éventuellement la mettre sur liste noire / éventuellement la supprimer du client

### Le nom de l'épisode est TBA

Sur TVDB, lorsque les noms des épisodes sont inconnus, ils sont intitulés TBA et il y a un cache de 24 heures sur l'API. En général, les modifications apportées au site TVDB mettent de 24 à 48 heures pour atteindre Sonarr en raison du cache de TVDB, du cache de Skyhook et de l'intervalle de rafraîchissement de la série.

Le paramètre [Titre de l'épisode requis](/sonarr/settings#importing) dans Sonarr contrôle le comportement d'importation lorsque le titre est TBA, mais après 24 heures à partir de la date de diffusion de l'épisode, la publication sera importée même si le titre est toujours TBA. Il n'y a également aucune modification automatique du renommage des fichiers intitulés TBA.

### La connexion sous-jacente a été fermée : une erreur inattendue s'est produite lors de l'envoi

Cela est dû à l'indexeur utilisant un protocole SSL non pris en charge par la version .NET actuelle trouvée dans [Sonarr => Système => État](/sonarr/system#status).

### La demande a expiré

Sonarr ne reçoit aucune réponse du client.

```none
    System.NET.WebException: La demande a expiré : ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: La demande a expiré
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Impossible de se connecter à l'indexeur

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Une tâche a été annulée.
```

Cela peut également être causé par :

- une configuration incorrecte ou l'utilisation d'un VPN
- une configuration incorrecte ou l'utilisation d'un proxy
- des problèmes DNS locaux - essayez de changer de fournisseur DNS
- des problèmes IPv6 locaux - généralement IPv6 est activé, mais non fonctionnel
- l'utilisation de Privoxy et une configuration incorrecte de celui-ci

## Problème non répertorié

Vous pouvez également consulter quelques commandes courantes de dépannage des autorisations et du réseau [dans notre guide](/permissions-and-networking). Sinon, veuillez discuter avec l'équipe de support sur Discord. Si c'est quelque chose qui peut être un problème courant, veuillez suggérer de l'ajouter au wiki.

# Recherches d'indexeurs et de trackers

- L'entrée FAQ [Pourquoi Sonarr n'a-t-il pas récupéré un épisode que j'attendais ?](/sonarr/faq#why-didnt-sonarr-grab-an-episode-i-was-expecting) est également probablement utile.
- Si vous utilisez [Prowlarr](/prowlarr), vous pouvez consulter l'[Historique](/prowlarr/history) de toutes les requêtes reçues par Prowlarr et comment elles ont été envoyées aux sites. Assurez-vous que `Paramètres` est activé dans Prowlarr Historique => Options. L'icône (i) fournit des détails supplémentaires.
- Les étapes de dépannage sont indiquées ci-dessous

## Augmentez le niveau de journalisation à la trace

> **La première étape consiste à augmenter le niveau de journalisation à Trace, consultez [Journalisation et fichiers journaux](#logging-and-log-files) pour plus de détails sur l'ajustement de la journalisation et la recherche dans les journaux. Vous reproduirez ensuite le problème et utiliserez les journaux de niveau trace de cette période pour examiner le problème.** Si quelqu'un vous aide, mettez le contexte avant/après dans un [pastebin](https://0bin.net), [Gist](https://gist.com) ou un site similaire pour le leur montrer. Il n'est pas nécessaire de fournir l'intégralité du fichier et il ne doit pas *uniquement* s'agir de l'erreur. Vous devez également reproduire le problème lorsque les tâches qui encombrent le fichier journal ne sont pas en cours d'exécution.
{.is-danger}

## Tester un indexeur ou un tracker

Lorsque vous testez un indexeur ou un tracker, dans les journaux de débogage ou de trace, vous pouvez trouver l'URL utilisée. Un exemple de test réussi est ci-dessous, vous pouvez voir qu'il interroge l'indexeur via une URL spécifique avec des paramètres spécifiques, puis la réponse. Vous pouvez tester cette URL dans votre navigateur en remplaçant `apikey=(removed)` par la clé API correcte comme `apikey=123`. Vous pouvez expérimenter avec les paramètres si vous obtenez une erreur de l'indexeur ou voir si vous avez des problèmes de connectivité s'il ne fonctionne pas du tout. Après avoir testé dans votre propre navigateur, vous devez tester à partir du système sur lequel il s'exécute *si* vous ne l'avez pas déjà fait.

## Tester une recherche

Tout comme le test d'indexeur/tracker ci-dessus, lorsque vous déclenchez une recherche tout en étant enregistré avec un niveau de journalisation de débogage ou de trace, vous pouvez obtenir l'URL utilisée à partir des fichiers journaux. Lors des tests, il est préférable d'utiliser une recherche aussi spécifique que possible. Une recherche manuelle (interactive) pour un seul épisode ou une saison est bonne car elle est spécifique et vous pouvez voir les résultats dans l'interface utilisateur tout en examinant les journaux. Les recherches manuelles (interactives) sont déclenchées en allant dans une série et en cliquant sur l'icône humaine pour un épisode ou une saison.

Dans ce test, vous rechercherez des erreurs évidentes et effectuerez quelques tests simples. Vous pouvez voir que la recherche a utilisé l'URL `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1`, que vous pouvez essayer vous-même dans un navigateur après avoir remplacé (removed) par votre clé API pour cet indexeur. Est-ce que cela fonctionne ? Voyez-vous les résultats attendus ? Cette entrée FAQ s'applique-t-elle ? Dans cette URL, vous pouvez voir qu'elle a défini des catégories spécifiques avec `cat=5030,5040,5045,5080`, donc si vous ne voyez pas les résultats attendus, c'est une raison probable. Vous pouvez également voir qu'elle a recherché par tvdbid avec `tvdbid=354629`, donc si l'épisode n'est pas correctement catégorisé sur l'indexeur, il devra être corrigé. Vous pouvez également voir qu'elle recherche par saison et épisode spécifiques avec season=1 et ep=1, donc si cela n'est pas correct sur l'indexeur, vous ne verrez pas ces résultats. Consultez la sortie XML de la recherche manuelle ci-dessous pour voir un exemple de sortie de requête fonctionnelle.

- Sortie XML de la recherche manuelle

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1" rel="self" type="application/rss+xml"/>
<title>api.nzbgeek.info</title>
<description>NZBgeek API</description>
<link>http://api.nzbgeek.info/</link>
<language>en-gb</language>
<webMaster>info@nzbgeek.info (NZBgeek)</webMaster>
<category/>
<image>
<url>https://api.nzbgeek.info/covers/nzbgeek.png</url>
<title>api.nzbgeek.info</title>
<link>http://api.nzbgeek.info/</link>
<description>NZBgeek</description>
</image>
<newznab:response offset="0" total="2"/>
<item>
<title>The.Fix.S01E01.1080p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/358e0f946f953771c7688864b0334ba1
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=358e0f946f953771c7688864b0334ba1
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:32 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.1080p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)" length="3810861000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="3810861000"/>
<newznab:attr name="guid" value="358e0f946f953771c7688864b0334ba1"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="55"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:54:15 +0000"/>
</item>
<item>
<title>The.Fix.S01E01.720p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/f7e4ac2875b6a1ce45bae91ab19e9699
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=f7e4ac2875b6a1ce45bae91ab19e9699
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:33 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.720p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)" length="1195794000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="1195794000"/>
<newznab:attr name="guid" value="f7e4ac2875b6a1ce45bae91ab19e9699"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="14"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:51:45 +0000"/>
</item>
</channel>
</rss>
```

![searches-indexers-and-trackers1.png](/assets/sonarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/sonarr/searches-indexers-and-trackers2.png)

- Extrait du journal de suivi

```none
2021-03-20 13:15:23.6|Info|NzbSearchService|Recherche de 1 indexeurs pour [The Fix : S01E01]
2021-03-20 13:15:23.6|Debug|Newznab|Téléchargement du flux https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
2021-03-20 13:15:23.6|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
```

- Journal de suivi complet d'une recherche

```none
2022-04-24 20:14:26.7|Info|ReleaseSearchService|Searching indexers for [Fairy Tail : S02E91 (91)]. 5 active indexers
2022-04-24 20:14:26.7|Debug|ReleaseSearchService|Total of 10 reports were found for [Fairy Tail : S02E91 (91)] from 5 indexers
2022-04-24 20:14:26.7|Info|DownloadDecisionMaker|Processing 10 releases
2022-04-24 20:14:26.7|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.1080p.WEB-DL' from 'Indexer1'
2022-04-24 20:14:26.7|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.1080p.WEB-DL'
2022-04-24 20:14:26.7|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:26.7|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:26.7|Debug|Parser|Language parsed: English
2022-04-24 20:14:26.7|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:26.7|Debug|Parser|Quality parsed: WEBDL-1080p v1
2022-04-24 20:14:26.7|Debug|Parser|Release Group parsed:
2022-04-24 20:14:26.7|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.1080p.WEB-DL'
2022-04-24 20:14:26.7|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.1080p.WEB-DL': 0
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.1080p.WEB-DL, meets size constraints.
2022-04-24 20:14:26.7|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:26.7|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:26.7|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:26.7|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-1080p v1
2022-04-24 20:14:26.7|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:26.7|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.1080p.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:26.7|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:26.7|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:26.7|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:26.7|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:26.7|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] WEBDL-1080p is not wanted in profile
2022-04-24 20:14:26.7|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.720p.WEB-DL' from 'Indexer2'
2022-04-24 20:14:26.7|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.720p.WEB-DL'
2022-04-24 20:14:26.7|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:26.7|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:26.7|Debug|Parser|Language parsed: English
2022-04-24 20:14:26.7|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:26.7|Debug|Parser|Quality parsed: WEBDL-720p v1
2022-04-24 20:14:26.7|Debug|Parser|Release Group parsed:
2022-04-24 20:14:26.7|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.720p.WEB-DL'
2022-04-24 20:14:26.7|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.720p.WEB-DL': 0
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.720p.WEB-DL, meets size constraints.
2022-04-24 20:14:26.7|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:26.7|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:26.7|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:26.7|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-720p v1
2022-04-24 20:14:26.7|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:26.7|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.720p.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:26.7|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:26.7|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:26.7|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:26.7|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:26.7|Debug|DownloadDecisionMaker|Release accepted
2022-04-24 20:14:26.7|Trace|Http|Res: 66 [GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
2022-04-24 20:14:26.7|Debug|Api|[GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
```

- Logs will look like

```none
2022-04-24 20:14:26.7|Info|ReleaseSearchService|Searching indexers for [Fairy Tail : S02E91 (91)]. 5 active indexers
2022-04-24 20:14:26.7|Debug|ReleaseSearchService|Total of 10 reports were found for [Fairy Tail : S02E91 (91)] from 5 indexers
2022-04-24 20:14:26.7|Info|DownloadDecisionMaker|Processing 10 releases
2022-04-24 20:14:26.7|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.1080p.WEB-DL' from 'Indexer1'
2022-04-24 20:14:26.7|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.1080p.WEB-DL'
2022-04-24 20:14:26.7|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:26.7|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:26.7|Debug|Parser|Language parsed: English
2022-04-24 20:14:26.7|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:26.7|Debug|Parser|Quality parsed: WEBDL-1080p v1
2022-04-24 20:14:26.7|Debug|Parser|Release Group parsed:
2022-04-24 20:14:26.7|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.1080p.WEB-DL'
2022-04-24 20:14:26.7|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.1080p.WEB-DL': 0
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.1080p.WEB-DL, meets size constraints.
2022-04-24 20:14:26.7|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:26.7|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:26.7|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:26.7|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-1080p v1
2022-04-24 20:14:26.7|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.1080p.WEB-DL
2022-04-24 20:14:26.7|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.1080p.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:26.7|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:26.7|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:26.7|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:26.7|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:26.7|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] WEBDL-1080p is not wanted in profile
2022-04-24 20:14:26.7|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.720p.WEB-DL' from 'Indexer2'
2022-04-24 20:14:26.7|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.720p.WEB-DL'
2022-04-24 20:14:26.7|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:26.7|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:26.7|Debug|Parser|Language parsed: English
2022-04-24 20:14:26.7|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:26.7|Debug|Parser|Quality parsed: WEBDL-720p v1
2022-04-24 20:14:26.7|Debug|Parser|Release Group parsed:
2022-04-24 20:14:26.7|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.720p.WEB-DL'
2022-04-24 20:14:26.7|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.720p.WEB-DL': 0
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:26.7|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.720p.WEB-DL, meets size constraints.
2022-04-24 20:14:26.7|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:26.7|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:26.7|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:26.7|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-720p v1
2022-04-24 20:14:26.7|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.720p.WEB-DL
2022-04-24 20:14:26.7|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.720p.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:26.7|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:26.7|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:26.7|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:26.7|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:26.7|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:26.7|Debug|DownloadDecisionMaker|Release accepted
2022-04-24 20:14:26.7|Trace|Http|Res: 66 [GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
2022-04-24 20:14:26.7|Debug|Api|[GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
```

- Note that in the above case, there are 10 releases found for the episode, but only 2 are processed. This is because the other releases are rejected due to the quality not being wanted in the profile.
- To resolve this issue, you can do the following:
  - Check your profile settings to ensure that the desired qualities are selected.
  - Check the release restrictions for the series to ensure that the desired qualities are allowed.
  - If the releases have a different naming convention, you can try adding a custom format in the series settings to match the releases.
  - If the releases have a different language, you can try adjusting the language settings in the series settings to match the releases.
  - If the releases have a different release group, you can try adjusting the release group settings in the series settings to match the releases.
  - If the releases have a different size, you can try adjusting the size settings in the series settings to allow for a wider range of sizes.
  - If the releases have a different age, you can try adjusting the age settings in the series settings to allow for a wider range of ages.
  - If the releases have different retention, you can try adjusting the retention settings in the series settings to allow for a wider range of retentions.
  - If the releases have different delay, you can try adjusting the delay settings in the series settings to allow for a wider range of delays.
  - If the releases have already been imported, you can try adjusting the already imported settings in the series settings to allow for re-importing.
  - If the releases are not being searched at all, you can check the health checks in the system status to see if there are any issues with the indexers.
  - If the releases are poorly named, you can try adjusting the custom format in the series settings to match the releases.
  - If none of the above solutions work, you can try manually searching for the releases and adding them to your download client.

- Les packs de séries ne sont pas pris en charge
- Les packs de saisons multiples ne sont pas pris en charge
- Dans de nombreux cas, Sonarr est tout simplement incapable de faire correspondre le résultat renvoyé à une série connue. Dans ces cas, vos journaux ressembleront à ce qui suit. Il faudrait les récupérer et les importer manuellement. La phrase clé à rechercher dans les journaux est `|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings` (« Impossible d'identifier le(s) épisode(s) correct(s) à l'aide du nom de la version et des correspondances de scène »).

```none
2022-02-23 14:11:09.7|Debug|Parser|Parsing string 'Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR'
2022-02-23 14:11:09.7|Trace|Parser|^(?<title>.+?)[-_. ]+?(?:S|Season|Saison|Series)[-_. ]?(?<season>\d{1,2}(?![-_. ]?\d+))(\W+|_|$)(?<extras>EXTRAS|SUBPACK)?(?!\\)
2022-02-23 14:11:09.7|Debug|Parser|Episode Parsed. Johnny Bravo 1997 Season 1 4 - Season 01 
2022-02-23 14:11:09.7|Debug|Parser|Language parsed: English
2022-02-23 14:11:09.7|Debug|QualityParser|Trying to parse quality for Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR
2022-02-23 14:11:09.7|Debug|Parser|Quality parsed: SDTV v1
2022-02-23 14:11:09.7|Debug|Parser|Release Group parsed: 
2022-02-23 14:11:09.8|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings
```

### Le tracker nécessite des capacités de recherche brute

- Sonarr recherche `9 1 1`, mais votre tracker n'a que des résultats pour `9-1-1` ou `John s Show` et `John's Show`
- Cela est dû au fait que votre tracker ne prend pas en charge les recherches normalisées standard.
- La solution consiste à mettre à jour les capacités de recherche de la définition de votre tracker pour indiquer qu'il [requiert et prend en charge la recherche brute](https://github.com/Sonarr/Sonarr/issues/1225#issuecomment-981153943)
- Jackett prend en charge le drapeau, mais les capacités doivent être mises à jour pour chaque indexeur. Ouvrez une demande de fonctionnalité pour que Jackett ajoute cette fonctionnalité à votre indexeur.
- Prowlarr prend en charge le drapeau, mais les capacités doivent être mises à jour pour chaque indexeur. Ouvrez une demande de fonctionnalité pour que Prowlarr ajoute cette fonctionnalité à votre indexeur.

### La série a besoin d'un alias

Les versions peuvent être téléchargées sous le nom de `The Series Name`, mais TVDB a la série sous le nom de `Series Name` ou des différences de nom similaires. Veuillez consulter [cette entrée FAQ](/sonarr/faq#why-cannot-sonarr-import-episode-files-for-series-x-why-cannot-sonarr-find-releases-for-series-x) pour plus d'informations.

### La série a besoin d'un mappage XEM

Les versions peuvent être téléchargées sous le nom de `Series Title S02E45` ou `Other Series Title S2022E42`, mais TVDB a cet épisode sous le nom de `Series Title S03E01` ou `Other Series Title S03E42`. Veuillez consulter [cette entrée FAQ](/sonarr/faq#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc) pour plus d'informations.

### Mauvais type de série

Le type de série affecte la façon dont Sonarr effectue les recherches. Le type de série doit être sélectionné en fonction de la façon dont la série est diffusée sur les indexeurs.
[Voir cette entrée FAQ pour plus de détails](/sonarr/faq#whats-the-different-series-types)

> Si le type de série **Anime** est utilisé, il est [possible de rechercher également votre indexeur avec le type standard](/sonarr/settings#indexers)
{.is-info}

#### Quotidien

Les journaux afficheront `Searching indexers for [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Les journaux afficheront `Searching indexers for [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Les journaux afficheront `Searching indexers for [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

### Le média n'est pas surveillé

Les journaux afficheront quelque chose de similaire à

```none
2022-03-30 13:46:03.0|Debug|MonitoredEpisodeSpecification|No episodes in the release are monitored. Rejecting
2022-03-30 13:46:03.0|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] One or more episodes is not monitored
```

La série/saison/épisode(s) n'est(sont) pas surveillé(s). Vérifiez l'état de surveillance de la série, de la saison et de l'épisode(s).

> Les packs de saisons ne seront téléchargés que si tous les épisodes de la saison sont surveillés et que le pack de saison met à jour tous les épisodes existants ou que tous les épisodes sont manquants.
{.is-info}

### Requête réussie - Aucun résultat renvoyé

Vous recevez un message similaire à `Query successful, but no results were returned from your indexer. This may be an issue with the indexer or your indexer category settings.` (« Requête réussie, mais aucun résultat n'a été renvoyé par votre indexeur. Cela peut être un problème avec l'indexeur ou les paramètres de catégorie de votre indexeur. »)

Cela est dû à votre indexeur qui ne renvoie aucun résultat dans les catégories que vous avez configurées pour l'indexeur.

### Mauvaises catégories

Les catégories incorrectes sont probablement la cause la plus courante des résultats affichés dans les recherches manuelles d'un indexeur/tracker, mais pas dans \*Arr. L'indexeur/tracker *devrait* afficher la catégorie dans les résultats de recherche, ce qui devrait vous aider à comprendre ce qui manque. Si vous utilisez Jackett ou Prowlarr, chaque tracker a une liste de catégories spécifiquement prises en charge. Assurez-vous d'utiliser les bonnes catégories pour les catégories. Beaucoup trouvent utile d'avoir la liste visible dans une fenêtre de navigateur pendant qu'ils modifient l'entrée dans Sonarr.

> Notez que si vous avez la catégorie `Anime Categories` vide dans les paramètres de votre indexeur, l'indexeur ne sera pas utilisé pour les recherches de type Anime.
> De même, si vous avez la catégorie `Categories` vide dans les paramètres de votre indexeur, l'indexeur ne sera pas utilisé pour les recherches de type Standard ou Quotidien.
{.is-info}

### Résultats incorrects

Parfois, les indexeurs renvoient des résultats totalement non pertinents ; Sonarr envoie des paramètres pour limiter la recherche à une série. Parfois, les résultats renvoyés sont totalement non pertinents. Ou parfois, principalement pertinents avec quelques résultats incorrects. Le premier est généralement un problème d'indexeur et vous pourrez le déterminer à partir des journaux de trace qui en sont la cause. Vous pouvez désactiver cet indexeur et signaler le problème. L'autre est généralement des versions catégorisées qui peuvent être signalées sur l'indexeur/tracker.

Certains trackers - comme EZTV et d'autres publics - renvoient des résultats aléatoires s'ils n'ont pas de correspondance exacte avec la série/saison/épisode interrogé. Il n'y a pas de solution à cela.

### Résultats manquants

Si vous avez des résultats sur le site que vous pouvez trouver mais qui n'apparaissent pas dans Sonarr, alors votre problème est probablement l'une des possibilités suivantes :

- [Les catégories sont incorrectes - Voir ci-dessus](#wrong-categories)
- Une recherche basée sur un ID (IMDbId, TVDBId, etc.) est effectuée et l'indexeur n'a pas correctement mappé les versions à cet ID. C'est quelque chose que seul votre indexeur peut résoudre. Ils doivent s'assurer que la version est associée aux bons ID applicables.
- Vous ne recherchez pas comme Sonarr recherche ; Il est très probable que les termes que vous recherchez sur l'indexeur ne sont pas ceux que Sonarr interroge. Vous pouvez voir comment Sonarr interroge à partir des journaux de trace. Les requêtes basées sur du texte seront généralement au format `q=words%20and%20things%20here` cette chaîne est encodée en HTTP et peut être facilement décodée à l'aide de n'importe quel outil de décodage/encodage HTML en ligne.
- Des morceaux manquants du flux RSS des nouveaux téléchargements. Les journaux apparaîtront comme suit et un événement d'avertissement sera noté.

```none
2022-02-22 08:03:38.7|Debug|Torznab|Downloading Feed http://jackett:9117/api/v2.0/indexers/torrentdownloads/results/torznab?t=tvsearch&cat=5000,100008&extended=1&apikey=(removed)&offset=2900&limit=100
2022-02-22 08:03:40.7|Warn|Torznab|Indexer TorrentDownloads rss sync didn't cover the period between 2/21/2022 8:32:06 PM and 2/21/2022 9:02:42 PM UTC. Search may be required.
```

### Validation du certificat

Vous vous connecterez à la plupart des indexeurs/trackers via https, donc vous devez vous assurer que cela fonctionne correctement sur votre système. Cela signifie que votre fuseau horaire et votre heure doivent être définis *correctement*. Cela signifie également que vos certificats système doivent être à jour.

### Atteinte des limites de taux

Si vous utilisez un VPN ou un proxy, vous pouvez être en concurrence avec des dizaines, des centaines ou des milliers d'autres personnes qui essaient toutes d'utiliser des services comme , theXEM et/ou vos indexeurs et trackers. La limitation des taux et la protection contre les attaques par déni de service sont souvent effectuées par adresse IP et le point de sortie de votre VPN/proxy est *une* adresse IP. À moins que vous ne soyez dans un pays répressif comme la Chine, l'Australie ou l'Afrique du Sud, vous n'avez pas besoin de VPN/proxy.

Rarbg a tendance à avoir une sorte de limitation des taux dans leur API et affiche une réponse sans résultats.

### Interdiction IP

De même que pour les limites de taux, certains indexeurs - comme Nyaa - peuvent interdire purement et simplement une adresse IP. Cela est généralement semi-permanent et la solution consiste à obtenir une nouvelle adresse IP auprès de votre fournisseur d'accès Internet ou de votre fournisseur de VPN.

### Utilisation de l'endpoint Jackett /all

L'endpoint `/all` de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc nécessaire d'ajouter chaque tracker individuellement. Alternativement, vous pouvez envisager d'utiliser l'alternative Jackett & NZBHydra2 [Prowlarr](/prowlarr)

[Même Jackett dit que /all devrait être évité et ne devrait pas être utilisé.](https://github.com/Jackett/Jackett#aggregate-indexers)

L'utilisation de l'endpoint all n'a aucun avantage (à part une réduction de la charge de gestion), seulement des inconvénients :

- vous perdez le contrôle sur les paramètres spécifiques à l'indexeur (catégories, modes de recherche, etc.)
- mélanger les modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
- les catégories spécifiques à l'indexeur (\>= 100000) ne peuvent pas être utilisées.
- les indexeurs lents ralentiront le résultat global
- le nombre total de résultats est limité à 1000
- résultats non pertinents
- résultats manquants

Ajouter chaque indexeur séparément permet d'ajuster finement les catégories pour chaque indexeur, ce qui peut poser problème avec l'endpoint `/all` si l'utilisation de la mauvaise catégorie provoque des erreurs sur certains trackers. Dans Sonarr, chaque indexeur est limité à 1000 résultats si la pagination est prise en charge ou à 100 si ce n'est pas le cas, ce qui signifie que plus vous ajoutez de trackers à Jackett, plus vous avez de chances de manquer des résultats. Enfin, si *un seul* des trackers dans `/all` renvoie une erreur,  le désactivera et vous n'obtiendrez plus aucun résultat.

### Utilisation de NZBHydra2 comme une seule entrée

L'utilisation de NZBHydra2 comme une seule entrée d'indexeur (c'est-à-dire 1 entrée NZBHydra2 dans Sonarr pour de nombreux indexeurs dans NZBHydra2) plutôt que plusieurs (c'est-à-dire de nombreuses entrées NZBHydra2 dans Sonarr pour de nombreux indexeurs dans NZBHydra2) présente les mêmes problèmes que ceux mentionnés ci-dessus avec l'endpoint `/all` de Jackett.

### L'indexeur n'est pas recherché

- Si un indexeur ne semble pas être recherché, il est probable que cela soit dû au fait que l'indexeur ne prend pas en charge le type de requête. Le cas le plus courant est que Nyaa ne prend en charge que les recherches par requête et non les recherches par saison/épisode. Les journaux de trace indiquent après un redémarrage lors de la première recherche quelles sont les capacités d'un indexeur ou ce qu'il ne peut pas faire.

### La recherche manuelle Jackett trouve plus de résultats

- [Voir cette entrée FAQ](/sonarr/faq#jackett-shows-more-results-than-sonarr-when-manually-searching)

### Les profils de versions ne sont pas respectés

Il y a quelques raisons pour lesquelles il peut sembler que vos profils ne sont pas pris en compte. La plus courante est liée à la restriction de l'indexeur dans les profils de versions. Étant donné que l'indexeur n'est pas stocké avec les données, tous les scores de `mot préféré` sont *nuls* pour les médias de votre bibliothèque, mais pendant le "RSS" et la recherche, ils seront appliqués. De même pour toutes les restrictions de `doit contenir` ou `ne doit pas contenir`, les restrictions ne s'appliquent qu'à cet indexeur ; tout le reste est autorisé. Cela peut alors donner l'impression que les profils de versions sont ignorés ou que des boucles de mise à niveau se produisent.

### Problème non répertorié

Vous pouvez également consulter certaines commandes courantes de dépannage des autorisations et du réseau [dans notre guide](/permissions-and-networking). Sinon, veuillez en discuter avec l'équipe de support sur Discord. Si c'est quelque chose qui pourrait être un problème courant, veuillez suggérer de l'ajouter au wiki.

## Erreurs

Voici quelques-unes des erreurs courantes que vous pouvez rencontrer lors de l'ajout d'un indexeur

### La connexion sous-jacente a été fermée : Une erreur inattendue s'est produite lors de l'envoi

Cela est dû à l'indexeur utilisant un protocole SSL non pris en charge par la version .NET actuelle trouvée dans [Sonarr => Système => État](/sonarr/system#status).

### La demande a expiré

Sonarr ne reçoit aucune réponse de l'indexeur.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

Cela peut également être causé par :

- une configuration incorrecte ou l'utilisation d'un VPN
- une configuration incorrecte ou l'utilisation d'un proxy
- des problèmes DNS locaux - Essayez de passer à un autre fournisseur DNS
- des problèmes IPv6 locaux - généralement, IPv6 est activé, mais non fonctionnel
- l'utilisation de Privoxy et une mauvaise configuration de celui-ci

### Problème non répertorié

Vous pouvez également consulter certaines commandes courantes de dépannage des autorisations et du réseau [dans notre guide](/permissions-and-networking). Sinon, veuillez en discuter avec l'équipe de support sur Discord. Si c'est quelque chose qui pourrait être un problème courant, veuillez suggérer de l'ajouter au wiki.