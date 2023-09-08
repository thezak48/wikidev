# \*Arr Installation Script

Dette er et fællesskabsskabt og fællesskabsunderstøttet **uofficielt** script til håndtering af installationen af Lidarr/Prowlarr/Radarr/Readarr/Whisparr på et Linux-operativsystem - normalt rettet mod Debian & Ubuntu eller lignende distributioner.

> Dette vil installere den valgte applikation til /opt. Den vil køre applikationen som den bruger og gruppe, du konfigurerer.
> For Lidarr/Radarr/Readarr/Whisparr - bør du bruge en fælles gruppe, der er den samme som din downloadklient kører som og medieserveren kører som for at sikre, at ejerskab og tilladelser er fornuftige, og at alle filer er tilgængelige.
{.is-info}

Vær opmærksom på følgende almindelige fejl vedrørende tilladelser.

> To ting at huske er, at Lidarr/Radarr/Readarr/Whisparr kræver læse- og skriveadgang til din downloadklients downloadmappe og den mappe, du konfigurerer som din rod (bibliotek eller medie) mappe.
> Ideelt set kører hver app som sin egen bruger og fælles gruppe med navnet `media` med tilladelserne `775` og `664`, hvilket er en UMask på `002`.
> \* Dine downloadklienter og medieserver kører som og er en del af den gruppe, du indtaster
> \* Dine stier, der bruges af dine downloadklienter og medieserver, er tilgængelige (læse/skrive) for den gruppe, du indtaster
{.is-warning}

Vær opmærksom på følgende:

> Dette vil fjerne eventuelle eksisterende installationer, der er installeret i /opt. Det vil ikke afinstallere eksisterende installationer fra nogen anden placering; sørg for at du har en sikkerhedskopi af dine indstillinger ved hjælp af Backup fra inden i appen (System => Backup). Scriptet vil ikke slette dine indstillinger (applikationsdata), men vær på den sikre side.
{.is-danger}

- (Valgfrit) Sørg for, at du har [indstillet en statisk IP-adresse](https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/), det vil gøre dit liv lettere.
- SSH ind på din Debian (Raspbian / Raspberry Pi OS) / Ubuntu-boks og bliv eller log ind som root.

> SSH ind ved hjælp af Putty, mRemoteNG eller et andet SSH-værktøj. Bemærk, at de fleste værktøjer understøtter at gemme din forbindelse.
{.is-info}

- Når du er SSH'et ind, skal du skrive nedenstående for at oprette installationscriptet i din aktuelle mappe

```bash
nano ArrInstall.sh
```

- Kopier (øverst i højre hjørne af scriptet) og indsæt i din SSH-konsol. Gennemgå variablerne med kommentarer og opdater om nødvendigt.
  - Hvis du er i et GUI-operativsystem som Windows eller MacOS (OSX): indsættelse kan være så simpelt som at 'højreklikke' i din SSH-klient.

