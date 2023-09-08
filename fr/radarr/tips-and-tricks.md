---
title: Astuces et conseils pour Radarr
description: 
published: true
date: 2022-03-24T02:53:26.272Z
tags: radarr, needs-love, tips-and-tricks
editor: markdown
dateCreated: 2021-08-14T15:12:58.934Z
---

# Formats personnalisés de TRaSH

- [TRaSH a rédigé un guide](https://trash-guides.info/Radarr/) sur l'utilisation des [Formats personnalisés de Radarr => Paramètres](/radarr/settings#custom-formats) ainsi qu'un référentiel partagé de Formats personnalisés.

# Synchronisation de deux instances de Radarr

- TRaSH a rédigé [un guide](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) pour synchroniser deux instances.

# Renommer les dossiers de films

- [Consultez cette entrée FAQ](/radarr/faq#how-can-i-rename-my-movie-folders)

# Créer un dossier pour chaque film

- Ceci est uniquement nécessaire pour nettoyer/organiser une bibliothèque existante afin de faciliter l'importation dans Radarr. Voici quelques méthodes différentes.

## Filebot

> Filebot est pris en charge sur Windows, Linux et MacOS {.is-info}

- [Filebot](https://www.filebot.net/) est un utilitaire fantastique pour organiser vos films de manière à ce que Radarr puisse les analyser avec succès. La version 4.7.9 peut toujours être téléchargée gratuitement depuis un miroir SourceForge, mais il existe également des versions payantes dans les magasins Windows et Apple. Sur Linux, votre distribution préférée peut proposer un paquet pour cela, comme le paquet AUR d'Arch ou les fichiers `.deb` pour Debian/Ubuntu depuis leur page de téléchargement. Il dispose à la fois d'une interface graphique et d'une interface en ligne de commande, il devrait donc satisfaire presque tout le monde.

- Une grande aide est disponible, y compris leur page d'expressions de format. Ma suggestion personnelle est d'utiliser quelque chose comme `{ny}\{fn}` si vos fichiers incluent des détails utiles tels que la qualité, l'édition et/ou le groupe, ou `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]` s'ils ne le font pas, ce qui donnerait `Film (Année)/Film (Année) [Bluray-1080p]` ou `Film (Année)/Film (Année) [DVD-480p]` par exemple. Au lieu de Bluray, vous pouvez également utiliser WEBDL si vous préférez que votre collection soit considérée comme telle.

- Pour conserver ce modèle pour les futurs films, vous devez définir :

- [Paramètres => Gestion des médias (Paramètres avancés affichés) => Nom du film](/radarr/settings#media-management)

  - Fichier : `{Movie CleanTitle} {(Release Year)} {Edition Tags} {\[Quality Title]}`
  - Dossier : `{Movie CleanTitle} {(Release Year)}`

- Remarque : Vous pouvez remplacer les espaces ci-dessus par `.` ou `_` si vous préférez ce format de nommage.

## Files 2 Folder

> Files 2 Folder est une application Windows {.is-info}

[Files 2 Folder](http://www.dcmembers.com/skwire/download/files-2-folder/) peut organiser votre bibliothèque de films pour l'importer dans Radarr. Il vous suffit d'extraire le fichier zip sur votre ordinateur et d'exécuter le fichier .exe en tant qu'administrateur, puis de cliquer sur Oui pour l'ajouter à votre menu clic droit.

Une fois installé, il vous suffit de quelques clics pour organiser tous vos fichiers dans leurs propres dossiers.

1. Accédez à votre dossier de films.
1. Sélectionnez tous les fichiers, puis cliquez avec le bouton droit pour afficher le menu.
1. Sélectionnez l'option `files 2 folder` dans le menu.
1. Dans la fenêtre Files 2 Folder, sélectionnez `Déplacer chaque fichier dans des sous-dossiers individuels en fonction de leur nom`.
1. Cliquez sur OK.
1. Attendez un moment et tous vos fichiers seront dans leurs propres dossiers.

## Script Bash Linux

Le script suivant prendra tous les fichiers `*.mkv` dans votre dossier sélectionné et les déplacera dans un dossier basé sur leur nom. Notez que cela ne parcourt pas les sous-dossiers du dossier de départ/sélectionné.

```shell
cd /chemin/vers/vos/fichiers/de/films/
find . -maxdepth 1 -type f -iname "*.mkv" -exec sh -c 'mkdir "${1%.*}" ; mv "${1%}" "${1%.*}" ' _ {} \;
```

## Ligne de commande Windows

Accédez à une ligne de commande dans Windows (cmd.exe) `en tant qu'administrateur`. Accédez à votre dossier de films. Exécutez ces deux commandes (copier/coller est correct, il n'y a rien à modifier) :

`for %i in (*) do md "%~ni"`

Cela créera un dossier pour chaque fichier du répertoire.

`for %i in (*) do move "%i" "%~ni"`

Cela déplacera tous vos fichiers dans les nouveaux répertoires.

Si vous devez nettoyer les dossiers vides, cette commande le fera :

`for /f "usebackq delims=" %d in ("dir /ad/b/s | sort /R") do rd "%d"`

## PowerShell Windows

Alternativement, sous Windows, vous pouvez exécuter le script suivant dans PowerShell pour itérer sur chaque fichier d'un répertoire et le déplacer dans un dossier portant le même nom.

```powershell
Get-ChildItem -File 
  | ForEach-Object {
    $dir = New-Item -ItemType Directory -Name $_.BaseName -Force
    $_ | Move-Item -Destination $dir
  }
```