---
title: Readarr FreeBSD Installation
description: FreeBSD-Installationsanleitung für Readarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Das Readarr-Team stellt nur Builds für FreeBSD zur Verfügung. Plugins und Ports werden von der FreeBSD-Community gepflegt und erstellt.

Anleitungen für FreeBSD-Installationen werden ebenfalls von der FreeBSD-Community gepflegt, und jeder mit einem GitHub-Konto kann das Wiki bei Bedarf aktualisieren.

[Freshports Readarr Link](https://www.freshports.org/net-p2p/readarr/)

## Jail-Einrichtung mit TrueNAS GUI

1. Wählen Sie auf dem Hauptbildschirm Jails aus.

1. Klicken Sie auf HINZUFÜGEN.

1. Klicken Sie auf Erweiterte Jail-Erstellung.

1. Name (beliebiger Name möglich): Readarr

1. Jail-Typ: Standard (Klon-Jail)

1. Release: 12.2-Release (oder neuer)

1. Konfigurieren Sie die grundlegenden Eigenschaften nach Ihren Wünschen.

1. Konfigurieren Sie die Jail-Eigenschaften nach Ihren Wünschen, aber fügen Sie hinzu:

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` ist hilfreich für Fehlerbehebung (z. B. Ping, Traceroute), aber keine Voraussetzung. {.is-info}

1. Konfigurieren Sie die Netzwerkeigenschaften nach Ihren Wünschen.

1. Konfigurieren Sie die benutzerdefinierten Eigenschaften nach Ihren Wünschen.

1. Klicken Sie auf Speichern.

1. Nachdem das Jail erstellt wurde, wird es automatisch gestartet. Eine weitere Eigenschaft muss festgelegt werden, damit Readarr den Speicherplatz Ihrer eingebundenen Medienorte sehen kann. Öffnen Sie eine Root-Shell auf dem Server und geben Sie diese Befehle ein:

```shell
iocage stop <jailname>
iocage set enforce_statfs=1 <jailname>
iocage start <jailname>
```

## Readarr-Installation

Suchen Sie in der Jails-Liste Ihr neu erstelltes Jail für `readarr` und klicken Sie auf "Shell".

Um Readarr zu installieren:

> \* Stellen Sie sicher, dass Ihr pkg-Repository so konfiguriert ist, dass Pakete von `/latest` und nicht von `/quarterly` bezogen werden.
> \* Überprüfen Sie `/usr/local/etc/pkg/repos/FreeBSD.conf`.
> \* Wenn dies nicht vorhanden ist, kopieren Sie `/etc/pkg/FreeBSD.conf` an diesen Ort, öffnen Sie es und ersetzen Sie `quarterly` durch `latest`.
{.is-warning}

```shell
pkg install readarr
```

Schließen Sie die Shell noch nicht, es gibt noch ein paar weitere Dinge zu tun!

## Konfiguration von Readarr

Jetzt, da wir es installiert haben, sind noch ein paar weitere Schritte erforderlich.

### Service-Einrichtung

Es ist Zeit, den Service zu aktivieren, aber bevor wir das tun, eine Anmerkung:

Der Updater ist standardmäßig deaktiviert. Die `pkg-message` gibt Anweisungen, wie der Updater aktiviert werden kann, aber beachten Sie: Dies kann Dinge wie `pkg check -s` und `pkg remove` für Readarr brechen, wenn der integrierte Updater Dateien ersetzt.

Um den Service zu aktivieren:

```shell
sysrc readarr_enable=TRUE
```

Wenn Sie nicht den Benutzer/Gruppe `readarr` verwenden möchten, müssen Sie der Service-Datei mitteilen, unter welchem Benutzer/Gruppe sie ausgeführt werden soll.

```shell
sysrc readarr_user="BENUTZER_DEN_SIE_WOLLEN"
```

```shell
sysrc readarr_group="GRUPPE_DEN_SIE_WOLLEN"
```

`readarr` speichert seine Daten, Konfiguration, Protokolle und PID-Dateien standardmäßig in `/usr/local/readarr`. Die Service-Datei erstellt dies und übernimmt den Besitz davon, WENN UND NUR WENN ES NICHT VORHANDEN IST. Wenn Sie diese Dateien an einem anderen Ort speichern möchten (z. B. ein Dataset, das in das Jail eingebunden ist, um einfachere Snapshots zu erstellen), müssen Sie dies mit `sysrc` ändern.

```shell
sysrc readarr_data_dir="ORDNER_DEN_SIE_WOLLEN"
```

Erinnerung: Wenn Sie einen vorhandenen Speicherort verwenden, müssen Sie entweder die Eigentümerschaft auf die UID/GID ändern, die `readarr` verwendet, UND/ODER `readarr` zu einer GID hinzufügen, die Schreibzugriff hat.

Fast fertig, lassen Sie uns den Service starten:

```shell
service readarr start
```

Wenn alles nach Plan verlaufen ist, sollte Readarr auf der IP des Jails (Port 8787) ausgeführt werden!

Sie können die Shell jetzt sicher schließen.

## Fehlerbehebung

- Der Service scheint ausgeführt zu werden, aber die Benutzeroberfläche wird nicht geladen oder die Seite läuft ab.
  - Überprüfen Sie, ob `allow_mlock` im Jail aktiviert ist.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Stellen Sie sicher, dass Sie `VNET` für Ihr Jail aktiviert haben, ip6=inherit oder ip6=new.

> Das Service-Skript sollte jetzt das Fehlen von VNET und/oder IP6 umgehen und somit die Voraussetzung für VNET oder ip6=inherit entfernen.
{.is-info}