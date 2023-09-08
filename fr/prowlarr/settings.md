---
title: Paramètres de Prowlarr
description: 
published: true
date: 2023-03-30T14:07:39.851Z
tags: 
editor: markdown
dateCreated: 2021-06-06T15:04:48.057Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Options de menu](#options-de-menu)
- [Proxies d'indexeur](#proxies-dindexeur)
  - [Paramètres de proxy](#paramètres-de-proxy)
  - [Paramètres de proxy FlareSolverr](#paramètres-de-proxy-flaresolverr)
  - [Paramètres de proxy HTTP](#paramètres-de-proxy-http)
  - [Paramètres de proxy Socks4](#paramètres-de-proxy-socks4)
  - [Paramètres de proxy Socks5](#paramètres-de-proxy-socks5)
- [Applications](#applications)
  - [Paramètres de l'application](#paramètres-de-lapplication)
  - [Tester l'application](#tester-lapplication)
- [Clients de téléchargement (recherches Prowlarr)](#clients-de-téléchargement-recherches-prowlarr)
  - [Paramètres du client Usenet](#paramètres-du-client-usenet)
  - [Paramètres du client Torrent](#paramètres-du-client-torrent)
  - [Tester le client de téléchargement](#tester-le-client-de-téléchargement)
- [Notifications](#notifications)
  - [Connexions](#connexions)
  - [Déclencheurs de notification](#déclencheurs-de-notification)
- [Tags](#tags)
- [Général](#général)
  - [Hôte](#hôte)
  - [Sécurité](#sécurité)
  - [Proxy](#proxy)
  - [Journalisation](#journalisation)
  - [Analytique](#analytique)
  - [Mises à jour](#mises-à-jour)
  - [Sauvegardes](#sauvegardes)
- [Interface utilisateur](#interface-utilisateur)
  - [Dates](#dates)
  - [Style](#style)
  - [Langue](#langue)
  
Cette page présente tous les paramètres disponibles dans Prowlarr et leur fonctionnement. Elle ne vise pas à être un guide complet sur la configuration de Prowlarr. Si vous souhaitez cela, veuillez consulter la page [Guide de démarrage rapide](/prowlarr/quick-start-guide) à la place.

# Options de menu

Pour accéder à la page des paramètres, veuillez choisir Paramètres dans le menu de gauche. Les options de sous-menu suivantes seront disponibles :

![settings_1_menu.png](/assets/prowlarr/settings_1_menu.png)

Notez également que pour chaque page de paramètres individuelle, il y a des options en haut du menu :

![settings_2_topmenu.png](/assets/prowlarr/settings_2_topmenu.png)

- Masquer/Afficher les options avancées est important pour tous les éléments marqués ci-dessous comme `(Option avancée)`, sinon ils n'apparaîtront pas. Ces éléments de menu sont affichés en orange sur les captures d'écran.

- Vous devez enregistrer vos modifications avant de quitter l'écran. Pour cela, cliquez sur l'icône du disque. Si vous n'avez apporté aucune modification, il affichera "Pas de modifications" et sera grisé, comme indiqué ci-dessus.

# Proxies d'indexeur

> Des informations sur les types de proxy pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/prowlarr/supported#indexer-proxies) pour cette section
{.is-info}

C'est ici que vous pouvez ajouter des proxies ou des configurations Flaresolverr pour les indexeurs qui en ont besoin.

Accédez à `Paramètres` => `Proxies d'indexeur`, puis cliquez sur le <kb>+</kb> pour ajouter un proxy.

![proxies.png](/assets/prowlarr/proxies.png)

## Paramètres de proxy
  
- Nom - Nom du proxy dans Prowlarr
- Tags - Les tags pour ce proxy. Les proxies s'appliquent à tous les indexeurs correspondants (même tag). Si cette zone est vide, ce proxy s'applique à tous les indexeurs.

## Paramètres de proxy FlareSolverr

- Hôte - le chemin d'accès complet de l'hôte (incluant http et le port) vers votre instance FlareSolverr
- (Paramètre avancé) Délai d'attente de la requête (en secondes) - la valeur de la requête FlareSolverr `maxTimeout` que Prowlarr doit utiliser pour les requêtes FlareSolverr. Doit être compris entre `1` seconde et `180` secondes (par défaut : `60` secondes)

> \* Un proxy FlareSolverr ne sera utilisé que pour les requêtes si et seulement si Cloudflare est détecté par Prowlarr
> \* Un proxy FlareSolverr ne sera utilisé que pour les requêtes si et seulement si le proxy et l'indexeur ont des tags correspondants
> \* **Un proxy Flaresolverr configuré sans aucun tag ou sans indexeurs ayant des tags correspondants sera désactivé.**
{.is-info}

## Paramètres de proxy HTTP

- Hôte - l'adresse de l'hôte de votre proxy
- Port - le port de votre proxy
- Nom d'utilisateur - le nom d'utilisateur de votre proxy
- Mot de passe - le mot de passe de votre proxy

## Paramètres de proxy Socks4

- Hôte - l'adresse de l'hôte de votre proxy
- Port - le port de votre proxy
- Nom d'utilisateur - le nom d'utilisateur de votre proxy
- Mot de passe - le mot de passe de votre proxy

## Paramètres de proxy Socks5

- Hôte - l'adresse de l'hôte de votre proxy
- Port - le port de votre proxy
- Nom d'utilisateur - le nom d'utilisateur de votre proxy
- Mot de passe - le mot de passe de votre proxy

# Applications

> Des informations sur les applications prises en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/prowlarr/supported#applications) pour cette section
{.is-info}

C'est ici que vous ajouterez les applications qui utilisent Prowlarr (Radarr, Sonarr, Lidarr, Readarr, etc.) et comment elles restent synchronisées avec Prowlarr.

- Cliquez sur `Paramètres` => `Applications`, puis cliquez sur le <kb>+</kb> pour ajouter une application.
- Synchroniser les indexeurs de l'application - Déclenche une synchronisation de tous les indexeurs vers toutes les applications
- Tester toutes les applications - Déclenche un test de toutes les applications
  
![addapps.png](/assets/prowlarr/addapps.png)

Tous les programmes que vous pouvez ajouter sont répertoriés. Vous ne devez ajouter que les programmes que vous avez actuellement installés, et si vous en avez plusieurs instances, vous devez les ajouter séparément.

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Remarque : Les indexeurs sont synchronisés en fonction des catégories/capacités qu'ils prétendent prendre en charge. Si un indexeur ne prend en charge que les catégories `tv`, il ne sera pas synchronisé avec Lidarr, Radarr et Readarr. Il sera uniquement synchronisé avec Sonarr. Les catégories "Pris en charge" peuvent être sélectionnées comme paramètre avancé pour chaque application. **Notez également que les \*Arrs n'acceptent que les indexeurs dont les requêtes de test renvoient des résultats contenant au moins l'une des catégories configurées.**
{.is-info}

## Paramètres de l'application

- Nom - Entrez un nom pour cette application.
- Niveau de synchronisation - Sélectionnez le niveau de synchronisation à utiliser
  - `Ajouter et supprimer uniquement` - Lorsque des indexeurs sont ajoutés ou supprimés de Prowlarr, cela mettra à jour cette application distante. Si l'indexeur est hors service au moment de la synchronisation, il sera désactivé sur l'application distante.
  - `Synchronisation complète` - La synchronisation complète maintiendra les indexeurs de cette application entièrement synchronisés. Les modifications apportées aux indexeurs dans Prowlarr sont ensuite synchronisées avec cette application. Toute modification apportée aux paramètres sur la FAQ pour ces indexeurs à distance dans cette application sera écrasée par Prowlarr lors de la prochaine synchronisation. Une liste des facteurs utilisés pour comparer et déterminer si une synchronisation doit avoir lieu peut être trouvée dans la [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Désactivé` - empêchera la synchronisation des indexeurs avec le programme.

> `Synchronisation complète` signifie que Prowlarr remplacera la plupart des paramètres, y compris les catégories sélectionnées par l'utilisateur configurables dans Prowlarr. Cependant, les paramètres gérés par Prowlarr ne seront pas modifiés. Cependant, [presque tous les autres facteurs de modifications](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) déclencheront une synchronisation et écraseront les paramètres correspondants dans \*Arr
{.is-warning}

- Tags - Si vous avez ajouté un tag à votre indexeur lors de la configuration, seuls les indexeurs avec ce tag seront utilisés pour cette entrée de programme.
- Serveur Prowlarr - Entrez l'URL du serveur Prowlarr (y compris http, le port et l'URL de base si nécessaire) comme l'application y accéderait ici.

> Notez que si vous utilisez un proxy inverse, vous devez ajouter l'URL de base à cela ! Si vous ne le faites pas, lorsque les indexeurs se synchronisent, ils seront cassés, et si vous avez sélectionné Ajouter et supprimer uniquement, cela ne sera pas corrigé lorsque vous l'éditez !{.is-info}

- Serveur de l'application - Entrez l'URL du serveur de l'application (y compris http, le port et l'URL de base si nécessaire) ici. Encore une fois, entrez l'URL de base complète si elle est utilisée.
- Clé API - Entrez la clé API de votre programme ici. Pour les \*Arrs, vous pouvez la trouver dans Paramètres => Général. Vous pouvez l'obtenir à partir de votre programme dans l'onglet `Paramètres` => `Général`, puis la copier/coller ici.
- (Paramètre avancé) Synchroniser les catégories - Sélectionnez les catégories à synchroniser avec cette application. Les indexeurs prenant en charge ces catégories seront synchronisés.
  - Les catégories personnalisées de l'indexeur sont mappées dans les catégories Torznab/Newznab standardisées, de sorte que la recherche des catégories standardisées inclut toutes les catégories personnalisées sous-jacentes. Les catégories personnalisées de l'indexeur sont répertoriées pour un réglage fin si vous ne les voulez pas toutes en même temps.
  
## Tester l'application

Testez votre entrée. Si une coche verte apparaît, vous pouvez enregistrer votre entrée et répéter si nécessaire pour chaque programme que vous souhaitez synchroniser avec Prowlarr. S'il échoue, vous devrez vérifier votre journal pour l'erreur (URL, clé API, etc.).

## Profils de synchronisation

Configurez les profils de synchronisation à utiliser pour une ou plusieurs applications

> Vous pouvez avoir des paramètres différents par application en créant plusieurs instances de l'indexeur
{.is-info}

- Nom - Nom unique du profil de synchronisation
- Activer RSS - Pour les indexeurs avec ce profil, activer les recherches/interrogations RSS pour l'application \*Arr
- Activer la recherche interactive - Pour les indexeurs avec ce profil, activer les recherches interactives (manuelles) pour l'application \*Arr
- Activer la recherche automatique - Pour les indexeurs avec ce profil, activer les recherches automatiques pour l'application \*Arr
- Seeders minimum - Pour les indexeurs avec ce profil, le nombre minimum de seeders requis pour que \*Arr récupère un torrent

# Clients de téléchargement (recherches Prowlarr)

{#download-clients}

> Des informations sur les clients de téléchargement pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/prowlarr/supported#download-clients) pour cette section
{.is-info}

Si vous avez l'intention d'effectuer des recherches directement dans Prowlarr, vous devez ajouter des clients de téléchargement. Sinon, vous n'avez pas besoin de les ajouter ici. Pour les recherches à partir de vos applications, les clients de téléchargement configurés là-bas sont utilisés à la place.

> Prowlarr ne synchronise pas les clients de téléchargement avec les applications.
{.is-info}

Cliquez sur `Paramètres` => `Clients de téléchargement`, puis cliquez sur le <kb>+</kb> pour ajouter un nouveau client de téléchargement. Votre client de téléchargement doit déjà être configuré en suivant ce guide.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

Sélectionnez le client de téléchargement que vous souhaitez ajouter, et une boîte de dialogue apparaîtra pour saisir les détails de connexion. Ces détails sont similaires pour la plupart des clients. Certains vous demanderont un nom d'utilisateur ou un mot de passe, d'autres vous demanderont si vous souhaitez ajouter de nouveaux téléchargements en pause/en cours, etc.
  
> La priorité du client ne compte que lorsque 2 clients du même type (usenet ou torrent) sont ajoutés. 1 est la priorité la plus élevée, et si plusieurs clients du même type existent et ont la même priorité, Prowlarr les alternera.
{.is-info}

## Paramètres du client Usenet

- Nom - Le nom du client de téléchargement dans Prowlarr
- Activer - Activer ce client de téléchargement
- Hôte - L'URL de votre client de téléchargement
- Port - Le port de votre client de téléchargement
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez être conscient de cette erreur courante.
- URL de base - Ajoutez un préfixe à l'URL ; cela est généralement nécessaire pour les proxies inverses.
- Clé API - la clé API pour s'authentifier auprès de votre client
- Nom d'utilisateur - le nom d'utilisateur pour s'authentifier auprès de votre client (généralement pas nécessaire)
- Mot de passe - le mot de passe pour s'authentifier auprès de votre client (généralement pas nécessaire)
- Catégorie - la catégorie dans votre client de téléchargement que Prowlarr utilisera
- Priorité - priorité du client de téléchargement pour les éléments ajoutés
- Priorité du client - Priorité du client de téléchargement dans Prowlarr. Le round-robin est utilisé pour les clients du même type (torrent/usenet) qui ont la même priorité.

## Paramètres du client Torrent

- Nom - Le nom du client de téléchargement dans Prowlarr
- Activer - Activer ce client de téléchargement
- Hôte - L'URL de votre client de téléchargement
- Port - Le port de votre client de téléchargement ; il s'agit généralement du port webgui
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez être conscient de cette erreur courante.
- URL de base - Ajoutez un préfixe à l'URL ; cela est généralement nécessaire pour les proxies inverses.
- Nom d'utilisateur - le nom d'utilisateur pour s'authentifier auprès de votre client
- Mot de passe - le mot de passe pour s'authentifier auprès de votre client
- Catégorie - la catégorie dans votre client de téléchargement que Prowlarr utilisera
- Priorité - priorité du client de téléchargement pour les éléments ajoutés
- État initial - État initial des torrents (uniquement pour Qbittorrent : Forcé contourne tous les seuils de seed)
- Priorité du client - Priorité du client de téléchargement dans Prowlarr. Le round-robin est utilisé pour les clients du même type (torrent/usenet) qui ont la même priorité.

## Tester le client de téléchargement

Testez votre entrée. Si une coche verte apparaît, vous pouvez enregistrer votre entrée et répéter si nécessaire pour chaque client de téléchargement que vous souhaitez que Prowlarr utilise. S'il échoue, vous devrez vérifier votre journal pour l'erreur (connexion, identifiants, etc.).

# Notifications

> Des informations sur les fournisseurs de notifications pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/prowlarr/supported#notifications) pour cette section
{.is-info}

## Connexions

Les connexions déterminent comment vous souhaitez que Prowlarr communique avec le monde extérieur.

- En appuyant sur le bouton <kb>+</kb>, une nouvelle fenêtre s'ouvrira vous permettant de configurer de nombreux points de terminaison différents

- Une liste des notifications et connexions prises en charge se trouve sur la page [Plus d'informations (Pris en charge)](/prowlarr/supported#notifications)

## Déclencheurs de notification

- Lors de la capture d'une version - Soyez notifié lors de la capture d'une version depuis Prowlarr ou depuis l'API
  - Inclure les captures manuelles - Soyez notifié des captures déclenchées manuellement dans l'interface utilisateur de Prowlarr
- En cas de problème de santé - Soyez notifié en cas d'échec de la vérification de santé
  - Inclure les avertissements de santé - Soyez notifié des avertissements de santé en plus des erreurs.
- Lors de la mise à jour de l'application - Soyez notifié lorsque Prowlarr est mis à jour vers une nouvelle version

# Tags

- La section des tags dans Prowlarr est utilisée pour lier différents aspects de Prowlarr.
- Les tags sont particulièrement utiles pour :
  - Activer le proxy Flaresolverr pour une utilisation avec un indexeur ; Notez que les proxies Flaresolverr sont désactivés sans tag
  - Activer un proxy HTTP ou SOCKS pour une utilisation avec un indexeur
  - Spécifier des indexeurs pour certaines applications

# Général

C'est ici que vous modifierez les paramètres généraux de l'application tels que le port et le niveau de journalisation.

Cliquez sur `Paramètres` => `Général`.

> Beaucoup d'options ici ne peuvent être vues qu'en cliquant sur "Afficher les options avancées" en haut de l'écran. Tous les éléments de menu en orange ne sont affichés que lorsque les options avancées sont activées.
{.is-info}

## Hôte

![general_host.png](/assets/prowlarr/general_host.png)

- (Option avancée) Adresse de liaison - Laissez-la sur `*` à moins que vous ayez besoin de la modifier. L'adresse/le nom d'hôte IPv4 sur lequel Prowlarr écoutera. (par défaut : `*`)
  - Notez que `*` correspond à toutes les adresses
- Numéro de port - le port sur lequel Prowlarr s'exécute. Il doit être unique. (par défaut : 9696)
- URL de base - Entrez ici une URL de base si vous utilisez un proxy inverse. (redémarrage requis) (par défaut : vide)
- (Option avancée) Nom de l'instance - Nom à utiliser pour l'onglet du navigateur et le SysLog (si activé) (redémarrage requis) (par défaut : Prowlarr)
- (Option avancée) Utiliser SSL - Cochez cette case si vous utilisez une adresse https pour vous connecter à Prowlarr. Si vous utilisez `localhost` ou une adresse IP, cela ne doit presque JAMAIS être coché. (par défaut : false)
- Lancer le navigateur (Windows uniquement) - Cochez cette case si vous souhaitez qu'une fenêtre de navigateur soit ouverte lorsque Prowlarr démarre. (par défaut : oui)

## Sécurité

![general_security.png](/assets/prowlarr/general_security.png)

- Authentification - Comment souhaitez-vous vous authentifier pour accéder à votre instance de Prowlarr
  - Aucune - Vous n'avez pas besoin d'authentification pour accéder à votre Prowlarr. Cela est généralement le cas si vous êtes le seul utilisateur de votre réseau, si personne sur votre réseau ne souhaite accéder à votre Radarr ou si votre Radarr n'est pas exposé sur le web.
  - Basique (fenêtre contextuelle du navigateur) - Cette option affiche une petite fenêtre contextuelle vous permettant de saisir un nom d'utilisateur et un mot de passe lorsque vous accédez à votre Prowlarr.
  - Formulaire (page de connexion) - Cette option affiche une page de connexion familière, similaire à celle des autres sites web, qui vous permet de vous connecter à votre Prowlarr.
- Clé API - La clé API est utilisée par les applications externes pour accéder à Prowlarr. Elle est secrète et ne doit être partagée avec personne. Si elle est partagée, vous devez la régénérer et mettre à jour vos applications.
- Validation du certificat - Modifiez le niveau de validation strict du certificat HTTPS
  - Activé - Valider tous les certificats HTTPS (recommandé)
  - Désactivé pour les adresses locales - Valider tous les certificats HTTPS, sauf ceux de localhost et du réseau local (LAN)
  - Désactivé - Ne pas valider les certificats HTTPS

## Proxy

![general_proxy.png](/assets/prowlarr/general_proxy.png)

Proxy - Cette option vous permet de faire passer les informations récupérées et recherchées par votre Prowlarr par un proxy. Cela peut être utile si vous vous trouvez dans un pays qui n'autorise pas le téléchargement de fichiers Torrent.

- Utiliser un proxy - Activer pour utiliser un proxy
- Type de proxy - Sélectionnez le type de proxy (HTTPS, Socks4 ou Socks5)
- Nom d'hôte - Saisissez le nom d'hôte de votre proxy (ne pas inclure http/https ou tout autre protocole)
- Port - Saisissez le port de votre proxy
- Nom d'utilisateur - Saisissez le nom d'utilisateur de votre proxy, le cas échéant
- Mot de passe - Saisissez le mot de passe de votre proxy, le cas échéant
- Adresses ignorées - Saisissez une liste d'adresses séparées par des virgules qui doivent contourner le proxy
- Contourner le proxy pour les adresses locales - Cochez la case pour contourner le proxy pour les adresses locales.

## Journalisation

![general_logging.png](/assets/prowlarr/general_logging.png)

Le niveau de journalisation par défaut est `Info`. Il s'agit d'une journalisation très basique. Vous pouvez le modifier ici pour obtenir une journalisation plus détaillée. Les fichiers journaux seront rotatifs, vous n'avez donc pas à craindre de prendre trop d'espace.

- Niveau de journalisation - L'un des outils de dépannage les plus utiles
  - Info - Il s'agit de la méthode la plus basique utilisée par Prowlarr pour collecter des informations. Elle inclut un minimum d'informations dans les journaux. Ce fichier journal contient les entrées fatales, d'erreur, d'avertissement et d'information.
  - Debug - Le mode de débogage inclut toutes les informations de la méthode Info, ainsi que des informations supplémentaires qui peuvent être utiles. Ce fichier journal contient les entrées fatales, d'erreur, d'avertissement, d'information et de débogage.
  - Trace - Il s'agit du mode de journalisation le plus avancé et détaillé de Prowlarr. Le mode Trace inclut toutes les informations collectées par les modes Info et Debug, ainsi que d'autres informations. Il s'agit du type de journal le plus couramment demandé lors du dépannage sur Discord ou Reddit. Si vous avez besoin d'aide, veuillez sélectionner le mode Trace dans vos journaux et refaire la tâche qui vous posait problème afin de capturer le journal. Ce fichier journal contient les entrées fatales, d'erreur, d'avertissement, d'information, de débogage et de trace.

## Analyse

![general_analytics.png](/assets/prowlarr/general_analytics.png)

- Analyse - Envoyer des informations d'utilisation et d'erreurs anonymes aux serveurs de Prowlarr (Servarr). Cela inclut des informations sur votre navigateur, les pages WebUI de Prowlarr que vous utilisez, les rapports d'erreurs, ainsi que des informations sur le système d'exploitation, la version d'exécution, et d'autres informations connexes. Nous utiliserons ces informations pour hiérarchiser les fonctionnalités et les corrections de bugs.

## Mises à jour

![general_updates.png](/assets/prowlarr/general_updates.png)

- (Option avancée) Branche - Il s'agit de la branche de Prowlarr que vous utilisez.
  - [Veuillez consulter cette entrée de FAQ pour plus d'informations](/prowlarr/faq#how-do-i-update-prowlarr)
- Automatique - Télécharger et installer automatiquement les mises à jour. Vous pourrez toujours installer les mises à jour depuis Système : Mises à jour. Remarque : Les utilisateurs de Windows sont toujours mis à jour automatiquement.
- Mécanisme - Utiliser le système de mise à jour intégré de Prowlarr ou un script
  - Intégré - Utiliser le système de mise à jour intégré de Prowlarr
  - Script - Faire exécuter le script de mise à jour par Prowlarr
  - Docker - Ne pas mettre à jour Prowlarr depuis l'intérieur du conteneur Docker, mais plutôt télécharger une nouvelle image avec la nouvelle mise à jour
- Script - Visible uniquement lorsque le mécanisme est défini sur Script - Chemin vers le script de mise à jour
- Processus de mise à jour - Prowlarr téléchargera le fichier de mise à jour, vérifiera son intégrité, l'extraiera dans un emplacement temporaire et appellera la méthode choisie. Le processus de mise à jour sera exécuté avec le même utilisateur que celui utilisé pour exécuter Prowlarr, il aura donc besoin des autorisations nécessaires pour mettre à jour les fichiers de Prowlarr ainsi que pour arrêter/démarrer Prowlarr.
- Intégré - La méthode intégrée sauvegardera les fichiers et les paramètres de Prowlarr, arrêtera Prowlarr, mettra à jour l'installation et redémarrera Prowlarr. Si votre système ne supporte pas l'arrêt de Prowlarr et tente de le redémarrer automatiquement, il est préférable d'utiliser un script à la place. En cas d'échec, la version précédente de Prowlarr sera redémarrée.
- Script - Le script devrait gérer la mise à jour de la même manière que le système de mise à jour intégré. Si vous devez arrêter et démarrer des services (upstart/launchd/etc), vous devrez le faire ici.

## Sauvegardes

![general_backups.png](/assets/prowlarr/general_backups.png)

- (Option avancée) Dossier - Cela vous permet de sélectionner l'emplacement de sauvegarde. Dans Docker, vous serez limité à ce que le conteneur peut voir. Les chemins sont relatifs au dossier appdata ; si nécessaire, vous pouvez spécifier un chemin absolu pour sauvegarder en dehors du dossier appdata.
- (Option avancée) Intervalle - À quelle fréquence souhaitez-vous que Prowlarr effectue une sauvegarde ?
- (Option avancée) Rétention - Combien de temps souhaitez-vous que Prowlarr conserve chaque sauvegarde ? Une fois qu'une nouvelle sauvegarde est effectuée, la plus ancienne sera supprimée.

> Les sauvegardes manuelles sont conservées indéfiniment, stockées dans le même dossier et portent un nom différent.
{.is-info}

# Interface utilisateur

## Dates

- Format de date court - Comment souhaitez-vous que Prowlarr affiche les dates courtes ?
- Format de date long - Comment souhaitez-vous que Prowlarr affiche les dates au format long ?
- Format de l'heure - Souhaitez-vous un format 12 heures ou 24 heures ?
- Afficher les dates relatives - Souhaitez-vous que Prowlarr affiche des dates relatives (Aujourd'hui/Hier/etc) ou des dates absolues ?

## Style

- Thème - Sélectionnez le thème de couleur que Prowlarr doit utiliser, inspiré de [Theme.Park](https://github.com/GilbN/theme.park)
- Activer le mode pour les personnes atteintes de daltonisme - Style modifié pour permettre aux personnes atteintes de daltonisme de mieux distinguer les informations codées par couleur

## Langue

- Langue de l'interface utilisateur - Sélectionnez la langue que Prowlarr doit utiliser dans l'interface de l'application