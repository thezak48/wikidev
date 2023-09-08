---
title: Radarr Linux Installation
description: Linux-Installationsanleitung für Radarr
published: true
date: 2023-09-07T20:43:01.533Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:59.391Z
---

# Linux

## Debian / Ubuntu

> Hinweis: Raspberry Pi OS und Raspbian sind beide Varianten von Debian {.is-info}

### Einfache Installation

Für Anfänger in Debian / Ubuntu / Raspbian gibt es kein Apt-Repository oder Deb-Paket.

Wenn Sie es einfach haben möchten, folgen Sie diesem von der Community bereitgestellten und gepflegten `Easy Install`-Skript für eine Basisinstallation von Debian (Raspbian / Raspberry Pi OS) / Ubuntu.

**Für die offiziellen Installationsanweisungen, die "Hands-on" sind, folgen Sie den weiter unten stehenden [Debian / Ubuntu Hands-on Install](#debian-ubuntu-hands-on-install)-Schritten.**

[Bitte sehen Sie sich das \*Arr Community Installationsskript an](/install-script)

> Radarr verwendet eine gebündelte Version von ffprobe für die Analyse von Mediendateien und erfordert nicht, dass ffprobe oder ffmpeg auf dem System installiert sind. Wenn Radarr angibt, dass Ffprobe nicht gefunden wurde, kann dies in der Regel durch eine Neuinstallation behoben werden.
{.is-info}

### Debian / Ubuntu Hands-on Install

Sie müssen die Binärdateien mit den folgenden Befehlen installieren.

> Die folgenden Schritte laden die stabile Version (Hauptversionszweig "master") von Radarr herunter und installieren sie in `/opt`.
> Radarr wird unter dem Benutzer `radarr` und der Gruppe `media` ausgeführt. `media` ist die häufig empfohlene Gruppe, unter der die \*Arrs, Download-Clients und Media-Server ausgeführt werden.
> Die Konfigurationsdateien von Radarr werden in `/var/lib/radarr` gespeichert.
{.is-success}

- Stellen Sie sicher, dass Sie die erforderlichen Voraussetzungspakete installiert haben:

```shell
sudo apt install curl sqlite3
```

> Warnung: Wenn Sie die folgenden Voraussetzungen ignorieren, schlägt die Installation fehl und die Anwendung funktioniert nicht ordnungsgemäß. {.is-warning}

> **Installationsvoraussetzungen**
> Die folgenden Anweisungen basieren auf den folgenden Voraussetzungen. Passen Sie die Anweisungen bei Bedarf an Ihre spezifischen Anforderungen an.
> \* Der Benutzer `radarr` ist erstellt
> \* Der Benutzer `radarr` gehört zur Gruppe `media`
> \* Ihre Download-Clients und Media-Server werden als und sind Teil der Gruppe `media` ausgeführt
> \* Ihre Pfade, die von Ihren Download-Clients und Media-Servern verwendet werden, sind für die Gruppe `media` zugänglich (lesen/schreiben)
> \* Sie haben das Verzeichnis `/var/lib/radarr` erstellt und sichergestellt, dass der Benutzer `radarr` Lese-/Schreibrechte dafür hat
> \* Vorherige/vorhandene Installationen verwendeten den Hauptversionszweig "master", der in den [FAQ](/radarr/faq) angegeben ist, oder Sie aktualisieren "master" in der Download-URL
{.is-danger}

> Durch die Fortsetzung unten bestätigen Sie, dass Sie die oben genannten Anforderungen gelesen und erfüllt haben. {.is-success}

- Laden Sie die richtigen Binärdateien für Ihre Architektur herunter.
  - Sie können Ihre Architektur mit `dpkg --print-architecture` ermitteln
    - AMD64 verwenden `arch=x64`
    - ARM, armf und armh verwenden `arch=arm`
    - ARM64 verwenden `arch=arm64`

```shell
wget --content-disposition 'http://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Entpacken Sie die Dateien:

```shell
tar -xvzf Radarr*.linux*.tar.gz
```

- Verschieben Sie die Dateien nach `/opt/`

```shell
sudo mv Radarr /opt/
```

> Hinweis: Dies setzt voraus, dass Sie als Benutzer `radarr` und Gruppe `media` ausgeführt werden. Sie können dies entsprechend Ihren Anforderungen ändern. Es ist wichtig, dass Sie bei Ihren Mediendateien zumindest den Gruppennamen zwischen Ihrem Download-Client(s) und Radarr identisch halten.
{.is-danger}

- Stellen Sie den Besitz des Binärverzeichnisses sicher.

```shell  
sudo chown radarr:radarr -R /opt/Radarr
```

- Konfigurieren Sie systemd, damit Radarr beim Start automatisch gestartet wird.

> Das unten stehende systemd-Erstellungsskript verwendet ein Datenverzeichnis von `/var/lib/radarr`. Stellen Sie sicher, dass es existiert oder passen Sie es bei Bedarf an. Für das Standarddatenverzeichnis `/home/$USER/.config/Radarr` entfernen Sie einfach das `-data`-Argument. Beachten Sie, dass `$USER` der Benutzer ist, unter dem Radarr ausgeführt wird und unten definiert ist.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/radarr.service > /dev/null
[Unit]
Description=Radarr-Daemon
After=syslog.target network.target
[Service]
User=radarr
Group=media
Type=simple

ExecStart=/opt/Radarr/Radarr -nobrowser -data=/var/lib/radarr/
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

- Aktivieren Sie den Radarr-Dienst:

```shell
sudo systemctl enable --now -q radarr
```

- (Optional) Entfernen Sie das Tarball:

```shell
rm Radarr*.linux*.tar.gz
```

Normalerweise greifen Sie auf die Radarr-Webbenutzeroberfläche zu, indem Sie zu `http://{Ihre Server-IP-Adresse}:7878` navigieren

> Radarr verwendet eine gebündelte Version von ffprobe für die Analyse von Mediendateien und erfordert nicht, dass ffprobe oder ffmpeg auf dem System installiert sind. Wenn Radarr angibt, dass Ffprobe nicht gefunden wurde, kann dies in der Regel durch eine Neuinstallation behoben werden.
{.is-info}

Wenn Radarr nicht zu starten scheint, überprüfen Sie den Status des Dienstes:

```shell
sudo journalctl --since today -u radarr
```

---

### Deinstallation

Um zu deinstallieren und zu bereinigen:
> Warnung: Dadurch werden Ihre Anwendungsdaten zerstört. {.is-danger}

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /var/lib/radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```

Um zu deinstallieren und Ihre Anwendungsdaten zu behalten:

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```