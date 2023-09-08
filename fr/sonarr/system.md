# Statut

## Santé

- Cette page contient une liste des erreurs de vérification de santé. Ces vérifications de santé sont effectuées périodiquement par Sonarr et lors de certains événements. Les avertissements et les erreurs résultants sont répertoriés ici pour donner des conseils sur la façon de les résoudre.

### Avertissements système

#### La version actuellement installée du .NET Framework est ancienne et non prise en charge

- Sonarr utilise le .NET Framework. Nous devons construire Sonarr en fonction de la version prise en charge la plus basse encore utilisée par nos utilisateurs. De temps en temps, nous augmentons la version avec laquelle nous construisons pour pouvoir utiliser de nouvelles fonctionnalités. Apparemment, vous n'avez pas appliqué les mises à jour Windows appropriées depuis un certain temps et vous devez mettre à niveau .NET pour pouvoir utiliser les nouvelles versions de Sonarr.

- La mise à niveau du .NET Framework est très simple sur Windows, bien qu'elle nécessite souvent un redémarrage.

#### La version actuellement installée du .NET Framework est prise en charge mais une mise à niveau est recommandée

- Sonarr utilise le .NET Framework. Nous devons construire Sonarr en fonction de la version prise en charge la plus basse encore utilisée par nos utilisateurs. La mise à niveau vers des versions plus récentes nous permet de construire contre des versions plus récentes et d'utiliser de nouvelles fonctionnalités du Framework.

- La mise à niveau du .NET Framework est très simple sur Windows, bien qu'elle nécessite souvent un

#### La version actuellement installée de Mono est ancienne et non prise en charge

- Sonarr v4 est écrit en .NET et v3 nécessitait Mono. Mono 5.20 est le minimum absolu pour Sonarr.
- La procédure de mise à niveau de Mono varie selon la plateforme.

> Mono n'est plus pris en charge à partir de la version 4.0 de Sonarr
{.is-warning}

#### La version actuellement installée de SQLite n'est pas prise en charge

- Sonarr stocke ses données dans une base de données SQLite. La bibliothèque SQLite3 installée sur votre système est trop ancienne. Sonarr nécessite au moins la version 3.9.0.

> Notez que Sonarr utilise `libSQLite3.so` qui peut être ou non contenu dans un package de mise à niveau SQLite3.
{.is-info}

#### Message du mainteneur du package

- Votre mainteneur de package a un message pour vous. Cela est contrôlé par votre mainteneur et non par Sonarr.

#### Une nouvelle mise à jour est disponible

