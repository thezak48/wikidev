---
title: Guide de démarrage rapide de Readarr
description: 
published: true
date: 2022-09-07T23:19:05.590Z
tags: readarr
editor: markdown
dateCreated: 2021-12-11T19:42:31.825Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Guide de configuration rapide](#guide-de-configuration-rapide)
- [Démarrage](#démarrage)
- [Gestion des médias](#gestion-des-médias)
- [Nom des livres](#nom-des-livres)
- [Dossiers](#dossiers)
- [Importation](#importation)
- [Gestion des fichiers](#gestion-des-fichiers)
- [Dossiers racines et intégration de Calibre](#dossiers-racines-et-intégration-de-calibre)
  - [Serveur de contenu Calibre (facultatif)](#serveur-de-contenu-calibre-facultatif)
  - [Intégration de Calibre](#intégration-de-calibre)
- [Clients de téléchargement](#clients-de-téléchargement)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Comment importer votre bibliothèque multimédia organisée existante](#comment-importer-votre-bibliothèque-multimédia-organisée-existante)
  - [Importation de médias existants](#importation-de-médias-existants)
- [Ajouter de nouveaux livres](#ajouter-de-nouveaux-livres)

# Guide de configuration rapide

> Cette page est encore en cours de rédaction et n'est pas complète. Les contributions sont les bienvenues.

> Pour une description plus détaillée de tous les paramètres, consultez [Readarr => Paramètres](/readarr/settings)
{.is-info}

Dans ce guide, nous allons essayer d'expliquer la configuration de base que vous devez effectuer pour commencer avec Readarr. Nous allons passer en revue certaines options que vous pouvez voir à l'écran. Si vous souhaitez approfondir ces options, veuillez consulter la page appropriée dans la FAQ et la documentation pour une explication complète.

> Veuillez noter que dans les captures d'écran et les paramètres de l'interface utilisateur en `orange`, il s'agit d'options avancées. Vous devrez cliquer sur `Afficher les options avancées` en haut de la page pour les rendre visibles.
{.is-warning}

# Démarrage

Après l'installation et le démarrage, ouvrez un navigateur et accédez à `http://{votre_ip_ici}:8787`

![qs_startup.png](/assets/readarr/qs_startup.png)

# Gestion des médias

Tout d'abord, nous allons jeter un coup d'œil aux paramètres de `Gestion des médias` où nous pouvons configurer nos préférences de nommage et de gestion des fichiers.

`Paramètres` => `Gestion des médias`

![mediamanagement.png](/assets/readarr/mediamanagement.png)

# Nom des livres

![booknaming.png](/assets/readarr/booknaming.png)

- Activer/Désactiver le renommage de vos livres (par opposition à laisser les noms tels quels ou tels qu'ils étaient lors de leur téléchargement).
- Si vous souhaitez remplacer ou supprimer les caractères illégaux (`\ / : * ? " < > | ~ - % & + { }`).
- Vous sélectionnerez ici la convention de nommage pour les fichiers de livres réels. Notez que le nom du dossier du livre est également défini ici.
- `(Option avancée) C'est ici que vous définirez la convention de nommage pour le dossier de l'auteur.`

> Cela ne s'applique pas si Calibre est utilisé, car Calibre gère le nommage des fichiers/dossiers à l'aide de son propre schéma interne.
{.is-info}

# Dossiers

![folders.png](/assets/readarr/folders.png)

- (Option avancée) Créer des dossiers d'auteur vides - Activer pour créer des dossiers d'auteur vides lorsqu'un nouvel auteur est ajouté à Readarr.
- (Option avancée) Supprimer les dossiers vides - Activer pour supprimer les dossiers d'auteur vides lorsqu'il ne reste plus de livres pour cet auteur.

> Une de ces cases peut être cochée, mais elles ne doivent PAS être cochées TOUTES LES DEUX.
{.is-warning}

> Cela ne s'applique pas si Calibre est utilisé, car Calibre gère le nommage des fichiers/dossiers à l'aide de son propre schéma interne.
{.is-info}

# Importation

![importing.png](/assets/readarr/importing.png)

- (Option avancée) Ignorer la vérification de l'espace libre - Si activé, ignorez la vérification de l'espace libre avant l'importation.
- (Option avancée) Espace libre minimum - Entrez l'espace libre minimum requis sur le disque avant que l'importation ne s'arrête.
- (Option avancée) Utiliser des liens durs au lieu de la copie - Cochez cette case pour utiliser des liens durs au lieu de la copie (pour les torrents). Notez que cela est activé par défaut.
  
> Vous devriez idéalement utiliser cette option chaque fois que possible. Pour que les liens durs soient utilisés, votre source/destination doit être sur le même système de fichiers (lecteur, partition) et les points de montage doivent être les mêmes. [Consultez le guide des liens durs de TRaSH pour plus d'informations](https://trash-guides.info/hardlinks/)
{.is-info}
  
- Importer des fichiers supplémentaires - Si activé, importez les fichiers supplémentaires spécifiés situés dans le dossier du livre lors de son importation.
- (Option avancée) Importer des fichiers supplémentaires - Si l'importation de fichiers supplémentaires est activée, entrez une liste séparée par des virgules des extensions à importer.

> Si vous utilisez Readarr pour les livres audio, vous devez ajouter .cue à cette liste, car il contient les informations sur les chapitres !
{.is-info}

# Gestion des fichiers

![filemanagement.png](/assets/readarr/filemanagement.png)

- Les livres supprimés du disque ne sont plus surveillés par Readarr.

- Ignorer les livres supprimés - Cochez cette case pour ne plus surveiller les livres détectés comme supprimés ou inaccessibles dans le dossier racine de Readarr.
- Télécharger les versions correctes et les rééditions - Indiquez si vous souhaitez ou non mettre automatiquement à niveau vers les versions correctes/rééditées. Utilisez `Ne pas préférer` pour trier en fonction du score de mots préféré plutôt que des versions correctes/rééditées.
  - Préférer et mettre à niveau - Classez les rééditions et les versions correctes plus haut que les versions non rééditées et non correctes. Considérez les nouvelles rééditions et versions correctes comme une mise à niveau des versions actuelles.
  - Ne pas mettre à niveau automatiquement - Classez les rééditions et les versions correctes plus haut que les versions non rééditées et non correctes. Ne considérez pas les nouvelles rééditions et versions correctes comme une mise à niveau des versions actuelles.
  - Ne pas préférer - Ignorez les rééditions et les versions correctes. Vous devrez gérer toute préférence pour celles-ci avec les [mots préférés](#profils-de-sortie).

> \* `CORRECT` - signifie qu'il y avait un problème avec la version précédente. Les téléchargements marqués comme CORRECT indiquent que les problèmes ont été résolus dans cette version. Cela est fait par un groupe qui n'a pas publié l'original.
> \* `RÉÉDITION` - signifie qu'il y avait un problème avec la version précédente et qu'il a été corrigé par le groupe original. Les téléchargements marqués comme RÉÉDITION indiquent que les problèmes ont été résolus dans cette version. Cela est fait par un groupe qui a publié l'original.
{.is-info}

- (Option avancée) Surveiller les dossiers racines pour les modifications de fichiers - Cochez cette case pour déclencher une nouvelle analyse lorsque des modifications sont détectées dans le dossier racine.
- (Option avancée) Analyser à nouveau le dossier de l'auteur après le rafraîchissement - Choisissez quand analyser à nouveau un dossier d'auteur après le rafraîchissement de l'auteur.
  - Toujours - Cela analysera à nouveau les dossiers d'auteur en fonction de la planification des tâches
  - Après un rafraîchissement manuel - Vous devrez analyser manuellement le disque
  - Jamais - Comme son nom l'indique, ne jamais analyser à nouveau les dossiers d'auteur.
- (Option avancée) Autoriser l'empreinte digitale - Choisissez comment gérer l'empreinte digitale, ce qui permet une correspondance plus précise des livres, au détriment du temps CPU/disque.
  - Toujours - Utilisez toujours l'empreinte digitale si possible
  - Uniquement pour les nouvelles importations - Utilisez uniquement l'empreinte digitale pour les nouvelles versions importées
  - Jamais - Comme son nom l'indique, n'utilisez jamais l'empreinte digitale
- (Option avancée) Modifier la date du fichier - Modifier la date du fichier lors de l'importation/nouvelle analyse
  - Aucun - Readarr ne modifiera pas la date affichée dans votre explorateur de fichiers
  - Date de sortie du livre - La date de sortie du livre.
- (Option avancée) Corbeille de recyclage - Les fichiers de livres iront ici lorsqu'ils seront supprimés au lieu d'être supprimés définitivement
- (Option avancée) Nettoyage de la corbeille de recyclage - C'est l'ancienneté d'un fichier donné avant qu'il ne soit supprimé définitivement

> Il est fortement recommandé d'utiliser une corbeille de recyclage. Il est facile de supprimer des fichiers et il est facile de les récupérer si vous utilisez la corbeille.
{.is-warning}

# Dossiers racines et intégration de Calibre

![rootfolders1.png](/assets/readarr/rootfolders1.png)

Ici, nous allons ajouter le dossier racine que Readarr utilisera pour importer votre bibliothèque multimédia organisée existante et où Readarr importera (copie/liens durs/déplacement) vos médias après que votre client de téléchargement les a téléchargés.

> **L'utilisateur et le groupe que vous avez configurés pour exécuter Readarr doivent avoir un accès en lecture et en écriture à cet emplacement.** {.is-info}

Vous pouvez également choisir d'utiliser Calibre pour gérer votre bibliothèque sur cet écran. Pour ce faire, vous devrez exécuter le serveur de contenu Calibre. Il ne s'agit PAS de Calibre-Web.

> Utilisateurs non Windows :
> \* Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
> \* Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.
{.is-warning}

> Si vous allez utiliser Calibre, les livres que vous souhaitez que Readarr reconnaisse lors de l'importation initiale de la bibliothèque **doivent déjà être dans Calibre**. Les livres présents dans le dossier mais pas dans Calibre seront ignorés. Les liens durs ne sont pas utilisés lors de l'ajout de l'intégration de Calibre.
> **Notez que vous ne pouvez pas ajouter l'intégration de Calibre à un dossier racine après sa création.**
{.is-danger}

> Votre client de téléchargement télécharge dans un dossier de téléchargement, et Readarr l'importe dans votre dossier multimédia (destination finale) que votre serveur multimédia utilise. Votre dossier de téléchargement et votre dossier multimédia ne peuvent pas être situés au même endroit !
{.is-warning}

N'oubliez pas d'enregistrer vos modifications.

## Serveur de contenu Calibre (facultatif)

Si vous souhaitez utiliser Calibre pour gérer vos livres, vous devez configurer le serveur de contenu Calibre. Encore une fois, il ne s'agit pas de Calibre-Web, mais d'une partie de Calibre lui-même. Vous devez exécuter Calibre et configurer le serveur de contenu.

> Si vous choisissez d'utiliser Calibre, vous ne pouvez rien modifier dans la base de données de Calibre. Ne pas respecter cet avertissement vous obligera à supprimer votre base de données Readarr et à recommencer à zéro.
{.is-danger}

Si vous utilisez Docker, votre répertoire de livres monté de Calibre et votre répertoire de livres monté de Readarr doivent être identiques.

> Veuillez noter que tant que Readarr est en version bêta, si vous utilisez Calibre, il est recommandé de désactiver le renommage dans Readarr au cas où un bogue non intentionnel se glisserait.
{.is-info}

Pour ce faire, ouvrez Calibre et cliquez sur `Préférences / Partage sur le net`

![calibreprefs.png](/assets/readarr/calibreprefs.png)

Tout d'abord, ajoutez un compte utilisateur. Le compte DOIT avoir un accès "apporter des modifications".

![calibreacct.png](/assets/readarr/calibreacct.png)

Ensuite, vous devrez redémarrer Calibre. Une fois de retour, configurez et démarrez le serveur de contenu. Il devrait vous montrer qu'il fonctionne. Configurez-le pour qu'il démarre automatiquement au démarrage. Après avoir enregistré, vous devrez à nouveau redémarrer Calibre. Assurez-vous que le serveur est démarré lorsqu'il redémarre, puis vous pouvez passer à la section suivante.

> Vous devez sélectionner "Exiger un nom d'utilisateur et un mot de passe pour accéder au serveur de contenu" afin que Readarr fonctionne correctement. Sinon, vous obtiendrez une erreur indiquant "Les utilisateurs anonymes ne sont pas autorisés à apporter des modifications" lorsque Readarr importe un livre !
{.is-info}

![calibreserver.png](/assets/readarr/calibreserver.png)

## Intégration de Calibre

![calibre1.png](/assets/readarr/calibre1.png)

Les paramètres suivants sont spécifiques à Calibre et n'apparaissent que si `Utiliser Calibre` est activé

- Utiliser Calibre - Activer/Désactiver l'utilisation du serveur de contenu Calibre pour gérer votre dossier racine.

> \* Notez que cela **ne peut pas être activé sur un dossier racine existant**.
> \* Notez que cela **ne peut pas être désactivé sur un dossier racine existant avec l'intégration de Calibre activée**.
> \* Notez que cela nécessite le **serveur de contenu Calibre** et ne fonctionnera pas avec Calibre Web ni Calibre.
> \* Notez que les liens durs ne fonctionnent pas avec l'intégration de Calibre.
> \* Notez que cela nécessite que Calibre ait `Exiger un nom d'utilisateur et un mot de passe pour accéder au serveur de contenu` activé.
> \* Si vous n'activez pas `Exiger un nom d'utilisateur et un mot de passe pour accéder au serveur de contenu` dans Calibre, vous obtiendrez une erreur `Les utilisateurs anonymes ne sont pas autorisés à apporter des modifications` lors de l'importation d'un livre par Readarr !
{.is-warning}

> Si vous choisissez d'utiliser Calibre, vous ne pouvez rien modifier dans la base de données de Calibre. Ne pas respecter cet avertissement vous obligera à supprimer votre base de données Readarr et à recommencer à zéro.
{.is-danger}

- Hôte Calibre - L'IP/domaine de l'hôte du serveur de contenu Calibre
- Port Calibre - Le port sur lequel le serveur de contenu Calibre écoute
- (Avancé) Base de l'URL Calibre - Ajoutez un préfixe à l'URL Calibre, par exemple `http://[hôte]:[port]/[baseURL]`
- Nom d'utilisateur Calibre - Nom d'utilisateur à utiliser pour accéder au serveur de contenu Calibre
- Mot de passe Calibre - Mot de passe à utiliser pour accéder au serveur de contenu Calibre
- Bibliothèque Calibre - Nom de la bibliothèque du serveur de contenu Calibre. Laissez vide pour la valeur par défaut
- Convertir en format - (Facultatif) Demandez au serveur de contenu Calibre de convertir vers d'autres formats avec une liste séparée par des virgules.
  - Consultez l'icône (i) dans l'application pour obtenir une liste à jour des options.
  - Les options sont : MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Profil de sortie Calibre - Sélectionnez le profil de sortie du serveur de contenu Calibre à utiliser
  - Le profil de sortie indique au système de conversion du serveur de contenu Calibre comment optimiser le document créé pour le périphérique spécifié (par exemple, en redimensionnant les images pour la taille de l'écran du périphérique). Dans certains cas, un profil de sortie peut être utilisé pour optimiser la sortie pour un périphérique particulier, mais cela est rarement nécessaire.
- Utiliser SSL - Activer ou désactiver l'utilisation de SSL (HTTPS) pour le serveur de contenu Calibre

> Si vous ajoutez un livre individuel et sélectionnez `Aucun`\* pour le [profil de métadonnées](/readarr/settings#metadata-profiles), seul ce livre apparaîtra sous l'auteur lorsqu'il sera ajouté. Si vous souhaitez ajouter d'autres livres pour cet auteur, choisissez un profil de métadonnées approprié.
> \* **Notez que `Aucun` n'applique aucun filtre de métadonnées et vous pouvez obtenir des éditions étrangères indésirables. Pour contourner cela, [créez un profil de métadonnées comme indiqué dans la FAQ](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Clients de téléchargement

`Paramètres` => `Clients de téléchargement`

Le téléchargement et l'importation sont les étapes où la plupart des utilisateurs rencontrent des problèmes. D'un point de vue général, le logiciel doit être capable de communiquer avec votre client de téléchargement et d'avoir accès aux fichiers qu'il télécharge. Il existe une grande variété de clients de téléchargement pris en charge et une variété encore plus grande de configurations. Cela signifie qu'il existe quelques configurations courantes, mais il n'y a pas une seule configuration correcte et la configuration de chacun peut être légèrement différente. Mais il existe de nombreuses configurations incorrectes.

> Consultez la [page des paramètres](/readarr/settings#download-clients), la page [Plus d'informations (Pris en charge)](/readarr/supported#download-clients) pour cette section et les [guides de clients de téléchargement de TRaSH](https://trash-guides.info/Downloaders/) pour plus d'informations.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Readarr enverra une demande de téléchargement à votre client et l'associera à un label ou à une catégorie que vous avez configuré dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Readarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Readarr connaîtra l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia et accessible par Readarr.
- Readarr analysera cet emplacement de fichier terminé à la recherche de fichiers que Readarr peut utiliser. Il analysera le nom du fichier pour le faire correspondre avec le média demandé. S'il peut le faire, il renommera le fichier selon vos spécifications et le déplacera vers l'emplacement multimédia spécifié.
- Les déplacements atomiques (déplacements instantanés) sont activés par défaut. Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si le déplacement atomique échoue ou si votre configuration ne prend pas en charge les liens durs et les déplacements atomiques, Readarr effectuera une copie du fichier, puis le supprimera de la source, ce qui est intensif en E/S.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Readarr, les fichiers restants du téléchargement seront envoyés à votre corbeille ou à votre recyclage via une demande à votre client pour supprimer le téléchargement.

### BitTorrent

{#bittorrent}

- Readarr enverra une demande de téléchargement à votre client et l'associera à un label ou à une catégorie que vous avez configurée dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Readarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de les partager (le ratio ou le temps peuvent être ajustés dans le client de téléchargement ou depuis Readarr sous le client de téléchargement spécifique). Lorsque les fichiers sont importés dans votre dossier multimédia, Readarr créera un lien physique vers le fichier s'il est pris en charge par votre configuration, sinon il le copiera si les liens physiques ne sont pas pris en charge.
- Les liens physiques sont activés par défaut. [Un lien physique ne nécessite pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien physique échoue ou si votre configuration ne prend pas en charge les liens physiques, Readarr utilisera une copie du fichier.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Readarr, Readarr supprimera le torrent de votre client et demandera au client de supprimer les données du torrent, mais seulement si le client signale que le partage est terminé et que le torrent est arrêté (en pause à la fin).

# Comment importer votre bibliothèque multimédia existante et organisée

> Notez que Readarr ne recherche pas régulièrement les livres. Consultez ces deux questions fréquemment posées pour comprendre comment fonctionne Readarr.
[Comment Readarr trouve-t-il des livres ?](/readarr/faq#how-does-readarr-find-books) et [Comment fonctionne Readarr ?](/readarr/faq#how-does-readarr-work)
{.is-info}

Après avoir configuré vos profils/tailles de qualité et ajouté vos indexeurs et clients de téléchargement, il est temps d'importer votre bibliothèque multimédia existante et organisée.

Bientôt disponible - Contributions bienvenues

## Importation de médias existants

Bientôt disponible - Contributions bienvenues

# Ajouter de nouveaux livres

[Référez-vous à la page de la bibliothèque pour plus d'informations](/readarr/library#add-new)