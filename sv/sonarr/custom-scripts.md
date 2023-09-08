# Sonarr Anpassade Skript

Om du vill utlösa ett anpassat skript kan du hitta mer information här. Skript läggs till i Sonarr via [Anslutningsinställningar](/sonarr/settings#connections).

# Översikt

Sonarr kan köra ett anpassat skript när en episod är nyimporterad eller omdöpt. Beroende på åtgärden tillhandahålls olika parametrar. Parametrar skickas till skriptet genom miljövariabler.

## Sonarr-loggar

Observera att följande endast loggas för anpassade skript:

- Skriptets `stdout`-utdata loggas som `Debug`
- Skriptets `stderr`-utdata loggas som `Info`
- Triggern för skriptet loggas som `Trace`

# Miljövariabler

## Vid hämtning

| Miljövariabel                          | Detaljer                                                                                     |
| -------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                     | `Grab`                                                                                       |
| `sonarr_series_id`                     | Intern ID för serien                                                                         |
| `sonarr_series_title`                  | Titel på serien                                                                              |
| `sonarr_series_tvdbid`                 | TVDB-ID för serien                                                                           |
| `sonarr_series_tvmazeid`               | TVMaze-ID för serien                                                                         |
| `sonarr_series_imdbid`                 | IMDB-ID för serien (tom om okänd)                                                            |
| `sonarr_series_type`                   | Typ av serien (`Anime`, `Daily` eller `Standard`)                                            |
| `sonarr_release_episodecount`          | Antal avsnitt i utgåvan                                                                     |
| `sonarr_release_seasonnumber`          | Säsongsnummer från utgåvan                                                                   |
| `sonarr_release_episodenumbers`        | Kommaavgränsad lista över avsnittsnummer                                                     |
| `sonarr_release_absoluteepisodenumbers`| Kommaavgränsad lista över absoluta avsnittsnummer                                            |
| `sonarr_release_episodeairdates`       | Kommaavgränsad lista över sändningsdatum från originalnätverket                             |
| `sonarr_release_episodeairdatesutc`    | Kommaavgränsad lista över sändningsdatum i UTC                                               |
| `sonarr_release_episodetitles`         | `\|`-avgränsad lista över avsnittstitlar                                                     |
| `sonarr_release_title`                 | Torrent-/NZB-titel                                                                           |
| `sonarr_release_indexer`               | Indexer från vilken utgåvan hämtades                                                         |
| `sonarr_release_size`                  | Storlek på utgåvan, enligt indexer                                                            |
| `sonarr_release_quality`               | Kvalitetsnamn på utgåvan, som detekterats av Sonarr                                           |
| `sonarr_release_qualityversion`        | `1` är standard, `2` är för korrekt och `3`+ kan användas för animeversioner                 |
| `sonarr_release_releasegroup`          | Utgivargrupp (tom om okänd)                                                                  |
| `sonarr_download_client`               | Nedladdningsklient                                                                           |
| `sonarr_download_id`                   | Hash för torrent-/NZB-filen (används för att unikt identifiera nedladdningen i nedladdningsklienten) |

## Vid import/uppgradering

| Miljövariabel                           | Detaljer                                                                                     |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Download`                                                                                   |
| `sonarr_isupgrade`                      | `True` om en befintlig fil uppgraderas, `False` annars                                       |
| `sonarr_series_id`                      | Intern ID för serien                                                                        |
| `sonarr_series_title`                   | Titel på serien                                                                             |
| `sonarr_series_path`                    | Full sökväg till serien                                                                     |
| `sonarr_series_tvdbid`                  | TVDB-ID för serien                                                                          |
| `sonarr_series_tvmazeid`                | TVMaze-ID för serien                                                                        |
| `sonarr_series_imdbid`                  | IMDB-ID för serien (tom om okänd)                                                           |
| `sonarr_series_type`                    | Typ av serien (`Anime`, `Daily` eller `Standard`)                                           |
| `sonarr_episodefile_id`                 | Intern ID för episodfilen                                                                  |
| `sonarr_episodefile_episodecount`       | Antal avsnitt i filen                                                                      |
| `sonarr_episodefile_relativepath`       | Sökväg till episodfilen, relativt seriens sökväg                                            |
| `sonarr_episodefile_path`               | Full sökväg till episodfilen                                                               |
| `sonarr_episodefile_episodeids`         | Intern(a) ID(s) för episodfilen                                                            |
| `sonarr_episodefile_seasonnumber`       | Säsongsnummer för episodfilen                                                              |
| `sonarr_episodefile_episodenumbers`     | Komma-separerad lista med avsnittsnummer                                                    |
| `sonarr_episodefile_episodeairdates`    | Komma-separerad lista med sändningsdatum från ursprunglig nätverk                           |
| `sonarr_episodefile_episodeairdatesutc` | Komma-separerad lista med sändningsdatum i UTC                                              |
| `sonarr_episodefile_episodetitles`      | `\|`-separerad lista med avsnittstitlar                                                     |
| `sonarr_episodefile_quality`            | Kvalitetsnamn på episodfilen, som detekterats av Sonarr                                      |
| `sonarr_episodefile_qualityversion`     | `1` är standard, `2` är för korrekt och `3`+ kan användas för anime-versioner               |
| `sonarr_episodefile_releasegroup`       | Släppgrupp (tom om okänd)                                                                   |
| `sonarr_episodefile_scenename`          | Ursprungligt namn på släppet (tom om okänt)                                                 |
| `sonarr_episodefile_sourcepath`         | Full sökväg till den importerade episodfilen                                                |
| `sonarr_episodefile_sourcefolder`       | Full sökväg till mappen där episodfilen importerades från                                  |
| `sonarr_download_client`                | Nedladdningsklient                                                                          |
| `sonarr_download_id`                    | Hash av torrent-/NZB-filen (används för att unikt identifiera nedladdningen i klienten)     |
| `sonarr_deletedrelativepaths`           | `\|`-separerad lista med filer som raderades för att importera denna fil                    |
| `sonarr_deletedpaths`                   | `\|`-separerad lista med fullständiga sökvägar till filer som raderades för att importera denna fil |

## Vid omdöpning

| Miljövariabel              | Detaljer                                              |
| ------------------------- | ---------------------------------------------------- |
| `sonarr_eventtype`        | `Rename`                                              |
| `sonarr_series_id`        | Intern ID för serien                                 |
| `sonarr_series_title`     | Titel på serien                                      |
| `sonarr_series_path`      | Full sökväg till serien                              |
| `sonarr_series_tvdbid`    | TVDB-ID för serien                                   |
| `sonarr_series_tvmazeid`  | TVMaze-ID för serien                                 |
| `sonarr_series_imdbid`    | IMDB-ID för serien (tom om okänd)                     |
| `sonarr_series_type`      | Typ av serien (`Anime`, `Daily` eller `Standard`)     |

## Vid borttagning av episodfil

| Miljövariabel                         | Detaljer                                                                         |
| ------------------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`                     | `EpisodeFileDelete`                                                              |
| `sonarr_series_id`                     | Intern ID för serien                                                             |
| `sonarr_series_title`                  | Titel på serien                                                                  |
| `sonarr_series_path`                   | Full sökväg till serien                                                          |
| `sonarr_series_tvdbid`                 | TVDB ID för serien                                                               |
| `sonarr_series_tvmazeid`               | TVMaze ID för serien                                                             |
| `sonarr_series_imdbid`                 | IMDB ID för serien (tom om okänd)                                                 |
| `sonarr_series_type`                   | Typ av serien (`Anime`, `Daily` eller `Standard`)                                 |
| `sonarr_episodefile_id`                | Intern ID för episodfilen                                                       |
| `sonarr_episodefile_episodecount`      | Antal avsnitt i filen                                                            |
| `sonarr_episodefile_relativepath`      | Sökväg till episodfilen, relativt seriens sökväg                                  |
| `sonarr_episodefile_path`              | Full sökväg till episodfilen                                                     |
| `sonarr_episodefile_episodeids`        | Interna ID:n för episodfilen                                                     |
| `sonarr_episodefile_seasonnumber`      | Säsongsnummer för episodfilen                                                    |
| `sonarr_episodefile_episodenumbers`    | Komma-separerad lista med avsnittsnummer                                          |
| `sonarr_episodefile_episodeairdates`   | Komma-separerad lista med sändningsdatum från originalnätverket                   |
| `sonarr_episodefile_episodeairdatesutc`| Komma-separerad lista med sändningsdatum i UTC                                    |
| `sonarr_episodefile_episodetitles`     | `\|`-separerad lista med avsnittstitlar                                           |
| `sonarr_episodefile_quality`           | Kvalitetsnamn på episodfilen, som detekterats av Sonarr                            |
| `sonarr_episodefile_qualityversion`    | `1` är standard, `2` används för korrekta versioner och `3`+ kan användas för animeversioner |
| `sonarr_episodefile_releasegroup`      | Releasegrupp (tom om okänd)                                                      |
| `sonarr_episodefile_scenename`         | Ursprungligt releasenamn (tom om okänd)                                           |

## Vid borttagning av serie

| Miljövariabel               | Detaljer                                                              |
| -------------------------- | --------------------------------------------------------------------- |
| `sonarr_eventtype`         | `SeriesDelete`                                                        |
| `sonarr_series_id`         | Intern ID för serien                                                  |
| `sonarr_series_title`      | Titel på serien                                                       |
| `sonarr_series_path`       | Full sökväg till serien                                               |
| `sonarr_series_tvdbid`     | TVDB ID för serien                                                    |
| `sonarr_series_imdbid`     | IMDB ID för serien (tom om okänd)                                      |
| `sonarr_series_type`       | Typ av serien (`Anime`, `Daily` eller `Standard`)                      |
| `sonarr_series_deletedfiles` | `True` om alternativet för att ta bort filer har valts, annars `False` |

## Vid hälsoproblem

| Miljövariabel               | Detaljer                                                               |
| -------------------------- | ---------------------------------------------------------------------- |
| `sonarr_eventtype`         | `HealthIssue`                                                          |
| `sonarr_health_issue_level` | Typ av hälsoproblem (`Ok`, `Notice`, `Warning` eller `Error`)           |
| `sonarr_health_issue_message` | Meddelande från hälsoproblemet                                        |
| `sonarr_health_issue_type`  | Område som misslyckades och utlöste hälsoproblemet                      |
| `sonarr_health_issue_wiki`  | Wiki-URL (tom om den inte finns)                                        |

## Vid uppdatering av applikationen

| Miljövariabel                 | Detaljer                                      |
| ---------------------------- | --------------------------------------------- |
| `sonarr_eventtype`           | `ApplicationUpdate`                           |
| `sonarr_update_message`      | Meddelande från uppdateringen                  |
| `sonarr_update_newversion`   | Version som Sonarr uppdaterades till (sträng)  |
| `sonarr_update_previousversion` | Version som Sonarr uppdaterades från (sträng) |

## Vid test

När du lägger till skriptet i Sonarr och klickar på 'Test' kommer skriptet att köras med följande parametrar. Skriptet bör kunna ignorera eventtyper som inte stöds.

| Miljövariabel         | Detaljer |
| -------------------- | ------- |
| `sonarr_eventtype`   | `Test`  |