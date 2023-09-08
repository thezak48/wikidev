---
title: Sonarr FreeBSD Installation
description: Installationsanleitung für Sonarr auf FreeBSD
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# FreeBSD

Das Sonarr-Team stellt nur Builds für FreeBSD zur Verfügung. Plugins und Ports werden von der FreeBSD-Community gepflegt und erstellt.

Anleitungen zur Installation auf FreeBSD werden ebenfalls von der FreeBSD-Community gepflegt, und jeder mit einem GitHub-Konto kann das Wiki bei Bedarf aktualisieren.

[Freshports Sonarr Link](https://www.freshports.org/net-p2p/sonarr/)

## Jail-Einrichtung mit TrueNAS GUI

1. Wählen Sie auf dem Hauptbildschirm "Jails".

1. Klicken Sie auf "HINZUFÜGEN".

1. Klicken Sie auf "Erweiterte Jail-Erstellung".

1. Name (beliebiger Name): Sonarr

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

1. Nachdem das Jail erstellt wurde, wird es automatisch gestartet. Eine weitere Eigenschaft muss festgelegt werden, damit Sonarr den Speicherplatz Ihrer eingebundenen Medienstandorte sehen kann. Öffnen Sie eine Root-Shell auf dem Server und geben Sie diese Befehle ein:

```shell
iocage stop <jailname>
iocage set enforce_statfs=1 <jailname>
iocage start <jailname>
```

## Jail-Einrichtung mit CLI

Voraussetzung ist, dass iocage installiert und konfiguriert ist (<https://iocage.readthedocs.io/en/latest/install.html>).
Voraussetzung ist, dass die iocage-Netzwerkbrücke (vnet) konfiguriert ist (<https://iocage.readthedocs.io/en/latest/networking.html>).

Ersetzen Sie "10.0.0.100" durch eine freie IPV4-Adresse in Ihrem Netzwerk.
Ersetzen Sie "13.1-RELEASE" durch die bevorzugte FreeBSD-Version.
Ersetzen Sie "sonarr" durch Ihren bevorzugten Jail-Namen.
Ersetzen Sie "accept_rtadv" oder entfernen Sie ip6_addr, wenn Sie die automatische Konfiguration von IPV6 nicht wünschen.

```shell
iocage create -n "sonarr" -r 13.1-RELEASE ip4_addr="vnet0|10.0.0.100/24" vnet="on" allow_raw_sockets="1" boot="on" allow_mlock="1" ip6_addr="vnet0|accept_rtadv" enforce_statfs="1"
iocage console sonarr
```

## Sonarr Mono Installation

Gehen Sie zurück zur Jail-Liste und suchen Sie das neu erstellte Jail für `sonarr`. Klicken Sie auf "Shell".

Um Sonarr zu installieren:

> \* Stellen Sie sicher, dass Ihr pkg-Repository so konfiguriert ist, dass Pakete von `/latest` und nicht von `/quarterly` bezogen werden.
> \* Überprüfen Sie `/usr/local/etc/pkg/repos/FreeBSD.conf`.
> \* Wenn dies nicht vorhanden ist, kopieren Sie `/etc/pkg/FreeBSD.conf` an diesen Ort, öffnen Sie es und ersetzen Sie `quarterly` durch `latest`.
{.is-warning}

```shell
pkg install sonarr
```

Schließen Sie die Shell noch nicht, es gibt noch ein paar weitere Schritte!

## Sonarr .NET Installation

Gehen Sie zurück zur Jail-Liste und suchen Sie das neu erstellte Jail für `sonarr`. Klicken Sie auf "Shell".

Um Sonarr zu installieren:

> \* Stellen Sie sicher, dass Ihr pkg-Repository so konfiguriert ist, dass Pakete von `/latest` und nicht von `/quarterly` bezogen werden.
> \* Überprüfen Sie `/usr/local/etc/pkg/repos/FreeBSD.conf`.
> \* Wenn dies nicht vorhanden ist, kopieren Sie `/etc/pkg/FreeBSD.conf` an diesen Ort, öffnen Sie es und ersetzen Sie `quarterly` durch `latest`.
{.is-warning}

Installieren Sie die folgenden Bibliotheken, um Sonarr zu unterstützen:

```shell
pkg install icu libunwind krb5 libnotify libinotify sqlite3
```

Erstellen Sie den Sonarr-Benutzer und die Sonarr-Gruppe (Wenn Sie den Benutzer/Gruppe 'sonarr' nicht verwenden möchten, können Sie dies nach Belieben ändern):

```shell
pw user add sonarr -c sonarr -u 351 -d /nonexistent -s /usr/bin/nologin
```

Laden Sie die neueste Version von <https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64> herunter und setzen Sie die Berechtigungen:

```shell
curl -J -L "https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64" -o Sonarr.develop.freebsd-x64.tar.gz
tar -xvf Sonarr.develop.freebsd-x64.tar.gz -C /usr/local/share
chown -R sonarr:sonarr /usr/local/share/Sonarr
```

Erstellen Sie ein rc.subr-Skript, um Sonarr als Daemon in einem Editor Ihrer Wahl auszuführen (Sie können Zeile 1 überspringen, wenn der Ordner bereits vorhanden ist), und verwenden Sie den Inhalt des folgenden Sonarr rc.subr:

```shell
mkdir -p /usr/local/etc/rc.d
vi /usr/local/etc/rc.d/sonarr
chmod +x /usr/local/etc/rc.d/sonarr
```

```shell
#!/bin/sh

# PROVIDE: sonarr
# REQUIRE: LOGIN
# KEYWORD: shutdown
#
# Fügen Sie die folgenden Zeilen zu /etc/rc.conf.local oder /etc/rc.conf hinzu,
# um diesen Dienst zu aktivieren:
#
# sonarr_enable:   Auf "yes" setzen, um den Sonarr-Dienst zu aktivieren.
#                       Standard: no
# sonarr_user:     Das Benutzerkonto, unter dem der Sonarr-Daemon ausgeführt wird.
#                       Dies ist optional, setzen Sie dies jedoch nicht explizit auf einen
#                       leeren String, da der Daemon dann als root ausgeführt wird.
#                       Standard: sonarr
# sonarr_group:    Das Gruppenkonto, unter dem der Sonarr-Daemon ausgeführt wird.
#                       Dies ist optional, setzen Sie dies jedoch nicht explizit auf einen
#                       leeren String, da der Daemon dann mit der Gruppe wheel ausgeführt wird.
#                       Standard: sonarr
# sonarr_data_dir: Verzeichnis, in dem die Sonarr-Konfigurationsdaten gespeichert werden.
#                       Standard: /var/db/sonarr
# sonarr_pid:      Name der PID-Datei.
#                       Standard: sonarr.pid
# sonarr_pid_dir:  Pfad der PID-Datei.
#                       Standard: /var/run/sonarr

. /etc/rc.subr
name=sonarr
rcvar=${name}_enable
load_rc_config ${name}

: ${sonarr_enable:="no"}
: ${sonarr_user:="sonarr"}
: ${sonarr_group:="sonarr"}
: ${sonarr_data_dir:="/var/db/sonarr"}
: ${sonarr_pid:="sonarr.pid"}
: ${sonarr_pid_dir:="/var/run/sonarr"}

pidfile="${sonarr_pid_dir}/${sonarr_pid}"
command="/usr/sbin/daemon"
command_args="-r -f -P ${pidfile} /usr/local/share/Sonarr/Sonarr --debug --data=${sonarr_data_dir} --nobrowser"

start_precmd=sonarr_start_precmd
sonarr_start_precmd()
{
 [ -d ${sonarr_pid_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_pid_dir}
 [ -d ${sonarr_data_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_data_dir}

 # .NET 6+ verwendet Dual-Mode-Sockets, um die separate AF-Behandlung zu vermeiden.
 # Deaktivieren Sie die Verwendung von V6 durch .NET, wenn kein ipv6 konfiguriert ist.
 # Siehe https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259194#c17
 ifconfig | grep -q inet6
 if [ $? == 1 ]; then
  export DOTNET_SYSTEM_NET_DISABLEIPV6=1
 fi
}

run_rc_command "$1"
```

Schließen Sie die Shell noch nicht, es gibt noch ein paar weitere Schritte!

## Konfiguration von Sonarr

Jetzt, da wir es installiert haben, sind noch ein paar weitere Schritte erforderlich.

### Service-Einrichtung

Es ist Zeit, den Dienst zu aktivieren, aber bevor wir das tun, eine Anmerkung:

Der Updater ist standardmäßig deaktiviert. Die `pkg-message` gibt Anweisungen, wie der Updater aktiviert werden kann, aber beachten Sie: Dies kann dazu führen, dass Dinge wie `pkg check -s` und `pkg remove` für Sonarr nicht mehr funktionieren, wenn der integrierte Updater Dateien ersetzt.

Um den Dienst zu aktivieren:

```shell
sysrc sonarr_enable=TRUE
```

Wenn Sie den Benutzer/Gruppe `sonarr` nicht verwenden möchten, müssen Sie der Dienstdatei mitteilen, unter welchem Benutzer/Gruppe er ausgeführt werden soll.

```shell
sysrc sonarr_user="BENUTZER_DEN_SIE_WÜNSCHEN"
```

```shell
sysrc sonarr_group="GRUPPE_DEN_SIE_WÜNSCHEN"
```

`sonarr` speichert seine Daten, Konfiguration, Protokolle und PID-Dateien standardmäßig in `/usr/local/sonarr`. Die Dienstdatei erstellt dies und übernimmt die Eigentümerschaft, WENN UND NUR WENN ES NICHT VORHANDEN IST. Wenn Sie diese Dateien an einem anderen Ort speichern möchten (z. B. ein in das Jail eingebundenes Dataset für einfachere Snapshots), müssen Sie dies mit `sysrc` ändern.

```shell
sysrc sonarr_data_dir="VERZEICHNIS_DEN_SIE_WÜNSCHEN"
```

Erinnerung: Wenn Sie einen vorhandenen Speicherort verwenden, müssen Sie entweder manuell die Eigentümerschaft auf die UID/GID ändern, die `sonarr` verwendet, UND/ODER `sonarr` zu einer GID hinzufügen, die Schreibzugriff hat.

Fast fertig, lassen Sie uns den Dienst starten:

```shell
service sonarr start
```

Wenn alles nach Plan verlaufen ist, sollte Sonarr auf der IP des Jails (Port 8989) ausgeführt werden!

Sie können die Shell jetzt sicher schließen.

## Fehlerbehebung

- Der Dienst scheint zu laufen, aber die Benutzeroberfläche wird nicht geladen oder die Seite läuft ab
  - Überprüfen Sie, ob `allow_mlock` im Jail aktiviert ist.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Stellen Sie sicher, dass Sie `VNET` für Ihr Jail aktiviert haben, ip6=inherit oder ip6=new

> Das Dienstskript sollte jetzt das Fehlen von VNET und/oder IP6 umgehen und somit die Voraussetzung für VNET oder ip6=inherit entfernen.
{.is-info}

### BSD Mono SSL-Probleme

- SSL- oder andere Zertifikatsprobleme (z. B. `unable to verify SSL certificate`)
  - Siehe [diesen Beitrag im TrueNAS-Forum, da Sie die Zertifikate von Mono aktualisieren und synchronisieren müssen](https://www.truenas.com/community/threads/sonarr-radarr-probably-other-arr-jails-unable-to-verify-ssl-certificates-after-latest-update.96008/)