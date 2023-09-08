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

> Sonarr v4 er i øjeblikket i beta, og derfor kan der forventes fejl og problemer. Brug venligst vores supportkanaler til at stille spørgsmål, rapportere problemer eller give feedback med v4 beta. Hvis det er nødvendigt, kan du blive bedt om at åbne en sag på Github, hvis du bliver bedt om at åbne en sag på [Github](https://github.com/Sonarr/Sonarr). Angiv venligst et link til den oprindelige diskussion sammen med al anden anmodet information. {.is-warning}

## Hvad er der ændret?

Se [v4 beta-annonceringen](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/) for mere information.

Her er nogle af højdepunkterne og de mest markante ændringer:

- [Tvungen godkendelse](#tvungen-godkendelse)
- Mono => Dotnet (mere hastighed; ikke mere mono). På grund af denne ændring er det sandsynligt, at der kræves opdateringer af Reverse Proxy-konfigurationen:
  - [Nginx](#nginx)
  - [Apache](#apache)
- [Foretrukne ord er væk](#migrering-af-foretrukne-ord-til-tilpassede-formater) og erstattet med Tilpassede Formater
- [Sprogprofiler er væk](#hvor-er-sprogprofilerne-gået-hen) og erstattet med Tilpassede Formater
- Mørkt/lyst tema
- SysLog og understøttelse af instansnavn
- Sammensmeltning af Masseredigering i [Serieoversigt](#hvor-er-masseredigeringen-gået-hen)
- Meget mere

## Tvungen godkendelse

Hvis Sonarr er udsat, så UI'en kan tilgås udefra dit lokale netværk, bør du have en form for godkendelsesmetode aktiveret for at få adgang til UI'en. Dette kræves også i stigende grad af Trackers og Indexers.

Fra Sonarr v4 er godkendelse obligatorisk.

### Godkendelsesmetode

- `Basic` (Browser pop-up) - Denne mulighed viser en lille pop-up, når du tilgår din Sonarr, der giver dig mulighed for at indtaste et brugernavn og adgangskode.
- `Forms` (Login-side) - Denne mulighed har en velkendt login-skærm, ligesom andre hjemmesider har, der giver dig mulighed for at logge ind på din Sonarr.
- `Ekstern` - Konfigurerbar via konfigurationsfilen kun
  - Hvis du bruger en **ekstern godkendelse** som Authelia, Authetik, NGINX Basic auth osv., kan du undgå at skulle godkendes to gange ved at lukke appen ned, indstille `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurationsfilen](/sonarr/appdata-directory) og genstarte appen. **Bemærk, at flere `AuthenticationMethod`-poster i filen ikke understøttes, og kun den øverste værdi vil blive brugt**

### Påkrævet godkendelse

- Hvis du ikke udsætter appen eksternt og/eller ikke ønsker, at godkendelse er påkrævet for lokal (f.eks. LAN) adgang, skal du ændre i Indstillinger => Generel sikkerhed => Påkrævet godkendelse til `Deaktiveret for lokale adresser`
  - Ækvivalenten i konfigurationsfilen er `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Migrering af foretrukne ord til tilpassede formater

Foretrukne ord-systemet er blevet erstattet med tilpassede formater-systemet. Dette giver mulighed for meget mere granularitet i de beslutninger, Sonarr kan træffe. Hvor foretrukne ord var gældende for alle kvalitetsprofiler, kan tilpassede formater gives forskellige niveauer af vigtighed for hver kvalitetsprofil.

Tilpassede formater kan også gives en cutoff-værdi, så opgraderinger stopper, når et ønsket præference-niveau er nået, hvorimod det gamle foretrukne ord-system altid opgraderede, hvis der blev fundet en bedre udgivelse.

### Skal (ikke) indeholde

Skal indeholde og Må ikke indeholde er stadig til stede i indstillingerne for udgivelsesprofilen, som det var i v3.

### Filnavne-token

Filnavne-tokenet `{Preferred Words}` brugte udtrykket, der blev matchet på regex-indgangen for navngivning i filer.
Filnavne-tokenet `{Custom Formats}` bruger navnet på det tilpassede format til navngivning i filer.

> Det anbefales at tage et screenshot eller fjerne dine foretrukne ord-udgivelsesprofiler FØR opgradering. Hver linje med foretrukne ord bliver til sit eget tilpassede format efter migrationen.
{.is-warning}

## Hvor er sprogprofilerne gået hen?

Sprog håndteres anderledes i Sonarr v4. De administreres ikke længere via det gamle sprogprofilsystem, men er nu en del af Tilpassede Formater. Du skal oprette tilpassede formater for de sprog, du ønsker at hente, og derefter tilføje disse tilpassede formater til dine kvalitetsprofiler med en passende vurdering for at sikre, at sproget hentes.

> Se TRaSH Guides [Sådan opsættes tilpassede sprogformater](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/) for mere information
{.is-info}

### Kun engelsk

**Fra [TRaSH => Sprog: Kun engelsk](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-english-only)**

Hvis du kun vil hente udgivelser på engelsk, kan du bruge følgende tilpassede format. Importer dette tilpassede format og tildel det derefter til hver af dine kvalitetsprofiler med en score på -10000. Hvis din minimumscore for tilpassede formater er 0, vil dette afvise alle udgivelser, der ikke er analyseret som engelsk.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Sprog: Kun engelsk",
  "name": "Sprog: Ikke engelsk",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Ikke engelsk sprog",
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

### Kun original

**Fra [TRaSH => Sprog: Kun original](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-original-only)**

Hvis du kun vil hente udgivelser på seriens TVDb-originale sprog, kan du bruge følgende tilpassede format. Importer dette tilpassede format og tildel det derefter til hver af dine kvalitetsprofiler med en score på -10000. Hvis din minimumscore for tilpassede formater er 0, vil dette afvise alle udgivelser, der ikke er analyseret som seriens TVDb-originale sprog.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Sprog: Kun original",
  "name": "Sprog: Ikke original",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Ikke originalt sprog",
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

## Min Reverse Proxy virker ikke længere?

På grund af ændringer i backenden af Sonarr (migrering fra mono til donnet) fungerer din måske ikke længere.

### Nginx

Din Nginx-konfigurationsfil skal ændres. Erstat denne linje:

```nginx
   proxy_set_header   Host $proxy_host;
```

med denne linje:

```nginx
  proxy_set_header   Host $host;
```

### Apache

Din Apache-virtualhost-konfigurationsfil skal ændres. Tilføj denne linje:

```apache2
  ProxyPreserveHost On
```

## Hvad er denne nye "*Override and add to download queue*" knap?

Når du foretager en interaktiv søgning, er der blevet tilføjet en anden downloadknap med titlen "Override and add to download queue". Denne knap giver dig mulighed for at gøre to ting:

- Vælg hvilken downloadklient, downloaden skal sendes til. Dette er nyttigt, hvis du har flere downloadklienter til samme protokol (f.eks. flere instanser af en torrentklient) i stedet for at lade Sonarr beslutte, hvilken klient der skal bruges.
- Overskriv Sonarrs analyse af udgivelsens titel, hvis Sonarr har analyseret den forkert, eller Sonarr ikke kunne analysere den, men du stadig ønsker at hente udgivelsen. Følgende analyserede felter kan overskrives:
  - Serie
  - Sæsonnummer
  - Episode(r)
  - Kvalitet
  - Sprog

## Hvor er Masseredigeringen gået hen?

Masseredigerings-siden er blevet fjernet, og funktionaliteten er blevet fusioneret ind i serieoversigt-siden. For at masse-redigere shows skal du først klikke på knappen "Vælg serie" øverst på serieoversigten og vælge de shows, du vil redigere.

Sæsonpas-siden er også blevet fjernet. En del af funktionaliteten er stadig til stede i Serieoversigt-redigeringsværktøjet. Vælg tabelvisning og tryk på "Vælg serie". Når du er i valgtilstand, skal du holde musen over tallet i sæsonkolonnen for at få adgang til sæsonpas-popoveren for den serie.

## Episoder viser køretider på 0

v4 bruger en køretid pr. episode fra TVDb. Hvis køretiden for episoden er 0, vil den forsøge at falde tilbage til seriens køretid.
Hvis seriens køretid også er 0, vil Sonarr bruge en køretid på 45 for enhver episode, der blev sendt inden for 24 timer efter den første episode.