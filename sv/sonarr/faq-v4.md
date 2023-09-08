---
title: Sonarr v4 Beta FAQ
description: Vanliga frågor om Sonarr v4 Beta
published: true
date: 2023-08-28T19:29:38.774Z
tags: 
editor: markdown
dateCreated: 2022-11-25T14:02:10.493Z
---

# Vanliga frågor om Sonarr v4 Beta

> Sonarr v4 är för närvarande i beta och som sådan kan fel och problem förväntas. Använd våra supportkanaler för att ställa frågor, rapportera problem eller ge feedback om v4-beta. Om det behövs kan du bli ombedd att öppna ett ärende på Github, om du ombeds att öppna ett ärende på [Github](https://github.com/Sonarr/Sonarr). Vänligen ange en länk till den ursprungliga diskussionen tillsammans med all annan begärd information. {.is-warning}

## Vad har ändrats?

Se [v4 beta-annonseringen](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/) för mer information.

Här är några av höjdpunkterna och de mest framträdande förändringarna:

- [Tvingad autentisering](#tvingad-autentisering)
- Mono => Dotnet (snabbare; inget mer mono). På grund av denna ändring kan det vara nödvändigt att uppdatera Reverse Proxy-konfigurationen:
  - [Nginx](#nginx)
  - [Apache](#apache)
- [Föredragna ord är borta](#migration-av-föredragna-ord-till-anpassade-format) och ersatta med Anpassade format
- [Språkprofiler är borta](#vart-har-språkprofilerna-tagit-vägen) och ersatta med Anpassade format
- Mörkt/ljust tema
- SysLog och stöd för instansnamn
- Sammanslagning av Massredigeraren i [Serieöversikt](#vart-har-massredigeraren-tagit-vägen)
- Mycket mer

## Tvingad autentisering

Om Sonarr är exponerad så att användargränssnittet kan nås utanför ditt lokala nätverk bör du ha någon form av autentiseringsmetod aktiverad för att komma åt användargränssnittet. Detta krävs också alltmer av spårare och indexerare.

Från och med Sonarr v4 är autentisering obligatorisk.

### Autentiseringsmetod

- `Basic` (Webbläsarpopup) - Den här inställningen visar en liten popup när du går till Sonarr där du kan ange användarnamn och lösenord.
- `Forms` (Inloggningssida) - Den här inställningen visar en inloggningssida som liknar andra webbplatser där du kan logga in på Sonarr.
- `External` - Konfigurerbar endast via konfigurationsfilen
  - Om du använder **extern autentisering** som Authelia, Authetik, NGINX Basic auth, etc. kan du undvika att behöva autentisera två gånger genom att stänga av appen, ange `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurationsfilen](/sonarr/appdata-directory) och starta om appen. **Observera att flera `AuthenticationMethod`-poster i filen inte stöds och endast det översta värdet används**

### Obligatorisk autentisering

- Om du inte exponerar appen externt och/eller inte vill ha autentisering som krävs för lokal (t.ex. LAN) åtkomst kan du ändra inställningen i Inställningar => Allmänt => Obligatorisk autentisering till `Inaktiverad för lokala adresser`
  - Detta motsvaras i konfigurationsfilen av `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Migration av föredragna ord till anpassade format

Systemet med föredragna ord har ersatts med systemet för anpassade format. Detta ger mycket mer granularitet i de beslut som Sonarr kan fatta. Medan föredragna ord gällde för alla kvalitetsprofiler kan anpassade format ges olika vikt för varje kvalitetsprofil.

Anpassade format kan också ges en avskärningsnivå så att uppgraderingar slutar hända när en önskad nivå av preferens har uppnåtts, medan det gamla systemet med föredragna ord alltid uppgraderade om en bättre version hittades.

### Måste (inte) innehålla

Måste innehålla och Får inte innehålla finns kvar i inställningarna för utgivningsprofilen som i v3.

### Tokens för filnamn

Tokenet `{Preferred Words}` använde termen som matchades i regex-posten för namngivning i filer.
Tokenet `{Custom Formats}` använder namnet på det anpassade formatet för namngivning i filer.

> Det rekommenderas att du tar en skärmdump eller tar bort dina föredragna ord-utgivningsprofiler INNAN du uppgraderar. Varje rad med föredragna ord blir ett eget anpassat format efter migrationen.
{.is-warning}

## Vart har språkprofilerna tagit vägen?

Språk hanteras på ett annat sätt i Sonarr v4. De hanteras inte längre via det gamla systemet med språkprofiler, utan ingår nu i Anpassade format. Du måste skapa anpassade format för de språk du vill hämta och sedan lägga till dessa anpassade format i dina kvalitetsprofiler med en lämplig betyg för att tvinga hämtning av det språket.

> Se TRaSH Guides [Guide för att ställa in anpassade språkformat](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/) för mer information.
{.is-info}

### Endast engelska

**Från [TRaSH => Språk: Endast engelska](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-english-only)**

Om du bara vill hämta utgåvor på engelska kan du använda följande anpassade format. Importera detta anpassade format och tilldela det sedan till var och en av dina kvalitetsprofiler med ett poängvärde på -10000. Om det lägsta poängvärdet för anpassade format är 0 kommer detta att avvisa alla utgåvor som inte tolkas som engelska.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Språk: Endast engelska",
  "name": "Språk: Inte engelska",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Inte engelska språk",
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

### Endast originalspråk

**Från [TRaSH => Språk: Endast originalspråk](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-original-only)**

Om du bara vill hämta utgåvor på seriens ursprungliga språk enligt TVDb kan du använda följande anpassade format. Importera detta anpassade format och tilldela det sedan till var och en av dina kvalitetsprofiler med ett poängvärde på -10000. Om det lägsta poängvärdet för anpassade format är 0 kommer detta att avvisa alla utgåvor som inte tolkas som seriens ursprungliga språk enligt TVDb.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Språk: Endast originalspråk",
  "name": "Språk: Inte originalspråk",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Inte originalspråk",
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

## Min reverse proxy fungerar inte längre?

På grund av ändringar i Sonarrs backend (migration från mono till dotnet) kan din reverse proxy sluta fungera.

### Nginx

Din Nginx-konfigurationsfil behöver ändras. Ersätt den här raden:

```nginx
   proxy_set_header   Host $proxy_host;
```

med den här raden:

```nginx
  proxy_set_header   Host $host;
```

### Apache

Din Apache-virtualhost-konfigurationsfil behöver ändras. Lägg till den här raden:

```apache2
  ProxyPreserveHost On
```

## Vad är den nya knappen "*Override and add to download queue*" (Åsidosätt och lägg till i nedladdningskön)?

Vid en interaktiv sökning har en andra nedladdningsknapp lagts till med titeln "Åsidosätt och lägg till i nedladdningskön". Denna knapp gör det möjligt att göra två saker:

- Välj vilken nedladdningsklient nedladdningen ska skickas till. Detta är användbart om du har flera nedladdningsklienter för samma protokoll (t.ex. flera instanser av en torrentklient) istället för att låta Sonarr bestämma vilken klient som ska användas.
- Åsidosätt Sonarrs tolkning av utgåvans titel om Sonarr har tolkat den felaktigt eller om Sonarr inte kunde tolka den, men du vill ändå hämta utgåvan. Följande tolkade fält kan åsidosättas:
  - Serie
  - Säsongnummer
  - Avsnitt
  - Kvalitet
  - Språk

## Vart har massredigeraren tagit vägen?

Den fristående sidan för massredigering har tagits bort och funktionaliteten har integrerats i serieöversiktssidan. För att massredigera serier klickar du först på knappen "Välj serier" längst upp på serieöversikten och väljer de serier du vill redigera.

Sidan för säsongspass har också tagits bort. En del av funktionaliteten finns kvar i serieöversiktsredigeraren, välj tabellvyn och tryck på "Välj serier". När du är i valt läge sveper du över numret i säsongskolumnen för att få tillgång till säsongspasspopovern för den serien.

## Avsnitt visar körtider på 0

v4 använder en körtid per avsnitt från TVDb. Om körtiden för avsnittet är 0 kommer den att försöka använda seriens körtid som fallback.
Om seriens körtid också är 0 kommer Sonarr att använda en körtid på 45 för alla avsnitt som sänds inom 24 timmar efter det första avsnittet.