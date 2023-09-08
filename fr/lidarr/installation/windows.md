---
title: Installation de Lidarr sur Windows
description: Guide d'installation de Lidarr sur Windows
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Windows

Lidarr est nativement pris en charge sur Windows. Lidarr peut être installé sur Windows en tant que service Windows ou en tant qu'application de la barre système.
> Les versions de Windows sont limitées au support des versions actuellement prises en charge par Microsoft. D'autres versions peuvent fonctionner, mais cela n'est pas pris en charge.
{.is-warning}

Un service Windows s'exécute même lorsque l'utilisateur n'est pas connecté, mais des précautions particulières doivent être prises car les services Windows [ne peuvent pas accéder aux lecteurs réseau](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (lecteurs mappés X:\ ou chemins UNC \\\serveur\partage) sans des étapes de configuration spéciales.

De plus, le service Windows s'exécute sous le compte 'Local Service'. Par défaut, ce compte **n'a pas les autorisations pour accéder au répertoire personnel de votre utilisateur, à moins que des autorisations n'aient été attribuées manuellement**. Cela est particulièrement pertinent lorsque vous utilisez des clients de téléchargement configurés pour télécharger dans votre répertoire personnel.

Il est donc conseillé d'installer Lidarr en tant qu'application de la barre système si l'utilisateur peut rester connecté. L'option pour le faire est fournie lors de l'installation.

> Vous devrez peut-être exécuter une fois "En tant qu'administrateur" après l'installation en mode barre système, si vous obtenez une erreur d'accès - telle que l'accès au chemin `C:\ProgramData\Lidarr\config.xml` est refusé - ou si vous utilisez des lecteurs réseau mappés. Cela donne à Lidarr les autorisations dont il a besoin. Vous ne devriez pas avoir besoin d'exécuter en tant qu'administrateur à chaque fois.
{.is-warning}

1. Téléchargez la dernière version de Lidarr correspondant à votre architecture via les liens ci-dessous.
1. Exécutez l'installateur.
1. Accédez à <http://localhost:8686> pour commencer à utiliser Lidarr.

- [Installateur Windows x64](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Installateur Windows x32](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Il est possible d'installer Lidarr manuellement en utilisant le [téléchargement .zip x64](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). Cependant, dans ce cas, vous devez gérer manuellement les dépendances, l'installation et les autorisations.
{.is-info}