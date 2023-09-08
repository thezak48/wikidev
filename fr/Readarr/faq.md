- No, you cannot disable the refresh books task in Readarr. The refresh books task is responsible for updating the metadata and status of your books in Readarr. It ensures that the information about your books is up to date and accurate. Disabling this task would prevent Readarr from functioning properly.

- Non, et vous ne devriez pas non plus par le biais de manipulations SQL. La tâche de rafraîchissement des livres interroge le proxy Servarr en amont et vérifie si les métadonnées de chaque livre (identifiants, casting, résumé, note, traductions, titres alternatifs, etc.) ont été mises à jour par rapport à ce qui est actuellement dans Readarr. Si nécessaire, il mettra ensuite à jour les livres concernés.
- Une plainte courante est que la tâche de rafraîchissement entraîne une utilisation intensive de l'E/S. Un paramètre qui peut poser problème est "Rescan Author Folder after Refresh". Si votre utilisation de l'E/S sur le disque augmente pendant un rafraîchissement, vous voudrez peut-être changer le paramètre de rescan en `Manuel`. Ne le changez pas en `Jamais` à moins que toutes les modifications de votre bibliothèque (nouveaux livres, mises à niveau, suppressions, etc.) ne soient effectuées via Readarr. Si vous supprimez manuellement des fichiers de livres ou utilisez un programme tiers, ne définissez pas cette option sur `Jamais`.

## Puis-je avoir à la fois une version ebook et une version livre audio du même livre ?

- Non. Avec une seule instance de Readarr, vous pouvez avoir soit l'un, soit l'autre, mais pas les deux. Si vous voulez les deux, vous devrez exécuter deux instances distinctes de Readarr (tout comme certaines personnes exécutent 2 instances de Sonarr ou Radarr pour les versions 1080p et 4K de leurs médias).

## Dois-je utiliser Calibre ?

- Non. En général, Calibre offre quelques améliorations supplémentaires, telles que la possibilité de convertir automatiquement les ebooks dans un autre format spécifique aux capacités de votre liseuse, ainsi que de se connecter à cette liseuse. Mais si vous n'utilisiez pas Calibre avant d'installer Readarr, il est probablement peu utile de l'installer, d'autant plus que c'est un programme très volumineux.

## Pourquoi Readarr ne peut-il pas voir mes fichiers sur un serveur distant ?

- Pour tous les systèmes d'exploitation, assurez-vous que l'utilisateur/le groupe sous lequel vous exécutez \*Arr ait les droits de lecture et d'écriture sur le lecteur monté.
- Pour Linux, assurez-vous de :
  - Si vous utilisez un montage NFS, activez nolock pour votre montage.
  - Si vous utilisez un montage SMB, activez nobrl pour votre montage.
