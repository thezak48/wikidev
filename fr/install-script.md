---
title: Script d'installation *Arr
description: Script d'installation commun pour la suite d'applications *Arr
published: true
date: 2023-07-14T12:19:34.383Z
tags: 
editor: markdown
dateCreated: 2022-02-03T15:12:29.483Z
---

# Script d'installation *Arr

Il s'agit d'un script **non officiel** créé et pris en charge par la communauté pour gérer l'installation de Lidarr/Prowlarr/Radarr/Readarr/Whisparr sur un système d'exploitation Linux, généralement Debian & Ubuntu ou des distributions similaires.

> Cela installera l'application sélectionnée dans /opt. Elle sera exécutée en tant qu'utilisateur et groupe que vous configurez.
> Pour Lidarr/Radarr/Readarr/Whisparr - vous devriez utiliser un groupe commun qui est le même que celui de votre client de téléchargement et de votre serveur multimédia pour garantir la propriété et les autorisations correctes et que tous les fichiers sont accessibles.
{.is-info}

Veuillez prendre en compte l'erreur courante suivante concernant les autorisations.

> Deux choses à garder à l'esprit sont que Lidarr/Radarr/Readarr/Whisparr nécessitent un accès en lecture et en écriture au répertoire de téléchargement de votre client de téléchargement et au dossier que vous configurez comme votre dossier racine (bibliothèque ou média).
> Idéalement, chaque application s'exécute en tant qu'utilisateur et groupe distinct avec le groupe commun `media` et les autorisations `775` et `664`, ce qui correspond à un UMask de `002`.
> \* Vos clients de téléchargement et votre serveur multimédia s'exécutent en tant que membre du groupe que vous avez saisi.
> \* Les chemins utilisés par vos clients de téléchargement et votre serveur multimédia sont accessibles (lecture/écriture) par le groupe que vous avez saisi.
{.is-warning}

Veuillez prendre en compte ce qui suit :

> Cela supprimera toutes les installations existantes installées dans /opt. Cela ne désinstallera pas les installations existantes à partir d'un autre emplacement ; veuillez vous assurer de sauvegarder vos paramètres à l'aide de la fonction de sauvegarde de l'application (Système => Sauvegarde). Le script ne supprimera pas vos paramètres (données de l'application), mais soyez prudent.
{.is-danger}

- (Facultatif) Assurez-vous d'avoir [défini une adresse IP statique](https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/), cela vous facilitera la vie.
- Connectez-vous en SSH à votre boîtier Debian (Raspbian / Raspberry Pi OS) / Ubuntu et devenez ou connectez-vous en tant que root.

> Connectez-vous en SSH à l'aide de Putty, mRemoteNG ou tout autre outil SSH. Notez que la plupart des outils prennent en charge l'enregistrement de votre connexion.{.is-info}

- Une fois connecté en SSH, tapez la commande suivante pour créer le script d'installation dans votre répertoire actuel

```bash
nano ArrInstall.sh
```

- Copiez (coin supérieur droit du script) et collez dans votre console SSH. Vérifiez les variables avec les commentaires et mettez-les à jour si nécessaire.
  - Si vous êtes dans un système d'exploitation avec interface graphique tel que Windows ou MacOS (OSX) : coller peut être aussi simple que de "cliquer avec le bouton droit" dans votre client SSH.

