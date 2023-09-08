---
title: Sonarr v4 Beta FAQ
description: Sonarr v4 Beta FAQ
published: true
date: 2023-08-28T19:29:38.774Z
tags: 
editor: markdown
dateCreated: 2022-11-25T14:02:10.493Z
---

# Sonarr v4 Beta FAQ

> Sonarr v4 er for øyeblikket i beta, og feil og problemer kan forventes. Vennligst bruk våre støttekanaler for å stille spørsmål, rapportere problemer eller gi tilbakemelding med v4 beta. Hvis nødvendig kan du bli bedt om å åpne en sak på Github, hvis du blir bedt om å åpne en sak på [Github](https://github.com/Sonarr/Sonarr). Vennligst oppgi en lenke til den opprinnelige diskusjonen sammen med all annen forespurt informasjon. {.is-warning}

## Hva har endret seg?

Se [v4 beta-annonseringen](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/) for mer informasjon.

Her er noen av høydepunktene og de mest fremtredende endringene:

- [Tvungen autentisering](#tvungen-autentisering)
- Mono => Dotnet (mer hastighet; ikke mer mono). På grunn av denne endringen er det sannsynligvis nødvendig med oppdateringer av Reverse Proxy-konfigurasjonen:
  - [Nginx](#nginx)
  - [Apache](#apache)
- [Foretrukne ord er borte](#migrering-av-foretrukne-ord-til-tilpassede-formater) og erstattet med Tilpassede formater
- [Språkprofiler er borte](#hvor-har-spr%C3%A5kprofilene-g%C3%A5tt) og erstattet med Tilpassede formater
- Mørkt/lys tema
- SysLog og støtte for instansnavn
- Sammenslåing av Masseredigerer i [Serieoversikt](#hvor-har-masseredigereren-g%C3%A5tt)
- Mye mer

## Tvungen autentisering

Hvis Sonarr er eksponert slik at brukergrensesnittet kan nås utenfor det lokale nettverket ditt, bør du ha en form for autentiseringsmetode aktivert for å få tilgang til brukergrensesnittet. Dette er også i økende grad påkrevd av sporere og indekser.

Fra og med Sonarr v4 er autentisering obligatorisk.

### Autentiseringsmetode

- `Basic` (Nettleser pop-up) - Denne alternativet vil vise en liten pop-up når du får tilgang til Sonarr, som lar deg skrive inn brukernavn og passord.
- `Forms` (Påloggingsside) - Dette alternativet vil ha en kjent påloggingsskjerm, slik som andre nettsteder har, som lar deg logge på Sonarr.
- `Ekstern` - Konfigurerbart via konfigurasjonsfilen bare
  - Hvis du bruker en **ekstern autentisering** som Authelia, Authetik, NGINX Basic auth, osv., kan du unngå å måtte autentisere to ganger ved å avslutte appen, angi `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurasjonsfilen](/sonarr/appdata-directory) og starte appen på nytt. **Merk at flere `AuthenticationMethod`-oppføringer i filen ikke støttes, og bare verdien øverst vil bli brukt**.

### Påkrevd autentisering

- Hvis du ikke eksponerer appen eksternt og/eller ikke ønsker at autentisering skal være påkrevd for lokal (f.eks. LAN) tilgang, kan du endre innstillingene til `Innstillinger => Generell sikkerhet => Påkrevd autentisering` til `Deaktivert for lokale adresser`.
  - Den tilsvarende konfigurasjonsfilen for dette er `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`.

## Migrering av foretrukne ord til tilpassede formater

Foretrukne ord-systemet er erstattet med tilpassede formater-systemet. Dette gir mye mer granularitet i beslutningene Sonarr kan ta. Mens foretrukne ord gjaldt for alle kvalitetsprofiler, kan tilpassede formater få forskjellige vektingsnivåer for hver kvalitetsprofil.

Tilpassede formater kan også få en avkortningsgrense slik at oppgraderinger stopper når en ønsket preferanse er nådd, mens det gamle foretrukne ord-systemet alltid oppgraderte hvis en bedre utgivelse ble funnet.

### Må (ikke) inneholde

Må inneholde og Må ikke inneholde er fortsatt tilgjengelig i innstillingene for utgivelsesprofilen, slik det var i v3.

### Filnavntokens

`{Preferred Words}`-filnavntokenet brukte begrepet som ble matchet i regex-oppføringen for navngivning i filer.
`{Custom Formats}`-filnavntokenet bruker navnet på tilpasset format for navngivning i filer.

> Det anbefales å ta skjermbilde av eller fjerne foretrukne ord-utgivelsesprofilene DITT FØR du oppgraderer. Hver foretrukne ord-linje blir til sitt eget tilpassede format etter migreringen.
{.is-warning}

## Hvor har språkprofilene gått?

Språk håndteres annerledes i Sonarr v4. De administreres ikke lenger via det gamle språkprofil-systemet, men er nå en del av tilpassede formater. Du må opprette tilpassede formater for språk du ønsker å laste ned, og deretter legge til disse tilpassede formatene i kvalitetsprofilene dine med en passende rangering for å tvinge nedlasting av det språket.

> Se TRaSH Guide's [Hvordan sette opp tilpassede språkformater](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/) for mer informasjon.
{.is-info}

### Kun engelsk

**Fra [TRaSH => Språk: Kun engelsk](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-english-only)**

Hvis du bare vil laste ned utgivelser på engelsk, kan du bruke følgende tilpassede format. Importer dette tilpassede formatet, og tildel det deretter til hver av kvalitetsprofilene dine med en poengsum på -10000. Hvis minimum poengsum for tilpassede formater er 0, vil dette avvise alle utgivelser som ikke er analysert som engelsk.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Språk: Kun engelsk",
  "name": "Språk: Ikke engelsk",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Ikke engelsk språk",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 1
      }
    }
  ]
}
```

### Kun originalspråk

**Fra [TRaSH => Språk: Kun originalspråk](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-original-only)**

Hvis du bare vil laste ned utgivelser på seriens TVDb-originalspråk, kan du bruke følgende tilpassede format. Importer dette tilpassede formatet, og tildel det deretter til hver av kvalitetsprofilene dine med en poengsum på -10000. Hvis minimum poengsum for tilpassede formater er 0, vil dette avvise alle utgivelser som ikke er analysert som seriens TVDb-originalspråk.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Språk: Kun originalspråk",
  "name": "Språk: Ikke originalspråk",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Ikke originalspråk",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": -2
      }
    }
  ]
}
```

## Min Reverse Proxy fungerer ikke lenger?

På grunn av endringer i Sonarrs backend (overgang fra mono til dotnet) kan det hende at din ikke lenger fungerer.

### Nginx

Din Nginx-konfigurasjonsfil må endres. Erstatt denne linjen:

```nginx
   proxy_set_header   Host $proxy_host;
```

med denne linjen:

```nginx
  proxy_set_header   Host $host;
```

### Apache

Din Apache virtualhost-konfigurasjonsfil må endres. Legg til denne linjen:

```apache2
  ProxyPreserveHost On
```

## Hva er denne nye "*Overstyr og legg til i nedlastingskøen*" -knappen?

Når du utfører et interaktivt søk, har det blitt lagt til en ekstra nedlastingsknapp med tittelen "Overstyr og legg til i nedlastingskøen". Denne knappen lar deg gjøre to ting:

- Velg hvilken nedlastingsklient nedlastingen skal sendes til. Dette er nyttig hvis du har flere nedlastingsklienter for samme protokoll (f.eks. flere instanser av en torrentklient) i stedet for å la Sonarr bestemme hvilken klient som skal brukes.
- Overstyr Sonarrs analyse av utgivelsestittelen i tilfelle Sonarr har analysert den feil eller Sonarr ikke klarte å analysere den, men du vil fortsatt laste ned utgivelsen. Følgende analyserte felt kan overstyres:
  - Serie
  - Sesongnummer
  - Episode(r)
  - Kvalitet
  - Språk

## Hvor har Masseredigereren gått?

Den frittstående Masseredigerer-siden er fjernet, og funksjonaliteten er slått sammen i serieoversiktssiden. For å masse-redigere serier, klikk først på "Velg serier"-knappen øverst på serieoversikten og velg seriene du vil redigere.

Sesongpass-siden er også fjernet. Noe av funksjonaliteten er fortsatt tilgjengelig i Serieoversikt-redigereren. Velg tabellvisning og trykk på "Velg serier". Når du er i valgmodus, hold musepekeren over tallet i sesongkolonnen for å få tilgang til sesongpass-popoveren for den serien.

## Episoder viser kjøretider på 0

v4 bruker en kjøretid per episode fra TVDb. Hvis kjøretiden for episoden er 0, vil den prøve å falle tilbake til seriens kjøretid.
Hvis seriens kjøretid også er 0, vil Sonarr bruke en kjøretid på 45 for alle episoder som ble sendt innen 24 timer etter den første episoden.