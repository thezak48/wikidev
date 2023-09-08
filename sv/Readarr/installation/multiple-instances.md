# Flera instanser

Det är möjligt att köra flera instanser av Readarr. Detta görs vanligtvis när man vill ha en ljudbok och en e-bokskopia av en bok.
Observera att du kan konfigurera Readarr att använda en andra Readarr som en lista. Detta är användbart om du vill hålla båda synkroniserade.

- [Windows - Flera instanser](#windows-multi)
- [Linux - Flera instanser](#linux-multi)
- [MacOS - Flera instanser](#macos-multi)
- [Docker - Flera instanser](#docker-multi)
{.links-list}

Följande krav bör noteras:

- Om det inte är Docker ska samma binärer (programfiler) användas
- Om det inte är Docker måste alla instanser *måste* ha ett `-data=` eller `/data=` argument som skickas
- Om det inte är Docker måste olika portar användas
  - Om det är Docker måste olika externa portar användas
- Olika nedladdningsklientkategorier måste användas
- Olika rotmappar måste användas.
- Om det inte är Docker, inaktivera automatiska uppdateringar för alla utom 1 instans.

## Windows - Flera instanser

{#windows-multi}

Denna guide visar hur du kör flera instanser av Readarr på Windows med bara en grundinstallation. Denna guide sammanställdes med Windows 10; om du använder en tidigare version av Windows (7, 8, etc.) kan du behöva justera vissa saker. Denna guide antar också att du har installerat Readarr i standardkatalogen och att din andra instans av Readarr kommer att kallas Readarr-ljudböcker. Ändra gärna saker för att passa dina egna installationer.

### Tjänst (Windows)

#### Förutsättningar (Tjänst)

- [Du måste redan ha installerat Readarr](#windows)
- Du måste ha [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installerat. För att installera, ladda ner den senaste versionen (2.24 vid skrivande tidpunkt) och kopiera antingen 32-bitars eller 64-bitars nssm.exe-filen till C:/windows/system32.
  - Om du är osäker på om du har ett 32-bitars eller 64-bitars system, kontrollera Inställningar => System => Om => Systemtyp.

#### Konfigurera Readarr-tjänst

1. Öppna ett kommandotolksadministratörfönster. (För att köra som administratör,
    högerklicka på kommandotolksikonen och välj "Kör som
    administratör".)
1. Om Readarr körs, stoppa tjänsten genom att köra `nssm stop Readarr`
    i kommandotolken.
1. Nu måste vi redigera den befintliga Readarr-instansen för att explicit peka
    till sin datakatalog. Standardkommandot är följande:
    `sc config Readarr binpath= "C:\ProgramData\Readarr\bin\Readarr.exe
    -data=C:\ProgramData\Readarr"`

Detta kommando talar om för den ursprungliga instansen av Readarr att använda
`C:\ProgramData\Readarr` som sin datakatalog. Om du inte använde den
standardinstallationen av Readarr, eller om din datakatalog är någon annanstans, måste du
ändra dina sökvägar här.

#### Skapa Readarr-ljudböcker-tjänst

1. Skapa en ny mapp där du vill att Readarr-ljudböcker ska finnas. De flesta använder en liknande plats som
    `C:\ProgramData\Readarr-ljudböcker`
1. Återgå till kommandotolken och skapa den nya Readarr-ljudböcker-tjänsten med `nssm
    install Readarr-ljudböcker`. Ett popup-fönster öppnas där du kan skriva in dina
    parametrar för den nya instansen. För detta exempel kommer vi att använda
    följande:
      - Sökväg: `C:\ProgramData\Readarr\bin\Readarr.exe`
      - Startmapp: `C:\ProgramData\Readarr\bin`
      - Argument: `-data=C:\ProgramData\Readarr-ljudböcker`

> Observera att **Argument** pekar på den *nya* mappen som skapades i steg 1.
Detta är avgörande, eftersom det håller alla datafiler från båda instanserna i
separerade platser. {.is-warning}

1. Klicka på *Installera tjänst*. Fönstret ska stängas och tjänsten
    kommer nu att vara tillgänglig att köra.
1. Fortsätt till [Konfigurera Readarr-ljudböcker](#windows-multi-config-second)

### Tray App (Windows)

#### Förutsättningar (Tray App)

- [Du måste redan ha installerat Readarr](#windows)
- Readarr måste vara konfigurerat med ett `/data=` argument för att tillåta flera instanser
- Navigera till Startmappen för den aktuella användaren `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` och redigera den befintliga genvägen om det behövs.

#### Skapa Readarr-ljudböcker Tray App

- Högerklicka och skapa en ny genväg
- Sökväg: `C:\ProgramData\Readarr\bin\Readarr.exe /data=C:\ProgramData\Readarr-ljudböcker`
- Ge genvägen ett unikt namn som `Readarr-ljudböcker` och slutför guiden.
- Dubbelklicka på den nya genvägen för att köra och testa.
- Fortsätt till [Konfigurera Readarr-ljudböcker](#windows-multi-config-second)

### Konfigurera Readarr-ljudböcker {#windows-multi-config-second}

- Oavsett om du använde Tjänstmetoden eller Tray App: Stoppa både tjänsterna och apparna
- Starta Readarr-ljudböcker (tjänst eller Tray App)
- Öppna Readarr-ljudböcker och navigera inom appen till [Inställningar => Allmänt => Värd](/readarr/settings/#host)
- Ändra `Portnummer` från `8787` till en annan port, t.ex. `8879`, så att Readarr och Readarr-ljudböcker inte kommer i konflikt
- Du bör nu kunna starta båda apparna
- Fortsätt till [Hantera uppdateringar](#dealing-with-updates)

### Hantera uppdateringar

- Inaktivera automatiska uppdateringar i en av dina instanser
- Om en Readarr-instans uppdateras stängs båda instanserna av och bara den uppdaterade startas om. För att åtgärda detta måste du manuellt starta den andra instansen, eller så kan du titta på att använda det nedanstående PowerShell-skriptet för att åtgärda problemet.

#### PowerShell-skript för att kontrollera och starta om Windows-portar

{#win-portchecker}

- När du använder två Readarr-instanser och en av dem uppdateras, kommer den att stänga av alla instanser. Bara den som uppdateras kommer att komma tillbaka online.
- Nedanstående PowerShell-skript bör konfigureras som en schemalagd uppgift.
- Det kontrollerar portarna och om en inte är online kommer det att (om)starta den schemalagda uppgiften för att starta Readarr.

1. Skapa en ny fil och namnge den ReadarrInstancesChecker.ps1 med följande kod.
1. Redigera skriptet med dina faktiska tjänstenamn, IP och portar.
1. [Skapa en schemalagd uppgift](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) för att köra skriptet enligt en upprepad tidtabell.

- Säkerhetsalternativ: Aktivera `Kör med högsta behörighet`
  - Annars kommer skriptet inte att kunna manipulera tjänster
- Utlösare: `Vid start`
- Upprepa uppgiften varje: `5` eller `10` minuter
- Åtgärd: `Starta ett program`
- Program/skript: `powershell`
- Argument: `-File D:\ReadarrInstancesChecker.ps1`
  - Se till att du använder den fullständiga sökvägen till skriptets plats

```powershell
################################################################################################
### ReadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Håller flera Readarr-instanser igång genom att kontrollera porten                           ###
### Använd Readarrs Discord eller Reddit för support!                                          ###
### https://wiki.servarr.com/readarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Uppdaterad: 2020-10-22                                                                    ###
### Författare:  reloxx13                                                                      ###
################################################################################################



### ANGE DIN KONFIGURATION HÄR ###
# Ange din värd-IP och port korrekt och använd dina tjänste- eller schemalagda uppgiftsnamn!

# (sträng) Typen av hur Readarr startas
# "Tjänst" (standard) Tjänstprocess används
# "Schemalagd uppgift" Uppgiftsplaneraren används
$starttyp = 'Tjänst'

# (bool) Skriver loggen till C:\Users\DITTANVÄNDARNAMN\log.txt när den är aktiverad
# $false (standard)
# $true
$loggaTillFil = $false


$instanser = @(
    [pscustomobject]@{   # Instans 1
        Namn = 'Readarr'; # (sträng) Tjänste- eller uppgiftsnamn (standard: Readarr)
        IP   = '192.168.178.12'; # (sträng) Server-IP där Readarr körs (standard: 192.168.178.12)
        Port = '8873'; # (sträng) Serverport där Readarr körs (standard: 8873)
    }
    [pscustomobject]@{   # Instans 2
        Namn = 'Readarr-ljudböcker'; # (sträng) Tjänste- eller uppgiftsnamn (standard: Readarr-ljudböcker)
        IP   = '192.168.178.12'; # (sträng) Server-IP där Readarr körs (standard: 192.168.178.12)
        Port = '8874'; # (sträng) Serverport där Readarr körs (standard: 8874)
    }
    # Om det behövs kan du lägga till fler instanser här... genom att ta bort kommentarer från nedanstående rader
    # [pscustomobject]@{   # Instans 3
    # Namn='Readarr-3D';    # (sträng) Tjänste- eller uppgiftsnamn (standard: Readarr-3D)
    # IP='192.168.178.12'; # (sträng) Server-IP där Readarr körs (standard: 192.168.178.12)
    # Port='8875';         # (sträng) Serverport där Readarr körs (standard: 7875)
    # }
)


### ÄNDRA INGET UNDER DENNA RAD ###


###
# Denna funktion skriver till en loggfil eller till konsolens utdata
###
function Skriv-Logg
{
    #Kommer att skriva till C:\Users\DITTANVÄNDARNAMN\log.txt
    
    Param(
        $Meddelande,
        $Sökväg = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    #Konsolens utdata
    Write-Output "[$(TS)]$Meddelande"
    
    #Filutdata
    if ($loggaTillFil)
    {
        "[$(TS)]$Meddelande" | Tee-Object -FilePath $Sökväg -Append | Write-Verbose
    }
}


Skriv-Logg 'START ====================='


$instanser | ForEach-Object {
    Skriv-Logg "Kontrollera $($_.Namn) $($_.IP):$($_.Port)"
    
    $PortÖppen = ( Test-NetConnection $_.IP -Port $_.Port -WarningAction SilentlyContinue ).TcpTestSucceeded 
    
    if (!$PortÖppen)
    {
        Skriv-Logg "Port $($_.Port) är stängd, starta om $($starttyp) $($_.Namn)!"

        if ($starttyp -eq 'Tjänst')
        {
            Get-Service -Name $_.Namn | Stop-Service
            Get-Service -Name $_.Namn | Start-Service
        }
        elseif ($starttyp -eq 'Schemalagd uppgift')
        {
            Get-ScheduledTask -TaskName $_.Namn | Stop-ScheduledTask
            Get-ScheduledTask -TaskName $_.Namn | Start-ScheduledTask
        }
        else
        {
            Skriv-Logg '[FEL] STARTTYP OKÄND! ANVÄND Tjänst eller Schemalagd uppgift!'
        }
    }
    else
    {
        Skriv-Logg "Port $($_.Port) är öppen!"
    }
}

Skriv-Logg 'SLUT ====================='
```

## Linux - Flera instanser

{#linux-multi}

- [Swizzin-användare](https://github.com/ComputerByte/readarr-audiobooks)
- Användare som inte använder Swizzin
  - Se till att din första instans har det `-data=` argumentet som skickas.
  - Stoppa tillfälligt din första instans så att du kan ändra den andra instansens port `systemctl stop readarr`
  - Inaktivera automatiska uppdateringar för en av dina Readarr-instanser

> Nedan finns ett exempelskript för att skapa en Readarr-ljudböcker-instans. Det nedanstående systemd-skriptet kommer att använda en datakatalog på `/var/lib/readarr-ljudböcker/`. Se till att katalogen finns eller ändra den vid behov.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr-ljudböcker.service > /dev/null
[Unit]
Description=Readarr-ljudböcker Daemon
After=syslog.target network.target
[Service]
User=readarr
Group=media
Type=simple

ExecStart=/opt/Readarr/Readarr -nobrowser -data=/var/lib/Readarr-ljudböcker/
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

- Aktivera Readarr-ljudböcker-tjänsten:

```shell
sudo systemctl enable --now -q readarr-ljudböcker
```

## MacOS - Flera instanser

{#macos-multi}

Denna guide gjordes och testades med macOS 13 (Ventura), men bör fungera på vilken version som helst som Readarr stöder.

### Förutsättningar
- Readarr-applikationen måste vara installerad i `/Applications`-mappen
- Om Readarr redan har använts tidigare kommer all data att förloras. Flytta `~/.config/Readarr` till `~/.config/readarr-books` eller `~/.config/readarr-audiobooks` för att behålla data.

### Skapa applikationer (starta Readarr enkelt)
Du kommer att skapa två nya applikationer: "Readarr Books" och "Readarr Audiobooks".

- Öppna Automator-appen
- Välj `Ny dokument`, sedan `Applikation`
- Använd sökrutan längst upp till vänster för att söka efter `Kör skalprogram`, dubbelklicka sedan på det
- I rutan som öppnas klistrar du in följande:

```shell
# Readarr Books
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-books
```



- Spara applikationen som `Readarr Books`
- Gå till `Fil` > `Duplicera` i menyraden
- Ersätt innehållet i skriptet med följande:

```shell
# Readarr Audiobooks
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-audiobooks
```

- Spara den nya applikationen som `Readarr Audiobooks`
- Visa applikationerna i Finder, ändra eventuellt deras ikoner efter eget tycke (via `Hämta info`-fönstret).

### Konfigurera instanser
Nu kommer du att ställa in portar och namn för varje instans.

- Välj ett portnummer för varje instans. Till exempel, standardporten `8787` för e-böcker och `8789` för ljudböcker.
- Om en av instanserna använder standardporten, starta den andra först. Annars kan du starta vilken som helst av dem.
- Gå till `Inställningar` > `Allmänt` i Readarr och ange rätt port.

> Valfritt: Slå på avancerade alternativ och ange önskat `Instansnamn`.
{.is-success}

- Starta den andra instansen och gör samma sak.

### Uppdateringar
När du uppdaterar en instans stänger uppdateraren av båda och startar bara om den du uppdaterade. För att komma runt detta kommer en periodisk uppgift för portkontroll att skapas (anpassad men något ändrad från [Windows-guiden](#win-portchecker)).

- Inaktivera automatiska uppdateringar i en av instanserna och se till att aldrig uppdatera den.
- Skapa en ny fil på en plats du kommer ihåg och döp den till `readarrportchecker.zsh`.
- Lägg till följande innehåll:

```shell
#!/bin/zsh

# Första instansens *applikationsnamn*
name0="Readarr Books"
# Första instansens portnummer
port0=8787

# Andra instansens *applikationsnamn*
name1="Readarr Audiobooks"
# Andra instansens portnummer
port1=8789

# Loggning
LOGFILE="$HOME/.local/state/readarr.log"
test -d "$HOME/.local/state" || mkdir -p "$HOME/.local/state"

function checkport {
    lsof -i ":${1}" &>/dev/null
}

# Om en instans körs betyder det att båda ska vara igång
if checkport "${port0}" && ! checkport "${port1}"; then
		open -a "${name1}"
    echo "Öppnade ${name1}" >> "$LOGFILE"
elif checkport "${port1}" && ! checkport "${port0}"; then
		open -a "${name0}"
    echo "Öppnade ${name0}" >> "$LOGFILE"
fi
```

- Gör skriptet körbart:

```shell
chmod +x readarrportchecker.zsh
```

- Schemalägg skriptet att köras periodiskt. Skapa en ny fil i `~/Library/LaunchAgents` med namnet `local.readarr.portchecker.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>local.readarr.portchecker</string>
    <key>Program</key>
    <!-- Hitta sökvägen genom att högerklicka, sedan Option och kopiera -->
    <string>/sökväg/till/readarrportchecker.zsh</string>
    <key>StartInterval</key>
    <!-- Periodiskt intervall i sekunder. 300 för fem minuter,
         600 för tio minuter. -->
    <integer>300</integer>
  </dict>
</plist>
```

- Ändra filen enligt kommentarerna
- Antingen logga ut och logga in igen eller ladda in filen manuellt:

```shell
launchctl load ~/Library/LaunchAgents/local.readarr.portchecker.plist
```

> `TODO`: Eventuellt integrera detta i ett anpassat skript för uppdateringsprocessen, eller observera filändringar istället för att köra var 300:e sekund.
{.is-info}

## Docker med flera instanser

{#docker-multi}

- Starta helt enkelt upp en andra Docker-kontainer med ett annat namn och se till att de ovanstående kraven uppfylls.