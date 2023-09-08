# Serier

Sidan för serier visar hela din bibliotek och låter dig välja enskilda serier (men att söka kan vara mer effektivt i stora bibliotek) och göra sökningar efter specifika serier, samt redigera dem. Det låter dig också filtrera dina serier.

# Filter

Filteralternativen låter dig begränsa dina serier och är otroligt användbara. Det kan användas för att se utgivningsdatum, namn, antal avsnitt, diskstorlek och mycket mer, inklusive anpassade filter, för att passa alla dina behov. Dessa kan också användas i massredigeraren.

# Lägg till ny

Funktionen för att lägga till nytt låter dig lägga till en ny serie som Sonarr ska övervaka och ladda ner.

- Rotmapp - Den valda [rot-/biblioteksmappen](/sonarr/settings#root-folders) i Sonarr som denna serie ska använda
- Övervaka - Hur vill du att serien ska övervakas initialt?
  - Alla avsnitt - Övervaka alla avsnitt utom specialavsnitt
  - Kommande avsnitt - Övervaka avsnitt som ännu inte har sänts
  - Saknade avsnitt - Övervaka avsnitt som inte har filer eller ännu inte har sänts
  - Befintliga avsnitt - Övervaka avsnitt som har filer
  - Första säsongen - Övervaka alla avsnitt i första säsongen; alla andra säsonger kommer att ignoreras
  - Senaste säsongen - Övervaka alla avsnitt i den senaste säsongen och framtida säsonger
  - Ingen - Inga avsnitt kommer att övervakas
- Kvalitetsprofil - Den [kvalitetsprofil](/sonarr/settings#quality-profiles) som ska användas för denna serie
- Serie typ - Vilken serie typ som ska användas för denna serie; detta ändrar hur sökningar utförs [Se FAQ för mer information](/sonarr/faq#whats-the-different-series-types)
- Säsongs mapp - Aktivera eller inaktivera skapande och användning av säsongs mappar för denna serie
- Taggar - Används för att tilldela serier till utgivningsprofiler, fördröjningsprofiler, indexerare eller bara för att organisera dina serier
- [ ] Starta sökning efter saknade avsnitt - baserat på dina valda övervakningsinställningar, sök efter alla saknade och övervakade avsnitt i denna serie
- [ ] Starta sökning efter avsnitt som inte uppfyller avskärningskriterier - baserat på dina valda övervakningsinställningar och endast tillämpligt om du har befintliga filer för dina avsnitt i serie mappen, sök efter alla befintliga och övervakade avsnitt i denna serie som inte uppfyller eller överstiger din kvalitetsprofils avskärningskriterier

# Biblioteksimport

Biblioteksimport låter dig importera befintliga, organiserade serier och avsnittsfiler till Sonarr via befintliga filer i sökvägen. Detta är särskilt användbart när du skapar en ny Sonarr-instans och vill behålla dina befintliga serier.

- Biblioteksimport används för att lägga till och importera ett befintligt organiserat bibliotek av serier till Sonarr.

- Biblioteksimport kan inte användas för:
  - Att importera filer från en nedladdningsmapp
  - Att lägga till eller importera en eller flera filer som inte är korrekt namngivna och organiserade i sin egen serie mapp inom din rotmapp eller en mapp som du vill lägga till som rotmapp
  - Andra användningsområden som inte innebär att lägga till en serie eller ett avsnitt i Sonarr och importera serien och dess fil(er) från rot- (biblioteks-) mappen som angavs vid biblioteksimporten

> \* Ej Windows: Om du använder en NFS-montering, se till att `nolock` är aktiverat.
> \* Om du använder en SMB-montering, se till att `nobrl` är aktiverat.
{.is-warning}

> **Användaren och gruppen som du konfigurerade Sonarr att köra som måste ha läs- och skrivrättigheter till denna plats.** {.is-info}

> Din nedladdningsklient laddar ner till en nedladdningsmapp och Sonarr importerar det till din mediamapp (slutdestination) som din mediaserver använder.
{.is-info}

> **Din nedladdningsmapp och mediamapp kan inte vara samma plats**
{.is-danger}

# Massredigerare

Massredigeraren låter dig redigera serier i stora mängder. Du kan ändra alla tidigare inställningar som gjordes när du lade till serien.

# Säsongspass

Detta visar information om hur många säsonger varje serie har och hur många avsnitt som saknas i varje säsong.