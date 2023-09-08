Om du vill utlösa ett anpassat skript kan du hitta mer information här. Skript läggs till i Prowlarr via [Anslutningsinställningar](/prowlarr/settings#connections).

# Översikt

Prowlarr kan köra ett anpassat skript när en episod är nyimporterad eller omdöpt. Beroende på åtgärden tillhandahålls olika parametrar. Parametrar skickas till skriptet genom miljövariabler.

## Prowlarr-loggar

Observera att följande endast loggas för anpassade skript:

- Skriptets `stdout`-utdata loggas som `Debug`
- Skriptets `stderr`-utdata loggas som `Info`
- Utlösningen av skriptet loggas som `Trace`

# Miljövariabler

Miljövariabler varierar beroende på händelsetypen. Detaljer kommer snart^tm^

> [Koden att granska finns här för tillfället. Bidrag till wikin är välkomna](https://github.com/Prowlarr/Prowlarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## På test

När du lägger till skriptet i Prowlarr och klickar på 'Test', kommer skriptet att köras med följande parametrar. Skriptet bör kunna ignorera eventuella osupporterade händelsetyper på ett korrekt sätt.

| Miljövariabel       | Detaljer |
| ------------------- | -------- |
| `prowlarr_eventtype` | `Test`   |