- Pour Windows : En bref, l'utilisateur sous lequel \*Arr s'exécute (s'il s'agit d'un service) ou en dessous (s'il s'agit d'une application de la barre d'état système) ne peut pas accéder au chemin d'accès du fichier sur le serveur distant. Cela peut être dû à diverses raisons, mais la plus courante est que \*Arr s'exécute en tant que service, ce qui cause les problèmes décrits ci-dessous.

### Readarr s'exécute par défaut sous le compte LocalService qui n'a pas accès aux partages de fichiers distants protégés

- Exécutez le service Readarr sous un autre utilisateur qui a accès à ce partage.
- Ouvrez la fenêtre Outils d'administration \> Services sur votre serveur Windows.
- Arrêtez le service Readarr.
- Ouvrez la boîte de dialogue Propriétés \> Connexion.
- Changez le compte utilisateur du service en compte utilisateur cible.
- Exécutez Readarr.exe à partir du dossier de démarrage

### Vous utilisez un lecteur réseau mappé (pas un chemin UNC)

- Modifiez vos chemins d'accès en chemins UNC (`\\serveur\partage`)
- Exécutez Readarr.exe via le dossier de démarrage

## Aide, je me suis enfermé dehors

{#help-i-have-forgotten-my-password}

Pour désactiver l'authentification (pour réinitialiser votre nom d'utilisateur ou votre mot de passe oublié), vous devrez modifier `config.xml` qui se trouve à l'intérieur du [Répertoire des données de Readarr](/readarr/appdata-directory)

1. Ouvrez config.xml dans un éditeur de texte
1. Trouvez la ligne de méthode d'authentification qui sera
`<AuthenticationMethod>Basic</AuthenticationMethod>` ou `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Changez la ligne `AuthenticationMethod` en `<AuthenticationMethod>None</AuthenticationMethod>`
1. Redémarrez Readarr
1. Readarr sera maintenant accessible sans mot de passe, vous devriez aller dans `Paramètres : Général` dans l'interface utilisateur et définir votre nom d'utilisateur et votre mot de passe

## Comment empêcher le navigateur de se lancer au démarrage ?

Selon votre système d'exploitation, il existe plusieurs façons possibles.

- Dans `Paramètres` => `Général` sur certains systèmes d'exploitation, il y a une case à cocher pour lancer le navigateur au démarrage.
- Lorsque vous invoquez Readarr, vous pouvez ajouter `-nobrowser` (*nix) ou `/nobrowser` (Windows) aux arguments.
- Arrêtez Readarr et modifiez le fichier config.xml, et changez `<LaunchBrowser>True</LaunchBrowser>` en `<LaunchBrowser>False</LaunchBrowser>`.

## Problèmes d'interface utilisateur étranges

- Si vous rencontrez des problèmes d'interface utilisateur étranges, comme la page de la bibliothèque qui ne répertorie rien ou une certaine vue ou un certain tri qui ne fonctionne pas, essayez de voir dans une fenêtre de navigation privée Chrome ou une fenêtre privée Firefox. Si cela fonctionne correctement là-bas, effacez le cache et les cookies de votre navigateur pour votre adresse IP/domaine spécifique. Pour plus d'informations, consultez l'article du wiki [Effacer le cache, les cookies et le stockage local](/useful-tools#clearing-cookies-and-local-storage).

## VPN, Jackett et les \*ARRs

- Sauf si vous êtes dans un pays répressif comme la Chine, l'Australie ou l'Afrique du Sud, votre client torrent est généralement le seul élément qui doit être derrière un VPN. Étant donné que le point de terminaison VPN est partagé par de nombreux utilisateurs, vous pouvez rencontrer des limites de débit, une protection contre les attaques DDOS et des interdictions d'IP de la part des différents services utilisés par chaque logiciel.
- En d'autres termes, mettre les \*Arrs (Lidarr, Prowlarr, Radarr, Readarr et Lidarr) derrière un VPN peut rendre les applications inutilisables dans certains cas en raison de l'inaccessibilité des services.

> **Pour être clair, il ne s'agit pas de savoir si les VPN vont causer des problèmes avec les \*Arrs, mais quand : les fournisseurs d'images vous bloqueront et Cloudflare est devant la plupart des serveurs \*Arr (mises à jour, métadonnées, etc.) et est susceptible de vous bloquer également**
{.is-warning}

- **De nombreux trackers privés vous banniront si vous les utilisez ou y accédez (c'est-à-dire en utilisant Jackett ou Prowlarr) via un VPN.**

### Utilisation d'un VPN

- Si un VPN est requis et que Docker est utilisé, il est recommandé d'utiliser les conteneurs Download Client + VPN de Hotio ou Binhex.
- Si un VPN est requis et que Docker n'est pas utilisé, votre client VPN ***doit*** prendre en charge le fractionnement du tunnel afin que seules les applications requises (Download Client) soient derrière le VPN.
- De nombreux problèmes d'accès aux trackers peuvent être résolus en utilisant les serveurs DNS de Google ou de Cloudflare à la place des serveurs DNS de votre fournisseur d'accès Internet.
- Dans certains cas (par exemple, les fournisseurs d'accès Internet au Royaume-Uni), vous devrez peut-être mettre votre client de téléchargement torrent derrière un VPN et Jackett/Prowlarr comme suit :
  - mettez Jackett derrière le VPN et assurez-vous que le fractionnement du tunnel permet l'accès local
  - pour Prowlarr, configurez votre client VPN pour fournir un proxy et ajoutez le proxy dans Paramètres => Indexeurs. Donnez au proxy une étiquette et attribuez la même étiquette aux indexeurs qui doivent l'utiliser.
    - Si cela est absolument nécessaire et si votre VPN ne propose pas de moyen de créer un proxy, vous pouvez mettre Prowlarr derrière le VPN et vous assurer que le fractionnement du tunnel permet l'accès local.

## L'endpoint /all de Jackett

{#jackett-all-endpoint}

- L'endpoint `/all` de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc nécessaire d'ajouter chaque tracker individuellement. Vous pouvez également envisager de consulter l'alternative à Jackett & NZBHydra2, [Prowlarr](/prowlarr)
- **Mise à jour du 20 janvier 2022 : L'endpoint `/all` de Jackett n'est plus pris en charge (des avertissements apparaîtront) à partir de la version 0.1.0.1188 car il ne cause que des problèmes.**
- L'endpoint /all de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc désormais nécessaire d'ajouter chaque tracker individuellement.
- [Même les développeurs de Jackett disent qu'il faut l'éviter et ne pas l'utiliser.](https://github.com/Jackett/Jackett#aggregate-indexers)
- L'utilisation de l'endpoint /all n'a aucun avantage, seulement des inconvénients :
  - vous perdez le contrôle sur les paramètres spécifiques de l'indexeur (catégories, modes de recherche, etc.)
  - mélanger les modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
  - les catégories spécifiques à l'indexeur (\>= 100000) ne peuvent pas être utilisées.
  - les indexeurs lents ralentiront le résultat global
  - le nombre total de résultats est limité à 1000
  - si l'un des trackers dans /all renvoie une erreur, \*Arr le désactivera et vous n'obtiendrez plus aucun résultat.

### Solutions pour l'endpoint /all de Jackett

- Ajoutez chaque tracker manuellement dans Jackett en tant qu'indexeur dans \*Arr
- Consultez [Prowlarr](/prowlarr) qui peut synchroniser les indexeurs avec \*Arr et qui est développé par l'équipe de développement de Lidarr/Radarr/Readarr.
- Consultez [NZBHydra2](https://github.com/theotherp/nzbhydra2) qui peut synchroniser les indexeurs avec \*Arr. Mais n'utilisez pas leur endpoint unique et utilisez `multi` si la synchronisation est utilisée.

## Pourquoi y a-t-il deux fichiers ? | Pourquoi y a-t-il un fichier restant dans les téléchargements ?

C'est normal. Avec une configuration prenant en charge les [liens physiques](https://trash-guides.info/hardlinks), aucun espace supplémentaire ne sera utilisé. Voici comment fonctionne le processus de torrent.

1. Readarr envoie une demande de téléchargement à votre client et l'associe à un label ou à une catégorie que vous avez configuré dans les paramètres du client de téléchargement. Exemples : films, séries TV, musique, etc.
1. Readarr surveille les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
1. Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de partager le fichier (le ratio ou le temps peut être ajusté dans le client de téléchargement ou depuis l'intérieur de celui-ci, sous le téléchargement spécifique). Lorsque les fichiers sont importés dans votre dossier multimédia, ils seront liés physiquement s'ils sont pris en charge par votre configuration, sinon ils seront copiés si les liens physiques ne sont pas pris en charge.
1. Si l'option "Gestion des téléchargements terminés - Supprimer les téléchargements terminés" est activée dans les paramètres de Readarr, Readarr supprimera le fichier et le torrent d'origine de votre client de téléchargement, mais seulement si le client de téléchargement signale que le partage est terminé et que le torrent est arrêté.

> Les liens physiques sont activés par défaut. [Un lien physique ne nécessitera pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien physique échoue ou si votre configuration ne prend pas en charge les liens physiques, une copie du fichier sera effectuée en dernier recours.
{.is-info}

## Calibre indique "Calibre a rejeté le livre en double" mais ce n'est pas le cas

Si vous utilisez l'intégration de Calibre, il arrive parfois que Calibre rejette un livre en disant qu'il est en double. Ce n'est probablement pas vraiment un doublon. Si cela se produit, il n'y a pas grand-chose que Readarr puisse faire, et vous devrez désactiver le suivi de ce livre pour empêcher Readarr de continuer à essayer de le récupérer et de le pousser vers Calibre. C'est l'un des inconvénients amusants de l'intégration de Calibre.