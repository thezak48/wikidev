# \*Arr 설치 스크립트

이것은 리눅스 운영 체제에서 Lidarr/Prowlarr/Radarr/Readarr/Whisparr을(를) 설치하기 위한 커뮤니티에서 만들어진 커뮤니티 지원 **비공식** 스크립트입니다. 일반적으로 Debian 및 Ubuntu 또는 유사한 배포판을 대상으로 합니다.

> 이 스크립트는 선택한 애플리케이션을 /opt에 설치합니다. 설정한 사용자와 그룹으로 애플리케이션을 실행합니다.
> Lidarr/Radarr/Readarr/Whisparr의 경우, 다운로드 클라이언트와 미디어 서버가 실행되는 공통 그룹을 사용하여 소유권과 권한이 올바르게 설정되고 모든 파일에 액세스할 수 있도록 해야 합니다.
{.is-info}

다음과 같은 권한 관련 일반적인 실수에 주의하세요.

> Lidarr/Radarr/Readarr/Whisparr은 다운로드 클라이언트의 다운로드 디렉토리와 루트(라이브러리 또는 미디어) 폴더에 대한 읽기 및 쓰기 액세스 권한이 필요합니다.
> 이상적으로 각 앱은 고유한 사용자로 실행되며, 권한이 `775` 및 `664`인 `media` 그룹을 사용하여 다운로드 클라이언트와 미디어 서버가 실행되는 그룹에 속해야 하며, 다운로드 클라이언트와 미디어 서버가 사용하는 경로가 해당 그룹에게 액세스(읽기/쓰기) 가능해야 합니다.
{.is-warning}

다음 사항을 유의하세요.

> 이 스크립트는 /opt에 설치된 기존 설치를 제거합니다. 다른 위치에 설치된 기존 설치는 제거하지 않습니다. 앱 내에서 백업을 사용하여 설정의 백업을 보관하는지 확인하세요(시스템 => 백업). 스크립트는 설정(애플리케이션 데이터)를 삭제하지 않지만, 안전을 위해 백업을 만들어 두세요.
{.is-danger}

- (선택 사항) [정적 IP 주소를 설정](https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/)했는지 확인하세요. 이렇게 하면 더 편리합니다.
- Debian (Raspbian / Raspberry Pi OS) / Ubuntu 상자에 SSH로 로그인하여 root로 전환하거나 로그인하세요.

> Putty, mRemoteNG 또는 다른 SSH 도구를 사용하여 SSH로 로그인하세요. 대부분의 도구에서 연결을 저장할 수 있습니다.{.is-info}

- SSH로 로그인한 후 아래 명령을 입력하여 현재 디렉토리에 설치 스크립트를 생성하세요.

```bash
nano ArrInstall.sh
```

- 스크립트의 오른쪽 상단에서 복사하여 SSH 콘솔에 붙여넣으세요. 필요한 경우 변수를 검토하고 업데이트하세요.
  - Windows 또는 MacOS (OSX)와 같은 GUI OS의 경우, 붙여넣기는 SSH 클라이언트에서 '오른쪽 클릭'만으로도 가능할 수 있습니다.

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

echo "Running \*Arr Install Script - Version [$scriptversion] as of [$scriptdate]"

# Am I root?, need root!

if [ "$EUID" -ne 0 ]; then
    echo "Please run as root."
    exit
fi

echo "Select the application to install: "

select app in lidarr prowlarr radarr readarr whisparr quit; do

    case $app in
    lidarr)
        app_port="8686"                                          # Default App Port; Modify config.xml after install if needed
        app_prereq="curl sqlite3 libchromaprint-tools mediainfo" # Required packages
        app_umask="0002"                                         # UMask the Service will run as
        branch="master"                                          # {Update me if needed} branch to install
        break
        ;;
    prowlarr)
        app_port="9696"           # Default App Port; Modify config.xml after install if needed
        app_prereq="curl sqlite3" # Required packages
        app_umask="0002"          # UMask the Service will run as
        branch="master"          # {Update me if needed} branch to install
        break
        ;;
    radarr)
        app_port="7878"           # Default App Port; Modify config.xml after install if needed
        app_prereq="curl sqlite3" # Required packages
        app_umask="0002"          # UMask the Service will run as
        branch="master"           # {Update me if needed} branch to install
        break
        ;;
    readarr)
        app_port="8787"           # Default App Port; Modify config.xml after install if needed
        app_prereq="curl sqlite3" # Required packages
        app_umask="0002"          # UMask the Service will run as
        branch="develop"          # {Update me if needed} branch to install
        break
        ;;
    whisparr)
        app_port="6969"           # Default App Port; Modify config.xml after install if needed
        app_prereq="curl sqlite3" # Required packages
        app_umask="0002"          # UMask the Service will run as
        branch="nightly"          # {Update me if needed} branch to install
        break
        ;;
    quit)
        exit 0
        ;;
    *)
        echo "Invalid option $REPLY"
        ;;
    esac
done

