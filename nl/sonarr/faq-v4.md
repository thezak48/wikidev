---
title: Sonarr v4 Beta FAQ
description: Sonarr v4 Beta FAQ
published: true
date: 2023-08-28T19:29:38.774Z
tags: 
editor: markdown
dateCreated: 2022-11-25T14:02:10.493Z
---

# Veelgestelde vragen over Sonarr v4 Beta

> Sonarr v4 is momenteel in bèta en daarom kunnen fouten en problemen worden verwacht. Gebruik onze ondersteuningskanalen om vragen te stellen, problemen te melden of feedback te geven over de v4-bèta. Indien nodig kan u worden gevraagd om een probleem te openen op Github, als u wordt gevraagd om een probleem te openen op [Github](https://github.com/Sonarr/Sonarr). Geef een link naar de oorspronkelijke discussie en alle andere gevraagde informatie. {.is-warning}

## Wat is er veranderd?

Raadpleeg de [v4 bèta-aankondiging](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/) voor meer informatie.

Hieronder volgen enkele hoogtepunten en opvallende veranderingen:

- [Gedwongen authenticatie](#gedwongen-authenticatie)
- Mono => Dotnet (meer snelheid; geen mono meer). Vanwege deze wijziging zijn waarschijnlijk updates van de omgekeerde proxyconfiguratie vereist:
  - [Nginx](#nginx)
  - [Apache](#apache)
- [Voorkeurswoorden zijn verdwenen](#migratie-van-voorkeurswoorden-naar-aangepaste-indelingen) en vervangen door aangepaste indelingen
- [Taalprofielen zijn verdwenen](#waar-zijn-de-taalprofielen-gebleven) en vervangen door aangepaste indelingen
- Donker/licht thema
- SysLog en ondersteuning voor instantienaam
- Samenvoeging van Massa-editor in [Serieoverzicht](#waar-is-de-massa-editor-gebleven)
- En nog veel meer

## Gedwongen authenticatie

Als Sonarr zo is ingesteld dat de gebruikersinterface van buiten uw lokale netwerk toegankelijk is, moet u een vorm van authenticatiemethode hebben ingeschakeld om toegang te krijgen tot de gebruikersinterface. Dit is ook steeds vaker vereist door Trackers en Indexers.

Vanaf Sonarr v4 is authenticatie verplicht.

### Authenticatiemethode

- `Basis` (Browser pop-up) - Deze optie toont bij het openen van Sonarr een klein pop-upvenster waarin u een gebruikersnaam en wachtwoord kunt invoeren.
- `Formulieren` (Aanmeldingspagina) - Deze optie heeft een vertrouwd uitziend aanmeldingsscherm, vergelijkbaar met andere websites, waarmee u kunt inloggen op Sonarr.
- `Extern` - Configuratie alleen mogelijk via configuratiebestand
  - Als u een **externe authenticatie** zoals Authelia, Authetik, NGINX Basic auth, enz. gebruikt, kunt u voorkomen dat u dubbel moet authenticeren door de app af te sluiten, `<AuthenticationMethod>External</AuthenticationMethod>` in het [configuratiebestand](/sonarr/appdata-directory) in te stellen en de app opnieuw te starten. **Let op dat meerdere `AuthenticationMethod`-vermeldingen in het bestand niet worden ondersteund en alleen de bovenste waarde wordt gebruikt.**

### Verplichte authenticatie

- Als u de app niet extern blootstelt en/of geen authenticatie vereist voor lokale (bijv. LAN) toegang, wijzig dan in Instellingen => Algemene beveiliging => Verplichte authenticatie naar `Uitgeschakeld voor lokale adressen`
  - Het equivalent van deze instelling in het configuratiebestand is `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Migratie van voorkeurswoorden naar aangepaste indelingen

Het systeem van voorkeurswoorden is vervangen door het systeem van aangepaste indelingen. Dit biedt veel meer precisie in de beslissingen die Sonarr kan nemen. Terwijl voorkeurswoorden van toepassing waren op alle kwaliteitsprofielen, kunnen aangepaste indelingen verschillende niveaus van belangrijkheid krijgen voor elk kwaliteitsprofiel.

Aangepaste indelingen kunnen ook een afkappunt krijgen, zodat upgrades stoppen zodra een gewenst niveau van voorkeur is bereikt, terwijl het oude systeem van voorkeurswoorden altijd een upgrade uitvoerde als er een betere release werd gevonden.

### Moet (niet) bevatten

Moet bevatten en Mag niet bevatten blijven aanwezig in de instellingen van het releaseprofiel, zoals in v3.

### Bestandsnaamtokens

Het `{Voorkeurswoorden}`-naamtoken gebruikte de term die overeenkwam met de regex-invoer voor de naamgeving in bestanden.
Het `{Aangepaste indelingen}`-naamtoken gebruikt de naam van de aangepaste indeling voor de naamgeving in bestanden.

> Het wordt aanbevolen om uw releaseprofielen voor Voorkeurswoorden te screenshoten of te verwijderen VOORDAT u een upgrade uitvoert. Elke regel voor Voorkeurswoorden wordt na de migratie een eigen aangepaste indeling.
{.is-warning}

## Waar zijn de taalprofielen gebleven?

Talen worden in Sonarr v4 anders behandeld. Ze worden niet langer beheerd via het oude systeem van taalprofielen, maar maken nu deel uit van aangepaste indelingen. U moet aangepaste indelingen maken voor talen die u wilt downloaden en deze aangepaste indelingen vervolgens toevoegen aan uw kwaliteitsprofielen met een geschikte beoordeling om het downloaden van die taal af te dwingen.

> Zie de [TRaSH Guide's How to setup Language Custom Formats](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/) voor meer informatie.
{.is-info}

### Alleen Engels

**Van [TRaSH => Taal: Alleen Engels](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-english-only)**

Als u alleen releases in het Engels wilt downloaden, kunt u de volgende aangepaste indeling gebruiken. Importeer deze aangepaste indeling en wijs deze vervolgens toe aan elk van uw kwaliteitsprofielen met een score van -10000. Als uw minimale score voor aangepaste indeling 0 is, worden alle releases die niet als Engels zijn geanalyseerd, afgewezen.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Taal: Alleen Engels",
  "name": "Taal: Niet Engels",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Niet-Engelse taal",
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

### Alleen origineel

**Van [TRaSH => Taal: Alleen origineel](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-original-only)**

Als u alleen releases in de oorspronkelijke taal van de serie wilt downloaden, kunt u de volgende aangepaste indeling gebruiken. Importeer deze aangepaste indeling en wijs deze vervolgens toe aan elk van uw kwaliteitsprofielen met een score van -10000. Als uw minimale score voor aangepaste indeling 0 is, worden alle releases die niet als de oorspronkelijke taal van de serie zijn geanalyseerd, afgewezen.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Taal: Alleen origineel",
  "name": "Taal: Niet origineel",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Niet-originele taal",
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

## Mijn omgekeerde proxy werkt niet meer?

Vanwege wijzigingen in de backend van Sonarr (migratie van mono naar dotnet) werkt uw omgekeerde proxy mogelijk niet meer.

### Nginx

Uw Nginx-configuratiebestand moet worden gewijzigd. Vervang deze regel:

```nginx
   proxy_set_header   Host $proxy_host;
```

door deze regel:

```nginx
  proxy_set_header   Host $host;
```

### Apache

Uw Apache-virtualhost-configuratiebestand moet worden gewijzigd. Voeg deze regel toe:

```apache2
  ProxyPreserveHost On
```

## Wat is deze nieuwe knop "*Override and add to download queue*" (Overschrijven en toevoegen aan downloadwachtrij)?

Bij het uitvoeren van een interactieve zoekopdracht is er een tweede downloadknop toegevoegd met de titel "Override and add to download queue" (Overschrijven en toevoegen aan downloadwachtrij). Met deze knop kunt u twee dingen doen:

- Kiezen naar welke downloadclient de download wordt verzonden. Dit is handig in het geval dat u meerdere downloadclients heeft voor hetzelfde protocol (bijv. meerdere instanties van een torrentclient) in plaats van Sonarr te laten beslissen welke client moet worden gebruikt.
- De analyse van de titel van de release door Sonarr overschrijven in het geval dat Sonarr deze verkeerd heeft geanalyseerd of dat Sonarr deze niet kon analyseren, maar u de release toch wilt downloaden. De volgende geanalyseerde velden kunnen worden overschreven:
  - Serie
  - Seizoennummer
  - Aflevering(en)
  - Kwaliteit
  - Taal

## Waar is de Massa-editor gebleven?

De zelfstandige pagina van de Massa-editor is verwijderd en de functionaliteit is samengevoegd in de serieoverzichtspagina. Om shows massaal te bewerken, klikt u eerst op de knop `Select Series` (Series selecteren) bovenaan het serieoverzicht en selecteert u de shows die u wilt bewerken.

De pagina Seizoenspas is ook verwijderd. Een deel van de functionaliteit blijft beschikbaar in de Serieoverzicht-editor. Kies de tabelweergave en druk op `Select Series` (Series selecteren). Als u eenmaal in de selectiemodus bent, beweegt u de muis over het nummer in de kolom Seizoenen om het popovermenu voor de seizoenspas voor die show te openen.

## Afleveringen tonen een looptijd van 0

In v4 wordt de looptijd per aflevering van TVDb gebruikt. Als de looptijd voor de aflevering 0 is, zal Sonarr proberen terug te vallen op de looptijd van de serie.
Als de looptijd van de serie ook 0 is, zal Sonarr een looptijd van 45 gebruiken voor elke aflevering die binnen 24 uur na de eerste aflevering is uitgezonden.