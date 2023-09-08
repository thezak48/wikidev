---
title: *Arr Installasjonsskript
description: Felles installasjonsskript for *Arr-pakken med applikasjoner
published: true
date: 2023-07-14T12:19:34.383Z
tags: 
editor: markdown
dateCreated: 2022-02-03T15:12:29.483Z
---

# \*Arr Installasjonsskript

Dette er et samfunnsopprettet og samfunnsstøttet **uoffisielt** skript for å håndtere installasjon av Lidarr/Prowlarr/Radarr/Readarr/Whisparr på et Linux-operativsystem - vanligvis rettet mot Debian og Ubuntu eller lignende distribusjoner.

> Dette vil installere den valgte applikasjonen til /opt. Den vil kjøre applikasjonen som brukeren og gruppen du konfigurerer.
> For Lidarr/Radarr/Readarr/Whisparr - bør du bruke en felles gruppe som er den samme som din nedlastingsklient kjører som og medieserveren kjører som for å sikre at eierskap og tillatelser er fornuftige og at alle filer er tilgjengelige.
{.is-info}

Vær oppmerksom på følgende vanlige feil angående tillatelser.

> To ting å huske er at Lidarr/Radarr/Readarr/Whisparr krever lese- og skrivetilgang til nedlastingsklientens nedlastingskatalog og hvilken som helst mappe du konfigurerer som rot (bibliotek eller medie) mappe.
> Ideelt sett kjører hver app som sin egen bruker og felles gruppe `media` med tillatelser `775` og `664`, som er en UMask på `002`.
> \* Nedlastingsklientene og medieserveren kjører som og er en del av gruppen du angir
> \* Stiene som brukes av nedlastingsklientene og medieserveren er tilgjengelige (lese/skrive) for gruppen du angir
{.is-warning}

Vær oppmerksom på følgende:

> Dette vil fjerne eventuelle eksisterende installasjoner som er installert i /opt. Den vil ikke avinstallere eksisterende installasjoner fra noen annen plassering; sørg for at du har en sikkerhetskopi av innstillingene dine ved å bruke Sikkerhetskopi fra appen (System => Sikkerhetskopi). Skriptet vil ikke slette innstillingene dine (applikasjonsdata), men vær på den sikre siden.
{.is-danger}

- (Valgfritt) Sørg for at du har [satt en statisk IP-adresse](https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/), det vil gjøre livet ditt enklere.
- SSH inn i Debian (Raspbian / Raspberry Pi OS) / Ubuntu-boksen din og bli eller logg inn som root.

> SSH inn ved hjelp av Putty, mRemoteNG eller et annet SSH-verktøy. Merk at de fleste verktøy støtter å lagre tilkoblingen din.{.is-info}

- Når du er SSHet inn, skriv inn følgende for å opprette installasjonsskriptet i gjeldende mappe

```bash
nano ArrInstall.sh
```

- Kopier (øverst til høyre i skriptet) og lim inn i SSH-konsollen. Gjennomgå variablene med kommentarer og oppdater om nødvendig.
  - Hvis du er i et GUI-operativsystem som Windows eller MacOS (OSX): lim inn kan være like enkelt som å 'høyreklikke' i SSH-klienten din.

