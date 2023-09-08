- No, you cannot disable the refresh books task in Readarr. The refresh books task is responsible for updating the metadata and status of your books, ensuring that the information in Readarr is accurate and up to date. Disabling this task would result in outdated and incorrect information in your library.

- Nej, det bør du heller ikke gøre gennem nogen SQL-hack. Opdater bøger-opgaven forespørger upstream Servarr-proxyen og kontrollerer, om metadataen for hver bog (id'er, rollebesætning, resumé, vurdering, oversættelser, alternative titler osv.) er blevet opdateret i forhold til det, der er i Readarr. Hvis det er nødvendigt, opdateres de relevante bøger.
- En almindelig klage er, at opdateringsopgaven forårsager tung I/O-brug. En indstilling, der kan forårsage problemer, er "Rescan forfattermappe efter opdatering". Hvis din disk I/O-brug stiger under en opdatering, kan du ændre rescan-indstillingen til `Manuel`. Skift den ikke til `Aldrig`, medmindre alle ændringer i dit bibliotek (nye bøger, opgraderinger, sletninger osv.) udføres gennem Readarr. Hvis du sletter bogfiler manuelt eller ved hjælp af et tredjepartsprogram, skal du ikke indstille dette til `Aldrig`.

## Kan jeg have både en e-bog og en lydbogsversion af samme bog?

- Nej. Med en enkelt Readarr-instans kan du kun have enten den ene eller den anden, men ikke begge dele. Hvis du vil have begge dele, skal du køre to separate instanser af Readarr (ligesom nogle mennesker kører 2 instanser af Sonarr eller Radarr til 1080p- og 4K-versioner af deres medier).

## Skal jeg bruge Calibre?

- Nej. Generelt tilbyder Calibre nogle yderligere forbedringer, såsom evnen til automatisk at konvertere e-bøger til et andet format, der er specifikt for din e-læsers evner, og også til at oprette forbindelse til den e-læser. Men hvis du ikke kørte Calibre før du installerede Readarr, vil det sandsynligvis have begrænset merværdi for dig at installere det, og det er et meget stort program.

## Hvorfor kan Readarr ikke se mine filer på en fjernserver?

- For alle operativsystemer skal du sikre dig, at den bruger/gruppe, som du kører \*Arr som, har læse- og skriveadgang til det monterede drev.
- For Linux skal du sikre dig:
  - Hvis du bruger en NFS-montering, skal du sikre dig, at nolock er aktiveret for din montering.
  - Hvis du bruger en SMB-montering, skal du sikre dig, at nobrl er aktiveret for din montering.
- For Windows: Kort sagt kan brugeren, som \*Arr kører som (hvis det er en tjeneste) eller under (hvis det er en bakkeapp), ikke få adgang til filstien på fjernserveren. Dette kan skyldes forskellige årsager, men den mest almindelige er, at \*Arr kører som en tjeneste, hvilket forårsager de beskrevne problemer.

### Readarr kører som standard under LocalService-kontoen, som ikke har adgang til beskyttede fjernfiler

- Kør Readarr-tjenesten som en anden bruger, der har adgang til den delte mappe
- Åbn vinduet Administrative værktøjer \> Tjenester på din Windows-server.
- Stop Readarr-tjenesten.
- Åbn dialogboksen Egenskaber \> Logon.
- Skift tjenestebrugerkontoen til målbrugerkontoen.
- Kør Readarr.exe ved hjælp af opstartsmappe

### Du bruger et kortlagt netværksdrev (ikke en UNC-sti)

- Skift dine stier til UNC-stier (`\\server\share`)
- Kør Readarr.exe via opstartsmappe

## Hjælp, jeg har låst mig ude

{#hjaelp-jeg-har-glemt-mit-adgangskode}

Hvis du vil deaktivere godkendelse (for at nulstille dit glemte brugernavn eller adgangskode), skal du redigere `config.xml`, som vil være inde i [Readarr Appdata-mappen](/readarr/appdata-directory)

1. Åbn config.xml i en teksteditor
1. Find linjen med godkendelsesmetoden, som vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Ændr linjen `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Genstart Readarr
1. Readarr vil nu være tilgængelig uden adgangskode. Du bør gå til `Indstillinger: Generelt` i brugergrænsefladen og indstille dit brugernavn og adgangskode

## Hvordan stopper jeg browseren fra at åbne ved opstart?

Afhængigt af dit operativsystem er der flere mulige måder.

- I `Indstillinger` => `Generelt` på nogle operativsystemer er der en afkrydsningsboks til at åbne browseren ved opstart.
- Når du starter Readarr, kan du tilføje `-nobrowser` (*nix) eller `/nobrowser` (Windows) til argumenterne.
- Stop Readarr og rediger config.xml-filen, og ændr `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Underlige UI-problemer

- Hvis du oplever underlige UI-problemer som f.eks. at bibliotekssiden ikke viser noget eller en bestemt visning eller sortering ikke fungerer, skal du prøve at se det i et Chrome Inkognitovindue eller Firefox Privat vindue. Hvis det fungerer fint der, skal du rydde din browsers cache og cookies for din specifikke IP/domæne. For mere information, se artiklen [Ryd cache, cookies og lokal lagring](/useful-tools#clearing-cookies-and-local-storage) i wiki'en.

## VPN'er, Jackett og \*ARRs

- Medmindre du befinder dig i et undertrykkende land som Kina, Australien eller Sydafrika, er din torrentklient typisk det eneste, der skal være bag en VPN. Fordi VPN-endepunktet deles af mange brugere, kan du opleve hastighedsbegrænsning, beskyttelse mod DDOS og IP-blokeringer fra forskellige tjenester, som hver software bruger.
- Med andre ord kan det at placere \*Arrs (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bag en VPN gøre applikationerne ubrugelige i nogle tilfælde på grund af utilgængelige tjenester.

> **For at være klar, det handler ikke om, hvorvidt VPN'er vil forårsage problemer med \*Arrs, men hvornår: billedudbydere vil blokere dig, og cloudflare er foran de fleste \*Arr-servere (opdateringer, metadata osv.) og kan også blokere dig**
{.is-warning}

- **Mange private trackere vil udelukke dig, hvis du bruger eller får adgang til dem (f.eks. ved hjælp af Jackett eller Prowlarr) via en VPN.**

### Brug af en VPN

- Hvis en VPN er påkrævet, og Docker bruges, anbefales det at bruge Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er påkrævet, og Docker ikke bruges, skal din VPN-klient ***understøtte opdeling af tunnel***, så kun de nødvendige (Download Client) -apps er bag VPN'en.
- Mange problemer med adgang til trackere kan løses ved at bruge Googles eller Cloudflares DNS-servere i stedet for din internetudbyders DNS-servere.
- I nogle tilfælde (f.eks. britiske internetudbydere) skal du muligvis placere din torrent-downloadklient bag en VPN og Jackett/Prowlarr som følger:
  - Placer Jackett bag VPN'en og sørg for, at opdeling af tunnel tillader lokal adgang
  - Konfigurer din VPN-klient til at levere en proxy og tilføj proxyen i Indstillinger => Indekser. Giv proxyen en tag, og tildel det samme tag til eventuelle indekser, der skal bruge den.
    - Hvis det absolut er nødvendigt, og hvis din VPN ikke giver en måde at oprette en proxy på, kan du placere Prowlarr bag VPN'en og sikre dig, at opdeling af tunnel tillader lokal adgang.

## Jacketts /all-endepunkt

{#jackett-all-endepunkt}

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordel. Alt andet kan være potentielle problemer, så det er nødvendigt at tilføje hver tracker individuelt. Alternativt kan du overveje at bruge Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)
- **Opdatering 20. januar 2022: Jackett `/all`-endepunktet understøttes ikke længere (der vil forekomme advarsler) fra version 0.1.0.1188 på grund af at det kun skaber problemer.**
- Jackett /all-endepunktet er praktisk, men det er den eneste fordel. Alt andet kan være potentielle problemer, så det er nu nødvendigt at tilføje hver tracker individuelt.
- [Selv Jacketts udviklere siger, at det bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Brug af /all-endepunktet har ingen fordele, kun ulemper:
  - du mister kontrollen over indstillingen for den enkelte indekser (kategorier, søgemetoder osv.)
  - blanding af søgemetoder (IMDB, forespørgsel osv.) kan medføre resultater af lav kvalitet
  - indekser-specifikke kategorier (\>= 100000) kan ikke bruges.
  - langsomme indekser vil sænke den samlede resultat
  - det samlede antal resultater er begrænset til 1000
  - hvis en af trackerne i /all returnerer en fejl, vil \*Arr deaktivere den, og nu får du ingen resultater.

### Jackett /All-løsninger

- Tilføj hver tracker i Jackett manuelt som en indekser i \*Arr
- Prøv [Prowlarr](/prowlarr), som kan synkronisere indeksere til \*Arr og er udviklet af Lidarr/Radarr/Readarr-udviklingsteamet.
- Prøv [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indeksere til \*Arr. Men brug ikke deres enkeltstående samlede endepunkt, og brug `multi`, hvis synkroniseringen skal bruges.

## Hvorfor er der to filer? | Hvorfor er der en fil tilbage i downloads?

Dette er forventet. Med en konfiguration, der understøtter [hardlinks](https://trash-guides.info/hardlinks), vil der ikke blive brugt dobbelt plads. Her er, hvordan Torrent-processen fungerer.

1. Readarr sender en downloadanmodning til din klient og tilknytter den til etiketten eller kategorinavnet, som du har konfigureret i indstillingerne for downloadklienten. Eksempler: film, tv, serier, musik osv.
1. Readarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Denne overvågning sker via din downloadklients API.
1. Færdige filer efterlades på deres oprindelige placering for at tillade, at du kan seede filen (forhold eller tid kan justeres i downloadklienten eller inden for den specifikke downloadklient). Når filer importeres til din mediemappe, oprettes der en hardlink til filen, hvis det understøttes af din konfiguration, eller filen kopieres, hvis hardlinks ikke understøttes.
1. Hvis indstillingen "Behandling af fuldførte downloads - Fjern fuldførte" er aktiveret i Readarrs indstillinger, vil Readarr slette den oprindelige fil og torrent fra din downloadklient, men kun hvis downloadklienten rapporterer, at seeding er fuldført, og torrenten er stoppet.

> Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlink mislykkes, eller din konfiguration ikke understøtter hardlinks, vil der blive kopieret en fil i stedet.
{.is-info}

## Calibre siger "Calibre afviste duplikatbog", men det er det ikke

Hvis du bruger Calibre-integration, vil Calibre lejlighedsvis afvise en bog og sige, at det er en duplikat. Det er sandsynligvis ikke faktisk en duplikat. Hvis dette sker, er der ikke meget, Readarr kan gøre, og du bliver nødt til at stoppe overvågningen af den bog for at forhindre, at Readarr fortsætter med at forsøge at hente den og sende den til Calibre. Dette er bare en af de sjove ulemper ved Calibre-integrationen.