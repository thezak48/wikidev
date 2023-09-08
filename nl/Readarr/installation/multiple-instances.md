# Meerdere instanties

Het is mogelijk om meerdere instanties van Readarr uit te voeren. Dit wordt meestal gedaan wanneer je zowel een audioboek- als een ebook-kopie van een boek wilt hebben.
Merk op dat je Readarr kunt configureren om een tweede Readarr als lijst te gebruiken. Dit is handig als je beide gesynchroniseerd wilt houden.

- [Windows meerdere instanties](#windows-multi)
- [Linux meerdere instanties](#linux-multi)
- [MacOS meerdere instanties](#macos-multi)
- [Docker meerdere instanties](#docker-multi)
{.links-list}

De volgende vereisten moeten worden opgemerkt:

- Als het geen Docker is, moeten dezelfde binaries (programmabestanden) worden gebruikt
- Als het geen Docker is, moet aan alle instanties een `-data=` of `/data=` argument worden doorgegeven
- Als het geen Docker is, moeten verschillende poorten worden gebruikt
  - Als het Docker is, moeten verschillende externe poorten worden gebruikt
- Verschillende categorieën voor downloadclients moeten worden gebruikt
- Verschillende hoofdmappen moeten worden gebruikt.
- Als het geen Docker is, schakel automatische updates uit voor alle instanties behalve 1.

## Windows meerdere instanties

{#windows-multi}

Deze handleiding laat zien hoe je meerdere instanties van Readarr kunt uitvoeren op Windows met slechts één basisinstallatie. Deze handleiding is samengesteld met behulp van Windows 10; als je een eerdere versie van Windows (7, 8, enz.) gebruikt, moet je mogelijk enkele aanpassingen doen. Deze handleiding gaat er ook van uit dat je Readarr hebt geïnstalleerd in de standaardmap en dat je tweede instantie van Readarr Readarr-audioboeken wordt genoemd. Voel je vrij om dingen aan te passen aan je eigen installaties.

### Service (Windows)

#### Vereisten (Service)

- [Je moet Readarr al geïnstalleerd hebben](#windows)
- Je moet [NSSM (Non-Sucking Service Manager)](http://nssm.cc) geïnstalleerd hebben. Download de nieuwste release (2.24 op het moment van schrijven) en kopieer het nssm.exe-bestand (32-bits of 64-bits) naar C:/windows/system32.
  - Als je niet zeker weet of je een 32-bits of 64-bits systeem hebt, controleer dan Instellingen => Systeem => Info => Systeemtype.

#### Configuratie van de Readarr-service

1. Open een opdrachtprompt-venster als beheerder. (Klik met de rechtermuisknop op het pictogram van de opdrachtprompt en kies "Als administrator uitvoeren".)
1. Als Readarr actief is, stop dan de service door `nssm stop Readarr` uit te voeren in de opdrachtprompt.
1. Nu moeten we de bestaande Readarr-instantie bewerken om expliciet naar de gegevensmap te verwijzen. De standaardopdracht is als volgt: `sc config Readarr binpath= "C:\ProgramData\Readarr\bin\Readarr.exe -data=C:\ProgramData\Readarr"`

Deze opdracht vertelt de oorspronkelijke instantie van Readarr om expliciet `C:\ProgramData\Readarr` te gebruiken als gegevensmap. Als je de standaardinstallatie van Readarr niet hebt gebruikt, of als je gegevensmap ergens anders staat, moet je hier je paden aanpassen.

#### Aanmaken van de Readarr-audioboeken-service

1. Maak een nieuwe map waar je Readarr-audioboeken wilt plaatsen. De meeste mensen gebruiken een vergelijkbare locatie zoals `C:\ProgramData\Readarr-audioboeken`
1. Ga terug naar de opdrachtprompt en maak de nieuwe Readarr-audioboeken-service met `nssm install Readarr-audioboeken`. Er wordt een pop-upvenster geopend waarin je de parameters voor de nieuwe instantie kunt invoeren. Voor dit voorbeeld gebruiken we het volgende:
      - Pad: `C:\ProgramData\Readarr\bin\Readarr.exe`
      - Opstartmap: `C:\ProgramData\Readarr\bin`
      - Argumenten: `-data=C:\ProgramData\Readarr-audioboeken`

> Let op dat **Argumenten** wijst naar de *nieuwe* map die in stap 1 is gemaakt.
Dit is cruciaal, omdat hiermee alle gegevensbestanden van beide instanties op afzonderlijke locaties worden bewaard. {.is-warning}

1. Klik op *Service installeren*. Het venster wordt gesloten en de service is nu beschikbaar om te worden uitgevoerd.
1. Ga verder naar [Configuratie van Readarr-audioboeken](#windows-multi-config-second)

### Tray-app (Windows)

#### Vereisten (Tray-app)

- [Je moet Readarr al geïnstalleerd hebben](#windows)
- Readarr moet geconfigureerd zijn met een `/data=` argument om meerdere instanties mogelijk te maken
- Ga naar de opstartmap voor de huidige gebruiker `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` en bewerk de bestaande snelkoppeling indien nodig.

#### Aanmaken van de Readarr-audioboeken-tray-app

- Klik met de rechtermuisknop en maak een nieuwe snelkoppeling
- Pad: `C:\ProgramData\Readarr\bin\Readarr.exe /data=C:\ProgramData\Readarr-audioboeken`
- Geef de snelkoppeling een unieke naam zoals `Readarr-audioboeken` en voltooi de wizard.
- Dubbelklik op de nieuwe snelkoppeling om deze uit te voeren en te testen.
- Ga verder naar [Configuratie van Readarr-audioboeken](#windows-multi-config-second)

### Configuratie van Readarr-audioboeken {#windows-multi-config-second}

- Ongeacht of je de servicemethode of de tray-app hebt gebruikt: Stop beide services en beide apps
- Start Readarr-audioboeken (service of tray-app)
- Open Readarr-audioboeken en ga binnen de app naar [Instellingen => Algemeen => Host](/readarr/settings/#host)
- Wijzig het `Poortnummer` van `8787` naar een andere poort, bijvoorbeeld `8879`, zodat Readarr en Readarr-audioboeken niet met elkaar in conflict komen
- Je zou nu beide apps moeten kunnen starten
- Ga verder naar [Omgaan met updates](#dealing-with-updates)

### Omgaan met updates

- Schakel automatische updates uit in één van je instanties
- Als één Readarr-instantie wordt bijgewerkt, worden beide instanties afgesloten en wordt alleen de bijgewerkte instantie opnieuw gestart. Om dit op te lossen, moet je de andere instantie handmatig starten, of je kunt overwegen het onderstaande PowerShell-script te gebruiken om het probleem aan te pakken.

#### Windows Port Checker en Restarter PowerShell-script

{#win-portchecker}

- Wanneer je twee Readarr-instanties gebruikt en één ervan wordt bijgewerkt, worden alle instanties afgesloten. Alleen degene die wordt bijgewerkt, komt weer online.
- Het onderstaande PowerShell-script moet worden geconfigureerd als een geplande taak.
- Het controleert de poorten en als er één niet online is, wordt de geplande taak (opnieuw) gestart om Readarr te starten.

1. Maak een nieuw bestand en noem het ReadarrInstancesChecker.ps1 met de onderstaande code.
1. Bewerk het script met je werkelijke servicenamen, IP en poorten.
1. [Maak een geplande taak aan](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) om het script op een herhalend schema uit te voeren.

- Beveiligingsopties: Schakel `Uitvoeren met hoogste bevoegdheden` in
  - Anders kan het script de services niet manipuleren
- Trigger: `Bij starten`
- Taak elke herhalen: `5` of `10` minuten
- Actie: `Programma starten`
- Programma/script: `powershell`
- Argument: `-File D:\ReadarrInstancesChecker.ps1`
  - Zorg ervoor dat je het volledige pad naar de locatie van je script gebruikt

```powershell
################################################################################################
### ReadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Houdt meerdere Readarr-instanties actief door de poort te controleren                        ###
### Gebruik Readarr's Discord of Reddit voor ondersteuning!                                    ###
### https://wiki.servarr.com/readarr/installation#windows-multi                               ###
################################################################################################
### Versie: 1.1                                                                             ###
### Bijgewerkt: 2020-10-22                                                                      ###
### Auteur:  reloxx13                                                                        ###
################################################################################################



### STEL HIER JE CONFIGURATIE IN ###
# Stel je host-ip en poort correct in en gebruik je servicenamen of geplande taaknamen!

# (string) Het type waarmee Readarr wordt gestart
# "Service" (standaard) er wordt gebruikgemaakt van een servicesproces
# "ScheduledTask" er wordt gebruikgemaakt van de Taakplanner
$startType = 'Service'

# (bool) Schrijft het logboek naar C:\Gebruikers\JOUWGEBRUIKERSNAAM\log.txt wanneer ingeschakeld
# $false (standaard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instantie 1
        Name = 'Readarr'; # (string) Servicenaam of taaknaam (standaard: Readarr)
        IP   = '192.168.178.12'; # (string) IP-adres van de server waarop Readarr wordt uitgevoerd (standaard: 192.168.178.12)
        Port = '8873'; # (string) Poortnummer waarop Readarr wordt uitgevoerd (standaard: 8873)
    }
    [pscustomobject]@{   # Instantie 2
        Name = 'Readarr-audiobooks'; # (string) Servicenaam of taaknaam (standaard: Readarr-audiobooks)
        IP   = '192.168.178.12'; # (string) IP-adres van de server waarop Readarr wordt uitgevoerd (standaard: 192.168.178.12)
        Port = '8874'; # (string) Poortnummer waarop Readarr wordt uitgevoerd (standaard: 8874)
    }
    # Indien nodig kun je hier meer instanties toevoegen... door de onderstaande regels uit te commentariëren
    # [pscustomobject]@{   # Instantie 3
    # Name='Readarr-3D';    # (string) Servicenaam of taaknaam (standaard: Readarr-3D)
    # IP='192.168.178.12'; # (string) IP-adres van de server waarop Readarr wordt uitgevoerd (standaard: 192.168.178.12)
    # Port='8875';         # (string) Poortnummer waarop Readarr wordt uitgevoerd (standaard: 7875)
    # }
)


### WIJZIG NIETS ONDER DEZE REGEL ###


###
# Deze functie schrijft naar een logbestand of naar de console-uitvoer
###
function Write-Log
{
    #Schrijft naar C:\Gebruikers\JOUWGEBRUIKERSNAAM\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    #Console-uitvoer
    Write-Output "[$(TS)]$Message"
    
    #Bestandsuitvoer
    if ($logToFile)
    {
        "[$(TS)]$Message" | Tee-Object -FilePath $Path -Append | Write-Verbose
    }
}


Write-Log 'START ====================='


$instances | ForEach-Object {
    Write-Log "Controleren van $($_.Name) $($_.IP):$($_.Port)"
    
    $PortOpen = ( Test-NetConnection $_.IP -Port $_.Port -WarningAction SilentlyContinue ).TcpTestSucceeded 
    
    if (!$PortOpen)
    {
        Write-Log "Poort $($_.Port) is gesloten, herstart $($startType) $($_.Name)!"

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
            Write-Log '[ERROR] STARTTYPE UNKNOWN! USE Service or ScheduledTask !'
        }
    }
    else
    {
        Write-Log "Poort $($_.Port) is open!"
    }
}

Write-Log 'END ====================='
```

## Linux meerdere instanties

{#linux-multi}

- [Swizzin-gebruikers](https://github.com/ComputerByte/readarr-audiobooks)
- Niet-Swizzin-gebruikers
  - Zorg ervoor dat je eerste instantie het `-data=` argument heeft doorgegeven.
  - Stop tijdelijk je eerste instantie, zodat je de poort van de tweede instantie kunt wijzigen `systemctl stop readarr`
  - Schakel automatische updates uit voor één van je Readarr-instanties

> Hieronder staat een voorbeeldscript om een Readarr-audioboeken-instantie te maken. Het onderstaande systemd-creatie-script gebruikt een gegevensmap van `/var/lib/readarr-audiobooks/`. Zorg ervoor dat de map bestaat of pas deze aan indien nodig.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr-audiobooks.service > /dev/null
[Unit]
Description=Readarr-audiobooks Daemon
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

- Herlaad systemd:

```shell
sudo systemctl -q daemon-reload
```

- Schakel de Readarr-audiobooks-service in:

```shell
sudo systemctl enable --now -q readarr-audiobooks
```

## MacOS meerdere instanties

{#macos-multi}

Deze handleiding is gemaakt en getest met macOS 13 (Ventura), maar zou moeten werken op elke versie die Readarr ondersteunt.

### Vereisten
- De Readarr-applicatie moet geïnstalleerd zijn in de `/Applications`-map
- Als Readarr al eerder is gebruikt, gaan alle gegevens verloren. Verplaats `~/.config/Readarr` naar `~/.config/readarr-books` of `~/.config/readarr-audiobooks` om de gegevens te behouden.

### Aanmaken van applicaties (eenvoudig starten van Readarr)
Je maakt twee nieuwe applicaties: "Readarr Books" en "Readarr Audiobooks".

- Open de Automator-app
- Selecteer `Nieuw document` en vervolgens `Toepassing`
- Gebruik de zoekbalk linksboven om te zoeken naar `Voer shellscript uit` en dubbelklik erop
- Plak het volgende in het geopende vak:

```shell
# Readarr Books
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-books
```



- Sla de applicatie op als `Readarr Books`
- Ga naar `Bestand` > `Dupliceren` in de menubalk
- Vervang de inhoud van het script door het volgende:

```shell
# Readarr Audioboeken
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-audioboeken
```

- Sla de nieuwe applicatie op als `Readarr Audioboeken`
- Bekijk de applicaties in Finder, verander indien gewenst hun pictogrammen (via het `Info`-venster).

### Configuratie van instanties
Nu ga je de poorten en namen instellen voor elke instantie.

- Kies een poortnummer voor elke instantie. Bijvoorbeeld, de standaard `8787` voor e-books en `8789` voor audioboeken.
- Als een van de instanties het standaard poortnummer gebruikt, start dan eerst de andere instantie. Start anders een van hen.
- Ga naar `Instellingen` > `Algemeen` in Readarr en stel de juiste poort in.

> Optioneel: Schakel geavanceerde opties in en stel `Instantienaam` naar wens in.
{.is-success}

- Start de andere instantie en doe hetzelfde.

### Updates
Wanneer je een instantie bijwerkt, worden beide afgesloten en wordt alleen de bijgewerkte instantie opnieuw gestart. Om dit te omzeilen, wordt er een periodieke taak voor het controleren van de poort gemaakt (aangepast maar iets gewijzigd van de [Windows handleiding](#win-portchecker)).

- Schakel automatische updates uit in een van de instanties en zorg ervoor dat je deze nooit bijwerkt.
- Maak een nieuw bestand aan op een plek die je zult onthouden en noem het `readarrportchecker.zsh`.
- Voeg de volgende inhoud toe:

```shell
#!/bin/zsh

# Naam van de eerste instantie van de *applicatie*
name0="Readarr Books"
# Poortnummer van de eerste instantie
port0=8787

# Naam van de tweede instantie van de *applicatie*
name1="Readarr Audioboeken"
# Poortnummer van de tweede instantie
port1=8789

# Logging
LOGFILE="$HOME/.local/state/readarr.log"
test -d "$HOME/.local/state" || mkdir -p "$HOME/.local/state"

function checkport {
    lsof -i ":${1}" &>/dev/null
}

# Als er één instantie actief is, moeten beide actief zijn
if checkport "${port0}" && ! checkport "${port1}"; then
		open -a "${name1}"
    echo "Geopend ${name1}" >> "$LOGFILE"
elif checkport "${port1}" && ! checkport "${port0}"; then
		open -a "${name0}"
    echo "Geopend ${name0}" >> "$LOGFILE"
fi
```

- Maak het script uitvoerbaar:

```shell
chmod +x readarrportchecker.zsh
```

- Plan het script om periodiek uit te voeren. Maak een nieuw bestand aan in `~/Library/LaunchAgents` met de naam `local.readarr.portchecker.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>local.readarr.portchecker</string>
    <key>Program</key>
    <!-- Vind het pad door er met de rechtermuisknop op te klikken, vervolgens Option en kopiëren -->
    <string>/pad/naar/readarrportchecker.zsh</string>
    <key>StartInterval</key>
    <!-- Periodiek interval in seconden. 300 voor vijf minuten,
         600 voor tien minuten. -->
    <integer>300</integer>
  </dict>
</plist>
```

- Pas het bestand aan volgens de opmerkingen
- Log opnieuw in of laad het bestand handmatig:

```shell
launchctl load ~/Library/LaunchAgents/local.readarr.portchecker.plist
```

> `TODO`: mogelijk integreren in een aangepast script voor het updateproces, of bestandswijzigingen observeren in plaats van elke 300 seconden uitvoeren.
{.is-info}

## Docker Meerdere Instanties

{#docker-multi}

- Start eenvoudig een tweede Docker-container met een andere naam, waarbij aan de bovenstaande vereisten wordt voldaan.