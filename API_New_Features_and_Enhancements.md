---
title: "API: New Feature and Enhancements V2"
output:
  html_document:
    keep_md: true
---
**Note: To use the V2 API, you must place v2 in the call.**
For example: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL>

# New Features and Enhancements Found in V2 API

* The API now returns ISO 3 and ISO 2 codes for all the countries along with country name, region, admin region, income level, lending type, Capital City, geographical co-ordinates.
* The 2-letter codes for Region, admin Region, Income Level and Lending Type are assigned and used by The World Bank.
* ISO2 code is available for Region, Income Level & Lending Type.

Examples:
  * <http://api.worldbank.org/v2/countries>
    - *Note: this call also list regions, incomelevels and lendingtypes along with countries. This helps in filtering country calls using regions/incomelevels/lendingtypes.*
  * <http://api.worldbank.org/v2/regions>
  * <http://api.worldbank.org/v2/incomelevels>
  * <http://api.worldbank.org/v2/lendingtypes>

## Enhancements in the indicator data queries
Example: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL>

The below information is now included in the response:

* The date(YYYY-mm-dd) of the source's most recent update.
* **Country ISO3 code:** Returns the country's ISO3 code.
* **Country Code (optional):** Returns the country's 3 character code, if desired. "Ctrycode=y" gives the Worldbank's 3 character code for the country, region, income level, and/or lending types called. "Ctrycode=n" removes the country code from the response.
  - Example: <http://api.worldbank.org/v2/country/EAP/indicator/SL.AGR.EMPL.ZS?ctrycode=y>
* **Footnote (optional):** Fetches footnote details in data calls, if desired. "Footnote=y" gives the footnote value for country, indicator and year. "Footnote=n" removes the footnote from the response.
  - Example: <http://api.worldbank.org/v2/country/chn/indicator/SL.AGR.EMPL.ZS?footnote=y>
* **Automatic Scale of numbers (optional):** Data values will be scaled automatically in thousands, millions, billions or trillions. If the data is less than a thousand, no scaling will be applied. "Scale=y" gives the scale in the response.  "Scale=n" removes the scale from the response.
  - Example: <http://api.worldbank.org/v2/country/ind/indicator/SP.POP.TOTL?scale=y>
* **Precision:** If the user requests for scaling, precision of decimal point will be based on the `<wb:decimal>` tag value, found in the response. If `<wb:decimal>` is 1 then the scaled value will have precision up to 1 decimal point. For example, if the data value is 2500 and `<wb:decimal>` is 1, then the data value will be scaled to 2.5 and `<wb:scale>` will read "thousands".
  - Example: <http://api.worldbank.org/v2/country/ind/indicator/SP.POP.TOTL?scale=y>
* **Observation Status:** Returns the observation status for country, indicator, and year combination. For example, <wb:Obs_status> F <wb:Obs_status>  in the response indicates that the observation status for that data point is "forecast".
  - Example: <http://api.worldbank.org/v2/countries/chn/indicators/NYGDPMKTPKDZ>

## Enhancements in JSON responses for indicator data queries
Example: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?format=json>

* Supports native JSON parser.
* The "fact" data type is now a number.
* Multiple indicators data: Multiple indicators data can be queried from a particular data source by providing source ID and indicators codes separated by ";" (semicolon).
  - Example: <http://api.worldbank.org/v2/country/chn;ago/indicator/AG.AGR.TRAC.NO;SP.POP.TOTL?source=2>
  - *Note: A maximum of 60 indicators can be used. A maximum of 1,500 characters are allowed between two /'s (back-slashes). A maximum of 4,000 characters are allowed in the entire URL.*


### Local Languages
Some countries are translated in their local languages. Any call to the API can be prefixed with a language code to retrieve localized results. The following local languages are available:

|Code|Language|
|--|--|
|bg	|Bulgarian|
|de	|German|
|hi	|Hindi|
|id	|Indonesian|
|ja	|Japanese|
|km	|Khmer|
|ko	|Korean|
|mk	|Macedonian|
|mn	|Mongolian|
|pl	|Polish|
|pt	|Portuguese|
|ro	|Romanian|
|ru	|Russian|
|sq	|Albanian|
|th |Thai|
|tr |Turkish|
|uk |Ukrainian|
|vi |Vietnamese|

A backslash followed by the country code gives localized results.  For example, to retrieve the country name of Vietnam in Vietnamese language you would use the following query:
<http://api.worldbank.org/v2/vi/country/vi>

*Note: The translated local language country names are not available for all the countries.*

## New JSONstat response format option for indicator data queries (BETA):
JSONstat is a simple lightweight JSON dissemination format best suited for data visualization, mobile apps or open data initiatives that has been designed for all kinds of disseminators.  Format=jsonstat' gives the JSONstat response.

Example: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?format=jsonstat>

## Download Enhancements

**Download to CSC or EXCEL Formats**
* CSV
  - Download .zip file that contains data, country metadata, and indicator metadata CSV files.
  - Example: <http://api.worldbank.org/v2/country/ind/indicator/AG.AGR.TRAC.NO?source=2&downloadformat=csv>

* EXCEL
  - Download .xls file that contains data, country metadata, and indicator metadata work sheets.
  - Example: <http://api.worldbank.org/v2/country/ind/indicator/AG.AGR.TRAC.NO?source=2&downloadformat=excel>

*Note: Country metadata will have special notes only for English language.*

### List or Table Formatting
You can now download indicator data in either List or Table format. The query string "dataformat" is used to download the indicator data into a list, with the years in either rows or columns. This query string works together with the "downloadformat" query string.

**Possible query strings for "dataformat":**
* "Dataformat=table" gives data in table format (column-wise year).
* "Dataformat=list" gives data in list format (row-wise year).

Example Request:
<http://api.worldbank.org/v2/country/usa/indicator/sp.pop.totl/?downloadformat=excel&dataformat=table>

Example Response:

![*Data Format: Table*](response1.png)

Example Request:
<http://api.worldbank.org/v2/country/usa/indicator/sp.pop.totl/?downloadformat=excel&dataformat=list>

Example Response:

![*Data Format: List*](response2.png)

## Metadata API Queries

Metadata queries are now available through the API.  Please refer to the Metadata API query documentation at (url for metadata api documentation) for more information.

## Subnational Data API Queries

Subnational queries are now available through the API.  Please refer to the Subnational API query documentation at (url for subnational data api documentation) for more information.
