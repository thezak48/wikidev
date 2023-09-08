---
title: Flera instanser
description: 
published: true
date: 2023-09-01T05:05:47.102Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:10.189Z
---

# Flera instanser

Det är möjligt att köra flera instanser av Radarr. Detta görs vanligtvis när man vill ha en 4K- och en 1080p-kopia av en film. Observera att du kan (och förmodligen bör) [granska TRaSH:s guide och konfigurera Radarr för att använda en andra Radarr som en lista](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/). Detta är användbart om du vill hålla båda synkroniserade.

- [Windows - Flera instanser](#windows-multi)
- [Linux - Flera instanser](#linux-multi)
- [Docker - Flera instanser](#docker-multi)
{.links-list}

Följande krav bör noteras:

- Om det inte är Docker ska samma binärer (programfiler) användas
- Om det inte är Docker måste alla instanser *måste* ha ett `-data=` eller `/data=` argument som skickas med
- Om det inte är Docker måste olika portar användas
  - Om det är Docker måste olika externa portar användas
- Olika nedladdningsklientkategorier måste användas
- Olika rotmappar måste användas.
- Om det inte är Docker ska automatiska uppdateringar inaktiveras för alla utom 1 instans.

## Windows - Flera instanser

{#windows-multi}

Denna guide visar hur du kör flera instanser av Radarr på Windows med bara en grundinstallation. Denna guide sammanställdes med Windows 10; om du använder en tidigare version av Windows (7, 8, etc.) kan du behöva justera vissa saker. Denna guide antar också att du har installerat Radarr i standardkatalogen och att din andra instans av Radarr kommer att kallas Radarr-4K. Ändra gärna saker för att passa dina egna installationer.

> Observera: Du bör köra Radarr antingen som [en tjänst](#service-windows) eller som en [tray-app](#tray-app-windows). Att köra både en app och en tjänst är onödigt och kan orsaka problem.

### Tjänst (Windows)

#### Förutsättningar (Tjänst)

- [Du måste redan ha installerat Radarr](#windows)
- Du måste ha [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installerat. För att installera, ladda ner den senaste versionen (2.24 vid skrivande tidpunkt) och kopiera antingen 32-bitars eller 64-bitars nssm.exe-filen till C:/windows/system32.
  - Om du är osäker på om du har ett 32-bitars eller 64-bitars system, kontrollera Inställningar => System => Om => Systemtyp.

#### Konfigurera Radarr-tjänst

1. Öppna ett kommandotolksadministratörfönster. (För att köra som administratör,
    högerklicka på kommandotolksikonen och välj "Kör som
    administratör".)
1. Om Radarr körs, stoppa tjänsten genom att köra `nssm stop Radarr`
    i kommandotolken.
1. Nu måste vi redigera den befintliga Radarr-instansen för att explicit peka
    på sin datakatalog. Standardkommandot är följande:
    `sc config Radarr binpath= "C:\ProgramData\Radarr\bin\Radarr.exe
    -data=C:\ProgramData\Radarr"`

Detta kommando talar om för den ursprungliga Radarr-instansen att använda
`C:\ProgramData\Radarr` som sin datakatalog. Om du inte använde den
standardinstallationen av Radarr, eller om din datakatalog är någon annanstans, kan du
behöva ändra dina sökvägar här.

#### Skapa Radarr-4K-tjänst

1. Skapa en ny mapp där du vill att Radarr-4K ska vara. De flesta använder en liknande plats som
    `C:\ProgramData\Radarr-4K`
1. Återgå till kommandotolken och skapa den nya Radarr-4K-tjänsten med `nssm
    install Radarr-4K`. Ett popup-fönster öppnas där du kan skriva in dina
    parametrar för den nya instansen. För detta exempel kommer vi att använda
    följande:
      - Sökväg: `C:\ProgramData\Radarr\bin\Radarr.exe`
      - Startmapp: `C:\ProgramData\Radarr\bin`
      - Argument: `-data=C:\ProgramData\Radarr-4K`
      - Flik för avslutshandlingar
        - Starta om: Starta om programmet
        - Fördröjning: 120000 ms
        (2 minuter, kan vara längre om uppdateringen inte slutförs i tid)

> Observera att **Argument** pekar på den *nya* mappen som skapades i steg 1.
Detta är avgörande, eftersom det håller alla datafiler från båda instanserna i
separata platser. {.is-warning}

1. Klicka på *Installera tjänst*. Fönstret ska stängas och tjänsten
    kommer nu att vara tillgänglig att köra.
1. Fortsätt till [Konfigurera Radarr-4K](#windows-multi-config-second)

### Tray-app (Windows)

#### Förutsättningar (Tray-app)

- [Du måste redan ha installerat Radarr](#windows)
- Radarrs genväg måste vara konfigurerad med ett `/data=` argument i fältet 'target' för att tillåta flera instanser
- Gå till uppstarts-mappen för den aktuella användaren `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` och redigera den befintliga genvägen om det behövs.

#### Skapa Radarr-4K Tray-app

- Skapa en ny mapp för Radarr-4K:s konfigurationsfiler. De flesta använder en liknande plats som
    `C:\ProgramData\Radarr-4K`
- Högerklicka och skapa en ny genväg
- Sökväg: `C:\ProgramData\Radarr\bin\Radarr.exe /data=C:\ProgramData\Radarr-4K`
- Ge genvägen ett unikt namn som `Radarr-4K` och slutför guiden.
- Dubbelklicka på den nya genvägen för att köra och testa.
- Fortsätt till [Konfigurera Radarr-4K](#windows-multi-config-second)

### Konfigurera Radarr-4K {#windows-multi-config-second}

- Oavsett om du använde tjänstmetoden eller tray-appen: Stoppa både tjänsterna och apparna
- Starta Radarr-4K (tjänst eller tray-app)
- Öppna Radarr-4K och navigera inom appen till [Inställningar => Allmänt => Värd](/radarr/settings/#host)
- Ändra `Portnummer` från `7878` till en annan port, t.ex. `7879`, så att Radarr och Radarr4K inte kommer i konflikt
- Nu bör du kunna starta båda apparna
- Fortsätt till [Hantera uppdateringar](#dealing-with-updates)

### Hantera uppdateringar

> - Inaktivera automatiska uppdateringar i en av dina instanser
  - I config.xml ändra uppdateringsgrenen till `<Branch>nonexistent</Branch>`
- Om en Radarr-instans uppdateras kommer båda instanserna att stängas av och bara den uppdaterade kommer att startas igen. För att åtgärda detta måste du manuellt starta den andra instansen, eller så kan du överväga att använda följande PowerShell-skript för att lösa problemet.

> Om [NSSM Exit Action](#creating-radarr-4k-service) är korrekt konfigurerad kan Radarr uppdateras och starta om flera instanser utan ytterligare skript.
Om återstartfördröjningen inte är konfigurerad som standard kommer instansen att startas om omedelbart.
Detta kan förhindra att uppdateringar tillämpas och kan resultera i följande felmeddelande: `Radarr startades om för tidigt av en extern process.`
{.is-info}

#### PowerShell-skript för att kontrollera och starta om Windows-portar

- När du använder två Radarr-instanser och en av dem uppdateras kommer den att stänga av alla instanser. Bara den som uppdateras kommer att startas igen.
- Nedan följer ett PowerShell-skript som bör konfigureras som en schemalagd uppgift.
- Det kontrollerar portarna och om en inte är online kommer det att (om)starta den schemalagda uppgiften för att starta Radarr.

1. Skapa en ny fil och namnge den RadarrInstancesChecker.ps1 med följande kod.
1. Redigera skriptet med dina faktiska tjänstenamn, IP och portar. *Om du kör i Tray-läge måste du skapa schemalagda uppgifter för att starta varje Radarr-instans och använda de uppgiftsnamnen i skriptet nedan.*
1. [Skapa en schemalagd uppgift](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) för att köra skriptet med en upprepad tidsplan.

- Säkerhetsalternativ: Aktivera `Kör med högsta behörighet`
  - Annars kommer skriptet inte att kunna manipulera tjänster
- Trigger: `Vid start`
- Upprepa uppgiften varje: `5` eller `10` minuter
- Åtgärd: `Starta ett program`
- Program/skript: `powershell`
- Argument: `-File D:\RadarrInstancesChecker.ps1`
  - Se till att du använder den fullständiga sökvägen till skriptets plats

```powershell
################################################################################################
### RadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Håller flera Radarr-instanser igång genom att kontrollera porten                          ###
### Använd Radarrs Discord eller Reddit för support!                                          ###
### https://wiki.servarr.com/radarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Uppdaterad: 2020-10-22                                                                   ###
### Författare:  reloxx13                                                                     ###
################################################################################################



### ANGE DIN KONFIGURATION HÄR ###
# Ange ditt värd-IP och port korrekt och använd dina tjänste- eller schemalagda uppgiftsnamn!

# (sträng) Typen hur Radarr startas
# "Service" (standard) Tjänstprocess används
# "ScheduledTask" Uppgiftsplaneraren används
$startType = 'Service'

# (bool) Skriver loggen till C:\Users\DITTANVÄNDARNAMN\log.txt när den är aktiverad
# $false (standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instans 1
        Name = 'Radarr-V3'; # (sträng) Tjänste- eller uppgiftsnamn (standard: Radarr-V3)
        IP   = '192.168.178.12'; # (sträng) Server-IP där Radarr körs (standard: 192.168.178.12)
        Port = '7873'; # (sträng) Serverport där Radarr körs (standard: 7873)
    }
    [pscustomobject]@{   # Instans 2
        Name = 'Radarr-4K'; # (sträng) Tjänste- eller uppgiftsnamn (standard: Radarr-4K)
        IP   = '192.168.178.12'; # (sträng) Server-IP där Radarr körs (standard: 192.168.178.12)
        Port = '7874'; # (sträng) Serverport där Radarr körs (standard: 7874)
    }
    # Om det behövs kan du lägga till fler instanser här... genom att ta bort kommentarerna nedan
    # [pscustomobject]@{   # Instans 3
    # Name='Radarr-3D';    # (sträng) Tjänste- eller uppgiftsnamn (standard: Radarr-3D)
    # IP='192.168.178.12'; # (sträng) Server-IP där Radarr körs (standard: 192.168.178.12)
    # Port='7875';         # (sträng) Serverport där Radarr körs (standard: 7875)
    # }
)


### ÄNDRA INGET NEDANFÖR DENNA RAD ###


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
        Write-Log "Port $($_.Port) är öppen!"
    }
}

Write-Log 'END ====================='
```

## Linux - Flera instanser

{#linux-multi}

- [Swizzin-användare](https://github.com/ComputerByte/radarr4k)
- Användare som inte använder Swizzin
  - Se till att din första instans har `-data=` argumentet skickat.
  - Stoppa tillfälligt din första instans så att du kan ändra den andra instansens port `systemctl stop radarr`
  - Inaktivera automatiska uppdateringar för en av dina Radarr-instanser

> Nedan följer ett exempelskript för att skapa en Radarr4K-instans. Det systemd-skript för skapande som visas nedan kommer att använda en datakatalog på `/var/lib/radarr4k/`. Se till att katalogen finns eller ändra den vid behov.{.is-danger}

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

- Ladda om systemd:

```shell
sudo systemctl -q daemon-reload
```

- Aktivera Radarr4k-tjänsten:

```shell
sudo systemctl enable --now -q radarr4k
```

## Docker flera instanser

{#docker-multi}

- Starta helt enkelt upp en andra Docker-kontainer med ett annat namn och se till att ovanstående krav är uppfyllda.