```bash
#!/bin/bash
### Description: \*Arr .NET Debian install
### Originally written for Radarr by: DoctorArr - doctorarr@the-rowlands.co.uk on 2021-10-01 v1.0
### Version v1.1 2021-10-02 - Bakerboy448 (Made more generic and conformant)
### Version v1.1.1 2021-10-02 - DoctorArr (Spellcheck and boilerplate update)
### Version v2.0.0 2021-10-09 - Bakerboy448 (Refactored and ensured script is generic. Added more variables.)
### Version v2.0.1 2021-11-23 - brightghost (Fixed datadir step to use correct variables.)
### Version v3.0.0 2022-02-03 - Bakerboy448 (Rewrote script to prompt for user/group and made generic for all \*Arrs)
### Version v3.0.1 2022-02-05 - aeramor (typo fix line 179: 'chown "$app_uid":"$app_uid" -R "$bindir"' -> 'chown "$app_uid":"$app_guid" -R "$bindir"')
### Version v3.0.3 2022-02-06 - Bakerboy448 fixup ownership
### Version v3.0.3a Readarr to develop
### Version v3.0.4 2022-03-01 - Add sleep before checking service status
### Version v3.0.5 2022-04-03 - VP-EN (Added Whisparr)
### Version v3.0.6 2022-04-26 - Bakerboy448 - binaries to group
### Version v3.0.7 2023-01-05 - Bakerboy448 - Prowlarr to master
### Version v3.0.8 2023-04-20 - Bakerboy448 - Shellcheck fixes & remove prior tarballs
### Version v3.0.9 2023-04-28 - Bakerboy448 - fix tarball check
### Version v3.0.9a 2023-07-14 - DoctorArr - updated scriptversion and scriptdate and to see how this is going! It was still at v3.0.8.
### Additional Updates by: The \*Arr Community

### Boilerplate Warning
#THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
#EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
#MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
#NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
#LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
#OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
#WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

scriptversion="3.0.9a"
scriptdate="2023-07-14"

set -euo pipefail

echo "Exécution du script d'installation *Arr - Version [$scriptversion] du [$scriptdate]"

# Suis-je root ? J'ai besoin des droits root !

if [ "$EUID" -ne 0 ]; then
    echo "Veuillez exécuter en tant que root."
    exit
fi

echo "Sélectionnez l'application à installer : "

select app in lidarr prowlarr radarr readarr whisparr quit; do

    case $app in
    lidarr)
        app_port="8686"                                          # Port de l'application par défaut ; Modifiez config.xml après l'installation si nécessaire
        app_prereq="curl sqlite3 libchromaprint-tools mediainfo" # Paquets requis
        app_umask="0002"                                         # UMask avec lequel le service s'exécutera
        branch="master"                                          # {Mettez à jour si nécessaire} branche à installer
        break
        ;;
    prowlarr)
        app_port="9696"           # Port de l'application par défaut ; Modifiez config.xml après l'installation si nécessaire
        app_prereq="curl sqlite3" # Paquets requis
        app_umask="0002"          # UMask avec lequel le service s'exécutera
        branch="master"          # {Mettez à jour si nécessaire} branche à installer
        break
        ;;
    radarr)
        app_port="7878"           # Port de l'application par défaut ; Modifiez config.xml après l'installation si nécessaire
        app_prereq="curl sqlite3" # Paquets requis
        app_umask="0002"          # UMask avec lequel le service s'exécutera
        branch="master"           # {Mettez à jour si nécessaire} branche à installer
        break
        ;;
    readarr)
        app_port="8787"           # Port de l'application par défaut ; Modifiez config.xml après l'installation si nécessaire
        app_prereq="curl sqlite3" # Paquets requis
        app_umask="0002"          # UMask avec lequel le service s'exécutera
        branch="develop"          # {Mettez à jour si nécessaire} branche à installer
        break
        ;;
    whisparr)
        app_port="6969"           # Port de l'application par défaut ; Modifiez config.xml après l'installation si nécessaire
        app_prereq="curl sqlite3" # Paquets requis
        app_umask="0002"          # UMask avec lequel le service s'exécutera
        branch="nightly"          # {Mettez à jour si nécessaire} branche à installer
        break
        ;;
    quit)
        exit 0
        ;;
    *)
        echo "Option invalide $REPLY"
        ;;
    esac
done

# Constantes
### Mettez à jour ces variables selon vos besoins spécifiques
installdir="/opt"              # {Mettez à jour si nécessaire} Emplacement de l'installation
bindir="${installdir}/${app^}" # Chemin complet vers l'emplacement de l'installation
datadir="/var/lib/$app/"       # {Mettez à jour si nécessaire} Répertoire des données de l'application à utiliser
app_bin=${app^}                # Nom binaire de l'application

if [[ $app != 'prowlarr' ]]; then
    echo "Il est essentiel que l'utilisateur et le groupe que vous sélectionnez pour exécuter ${app^} aient un accès en lecture et en écriture à votre bibliothèque multimédia et aux dossiers de téléchargement terminés du client de téléchargement."
fi

# Demander à l'utilisateur
read -r -p "Avec quel utilisateur ${app^} doit-il s'exécuter ? (Par défaut : $app) : " app_uid
app_uid=$(echo "$app_uid" | tr -d ' ')
app_uid=${app_uid:-$app}
# Demander le groupe
read -r -p "Avec quel groupe ${app^} doit-il s'exécuter ? (Par défaut : media) : " app_guid
app_guid=$(echo "$app_guid" | tr -d ' ')
app_guid=${app_guid:-media}

echo "${app^} sélectionné"
echo "Cela installera [${app^}] dans [$bindir] et utilisera [$datadir] pour le répertoire des données de l'application"
if [[ $app == 'prowlarr' ]]; then
    echo "${app^} s'exécutera avec l'utilisateur [$app_uid] et le groupe [$app_guid]."
else
    echo "${app^} s'exécutera avec l'utilisateur [$app_uid] et le groupe [$app_guid]. En continuant, vous confirmez que cet utilisateur et ce groupe auront un accès en lecture et en écriture à votre bibliothèque multimédia et à vos dossiers de téléchargement terminés du client de téléchargement."
fi
echo "Continuer l'installation [Oui/Non] ?"
select yn in "Oui" "Non"; do
    case $yn in
    Oui) break ;;
    Non) exit 0 ;;
    esac
done

# Créer l'utilisateur / le groupe si nécessaire
if [ "$app_guid" != "$app_uid" ]; then
    if ! getent group "$app_guid" >/dev/null; then
        groupadd "$app_guid"
    fi
fi
if ! getent passwd "$app_uid" >/dev/null; then
    adduser --system --no-create-home --ingroup "$app_guid" "$app_uid"
    echo "Utilisateur [$app_uid] créé et ajouté au groupe [$app_guid]"
fi
if ! getent group "$app_guid" | grep -qw "$app_uid"; then
    echo "L'utilisateur [$app_uid] n'existait pas dans le groupe [$app_guid]"
    usermod -a -G "$app_guid" "$app_uid"
    echo "Utilisateur [$app_uid] ajouté au groupe [$app_guid]"
fi

# Arrêter l'application si elle est en cours d'exécution
if service --status-all | grep -Fq "$app"; then
    systemctl stop "$app"
    systemctl disable "$app".service
    echo "Arrêt de l'ancienne $app"
fi

# Créer le répertoire des données de l'application

# Données de l'application
mkdir -p "$datadir"
chown -R "$app_uid":"$app_guid" "$datadir"
chmod 775 "$datadir"
echo "Répertoires créés"
# Télécharger et installer l'application

# Paquets prérequis
echo ""
echo "Installation des paquets prérequis"
# shellcheck disable=SC2086
apt update && apt install $app_prereq
echo ""
ARCH=$(dpkg --print-architecture)
# obtenir l'architecture
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo "Architecture non prise en charge"
    exit 1
    ;;
esac
echo ""
echo "Suppression des anciens fichiers tar"
# -f pour forcer l'échec si le fichier n'existe pas
rm -f "${app^}".*.tar.gz
echo ""
echo "Téléchargement..."
wget --content-disposition "$DLURL"
tar -xvzf "${app^}".*.tar.gz
echo ""
echo "Fichiers d'installation téléchargés et extraits"

# Supprimer les installations existantes
echo "Suppression de l'installation existante"
# Si vous exécutez ce script dans le répertoire d'installation, la ligne ci-dessous supprimera les fichiers extraits et provoquera l'échec de la commande mv quelques lignes plus bas.
rm -rf "$bindir"
echo "Installation..."
mv "${app^}" $installdir
chown "$app_uid":"$app_guid" -R "$bindir"
chmod 775 "$bindir"
rm -rf "${app^}.*.tar.gz"
# Assurons-nous de vérifier les mises à jour au cas où l'utilisateur installe une version plus ancienne ou une branche différente
touch "$datadir"/update_required
chown "$app_uid":"$app_guid" "$datadir"/update_required
echo "Application installée"
# Configurer le démarrage automatique

# Supprimer tout fichier .service précédent de l'application
echo "Suppression de l'ancien fichier de service"
rm -rf /etc/systemd/system/"$app".service

# Créer le fichier .service de l'application avec le démarrage utilisateur correct
echo "Création du fichier de service"
cat <<EOF | tee /etc/systemd/system/"$app".service >/dev/null
[Unit]
Description=Démon ${app^}
After=syslog.target network.target
[Service]
User=$app_uid
Group=$app_guid
UMask=$app_umask
Type=simple
ExecStart=$bindir/$app_bin -nobrowser -data=$datadir
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF

# Démarrer l'application
echo "Fichier de service créé. Tentative de démarrage de l'application"
systemctl -q daemon-reload
systemctl enable --now -q "$app"

# Fin de la mise à jour / de l'installation
host=$(hostname -I)
ip_local=$(grep -oP '^\S*' <<<"$host")
echo ""
echo "Installation terminée"
sleep 10
STATUS="$(systemctl is-active "$app")"
if [ "${STATUS}" = "active" ]; then
    echo "Accédez à http://$ip_local:$app_port pour l'interface graphique de ${app^}"
else
    echo "Échec du démarrage de ${app^}"
fi

# Sortie
exit 0

```

- Appuyez sur <kbd>Ctrl</kbd>+<kbd>O</kbd> (enregistrer) puis sur <kbd>Entrée</kbd>
- Appuyez sur <kbd>Ctrl</kbd>+<kbd>X</kbd> (quitter) puis sur <kbd>Entrée</kbd>
- Ensuite, dans votre console, tapez et suivez les invites

```shell
sudo bash ArrInstall.sh
```