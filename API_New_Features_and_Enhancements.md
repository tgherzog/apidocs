---
title: New Features and Enhancements in the V2 API
output:
  html_document:
    keep_md: true
---
Version 2 of the Indidators API has now been released! Version 1 of the API is no longer supported.

**Note: To use the V2 API, you must place `v2` in the call.**
For example: <http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL>

## Improved metadata in reponses

Metadata for countries and regions has been improved with the API now returning:
* ISO 3 and ISO 2 codes for all countries along with country name, region, admin region, income level, lending type, capital city and geographical co-ordinates.
* Both World Bank codes and ISO 2 codes for Region, Admin Region, Income Level and Lending Type

Examples:

  * <http://api.worldbank.org/v2/country>
    - *Note: this call also lists regions, incomelevels and lendingtypes along with countries. This helps in filtering country calls using regions/incomelevels/lendingtypes.*
  * <http://api.worldbank.org/v2/region>
  * <http://api.worldbank.org/v2/incomelevel>
  * <http://api.worldbank.org/v2/lendingtype>

## Enhancements to indicator data queries
Indicator query responses have also been enhanced with additional information provided.

Example: <http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL>

The following information is now included in the response:

* The date(YYYY-mm-dd) of the source's most recent update.

* **Country ISO3 code:** Returns the country's ISO3 code.

* **Country Code (optional):** Returns the country's 3 character code, if desired. Including `ctrycode=y` gives The World Bank's 3-character code for the country, region, income level, and/or lending types called. Adding `ctrycode=n` removes the country code from the response.
  - Example: <http://api.worldbank.org/v2/country/EAP/indicator/SL.AGR.EMPL.ZS?ctrycode=y>

* **Footnote (optional):** Fetches footnote details in data calls, if desired. Setting `footnote=y` gives the footnote value for country, indicator and year while `footnote=n` removes the footnote from the response.
  - Example: <http://api.worldbank.org/v2/country/chn/indicator/SL.AGR.EMPL.ZS?footnote=y>

* **Automatic Scale of numbers (optional):** Data values will be scaled automatically in thousands, millions, billions or trillions. If the data is less than a thousand, no scaling will be applied. Adding `scale=y` gives the scale in the response while `scale=n` removes the scale from the response.
  - Example: <http://api.worldbank.org/v2/country/ind/indicator/SP.POP.TOTL?scale=y>

* **Precision:** If the user requests scaling, the precision of the decimal point will be based on the `<wb:decimal>` tag value, found in the response. If `<wb:decimal>` is 1 then the scaled value will have precision up to 1 decimal point. For example, if the data value is 2500 and `<wb:decimal>` is 1, then the data value will be scaled to 2.5 and `<wb:scale>` will read "thousands".
  - Example: <http://api.worldbank.org/v2/country/ind/indicator/SP.POP.TOTL?scale=y>

* **Observation Status:** Indicates the observation status for country, indicator and year combination. For example, `<wb:obs_status> F </wb:obs_status>`  in the response indicates that the observation status for that data point is "forecast".
  - Example: <http://api.worldbank.org/v2/country/chn/indicator/NYGDPMKTPKDZ>

## Enhancements in JSON responses for indicator data queries
Responses in JSON format are available by using `format=json` in the API call.

Example: <http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL?format=json>

The following improvements have been made to JSON responses:

* Supports native JSON parser.
* The "fact" data type is now a number.
* Multiple indicators data: Data can be queried for multiple indicators from a particular data source by providing source ID and indicator codes separated by `;` (semicolon).
  - Example: <http://api.worldbank.org/v2/country/chn;ago/indicator/AG.AGR.TRAC.NO;SP.POP.TOTL?source=2>
  - *Note: A maximum of 60 indicators can be included with a maximum of 1,500 characters allowed between two `/`'s (back-slashes). A maximum of 4,000 characters are allowed in the entire URL.*

### Local Languages
Local language translations are available for some countries. Any call to the API can be prefixed with a language code to retrieve localized results where available. The following local languages are available:

|Code|Language|
|---|---|
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

A backslash followed by the country code after `http://api.worldbank.org/v2/` in an API call gives localized results.  

For example, to retrieve the country name of Vietnam in Vietnamese language you would use the following query:
<http://api.worldbank.org/v2/vi/country/vn>

*Note: The translated local language country and region names are not available for all countries.*

## New JSONstat response format option for indicator data queries (BETA):
JSONstat is a simple, lightweight JSON dissemination format best suited for data visualization, mobile apps or open data initiatives that has been designed for all kinds of disseminators.  Using `format=jsonstat` returns a JSONstat response.

Example: <http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL?format=jsonstat>

## Download Enhancements

Query responses can be downloaded in either zipped CSV or EXCEL format by using the `downloadformat` query string.
* CSV
  - Download .zip file that contains data, country metadata, and indicator metadata CSV files.
  - Example: <http://api.worldbank.org/v2/country/ind/indicator/AG.AGR.TRAC.NO?source=2&downloadformat=csv>

* EXCEL
  - Download .xls file that contains data, country metadata, and indicator metadata worksheets.
  - Example: <http://api.worldbank.org/v2/country/ind/indicator/AG.AGR.TRAC.NO?source=2&downloadformat=excel>

*Note: Country metadata will have special notes provided only in the English language.*

### List or Table Formatting
You can now download indicator data in either List or Table format. The query string `dataformat` is used to download the indicator data as a list, with the years in either rows or columns. This query string works together with the `downloadformat` query string.

**Possible query strings for `dataformat`:**
* `dataformat=table` returns data in table format (column-wise year).
* `dataformat=list` returns data in list format (row-wise year).

Example 1:
<http://api.worldbank.org/v2/country/usa/indicator/sp.pop.totl/?downloadformat=excel&dataformat=table>

Response 1:

![*Data Format: Table*](https://databank.worldbank.org/data/download/site-content/kb/api/response1.png)

Example 2:
<http://api.worldbank.org/v2/country/usa/indicator/sp.pop.totl/?downloadformat=excel&dataformat=list>

Response 2:

![*Data Format: List*](https://databank.worldbank.org/data/download/site-content/kb/api/response2.png)

## New Metadata API ##

* Metadata is now available via a [Metadata API](https://datahelpdesk.worldbank.org/knowledgebase/articles/1886695-metadata-api-queries)

<!--
* Subnational data is now available for select databases via the [Subnational Data API](link here)
-->

