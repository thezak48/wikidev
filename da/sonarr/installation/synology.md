---
title: Sonarr Synology Installation
description: Installationsguide til Sonarr på Synology
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Synology

- [SynoCommunity opretter, supporterer og vedligeholder en Synology NAS-pakke](https://synocommunity.com/package/nzbdrone)

> NAS-pakken er dårligt vedligeholdt og ofte forældet. Hvis din NAS understøtter Docker, anbefales det stærkt [at køre Docker](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) i stedet. Du vil ikke kunne geninstallere Sonarr uden at slette din database manuelt, da NAS-pakken er forældet og ikke er konfigureret til at opdatere sig selv ved opstart. {.is-info}

- [SynoCommunity opretter også, supporterer og vedligeholder den nødvendige Mono-pakke](https://synocommunity.com/package/mono)

## Synology Mono SSL-fejl

> På grund af en fejl introduceret af SynoCommunity's dårligt vedligeholdte Mono-pakke, vil Sonarr ikke kunne oprette forbindelse efter opdatering af Mono eller efter en frisk installation. Dette kan løses ved at følge instruktionerne på [SynoCommunity Bug Report #5051](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1009758625). Bemærk, at baseret på [denne kommentar](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1153245799) har DSM7-brugere et ekstra trin.
{.is-danger}

1. Inden for DSM skal du aktivere SSH-tjenesten i *Kontrolpanel => Terminal & SNMP* og klikke på "Anvend".
1. Brug [Terminal](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) (MacOS) til at oprette forbindelse til NAS'en ved hjælp af `ssh -l [admin-brugernavn] [NAS-adresse]` eller brug [Putty](https://www.putty.org/) (Windows) til at oprette forbindelse til netværksadressen for din NAS.
1. Indtast den påkrævede administratoradgangskode og tryk på Enter.
1. Indtast den relevante kommando(er) for din DSM-version, som er angivet nedenfor, og tryk på Enter.
1. Indtast den påkrævede administratoradgangskode og tryk på Enter. Når processen er fuldført, skal du se linjen "*Import process completed*".
1. Afslut SSH-sessionen ved at skrive `exit` og trykke på Enter.
1. Inden for DSM skal du deaktivere SSH-tjenesten i *Kontrolpanel => Terminal & SNMP* og klikke på "Anvend".
1. Når processen er fuldført, bør fejlene i Sonarr forsvinde af sig selv inden for et par minutter.

### Kommando til Synology DSM6 Mono-fix

```shell
sudo /var/packages/mono/target/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
```

### Kommando til Synology DSM7 Mono-fix

```shell
sudo /volume1/@appstore/mono/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
sudo chmod -R a+rX /usr/share/.mono
```