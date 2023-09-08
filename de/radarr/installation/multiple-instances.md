---
title: Mehrere Instanzen
description: 
published: true
date: 2023-09-01T05:05:47.102Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:10.189Z
---

# Mehrere Instanzen

Es ist möglich, mehrere Instanzen von Radarr auszuführen. Dies wird in der Regel gemacht, wenn man eine 4K- und eine 1080p-Kopie eines Films haben möchte. Beachten Sie, dass Sie (und wahrscheinlich sollten Sie) [TRaSH's Anleitung überprüfen und Radarr so konfigurieren, dass es eine zweite Radarr-Instanz als Liste verwendet](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/). Dies ist hilfreich, wenn Sie beide synchron halten möchten.

- [Windows-Mehrere-Instanzen](#windows-multi)
- [Linux-Mehrere-Instanzen](#linux-multi)
- [Docker-Mehrere-Instanzen](#docker-multi)
{.links-list}

Die folgenden Anforderungen sollten beachtet werden:

- Wenn nicht in Docker, sollten dieselben Binärdateien (Programmdateien) verwendet werden
- Wenn nicht in Docker, müssen alle Instanzen *unbedingt* mit einem `-data=` oder `/data=`-Argument übergeben werden
- Wenn nicht in Docker, müssen unterschiedliche Ports verwendet werden
  - Wenn in Docker, müssen unterschiedliche externe Ports verwendet werden
- Unterschiedliche Kategorien für Download-Clients müssen verwendet werden
- Unterschiedliche Stammordner müssen verwendet werden.
- Wenn nicht in Docker, deaktivieren Sie automatische Updates in allen Instanzen außer einer.

## Windows-Mehrere-Instanzen

{#windows-multi}

Diese Anleitung zeigt Ihnen, wie Sie unter Windows mehrere Instanzen von Radarr mit nur einer Basiseinrichtung ausführen können. Diese Anleitung wurde unter Windows 10 erstellt. Wenn Sie eine frühere Version von Windows (7, 8 usw.) verwenden, müssen Sie möglicherweise einige Dinge anpassen. Diese Anleitung geht auch davon aus, dass Sie Radarr im Standardverzeichnis installiert haben und Ihre zweite Radarr-Instanz Radarr-4K genannt wird. Sie können die Dinge gerne ändern, um sie an Ihre eigenen Installationen anzupassen.

> Hinweis: Sie sollten Radarr entweder als **Dienst** [ausführen](#service-windows) oder als [Tray-App](#tray-app-windows). Das Ausführen einer App und eines Dienstes ist unnötig und kann zu Problemen führen.

### Dienst (Windows)

#### Voraussetzungen (Dienst)

- [Sie müssen Radarr bereits installiert haben](#windows)
- Sie müssen [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installiert haben. Laden Sie die neueste Version herunter (2.24 zum Zeitpunkt des Schreibens) und kopieren Sie entweder die 32-Bit- oder die 64-Bit-nssm.exe-Datei in C:/windows/system32.
  - Wenn Sie nicht sicher sind, ob Sie ein 32-Bit- oder 64-Bit-System haben, überprüfen Sie Einstellungen => System => Info => Systemtyp.

#### Konfigurieren des Radarr-Dienstes

1. Öffnen Sie ein Administratorfenster der Eingabeaufforderung. (Um als Administrator auszuführen, klicken Sie mit der rechten Maustaste auf das Eingabeaufforderungssymbol und wählen Sie "Als Administrator ausführen".)
1. Wenn Radarr ausgeführt wird, stoppen Sie den Dienst, indem Sie in der Eingabeaufforderung `nssm stop Radarr` ausführen.
1. Jetzt müssen wir die vorhandene Radarr-Instanz bearbeiten, um explizit auf ihr Datenverzeichnis zu verweisen. Der Standardbefehl lautet wie folgt: `sc config Radarr binpath= "C:\ProgramData\Radarr\bin\Radarr.exe -data=C:\ProgramData\Radarr"`

Dieser Befehl teilt der ursprünglichen Radarr-Instanz explizit mit, dass sie für ihr Datenverzeichnis `C:\ProgramData\Radarr` verwenden soll. Wenn Sie die Standard-Radarr-Installation nicht verwendet haben oder wenn sich Ihr Datenordner an einem anderen Ort befindet, müssen Sie hier Ihre Pfade ändern.

#### Erstellen des Radarr-4K-Dienstes

1. Erstellen Sie einen neuen Ordner, in dem Radarr-4K installiert werden soll. Die meisten verwenden einen ähnlichen Ort wie `C:\ProgramData\Radarr-4K`.
1. Gehen Sie zurück zur Eingabeaufforderung und erstellen Sie den neuen Radarr-4K-Dienst mit `nssm install Radarr-4K`. Es wird ein Popup-Fenster geöffnet, in dem Sie Ihre Parameter für die neue Instanz eingeben können. In diesem Beispiel verwenden wir Folgendes:
      - Pfad: `C:\ProgramData\Radarr\bin\Radarr.exe`
      - Startverzeichnis: `C:\ProgramData\Radarr\bin`
      - Argumente: `-data=C:\ProgramData\Radarr-4K`
      - Registerkarte "Exit Actions"
        - Neustart: Anwendung neu starten
        - Verzögerung: 120000 ms
        (2 Minuten, kann länger sein, wenn das Update nicht rechtzeitig abgeschlossen wird)

> Beachten Sie, dass **Argumente** auf den *neuen* Ordner verweist, der in Schritt 1 erstellt wurde. Dies ist entscheidend, da so alle Datendateien beider Instanzen an separaten Orten aufbewahrt werden. {.is-warning}

1. Klicken Sie auf *Dienst installieren*. Das Fenster sollte sich schließen und der Dienst steht nun zur Verfügung.
1. Fahren Sie mit [Konfigurieren von Radarr-4K](#windows-multi-config-second) fort.

### Tray-App (Windows)

#### Voraussetzungen (Tray-App)

- [Sie müssen Radarr bereits installiert haben](#windows)
- Die Verknüpfung von Radarr muss mit einem `/data=`-Argument im Feld "Ziel" konfiguriert sein, um mehrere Instanzen zu ermöglichen
- Navigieren Sie zum Startordner für den aktuellen Benutzer `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` und bearbeiten Sie die vorhandene Verknüpfung bei Bedarf.

#### Erstellen der Radarr-4K-Tray-App

- Erstellen Sie einen neuen Ordner für die Konfigurationsdateien von Radarr-4K. Die meisten verwenden einen ähnlichen Ort wie `C:\ProgramData\Radarr-4K`.
- Klicken Sie mit der rechten Maustaste und erstellen Sie eine neue Verknüpfung
- Pfad: `C:\ProgramData\Radarr\bin\Radarr.exe /data=C:\ProgramData\Radarr-4K`
- Geben Sie der Verknüpfung einen eindeutigen Namen wie `Radarr-4K` und beenden Sie den Assistenten.
- Doppelklicken Sie auf die neue Verknüpfung, um sie auszuführen und zu testen.
- Fahren Sie mit [Konfigurieren von Radarr-4K](#windows-multi-config-second) fort.

### Konfigurieren von Radarr-4K {#windows-multi-config-second}

- Unabhängig davon, ob Sie die Methode "Dienst" oder die Tray-App verwendet haben: Stoppen Sie sowohl den Dienst als auch die App.
- Starten Sie Radarr-4K (Dienst oder Tray-App)
- Öffnen Sie Radarr-4K und navigieren Sie in der App zu [Einstellungen => Allgemein => Host](/radarr/settings/#host)
- Ändern Sie die `Portnummer` von `7878` auf einen anderen Port, z.B. `7879`, damit sich Radarr und Radarr4K nicht gegenseitig beeinflussen
- Sie sollten jetzt beide Apps starten können
- Fahren Sie mit [Umgang mit Updates](#dealing-with-updates) fort

### Umgang mit Updates

> - Deaktivieren Sie automatische Updates in einer Ihrer Instanzen
  - Ändern Sie in der Datei config.xml den Update-Zweig in `<Branch>nonexistent</Branch>`
- Wenn eine Radarr-Instanz aktualisiert wird, werden beide Instanzen heruntergefahren und nur die aktualisierte Instanz wird wieder gestartet. Um dies zu beheben, müssen Sie die andere Instanz manuell starten oder Sie können das unten stehende PowerShell-Skript verwenden, um das Problem zu beheben.

> Wenn die [NSSM Exit Action](#creating-radarr-4k-service) richtig konfiguriert ist, kann Radarr mehrere Instanzen aktualisieren und neu starten, ohne dass zusätzliche Skripte erforderlich sind.
Wenn die Neustartverzögerung nicht standardmäßig konfiguriert ist, wird die Instanz sofort neu gestartet.
Dies kann dazu führen, dass Updates nicht angewendet werden und zu folgendem Fehler führen: `Radarr wurde vorzeitig von einem externen Prozess neu gestartet.`
{.is-info}

#### PowerShell-Skript zum Überprüfen und Neustarten von Windows-Ports

- Wenn Sie zwei Radarr-Instanzen verwenden und eine davon aktualisiert wird, werden alle Instanzen beendet. Nur die aktualisierte Instanz wird wieder online gehen.
- Das folgende PowerShell-Skript sollte als geplante Aufgabe konfiguriert werden.
- Es überprüft die Ports und startet die geplante Aufgabe neu, um Radarr zu starten, wenn einer der Ports nicht online ist.

1. Erstellen Sie eine neue Datei und nennen Sie sie RadarrInstancesChecker.ps1 mit dem folgenden Code.
1. Bearbeiten Sie das Skript mit Ihren tatsächlichen Dienstnamen, IP-Adressen und Ports. *Wenn Sie den Tray-Modus verwenden, müssen Sie geplante Aufgaben erstellen, um jede Radarr-Instanz zu starten, und die Namen dieser Aufgaben im folgenden Skript verwenden.*
1. [Erstellen Sie eine geplante Aufgabe](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler), um das Skript in einem wiederkehrenden Zeitplan auszuführen.

- Sicherheitsoptionen: Aktivieren Sie `Mit höchsten Privilegien ausführen`
  - Andernfalls kann das Skript die Dienste nicht manipulieren
- Auslöser: `Beim Start`
- Aufgabe alle wiederholen: `5` oder `10` Minuten
- Aktion: `Programm starten`
- Programm/Skript: `powershell`
- Argument: `-File D:\RadarrInstancesChecker.ps1`
  - Stellen Sie sicher, dass der vollständige Pfad zum Speicherort Ihres Skripts verwendet wird

```powershell
################################################################################################
### RadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Hält mehrere Radarr-Instanzen aufrecht, indem der Port überprüft wird                      ###
### Bitte verwenden Sie Radarrs Discord oder Reddit für Support!                              ###
### https://wiki.servarr.com/radarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Aktualisiert: 2020-10-22                                                                  ###
### Autor:  reloxx13                                                                          ###
################################################################################################



### SETZEN SIE IHRE KONFIGURATION HIER ###
# Legen Sie Ihren Host-IP und Port korrekt fest und verwenden Sie Ihre Dienst- oder geplanten Aufgabennamen!

# (string) Der Typ, wie Radarr gestartet wird
# "Service" (Standard) Service-Prozess wird verwendet
# "ScheduledTask" Taskplaner wird verwendet
$startType = 'Service'

# (bool) Schreibt das Protokoll in C:\Users\IHRBENUTZERNAME\log.txt, wenn aktiviert
# $false (Standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instanz 1
        Name = 'Radarr-V3'; # (string) Dienst- oder Aufgabenname (Standard: Radarr-V3)
        IP   = '192.168.178.12'; # (string) Server-IP, auf dem Radarr läuft (Standard: 192.168.178.12)
        Port = '7873'; # (string) Server-Port, auf dem Radarr läuft (Standard: 7873)
    }
    [pscustomobject]@{   # Instanz 2
        Name = 'Radarr-4K'; # (string) Dienst- oder Aufgabenname (Standard: Radarr-4K)
        IP   = '192.168.178.12'; # (string) Server-IP, auf dem Radarr läuft (Standard: 192.168.178.12)
        Port = '7874'; # (string) Server-Port, auf dem Radarr läuft (Standard: 7874)
    }
    # Wenn nötig, können Sie hier weitere Instanzen hinzufügen, indem Sie die folgenden Zeilen auskommentieren
    # [pscustomobject]@{   # Instanz 3
    # Name='Radarr-3D';    # (string) Dienst- oder Aufgabenname (Standard: Radarr-3D)
    # IP='192.168.178.12'; # (string) Server-IP, auf dem Radarr läuft (Standard: 192.168.178.12)
    # Port='7875';         # (string) Server-Port, auf dem Radarr läuft (Standard: 7875)
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
            Write-Log '[FEHLER] STARTTYPE UNKNOWN! VERWENDEN SIE Service oder ScheduledTask!'
        }
    }
    else
    {
        Write-Log "Port $($_.Port) ist geöffnet!"
    }
}

Write-Log 'END ====================='
```

## Linux-Mehrere-Instanzen

{#linux-multi}

- [Swizzin-Benutzer](https://github.com/ComputerByte/radarr4k)
- Benutzer außerhalb von Swizzin
  - Stellen Sie sicher, dass Ihre erste Instanz das `-data=`-Argument übergeben hat.
  - Stoppen Sie vorübergehend Ihre erste Instanz, damit Sie den Port der zweiten Instanz ändern können `systemctl stop radarr`
  - Deaktivieren Sie automatische Updates in einer Ihrer Radarr-Instanzen

> Unten finden Sie ein Beispiel-Skript zum Erstellen einer Radarr4K-Instanz. Das unten stehende systemd-Erstellungsskript verwendet ein Datenverzeichnis von `/var/lib/radarr4k/`. Stellen Sie sicher, dass das Verzeichnis vorhanden ist oder passen Sie es bei Bedarf an.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/radarr4k.service > /dev/null
[Unit]
Description=Radarr4k-Daemon
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

- Systemd neu laden:

```shell
sudo systemctl -q daemon-reload
```

- Aktivieren Sie den Radarr4k-Dienst:

```shell
sudo systemctl enable --now -q radarr4k
```

## Docker Mehrere Instanzen

{#docker-multi}

- Starten Sie einfach einen zweiten Docker-Container mit einem anderen Namen und stellen Sie sicher, dass die oben genannten Anforderungen erfüllt sind.