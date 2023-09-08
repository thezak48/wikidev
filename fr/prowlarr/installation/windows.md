---
title: Installation de Prowlarr sur Windows
description: Guide d'installation de Prowlarr sur Windows
published: true
date: 2023-08-28T19:43:08.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:39.779Z
---

# Windows

Prowlarr est nativement pris en charge sur Windows. Prowlarr peut être installé sur Windows en tant que service Windows ou en tant qu'application de la barre système.
> Les versions de Windows sont limitées à celles actuellement prises en charge par Microsoft. D'autres versions peuvent fonctionner, mais cela n'est pas pris en charge.
{.is-warning}

Un service Windows s'exécute même lorsque l'utilisateur n'est pas connecté.
Sinon, une application de la barre système peut être utilisée si l'utilisateur reste connecté. L'option correspondante est proposée lors de l'installation.

> Vous devrez peut-être exécuter une fois "En tant qu'administrateur" après l'installation si vous obtenez une erreur d'accès telle que "Accès au chemin `C:\ProgramData\Prowlarr\config.xml` refusé". Cela donne à Prowlarr les autorisations dont il a besoin. Vous ne devriez pas avoir besoin d'exécuter en tant qu'administrateur à chaque fois.
{.is-warning}

1. Téléchargez la dernière version de Prowlarr correspondant à votre architecture en suivant les liens ci-dessous.
1. Exécutez l'installateur.
1. Accédez à <http://localhost:9696> pour commencer à utiliser Prowlarr.

- [Installateur Windows x64](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Installateur Windows x32](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Il est possible d'installer Prowlarr manuellement en utilisant le [téléchargement .zip x64](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64). Cependant, dans ce cas, vous devrez gérer manuellement les dépendances, l'installation et les autorisations.
{.is-info}

> Si vous utilisez [Certify The Web](https://docs.certifytheweb.com/docs/backgroundservice/) pour la gestion des certificats LetsEncrypt pour IIS et que vous installez Prowlarr sur la même machine, le port `9696` est utilisé par le service en arrière-plan. Vous devrez soit changer le port d'écoute de Prowlarr dans votre `config.xml` pour un autre port, soit changer le port du service en arrière-plan de Certify The Web.
{.is-info}