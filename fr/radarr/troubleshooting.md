---
title: Dépannage de Radarr
description: Dépannage de Radarr, y compris l'obtention des fichiers journaux, le dépannage de la recherche et des problèmes courants, ainsi que le dépannage du téléchargement/importation et des problèmes courants
published: true
date: 2023-08-12T09:40:45.369Z
tags: radarr, dépannage
editor: markdown
dateCreated: 2021-08-03T21:05:52.988Z
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
    - [L'image disque de la base de données est corrompue](#limage-disque-de-la-base-de-données-est-corrompue)
    - [Problème de migration](#problème-de-migration)
    - [Problèmes de migration de l'interface utilisateur](#problèmes-de-migration-de-linterface-utilisateur)
    - [Problème de permission](#problème-de-permission)
  - [Résoudre le problème](#résoudre-le-problème)
    - [Problèmes de migration](#problèmes-de-migration)
    - [Problèmes de permissions](#problèmes-de-permissions)
    - [Mise à niveau manuelle](#mise-à-niveau-manuelle)
- [Téléchargements et importation](#téléchargements-et-importation)
  - [Tester le client de téléchargement](#tester-le-client-de-téléchargement)
  - [Tester un téléchargement](#tester-un-téléchargement)
  - [Tester une importation](#tester-une-importation)
  - [Problèmes courants](#problèmes-courants)
    - [L'interface Web du client de téléchargement n'est pas activée](#linterface-web-du-client-de-téléchargement-nest-pas-activée)
    - [SSL est utilisé et mal configuré](#ssl-est-utilisé-et-mal-configuré)
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
    - [Temps de connexion dépassé](#temps-de-connexion-dépassé)
  - [Problème non répertorié](#problème-non-répertorié)
- [Recherches, indexeurs et trackers](#recherches-indexeurs-et-trackers)
  - [Augmenter le niveau de journalisation à la trace](#augmenter-le-niveau-de-journalisation-à-la-trace)
  - [Tester un indexeur ou un tracker](#tester-un-indexeur-ou-un-tracker)
  - [Tester une recherche](#tester-une-recherche)
  - [Problèmes courants](#problèmes-courants-1)
    - [L'indexeur nécessite des capacités de recherche brute](#lindexeur-nécessite-des-capacités-de-recherche-brute)
    - [Le média n'est pas surveillé](#le-média-nest-pas-surveillé)
    - [Catégories incorrectes](#catégories-incorrectes)
    - [Requête réussie - Aucun résultat retourné](#requête-réussie---aucun-résultat-retourné)
    - [Résultats incorrects](#résultats-incorrects)
    - [Résultats manquants](#résultats-manquants)
    - [Validation du certificat](#validation-du-certificat)
    - [Atteinte des limites de taux](#atteinte-des-limites-de-taux)
    - [Interdiction IP](#interdiction-ip)
    - [L'année ne correspond pas](#lannée-ne-correspond-pas)
    - [Année manquante](#année-manquante)
    - [Utilisation de l'endpoint /all de Jackett](#utilisation-de-lendpoint-all-de-jackett)
    - [Utilisation de NZBHydra2 comme une seule entrée](#utilisation-de-nzbhydra2-comme-une-seule-entrée)
    - [Problème non répertorié](#problème-non-répertorié-1)
  - [Erreurs](#erreurs)
    - [La connexion sous-jacente a été fermée : une erreur inattendue s'est produite lors de l'envoi](#la-connexion-sous-jacente-a-été-fermée-une-erreur-inattendue-sest-produite-lors-de-lenvoi)
    - [La demande a expiré](#la-demande-a-expiré)
    - [Problème non répertorié](#problème-non-répertorié-2)

# Demander de l'aide

Vous avez besoin d'aide ? C'est normal, tout le monde a besoin d'aide parfois. Vous pouvez obtenir de l'aide en temps réel via le chat sur :

- [<i class="fab fa-discord"></i>&emsp;Discord *Discord officiel de Radarr*](https://radarr.video/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Subreddit officiel de Radarr*](https://reddit.com/r/radarr)
{.links-list}

Mais avant d'y aller et de poster, assurez-vous que votre demande d'aide est la meilleure possible. Décrivez clairement le problème et décrivez brièvement votre configuration, y compris des éléments tels que votre système d'exploitation/distribution, la version de .NET, la version de Radarr, le client de téléchargement et sa version. **Si vous utilisez [Docker](https://www.docker.com/), veuillez suivre d'abord le [Guide Docker](/docker-guide) car cela résoudra les problèmes courants et fréquents de chemin/permissions. Sinon, veuillez avoir un [docker compose](/docker-guide#docker-compose) à portée de main. [Comment générer un Docker Compose](https://trash-guides.info/compose)** Parlez-nous de ce que vous avez déjà essayé, de ce que vous avez examiné. Utilisez la section [Journalisation et fichiers journaux](#journalisation-et-fichiers-journaux) pour augmenter le niveau de journalisation à la trace, recréer le problème, collez le contexte pertinent sur un site de partage de code et incluez un lien vers celui-ci dans votre message. Vous pouvez même inclure des captures d'écran pour mettre en évidence le problème.

Plus nous en savons, plus il est facile de vous aider.

# Journalisation et fichiers journaux

Il est également utile de consulter les problèmes courants de dépannage :
- [Problèmes courants de téléchargement et d'importation](#problèmes-courants)
- [Problèmes courants de recherche d'indexeurs et de trackers](#problèmes-courants-1)
{.links-list}

Si on vous demande des journaux de débogage, vos journaux contiendront `debug` et si on vous demande des journaux de trace, vos journaux contiendront `trace`. Si les journaux que vous fournissez ne contiennent ni l'un ni l'autre, ce ne sont pas les journaux demandés.

- Évitez de partager l'intégralité du fichier journal à moins qu'on ne vous le demande.
- N'envoyez pas les journaux directement sur Discord ou ne les collez pas sous forme de murs de texte, sauf si on vous le demande.
- Ne partagez pas les journaux en tant que pièce jointe, archive zip ou tout autre format autre que du texte partagé via les services indiqués ci-dessous.

Pour fournir des journaux de qualité et utiles à partager :

> Assurez-vous qu'une tâche indésirable NE s'exécute PAS, comme une actualisation RSS
{.is-warning}

1. [Augmentez le niveau de journalisation à la trace (Paramètres => Général => Niveau de journalisation ou Modifiez le fichier de configuration)](#journaux-de-tracedébogage)
2. [Effacez les journaux (Système => Journaux => Effacer les journaux ou Supprimez tous les journaux du dossier des journaux)](#effacement-des-journaux)
3. Reproduisez le problème (Refaites ce qui casse les choses)
4. [Ouvrez le fichier journal de trace (radarr.trace.txt) via l'interface utilisateur ou le fichier journal](#emplacement-des-journaux-standard) sur le système de fichiers et trouvez le contexte pertinent
5. Copiez une grande partie avant le problème, le problème lui-même et une grande partie après le problème.
6. Utilisez [Gist](https://gist.github.com/), [0bin (**Assurez-vous de désactiver la colorisation**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Pastebin d'Ubuntu](https://pastebin.ubuntu.com/) ou des sites similaires - à l'exception de ceux mentionnés ci-dessous - pour partager les journaux copiés ci-dessus

**Avertissements :**
- **N'utilisez pas [pastebin.com](https://pastebin.com) car leurs filtres ont tendance à bloquer les journaux.
- N'utilisez pas [pastebin.pl](https://pastebin.pl) car leur site n'est souvent pas accessible.
- N'utilisez pas [JustPasteIt](https://justpaste.it/) car leur site ne facilite pas l'examen des journaux.
- N'envoyez pas votre journal en tant que fichier
- N'envoyez pas et ne partagez pas vos journaux via Google Drive, Dropbox ou tout autre site non mentionné ci-dessus.
- N'archivez pas (zip, tar (tarball), 7zip, etc.) vos journaux.
- Ne partagez pas la sortie de la console, la sortie du conteneur Docker ou autre chose que les journaux d'application spécifiés

**Note importante :**
- Lors de l'utilisation de [0bin](https://0bin.net/), assurez-vous de désactiver la colorisation et de ne pas brûler après lecture.

- Alternativement, si vous recherchez une entrée spécifique dans un ancien fichier journal mais que vous n'êtes pas sûr duquel, vous pouvez utiliser N++. Vous pouvez utiliser la fonction "Rechercher dans les fichiers" de Notepad++ pour rechercher les anciens fichiers journaux si nécessaire.
- **Unix uniquement :** Alternativement, si vous recherchez une entrée spécifique dans un ancien fichier journal mais que vous n'êtes pas sûr duquel, vous pouvez utiliser grep. Par exemple, si vous souhaitez trouver des informations sur le film/série/livre/chanson/indexeur "Shooter", vous pouvez exécuter la commande suivante `grep -inr -C 100 -e 'Shooter' /chemin/vers/les/journaux/*.trace*.txt` Si votre [Répertoire Appdata](/radarr/appdata-directory) est dans votre dossier personnel, vous exécuteriez : `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Les indicateurs ont les fonctions suivantes
    * -i : ignorer la casse
    * -n : afficher le numéro de ligne
    * -r : vérifier récursivement tous les fichiers dans le chemin
    * -C : fournir le nombre de lignes avant et après la ligne où il est trouvé
    * -e : le motif à rechercher

```

## Emplacement des journaux standard

Les fichiers journaux se trouvent dans le [Répertoire Appdata](/radarr/appdata-directory) de Radarr, à l'intérieur du dossier logs/. Vous pouvez également accéder aux fichiers journaux depuis l'interface utilisateur à Système => Journaux => Fichiers.

> Remarque : Le tableau des journaux ("Événements") dans l'interface utilisateur n'est pas identique aux fichiers journaux et n'est pas aussi utile. Si on vous demande des journaux, veuillez copier/coller à partir des fichiers journaux et non de la table.
{.is-info}

## Emplacement des journaux de mise à jour

Les fichiers journaux de mise à jour se trouvent dans le [Répertoire Appdata](/radarr/appdata-directory) de Radarr, à l'intérieur du dossier UpdateLogs/.

## Partage des journaux

Les journaux peuvent être longs et difficiles à lire dans un message sur un forum ou sur Reddit, et ils sont encombrants sur Discord, veuillez donc utiliser [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) ou tout autre site similaire de partage de code. Le fichier entier n'est généralement pas nécessaire, seulement une bonne quantité de contexte avant et après le problème/erreur. N'oubliez pas d'attendre que des tâches indésirables telles qu'une synchronisation RSS ou une actualisation de la bibliothèque se terminent.

## Journaux de trace/débogage

Vous pouvez modifier le niveau de journalisation dans Paramètres => Général => Journalisation. Radarr n'a pas besoin d'être redémarré pour que le changement prenne effet. Les derniers fichiers journaux de débogage/traces sont nommés respectivement `radarr.debug.txt` et `radarr.trace.txt`.

Si vous ne pouvez pas accéder à l'interface utilisateur pour définir le niveau de journalisation, vous pouvez le faire en modifiant le fichier config.xml dans le répertoire AppData en définissant la valeur LogLevel sur Debug ou Trace au lieu de Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Effacement des journaux

Vous pouvez effacer les fichiers journaux et la base de données des journaux directement depuis l'interface utilisateur, sous Système => Journaux => Fichiers et Système => Journaux => Supprimer (Icône de corbeille)

# Fichiers journaux multiples

Radarr utilise des fichiers journaux roulants limités à 1 Mo chacun. Le fichier journal actuel est toujours `radarr.txt`, pour les autres fichiers, `radarr.0.txt` est le plus récent (plus le nombre est élevé, plus il est ancien). Ce fichier journal contient les entrées `fatal`, `error`, `warn` et `info`.

Lorsque le niveau de journalisation de débogage est activé, des fichiers journaux roulants supplémentaires `radarr.debug.txt` seront présents. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info` et `debug`. Ils couvrent généralement une période de 40 heures.

Lorsque le niveau de journalisation de trace est activé, des fichiers journaux roulants supplémentaires `radarr.trace.txt` seront présents. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info`, `debug` et `trace`. En raison de la verbosité de la trace, ils ne couvrent que quelques heures au maximum.

# Récupération après une mise à jour échouée

- Nous faisons tout notre possible pour éviter les problèmes lors de la mise à niveau, mais s'ils se produisent, nous vous guiderons à travers les étapes à suivre pour récupérer votre installation.
- Cette section couvre également les problèmes courants après la mise à jour.

## Déterminer le problème

- Le meilleur endroit où chercher lorsque l'application ne démarre pas après une mise à jour est de consulter les [journaux de mise à jour](#emplacement-des-journaux-de-mise-à-jour) et de voir si la mise à jour s'est terminée avec succès. Si ceux-ci ne présentent aucun problème, la prochaine étape consiste à consulter vos fichiers journaux d'application habituels. Avant de tenter de redémarrer, utilisez [Journalisation](/radarr/settings#journalisation) et [Fichiers journaux](/radarr/system#fichiers-journaux) pour les trouver et augmenter le niveau de journalisation.
- Le problème le plus fréquemment rencontré est que le système sur lequel l'application est installée a modifié le répertoire `/tmp` et a supprimé des fichiers \*Arr critiques lors de la mise à niveau, ce qui a entraîné l'échec de la mise à niveau et du retour en arrière. Dans ce cas, réinstallez simplement par-dessus l'installation bâclée existante.

### L'image disque de la base de données est corrompue

- Consultez notre [FAQ](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)

### Problème de migration

- Les erreurs de migration ne seront pas identiques, mais voici un exemple :

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Problèmes de migration de l'interface utilisateur

- Si vous passez entre des [versions/branches non prises en charge](/radarr/faq#can-i-switch-between-branches), vous pouvez rencontrer un problème de migration qui ressemble à celui ci-dessous. La solution consiste à [revenir à la branche ou à la version supérieure sur laquelle vous étiez précédemment](/radarr/faq#how-do-i-update-radarr), ou à [restaurer une sauvegarde](/radarr/faq#how-do-i-backuprestore-radarr) pour votre version actuelle.

![radarr-migration-error-ui.png](/assets/radarr/radarr-migration-error-ui.png)

### Problème de permission

- Les problèmes de permissions sont dus au fait que l'application ne peut pas accéder aux dossiers temporaires pertinents et/ou au dossier binaire de l'application. Corrigez les permissions afin que l'utilisateur/le groupe sous lequel s'exécute l'application ait les autorisations appropriées.

- Les utilisateurs de Synology peuvent rencontrer le bug Synology `Access to the path '/proc/{some number}/maps is denied`

- Les utilisateurs de Synology peuvent également rencontrer des problèmes d'espace dans `/tmp` sur certains NAS. Vous devrez spécifier un chemin `/tmp` différent pour l'application. Consultez la communauté SynoCommunity ou d'autres canaux de support Synology pour obtenir de l'aide à ce sujet.

## Résolution du problème

### Problèmes de migration

En cas de problème de migration, il n'y a pas grand-chose que vous puissiez faire immédiatement. Si le problème vous concerne spécifiquement (ou s'il n'y a pas encore de publications à ce sujet), veuillez créer une publication sur [notre subreddit](https://reddit.com/r/radarr) ou passer sur notre [discord](https://radarr.video/discord). Si d'autres personnes rencontrent le même problème, soyez assuré que nous y travaillons.

> Veuillez vous assurer de ne pas avoir essayé d'utiliser une base de données de la version `nightly` sur la version stable. Il est déconseillé de passer d'une branche à l'autre.{.is-info}

### Problèmes de permissions

- Corrigez les permissions pour vous assurer que l'utilisateur/groupe sous lequel l'application s'exécute peut accéder (lecture et écriture) à la fois à `/tmp` et au répertoire d'installation de l'application.

- Pour les utilisateurs de Synology qui rencontrent des problèmes avec `/proc/###/maps` qui arrêtent Sonarr ou les autres applications \*Arr, mettre à jour devrait résoudre ce problème. Il s'agit d'un problème avec le package SynoCommunity.

### Mise à niveau manuelle

Téléchargez la dernière version depuis notre site web.

Installez la mise à jour (.exe) ou extrayez (.zip) le contenu par-dessus votre installation existante et relancez Radarr comme d'habitude.

# Téléchargements et importation

Le téléchargement et l'importation sont les étapes où *la plupart* des utilisateurs rencontrent des problèmes. D'un point de vue général, Radarr doit être en mesure de communiquer avec votre client de téléchargement et d'avoir accès aux fichiers qu'il télécharge. Il existe une grande variété de clients de téléchargement pris en charge et une variété encore *plus grande* de configurations. Cela signifie qu'il existe quelques configurations *courantes*, mais il n'y a pas de configuration *correcte* unique et la configuration de chacun peut être légèrement différente.

> **La première étape consiste à augmenter le niveau de journalisation à Trace, consultez [Logging and Log Files](#logging-and-log-files) pour plus de détails sur l'ajustement de la journalisation et la recherche dans les journaux. Vous reproduirez ensuite le problème et utiliserez les journaux de niveau trace de cette période pour examiner le problème.** Si quelqu'un vous aide, mettez le contexte avant/après dans un [pastebin](https://0bin.net), [Gist](https://gist.com) ou un site similaire pour le lui montrer. Il n'est pas nécessaire de fournir l'intégralité du fichier et il ne doit pas se limiter à l'erreur. Vous devez également reproduire le problème lorsque des tâches qui encombrent le fichier journal ne sont pas en cours d'exécution.
{.is-danger}

Lorsque vous demandez de l'aide, assurez-vous de lire [demande d'aide](#demande-d-aide) afin de pouvoir nous fournir les détails dont nous aurons besoin.

## Test du client de téléchargement

Assurez-vous que votre(des) client(s) de téléchargement est(sont) en cours d'exécution. Commencez par tester le client de téléchargement, s'il ne fonctionne pas, vous pourrez voir les détails dans les journaux de niveau trace. Vous devriez trouver une URL que vous pouvez entrer dans votre navigateur pour voir si cela fonctionne. Il peut s'agir d'un problème de connexion, ce qui pourrait indiquer une mauvaise adresse IP, un nom d'hôte, un port ou même un pare-feu bloquant l'accès. Cela peut être évident, comme un problème d'authentification où vous avez mal saisi le nom d'utilisateur, le mot de passe ou la clé API. Notez que certaines seedbox nécessitent l'utilisation de HTTPS, du port 443 et d'une URL de base (options avancées), au lieu du port réel de votre client de téléchargement.

## Test d'un téléchargement

Maintenant, nous allons essayer un téléchargement, choisissez un film et effectuez une recherche manuelle. Choisissez l'un de ces fichiers et essayez de le télécharger. Est-il envoyé au client de téléchargement ? Se retrouve-t-il dans la bonne catégorie ? Apparaît-il dans l'activité ? Apparaît-il dans les journaux de niveau trace pendant les tâches **Vérifier les téléchargements terminés** (Rafraîchir les téléchargements surveillés et Traiter les téléchargements surveillés) qui s'exécutent environ toutes les minutes ? Est-il correctement analysé pendant cette tâche ? Le téléchargement en attente a-t-il un nom raisonnable ? Étant donné que les recherches se font par ID sur certains indexeurs/trackers, il peut en mettre un en file d'attente avec un nom qu'il ne peut pas reconnaître.

## Test d'une importation

Les problèmes d'importation se manifestent presque toujours par un élément dans l'activité avec une icône orange sur laquelle vous pouvez survoler pour voir l'erreur. S'ils n'apparaissent pas dans l'activité, c'est le problème sur lequel vous devez vous concentrer en premier, alors revenez en arrière et résolvez-le. La plupart des erreurs d'importation sont des problèmes de *permissions*, n'oubliez pas que doit être en mesure de lire et d'écrire dans le dossier de téléchargement. Parfois, les permissions dans le dossier de la bibliothèque peuvent également être en cause, alors assurez-vous de vérifier les deux.

Il est également possible que des problèmes de chemin incorrect se produisent, bien que cela soit moins courant dans les configurations normales. La clé pour comprendre les problèmes de chemin est de savoir que récupère le chemin du téléchargement *à partir* du client de téléchargement, via son API. Cela pose problème dans des cas d'utilisation plus spécifiques, comme lorsque le client de téléchargement s'exécute sur un système différent (voire même un système d'exploitation différent\!). Cela peut également se produire dans une configuration Docker, lorsque les volumes ne sont pas bien configurés. Une correspondance de chemin distant est une bonne solution lorsque vous n'avez pas le contrôle, comme dans une configuration de seedbox. Dans une configuration Docker, il est préférable de corriger les chemins.

## Problèmes courants

Voici quelques problèmes courants.

### L'interface Web du client de téléchargement n'est pas activée

Radarr communique avec votre client de téléchargement via son API et y accède via l'interface Web du client. Vous devez vous assurer que l'interface Web du client est activée et que le port qu'elle utilise ne rentre pas en conflit avec d'autres ports utilisés par d'autres clients ou par votre système.

### SSL activé et mal configuré

Assurez-vous que le chiffrement SSL n'est pas activé si vous utilisez à la fois votre instance et votre client de téléchargement sur un réseau local. Consultez [l'entrée de FAQ sur les certificats invalides et autres problèmes HTTPS ou SSL](/radarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) pour plus d'informations.

### Impossible de voir le partage sur Windows

L'utilisateur par défaut pour un service Windows est `LocalService`, qui n'a généralement pas accès à vos partages. Modifiez le service et configurez-le pour qu'il s'exécute en tant qu'utilisateur propre, consultez l'entrée de FAQ [pourquoi je ne peux pas voir mes fichiers sur un serveur distant](/radarr/faq#why-cant-i-see-my-files-on-a-remote-server) pour plus de détails.

### Les lecteurs réseau mappés ne sont pas fiables

Bien que les lecteurs réseau mappés comme `X:\` soient pratiques, ils ne sont pas aussi fiables que les chemins UNC comme `\\serveur\partage` et ils ne sont pas disponibles avant la connexion. Configurez votre client de téléchargement et vos clients de téléchargement de manière à utiliser les chemins UNC si nécessaire. Si votre bibliothèque se trouve sur un partage, assurez-vous que vos dossiers racines utilisent des chemins UNC. Si votre client de téléchargement envoie vers un partage, c'est là que vous devrez configurer des chemins UNC, car récupère le chemin de téléchargement à partir du client de téléchargement. Il est possible de conserver vos lecteurs réseau mappés pour votre propre utilisation, mais ne les utilisez pas pour l'automatisation.

### Docker et utilisateur, groupe, propriété, permissions et chemins

Docker ajoute une autre couche de complexité qui est facile à mal configurer, mais qui peut quand même fonctionner, mais avec divers problèmes. Au lieu de les passer en revue ici, lisez cet article du wiki [pour ces logiciels d'automatisation et Docker](/docker-guide) qui traite de l'utilisateur, du groupe, de la propriété, des permissions et des chemins. Il n'est pas spécifique à un système Docker particulier, mais il passe en revue les choses de manière générale afin que vous puissiez les mettre en œuvre dans votre propre environnement.

### Correspondance de chemin distant

Si vous avez Radarr dans Docker et le client de téléchargement en dehors de Docker (ou vice versa) ou si les programmes sont sur différents serveurs, vous devrez peut-être utiliser une correspondance de chemin distant.

Les journaux indiqueront quelque chose de similaire à ceci.

```none
2022-02-03 14:03:54.3|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /volume3/data/torrents/movies/The.Orville.2022.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Ainsi, `/volume3/data` n'existe pas dans le conteneur de Radarr ou n'est pas accessible.

- [Paramètres => Clients de téléchargement => Correspondances de chemin distant](/radarr/settings#remote-path-mappings)
- Une correspondance de chemin distant est utilisée lorsque votre client de téléchargement signale un chemin pour les données terminées soit sur un autre serveur, soit d'une manière que \*Arr n'adresse pas ce dossier.
- En général, une correspondance de chemin distant n'est nécessaire que si votre client de téléchargement est sous Linux lorsque \*Arr est sous Windows ou vice versa. Une correspondance de chemin distant peut également être nécessaire si vous mélangez des clients Docker et natifs ou si vous utilisez un serveur distant.
- Une correspondance de chemin distant est une recherche/remplacement STUPIDE (où elle trouve la valeur DISTANTE, la remplace par la valeur LOCALE pour l'hôte spécifié).
- Si le message d'erreur concernant un mauvais chemin ne contient pas la valeur REMPLACÉE, alors la correspondance de chemin ne fonctionne pas comme vous le souhaitez. La solution typique consiste à ajouter et supprimer la correspondance.
- [Consultez le tutoriel de TRaSH pour des informations supplémentaires sur la correspondance de chemin distant](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Si à la fois \*Arr et votre client de téléchargement sont des conteneurs Docker, il est rare qu'une correspondance de chemin distant soit nécessaire. Il est recommandé de [revoir le guide Docker](/docker-guide) et/ou de [suivre le tutoriel de TRaSH](https://trash-guides.info/hardlinks)
{.is-info}

#### Montage distant ou synchronisation distante (Syncthing)

- Vous devez le synchroniser pendant toute la durée du téléchargement. Et vous devez pouvoir créer des liens physiques dans la destination de synchronisation locale lorsque \*Arr importe, ce qui signifie le même système de fichiers et une apparence similaire.
  - Synchronisez dans un dossier inférieur et commun qui contient à la fois les fichiers incomplets et les fichiers complets.
  - Synchronisez vers un emplacement qui se trouve sur le même système de fichiers localement que votre bibliothèque et qui lui ressemble (Docker et les partages réseau facilitent la mauvaise configuration de cela)
  - Vous voulez synchroniser les fichiers incomplets et complets afin que lorsque le client de torrent effectue le déplacement, cela soit reflété localement et que tous les fichiers soient déjà "là" (même s'ils sont toujours en cours de téléchargement). Ensuite, vous voulez utiliser des liens physiques car même s'ils sont importés avant d'être terminés, ils finiront quand même.
  - De cette façon, pendant tout le téléchargement, il est synchronisé, puis le client de torrent déplace vers le sous-dossier tv et la synchronisation le reflète. De cette façon, les téléchargements sont presque terminés lorsqu'ils sont déclarés terminés. Et même s'ils ne sont pas totalement terminés, le fait que le lien physique soit possible signifie que c'est toujours bon.
  - (Facultatif - si applicable et/ou requis (par exemple, client usenet distant)) Configurez un script personnalisé à exécuter lors de l'importation/téléchargement/mise à niveau pour supprimer le fichier distant
- Alternativement, un montage distant plutôt qu'une configuration de synchronisation distante est beaucoup moins compliqué à configurer, mais généralement plus lent.
  - Montez votre stockage distant avec sshfs ou un autre protocole de système de fichiers réseau
  - Assurez-vous que l'utilisateur et le groupe sous lesquels \*Arr est configuré pour s'exécuter ont un accès en lecture ou en écriture.
  - Configurez une correspondance de chemin distant pour trouver le chemin DISTANT et le remplacer par l'équivalent LOCAL

### Permissions sur le dossier de la bibliothèque

Les journaux ressembleront à ceci

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/media/Movie Name (2010). Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

N'oubliez pas de vérifier les permissions et la propriété de la *destination*. Il est facile de se concentrer sur la propriété et les permissions du téléchargement et c'est *généralement* la cause des problèmes liés aux permissions, mais cela *pourrait* être la destination également. Vérifiez que le(s) dossier(s) de destination existe(nt). Vérifiez qu'un fichier de destination n'existe pas déjà ou ne peut pas être supprimé ou déplacé vers la corbeille. Vérifiez que la propriété et les permissions permettent de copier, de créer des liens physiques ou de déplacer le fichier téléchargé. L'utilisateur ou le groupe sous lequel s'exécute doit être en mesure de lire et d'écrire dans le dossier racine.

- Pour les utilisateurs de Windows, cela peut être dû à l'exécution en tant que service :
  - le service Windows s'exécute sous le compte 'Local Service', par défaut ce compte n'a pas les permissions pour accéder au répertoire personnel de votre utilisateur à moins que les permissions n'aient été attribuées manuellement. Cela est particulièrement pertinent lorsque vous utilisez des clients de téléchargement configurés pour télécharger dans votre répertoire personnel.
  - 'Local Service' a également généralement des permissions très limitées. Il est donc conseillé d'installer l'application en tant qu'application de la barre d'état système si l'utilisateur peut rester connecté. L'option pour le faire est fournie lors de l'installation. Consultez la FAQ pour savoir comment passer d'un service à une application de la barre d'état système.

- Pour les utilisateurs de Synology, consultez [l'article sur les permissions de SynoCommunity pour leurs packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Non-Windows : Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
- Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.

### Permissions sur le dossier de téléchargement

Les journaux ressembleront à ceci

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/downloads/The.Movie. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

N'oubliez pas de vérifier les permissions et la propriété de la *source*. Il est facile de se concentrer sur la propriété et les permissions de la destination et c'est une cause *possible* de problèmes liés aux permissions, mais c'est généralement la source. Vérifiez que le(s) dossier(s) source existe(nt). Vérifiez que la propriété et les permissions permettent de copier/créer des liens physiques ou de copier+supprimer/déplacer le fichier. L'utilisateur ou le groupe sous lequel s'exécute doit être en mesure de lire et d'écrire dans le dossier de téléchargement.

- Pour les utilisateurs de Windows, cela peut être dû à l'exécution en tant que service :
  - le service Windows s'exécute sous le compte 'Local Service', par défaut ce compte n'a pas les permissions pour accéder au répertoire personnel de votre utilisateur à moins que les permissions n'aient été attribuées manuellement. Cela est particulièrement pertinent lorsque vous utilisez des clients de téléchargement configurés pour télécharger dans votre répertoire personnel.
  - 'Local Service' a également généralement des permissions très limitées. Il est donc conseillé d'installer l'application en tant qu'application de la barre d'état système si l'utilisateur peut rester connecté. L'option pour le faire est fournie lors de l'installation. Consultez la FAQ pour savoir comment passer d'un service à une application de la barre d'état système.

- Pour les utilisateurs de Synology, consultez [l'article sur les permissions de SynoCommunity pour leurs packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Non-Windows : Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
- Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.

### Le dossier de téléchargement et le dossier de la bibliothèque ne sont pas des dossiers différents

- Le client de téléchargement doit télécharger dans un dossier accessible par \*Arr et qui n'est pas votre dossier racine/bibliothèque ; il doit importer depuis ce dossier de téléchargement séparé dans votre dossier de bibliothèque.
- Vous ne devez jamais télécharger directement dans votre dossier racine. Vous ne devez pas non plus utiliser votre dossier racine comme dossier de téléchargement complet ou dossier de téléchargement incomplet de votre client de téléchargement.
- [**Cela provoquera également une vérification de l'état de santé dans le système**](/radarr/system#downloading-into-root-folder)
- Dans l'application, un dossier racine est défini comme le dossier de bibliothèque multimédia configuré. Il ne s'agit pas du dossier racine d'un montage. Votre client de téléchargement a un dossier incomplet ou complet (ou déplace les téléchargements terminés) dans votre dossier racine (bibliothèque). Cela cause fréquemment des problèmes et n'est pas recommandé. Pour résoudre ce problème, modifiez votre client de téléchargement afin qu'il ne place pas les téléchargements dans votre dossier racine. Notez que 'placer' inclut également si la catégorie de votre client de téléchargement est définie sur votre dossier racine ou si NZBGet/SABnzbd a la fonction de tri activée et trie vers votre dossier racine. Veuillez noter que cette vérification examine tous les dossiers racines définis/configurés ajoutés, pas seulement les dossiers racines actuellement utilisés. En d'autres termes, le dossier dans lequel votre client de téléchargement télécharge ou déplace les téléchargements terminés ne doit pas être le même dossier que vous avez configuré comme dossier racine/bibliothèque/destination finale des médias dans l'application \*Arr.
- Les dossiers racines configurés (alias dossiers de bibliothèque) peuvent être trouvés dans [Paramètres => Gestion des médias => Dossiers racines](/radarr/settings/#root-folders)
- Un exemple est si vos téléchargements vont dans `\data\downloads` puis vous avez un dossier racine défini comme `\data\downloads`.
- Il est recommandé d'utiliser des chemins comme `\data\media\` pour votre dossier racine/bibliothèque et `\data\downloads\` pour vos téléchargements.

> Votre dossier de téléchargement et votre dossier racine/bibliothèque DOIVENT être séparés
{.is-warning}

### Catégorie incorrecte

Radarr doit être configuré pour utiliser une catégorie afin de ne traiter que ses propres téléchargements. Il est rare qu'un torrent soumis par soit ajouté sans la catégorie correcte, mais cela peut arriver. Si vous ajoutez manuellement des torrents et que vous souhaitez les traiter, ils devront avoir la catégorie correcte. Elle peut être définie à tout moment, car essaie de traiter les téléchargements toutes les minutes.

### Torrents compressés

Les journaux indiqueront des erreurs comme

```none
No files found are eligible for import
```

Si votre torrent est compressé dans des fichiers `.rar`, vous devrez configurer l'extraction. Nous recommandons [Unpackerr](https://github.com/unpackerr/unpackerr) car il fait l'extraction correctement : il empêche les imports partiels corrompus et nettoie les fichiers extraits après l'importation.

L'erreur peut également être visible s'il n'y a aucun fichier multimédia valide dans le dossier.

### Téléchargements répétés

Il existe plusieurs causes de téléchargements répétés, mais l'une d'entre elles est liée aux formats personnalisés. Il est possible que le nom de la version corresponde à un format personnalisé, mais pas les fichiers téléchargés. Cela crée une boucle où vous téléchargez les éléments encore et encore car ils semblent être une mise à niveau, puis ne le sont pas, puis réapparaissent et semblent être une mise à niveau, puis ne le sont pas. Selon votre format personnalisé, vous pouvez contourner ce problème en incluant le format personnalisé dans votre schéma de renommage. (Activez l'inclusion du format personnalisé dans le renommage, puis ajoutez le format personnalisé à votre schéma de renommage)

Cela peut également être dû au fait que le téléchargement n'est jamais importé et qu'il manque dans la file d'attente, de sorte qu'un nouveau téléchargement est constamment récupéré et jamais importé. Veuillez consulter les autres problèmes courants et les étapes de dépannage à cet égard.

### Le téléchargement Usenet ne parvient pas à s'importer

Radarr ne regarde que les 60 téléchargements les plus récents dans SABnzbd et NZBGet, donc si vous *gardez* votre historique, cela signifie que pendant les files d'attente importantes avec des problèmes d'importation, les téléchargements peuvent être manqués silencieusement et ne pas être importés. La meilleure façon d'éviter cela est de garder votre historique clair, de sorte que tous les éléments qui apparaissent encore nécessitent une enquête. Vous pouvez y parvenir en activant la suppression sous Completed and Failed Download Handler. Dans NZBGet, cela déplacera les éléments vers l'historique *caché*, ce qui est génial. Malheureusement, SABnzbd n'a pas de fonctionnalité similaire. Le mieux que vous puissiez réaliser là-bas est d'utiliser le dossier de sauvegarde nzb.

### Le client de téléchargement efface les éléments

Le client de téléchargement ne doit *pas* être responsable de la suppression des téléchargements. Les clients Usenet doivent être configurés pour *ne pas* supprimer les téléchargements de l'historique. Les clients de torrents doivent être configurés pour *ne pas* supprimer les torrents lorsqu'ils ont fini de partager (les mettre en pause ou les arrêter à la place). C'est parce que Radarr communique avec le client de téléchargement pour savoir quoi importer, donc s'ils sont *supprimés*, il n'y a rien à importer... même s'il y a un dossier rempli de fichiers.

Pour SABnzbd, cela est géré avec le paramètre History Retention.

### Le téléchargement ne peut pas être associé à un élément de bibliothèque

Pour diverses raisons, les versions ne peuvent pas être analysées une fois récupérées et envoyées au client de téléchargement. Activity => Options => Show Unknown (c'est maintenant activé par défaut dans les versions récentes) affiche tous les éléments non ignorés / déjà importés dans la catégorie du client de téléchargement de \*Arr. Ceux-ci devront généralement être mappés et importés manuellement.

Les raisons incluent :
- Le nom du film contient un `:` sur TMDb et TMDb n'a pas de titre alternatif avec un `-` ou avec un espace remplaçant le `:`
- Le nom du fichier ne contient pas l'année qui est requise
- AKA ou des noms multiples étranges ; Radarr a une prise en charge limitée pour ceux-ci
- Le nom du fichier correspond à plusieurs films
- Le nom de version ou l'ID de version de l'indexeur ne correspond pas au nom du fichier

Cela peut également se produire si vous avez une version dans votre client de téléchargement mais que cet élément multimédia (film/épisode/livre/chanson) n'existe pas dans l'application.

### La connexion sous-jacente a été fermée : une erreur inattendue s'est produite lors de l'envoi

Cela est dû à l'indexeur utilisant un protocole SSL non pris en charge par la version .NET actuelle trouvée dans [Radarr => Système => Statut](/radarr/system#status).

### La demande a expiré

Radarr ne reçoit aucune réponse du client.

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
- des problèmes IPv6 locaux - généralement, IPv6 est activé, mais non fonctionnel
- l'utilisation de Privoxy et une configuration incorrecte de celui-ci

## Problème non répertorié

Vous pouvez également consulter quelques commandes courantes de dépannage des autorisations et du réseau [dans notre guide](/permissions-and-networking). Sinon, veuillez discuter avec l'équipe d'assistance sur Discord. Si c'est quelque chose qui pourrait être un problème courant, veuillez suggérer de l'ajouter au wiki.

# Recherches, indexeurs et trackers

- Si vous utilisez [Prowlarr](/prowlarr), vous pouvez consulter l'[historique](/prowlarr/history) de toutes les requêtes reçues par Prowlarr et comment elles ont été envoyées aux sites. Assurez-vous que `Parameters` est activé dans Prowlarr History => Options. L'icône (i) fournit des détails supplémentaires.

## Augmenter le niveau de journalisation à la trace

> **La première étape consiste à augmenter le niveau de journalisation à Trace, consultez [Logging and Log Files](#logging-and-log-files) pour plus de détails sur l'ajustement de la journalisation et la recherche dans les journaux. Vous reproduirez ensuite le problème et utiliserez les journaux de niveau trace de cette période pour examiner le problème.** Si quelqu'un vous aide, mettez le contexte avant/après dans un [pastebin](https://0bin.net), [Gist](https://gist.com) ou un site similaire pour le leur montrer. Il n'est pas nécessaire de fournir l'intégralité du fichier et cela ne devrait pas se limiter à l'erreur. Vous devez également reproduire le problème lorsque des tâches qui inondent le fichier journal ne sont pas en cours d'exécution.
{.is-danger}

## Tester un indexeur ou un tracker

Lorsque vous testez un indexeur ou un tracker, dans les journaux de débogage ou de trace, vous pouvez trouver l'URL utilisée. Un exemple de test réussi est donné ci-dessous, vous pouvez voir qu'il interroge l'indexeur via une URL spécifique avec des paramètres spécifiques, puis la réponse. Vous pouvez tester cette URL dans votre navigateur en remplaçant `apikey=(removed)` par la bonne apikey comme `apikey=123`. Vous pouvez expérimenter avec les paramètres si vous obtenez une erreur de l'indexeur ou voir si vous avez des problèmes de connectivité s'il ne fonctionne pas du tout. Après avoir testé dans votre propre navigateur, vous devriez tester à partir du système sur lequel il s'exécute *si* vous ne l'avez pas déjà fait.

## Tester une recherche

Tout comme le test d'indexeur/tracker ci-dessus, lorsque vous déclenchez une recherche en utilisant les journaux de niveau Débogage ou Trace, vous pouvez obtenir l'URL utilisée à partir des fichiers journaux. Lors des tests, il est préférable d'utiliser une recherche aussi précise que possible. Une recherche manuelle est bonne car elle est spécifique et vous pouvez voir les résultats dans l'interface utilisateur tout en examinant les journaux.

Dans ce test, vous rechercherez des erreurs évidentes et effectuerez quelques tests simples. Vous pouvez voir que la recherche a utilisé l'URL `https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(removed)&q=O+Brother+Where+Art+Thou`, que vous pouvez essayer vous-même dans un navigateur après avoir remplacé `(removed)` par votre apikey pour cet indexeur. Est-ce que ça marche ? Voyez-vous les résultats attendus ? Dans cette URL, vous pouvez voir qu'elle a défini la catégorie spécifique de 2000, donc si vous ne voyez pas les résultats attendus, c'est une raison probable. Si le film n'est pas correctement catégorisé sur l'indexeur, il devra être corrigé. Consultez la sortie XML de la recherche manuelle ci-dessous pour voir un exemple de sortie de requête fonctionnelle.

- Sortie XML de la recherche manuelle

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(removed)&q=O+Brother+Where+Art+Thou" rel="self" type="application/rss+xml"/>
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
<newznab:response offset="0" total="17"/>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=e83b7ae75bca71e92367fab29b036731&apikey=(removed)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(removed)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=e83b7ae75bca71e92367fab29b036731</comments>
<pubDate>Sat, 10 Jul 2021 08:33:22 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(removed)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="e83b7ae75bca71e92367fab29b036731"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=c00a92567863801ab1a4901458ae31ba&apikey=(removed)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(removed)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=c00a92567863801ab1a4901458ae31ba</comments>
<pubDate>Sun, 28 Mar 2021 10:50:38 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(removed)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="c00a92567863801ab1a4901458ae31ba"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=75f5be8b4cd573c2359b638350689f73&apikey=(removed)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(removed)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=75f5be8b4cd573c2359b638350689f73</comments>
<pubDate>Sun, 28 Jul 2019 00:46:00 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(removed)" length="936738000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="936738000"/>
<newznab:attr name="guid" value="75f5be8b4cd573c2359b638350689f73"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(removed)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(removed)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=a0fe801d9ba0a703db7d2164e996aa1f</comments>
<pubDate>Mon, 14 Aug 2017 15:34:36 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(removed)" length="9746182000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="9746182000"/>
<newznab:attr name="guid" value="a0fe801d9ba0a703db7d2164e996aa1f"/>
</item>
</channel>
</rss>
```

***Images nécessaires***

![searches-indexers-and-trackers1.png](/assets/radarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/radarr/searches-indexers-and-trackers2.png)

- Extrait du journal de trace

```none
Extrait du journal de trace pour une recherche manuelle nécessaire
```

- Journal de trace complet d'une recherche

```none
Section complète du journal de trace pour une recherche manuelle nécessaire
```

## Problèmes courants

Voici quelques problèmes courants.

### L'indexeur nécessite des capacités de recherche brutes

- Radarr recherche `Kikis Delivery Service` mais votre indexeur n'a que des résultats pour `Kiki's Delivery Service`
- Cela est dû à votre indexeur qui ne prend pas en charge les recherches normalisées standardisées.
- La solution est que les capacités de recherche de la définition de votre indexeur doivent être mises à jour pour indiquer qu'il [requiert et prend en charge `RawSearch`](https://github.com/Radarr/Radarr/issues/4502#issuecomment-981143905)
- Jackett prend en charge le drapeau, mais les capacités doivent être mises à jour pour chaque indexeur. Ouvrez une demande de fonctionnalité pour que Jackett ajoute cette fonctionnalité pour votre indexeur.
- Prowlarr prend en charge le drapeau, mais les capacités doivent être mises à jour pour chaque indexeur. Ouvrez une demande de fonctionnalité pour que Prowlarr ajoute cette fonctionnalité pour votre indexeur.

### Le média n'est pas surveillé

Le(s) film(s) n'est (ne sont) pas surveillé(s).

### Mauvaises catégories

Les catégories incorrectes sont probablement la cause la plus courante des résultats qui s'affichent lors de recherches manuelles sur un indexeur/tracker, mais pas dans Radarr. L'indexeur/tracker devrait afficher la catégorie dans les résultats de recherche, ce qui devrait vous aider à comprendre ce qui manque. Si vous utilisez Jackett ou Prowlarr, chaque tracker a une liste de catégories spécifiquement prises en charge. Assurez-vous d'utiliser les bonnes catégories pour Radarr. Beaucoup trouvent utile d'avoir la liste visible dans une fenêtre de navigateur pendant qu'ils modifient l'entrée.

### Requête réussie - Aucun résultat retourné

Vous recevez un message similaire à `Requête réussie, mais aucun résultat n'a été retourné par votre indexeur. Cela peut être un problème avec l'indexeur ou vos paramètres de catégorie d'indexeur.`

Cela est dû à votre indexeur qui ne renvoie aucun résultat correspondant aux catégories que vous avez configurées pour l'indexeur.

### Résultats incorrects

Parfois, les indexeurs renvoient des résultats totalement non pertinents. Radarr envoie des paramètres pour limiter la recherche, mais les résultats renvoyés sont totalement non pertinents. Ou parfois, principalement pertinents avec quelques résultats incorrects. Le premier cas est généralement un problème de l'indexeur et vous pourrez le déterminer à partir des journaux de trace. Vous pouvez désactiver cet indexeur et signaler le problème. L'autre cas concerne généralement des versions catégorisées qui peuvent être signalées sur l'indexeur/tracker.

### Résultats manquants

Si vous avez des résultats sur le site que vous ne voyez pas dans Radarr, alors votre problème est probablement l'une des possibilités suivantes :

- [Les catégories sont incorrectes - Voir ci-dessus](#wrong-categories)
- Une recherche basée sur un ID (IMDbId, TMDbId, etc.) est effectuée et l'indexeur n'a pas correctement associé les versions à cet ID. C'est quelque chose que seul votre indexeur peut résoudre. Ils doivent s'assurer que la version est associée aux bons IDs applicables.
- Vous ne recherchez pas de la même manière que Radarr. Il est fort probable que les termes que vous recherchez sur l'indexeur ne correspondent pas à la façon dont Radarr les interroge. Vous pouvez voir comment Radarr interroge dans les journaux de trace. Les requêtes basées sur du texte seront généralement au format `q=mots%20et%20choses%20ici`. Cette chaîne est encodée en HTTP et peut être facilement décodée à l'aide de tout outil de décodage/encodage HTML en ligne.
- [Consultez la FAQ pour savoir comment Radarr gère les films étrangers ou les titres étrangers](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

### Validation du certificat

Vous vous connecterez à la plupart des indexeurs/trackers via HTTPS, donc vous devez vous assurer que cela fonctionne correctement sur votre système. Cela signifie que votre fuseau horaire et votre heure doivent être réglés *correctement*. Cela signifie également que vos certificats système doivent être à jour.

### Limites de taux atteintes

Si vous utilisez un VPN ou un proxy, vous pouvez être en concurrence avec des dizaines, des centaines ou des milliers d'autres personnes qui essaient toutes d'utiliser des services comme , theXEM et/ou vos indexeurs et trackers. La limitation du taux et la protection contre les attaques par déni de service (DDoS) sont souvent effectuées par adresse IP et votre point de sortie VPN/proxy correspond à *une* adresse IP. À moins que vous ne soyez dans un pays répressif comme la Chine, l'Australie ou l'Afrique du Sud, vous n'avez pas besoin de VPN/proxy .

Rarbg a tendance à avoir une sorte de limitation du taux dans leur API et peut renvoyer aucune résultat.

### Interdiction IP

De même que les limites de taux, certains indexeurs - comme Nyaa - peuvent interdire complètement une adresse IP. Cela est généralement semi-permanent et la solution consiste à obtenir une nouvelle adresse IP auprès de votre fournisseur d'accès Internet (FAI) ou de votre fournisseur de VPN.

### Année ne correspond pas

- [Voir cette entrée de FAQ](/radarr/faq#how-does-radarr-determine-the-year-of-a-movie)
  - Radarr obtient les métadonnées de TMDb
  - Radarr utilise l'année de la plus ancienne date de **sortie en salle** et la plus ancienne date de **première** pour la correspondance
- Dans certains cas, le film a été repoussé ou déplacé et l'année utilisée par les groupes de versions ne correspond ni à l'année de la plus ancienne date de première ni à l'année de la plus ancienne date de sortie en salle. Dans ces situations, vous devez le télécharger et l'importer manuellement.

### Année manquante

Radarr ne téléchargera pas une version si le nom de la version ne contient pas d'année. Il s'agit d'une mauvaise version et ne peut être téléchargée que manuellement. C'est une chose courante à négliger lorsque vous essayez de comprendre pourquoi un film n'a pas été téléchargé comme prévu.

### Utilisation de l'endpoint Jackett /all

L'endpoint `/all` de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc nécessaire d'ajouter chaque tracker individuellement. Vous pouvez également envisager d'utiliser l'alternative Jackett & NZBHydra2 appelée [Prowlarr](/prowlarr).

[Même Jackett dit que /all devrait être évité et ne pas être utilisé.](https://github.com/Jackett/Jackett#aggregate-indexers)

L'utilisation de l'endpoint all n'a aucun avantage (à part une réduction de la charge de gestion), seulement des inconvénients :

- vous perdez le contrôle sur les paramètres spécifiques de l'indexeur (catégories, modes de recherche, etc.)
- mélanger les modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
- les catégories spécifiques à l'indexeur (\>= 100000) ne peuvent pas être utilisées.
- les indexeurs lents ralentiront le résultat global
- le nombre total de résultats est limité à 1000

L'ajout de chaque indexeur séparément permet d'ajuster finement les catégories pour chaque indexeur, ce qui peut poser problème avec l'endpoint `/all` si l'utilisation de la mauvaise catégorie provoque des erreurs sur certains trackers. Dans , chaque indexeur est limité à 1000 résultats si la pagination est prise en charge ou 100 si ce n'est pas le cas, ce qui signifie que plus vous ajoutez de trackers à Jackett, plus vous risquez de manquer de résultats. Enfin, si *un seul* des trackers dans `/all` renvoie une erreur,  le désactivera et vous n'obtiendrez plus aucun résultat.

### Utilisation de NZBHydra2 comme une seule entrée

Utiliser NZBHydra2 comme une seule entrée d'indexeur (c'est-à-dire 1 entrée NZBHydra2 dans Radarr pour de nombreux indexeurs dans NZBHydra2) plutôt que plusieurs (c'est-à-dire de nombreuses entrées NZBHydra2 dans Radarr pour de nombreux indexeurs dans NZBHydra2) présente les mêmes problèmes que ceux mentionnés ci-dessus avec l'endpoint `/all` de Jackett.

### Problème non répertorié

Vous pouvez également consulter certaines commandes courantes de dépannage des autorisations et du réseau [dans notre guide](/permissions-and-networking). Sinon, veuillez en discuter avec l'équipe de support sur Discord. Si c'est quelque chose qui pourrait être un problème courant, veuillez suggérer de l'ajouter au wiki.

## Erreurs

Voici quelques-unes des erreurs courantes que vous pouvez rencontrer lors de l'ajout d'un indexeur.

### La connexion sous-jacente a été fermée : Une erreur inattendue s'est produite lors de l'envoi

Cela est dû à l'indexeur utilisant un protocole SSL non pris en charge par la version .NET actuelle trouvée dans [Radarr => Système => État](/radarr/system#status).

### La demande a expiré

Radarr ne reçoit aucune réponse de l'indexeur.

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
- des problèmes DNS locaux - Essayez de passer à un autre fournisseur DNS
- des problèmes IPv6 locaux - généralement IPv6 est activé, mais non fonctionnel
- l'utilisation de Privoxy et une configuration incorrecte de celui-ci

### Problème non répertorié

Vous pouvez également consulter certaines commandes courantes de dépannage des autorisations et du réseau [dans notre guide](/permissions-and-networking). Sinon, veuillez en discuter avec l'équipe de support sur Discord. Si c'est quelque chose qui pourrait être un problème courant, veuillez suggérer de l'ajouter au wiki.