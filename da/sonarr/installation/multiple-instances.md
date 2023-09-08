---
title: Multiple Instances
description: 
published: true
date: 2023-08-20T02:23:13.676Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:35.847Z
---

# Multiple Instances

Det er muligt at køre flere instanser af Sonarr. Dette gøres typisk, når man ønsker en 4K- og 1080p-kopi af en serie.
[Bemærk, at du kan konfigurere Sonarr til at bruge en anden Sonarr som en liste. Dette er nyttigt, hvis du ønsker at holde begge synkroniserede.](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)

- [Windows Multiple Instances](#windows-multi)
- [Linux Multiple Instances](#linux-multi)
- [Docker Multiple Instances](#docker-multi)
{.links-list}

Følgende krav skal bemærkes:

- Hvis det ikke er Docker, skal de samme binære filer (programfiler) bruges
- Hvis det ikke er Docker, skal alle instanser *skal* have en `-data=` eller `/data=` argument
- Hvis det ikke er Docker, skal der bruges forskellige porte
  - Hvis det er Docker, skal der bruges forskellige eksterne porte
- Der skal bruges forskellige kategorier af downloadklienter
- Der skal bruges forskellige rodmapper.
- Hvis det ikke er Docker, skal automatisk opdatering deaktiveres på alle undtagen 1 instans.

## Windows Multiple Instances

{#windows-multi}

Denne vejledning viser, hvordan du kører flere instanser af Sonarr på Windows ved kun at bruge en grundinstallation. Denne vejledning er lavet med Windows 10; hvis du bruger en tidligere version af Windows (7, 8 osv.), skal du muligvis foretage nogle ændringer. Denne vejledning antager også, at du har installeret Sonarr i standardmappen, og din anden instans af Sonarr vil blive kaldt Sonarr-4K. Du er velkommen til at ændre tingene, så de passer til dine egne installationer.

### Tjeneste (Windows)

#### Forudsætninger (Tjeneste)

- [Du skal allerede have installeret Sonarr](#windows)
- Du skal have [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installeret. For at installere skal du downloade den nyeste version (2.24 på skrivetidspunktet) og kopiere enten den 32-bit eller 64-bit nssm.exe-fil til C:/windows/system32.
  - Hvis du ikke er sikker på, om du har et 32-bit eller 64-bit system, skal du kontrollere Indstillinger => System => Om => Systemtype.

#### Konfiguration af Sonarr-tjeneste

1. Åbn et kommandoprompt-administrationsvindue. (For at køre som administrator skal du højreklikke på kommandoprompt-ikonet og vælge "Kør som administrator".)
1. Hvis Sonarr kører, skal du stoppe tjenesten ved at køre `nssm stop Sonarr` i kommandoprompten.
1. Nu skal vi redigere den eksisterende Sonarr-instans for at pege eksplicit på dens data-mappe. Den standardkommando er som følger: `sc config Sonarr binpath= "C:\ProgramData\Sonarr\bin\Sonarr.exe -data=C:\ProgramData\Sonarr"`

Denne kommando fortæller den oprindelige instans af Sonarr at bruge `C:\ProgramData\Sonarr` som dens data-mappe. Hvis du ikke brugte den standard Sonarr-installation, eller hvis din data-mappe er et andet sted, skal du muligvis ændre dine stier her.

#### Oprettelse af Sonarr-4K-tjeneste

1. Opret en ny mappe, hvor du vil have Sonarr-4K til at være. De fleste bruger et lignende sted som `C:\ProgramData\Sonarr-4K`
1. Tilbage i kommandoprompten skal du oprette den nye Sonarr-4K-tjeneste ved hjælp af `nssm install Sonarr-4K`. Et pop op-vindue åbnes, hvor du kan indtaste dine parametre for den nye instans. Til dette eksempel vil vi bruge følgende:
      - Sti: `C:\ProgramData\Sonarr\bin\Sonarr.exe`
      - Startmappe: `C:\ProgramData\Sonarr\bin`
      - Argumenter: `-data=C:\ProgramData\Sonarr-4K`

> Bemærk, at **Argumenter** peger på den *nye* mappe, der blev oprettet i trin 1.
Dette er afgørende, da det holder alle datafiler fra begge instanser på separate steder. {.is-warning}

1. Klik på *Installer tjeneste*. Vinduet skal lukke, og tjenesten vil nu være tilgængelig til kørsel.
1. Fortsæt til [Konfiguration af Sonarr-4k](#windows-multi-config-second)

### Bakkeapp (Windows)

#### Forudsætninger (Bakkeapp)

- [Du skal allerede have installeret Sonarr](#windows)
- Sonarr skal være konfigureret med et `/data=` argument for at tillade flere instanser
- Gå til opstartsmappe for den aktuelle bruger `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` og rediger den eksisterende genvej om nødvendigt.

#### Oprettelse af Sonarr-4K-bakkeapp

- Højreklik og opret en ny genvej
- Sti: `C:\ProgramData\Sonarr\bin\Sonarr.exe /data=C:\ProgramData\Sonarr-4K`
- Giv genvejen et unikt navn som f.eks. `Sonarr-4K` og afslut guiden.
- Dobbeltklik på den nye genvej for at køre og teste.
- Fortsæt til [Konfiguration af Sonarr-4k](#windows-multi-config-second)

### Konfiguration af Sonarr-4k {#windows-multi-config-second}

- Uanset om du brugte tjenestemetoden eller bakkeappen: Stop begge tjenester og begge apps
- Start Sonarr-4k (tjeneste eller bakkeapp)
- Åbn Sonarr-4k og naviger i appen til [Indstillinger => Generelt => Vært](/sonarr/settings/#host)
- Skift `Portnummer` fra `8989` til en anden port f.eks. `7879`, så Sonarr og Sonarr4k ikke konflikter
- Du bør nu kunne starte begge apps
- Fortsæt til [Håndtering af opdateringer](#dealing-with-updates)

### Håndtering af opdateringer

- Deaktiver automatisk opdatering i en af dine instanser
- Hvis en Sonarr-instans opdateres, lukker begge instanser ned, og kun den opdaterede vil starte igen. For at løse dette skal du manuelt starte den anden instans, eller du kan overveje at bruge følgende PowerShell-script til at løse problemet.

#### PowerShell-script til kontrol og genstart af Windows-port

- Når du bruger to Sonarr-instanser, og en af dem opdateres, vil den lukke alle instanser. Kun den, der opdateres, vil komme online igen.
- Det følgende PowerShell-script skal konfigureres som en planlagt opgave.
- Det kontrollerer porte, og hvis en ikke er online, vil det (gen-)starte den planlagte opgave for at starte Sonarr.

1. Opret en ny fil og navngiv den SonarrInstancesChecker.ps1 med følgende kode.
1. Rediger scriptet med dine faktiske tjenestenavne, IP og porte.
1. [Opret en planlagt opgave](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) for at køre scriptet på en gentagende tidsplan.

- Sikkerhedsoptioner: Aktivér `Kør med højeste privilegier`
  - Ellers vil scriptet ikke kunne manipulere tjenester
- Udløser: `Ved start`
- Gentag opgave hver: `5` eller `10` minutter
- Handling: `Start et program`
- Program/script: `powershell`
- Argument: `-File D:\SonarrInstancesChecker.ps1`
  - Sørg for at bruge den fulde sti til din scripts placering

```powershell
################################################################################################
### SonarrInstancesChecker.ps1                                                               ###
################################################################################################
### Holder flere Sonarr-instanser kørende ved at kontrollere porten                           ###
### Brug Sonarrs Discord eller Reddit til support!                                            ###
### https://wiki.servarr.com/sonarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Opdateret: 2020-10-22                                                                    ###
### Forfatter:  reloxx13                                                                      ###
################################################################################################



### ANGIV DIN KONFIGURATION HER ###
# Angiv din værts-IP og port korrekt og brug dine tjeneste- eller planlagte opgavenavne!

# (string) Typen, som Sonarr starter
# "Service" (standard) Serviceprocessen bruges
# "ScheduledTask" Opgaveplanlæggeren bruges
$startType = 'Service'

# (bool) Skriver loggen til C:\Users\YOURUSERNAME\log.txt, når den er aktiveret
# $false (standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instans 1
        Name = 'Sonarr-V3'; # (string) Tjeneste- eller opgavenavn (standard: Sonarr-V3)
        IP   = '192.168.178.12'; # (string) Server-IP, hvor Sonarr kører (standard: 192.168.178.12)
        Port = '7873'; # (string) Serverport, hvor Sonarr kører (standard: 7873)
    }
    [pscustomobject]@{   # Instans 2
        Name = 'Sonarr-4K'; # (string) Tjeneste- eller opgavenavn (standard: Sonarr-4K)
        IP   = '192.168.178.12'; # (string) Server-IP, hvor Sonarr kører (standard: 192.168.178.12)
        Port = '7874'; # (string) Serverport, hvor Sonarr kører (standard: 7874)
    }
    # Hvis det er nødvendigt, kan du tilføje flere instanser her... ved at fjerne kommentarerne fra nedenstående linjer
    # [pscustomobject]@{   # Instans 3
    # Name='Sonarr-3D';    # (string) Tjeneste- eller opgavenavn (standard: Sonarr-3D)
    # IP='192.168.178.12'; # (string) Server-IP, hvor Sonarr kører (standard: 192.168.178.12)
    # Port='7875';         # (string) Serverport, hvor Sonarr kører (standard: 7875)
    # }
)


### ÆNDRE IKKE NOGET UNDER DENNE LINJE ###


###
# Denne funktion skriver til en logfil eller i konsoloutput
###
function Write-Log
{
    # Skriver til C:\Users\YOURUSERNAME\log.txt
    
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

- [Swizzin-brugere](https://github.com/ComputerByte/sonarr4k)
- Ikke-Swizzin-brugere
  - Sørg for, at din første instans har det `-data=` argument, der er givet.
  - Stop midlertidigt din første instans, så du kan ændre den anden instans' port `systemctl stop sonarr`
  - Deaktiver automatisk opdatering på en af dine Sonarr-instanser

> Nedenfor er et eksempel på et script til oprettelse af en Sonarr4K-instans. Det følgende systemd-oprettelsesscript vil bruge en data-mappe på `/var/lib/sonarr4k/`. Sørg for, at mappen eksisterer, eller ændr den efter behov.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/sonarr4k.service > /dev/null
[Unit]
Description=Sonarr4k Daemon
After=syslog.target network.target
[Service]
User=sonarr
Group=media
Type=simple

ExecStart=mono --debug /usr/lib/sonarr/bin/Sonarr.exe -nobrowser -data=/var/lib/sonarr4k/
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

- Aktivér Sonarr4k-tjenesten:

```shell
sudo systemctl enable --now -q sonarr4k
```

## Docker Multiple Instances

{#docker-multi}

- Start simpelthen en anden Docker-container med et andet navn og sørg for, at ovenstående krav er opfyldt.