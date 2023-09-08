# Instances multiples

Il est possible d'exécuter plusieurs instances de Readarr. Cela est généralement fait lorsque l'on souhaite avoir une copie audio et une copie ebook d'un livre.
Notez que vous pouvez configurer Readarr pour utiliser un deuxième Readarr en tant que liste. Cela est utile si vous souhaitez les maintenir tous les deux synchronisés.

- [Instances multiples sous Windows](#windows-multi)
- [Instances multiples sous Linux](#linux-multi)
- [Instances multiples sous MacOS](#macos-multi)
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

Ce guide vous montrera comment exécuter plusieurs instances de Readarr sous Windows en utilisant une seule installation de base. Ce guide a été réalisé avec Windows 10 ; si vous utilisez une version antérieure de Windows (7, 8, etc.), vous devrez peut-être ajuster certaines choses. Ce guide suppose également que vous avez installé Readarr dans le répertoire par défaut et que votre deuxième instance de Readarr s'appellera Readarr-audiobooks. N'hésitez pas à modifier les éléments pour correspondre à vos propres installations.

### Service (Windows)

#### Prérequis (Service)

- [Vous devez déjà avoir installé Readarr](#windows)
- Vous devez avoir [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installé. Pour l'installer, téléchargez la dernière version (2.24 au moment de la rédaction) et copiez le fichier nssm.exe 32 bits ou 64 bits dans C:/windows/system32.
  - Si vous n'êtes pas sûr d'avoir un système 32 bits ou 64 bits, vérifiez Paramètres => Système => À propos => Type de système.

#### Configuration du service Readarr

1. Ouvrez une fenêtre d'invite de commandes en tant qu'administrateur. (Pour exécuter en tant qu'administrateur, faites un clic droit sur l'icône de l'invite de commandes et choisissez "Exécuter en tant qu'administrateur".)
1. Si Readarr est en cours d'exécution, arrêtez le service en exécutant `nssm stop Readarr` dans l'invite de commandes.
1. Maintenant, nous devons modifier l'instance existante de Readarr pour qu'elle pointe explicitement vers son répertoire de données. La commande par défaut est la suivante :
   `sc config Readarr binpath= "C:\ProgramData\Readarr\bin\Readarr.exe -data=C:\ProgramData\Readarr"`

Cette commande indique à l'instance originale de Readarr d'utiliser explicitement `C:\ProgramData\Readarr` comme répertoire de données. Si vous n'avez pas utilisé l'installation par défaut de Readarr, ou si votre dossier de données se trouve ailleurs, vous devrez peut-être modifier vos chemins ici.

#### Création du service Readarr-audiobooks

1. Créez un nouveau dossier où vous souhaitez que Readarr-audiobooks soit installé. La plupart utilisent un emplacement similaire tel que `C:\ProgramData\Readarr-audiobooks`.
1. De retour dans l'invite de commandes, créez le nouveau service Readarr-audiobooks en utilisant `nssm install Readarr-audiobooks`. Une fenêtre contextuelle s'ouvrira où vous pourrez saisir les paramètres de la nouvelle instance. Pour cet exemple, nous utiliserons les paramètres suivants :
   - Chemin : `C:\ProgramData\Readarr\bin\Readarr.exe`
   - Répertoire de démarrage : `C:\ProgramData\Readarr\bin`
   - Arguments : `-data=C:\ProgramData\Readarr-audiobooks`

> Notez que **Arguments** pointe vers le *nouveau* dossier créé à l'étape 1.
Ceci est crucial, car il permet de conserver tous les fichiers de données des deux instances dans des emplacements distincts. {.is-warning}

1. Cliquez sur *Installer le service*. La fenêtre devrait se fermer et le service sera désormais disponible pour être exécuté.
1. Poursuivez avec [la configuration de Readarr-audiobooks](#windows-multi-config-second)

### Application de la barre d'état système (Windows)

#### Prérequis (Application de la barre d'état système)

- [Vous devez déjà avoir installé Readarr](#windows)
- Readarr doit être configuré avec un argument `/data=` pour permettre plusieurs instances
- Accédez au dossier de démarrage pour l'utilisateur actuel `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` et modifiez le raccourci existant si nécessaire.

#### Création de l'application Readarr-audiobooks dans la barre d'état système

- Faites un clic droit et créez un nouveau raccourci
- Chemin : `C:\ProgramData\Readarr\bin\Readarr.exe /data=C:\ProgramData\Readarr-audiobooks`
- Donnez un nom unique au raccourci, tel que `Readarr-audiobooks`, et terminez l'assistant.
- Double-cliquez sur le nouveau raccourci pour l'exécuter et le tester.
- Poursuivez avec [la configuration de Readarr-audiobooks](#windows-multi-config-second)

### Configuration de Readarr-audiobooks {#windows-multi-config-second}

- Peu importe que vous ayez utilisé la méthode du service ou l'application de la barre d'état système : arrêtez les deux services et les deux applications.
- Démarrez Readarr-audiobooks (service ou application de la barre d'état système).
- Ouvrez Readarr-audiobooks et naviguez dans l'application vers [Paramètres => Général => Hôte](/readarr/settings/#host)
- Modifiez le `Numéro de port` de `8787` à un port différent, par exemple `8879`, afin que Readarr et Readarr-audiobooks ne se chevauchent pas.
- Vous devriez maintenant pouvoir démarrer les deux applications.
- Poursuivez avec [la gestion des mises à jour](#dealing-with-updates)

### Gestion des mises à jour

- Désactivez les mises à jour automatiques sur l'une de vos instances.
- Si une instance de Readarr est mise à jour, les deux instances s'arrêteront et seule l'instance mise à jour redémarrera. Pour résoudre ce problème, vous devrez démarrer manuellement l'autre instance, ou vous voudrez peut-être envisager d'utiliser le script PowerShell ci-dessous pour résoudre le problème.

#### Script PowerShell de vérification et de redémarrage des ports Windows

{#win-portchecker}

- Lorsque vous utilisez deux instances de Readarr et que l'une d'entre elles est mise à jour, cela tuera toutes les instances. Seule celle qui est en cours de mise à jour reviendra en ligne.
- Le script PowerShell ci-dessous doit être configuré en tant que tâche planifiée.
- Il vérifie les ports et, s'il en trouve un qui n'est pas en ligne, il (re)démarre la tâche planifiée pour lancer Readarr.

1. Créez un nouveau fichier et nommez-le ReadarrInstancesChecker.ps1 avec le code ci-dessous.
1. Modifiez le script avec vos noms de service, IP et ports réels.
1. [Créez une tâche planifiée](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) pour exécuter le script selon un calendrier répétitif.

- Options de sécurité : Activer `Exécuter avec les privilèges les plus élevés`
  - Sinon, le script ne pourra pas manipuler les services
- Déclencheur : `Au démarrage`
- Répéter la tâche toutes les : `5` ou `10` minutes
- Action : `Démarrer un programme`
- Programme/script : `powershell`
- Argument : `-File D:\ReadarrInstancesChecker.ps1`
  - Assurez-vous d'utiliser le chemin complet vers l'emplacement de votre script

```powershell
################################################################################################
### ReadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Garde plusieurs instances de Readarr actives en vérifiant le port                          ###
### Veuillez utiliser le Discord ou Reddit de Readarr pour obtenir de l'aide !                  ###
### https://wiki.servarr.com/readarr/installation#windows-multi                               ###
################################################################################################
### Version : 1.1                                                                             ###
### Mis à jour : 2020-10-22                                                                   ###
### Auteur : reloxx13                                                                         ###
################################################################################################



### CONFIGUREZ VOTRE CONFIGURATION ICI ###
# Définissez correctement votre adresse IP et votre port d'hôte et utilisez vos noms de service ou de tâche planifiée !

# (chaîne) Le type de démarrage de Readarr
# "Service" (par défaut) : le processus de service est utilisé
# "ScheduledTask" : le planificateur de tâches est utilisé
$startType = 'Service'

# (bool) Écrit le journal dans C:\Users\VOTRENOMDUTILISATEUR\log.txt lorsqu'il est activé
# $false (par défaut)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instance 1
        Name = 'Readarr'; # (chaîne) Nom du service ou de la tâche (par défaut : Readarr)
        IP   = '192.168.178.12'; # (chaîne) IP du serveur où Readarr s'exécute (par défaut : 192.168.178.12)
        Port = '8873'; # (chaîne) Port du serveur où Readarr s'exécute (par défaut : 8873)
    }
    [pscustomobject]@{   # Instance 2
        Name = 'Readarr-audiobooks'; # (chaîne) Nom du service ou de la tâche (par défaut : Readarr-audiobooks)
        IP   = '192.168.178.12'; # (chaîne) IP du serveur où Readarr s'exécute (par défaut : 192.168.178.12)
        Port = '8874'; # (chaîne) Port du serveur où Readarr s'exécute (par défaut : 8874)
    }
    # Si nécessaire, vous pouvez ajouter plus d'instances ici... en décommentant les lignes ci-dessous
    # [pscustomobject]@{   # Instance 3
    # Name='Readarr-3D';    # (chaîne) Nom du service ou de la tâche (par défaut : Readarr-3D)
    # IP='192.168.178.12'; # (chaîne) IP du serveur où Readarr s'exécute (par défaut : 192.168.178.12)
    # Port='8875';         # (chaîne) Port du serveur où Readarr s'exécute (par défaut : 7875)
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

- [Utilisateurs de Swizzin](https://github.com/ComputerByte/readarr-audiobooks)
- Utilisateurs non-Swizzin
  - Assurez-vous que votre première instance a l'argument `-data=` passé.
  - Arrêtez temporairement votre première instance pour pouvoir modifier le port de la deuxième instance `systemctl stop readarr`
  - Désactivez les mises à jour automatiques sur l'une de vos instances de Readarr

> Voici un exemple de script pour créer une instance Readarr-audiobooks. Le script de création systemd ci-dessous utilisera un répertoire de données `/var/lib/readarr-audiobooks/`. Assurez-vous que le répertoire existe ou modifiez-le si nécessaire. {.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr-audiobooks.service > /dev/null
[Unit]
Description=Démon Readarr-audiobooks
After=syslog.target network.target
[Service]
User=readarr
Group=media
Type=simple

ExecStart=/opt/Readarr/Readarr -nobrowser -data=/var/lib/Readarr-audiobooks/
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

- Activez le service Readarr-audiobooks :

```shell
sudo systemctl enable --now -q readarr-audiobooks
```

## Instances multiples sous MacOS

{#macos-multi}

Ce guide a été réalisé et testé avec macOS 13 (Ventura), mais devrait fonctionner avec n'importe quelle version prise en charge par Readarr.

### Prérequis
- L'application Readarr doit être installée dans le dossier `/Applications`
- Si Readarr a déjà été utilisé auparavant, toutes les données seront perdues. Déplacez `~/.config/Readarr` vers `~/.config/readarr-books` ou `~/.config/readarr-audiobooks` pour conserver les données.

### Création d'applications (démarrage facile de Readarr)
Vous allez créer deux nouvelles applications : "Readarr Books" et "Readarr Audiobooks".

- Ouvrez l'application Automator
- Sélectionnez `Nouveau document`, puis `Application`
- Utilisez la zone de recherche en haut à gauche pour rechercher `Exécuter un script shell`, puis double-cliquez dessus
- Dans la fenêtre qui s'ouvre, collez ce qui suit :

```shell
# Readarr Books
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-books
```



- Enregistrez l'application sous le nom `Readarr Books`
- Allez dans `Fichier` > `Dupliquer` dans la barre de menu
- Remplacez le contenu du script par ce qui suit :

```shell
# Readarr Audiobooks
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-audiobooks
```

- Enregistrez la nouvelle application sous le nom `Readarr Audiobooks`
- Affichez les applications dans Finder, modifiez éventuellement leurs icônes à votre goût (via la fenêtre `Obtenir des informations`).

### Configuration des instances
Maintenant, vous allez définir les ports et les noms pour chaque instance.

- Choisissez un numéro de port pour chaque instance. Par exemple, le port par défaut `8787` pour les livres électroniques et `8789` pour les livres audio.
- Si l'une des instances utilise le numéro de port par défaut, lancez l'autre en premier. Sinon, lancez l'une d'entre elles.
- Allez dans `Paramètres` > `Général` dans Readarr, et définissez le port correct.

> Facultatif : Activez les options avancées et définissez le `Nom de l'instance` selon vos préférences.
{.is-success}

- Lancez l'autre instance et faites de même.

### Mises à jour
Lorsque vous mettez à jour une instance, le programme de mise à jour arrête les deux instances et ne redémarre que celle que vous avez mise à jour. Pour contourner ce problème, une tâche périodique de vérification de port sera créée (adaptée mais légèrement modifiée à partir du [guide Windows](#win-portchecker)).

- Désactivez les mises à jour automatiques sur l'une des instances et assurez-vous de ne jamais la mettre à jour.
- Créez un nouveau fichier à un endroit que vous vous souviendrez, et nommez-le `readarrportchecker.zsh`.
- Ajoutez le contenu suivant :

```shell
#!/bin/zsh

# Nom de l'application de la première instance
name0="Readarr Books"
# Numéro de port de la première instance
port0=8787

# Nom de l'application de la deuxième instance
name1="Readarr Audiobooks"
# Numéro de port de la deuxième instance
port1=8789

# Journalisation
LOGFILE="$HOME/.local/state/readarr.log"
test -d "$HOME/.local/state" || mkdir -p "$HOME/.local/state"

function checkport {
    lsof -i ":${1}" &>/dev/null
}

# Si une instance est en cours d'exécution, les deux doivent l'être
if checkport "${port0}" && ! checkport "${port1}"; then
		open -a "${name1}"
    echo "Opened ${name1}" >> "$LOGFILE"
elif checkport "${port1}" && ! checkport "${port0}"; then
		open -a "${name0}"
    echo "Opened ${name0}" >> "$LOGFILE"
fi
```

- Rendez le script exécutable :

```shell
chmod +x readarrportchecker.zsh
```

- Planifiez l'exécution périodique du script. Créez un nouveau fichier dans `~/Library/LaunchAgents` nommé `local.readarr.portchecker.plist` :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>local.readarr.portchecker</string>
    <key>Program</key>
    <!-- Trouvez le chemin en cliquant avec le bouton droit, puis Option et copiez -->
    <string>/chemin/vers/readarrportchecker.zsh</string>
    <key>StartInterval</key>
    <!-- Intervalle périodique en secondes. 300 pour cinq minutes,
         600 pour dix minutes. -->
    <integer>300</integer>
  </dict>
</plist>
```

- Modifiez le fichier en fonction des commentaires
- Soit reconnectez-vous, soit chargez manuellement le fichier :

```shell
launchctl load ~/Library/LaunchAgents/local.readarr.portchecker.plist
```

> `TODO` : intégrez éventuellement cela dans un script personnalisé pour le processus de mise à jour, ou observez les modifications de fichiers au lieu de s'exécuter toutes les 300 secondes.
{.is-info}

## Docker : plusieurs instances

{#docker-multi}

- Lancez simplement un deuxième conteneur Docker avec un nom différent, en veillant à respecter les exigences mentionnées ci-dessus.