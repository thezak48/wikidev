# \*Arr Installatiescript

Dit is een door de community gemaakt en door de community ondersteund **onofficieel** script om de installatie van Lidarr/Prowlarr/Radarr/Readarr/Whisparr op een Linux-besturingssysteem te beheren - meestal gericht op Debian & Ubuntu of vergelijkbare distributies.

> Dit zal de geselecteerde applicatie installeren in /opt. Het zal de applicatie uitvoeren als de gebruiker en groep die u configureert.
> Voor Lidarr/Radarr/Readarr/Whisparr - moet u een gemeenschappelijke groep gebruiken die hetzelfde is als uw downloadclient en mediaserver om ervoor te zorgen dat eigendom en machtigingen kloppen en alle bestanden toegankelijk zijn.
{.is-info}

Houd rekening met de volgende veelvoorkomende fout met betrekking tot machtigingen.

> Twee dingen om in gedachten te houden zijn dat Lidarr/Radarr/Readarr/Whisparr lees- en schrijftoegang vereisen tot de downloadmap van uw downloadclient en de map die u configureert als uw hoofdmap (bibliotheek of media).
> Idealiter draait elke app als zijn eigen gebruiker en gemeenschappelijke groep `media` met machtigingen van `775` en `664`, wat een UMask is van `002`.
> \* Uw downloadclients en mediaserver draaien als en maken deel uit van de groep die u invoert
> \* Uw paden die worden gebruikt door uw downloadclients en mediaserver zijn toegankelijk (lezen/schrijven) voor de groep die u invoert
{.is-warning}

Houd rekening met het volgende:

> Dit zal alle bestaande installaties die zijn geïnstalleerd in /opt verwijderen. Het zal geen bestaande installaties verwijderen vanuit een andere locatie; zorg ervoor dat u een back-up hebt van uw instellingen met behulp van de back-upfunctie binnen de app (Systeem => Backup). Het script verwijdert uw instellingen (applicatiegegevens) niet, maar wees voorzichtig.
{.is-danger}

- (Optioneel) Zorg ervoor dat u [een statisch IP-adres hebt ingesteld](https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/), dit maakt uw leven gemakkelijker.
- SSH naar uw Debian (Raspbian / Raspberry Pi OS) / Ubuntu-box en word root of log in als root.

> SSH in met behulp van Putty, mRemoteNG of een andere SSH-tool. Merk op dat de meeste tools uw verbinding kunnen opslaan.{.is-info}

- Typ zodra u bent ingelogd via SSH het volgende om het installatiescript in uw huidige directory te maken

```bash
nano ArrInstall.sh
```

- Kopieer (rechterbovenhoek van het script) en plak in uw SSH-console. Controleer de variabelen met opmerkingen en werk ze indien nodig bij.
  - Als u zich in een GUI-besturingssysteem bevindt, zoals Windows of MacOS (OSX), kan plakken zo eenvoudig zijn als 'rechtsklikken' in uw SSH-client.

