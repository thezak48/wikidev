---
title: multiple-instances
description: 
published: true
date: 2023-09-01T05:05:47.102Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:10.189Z
---

# Flere instanser

Det er mulig å kjøre flere instanser av Radarr. Dette gjøres vanligvis når man ønsker en 4K- og en 1080p-kopi av en film. Merk at du kan (og bør sannsynligvis) [gå gjennom TRaSHs guide og konfigurere Radarr til å bruke en annen Radarr som en liste](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/). Dette er nyttig hvis du ønsker å holde begge instansene synkronisert.

- [Flere instanser på Windows](#windows-multi)
- [Flere instanser på Linux](#linux-multi)
- [Flere instanser med Docker](#docker-multi)
{.links-list}

Følgende krav bør merkes:

- Hvis du ikke bruker Docker, bør de samme binærene (programfilene) brukes
- Hvis du ikke bruker Docker, *må* alle instansene ha et `-data=` eller `/data=` argument
- Hvis du ikke bruker Docker, må forskjellige porter brukes
  - Hvis du bruker Docker, må forskjellige eksterne porter brukes
- Forskjellige kategorier for nedlastingsklienter må brukes
- Forskjellige rotmapper må brukes.
- Hvis du ikke bruker Docker, deaktiver automatisk oppdatering på alle instansene unntatt én.

## Flere instanser på Windows

{#windows-multi}

Denne veiledningen viser deg hvordan du kjører flere instanser av Radarr på Windows ved å bruke bare én grunnleggende installasjon. Denne veiledningen ble satt sammen ved hjelp av Windows 10; hvis du bruker en tidligere versjon av Windows (7, 8, osv.) kan du måtte justere noen ting. Denne veiledningen antar også at du har installert Radarr i standardkatalogen, og at den andre instansen av Radarr vil bli kalt Radarr-4K. Du kan gjerne endre ting for å passe dine egne installasjoner.

> Merk: Du bør kjøre Radarr enten som [en tjeneste](#service-windows) eller som en [tray-app](#tray-app-windows). Å kjøre både en app og en tjeneste er unødvendig og kan føre til problemer.

### Tjeneste (Windows)

#### Forutsetninger (Tjeneste)

- [Du må allerede ha installert Radarr](#windows)
- Du må ha [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installert. For å installere, last ned den nyeste versjonen (2.24 ved skrivetidspunktet) og kopier enten 32-biters eller 64-biters nssm.exe-filen til C:/windows/system32.
  - Hvis du er usikker på om du har et 32-biters eller 64-biters system, sjekk Innstillinger => System => Om => Systemtype.

#### Konfigurere Radarr-tjeneste

1. Åpne et ledetekstvindu som administrator. (For å kjøre som administrator,
    høyreklikk på ledetekstikonet og velg "Kjør som administrator".)
1. Hvis Radarr kjører, stopp tjenesten ved å kjøre `nssm stop Radarr`
    i ledetekstvinduet.
1. Nå må vi redigere den eksisterende Radarr-instansen for å eksplisitt peke
    til sin datamappe. Standardkommandoen er som følger:
    `sc config Radarr binpath= "C:\ProgramData\Radarr\bin\Radarr.exe
    -data=C:\ProgramData\Radarr"`

Denne kommandoen forteller den opprinnelige Radarr-instansen å bruke
`C:\ProgramData\Radarr` som sin datamappe. Hvis du ikke brukte standard Radarr-installasjon, eller hvis datamappen din er et annet sted, må du endre banene her.

#### Opprette Radarr-4K-tjeneste

1. Opprett en ny mappe der du vil at Radarr-4K skal være. De fleste bruker et lignende sted som
    `C:\ProgramData\Radarr-4K`
1. Gå tilbake til ledetekstvinduet og opprett den nye Radarr-4K-tjenesten ved å bruke `nssm
    install Radarr-4K`. Et popup-vindu åpnes der du kan skrive inn parameterne for den nye instansen. For dette eksempelet vil vi bruke følgende:
      - Bane: `C:\ProgramData\Radarr\bin\Radarr.exe`
      - Oppstartskatalog: `C:\ProgramData\Radarr\bin`
      - Argumenter: `-data=C:\ProgramData\Radarr-4K`
      - Kategorien Avslutningshandlinger
        - Start på nytt: Start programmet på nytt
        - Forsinkelse: 120000 ms
        (2 minutter, kan være lengre hvis oppdateringen ikke fullføres i tide)

> Merk at **Argumenter** peker på den *nye* mappen som ble opprettet i trinn 1.
Dette er avgjørende, da det holder alle datafilene fra begge instansene i
separate plasseringer. {.is-warning}

1. Klikk på *Installer tjeneste*. Vinduet skal lukkes og tjenesten
    vil nå være tilgjengelig for å kjøre.
1. Fortsett til [Konfigurere Radarr-4K](#windows-multi-config-second)

### Tray-app (Windows)

#### Forutsetninger (Tray-app)

- [Du må allerede ha installert Radarr](#windows)
- Radarr-snarveien må være konfigurert med et `/data=` argument i 'mål'-feltet for å tillate flere instanser
- Gå til oppstartsmappen for gjeldende bruker `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` og rediger den eksisterende snarveien om nødvendig.

#### Opprette Radarr-4K Tray-app

- Opprett en ny mappe for Radarr-4Ks konfigurasjonsfiler. De fleste bruker et lignende sted som
    `C:\ProgramData\Radarr-4K`
- Høyreklikk og opprett en ny snarvei
- Bane: `C:\ProgramData\Radarr\bin\Radarr.exe /data=C:\ProgramData\Radarr-4K`
- Gi snarveien et unikt navn som `Radarr-4K` og fullfør veiviseren.
- Dobbeltklikk på den nye snarveien for å kjøre og teste.
- Fortsett til [Konfigurere Radarr-4K](#windows-multi-config-second)

### Konfigurere Radarr-4K {#windows-multi-config-second}

- Uavhengig av om du brukte tjenestemetoden eller tray-appen: Stopp begge tjenestene og appene
- Start Radarr-4K (tjeneste eller tray-app)
- Åpne Radarr-4K og naviger i appen til [Innstillinger => Generelt => Vert](/radarr/settings/#host)
- Endre `Portnummer` fra `7878` til en annen port, f.eks. `7879`, slik at Radarr og Radarr4K ikke kommer i konflikt
- Du bør nå kunne starte begge appene
- Fortsett til [Håndtering av oppdateringer](#dealing-with-updates)

### Håndtering av oppdateringer

> - Deaktiver automatisk oppdatering i én av instansene dine
  - I config.xml endrer du oppdateringsgrensen til `<Branch>nonexistent</Branch>`
- Hvis én Radarr-instans blir oppdatert, vil begge instansene avsluttes og bare den oppdaterte vil starte på nytt. For å løse dette må du manuelt starte den andre instansen, eller du kan se på å bruke PowerShell-skriptet nedenfor for å løse problemet.

> Hvis [NSSM Exit Action](#creating-radarr-4k-service) er konfigurert riktig, kan Radarr oppdateres og starte på nytt flere ganger uten ekstra skript.
Hvis omstartsforsinkelsen ikke er konfigurert som standard, vil den starte instansen umiddelbart på nytt.
Dette kan forhindre at oppdateringer blir brukt, og kan føre til følgende feil: `Radarr was restarted prematurely by external process.` {.is-info}

#### PowerShell-skript for sjekking og omstart av porter på Windows

- Når du bruker to Radarr-instanser og én av dem blir oppdatert, vil den drepe alle instansene. Bare den som blir oppdatert, vil starte på nytt.
- PowerShell-skriptet nedenfor bør konfigureres som en planlagt oppgave.
- Det sjekker portene, og hvis én ikke er online, vil det starte (på nytt) den planlagte oppgaven for å starte Radarr.

1. Opprett en ny fil og navngi den RadarrInstancesChecker.ps1 med følgende kode.
1. Rediger skriptet med dine faktiske tjenestenavn, IP-adresse og porter. *Hvis du kjører i Tray-modus, må du opprette planlagte oppgaver for å starte hver Radarr-instans og bruke de oppgavenavnene i skriptet nedenfor.*
1. [Opprett en planlagt oppgave](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) for å kjøre skriptet med jevne mellomrom.

- Sikkerhetsalternativer: Aktiver `Kjør med høyeste privilegier`
  - Ellers vil skriptet ikke kunne manipulere tjenester
- Utløser: `Ved oppstart`
- Gjenta oppgaven hver: `5` eller `10` minutter
- Handling: `Start et program`
- Program/skript: `powershell`
- Argument: `-File D:\RadarrInstancesChecker.ps1`
  - Sørg for å bruke den fulle banen til skriptets plassering

```powershell
################################################################################################
### RadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Holder flere Radarr-instanser oppe ved å sjekke porten                                   ###
### Bruk Radarrs Discord eller Reddit for støtte!                                            ###
### https://wiki.servarr.com/radarr/installation#windows-multi                               ###
################################################################################################
### Versjon: 1.1                                                                             ###
### Oppdatert: 2020-10-22                                                                    ###
### Forfatter:  reloxx13                                                                      ###
################################################################################################



### ANGIs KONFIGURASJONEN DIN HER ###
# Angi IP-adressen og porten til Radarr riktig og bruk tjenestenavnene eller navnene på planlagte oppgaver!

# (string) Typen hvordan Radarr starter
# "Service" (standard) Bruker tjenesteprosessen
# "ScheduledTask" Bruker Oppgaveplanleggeren
$startType = 'Service'

# (bool) Skriver loggen til C:\Users\DINBRUKERNAVN\log.txt når den er aktivert
# $false (standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instans 1
        Name = 'Radarr-V3'; # (string) Tjeneste- eller oppgavenavn (standard: Radarr-V3)
        IP   = '192.168.178.12'; # (string) Server-IP der Radarr kjører (standard: 192.168.178.12)
        Port = '7873'; # (string) Serverport der Radarr kjører (standard: 7873)
    }
    [pscustomobject]@{   # Instans 2
        Name = 'Radarr-4K'; # (string) Tjeneste- eller oppgavenavn (standard: Radarr-4K)
        IP   = '192.168.178.12'; # (string) Server-IP der Radarr kjører (standard: 192.168.178.12)
        Port = '7874'; # (string) Serverport der Radarr kjører (standard: 7874)
    }
    # Hvis nødvendig kan du legge til flere instanser her... ved å fjerne kommenteringen på linjene nedenfor
    # [pscustomobject]@{   # Instans 3
    # Name='Radarr-3D';    # (string) Tjeneste- eller oppgavenavn (standard: Radarr-3D)
    # IP='192.168.178.12'; # (string) Server-IP der Radarr kjører (standard: 192.168.178.12)
    # Port='7875';         # (string) Serverport der Radarr kjører (standard: 7875)
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

## Flere instanser på Linux

{#linux-multi}

- [Swizzin-brukere](https://github.com/ComputerByte/radarr4k)
- Brukere som ikke bruker Swizzin
  - Sørg for at den første instansen har `-data=`-argumentet.
  - Stopp midlertidig den første instansen, slik at du kan endre porten til den andre instansen `systemctl stop radarr`
  - Deaktiver automatisk oppdatering på én av Radarr-instansene dine

> Nedenfor er et eksempel på et skript for å opprette en Radarr4K-instans. Det følgende systemd-opprettingsskriptet vil bruke en datamappe på `/var/lib/radarr4k/`. Sørg for at mappen eksisterer eller endre den etter behov.{.is-danger}

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

- Last inn systemd:

```shell
sudo systemctl -q daemon-reload
```

- Aktiver Radarr4k-tjenesten:

```shell
sudo systemctl enable --now -q radarr4k
```

## Docker flere instanser

{#docker-multi}

- Enkelt og greit, opprett en annen Docker-container med et annet navn, og sørg for at de ovennevnte kravene er oppfylt.