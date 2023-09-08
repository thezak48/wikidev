---
title: Instances multiples
description: 
published: true
date: 2023-09-01T05:05:47.102Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:10.189Z
---

# Instances multiples

Il est possible d'exécuter plusieurs instances de Radarr. Cela est généralement fait lorsque l'on souhaite avoir une copie d'un film en 4K et en 1080p. Notez que vous pouvez (et devriez probablement) [consulter le guide de TRaSH et configurer Radarr pour utiliser un deuxième Radarr comme liste](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/). Cela est utile si vous souhaitez les maintenir tous les deux synchronisés.

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

Ce guide vous montrera comment exécuter plusieurs instances de Radarr sous Windows en utilisant une seule installation de base. Ce guide a été réalisé sous Windows 10 ; si vous utilisez une version antérieure de Windows (7, 8, etc.), vous devrez peut-être ajuster certaines choses. Ce guide suppose également que vous avez installé Radarr dans le répertoire par défaut et que votre deuxième instance de Radarr s'appellera Radarr-4K. N'hésitez pas à modifier les éléments pour les adapter à vos propres installations.

> Note : Vous devez exécuter Radarr soit en tant que [service](#service-windows), soit en tant qu'[application de la barre d'état système](#tray-app-windows). Exécuter à la fois une application et un service est inutile et risque de causer des problèmes.

### Service (Windows)

#### Prérequis (Service)

- [Vous devez déjà avoir installé Radarr](#windows)
- Vous devez avoir [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installé. Pour l'installer, téléchargez la dernière version (2.24 au moment de la rédaction) et copiez le fichier nssm.exe 32 bits ou 64 bits dans C:/windows/system32.
  - Si vous n'êtes pas sûr d'avoir un système 32 bits ou 64 bits, vérifiez Paramètres => Système => À propos => Type de système.

#### Configuration du service Radarr

1. Ouvrez une fenêtre d'invite de commandes en tant qu'administrateur. (Pour exécuter en tant qu'administrateur, faites un clic droit sur l'icône de l'invite de commandes et choisissez "Exécuter en tant qu'administrateur".)
1. Si Radarr est en cours d'exécution, arrêtez le service en exécutant `nssm stop Radarr` dans l'invite de commandes.
1. Maintenant, nous devons modifier l'instance existante de Radarr pour qu'elle pointe explicitement vers son répertoire de données. La commande par défaut est la suivante :
   `sc config Radarr binpath= "C:\ProgramData\Radarr\bin\Radarr.exe -data=C:\ProgramData\Radarr"`

Cette commande indique à l'instance originale de Radarr d'utiliser explicitement `C:\ProgramData\Radarr` comme répertoire de données. Si vous n'avez pas utilisé l'installation par défaut de Radarr, ou si votre dossier de données se trouve ailleurs, vous devrez peut-être modifier vos chemins ici.

#### Création du service Radarr-4K

1. Créez un nouveau dossier où vous souhaitez que Radarr-4K soit installé. La plupart des utilisateurs utilisent un emplacement similaire tel que `C:\ProgramData\Radarr-4K`.
1. Revenez à l'invite de commandes et créez le nouveau service Radarr-4K en utilisant `nssm install Radarr-4K`. Une fenêtre contextuelle s'ouvrira où vous pourrez saisir les paramètres de la nouvelle instance. Pour cet exemple, nous utiliserons les paramètres suivants :
   - Chemin : `C:\ProgramData\Radarr\bin\Radarr.exe`
   - Répertoire de démarrage : `C:\ProgramData\Radarr\bin`
   - Arguments : `-data=C:\ProgramData\Radarr-4K`
   - Onglet Actions de sortie
     - Redémarrer : Redémarrer l'application
     - Délai : 120000 ms
       (2 minutes, peut être plus long si la mise à jour ne parvient pas à se terminer à temps)

> Notez que **Arguments** pointe vers le *nouveau* dossier créé à l'étape 1.
Ceci est crucial, car il permet de conserver tous les fichiers de données des deux instances dans des emplacements distincts. {.is-warning}

1. Cliquez sur *Installer le service*. La fenêtre devrait se fermer et le service sera désormais disponible pour être exécuté.
1. Poursuivez avec [Configuration de Radarr-4K](#windows-multi-config-second)

### Application de la barre d'état système (Windows)

#### Prérequis (Application de la barre d'état système)

- [Vous devez déjà avoir installé Radarr](#windows)
- Le raccourci de Radarr doit être configuré avec un argument `/data=` dans le champ 'cible' pour permettre plusieurs instances
- Accédez au dossier de démarrage pour l'utilisateur actuel `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` et modifiez le raccourci existant si nécessaire.

#### Création de l'application de la barre d'état système Radarr-4K

- Créez un nouveau dossier pour les fichiers de configuration de Radarr-4K. La plupart des utilisateurs utilisent un emplacement similaire tel que `C:\ProgramData\Radarr-4K`.
- Faites un clic droit et créez un nouveau raccourci
- Chemin : `C:\ProgramData\Radarr\bin\Radarr.exe /data=C:\ProgramData\Radarr-4K`
- Donnez un nom unique au raccourci, tel que `Radarr-4K`, et terminez l'assistant.
- Double-cliquez sur le nouveau raccourci pour l'exécuter et le tester.
- Poursuivez avec [Configuration de Radarr-4K](#windows-multi-config-second)

### Configuration de Radarr-4K {#windows-multi-config-second}

- Peu importe que vous ayez utilisé la méthode du service ou de l'application de la barre d'état système : arrêtez les deux services et les deux applications.
- Démarrez Radarr-4K (service ou application de la barre d'état système).
- Ouvrez Radarr-4K et naviguez dans l'application vers [Paramètres => Général => Hôte](/radarr/settings/#host)
- Modifiez le `Numéro de port` de `7878` à un port différent, par exemple `7879`, afin que Radarr et Radarr-4K ne se chevauchent pas.
- Vous devriez maintenant pouvoir démarrer les deux applications.
- Poursuivez avec [Gestion des mises à jour](#dealing-with-updates)

### Gestion des mises à jour

> - Désactivez les mises à jour automatiques sur l'une de vos instances
  - Dans config.xml, changez la branche de mise à jour en `<Branch>nonexistent</Branch>`
- Si une instance de Radarr est mise à jour, les deux instances s'arrêteront et seule l'instance mise à jour redémarrera. Pour résoudre ce problème, vous devrez démarrer manuellement l'autre instance, ou vous voudrez peut-être envisager d'utiliser le script PowerShell ci-dessous pour résoudre le problème.

> Configurer correctement l'[action de sortie NSSM](#creating-radarr-4k-service) devrait permettre à Radarr de mettre à jour et de redémarrer plusieurs instances sans scripts supplémentaires.
Si le délai de redémarrage n'est pas configuré par défaut, l'instance redémarrera immédiatement.
Cela peut empêcher l'application des mises à jour et peut entraîner l'erreur suivante : `Radarr was restarted prematurely by external process.` {.is-info}

#### Script PowerShell de vérification des ports et de redémarrage sous Windows

- Lorsque vous utilisez deux instances de Radarr et que l'une d'entre elles est en cours de mise à jour, toutes les instances seront arrêtées. Seule celle qui est en cours de mise à jour reviendra en ligne.
- Le script PowerShell ci-dessous doit être configuré en tant que tâche planifiée.
- Il vérifie les ports et, s'il en trouve un qui n'est pas en ligne, il (re)démarre la tâche planifiée pour lancer Radarr.

1. Créez un nouveau fichier et nommez-le RadarrInstancesChecker.ps1 avec le code ci-dessous.
1. Modifiez le script avec vos noms de service, IP et ports réels. *Si vous utilisez le mode de la barre d'état système, vous devez créer des tâches planifiées pour démarrer chaque instance de Radarr et utiliser ces noms de tâche dans le script ci-dessous.*
1. [Créez une tâche planifiée](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) pour exécuter le script selon un calendrier répétitif.

- Options de sécurité : Activer `Exécuter avec les privilèges les plus élevés`
  - Sinon, le script ne pourra pas manipuler les services
- Déclencheur : `Au démarrage`
- Répéter la tâche toutes les : `5` ou `10` minutes
- Action : `Démarrer un programme`
- Programme/script : `powershell`
- Argument : `-File D:\RadarrInstancesChecker.ps1`
  - Assurez-vous d'utiliser le chemin complet vers l'emplacement de votre script

```powershell
################################################################################################
### RadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Garde plusieurs instances de Radarr en ligne en vérifiant le port                          ###
### Veuillez utiliser le Discord ou Reddit de Radarr pour obtenir de l'aide !                  ###
### https://wiki.servarr.com/radarr/installation#windows-multi                               ###
################################################################################################
### Version : 1.1                                                                            ###
### Mis à jour : 2020-10-22                                                                  ###
### Auteur : reloxx13                                                                        ###
################################################################################################



### CONFIGUREZ VOTRE SCRIPT ICI ###
# Définissez correctement votre adresse IP et votre port d'hôte !

# (string) Le type de démarrage de Radarr
# "Service" (par défaut) Le processus de service est utilisé
# "ScheduledTask" Le planificateur de tâches est utilisé
$startType = 'Service'

# (bool) Écrit le journal dans C:\Users\VOTRENOMDUTILISATEUR\log.txt lorsqu'il est activé
# $false (par défaut)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instance 1
        Name = 'Radarr-V3'; # (string) Nom du service ou de la tâche (par défaut : Radarr-V3)
        IP   = '192.168.178.12'; # (string) IP du serveur où Radarr s'exécute (par défaut : 192.168.178.12)
        Port = '7873'; # (string) Port du serveur où Radarr s'exécute (par défaut : 7873)
    }
    [pscustomobject]@{   # Instance 2
        Name = 'Radarr-4K'; # (string) Nom du service ou de la tâche (par défaut : Radarr-4K)
        IP   = '192.168.178.12'; # (string) IP du serveur où Radarr s'exécute (par défaut : 192.168.178.12)
        Port = '7874'; # (string) Port du serveur où Radarr s'exécute (par défaut : 7874)
    }
    # Si nécessaire, vous pouvez ajouter d'autres instances ici... en décommentant les lignes ci-dessous
    # [pscustomobject]@{   # Instance 3
    # Name='Radarr-3D';    # (string) Nom du service ou de la tâche (par défaut : Radarr-3D)
    # IP='192.168.178.12'; # (string) IP du serveur où Radarr s'exécute (par défaut : 192.168.178.12)
    # Port='7875';         # (string) Port du serveur où Radarr s'exécute (par défaut : 7875)
    # }
)


### NE CHANGEZ RIEN CI-DESSOUS ###


###
# Cette fonction écrira dans un fichier journal ou dans la sortie de la console
###
function Write-Log
{
    # Écrira dans C:\Users\VOTRENOMDUTILISATEUR\log.txt
    
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

- [Utilisateurs de Swizzin](https://github.com/ComputerByte/radarr4k)
- Utilisateurs non-Swizzin
  - Assurez-vous que votre première instance a l'argument `-data=` passé.
  - Arrêtez temporairement votre première instance afin de pouvoir modifier le port de la deuxième instance `systemctl stop radarr`
  - Désactivez les mises à jour automatiques sur l'une de vos instances de Radarr

> Voici un exemple de script pour créer une instance Radarr4K. Le script de création systemd ci-dessous utilisera un répertoire de données `/var/lib/radarr4k/`. Assurez-vous que le répertoire existe ou modifiez-le si nécessaire.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/radarr4k.service > /dev/null
[Unit]
Description=Radarr4k Daemon
After=syslog.target network.target
[Service]
User=radarr
Group=media
Type=simple

ExecStart=/opt/Radarr/Radarr -nobrowser -data=/var/lib/radarr4k/
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

- Activer le service Radarr4k :

```shell
sudo systemctl enable --now -q radarr4k
```

## Instances multiples Docker

{#docker-multi}

- Il suffit de lancer un deuxième conteneur Docker avec un nom différent, en veillant à respecter les exigences mentionnées ci-dessus.