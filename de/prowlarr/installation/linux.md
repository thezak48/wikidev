---
title: Prowlarr Linux Installation
description: Linux-Installationsanleitung für Prowlarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Hinweis: Raspberry Pi OS und Raspbian sind beide Varianten von Debian {.is-info}

### Einfache Installation

Für Anfänger in Debian / Ubuntu / Raspbian gibt es kein Apt-Repository oder Deb-Paket.

Wenn Sie es einfach haben möchten, folgen Sie diesem von der Community bereitgestellten und gepflegten `Easy Install`-Skript für eine Basisinstallation von Debian (Raspbian / Raspberry Pi OS) / Ubuntu.

**Für die offiziellen Installationsanweisungen, die "Hands-on" sind, folgen Sie den weiter unten aufgeführten [Debian / Ubuntu Hands-on Install](#debian-ubuntu-hands-on-install)-Schritten.**

[Bitte sehen Sie sich das \*Arr Community Installations-Skript an](/install-script)

### Debian / Ubuntu Hands-on Install

Sie müssen die Binärdateien mit den folgenden Befehlen installieren.

> Die folgenden Schritte laden Prowlarr herunter und installieren es in `/opt`
> Prowlarr wird unter dem Benutzer `prowlarr` und der Gruppe `prowlarr` ausgeführt
> Die Konfigurationsdateien von Prowlarr werden in `/var/lib/prowlarr` gespeichert {.is-warning}

- Stellen Sie sicher, dass Sie die erforderlichen Voraussetzungspakete installiert haben:

```shell
sudo apt install curl sqlite3
```

> Warnung: Wenn Sie die unten aufgeführten Voraussetzungen ignorieren, schlägt die Installation fehl und die Anwendung funktioniert nicht. {.is-warning}

> **Installationsvoraussetzungen**
> Die folgenden Anweisungen basieren auf den folgenden Voraussetzungen. Passen Sie die Anweisungen bei Bedarf an Ihre spezifischen Anforderungen an.
> \* Der Benutzer `prowlarr` ist erstellt
> \* Sie haben das Verzeichnis `/var/lib/prowlarr` erstellt und sichergestellt, dass der Benutzer `prowlarr` Lese-/Schreibrechte dafür hat {.is-danger}

> Durch die Fortsetzung unten bestätigen Sie, dass Sie die oben genannten Anforderungen gelesen und erfüllt haben. {.is-warning}

- Laden Sie die richtigen Binärdateien für Ihre Architektur herunter.
  - Sie können Ihre Architektur mit `dpkg --print-architecture` ermitteln
    - AMD64 verwenden `arch=x64`
    - ARM, armf und armh verwenden `arch=arm`
    - ARM64 verwenden `arch=arm64`

```shell
wget --content-disposition 'http://prowlarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Entpacken Sie die Dateien:

```shell
tar -xvzf Prowlarr*.linux*.tar.gz
```

- Verschieben Sie die Dateien nach `/opt/`

```shell
sudo mv Prowlarr/ /opt
```

> Dies setzt voraus, dass Sie den Benutzer erstellt haben und als Benutzer `prowlarr` und Gruppe `prowlarr` ausgeführt werden. Sie können dies an Ihre Anforderungen anpassen. {.is-danger}

- Stellen Sie den Besitz des Binärverzeichnisses sicher.

```shell  
sudo chown prowlarr:prowlarr -R /opt/Prowlarr
```

- Konfigurieren Sie systemd, damit Prowlarr beim Start automatisch gestartet wird.

> Das unten stehende systemd-Erstellungsskript verwendet ein Datenverzeichnis von `/var/lib/prowlarr`. Stellen Sie sicher, dass es vorhanden ist oder passen Sie es bei Bedarf an. Für das Standarddatenverzeichnis `/home/$USER/.config/Prowlarr` entfernen Sie einfach das `-data`-Argument. Beachten Sie, dass `$USER` der Benutzer ist, unter dem Prowlarr ausgeführt wird und unten definiert ist. {.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/prowlarr.service > /dev/null
[Unit]
Description=Prowlarr-Daemon
After=syslog.target network.target
[Service]
User=prowlarr
Group=prowlarr
Type=simple

ExecStart=/opt/Prowlarr/Prowlarr -nobrowser -data=/var/lib/prowlarr/
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

- Aktivieren Sie den Prowlarr-Dienst:

```shell
sudo systemctl enable --now -q prowlarr
```

- (Optional) Entfernen Sie das Tarball:

```shell
rm Prowlarr*.linux*.tar.gz
```

Normalerweise können Sie auf die Prowlarr-Web-GUI zugreifen, indem Sie zu `http://{Ihre Server-IP-Adresse}:9696` navigieren

Wenn Prowlarr nicht zu starten schien, überprüfen Sie den Status des Dienstes:

```shell
sudo journalctl --since today -u prowlarr
```

---

### Deinstallation

Um zu deinstallieren und zu bereinigen:
> Warnung: Dadurch werden Ihre Anwendungsdaten gelöscht. {.is-danger}

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /var/lib/prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```

Um zu deinstallieren und Ihre Anwendungsdaten zu behalten:

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```