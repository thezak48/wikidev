---
title: Mehrere Instanzen
description: 
published: true
date: 2023-08-20T02:23:13.676Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:35.847Z
---

# Mehrere Instanzen

Es ist möglich, mehrere Instanzen von Sonarr auszuführen. Dies wird in der Regel gemacht, wenn man eine 4K- und eine 1080p-Kopie einer Serie haben möchte.
[Beachten Sie, dass Sie Sonarr so konfigurieren können, dass es eine zweite Sonarr-Instanz als Liste verwendet. Dies ist hilfreich, wenn Sie beide synchron halten möchten.](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)

- [Mehrere Instanzen unter Windows](#windows-multi)
- [Mehrere Instanzen unter Linux](#linux-multi)
- [Mehrere Instanzen mit Docker](#docker-multi)
{.links-list}

Folgende Anforderungen sollten beachtet werden:

- Bei Nicht-Docker müssen dieselben Binärdateien (Programmdateien) verwendet werden.
- Bei Nicht-Docker müssen alle Instanzen *müssen* mit einem `-data=` oder `/data=` Argument gestartet werden.
- Bei Nicht-Docker müssen unterschiedliche Ports verwendet werden.
  - Bei Docker müssen unterschiedliche externe Ports verwendet werden.
- Unterschiedliche Kategorien für Download-Clients müssen verwendet werden.
- Unterschiedliche Stammverzeichnisse müssen verwendet werden.
- Bei Nicht-Docker sollten automatische Updates auf allen, außer einer Instanz deaktiviert werden.

## Mehrere Instanzen unter Windows

{#windows-multi}

Diese Anleitung zeigt Ihnen, wie Sie unter Windows mehrere Instanzen von Sonarr mit nur einer Basisinstallation ausführen können. Diese Anleitung wurde unter Windows 10 erstellt. Wenn Sie eine frühere Version von Windows (7, 8 usw.) verwenden, müssen Sie möglicherweise einige Anpassungen vornehmen. Diese Anleitung geht auch davon aus, dass Sie Sonarr im Standardverzeichnis installiert haben und Ihre zweite Sonarr-Instanz Sonarr-4K genannt wird. Sie können die Anpassungen jedoch nach Ihren eigenen Installationen vornehmen.

### Dienst (Windows)

#### Voraussetzungen (Dienst)

- [Sie müssen Sonarr bereits installiert haben](#windows)
- Sie müssen [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installiert haben. Um es zu installieren, laden Sie die neueste Version (2.24 zum Zeitpunkt des Schreibens) herunter und kopieren Sie entweder die 32-Bit- oder die 64-Bit-nssm.exe-Datei in C:/windows/system32.
  - Wenn Sie nicht sicher sind, ob Sie ein 32-Bit- oder 64-Bit-System haben, überprüfen Sie Einstellungen => System => Info => Systemtyp.

#### Konfiguration des Sonarr-Dienstes

1. Öffnen Sie ein Administratorfenster der Eingabeaufforderung. (Um als Administrator auszuführen, klicken Sie mit der rechten Maustaste auf das Eingabeaufforderungssymbol und wählen Sie "Als Administrator ausführen".)
1. Wenn Sonarr ausgeführt wird, stoppen Sie den Dienst, indem Sie `nssm stop Sonarr` in der Eingabeaufforderung ausführen.
1. Jetzt müssen wir die vorhandene Sonarr-Instanz bearbeiten, um explizit auf ihr Datenverzeichnis zu verweisen. Der Standardbefehl lautet wie folgt: `sc config Sonarr binpath= "C:\ProgramData\Sonarr\bin\Sonarr.exe -data=C:\ProgramData\Sonarr"`

Dieser Befehl gibt der Originalinstanz von Sonarr explizit an, `C:\ProgramData\Sonarr` für ihr Datenverzeichnis zu verwenden. Wenn Sie die Standard-Sonarr-Installation nicht verwendet haben oder wenn sich Ihr Datenordner an einem anderen Ort befindet, müssen Sie hier Ihre Pfade ändern.

#### Erstellen des Sonarr-4K-Dienstes

1. Erstellen Sie einen neuen Ordner, in dem Sonarr-4K installiert werden soll. Die meisten verwenden einen ähnlichen Ort wie `C:\ProgramData\Sonarr-4K`.
1. Kehren Sie zur Eingabeaufforderung zurück und erstellen Sie den neuen Sonarr-4K-Dienst mit `nssm install Sonarr-4K`. Ein Popup-Fenster wird geöffnet, in dem Sie Ihre Parameter für die neue Instanz eingeben können. In diesem Beispiel verwenden wir folgende Einstellungen:
      - Pfad: `C:\ProgramData\Sonarr\bin\Sonarr.exe`
      - Startverzeichnis: `C:\ProgramData\Sonarr\bin`
      - Argumente: `-data=C:\ProgramData\Sonarr-4K`

> Beachten Sie, dass **Argumente** auf den *neuen* Ordner verweisen, der in Schritt 1 erstellt wurde. Dies ist entscheidend, da alle Daten von beiden Instanzen an separaten Orten gespeichert werden. {.is-warning}

1. Klicken Sie auf *Dienst installieren*. Das Fenster sollte sich schließen und der Dienst ist jetzt verfügbar.
1. Fahren Sie mit [Konfigurieren von Sonarr-4K](#windows-multi-config-second) fort.

### Tray-App (Windows)

#### Voraussetzungen (Tray-App)

- [Sie müssen Sonarr bereits installiert haben](#windows)
- Sonarr muss mit einem `/data=` Argument konfiguriert sein, um mehrere Instanzen zu ermöglichen.
- Navigieren Sie zum Startordner für den aktuellen Benutzer `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` und bearbeiten Sie die vorhandene Verknüpfung bei Bedarf.

#### Erstellen der Sonarr-4K-Tray-App

- Klicken Sie mit der rechten Maustaste und erstellen Sie eine neue Verknüpfung.
- Pfad: `C:\ProgramData\Sonarr\bin\Sonarr.exe /data=C:\ProgramData\Sonarr-4K`
- Geben Sie der Verknüpfung einen eindeutigen Namen wie `Sonarr-4K` und beenden Sie den Assistenten.
- Doppelklicken Sie auf die neue Verknüpfung, um sie auszuführen und zu testen.
- Fahren Sie mit [Konfigurieren von Sonarr-4K](#windows-multi-config-second) fort.

### Konfigurieren von Sonarr-4K {#windows-multi-config-second}

- Unabhängig davon, ob Sie die Methode mit dem Dienst oder der Tray-App verwendet haben: Stoppen Sie sowohl den Dienst als auch die App.
- Starten Sie Sonarr-4K (Dienst oder Tray-App).
- Öffnen Sie Sonarr-4K und navigieren Sie in der App zu [Einstellungen => Allgemein => Host](/sonarr/settings/#host)
- Ändern Sie die `Portnummer` von `8989` auf einen anderen Port, z.B. `7879`, damit sich Sonarr und Sonarr-4K nicht gegenseitig beeinflussen.
- Sie sollten jetzt beide Apps starten können.
- Fahren Sie mit [Umgang mit Updates](#dealing-with-updates) fort.

### Umgang mit Updates

- Deaktivieren Sie automatische Updates in einer Ihrer Instanzen.
- Wenn eine Sonarr-Instanz aktualisiert wird, werden beide Instanzen heruntergefahren und nur die aktualisierte wird wieder gestartet. Um dies zu beheben, müssen Sie die andere Instanz manuell starten oder Sie können das unten stehende PowerShell-Skript verwenden, um das Problem zu beheben.

#### PowerShell-Skript zum Überprüfen und Neustarten des Ports unter Windows

- Wenn Sie zwei Sonarr-Instanzen verwenden und eine davon aktualisiert wird, werden alle Instanzen beendet. Nur die aktualisierte Instanz wird wieder online kommen.
- Das folgende PowerShell-Skript sollte als geplante Aufgabe konfiguriert werden.
- Es überprüft die Ports und startet den geplanten Task zum Starten von Sonarr neu, wenn einer nicht online ist.

1. Erstellen Sie eine neue Datei mit dem Namen SonarrInstancesChecker.ps1 und dem folgenden Code.
1. Bearbeiten Sie das Skript mit Ihren tatsächlichen Dienstnamen, IP-Adressen und Ports.
1. [Erstellen Sie eine geplante Aufgabe](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler), um das Skript in einem wiederkehrenden Zeitplan auszuführen.

- Sicherheitsoptionen: Aktivieren Sie `Mit höchsten Privilegien ausführen`
  - Andernfalls kann das Skript keine Dienste manipulieren.
- Auslöser: `Beim Start`
- Aufgabe alle wiederholen: `5` oder `10` Minuten
- Aktion: `Programm starten`
- Programm/Skript: `powershell`
- Argument: `-File D:\SonarrInstancesChecker.ps1`
  - Stellen Sie sicher, dass Sie den vollständigen Pfad zum Speicherort Ihres Skripts verwenden

```powershell
################################################################################################
### SonarrInstancesChecker.ps1                                                               ###
################################################################################################
### Hält mehrere Sonarr-Instanzen aktiv, indem der Port überprüft wird                         ###
### Bitte verwenden Sie das Sonarr-Discord oder Reddit für Support!                           ###
### https://wiki.servarr.com/sonarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Aktualisiert: 2020-10-22                                                                  ###
### Autor:  reloxx13                                                                          ###
################################################################################################



### KONFIGURATION HIER EINSTELLEN ###
# Legen Sie Ihren Host-IP und Port korrekt fest und verwenden Sie Ihre Dienst- oder geplanten Tasknamen!

# (string) Der Typ, wie Sonarr gestartet wird
# "Service" (Standard) Service-Prozess wird verwendet
# "ScheduledTask" Taskplaner wird verwendet
$startType = 'Service'

# (bool) Schreibt das Protokoll in C:\Users\IHRBENUTZERNAME\log.txt, wenn aktiviert
# $false (Standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instanz 1
        Name = 'Sonarr-V3'; # (string) Dienst- oder Taskname (Standard: Sonarr-V3)
        IP   = '192.168.178.12'; # (string) Server-IP, auf dem Sonarr läuft (Standard: 192.168.178.12)
        Port = '7873'; # (string) Server-Port, auf dem Sonarr läuft (Standard: 7873)
    }
    [pscustomobject]@{   # Instanz 2
        Name = 'Sonarr-4K'; # (string) Dienst- oder Taskname (Standard: Sonarr-4K)
        IP   = '192.168.178.12'; # (string) Server-IP, auf dem Sonarr läuft (Standard: 192.168.178.12)
        Port = '7874'; # (string) Server-Port, auf dem Sonarr läuft (Standard: 7874)
    }
    # Wenn nötig, können Sie hier weitere Instanzen hinzufügen, indem Sie die folgenden Zeilen auskommentieren
    # [pscustomobject]@{   # Instanz 3
    # Name='Sonarr-3D';    # (string) Dienst- oder Taskname (Standard: Sonarr-3D)
    # IP='192.168.178.12'; # (string) Server-IP, auf dem Sonarr läuft (Standard: 192.168.178.12)
    # Port='7875';         # (string) Server-Port, auf dem Sonarr läuft (Standard: 7875)
    # }
)


### ÄNDERN SIE NICHTS UNTERHALB DIESER LINIE ###


###
# Diese Funktion schreibt in eine Protokolldatei oder in die Konsolenausgabe
###
function Write-Log
{
    # Schreibt in C:\Users\IHRBENUTZERNAME\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    # Konsolenausgabe
    Write-Output "[$(TS)]$Message"
    
    # Dateiausgabe
    if ($logToFile)
    {
        "[$(TS)]$Message" | Tee-Object -FilePath $Path -Append | Write-Verbose
    }
}


Write-Log 'START ====================='


$instances | ForEach-Object {
    Write-Log "Überprüfe $($_.Name) $($_.IP):$($_.Port)"
    
    $PortOpen = ( Test-NetConnection $_.IP -Port $_.Port -WarningAction SilentlyContinue ).TcpTestSucceeded 
    
    if (!$PortOpen)
    {
        Write-Log "Port $($_.Port) ist geschlossen, starte $($startType) $($_.Name) neu!"

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
            Write-Log '[FEHLER] STARTTYPE UNBEKANNT! VERWENDEN SIE Service oder ScheduledTask!'
        }
    }
    else
    {
        Write-Log "Port $($_.Port) ist geöffnet!"
    }
}

Write-Log 'END ====================='
```

## Mehrere Instanzen unter Linux

{#linux-multi}

- [Swizzin-Benutzer](https://github.com/ComputerByte/sonarr4k)
- Benutzer ohne Swizzin
  - Stellen Sie sicher, dass Ihre erste Instanz das `-data=` Argument enthält.
  - Stoppen Sie vorübergehend Ihre erste Instanz, damit Sie den Port der zweiten Instanz ändern können: `systemctl stop sonarr`
  - Deaktivieren Sie automatische Updates in einer Ihrer Sonarr-Instanzen.

> Unten finden Sie ein Beispiel-Skript zum Erstellen einer Sonarr4K-Instanz. Das unten stehende systemd-Erstellungsskript verwendet ein Datenverzeichnis von `/var/lib/sonarr4k/`. Stellen Sie sicher, dass das Verzeichnis vorhanden ist oder passen Sie es bei Bedarf an. {.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/sonarr4k.service > /dev/null
[Unit]
Description=Sonarr4k-Daemon
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

- Systemd neu laden:

```shell
sudo systemctl -q daemon-reload
```

- Aktivieren Sie den Sonarr4k-Dienst:

```shell
sudo systemctl enable --now -q sonarr4k
```

## Mehrere Instanzen mit Docker

{#docker-multi}

- Starten Sie einfach einen zweiten Docker-Container mit einem anderen Namen und stellen Sie sicher, dass die oben genannten Anforderungen erfüllt sind.