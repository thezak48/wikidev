# Paramètres de Readarr

Cette page présente tous les paramètres disponibles dans Readarr et leur fonctionnement. Elle ne vise pas à être un guide complet sur la configuration de Readarr. Si vous souhaitez cela, veuillez consulter la page [Guide de démarrage rapide](/readarr/quick-start-guide) à la place.

# Options de menu

Pour accéder à la page des paramètres, sélectionnez Paramètres dans le menu de gauche. Les options de sous-menu suivantes seront disponibles :

![settings_1_menu.png](/assets/readarr/settings_1_menu.png)

Notez également que pour chaque page de paramètres individuelle, il y a des options en haut du menu :

![settings_2_topmenu.png](/assets/readarr/settings_2_topmenu.png)

- Masquer/Afficher les options avancées est important pour tous les éléments marqués ci-dessous comme `(Option avancée)`, sinon ils n'apparaîtront pas. Ces éléments de menu sont affichés en orange dans les captures d'écran.

- Vous devez enregistrer vos modifications avant de quitter l'écran. Pour cela, cliquez sur l'icône du disque. Si vous n'avez apporté aucune modification, il affichera "Aucune modification" et sera grisé, comme indiqué ci-dessus.

# Gestion des médias

> Certains de ces paramètres ne sont visibles que si vous activez `Afficher les paramètres avancés`, qui se trouve dans la barre supérieure sous la barre de recherche{.is-info}

## Dossiers racines

- Une liste de vos dossiers racines configurés (dossiers de bibliothèque) est affichée.
- Cliquez sur le bouton <kb>+</kb> pour ajouter un nouveau dossier racine ou cliquez sur la carte d'un dossier existant pour le modifier.

### Paramètres du dossier racine

- Nom - Le nom du dossier racine à des fins d'interface utilisateur
- Chemin - Le dossier contenant votre bibliothèque de livres, c'est-à-dire la destination finale telle que Readarr la voit.
  - Notez que cela doit être différent de l'emplacement où votre client de téléchargement place les fichiers.
  - Si vous utilisez Docker et l'intégration de Calibre, les montages doivent être identiques à votre dossier de livres.

