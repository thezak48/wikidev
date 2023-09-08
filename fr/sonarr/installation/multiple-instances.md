---
title: Instances multiples
description: 
published: true
date: 2023-08-20T02:23:13.676Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:35.847Z
---

# Instances multiples

Il est possible d'exécuter plusieurs instances de Sonarr. Cela est généralement fait lorsque l'on souhaite avoir une copie en 4K et une copie en 1080p d'une série.
[Notez que vous pouvez configurer Sonarr pour utiliser un deuxième Sonarr comme liste. Cela est utile si vous souhaitez les garder synchronisés.](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)

- [Instances multiples sous Windows](#windows-multi)
- [Instances multiples sous Linux](#linux-multi)
- [Instances multiples avec Docker](#docker-multi)
{.links-list}

Les exigences suivantes doivent être notées :

- Si vous n'utilisez pas Docker, les mêmes binaires (fichiers de programme) doivent être utilisés.
- Si vous n'utilisez pas Docker, toutes les instances *doivent* avoir un argument `-data=` ou `/data=` passé.
- Si vous n'utilisez pas Docker, des ports différents doivent être utilisés.
  - Si vous utilisez Docker, des ports externes différents doivent être utilisés.
- Des catégories de clients de téléchargement différentes doivent être utilisées.
- Des dossiers racine différents doivent être utilisés.
- Si vous n'utilisez pas Docker, désactivez les mises à jour automatiques sur toutes les instances sauf une.

## Instances multiples sous Windows

{#windows-multi}

Ce guide vous montrera comment exécuter plusieurs instances de Sonarr sur Windows en utilisant une seule installation de base. Ce guide a été réalisé avec Windows 10 ; si vous utilisez une version antérieure de Windows (7, 8, etc.), vous devrez peut-être ajuster certaines choses. Ce guide suppose également que vous avez installé Sonarr dans le répertoire par défaut et que votre deuxième instance de Sonarr s'appellera Sonarr-4K. N'hésitez pas à modifier les éléments pour correspondre à vos propres installations.

### Service (Windows)

#### Prérequis (Service)

- [Vous devez déjà avoir installé Sonarr](#windows)
- Vous devez avoir [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installé. Pour l'installer, téléchargez la dernière version (2.24 au moment de la rédaction) et copiez le fichier nssm.exe 32 bits ou 64 bits dans C:/windows/system32.
  - Si vous n'êtes pas sûr d'avoir un système 32 bits ou 64 bits, vérifiez Paramètres => Système => À propos => Type de système.

#### Configuration du service Sonarr

1. Ouvrez une fenêtre d'invite de commandes en tant qu'administrateur. (Pour exécuter en tant qu'administrateur, faites un clic droit sur l'icône de l'invite de commandes et choisissez "Exécuter en tant qu'administrateur".)
1. Si Sonarr est en cours d'exécution, arrêtez le service en exécutant `nssm stop Sonarr` dans l'invite de commandes.
1. Maintenant, nous devons modifier l'instance existante de Sonarr pour lui indiquer explicitement son répertoire de données. La commande par défaut est la suivante :
   `sc config Sonarr binpath= "C:\ProgramData\Sonarr\bin\Sonarr.exe -data=C:\ProgramData\Sonarr"`

Cette commande indique à l'instance originale de Sonarr d'utiliser explicitement `C:\ProgramData\Sonarr` comme répertoire de données. Si vous n'avez pas utilisé l'installation par défaut de Sonarr, ou si votre dossier de données se trouve ailleurs, vous devrez peut-être modifier vos chemins ici.

#### Création du service Sonarr-4K

1. Créez un nouveau dossier où vous souhaitez que Sonarr-4K soit installé. La plupart des utilisateurs utilisent un emplacement similaire tel que `C:\ProgramData\Sonarr-4K`.
1. De retour dans l'invite de commandes, créez le nouveau service Sonarr-4K en utilisant `nssm install Sonarr-4K`. Une fenêtre contextuelle s'ouvrira où vous pourrez saisir les paramètres de la nouvelle instance. Pour cet exemple, nous utiliserons les paramètres suivants :
   - Chemin : `C:\ProgramData\Sonarr\bin\Sonarr.exe`
   - Répertoire de démarrage : `C:\ProgramData\Sonarr\bin`
   - Arguments : `-data=C:\ProgramData\Sonarr-4K`

> Notez que **Arguments** pointe vers le *nouveau* dossier créé à l'étape 1. Cela est crucial, car il permet de conserver tous les fichiers de données des deux instances dans des emplacements distincts. {.is-warning}

1. Cliquez sur *Installer le service*. La fenêtre devrait se fermer et le service sera désormais disponible pour être exécuté.
1. Poursuivez avec [la configuration de Sonarr-4k](#windows-multi-config-second)

### Application de la barre d'état système (Windows)

#### Prérequis (Application de la barre d'état système)

- [Vous devez déjà avoir installé Sonarr](#windows)
- Sonarr doit être configuré avec un argument `/data=` pour permettre plusieurs instances
- Accédez au dossier de démarrage de l'utilisateur actuel `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` et modifiez le raccourci existant si nécessaire.

#### Création de l'application de la barre d'état système Sonarr-4K

- Faites un clic droit et créez un nouveau raccourci
- Chemin : `C:\ProgramData\Sonarr\bin\Sonarr.exe /data=C:\ProgramData\Sonarr-4K`
- Donnez un nom unique au raccourci, tel que `Sonarr-4K`, et terminez l'assistant.
- Double-cliquez sur le nouveau raccourci pour l'exécuter et le tester.
- Poursuivez avec [la configuration de Sonarr-4k](#windows-multi-config-second)

### Configuration de Sonarr-4k {#windows-multi-config-second}

- Peu importe que vous ayez utilisé la méthode du service ou de l'application de la barre d'état système : arrêtez les deux services et les deux applications.
- Démarrez Sonarr-4k (service ou application de la barre d'état système).
- Ouvrez Sonarr-4k et naviguez dans l'application vers [Paramètres => Général => Hôte](/sonarr/settings/#host)
- Modifiez le `Numéro de port` de `8989` à un port différent, par exemple `7879`, afin que Sonarr et Sonarr-4k ne se chevauchent pas.
- Vous devriez maintenant pouvoir démarrer les deux applications.
- Poursuivez avec [la gestion des mises à jour](#dealing-with-updates)

### Gestion des mises à jour

- Désactivez les mises à jour automatiques sur l'une de vos instances.
- Si une instance de Sonarr est mise à jour, les deux instances s'arrêteront et seule l'instance mise à jour redémarrera. Pour résoudre ce problème, vous devrez démarrer manuellement l'autre instance, ou vous voudrez peut-être envisager d'utiliser le script PowerShell ci-dessous pour résoudre le problème.

#### Script PowerShell de vérification des ports et de redémarrage sous Windows

- Lorsque vous utilisez deux instances de Sonarr et que l'une d'entre elles est mise à jour, toutes les instances seront arrêtées. Seule celle qui est mise à jour reviendra en ligne.
- Le script PowerShell ci-dessous doit être configuré en tant que tâche planifiée.
- Il vérifie les ports et, s'il en trouve un qui n'est pas en ligne, il (re)démarre la tâche planifiée pour lancer Sonarr.

1. Créez un nouveau fichier et nommez-le SonarrInstancesChecker.ps1 avec le code ci-dessous.
1. Modifiez le script avec vos noms de service, IP et ports réels.
1. [Créez une tâche planifiée](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) pour exécuter le script selon un calendrier répétitif.

- Options de sécurité : Activer `Exécuter avec les privilèges les plus élevés`
  - Sinon, le script ne pourra pas manipuler les services
- Déclencheur : `Au démarrage`
- Répéter la tâche toutes les : `5` ou `10` minutes
- Action : `Démarrer un programme`
- Programme/script : `powershell`
- Argument : `-File D:\SonarrInstancesChecker.ps1`
  - Assurez-vous d'utiliser le chemin complet vers l'emplacement de votre script

```powershell
################################################################################################
### SonarrInstancesChecker.ps1                                                               ###
################################################################################################
### Garde plusieurs instances de Sonarr en ligne en vérifiant le port                          ###
### Veuillez utiliser le Discord ou Reddit de Sonarr pour obtenir de l'aide !                  ###
### https://wiki.servarr.com/sonarr/installation#windows-multi                               ###
################################################################################################
### Version : 1.1                                                                             ###
### Mis à jour : 2020-10-22                                                                   ###
### Auteur : reloxx13                                                                         ###
################################################################################################



### CONFIGURATION ###
# Définissez vos paramètres ici #
# Définissez correctement votre adresse IP et votre port d'hôte, et utilisez les noms de service ou de tâche planifiée appropriés !

# (string) Le type de démarrage de Sonarr
# "Service" (par défaut) : le processus de service est utilisé
# "ScheduledTask" : le planificateur de tâches est utilisé
$startType = 'Service'

# (bool) Écrit le journal dans C:\Users\VOTRENOMDUTILISATEUR\log.txt lorsqu'il est activé
# $false (par défaut)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instance 1
        Name = 'Sonarr-V3'; # (string) Nom du service ou de la tâche (par défaut : Sonarr-V3)
        IP   = '192.168.178.12'; # (string) Adresse IP du serveur où Sonarr s'exécute (par défaut : 192.168.178.12)
        Port = '7873'; # (string) Port du serveur où Sonarr s'exécute (par défaut : 7873)
    }
    [pscustomobject]@{   # Instance 2
        Name = 'Sonarr-4K'; # (string) Nom du service ou de la tâche (par défaut : Sonarr-4K)
        IP   = '192.168.178.12'; # (string) Adresse IP du serveur où Sonarr s'exécute (par défaut : 192.168.178.12)
        Port = '7874'; # (string) Port du serveur où Sonarr s'exécute (par défaut : 7874)
    }
    # Si nécessaire, vous pouvez ajouter plus d'instances ici... en décommentant les lignes ci-dessous
    # [pscustomobject]@{   # Instance 3
    # Name='Sonarr-3D';    # (string) Nom du service ou de la tâche (par défaut : Sonarr-3D)
    # IP='192.168.178.12'; # (string) Adresse IP du serveur où Sonarr s'exécute (par défaut : 192.168.178.12)
    # Port='7875';         # (string) Port du serveur où Sonarr s'exécute (par défaut : 7875)
    # }
)


### NE CHANGEZ RIEN CI-DESSOUS ###


###
# Cette fonction écrit dans un fichier journal ou dans la sortie de la console
###
function Write-Log
{
    # Écrit dans C:\Users\VOTRENOMDUTILISATEUR\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    # Sortie de la console
    Write-Output "[$(TS)]$Message"
    
    # Sortie dans un fichier
    if ($logToFile)
    {
        "[$(TS)]$Message" | Tee-Object -FilePath $Path -Append | Write-Verbose
    }
}


Write-Log 'DÉBUT ====================='


$instances | ForEach-Object {
    Write-Log "Vérification de $($_.Name) $($_.IP):$($_.Port)"
    
    $PortOpen = ( Test-NetConnection $_.IP -Port $_.Port -WarningAction SilentlyContinue ).TcpTestSucceeded 
    
    if (!$PortOpen)
    {
        Write-Log "Le port $($_.Port) est fermé, redémarrage de $($startType) $($_.Name) !"

        if ($startType -eq 'Service')
        {
            Get-Service -Name $_.Name | Stop-Service
            Get-Service -Name $_.Name | Start-Service
        }
        elseif ($startType -eq 'ScheduledTask')
        {
            Get-ScheduledTask -TaskName $_.Name | Stop-ScheduledTask
            Get-ScheduledTask -TaskName $_.Name | Start-ScheduledTask
        }
        else
        {
            Write-Log '[ERREUR] TYPE DE DÉMARRAGE INCONNU ! UTILISEZ Service ou ScheduledTask !'
        }
    }
    else
    {
        Write-Log "Le port $($_.Port) est ouvert !"
    }
}

Write-Log 'FIN ====================='
```

## Instances multiples sous Linux

{#linux-multi}

- [Utilisateurs de Swizzin](https://github.com/ComputerByte/sonarr4k)
- Utilisateurs non-Swizzin
  - Assurez-vous que votre première instance a l'argument `-data=` passé.
  - Arrêtez temporairement votre première instance afin de pouvoir modifier le port de la deuxième instance `systemctl stop sonarr`
  - Désactivez les mises à jour automatiques sur l'une de vos instances Sonarr

> Voici un exemple de script pour créer une instance Sonarr4K. Le script de création systemd ci-dessous utilisera un répertoire de données `/var/lib/sonarr4k/`. Assurez-vous que le répertoire existe ou modifiez-le si nécessaire.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/sonarr4k.service > /dev/null
[Unit]
Description=Démon Sonarr4k
After=syslog.target network.target
[Service]
User=sonarr
Group=media
Type=simple

ExecStart=mono --debug /usr/lib/sonarr/bin/Sonarr.exe -nobrowser -data=/var/lib/sonarr4k/
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
```

- Rechargez systemd :

```shell
sudo systemctl -q daemon-reload
```

- Activez le service Sonarr4k :

```shell
sudo systemctl enable --now -q sonarr4k
```

## Instances multiples avec Docker

{#docker-multi}

- Il suffit de lancer un deuxième conteneur Docker avec un nom différent, en veillant à respecter les exigences mentionnées ci-dessus.