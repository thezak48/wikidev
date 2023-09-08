---
title: Multiple instanser
description: 
published: true
date: 2023-09-01T05:05:47.102Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:10.189Z
---

# Multiple Instances

Det er muligt at køre flere instanser af Radarr. Dette gøres typisk, når man ønsker en 4K- og en 1080p-kopi af en film. Bemærk, at du kan (og sandsynligvis bør) [gennemgå TRaSH's guide og konfigurere Radarr til at bruge en anden Radarr som en liste](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/). Dette er nyttigt, hvis du ønsker at holde begge synkroniserede.

- [Windows Multiple Instances](#windows-multi)
- [Linux Multiple Instances](#linux-multi)
- [Docker Multiple Instances](#docker-multi)
{.links-list}

Følgende krav skal bemærkes:

- Hvis det ikke er Docker, skal de samme binære filer (programfiler) bruges
- Hvis det ikke er Docker, skal alle instanser *skal* have et `-data=` eller `/data=` argument angivet
- Hvis det ikke er Docker, skal der bruges forskellige porte
  - Hvis det er Docker, skal der bruges forskellige eksterne porte
- Der skal bruges forskellige kategorier af downloadklienter
- Der skal bruges forskellige rodmapper.
- Hvis det ikke er Docker, skal automatisk opdatering deaktiveres på alle undtagen én instans.

## Windows Multiple Instances

{#windows-multi}

Denne vejledning viser, hvordan du kører flere instanser af Radarr på Windows ved kun at bruge én grundinstallation. Denne vejledning er udarbejdet ved hjælp af Windows 10; hvis du bruger en tidligere version af Windows (7, 8 osv.), skal du muligvis foretage nogle ændringer. Denne vejledning antager også, at du har installeret Radarr i standardmappen, og at din anden instans af Radarr vil blive kaldt Radarr-4K. Du er velkommen til at ændre tingene, så de passer til dine egne installationer.

> Bemærk: Du skal køre Radarr som **enten** [en tjeneste](#service-windows) eller som en [bakkeapp](#tray-app-windows). Det er unødvendigt og kan forårsage problemer at køre både en app og en tjeneste.

### Tjeneste (Windows)

#### Forudsætninger (Tjeneste)

- [Du skal allerede have installeret Radarr](#windows)
- Du skal have [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installeret. For at installere det skal du downloade den nyeste version (2.24 på tidspunktet for skrivningen) og kopiere enten den 32-bit eller 64-bit nssm.exe-fil til C:/windows/system32.
  - Hvis du er i tvivl om, hvorvidt du har et 32-bit eller 64-bit system, kan du tjekke Indstillinger => System => Om => Systemtype.

#### Konfiguration af Radarr-tjeneste

1. Åbn et kommandoprompt-administrationsvindue. (For at køre som administrator skal du højreklikke på kommandoprompt-ikonet og vælge "Kør som administrator".)
1. Hvis Radarr kører, skal du stoppe tjenesten ved at køre `nssm stop Radarr` i kommandoprompten.
1. Nu skal vi redigere den eksisterende Radarr-instans for at pege eksplicit på dens data-mappe. Den standardkommando er som følger: `sc config Radarr binpath= "C:\ProgramData\Radarr\bin\Radarr.exe -data=C:\ProgramData\Radarr"`

Denne kommando fortæller den oprindelige instans af Radarr at bruge `C:\ProgramData\Radarr` som dens data-mappe. Hvis du ikke brugte den standard Radarr-installation, eller hvis din data-mappe er et andet sted, skal du muligvis ændre dine stier her.

#### Oprettelse af Radarr-4K-tjeneste

1. Opret en ny mappe, hvor du vil have Radarr-4K til at være. De fleste bruger et lignende sted som f.eks. `C:\ProgramData\Radarr-4K`
1. Tilbage i kommandoprompten skal du oprette den nye Radarr-4K-tjeneste ved hjælp af `nssm install Radarr-4K`. Et pop op-vindue åbnes, hvor du kan indtaste dine parametre for den nye instans. Til dette eksempel vil vi bruge følgende:
      - Sti: `C:\ProgramData\Radarr\bin\Radarr.exe`
      - Startmappe: `C:\ProgramData\Radarr\bin`
      - Argumenter: `-data=C:\ProgramData\Radarr-4K`
      - Fanebladet Exit Actions
        - Genstart: Genstart program
        - Forsinkelse: 120000 ms
        (2 minutter, kan være længere, hvis opdateringen ikke fuldføres i tide)

> Bemærk, at **Argumenter** peger på den *nye* mappe, der blev oprettet i trin 1.
Dette er afgørende, da det holder alle datafiler fra begge instanser på separate steder. {.is-warning}

1. Klik på *Installer tjeneste*. Vinduet lukkes, og tjenesten vil nu være tilgængelig til kørsel.
1. Fortsæt til [Konfiguration af Radarr-4k](#windows-multi-config-second)

### Bakkeapp (Windows)

#### Forudsætninger (Bakkeapp)

- [Du skal allerede have installeret Radarr](#windows)
- Radarr-genvejen skal konfigureres med et `/data=` argument i feltet 'target' for at tillade flere instanser
- Gå til opstartsmappe for den aktuelle bruger `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` og rediger den eksisterende genvej, hvis det er nødvendigt.

#### Oprettelse af Radarr-4K-bakkeapp

- Opret en ny mappe til Radarr-4K's konfigurationsfiler. De fleste bruger et lignende sted som f.eks. `C:\ProgramData\Radarr-4K`
- Højreklik og opret en ny genvej
- Sti: `C:\ProgramData\Radarr\bin\Radarr.exe /data=C:\ProgramData\Radarr-4K`
- Giv genvejen et unikt navn som f.eks. `Radarr-4K` og afslut guiden.
- Dobbeltklik på den nye genvej for at køre og teste.
- Fortsæt til [Konfiguration af Radarr-4k](#windows-multi-config-second)

### Konfiguration af Radarr-4k {#windows-multi-config-second}

- Uanset om du brugte tjenestemetoden eller bakkeappen: Stop begge tjenester og begge apps
- Start Radarr-4k (tjeneste eller bakkeapp)
- Åbn Radarr-4k og naviger i appen til [Indstillinger => Generelt => Vært](/radarr/settings/#host)
- Skift `Portnummer` fra `7878` til en anden port f.eks. `7879`, så Radarr og Radarr4k ikke konflikter
- Nu skal du kunne starte begge apps
- Fortsæt til [Håndtering af opdateringer](#dealing-with-updates)

### Håndtering af opdateringer

> - Deaktiver automatisk opdatering i en af dine instanser
  - I config.xml skal du ændre opdateringsgrenen til `<Branch>nonexistent</Branch>`
- Hvis en Radarr-instans opdateres, lukker begge instanser ned, og kun den opdaterede vil starte igen. For at løse dette skal du manuelt starte den anden instans, eller du kan overveje at bruge nedenstående PowerShell-script til at løse problemet.

> Hvis [NSSM Exit Action](#creating-radarr-4k-service) er konfigureret korrekt, kan Radarr opdatere og genstarte flere instanser uden yderligere scripts.
Hvis genstartsforsinkelsen ikke er konfigureret som standard, vil instansen genstarte med det samme.
Dette kan forhindre, at opdateringer anvendes, og kan resultere i følgende fejl "Radarr blev genstartet for tidligt af en ekstern proces."
{.is-info}

#### PowerShell-script til kontrol og genstart af porte i Windows

- Når du bruger to Radarr-instanser, og en af dem opdateres, vil den lukke alle instanser. Kun den, der opdateres, vil komme online igen.
- Nedenstående PowerShell-script skal konfigureres som en planlagt opgave.
- Det kontrollerer portene, og hvis en ikke er online, vil det (gen-)starte den planlagte opgave for at starte Radarr.

1. Opret en ny fil og navngiv den RadarrInstancesChecker.ps1 med følgende kode.
1. Rediger scriptet med dine faktiske tjenestenavne, IP og porte. *Hvis du kører i bakke-tilstand, skal du oprette planlagte opgaver for at starte hver Radarr-instans og bruge de opgavenavne i nedenstående script.*
1. [Opret en planlagt opgave](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) for at køre scriptet med jævne mellemrum.

- Sikkerhedsoptioner: Aktivér `Kør med højeste privilegier`
  - Ellers vil scriptet ikke kunne manipulere tjenester
- Udløser: `Ved start`
- Gentag opgave hver: `5` eller `10` minutter
- Handling: `Start et program`
- Program/skript: `powershell`
- Argument: `-File D:\RadarrInstancesChecker.ps1`
  - Sørg for at bruge den fulde sti til din scripts placering

```powershell
################################################################################################
### RadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Holder flere Radarr-instanser kørende ved at kontrollere porten                            ###
### Brug Radarr's Discord eller Reddit til support!                                           ###
### https://wiki.servarr.com/radarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Opdateret: 2020-10-22                                                                    ###
### Forfatter:  reloxx13                                                                      ###
################################################################################################



### INDSTIL DIN KONFIGURATION HER ###
# Indstil din værts-IP og port korrekt og brug dit tjeneste- eller planlagte opgavenavn!

# (string) Typen, hvorpå Radarr startes
# "Service" (standard) Serviceprocessen bruges
# "ScheduledTask" Opgaveplanlæggeren bruges
$startType = 'Service'

# (bool) Skriver loggen til C:\Users\DITBRUGERNAVN\log.txt, når den er aktiveret
# $false (standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instans 1
        Name = 'Radarr-V3'; # (string) Tjeneste- eller opgavenavn (standard: Radarr-V3)
        IP   = '192.168.178.12'; # (string) Server-IP, hvor Radarr kører (standard: 192.168.178.12)
        Port = '7873'; # (string) Serverport, hvor Radarr kører (standard: 7873)
    }
    [pscustomobject]@{   # Instans 2
        Name = 'Radarr-4K'; # (string) Tjeneste- eller opgavenavn (standard: Radarr-4K)
        IP   = '192.168.178.12'; # (string) Server-IP, hvor Radarr kører (standard: 192.168.178.12)
        Port = '7874'; # (string) Serverport, hvor Radarr kører (standard: 7874)
    }
    # Hvis det er nødvendigt, kan du tilføje flere instanser her... ved at fjerne kommenteringen fra nedenstående linjer
    # [pscustomobject]@{   # Instans 3
    # Name='Radarr-3D';    # (string) Tjeneste- eller opgavenavn (standard: Radarr-3D)
    # IP='192.168.178.12'; # (string) Server-IP, hvor Radarr kører (standard: 192.168.178.12)
    # Port='7875';         # (string) Serverport, hvor Radarr kører (standard: 7875)
    # }
)


### ÆNDRE IKKE NOGET UNDER DENNE LINJE ###


###
# Denne funktion skriver til en logfil eller i konsoloutput
###
function Write-Log
{
    # Skriver til C:\Users\DITBRUGERNAVN\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    # Konsoloutput
    Write-Output "[$(TS)]$Message"
    
    # Filoutput
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

- [Swizzin-brugere](https://github.com/ComputerByte/radarr4k)
- Brugere, der ikke bruger Swizzin
  - Sørg for, at din første instans har det `-data=` argument, der er angivet.
  - Stop midlertidigt din første instans, så du kan ændre den anden instans' port `systemctl stop radarr`
  - Deaktiver automatisk opdatering på en af dine Radarr-instanser

> Nedenfor er et eksempel på et script til oprettelse af en Radarr4K-instans. Det nedenstående systemd-oprettelsesscript vil bruge en data-mappe på `/var/lib/radarr4k/`. Sørg for, at mappen eksisterer, eller ændr den efter behov.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/radarr4k.service > /dev/null
[Unit]
Description=Radarr4k Daemon
After=syslog.target network.target
[Service]
User=radarr
Group=media
Type=simple

ExecStart=/opt/Radarr/Radarr -nobrowser -data=/var/lib/radarr4k/
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

- Aktivér Radarr4k-tjenesten:

```shell
sudo systemctl enable --now -q radarr4k
```

## Docker flere instanser

{#docker-multi}

- Start simpelthen en anden Docker-container op med et andet navn og sørg for, at ovenstående krav er opfyldt.