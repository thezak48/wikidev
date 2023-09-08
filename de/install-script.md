# \*Arr Installationsskript

Dies ist ein von der Community erstelltes und von der Community unterstütztes **inoffizielles** Skript zur Installation von Lidarr/Prowlarr/Radarr/Readarr/Whisparr auf einem Linux-Betriebssystem, das in der Regel auf Debian & Ubuntu oder ähnlichen Distributionen abzielt.

> Dies installiert die ausgewählte Anwendung in /opt. Sie wird als der von Ihnen konfigurierte Benutzer und die von Ihnen konfigurierte Gruppe ausgeführt.
> Für Lidarr/Radarr/Readarr/Whisparr sollten Sie eine gemeinsame Gruppe verwenden, die dieselbe ist wie die, unter der Ihr Download-Client und Ihr Medienserver ausgeführt werden, um eine korrekte Besitzverhältnis und Berechtigungen sicherzustellen und auf alle Dateien zugreifen zu können.
{.is-info}

Bitte beachten Sie den folgenden häufigen Fehler in Bezug auf Berechtigungen.

> Zwei Dinge, die Sie beachten sollten, sind, dass Lidarr/Radarr/Readarr/Whisparr Lese- und Schreibzugriff auf das Download-Verzeichnis Ihres Download-Clients und auf den Ordner benötigen, den Sie als Stammverzeichnis (Bibliothek oder Medien) konfigurieren.
> Idealerweise läuft jede Anwendung als eigener Benutzer und gemeinsame Gruppe `media` mit Berechtigungen von `775` und `664`, was einer UMask von `002` entspricht.
> \* Ihre Download-Clients und Medienserver werden als und sind Teil der von Ihnen eingegebenen Gruppe ausgeführt.
> \* Ihre Pfade, die von Ihren Download-Clients und Medienservern verwendet werden, sind für die von Ihnen eingegebene Gruppe zugänglich (Lesen/Schreiben).
{.is-warning}

Beachten Sie Folgendes:

> Dies entfernt alle vorhandenen Installationen, die in /opt installiert sind. Es deinstalliert jedoch keine vorhandenen Installationen an einem anderen Speicherort. Stellen Sie sicher, dass Sie eine Sicherung Ihrer Einstellungen mit der Backup-Funktion in der App (System => Backup) haben. Das Skript löscht Ihre Einstellungen (Anwendungsdaten) nicht, aber seien Sie vorsichtig.
{.is-danger}

- (Optional) Stellen Sie sicher, dass Sie eine [statische IP-Adresse festgelegt](https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/) haben, dies wird Ihnen das Leben erleichtern.
- Greifen Sie über SSH auf Ihren Debian (Raspbian / Raspberry Pi OS) / Ubuntu-Computer zu und werden Sie zum Root-Benutzer oder melden Sie sich als Root-Benutzer an.

> Greifen Sie über Putty, mRemoteNG oder ein anderes SSH-Tool auf SSH zu. Beachten Sie, dass die meisten Tools Ihre Verbindung speichern können.
{.is-info}

- Geben Sie nach dem SSH-Zugriff den folgenden Befehl ein, um das Installationsskript in Ihrem aktuellen Verzeichnis zu erstellen.

```bash
nano ArrInstall.sh
```

- Kopieren Sie (obere rechte Ecke des Skripts) und fügen Sie es in Ihre SSH-Konsole ein. Überprüfen Sie die Variablen mit Kommentaren und aktualisieren Sie sie bei Bedarf.
  - Wenn Sie ein GUI-Betriebssystem wie Windows oder MacOS (OSX) verwenden, können Sie einfach mit der rechten Maustaste in Ihren SSH-Client klicken, um einzufügen.

