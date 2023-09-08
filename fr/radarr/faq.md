## Est-ce que tous mes fichiers de films peuvent être stockés dans un seul dossier ?

- Oui, Radarr vous permet de stocker tous vos fichiers de films dans un seul dossier si vous le souhaitez. Cependant, il est important de noter que cela peut rendre la gestion de votre bibliothèque de films plus difficile, en particulier si vous avez une grande collection de films. Il est recommandé d'organiser vos fichiers de films dans des dossiers séparés par film pour une meilleure organisation et une recherche plus facile.

- Non, et la raison en est que Radarr est un fork de [Sonarr](/sonarr), où chaque émission a un dossier. Cette limitation est un point douloureux connu pour de nombreux utilisateurs et peut-être sera-t-elle prise en compte dans une version future. Veuillez noter que ce n'est pas un simple changement et qu'il nécessite effectivement une réécriture complète du backend.
- La [question GitHub sur les dossiers personnalisés](https://github.com/Radarr/Radarr/issues/153) couvre techniquement cette demande, mais cela ne garantit pas que tous les fichiers de film dans un seul dossier seront implémentés à ce moment-là.
- Une solution légèrement bricolée est décrite ci-dessous. Veuillez noter que vous ne devez pas déclencher une nouvelle analyse dans Radarr, sinon elle sera considérée comme manquante et le film ne sera jamais mis à niveau.
  - Utilisez un script personnalisé
    - Le script doit être déclenché lors de l'importation
    - Il doit être conçu pour déplacer le fichier quand vous le souhaitez
    - Ensuite, il doit appeler l'API Radarr et changer le film en non surveillé.
- Si vous souhaitez déplacer tous vos films d'un seul dossier vers des dossiers individuels, consultez l'article [Section Astuces et Conseils => Créer un dossier pour chaque film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

## Puis-je mettre tous mes films de ma bibliothèque dans un seul dossier ?

- Non, voir ci-dessus.

## Comment mettre à jour Radarr ?

- Allez dans Paramètres, puis l'onglet Général et affichez les paramètres avancés (utilisez le bouton bascule près du bouton Enregistrer).

1. Dans la section Mises à jour, changez le nom de la branche en `master` ou `develop`
1. Enregistrez

*Cela n'installera pas immédiatement les éléments de cette branche, cela se produira lors de la prochaine mise à jour.*

- ![Master/Stable actuel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (Par défaut/Stable) : Il a été testé par les utilisateurs sur les branches develop et nightly et il n'est pas connu pour avoir de problèmes majeurs. Cette version recevra des mises à jour environ une fois par mois. Sur GitHub, il s'agit de la branche `master`.

- ![Develop/Beta actuel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (Beta) : Il s'agit de la version de test. Elle est publiée après avoir été testée en nightly pour s'assurer qu'il n'y a pas de problèmes immédiats. Les nouvelles fonctionnalités et les corrections de bugs sont d'abord publiées ici après la nightly. Elle peut être considérée comme semi-stable, mais reste en version `beta`. Cette version recevra des mises à jour hebdomadaires ou bihebdomadaires en fonction du développement.

> **Attention : Vous ne pourrez peut-être pas revenir à `master` après avoir basculé sur cette branche.** Sur GitHub, il s'agit d'un instantané de la branche `develop` à un moment précis.
{.is-warning}

- ![Nightly/Instable actuel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (Alpha/Instable) : Il s'agit de la version de pointe. Elle est publiée dès que le code est validé et passe tous les tests automatisés. Cette version n'a peut-être pas encore été utilisée par nous ou d'autres utilisateurs. Il n'y a aucune garantie qu'elle fonctionnera même dans certains cas. Cette branche est recommandée uniquement pour les utilisateurs avancés. Des problèmes et des investigations personnelles sont attendus dans cette branche. ***Utilisez cette branche uniquement si vous savez ce que vous faites et êtes prêt à mettre les mains dans le cambouis pour récupérer une mise à jour échouée.*** Cette version est mise à jour immédiatement.

> **Attention : Vous ne pourrez peut-être pas revenir à `master` après avoir basculé sur cette branche.** Sur GitHub, il s'agit de la branche `develop`.
{.is-danger}

- Remarque : Si vous utilisez Docker, ajoutez `:release`, `:latest`, `:testing` ou `:develop` à la fin de votre balise de conteneur en fonction de qui crée vos builds.

|                                                                    | ![Master/Latest actuel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Develop/Beta actuel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Nightly/Alpha actuel](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Puis-je mettre à jour Radarr à l'intérieur de mon conteneur Docker ?

- *Techniquement, oui.* **Mais vous ne devriez absolument pas le faire.** C'est une philosophie fondamentale de Docker. Des problèmes de base de données peuvent survenir si vous mettez à niveau votre installation vers la version `nightly` la plus récente, puis mettez à jour le conteneur Docker lui-même (éventuellement en revenant à une version plus ancienne).

### Installation d'une version plus récente

#### Native

1. Allez dans Système, puis l'onglet Mises à jour
1. Les versions plus récentes qui ne sont pas encore installées auront un bouton de mise à jour à côté d'elles, cliquez sur ce bouton pour installer la mise à jour.

#### Docker

1. Re-téléchargez votre balise et mettez à jour votre conteneur

## Puis-je passer de `nightly` à `develop` ?

## Puis-je passer d'une branche à une autre ?

- Si les versions sont identiques, vous pouvez passer d'une branche à l'autre, sinon vérifiez avec l'équipe de développement si vous pouvez passer de `nightly` à `master` ; `nightly` à `develop` ; ou `develop` à `master` pour votre build spécifique.
- Si vous ne suivez pas ces instructions, votre Radarr risque de devenir inutilisable ou de générer des erreurs. Vous avez été prévenu. Si les erreurs suivantes se produisent, cela signifie que vous utilisez une base de données plus récente avec une version \*Arr plus ancienne, ce qui n'est pas pris en charge. Mettez à niveau \*Arr vers la version que vous utilisiez précédemment ou une version plus récente.
  - Exemples de messages d'erreur :
    - `Erreur d'analyse de la colonne 45 (Language=31 - Int64)`
    - `Le DataMapper n'a pas pu charger le champ suivant : 'Languages' value`
    - `ID ne correspond pas à une langue connue Nom du paramètre : id`
    - Autres erreurs de base de données similaires concernant des colonnes ou des tables manquantes.

## Comment sauvegarder/restaurer Radarr ?

### Sauvegarde de Radarr

#### Utilisation de la sauvegarde intégrée

- Allez dans Système => Sauvegarde dans l'interface utilisateur de Radarr
- Cliquez sur le bouton Sauvegarder
- Téléchargez le fichier zip après la création de la sauvegarde pour le mettre en lieu sûr

#### Utilisation du système de fichiers directement

- Trouvez l'emplacement du répertoire AppData de Radarr
  - Via l'interface utilisateur de Radarr, allez dans Système => À propos
  - [Répertoire AppData de Radarr](/radarr/appdata-directory)
- Arrêtez Radarr - Cela empêchera la base de données de se corrompre
- Copiez le contenu vers un emplacement sûr

### Restauration à partir d'une sauvegarde

> La restauration sur un système d'exploitation qui utilise des chemins différents ne fonctionnera pas (Windows vers Linux, Linux vers Windows, Windows vers OS X ou OS X vers Windows), le passage entre OS X et Linux peut fonctionner, car les deux utilisent des chemins contenant `/` au lieu de `\` utilisé par Windows, mais ce n'est pas pris en charge. Vous devrez modifier manuellement tous les chemins dans la base de données ou utiliser [Toolbarr](https://github.com/Notifiarr/toolbarr).
{.is-warning}

#### Utilisation de la sauvegarde au format zip

- Réinstallez Radarr (si applicable / non déjà installé)
- Lancez Radarr
- Accédez à Système => Sauvegarde
- Sélectionnez Restaurer la sauvegarde
- Sélectionnez Choisir le fichier
- Sélectionnez votre fichier de sauvegarde au format zip
- Sélectionnez Restaurer

#### Utilisation de la sauvegarde du système de fichiers

- Réinstallez Radarr (si applicable / non déjà installé)
- Trouvez l'emplacement du répertoire AppData de Radarr
  - Exécutez Radarr une fois et via l'interface utilisateur, allez dans Système => À propos
  - [Répertoire AppData de Radarr](/radarr/appdata-directory)
- Arrêtez Radarr
- Supprimez le contenu du répertoire AppData **(y compris les fichiers .db-wal/.db-journal s'ils existent)**
- Restaurez à partir de votre sauvegarde
- Démarrez Radarr
- Tant que les chemins sont les mêmes, tout reprendra là où cela s'était arrêté

#### Restauration du système de fichiers sur un NAS Synology

> ATTENTION : La restauration sur un Synology nécessite des connaissances en Linux et un accès SSH root à l'appareil Synology.
{.is-warning}

- Réinstallez Radarr (si applicable / non déjà installé)
- Trouvez l'emplacement du répertoire AppData de Radarr
  - Exécutez Radarr une fois et via l'interface utilisateur, allez dans Système => À propos
  - [Répertoire AppData de Radarr](/radarr/appdata-directory)
- Arrêtez Radarr
- Connectez-vous au NAS Synology via SSH et connectez-vous en tant que root

> Sur certaines installations, l'utilisateur est différent des commandes ci-dessous : `chown -R sc-Radarr:Radarr *` {.is-info}

- Exécutez les commandes suivantes :

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- Mettez à jour les autorisations sur les fichiers :

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- Démarrez Radarr

# Problèmes courants avec Radarr

## Une tâche a été annulée

- Radarr n'a reçu aucune réponse du serveur auquel la demande a été adressée après 100 secondes.
- Les journaux contiendront `System.Threading.Tasks.TaskCanceledException: A task was canceled.` (Une tâche a été annulée).
- Cela est souvent causé par :
  - une configuration incorrecte ou l'utilisation d'un VPN
  - une configuration incorrecte ou l'utilisation d'un proxy
  - des problèmes DNS locaux - Essayez de passer à un autre fournisseur DNS
  - des problèmes IPv6 locaux - *le plus courant* - généralement, IPv6 est activé sur le système hôte, mais non fonctionnel
  - l'utilisation de Privoxy et une configuration incorrecte de celui-ci
  - des requêtes de PiHole [Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit)
- Vous pouvez effectuer des tests de dépannage avec DNS `nslookup <domaine.tld à partir des journaux de trace>` et IPv6 avec `curl -sv -6 "<URL à partir des journaux de trace>"` / toute autre connectivité avec `curl -sv -4 "<URL à partir des journaux de trace>"`

## Le chemin est déjà configuré pour un film existant

![existing-movie.png](/assets/radarr/existing-movie.png)

- L'importation de la bibliothèque affiche "Existant" ou vous obtenez une erreur "Le chemin est configuré pour un film existant"
- Cela se produit lorsque vous essayez d'ajouter un film ou de modifier le chemin d'un film existant qui est déjà attribué à un autre film.
- Il est probable que cela soit dû à une erreur de correspondance de film lorsque l'utilisateur a importé sa bibliothèque.
- Localisez et corrigez le film qui est déjà attribué à ce chemin de film.
  - Index des films
  - Vue en tableau
  - Options => Ajouter le chemin en tant que colonne
  - Triez et trouvez le film au chemin problématique noté.
- Sinon, supprimez le film utilisant le chemin existant de Radarr

## Comment puis-je renommer mes dossiers de films ?

{#rename-folders}

> Le même processus s'applique également pour déplacer/changer les chemins des films. Si vous mettez simplement à jour les chemins dans Radarr et que vous n'avez pas besoin de déplacer les fichiers, ne sélectionnez pas "Oui, déplacer les fichiers" à l'étape 5.
{.is-info}

1. Films
1. Éditeur de films
1. Sélectionnez les films dont le dossier doit être renommé
1. Changez le dossier racine en le même dossier racine dans lequel les films se trouvent actuellement
1. Sélectionnez "Oui, déplacer les fichiers"

> Si vous utilisez Plex, cela déclenchera la redétection des intros, des vignettes, des chapitres et des métadonnées de prévisualisation.
{.is-warning}

## Nom des fichiers et dossiers de films

- Actuellement, Radarr exige que chaque film soit dans un dossier avec le format contenant au minimum `Titre du film (Année)/`, les séparateurs `_` ou `.` sont également valides. Pour faciliter l'identification correcte de la qualité et de la résolution lors de l'importation, un nom de fichier tel que `Titre du film (Année) [Qualité-Résolution].ext` est préférable, encore une fois, les séparateurs `_` ou `.` sont également valides.

  - Un outil utile pour effectuer ces modifications sur votre collection est [filebot](http://www.filebot.net/#download) qui a une version payante dans les magasins Apple et Windows, mais qui peut être trouvée gratuitement sur leur ancien site [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download). Il dispose à la fois d'une interface graphique et d'une interface en ligne de commande, vous pouvez donc utiliser celle avec laquelle vous êtes à l'aise. Pour l'exemple ci-dessus, `{ny}` se développe en `Nom (Année)` et `{vf}` donne la résolution comme `1080p`. Il n'y a rien à déduire de la qualité, vous pouvez donc la simuler en utilisant `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]` qui nommera tout ce qui est inférieur à 720p en `[DVD-572p]` et supérieur ou égal à 720p en `[Bluray-1080p]`.

- Voir la section [Trucs et astuces => Créer un dossier pour chaque film](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie) pour plus de détails.

## Dossiers de films mal nommés

- Le nom du dossier de film est basé sur les métadonnées (nom/année) au moment où le film a été ajouté. Si vous avez ajouté un film avant sa sortie, vous devrez peut-être utiliser l'astuce de renommage du dossier mentionnée ci-dessus pour mettre à jour le nom du dossier du film afin de refléter les nouvelles données actuelles.
- Même si vos films sont déjà dans des dossiers, les dossiers peuvent ne pas être correctement nommés. Le nom du dossier doit être `Titre du film (Année)`, avoir le titre et l'année dans le nom du dossier est actuellement essentiel.

  - Exemples qui fonctionneront bien :
    - `/mnt/Films/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Films pour enfants/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - Exemples qui fonctionneront, mais nécessiteront une gestion manuelle :
    - Par lettres : `/mnt/Films/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Par classement : `/mnt/Films/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Par genre : `/mnt/Films/Crime, Drame, Science-fiction/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Ces exemples nécessiteront une gestion manuelle lors de l'ajout du film. Chacun des exemples aura de nombreux répertoires racine, comme `A-D` et `E-G` dans le premier exemple de lettre, `R` et `PG-13` dans l'exemple de classement, et vous pouvez deviner la variété de dossiers de genre. Lors de l'ajout d'un nouveau film, le bon dossier de base devra être sélectionné pour que ce format fonctionne.
  - Exemples qui ne fonctionneront pas :
    - Dossier unique : `/mnt/Films pour enfants/Frozen (2013) [Bluray-1080p].mkv`
      - À l'heure actuelle, les films doivent simplement être dans un dossier portant le nom du film. Il n'y a pas d'autre solution jusqu'à ce que des travaux de développement soient effectués pour ajouter cette fonctionnalité.
    - Les formats de nom de dossier de film à partir de la version 0.2 qui incluent les propriétés de fichier dans le nom du dossier de film comme ``{Movie.Title}.{Release Year}.{Quality.Full}-{MediaInfo.Simple}{`Release.Group}`` ne fonctionneront pas dans la version 3.
      - Les dossiers sont liés au film et indépendants du fichier. De plus, cela ne fonctionnera pas avec la prise en charge prévue de plusieurs fichiers par film.
      - L'autre raison pour laquelle cela a été supprimé est qu'il causait fréquemment des confusions, des corruptions de base de données et était généralement mal conçu.
  - La section [Trucs et astuces => Créer un dossier pour chaque film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) est une excellente source pour vous assurer que votre structure de fichiers et de dossiers fonctionnera parfaitement.

## Puis-je désactiver la tâche de rafraîchissement des films

- Non, et vous ne devriez pas le faire non plus en utilisant des astuces SQL. La tâche de rafraîchissement des films interroge le proxy Servarr en amont et vérifie si les métadonnées de chaque film (identifiants, casting, résumé, évaluation, traductions, titres alternatifs, etc.) ont été mises à jour par rapport à ce qui est actuellement dans Radarr. Si nécessaire, il mettra ensuite à jour les films concernés.
- Une plainte courante est que la tâche de rafraîchissement provoque une utilisation intensive de l'E/S.
- Le paramètre principal est "Rescan Movie Folder after Refresh". Si votre utilisation de l'E/S du disque augmente pendant un rafraîchissement, vous voudrez peut-être modifier le paramètre de rescan en `Manuel`.
  - Ne le changez pas en `Jamais` à moins que toutes les modifications de votre bibliothèque (nouveaux films, mises à niveau, suppressions, etc.) ne soient effectuées via Radarr.
  - Si vous supprimez manuellement des fichiers de films ou via Plex ou un autre programme tiers, ne définissez pas cela sur `Jamais`.
- L'autre paramètre qui peut être modifié est "Analyze video files", qui est conseillé d'activer si vous utilisez tdarr ou si vous modifiez vos fichiers de manière externe. Si ce n'est pas le cas, vous pouvez désactiver en toute sécurité "Analyze video files" pour réduire une partie de l'E/S.

## Comment puis-je demander une fonctionnalité pour Radarr ?

- C'est facile [cliquez ici](https://github.com/Radarr/Radarr/issues)

## Aide, mon Mac dit que Radarr ne peut pas être ouvert car le développeur ne peut pas être vérifié

- C'est simple, veuillez consulter ce lien pour plus d'informations [ici](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Le développeur ne peut pas être vérifié](developer-cannot-be-verified.png "Le développeur ne peut pas être vérifié")
- Alternativement, vous devrez peut-être auto-signer Radarr `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## Aide, mon Mac dit que Radarr.app est endommagé et ne peut pas être ouvert

- Cela est dû soit à un téléchargement corrompu, essayez à nouveau, soit à des problèmes de sécurité, veuillez consulter cette entrée FAQ connexe.](#help-my-mac-says-radarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## J'obtiens une erreur : Database disk image is malformed

> \* Pour les utilisateurs de Radarr qui rencontrent ce problème après la mise à niveau vers les versions v4.X. Les versions v4 effectuent plusieurs migrations de grande envergure, de sorte que si votre base de données avait une corruption antérieure à un endroit quelconque (qui n'aurait peut-être pas été détectable en exécutant précédemment Radarr), la migration échouera. Cela provoquera l'échec du démarrage de Radarr. Il est probable que toutes vos sauvegardes soient également corrompues, donc la simple restauration de celles-ci ne résoudra probablement pas le problème.
> \* Si la base de données post-migrée ne s'ouvre pas ou ne peut pas être récupérée, faites une copie de la base de données à partir d'une sauvegarde récente et appliquez le processus de récupération de la base de données à ce fichier, puis essayez de démarrer Radarr avec le fichier de sauvegarde récupéré. Il devrait ensuite migrer sans problème.
{.is-warning}

- **Les erreurs de `Error creating log database` indiquent des problèmes avec logs.db**
  - Cela peut être rapidement résolu en renommant ou en supprimant la base de données. La base de données des journaux contient des informations non importantes concernant l'historique des commandes et l'historique des installations de mise à jour, ainsi que des entrées Info, Warn et Error.
- **Les erreurs de `Error creating main database` ou `database disk image is malformed` génériques sans base de données spécifiée indiquent des problèmes avec radarr.db**
  - Poursuivez avec les étapes indiquées ci-dessous
- Cela signifie que votre base de données SQLite qui stocke la plupart des informations de Radarr est corrompue. Vos options sont d'essayer (un) (des) sauvegarde(s), d'essayer de récupérer la base de données existante, d'essayer de récupérer la (les) sauvegarde(s), ou si tout le reste échoue, de recommencer avec une nouvelle base de données fraîche.
- Cette erreur peut apparaître si le fichier de base de données n'est pas accessible en écriture par l'utilisateur/groupe sous lequel \*Arr s'exécute. Les autorisations étant la cause, cela ne sera probablement un problème que pour les nouvelles installations, les installations migrées vers un nouveau serveur, si vous avez récemment modifié les autorisations de votre répertoire appdata, ou si vous avez modifié l'utilisateur et le groupe sous lesquels \*Arr s'exécute.
- Votre meilleure et première option est d'essayer de [restaurer à partir d'une sauvegarde](#how-do-i-backuprestore-my-radarr). Cependant, pour les utilisateurs qui reçoivent cette erreur après la mise à niveau vers la version 4, il est très peu probable que la sauvegarde elle-même fonctionne et vous devrez essayer les autres méthodes de récupération mentionnées.
- Vous pouvez également essayer de récupérer votre base de données. C'est généralement la seule option lorsque ce problème survient après une mise à jour. Essayez la commande [sqlite3 `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Si votre sqlite n'a pas `.recover` ou si vous souhaitez une méthode plus conviviale pour l'interface graphique (par exemple, Windows), suivez [nos instructions sur ce wiki](/useful-tools#recovering-a-corrupt-db-ui).
- Une autre cause possible de l'erreur de base de données est que vous placez votre base de données sur un lecteur réseau (nfs ou smb ou autre chose non local). **SQLite est conçu pour des situations où les données et l'application coexistent sur la même machine.** Ainsi, votre dossier \*Arr AppData (/montage de configuration pour Docker) DOIT être sur un stockage local. [SQLite et les lecteurs réseau ne fonctionnent pas bien ensemble et provoqueront éventuellement une base de données corrompue](https://www.sqlite.org/draft/useovernet.html).
- Si vous utilisez mergerFS, vous devez supprimer `direct_io` car SQLite utilise mmap qui n'est pas pris en charge par `direct_io`, comme expliqué dans la documentation de mergerFS [ici](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## J'utilise Radarr sur un Mac et il a soudainement cessé de fonctionner. Que s'est-il passé ?

- Il s'agit très probablement d'un bogue de MacOS qui a provoqué la corruption de l'une des bases de données.
- Voir l'entrée ci-dessus sur la base de données corrompue.
- Ensuite, essayez de le lancer et voyez s'il fonctionne. S'il ne fonctionne pas, vous aurez besoin d'un soutien supplémentaire. Postez sur notre [subreddit /r/radarr](http://reddit.com/r/radarr) ou rejoignez [notre discord](https://radarr.video/discord) pour obtenir de l'aide.

## Pourquoi Radarr ne peut-il pas voir mes fichiers sur un serveur distant ?

- Pour tous les systèmes d'exploitation, assurez-vous que l'utilisateur/groupe sous lequel vous exécutez \*Arr ait un accès en lecture et en écriture au lecteur monté.
- Pour Linux, assurez-vous de :
  - Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé pour votre montage.
  - Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé pour votre montage.
- Pour Windows : En bref : l'utilisateur sous lequel \*Arr s'exécute (s'il s'agit d'un service) ou en dessous (s'il s'agit d'une application de la barre d'état système) ne peut pas accéder au chemin d'accès du fichier sur le serveur distant. Cela peut être dû à diverses raisons, mais la plus courante est que \*Arr s'exécute en tant que service, ce qui provoque les problèmes décrits ci-dessous.

### Radarr s'exécute par défaut sous le compte LocalService qui n'a pas accès aux partages de fichiers distants protégés

- Exécutez le service Radarr en tant qu'un autre utilisateur qui a accès à ce partage
- Ouvrez la fenêtre Outils d'administration \> Services sur votre serveur Windows.
- Arrêtez le service Radarr.
- Ouvrez la boîte de dialogue Propriétés \> Connexion.
- Changez le compte utilisateur du service en compte utilisateur cible.
- Exécutez Radarr.exe à l'aide du dossier de démarrage

### Vous utilisez un lecteur réseau mappé (pas un chemin UNC)

- Modifiez vos chemins en chemins UNC (`\\serveur\partage`)
- Exécutez Radarr.exe via le dossier de démarrage

## Comment passer du service Windows à une application de la barre d'état système ?

1. Arrêtez Radarr
1. Exécutez serviceuninstall.exe qui se trouve dans le répertoire Radarr
1. Exécutez `Radarr.exe` en tant qu'administrateur une fois pour lui donner les autorisations appropriées et ouvrir le pare-feu. Une fois terminé, vous pouvez le fermer et l'exécuter normalement.
1. (Facultatif) Ajoutez un raccourci vers .exe dans le dossier de démarrage pour le démarrage automatique au démarrage.

## Aide, je me suis verrouillé

{#help-i-have-forgotten-my-password}

Pour désactiver l'authentification (pour réinitialiser votre nom d'utilisateur ou votre mot de passe oublié), vous devrez modifier `config.xml` qui se trouvera dans le [répertoire Radarr Appdata](/radarr/appdata-directory)

1. Ouvrez config.xml dans un éditeur de texte
1. Trouvez la ligne de méthode d'authentification qui sera
`<AuthenticationMethod>Basic</AuthenticationMethod>` ou `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Changez la ligne `AuthenticationMethod` en `<AuthenticationMethod>None</AuthenticationMethod>`
1. Redémarrez Radarr
1. Radarr sera maintenant accessible sans mot de passe, vous devriez aller dans `Paramètres : Général` dans l'interface utilisateur et définir votre nom d'utilisateur et votre mot de passe

## Comment empêcher le navigateur de se lancer au démarrage ?

Selon votre système d'exploitation, il existe plusieurs façons possibles.

- Dans `Paramètres` => `Général` sur certains systèmes d'exploitation, il y a une case à cocher pour lancer le navigateur au démarrage.
- Lors de l'appel de Radarr, vous pouvez ajouter `-nobrowser` (*nix) ou `/nobrowser` (Windows) aux arguments.
- Arrêtez Radarr et modifiez le fichier config.xml, et changez `<LaunchBrowser>True</LaunchBrowser>` en `<LaunchBrowser>False</LaunchBrowser>`.

## Problèmes d'interface utilisateur étranges

- Si vous rencontrez des problèmes d'interface utilisateur étranges comme l'affichage de la page Bibliothèque sans rien afficher ou une vue ou un tri spécifique qui ne fonctionne pas, essayez de voir dans une fenêtre de navigation privée de Chrome ou une fenêtre privée de Firefox. Si cela fonctionne correctement, videz le cache et les cookies de votre navigateur pour votre adresse IP/domaine spécifique. Pour plus d'informations, consultez l'article du wiki [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage).

## L'interface Web ne se charge qu'en localhost sur Windows

- Si vous ne pouvez atteindre votre interface Web qu'à l'adresse <http://localhost:7878/> ou <http://127.0.0.1:7878/>, vous devez exécuter en tant qu'administrateur au moins une fois.

## Autorisations

- Radarr devra déplacer les fichiers du dossier où le téléchargeur les place vers l'emplacement final, cela signifie qu'il devra lire/écrire à la fois dans le dossier source et dans le dossier de destination, ainsi que dans les fichiers.
- Sur Linux, où les meilleures pratiques consistent à exécuter les services en tant qu'utilisateur distinct, cela signifiera probablement utiliser un groupe partagé et définir les autorisations des dossiers sur `775` et des fichiers sur `664` à la fois dans votre téléchargeur et . En notation umask, cela serait `002`.

## Le chargement de System & Logs dure indéfiniment

- C'est la liste de blocage easy-privacy. Ils bloquent essentiellement toutes les URL contenant `/api/log?`. Regardez la liste et dites-moi si vous pensez que bloquer toutes les URL de cette liste est une idée sensée, il y a des dizaines d'URL dans cette liste qui peuvent potentiellement casser des sites. Vous l'avez sélectionné dans votre bloqueur de publicités. La solution simple consiste à ajouter le domaine sur lequel Radarr s'exécute à la liste blanche. Mais je recommande quand même de vérifier la liste.

## Décompresser les torrents

- La plupart des clients torrent ne sont pas livrés avec la gestion automatique des archives compressées comme leurs homologues Usenet. Nous recommandons [unpackerr](https://github.com/unpackerr/unpackerr).

## uTorrent ne fonctionne plus

- Assurez-vous que l'interface Web est activée
- Assurez-vous que le port d'écoute alternatif (Avancé => Interface Web) n'est pas le même que le port d'écoute (Connexions)
- Nous vous suggérons de changer le port d'écoute alternatif de l'interface Web afin de ne pas perturber la redirection de port pour les connexions.

## J'ai reçu une fenêtre contextuelle indiquant que config.xml était corrompu, que faire maintenant ?

- Radarr n'a pas pu lire votre fichier de configuration au démarrage car il est devenu corrompu d'une manière ou d'une autre. Pour revenir en ligne, vous devrez supprimer `.xml` dans votre [répertoire appdata-directory](/radarr/appdata-directory), une fois supprimé, démarrez et il démarrera sur le port par défaut (7878), vous devriez maintenant reconfigurer les paramètres que vous avez configurés sur la page Paramètres généraux.

## Certificat invalide et autres problèmes HTTPS ou SSL



- Votre client de téléchargement ne fonctionne plus et vous obtenez une erreur du type `Localhost est un certificat non valide` ?
  - Radarr valide les certificats SSL. Si aucun certificat SSL n'est défini dans le client de téléchargement, ou si vous utilisez un certificat https auto-signé sans le certificat CA ajouté à votre magasin de certificats local, alors Radarr refusera de se connecter. Des certificats correctement signés et gratuits sont disponibles sur [let's encrypt](https://letsencrypt.org/).
  - Si votre client de téléchargement et votre machine sont sur la même machine, il n'y a aucune raison d'utiliser HTTPS, donc la solution la plus simple est de désactiver SSL pour la connexion. La plupart des gens conviendront que ce n'est pas nécessaire non plus sur un réseau local. Il est possible de désactiver la validation du certificat dans les paramètres avancés si vous souhaitez conserver une configuration SSL non sécurisée.

## VPN, Jackett et les \*ARRs

- Sauf si vous êtes dans un pays répressif comme la Chine, l'Australie ou l'Afrique du Sud, votre client torrent est généralement le seul élément qui doit être derrière un VPN. Étant donné que le point de terminaison VPN est partagé par de nombreux utilisateurs, vous pouvez rencontrer des limites de débit, une protection contre les attaques DDOS et des interdictions IP de divers services utilisés par chaque logiciel.
- En d'autres termes, mettre les \*Arrs (Lidarr, Prowlarr, Radarr, Readarr et Lidarr) derrière un VPN peut rendre les applications inutilisables dans certains cas en raison de l'inaccessibilité des services.

> **Pour être clair, ce n'est pas une question de savoir si les VPN causeront des problèmes avec les \*Arrs, mais quand : les fournisseurs d'images vous bloqueront et Cloudflare est devant la plupart des serveurs \*Arr (mises à jour, métadonnées, etc.) et est susceptible de vous bloquer également**
{.is-warning}

- **De nombreux trackers privés vous interdiront d'utiliser ou d'y accéder (c'est-à-dire en utilisant Jackett ou Prowlarr) via un VPN.**

### Utilisation d'un VPN

- Si un VPN est requis et que Docker est utilisé, il est recommandé d'utiliser les conteneurs Hotio ou Binhex's Download Client + VPN.
- Si un VPN est requis et que Docker n'est pas utilisé, votre client VPN ***doit*** prendre en charge le fractionnement du tunnel afin que seules les applications requises (client de téléchargement) soient derrière le VPN.
- De nombreux problèmes d'accès aux trackers peuvent être résolus en utilisant les serveurs DNS de Google ou de Cloudflare à la place des serveurs DNS de votre fournisseur d'accès Internet.
- Dans certains cas (par exemple, les fournisseurs d'accès Internet britanniques), vous devrez peut-être mettre votre client de téléchargement de torrents derrière un VPN et Jackett/Prowlarr comme suit :
  - mettez Jackett derrière le VPN et assurez-vous que le fractionnement du tunnel permet l'accès local
  - pour Prowlarr, configurez votre client VPN pour fournir un proxy et ajoutez le proxy dans Paramètres => Indexeurs. Donnez au proxy une étiquette et attribuez la même étiquette aux indexeurs qui doivent l'utiliser.
    - Si cela est absolument nécessaire et si votre VPN ne propose pas de moyen de créer un proxy, vous pouvez mettre Prowlarr derrière le VPN et vous assurer que le fractionnement du tunnel permet l'accès local.

# Problèmes courants de recherche et de téléchargement de Radarr

## Pourquoi ne puis-je pas ajouter un nouveau film à Radarr ?

{#pourquoi-ne-puis-je-pas-ajouter-un-nouveau-film-à-radarr}

- Radarr utilise [The Movie Database (TMDb)](http://themoviedb.org) pour les informations sur les films et les images telles que les fanarts, les bannières et les arrière-plans. En général, il existe quelques raisons pour lesquelles vous ne pouvez pas ajouter un film :
  - TMDb n'aime pas que des caractères spéciaux soient utilisés lors de la recherche de films via l'API (que Radarr utilise), donc essayez de rechercher un nom traduit et/ou sans caractères spéciaux.
  - Vous pouvez également ajouter par ID TMDb ou, si TMDb le permet, l'ID IMDb.
  - Le film n'a pas encore été ajouté à TMDb, suivez leur [guide](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006) pour l'ajouter.

## Jackett affiche plus de résultats que lors d'une recherche manuelle

- Cela est généralement dû à une recherche différente dans Jackett. Consultez notre [article de dépannage](/radarr/troubleshooting) pour plus d'informations.

## Comment Radarr détermine-t-il l'année d'un film ?

- Radarr récupère les métadonnées de [TMDb](https://www.themoviedb.org/)
- Radarr utilise l'année de la plus ancienne date de **sortie en salle** et la plus ancienne date de **première** pour la correspondance.
  - Notez que si une sortie en salle n'existe pas, la logique se rabattra sur la date de sortie la plus ancienne en version physique ou numérique.
- Si un film n'a pas de date de sortie numérique, physique, en salle ou en première, TMDb devrait être mis à jour.
- [Le guide de contribution de TMDb](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013) indique ce qui suit à propos de leurs types de sortie.
  - **Première** - Une première projection peut prendre la forme d'une projection lors d'un festival (par exemple, TIFF) ou d'un événement de première avec l'équipe du film dans une grande ville (par exemple, LA, Londres, Toronto).
  - **Sortie en salle** - Peut être utilisé pour la sortie originale et toutes les sorties officielles ultérieures. Utilisé pour les sorties larges ou saturées. Aux États-Unis, 600 à 1 999 écrans sont considérés comme une sortie large et 2 000+ comme une sortie saturée.
  - **Sortie en salle (limitée)** - Une sortie en salle limitée est une stratégie de distribution de films consistant à sortir un nouveau film dans quelques salles d'un pays, généralement dans les grands marchés métropolitains. Aux États-Unis, le nombre de salles est inférieur à 600.
  - **Physique** - Comprend toutes les sorties VHS, DVD et Blu-ray.
  - **Numérique** - Toutes les sorties pertinentes peuvent être ajoutées, y compris les plateformes de streaming, la location ou l'achat VOD. Les projections numériques, y compris les festivals de cinéma en ligne et les sorties de cinéma virtuelles, sont également considérées comme des sorties numériques.

## Comment Radarr gère-t-il les films étrangers ou les titres étrangers ?

> [Le guide du langage de format personnalisé de TRaSH](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) peut être utile pour vous aider à obtenir des films dans la ou les langues que vous souhaitez.{.is-info}

> À partir du 12 février 2023, le cache de métadonnées de Radarr commencera à considérer la langue originale d'un film comme la langue parlée de TMDb si et seulement si un seul langage parlé existe pour le film sur TMDb ; sinon, la langue originale de TMDb du film sera utilisée.
{.is-warning}

## Recherches par ID

- **Indexeurs prenant en charge les recherches basées sur l'ID** - Les recherches sur les indexeurs et les trackers qui prennent en charge les recherches basées sur l'ID (TMDbId, IMDbId, etc.) - comme de nombreux indexeurs Usenet et de nombreux trackers privés - les requêtes textuelles ne sont pas utilisées si des résultats sont renvoyés pour une recherche basée sur l'ID. Si des résultats sont renvoyés, la recherche ne se rabattra pas sur une recherche par nom/texte. Si vous ne trouvez pas de résultats dans votre indexeur, cela est dû au fait que les versions associées à l'ID du film sont incorrectes.
  - La langue de la version peut également être déduite de la langue de la version de l'indexeur ou du tracker dans le résultat, si elle est fournie, plutôt que d'être analysée à partir du nom.

## Recherches par texte

- **Indexeurs ne prenant pas en charge les recherches basées sur l'ID ou les recherches basées sur l'ID sans résultats** - La recherche utilisera le titre original du film, le titre anglais et le titre traduit dans les langues que vous avez préférées dans le profil de qualité du film et tous les formats personnalisés avec des scores dans le profil de qualité supérieurs à zéro.
- L'analyse (c'est-à-dire l'importation) recherche une correspondance dans toutes les traductions et les titres alternatifs.
  - La langue de la version peut également être déduite de la langue de la version de l'indexeur ou du tracker dans le résultat, si elle est fournie, plutôt que d'être analysée à partir du nom.

## Obtenir des films étrangers

- Pour obtenir un film dans une langue étrangère, définissez la langue du profil de qualité de votre film sur Original (langue originale du film\*), une langue spécifique pour ce profil ou `Any` et créez des formats personnalisés avec des conditions de langue et un score supérieur à 0 pour déterminer quelle langue récupérer.
- Notez que cela n'inclut pas les langues des indexeurs configurées dans les paramètres de l'indexeur en tant que `multi`.
  - Notez qu'à partir de [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c), `multi` n'est plus supposé inclure l'anglais
  - Les utilisateurs peuvent ajuster leurs paramètres par indexeur pour définir quelles langues `multi` indique

## Comment Radarr gère-t-il "multi" dans les noms ?

- Avec Radarr v4.1+, Radarr suppose que
`multi` est uniquement la langue du film et **PAS** l'anglais comme dans les versions précédentes.
  - Les utilisateurs peuvent ajuster leurs paramètres par indexeur pour définir quelles langues `multi` indique
- Notez que les définitions de `multi` n'aident que pour l'analyse des versions et non pour les titres étrangers ou les recherches de films.

## Aide, le film a été ajouté, mais pas recherché

- Radarr ne recherche pas *activement* les films manquants automatiquement. Au lieu de cela, une requête périodique de nouveaux messages est effectuée sur tous les indexeurs configurés pour le flux RSS. Lorsqu'un film souhaité ou un film dont les critères de coupure ne sont pas satisfaits apparaît dans cette liste, il est téléchargé. Cela signifie que tant qu'un film n'est pas publié (ou republié), il ne sera pas téléchargé.
- Si vous ajoutez un film que vous voulez maintenant, la meilleure option est de cocher la case "Démarrer la recherche pour le film manquant", à gauche du bouton *Ajouter un film* (**1**). Vous pouvez également vous rendre sur la page d'un film que vous avez ajouté et cliquer sur l'icône de la loupe "Rechercher" (**2**) ou utiliser la vue "Recherché" pour rechercher des films manquants ou des films dont les critères de coupure ne sont pas satisfaits.

  - Ajouter et rechercher un film lors de l'ajout d'un film
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - Rechercher un film existant
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## L'endpoint /all de Jackett

{#jackett-all-endpoint}

- L'endpoint `/all` de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes potentiels, il est donc nécessaire d'ajouter chaque tracker individuellement. Vous pouvez également envisager d'utiliser l'alternative Jackett & NZBHydra2 [Prowlarr](/prowlarr)

- **Mise à jour du 1er janvier 2022 : L'endpoint `/all` de Jackett n'est plus pris en charge (par exemple, des avertissements apparaîtront) à partir de la version 4.0.0.5730 car il ne cause que des problèmes.**

- L'endpoint /all de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc maintenant nécessaire d'ajouter chaque tracker individuellement.
- [Même les développeurs de Jackett disent qu'il faut l'éviter et ne pas l'utiliser.](https://github.com/Jackett/Jackett#aggregate-indexers)
- L'utilisation de l'endpoint /all n'a aucun avantage, seulement des inconvénients :
  - vous perdez le contrôle sur les paramètres spécifiques de l'indexeur (catégories, modes de recherche, etc.)
  - mélanger les modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
  - les catégories spécifiques de l'indexeur (\>= 100000) ne peuvent pas être utilisées.
  - les indexeurs lents ralentiront le résultat global
  - le nombre total de résultats est limité à 1000
  - si l'un des trackers dans /all renvoie une erreur, \*Arr le désactivera et vous n'obtiendrez plus aucun résultat.

### Solutions pour Jackett /All

- Ajoutez chaque tracker dans Jackett manuellement en tant qu'indexeur dans \*Arr
- Consultez [Prowlarr](/prowlarr) qui peut synchroniser les indexeurs avec \*Arr et qui est développé par l'équipe de Lidarr/Radarr/Readarr.
- Consultez [NZBHydra2](https://github.com/theotherp/nzbhydra2) qui peut synchroniser les indexeurs avec \*Arr. Mais n'utilisez pas leur endpoint d'agrégation unique et utilisez `multi` si la synchronisation est utilisée.

## Pourquoi y a-t-il deux fichiers ? | Pourquoi y a-t-il un fichier restant dans les téléchargements ?

C'est normal. Avec une configuration prenant en charge les [liens physiques](https://trash-guides.info/hardlinks), aucun espace supplémentaire ne sera utilisé. Voici comment fonctionne le processus de torrent.

1. Radarr envoie une demande de téléchargement à votre client et l'associe à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement. Exemples : films, tv, séries, musique, etc.
1. Radarr surveille les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
1. Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de partager le fichier (le ratio ou le temps peut être ajusté dans le client de téléchargement ou depuis Radarr sous le client de téléchargement spécifique). Lorsque les fichiers sont importés dans votre dossier multimédia, ils sont liés physiquement s'ils sont pris en charge par votre configuration, sinon ils sont copiés.
1. Si l'option "Gestion des téléchargements terminés - Supprimer les téléchargements terminés" est activée dans les paramètres de Radarr, Radarr supprimera le fichier et le torrent d'origine de votre client de téléchargement, mais seulement si le client de téléchargement signale que le partage est terminé et que le torrent est arrêté (c'est-à-dire en pause). Consultez les [guides de TRaSH sur les clients de téléchargement](https://trash-guides.info/Downloaders/) pour savoir comment configurer votre client de téléchargement de manière optimale.

> Les liens physiques sont activés par défaut. [Un lien physique ne nécessitera pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien physique échoue ou si votre configuration ne prend pas en charge les liens physiques, une copie du fichier sera effectuée.
{.is-info}

## Pourquoi Radarr ne fonctionne-t-il pas derrière un proxy inverse ?

- À partir de la version 3, Radarr est passé à .NET et à un nouveau serveur web. Pour que SignalR fonctionne, que les boutons de l'interface utilisateur fonctionnent, que les modifications de la base de données soient prises en compte et autres éléments, il est nécessaire d'ajouter les lignes suivantes au bloc de localisation de Radarr :

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- Assurez-vous de **ne pas** inclure `proxy_set_header Connection "Upgrade";` comme suggéré par la documentation de nginx. **CELA NE FONCTIONNERA PAS**
- [Voir ce problème ASP.NET Core](https://github.com/aspnet/AspNetCore/issues/17081)
- Si vous utilisez un CDN comme Cloudflare, assurez-vous que les websockets sont activés pour permettre les connexions websocket.
- Si vous rencontrez des redirections inattendues, assurez-vous que votre en-tête d'hôte est transmis.