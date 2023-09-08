> This FAQ item is a legacy FAQ Entry. Refer to [How does Readarr work?](#how-does-readarr-work)
{.is-info}

- Nei, og du bør heller ikke gjøre det gjennom noen SQL-hacking. Oppgaven "Oppdater bøker" spør oppstrøms Servarr-proxyen og sjekker om metadata for hver bok (ID-er, rollebesetning, sammendrag, rangering, oversettelser, alternative titler osv.) har blitt oppdatert sammenlignet med det som er i Readarr. Hvis det er nødvendig, vil den deretter oppdatere de aktuelle bøkene.
- En vanlig klage er at oppgaven "Oppdater" forårsaker tung I/O-bruk. En innstilling som kan forårsake problemer er "Skann forfattermappe etter oppdatering". Hvis disk I/O-bruken øker under en oppdatering, kan du vurdere å endre innstillingen for skanning til `Manuell`. Ikke endre dette til `Aldri` med mindre alle endringer i biblioteket ditt (nye bøker, oppgraderinger, slettinger osv.) blir gjort gjennom Readarr. Hvis du sletter bokfiler manuelt eller med et tredjepartsprogram, må du ikke sette dette til `Aldri`.

## Kan jeg ha både en e-bok og en lydbokversjon av samme bok?

- Nei. Med en enkelt Readarr-instans kan du ha enten den ene eller den andre, men ikke begge deler. Hvis du ønsker begge deler, må du kjøre to separate instanser av Readarr (på samme måte som noen kjører 2 instanser av Sonarr eller Radarr for 1080p- og 4K-versjoner av mediefilene sine).

## Må jeg bruke Calibre?

- Nei. Generelt sett tilbyr Calibre noen ytterligere fordeler, som muligheten til å automatisk konvertere e-bøker til et annet format som er spesifikt for leserens funksjoner, og også å koble til leseren. Men hvis du ikke brukte Calibre før du installerte Readarr, vil det sannsynligvis ha begrenset nytteverdi for deg å installere det, og det er et veldig stort program.

## Hvorfor kan ikke Readarr se filene mine på en ekstern server?

- For alle operativsystemer må du sørge for at brukeren/gruppen du kjører \*Arr som, har lese- og skrivetilgang til den monterte disken.
- For Linux må du sørge for:
  - Hvis du bruker en NFS-montering, må du sørge for at nolock er aktivert for monteringen din.
  - Hvis du bruker en SMB-montering, må du sørge for at nobrl er aktivert for monteringen din.
- For Windows: Kort sagt, brukeren \*Arr kjører som (hvis tjeneste) eller under (hvis brettapp) har ikke tilgang til filbanen på den eksterne serveren. Dette kan skyldes forskjellige årsaker, men det vanligste er at \*Arr kjører som en tjeneste, noe som forårsaker problemene som beskrives nedenfor.

### Readarr kjører som standard under LocalService-kontoen, som ikke har tilgang til beskyttede eksterne filområder

- Kjør Readarr-tjenesten som en annen bruker som har tilgang til den delte mappen
- Åpne vinduet Administrative verktøy \> Tjenester på Windows-serveren din.
- Stopp Readarr-tjenesten.
- Åpne dialogboksen Egenskaper \> Pålogging.
- Endre brukerkontoen for tjenesten til målbrukerkontoen.
- Kjør Readarr.exe ved hjelp av oppstartsmappen

### Du bruker en kartlagt nettverksstasjon (ikke en UNC-sti)

- Endre stiene dine til UNC-stier (`\\server\share`)
- Kjør Readarr.exe via oppstartsmappen

## Hjelp, jeg har låst meg ute

{#hjelp-jeg-har-glemt-passordet-mitt}

Hvis du vil deaktivere autentisering (for å tilbakestille glemt brukernavn eller passord), må du redigere `config.xml`, som vil være inne i [Readarr Appdata-mappen](/readarr/appdata-directory)

1. Åpne config.xml i en tekstredigerer
1. Finn linjen for autentiseringsmetode, som vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Endre linjen for `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Readarr på nytt
1. Readarr vil nå være tilgjengelig uten passord. Du bør gå til `Innstillinger: Generelt` i brukergrensesnittet og angi brukernavnet og passordet ditt

## Hvordan stopper jeg nettleseren fra å starte ved oppstart?

Avhengig av operativsystemet ditt, finnes det flere mulige måter.

- I `Innstillinger` => `Generelt` på noen operativsystemer, er det en avmerkingsboks for å starte nettleseren ved oppstart.
- Når du starter Readarr, kan du legge til `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumentene.
- Stopp Readarr og rediger config.xml-filen, og endre `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Rar UI-problemer

- Hvis du opplever rare UI-problemer, som at bibliotekssiden ikke viser noe eller at en bestemt visning eller sortering ikke fungerer, kan du prøve å se det i et Chrome Inkognitovindu eller Firefox Privat vindu. Hvis det fungerer fint der, kan du tømme nettleserens hurtigbuffer og informasjonskapsler for din spesifikke IP/domene. For mer informasjon, se artikkelen [Tøm hurtigbuffer, informasjonskapsler og lokal lagring](/useful-tools#clearing-cookies-and-local-storage) i wikien.

## VPN-er, Jackett og \*ARR-ene

- Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, er det vanligvis bare torrentklienten din som trenger å være bak en VPN. Fordi VPN-tilkoblingspunktet deles av mange brukere, kan du oppleve begrensning av hastigheten, DDOS-beskyttelse og IP-blokkering fra ulike tjenester som hver programvare bruker.
- Med andre ord kan det å plassere \*Arr-ene (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bak en VPN gjøre applikasjonene ubrukelige i noen tilfeller på grunn av at tjenestene ikke er tilgjengelige.

> **For å være tydelig, det handler ikke om hvorvidt VPN-er vil forårsake problemer med \*Arr-ene, men når: bildetilbydere vil blokkere deg, og Cloudflare er foran de fleste \*Arr-servere (oppdateringer, metadata osv.) og kan også blokkere deg**
{.is-warning}

- **Mange private sporingsnettsteder vil utestenge deg hvis du bruker eller får tilgang til dem (f.eks. ved å bruke Jackett eller Prowlarr) via en VPN.**

### Bruk av VPN

- Hvis en VPN er nødvendig og Docker brukes, anbefales det å bruke Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er nødvendig og Docker ikke brukes, må VPN-klienten din ***støtte*** delt tunnelering slik at bare de nødvendige (nedlastingsklient)appene er bak VPN-en.
- Mange problemer med å få tilgang til sporingsnettsteder kan løses ved å bruke Googles eller Cloudflares DNS-servere i stedet for ISP-ens DNS-servere.
- I noen tilfeller (f.eks. britiske internettleverandører) kan du trenge å plassere torrentnedlastingsklienten bak en VPN og Jackett/Prowlarr som følger:
  - Plasser Jackett bak VPN-en og sørg for at delt tunnelering tillater lokal tilgang
  - For Prowlarr kan du konfigurere VPN-klienten din til å gi en proxy og legge til proxyen i Innstillinger => Indekser. Gi proxyen en tagg, og gi alle indekser som trenger å bruke den samme taggen.
    - Hvis det absolutt er nødvendig, og hvis VPN-en din ikke gir en måte å opprette en proxy på, kan du plassere Prowlarr bak VPN-en og sørge for at delt tunnelering tillater lokal tilgang.

## Jacketts /all-endepunkt

{#jackett-all-endpoint}

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan føre til problemer, så det er nødvendig å legge til hver sporingsnettsted individuelt. Alternativt kan du vurdere å bruke Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)
- **Oppdatering 20. januar 2022: Jackett `/all`-endepunktet støttes ikke lenger (det vil vises advarsler) fra og med versjon 0.1.0.1188 på grunn av at det bare forårsaker problemer.**
- Jackett /all-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan føre til problemer, så det er nå nødvendig å legge til hvert sporingsnettsted individuelt.
- [Selv Jacketts utviklere sier at det bør unngås og ikke brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Bruk av /all-endepunktet har ingen fordeler, bare ulemper:
  - Du mister kontrollen over innstillingene for hvert sporingsnettsted (kategorier, søkemåter osv.)
  - Blanding av søkemåter (IMDB, søk, osv.) kan føre til resultater av lav kvalitet
  - Spesifikke kategorier for hvert sporingsnettsted (\>= 100000) kan ikke brukes.
  - Tregt sporingsnettsted vil bremse ned den generelle resultatet
  - Totalt antall resultater er begrenset til 1000
  - Hvis ett av sporingsnettstedene i /all returnerer en feil, vil \*Arr deaktivere det, og du får ingen resultater.

### Løsninger for Jackett /all

- Legg til hvert sporingsnettsted i Jackett manuelt som en indekser i \*Arr
- Sjekk ut [Prowlarr](/prowlarr), som kan synkronisere indekser til \*Arr og er utviklet av Lidarr/Radarr/Readarr-utviklingsteamet.
- Sjekk ut [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indekser til \*Arr. Men ikke bruk deres enkeltstående aggregerte endepunkt, bruk `multi` hvis synkronisering skal brukes.

## Hvorfor er det to filer? | Hvorfor er det en fil igjen i nedlastinger?

Dette er forventet. Med en konfigurasjon som støtter [hardlinker](https://trash-guides.info/hardlinks), vil ikke dobbelt plass bli brukt. Her er hvordan torrentprosessen fungerer.

1. Readarr sender en nedlastingsforespørsel til klienten din og knytter den til en etikett eller kategorinavn som du har konfigurert i innstillingene for nedlastingsklienten. Eksempler: filmer, tv, serier, musikk osv.
1. Readarr overvåker de aktive nedlastingene i nedlastingsklienten som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
1. Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Readarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil de enten bli hardlinket hvis det støttes av konfigurasjonen din, eller kopiert hvis hardlinker ikke støttes.
1. Hvis alternativet "Behandling av fullførte nedlastinger - Fjern fullførte" er aktivert i Readarrs innstillinger, vil Readarr slette den opprinnelige filen og torrenten fra nedlastingsklienten, men bare hvis nedlastingsklienten rapporterer at seeding er fullført og torrenten er stoppet.

> Hardlinker er aktivert som standard. [En hardlink vil ikke bruke ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringspunktene må være de samme for mappen der fullførte nedlastinger er og mediebiblioteket ditt. Hvis opprettelsen av hardlinker mislykkes eller konfigurasjonen din ikke støtter hardlinker, vil den falle tilbake og kopiere filen.
{.is-info}

## Calibre sier "Calibre rejected duplicate book", men det er det ikke

Hvis du bruker Calibre-integrasjon, vil Calibre av og til avvise en bok og si at den er en duplikat. Det er sannsynligvis ikke faktisk en duplikat. Hvis dette skjer, er det ikke mye Readarr kan gjøre, og du må slutte å overvåke den boken for å forhindre at Readarr fortsetter å prøve å hente den og sende den til Calibre. Dette er bare en av de morsomme ulempene med Calibre-integrasjonen.