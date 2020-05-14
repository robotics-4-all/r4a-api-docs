# Weather report API
---

## *CloudAPI*.**weatherReport**

Returns weather information for a specific area / country.

#### Input parameters

An `InputMessage`, containing in `data`:

- `location`: A location (e.g. a city)
- `country_code`: An [ISO 3166 country code](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)

#### Output

The TekVariables affected are:

- `TekVariables.WEATHER_REPORT`: The full weather report json
- `TekVariables.WEATHER_REPORT_DESCRIPTION`: A literal description
- `TekVariables.WEATHER_REPORT_TEMPERATURE`: The reported temperature
- `TekVariables.WEATHER_REPORT_PRESSURE`: The reported pressure
- `TekVariables.WEATHER_REPORT_HUMIDITY`: The reported humidity
