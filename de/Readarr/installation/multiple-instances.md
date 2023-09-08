# Mehrere Instanzen

Es ist möglich, mehrere Instanzen von Readarr auszuführen. Dies wird in der Regel gemacht, wenn man eine Hörbuch- und E-Book-Kopie eines Buches haben möchte.
Beachten Sie, dass Sie Readarr so konfigurieren können, dass es eine zweite Readarr-Instanz als Liste verwendet. Dies ist hilfreich, wenn Sie beide synchron halten möchten.

- [Windows-Mehrere Instanzen](#windows-multi)
- [Linux-Mehrere Instanzen](#linux-multi)
- [MacOS-Mehrere Instanzen](#macos-multi)
- [Docker-Mehrere Instanzen](#docker-multi)
{.links-list}

Folgende Anforderungen sollten beachtet werden:

- Wenn nicht mit Docker, sollten dieselben Binärdateien (Programmdateien) verwendet werden
- Wenn nicht mit Docker, müssen alle Instanzen *müssen* mit einem `-data=` oder `/data=` Argument gestartet werden
- Wenn nicht mit Docker, müssen unterschiedliche Ports verwendet werden
  - Wenn mit Docker, müssen unterschiedliche externe Ports verwendet werden
- Unterschiedliche Download-Client-Kategorien müssen verwendet werden
- Unterschiedliche Stammordner müssen verwendet werden.
- Wenn nicht mit Docker, deaktivieren Sie automatische Updates auf allen Instanzen außer einer.

## Windows-Mehrere Instanzen

{#windows-multi}

Diese Anleitung zeigt Ihnen, wie Sie unter Windows mehrere Instanzen von Readarr mit nur einer Basisinstallation ausführen können. Diese Anleitung wurde unter Windows 10 erstellt. Wenn Sie eine frühere Version von Windows (7, 8 usw.) verwenden, müssen Sie möglicherweise einige Dinge anpassen. Diese Anleitung geht auch davon aus, dass Sie Readarr im Standardverzeichnis installiert haben und Ihre zweite Readarr-Instanz Readarr-Hörbücher genannt wird. Passen Sie die Dinge nach Belieben an Ihre eigenen Installationen an.

### Dienst (Windows)

#### Voraussetzungen (Dienst)

- [Sie müssen Readarr bereits installiert haben](#windows)
- Sie müssen [NSSM (Non-Sucking Service Manager)](http://nssm.cc) installiert haben. Laden Sie die neueste Version herunter (2.24 zum Zeitpunkt des Schreibens) und kopieren Sie entweder die 32-Bit- oder die 64-Bit-nssm.exe-Datei in C:/windows/system32.
  - Wenn Sie nicht sicher sind, ob Sie ein 32-Bit- oder 64-Bit-System haben, überprüfen Sie Einstellungen => System => Info => Systemtyp.

#### Konfigurieren des Readarr-Dienstes

1. Öffnen Sie ein Administratorfenster der Eingabeaufforderung. (Um als Administrator auszuführen, klicken Sie mit der rechten Maustaste auf das Eingabeaufforderungssymbol und wählen Sie "Als Administrator ausführen".)
1. Wenn Readarr ausgeführt wird, stoppen Sie den Dienst, indem Sie in der Eingabeaufforderung `nssm stop Readarr` ausführen.
1. Jetzt müssen wir die vorhandene Readarr-Instanz bearbeiten, um explizit auf ihr Datenverzeichnis zu verweisen. Der Standardbefehl lautet wie folgt: `sc config Readarr binpath= "C:\ProgramData\Readarr\bin\Readarr.exe -data=C:\ProgramData\Readarr"`

Dieser Befehl gibt der ursprünglichen Readarr-Instanz explizit an, `C:\ProgramData\Readarr` für ihr Datenverzeichnis zu verwenden. Wenn Sie die Standard-Readarr-Installation nicht verwendet haben oder wenn sich Ihr Datenordner an einem anderen Ort befindet, müssen Sie hier Ihre Pfade ändern.

#### Erstellen des Readarr-Hörbücher-Dienstes

1. Erstellen Sie einen neuen Ordner, in dem Readarr-Hörbücher installiert werden soll. Die meisten verwenden einen ähnlichen Ort wie `C:\ProgramData\Readarr-Hörbücher`.
1. Gehen Sie zurück zur Eingabeaufforderung und erstellen Sie den neuen Readarr-Hörbücher-Dienst mit `nssm install Readarr-Hörbücher`. Es wird ein Popup-Fenster geöffnet, in dem Sie Ihre Parameter für die neue Instanz eingeben können. In diesem Beispiel verwenden wir die folgenden Werte:
      - Pfad: `C:\ProgramData\Readarr\bin\Readarr.exe`
      - Startverzeichnis: `C:\ProgramData\Readarr\bin`
      - Argumente: `-data=C:\ProgramData\Readarr-Hörbücher`

> Beachten Sie, dass **Argumente** auf den *neuen* Ordner verweist, der in Schritt 1 erstellt wurde. Dies ist entscheidend, da alle Daten von beiden Instanzen an separaten Orten gespeichert werden. {.is-warning}

1. Klicken Sie auf *Dienst installieren*. Das Fenster sollte sich schließen und der Dienst ist jetzt verfügbar.
1. Fahren Sie mit [Konfigurieren von Readarr-Hörbüchern](#windows-multi-config-second) fort.

### Tray-App (Windows)

#### Voraussetzungen (Tray-App)

- [Sie müssen Readarr bereits installiert haben](#windows)
- Readarr muss mit einem `/data=`-Argument konfiguriert sein, um mehrere Instanzen zu ermöglichen
- Navigieren Sie zum Startordner für den aktuellen Benutzer `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup` und bearbeiten Sie die vorhandene Verknüpfung bei Bedarf.

#### Erstellen der Readarr-Hörbücher-Tray-App

- Klicken Sie mit der rechten Maustaste und erstellen Sie eine neue Verknüpfung
- Pfad: `C:\ProgramData\Readarr\bin\Readarr.exe /data=C:\ProgramData\Readarr-Hörbücher`
- Geben Sie der Verknüpfung einen eindeutigen Namen wie `Readarr-Hörbücher` und beenden Sie den Assistenten.
- Doppelklicken Sie auf die neue Verknüpfung, um sie auszuführen und zu testen.
- Fahren Sie mit [Konfigurieren von Readarr-Hörbüchern](#windows-multi-config-second) fort.

### Konfigurieren von Readarr-Hörbüchern {#windows-multi-config-second}

- Unabhängig davon, ob Sie die Methode mit dem Dienst oder der Tray-App verwendet haben: Stoppen Sie beide Dienste und beide Apps
- Starten Sie Readarr-Hörbücher (Dienst oder Tray-App)
- Öffnen Sie Readarr-Hörbücher und navigieren Sie in der App zu [Einstellungen => Allgemein => Host](/readarr/settings/#host)
- Ändern Sie die `Portnummer` von `8787` auf einen anderen Port, z.B. `8879`, damit sich Readarr und Readarr-Hörbücher nicht überschneiden
- Sie sollten jetzt beide Apps starten können
- Fahren Sie mit [Umgang mit Updates](#dealing-with-updates) fort

### Umgang mit Updates

- Deaktivieren Sie automatische Updates in einer Ihrer Instanzen
- Wenn eine Readarr-Instanz aktualisiert wird, werden beide Instanzen heruntergefahren und nur die aktualisierte wird wieder gestartet. Um dies zu beheben, müssen Sie die andere Instanz manuell starten oder Sie können das unten stehende PowerShell-Skript verwenden, um das Problem zu beheben.

#### PowerShell-Skript zum Überprüfen und Neustarten des Windows-Ports

{#win-portchecker}

- Wenn Sie zwei Readarr-Instanzen verwenden und eine davon aktualisiert wird, werden alle Instanzen beendet. Nur die aktualisierte Instanz wird wieder online gehen.
- Das folgende PowerShell-Skript sollte als geplante Aufgabe konfiguriert werden.
- Es überprüft die Ports und startet den geplanten Task zum Starten von Readarr neu, wenn einer nicht online ist.

1. Erstellen Sie eine neue Datei und nennen Sie sie ReadarrInstancesChecker.ps1 mit dem folgenden Code.
1. Bearbeiten Sie das Skript mit Ihren tatsächlichen Dienstnamen, IP-Adressen und Ports.
1. [Erstellen Sie eine geplante Aufgabe](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler), um das Skript in einem wiederkehrenden Zeitplan auszuführen.

- Sicherheitsoptionen: Aktivieren Sie `Mit höchsten Privilegien ausführen`
  - Andernfalls kann das Skript die Dienste nicht manipulieren
- Auslöser: `Beim Start`
- Aufgabe alle wiederholen: `5` oder `10` Minuten
- Aktion: `Programm starten`
- Programm/Skript: `powershell`
- Argument: `-File D:\ReadarrInstancesChecker.ps1`
  - Stellen Sie sicher, dass Sie den vollständigen Pfad zum Speicherort Ihres Skripts verwenden

```powershell
################################################################################################
### ReadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Hält mehrere Readarr-Instanzen aufrecht, indem der Port überprüft wird                      ###
### Bitte verwenden Sie Readarr´s Discord oder Reddit für Support!                            ###
### https://wiki.servarr.com/readarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Aktualisiert: 2020-10-22                                                                  ###
### Autor:  reloxx13                                                                          ###
################################################################################################



### SETZEN SIE IHRE KONFIGURATION HIER ###
# Setzen Sie Ihre Host-IP und den Port korrekt und verwenden Sie Ihre Dienst- oder geplanten Tasknamen!

# (string) Der Typ, wie Readarr gestartet wird
# "Service" (Standard) Service-Prozess wird verwendet
# "ScheduledTask" Taskplaner wird verwendet
$startType = 'Service'

# (bool) Schreibt das Protokoll in C:\Users\IHRBENUTZERNAME\log.txt, wenn aktiviert
# $false (Standard)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instanz 1
        Name = 'Readarr'; # (string) Dienst- oder Taskname (Standard: Readarr)
        IP   = '192.168.178.12'; # (string) Server-IP, auf dem Readarr läuft (Standard: 192.168.178.12)
        Port = '8873'; # (string) Server-Port, auf dem Readarr läuft (Standard: 8873)
    }
    [pscustomobject]@{   # Instanz 2
        Name = 'Readarr-Hörbücher'; # (string) Dienst- oder Taskname (Standard: Readarr-Hörbücher)
        IP   = '192.168.178.12'; # (string) Server-IP, auf dem Readarr läuft (Standard: 192.168.178.12)
        Port = '8874'; # (string) Server-Port, auf dem Readarr läuft (Standard: 8874)
    }
    # Wenn nötig, können Sie hier weitere Instanzen hinzufügen, indem Sie die folgenden Zeilen auskommentieren
    # [pscustomobject]@{   # Instanz 3
    # Name='Readarr-3D';    # (string) Dienst- oder Taskname (Standard: Readarr-3D)
    # IP='192.168.178.12'; # (string) Server-IP, auf dem Readarr läuft (Standard: 192.168.178.12)
    # Port='8875';         # (string) Server-Port, auf dem Readarr läuft (Standard: 7875)
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

## Linux-Mehrere Instanzen

{#linux-multi}

- [Swizzin-Benutzer](https://github.com/ComputerByte/readarr-audiobooks)
- Benutzer außerhalb von Swizzin
  - Stellen Sie sicher, dass Ihre erste Instanz das `-data=`-Argument enthält.
  - Stoppen Sie vorübergehend Ihre erste Instanz, damit Sie den Port der zweiten Instanz ändern können `systemctl stop readarr`
  - Deaktivieren Sie automatische Updates in einer Ihrer Readarr-Instanzen

> Unten finden Sie ein Beispiel-Skript zum Erstellen einer Readarr-Hörbücher-Instanz. Das unten stehende systemd-Erstellungsskript verwendet ein Datenverzeichnis von `/var/lib/readarr-audiobooks/`. Stellen Sie sicher, dass das Verzeichnis vorhanden ist oder passen Sie es bei Bedarf an. {.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr-audiobooks.service > /dev/null
[Unit]
Description=Readarr-audiobooks-Daemon
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

- Systemd neu laden:

```shell
sudo systemctl -q daemon-reload
```

- Aktivieren Sie den Readarr-audiobooks-Dienst:

```shell
sudo systemctl enable --now -q readarr-audiobooks
```

## MacOS-Mehrere Instanzen

{#macos-multi}

Diese Anleitung wurde mit macOS 13 (Ventura) erstellt und getestet, sollte jedoch auf jeder Version funktionieren, die von Readarr unterstützt wird.

### Voraussetzungen
- Die Readarr-Anwendung muss im Ordner `/Applications` installiert sein
- Wenn Readarr bereits verwendet wurde, gehen alle Daten verloren. Verschieben Sie `~/.config/Readarr` nach `~/.config/readarr-books` oder `~/.config/readarr-audiobooks`, um die Daten zu behalten.

### Erstellen von Anwendungen (einfaches Starten von Readarr)
Sie erstellen zwei neue Anwendungen: "Readarr Books" und "Readarr Audiobooks".

- Öffnen Sie die Automator-App
- Wählen Sie `Neues Dokument` und dann `Anwendung`
- Verwenden Sie das Suchfeld oben links, um nach `Shell-Skript ausführen` zu suchen, und doppelklicken Sie darauf
- Fügen Sie im geöffneten Feld folgendes ein:

```shell
# Readarr Books
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-books
```



- Speichern Sie die Anwendung als `Readarr Bücher`.
- Gehen Sie in der Menüleiste zu `Datei` > `Duplizieren`.
- Ersetzen Sie den Inhalt des Skripts durch Folgendes:

```shell
# Readarr Hörbücher
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-hoerbuecher
```

- Speichern Sie die neue Anwendung als `Readarr Hörbücher`.
- Öffnen Sie den Finder und sehen Sie sich die Anwendungen an. Sie können optional ihre Symbole nach Belieben ändern (über das `Informationen`-Fenster).

### Konfigurieren von Instanzen
Jetzt legen Sie die Ports und Namen für jede Instanz fest.

- Wählen Sie für jede Instanz eine Portnummer aus. Zum Beispiel die Standardportnummer `8787` für E-Books und `8789` für Hörbücher.
- Wenn eine der Instanzen die Standardportnummer verwendet, starten Sie zuerst die andere. Andernfalls starten Sie eine beliebige Instanz.
- Gehen Sie in Readarr zu `Einstellungen` > `Allgemein` und stellen Sie den richtigen Port ein.

> Optional: Aktivieren Sie erweiterte Optionen und legen Sie den `Instanznamen` nach Belieben fest.
{.is-success}

- Starten Sie die andere Instanz und machen Sie dasselbe.

### Aktualisierungen
Wenn Sie eine Instanz aktualisieren, werden beide heruntergefahren und nur die aktualisierte Instanz wird neu gestartet. Um dies zu umgehen, wird eine periodische Aufgabe zum Überprüfen der Ports erstellt (angepasst, aber leicht verändert aus dem [Windows-Leitfaden](#win-portchecker)).

- Deaktivieren Sie die automatischen Updates in einer der Instanzen und stellen Sie sicher, dass Sie sie niemals aktualisieren.
- Erstellen Sie eine neue Datei an einem Ort, an den Sie sich erinnern können, und nennen Sie sie `readarrportchecker.zsh`.
- Fügen Sie den folgenden Inhalt hinzu:

```shell
#!/bin/zsh

# Name der ersten Instanz
name0="Readarr Bücher"
# Portnummer der ersten Instanz
port0=8787

# Name der zweiten Instanz
name1="Readarr Hörbücher"
# Portnummer der zweiten Instanz
port1=8789

# Protokollierung
LOGFILE="$HOME/.local/state/readarr.log"
test -d "$HOME/.local/state" || mkdir -p "$HOME/.local/state"

function checkport {
    lsof -i ":${1}" &>/dev/null
}

# Wenn eine Instanz läuft, sollten beide laufen
if checkport "${port0}" && ! checkport "${port1}"; then
		open -a "${name1}"
    echo "Öffnete ${name1}" >> "$LOGFILE"
elif checkport "${port1}" && ! checkport "${port0}"; then
		open -a "${name0}"
    echo "Öffnete ${name0}" >> "$LOGFILE"
fi
```

- Machen Sie das Skript ausführbar:

```shell
chmod +x readarrportchecker.zsh
```

- Planen Sie das Skript, um es regelmäßig auszuführen. Erstellen Sie eine neue Datei in `~/Library/LaunchAgents` mit dem Namen `local.readarr.portchecker.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>local.readarr.portchecker</string>
    <key>Program</key>
    <!-- Finden Sie den Pfad, indem Sie mit der rechten Maustaste klicken, dann Option und kopieren -->
    <string>/Pfad/zur/readarrportchecker.zsh</string>
    <key>StartInterval</key>
    <!-- Periodisches Intervall in Sekunden. 300 für fünf Minuten,
         600 für zehn Minuten. -->
    <integer>300</integer>
  </dict>
</plist>
```

- Passen Sie die Datei entsprechend den Kommentaren an.
- Melden Sie sich entweder erneut an oder laden Sie die Datei manuell:

```shell
launchctl load ~/Library/LaunchAgents/local.readarr.portchecker.plist
```

> `TODO`: Möglicherweise in einen benutzerdefinierten Skript für den Aktualisierungsprozess integrieren oder Änderungen an der Datei überwachen, anstatt alle 300 Sekunden auszuführen.
{.is-info}

## Docker Mehrere Instanzen

{#docker-multi}

- Starten Sie einfach einen zweiten Docker-Container mit einem anderen Namen und stellen Sie sicher, dass die oben genannten Anforderungen erfüllt sind.