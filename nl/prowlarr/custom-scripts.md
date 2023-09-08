Als je een aangepast script wilt activeren, kun je hier meer details vinden. Scripts worden aan Prowlarr toegevoegd via de [Connect Settings](/prowlarr/settings#connections).

# Overzicht

Prowlarr kan een aangepast script uitvoeren wanneer een aflevering nieuw wordt geïmporteerd of hernoemd. Afhankelijk van de actie worden verschillende parameters meegegeven. Parameters worden aan het script doorgegeven via omgevingsvariabelen.

## Prowlarr Logs

Merk op dat het volgende alleen wordt gelogd voor aangepaste scripts:

- Uitvoer van het script `stdout` wordt gelogd als `Debug`
- Uitvoer van het script `stderr` wordt gelogd als `Info`
- De trigger van het script wordt gelogd als `Trace`

# Omgevingsvariabelen

Omgevingsvariabelen variëren afhankelijk van het type gebeurtenis. Details volgen binnenkort^tm^

> [De code om te bekijken staat hier tijdelijk. Bijdragen aan de wiki zijn welkom](https://github.com/Prowlarr/Prowlarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Bij testen

Wanneer je het script aan Prowlarr toevoegt en op 'Test' klikt, wordt het script aangeroepen met de volgende parameters. Het script moet in staat zijn om eventuele niet-ondersteunde gebeurtenistypen op een elegante manier te negeren.

| Omgevingsvariabele | Details |
| ------------------ | ------- |
| `prowlarr_eventtype` | `Test`  |