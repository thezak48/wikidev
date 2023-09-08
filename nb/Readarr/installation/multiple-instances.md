# Flere instanser

Det er mulig å kjøre flere instanser av Readarr. Dette gjøres vanligvis når man ønsker en lydbok- og ebok-kopi av en bok.
Merk at du kan konfigurere Readarr til å bruke en annen Readarr som en liste. Dette er nyttig hvis du ønsker å holde begge synkronisert.

- [Windows flere instanser](#windows-multi)
- [Linux flere instanser](#linux-multi)
- [MacOS flere instanser](#macos-multi)
- [Docker flere instanser](#docker-multi)
{.links-list}

Følgende krav bør merkes:

- Hvis det ikke er Docker, bør de samme binærene (programfilene) brukes
- Hvis det ikke er Docker, *må* alle instanser ha en `-data=` eller `/data=` argument som blir sendt
- Hvis det ikke er Docker, må forskjellige porter brukes
  - Hvis det er Docker, må forskjellige eksterne porter brukes
- Forskjellige nedlastingsklientkategorier må brukes
- Forskjellige rotmapper må brukes.
- Hvis det ikke er Docker, deaktiver automatisk oppdatering på alle unntatt 1 instans.

## Windows flere instanser

{#windows-multi}

Denne veiledningen viser deg hvordan du kjører flere instanser av Readarr på Windows ved hjelp av bare én grunninstallasjon. Denne veiledningen ble satt sammen ved hjelp av Windows 10; hvis du bruker en tidligere versjon av Windows (7, 8, osv.) kan du måtte justere noen ting. Denne veiledningen antar også at du har installert Readarr i standardkatalogen, og at den andre instansen av Readarr vil bli kalt Readarr-audiobooks. Du kan gjerne endre ting for å passe dine egne installasjoner.

### Tjeneste (Windows)

#### Forutsetninger (Tjeneste)

- [Du må allerede ha installert Readarr](#windows)
- Du må ha [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installert. For å installere, last ned den nyeste versjonen (2.24 ved skrivetidspunktet) og kopier enten 32-biters eller 64-biters nssm.exe-filen til C:/windows/system32.
  - Hvis du er usikker på om du har et 32-biters eller 64-biters system, sjekk Innstillinger => System => Om => Systemtype.

#### Konfigurere Readarr-tjeneste

1. Åpne et ledetekstadministratorvindu. (For å kjøre som administrator,
    høyreklikk på ledetekstikonet og velg "Kjør som
    administrator".)
1. Hvis Readarr kjører, stopp tjenesten ved å kjøre `nssm stop Readarr`
    i ledeteksten.
1. Nå må vi redigere den eksisterende Readarr-instansen for å peke
    eksplisitt på sin datamappe. Standardkommandoen er som følger:
    `sc config Readarr binpath= "C:\ProgramData\Readarr\bin\Readarr.exe
    -data=C:\ProgramData\Readarr"`

Denne kommandoen forteller den opprinnelige Readarr-instansen å bruke
`C:\ProgramData\Readarr` eksplisitt for sin datamappe. Hvis du ikke brukte
standardinstallasjonen av Readarr, eller hvis datakatalogen din er et annet sted, må du
kanskje endre banene her.

#### Opprette Readarr-audiobooks-tjeneste

1. Opprett en ny mappe der du vil at Readarr-audiobooks skal være. De fleste bruker et lignende sted som
    `C:\ProgramData\Readarr-audiobooks`
1. Gå tilbake til ledeteksten og opprett den nye Readarr-audiobooks-tjenesten ved hjelp av `nssm
    install Readarr-audiobooks`. Et popup-vindu åpnes der du kan skrive inn parametrene for den nye instansen. For dette eksempelet vil vi bruke
    følgende:
      - Bane: `C:\ProgramData\Readarr\bin\Readarr.exe`
      - Oppstartskatalog: `C:\ProgramData\Readarr\bin`
      - Argumenter: `-data=C:\ProgramData\Readarr-audiobooks`

> Merk at **Argumenter** peker på den *nye* mappen som ble opprettet i trinn 1.
Dette er avgjørende, da det holder alle datafilene fra begge instansene i
separate steder. {.is-warning}

1. Klikk på *Installer tjeneste*. Vinduet skal lukkes og tjenesten
    vil nå være tilgjengelig for å kjøre.
1. Fortsett til [Konfigurere Readarr-audiobooks](#windows-multi-config-second)

### Bakgrunnsprogram (Windows)

#### Forutsetninger (Bakgrunnsprogram)

- [Du må allerede ha installert Readarr](#windows)
- Readarr må være konfigurert med et `/data=` argument for å tillate flere instanser
- Gå til oppstartsmappen for gjeldende bruker `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` og rediger den eksisterende snarveien om nødvendig.

#### Opprette Readarr-audiobooks bakgrunnsprogram

- Høyreklikk og opprett en ny snarvei
- Bane: `C:\ProgramData\Readarr\bin\Readarr.exe /data=C:\ProgramData\Readarr-audiobooks`
- Gi snarveien et unikt navn som f.eks. `Readarr-audiobooks` og fullfør veiviseren.
- Dobbeltklikk på den nye snarveien for å kjøre og teste.
- Fortsett til [Konfigurere Readarr-audiobooks](#windows-multi-config-second)

### Konfigurere Readarr-audiobooks {#windows-multi-config-second}

- Uavhengig av om du brukte tjenestemetoden eller bakgrunnsprogrammet: Stopp begge tjenestene og begge programmene
- Start Readarr-audiobooks (tjeneste eller bakgrunnsprogram)
- Åpne Readarr-audiobooks og naviger i appen til [Innstillinger => Generelt => Vert](/readarr/settings/#host)
- Endre `Portnummer` fra `8787` til en annen port, f.eks. `8879`, slik at Readarr og Readarr-audiobooks ikke kommer i konflikt
- Du bør nå kunne starte begge appene
- Fortsett til [Håndtering av oppdateringer](#dealing-with-updates)

### Håndtering av oppdateringer

- Deaktiver automatisk oppdatering i én av instansene dine
- Hvis én Readarr-instans blir oppdatert, vil begge instansene avsluttes og bare den oppdaterte vil starte igjen. For å løse dette må du manuelt starte den andre instansen, eller du kan se på å bruke PowerShell-skriptet nedenfor for å løse problemet.

#### PowerShell-skript for sjekking og omstart av porter i Windows

{#win-portchecker}

- Når du bruker to Readarr-instanser og én av dem blir oppdatert, vil den drepe alle instansene. Bare den som blir oppdatert vil komme online igjen.
- PowerShell-skriptet nedenfor bør konfigureres som en planlagt oppgave.
- Det sjekker portene, og hvis én ikke er online, vil det (om)starte den planlagte oppgaven for å starte Readarr.

1. Opprett en ny fil og gi den navnet ReadarrInstancesChecker.ps1 med følgende kode.
1. Rediger skriptet med dine faktiske tjenestenavn, IP-adresse og porter.
1. [Opprett en planlagt oppgave](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) for å kjøre skriptet med jevne mellomrom.

- Sikkerhetsalternativer: Aktiver `Kjør med høyeste privilegier`
  - Ellers vil skriptet ikke kunne manipulere tjenester
- Utløser: `Ved oppstart`
- Gjenta oppgave hver: `5` eller `10` minutter
- Handling: `Start et program`
- Program/skript: `powershell`
- Argument: `-File D:\ReadarrInstancesChecker.ps1`
  - Sørg for å bruke den fulle banen til skriptets plassering

```powershell
################################################################################################
### ReadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Holder flere Readarr-instanser oppe ved å sjekke porten                                    ###
### Bruk Readarrs Discord eller Reddit for støtte!                                             ###
### https://wiki.servarr.com/readarr/installation#windows-multi                               ###
################################################################################################
### Versjon: 1.1                                                                             ###
### Oppdatert: 2020-10-22                                                                    ###
### Forfatter:  reloxx13                                                                      ###
################################################################################################



### ANGIs KONFIGURASJONEN DIN HER ###
# Angi IP-adressen og porten for Readarr riktig og bruk tjenestenavnene eller planlagte oppgavenavnene dine!

# (string) Typen hvordan Readarr starter
# "Service" (standard) Bruker tjenesteprosessen
# "ScheduledTask" Bruker oppgaveplanleggeren
$startType = 'Service'

# (bool) Skriver loggen til C:\Users\DINBRUKERNAVN\log.txt når den er aktivert
# $false (standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instans 1
        Name = 'Readarr'; # (string) Tjeneste- eller oppgavenavn (standard: Readarr)
        IP   = '192.168.178.12'; # (string) Server-IP der Readarr kjører (standard: 192.168.178.12)
        Port = '8873'; # (string) Serverport der Readarr kjører (standard: 8873)
    }
    [pscustomobject]@{   # Instans 2
        Name = 'Readarr-audiobooks'; # (string) Tjeneste- eller oppgavenavn (standard: Readarr-audiobooks)
        IP   = '192.168.178.12'; # (string) Server-IP der Readarr kjører (standard: 192.168.178.12)
        Port = '8874'; # (string) Serverport der Readarr kjører (standard: 8874)
    }
    # Hvis nødvendig kan du legge til flere instanser her... ved å fjerne kommenteringen fra linjene nedenfor
    # [pscustomobject]@{   # Instans 3
    # Name='Readarr-3D';    # (string) Tjeneste- eller oppgavenavn (standard: Readarr-3D)
    # IP='192.168.178.12'; # (string) Server-IP der Readarr kjører (standard: 192.168.178.12)
    # Port='8875';         # (string) Serverport der Readarr kjører (standard: 7875)
    # }
)


### IKKE ENDRE NOE UNDER DENNE LINJEN ###


###
# Denne funksjonen skriver til en loggfil eller i konsollutdata
###
function Write-Log
{
    # Skriver til C:\Users\DINBRUKERNAVN\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    # Konsollutdata
    Write-Output "[$(TS)]$Message"
    
    # Filutdata
    if ($logToFile)
    {
        "[$(TS)]$Message" | Tee-Object -FilePath $Path -Append | Write-Verbose
    }
}


Write-Log 'START ====================='


$instances | ForEach-Object {
    Write-Log "Sjekker $($_.Name) $($_.IP):$($_.Port)"
    
    $PortOpen = ( Test-NetConnection $_.IP -Port $_.Port -WarningAction SilentlyContinue ).TcpTestSucceeded 
    
    if (!$PortOpen)
    {
        Write-Log "Port $($_.Port) er lukket, starter $($startType) $($_.Name) på nytt!"

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
        Write-Log "Port $($_.Port) er åpen!"
    }
}

Write-Log 'END ====================='
```

## Linux flere instanser

{#linux-multi}

- [Swizzin-brukere](https://github.com/ComputerByte/readarr-audiobooks)
- Brukere som ikke bruker Swizzin
  - Sørg for at den første instansen har `-data=` argumentet sendt.
  - Stopp midlertidig den første instansen, slik at du kan endre porten til den andre instansen `systemctl stop readarr`
  - Deaktiver automatisk oppdatering på én av Readarr-instansene dine

> Nedenfor er et eksempel på et skript for å opprette en Readarr-audiobooks-instans. Det nedenstående systemd-opprettingsskriptet vil bruke en datamappe på `/var/lib/readarr-audiobooks/`. Sørg for at mappen eksisterer eller endre den etter behov.{.is-danger}

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

- Last inn systemd på nytt:

```shell
sudo systemctl -q daemon-reload
```

- Aktiver Readarr-audiobooks-tjenesten:

```shell
sudo systemctl enable --now -q readarr-audiobooks
```

## MacOS flere instanser

{#macos-multi}

Denne veiledningen ble laget og testet med macOS 13 (Ventura), men bør fungere på hvilken som helst versjon som Readarr støtter.

### Forutsetninger
- Readarr-applikasjonen må være installert i `/Applications`-mappen
- Hvis Readarr allerede har blitt brukt tidligere, vil all data gå tapt. Flytt `~/.config/Readarr` til `~/.config/readarr-books` eller `~/.config/readarr-audiobooks` for å beholde dataene.

### Opprette applikasjoner (start Readarr enkelt)
Du vil opprette to nye applikasjoner: "Readarr Books" og "Readarr Audiobooks".

- Åpne Automator-appen
- Velg `Ny dokument`, deretter `Applikasjon`
- Bruk søkeboksen øverst til venstre for å søke etter `Kjør skallskript`, og dobbeltklikk på det
- I boksen som åpnes, lim inn følgende:

```shell
# Readarr Books
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-books
```



- Lagre applikasjonen som `Readarr Books`
- Gå til `Fil` > `Dupliser` i menylinjen
- Erstatt innholdet i skriptet med følgende:

```shell
# Readarr lydbøker
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-lydbøker
```

- Lagre den nye applikasjonen som `Readarr lydbøker`
- Se på applikasjonene i Finder, og endre eventuelt ikonene etter eget ønske (via `Få info`-vinduet).

### Konfigurere instanser
Nå skal du sette porter og navn for hver instans.

- Velg et portnummer for hver instans. For eksempel, standard `8787` for e-bøker og `8789` for lydbøker.
- Hvis en av instansene bruker standard portnummer, start den andre først. Ellers, start en av dem.
- Gå til `Innstillinger` > `Generelt` i Readarr, og sett riktig portnummer.

> Valgfritt: Slå på avanserte alternativer og sett `Instansnavn` etter eget ønske.
{.is-success}

- Start den andre instansen og gjør det samme.

### Oppdateringer
Når du oppdaterer en instans, lukker oppdateringsprogrammet begge og starter bare den du oppdaterte. For å omgå dette, vil det bli opprettet en periodisk oppgave for portkontroll (tilpasset, men litt endret fra [Windows-guiden](#win-portchecker)).

- Deaktiver automatisk oppdatering i en av instansene, og sørg for å aldri oppdatere den.
- Opprett en ny fil på et sted du husker, og kall den `readarrportchecker.zsh`.
- Legg til følgende innhold:

```shell
#!/bin/zsh

# Første instans sitt *applikasjonsnavn*
name0="Readarr Books"
# Første instans sitt portnummer
port0=8787

# Andre instans sitt *applikasjonsnavn*
name1="Readarr Audiobooks"
# Andre instans sitt portnummer
port1=8789

# Logging
LOGFILE="$HOME/.local/state/readarr.log"
test -d "$HOME/.local/state" || mkdir -p "$HOME/.local/state"

function checkport {
    lsof -i ":${1}" &>/dev/null
}

# Én instans som kjører betyr at begge skal kjøre
if checkport "${port0}" && ! checkport "${port1}"; then
		open -a "${name1}"
    echo "Åpnet ${name1}" >> "$LOGFILE"
elif checkport "${port1}" && ! checkport "${port0}"; then
		open -a "${name0}"
    echo "Åpnet ${name0}" >> "$LOGFILE"
fi
```

- Gjør skriptet kjørbart:

```shell
chmod +x readarrportchecker.zsh
```

- Planlegg at skriptet skal kjøre periodisk. Opprett en ny fil i `~/Library/LaunchAgents` med navnet `local.readarr.portchecker.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>local.readarr.portchecker</string>
    <key>Program</key>
    <!-- Finn banen ved å høyreklikke, deretter Option og kopier -->
    <string>/path/to/readarrportchecker.zsh</string>
    <key>StartInterval</key>
    <!-- Periodisk intervall i sekunder. 300 for fem minutter,
         600 for ti minutter. -->
    <integer>300</integer>
  </dict>
</plist>
```

- Endre filen i henhold til kommentarene
- Logg ut og logg inn igjen, eller last inn filen manuelt:

```shell
launchctl load ~/Library/LaunchAgents/local.readarr.portchecker.plist
```

> `TODO`: muligens integrer dette i et tilpasset skript for oppdateringsprosessen, eller observer filendringer i stedet for å kjøre hvert 300. sekund.
{.is-info}

## Docker flere instanser

{#docker-multi}

- Start enkelt og greit opp en annen Docker-container med et annet navn, og sørg for at de ovennevnte kravene er oppfylt.