{#calibre}

- Paramètres spécifiques à Calibre (uniquement si l'utilisation de Calibre est activée)
  - Utiliser Calibre - Activer/Désactiver l'utilisation du serveur de contenu Calibre pour gérer votre dossier racine.

> \* Notez que cela **ne peut pas être activé sur un dossier racine existant**.
> \* Notez que cela **ne peut pas être désactivé sur un dossier racine Calibre activé existant**.
> \* Notez que cela nécessite le **serveur de contenu Calibre** et ne fonctionnera pas avec Calibre Web ou Calibre.
> \* Notez que les liens physiques ne fonctionnent pas avec l'intégration de Calibre.
> \* Notez que cela nécessite que Calibre ait activé "Exiger un nom d'utilisateur et un mot de passe pour accéder au serveur de contenu".
> \* L'absence de l'activation de "Exiger un nom d'utilisateur et un mot de passe pour accéder au serveur de contenu" dans Calibre entraînera une erreur "Les utilisateurs anonymes ne sont pas autorisés à apporter des modifications".
{.is-warning}

- Hôte Calibre - L'IP/domaine de l'hôte du serveur de contenu Calibre
- Port Calibre - Le port sur lequel le serveur de contenu Calibre écoute
- (Avancé) Base d'URL Calibre - Ajoutez un préfixe à l'URL Calibre, par exemple `http://[hôte]:[port]/[baseURL]`
- Nom d'utilisateur Calibre - Nom d'utilisateur à utiliser pour accéder au serveur de contenu Calibre
- Mot de passe Calibre - Mot de passe à utiliser pour accéder au serveur de contenu Calibre
- Bibliothèque Calibre - Nom de la bibliothèque du serveur de contenu Calibre. Laissez vide pour la valeur par défaut
- Convertir en format - (Facultatif) Demandez au serveur de contenu Calibre de convertir vers d'autres formats avec une liste séparée par des virgules.
  - Consultez l'icône (i) dans l'application pour obtenir une liste actuelle des options.
  - Les options sont : MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Profil de sortie Calibre - Sélectionnez le profil de sortie du serveur de contenu Calibre à utiliser
  - Le profil de sortie indique au système de conversion du serveur de contenu Calibre comment optimiser le document créé pour le périphérique spécifié (par exemple, en redimensionnant les images pour la taille de l'écran du périphérique). Dans certains cas, un profil de sortie peut être utilisé pour optimiser la sortie pour un périphérique particulier, mais cela est rarement nécessaire.
- Utiliser SSL - Activer ou désactiver l'utilisation de SSL (HTTPS) pour le serveur de contenu Calibre
- Surveillance - Configurez vos options de surveillance pour les livres détectés dans ce dossier
  - Tous les livres - Surveiller tous les livres
  - Livres futurs - Surveiller les livres qui ne sont pas encore sortis
  - Livres manquants - Surveiller les livres qui n'ont pas de fichiers ou qui ne sont pas encore sortis
  - Livres existants - Surveiller les livres qui ont des fichiers ou qui ne sont pas encore sortis
  - Premier livre - Surveiller le premier livre. Tous les autres livres seront ignorés
  - Dernier livre - Surveiller le dernier livre et les livres futurs
  - Aucun - Aucun livre ne sera surveillé sauf s'il est explicitement ajouté
- Profil de qualité - Profil de qualité par défaut pour les livres et les auteurs détectés dans ce dossier
- Profil de métadonnées - Sélectionnez le profil de métadonnées à utiliser pour les auteurs détectés dans ce dossier. Pour charger uniquement les livres qui ont été ajoutés ou détectés explicitement, sélectionnez Aucun.
- Balises Readarr par défaut - Balises par défaut pour les auteurs détectés dans ce dossier

> Utilisateurs non Windows :
> \* Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
> \* Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.
{.is-warning}

## Mappages de chemin distant

- Le mappage de chemin distant agit comme une recherche simple du chemin distant et le remplace par le chemin local. Cela est principalement utilisé pour les configurations locales/à distance fusionnées utilisant mergerfs ou similaire, ou pour les cas où l'application et le client de téléchargement ou Calibre ne sont pas sur le même serveur.
- Pour plus d'informations, consultez la section [Clients de téléchargement => Mappage de chemin distant](#remote-path-mappings-1) en remplaçant `<Client de téléchargement>` par `<Calibre>`

## Nom des fichiers de livre

![bookfilenaming.png](/assets/readarr/bookfilenaming.png)

**Si vous utilisez l'intégration de Calibre, vous ne pouvez pas nommer les fichiers de livre. Calibre s'en charge pour vous. Vous ne devez modifier ces paramètres que si vous n'utilisez pas Calibre.**

> Veuillez noter que tant que Readarr est en version bêta, si vous utilisez Calibre, il est recommandé de désactiver le renommage dans Readarr au cas où un bogue non intentionnel se glisserait. {.is-info}

Les schémas de nommage couramment utilisés sont :

- Format standard du livre
  - `{Titre du livre}\{Nom de l'auteur}` - `{Titre du livre}` qui donnerait un dossier nommé `Cujo`, et un sous-dossier contenant un fichier portant le nom `Stephen King - Cujo.m4b`

- Format du dossier de l'auteur
  - `{Nom de l'auteur}` qui donnerait : `Stephen King`

## Nom du livre

- Renommer les livres - Si cette option est désactivée (pas de case cochée), Readarr utilisera le nom de fichier existant si le renommage est désactivé.
  - Si non coché :
    - Importation du client de téléchargement
      - Le titre de la version du client de téléchargement est utilisé
    - Importation manuelle (adhoc) : Nom de fichier d'origine

> Si vous laissez "Renommer les livres" non coché, alors aucune des options de nommage ci-dessous ne s'applique - vous avez indiqué à Readarr que vous ne souhaitez aucun renommage du tout. Le livre sera importé directement dans le dossier de l'auteur.
{.is-info}

> Cela ne s'applique pas si Calibre est utilisé, car Calibre gère le nom des fichiers/dossiers à l'aide de son propre schéma interne.
{.is-info}

- Remplacer les caractères illégaux - Si désactivé, Readarr supprimera les caractères illégaux. S'il est activé, Readarr les remplacera. Les exemples incluent `\ # / $ * < >` et d'autres.

### Format standard du livre

- Sélectionnez le format

- Boîte déroulante (coin supérieur droit)
  - Boîte de gauche - Gestion des espaces
    - `Espace ( )` - Utiliser des espaces dans le nom (par défaut)
    - `Point (.)` - Utiliser des points à la place des espaces dans le nom
    - `Tiret bas (_)` - Utiliser des tirets bas à la place des espaces dans le nom
    - `Tiret (-)` - Utiliser des tirets à la place des espaces dans le nom
  - Boîte de droite - Gestion de la casse
    - `Casse par défaut` - Mettre le titre en majuscules et minuscules (~camel-case) (par défaut)
    - `Majuscules` - Mettre le titre tout en majuscules
    - `Minuscules` - Mettre le titre tout en minuscules

### Auteur

- `{Nom de l'auteur}` = Nom de l'auteur
- `{Nom de l'auteurThe}` = Nom de l'auteur, Le
- `{Nom de l'auteurClean}` = Nom de l'auteur
- `{Nom de l'auteurSort}` = Nom, Auteur
- `{Nom de l'auteurDisambiguation}` = Nom de l'auteur (disambiguation utilisé par GoodReads pour plusieurs auteurs ayant le même nom)

### Livre

- `{Titre du livre}` = Le titre du livre !: Sous-titre !
- `{Titre du livreThe}` = Titre du livre !, Le : Sous-titre !
- `{Titre du livreClean}` = Le titre du livre : Sous-titre
- `{Titre du livreNoSub}` = Le titre du livre !
- `{Titre du livreTheNoSub}` = Titre du livre !, Le
- `{Titre du livreCleanNoSub}` = Le titre du livre
- `{Sous-titre du livre}` = Sous-titre !
- `{Sous-titre du livreThe}` Sous-titre !, Le
- `{Sous-titre du livreClean}` = Sous-titre
- `{Disambiguation du livre}` = Nom du livre ! (titre de disambiguation utilisé par GoodReads)
- `{Série du livre}` = Titre de la série
- `{Position de la série du livre}` = 1
- `{Titre de la série du livre}` = Titre de la série #1
- `{Numéro de partie:0}` ou `{Numéro de partie:0}` = 2
- `{Numéro de partie:00}` = 02
- `{Compte de parties}` ou `{Compte de parties:0} = 9
- `{Compte de parties:00}` = 09

### Date de sortie

- `{Année de sortie}` = 2016
- `{Année de sortieFirst}` = 2015
- `{Année d'édition}` = 2016

### Qualité

- `{Qualité complète}` = AZW3 Correct
- `{Titre de qualité}` = AZW3

### Informations sur les médias

- `{MediaInfo AudioCodec}` = MP3
- `{MediaInfo AudioChannels}` = 2.0
- `{MediaInfo AudioBitRate}` = 320kbps
- `{MediaInfo AudioBitsPerSample}` = 24bit
- `{MediaInfo AudioSampleRate}` = 44.1kHz

### Autre

- `{Groupe de sortie}` = Rls Grp
- `{Mots préférés}` = iNTERNAL

### Original

- `{Titre original}` = Auteur.Nom.Livre.Nom.2018.AZW3-EVOLVE
- `{Nom de fichier d'origine}` = 01-nom du livre

> Le nom de fichier d'origine n'est pas recommandé. Il s'agit du nom de fichier d'origine littéral et peut être obscurci t1i0p3s7i8yuti. Le titre original est le nom de la version et doit être utilisé à la place.
{.is-info}
  
## Format du dossier de l'auteur

- (Option avancée) C'est ici que vous définissez la convention de nommage pour le nom du dossier de l'auteur.

> Cela ne s'applique pas si Calibre est utilisé, car Calibre gère le nom des fichiers/dossiers à l'aide de son propre schéma interne.
{.is-info}

### Auteur

- `{Nom de l'auteur}` = Nom de l'auteur
- `{Nom de l'auteurThe}` = Nom de l'auteur, Le
- `{Nom de l'auteurClean}` = Nom de l'auteur
- `{Nom de l'auteurSort}` = Nom, Auteur
- `{Nom de l'auteurDisambiguation}` = Nom de l'auteur (disambiguation utilisé par GoodReads pour plusieurs auteurs ayant le même nom)

## Dossiers

![mm_folders.png](/assets/readarr/mm_folders.png)
  
- (Option avancée) Créer des dossiers d'auteur vides - Cochez la case pour créer des dossiers d'auteur vides lorsqu'un nouvel auteur est ajouté.
- (Option avancée) Supprimer les dossiers d'auteur vides - Cochez la case pour supprimer les dossiers d'auteur vides s'il n'y a aucun livre dedans.
  
> Une de ces cases peut être cochée, mais elles ne doivent PAS être cochées TOUTES LES DEUX. {.is-warning}

> Cela ne s'applique pas si Calibre est utilisé, car Calibre gère le nom des fichiers/dossiers à l'aide de son propre schéma interne.
{.is-info}

## Importation
  
![mm_importing.png](/assets/readarr/mm_importing.png)
  
- (Option avancée) Ignorer la vérification de l'espace libre - Si activée, ignore la vérification de l'espace libre avant l'importation.
- (Option avancée) Espace libre minimum - Entrez l'espace libre minimum que le lecteur doit avoir avant que l'importation ne s'arrête.
- (Option avancée) Utiliser des liens durs au lieu de la copie - Cochez cette case pour utiliser des liens durs au lieu de copies (pour les torrents). Notez que cela est activé par défaut.
  
> Vous devriez idéalement utiliser cela chaque fois que possible. Pour que les liens durs soient utilisés, vous devez avoir votre source/destination sur le même système de fichiers (lecteur, partition) et points de montage. [Voir le guide des liens durs de TRaSH pour plus d'informations](https://trash-guides.info/hardlinks/)
  
- Importer des fichiers supplémentaires - Si activé, importe les fichiers supplémentaires spécifiés situés dans le dossier du livre lors de son importation.
- (Option avancée) Importer des fichiers supplémentaires - Si l'importation de fichiers supplémentaires est activée, entrez une liste séparée par des virgules des extensions à importer.

> Si vous utilisez Readarr pour les livres audio, vous devriez ajouter .cue à cette liste, car il contient les informations de chapitre !
{.is-info}
  
## Gestion des fichiers
  
  ![mm_filemgmt.png](/assets/readarr/mm_filemgmt.png)

- Ignorer les livres supprimés - Cochez cette case pour ne pas surveiller les livres détectés comme supprimés ou inaccessibles à partir du dossier racine de Readarr.
- Télécharger les versions correctes et les repacks - Indique si oui ou non mettre automatiquement à niveau vers les versions correctes/repacks. Utilisez `Ne pas préférer` pour trier par score de mots préféré plutôt que par versions correctes/repacks
  - Préférer et mettre à niveau - Classez les repacks et les versions correctes plus haut que les versions non-repacks et non-correctes. Considérez les nouveaux repacks et les versions correctes comme une mise à niveau des versions actuelles.
  - Ne pas mettre à niveau automatiquement - Classez les repacks et les versions correctes plus haut que les versions non-repacks et non-correctes. Ne considérez pas les nouveaux repacks et les versions correctes comme une mise à niveau des versions actuelles.
  - Ne pas préférer - Cela ignore effectivement les repacks et les versions correctes. Vous devrez gérer toute préférence pour ceux-ci avec [les mots préférés](#profils-de-sortie).
  
> \* `CORRECT` - signifie qu'il y avait un problème avec la version précédente. Les téléchargements marqués comme CORRECT montrent que les problèmes ont été résolus dans cette version. Cela est fait par un groupe qui n'a pas publié l'original.
> \* `REPACK` - signifie qu'il y avait un problème avec la version précédente et qu'il a été corrigé par le groupe original. Les téléchargements marqués comme REPACK montrent que les problèmes ont été résolus dans cette version. Cela est fait par un groupe qui a publié l'original.
{.is-info}

- (Option avancée) Surveiller les dossiers racine pour les modifications de fichiers - Cochez cette case pour déclencher une nouvelle analyse lorsque des modifications sont détectées dans le dossier racine.
- (Option avancée) Rescan du dossier de l'auteur après actualisation - Choisissez quand effectuer une nouvelle analyse d'un dossier d'auteur après actualisation de l'auteur.
  - Toujours - Cela permet de refaire une analyse des dossiers d'auteur en fonction de la planification des tâches
  - Après actualisation manuelle - Vous devrez refaire manuellement l'analyse du disque
  - Jamais - Comme son nom l'indique, ne refait jamais l'analyse des dossiers d'auteur.
- (Option avancée) Autoriser l'empreinte digitale - Choisissez comment gérer l'empreinte digitale, ce qui permet une précision accrue pour la correspondance des livres, au détriment du temps CPU/disque.
  - Toujours - Utilisez toujours l'empreinte digitale si possible
  - Uniquement pour les nouvelles importations - Utilisez uniquement l'empreinte digitale pour les nouvelles versions importées
  - Jamais - Comme son nom l'indique, n'utilisez jamais l'empreinte digitale
- (Option avancée) Modifier la date du fichier - Modifier la date du fichier lors de l'importation/nouvelle analyse
  - Aucune - Readarr ne modifiera pas la date qui s'affiche dans votre explorateur de fichiers donné
  - Date de sortie du livre - La date de sortie du livre.
- (Option avancée) Corbeille de recyclage - Les fichiers de livres iront ici lorsqu'ils seront supprimés au lieu d'être supprimés définitivement
- (Option avancée) Nettoyage de la corbeille de recyclage - C'est l'ancienneté d'un fichier donné avant qu'il ne soit supprimé définitivement

> Il est fortement recommandé d'utiliser une corbeille de recyclage. Il est facile de supprimer des fichiers et de les récupérer facilement si vous utilisez la corbeille.
{.is-warning}

# Autorisations

- Définir les autorisations - `chmod` doit-il être exécuté lorsque les fichiers sont importés/renommés ?
  - chmod Dossier - Octal, appliqué lors de l'importation/du renommage des dossiers et des fichiers multimédias (sans bits d'exécution)

> La liste déroulante propose une liste prédéfinie d'autorisations très couramment utilisées. Cependant, vous pouvez entrer manuellement un octal de dossier si vous le souhaitez.
{.is-info}

> Cela ne fonctionne que si l'utilisateur exécutant `Readarr` est le propriétaire du fichier. Il est préférable de s'assurer que le client de téléchargement définit correctement les autorisations.
{.is-warning}

- chown Groupe - Nom du groupe ou GID. Utilisez GID pour les systèmes de fichiers distants

> Cela ne fonctionne que si l'utilisateur exécutant `Readarr` est le propriétaire du fichier. Il est préférable de s'assurer que le client de téléchargement définit correctement les autorisations.
{.is-warning}

# Profils

## Profils de qualité

Les profils de qualité sont utilisés pour déterminer les formats de livres acceptables pour un livre de votre bibliothèque.
  
![qualityprofile.png](/assets/readarr/qualityprofile.png)

- Définissez des profils pour la qualité des livres que vous souhaitez télécharger.

> Lorsque vous sélectionnez un profil existant ou ajoutez un profil supplémentaire, une nouvelle fenêtre apparaît
> Remarque : la qualité qui a une case bleue est la qualité à laquelle tout support avec ce profil sera continuellement mis à niveau.
{.is-info}

- Icône Plus (<kb>+</kb>) - Créez un nouveau profil de qualité

- Nom - Entrez un nom **UNIQUE** pour le profil de qualité que vous créez
- Mises à niveau autorisées - Lorsque cette option est cochée et que vous demandez à Readarr de télécharger un `EPUB` car c'est la première version d'un livre spécifique, puis plus tard quelqu'un est capable de télécharger un `AZW3`, Readarr se mettra automatiquement à niveau vers une meilleure qualité ***si*** `Mise à niveau jusqu'à` a cette qualité sélectionnée
  - Mise à niveau jusqu'à - Une fois cette qualité atteinte, Readarr ne téléchargera plus de livres

> Remarque : cela s'applique uniquement si vous avez `AZW3` supérieur à `EPUB` dans la section `Qualités`
{.is-warning}

- Qualités - Les qualités les plus élevées dans la liste sont les plus préférées, indépendamment de l'état souhaité (activé/coché). pour le classement indépendamment de l'état activé. Les qualités du même groupe sont égales. Seules les qualités cochées (activées) sont souhaitées (autorisées)
  - Modifier les groupes - Certaines qualités sont regroupées pour réduire la taille de la liste ainsi que les versions similaires. L'exemple typique est `WebDL` et `WebRip` car ils sont très similaires et ont généralement des débits similaires. Lorsque vous modifiez les groupes, vous pouvez modifier la préférence au sein de chacun des groupes.

  - [Voir les qualités](#qualités-définies)

> Par défaut, les qualités sont définies de "pire" (bas) à "meilleure" (haut)
{.is-info}

## Profils de métadonnées

Les profils de métadonnées sont utilisés pour déterminer quels livres de GoodReads ajouter sous un auteur lorsqu'un nouvel auteur est ajouté.

- Icône Plus (<kb>+</kb>) - Créez un nouveau profil de métadonnées

![metaprofiles.png](/assets/readarr/metaprofiles.png)
  
- Nom - Entrez un nom **UNIQUE** pour le profil de métadonnées
- Popularité minimale - Entrez la popularité minimale pour qu'un livre soit ajouté à un auteur.

> Si vous le réglez trop haut, les livres ne seront pas ajoutés à Readarr, mais si vous le réglez trop bas, des publications obscures apparaîtront.
{.is-warning}

> Réglez-le sur `10000000000` exactement pour créer un profil équivalent à `Aucun` mais permettant toujours d'autres filtrages d'éditions et de livres. Notez que `Aucun` n'applique aucun filtre de métadonnées et vous pouvez obtenir des éditions étrangères.
{.is-info}

- Nombre de pages minimum - Entrez le nombre minimum de pages qu'un livre doit avoir pour être ajouté à un auteur.
- Ignorer les livres sans date de sortie - Activez cette option pour ignorer les livres sans date de sortie.
- Ignorer les livres sans ISBN ou ASIN - Activez cette option pour ignorer les livres qui ne contiennent ni un numéro ISBN ni un numéro ASIN.
- Ignorer les livres partiels et les ensembles - Activez cette option pour ignorer les livres partiels et les ensembles.
- Ignorer les livres de séries secondaires - Activez cette option pour ignorer les livres de séries secondaires.
- Langues autorisées - Entrez une liste de codes de langue ISO 639-3 séparés par des virgules, ou 'null' pour les langues autorisées pour vos livres
- Ne doit pas contenir - Entrez des mots ou des phrases qu'un titre de livre ne doit pas contenir pour être ajouté.
  
> Vous pouvez créer plusieurs profils de métadonnées et en appliquer un séparé à chaque auteur selon vos besoins. Cependant, vous ne pouvez appliquer qu'un seul profil de métadonnées à un auteur donné.
{.is-info}
  
## Profils de sortie

Les profils de sortie sont utilisés pour déterminer si les noms de version de l'indexeur sont éligibles pour le téléchargement.

![releaseprofiles.png](/assets/readarr/releaseprofiles.png)  
  
- Activer le profil - Cochez la case pour activer ce profil.
- Doit contenir - Ajoutez une liste de mots ou de phrases qui DOIVENT être dans le nom de la version pour être considérés comme valides.
- Ne doit pas contenir - Ajoutez une liste de mots ou de phrases qui NE DOIVENT PAS être dans le nom de la version pour être considérés comme valides.
- Préféré (Mots) - Ici, vous pouvez ajouter des termes ou des expressions régulières avec des scores (positifs et négatifs) pour être considérés comme plus ou moins préférables. Par exemple, vous pouvez préférer "non abrégé" avec un score positif.
  
> Les versions avec un score de mots préféré plus élevé que le fichier existant sont TOUJOURS une mise à niveau !
{.is-info}
  
- Inclure les mots préférés lors du renommage Cochez cette case pour inclure vos mots préférés (ou les correspondances regex) dans l'attribution de nom de fichier `{Mots préférés}`.
  
> Vous devriez inclure `{Mots préférés}` dans votre nom de fichier, et cocher cette case si vous les utilisez, car sinon vous pouvez vous retrouver dans une boucle de téléchargement.
{.is-warning}

- Indexeur - Dans cette liste déroulante, vous pouvez limiter ce profil de version à un seul indexeur. Cela devrait presque toujours être laissé à `(n'importe lequel)`
- Balises - Entrez une balise ici, pour pouvoir appliquer cette balise aux auteurs ayant la même balise. Si vous n'appliquez pas de balise ici, alors ce profil s'applique à TOUS les auteurs.

## Profils de délai

- Les profils de délai vous permettent de réduire le nombre de versions qui seront téléchargées pour un livre en ajoutant un délai pendant que Readarr continue de rechercher des versions qui correspondent mieux à vos préférences.
- Protocole - Il s'agit soit de `Usenet`, soit de `Torrent` en fonction du protocole de téléchargement que vous préférez
- Délai Usenet - Défini par le nombre de minutes que vous souhaitez attendre avant que le téléchargement ne commence
- Délai Torrent - Défini par le nombre de minutes que vous souhaitez attendre avant que le téléchargement ne commence
- Contourner si meilleure qualité - Contourner le délai lorsque la version a le profil de qualité le plus élevé activé avec le protocole préféré
- Balises - En donnant à ce profil de délai une balise, vous pourrez baliser un livre donné pour qu'il suive les règles définies ici.
- Icône Clé à molette - Cela vous permettra de modifier le profil de délai
- Icône Plus (<kb>+</kb>) - Créez un nouveau profil de délai

### Utilisations

Certains médias recevront une demi-douzaine de versions différentes de qualité variable dans les heures qui suivent leur sortie, et sans profils de délai, Readarr pourrait essayer de toutes les télécharger. Avec les profils de délai, Readarr peut être configuré pour ignorer les premières heures de versions.

Les profils de délai sont également utiles si vous souhaitez mettre l'accent sur un protocole (Usenet ou BitTorrent) plutôt que sur l'autre. (Voir l'exemple 3)

### Fonctionnement des profils de délai

Le chronomètre commence dès que Readarr détecte qu'un livre a une version disponible. Cette version apparaîtra dans votre file d'attente avec une icône d'horloge pour indiquer qu'elle est soumise à un délai.

> L'horloge démarre à partir de l'heure de téléchargement des versions et non à partir du moment où Readarr les voit. {.is-info}

Pendant la période de délai, toutes les nouvelles versions disponibles seront notées par Readarr. Lorsque le chronomètre de délai expire, Readarr téléchargera la seule version qui correspond le mieux à vos préférences de qualité.

La durée du chronomètre peut être différente pour Usenet et les torrents. Chaque profil peut être associé à une ou plusieurs balises pour vous permettre de personnaliser lesquels livres ont quels profils. Un profil de délai sans balise est considéré comme le profil par défaut et s'applique à tous les livres qui n'ont pas de balise spécifique.

> Les profils de délai commencent à partir de l'horodatage que l'indexeur signale comme l'heure de téléchargement de la version. Cela signifie que tout contenu plus ancien que le nombre de minutes que vous avez défini n'est pas impacté de quelque manière que ce soit par votre profil de délai et sera téléchargé immédiatement. De plus, **toutes les recherches manuelles** de contenu (recherches non basées sur des flux RSS) ignoreront les paramètres du profil de délai.
{.is-warning}

#### Exemples

- Pour chaque exemple, supposons que l'utilisateur a le profil de qualité suivant actif : EPUB et au-dessus sont autorisés MOBI est la limite de qualité * AZW3 est la qualité la mieux classée

##### Exemple 1

- Dans cet exemple simple, le profil est défini avec un délai de 120 minutes (deux heures) pour Usenet et Torrent.

- À 23h00, la première version d'un livre est détectée par Readarr et elle a été téléchargée à 22h50 et le chronomètre de 120 minutes commence. À 00h50, Readarr évaluera toutes les versions qu'il a trouvées au cours des deux dernières heures et téléchargera la meilleure, qui est MOBI.

- À 03h00, une autre version est trouvée, qui est MOBI et qui a été ajoutée à votre indexeur à 02h46. Un autre chronomètre de 120 minutes commence. À 04h46, la meilleure version disponible est téléchargée. Comme la limite de qualité est maintenant atteinte, le livre n'est plus améliorable et Readarr cessera de rechercher de nouvelles versions.

- À tout moment, si une version AZW3 est trouvée, elle sera téléchargée immédiatement car c'est la qualité la mieux classée. Si un chronomètre de délai est actuellement actif, il sera annulé.

##### Exemple 2

- Cet exemple a des chronomètres différents pour Usenet et les torrents. Supposons un chronomètre de 120 minutes pour Usenet et un chronomètre de 180 minutes pour BitTorrent.

- À 23h00, la première version d'un livre est détectée par Readarr et les deux chronomètres commencent. La version a été ajoutée à l'indexeur à 22h15. À 00h15, Readarr évaluera toutes les versions et, s'il y a des versions Usenet acceptables, la meilleure sera téléchargée et les deux chronomètres prendront fin. Sinon, Readarr attendra jusqu'à 00h15 et téléchargera la meilleure version, quelle que soit sa source.

##### Exemple 3

- Une utilisation courante des profils de délai est de mettre l'accent sur un protocole plutôt que sur un autre. Par exemple, vous ne voudrez peut-être télécharger une version BitTorrent que si rien n'a été téléchargé sur Usenet après un certain laps de temps.

- Vous pourriez définir un chronomètre de 60 minutes pour BitTorrent et un chronomètre de 0 minute pour Usenet.

- Si la première version détectée provient d'Usenet, Readarr la téléchargera immédiatement.

- Si la première version provient de BitTorrent, Readarr définira un chronomètre de 60 minutes. Si une version Usenet admissible est détectée pendant ce chronomètre, la version BitTorrent sera ignorée et la version Usenet sera téléchargée.

# Qualité

![qualitydefinitions.png](/assets/readarr/qualitydefinitions.png)

## Signification du tableau des qualités

- Qualité - Le nom de qualité de la scène (codé en dur)
- Titre - Le nom de la qualité dans l'interface utilisateur (configurable)
- Mégaoctets par minute - Auto-explicatif
- Limite de taille - Auto-explicatif
- Min - Le nombre minimum d'octets ou de kilooctets par seconde (o/s|ko/s) qu'une qualité peut avoir.
- Max - Le nombre maximum d'octets ou de kilooctets par seconde (o/s|ko/s) qu'une qualité peut avoir.

## Qualités définies

- Texte inconnu - Auto-explicatif
- PDF - Fichier de document portable
- MOBI - L'un des formats de fichier de livre électronique les plus utilisés
- EPUB - Un autre des formats de fichier de livre électronique les plus utilisés
- AZW3 - AZW3 est un fichier de livre électronique développé par Amazon. Il est utilisé dans les Kindle d'Amazon pour visualiser les livres électroniques.
- Audio inconnu - Auto-explicatif
- MP3 - Format audio compressé courant
- M4B - Format de fichier audio courant pour les livres audio
- FLAC - Codec audio sans perte, un format audio similaire au MP3, mais sans perte

# Indexeurs

> Des informations sur les indexeurs pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/readarr/supported#indexers) de cette section
{.is-info}

## Indexeurs pris en charge

- Une liste des indexeurs pris en charge se trouve sur la page [Plus d'informations (Pris en charge)](/readarr/supported#indexers)

### Paramètres de l'indexeur

- Une fois que vous avez cliqué sur le bouton <kb>+</kb> pour ajouter un nouvel indexeur, une nouvelle fenêtre s'ouvre avec de nombreuses options différentes. Aux fins de ce wiki, Readarr considère à la fois les indexeurs Usenet et les trackers BitTorrent comme des "indexeurs".

- Il y a deux sections ici : Usenet et Torrents. En fonction du client de téléchargement que vous utiliserez, vous devrez sélectionner le type d'indexeur que vous utiliserez.

### Configuration de l'indexeur Usenet

- Newznab - Ici, vous trouverez des préréglages des indexeurs Usenet populaires (préremplis, il vous suffira d'ajouter votre clé API fournie par l'indexeur Usenet de votre choix), ainsi que la possibilité de créer un indexeur personnalisé.
- Les logiciels qui fonctionnent avec Usenet et s'intègrent bien avec Readarr sont [NZBHydra2](https://github.com/theotherp/nzbhydra2/) ou [Prowlarr](/prowlarr) qui s'intègrent à la fois à Usenet et aux torrents.
- Que vous choisissiez un indexeur prérempli ou une configuration d'indexeur personnalisée, une nouvelle fenêtre s'affichera pour saisir tous vos paramètres.
- Choisissez parmi les préréglages ou ajoutez un indexeur personnalisé (comme NZBHydra2 ou Prowlarr).
- Nom - Le nom de l'indexeur dans Readarr.
- Activer le flux RSS - Si activé, utilisez cet indexeur pour rechercher les fichiers manquants ou qui n'ont pas encore atteint leur limite.
- Activer la recherche automatique - Si activé, utilisez cet indexeur pour les recherches automatiques, y compris la recherche lors de l'ajout.
- Activer la recherche interactive - Si activé, utilisez cet indexeur pour les recherches interactives manuelles.
- URL - L'URL fournie par l'indexeur, telle que `https://api.nzbgeek.info`.
- Chemin de l'API - Le chemin de l'API fourni par l'indexeur. Il s'agit généralement de `/api`.
- Langues multiples - Définissez les langues `MULTI` pour cet indexeur.
- Clé API - La clé fournie par l'indexeur pour accéder à l'API.
- Catégories - Les catégories par défaut seront utilisées sauf si elles sont modifiées. Il est probable que ces catégories par défaut ne soient pas optimales. Lorsque vous modifiez ce paramètre, Readarr interroge l'indexeur pour obtenir ses catégories disponibles et les affiche dans une liste sélectionnable. Les catégories obsolètes seront effacées dès qu'une catégorie sera activée.
- (Option avancée) Limite de téléchargement anticipé - Temps avant la date de sortie à partir duquel Readarr téléchargera à partir de cet indexeur. Laissez vide pour aucune limite. Cela est similaire à la disponibilité dans Radarr.
- (Option avancée) Paramètres supplémentaires - Paramètres Newznab supplémentaires à ajouter au lien de requête.
- (Option avancée) Priorité de l'indexeur - Priorité de cet indexeur pour préférer un indexeur à un autre dans les scénarios d'égalité de sortie. 1 est la priorité la plus élevée et 50 est la priorité la plus basse.

### Configuration du tracker de torrents

- Comme pour Usenet, il existe une variété de trackers de torrents préremplis. Si vous n'êtes membre d'aucun de ces trackers spécifiques, ils ne vous seront d'aucune utilité.
- L'une des façons les plus simples d'utiliser les trackers de torrents avec Readarr est d'utiliser un autre programme tel que [Prowlarr](/prowlarr) ou [Jackett](https://github.com/Jackett/Jackett). Ces logiciels s'intègrent bien avec Readarr et agissent comme un indexeur de recherche qui regroupe toutes vos informations et les envoie à Readarr.
- Torznab - Cette option vous permettra de configurer un préréglage Jackett. Si vous utilisez plusieurs trackers, chaque entrée doit avoir un nom unique.
- Indexeur Torznab
- Choisissez parmi les préréglages ou ajoutez un indexeur personnalisé (comme Jackett).
- Nom - Le nom de l'indexeur dans Readarr.
- Activer le flux RSS - Si activé, utilisez cet indexeur pour rechercher les fichiers manquants ou qui n'ont pas encore atteint leur limite.
- Activer la recherche automatique - Si activé, utilisez cet indexeur pour les recherches automatiques, y compris la recherche lors de l'ajout.
- Activer la recherche interactive - Si activé, utilisez cet indexeur pour les recherches interactives manuelles.
- URL - L'URL fournie par l'indexeur, telle que `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- Chemin de l'API - Le chemin de l'API fourni par l'indexeur. Il s'agit généralement de `/api`.
- Clé API - La clé fournie par l'indexeur pour accéder à l'API.
- Langues multiples - Définissez les langues `MULTI` pour cet indexeur.
- Catégories - Les catégories par défaut seront utilisées sauf si elles sont modifiées. Il est probable que ces catégories par défaut ne soient pas optimales. Lorsque vous modifiez ce paramètre, Readarr interroge l'indexeur pour obtenir ses catégories disponibles et les affiche dans une liste sélectionnable. Les catégories obsolètes seront effacées dès qu'une catégorie sera activée.
- (Option avancée) Limite de téléchargement anticipé - Temps avant la date de sortie à partir duquel Readarr téléchargera à partir de cet indexeur. Laissez vide pour aucune limite. Cela est similaire à la disponibilité dans Radarr.
- (Option avancée) Paramètres supplémentaires - Paramètres Newznab supplémentaires à ajouter au lien de requête.
- (Option avancée) Priorité de l'indexeur - Priorité de cet indexeur pour préférer un indexeur à un autre dans les scénarios d'égalité de sortie. 1 est la priorité la plus élevée et 50 est la priorité la plus basse.
- (Option avancée) Nombre minimum de sources - Le nombre minimum de sources requis pour qu'une sortie de ce tracker soit téléchargée.
- (Option avancée) Ratio de partage - Si vide, utilisez la valeur par défaut du client de téléchargement. Sinon, le ratio de partage minimum requis pour que votre client de téléchargement le respecte avant qu'il ne soit mis en pause par votre client et supprimé par Readarr (nécessite la gestion des téléchargements terminés - suppression activée).
- (Option avancée) Temps de partage - Si vide, utilisez la valeur par défaut du client de téléchargement. Sinon, le temps de partage minimum en minutes requis pour que votre client de téléchargement le respecte avant qu'il ne soit mis en pause par votre client et supprimé par Readarr (nécessite la gestion des téléchargements terminés - suppression activée).
- (Option avancée) Temps de partage de la discographie - Ignorer, reprendre depuis Lidarr.
- (Option avancée) Priorité de l'indexeur - Priorité de cet indexeur pour préférer un indexeur à un autre dans les scénarios d'égalité de sortie. 1 est la priorité la plus élevée et 50 est la priorité la plus basse.

## Options

- Âge minimum - Usenet uniquement : Âge minimum en minutes des NZB avant leur téléchargement. Utilisez cette option pour laisser aux nouvelles sorties le temps de se propager à votre fournisseur Usenet.
- Conservation - Usenet uniquement : Définissez la valeur sur zéro pour une conservation illimitée.
- Taille maximale - Taille maximale d'une sortie à télécharger en Mo. Définissez la valeur sur zéro pour une taille illimitée. Veuillez noter que cela s'applique globalement.
- Intervalle de synchronisation du flux RSS - Intervalle en minutes. Définissez la valeur sur zéro pour désactiver (cela arrêtera toutes les récupérations automatiques de sorties). Minimum : 10 minutes Maximum : 120 minutes
  - Veuillez consulter [Comment Readarr trouve-t-il des livres ?](/readarr/faq#how-does-readarr-find-books) pour mieux comprendre comment la synchronisation du flux RSS peut vous aider.

> Si Readarr a été hors ligne pendant une période prolongée, Readarr essaiera de revenir en arrière pour trouver la dernière sortie qu'il a traitée afin d'éviter de manquer une sortie. Tant que votre indexeur prend en charge le retour en arrière et que cela n'a pas été trop long, Readarr pourra traiter les sorties qu'il aurait manquées et vous évitera d'avoir à effectuer une recherche pour les sorties manquées.{.is-info}

# Clients de téléchargement

> Des informations sur les clients de téléchargement pris en charge sont disponibles sur la page [Plus d'informations (Pris en charge)](/readarr/supported#download-clients) pour cette section
{.is-info}

## Aperçu

- Le téléchargement et l'importation sont les étapes où la plupart des utilisateurs rencontrent des problèmes. D'un point de vue général, le logiciel doit être capable de communiquer avec votre client de téléchargement et d'avoir accès aux fichiers qu'il télécharge. Il existe une grande variété de clients de téléchargement pris en charge et une encore plus grande variété de configurations. Cela signifie qu'il n'y a pas une seule configuration correcte et que la configuration de chacun peut être légèrement différente. Mais il existe de nombreuses configurations incorrectes.

## Processus du client de téléchargement

### Processus Usenet

- Readarr envoie une demande de téléchargement à votre client et l'associe à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement. Exemples : livres, séries TV, musique, etc.
- Readarr surveille les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Readarr connaît l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia et accessible par Readarr.
- Readarr analyse cet emplacement de fichier terminé pour trouver les fichiers que Readarr peut utiliser. Il analyse le nom du fichier pour le faire correspondre avec le média demandé. S'il peut le faire, il renomme le fichier selon vos spécifications et le déplace vers l'emplacement multimédia spécifié.
- Les déplacements atomiques (déplacements instantanés) sont activés par défaut. Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si le déplacement atomique échoue ou si votre configuration ne prend pas en charge les liens physiques et les déplacements atomiques, Readarr effectuera une copie du fichier, puis le supprimera de la source, ce qui est intensif en termes d'E/S.

### Processus Torrent

- Readarr envoie une demande de téléchargement à votre client et l'associe à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement. Exemples : livres, séries TV, musique, etc.
- Readarr surveille les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de partager le fichier (le ratio ou le temps peut être ajusté dans le client de téléchargement ou depuis Readarr sous le client de téléchargement spécifique). Lorsque les fichiers sont importés dans votre dossier multimédia, Readarr crée un lien physique vers le fichier s'il est pris en charge par votre configuration, sinon il effectue une copie si les liens physiques ne sont pas pris en charge.
- Les liens physiques sont activés par défaut. [Un lien physique ne nécessite pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien physique échoue ou si votre configuration ne prend pas en charge les liens physiques, Readarr effectuera une copie du fichier.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Readarr, Readarr supprimera le fichier et le torrent d'origine de votre client, mais seulement si le client signale que le partage est terminé et que le torrent est arrêté.

## Clients de téléchargement

Cliquez sur `Paramètres => Clients de téléchargement`, puis cliquez sur le <kb>+</kb> pour ajouter un nouveau client de téléchargement. Votre client de téléchargement doit déjà être configuré et en cours d'exécution.

### Clients de téléchargement pris en charge

- Une liste des clients de téléchargement pris en charge se trouve sur la page [Plus d'informations (Pris en charge)](/readarr/supported#download-clients)

Sélectionnez le client de téléchargement que vous souhaitez ajouter, et une boîte de dialogue s'affichera pour saisir les détails de connexion. Ces détails sont similaires pour la plupart des clients. Certains vous demanderont un nom d'utilisateur ou un mot de passe, d'autres vous demanderont si vous souhaitez ajouter de nouveaux téléchargements en pause ou en cours, etc.

### Paramètres du client Usenet

- Nom - Le nom du client de téléchargement dans Readarr.
- Activer - Activer ce client de téléchargement.
- Hôte - L'URL de votre client de téléchargement.
- Port - Le port de votre client de téléchargement.
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- (Option avancée) Base de l'URL - Ajouter un préfixe à l'URL ; cela est souvent nécessaire pour les serveurs proxy inverses.
- Clé API - La clé API pour s'authentifier auprès de votre client.
- Nom d'utilisateur - Le nom d'utilisateur pour s'authentifier auprès de votre client (généralement pas nécessaire).
- Mot de passe - Le mot de passe pour s'authentifier auprès de votre client (généralement pas nécessaire).
- Catégorie - La catégorie dans votre client de téléchargement que \*Arr utilisera. Pour éviter que des téléchargements non liés n'apparaissent dans l'activité, il est fortement recommandé de définir une catégorie.
- Priorité récente - Priorité du client de téléchargement pour les médias récemment sortis.
- Priorité plus ancienne - Priorité du client de téléchargement pour les médias sortis il y a un certain temps.
- (Option avancée) Priorité du client - Priorité du client de téléchargement. La rotation est utilisée pour les clients du même type (torrent/usenet) ayant la même priorité. 1 est la priorité la plus élevée et 50 est la priorité la plus basse.

### Paramètres du client de torrents

- Nom - Le nom du client de téléchargement dans Readarr.
- Activer - Activer ce client de téléchargement.
- Hôte - L'URL de votre client de téléchargement.
- Port - Le port de votre client de téléchargement ; il s'agit généralement du port de l'interface web.
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- (Option avancée) Base de l'URL - Ajouter un préfixe à l'URL ; cela est souvent nécessaire pour les serveurs proxy inverses.
- Nom d'utilisateur - Le nom d'utilisateur pour s'authentifier auprès de votre client.
- Mot de passe - Le mot de passe pour s'authentifier auprès de votre client.
- Catégorie - La catégorie dans votre client de téléchargement que \*Arr utilisera. Pour éviter que des téléchargements non liés n'apparaissent dans l'activité, il est fortement recommandé de définir une catégorie.
- Catégorie après importation - La catégorie à définir après le téléchargement et l'importation de la sortie. Veuillez noter que cela désactive la suppression de la gestion des téléchargements terminés.
- Priorité récente - Priorité du client de téléchargement pour les médias récemment sortis.
- Priorité plus ancienne - Priorité du client de téléchargement pour les médias sortis il y a un certain temps.
- État initial - État initial des torrents (uniquement pour Qbittorrent : forcer contourne tous les seuils de partage).
- (Option avancée) Priorité du client - Priorité du client de téléchargement. La rotation est utilisée pour les clients du même type (torrent/usenet) ayant la même priorité. 1 est la priorité la plus élevée et 50 est la priorité la plus basse.

### Compatibilité de suppression des téléchargements terminés du client de torrents

- Readarr est uniquement capable de définir le ratio de partage/temps sur les clients qui prennent en charge le réglage de cette valeur via leur API lors de l'ajout du torrent. Les objectifs de partage peuvent être définis globalement dans le client lui-même ou par tracker dans les paramètres de \*Arr pour chaque indexeur. Consultez le tableau ci-dessous pour connaître la compatibilité du client.

|      Client       |                                Ratio                                 |                                   Temps                                   |
| :---------------: | :------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
|      Deluge       |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
| Download Station  | ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical) |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
|       Flood       |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |
|     Hadouken      | ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical) |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
|    qBittorrent    |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |
|     rTorrent      |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |
| Torrent Blackhole | ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical) |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
|   Transmission    |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   | ![Limite d'inactivité](https://img.shields.io/badge/Pris%20en%20charge-Limite%20d%27inactivité*-blue) |
|     uTorrent      |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |
|       Vuze        |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |

> ![Limite d'inactivité](https://img.shields.io/badge/Pris%20en%20charge-Limite%20d%27inactivité*-blue) - Transmission dispose d'une vérification interne du temps d'inactivité, mais Readarr la compare avec le temps de partage si la limite d'inactivité est définie pour chaque torrent. Cela est fait en tant que solution de contournement des limitations de l'API de Transmission.{.is-info}

## Gestion des téléchargements terminés

- La gestion des téléchargements terminés est la façon dont Readarr importe les médias de votre client de téléchargement vers vos dossiers de séries. De nombreux problèmes courants sont liés à des chemins Docker incorrects et/ou à d'autres problèmes de permissions Docker.

- Activer - Importer automatiquement les téléchargements terminés à partir du client de téléchargement.
- (Option avancée) Supprimer - Supprimer les téléchargements terminés lorsque le téléchargement est terminé (Usenet) ou arrêté/terminé (torrents).

- Readarr enverra une demande de téléchargement à votre client et l'associera à un label ou à une catégorie que vous avez configurée dans les paramètres du client de téléchargement.
- Readarr surveillera les téléchargements actifs de vos clients de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Readarr connaîtra l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia.
- Readarr analysera cet emplacement de fichier terminé à la recherche de fichiers vidéo. Il analysera le nom du fichier vidéo pour le faire correspondre à un livre. S'il peut le faire, il renommera le fichier selon vos spécifications et le déplacera dans le dossier de bibliothèque assigné.
- Les fichiers restants du téléchargement seront envoyés à la corbeille ou au recyclage.

Si vous téléchargez à l'aide d'un client BitTorrent, le processus est légèrement différent :

- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de les partager. Lorsque les fichiers sont importés dans votre dossier de bibliothèque assigné, Readarr tentera de créer un lien physique vers le fichier ou, en cas d'absence de prise en charge des liens physiques, effectuera une copie (utilisez un double espace).
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres, Readarr demandera au client torrent de supprimer le fichier et le torrent d'origine, mais cela ne se produira que si le client signale que le partage est terminé, que le torrent est dans la même catégorie (c'est-à-dire qu'il n'utilise pas une catégorie post-importation), que l'objectif de partage atteint est pris en charge par Readarr et que le torrent est en pause (arrêté).

### Gestion des téléchargements échoués

- La gestion des téléchargements échoués est uniquement compatible avec SABnzbd et NZBGet.
- La gestion des téléchargements échoués ne s'applique pas aux torrents et il n'est pas prévu d'ajouter une telle fonctionnalité.

- Plusieurs composants composent le processus de gestion des téléchargements échoués :

- Vérification du téléchargeur :
  - File d'attente - Vérifiez la file d'attente de votre téléchargeur pour les versions protégées par mot de passe (cryptées) marquées comme échec
  - Historique - Vérifiez l'historique de votre téléchargeur pour les échecs (par exemple, pas assez pour réparer ou échec de l'extraction)
- Lorsque Readarr trouve un téléchargement échoué, il commence à les traiter et fait quelques choses :
  - Ajoute un événement d'échec à l'historique de Readarr
  - Supprime le téléchargement échoué du client de téléchargement pour libérer de l'espace et effacer les fichiers téléchargés (facultatif)
  - Commence à rechercher un fichier de remplacement (facultatif)
  - La liste de blocage (anciennement appelée "liste noire") permet de sauter automatiquement les fichiers NZB lorsqu'ils échouent, ce qui signifie que le NZB ne sera jamais téléchargé automatiquement par Readarr (vous pouvez toujours forcer le téléchargement via une recherche manuelle).
  - Il existe 2 options avancées (sur la page des paramètres du "Client de téléchargement") qui contrôlent le comportement des téléchargements échoués dans Readarr, pour le moment, elles sont toutes activées par défaut.

- Téléchargement à nouveau - Contrôle si Readarr recherchera à nouveau le même fichier après un échec
- (Option avancée) Supprimer - Indique si le téléchargement doit être automatiquement supprimé du client de téléchargement lorsque l'échec est détecté

## Mappages de chemin distant

- Le mappage de chemin distant agit comme une recherche et un remplacement de chemin distant par un chemin local. Cela est principalement utilisé pour les configurations locales/à distance fusionnées utilisant mergerfs ou similaires, ou est utilisé lorsque l'application et le client de téléchargement ne sont pas sur le même serveur.
- Un mappage de chemin distant est utilisé lorsque votre client de téléchargement signale un chemin pour les données terminées soit sur un autre serveur, soit d'une manière que \*Arr n'adresse pas ce dossier.
- En général, un mappage de chemin distant n'est nécessaire que si votre client de téléchargement est sur Linux lorsque \*Arr est sur Windows ou vice versa. Un mappage de chemin distant peut également être nécessaire si vous mélangez des clients Docker et natifs ou si vous utilisez un serveur distant.
- Un mappage de chemin distant est une recherche/remplacement SIMPLE (où il trouve la valeur DISTANTE, la remplace par la valeur LOCALE pour l'hôte spécifié).
- Si le message d'erreur concernant un mauvais chemin ne contient pas la valeur REMPLACÉE, alors le mappage de chemin ne fonctionne pas comme vous le souhaitez. La solution typique consiste à ajouter et supprimer le mappage.
- [Consultez le tutoriel de TRaSH pour plus d'informations sur le mappage de chemin distant](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Si à la fois \*Arr et votre client de téléchargement sont des conteneurs Docker, il est rare qu'un mappage de chemin distant soit nécessaire. Il est recommandé de [consulter le guide Docker](/docker-guide) et/ou de [suivre le tutoriel de TRaSH](https://trash-guides.info/hardlinks)
{.is-info}

# Importer des listes

> Des informations sur les types de listes pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/readarr/supported#lists) de cette section
{.is-info}

Les listes d'importation vous permettent d'ajouter automatiquement des éléments à Readarr à partir de vos étagères GoodReads ou d'autres utilisateurs. Cela peut potentiellement ajouter beaucoup d'éléments inattendus à votre base de données Readarr, veuillez donc l'utiliser avec précaution.

![importlists.png](/assets/readarr/importlists.png)

## Listes d'importation

Cela vous montre les listes que vous avez actuellement et vous permet d'ajouter de nouvelles listes. L'ajout de listes est expliqué plus en détail ci-dessous.

## Exclusions de listes d'importation

Tout ce qui se trouve ici a été exclu de l'ajout par des listes et ne sera jamais ajouté à partir d'une liste. Vous pouvez supprimer des éléments de cette liste en cliquant dessus.

## Ajout d'une liste d'importation

Après avoir cliqué sur le <kb>+</kb>, choisissez le type de liste que vous souhaitez ajouter :

![addlist.png](/assets/readarr/addlist.png)

Dans cet exemple, nous allons ajouter une liste d'étagères GoodReads.

![bookshelflist.png](/assets/readarr/bookshelflist.png)

- Nom - Entrez un nom pour cette liste.
- Activer l'ajout automatique - Si activé, tout ce qui se trouve sur la liste sera automatiquement ajouté à Readarr.

> Cela ajoutera tous les auteurs et TOUS LES LIVRES de cet auteur à Readarr !

- Surveillance - Sélectionnez votre niveau de surveillance pour les éléments ajoutés. Les options valides sont `Aucun`, `Livre sélectionné` et `Tous les livres de l'auteur`. Tous les livres sont ajoutés à Readarr, mais ils seront surveillés ou non en fonction de cette sélection.
- Rechercher de nouveaux éléments - Si activé, Readarr lancera une recherche pour les éléments manquants surveillés lorsqu'ils sont ajoutés à partir d'une liste. Si vous ajoutez beaucoup d'auteurs/livres surveillés, cela peut surcharger votre système !
- Dossier racine - Choisissez le dossier racine pour les auteurs ajoutés à partir de cette liste
- Profil de qualité - Choisissez votre profil de qualité pour les auteurs ajoutés à partir de cette liste
- Profil de métadonnées - Choisissez votre profil de métadonnées pour les auteurs ajoutés à partir de cette liste
- Balises Readarr - Choisissez les balises qui s'appliquent aux auteurs ajoutés à partir de cette liste

> Il est fortement recommandé d'ajouter une balise descriptive ici. Sinon, vous ne saurez pas quelle liste a ajouté ces éléments à Readarr, et une fois qu'ils sont ajoutés, vous ne pourrez plus obtenir cette information ! Ces informations ne sont pas enregistrées !

Les listes se synchronisent par défaut toutes les 24 heures, mais peuvent être déclenchées manuellement depuis la page `Paramètres` => `Tâches`. Vous ne pouvez pas automatiser ce processus plus rapidement que cela.

# Connexion

> Des informations sur les types de connexion pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/readarr/supported#notifications) de cette section
{.is-info}

## Connexions

Les connexions sont la façon dont vous souhaitez que Readarr communique avec le monde extérieur.

- En appuyant sur le bouton <kb>+</kb>, vous obtiendrez une nouvelle fenêtre qui vous permettra de configurer de nombreux points de terminaison différents.

- Une liste des notifications et connexions prises en charge se trouve sur la page [Plus d'informations (Pris en charge)](/readarr/supported#notifications)

## Déclencheurs de connexion

- Sur la capture - Soyez averti lorsque des livres sont disponibles en téléchargement et ont été envoyés à un client de téléchargement
- Sur l'importation de la version - Soyez averti lorsque les livres sont importés avec succès
- Sur la mise à niveau - Soyez averti lorsque les livres sont mis à niveau vers une meilleure qualité
- En cas d'échec du téléchargement - Soyez averti en cas d'échec du téléchargement d'un livre (usenet uniquement)
- En cas d'échec de l'importation - Soyez averti en cas d'échec de l'importation d'un livre
- Sur le renommage - Soyez averti lorsque les livres sont renommés
- Sur la suppression de l'auteur - Soyez averti lorsque un auteur est supprimé
- Sur la suppression du livre - Soyez averti lorsque un livre est supprimé
- Sur la suppression du fichier du livre - Soyez averti lorsque le fichier d'un livre est supprimé
- Sur la suppression du fichier du livre pour une mise à niveau - Soyez averti lorsque le fichier d'un livre est supprimé pour une mise à niveau
- Sur la retagification du livre - Soyez averti lorsque les livres sont retagifiés
- Sur les problèmes de santé - Soyez averti en cas d'échec de la vérification de santé
  - Inclure les avertissements de santé - Soyez averti des avertissements de santé en plus des erreurs.

# Métadonnées

{#write-metadata-to-book-files}

> Des informations sur les consommateurs de métadonnées pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/readarr/supported#metadata) de cette section
{.is-info}

Cette page vous permet de créer/mettre à jour des balises/couvertures de métadonnées.

![metadata.png](/assets/readarr/metadata.png)

## Métadonnées Calibre

Si vous utilisez Calibre pour gérer votre collection de livres électroniques, vous utiliserez ces options pour le contrôler.

- Envoyer les métadonnées à Calibre
  - Tous les fichiers ; synchroniser avec GoodReads - Écrire les balises dans tous les fichiers et les mettre à jour si GoodReads les met à jour
  - Tous les fichiers ; importation initiale uniquement - Écrire les balises dans tous les fichiers une fois et ne pas les mettre à jour si GoodReads les met à jour
  - Uniquement pour les nouveaux téléchargements - Écrire les balises uniquement dans les nouveaux téléchargements lorsqu'ils sont importés
- Mettre à jour les couvertures - Activer pour indiquer à Calibre Content Server d'utiliser les mêmes couvertures de livre que Readarr
- Intégrer les métadonnées dans les fichiers de livre - Activer pour indiquer à Calibre Content Server d'écrire et d'intégrer les métadonnées dans les fichiers de livre.

## Écrire les métadonnées dans les fichiers audio

Si vous utilisez des livres audio, vous utiliserez ces options pour le contrôler.

- Baliser les fichiers audio avec les métadonnées
  - Tous les fichiers ; synchroniser avec GoodReads - Écrire les balises dans tous les fichiers et les mettre à jour si GoodReads les met à jour
  - Tous les fichiers ; importation initiale uniquement - Écrire les balises dans tous les fichiers une fois et ne pas les mettre à jour si GoodReads les met à jour
  - Uniquement pour les nouveaux téléchargements - Écrire les balises uniquement dans les nouveaux téléchargements lorsqu'ils sont importés
- Nettoyer les balises existantes - Activer pour supprimer toutes les balises des fichiers, sauf celles ajoutées par Readarr

# Balises

- La section des balises dans Readarr est utilisée pour lier différents aspects de Readarr.
- Les balises sont particulièrement utiles pour :

  - Profils de versions
  - Indexeurs
  - Listes d'importation

- Les balises peuvent être utilisées pour lier des profils de versions, des indexeurs, des listes d'importation et des auteurs/livres ensemble.
- Par exemple :
  - Vous voulez qu'un auteur/livre spécifique utilise uniquement un indexeur spécifique. Vous créeriez une balise et assigneriez l'auteur/livre et l'indexeur à cette balise.
  - Vous voulez qu'une liste d'importation spécifique utilise uniquement un profil de version spécifique. Vous créeriez une balise et assigneriez la liste d'importation et le profil de version à cette balise.

> Il est fortement recommandé d'ajouter une balise descriptive à une liste d'importation en plus de ce qui est mentionné ci-dessus.

> Remarque : Les balises n'influencent pas les "Profils de qualité", les "Profils de métadonnées" ou tout autre aspect non mentionné ci-dessus.
{.is-info}

# Général

Cette page contient les paramètres généraux de Readarr qui ne sont pas couverts dans d'autres sections.

## Hôte

![genhost.png](/assets/readarr/genhost.png)

- Adresse de liaison - Adresse IP4 valide ou '*' pour toutes les interfaces
  - 0.0.0.0 ou `*` - toutes les adresses peuvent se connecter
  - 127.0.0.1 ou localhost - seules les applications locales peuvent se connecter
  - Toute autre IP (par exemple, 1.2.3.4) - seule cette IP (1.2.3.4) peut se connecter
- Numéro de port - Le numéro de port que vous souhaitez utiliser pour accéder à l'interface Web de Readarr

> Remarque : Si vous utilisez Docker, ne modifiez pas ce paramètre.
{.is-warning}

- Base URL - Pour prendre en charge un proxy inverse, la valeur par défaut est vide

> Remarque : Si vous utilisez un proxy inverse (par exemple : mondomaine.com/readarr), vous devez entrer '/readarr' pour la base URL.
{.is-info}

- Activer SSL - Si vous disposez de certificats SSL et que vous souhaitez sécuriser la communication vers et depuis votre Readarr, activez cette option.

> Remarque : N'utilisez pas cela à moins de savoir ce que vous faites.
{.is-warning}

## Sécurité

![gensecurity.png](/assets/readarr/gensecurity.png)

- Authentification - Comment souhaitez-vous vous authentifier pour accéder à votre instance Readarr
  - Aucune - Vous n'avez pas besoin d'authentification pour accéder à votre Readarr. Généralement, si vous êtes le seul utilisateur de votre réseau, si vous n'avez personne sur votre réseau qui souhaiterait accéder à votre Readarr ou si votre Readarr n'est pas exposé sur le Web
  - Basique (pop-up du navigateur) - Cette option, lors de l'accès à votre Readarr, affiche une petite fenêtre contextuelle vous permettant de saisir un nom d'utilisateur et un mot de passe
  - Formulaires (page de connexion) - Cette option affiche un écran de connexion familier, comme le font d'autres sites Web, pour vous permettre de vous connecter à votre Readarr
- Clé API - C'est ainsi que d'autres programmes communiquent ou font communiquer Readarr avec d'autres programmes. Cette clé, si elle est donnée à la mauvaise personne ayant accès, pourrait faire toutes sortes de choses à votre bibliothèque. C'est pourquoi dans les journaux, la clé API est masquée
- Validation du certificat - Modifiez la rigueur de la validation du certificat HTTPS
  - Activée - Valider tous les certificats HTTPS (recommandé)
  - Désactivée pour les adresses locales - Valider tous les certificats HTTPS sauf ceux sur localhost et le LAN
  - Désactivée - Ne pas valider les certificats HTTPS

## Proxy

![genproxy.png](/assets/readarr/genproxy.png)

- Proxy - Cette option vous permet de faire passer les informations que votre Radarr récupère et recherche par un proxy. Cela peut être utile si vous vous trouvez dans un pays qui n'autorise pas le téléchargement de fichiers Torrent.

- Utiliser un proxy - Activer pour utiliser un proxy
- Type de proxy - Sélectionnez votre type de proxy (HTTPS, Socks4 ou Socks5)
- Nom d'hôte - Entrez le nom d'hôte de votre proxy (Ne pas inclure http/https ou tout autre protocole)
- Port - Entrez le port de votre proxy
- Nom d'utilisateur - Entrez le nom d'utilisateur de votre proxy si applicable
- Mot de passe - Entrez le mot de passe de votre proxy si applicable
- Adresses ignorées - Entrez une liste séparée par des virgules d'adresses qui contournent le proxy
- Ignorer le proxy pour les adresses locales - Cochez la case pour contourner le proxy pour les adresses locales.

## Journalisation

![genlogging.png](/assets/readarr/genlogging.png)

- Niveau de journalisation - L'un des outils de dépannage les plus utiles
  - Info - C'est la façon la plus basique dont Readarr recueille des informations, cela inclura une quantité très minimale d'informations dans les journaux. Ce fichier journal contient des entrées fatales, d'erreur, d'avertissement et d'info.
  - Debug - Le débogage inclura toutes les informations incluses dans Info ainsi que des informations supplémentaires qui peuvent être utiles. Ce fichier journal contient des entrées fatales, d'erreur, d'avertissement, d'info et de débogage.
  - Trace - Le journal le plus avancé et détaillé sur Readarr, Trace inclura toutes les informations recueillies par Info et Debug et plus encore. C'est le type de journal le plus courant qui sera demandé lors du dépannage sur Discord ou Reddit. Si vous avez besoin d'aide, veuillez sélectionner votre journal en mode Trace et refaire la tâche qui vous posait problème pour capturer le journal. Ce fichier journal contient des entrées fatales, d'erreur, d'avertissement, d'info, de débogage et de trace.

## Analyse

![genanalytics.png](/assets/readarr/genanalytics.png)

- Analyse - Envoyer des informations d'utilisation et d'erreurs anonymes aux serveurs de Readarr (Servarr). Cela inclut des informations sur votre navigateur, les pages de l'interface Web de Readarr que vous utilisez, les rapports d'erreurs ainsi que la version du système d'exploitation et de l'exécution. Nous utiliserons ces informations pour hiérarchiser les fonctionnalités et les corrections de bugs.

## Mises à jour

![genupdates.png](/assets/readarr/genupdates.png)

- (Option avancée) Branche - Il s'agit de la branche de Readarr que vous utilisez.
  - [Veuillez consulter cette entrée de FAQ pour plus d'informations](/readarr/faq#how-do-i-update-readarr)
- Automatique - Téléchargez et installez automatiquement les mises à jour. Vous pourrez toujours installer depuis Système : Mises à jour. Remarque : Les utilisateurs de Windows sont toujours mis à jour automatiquement.
- Mécanisme - Utilisez le programme de mise à jour intégré de Readarr ou un script
  - Intégré - Utilisez le propre programme de mise à jour de Readarr
  - Script - Faites en sorte que Readarr exécute le script de mise à jour
  - Docker - Ne mettez pas à jour Readarr depuis l'intérieur du Docker, mais tirez plutôt une nouvelle image avec la nouvelle mise à jour
- Script - Visible uniquement lorsque le mécanisme est défini sur Script - Chemin vers le script de mise à jour
- Processus de mise à jour - Readarr téléchargera le fichier de mise à jour, vérifiera son intégrité, l'extraiera dans un emplacement temporaire et appellera la méthode choisie. Le processus de mise à jour sera exécuté sous le même utilisateur que celui sous lequel Readarr est exécuté, il aura besoin des autorisations pour mettre à jour les fichiers de Readarr ainsi que pour arrêter/démarrer Readarr.
- Intégré - La méthode intégrée sauvegardera les fichiers et les paramètres de Readarr, arrêtera Readarr, mettra à jour l'installation et démarrera Readarr. Si votre système ne gère pas l'arrêt de Readarr et tente de le redémarrer automatiquement, il est peut-être préférable d'utiliser un script à la place. En cas d'échec, la version précédente de Readarr sera redémarrée.
- Script - Le script devrait gérer la même chose que le programme de mise à jour intégré, si vous devez gérer l'arrêt et le démarrage des services (upstart/launchd/etc), vous devrez le faire ici.

## Sauvegardes

![genbackups.png](/assets/readarr/genbackups.png)

- La section des sauvegardes vous permet de définir comment vous souhaitez que Readarr gère les sauvegardes

- Dossier - Cela vous permet de sélectionner l'emplacement de sauvegarde. Dans Docker, vous serez limité à ce que vous permettez au conteneur de voir. Les chemins sont relatifs au dossier appdata ; si nécessaire, vous pouvez définir un chemin absolu pour sauvegarder en dehors du dossier appdata.
- Intervalle - À quelle fréquence souhaitez-vous que Readarr effectue une sauvegarde
- Rétention - Combien de temps souhaitez-vous que Readarr conserve chaque sauvegarde. Après la création d'une nouvelle sauvegarde, la plus ancienne sera supprimée

Par défaut, les sauvegardes sont effectuées tous les 7 jours et les 4 dernières sont conservées.

# Interface utilisateur (UI)

Cette page vous permet de personnaliser les options d'affichage de l'interface utilisateur.

## Calendrier

![uicalendar.png](/assets/readarr/uicalendar.png)

- Premier jour de la semaine - Ici, vous pouvez sélectionner le premier jour de la semaine.
- En-tête de colonne de la semaine - Ici, vous pouvez sélectionner l'en-tête des colonnes.

## Dates

![caldates.png](/assets/readarr/caldates.png)

- Format de date court - Comment souhaitez-vous que Readarr affiche les dates courtes ?
- Format de date long - Comment souhaitez-vous que Readarr affiche les dates au format long ?
- Format de l'heure - Souhaitez-vous un format de 12 heures ou de 24 heures ?
- Afficher les dates relatives - Souhaitez-vous que Readarr affiche des dates relatives (Aujourd'hui/Hier/etc) ou des dates absolues ?

## Style

![calstyle.png](/assets/readarr/calstyle.png)

- Activer le mode pour les personnes atteintes de daltonisme - Style modifié pour permettre aux utilisateurs atteints de daltonisme de mieux distinguer les informations codées par couleur.

## Langue

![callanguage.png](/assets/readarr/callanguage.png)

- Langue de l'interface utilisateur - Sélectionnez la langue que Radarr doit utiliser dans l'interface de l'application.