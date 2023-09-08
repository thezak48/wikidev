---
title: Synology-pakker
description: Servarr Synology-pakker
published: true
date: 2022-06-23T19:58:34.255Z
tags: lidarr, prowlarr, synology, radarr,readarr,sonarr
editor: markdown
dateCreated: 2022-05-06T13:45:19.731Z
---

- [Servarr Synology-pakker](#servarr-synology-pakker)
- [DSM 6.x](#dsm-6x)
- [DSM 7.x](#dsm-7x)
  - [Bubblewrap-installasjon på DSM 7.X](#bubblewrap-installasjon-på-dsm-7x)
    - [Enkel Bubblewrap-installasjon](#enkel-bubblewrap-installasjon)
    - [Manuell Bubblewrap-installasjon](#manuell-bubblewrap-installasjon)

# Servarr Synology-pakker

> Disse pakkene kan betraktes som "beta"
{.is-danger}

- Servarr-teamet oppretter og vedlikeholder nå Synology-pakkene
- Installasjonsinstruksjoner er angitt nedenfor for de spesifikke DSM-versjonene

> Generelt sett er de eksisterende SynoCommunity-versjonene ikke kompatible med Servarr-versjonene uten noen ekstra trinn. Dette betyr at det vil være nødvendig å slette den gamle pakken etter å ha tatt en [sikkerhetskopi av databasen din *lenken er for et Radarr-eksempel, men instruksjonene/konseptene er de samme*](/radarr/faq#how-do-i-backuprestore-radarr). Dette kan gjøres via nettgrensesnittet til \*Arr-appen.
{.is-warning}

> SynoCommunity har en liste over [NAS etter arkitektur](https://github.com/SynoCommunity/spksrc/wiki/Architecture-per-Synology-model) som vil hjelpe deg med å identifisere riktig pakke.
{.is-info}

# DSM 6.x

- Lidarr-Official, Prowlarr-Official, Radarr-Official, Readarr-Official og Sonarr-pakkene skal *bare fungere*.
- Merk at den frittstående Mono-pakken fra SynoCommunity ikke lenger er nødvendig, den er for øyeblikket inkludert i vår pakke.
- Last ned utgivelsen av applikasjonen for NAS-ens arkitektur fra [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) og [installer pakken manuelt](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via pakkehåndtereren.

# DSM 7.x

- Lidarr-Official, Prowlarr-Official, Radarr-Official og Readarr-Official-pakkene skal *bare fungere* for de fleste arkitekturer.
  - Merk at en NAS med `comcerto2k` krever ekstra trinn for Lidarr, Prowlarr, Radarr og Readarr; [se instruksjonene](#bubblewrap-installasjon-på-dsm-7x).
- Merk at Sonarr-pakken krever ekstra trinn for **alle** arkitekturer.
- Merk at den frittstående Mono-pakken fra SynoCommunity ikke lenger er nødvendig, den er for øyeblikket inkludert i vår pakke.

> For NAS som kjører på `comcerto2k` (*alle pakker*) og Sonarr (*alle NAS-arkitekturer*), må du installere Bubblewrap-pakken og utføre de manuelle trinnene som er angitt. **Bubblewrap må installeres før du prøver å installere \*Arr-pakkene**
{.is-warning}

- Last ned utgivelsen av Bubblewrap for NAS-ens arkitektur fra [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) og [installer pakken manuelt](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via pakkehåndtereren.
- Fullfør følgende Bubblewrap-installasjonstrinn for DSM 7.X
- Når Bubblewrap er installert, kan du laste ned utgivelsen av applikasjonen for NAS-ens arkitektur fra [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases) og [installer pakken manuelt](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via pakkehåndtereren.

## Bubblewrap-installasjon på DSM 7.X

Bubblewrap lar oss kjøre programmer i en grunnleggende beholder slik at vi kan bruke nye nok biblioteker til å kjøre .NET6.

> **På grunn av begrensningene i DSM 7.0+ kreves det noen manuelle oppsett etter installasjonen.**
{.is-danger}

### Enkel Bubblewrap-installasjon

1. Opprett en utløst oppgave i DSM:

- Bruker: `root`
  - Hendelse: `Oppstart`

1. Skriv inn følgende kommando i `Kjør kommando`:

```bash
chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```

1. Lagre den utløste oppgaven og kjør den én gang.

![triggered_task.png](/assets/synology/triggered_task.png)

![create_task1.png](/assets/synology/create_task1.png)

![create_task2.png](/assets/synology/create_task2.png)

![run_task.png](/assets/synology/run_task.png)

### Manuell Bubblewrap-installasjon

1. [Logg inn på Synology via SSH og få forhøyet tilgang til `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)
1. Utfør følgende kommandoer:

```bash
sudo chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
```

```bash
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```