```bash
#!/bin/bash
### Beschreibung: \*Arr .NET Debian-Installation
### Ursprünglich für Radarr von: DoctorArr - doctorarr@the-rowlands.co.uk am 2021-10-01 v1.0
### Version v1.1 2021-10-02 - Bakerboy448 (Allgemeiner und konformer gemacht)
### Version v1.1.1 2021-10-02 - DoctorArr (Rechtschreibprüfung und Boilerplate-Update)
### Version v2.0.0 2021-10-09 - Bakerboy448 (Skript umgeschrieben, um nach Benutzer/Gruppe zu fragen und für alle \*Arrs allgemein zu sein)
### Version v2.0.1 2021-11-23 - brightghost (Schritt datadir korrigiert, um die richtigen Variablen zu verwenden.)
### Version v3.0.0 2022-02-03 - Bakerboy448 (Skript umgeschrieben, um nach Benutzer/Gruppe zu fragen und für alle \*Arrs allgemein zu sein)
### Version v3.0.1 2022-02-05 - aeramor (Tippfehlerkorrektur Zeile 179: 'chown "$app_uid":"$app_uid" -R "$bindir"' -> 'chown "$app_uid":"$app_guid" -R "$bindir"')
### Version v3.0.3 2022-02-06 - Bakerboy448 - Berechtigungen korrigiert
### Version v3.0.3a Readarr zu entwickeln
### Version v3.0.4 2022-03-01 - Vor dem Überprüfen des Dienststatus warten
### Version v3.0.5 2022-04-03 - VP-EN (Whisparr hinzugefügt)
### Version v3.0.6 2022-04-26 - Bakerboy448 - Binärdateien zur Gruppe
### Version v3.0.7 2023-01-05 - Bakerboy448 - Prowlarr zu Master
### Version v3.0.8 2023-04-20 - Bakerboy448 - Shellcheck-Korrekturen & vorherige Tarballs entfernen
### Version v3.0.9 2023-04-28 - Bakerboy448 - Tarball-Überprüfung korrigieren
### Version v3.0.9a 2023-07-14 - DoctorArr - Skriptversion und Skriptdatum aktualisiert und sehen, wie es läuft! Es war immer noch bei v3.0.8.
### Weitere Updates von: Der \*Arr-Community

### Boilerplate-Warnung
# DIE SOFTWARE WIRD "WIE BESEHEN" OHNE JEGLICHE AUSDRÜCKLICHE ODER
# STILLSCHWEIGENDE GEWÄHRLEISTUNG BEREITGESTELLT, EINSCHLIESSLICH, ABER NICHT
# BESCHRÄNKT AUF DIE GEWÄHRLEISTUNG DER MARKTGÄNGIGKEIT, DER EIGNUNG FÜR EINEN
# BESTIMMTEN ZWECK UND DER NICHTVERLETZUNG. IN KEINEM FALL HAFTEN DIE AUTOREN ODER
# COPYRIGHT-INHABER FÜR ANSPRÜCHE, SCHÄDEN ODER ANDERE HAFTUNGEN, OB IN EINER
# VERTRAGS-, UNERLAUBTEN HANDLUNG ODER ANDERWEITIG, DIE SICH AUS, AUS ODER IN
# VERBINDUNG MIT DER SOFTWARE ODER DER VERWENDUNG ODER ANDEREN GESCHÄFTEN MIT DER
# SOFTWARE ERGEBEN.

scriptversion="3.0.9a"
scriptdate="2023-07-14"

set -euo pipefail

echo "Ausführung des \*Arr-Installations-Skripts - Version [$scriptversion] vom [$scriptdate]"

# Bin ich root?, benötige root!

if [ "$EUID" -ne 0 ]; then
    echo "Bitte als Root ausführen."
    exit
fi

echo "Wählen Sie die Anwendung aus, die installiert werden soll: "

select app in lidarr prowlarr radarr readarr whisparr quit; do

    case $app in
    lidarr)
        app_port="8686"                                          # Standard-App-Port; Konfigurieren Sie config.xml nach der Installation bei Bedarf
        app_prereq="curl sqlite3 libchromaprint-tools mediainfo" # Erforderliche Pakete
        app_umask="0002"                                         # UMask, unter der der Dienst ausgeführt wird
        branch="master"                                          # {Bei Bedarf aktualisieren} zu installierender Branch
        break
        ;;
    prowlarr)
        app_port="9696"           # Standard-App-Port; Konfigurieren Sie config.xml nach der Installation bei Bedarf
        app_prereq="curl sqlite3" # Erforderliche Pakete
        app_umask="0002"          # UMask, unter der der Dienst ausgeführt wird
        branch="master"          # {Bei Bedarf aktualisieren} zu installierender Branch
        break
        ;;
    radarr)
        app_port="7878"           # Standard-App-Port; Konfigurieren Sie config.xml nach der Installation bei Bedarf
        app_prereq="curl sqlite3" # Erforderliche Pakete
        app_umask="0002"          # UMask, unter der der Dienst ausgeführt wird
        branch="master"           # {Bei Bedarf aktualisieren} zu installierender Branch
        break
        ;;
    readarr)
        app_port="8787"           # Standard-App-Port; Konfigurieren Sie config.xml nach der Installation bei Bedarf
        app_prereq="curl sqlite3" # Erforderliche Pakete
        app_umask="0002"          # UMask, unter der der Dienst ausgeführt wird
        branch="develop"          # {Bei Bedarf aktualisieren} zu installierender Branch
        break
        ;;
    whisparr)
        app_port="6969"           # Standard-App-Port; Konfigurieren Sie config.xml nach der Installation bei Bedarf
        app_prereq="curl sqlite3" # Erforderliche Pakete
        app_umask="0002"          # UMask, unter der der Dienst ausgeführt wird
        branch="nightly"          # {Bei Bedarf aktualisieren} zu installierender Branch
        break
        ;;
    quit)
        exit 0
        ;;
    *)
        echo "Ungültige Option $REPLY"
        ;;
    esac
done

# Konstanten
### Aktualisieren Sie diese Variablen nach Bedarf für Ihre spezifische Instanz
installdir="/opt"              # {Bei Bedarf aktualisieren} Installationsort
bindir="${installdir}/${app^}" # Vollständiger Pfad zum Installationsort
datadir="/var/lib/$app/"       # {Bei Bedarf aktualisieren} Zu verwendendes AppData-Verzeichnis
app_bin=${app^}                # Binärname der App

if [[ $app != 'prowlarr' ]]; then
    echo "Es ist wichtig, dass der Benutzer und die Gruppe, unter der ${app^} ausgeführt wird, Lese- und Schreibzugriff auf Ihre Medienbibliothek und den abgeschlossenen Downloadordner des Download-Clients haben."
fi

# Benutzer abfragen
read -r -p "Als welcher Benutzer soll ${app^} ausgeführt werden? (Standard: $app): " app_uid
app_uid=$(echo "$app_uid" | tr -d ' ')
app_uid=${app_uid:-$app}
# Gruppe abfragen
read -r -p "Als welche Gruppe soll ${app^} ausgeführt werden? (Standard: media): " app_guid
app_guid=$(echo "$app_guid" | tr -d ' ')
app_guid=${app_guid:-media}

echo "${app^} ausgewählt"
echo "Dies installiert [${app^}] in [$bindir] und verwendet [$datadir] für das AppData-Verzeichnis"
if [[ $app == 'prowlarr' ]]; then
    echo "${app^} wird als Benutzer [$app_uid] und Gruppe [$app_guid] ausgeführt."
else
    echo "${app^} wird als Benutzer [$app_uid] und Gruppe [$app_guid] ausgeführt. Durch die Fortsetzung haben Sie bestätigt, dass dieser Benutzer und diese Gruppe Lese- und Schreibzugriff auf Ihre Medienbibliothek und den abgeschlossenen Downloadordner des Download-Clients haben."
fi
echo "Mit der Installation fortfahren [Ja/Nein]?"
select yn in "Ja" "Nein"; do
    case $yn in
    Ja) break ;;
    Nein) exit 0 ;;
    esac
done

# Benutzer/Gruppe bei Bedarf erstellen
if [ "$app_guid" != "$app_uid" ]; then
    if ! getent group "$app_guid" >/dev/null; then
        groupadd "$app_guid"
    fi
fi
if ! getent passwd "$app_uid" >/dev/null; then
    adduser --system --no-create-home --ingroup "$app_guid" "$app_uid"
    echo "Benutzer [$app_uid] wurde erstellt und zur Gruppe [$app_guid] hinzugefügt"
fi
if ! getent group "$app_guid" | grep -qw "$app_uid"; then
    echo "Benutzer [$app_uid] war nicht in der Gruppe [$app_guid] vorhanden"
    usermod -a -G "$app_guid" "$app_uid"
    echo "Benutzer [$app_uid] wurde zur Gruppe [$app_guid] hinzugefügt"
fi

# App stoppen, falls ausgeführt
if service --status-all | grep -Fq "$app"; then
    systemctl stop "$app"
    systemctl disable "$app".service
    echo "Vorhandenes $app wurde gestoppt"
fi

# AppData-Verzeichnis erstellen

# AppData
mkdir -p "$datadir"
chown -R "$app_uid":"$app_guid" "$datadir"
chmod 775 "$datadir"
echo "Verzeichnisse erstellt"
# App herunterladen und installieren

# Voraussetzungspakete
echo ""
echo "Installation der Voraussetzungspakete"
# shellcheck disable=SC2086
apt update && apt install $app_prereq
echo ""
ARCH=$(dpkg --print-architecture)
# Architektur abrufen
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo "Architektur wird nicht unterstützt"
    exit 1
    ;;
esac
echo ""
echo "Entfernen vorheriger Tarballs"
# -f zum Erzwingen, damit wir fehlschlagen, wenn er nicht vorhanden ist
rm -f "${app^}".*.tar.gz
echo ""
echo "Herunterladen..."
wget --content-disposition "$DLURL"
tar -xvzf "${app^}".*.tar.gz
echo ""
echo "Installationsdateien heruntergeladen und extrahiert"

# Vorhandene Installationen entfernen
echo "Vorhandene Installation wird entfernt"
# Wenn Sie dieses Skript zufällig im Installationsverzeichnis ausführen, löscht die folgende Zeile die extrahierten Dateien und führt dazu, dass das mv in den folgenden Zeilen fehlschlägt.
rm -rf "$bindir"
echo "Installation..."
mv "${app^}" $installdir
chown "$app_uid":"$app_guid" -R "$bindir"
chmod 775 "$bindir"
rm -rf "${app^}.*.tar.gz"
# Sicherstellen, dass wir nach einem Update suchen, falls der Benutzer eine ältere Version oder einen anderen Branch installiert
touch "$datadir"/update_required
chown "$app_uid":"$app_guid" "$datadir"/update_required
echo "App installiert"
# Autostart konfigurieren

# Vorherige app .service entfernen
echo "Alte Service-Datei wird entfernt"
rm -rf /etc/systemd/system/"$app".service

# app .service mit korrektem Benutzerstart erstellen
echo "Service-Datei wird erstellt"
cat <<EOF | tee /etc/systemd/system/"$app".service >/dev/null
[Unit]
Beschreibung=${app^} Daemon
After=syslog.target network.target
[Service]
Benutzer=$app_uid
Gruppe=$app_guid
UMask=$app_umask
Typ=simple
ExecStart=$bindir/$app_bin -nobrowser -data=$datadir
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF

# App starten
echo "Service-Datei erstellt. Versuche, die App zu starten"
systemctl -q daemon-reload
systemctl enable --now -q "$app"

# Installation/Update abschließen
host=$(hostname -I)
ip_local=$(grep -oP '^\S*' <<<"$host")
echo ""
echo "Installation abgeschlossen"
sleep 10
STATUS="$(systemctl is-active "$app")"
if [ "${STATUS}" = "active" ]; then
    echo "Öffnen Sie http://$ip_local:$app_port für die ${app^} GUI"
else
    echo "${app^} konnte nicht gestartet werden"
fi

# Beenden
exit 0

```

- Drücken Sie <kbd>Strg</kbd>+<kbd>O</kbd> (speichern) und dann <kbd>Eingabe</kbd>.
- Drücken Sie <kbd>Strg</kbd>+<kbd>X</kbd> (beenden) und dann <kbd>Eingabe</kbd>.
- Geben Sie dann in Ihrer Konsole ein und folgen Sie den Anweisungen

```shell
sudo bash ArrInstall.sh
```