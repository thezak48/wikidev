---
title: Radarr Pris en charge
description: 
published: true
date: 2023-09-01T16:45:41.479Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:24.002Z
---

# Table des matières

> Cette page est en cours de réalisation et nécessite des efforts supplémentaires.{.is-warning}

Cette page est la page de désambiguïsation pour tous les liens wiki `pris en charge` (c'est-à-dire généralement "plus d'informations" dans l'interface utilisateur).

# Clients de téléchargement

{#downloadclient}

- Aria2 {#aria2}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- Deluge {#deluge}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- Flood {#flood}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- Transmission {#transmission}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Voir la page des paramètres](/radarr/settings#download-clients)
  - Étant donné que uTorrent est un logiciel publicitaire et autrefois un logiciel espion, il n'est pas recommandé. La plupart des utilisateurs utilisent Qbittorrent.
- Vuze {#vuze}
  - [Voir la page des paramètres](/radarr/settings#download-clients)

# Indexeurs

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)
  - Newznab est une API standardisée utilisée par de nombreux sites d'indexation Usenet. De nombreux paramètres prédéfinis sont disponibles, mais tous nécessitent une clé API pour être accessibles.
  - Des applications d'indexation comme [Prowlarr](/prowlarr) et [NZBHydra2](https://github.com/theotherp/nzbhydra2) peuvent fournir des fonctionnalités avancées telles que le suivi des statistiques.
- omgwtfnzbs {#omgwtfnzbs}
  - Une implémentation obsolète d'un indexeur Usenet privé. Utilisez plutôt Newznab.
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - Tracker privé
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Tracker privé
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Tracker privé
  > L'implémentation native d'IP Torrents ne prend pas en charge la recherche. Utilisez-la via Prowlarr ou Jackett en tant que torznab à la place {.is-info}
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Tracker de torrents exclusivement pour les médias japonais (anime).
  > Nyaa n'apprécie pas l'automatisation et bannit fréquemment votre adresse IP. {.is-info}
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)
- Pass The Popcorn (PTP) {#passthepopcorn}
  - Tracker privé
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Tracker public
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)
- Torrent RSS Feed {#torrentrssindexer}
  - Analyseur de flux RSS de torrents générique.
  > Le flux RSS doit contenir une `pubdate`. La taille de la version est également recommandée.
  {.is-info}
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)
- TorrentPotato {#torrentpotato}
  - Un format hérité de Couchpotato avant Torznab.
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab est un jeu de mots entre Torrent et Newznab. Il utilise la même structure et la même syntaxe que la spécification de l'API Newznab, mais expose des attributs spécifiques aux torrents et des fichiers .torrent. Il prend donc en charge un flux RSS récent ET des capacités de recherche dans les archives. La spécification n'est pas maintenue ni prise en charge par l'organisation Newznab. (La même spécification d'API est partagée avec nZEDb)
  - Cela est principalement pris en charge par [Prowlarr](/prowlarr) et [Jackett](https://github.com/Jackett/Jackett)
  - [Voir la page des paramètres](/radarr/settings#indexer-settings)

> De nombreux trackers de torrents s'appuient sur la communauté et peuvent avoir des règles en place qui imposent des visites sur le site, du karma, des votes, des commentaires, etc.
> Veuillez consulter les règles et l'étiquette de votre tracker, maintenez votre communauté en vie.
> Nous ne sommes pas responsables si votre compte est banni pour non-respect des règles ou accumulation de Hit and Runs (HnRs)/faible ratio.
{.is-warning}

# Notifications

{#notification}

- Boxcar {#boxcar}
- Script personnalisé {#customscript}
  - Cela vous permet de créer un script personnalisé qui s'exécutera lorsqu'une action particulière se produit. Consultez [Scripts personnalisés](/radarr/custom-scripts) pour plus de détails.
- Discord {#discord}
  - De loin l'un des moyens les plus courants de recevoir des notifications sur les actions se produisant sur votre Radarr
- Email {#email}
  - Envoyez simplement un e-mail à vous-même ou à quelqu'un que vous voulez ennuyer. Si vous utilisez Gmail, vous devez activer les applications moins sécurisées. Si vous utilisez Gmail et que vous avez activé l'authentification à deux facteurs, vous devez utiliser un mot de passe spécifique à l'application.

> Vous pouvez utiliser une "jolie adresse" comme `SomePrettyName <email@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi est né de l'amour des médias. C'est un centre de divertissement qui regroupe tous vos médias numériques dans une interface conviviale et esthétique. Il est entièrement gratuit et open source, très personnalisable et fonctionne sur une grande variété d'appareils. Il est soutenu par une équipe de bénévoles dévoués et une communauté très active. En ajoutant Kodi en tant que connexion, vous pouvez mettre à jour la bibliothèque de Kodi lorsqu'un nouveau film est ajouté à Radarr.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Voir l'entrée sur [Outils utiles - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Serveur multimédia Plex {#plexserver}
  - Le serveur pour votre système Plex auto-hébergé. L'activation de cette option, tout comme Kodi, vous permettra de mettre à jour votre serveur Plex pour lui signaler qu'un nouveau film est disponible ou a été mis à niveau.
  - Cela est rarement nécessaire et n'est requis que si Plex ne peut pas surveiller le système de fichiers pour détecter les modifications.
  - Dans les quelques situations où Plex ne peut pas surveiller le système de fichiers à l'aide d'ionotify - comme certains types de montages distants et quelques anciens montages réseau - il est recommandé d'utiliser l'application plexautoscan plutôt que la connexion Plex
- Un outil comme [plexautoscan](https://github.com/l3uddz/plex_autoscan) est une autre option.

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Indexeur Synology {#synologyindexer}
- Telegram {#telegram}
- Trakt {#trakt}
- Twitter {#twitter}
  - Voir cette entrée [Trucs et astuces](/useful-tools#twitter)
- Webhook {#webhook}

# Listes

{#importlist}

- CouchPotato {#couchpotatoimport}
- Listes personnalisées {#radarrlistimport}
- Listes IMDb {#imdblistimport}
  - Pour ajouter votre liste de surveillance IMDb, accédez à votre liste et cliquez sur Modifier. Assurez-vous que le paramètre de confidentialité est défini sur public. Dans la barre d'adresse, vous trouverez le numéro `lsxxxxxx` que vous devrez entrer dans Radarr

    1. Accédez aux paramètres de votre liste IMDb
    1. Assurez-vous que la confidentialité est définie sur `Public` (c'est-à-dire `Désactivée`)
    1. Utilisez le numéro `ls` dans l'URL

  ![imdb-list-ls.png](/assets/radarr/imdb-list-ls.png)
- Liste de surveillance Plex {#plex}
  - Requiert : v4.1.0.6176+
  - Ajoutez simplement une liste de surveillance Plex pour l'utilisateur Plex authentifié à Radarr. Notez qu'il est nécessaire que votre liste contienne des films.
  - Pour avoir les listes de surveillance de plusieurs utilisateurs, vous devrez ajouter les listes de chaque utilisateur et vous authentifier avec leur utilisateur Plex.
- Radarr {#radarrimport}
  - TRaSH a [un guide](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) pour synchroniser deux instances
- Liste RSS {#rssimport}
- StevenLu Custom {#stevenluimport}
	- Vous permet de créer des listes de films personnalisées au format JSON.
  	Votre flux doit fournir pour chaque film soit un `titre`, soit un `imdb_id`, les deux peuvent être fournis.
  		> Notez que `imdb_id` est plus sûr que `titre` car il ne nécessite pas de recherche large
    Voici un exemple de JSON valide :
      ```
      [
          {
            "title": "The Wastetown",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/6J32RMp8uko8CUEM3rYP962hQun.jpg",
            "imdb_id": "tt22889064"
          },
          {
            "title": "Wild Sunflowers",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/tHK4c0UZKrqkmXZ2HJeGNhNetRz.jpg",
            "imdb_id": "tt13774830"
          }
      ]
      ```
      - Des clés supplémentaires peuvent être ajoutées dans les éléments (elles seront ignorées)
      - Pour une liste vide, retournez simplement un tableau JSON vide `[]`
- StevenLu List {#stevenlu2import}
- Collection TMDb {#tmdbcollectionimport}
  - Les listes de collections ne sont plus prises en charge dans Radarr v4.2 et ont été migrées vers les collections dans Radarr. Consultez la section [Collections](/radarr/library#collections) pour plus de détails.
- Société TMDb {#tmdbcompanyimport}
- Mot-clé TMDb {#tmdbkeywordimport}
- Liste TMDb {#tmdblistimport}
- Personne TMDb {#tmdbpersonimport}
  - Si l'URL de la personne TMDb est `https://www.themoviedb.org/person/500-tom-cruise`, alors l'ID de la personne est `500`
- Populaire TMDb {#tmdbpopularimport}
  - Top utilise <https://developers.themoviedb.org/3/movies/get-top-rated-movies>
  - Populaire utilise <https://developers.themoviedb.org/3/movies/get-popular-movies>
  - En salle utilise <https://developers.themoviedb.org/3/movies/get-now-playing>
  - À venir utilise <https://developers.themoviedb.org/3/movies/get-upcoming>
- Utilisateur TMDb {#tmdbuserimport}
- Liste Trakt {#traktlistimport}
  - Nom d'utilisateur - Assurez-vous d'entrer le nom d'utilisateur réel de l'utilisateur et non le nom de l'utilisateur
  - Liste - Assurez-vous d'utiliser le nom de la liste tel qu'il apparaît dans l'URL de la liste
  - Exemple : `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Nom d'utilisateur : `some-user-name`
    - Liste : `trakt-list-name`
- Liste populaire Trakt {#traktpopularimport}
- Utilisateur Trakt {#traktuserimport}
  - Ce type doit être utilisé lorsque vous utilisez votre propre liste de surveillance

# Métadonnées

{#metadata}

- Emby (Legacy) {#mediabrowsermetadata}
  - Activer - Activer la création de fichiers de métadonnées pour ce type de métadonnées
  - Métadonnées de film - Activer la création de fichiers de métadonnées pour ce type de métadonnées
- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Activer - Activer la création de fichiers de métadonnées pour ce type de métadonnées
  - Métadonnées de film - Créer un fichier `<nomfichier>.nfo` avec les métadonnées du film
  - (Option avancée) URL des métadonnées de film - Créer un fichier `movie.nfo` avec les URL des films TMDb et IMDb
  - Langue des métadonnées - Sélectionnez la langue que Radarr doit utiliser pour écrire les métadonnées si elles sont disponibles dans cette langue
  - Images de film - Créer diverses images de saison, y compris des affiches et des bannières
  - Utiliser Movie.nfo - Écrire le fichier nfo en tant que `movie.nfo` plutôt que par défaut
  - Nom de la collection - Radarr écrira le nom de la collection dans le fichier .nfo
- Roksbox {#roksboxmetadata}
  - Activer - Activer la création de fichiers de métadonnées pour ce type de métadonnées
  - Métadonnées de film - Créer un fichier XML pour chaque film
  - Images de film - Créer `Movie.jpg`
- WDTV {#wdtvmetadata}
  - Activer - Activer la création de fichiers de métadonnées pour ce type de métadonnées
  - Métadonnées de film - Créer un fichier `<nomfichier>.xml` pour chaque épisode
  - Images de film - Créer `folder.jpg`