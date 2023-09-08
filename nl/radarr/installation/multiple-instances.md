---
title: Meerdere instanties
description: 
published: true
date: 2023-09-01T05:05:47.102Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:10.189Z
---

# Meerdere instanties

Het is mogelijk om meerdere instanties van Radarr uit te voeren. Dit wordt meestal gedaan wanneer je een 4K- en een 1080p-kopie van een film wilt hebben. Let op dat je [de handleiding van TRaSH kunt raadplegen en Radarr kunt configureren om een tweede Radarr als lijst te gebruiken](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/). Dit is handig als je beide wilt synchroniseren.

- [Meerdere instanties op Windows](#windows-multi)
- [Meerdere instanties op Linux](#linux-multi)
- [Meerdere instanties op Docker](#docker-multi)
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

Deze handleiding laat zien hoe je meerdere instanties van Radarr kunt uitvoeren op Windows met slechts één basisinstallatie. Deze handleiding is samengesteld met behulp van Windows 10; als je een eerdere versie van Windows gebruikt (7, 8, enz.), moet je mogelijk enkele aanpassingen doen. Deze handleiding gaat er ook vanuit dat je Radarr hebt geïnstalleerd in de standaardmap en dat je tweede instantie van Radarr Radarr-4K wordt genoemd. Voel je vrij om dingen aan te passen aan je eigen installaties.

> Opmerking: Je moet Radarr uitvoeren als **ofwel** [een service](#service-windows) of als [een systeemvak-app](#tray-app-windows). Het uitvoeren van zowel een app als een service is overbodig en kan waarschijnlijk problemen veroorzaken.

### Service (Windows)

#### Vereisten (Service)

- [Je moet Radarr al hebben geïnstalleerd](#windows)
- Je moet [NSSM (Non-Sucking Service Manager)](http://nssm.cc) geïnstalleerd hebben. Download de nieuwste versie (2.24 op het moment van schrijven) en kopieer het nssm.exe-bestand (32-bits of 64-bits) naar C:/windows/system32.
  - Als je niet zeker weet of je een 32-bits of 64-bits systeem hebt, controleer dan Instellingen => Systeem => Info => Systeemtype.

#### Configuratie van Radarr-service

1. Open een opdrachtpromptvenster als beheerder. (Klik met de rechtermuisknop op het pictogram van de opdrachtprompt en kies "Als administrator uitvoeren".)
1. Als Radarr actief is, stop dan de service door `nssm stop Radarr` uit te voeren in de opdrachtprompt.
1. Nu moeten we de bestaande Radarr-instantie bewerken om expliciet naar de gegevensmap te verwijzen. De standaardopdracht is als volgt: `sc config Radarr binpath= "C:\ProgramData\Radarr\bin\Radarr.exe -data=C:\ProgramData\Radarr"`

Deze opdracht vertelt de oorspronkelijke instantie van Radarr om expliciet `C:\ProgramData\Radarr` te gebruiken als de gegevensmap. Als je de standaardinstallatie van Radarr niet hebt gebruikt, of als je gegevensmap ergens anders is, moet je hier je paden wijzigen.

#### Het maken van de Radarr-4K-service

1. Maak een nieuwe map waar je Radarr-4K wilt plaatsen. De meeste mensen gebruiken een vergelijkbare locatie zoals `C:\ProgramData\Radarr-4K`.
1. Ga terug naar de opdrachtprompt en maak de nieuwe Radarr-4K-service met `nssm install Radarr-4K`. Er wordt een pop-upvenster geopend waarin je de parameters voor de nieuwe instantie kunt invoeren. Voor dit voorbeeld gebruiken we het volgende:
      - Pad: `C:\ProgramData\Radarr\bin\Radarr.exe`
      - Opstartmap: `C:\ProgramData\Radarr\bin`
      - Argumenten: `-data=C:\ProgramData\Radarr-4K`
      - Tabblad Acties bij afsluiten
        - Opnieuw opstarten: Toepassing opnieuw starten
        - Vertraging: 120000 ms
        (2 minuten, kan langer zijn als de update niet op tijd kan worden voltooid)

> Let op dat **Argumenten** wijst naar de *nieuwe* map die is aangemaakt in stap 1.
Dit is cruciaal, omdat het ervoor zorgt dat alle gegevensbestanden van beide instanties op afzonderlijke locaties worden bewaard. {.is-warning}

1. Klik op *Service installeren*. Het venster wordt gesloten en de service is nu beschikbaar om te worden uitgevoerd.
1. Ga verder naar [Configuratie van Radarr-4K](#windows-multi-config-second)

### Systeemvak-app (Windows)

#### Vereisten (Systeemvak-app)

- [Je moet Radarr al hebben geïnstalleerd](#windows)
- De snelkoppeling van Radarr moet geconfigureerd zijn met een `/data=` argument in het 'doel'-veld om meerdere instanties mogelijk te maken
- Ga naar de opstartmap voor de huidige gebruiker `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` en bewerk de bestaande snelkoppeling indien nodig.

#### Het maken van de Radarr-4K-systeemvak-app

- Maak een nieuwe map voor de configuratiebestanden van Radarr-4K. De meeste mensen gebruiken een vergelijkbare locatie zoals `C:\ProgramData\Radarr-4K`.
- Klik met de rechtermuisknop en maak een nieuwe snelkoppeling
- Pad: `C:\ProgramData\Radarr\bin\Radarr.exe /data=C:\ProgramData\Radarr-4K`
- Geef de snelkoppeling een unieke naam zoals `Radarr-4K` en voltooi de wizard.
- Dubbelklik op de nieuwe snelkoppeling om deze uit te voeren en te testen.
- Ga verder naar [Configuratie van Radarr-4K](#windows-multi-config-second)

### Configuratie van Radarr-4K {#windows-multi-config-second}

- Ongeacht of je de servicemethode of de systeemvak-app hebt gebruikt: Stop beide services en beide apps.
- Start Radarr-4K (service of systeemvak-app)
- Open Radarr-4K en ga binnen de app naar [Instellingen => Algemeen => Host](/radarr/settings/#host)
- Wijzig het `Poortnummer` van `7878` naar een andere poort, bijvoorbeeld `7879`, zodat Radarr en Radarr-4K niet met elkaar in conflict komen.
- Je zou nu beide apps moeten kunnen starten.
- Ga verder naar [Omgaan met updates](#dealing-with-updates)

### Omgaan met updates

> - Schakel automatische updates uit in één van je instanties
  - In config.xml wijzig je de update-tak naar `<Branch>nonexistent</Branch>`
- Als één Radarr-instantie wordt bijgewerkt, worden beide instanties afgesloten en wordt alleen de bijgewerkte instantie opnieuw gestart. Om dit op te lossen, moet je de andere instantie handmatig starten, of je kunt overwegen om het onderstaande PowerShell-script te gebruiken om het probleem aan te pakken.

> Het correct configureren van de [NSSM Exit Action](#creating-radarr-4k-service) zou Radarr in staat moeten stellen om meerdere instanties bij te werken en opnieuw te starten zonder extra scripts.
Als de herstartvertraging niet standaard is geconfigureerd, wordt de instantie direct opnieuw gestart.
Dit kan voorkomen dat updates worden toegepast en kan leiden tot de volgende foutmelding `Radarr was prematurely restarted by external process`.
{.is-info}

#### PowerShell-script voor het controleren en opnieuw starten van poorten in Windows

- Wanneer je twee Radarr-instanties gebruikt en één ervan wordt bijgewerkt, worden alle instanties afgesloten. Alleen degene die wordt bijgewerkt, wordt weer online gebracht.
- Het onderstaande PowerShell-script moet worden geconfigureerd als een geplande taak.
- Het controleert de poorten en als er één niet online is, wordt de geplande taak (opnieuw) gestart om Radarr te starten.

1. Maak een nieuw bestand en noem het RadarrInstancesChecker.ps1 met de onderstaande code.
1. Bewerk het script met je werkelijke servicenamen, IP en poorten. *Als je in de systeemvakmodus werkt, moet je geplande taken maken om elke Radarr-instantie te starten en de namen van die taken gebruiken in het onderstaande script.*
1. [Maak een geplande taak](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) om het script op een herhalend schema uit te voeren.

- Beveiligingsopties: Schakel `Uitvoeren met hoogste bevoegdheid` in
  - Anders kan het script de services niet manipuleren
- Trigger: `Bij het starten`
- Taak elke herhalen: `5` of `10` minuten
- Actie: `Programma starten`
- Programma/script: `powershell`
- Argument: `-File D:\RadarrInstancesChecker.ps1`
  - Zorg ervoor dat je het volledige pad naar de locatie van je script gebruikt

```powershell
################################################################################################
### RadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Houdt meerdere Radarr-instanties actief door de poort te controleren                      ###
### Gebruik Radarr's Discord of Reddit voor ondersteuning!                                    ###
### https://wiki.servarr.com/radarr/installation#windows-multi                               ###
################################################################################################
### Versie: 1.1                                                                             ###
### Bijgewerkt: 2020-10-22                                                                  ###
### Auteur:  reloxx13                                                                        ###
################################################################################################



### STEL HIER JE CONFIGURATIE IN ###
# Stel je host-ip en poort correct in en gebruik je servicenamen of geplande taaknamen!

# (string) Het type waarin Radarr wordt gestart
# "Service" (standaard) Er wordt gebruikgemaakt van een servicesproces
# "ScheduledTask" Er wordt gebruikgemaakt van de Taakplanner
$startType = 'Service'

# (bool) Schrijft het logbestand naar C:\Users\JE GEBRUIKERSNAAM\log.txt wanneer ingeschakeld
# $false (standaard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instantie 1
        Name = 'Radarr-V3'; # (string) Servicenaam of taaknaam (standaard: Radarr-V3)
        IP   = '192.168.178.12'; # (string) IP-adres van de server waarop Radarr wordt uitgevoerd (standaard: 192.168.178.12)
        Port = '7873'; # (string) Poortnummer waarop Radarr wordt uitgevoerd (standaard: 7873)
    }
    [pscustomobject]@{   # Instantie 2
        Name = 'Radarr-4K'; # (string) Servicenaam of taaknaam (standaard: Radarr-4K)
        IP   = '192.168.178.12'; # (string) IP-adres van de server waarop Radarr wordt uitgevoerd (standaard: 192.168.178.12)
        Port = '7874'; # (string) Poortnummer waarop Radarr wordt uitgevoerd (standaard: 7874)
    }
    # Indien nodig kun je hier meer instanties toevoegen... door de onderstaande regels uit te commentariëren
    # [pscustomobject]@{   # Instantie 3
    # Name='Radarr-3D';    # (string) Servicenaam of taaknaam (standaard: Radarr-3D)
    # IP='192.168.178.12'; # (string) IP-adres van de server waarop Radarr wordt uitgevoerd (standaard: 192.168.178.12)
    # Port='7875';         # (string) Poortnummer waarop Radarr wordt uitgevoerd (standaard: 7875)
    # }
)


### WIJZIG NIETS ONDER DEZE REGEL ###


###
# Deze functie schrijft naar een logbestand of naar de console-uitvoer
###
function Write-Log
{
    #Schrijft naar C:\Users\JE GEBRUIKERSNAAM\log.txt
    
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
    Write-Log "Controleren $($_.Name) $($_.IP):$($_.Port)"
    
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
        Write-Log "Poort $($_.Port) is geopend!"
    }
}

Write-Log 'END ====================='
```

## Meerdere instanties op Linux

{#linux-multi}

- [Gebruikers van Swizzin](https://github.com/ComputerByte/radarr4k)
- Gebruikers die geen Swizzin gebruiken
  - Zorg ervoor dat je eerste instantie het `-data=` argument doorgeeft.
  - Stop tijdelijk je eerste instantie, zodat je de poort van de tweede instantie kunt wijzigen `systemctl stop radarr`
  - Schakel automatische updates uit voor één van je Radarr-instanties

> Hieronder staat een voorbeeldscript om een Radarr4K-instantie te maken. Het onderstaande systemd-creatie-script gebruikt een gegevensmap van `/var/lib/radarr4k/`. Zorg ervoor dat de map bestaat of pas deze aan indien nodig.{.is-danger}

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

- Herlaad systemd:

```shell
sudo systemctl -q daemon-reload
```

- Schakel de Radarr4k-service in:

```shell
sudo systemctl enable --now -q radarr4k
```

## Docker meerdere instanties

{#docker-multi}

- Start eenvoudig een tweede Docker-container op met een andere naam, waarbij aan de bovenstaande vereisten wordt voldaan.