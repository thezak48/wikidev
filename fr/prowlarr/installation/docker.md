---
title: Installation de Prowlarr avec Docker
description: Guide d'installation de Prowlarr avec Docker
published: true
date: 2023-08-12T16:03:43.190Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:13.937Z
---

# Docker

L'équipe de Prowlarr ne propose pas d'image Docker officielle. Cependant, plusieurs tiers ont créé et maintiennent leurs propres images.

> Pour une explication plus détaillée de Docker et des pratiques recommandées, consultez l'article du wiki [The Best Docker Setup and Docker Guide](/docker-guide) (en anglais).
{.is-info}

Les utilisateurs de Synology peuvent consulter le guide Docker de Synology de [TRaSH](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) (en anglais).

## Portainer

> **Portainer doit être évité pour la configuration des conteneurs Docker** {.is-danger}

- Portainer offre une interface graphique pratique pour gérer les conteneurs, mais c'est tout ce qu'il est utile.
- Portainer ne doit être utilisé que pour afficher les journaux des conteneurs Docker ou l'état des conteneurs.
- Il est fortement recommandé d'utiliser Docker Compose et de ne pas utiliser Portainer.
- Portainer présente de nombreux problèmes, tels que :
  - Ordre incorrect des sources et des cibles des montages
  - Sensibilité à la casse incohérente
  - Absence de création automatique de réseaux personnalisés pour la communication entre conteneurs
  - Implémentations de Docker Compose incohérentes sur différentes architectures
  - Télécharge toutes les balises lors de la mise à jour si vous ne spécifiez pas une balise spécifique
  - Certaines fonctionnalités sont masquées et certaines ne fonctionnent pas du tout sur les plates-formes ARM

Consultez plutôt ce [guide Docker](/docker-guide) et ce [tutoriel Docker de TRaSH](https://trash-guides.info/hardlinks/) (en anglais) pour savoir comment configurer Docker Compose.

## Installer Prowlarr

Pour installer et utiliser ces images Docker, vous devrez garder à l'esprit les informations ci-dessus tout en suivant leur documentation. Il existe de nombreuses façons de gérer les images et les conteneurs Docker, donc l'installation et la maintenance dépendront de la méthode que vous choisissez.

- [hotio/prowlarr](https://hotio.dev/containers/prowlarr/) (en anglais)
- [lscr.io/linuxserver/prowlarr](https://docs.linuxserver.io/images/docker-prowlarr) (en anglais)
{.links-list}