---
title: Prowlarr Brugerdefinerede Scripts
description: 
published: true
date: 2021-12-20T16:40:47.702Z
tags: prowlarr, needs-love, brugerdefinerede scripts
editor: markdown
dateCreated: 2021-06-23T06:40:30.916Z
---

Hvis du vil udløse et brugerdefineret script, kan du finde flere detaljer her. Scripts tilføjes til Prowlarr via [Forbindelsesindstillingerne](/prowlarr/settings#connections).

# Oversigt

Prowlarr kan udføre et brugerdefineret script, når en episode er nyimporteret eller omdøbt. Afhængigt af handlingen leveres forskellige parametre. Parametrene sendes til scriptet gennem miljøvariabler.

## Prowlarr-logs

Bemærk, at følgende kun bliver logget for brugerdefinerede scripts:

- Scriptets `stdout`-output logges som `Debug`
- Scriptets `stderr`-output logges som `Info`
- Udløseren af scriptet logges som `Trace`

# Miljøvariabler

Miljøvariabler varierer afhængigt af begivenhedstypen. Flere detaljer kommer snart^tm^

> [Koden, der skal gennemses, findes her i mellemtiden. Bidrag til wikien er velkomne](https://github.com/Prowlarr/Prowlarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Ved test

Når du tilføjer scriptet til Prowlarr og klikker på 'Test', vil scriptet blive kaldt med følgende parametre. Scriptet bør kunne ignorere eventuelle ikke-understøttede begivenhedstyper på en hensigtsmæssig måde.

| Miljøvariabel        | Detaljer |
| -------------------- | ------- |
| `prowlarr_eventtype` | `Test`  |