# Constants
### Update these variables as required for your specific instance
installdir="/opt"              # {Update me if needed} Install Location
bindir="${installdir}/${app^}" # Full Path to Install Location
datadir="/var/lib/$app/"       # {Update me if needed} AppData directory to use
app_bin=${app^}                # Binary Name of the app

if [[ $app != 'prowlarr' ]]; then
    echo "It is critical that the user and group you select to run ${app^} as will have READ and WRITE access to your Media Library and Download Client Completed Folders"
fi

# Prompt User
read -r -p "What user should ${app^} run as? (Default: $app): " app_uid
app_uid=$(echo "$app_uid" | tr -d ' ')
app_uid=${app_uid:-$app}
# Prompt Group
read -r -p "What group should ${app^} run as? (Default: media): " app_guid
app_guid=$(echo "$app_guid" | tr -d ' ')
app_guid=${app_guid:-media}

echo "${app^} selected"
echo "This will install [${app^}] to [$bindir] and use [$datadir] for the AppData Directory"
if [[ $app == 'prowlarr' ]]; then
    echo "${app^} will run as the user [$app_uid] and group [$app_guid]."
else
    echo "${app^} will run as the user [$app_uid] and group [$app_guid]. By continuing, you've confirmed that that user and group will have READ and WRITE access to your Media Library and Download Client Completed Download directories"
fi
echo "Continue with the installation [Yes/No]?"
select yn in "Yes" "No"; do
    case $yn in
    Yes) break ;;
    No) exit 0 ;;
    esac
done

# Create User / Group as needed
if [ "$app_guid" != "$app_uid" ]; then
    if ! getent group "$app_guid" >/dev/null; then
        groupadd "$app_guid"
    fi
fi
if ! getent passwd "$app_uid" >/dev/null; then
    adduser --system --no-create-home --ingroup "$app_guid" "$app_uid"
    echo "Created and added User [$app_uid] to Group [$app_guid]"
fi
if ! getent group "$app_guid" | grep -qw "$app_uid"; then
    echo "User [$app_uid] did not exist in Group [$app_guid]"
    usermod -a -G "$app_guid" "$app_uid"
    echo "Added User [$app_uid] to Group [$app_guid]"
fi

# Stop the App if running
if service --status-all | grep -Fq "$app"; then
    systemctl stop "$app"
    systemctl disable "$app".service
    echo "Stopped existing $app"
fi

# Create Appdata Directory

# AppData
mkdir -p "$datadir"
chown -R "$app_uid":"$app_guid" "$datadir"
chmod 775 "$datadir"
echo "Directories created"
# Download and install the App

# prerequisite packages
echo ""
echo "Installing pre-requisite Packages"
# shellcheck disable=SC2086
apt update && apt install $app_prereq
echo ""
ARCH=$(dpkg --print-architecture)
# get arch
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo "Arch not supported"
    exit 1
    ;;
esac
echo ""
echo "Removing previous tarballs"
# -f to Force so we fail if it doesnt exist
rm -f "${app^}".*.tar.gz
echo ""
echo "Downloading..."
wget --content-disposition "$DLURL"
tar -xvzf "${app^}".*.tar.gz
echo ""
echo "Installation files downloaded and extracted"

# remove existing installs
echo "Removing existing installation"
# If you happen to run this script in the installdir the line below will delete the extracted files and cause the mv some lines below to fail.
rm -rf "$bindir"
echo "Installing..."
mv "${app^}" $installdir
chown "$app_uid":"$app_guid" -R "$bindir"
chmod 775 "$bindir"
rm -rf "${app^}.*.tar.gz"
# Ensure we check for an update in case user installs older version or different branch
touch "$datadir"/update_required
chown "$app_uid":"$app_guid" "$datadir"/update_required
echo "App Installed"
# Configure Autostart

# Remove any previous app .service
echo "Removing old service file"
rm -rf /etc/systemd/system/"$app".service

# Create app .service with correct user startup
echo "Creating service file"
cat <<EOF | tee /etc/systemd/system/"$app".service >/dev/null
[Unit]
Description=${app^} Daemon
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

# Start the App
echo "Service file created. Attempting to start the app"
systemctl -q daemon-reload
systemctl enable --now -q "$app"

# Finish Update/Installation
host=$(hostname -I)
ip_local=$(grep -oP '^\S*' <<<"$host")
echo ""
echo "Install complete"
sleep 10
STATUS="$(systemctl is-active "$app")"
if [ "${STATUS}" = "active" ]; then
    echo "Browse to http://$ip_local:$app_port for the ${app^} GUI"
else
    echo "${app^} failed to start"
fi

# Exit
exit 0

```

- <kbd>Ctrl</kbd>+<kbd>O</kbd> (저장)을 누르고 <kbd>Enter</kbd>를 누릅니다.
- <kbd>Ctrl</kbd>+<kbd>X</kbd> (종료)를 누르고 <kbd>Enter</kbd>를 누릅니다.
- 그런 다음 콘솔에서 다음을 입력하고 프롬프트에 따릅니다.

```shell
sudo bash ArrInstall.sh
```