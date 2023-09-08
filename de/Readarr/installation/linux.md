---
title: Readarr Linux Installation
description: Linux-Installationsanleitung für Readarr
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

**Für die offiziellen Installationsanweisungen, die "Hands-on" sind, folgen Sie den [Debian / Ubuntu Hands-on Install](#debian-ubuntu-hands-on-install)-Schritten weiter unten.**

[Bitte sehen Sie sich das \*Arr Community Installations-Skript an](/install-script)

### Debian / Ubuntu Hands-on Install

Sie müssen die Binärdateien mit den folgenden Befehlen installieren.

> Die folgenden Schritte laden Readarr herunter und installieren es in `/opt`
> Readarr wird unter dem Benutzer `readarr` und der Gruppe `media` ausgeführt; `media` ist die häufig empfohlene Gruppe, unter der die \*Arrs, Download-Clients und Media-Server ausgeführt werden.
> Die Konfigurationsdateien von Readarr werden in `/var/lib/readarr` gespeichert.
{.is-warning}

- Stellen Sie sicher, dass Sie die erforderlichen Voraussetzungspakete installiert haben:

```shell
sudo apt install curl sqlite3
```

> Warnung: Wenn Sie die folgenden Voraussetzungen ignorieren, schlägt die Installation fehl und die Anwendung funktioniert nicht. {.is-warning}

> **Installationsvoraussetzungen**
> Die folgenden Anweisungen basieren auf den folgenden Voraussetzungen. Passen Sie die Anweisungen bei Bedarf an Ihre spezifischen Anforderungen an.
> \* Der Benutzer `readarr` ist erstellt
> \* Der Benutzer `readarr` gehört zur Gruppe `media`
> \* Ihre Download-Clients und Media-Server werden als und sind Teil der Gruppe `media` ausgeführt
> \* Ihre Pfade, die von Ihren Download-Clients und Media-Servern verwendet werden, sind für die Gruppe `media` zugänglich (lesen/schreiben)
> \* Wenn Calibre verwendet wird, wird Calibre als Gruppe `media` ausgeführt und die Calibre-Bibliothek hat Lese-/Schreibberechtigungen für `media`
> \* Sie haben das Verzeichnis `/var/lib/readarr` erstellt und sichergestellt, dass der Benutzer `readarr` Lese-/Schreibberechtigungen dafür hat
{.is-danger}

> Durch die Fortsetzung unten bestätigen Sie, dass Sie die oben genannten Anforderungen gelesen und erfüllt haben. {.is-warning}

- Laden Sie die richtigen Binärdateien für Ihre Architektur herunter.
  - Sie können Ihre Architektur mit `dpkg --print-architecture` ermitteln
    - AMD64 verwenden `arch=x64`
    - ARM, armf und armh verwenden `arch=arm`
    - ARM64 verwenden `arch=arm64`

```shell
wget --content-disposition 'http://readarr.servarr.com/v1/update/develop/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Entpacken Sie die Dateien:

```shell
tar -xvzf Readarr*.linux*.tar.gz
```

- Verschieben Sie die Dateien nach `/opt/`

```shell
sudo mv Readarr /opt/
```

> Hinweis: Dies setzt voraus, dass Sie den Benutzer erstellt haben und als Benutzer `readarr` und Gruppe `media` ausgeführt werden. Sie können dies entsprechend Ihren Anforderungen ändern. Es ist wichtig, den Gruppennamen zwischen Ihrem Download-Client(s) und Readarr identisch zu halten, um Berechtigungsprobleme mit Ihren Mediendateien zu vermeiden. Bitte beachten Sie, dass Readarr Berechtigungen für dieses Verzeichnis benötigt, wenn Sie Calibre verwenden möchten.
{.is-danger}

- Stellen Sie den Besitz des Binärverzeichnisses sicher.

```shell  
sudo chown readarr:readarr -R /opt/Readarr
```

- Konfigurieren Sie systemd, damit Readarr beim Start automatisch gestartet werden kann.

> Das unten stehende systemd-Erstellungsskript verwendet ein Datenverzeichnis von `/var/lib/readarr`. Stellen Sie sicher, dass es existiert oder passen Sie es bei Bedarf an. Für das Standard-Datenverzeichnis `/home/$USER/.config/Readarr` entfernen Sie einfach das `-data`-Argument. Beachten Sie, dass `$USER` der Benutzer ist, unter dem Readarr ausgeführt wird und unten definiert ist.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr.service > /dev/null
[Unit]
Description=Readarr-Daemon
After=syslog.target network.target
[Service]
User=readarr
Group=media
Type=simple

ExecStart=/opt/Readarr/Readarr -nobrowser -data=/var/lib/readarr/
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
```

- systemd neu laden:

```shell
sudo systemctl -q daemon-reload
```

- Aktivieren Sie den Readarr-Dienst:

```shell
sudo systemctl enable --now -q readarr
```

- (Optional) Entfernen Sie das Tarball:

```shell
rm Readarr*.linux*.tar.gz
```

Normalerweise greifen Sie über `http://{Ihre Server-IP-Adresse}:8787` auf die Readarr-Web-GUI zu.

Wenn Readarr nicht zu starten schien, überprüfen Sie den Status des Dienstes:

```shell
sudo journalctl --since today -u readarr
```

---

### Deinstallation

Um zu deinstallieren und zu bereinigen:
> Warnung: Dadurch werden Ihre Anwendungsdaten gelöscht. {.is-danger}

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /var/lib/readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```

Um zu deinstallieren und Ihre Anwendungsdaten zu behalten:

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```