```bash
#!/bin/bash
### Beschrijving: \*Arr .NET Debian-installatie
### Oorspronkelijk geschreven voor Radarr door: DoctorArr - doctorarr@the-rowlands.co.uk op 2021-10-01 v1.0
### Versie v1.1 2021-10-02 - Bakerboy448 (Meer generiek en conform)
### Versie v1.1.1 2021-10-02 - DoctorArr (Spellingscontrole en boilerplate-update)
### Versie v2.0.0 2021-10-09 - Bakerboy448 (Herschreven en ervoor gezorgd dat het script generiek is. Meer variabelen toegevoegd.)
### Versie v2.0.1 2021-11-23 - brightghost (Stap voor datadir gefixeerd om de juiste variabelen te gebruiken.)
### Versie v3.0.0 2022-02-03 - Bakerboy448 (Script herschreven om te vragen naar gebruiker/groep en generiek te maken voor alle \*Arrs)
### Versie v3.0.1 2022-02-05 - aeramor (typo fix line 179: 'chown "$app_uid":"$app_uid" -R "$bindir"' -> 'chown "$app_uid":"$app_guid" -R "$bindir"')
### Versie v3.0.3 2022-02-06 - Bakerboy448 fixup ownership
### Versie v3.0.3a Readarr naar develop
### Versie v3.0.4 2022-03-01 - Sleep toegevoegd voor het controleren van de servicestatus
### Versie v3.0.5 2022-04-03 - VP-EN (Whisparr toegevoegd)
### Versie v3.0.6 2022-04-26 - Bakerboy448 - binaries naar groep
### Versie v3.0.7 2023-01-05 - Bakerboy448 - Prowlarr naar master
### Versie v3.0.8 2023-04-20 - Bakerboy448 - Shellcheck-fixes en eerdere tarballs verwijderen
### Versie v3.0.9 2023-04-28 - Bakerboy448 - tarball-controle fixen
### Versie v3.0.9a 2023-07-14 - DoctorArr - bijgewerkte scriptversie en scriptdatum en om te zien hoe dit gaat! Het was nog steeds op v3.0.8.
### Extra updates door: De \*Arr-community

### Boilerplate-waarschuwing
#DE SOFTWARE WORDT GELEVERD "ZOALS DIE IS", ZONDER ENIGE GARANTIE,
#UITDRUKKELIJK OF IMPLICIET, INCLUSIEF MAAR NIET BEPERKT TOT DE GARANTIES VAN
#VERKOOPBAARHEID, GESCHIKTHEID VOOR EEN BEPAALD DOEL EN
#NIET-INBREUKMAKENDHEID. IN GEEN GEVAL ZIJN DE AUTEURS OF AUTEURSRECHTHEBBENDEN
#AANSPRAKELIJK VOOR ENIGE CLAIM, SCHADE OF ANDERE AANSPRAKELIJKHEID, HETZIJ IN EEN ACTIE
#VAN CONTRACT, ONRECHT OF ANDERSZINS, VOORTVLOEIEND UIT, OF IN VERBAND MET DE SOFTWARE OF HET GEBRUIK OF ANDERE HANDELINGEN
#IN DE SOFTWARE.

scriptversion="3.0.9a"
scriptdate="2023-07-14"

set -euo pipefail

echo "Uitvoeren van \*Arr Installatiescript - Versie [$scriptversion] van [$scriptdate]"

# Ben ik root?, root nodig!

if [ "$EUID" -ne 0 ]; then
    echo "Voer uit als root."
    exit
fi

echo "Selecteer de applicatie die geïnstalleerd moet worden: "

select app in lidarr prowlarr radarr readarr whisparr quit; do

    case $app in
    lidarr)
        app_port="8686"                                          # Standaard App-poort; Wijzig indien nodig config.xml na installatie
        app_prereq="curl sqlite3 libchromaprint-tools mediainfo" # Vereiste pakketten
        app_umask="0002"                                         # UMask waarin de service wordt uitgevoerd
        branch="master"                                          # {Update me indien nodig} tak om te installeren
        break
        ;;
    prowlarr)
        app_port="9696"           # Standaard App-poort; Wijzig indien nodig config.xml na installatie
        app_prereq="curl sqlite3" # Vereiste pakketten
        app_umask="0002"          # UMask waarin de service wordt uitgevoerd
        branch="master"          # {Update me indien nodig} tak om te installeren
        break
        ;;
    radarr)
        app_port="7878"           # Standaard App-poort; Wijzig indien nodig config.xml na installatie
        app_prereq="curl sqlite3" # Vereiste pakketten
        app_umask="0002"          # UMask waarin de service wordt uitgevoerd
        branch="master"           # {Update me indien nodig} tak om te installeren
        break
        ;;
    readarr)
        app_port="8787"           # Standaard App-poort; Wijzig indien nodig config.xml na installatie
        app_prereq="curl sqlite3" # Vereiste pakketten
        app_umask="0002"          # UMask waarin de service wordt uitgevoerd
        branch="develop"          # {Update me indien nodig} tak om te installeren
        break
        ;;
    whisparr)
        app_port="6969"           # Standaard App-poort; Wijzig indien nodig config.xml na installatie
        app_prereq="curl sqlite3" # Vereiste pakketten
        app_umask="0002"          # UMask waarin de service wordt uitgevoerd
        branch="nightly"          # {Update me indien nodig} tak om te installeren
        break
        ;;
    quit)
        exit 0
        ;;
    *)
        echo "Ongeldige optie $REPLY"
        ;;
    esac
done

# Constanten
### Werk deze variabelen bij zoals vereist voor uw specifieke instantie
installdir="/opt"              # {Update me indien nodig} Installatielocatie
bindir="${installdir}/${app^}" # Volledig pad naar installatielocatie
datadir="/var/lib/$app/"       # {Update me indien nodig} AppData-map om te gebruiken
app_bin=${app^}                # Binaire naam van de app

if [[ $app != 'prowlarr' ]]; then
    echo "Het is belangrijk dat de gebruiker en groep die u selecteert om ${app^} uit te voeren, LEES- en SCHRIJFtoegang hebben tot uw mediamap en voltooide downloadmappen van de downloadclient"
fi

# Vraag gebruiker
read -r -p "Als welke gebruiker moet ${app^} worden uitgevoerd? (Standaard: $app): " app_uid
app_uid=$(echo "$app_uid" | tr -d ' ')
app_uid=${app_uid:-$app}
# Vraag groep
read -r -p "Als welke groep moet ${app^} worden uitgevoerd? (Standaard: media): " app_guid
app_guid=$(echo "$app_guid" | tr -d ' ')
app_guid=${app_guid:-media}

echo "${app^} geselecteerd"
echo "Dit zal [${app^}] installeren in [$bindir] en [$datadir] gebruiken voor de AppData-map"
if [[ $app == 'prowlarr' ]]; then
    echo "${app^} wordt uitgevoerd als de gebruiker [$app_uid] en groep [$app_guid]."
else
    echo "${app^} wordt uitgevoerd als de gebruiker [$app_uid] en groep [$app_guid]. Door verder te gaan, bevestigt u dat die gebruiker en groep LEES- en SCHRIJFtoegang hebben tot uw mediamap en voltooide downloadmappen van de downloadclient"
fi
echo "Doorgaan met de installatie [Ja/Nee]?"
select yn in "Ja" "Nee"; do
    case $yn in
    Ja) break ;;
    Nee) exit 0 ;;
    esac
done

# Maak gebruiker/groep indien nodig
if [ "$app_guid" != "$app_uid" ]; then
    if ! getent group "$app_guid" >/dev/null; then
        groupadd "$app_guid"
    fi
fi
if ! getent passwd "$app_uid" >/dev/null; then
    adduser --system --no-create-home --ingroup "$app_guid" "$app_uid"
    echo "Gebruiker [$app_uid] aangemaakt en toegevoegd aan groep [$app_guid]"
fi
if ! getent group "$app_guid" | grep -qw "$app_uid"; then
    echo "Gebruiker [$app_uid] bestond niet in groep [$app_guid]"
    usermod -a -G "$app_guid" "$app_uid"
    echo "Gebruiker [$app_uid] toegevoegd aan groep [$app_guid]"
fi

# Stop de App als deze actief is
if service --status-all | grep -Fq "$app"; then
    systemctl stop "$app"
    systemctl disable "$app".service
    echo "Bestaande $app gestopt"
fi

# Maak Appdata-map

# AppData
mkdir -p "$datadir"
chown -R "$app_uid":"$app_guid" "$datadir"
chmod 775 "$datadir"
echo "Mappen aangemaakt"
# Download en installeer de App

# vereiste pakketten
echo ""
echo "Installeren van vereiste pakketten"
# shellcheck disable=SC2086
apt update && apt install $app_prereq
echo ""
ARCH=$(dpkg --print-architecture)
# krijg arch
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo "Arch wordt niet ondersteund"
    exit 1
    ;;
esac
echo ""
echo "Verwijderen van eerdere tarballs"
# -f om te forceren zodat we mislukken als het niet bestaat
rm -f "${app^}".*.tar.gz
echo ""
echo "Downloaden..."
wget --content-disposition "$DLURL"
tar -xvzf "${app^}".*.tar.gz
echo ""
echo "Installatiebestanden gedownload en uitgepakt"

# verwijder bestaande installaties
echo "Verwijderen van bestaande installatie"
# Als u dit script toevallig uitvoert in de installdir, verwijdert de onderstaande regel de uitgepakte bestanden en veroorzaakt het mv-commando enkele regels hieronder een fout.
rm -rf "$bindir"
echo "Installeren..."
mv "${app^}" $installdir
chown "$app_uid":"$app_guid" -R "$bindir"
chmod 775 "$bindir"
rm -rf "${app^}.*.tar.gz"
# Zorg ervoor dat we controleren op een update voor het geval de gebruiker een oudere versie of een andere tak installeert
touch "$datadir"/update_required
chown "$app_uid":"$app_guid" "$datadir"/update_required
echo "App geïnstalleerd"
# Configureer automatisch starten

# Verwijder eventuele eerdere app .service
echo "Verwijderen van oude servicebestand"
rm -rf /etc/systemd/system/"$app".service

# Maak app .service met juiste gebruikersopstart
echo "Maken van servicebestand"
cat <<EOF | tee /etc/systemd/system/"$app".service >/dev/null
[Unit]
Beschrijving=${app^} Daemon
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

# Start de App
echo "Servicebestand gemaakt. Proberen de app te starten"
systemctl -q daemon-reload
systemctl enable --now -q "$app"

# Voltooien van update/installatie
host=$(hostname -I)
ip_local=$(grep -oP '^\S*' <<<"$host")
echo ""
echo "Installatie voltooid"
sleep 10
STATUS="$(systemctl is-active "$app")"
if [ "${STATUS}" = "active" ]; then
    echo "Ga naar http://$ip_local:$app_port voor de ${app^} GUI"
else
    echo "${app^} kon niet worden gestart"
fi

# Afsluiten
exit 0

```

- Druk op <kbd>Ctrl</kbd>+<kbd>O</kbd> (opslaan) en vervolgens op <kbd>Enter</kbd>
- Druk op <kbd>Ctrl</kbd>+<kbd>X</kbd> (afsluiten) en vervolgens op <kbd>Enter</kbd>
- Typ vervolgens in uw console en volg de instructies

```shell
sudo bash ArrInstall.sh
```