---
title: Sonarr Synology Installation
description: Installationsanleitung für Sonarr auf Synology
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Synology

- [Die SynoCommunity erstellt, unterstützt und pflegt ein Synology NAS-Paket](https://synocommunity.com/package/nzbdrone)

> Das NAS-Paket wird schlecht gewartet und ist häufig veraltet. Wenn Ihr NAS Docker unterstützt, wird dringend empfohlen, [Docker auszuführen](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/). Sie können Sonarr nicht neu installieren, ohne Ihre Datenbank manuell zu löschen, da das NAS-Paket veraltet ist und nicht so konfiguriert ist, dass es sich beim Start aktualisiert. {.is-info}

- [Die SynoCommunity erstellt, unterstützt und pflegt auch das erforderliche Mono-Paket](https://synocommunity.com/package/mono)

## Synology Mono SSL-Fehler

> Aufgrund eines Fehlers im schlecht gewarteten Mono-Paket der SynoCommunity kann Sonarr nach dem Aktualisieren von Mono oder nach einer Neuinstallation keine Verbindung herstellen. Dieses Problem kann behoben werden, indem Sie den Anweisungen in [SynoCommunity Bug Report #5051](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1009758625) folgen. Beachten Sie, dass DSM7-Benutzer basierend auf [diesem Kommentar](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1153245799) einen zusätzlichen Schritt haben.
{.is-danger}

1. Aktivieren Sie in DSM den SSH-Dienst unter *Systemsteuerung => Terminal & SNMP* und klicken Sie auf "Anwenden".
1. Verbinden Sie sich mit dem NAS über [Terminal](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) (MacOS) mit dem Befehl `ssh -l [Administrator-Benutzername] [NAS-Adresse]` oder über [Putty](https://www.putty.org/) (Windows) mit der Netzwerkadresse Ihres NAS.
1. Geben Sie das erforderliche Administratorpasswort ein und drücken Sie die Eingabetaste.
1. Geben Sie den entsprechenden Befehl für Ihre DSM-Version ein, wie unten angegeben, und drücken Sie die Eingabetaste.
1. Geben Sie das erforderliche Administratorpasswort ein und drücken Sie die Eingabetaste. Wenn der Vorgang abgeschlossen ist, sollte die Meldung *Importprozess abgeschlossen* angezeigt werden.
1. Beenden Sie die SSH-Sitzung, indem Sie `exit` eingeben und die Eingabetaste drücken.
1. Deaktivieren Sie in DSM den SSH-Dienst unter *Systemsteuerung => Terminal & SNMP* und klicken Sie auf "Anwenden".
1. Nach Abschluss sollten die Fehler in Sonarr von selbst verschwinden.

### Befehl zur Behebung von Synology DSM6 Mono

```shell
sudo /var/packages/mono/target/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
```

### Befehl zur Behebung von Synology DSM7 Mono

```shell
sudo /volume1/@appstore/mono/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
sudo chmod -R a+rX /usr/share/.mono
```