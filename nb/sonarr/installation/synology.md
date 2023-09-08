---
title: Sonarr Synology-installasjon
description: Installasjonsveiledning for Sonarr på Synology
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Synology

- [SynoCommunity oppretter, støtter og vedlikeholder en Synology NAS-pakke](https://synocommunity.com/package/nzbdrone)

> NAS-pakken er dårlig vedlikeholdt og er ofte utdatert. Hvis NAS-en din støtter Docker, anbefales det sterkt å [kjøre Docker](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) i stedet. Du vil ikke kunne reinstallere Sonarr uten å manuelt slette databasen din på grunn av at NAS-pakken er utdatert og ikke er konfigurert til å oppdatere seg selv ved oppstart. {.is-info}

- [SynoCommunity oppretter, støtter og vedlikeholder også den nødvendige Mono-pakken](https://synocommunity.com/package/mono)

## Synology Mono SSL-feil

> På grunn av en feil som er introdusert av SynoCommunity sin dårlig vedlikeholdte Mono-pakke, vil Sonarr ikke kunne koble til etter at Mono er oppdatert eller etter en fersk installasjon. Dette kan løses ved å følge instruksjonene på [SynoCommunity Bug Report #5051](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1009758625). Merk at basert på [denne kommentaren](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1153245799) har DSM7-brukere et ekstra trinn.
{.is-danger}

1. Inne i DSM, aktiver SSH-tjenesten i *Kontrollpanel => Terminal og SNMP* og klikk på "Apply"
1. Bruk [Terminal](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) (MacOS) for å koble til NAS-en ved å bruke `ssh -l [admin-brukernavn] [NAS-adresse]`, eller bruk [Putty](https://www.putty.org/) (Windows) for å koble til nettverksadressen til NAS-en din
1. Skriv inn den nødvendige admin-passordet og trykk "Enter"
1. Skriv inn den passende kommandoen(e) for din DSM-versjon som er nevnt nedenfor, og trykk "Enter"
1. Skriv inn den nødvendige admin-passordet og trykk "Enter". Når prosessen er fullført, skal du se linjen *Import process completed*
1. Avslutt SSH-økten ved å skrive `exit` og trykk "Enter"
1. Inne i DSM, deaktiver SSH-tjenesten i *Kontrollpanel => Terminal og SNMP* og klikk på "Apply"
1. Når prosessen er fullført, skal feilene i Sonarr forsvinne av seg selv i løpet av noen minutter.

### Kommando for å fikse Synology DSM6 Mono

```shell
sudo /var/packages/mono/target/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
```

### Kommando for å fikse Synology DSM7 Mono

```shell
sudo /volume1/@appstore/mono/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
sudo chmod -R a+rX /usr/share/.mono
```