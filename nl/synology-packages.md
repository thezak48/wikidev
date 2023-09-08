---
title: Synology-pakketten
description: Servarr Synology-pakketten
published: true
date: 2022-06-23T19:58:34.255Z
tags: lidarr, prowlarr, synology, radarr,readarr,sonarr
editor: markdown
dateCreated: 2022-05-06T13:45:19.731Z
---

- [Servarr Synology-pakketten](#servarr-synology-pakketten)
- [DSM 6.x](#dsm-6x)
- [DSM 7.x](#dsm-7x)
  - [Bubblewrap-installatie op DSM 7.X](#bubblewrap-installatie-op-dsm-7x)
    - [Eenvoudige Bubblewrap-installatie](#eenvoudige-bubblewrap-installatie)
    - [Handmatige Bubblewrap-installatie](#handmatige-bubblewrap-installatie)

# Servarr Synology-pakketten

> Deze pakketten kunnen als "bèta" worden beschouwd
{.is-danger}

- Het Servarr-team maakt nu Synology-pakketten en onderhoudt deze
- Installatie-instructies worden hieronder vermeld voor de specifieke DSM-versies

> Over het algemeen zijn de bestaande SynoCommunity-versies niet compatibel met de Servarr-versies zonder enige moeite. Dit betekent dat het nodig zou zijn om het oude pakket te verwijderen na het maken van een [back-up van uw database *de link is voor een Radarr-voorbeeld, maar de instructies/concepten zijn hetzelfde*](/radarr/faq#how-do-i-backuprestore-radarr). Dit kan worden gedaan via de webinterface van de \*Arr-app.
{.is-warning}

> SynoCommunity heeft een lijst met [NAS per architectuur](https://github.com/SynoCommunity/spksrc/wiki/Architecture-per-Synology-model) die u kunnen helpen bij het identificeren van het juiste pakket.
{.is-info}

# DSM 6.x

- De Lidarr-Official, Prowlarr-Official, Radarr-Official, Readarr-Official en Sonarr-pakketten zouden *gewoon moeten werken*.
- Merk op dat het zelfstandige Mono-pakket van de SynoCommunity niet meer nodig is, het is momenteel opgenomen in ons pakket.
- Download de release van de applicatie voor de architectuur van uw NAS van [de Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) en [installeer het pakket handmatig](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via het pakketbeheer.

# DSM 7.x

- De Lidarr-Official, Prowlarr-Official, Radarr-Official en Readarr-Official-pakketten zouden *gewoon moeten werken* voor de meeste architecturen.
  - Merk op dat een NAS met `comcerto2k` extra stappen vereist voor Lidarr, Prowlarr, Radarr en Readarr; [zie de instructies](#bubblewrap-installatie-op-dsm-7x).
- Merk op dat het Sonarr-pakket extra stappen vereist voor **alle** architecturen.
- Merk op dat het zelfstandige Mono-pakket van de SynoCommunity niet meer nodig is, het is momenteel opgenomen in ons pakket.

> Voor NAS die draaien op een `comcerto2k` (*alle pakketten*) en Sonarr (*alle NAS-architecturen*), moet u het Bubblewrap-pakket installeren en de handmatige stappen uitvoeren die zijn vermeld. **Bubblewrap moet worden geïnstalleerd voordat u de \*Arr-pakketten probeert te installeren**
{.is-warning}

- Download de release van Bubblewrap voor de architectuur van uw NAS van [de Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) en [installeer het pakket handmatig](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via het pakketbeheer.
- Voltooi de onderstaande stappen voor de Bubblewrap-installatie voor DSM 7.X
- Nadat Bubblewrap is geïnstalleerd, kunt u de release van de applicatie voor de architectuur van uw NAS downloaden van [de Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) en [installeer het pakket handmatig](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via het pakketbeheer.

## Bubblewrap-installatie op DSM 7.X

Bubblewrap stelt ons in staat programma's uit te voeren in een basiscontainer, zodat we nieuwe bibliotheken kunnen gebruiken om .NET6 uit te voeren.

> **Vanwege de beperkingen in DSM 7.0+ is enige handmatige configuratie vereist na de installatie.**
{.is-danger}

### Eenvoudige Bubblewrap-installatie

1. Maak een getriggerde taak aan in DSM:

- Gebruiker: `root`
  - Gebeurtenis: `Opstarten`

1. Voer voor de `Uitvoeringsopdracht` het volgende in:

```bash
chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```

1. Sla de getriggerde taak op en voer deze één keer uit.

![triggered_task.png](/assets/synology/triggered_task.png)

![create_task1.png](/assets/synology/create_task1.png)

![create_task2.png](/assets/synology/create_task2.png)

![run_task.png](/assets/synology/run_task.png)

### Handmatige Bubblewrap-installatie

1. [Log in op uw Synology via SSH en verhoog de rechten naar `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)
1. Voer de volgende opdrachten uit:

```bash
sudo chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
```

```bash
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```