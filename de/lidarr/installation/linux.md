---
title: Lidarr Linux Installation
description: Linux-Installationsanleitung für Lidarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Hinweis: Raspberry Pi OS und Raspbian sind beides Varianten von Debian {.is-info}

> Lidarr v0.8 ist nicht mit Ubuntu 22.04 kompatibel und wird nicht unterstützt. [Weitere Informationen finden Sie in diesem FAQ-Eintrag](/lidarr/faq#lidarr-stopped-working-after-updating-to-ubuntu-2204)
{.is-warning}

### Einfache Installation

Für Anfänger in Debian / Ubuntu / Raspbian gibt es kein Apt-Repository oder Deb-Paket.

Wenn Sie es einfach haben möchten, folgen Sie diesem von der Community bereitgestellten und gepflegten `Easy Install`-Skript für eine grundlegende Debian (Raspbian / Raspberry Pi OS) / Ubuntu-Installation.

**Für die offiziellen Installationsanweisungen, die "Hands-on" sind, folgen Sie den [Debian / Ubuntu Hands-on Install](#debian-ubuntu-hands-on-install)-Schritten weiter unten.**

[Bitte sehen Sie sich das \*Arr Community Installationsskript an](/install-script)

### Debian / Ubuntu Hands-on Install

Sie müssen die Binärdateien mit den folgenden Befehlen installieren.

> Die folgenden Schritte laden Lidarr herunter und installieren es in `/opt`
> Lidarr wird unter dem Benutzer `lidarr` und der Gruppe `media` ausgeführt
> Lidarrs Konfigurationsdateien werden in `/var/lib/lidarr` gespeichert
{.is-warning}

- Stellen Sie sicher, dass Sie die erforderlichen Voraussetzungspakete installiert haben:

```shell
sudo apt install curl mediainfo sqlite3 libchromaprint-tools
```

> Warnung: Das Ignorieren der unten aufgeführten Voraussetzungen führt zu einer fehlgeschlagenen Installation und einer nicht funktionierenden Anwendung. {.is-warning}

> **Installationsvoraussetzungen**
> Die folgenden Anweisungen basieren auf den folgenden Voraussetzungen. Passen Sie die Anweisungen bei Bedarf an Ihre spezifischen Anforderungen an.
> \* Der Benutzer `lidarr` ist erstellt
> \* Der Benutzer `lidarr` gehört zur Gruppe `media`
> \* Ihre Download-Clients und Media-Server werden als und sind Teil der Gruppe `media` ausgeführt
> \* Ihre Pfade, die von Ihren Download-Clients und Media-Servern verwendet werden, sind für die Gruppe `media` zugänglich (lesen/schreiben)
> \* Sie haben das Verzeichnis `/var/lib/lidarr` erstellt und sichergestellt, dass der Benutzer `lidarr` Lese-/Schreibrechte dafür hat
{.is-danger}

> Durch die Fortsetzung unten bestätigen Sie, dass Sie die oben genannten Anforderungen gelesen und erfüllt haben. {.is-warning}

- Laden Sie die richtigen Binärdateien für Ihre Architektur herunter.
  - Sie können Ihre Architektur mit `dpkg --print-architecture` ermitteln
    - AMD64 verwenden `arch=x64`
    - ARM, armf und armh verwenden `arch=arm`
    - ARM64 verwenden `arch=arm64`

```shell
wget --content-disposition 'http://lidarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Entpacken Sie die Dateien:

```shell
tar -xvzf Lidarr*.linux*.tar.gz
```

- Verschieben Sie die Dateien nach `/opt/`

```shell
sudo mv Lidarr/ /opt
```

> Dies setzt voraus, dass Sie den Benutzer erstellt haben und als Benutzer `lidarr` und Gruppe `media` ausgeführt werden. Sie können dies entsprechend Ihren Anforderungen ändern. Es ist wichtig, diese richtig zu wählen, um Berechtigungsprobleme mit Ihren Mediendateien zu vermeiden. Wir empfehlen, den Gruppennamen zwischen Ihrem Download-Client(s) und Lidarr identisch zu halten.
{.is-danger}

- Stellen Sie den Besitz des Binärverzeichnisses sicher.

```shell
sudo chown -R lidarr:media /opt/Lidarr
```

- Konfigurieren Sie systemd, damit Lidarr beim Start automatisch gestartet werden kann.

> Das unten stehende systemd-Erstellungsskript verwendet ein Datenverzeichnis von `/var/lib/lidarr`. Stellen Sie sicher, dass es existiert oder passen Sie es bei Bedarf an. Für das Standarddatenverzeichnis `/home/$USER/.config/Lidarr` entfernen Sie einfach das `-data`-Argument. Beachten Sie, dass `$USER` der Benutzer ist, unter dem Lidarr ausgeführt wird und unten definiert ist.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/lidarr.service > /dev/null
[Unit]
Description=Lidarr-Daemon
After=syslog.target network.target
[Service]
User=lidarr
Group=media
Type=simple

ExecStart=/opt/Lidarr/Lidarr -nobrowser -data=/var/lib/lidarr/
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

- Aktivieren Sie den Lidarr-Dienst:

```shell
sudo systemctl enable --now -q lidarr
```

- (Optional) Entfernen Sie das Tarball:

```shell
rm Lidarr*.linux*.tar.gz
```

Normalerweise können Sie auf die Lidarr-Web-Oberfläche zugreifen, indem Sie zu `http://{Ihre Server-IP-Adresse}:8686` navigieren

Wenn Lidarr nicht zu starten schien, überprüfen Sie den Status des Dienstes:

```shell
sudo journalctl --since today -u lidarr
```

---

### Deinstallation

Um zu deinstallieren und zu bereinigen:
> Warnung: Dadurch werden Ihre Anwendungsdaten gelöscht. {.is-danger}

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /var/lib/lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```

Um zu deinstallieren und Ihre Anwendungsdaten zu behalten:

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```