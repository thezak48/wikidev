---
title: Multiple Instances
description: 
published: true
date: 2023-08-20T02:23:13.676Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:35.847Z
---

# Flera instanser

Det är möjligt att köra flera instanser av Sonarr. Detta görs vanligtvis när man vill ha en 4K- och en 1080p-kopia av en serie.
[Märk att du kan konfigurera Sonarr att använda en andra Sonarr som en lista. Detta är användbart om du vill hålla båda synkroniserade.](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)

- [Windows - Flera instanser](#windows-multi)
- [Linux - Flera instanser](#linux-multi)
- [Docker - Flera instanser](#docker-multi)
{.links-list}

Följande krav bör noteras:

- Om det inte är Docker bör samma binärer (programfiler) användas
- Om det inte är Docker måste alla instanser *måste* ha en `-data=` eller `/data=` argument som skickas
- Om det inte är Docker måste olika portar användas
  - Om det är Docker måste olika externa portar användas
- Olika kategorier för nedladdningsklienter måste användas
- Olika rotmappar måste användas.
- Om det inte är Docker, inaktivera automatiska uppdateringar för alla utom 1 instans.

## Windows - Flera instanser

{#windows-multi}

Denna guide visar hur du kör flera instanser av Sonarr på Windows med bara en grundinstallation. Denna guide sattes samman med Windows 10; om du använder en tidigare version av Windows (7, 8, etc.) kan du behöva justera vissa saker. Denna guide antar också att du har installerat Sonarr i standardkatalogen och att din andra instans av Sonarr kommer att kallas Sonarr-4K. Ändra gärna saker för att passa dina egna installationer.

### Tjänst (Windows)

#### Förutsättningar (Tjänst)

- [Du måste redan ha installerat Sonarr](#windows)
- Du måste ha [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installerat. För att installera, ladda ner den senaste versionen (2.24 vid skrivande tidpunkt) och kopiera antingen 32-bitars eller 64-bitars nssm.exe-filen till C:/windows/system32.
  - Om du är osäker på om du har ett 32-bitars eller 64-bitars system, kontrollera Inställningar => System => Om => Systemtyp.

#### Konfigurera Sonarr-tjänst

1. Öppna ett kommandotolksadministratörfönster. (För att köra som administratör,
    högerklicka på kommandotolksikonen och välj "Kör som
    administratör".)
1. Om Sonarr körs, stoppa tjänsten genom att köra `nssm stop Sonarr`
    i kommandotolken.
1. Nu måste vi redigera den befintliga Sonarr-instansen för att explicit peka
    till sin datakatalog. Standardkommandot är följande:
    `sc config Sonarr binpath= "C:\ProgramData\Sonarr\bin\Sonarr.exe
    -data=C:\ProgramData\Sonarr"`

Detta kommando talar om för den ursprungliga Sonarr-instansen att explicit använda
`C:\ProgramData\Sonarr` som sin datakatalog. Om du inte använde
standardinstallationen av Sonarr, eller om din datakatalog är någon annanstans, kan du
behöva ändra dina sökvägar här.

#### Skapa Sonarr-4K-tjänst

1. Skapa en ny mapp där du vill att Sonarr-4K ska vara. De flesta använder en liknande plats som
    `C:\ProgramData\Sonarr-4K`
1. Återgå till kommandotolken och skapa den nya Sonarr-4K-tjänsten med `nssm
    install Sonarr-4K`. Ett popup-fönster öppnas där du kan skriva in dina
    parametrar för den nya instansen. För detta exempel kommer vi att använda
    följande:
      - Sökväg: `C:\ProgramData\Sonarr\bin\Sonarr.exe`
      - Startmapp: `C:\ProgramData\Sonarr\bin`
      - Argument: `-data=C:\ProgramData\Sonarr-4K`

> Observera att **Argument** pekar på den *nya* mappen som skapades i steg 1.
Detta är avgörande, eftersom det håller alla datafiler från båda instanserna i
separerade platser. {.is-warning}

1. Klicka på *Installera tjänst*. Fönstret ska stängas och tjänsten
    kommer nu att vara tillgänglig att köra.
1. Fortsätt till [Konfigurera Sonarr-4k](#windows-multi-config-second)

### Tray App (Windows)

#### Förutsättningar (Tray App)

- [Du måste redan ha installerat Sonarr](#windows)
- Sonarr måste vara konfigurerat med ett `/data=` argument för att tillåta flera instanser
- Gå till Startmappen för den aktuella användaren `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` och redigera den befintliga genvägen om det behövs.

#### Skapa Sonarr-4K Tray App

- Högerklicka och skapa en ny genväg
- Sökväg: `C:\ProgramData\Sonarr\bin\Sonarr.exe /data=C:\ProgramData\Sonarr-4K`
- Ge genvägen ett unikt namn som `Sonarr-4K` och slutför guiden.
- Dubbelklicka på den nya genvägen för att köra och testa.
- Fortsätt till [Konfigurera Sonarr-4k](#windows-multi-config-second)

### Konfigurera Sonarr-4k {#windows-multi-config-second}

- Oavsett om du använde Tjänstmetoden eller Tray App: Stoppa både tjänsterna och apparna
- Starta Sonarr-4k (tjänst eller Tray App)
- Öppna Sonarr-4k och navigera inom appen till [Inställningar => Allmänt => Värd](/sonarr/settings/#host)
- Ändra `Portnummer` från `8989` till en annan port, t.ex. `7879`, så att Sonarr och Sonarr4k inte krockar
- Du bör nu kunna starta båda apparna
- Fortsätt till [Hantera uppdateringar](#dealing-with-updates)

### Hantera uppdateringar

- Inaktivera automatiska uppdateringar i en av dina instanser
- Om en Sonarr-instans uppdateras kommer båda instanserna att stängas av och bara den uppdaterade kommer att startas igen. För att åtgärda detta måste du manuellt starta den andra instansen, eller så kan du titta på att använda det nedanstående PowerShell-skriptet för att lösa problemet.

#### PowerShell-skript för att kontrollera och starta om Windows-portar

- När du använder två Sonarr-instanser och en av dem uppdateras kommer den att stänga av alla instanser. Bara den som uppdateras kommer att komma tillbaka online.
- Nedanstående PowerShell-skript bör konfigureras som en schemalagd uppgift.
- Det kontrollerar portarna och om en inte är online kommer det att (om)starta den schemalagda uppgiften för att starta Sonarr.

1. Skapa en ny fil och namnge den SonarrInstancesChecker.ps1 med följande kod.
1. Redigera skriptet med dina faktiska tjänstenamn, IP och portar.
1. [Skapa en schemalagd uppgift](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) för att köra skriptet enligt en upprepad tidtabell.

- Säkerhetsalternativ: Aktivera `Kör med högsta behörighet`
  - Annars kommer skriptet inte att kunna manipulera tjänster
- Utlösare: `Vid start`
- Upprepa uppgiften varje: `5` eller `10` minuter
- Åtgärd: `Starta ett program`
- Program/skript: `powershell`
- Argument: `-File D:\SonarrInstancesChecker.ps1`
  - Se till att använda den fullständiga sökvägen till din skripts plats

```powershell
################################################################################################
### SonarrInstancesChecker.ps1                                                               ###
################################################################################################
### Håller flera Sonarr-instanser igång genom att kontrollera porten                           ###
### Använd Sonarrs Discord eller Reddit för support!                                          ###
### https://wiki.servarr.com/sonarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Uppdaterad: 2020-10-22                                                                   ###
### Författare:  reloxx13                                                                     ###
################################################################################################



### STÄLL IN DIN KONFIGURATION HÄR ###
# Ställ in din värd-IP och port korrekt och använd dina tjänste- eller schemalagda uppgiftsnamn!

# (sträng) Typen av hur Sonarr startas
# "Tjänst" (standard) Tjänsteprocess används
# "Schemalagd uppgift" Task Scheduler används
$startType = 'Tjänst'

# (bool) Skriver loggen till C:\Users\DITTANVÄNDARNAMN\log.txt när den är aktiverad
# $false (standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instans 1
        Name = 'Sonarr-V3'; # (sträng) Tjänste- eller uppgiftsnamn (standard: Sonarr-V3)
        IP   = '192.168.178.12'; # (sträng) Server-IP där Sonarr körs (standard: 192.168.178.12)
        Port = '7873'; # (sträng) Serverport där Sonarr körs (standard: 7873)
    }
    [pscustomobject]@{   # Instans 2
        Name = 'Sonarr-4K'; # (sträng) Tjänste- eller uppgiftsnamn (standard: Sonarr-4K)
        IP   = '192.168.178.12'; # (sträng) Server-IP där Sonarr körs (standard: 192.168.178.12)
        Port = '7874'; # (sträng) Serverport där Sonarr körs (standard: 7874)
    }
    # Om det behövs kan du lägga till fler instanser här... genom att ta bort kommentarerna från nedanstående rader
    # [pscustomobject]@{   # Instans 3
    # Name='Sonarr-3D';    # (sträng) Tjänste- eller uppgiftsnamn (standard: Sonarr-3D)
    # IP='192.168.178.12'; # (sträng) Server-IP där Sonarr körs (standard: 192.168.178.12)
    # Port='7875';         # (sträng) Serverport där Sonarr körs (standard: 7875)
    # }
)


### ÄNDRA INGET UNDER DENNA RAD ###


###
# Denna funktion skriver till en loggfil eller till konsolens utdata
###
function Write-Log
{
    # Kommer att skriva till C:\Users\DITTANVÄNDARNAMN\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    # Konsolens utdata
    Write-Output "[$(TS)]$Message"
    
    # Filutdata
    if ($logToFile)
    {
        "[$(TS)]$Message" | Tee-Object -FilePath $Path -Append | Write-Verbose
    }
}


Write-Log 'START ====================='


$instances | ForEach-Object {
    Write-Log "Kontrollerar $($_.Name) $($_.IP):$($_.Port)"
    
    $PortOpen = ( Test-NetConnection $_.IP -Port $_.Port -WarningAction SilentlyContinue ).TcpTestSucceeded 
    
    if (!$PortOpen)
    {
        Write-Log "Port $($_.Port) är stängd, startar om $($startType) $($_.Name)!"

        if ($startType -eq 'Tjänst')
        {
            Get-Service -Name $_.Name | Stop-Service
            Get-Service -Name $_.Name | Start-Service
        }
        elseif ($startType -eq 'Schemalagd uppgift')
        {
            Get-ScheduledTask -TaskName $_.Name | Stop-ScheduledTask
            Get-ScheduledTask -TaskName $_.Name | Start-ScheduledTask
        }
        else
        {
            Write-Log '[FEL] OKÄND STARTTYP! ANVÄND Tjänst eller Schemalagd uppgift!'
        }
    }
    else
    {
        Write-Log "Port $($_.Port) är öppen!"
    }
}

Write-Log 'SLUT ====================='
```

## Linux - Flera instanser

{#linux-multi}

- [Swizzin-användare](https://github.com/ComputerByte/sonarr4k)
- Användare som inte använder Swizzin
  - Se till att din första instans har det `-data=` argumentet skickat.
  - Stoppa tillfälligt din första instans så att du kan ändra den andra instansens port `systemctl stop sonarr`
  - Inaktivera automatiska uppdateringar för en av dina Sonarr-instanser

> Nedan finns ett exempelskript för att skapa en Sonarr4K-instans. Det systemd-skript för skapande som visas nedan kommer att använda en datakatalog på `/var/lib/sonarr4k/`. Se till att katalogen finns eller ändra den vid behov.{.is-danger}

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

- Ladda om systemd:

```shell
sudo systemctl -q daemon-reload
```

- Aktivera Sonarr4k-tjänsten:

```shell
sudo systemctl enable --now -q sonarr4k
```

## Docker - Flera instanser

{#docker-multi}

- Starta helt enkelt upp en andra Docker-container med ett annat namn och se till att ovanstående krav är uppfyllda.