```bash
#!/bin/bash
### Beskrivelse: \*Arr .NET Debian-installation
### Oprindeligt skrevet til Radarr af: DoctorArr - doctorarr@the-rowlands.co.uk den 2021-10-01 v1.0
### Version v1.1 2021-10-02 - Bakerboy448 (Gjort mere generisk og konform)
### Version v1.1.1 2021-10-02 - DoctorArr (Stavekontrol og boilerplate-opdatering)
### Version v2.0.0 2021-10-09 - Bakerboy448 (Omskrevet og sikret, at scriptet er generisk. Tilføjet flere variabler.)
### Version v2.0.1 2021-11-23 - brightghost (Fast datadir-trin til at bruge korrekte variabler.)
### Version v3.0.0 2022-02-03 - Bakerboy448 (Omskrevet script til at bede om bruger/gruppe og gjort generisk for alle \*Arrs)
### Version v3.0.1 2022-02-05 - aeramor (typo fix line 179: 'chown "$app_uid":"$app_uid" -R "$bindir"' -> 'chown "$app_uid":"$app_guid" -R "$bindir"')
### Version v3.0.3 2022-02-06 - Bakerboy448 fixup ownership
### Version v3.0.3a Readarr til udvikling
### Version v3.0.4 2022-03-01 - Tilføj sleep før kontrol af tjenestestatus
### Version v3.0.5 2022-04-03 - VP-EN (Tilføjet Whisparr)
### Version v3.0.6 2022-04-26 - Bakerboy448 - binærer til gruppe
### Version v3.0.7 2023-01-05 - Bakerboy448 - Prowlarr til master
### Version v3.0.8 2023-04-20 - Bakerboy448 - Shellcheck-fixes og fjern tidligere tarballs
### Version v3.0.9 2023-04-28 - Bakerboy448 - fix tarball check
### Version v3.0.9a 2023-07-14 - DoctorArr - opdateret scriptversion og scriptdato og for at se, hvordan det går! Det var stadig ved v3.0.8.
### Yderligere opdateringer af: \*Arr-fællesskabet

### Boilerplate-advarsel
#SOFTWAREN LEVERES "SOM DEN ER", UDEN GARANTI AF NOGEN ART,
#UDTRYKKELIG ELLER UNDERFORSTÅET, HERUNDER MEN IKKE BEGRÆNSET TIL GARANTIER FOR
#SALGBARHED, EGNETHED TIL ET BESTEMT FORMÅL OG
#OVERTRÆDELSE. UNDER INGEN OMSTÆNDIGHED SKAL FORFATTERNE ELLER OPHAVSRETSHAVERNE VÆRE
#ANSVARLIGE FOR NOGEN KRAV, SKADER ELLER ANDRE ANSVAR, UANSET OM DET ER I EN HANDLING
#AF KONTRAKT, TORT ELLER PÅ ANDEN MÅDE, DER OPSTÅR UD AF ELLER I FORBINDELSE MED SOFTWAREN
#ELLER BRUGEN ELLER ANDRE TRANSAKTIONER I SOFTWAREN.

scriptversion="3.0.9a"
scriptdate="2023-07-14"

set -euo pipefail

echo "Kører \*Arr Installationscript - Version [$scriptversion] pr. [$scriptdate]"

# Er jeg root?, har brug for root!

if [ "$EUID" -ne 0 ]; then
    echo "Kør venligst som root."
    exit
fi

echo "Vælg applikationen, der skal installeres: "

select app in lidarr prowlarr radarr readarr whisparr quit; do

    case $app in
    lidarr)
        app_port="8686"                                          # Standardapp-port; Opdater config.xml efter installationen, hvis det er nødvendigt
        app_prereq="curl sqlite3 libchromaprint-tools mediainfo" # Påkrævede pakker
        app_umask="0002"                                         # UMask, som tjenesten kører som
        branch="master"                                          # {Opdater mig om nødvendigt} gren til installation
        break
        ;;
    prowlarr)
        app_port="9696"           # Standardapp-port; Opdater config.xml efter installationen, hvis det er nødvendigt
        app_prereq="curl sqlite3" # Påkrævede pakker
        app_umask="0002"          # UMask, som tjenesten kører som
        branch="master"          # {Opdater mig om nødvendigt} gren til installation
        break
        ;;
    radarr)
        app_port="7878"           # Standardapp-port; Opdater config.xml efter installationen, hvis det er nødvendigt
        app_prereq="curl sqlite3" # Påkrævede pakker
        app_umask="0002"          # UMask, som tjenesten kører som
        branch="master"           # {Opdater mig om nødvendigt} gren til installation
        break
        ;;
    readarr)
        app_port="8787"           # Standardapp-port; Opdater config.xml efter installationen, hvis det er nødvendigt
        app_prereq="curl sqlite3" # Påkrævede pakker
        app_umask="0002"          # UMask, som tjenesten kører som
        branch="develop"          # {Opdater mig om nødvendigt} gren til installation
        break
        ;;
    whisparr)
        app_port="6969"           # Standardapp-port; Opdater config.xml efter installationen, hvis det er nødvendigt
        app_prereq="curl sqlite3" # Påkrævede pakker
        app_umask="0002"          # UMask, som tjenesten kører som
        branch="nightly"          # {Opdater mig om nødvendigt} gren til installation
        break
        ;;
    quit)
        exit 0
        ;;
    *)
        echo "Ugyldig mulighed $REPLY"
        ;;
    esac
done

# Konstanter
### Opdater disse variabler efter behov for din specifikke installation
installdir="/opt"              # {Opdater mig om nødvendigt} Installationsplacering
bindir="${installdir}/${app^}" # Fuld sti til installationsplacering
datadir="/var/lib/$app/"       # {Opdater mig om nødvendigt} AppData-mappe til brug
app_bin=${app^}                # Binært navn på appen

if [[ $app != 'prowlarr' ]]; then
    echo "Det er vigtigt, at den bruger og gruppe, du vælger at køre ${app^} som, har LÆSE- og SKRIVE-adgang til dit mediebibliotek og din downloadklients færdigmappede mapper"
fi

# Bed brugeren om input
read -r -p "Hvilken bruger skal ${app^} køre som? (Standard: $app): " app_uid
app_uid=$(echo "$app_uid" | tr -d ' ')
app_uid=${app_uid:-$app}
# Bed brugeren om input
read -r -p "Hvilken gruppe skal ${app^} køre som? (Standard: media): " app_guid
app_guid=$(echo "$app_guid" | tr -d ' ')
app_guid=${app_guid:-media}

echo "${app^} valgt"
echo "Dette vil installere [${app^}] til [$bindir] og bruge [$datadir] som AppData-mappen"
if [[ $app == 'prowlarr' ]]; then
    echo "${app^} vil køre som brugeren [$app_uid] og gruppen [$app_guid]."
else
    echo "${app^} vil køre som brugeren [$app_uid] og gruppen [$app_guid]. Ved at fortsætte har du bekræftet, at denne bruger og gruppe vil have LÆSE- og SKRIVE-adgang til dit mediebibliotek og din downloadklients færdigmappede downloadmapper"
fi
echo "Fortsæt installationen [Ja/Nej]?"
select yn in "Ja" "Nej"; do
    case $yn in
    Ja) break ;;
    Nej) exit 0 ;;
    esac
done

# Opret bruger/gruppe efter behov
if [ "$app_guid" != "$app_uid" ]; then
    if ! getent group "$app_guid" >/dev/null; then
        groupadd "$app_guid"
    fi
fi
if ! getent passwd "$app_uid" >/dev/null; then
    adduser --system --no-create-home --ingroup "$app_guid" "$app_uid"
    echo "Oprettede og tilføjede brugeren [$app_uid] til gruppen [$app_guid]"
fi
if ! getent group "$app_guid" | grep -qw "$app_uid"; then
    echo "Brugeren [$app_uid] eksisterede ikke i gruppen [$app_guid]"
    usermod -a -G "$app_guid" "$app_uid"
    echo "Tilføjede brugeren [$app_uid] til gruppen [$app_guid]"
fi

# Stop appen, hvis den kører
if service --status-all | grep -Fq "$app"; then
    systemctl stop "$app"
    systemctl disable "$app".service
    echo "Stoppede eksisterende $app"
fi

# Opret Appdata-mappe

# AppData
mkdir -p "$datadir"
chown -R "$app_uid":"$app_guid" "$datadir"
chmod 775 "$datadir"
echo "Mapper oprettet"
# Download og installer appen

# Påkrævede pakker
echo ""
echo "Installerer påkrævede pakker"
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
    echo "Arkitektur understøttes ikke"
    exit 1
    ;;
esac
echo ""
echo "Fjerner tidligere tarballs"
# -f for at tvinge, så vi fejler, hvis den ikke findes
rm -f "${app^}".*.tar.gz
echo ""
echo "Downloader..."
wget --content-disposition "$DLURL"
tar -xvzf "${app^}".*.tar.gz
echo ""
echo "Installation af filer er downloadet og udpakket"

# fjern eksisterende installationer
echo "Fjerner eksisterende installation"
# Hvis du tilfældigvis kører dette script i installationsmappen, vil linjen nedenfor slette de udpakkede filer og få mv-linjerne længere nede til at fejle.
rm -rf "$bindir"
echo "Installerer..."
mv "${app^}" $installdir
chown "$app_uid":"$app_guid" -R "$bindir"
chmod 775 "$bindir"
rm -rf "${app^}.*.tar.gz"
# Sørg for, at vi kontrollerer for en opdatering, hvis brugeren installerer en ældre version eller en anden gren
touch "$datadir"/update_required
chown "$app_uid":"$app_guid" "$datadir"/update_required
echo "App installeret"
# Konfigurer autostart

# Fjern eventuel tidligere app .service
echo "Fjerner gammel servicefil"
rm -rf /etc/systemd/system/"$app".service

# Opret app .service med korrekt brugeropstart
echo "Opretter servicefil"
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

# Start appen
echo "Servicefil oprettet. Forsøger at starte appen"
systemctl -q daemon-reload
systemctl enable --now -q "$app"

# Afslut opdatering/installation
host=$(hostname -I)
ip_local=$(grep -oP '^\S*' <<<"$host")
echo ""
echo "Installationen er fuldført"
sleep 10
STATUS="$(systemctl is-active "$app")"
if [ "${STATUS}" = "active" ]; then
    echo "Gå til http://$ip_local:$app_port for ${app^} GUI'en"
else
    echo "${app^} kunne ikke startes"
fi

# Afslut
exit 0

```

- Tryk på <kbd>Ctrl</kbd>+<kbd>O</kbd> (gem) og derefter <kbd>Enter</kbd>
- Tryk på <kbd>Ctrl</kbd>+<kbd>X</kbd> (afslut) og derefter <kbd>Enter</kbd>
- Derefter skal du skrive følgende i din konsol og følge anvisningerne

```shell
sudo bash ArrInstall.sh
```