---
title: Installation de Readarr sur Windows
description: Guide d'installation de Readarr sur Windows
published: true
date: 2023-07-04T15:23:25.114Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:03.495Z
---

# Windows

Readarr est nativement pris en charge sur Windows. Readarr peut être installé sur Windows en tant que service Windows ou en tant qu'application de la barre système.
> Les versions de Windows sont limitées au support des versions actuellement prises en charge par Microsoft. D'autres versions peuvent fonctionner, mais cela n'est pas pris en charge.
{.is-warning}

Un service Windows s'exécute même lorsque l'utilisateur n'est pas connecté, mais des précautions particulières doivent être prises car les services Windows [ne peuvent pas accéder aux lecteurs réseau](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (lecteurs mappés X:\ ou chemins UNC \\\serveur\partage) sans des étapes de configuration spéciales.

De plus, le service Windows s'exécute sous le compte 'Local Service'. Par défaut, ce compte **n'a pas les autorisations pour accéder au répertoire personnel de votre utilisateur, à moins que des autorisations n'aient été attribuées manuellement**. Cela est particulièrement pertinent lorsque vous utilisez des clients de téléchargement configurés pour télécharger dans votre répertoire personnel.

Il est donc conseillé d'installer Readarr en tant qu'application de la barre système si l'utilisateur peut rester connecté. L'option pour le faire est fournie lors de l'installation.

> Vous devrez peut-être exécuter une fois "En tant qu'administrateur" après l'installation si vous obtenez une erreur d'accès, telle que l'accès au chemin `C:\ProgramData\Readarr\config.xml` est refusé, ou si vous utilisez des lecteurs réseau mappés. Cela donne à Readarr les autorisations dont il a besoin. Vous ne devriez pas avoir besoin d'exécuter en tant qu'administrateur à chaque fois.
{.is-warning}

> Avertissement : Si vous exécutez Plex en tant que service via [PmsService](https://github.com/cjmurph/PmsService), vous devrez soit modifier le port de PMsService à partir de `8787`, soit modifier le port sur lequel Readarr s'exécute dans le fichier `config.xml`.
{.is-info}

1. Téléchargez la dernière version de Readarr pour votre architecture en suivant les liens ci-dessous.
1. Exécutez l'installateur.
1. Accédez à <http://localhost:8787> pour commencer à utiliser Readarr.

- [Installateur Windows x64](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Installateur Windows x32](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Il est possible d'installer Readarr manuellement en utilisant le [téléchargement .zip x64](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64). Cependant, dans ce cas, vous devez gérer manuellement les dépendances, l'installation et les autorisations.
{.is-info}