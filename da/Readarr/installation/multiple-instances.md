# Flere instanser

Det er muligt at køre flere instanser af Readarr. Dette gøres typisk, når man ønsker en lydbogs- og e-bogs-kopi af en bog.
Bemærk, at du kan konfigurere Readarr til at bruge en anden Readarr som en liste. Dette er nyttigt, hvis du ønsker at holde begge synkroniserede.

- [Windows Multiple Instances](#windows-multi)
- [Linux Multiple Instances](#linux-multi)
- [MacOS Multiple Instances](#macos-multi)
- [Docker Multiple Instances](#docker-multi)
{.links-list}

Følgende krav skal bemærkes:

- Hvis det ikke er Docker, skal de samme binære filer (programfiler) bruges
- Hvis det ikke er Docker, skal alle instanser *skal* have en `-data=` eller `/data=` argument, der sendes
- Hvis det ikke er Docker, skal der bruges forskellige porte
  - Hvis det er Docker, skal der bruges forskellige eksterne porte
- Der skal bruges forskellige kategorier af downloadklienter
- Der skal bruges forskellige rodmappe
- Hvis det ikke er Docker, skal automatisk opdatering deaktiveres på alle undtagen 1 instans.

## Windows Multiple Instances

{#windows-multi}

Denne vejledning viser, hvordan du kører flere instanser af Readarr på Windows ved hjælp af kun en grundinstallation. Denne vejledning blev lavet ved hjælp af Windows 10; hvis du bruger en tidligere version af Windows (7, 8 osv.), skal du muligvis foretage nogle justeringer. Denne vejledning antager også, at du har installeret Readarr i standardmappen, og din anden instans af Readarr vil blive kaldt Readarr-audiobooks. Du er velkommen til at ændre tingene, så de passer til dine egne installationer.

### Tjeneste (Windows)

#### Forudsætninger (Tjeneste)

- [Du skal allerede have installeret Readarr](#windows)
- Du skal have [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installeret. For at installere skal du downloade den nyeste version (2.24 på skrivetidspunktet) og kopiere enten 32-bit eller 64-bit nssm.exe-filen til C:/windows/system32.
  - Hvis du ikke er sikker på, om du har et 32-bit eller 64-bit system, skal du kontrollere Indstillinger => System => Om => Systemtype.

#### Konfiguration af Readarr-tjeneste

1. Åbn et kommandoprompt-administrationsvindue. (For at køre som administrator skal du højreklikke på kommandoprompt-ikonet og vælge "Kør som administrator".)
1. Hvis Readarr kører, skal du stoppe tjenesten ved at køre `nssm stop Readarr` i kommandoprompten.
1. Nu skal vi redigere den eksisterende Readarr-instans for at pege eksplicit på dens data-mappe. Den standardkommando er som følger: `sc config Readarr binpath= "C:\ProgramData\Readarr\bin\Readarr.exe -data=C:\ProgramData\Readarr"`

Denne kommando fortæller den oprindelige instans af Readarr at bruge `C:\ProgramData\Readarr` som dens data-mappe. Hvis du ikke brugte den standard Readarr-installation, eller hvis din data-mappe er et andet sted, skal du muligvis ændre dine stier her.

#### Oprettelse af Readarr-audiobooks-tjeneste

1. Opret en ny mappe, hvor du vil have Readarr-audiobooks til at være. De fleste bruger et lignende sted som `C:\ProgramData\Readarr-audiobooks`
1. Tilbage i kommandoprompten skal du oprette den nye Readarr-audiobooks-tjeneste ved hjælp af `nssm install Readarr-audiobooks`. Et pop op-vindue åbnes, hvor du kan indtaste dine parametre for den nye instans. Til dette eksempel vil vi bruge følgende:
      - Sti: `C:\ProgramData\Readarr\bin\Readarr.exe`
      - Startmappe: `C:\ProgramData\Readarr\bin`
      - Argumenter: `-data=C:\ProgramData\Readarr-audiobooks`

> Bemærk, at **Argumenter** peger på den *nye* mappe, der blev oprettet i trin 1.
Dette er afgørende, da det holder alle datafiler fra begge instanser på separate steder. {.is-warning}

1. Klik på *Installer tjeneste*. Vinduet skal lukke, og tjenesten vil nu være tilgængelig til kørsel.
1. Fortsæt til [Konfiguration af Readarr-audiobooks](#windows-multi-config-second)

### Bakkeapp (Windows)

#### Forudsætninger (Bakkeapp)

- [Du skal allerede have installeret Readarr](#windows)
- Readarr skal konfigureres med et `/data=` argument for at tillade flere instanser
- Gå til opstartsmappe for den aktuelle bruger `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` og rediger den eksisterende genvej om nødvendigt.

#### Oprettelse af Readarr-audiobooks bakkeapp

- Højreklik og opret ny genvej
- Sti: `C:\ProgramData\Readarr\bin\Readarr.exe /data=C:\ProgramData\Readarr-audiobooks`
- Giv genvejen et unikt navn som f.eks. `Readarr-audiobooks` og afslut guiden.
- Dobbeltklik på den nye genvej for at køre og teste.
- Fortsæt til [Konfiguration af Readarr-audiobooks](#windows-multi-config-second)

### Konfiguration af Readarr-audiobooks {#windows-multi-config-second}

- Uanset om du brugte Tjenestemetoden eller Bakkeappen: Stop begge tjenester og begge apps
- Start Readarr-audiobooks (Tjeneste eller Bakkeapp)
- Åbn Readarr-audiobooks og naviger inden for appen til [Indstillinger => Generelt => Vært](/readarr/settings/#host)
- Skift `Portnummer` fra `8787` til en anden port f.eks. `8879`, så Readarr og Readarr-audiobooks ikke konflikter
- Du bør nu kunne starte begge apps
- Fortsæt til [Håndtering af opdateringer](#dealing-with-updates)

### Håndtering af opdateringer

- Deaktiver automatisk opdatering i en af dine instanser
- Hvis en Readarr-instans opdateres, lukker begge instanser ned, og kun den opdaterede starter igen. For at løse dette skal du manuelt starte den anden instans, eller du kan overveje at bruge nedenstående PowerShell-script til at løse problemet.

#### PowerShell-script til Windows-portkontrol og genstart

{#win-portchecker}

- Når du bruger to Readarr-instanser, og en af dem opdateres, vil den lukke alle instanser. Kun den, der opdateres, vil komme online igen.
- Nedenstående PowerShell-script skal konfigureres som en planlagt opgave.
- Det kontrollerer portene, og hvis en ikke er online, vil det (gen-)starte den planlagte opgave for at starte Readarr.

1. Opret en ny fil og navngiv den ReadarrInstancesChecker.ps1 med følgende kode.
1. Rediger scriptet med dine faktiske tjenestenavne, IP og porte.
1. [Opret en planlagt opgave](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) for at køre scriptet på en gentaget tidsplan.

- Sikkerhedsoptioner: Aktivér `Kør med højeste privilegier`
  - Ellers vil scriptet ikke kunne manipulere tjenester
- Udløser: `Ved start`
- Gentag opgave hver: `5` eller `10` minutter
- Handling: `Start et program`
- Program/skript: `powershell`
- Argument: `-File D:\ReadarrInstancesChecker.ps1`
  - Sørg for at bruge den fulde sti til din scripts placering

```powershell
################################################################################################
### ReadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Holder flere Readarr-instanser oppe ved at kontrollere porten                               ###
### Brug Readarrs Discord eller Reddit til support!                                            ###
### https://wiki.servarr.com/readarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Opdateret: 2020-10-22                                                                    ###
### Forfatter:  reloxx13                                                                      ###
################################################################################################



### ANGIV DIN KONFIGURATION HER ###
# Angiv din værts-IP og port korrekt og brug dine tjeneste- eller planlagte opgavenavne!

# (string) Typen, hvorpå Readarr starter
# "Service" (standard) Serviceprocessen bruges
# "ScheduledTask" Opgaveplanlæggeren bruges
$startType = 'Service'

# (bool) Skriver loggen til C:\Users\YOURUSERNAME\log.txt, når den er aktiveret
# $false (standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instans 1
        Name = 'Readarr'; # (string) Tjeneste- eller opgavenavn (standard: Readarr)
        IP   = '192.168.178.12'; # (string) Server-IP, hvor Readarr kører (standard: 192.168.178.12)
        Port = '8873'; # (string) Serverport, hvor Readarr kører (standard: 8873)
    }
    [pscustomobject]@{   # Instans 2
        Name = 'Readarr-audiobooks'; # (string) Tjeneste- eller opgavenavn (standard: Readarr-audiobooks)
        IP   = '192.168.178.12'; # (string) Server-IP, hvor Readarr kører (standard: 192.168.178.12)
        Port = '8874'; # (string) Serverport, hvor Readarr kører (standard: 8874)
    }
    # Hvis det er nødvendigt, kan du tilføje flere instanser her... ved at fjerne kommentarerne fra nedenstående linjer
    # [pscustomobject]@{   # Instans 3
    # Name='Readarr-3D';    # (string) Tjeneste- eller opgavenavn (standard: Readarr-3D)
    # IP='192.168.178.12'; # (string) Server-IP, hvor Readarr kører (standard: 192.168.178.12)
    # Port='8875';         # (string) Serverport, hvor Readarr kører (standard: 7875)
    # }
)


### ÆNDRE IKKE NOGET UNDER DENNE LINJE ###


###
# Denne funktion skriver til en logfil eller i konsoloutput
###
function Write-Log
{
    #Skriver til C:\Users\YOURUSERNAME\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    #Konsoloutput
    Write-Output "[$(TS)]$Message"
    
    #Filoutput
    if ($logToFile)
    {
        "[$(TS)]$Message" | Tee-Object -FilePath $Path -Append | Write-Verbose
    }
}


Write-Log 'START ====================='


$instances | ForEach-Object {
    Write-Log "Kontroller $($_.Name) $($_.IP):$($_.Port)"
    
    $PortOpen = ( Test-NetConnection $_.IP -Port $_.Port -WarningAction SilentlyContinue ).TcpTestSucceeded 
    
    if (!$PortOpen)
    {
        Write-Log "Port $($_.Port) er lukket, genstart $($startType) $($_.Name)!"

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
        Write-Log "Port $($_.Port) er åben!"
    }
}

Write-Log 'END ====================='
```

## Linux Multiple Instances

{#linux-multi}

- [Swizzin-brugere](https://github.com/ComputerByte/readarr-audiobooks)
- Brugere, der ikke bruger Swizzin
  - Sørg for, at din første instans har det `-data=` argument, der sendes.
  - Stop midlertidigt din første instans, så du kan ændre den anden instans' port `systemctl stop readarr`
  - Deaktiver automatisk opdatering på en af dine Readarr-instanser

> Nedenfor er et eksempel på et script til at oprette en Readarr-audiobooks-instans. Det nedenstående systemd-oprettelsesscript vil bruge en data-mappe på `/var/lib/readarr-audiobooks/`. Sørg for, at mappen eksisterer, eller ændr den efter behov.{.is-danger}

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

- Genindlæs systemd:

```shell
sudo systemctl -q daemon-reload
```

- Aktivér Readarr-audiobooks-tjenesten:

```shell
sudo systemctl enable --now -q readarr-audiobooks
```

## MacOS Multiple Instances

{#macos-multi}

Denne vejledning blev lavet og testet med macOS 13 (Ventura), men bør virke på enhver version, som Readarr understøtter.

### Forudsætninger
- Du skal have Readarr-applikationen installeret i `/Applications`-mappen
- Hvis Readarr allerede er blevet brugt før, vil alle data gå tabt. Flyt `~/.config/Readarr` til `~/.config/readarr-books` eller `~/.config/readarr-audiobooks` for at beholde data.

### Oprettelse af applikationer (start Readarr nemt)
Du vil oprette to nye applikationer: "Readarr Books" og "Readarr Audiobooks".

- Åbn Automator-appen
- Vælg `Ny dokument`, og derefter `Applikation`
- Brug søgefeltet øverst til venstre til at søge efter `Kør Shell Script`, og dobbeltklik derefter på det
- I det åbne felt skal du indsætte følgende:

```shell
# Readarr Books
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-books
```



- Gem applikationen som `Readarr Books`
- Gå til `File` > `Duplicate` i menuen
- Erstat indholdet af scriptet med følgende:

```shell
# Readarr Audiobooks
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-audiobooks
```

- Gem den nye applikation som `Readarr Audiobooks`
- Se applikationerne i Finder, og ændr eventuelt deres ikoner efter eget ønske (via `Get Info`-vinduet).

### Konfiguration af instanser
Nu skal du indstille porte og navne for hver instans.

- Vælg et portnummer for hver instans. For eksempel, standardporten `8787` for e-bøger og `8789` for lydbøger.
- Hvis en af instanserne bruger standardportnummeret, skal du starte den anden først. Ellers kan du starte en af dem.
- Gå til `Settings` > `General` i Readarr, og indstil den korrekte port.

> Valgfrit: Aktivér avancerede indstillinger og indstil `Instance Name` efter eget ønske.
{.is-success}

- Start den anden instans, og gør det samme.

### Opdateringer
Når du opdaterer en instans, lukker opdateringsprogrammet begge ned og genstarter kun den, du har opdateret. For at omgå dette, vil der blive oprettet en periodisk opgave til portkontrol (tilpasset, men let ændret fra [Windows-guiden](#win-portchecker)).

- Deaktiver automatisk opdatering i en af instanserne, og sørg for aldrig at opdatere den.
- Opret en ny fil et sted, du kan huske, og kald den `readarrportchecker.zsh`.
- Tilføj følgende indhold:

```shell
#!/bin/zsh

# Første instans' *applikationsnavn*
name0="Readarr Books"
# Første instans' portnummer
port0=8787

# Anden instans' *applikationsnavn*
name1="Readarr Audiobooks"
# Anden instans' portnummer
port1=8789

# Logging
LOGFILE="$HOME/.local/state/readarr.log"
test -d "$HOME/.local/state" || mkdir -p "$HOME/.local/state"

function checkport {
    lsof -i ":${1}" &>/dev/null
}

# Hvis en instans kører, skal begge køre
if checkport "${port0}" && ! checkport "${port1}"; then
		open -a "${name1}"
    echo "Åbnede ${name1}" >> "$LOGFILE"
elif checkport "${port1}" && ! checkport "${port0}"; then
		open -a "${name0}"
    echo "Åbnede ${name0}" >> "$LOGFILE"
fi
```

- Gør scriptet eksekverbart:

```shell
chmod +x readarrportchecker.zsh
```

- Planlæg, at scriptet skal køre periodisk. Opret en ny fil i `~/Library/LaunchAgents` med navnet `local.readarr.portchecker.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>local.readarr.portchecker</string>
    <key>Program</key>
    <!-- Find stien ved at højreklikke, derefter Option og kopier -->
    <string>/sti/til/readarrportchecker.zsh</string>
    <key>StartInterval</key>
    <!-- Periodisk interval i sekunder. 300 for fem minutter,
         600 for ti minutter. -->
    <integer>300</integer>
  </dict>
</plist>
```

- Rediger filen i henhold til kommentarerne
- Log ind igen eller indlæs filen manuelt:

```shell
launchctl load ~/Library/LaunchAgents/local.readarr.portchecker.plist
```

> `TODO`: Muligvis integrer dette i en brugerdefineret script til opdateringsprocessen eller observer filændringer i stedet for at køre hvert 300. sekund.
{.is-info}

## Docker Flere Instanser

{#docker-multi}

- Start simpelthen en anden Docker-container med et andet navn og sørg for, at ovenstående krav er opfyldt.