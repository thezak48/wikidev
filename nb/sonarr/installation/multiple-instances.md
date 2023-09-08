---
title: Flere instanser
description: 
published: true
date: 2023-08-20T02:23:13.676Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:35.847Z
---

# Flere instanser

Det er mulig å kjøre flere instanser av Sonarr. Dette gjøres vanligvis når man ønsker en 4K- og 1080p-kopi av en serie.
[Merk at du kan konfigurere Sonarr til å bruke en annen Sonarr som en liste. Dette er nyttig hvis du ønsker å holde begge synkronisert.](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)

- [Flere instanser på Windows](#windows-multi)
- [Flere instanser på Linux](#linux-multi)
- [Flere instanser med Docker](#docker-multi)
{.links-list}

Følgende krav bør merkes:

- Hvis du ikke bruker Docker, bør de samme binærene (programfilene) brukes
- Hvis du ikke bruker Docker, *må* alle instanser ha en `-data=` eller `/data=` argument som blir sendt
- Hvis du ikke bruker Docker, må forskjellige porter brukes
  - Hvis du bruker Docker, må forskjellige eksterne porter brukes
- Forskjellige kategorier for nedlastingsklienter må brukes
- Forskjellige rotmapper må brukes.
- Hvis du ikke bruker Docker, deaktiver automatisk oppdatering på alle instanser unntatt én.

## Flere instanser på Windows

{#windows-multi}

Denne veiledningen viser deg hvordan du kjører flere instanser av Sonarr på Windows ved hjelp av bare én grunnleggende installasjon. Denne veiledningen ble satt sammen ved hjelp av Windows 10; hvis du bruker en tidligere versjon av Windows (7, 8, osv.) kan du måtte justere noen ting. Denne veiledningen antar også at du har installert Sonarr i standardkatalogen, og at den andre instansen av Sonarr vil bli kalt Sonarr-4K. Du kan gjerne endre ting for å passe dine egne installasjoner.

### Tjeneste (Windows)

#### Forutsetninger (Tjeneste)

- [Du må allerede ha installert Sonarr](#windows)
- Du må ha [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installert. For å installere, last ned den nyeste versjonen (2.24 per skrivende stund) og kopier enten 32-biters eller 64-biters nssm.exe-filen til C:/windows/system32.
  - Hvis du er usikker på om du har et 32-biters eller 64-biters system, sjekk Innstillinger => System => Om => Systemtype.

#### Konfigurere Sonarr-tjeneste

1. Åpne et ledetekstvindu som administrator. (For å kjøre som administrator,
    høyreklikk på ledetekstikonet og velg "Kjør som
    administrator".)
1. Hvis Sonarr kjører, stopp tjenesten ved å kjøre `nssm stop Sonarr`
    i ledetekstvinduet.
1. Nå må vi redigere den eksisterende Sonarr-instansen for å peke
    eksplisitt på sin datamappe. Standardkommandoen er som følger:
    `sc config Sonarr binpath= "C:\ProgramData\Sonarr\bin\Sonarr.exe
    -data=C:\ProgramData\Sonarr"`

Denne kommandoen forteller den opprinnelige Sonarr-instansen å bruke
`C:\ProgramData\Sonarr` som sin datamappe. Hvis du ikke brukte
standardinstallasjonen av Sonarr, eller hvis datamappen din er et annet sted, må du
kanskje endre banene her.

#### Opprette Sonarr-4K-tjeneste

1. Opprett en ny mappe der du vil at Sonarr-4K skal være. De fleste bruker et lignende sted som
    `C:\ProgramData\Sonarr-4K`
1. Gå tilbake til ledetekstvinduet og opprett den nye Sonarr-4K-tjenesten ved hjelp av `nssm
    install Sonarr-4K`. Et popup-vindu vil åpnes der du kan skrive inn
    parameterne for den nye instansen. For dette eksempelet vil vi bruke
    følgende:
      - Bane: `C:\ProgramData\Sonarr\bin\Sonarr.exe`
      - Oppstartskatalog: `C:\ProgramData\Sonarr\bin`
      - Argumenter: `-data=C:\ProgramData\Sonarr-4K`

> Merk at **Argumenter** peker på den *nye* mappen som ble opprettet i trinn 1.
Dette er avgjørende, da det holder alle datafilene fra begge instansene i
separate steder. {.is-warning}

1. Klikk på *Installer tjeneste*. Vinduet skal lukkes og tjenesten
    vil nå være tilgjengelig for å kjøre.
1. Fortsett til [Konfigurere Sonarr-4k](#windows-multi-config-second)

### Tray App (Windows)

#### Forutsetninger (Tray App)

- [Du må allerede ha installert Sonarr](#windows)
- Sonarr må være konfigurert med et `/data=` argument for å tillate flere instanser
- Gå til oppstartsmappen for gjeldende bruker `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` og rediger den eksisterende snarveien om nødvendig.

#### Opprette Sonarr-4K Tray App

- Høyreklikk og opprett en ny snarvei
- Bane: `C:\ProgramData\Sonarr\bin\Sonarr.exe /data=C:\ProgramData\Sonarr-4K`
- Gi snarveien et unikt navn som for eksempel `Sonarr-4K` og fullfør veiviseren.
- Dobbeltklikk på den nye snarveien for å kjøre og teste.
- Fortsett til [Konfigurere Sonarr-4k](#windows-multi-config-second)

### Konfigurere Sonarr-4k {#windows-multi-config-second}

- Uavhengig av om du brukte Tjenestemetoden eller Tray App: Stopp begge tjenestene og appene
- Start Sonarr-4k (Tjeneste eller Tray App)
- Åpne Sonarr-4k og naviger i appen til [Innstillinger => Generelt => Vert](/sonarr/settings/#host)
- Endre `Portnummer` fra `8989` til en annen port, f.eks. `7879`, slik at Sonarr og Sonarr4k ikke kommer i konflikt
- Du bør nå kunne starte begge appene
- Fortsett til [Håndtering av oppdateringer](#dealing-with-updates)

### Håndtering av oppdateringer

- Deaktiver automatisk oppdatering i én av instansene dine
- Hvis én Sonarr-instans blir oppdatert, vil begge instansene bli avsluttet og bare den oppdaterte vil starte igjen. For å løse dette må du manuelt starte den andre instansen, eller du kan se på å bruke PowerShell-skriptet nedenfor for å løse problemet.

#### PowerShell-skript for sjekking og omstart av porter på Windows

- Når du bruker to Sonarr-instanser og én av dem blir oppdatert, vil den drepe alle instansene. Bare den som blir oppdatert vil komme tilbake online.
- PowerShell-skriptet nedenfor bør konfigureres som en planlagt oppgave.
- Det sjekker portene, og hvis én ikke er online, vil det starte (om)planleggingen av oppgaven for å starte Sonarr.

1. Opprett en ny fil og kall den SonarrInstancesChecker.ps1 med følgende kode.
1. Rediger skriptet med dine faktiske tjenestenavn, IP-adresse og porter.
1. [Opprett en planlagt oppgave](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) for å kjøre skriptet med jevne mellomrom.

- Sikkerhetsalternativer: Aktiver `Kjør med høyeste privilegier`
  - Ellers vil skriptet ikke kunne manipulere tjenester
- Utløser: `Ved oppstart`
- Gjenta oppgave hver: `5` eller `10` minutter
- Handling: `Start et program`
- Program/skript: `powershell`
- Argument: `-File D:\SonarrInstancesChecker.ps1`
  - Sørg for å bruke den fulle banen til skriptets plassering

```powershell
################################################################################################
### SonarrInstancesChecker.ps1                                                               ###
################################################################################################
### Holder flere Sonarr-instanser oppe ved å sjekke porten                                   ###
### Bruk Sonarrs Discord eller Reddit for støtte!                                            ###
### https://wiki.servarr.com/sonarr/installation#windows-multi                               ###
################################################################################################
### Versjon: 1.1                                                                             ###
### Oppdatert: 2020-10-22                                                                    ###
### Forfatter:  reloxx13                                                                      ###
################################################################################################



### ANGIs KONFIGURASJON HER ###
# Angi IP-adressen og porten til Sonarr riktig og bruk tjenestenavnene eller planlagte oppgavenavnene dine!

# (string) Typen som brukes for å starte Sonarr
# "Service" (standard) Bruker tjenesteprosessen
# "ScheduledTask" Bruker Oppgaveplanleggeren
$startType = 'Service'

# (bool) Skriver loggen til C:\Users\DINBRUKERNAVN\log.txt når den er aktivert
# $false (standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instans 1
        Name = 'Sonarr-V3'; # (string) Tjeneste- eller oppgavenavn (standard: Sonarr-V3)
        IP   = '192.168.178.12'; # (string) Server-IP der Sonarr kjører (standard: 192.168.178.12)
        Port = '7873'; # (string) Serverport der Sonarr kjører (standard: 7873)
    }
    [pscustomobject]@{   # Instans 2
        Name = 'Sonarr-4K'; # (string) Tjeneste- eller oppgavenavn (standard: Sonarr-4K)
        IP   = '192.168.178.12'; # (string) Server-IP der Sonarr kjører (standard: 192.168.178.12)
        Port = '7874'; # (string) Serverport der Sonarr kjører (standard: 7874)
    }
    # Hvis nødvendig kan du legge til flere instanser her... ved å fjerne kommentartegnene fra linjene nedenfor
    # [pscustomobject]@{   # Instans 3
    # Name='Sonarr-3D';    # (string) Tjeneste- eller oppgavenavn (standard: Sonarr-3D)
    # IP='192.168.178.12'; # (string) Server-IP der Sonarr kjører (standard: 192.168.178.12)
    # Port='7875';         # (string) Serverport der Sonarr kjører (standard: 7875)
    # }
)


### IKKE ENDRE NOE UNDER DENNE LINJEN ###


###
# Denne funksjonen skriver til en loggfil eller til konsollutdata
###
function Write-Log
{
    # Vil skrive til C:\Users\DINBRUKERNAVN\log.txt
    
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
            Write-Log '[FEIL] UKJENT STARTTYPE! BRUK Service eller ScheduledTask !'
        }
    }
    else
    {
        Write-Log "Port $($_.Port) er åpen!"
    }
}

Write-Log 'SLUTT ====================='
```

## Flere instanser på Linux

{#linux-multi}

- [Swizzin-brukere](https://github.com/ComputerByte/sonarr4k)
- Brukere som ikke bruker Swizzin
  - Sørg for at den første instansen har `-data=` argumentet sendt.
  - Stopp midlertidig den første instansen, slik at du kan endre porten til den andre instansen `systemctl stop sonarr`
  - Deaktiver automatisk oppdatering på én av Sonarr-instansene dine

> Nedenfor er et eksempel på et skript for å opprette en Sonarr4K-instans. Det systemd-opprettelsesskriptet nedenfor vil bruke en datamappe på `/var/lib/sonarr4k/`. Sørg for at mappen eksisterer eller endre den etter behov.{.is-danger}

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

- Last inn systemd på nytt:

```shell
sudo systemctl -q daemon-reload
```

- Aktiver Sonarr4k-tjenesten:

```shell
sudo systemctl enable --now -q sonarr4k
```

## Flere instanser med Docker

{#docker-multi}

- Bare start opp en annen Docker-container med et annet navn, og sørg for at de ovennevnte kravene er oppfylt.