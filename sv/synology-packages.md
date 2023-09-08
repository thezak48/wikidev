---
title: Synology-paket
description: Servarr Synology-paket
published: true
date: 2022-06-23T19:58:34.255Z
tags: lidarr, prowlarr, synology, radarr,readarr,sonarr
editor: markdown
dateCreated: 2022-05-06T13:45:19.731Z
---

- [Servarr Synology-paket](#servarr-synology-paket)
- [DSM 6.x](#dsm-6x)
- [DSM 7.x](#dsm-7x)
  - [Bubblewrap-installation på DSM 7.X](#bubblewrap-installation-på-dsm-7x)
    - [Enkel Bubblewrap-installation](#enkel-bubblewrap-installation)
    - [Manuell Bubblewrap-installation](#manuell-bubblewrap-installation)

# Servarr Synology-paket

> Dessa paket kan betraktas som "beta"
{.is-danger}

- Servarr-teamet skapar och underhåller nu Synology-paket
- Installationsinstruktioner finns nedan för specifika DSM-versioner

> Generellt sett är de befintliga SynoCommunity-versionerna inte kompatibla med Servarr-versionerna utan vissa anpassningar. Det innebär att det skulle krävas att ta bort det gamla paketet efter att ha gjort en [säkerhetskopia av din databas *länken är för ett Radarr-exempel, men instruktionerna/koncepten är desamma*](/radarr/faq#how-do-i-backuprestore-radarr). Det kan göras via webbgränssnittet för \*Arr-appen.
{.is-warning}

> SynoCommunity har en lista över [NAS efter arkitektur](https://github.com/SynoCommunity/spksrc/wiki/Architecture-per-Synology-model) som hjälper dig att identifiera rätt paket.
{.is-info}

# DSM 6.x

- Lidarr-Official, Prowlarr-Official, Radarr-Official, Readarr-Official och Sonarr-paketen bör *bara fungera*.
- Observera att det fristående Mono-paketet från SynoCommunity inte längre är nödvändigt, det är för närvarande bundet med vårt paket.
- Ladda ner applikationens version för din NAS arkitektur från [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) och [installera paketet manuellt](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via pakethanteraren.

# DSM 7.x

- Lidarr-Official, Prowlarr-Official, Radarr-Official och Readarr-Official-paketen bör *bara fungera* för de flesta arkitekturer.
  - Observera att en NAS med `comcerto2k` kräver ytterligare steg för Lidarr, Prowlarr, Radarr och Readarr; [se instruktionerna](#bubblewrap-installation-på-dsm-7x).
- Observera att Sonarr-paketet kräver ytterligare steg för **alla** arkitekturer.
- Observera att det fristående Mono-paketet från SynoCommunity inte längre är nödvändigt, det är för närvarande bundet med vårt paket.

> För NAS som körs på `comcerto2k` (*alla paket*) och Sonarr (*alla NAS-arkitekturer*), måste du installera Bubblewrap-paketet och utföra de manuella stegen som anges. **Bubblewrap måste installeras innan du försöker installera \*Arr-paketen**
{.is-warning}

- Ladda ner Bubblewrap-versionen för din NAS arkitektur från [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) och [installera paketet manuellt](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via pakethanteraren.
- Slutför nedanstående steg för Bubblewrap-installation på DSM 7.X
- När Bubblewrap är installerat kan du ladda ner applikationens version för din NAS arkitektur från [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) och [installera paketet manuellt](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via pakethanteraren.

## Bubblewrap-installation på DSM 7.X

Bubblewrap gör det möjligt för oss att köra program i en grundläggande behållare så att vi kan använda tillräckligt nya bibliotek för att köra .NET6.

> **På grund av begränsningarna i DSM 7.0+ krävs viss manuell konfiguration efter installationen.**
{.is-danger}

### Enkel Bubblewrap-installation

1. Skapa en utlöst uppgift i DSM:

- Användare: `root`
  - Händelse: `Starta upp`

1. Skriv in följande kommando i "Kör kommando":

```bash
chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```

1. Spara den utlösta uppgiften och kör den en gång.

![triggered_task.png](/assets/synology/triggered_task.png)

![create_task1.png](/assets/synology/create_task1.png)

![create_task2.png](/assets/synology/create_task2.png)

![run_task.png](/assets/synology/run_task.png)

### Manuell Bubblewrap-installation

1. [Logga in på din Synology via SSH och höj till `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)
1. Kör följande kommandon:

```bash
sudo chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
```

```bash
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```