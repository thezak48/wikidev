---
title: Radarr Activiteit
description: 
published: true
date: 2022-02-06T09:07:15.520Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:28:36.350Z
---

# Activiteit

Het tabblad Activiteit is waar je de activiteiten van \*Arr kunt zien, zowel huidige als vroegere activiteiten. Dit omvat importeren, verwijderen, upgraden, grijpen, hernoemen en mislukkingen.

# Wachtrij

Wanneer iets actief wordt gedownload en nog niet geïmporteerd in \*Arr, wordt dit weergegeven op de pagina Wachtrij.

De wachtrij toont alle items die de applicatie kan herkennen en die zich bevinden in de categorie van de opgegeven downloadclient (Instellingen => Downloadclient => Categorie). Om alle releases te bekijken, ga naar Opties => Onbekende weergeven. De wachtrij wordt niet opgeslagen binnen de applicatie, maar wordt bijgewerkt via de API-respons van je downloadclient.

> Voor Usenet-clients zal \*Arr slechts 60 items diep in de wachtrij kijken voor potentiële imports! Het is belangrijk om dit niet te overschrijden, anders moet je handmatig imports opruimen wanneer je systeem overbelast raakt en items mist!.
> Verwijder voltooide downloads moet ook ingeschakeld zijn voor je downloadclient. {.is-warning}

## Pictogrammen voor wachtrijacties

- X - Item uit de wachtrij verwijderen
  - Release verwijderen uit downloadclient - Release verwijderen uit downloadclient. Verplicht voor niet-overeenkomende release-items
  - Release toevoegen aan blokkeerlijst - Release toevoegen aan blokkeerlijst
- Pictogram van een persoon - Handmatige import van release
- Pictogram van een hand - Release naar downloadclient sturen

## Wachtrijstatussen

> Let op: het onderstaande is onvolledig {.is-warning}

| Pictogram      | Status                   | Beschrijving                                                                                   | Oplossingsstappen                                         |
| -------------- | ------------------------ | --------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| Grijze klok    | Release in afwachting    | Download wacht op beschikbaarheid van de downloadclient of op het voldoen aan de vertraging van het profiel | N.v.t.                                                   |
| Geel           | Waarschuwing: kan niet importeren | \*Arr kon de release niet importeren. Bekijk de tooltip voor meer details                     | [Zie de Probleemoplossingsgids](/radarr/troubleshooting) |
| Paars          | Download wordt geïmporteerd | Download wordt geïmporteerd                                                                   | N.v.t.                                                   |
|                |                          |                                                                                               |                                                          |
|                |                          |                                                                                               |                                                          |

# Geschiedenis

Het tabblad Geschiedenis toont alles wat de wachtrij heeft verlaten doordat de taak is voltooid/beëindigd. Dit omvat imports, mislukkingen, grijpen, verwijderingen en upgrades.

Het linkericoon is de actie die is uitgevoerd (de lijst met mogelijke acties wordt hieronder weergegeven). Je kunt deze filteren door op het filterpictogram aan de rechterkant te klikken. Je kunt ook meer kolommen weergeven door op Opties te klikken.

![history2.png](/assets/radarr/history2.png)

Bij 'Grijpen'-statussen kun je op het informatiepictogram aan de rechterkant klikken om meer details over de download te zien (van welke indexer deze afkomstig is, de URL van de download, de leeftijd van de upload, enz.). Je kunt dit item ook markeren als mislukt om verwijdering, blokkering en opnieuw zoeken van het item te starten.

![history4.png](/assets/radarr/history4.png)

# Blokkeerlijst

> De blokkeerlijst stond voorheen bekend als 'Blacklist' {.is-info}

De blokkeerlijstpagina toont items die zijn geblokkeerd, zodat ze niet opnieuw worden gedownload. Dit zijn mislukkingen uit het automatische proces of handmatig gemarkeerde mislukte items. Items blijven voor altijd op de blokkeerlijst staan, tenzij je ze handmatig verwijdert.

![blocklist1.png](/assets/radarr/blocklist1.png)

Door op het informatiepictogram aan de uiterst rechterkant te klikken, kun je meer details over de geblokkeerde invoer zien en of deze handmatig als mislukt is gemarkeerd of automatisch is mislukt tijdens het downloaden.

![blocklist2.png](/assets/radarr/blocklist2.png)

Door op de 'x' aan de uiterst rechterkant te klikken, verwijder je het item uit de blokkeerlijst, zodat je het eventueel opnieuw kunt grijpen als het per ongeluk is toegevoegd.

## Veelvoorkomende redenen voor blokkering

- Gebruiker heeft download handmatig als mislukt gemarkeerd
- Gebruiker heeft "Toevoegen aan blokkeerlijst" geselecteerd bij het verwijderen uit de wachtrij
- Usenet-downloadclient heeft gemeld dat de release niet kon worden gedownload