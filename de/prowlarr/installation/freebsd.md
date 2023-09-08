---
title: Prowlarr FreeBSD Installation
description: Installationsanleitung für Prowlarr auf FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Das Prowlarr-Team stellt nur Builds für FreeBSD zur Verfügung. Plugins und Ports werden von der FreeBSD-Community gepflegt und erstellt.

Anleitungen zur Installation auf FreeBSD werden ebenfalls von der FreeBSD-Community gepflegt, und jeder mit einem GitHub-Konto kann das Wiki bei Bedarf aktualisieren.

[Freshports Prowlarr Link](https://www.freshports.org/net-p2p/prowlarr/)

## Jail-Einrichtung mit TrueNAS GUI

1. Wählen Sie auf dem Hauptbildschirm "Jails" aus.

1. Klicken Sie auf "Hinzufügen".

1. Klicken Sie auf "Erweiterte Jail-Erstellung".

1. Name (beliebiger Name): Prowlarr

1. Jail-Typ: Standard (Klon-Jail)

1. Version: 12.2-Release (oder neuer)

1. Konfigurieren Sie die grundlegenden Eigenschaften nach Ihren Wünschen.

1. Konfigurieren Sie die Jail-Eigenschaften nach Ihren Wünschen, aber fügen Sie Folgendes hinzu:

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` ist hilfreich für Fehlerbehebung (z. B. Ping, Traceroute), aber keine Voraussetzung. {.is-info}

1. Konfigurieren Sie die Netzwerkeigenschaften nach Ihren Wünschen.

1. Konfigurieren Sie die benutzerdefinierten Eigenschaften nach Ihren Wünschen.

1. Klicken Sie auf "Speichern".

## Prowlarr-Installation

Suchen Sie in der Liste der Jails Ihre neu erstellte Jail für `prowlarr` und klicken Sie auf "Shell".

Um Prowlarr zu installieren:

> \* Stellen Sie sicher, dass Ihr pkg-Repository so konfiguriert ist, dass Pakete von `/latest` und nicht von `/quarterly` bezogen werden.
> \* Überprüfen Sie `/usr/local/etc/pkg/repos/FreeBSD.conf`.
> \* Wenn dies nicht vorhanden ist, kopieren Sie `/etc/pkg/FreeBSD.conf` an diesen Ort, öffnen Sie es und ersetzen Sie `quarterly` durch `latest`.
{.is-warning}

```shell
pkg install prowlarr
```

Schließen Sie die Shell noch nicht, es gibt noch ein paar weitere Dinge zu tun!

## Konfiguration von Prowlarr

Jetzt, da wir es installiert haben, sind noch ein paar weitere Schritte erforderlich.

### Service-Einrichtung

Es ist Zeit, den Service zu aktivieren, aber zuvor eine Anmerkung:

Der Updater ist standardmäßig deaktiviert. Die `pkg-message` gibt Anweisungen, wie der Updater aktiviert werden kann, aber beachten Sie: Dies kann dazu führen, dass Dinge wie `pkg check -s` und `pkg remove` für Prowlarr nicht mehr funktionieren, wenn der integrierte Updater Dateien ersetzt.

Um den Service zu aktivieren:

```shell
sysrc prowlarr_enable=TRUE
```

Wenn Sie nicht den Benutzer/Gruppe `prowlarr` verwenden möchten, müssen Sie der Service-Datei mitteilen, unter welchem Benutzer/Gruppe sie ausgeführt werden soll.

```shell
sysrc prowlarr_user="GEWÜNSCHTER_BENUTZER"
```

```shell
sysrc prowlarr_group="GEWÜNSCHTE_GRUPPE"
```

`prowlarr` speichert seine Daten, Konfiguration, Protokolle und PID-Dateien standardmäßig in `/usr/local/prowlarr`. Die Service-Datei erstellt dies und übernimmt den Besitz, WENN UND NUR WENN ES NICHT VORHANDEN IST. Wenn Sie diese Dateien an einem anderen Ort speichern möchten (z. B. ein Dataset, das in die Jail eingebunden ist, um einfachere Snapshots zu erstellen), müssen Sie dies mit `sysrc` ändern.

```shell
sysrc prowlarr_data_dir="GEWÜNSCHTES_VERZEICHNIS"
```

Erinnerung: Wenn Sie einen vorhandenen Speicherort verwenden, müssen Sie entweder manuell den Besitz auf die UID/GID ändern, die `prowlarr` verwendet, UND/ODER `prowlarr` zu einer GID hinzufügen, die Schreibzugriff hat.

Fast fertig, starten wir den Service:

```shell
service prowlarr start
```

Wenn alles nach Plan verlaufen ist, sollte Prowlarr auf der IP der Jail (Port 9696) ausgeführt werden!

Sie können die Shell jetzt sicher schließen.

## Fehlerbehebung

- Der Service scheint ausgeführt zu werden, aber die Benutzeroberfläche wird nicht geladen oder die Seite läuft ab.
  - Überprüfen Sie erneut, ob `allow_mlock` in der Jail aktiviert ist.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Stellen Sie sicher, dass Sie `VNET` für Ihre Jail aktiviert haben, ip6=inherit oder ip6=new.

> Das Service-Skript sollte jetzt das Fehlen von VNET und/oder IP6 umgehen und somit die Voraussetzung für VNET oder ip6=inherit entfernen.
{.is-info}