- Réjouissez-vous, les développeurs ont publié une nouvelle mise à jour. Cela signifie généralement de nouvelles fonctionnalités géniales et des tas de bugs corrigés (n'est-ce pas ?). Apparemment, vous n'avez pas activé la mise à jour automatique, vous devrez donc trouver comment mettre à jour sur votre plateforme. Appuyer sur le bouton Installer sur la page Système => Mises à jour est probablement un bon point de départ.

> Cet avertissement n'apparaîtra pas si votre version actuelle a moins de 14 jours
{.is-info}

#### Impossible d'installer la mise à jour car le dossier de démarrage et/ou le dossier de l'interface utilisateur ne sont pas accessibles en écriture par l'utilisateur

{#cannot-install-update-because-UI-folder-is-not-writable-by-the-user}

{#cannot-install-update-because-startup-folder-is-not-writable-by-the-user}

Cela signifie que Sonarr ne pourra pas se mettre à jour. Vous devrez mettre à jour Sonarr manuellement ou définir les autorisations sur le répertoire de démarrage de Sonarr (le répertoire d'installation) pour permettre à Sonarr de se mettre à jour.

#### Impossible d'installer la mise à jour car le dossier de démarrage se trouve dans un dossier de translocation d'application

Dans macOS Sierra, Apple a ajouté une fonctionnalité de sécurité étrange appelée Translocation d'application (parfois appelée Randomisation du chemin de Gatekeeper), ce qui signifie qu'après avoir téléchargé une application, si vous ne déplacez pas l'application résultante quelque part (n'importe où !), avec le Finder (vous devez utiliser le Finder !), l'application sera exécutée comme si elle était située à un chemin choisi au hasard par le système.

#### La mise à jour ne sera pas possible pour éviter de supprimer les données de l'application lors de la mise à jour

Sonarr a détecté que le dossier AppData pour votre système d'exploitation est situé à l'intérieur du répertoire qui contient les binaires de Sonarr. Normalement, il s'agirait de C:\ProgramData pour Windows et ~/.config pour Linux.

Veuillez consulter Système => Info pour voir les répertoires AppData et de démarrage actuels.
Cela signifie que Sonarr ne pourra pas se mettre à jour sans risquer une perte de données.
Si vous êtes sous Linux, vous devrez probablement changer le répertoire personnel de l'utilisateur qui exécute Sonarr et copier le contenu actuel du répertoire ~/.config/Sonarr pour préserver votre base de données.

#### Échec de la résolution de l'adresse IP de l'hôte proxy configuré

Vérifiez vos paramètres de proxy et assurez-vous qu'ils sont corrects.
Assurez-vous que votre proxy est actif, en cours d'exécution et accessible.

#### Échec du test du proxy

Votre proxy configuré n'a pas réussi le test, vérifiez l'erreur HTTP fournie et/ou consultez les journaux pour plus de détails.

#### L'heure système est décalée de plus d'un jour

L'heure système est décalée de plus d'un jour. Les tâches planifiées peuvent ne pas s'exécuter correctement tant que l'heure n'est pas corrigée.
Vérifiez l'heure de votre système et assurez-vous qu'elle est synchronisée avec un serveur de temps fiable et précis.

#### Impossible de charger la bibliothèque MediaInfo

La bibliothèque MediaInfo n'a pas pu être chargée. Sonarr nécessite MediaInfo (`libmediainfo`) pour évaluer les attributs vidéo des fichiers.

#### Mono Legacy TLS activé

{#sonarr-mono-4.x-tls-workaround-still-enabled-consider-removing-mono_tls_provider-legacy-environment-option}

Le contournement Mono 4.x TLS est toujours activé, envisagez de supprimer l'option d'environnement MONO_TLS_PROVIDER=legacy.

### Clients de téléchargement

#### Aucun client de téléchargement n'est disponible

Un client de téléchargement correctement configuré et activé est requis pour que Sonarr puisse télécharger des médias. Étant donné que Sonarr prend en charge différents clients de téléchargement, vous devez déterminer celui qui correspond le mieux à vos besoins. Si vous avez déjà un client de téléchargement installé, vous devez le configurer pour l'utiliser et créer une catégorie. Voir Paramètres => Client de téléchargement.

#### Impossible de communiquer avec le client de téléchargement

Sonarr n'a pas pu communiquer avec le client de téléchargement configuré. Veuillez vérifier si le client de téléchargement est opérationnel et vérifier à nouveau l'URL. Cela peut également indiquer une erreur d'authentification.
Cela est généralement dû à un client de téléchargement mal configuré. Voici quelques points que vous pouvez vérifier :
L'adresse IP de vos clients de téléchargement, si elle est sur la même machine physique, il s'agit généralement de 127.0.0.1
Le numéro de port que votre client de téléchargement utilise, ces champs sont remplis avec le numéro de port par défaut, mais si vous l'avez modifié, vous devrez entrer le même numéro dans Sonarr.
Assurez-vous que le chiffrement SSL n'est pas activé si vous utilisez à la fois votre instance Sonarr et votre client de téléchargement sur un réseau local. Consultez la FAQ SSL pour plus d'informations.

#### Les clients de téléchargement ne sont pas disponibles en raison d'une défaillance

Un ou plusieurs de vos clients de téléchargement ne répondent pas aux demandes de Sonarr. Par conséquent, Sonarr a décidé d'arrêter temporairement l'interrogation du client de téléchargement selon son cycle normal d'une minute, qui est normalement utilisé pour suivre les téléchargements actifs et importer les téléchargements terminés. Cependant, Sonarr continuera à essayer d'envoyer des téléchargements au client, mais il est fort probable qu'il échouera.
Vous devriez inspecter Système => Journaux pour voir la raison des échecs.
Si vous n'utilisez plus ce client de téléchargement, désactivez-le dans Sonarr pour éviter les erreurs.

#### Activer la gestion des téléchargements terminés

- Sonarr nécessite la gestion des téléchargements terminés pour pouvoir importer les fichiers téléchargés par le client de téléchargement. Il est recommandé d'activer la gestion des téléchargements terminés.
(La gestion des téléchargements terminés est activée par défaut...)

#### Mauvaise correspondance du chemin distant Docker

- Cette erreur est généralement associée à des mauvais chemins Docker dans votre client de téléchargement ou Sonarr.

- Un exemple de cela serait :
  - Client de téléchargement : Chemin de téléchargement : /mnt/user/downloads:/downloads
  - Radarr : Chemin de téléchargement : /mnt/user/downloads:/data
- Dans cet exemple, le client de téléchargement place ses téléchargements dans /downloads et dit ensuite à Radarr, une fois qu'il a terminé, que le film terminé se trouve dans /downloads. Sonarr arrive ensuite et dit "D'accord, cool, je vais vérifier dans /downloads" Eh bien, à l'intérieur de Radarr, vous n'avez pas alloué un chemin /downloads, vous avez alloué un chemin /data, donc il affiche cette erreur.
- La solution la plus simple consiste à être CONSISTANT. Si vous utilisez un schéma dans votre client de téléchargement, utilisez-le partout.

- L'équipe Sonarr est très favorable à l'utilisation de /data.
  - Client de téléchargement : /mnt/user/data/downloads:/data/downloads
  - Radarr : /mnt/user/data:/data

- Maintenant, dans le client de téléchargement, vous pouvez spécifier où dans /data vous souhaitez placer vos téléchargements, cela varie en fonction du client, mais vous devriez pouvoir lui dire "Oui, client de téléchargement, placez mes fichiers dans." /data/torrents (ou usenet)/movies et comme vous avez utilisé /data dans Radarr, lorsque le client de téléchargement dit à Radarr qu'il a terminé, Radarr viendra et dira "Super, j'ai un /data et je peux aussi voir /torrents (ou usenet)/movies, tout va bien dans le monde."
- Il existe de nombreux bons guides : notre wiki [Guide Docker](/docker-guide) et le guide [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/) de TRaSH. Ces guides mettent l'accent sur les liens physiques et les déplacements instantanés (déplacements atomiques), mais le concept général des conteneurs et du fonctionnement de la correspondance des chemins est au cœur de ces discussions.

- Consultez [le guide de TRaSH sur la correspondance des chemins distants](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) pour plus d'informations.

#### Téléchargement dans le dossier racine

{#downloads-in-root-folder}

- Dans l'application, un dossier racine est défini comme le dossier de la bibliothèque multimédia configurée. Il ne s'agit pas du dossier racine d'un montage. Votre client de téléchargement télécharge des fichiers incomplets ou complets (ou déplace les téléchargements terminés) dans votre dossier racine (bibliothèque).
- Cela cause fréquemment des problèmes - y compris une perte de données - et ne doit pas être fait. Pour résoudre ce problème, modifiez votre client de téléchargement afin qu'il ne place pas les téléchargements dans votre dossier racine. Notez que « placer » inclut également si la catégorie de votre client de téléchargement est définie sur votre dossier racine ou si NZBGet/SABnzbd a activé le tri et trie vers votre dossier racine.
- Veuillez noter que cette vérification examine tous les dossiers racines définis/configurés ajoutés, et pas seulement les dossiers racines actuellement utilisés. En d'autres termes, le dossier dans lequel votre client de téléchargement télécharge ou déplace les téléchargements terminés ne doit pas être le même dossier que vous avez configuré comme dossier racine/bibliothèque/destination finale des médias dans l'application *arr.
- Les dossiers racines configurés (alias dossiers de bibliothèque) peuvent être trouvés dans [Paramètres => Gestion des médias => Dossiers racines](/sonarr/settings/#root-folders)
- Un exemple est si vos téléchargements vont dans `/data/downloads`, alors vous avez un dossier racine défini comme `/data/downloads`.
- Il est recommandé d'utiliser des chemins tels que `/data/media/` pour votre dossier racine/bibliothèque et `/data/downloads/` pour vos téléchargements.
- Consultez notre [Guide Docker](/docker-guide) et le guide [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/) de TRaSH pour plus d'informations sur la configuration correcte et optimale des chemins. Notez que les concepts s'appliquent aux conteneurs et aux non-conteneurs.

> Votre dossier de téléchargement où votre client de téléchargement place les téléchargements et votre dossier racine/bibliothèque DOIVENT être séparés. \*Arr importera le(s) fichier(s) du dossier de votre client de téléchargement dans votre bibliothèque. Le client de téléchargement ne doit rien déplacer ni télécharger dans votre bibliothèque.
{.is-warning}

#### Mauvais paramètres du client de téléchargement

- L'emplacement vers lequel votre client de téléchargement télécharge les fichiers pose problème. Vérifiez les journaux pour plus d'informations. Cela peut être dû à des autorisations ou à une tentative de passer de Windows à Linux ou de Linux à Windows sans une correspondance de chemin distant.

#### Mauvaise correspondance du chemin distant

- L'emplacement vers lequel votre client de téléchargement télécharge les fichiers pose problème. Vérifiez les journaux pour plus d'informations. Cela peut être dû à des autorisations ou à une tentative de passer de Windows à Linux ou de Linux à Windows sans une correspondance de chemin distant. Consultez [le guide de TRaSH sur la correspondance des chemins distants](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) pour plus d'informations.

#### Erreur de permissions

- Sonarr ou l'utilisateur sonarr qui l'exécute ne peut pas accéder à l'emplacement vers lequel votre client de téléchargement télécharge les fichiers. Il s'agit généralement d'un problème de permissions.

#### Le fichier distant a été supprimé avant la fin du traitement

- Un fichier accessible via une correspondance de chemin distant semble avoir été supprimé avant la fin du traitement.

#### Le chemin distant est utilisé et l'importation a échoué

- Consultez vos journaux pour plus d'informations ; consultez nos guides de dépannage

### Téléchargement dans le dossier racine

{#downloads-in-root-folder}

- Au sein de l'application, un dossier racine est défini comme le dossier de la bibliothèque multimédia configurée. Il ne s'agit pas du dossier racine d'un montage. Votre client de téléchargement place des téléchargements incomplets ou complets (ou déplace des téléchargements terminés) dans votre dossier racine (bibliothèque).
- Cela cause souvent des problèmes, y compris des pertes de données, et ne devrait pas être fait. Pour résoudre ce problème, modifiez votre client de téléchargement afin qu'il ne place pas les téléchargements dans votre dossier racine. Notez que « placer » inclut également si la catégorie de votre client de téléchargement est définie sur votre dossier racine ou si NZBGet/SABnzbd a la fonction de tri activée et trie vers votre dossier racine.
- Veuillez noter que cette vérification examine tous les dossiers racines définis/configurés ajoutés, pas seulement les dossiers racines actuellement utilisés. En d'autres termes, le dossier dans lequel votre client de téléchargement télécharge ou déplace les téléchargements terminés ne doit pas être le même dossier que celui que vous avez configuré comme dossier de destination finale de votre bibliothèque multimédia dans l'application *arr.
- Les dossiers racines configurés (également appelés dossiers de bibliothèque) peuvent être trouvés dans [Paramètres => Gestion des médias => Dossiers racines](/sonarr/settings/#root-folders)
- Un exemple est si vos téléchargements vont dans `/data/downloads`, alors vous avez un dossier racine défini comme `/data/downloads`.
- Il est conseillé d'utiliser des chemins tels que `/data/media/` pour votre dossier racine/bibliothèque et `/data/downloads/` pour vos téléchargements.
- Consultez notre [Guide Docker](/docker-guide) et le [Guide de TRaSH sur les liens durs et les déplacements instantanés (Atomic-Moves)](https://trash-guides.info/hardlinks/) pour plus d'informations sur la configuration correcte et optimale des chemins. Notez que les concepts s'appliquent à Docker et aux environnements non-Docker.

> Votre dossier de téléchargement où votre client de téléchargement place les téléchargements et votre dossier racine/bibliothèque DOIVENT être séparés. \*Arr importera le(s) fichier(s) du dossier du client de téléchargement dans votre bibliothèque. Le client de téléchargement ne doit déplacer ni télécharger quoi que ce soit dans votre bibliothèque.
{.is-warning}

#### La gestion des téléchargements terminés est désactivée

{#completedfailed-download-handling}

- Il est nécessaire d'utiliser la gestion des téléchargements terminés car elle offre une meilleure compatibilité avec la logique de décompression et de post-traitement de divers clients de téléchargement. Avec cela, Sonarr n'importera un téléchargement que lorsque le client de téléchargement le signalera comme prêt.
- Si la gestion des téléchargements terminés est désactivée :
  - Toutes les importations doivent être gérées manuellement
  - Cette vérification de l'état de santé persiste et ne peut pas être ignorée ou désactivée
  - Les épisodes seront toujours manquants dans Sonarr et pourront être récupérés indéfiniment
    - Les épisodes déplacés et renommés manuellement par l'utilisateur dans le dossier de la série dans le dossier de la bibliothèque de Sonarr seront éventuellement détectés par la recherche bihebdomadaire si leur nom est correct et ne seront donc plus manquants à ce moment-là.
  - L'utilisateur devra désactiver manuellement la surveillance ou configurer un script personnalisé On Grab pour désactiver la surveillance des épisodes.
  - FlexGet est probablement un meilleur outil pour votre cas d'utilisation si vous ne souhaitez pas utiliser les fonctionnalités de gestion de bibliothèque multimédia de Sonarr et que vous avez simplement besoin de quelque chose pour analyser les flux RSS et envoyer des versions au client de téléchargement.

> La gestion des téléchargements terminés ne fonctionne correctement que si le client de téléchargement et Sonarr sont sur la même machine, car elle obtient le chemin à importer directement à partir du client de téléchargement, sinon une correspondance à distance est nécessaire.
> La gestion des téléchargements terminés nécessite que Sonarr ait un accès en lecture et en écriture au répertoire de téléchargement terminé
{.is-warning}

### Indexeurs

#### Aucun indexeur disponible avec la recherche automatique activée, Sonarr ne fournira aucun résultat de recherche automatique

- En termes simples, vous n'avez aucun de vos indexeurs configurés pour autoriser les recherches automatiques.
Accédez à Paramètres > Indexeurs, sélectionnez un indexeur que vous souhaitez autoriser les recherches automatiques, puis cliquez sur Enregistrer.

#### Aucun indexeur disponible avec la synchronisation RSS activée, Sonarr ne récupérera pas automatiquement les nouvelles versions

{#no-indexers-available-with-rss-sync-enabled,-sonarr-will-not-grab-new-releases-automatically}
{#all-rss-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Sonarr utilise le flux RSS pour récupérer les nouvelles versions au fur et à mesure de leur sortie. [Consultez la FAQ pour plus d'informations](/sonarr/faq#how-does-sonarr-find-episodes)
- Pour corriger ce problème, accédez à Paramètres > Indexeurs, sélectionnez un indexeur que vous avez et activez la synchronisation RSS.

#### Aucun indexeur n'est activé

- Sonarr nécessite des indexeurs pour pouvoir découvrir de nouvelles versions. Tous vos indexeurs sont désactivés ou vous n'avez ajouté aucun indexeur.

#### Les indexeurs activés ne prennent pas en charge la recherche

{#all-search-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Aucun des indexeurs que vous avez activés et disponibles ne prend en charge la recherche. Cela signifie que Sonarr ne pourra trouver de nouvelles versions que via les flux RSS. Mais la recherche de séries (qu'il s'agisse de la recherche automatique ou manuelle) ne renverra jamais de résultats. La seule façon de remédier à cela est d'ajouter un autre indexeur.

#### Aucun indexeur disponible avec la recherche interactive activée

{#no-indexers-available-with-interactive-search-enabled-sonarr-will-not-provide-any-interactive-search-results}

- Aucun des indexeurs que vous avez activés et disponibles ne prend en charge la recherche interactive. Cela signifie que l'application ne pourra trouver de nouvelles versions que via les flux RSS ou une recherche automatique.

#### Les indexeurs ne sont pas disponibles en raison d'échecs

- Des erreurs se produisent lorsque Sonarr essaie d'utiliser l'un de vos indexeurs. Pour limiter les nouvelles tentatives, Sonarr n'utilisera pas l'indexeur pendant une durée de plus en plus longue (jusqu'à 24 heures).
- Ce mécanisme est déclenché si Sonarr n'a pas pu obtenir de réponse de l'indexeur (cela peut être dû à un problème DNS, de connexion proxy/VPN, d'authentification ou d'indexeur), ou s'il n'a pas pu récupérer le fichier nzb/torrent de l'indexeur. Veuillez consulter les journaux pour déterminer quel type d'erreur a causé le problème.
- Vous pouvez éviter cet avertissement en désactivant l'indexeur concerné.
- Exécutez un `Test` sur l'indexeur pour forcer Sonarr à vérifier à nouveau l'indexeur ; veuillez noter que l'avertissement de vérification de l'état de santé ne disparaîtra pas toujours immédiatement et vous devrez peut-être exécuter la tâche `Check Health`

#### Tous les indexeurs utilisent l'endpoint All de Jackett

- L'endpoint /all de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes potentiels, il est donc maintenant nécessaire d'ajouter chaque tracker individuellement.
- [Même les développeurs de Jackett disent qu'il devrait être évité et ne pas être utilisé.](https://github.com/Jackett/Jackett#aggregate-indexers)
- L'utilisation de l'endpoint /all n'a aucun avantage, seulement des inconvénients :
  - vous perdez le contrôle sur les paramètres spécifiques de l'indexeur (catégories, modes de recherche, etc.)
  - la combinaison de modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
  - les catégories spécifiques de l'indexeur (\>= 100000) ne peuvent pas être utilisées.
  - les indexeurs lents ralentiront le résultat global
  - le nombre total de résultats est limité à 1000
  - si l'un des trackers dans /all renvoie une erreur, \*Arr le désactivera et vous n'obtiendrez plus aucun résultat.

##### Solutions

- Ajoutez chaque tracker dans Jackett manuellement en tant qu'indexeur dans \*Arr
- Consultez [Prowlarr](/prowlarr) qui peut synchroniser les indexeurs avec \*Arr et qui provient de l'équipe de développement de Lidarr/Radarr/Readarr.
- Consultez [NZBHydra2](https://github.com/theotherp/nzbhydra2) qui peut synchroniser les indexeurs avec \*Arr. Mais n'utilisez pas leur endpoint unique et utilisez `multi` si la synchronisation est utilisée.

### Médias et listes

#### Série(s) supprimée(s) de TheTVDB

- La ou les séries concernées ont été supprimées de [The TVDb](https://thetvdb.com). Cela se produit généralement parce que la série est en double ou est considérée comme faisant partie d'une autre série. Alternativement, TVDb peut la considérer comme une série ; espérons que TMDb le fasse également afin que [Radarr](/radarr) puisse être utilisé à la place. Pour corriger cela, vous devrez supprimer la ou les séries concernées et ajouter la série correcte si applicable.

#### Les listes ne sont pas disponibles en raison d'échecs

{#import-lists-are-unavailable-due-to-failures}

- En général, cela signifie simplement que Sonarr n'est plus en mesure de communiquer via l'API ou en se connectant à votre fournisseur de listes choisi. Si le problème persiste, il est préférable de les contacter pour les exclure, car leurs systèmes peuvent être surchargés de temps en temps.
- Consultez Système => Événements filtrés pour les avertissements (avertissements et erreurs) pour voir les échecs historiques ou consultez les journaux pour plus de détails.

#### Liste d'importation sans dossier racine

- Une ou plusieurs de vos listes d'importation sont configurées avec un dossier racine inaccessible à Sonarr.
- Cela peut être dû à des problèmes de permissions, à un montage manquant ou simplement à la nécessité de mettre à jour les listes après avoir réorganisé votre configuration.

#### Dossier racine manquant

- Un dossier racine est ajouté à Sonarr et n'existe pas ou n'est pas accessible
- Cette erreur est généralement identifiée si une série recherche un dossier racine mais que ce dossier racine n'est plus disponible.
- Cette erreur peut également se produire si une liste est toujours pointée vers un dossier racine mais que ce dossier racine n'est plus disponible.
- Si vous souhaitez supprimer cet avertissement, il vous suffit de trouver la série qui utilise toujours l'ancien dossier racine et de l'éditer pour lui attribuer le dossier racine correct.

- La manière la plus simple de trouver la série posant problème est de :

  - Aller à l'onglet Mass Editor
  - Créer un filtre personnalisé avec le chemin de l'ancien dossier racine
  - Sélectionner l'édition en masse dans la barre supérieure et dans la liste déroulante Root Paths, sélectionner le nouveau chemin racine vers lequel vous souhaitez déplacer ces séries.
  - Ensuite, vous recevrez une fenêtre contextuelle indiquant Souhaitez-vous déplacer les dossiers de la série vers 'chemin racine' ? Cela indiquera également Cela renommera également le dossier de la série selon le format de dossier de série dans les paramètres. Sélectionnez simplement Non si vous ne souhaitez pas que Lidarr déplace vos fichiers.
  - Exécutez la tâche Check Health dans Système => Tâches

#### Le point de montage du chemin de la série est en lecture seule

{#series-mount-ro}

Un point de montage contenant un chemin de série est en lecture seule et n'est pas accessible en écriture par l'utilisateur sous lequel Sonarr s'exécute.

## Espace disque

- Cette section vous montrera l'espace disque disponible
- Dans Docker, cela peut être délicat car il affiche généralement l'espace disponible dans votre image Docker.

## À propos

- Cela vous donnera des informations sur votre installation actuelle de Sonarr.

## Plus d'informations

- Page d'accueil : [page d'accueil de Sonarr](https://www.sonarr.tv)
- Wiki : Vous êtes déjà ici.
- Reddit : [r/sonarr](https://www.reddit.com/r/sonarr)
- Discord : Rejoignez notre [discord](https://discord.sonarr.tv/)
- Dons : Si vous êtes généreux et souhaitez faire un don, cliquez [ici](https://sonarr.tv/donate).
- Source : [GitHub](https://www.github.com/sonarr/sonarr)
- Demandes de fonctionnalités : Vous avez une excellente idée, partagez-la [ici](https://www.github.com/sonarr/sonarr/issues).

# Tâches

## Planifiées

- Cette section répertorie toutes les tâches planifiées exécutées par Sonarr

- Vérification de la mise à jour de l'application - Cette tâche s'exécute selon la planification affichée dans l'interface utilisateur, vérifiant si Sonarr est à la version la plus récente, puis déclenchant le script de mise à jour pour mettre à jour Sonarr. Paramètres => Mise à jour

> Remarque : Si vous utilisez Docker, cela ne mettra pas à jour votre conteneur car une nouvelle image devra être téléchargée.
{.is-warning}

- Sauvegarde - Cette tâche effectuera une sauvegarde de la base de données de votre Sonarr selon une planification définie. Vous trouverez plus de détails à ce sujet ici. Vous trouverez plus d'informations sur les sauvegardes dans Système => Sauvegardes.
- Vérification de l'état de santé - La vérification de l'état de santé s'exécute selon la planification affichée dans l'interface utilisateur, vérifiant la santé globale de votre Sonarr. Pour voir une liste des problèmes de santé possibles, consultez l'entrée Wiki sur les vérifications de l'état de santé.
- Nettoyage de la corbeille - La corbeille sera vidée selon la planification affichée dans l'interface utilisateur. Cela ne sera utilisé que si la corbeille est définie dans la gestion des fichiers.
- Maintenance - Selon la planification affichée dans l'interface utilisateur, cela dépoussière les toiles d'araignée, balaye et aspire les sols, lave, fait briller et même fait de jolis petits mots pliés rien que pour vous. Mais il ne sort pas les poubelles. Il n'est tout simplement pas assez bien payé pour ça.
- Synchronisation de la liste d'importation - Selon la planification affichée dans l'interface utilisateur, cela exécutera vos listes et importera toutes les nouvelles séries possibles. Plus d'informations sur les listes peuvent être trouvées dans Paramètres => Listes.
- Nettoyage des messages - Selon la planification affichée dans l'interface utilisateur, cela nettoie les messages qui apparaissent dans le coin inférieur gauche de Sonarr
- Actualiser les téléchargements surveillés - Cela passe en revue et actualise la file de téléchargements située sous Activité. Il s'agit essentiellement de vérifier auprès de votre client de téléchargement les téléchargements terminés.
- Actualiser les séries - Cela passe en revue et actualise toutes les métadonnées de toutes les séries surveillées et non surveillées
- Synchronisation RSS - Cela exécutera la synchronisation RSS. Cela peut être modifié dans Paramètres => Indexeurs => Options. Plus d'informations sur la fonctionnalité RSS peuvent être trouvées dans notre [FAQ](/sonarr/faq)
  
> Toutes ces tâches peuvent être exécutées manuellement en dehors de leurs horaires prévus en cliquant sur l'icône à l'extrême droite de chaque tâche.
{.is-info}

## File d'attente

La file d'attente vous montrera les tâches en cours et à venir, ainsi qu'un historique des tâches récemment exécutées et la durée de ces tâches.

# Sauvegarde

> Si vous souhaitez savoir comment sauvegarder/restaurer votre instance Sonarr, cliquez [ici](/sonarr/faq).
{.is-info}

Dans la section Sauvegarde, vous verrez les sauvegardes précédentes (sauf si vous avez une nouvelle installation qui n'a effectué aucune sauvegarde).
  
- Sauvegarder maintenant - Cette option déclenchera une sauvegarde manuelle de la base de données de votre Sonarr
- Restaurer une sauvegarde - Cela ouvrira un nouvel écran pour restaurer à partir d'une sauvegarde précédente
  - En sélectionnant Choisir un fichier, cela ouvrira une boîte de dialogue dans votre navigateur pour restaurer à partir d'une sauvegarde Zip de Sonarr
  
- Si vous avez des sauvegardes précédentes et que vous souhaitez les télécharger depuis Sonarr pour les placer dans un emplacement non standard, vous pouvez simplement sélectionner l'un de ces fichiers pour les télécharger
- À droite de chacun des téléchargements précédents, vous avez deux options.

  - Restaurer (Icône de l'horloge) - Pour restaurer à partir d'une sauvegarde précédente - Cela ouvrira une nouvelle fenêtre pour confirmer que vous souhaitez restaurer à partir de cette sauvegarde
  - Supprimer (Icône de la corbeille) - Pour supprimer une sauvegarde précédente

# Mises à jour

L'écran des mises à jour affichera les 5 dernières mises à jour effectuées ainsi que la version actuelle que vous utilisez.
Cette page affichera également les notes de mise à jour des développeurs vous indiquant ce qui a été corrigé ou ajouté à Sonarr (Réjouissez-vous !)
  
> Une version de maintenance contient des corrections de bugs et diverses améliorations. Consultez l'historique des commits sur Github pour plus de détails.
{.is-info}

# Événements

L'onglet Événements vous montrera ce qui s'est passé dans votre Sonarr. Cela peut être utilisé pour diagnostiquer certains problèmes légers. Cependant, cela ne remplace pas les journaux de trace discutés dans la section Logging.

> Les événements sont l'équivalent des journaux INFO. {.is-info}

- Composants - Cette colonne vous indiquera quel composant de Sonarr a été déclenché
- Message - Cette colonne vous indiquera quel message a été envoyé par le composant de la colonne précédente.
- Icône d'engrenage - Cette option vous permet de modifier le nombre de composants/messages affichés par page (la valeur par défaut est de 50)
- Options en haut de la page
  - Actualiser - Cette option actualisera la page actuelle, en récupérant un nouveau journal des événements
  - Effacer - Cela effacera le journal des événements actuel, vous permettant de repartir à zéro

# Fichiers journaux

- Cette page vous permet de télécharger et de voir les fichiers journaux actuellement disponibles pour Sonarr.

- Sur la première ligne, vous trouverez plusieurs options pour vous permettre de contrôler vos fichiers journaux.

- La première ligne tout à gauche comporte une liste déroulante qui vous permet de passer des fichiers journaux aux fichiers journaux de mise à jour
  - Fichiers journaux - L'essentiel de tout problème de support, vous trouverez plus d'informations sur les fichiers journaux ici.
  - Fichiers journaux de mise à jour - Cela affichera les fichiers journaux associés au script de mise à jour de Sonarr

> Si vous utilisez Docker, cela sera vide car vous devriez mettre à jour en téléchargeant une nouvelle image Docker.
{.is-info}

- Actualiser - Cela actualisera la page actuelle et affichera tous les journaux récemment créés
- Supprimer - Cela effacera tous les journaux, vous permettant de repartir à zéro
- Nom de fichier - Cela affichera le nom de fichier associé au journal
- Dernière écriture - Il s'agit de l'heure locale à laquelle ce fichier journal particulier a été écrit.
  - Sonarr utilise des fichiers journaux rotatifs limités à 1 Mo chacun. Le fichier journal actuel est toujours sonarr.txt, pour les autres fichiers, sonarr.0.txt est le plus récent (plus le nombre est élevé, plus il est ancien) jusqu'à un total de 51 fichiers journaux. Ce fichier journal contient les entrées `fatal`, `error`, `warn` et `info`.
  - Lorsque le niveau de journalisation de débogage est activé, des fichiers journaux supplémentaires sonarr.debug.txt seront présents, jusqu'à 51 fichiers. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info` et `debug`. Ils couvrent généralement une période d'environ 40 heures.
  - Lorsque le niveau de journalisation de trace est activé, des fichiers journaux supplémentaires sonarr.trace.txt seront présents, jusqu'à 51 fichiers. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info`, `debug` et `trace`. En raison de la verbosité de la trace, ils ne couvrent que quelques heures au maximum.