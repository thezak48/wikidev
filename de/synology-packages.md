---
title: Synology-Pakete
description: Servarr Synology-Pakete
published: true
date: 2022-06-23T19:58:34.255Z
tags: lidarr, prowlarr, synology, radarr,readarr,sonarr
editor: markdown
dateCreated: 2022-05-06T13:45:19.731Z
---

- [Servarr Synology-Pakete](#servarr-synology-pakete)
- [DSM 6.x](#dsm-6x)
- [DSM 7.x](#dsm-7x)
  - [Bubblewrap-Installation auf DSM 7.X](#bubblewrap-installation-auf-dsm-7x)
    - [Einfache Bubblewrap-Installation](#einfache-bubblewrap-installation)
    - [Manuelle Bubblewrap-Installation](#manuelle-bubblewrap-installation)

# Servarr Synology-Pakete

> Diese Pakete können als "Beta" betrachtet werden
{.is-danger}

- Das Servarr-Team erstellt und pflegt jetzt Synology-Pakete
- Installationsanweisungen für die spezifischen DSM-Versionen sind unten aufgeführt

> Im Allgemeinen sind die vorhandenen SynoCommunity-Versionen ohne einige Umwege nicht mit den Servarr-Versionen kompatibel. Das bedeutet, dass es erforderlich wäre, das alte Paket nach einer [Sicherung Ihrer Datenbank *der Link ist ein Beispiel für Radarr, aber die Anweisungen/Konzepte sind die gleichen*](/radarr/faq#how-do-i-backuprestore-radarr) zu löschen. Dies kann über die Web-Schnittstelle der \*Arr-App erfolgen.
{.is-warning}

> SynoCommunity hat eine Liste von [NAS nach Architektur](https://github.com/SynoCommunity/spksrc/wiki/Architecture-per-Synology-model), die Ihnen bei der Identifizierung des richtigen Pakets helfen wird.
{.is-info}

# DSM 6.x

- Die Lidarr-Official-, Prowlarr-Official-, Radarr-Official-, Readarr-Official- und Sonarr-Pakete sollten *einfach funktionieren*.
- Beachten Sie, dass das eigenständige Mono-Paket von der SynoCommunity nicht mehr erforderlich ist, es ist derzeit in unserem Paket enthalten.
- Laden Sie die Version der Anwendung für die Architektur Ihres NAS von [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) herunter und [installieren Sie das Paket manuell](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) über den Paket-Manager.

# DSM 7.x

- Die Lidarr-Official-, Prowlarr-Official-, Radarr-Official- und Readarr-Official-Pakete sollten für die meisten Architekturen *einfach funktionieren*.
  - Beachten Sie, dass für ein NAS mit `comcerto2k` zusätzliche Schritte für Lidarr, Prowlarr, Radarr und Readarr erforderlich sind; [siehe die Anweisungen](#bubblewrap-installation-on-dsm-7x).
- Beachten Sie, dass für das Sonarr-Paket zusätzliche Schritte für **alle** Architekturen erforderlich sind.
- Beachten Sie, dass das eigenständige Mono-Paket von der SynoCommunity nicht mehr erforderlich ist, es ist derzeit in unserem Paket enthalten.

> Für NAS, die auf `comcerto2k` laufen (*alle Pakete*) und Sonarr (*alle NAS-Architekturen*), müssen Sie das Bubblewrap-Paket installieren und die manuellen Schritte ausführen. **Bubblewrap muss vor dem Versuch, die \*Arr-Pakete zu installieren, installiert sein**
{.is-warning}

- Laden Sie die Version von Bubblewrap für die Architektur Ihres NAS von [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) herunter und [installieren Sie das Paket manuell](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) über den Paket-Manager.
- Führen Sie die unten stehenden Schritte zur Bubblewrap-Installation für DSM 7.X aus.
- Sobald Bubblewrap installiert ist, können Sie die Version der Anwendung für die Architektur Ihres NAS von [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) herunterladen und [installieren Sie das Paket manuell](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) über den Paket-Manager.

## Bubblewrap-Installation auf DSM 7.X

Bubblewrap ermöglicht es uns, Programme in einem einfachen Container auszuführen, damit wir neue genug Bibliotheken verwenden können, um .NET6 auszuführen.

> **Aufgrund der Einschränkungen in DSM 7.0+ ist nach der Installation eine manuelle Einrichtung erforderlich.**
{.is-danger}

### Einfache Bubblewrap-Installation

1. Erstellen Sie eine ausgelöste Aufgabe in DSM:

- Benutzer: `root`
  - Ereignis: `Systemstart`

1. Geben Sie für den `Ausführen-Befehl` Folgendes ein:

```bash
chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```

1. Speichern Sie die ausgelöste Aufgabe und führen Sie sie einmal aus.

![triggered_task.png](/assets/synology/triggered_task.png)

![create_task1.png](/assets/synology/create_task1.png)

![create_task2.png](/assets/synology/create_task2.png)

![run_task.png](/assets/synology/run_task.png)

### Manuelle Bubblewrap-Installation

1. [Melden Sie sich über SSH bei Ihrem Synology an und wechseln Sie zu `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)
1. Führen Sie die folgenden Befehle aus:

```bash
sudo chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
```

```bash
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```