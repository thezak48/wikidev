# \*Arr Installationskript

Detta är ett gemenskapskreativt och gemenskapsstött **inofficiellt** skript för att hantera installationen av Lidarr/Prowlarr/Radarr/Readarr/Whisparr på ett Linux-operativsystem - vanligtvis riktat mot Debian & Ubuntu eller liknande distributioner.

> Detta kommer att installera den valda applikationen till /opt. Den kommer att köra applikationen som den användare och grupp du konfigurerar.
> För Lidarr/Radarr/Readarr/Whisparr - bör du använda en gemensam grupp som är samma som din nedladdningsklients och mediaserver kör som för att säkerställa att ägande och behörigheter är korrekta och att alla filer är åtkomliga.
{.is-info}

Var medveten om följande vanliga fel gällande behörigheter.

> Två saker att tänka på är att Lidarr/Radarr/Readarr/Whisparr kräver läs- och skrivåtkomst till din nedladdningsklients nedladdningskatalog och vilken mapp du konfigurerar som rot (bibliotek eller media) mapp.
> Idealt sett körs varje app som sin egen användare och gemensam grupp av `media` med behörigheter `775` och `664` vilket är en UMask på `002`
> \* Dina nedladdningsklienter och mediaserver körs som och är en del av den grupp du anger
> \* Dina sökvägar som används av dina nedladdningsklienter och mediaserver är åtkomliga (läs/skriv) för den grupp du anger
{.is-warning}

Var medveten om följande:

> Detta kommer att ta bort alla befintliga installationer som är installerade i /opt. Det kommer inte att avinstallera befintliga installationer från någon annan plats; se till att du har en säkerhetskopia av dina inställningar med hjälp av Backup från inom appen (System => Backup). Skriptet kommer inte att ta bort dina inställningar (applikationsdata), men var säker.
{.is-danger}

- (Valfritt) Se till att du har [ställt in en statisk IP-adress](https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/), det kommer att underlätta ditt liv.
- SSH:a in på din Debian (Raspbian / Raspberry Pi OS) / Ubuntu-box och bli eller logga in som root.

> SSH:a in med hjälp av Putty, mRemoteNG eller något annat SSH-verktyg. Observera att de flesta verktyg stöder att spara din anslutning.{.is-info}

- När du är inloggad via SSH, skriv följande för att skapa installationskriptet i din aktuella katalog

```bash
nano ArrInstall.sh
```

- Kopiera (övre högra hörnet av skriptet) och klistra in i din SSH-konsol. Granska variablerna med kommentarer och uppdatera vid behov.
  - Om du är i ett GUI-operativsystem som Windows eller MacOS (OSX): kan klistrandet vara så enkelt som att 'högerklicka' i din SSH-klient.

