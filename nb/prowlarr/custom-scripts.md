---
title: Prowlarr Egendefinerte Skript
description: 
published: true
date: 2021-12-20T16:40:47.702Z
tags: prowlarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-23T06:40:30.916Z
---

Hvis du ønsker å utløse et egendefinert skript, kan du finne mer informasjon her. Skript legges til i Prowlarr via [Tilkoblingsinnstillinger](/prowlarr/settings#connections).

# Oversikt

Prowlarr kan kjøre et egendefinert skript når en episode er nyimportert eller omdøpt. Avhengig av handlingen, blir forskjellige parametere levert. Parametere sendes til skriptet gjennom miljøvariabler.

## Prowlarr-logger

Merk at følgende kun blir logget for egendefinerte skript:

- Skriptets `stdout`-utdata blir logget som `Debug`
- Skriptets `stderr`-utdata blir logget som `Info`
- Utløseren av skriptet blir logget som `Trace`

# Miljøvariabler

Miljøvariabler varierer avhengig av hendelsestypen. Detaljer kommer snart^tm^

> [Koden som skal gjennomgås finnes her i mellomtiden. Bidrag til wikien er velkomne](https://github.com/Prowlarr/Prowlarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## På Test

Når du legger til skriptet i Prowlarr og klikker på 'Test', vil skriptet bli kalt med følgende parametere. Skriptet bør kunne ignorere eventuelle ikke-støttede hendelsestyper på en hensiktsmessig måte.

| Miljøvariabel       | Detaljer |
| -------------------- | ------- |
| `prowlarr_eventtype` | `Test`  |