```bash
#!/bin/bash
### Beskrivelse: \*Arr .NET Debian-installasjon
### Opprinnelig skrevet for Radarr av: DoctorArr - doctorarr@the-rowlands.co.uk den 2021-10-01 v1.0
### Versjon v1.1 2021-10-02 - Bakerboy448 (Gjort mer generisk og konformant)
### Versjon v1.1.1 2021-10-02 - DoctorArr (Stavekontroll og maloppdatering)
### Versjon v2.0.0 2021-10-09 - Bakerboy448 (Omskrevet og sikret at skriptet er generisk. Lagt til flere variabler.)
### Versjon v2.0.1 2021-11-23 - brightghost (Fikset datadir-trinn for å bruke riktige variabler.)
### Versjon v3.0.0 2022-02-03 - Bakerboy448 (Omskrevet skript for å be om bruker/gruppe og gjort det generisk for alle \*Arrs)
### Versjon v3.0.1 2022-02-05 - aeramor (skrivefeil rettet linje 179: 'chown "$app_uid":"$app_uid" -R "$bindir"' -> 'chown "$app_uid":"$app_guid" -R "$bindir"')
### Versjon v3.0.3 2022-02-06 - Bakerboy448 fikse eierskap
### Versjon v3.0.3a Readarr til utvikling
### Versjon v3.0.4 2022-03-01 - Legg til sleep før sjekk av tjenestestatus
### Versjon v3.0.5 2022-04-03 - VP-EN (Lagt til Whisparr)
### Versjon v3.0.6 2022-04-26 - Bakerboy448 - binærer til gruppe
### Versjon v3.0.7 2023-01-05 - Bakerboy448 - Prowlarr til master
### Versjon v3.0.8 2023-04-20 - Bakerboy448 - Shellcheck-fikser og fjern tidligere tarballs
### Versjon v3.0.9 2023-04-28 - Bakerboy448 - fiks tarball-sjekk
### Versjon v3.0.9a 2023-07-14 - DoctorArr - oppdatert skriptversjon og skriptdato og for å se hvordan dette går! Det var fortsatt på v3.0.8.
### Flere oppdateringer av: \*Arr-samfunnet

### Malvarsel
#PROGRAMVAREN LEVERES "SOM DEN ER", UTEN GARANTI FOR NOE SLAG,
#UTTRYKT ELLER UNDERFORSTÅTT, INKLUDERT MEN IKKE BEGRENSET TIL GARANTIER FOR
#SALGBARHET, EGNETHET FOR ET BESTEMT FORMÅL OG
#IKKE-KRENKELSE. UNDER INGEN OMSTENDIGHETER SKAL OPPHAVSRETTSEIERNE ELLER RETTIGHETSHAVERNE VÆRE
#ANSVARLIGE FOR NOEN KRAV, SKADER ELLER ANDRE ANSVAR, ENTEN I EN KONTRAKTSMESSIG
#HANDLING, TORT ELLER PÅ ANNEN MÅTE, SOM FØLGE AV, UT AV ELLER I FORBINDELSE
#MED PROGRAMVAREN ELLER BRUKEN ELLER ANDRE HANDLINGER I PROGRAMVAREN.

skriptversjon="3.0.9a"
skriptdato="2023-07-14"

set -euo pipefail

echo "Kjører \*Arr Installasjonsskript - Versjon [$skriptversjon] fra [$skriptdato]"

# Er jeg root?, trenger root!

if [ "$EUID" -ne 0 ]; then
    echo "Vennligst kjør som root."
    exit
fi

echo "Velg applikasjonen du vil installere: "

select app in lidarr prowlarr radarr readarr whisparr quit; do

    case $app in
    lidarr)
        app_port="8686"                                          # Standard app-port; Endre config.xml etter installasjonen om nødvendig
        app_prereq="curl sqlite3 libchromaprint-tools mediainfo" # Nødvendige pakker
        app_umask="0002"                                         # UMask som tjenesten vil kjøre som
        branch="master"                                          # {Oppdater meg om nødvendig} gren for installasjon
        break
        ;;
    prowlarr)
        app_port="9696"           # Standard app-port; Endre config.xml etter installasjonen om nødvendig
        app_prereq="curl sqlite3" # Nødvendige pakker
        app_umask="0002"          # UMask som tjenesten vil kjøre som
        branch="master"          # {Oppdater meg om nødvendig} gren for installasjon
        break
        ;;
    radarr)
        app_port="7878"           # Standard app-port; Endre config.xml etter installasjonen om nødvendig
        app_prereq="curl sqlite3" # Nødvendige pakker
        app_umask="0002"          # UMask som tjenesten vil kjøre som
        branch="master"           # {Oppdater meg om nødvendig} gren for installasjon
        break
        ;;
    readarr)
        app_port="8787"           # Standard app-port; Endre config.xml etter installasjonen om nødvendig
        app_prereq="curl sqlite3" # Nødvendige pakker
        app_umask="0002"          # UMask som tjenesten vil kjøre som
        branch="develop"          # {Oppdater meg om nødvendig} gren for installasjon
        break
        ;;
    whisparr)
        app_port="6969"           # Standard app-port; Endre config.xml etter installasjonen om nødvendig
        app_prereq="curl sqlite3" # Nødvendige pakker
        app_umask="0002"          # UMask som tjenesten vil kjøre som
        branch="nightly"          # {Oppdater meg om nødvendig} gren for installasjon
        break
        ;;
    quit)
        exit 0
        ;;
    *)
        echo "Ugyldig valg $REPLY"
        ;;
    esac
done

# Konstanter
### Oppdater disse variablene etter behov for din spesifikke installasjon
installdir="/opt"              # {Oppdater meg om nødvendig} Installasjonssted
bindir="${installdir}/${app^}" # Full bane til installasjonsstedet
datadir="/var/lib/$app/"       # {Oppdater meg om nødvendig} AppData-katalogen som skal brukes
app_bin=${app^}                # Binærnavn for appen

if [[ $app != 'prowlarr' ]]; then
    echo "Det er viktig at brukeren og gruppen du velger å kjøre ${app^} som, har LESE- og SKRIVETILGANG til mediebiblioteket ditt og fullførte nedlastingskataloger for nedlastingsklienten."
fi

# Be brukeren om informasjon
read -r -p "Hvilken bruker skal ${app^} kjøre som? (Standard: $app): " app_uid
app_uid=$(echo "$app_uid" | tr -d ' ')
app_uid=${app_uid:-$app}
# Be om gruppe
read -r -p "Hvilken gruppe skal ${app^} kjøre som? (Standard: media): " app_guid
app_guid=$(echo "$app_guid" | tr -d ' ')
app_guid=${app_guid:-media}

echo "${app^} valgt"
echo "Dette vil installere [${app^}] til [$bindir] og bruke [$datadir] som AppData-katalogen"
if [[ $app == 'prowlarr' ]]; then
    echo "${app^} vil kjøre som brukeren [$app_uid] og gruppen [$app_guid]."
else
    echo "${app^} vil kjøre som brukeren [$app_uid] og gruppen [$app_guid]. Ved å fortsette, har du bekreftet at denne brukeren og gruppen vil ha LESE- og SKRIVETILGANG til mediebiblioteket ditt og fullførte nedlastingskataloger for nedlastingsklienten."
fi
echo "Fortsette med installasjonen [Ja/Nei]?"
select yn in "Ja" "Nei"; do
    case $yn in
    Ja) break ;;
    Nei) exit 0 ;;
    esac
done

# Opprett bruker/gruppe hvis nødvendig
if [ "$app_guid" != "$app_uid" ]; then
    if ! getent group "$app_guid" >/dev/null; then
        groupadd "$app_guid"
    fi
fi
if ! getent passwd "$app_uid" >/dev/null; then
    adduser --system --no-create-home --ingroup "$app_guid" "$app_uid"
    echo "Opprettet og lagt til bruker [$app_uid] i gruppen [$app_guid]"
fi
if ! getent group "$app_guid" | grep -qw "$app_uid"; then
    echo "Brukeren [$app_uid] eksisterte ikke i gruppen [$app_guid]"
    usermod -a -G "$app_guid" "$app_uid"
    echo "Lagt til bruker [$app_uid] i gruppen [$app_guid]"
fi

# Stopp appen hvis den kjører
if service --status-all | grep -Fq "$app"; then
    systemctl stop "$app"
    systemctl disable "$app".service
    echo "Stoppet eksisterende $app"
fi

# Opprett Appdata-katalog

# AppData
mkdir -p "$datadir"
chown -R "$app_uid":"$app_guid" "$datadir"
chmod 775 "$datadir"
echo "Mapper opprettet"
# Last ned og installer appen

# Nødvendige pakker
echo ""
echo "Installerer nødvendige pakker"
# shellcheck disable=SC2086
apt update && apt install $app_prereq
echo ""
ARCH=$(dpkg --print-architecture)
# Hent arkitektur
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo "Arkitektur støttes ikke"
    exit 1
    ;;
esac
echo ""
echo "Fjerner tidligere tarballs"
# -f for å tvinge, slik at vi feiler hvis den ikke eksisterer
rm -f "${app^}".*.tar.gz
echo ""
echo "Laster ned..."
wget --content-disposition "$DLURL"
tar -xvzf "${app^}".*.tar.gz
echo ""
echo "Installasjonsfiler lastet ned og pakket ut"

# Fjern eksisterende installasjoner
echo "Fjerner eksisterende installasjon"
# Hvis du tilfeldigvis kjører dette skriptet i installasjonsmappen, vil linjen nedenfor slette de pakkede filene og føre til at mv noen linjer nedenfor mislykkes.
rm -rf "$bindir"
echo "Installerer..."
mv "${app^}" $installdir
chown "$app_uid":"$app_guid" -R "$bindir"
chmod 775 "$bindir"
rm -rf "${app^}.*.tar.gz"
# Sørg for at vi sjekker for en oppdatering i tilfelle brukeren installerer en eldre versjon eller en annen gren
touch "$datadir"/update_required
chown "$app_uid":"$app_guid" "$datadir"/update_required
echo "App installert"
# Konfigurer automatisk oppstart

# Fjern eventuell tidligere app .service
echo "Fjerner gammel tjenestefil"
rm -rf /etc/systemd/system/"$app".service

# Opprett app .service med riktig brukeroppstart
echo "Oppretter tjenestefil"
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
echo "Tjenestefil opprettet. Prøver å starte appen"
systemctl -q daemon-reload
systemctl enable --now -q "$app"

# Fullfør oppdatering/installasjon
host=$(hostname -I)
ip_local=$(grep -oP '^\S*' <<<"$host")
echo ""
echo "Installering fullført"
sleep 10
STATUS="$(systemctl is-active "$app")"
if [ "${STATUS}" = "active" ]; then
    echo "Gå til http://$ip_local:$app_port for ${app^} GUI"
else
    echo "${app^} kunne ikke startes"
fi

# Avslutt
exit 0

```

- Trykk på <kbd>Ctrl</kbd>+<kbd>O</kbd> (lagre) og deretter <kbd>Enter</kbd>
- Trykk på <kbd>Ctrl</kbd>+<kbd>X</kbd> (avslutt) og deretter <kbd>Enter</kbd>
- Deretter skriver du følgende i konsollen og følger instruksjonene

```shell
sudo bash ArrInstall.sh
```