```bash
#!/bin/bash
### Beskrivning: \*Arr .NET Debian-installation
### Ursprungligen skriven för Radarr av: DoctorArr - doctorarr@the-rowlands.co.uk den 2021-10-01 v1.0
### Version v1.1 2021-10-02 - Bakerboy448 (Gjorde mer generisk och konformant)
### Version v1.1.1 2021-10-02 - DoctorArr (Stavningskontroll och malluppdatering)
### Version v2.0.0 2021-10-09 - Bakerboy448 (Omskriven och säkerställt att skriptet är generiskt. Lade till fler variabler.)
### Version v2.0.1 2021-11-23 - brightghost (Fixade datadir-steg för att använda korrekta variabler.)
### Version v3.0.0 2022-02-03 - Bakerboy448 (Omskrev skriptet för att fråga efter användare/grupp och gjorde det generiskt för alla \*Arrs)
### Version v3.0.1 2022-02-05 - aeramor (stavningsfel fixa rad 179: 'chown "$app_uid":"$app_uid" -R "$bindir"' -> 'chown "$app_uid":"$app_guid" -R "$bindir"')
### Version v3.0.3 2022-02-06 - Bakerboy448 fixup ownership
### Version v3.0.3a Readarr till develop
### Version v3.0.4 2022-03-01 - Lägg till sleep innan du kontrollerar tjänststatus
### Version v3.0.5 2022-04-03 - VP-EN (Lade till Whisparr)
### Version v3.0.6 2022-04-26 - Bakerboy448 - binärer till grupp
### Version v3.0.7 2023-01-05 - Bakerboy448 - Prowlarr till master
### Version v3.0.8 2023-04-20 - Bakerboy448 - Shellcheck-fixar och ta bort tidigare tarballs
### Version v3.0.9 2023-04-28 - Bakerboy448 - fixa tarball-kontroll
### Version v3.0.9a 2023-07-14 - DoctorArr - uppdaterad skriptversion och skriptdatum och för att se hur det går! Det var fortfarande på v3.0.8.
### Ytterligare uppdateringar av: \*Arr Community

### Mallvarning
#PROGRAMVARAN LEVERERAS "I BEFINTLIGT SKICK", UTAN GARANTI AV NÅGOT SLAG,
#UTTRYCKLIGEN ELLER UNDERFÖRSTÅDD, INKLUSIVE MEN INTE BEGRÄNSAT TILL GARANTIER OM
#SÄLJBARHET, LÄMPLIGHET FÖR ETT VISST SYFTE OCH
#OTRÅNG. UNDER INGA OMSTÄNDIGHETER SKALL UPPHOVSMÄNNEN ELLER UPPHOVSRÄTTSHAVARENA VARA
#ANSVARIGA FÖR NÅGON FORDRAN, SKADOR ELLER ANNAN SKYLDIGHET, VARE SIG I ETT AVTAL
#SKADESTÅNDSRÄTT, TORT ELLER PÅ ANNAT SÄTT, SOM UPPSTÅR FRÅN, UT AV ELLER I SAMBAND
#MED PROGRAMVARAN ELLER ANVÄNDNINGEN ELLER ANDRA ÅTGÄRDER I PROGRAMVARAN.

skriptversion="3.0.9a"
skriptdatum="2023-07-14"

set -euo pipefail

echo "Kör \*Arr Installationskript - Version [$skriptversion] från [$skriptdatum]"

# Är jag root?, behöver root!

if [ "$EUID" -ne 0 ]; then
    echo "Kör som root."
    exit
fi

echo "Välj applikationen att installera: "

select app in lidarr prowlarr radarr readarr whisparr quit; do

    case $app in
    lidarr)
        app_port="8686"                                          # Standardapplikationsport; Uppdatera config.xml efter installationen om det behövs
        app_prereq="curl sqlite3 libchromaprint-tools mediainfo" # Nödvändiga paket
        app_umask="0002"                                         # UMask som tjänsten körs som
        branch="master"                                          # {Uppdatera mig om det behövs} gren att installera
        break
        ;;
    prowlarr)
        app_port="9696"           # Standardapplikationsport; Uppdatera config.xml efter installationen om det behövs
        app_prereq="curl sqlite3" # Nödvändiga paket
        app_umask="0002"          # UMask som tjänsten körs som
        branch="master"          # {Uppdatera mig om det behövs} gren att installera
        break
        ;;
    radarr)
        app_port="7878"           # Standardapplikationsport; Uppdatera config.xml efter installationen om det behövs
        app_prereq="curl sqlite3" # Nödvändiga paket
        app_umask="0002"          # UMask som tjänsten körs som
        branch="master"           # {Uppdatera mig om det behövs} gren att installera
        break
        ;;
    readarr)
        app_port="8787"           # Standardapplikationsport; Uppdatera config.xml efter installationen om det behövs
        app_prereq="curl sqlite3" # Nödvändiga paket
        app_umask="0002"          # UMask som tjänsten körs som
        branch="develop"          # {Uppdatera mig om det behövs} gren att installera
        break
        ;;
    whisparr)
        app_port="6969"           # Standardapplikationsport; Uppdatera config.xml efter installationen om det behövs
        app_prereq="curl sqlite3" # Nödvändiga paket
        app_umask="0002"          # UMask som tjänsten körs som
        branch="nightly"          # {Uppdatera mig om det behövs} gren att installera
        break
        ;;
    quit)
        exit 0
        ;;
    *)
        echo "Ogiltigt alternativ $REPLY"
        ;;
    esac
done

# Konstanter
### Uppdatera dessa variabler vid behov för din specifika instans
installdir="/opt"              # {Uppdatera mig om det behövs} Installationsplats
bindir="${installdir}/${app^}" # Full sökväg till installationsplatsen
datadir="/var/lib/$app/"       # {Uppdatera mig om det behövs} AppData-katalog att använda
app_bin=${app^}                # Binärnamn för appen

if [[ $app != 'prowlarr' ]]; then
    echo "Det är viktigt att användaren och gruppen du väljer att köra ${app^} som har LÄS- och SKRIV-åtkomst till ditt mediebibliotek och din nedladdningsklients slutförda mappar"
fi

# Be användaren
read -r -p "Vilken användare ska ${app^} köras som? (Standard: $app): " app_uid
app_uid=$(echo "$app_uid" | tr -d ' ')
app_uid=${app_uid:-$app}
# Be om grupp
read -r -p "Vilken grupp ska ${app^} köras som? (Standard: media): " app_guid
app_guid=$(echo "$app_guid" | tr -d ' ')
app_guid=${app_guid:-media}

echo "${app^} vald"
echo "Detta kommer att installera [${app^}] till [$bindir] och använda [$datadir] för AppData-katalogen"
if [[ $app == 'prowlarr' ]]; then
    echo "${app^} kommer att köras som användaren [$app_uid] och gruppen [$app_guid]."
else
    echo "${app^} kommer att köras som användaren [$app_uid] och gruppen [$app_guid]. Genom att fortsätta har du bekräftat att den användaren och gruppen kommer att ha LÄS- och SKRIV-åtkomst till ditt mediebibliotek och din nedladdningsklients slutförda nedladdningskataloger"
fi
echo "Fortsätt med installationen [Ja/Nej]?"
select yn in "Ja" "Nej"; do
    case $yn in
    Ja) break ;;
    Nej) exit 0 ;;
    esac
done

# Skapa användare/grupp vid behov
if [ "$app_guid" != "$app_uid" ]; then
    if ! getent group "$app_guid" >/dev/null; then
        groupadd "$app_guid"
    fi
fi
if ! getent passwd "$app_uid" >/dev/null; then
    adduser --system --no-create-home --ingroup "$app_guid" "$app_uid"
    echo "Skapade och lade till användaren [$app_uid] i gruppen [$app_guid]"
fi
if ! getent group "$app_guid" | grep -qw "$app_uid"; then
    echo "Användaren [$app_uid] fanns inte i gruppen [$app_guid]"
    usermod -a -G "$app_guid" "$app_uid"
    echo "Lade till användaren [$app_uid] i gruppen [$app_guid]"
fi

# Stoppa appen om den körs
if service --status-all | grep -Fq "$app"; then
    systemctl stop "$app"
    systemctl disable "$app".service
    echo "Stoppade befintlig $app"
fi

# Skapa Appdata-katalog

# AppData
mkdir -p "$datadir"
chown -R "$app_uid":"$app_guid" "$datadir"
chmod 775 "$datadir"
echo "Kataloger skapade"
# Ladda ner och installera appen

# förutsättningspaket
echo ""
echo "Installerar förutsättningspaket"
# shellcheck disable=SC2086
apt update && apt install $app_prereq
echo ""
ARCH=$(dpkg --print-architecture)
# få arkitektur
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo "Arkitektur stöds inte"
    exit 1
    ;;
esac
echo ""
echo "Tar bort tidigare tarballs"
# -f för att tvinga så att vi misslyckas om den inte finns
rm -f "${app^}".*.tar.gz
echo ""
echo "Laddar ner..."
wget --content-disposition "$DLURL"
tar -xvzf "${app^}".*.tar.gz
echo ""
echo "Installationsfiler har laddats ner och extraherats"

# ta bort befintliga installationer
echo "Tar bort befintlig installation"
# Om du råkar köra detta skript i installationskatalogen kommer raden nedan att ta bort de extraherade filerna och orsaka att mv några rader nedan misslyckas.
rm -rf "$bindir"
echo "Installerar..."
mv "${app^}" $installdir
chown "$app_uid":"$app_guid" -R "$bindir"
chmod 775 "$bindir"
rm -rf "${app^}.*.tar.gz"
# Se till att vi kontrollerar efter en uppdatering om användaren installerar en äldre version eller en annan gren
touch "$datadir"/update_required
chown "$app_uid":"$app_guid" "$datadir"/update_required
echo "Appen installerad"
# Konfigurera autostart

# Ta bort eventuell tidigare app .service
echo "Tar bort gammal tjänstefil"
rm -rf /etc/systemd/system/"$app".service

# Skapa app .service med korrekt användarstart
echo "Skapar tjänstefil"
cat <<EOF | tee /etc/systemd/system/"$app".service >/dev/null
[Unit]
Beskrivning=${app^} Daemon
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

# Starta appen
echo "Tjänstefil skapad. Försöker starta appen"
systemctl -q daemon-reload
systemctl enable --now -q "$app"

# Slutför uppdatering/installation
host=$(hostname -I)
ip_local=$(grep -oP '^\S*' <<<"$host")
echo ""
echo "Installationen är klar"
sleep 10
STATUS="$(systemctl is-active "$app")"
if [ "${STATUS}" = "active" ]; then
    echo "Bläddra till http://$ip_local:$app_port för ${app^} GUI"
else
    echo "${app^} misslyckades med att starta"
fi

# Avsluta
exit 0

```

- Tryck på <kbd>Ctrl</kbd>+<kbd>O</kbd> (spara) och sedan <kbd>Enter</kbd>
- Tryck på <kbd>Ctrl</kbd>+<kbd>X</kbd> (avsluta) och sedan <kbd>Enter</kbd>
- Sedan i din konsol, skriv och följ anvisningarna

```shell
sudo bash ArrInstall.sh
```