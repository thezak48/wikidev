---
title: Meerdere instanties
description: 
published: true
date: 2023-08-20T02:23:13.676Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:35.847Z
---

# Meerdere instanties

Het is mogelijk om meerdere instanties van Sonarr uit te voeren. Dit wordt meestal gedaan wanneer je een 4K- en 1080p-kopie van een serie wilt hebben.
[Merk op dat je Sonarr kunt configureren om een tweede Sonarr als lijst te gebruiken. Dit is handig als je beide gesynchroniseerd wilt houden.](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)

- [Meerdere instanties op Windows](#windows-multi)
- [Meerdere instanties op Linux](#linux-multi)
- [Meerdere instanties met Docker](#docker-multi)
{.links-list}

De volgende vereisten moeten worden opgemerkt:

- Als je geen Docker gebruikt, moeten dezelfde binaries (programmabestanden) worden gebruikt.
- Als je geen Docker gebruikt, moeten alle instanties *verplicht* een `-data=` of `/data=` argument doorgeven.
- Als je geen Docker gebruikt, moeten verschillende poorten worden gebruikt.
  - Als je Docker gebruikt, moeten verschillende externe poorten worden gebruikt.
- Verschillende categorieën voor downloadclients moeten worden gebruikt.
- Verschillende hoofdmappen moeten worden gebruikt.
- Als je geen Docker gebruikt, schakel dan automatische updates uit voor alle instanties behalve één.

## Meerdere instanties op Windows

{#windows-multi}

Deze handleiding laat zien hoe je meerdere instanties van Sonarr kunt uitvoeren op Windows met slechts één basisinstallatie. Deze handleiding is samengesteld met behulp van Windows 10; als je een eerdere versie van Windows gebruikt (7, 8, enz.), moet je mogelijk enkele aanpassingen doen. Deze handleiding gaat er ook vanuit dat je Sonarr hebt geïnstalleerd in de standaardmap en dat je tweede instantie van Sonarr Sonarr-4K zal heten. Voel je vrij om dingen aan te passen aan je eigen installaties.

### Service (Windows)

#### Vereisten (Service)

- [Je moet Sonarr al geïnstalleerd hebben](#windows)
- Je moet [NSSM (Non-Sucking Service Manager)](http://nssm.cc) geïnstalleerd hebben. Download de nieuwste release (2.24 op het moment van schrijven) en kopieer het nssm.exe-bestand (32-bits of 64-bits) naar C:/windows/system32.
  - Als je niet zeker weet of je een 32-bits of 64-bits systeem hebt, controleer dan Instellingen => Systeem => Info => Systeemtype.

#### Configuratie van Sonarr-service

1. Open een opdrachtpromptvenster als beheerder. (Klik met de rechtermuisknop op het pictogram van de opdrachtprompt en kies "Als administrator uitvoeren".)
1. Als Sonarr actief is, stop dan de service door `nssm stop Sonarr` uit te voeren in de opdrachtprompt.
1. Nu moeten we de bestaande Sonarr-instantie bewerken om expliciet naar de gegevensmap te verwijzen. Het standaardcommando is als volgt: `sc config Sonarr binpath= "C:\ProgramData\Sonarr\bin\Sonarr.exe -data=C:\ProgramData\Sonarr"`

Dit commando vertelt de oorspronkelijke instantie van Sonarr om expliciet `C:\ProgramData\Sonarr` te gebruiken als gegevensmap. Als je de standaardinstallatie van Sonarr niet hebt gebruikt, of als je gegevensmap ergens anders staat, moet je hier je paden aanpassen.

#### Aanmaken van Sonarr-4K-service

1. Maak een nieuwe map waar je Sonarr-4K wilt hebben. De meeste mensen gebruiken een vergelijkbare locatie zoals `C:\ProgramData\Sonarr-4K`.
1. Ga terug naar de opdrachtprompt en maak de nieuwe Sonarr-4K-service aan met `nssm install Sonarr-4K`. Er wordt een pop-upvenster geopend waarin je de parameters voor de nieuwe instantie kunt invoeren. Voor dit voorbeeld gebruiken we het volgende:
   - Pad: `C:\ProgramData\Sonarr\bin\Sonarr.exe`
   - Opstartmap: `C:\ProgramData\Sonarr\bin`
   - Argumenten: `-data=C:\ProgramData\Sonarr-4K`

> Merk op dat **Argumenten** verwijst naar de *nieuwe* map die in stap 1 is aangemaakt.
Dit is cruciaal, omdat het ervoor zorgt dat alle gegevensbestanden van beide instanties op afzonderlijke locaties worden bewaard. {.is-warning}

1. Klik op *Service installeren*. Het venster wordt gesloten en de service is nu beschikbaar om te worden uitgevoerd.
1. Ga verder naar [Configuratie van Sonarr-4k](#windows-multi-config-second)

### Tray-app (Windows)

#### Vereisten (Tray-app)

- [Je moet Sonarr al geïnstalleerd hebben](#windows)
- Sonarr moet geconfigureerd zijn met een `/data=` argument om meerdere instanties mogelijk te maken
- Ga naar de opstartmap voor de huidige gebruiker `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` en bewerk de bestaande snelkoppeling indien nodig.

#### Aanmaken van Sonarr-4K Tray-app

- Klik met de rechtermuisknop en maak een nieuwe snelkoppeling.
- Pad: `C:\ProgramData\Sonarr\bin\Sonarr.exe /data=C:\ProgramData\Sonarr-4K`
- Geef de snelkoppeling een unieke naam zoals `Sonarr-4K` en voltooi de wizard.
- Dubbelklik op de nieuwe snelkoppeling om deze uit te voeren en te testen.
- Ga verder naar [Configuratie van Sonarr-4k](#windows-multi-config-second)

### Configuratie van Sonarr-4k {#windows-multi-config-second}

- Ongeacht of je de servicemethode of de tray-app hebt gebruikt: Stop beide services en beide apps.
- Start Sonarr-4k (service of tray-app).
- Open Sonarr-4k en ga binnen de app naar [Instellingen => Algemeen => Host](/sonarr/settings/#host)
- Wijzig het `Poortnummer` van `8989` naar een andere poort, bijvoorbeeld `7879`, zodat Sonarr en Sonarr4k elkaar niet in de weg zitten.
- Je zou nu beide apps moeten kunnen starten.
- Ga verder naar [Omgaan met updates](#dealing-with-updates)

### Omgaan met updates

- Schakel automatische updates uit in één van je instanties.
- Als één Sonarr-instantie wordt bijgewerkt, worden beide instanties afgesloten en wordt alleen de bijgewerkte instantie opnieuw gestart. Om dit op te lossen, moet je de andere instantie handmatig starten, of je kunt kijken naar het gebruik van het onderstaande PowerShell-script om het probleem aan te pakken.

#### PowerShell-script voor het controleren en herstarten van poorten op Windows

- Wanneer je twee Sonarr-instanties gebruikt en één ervan wordt bijgewerkt, worden alle instanties afgesloten. Alleen de instantie die wordt bijgewerkt, wordt weer online gebracht.
- Het onderstaande PowerShell-script moet worden geconfigureerd als een geplande taak.
- Het controleert de poorten en als er één niet online is, wordt de geplande taak (opnieuw) gestart om Sonarr te starten.

1. Maak een nieuw bestand en noem het SonarrInstancesChecker.ps1 met de onderstaande code.
1. Bewerk het script met je werkelijke servicenamen, IP en poorten.
1. [Maak een geplande taak aan](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) om het script op een herhalend schema uit te voeren.

- Beveiligingsopties: Schakel `Uitvoeren met hoogste bevoegdheid` in
  - Anders kan het script de services niet manipuleren
- Trigger: `Bij starten`
- Taak elke herhalen: `5` of `10` minuten
- Actie: `Programma starten`
- Programma/script: `powershell`
- Argument: `-File D:\SonarrInstancesChecker.ps1`
  - Zorg ervoor dat je het volledige pad naar de locatie van je script gebruikt

```powershell
################################################################################################
### SonarrInstancesChecker.ps1                                                               ###
################################################################################################
### Houdt meerdere Sonarr-instanties actief door de poort te controleren                       ###
### Gebruik Sonarr's Discord of Reddit voor ondersteuning!                                    ###
### https://wiki.servarr.com/sonarr/installation#windows-multi                               ###
################################################################################################
### Versie: 1.1                                                                             ###
### Bijgewerkt: 2020-10-22                                                                      ###
### Auteur:  reloxx13                                                                        ###
################################################################################################



### STEL HIER JE CONFIGURATIE IN ###
# Stel je host-ip en poort correct in en gebruik je servicenamen of geplande taaknamen!

# (string) Het type waarin Sonarr wordt gestart
# "Service" (standaard) er wordt gebruikgemaakt van een servicesproces
# "ScheduledTask" er wordt gebruikgemaakt van de Taakplanner
$startType = 'Service'

# (bool) Schrijft het logboek naar C:\Gebruikers\JE GEBRUIKERSNAAM\log.txt wanneer ingeschakeld
# $false (standaard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instantie 1
        Name = 'Sonarr-V3'; # (string) Servicenaam of taaknaam (standaard: Sonarr-V3)
        IP   = '192.168.178.12'; # (string) IP-adres van de server waarop Sonarr wordt uitgevoerd (standaard: 192.168.178.12)
        Port = '7873'; # (string) Poortnummer waarop Sonarr wordt uitgevoerd (standaard: 7873)
    }
    [pscustomobject]@{   # Instantie 2
        Name = 'Sonarr-4K'; # (string) Servicenaam of taaknaam (standaard: Sonarr-4K)
        IP   = '192.168.178.12'; # (string) IP-adres van de server waarop Sonarr wordt uitgevoerd (standaard: 192.168.178.12)
        Port = '7874'; # (string) Poortnummer waarop Sonarr wordt uitgevoerd (standaard: 7874)
    }
    # Indien nodig kun je hier meer instanties toevoegen... door de onderstaande regels uit te commentariëren
    # [pscustomobject]@{   # Instantie 3
    # Name='Sonarr-3D';    # (string) Servicenaam of taaknaam (standaard: Sonarr-3D)
    # IP='192.168.178.12'; # (string) IP-adres van de server waarop Sonarr wordt uitgevoerd (standaard: 192.168.178.12)
    # Port='7875';         # (string) Poortnummer waarop Sonarr wordt uitgevoerd (standaard: 7875)
    # }
)


### WIJZIG NIETS ONDER DEZE REGEL ###


###
# Deze functie schrijft naar een logbestand of naar de console-uitvoer
###
function Write-Log
{
    # Schrijft naar C:\Gebruikers\JE GEBRUIKERSNAAM\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    # Console-uitvoer
    Write-Output "[$(TS)]$Message"
    
    # Bestandsuitvoer
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
        Write-Log "Poort $($_.Port) is gesloten, herstarten van $($startType) $($_.Name)!"

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
        Write-Log "Poort $($_.Port) is geopend!"
    }
}

Write-Log 'END ====================='
```

## Meerdere instanties op Linux

{#linux-multi}

- [Swizzin-gebruikers](https://github.com/ComputerByte/sonarr4k)
- Niet-Swizzin-gebruikers
  - Zorg ervoor dat je eerste instantie het `-data=` argument doorgeeft.
  - Stop tijdelijk je eerste instantie, zodat je de poort van de tweede instantie kunt wijzigen `systemctl stop sonarr`
  - Schakel automatische updates uit voor één van je Sonarr-instanties

> Hieronder staat een voorbeeldscript om een Sonarr4K-instantie te maken. Het onderstaande systemd-creatiebestand gebruikt een gegevensmap van `/var/lib/sonarr4k/`. Zorg ervoor dat de map bestaat of pas deze aan indien nodig.{.is-danger}

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

- Herlaad systemd:

```shell
sudo systemctl -q daemon-reload
```

- Schakel de Sonarr4k-service in:

```shell
sudo systemctl enable --now -q sonarr4k
```

## Meerdere instanties met Docker

{#docker-multi}

- Start eenvoudig een tweede Docker-container met een andere naam, waarbij aan de bovenstaande vereisten wordt voldaan.