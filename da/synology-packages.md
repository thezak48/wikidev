---
title: Synology Pakker
description: Servarr Synology Pakker
published: true
date: 2022-06-23T19:58:34.255Z
tags: lidarr, prowlarr, synology, radarr,readarr,sonarr
editor: markdown
dateCreated: 2022-05-06T13:45:19.731Z
---

- [Servarr Synology Pakker](#servarr-synology-pakker)
- [DSM 6.x](#dsm-6x)
- [DSM 7.x](#dsm-7x)
  - [Bubblewrap Installation på DSM 7.X](#bubblewrap-installation-på-dsm-7x)
    - [Simpel Bubblewrap Installation](#simpel-bubblewrap-installation)
    - [Manuel Bubblewrap Installation](#manuel-bubblewrap-installation)

# Servarr Synology Pakker

> Disse pakker kan betragtes som "beta"
{.is-danger}

- Servarr-teamet opretter og vedligeholder nu Synology-pakker
- Installationsinstruktioner er angivet nedenfor for de specifikke DSM-versioner

> Generelt er de eksisterende SynoCommunity-versioner ikke kompatible med Servarr-versionerne uden nogle omveje. Dette betyder, at det ville være nødvendigt at slette den gamle pakke efter at have taget en [sikkerhedskopi af din database *linket er til et Radarr-eksempel, men instruktionerne/koncepterne er de samme*](/radarr/faq#how-do-i-backuprestore-radarr). Dette kan gøres via webgrænsefladen for \*Arr-appen.
{.is-warning}

> SynoCommunity har en liste over [NAS efter arkitektur](https://github.com/SynoCommunity/spksrc/wiki/Architecture-per-Synology-model), som vil hjælpe dig med at identificere den korrekte pakke.
{.is-info}

# DSM 6.x

- Lidarr-Official, Prowlarr-Official, Radarr-Official, Readarr-Official og Sonarr-pakkerne skulle *bare virke*.
- Bemærk, at den selvstændige Mono-pakke fra SynoCommunity ikke længere er nødvendig, den er i øjeblikket inkluderet i vores pakke.
- Download udgivelsen af ​​applikationen til din NAS' arkitektur fra [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) og [installer pakken manuelt](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via pakkehåndteringen.

# DSM 7.x

- Lidarr-Official, Prowlarr-Official, Radarr-Official og Readarr-Official-pakkerne skulle *bare virke* for de fleste arkitekturer.
  - Bemærk, at en NAS med `comcerto2k` kræver yderligere trin for Lidarr, Prowlarr, Radarr og Readarr; [se instruktionerne](#bubblewrap-installation-på-dsm-7x).
- Bemærk, at Sonarr-pakken kræver yderligere trin for **alle** arkitekturer.
- Bemærk, at den selvstændige Mono-pakke fra SynoCommunity ikke længere er nødvendig, den er i øjeblikket inkluderet i vores pakke.

> For NAS, der kører på `comcerto2k` (*alle pakker*) og Sonarr (*alle NAS-arkitekturer*), skal du installere Bubblewrap-pakken og udføre de manuelle trin, der er angivet. **Bubblewrap skal installeres, inden du forsøger at installere \*Arr-pakkerne**
{.is-warning}

- Download udgivelsen af ​​Bubblewrap til din NAS' arkitektur fra [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) og [installer pakken manuelt](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via pakkehåndteringen.
- Udfør nedenstående trin for Bubblewrap-installation på DSM 7.X
- Når Bubblewrap er installeret, kan du downloade udgivelsen af ​​applikationen til din NAS' arkitektur fra [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) og [installer pakken manuelt](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via pakkehåndteringen.

## Bubblewrap Installation på DSM 7.X

Bubblewrap giver os mulighed for at køre programmer i en grundlæggende container, så vi kan bruge nye nok biblioteker til at køre .NET6.

> **På grund af begrænsningerne i DSM 7.0+ kræves der nogle manuelle indstillinger efter installationen.**
{.is-danger}

### Simpel Bubblewrap Installation

1. Opret en udløst opgave i DSM:

- Bruger: `root`
  - Begivenhed: `Opstart`

1. Indtast følgende kommando i feltet `Kør kommando`:

```bash
chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```

1. Gem den udløste opgave og kør den en gang.

![triggered_task.png](/assets/synology/triggered_task.png)

![create_task1.png](/assets/synology/create_task1.png)

![create_task2.png](/assets/synology/create_task2.png)

![run_task.png](/assets/synology/run_task.png)

### Manuel Bubblewrap Installation

1. [Log ind på din Synology via SSH og hæv til `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)
1. Udfør følgende kommandoer:

```bash
sudo chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
```

```bash
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```