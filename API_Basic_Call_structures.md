---
title: API Basic Call Structures
output:
  html_document:
    keep_md: true
---

The Indicators API supports two basic ways to build queries: a URL based structure and an argument based structure. For example, the following two requests will return the same data, a list of countries with income level classified as low income:

* Argument based: <http://api.worldbank.org/V2/countries?incomeLevel=LIC>
* URL based: <http://api.worldbank.org/V2/incomeLevels/LIC/countries>

## Query Strings
Requests support the following query strings.

**Date and Date-Range:** Date-range by year, month or quarter that scopes the result-set.

Examples:

  * <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?date=2000>
  * <http://api.worldbank.org/v2/countries/chn;bra/indicators/DPANUSSPB?date=2012M01>

A range is indicated using the colon (:) separator.

Examples:

  * <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?date=2000:2001>
  * <http://api.worldbank.org/v2/countries/chn;bra/indicators/DPANUSSPB?date=2012M01:2012M08>
  * <http://api.worldbank.org/v2/countries/CHL/indicators/DP.DOD.DECD.CR.BC.CD?date=2013Q1:2013Q4>

**Requests additionally support year-to-date values (YTD), which is useful for querying high frequency data.**

* Example: <http://api.worldbank.org/v2/countries/chn/indicators/DPANUSSPB?date=YTD:2013>

**Output Format:** API supports the following four output formats.

* XML format: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?format=xml>
*	JSON format: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?format=json>
*	JSONP format: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?format=jsonP&prefix=Getdata>
  - _Note: For JSONP format, 'prefix' parameter must be specified._
* JSON-stat format: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?format=jsonstat>
    - _Note: Refer <https://json-stat.org/> for more details._

**Download Format:** API supports the following three download formats.

*	CSV Download (Downloads to ZIP file): <http://api.worldbank.org/v2/country/ind/indicator/AG.AGR.TRAC.NO?source=2&downloadformat=csv>
*	XML Download (Downloads to ZIP file): <http://api.worldbank.org/v2/country/ind/indicator/AG.AGR.TRAC.NO?source=2&downloadformat=xml>
*	EXCEL Download (Downloads to ZIP file): <http://api.worldbank.org/v2/country/ind/indicator/AG.AGR.TRAC.NO?source=2&downloadformat=excel>


**Page:** For paging through large result-sets. This allows users to indicate the page number requested from the record-set.

* Example: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?page=2>

**Per_page:** For determining the number of results per page. The default setting is 50 results per page.

* Example: <http://api.worldbank.org/v2/countries/all/indicators/SP.POP.TOTL?per_page=25>

**MRV:** fetches most recent values based on the number specified.

* Example:  <http://api.worldbank.org/v2/country/chn;ago/indicator/AG.AGR.TRAC.NO?mrv=5>

**MRNEV:** For fetching most recent non-empty values based on the number specified.

* Example: <http://api.worldbank.org/v2/country/chn;ago/indicator/AG.AGR.TRAC.NO?mrnev=5>

**Gap-fill:** (Y/N) Works with MRV. Fills values, if not available, by back tracking to the next available period (max number of periods back tracked will be limited by MRV number)

* Example: <http://api.worldbank.org/v2/en/countries/ind;chn/indicators/DPANUSSPF?MRV=7&Gapfill=Y>

**Frequency:** For fetching quarterly (Q), monthly (M) or yearly (Y) values. This feature currently works along with MRV. This query string is useful for querying high frequency data.

* Example: <http://api.worldbank.org/v2/en/countries/ind;chn/indicators/DPANUSSPF?MRV=7&frequency=M>

**Multiple Indicators Usage:** Multiple indicators data can be queried from a single data source by providing the indicator codes separated by `";"` (semicolon), as well as the source ID.

* Example:
  <http://api.worldbank.org/v2/country/chn;ago/indicator/AG.AGR.TRAC.NO;SP.POP.TOTL?source=2>

_Note: A maximum of 60 indicators can be used. A maximum of 1,500 characters are allowed between two back-slashes (/). A maximum of 4,000 characters are allowed in the entire URL._

**Footnote:** For fetching footnote detail in data calls. `"footnote=y"` gives the footnote value for country, indicator and year.

* Example:
  <http://api.worldbank.org/v2/country/chn/indicator/SL.AGR.EMPL.ZS?footnote=y>

## Languages

The following returns all of the supported languages by World bank API v2: <http://api.worldbank.org/v2/languages>

When no language is specified English is assumed. The following languages are available:

| Code | Language |
|--|--|
|en| English |
|es | Spanish |
|fr | French |
|ar | Arabic |
|zh | Chinese |


### Local Languages

Some countries are translated in their local languages. Any call to the API can be prefixed with a language code to retrieve localized results. The following local languages are available:

|Code|Language|
|--|--|
|bg | Bulgarian|
|de	| German|
|hi	|Hindi|
|id	| Indonesian|
|ja	| Japanese|
|km	| Khmer|
|ko	| Korean|
|mk	| Macedonian|
|mn	| Mongolian|
|pl	| Polish|
|pt	| Portuguese|
|ro	| Romanian|
|ru	| Russian|
|sq	| Albanian|
|th	| Thai|
|tr	| Turkish|
|uk	| Ukrainian|
|vi	| Vietnamese|

For example, to retrieve the country name of Vietnam in Vietnamese language you would use the following query: <http://api.worldbank.org/v2/vi/country/vir>

_Note: The translated local language country names are not available for all the countries._

## Delimiters
**Range:** Use a colon ":" to indicate a range (for numeric values only). For example, "5:10" calls numeric value range from 5 to 10.

* Example: <http://api.worldbank.org/v2/country/chn;ago/indicator/AG.AGR.TRAC.NO;SP.POP.TOTL?source=2&date=2000:2010>

** Logical AND:** Use a semicolon ";" to represent logical "AND" For example, "us;ge" calls United States AND Georgia.

* Example: <http://api.worldbank.org/v2/country/us;ge/indicator/AG.AGR.TRAC.NO>

## Examples
Retrieving indicator data about countries is one common use of the API.

For example, the following is a call for 2006 data on the GDP of Brazil:
<http://api.worldbank.org/v2/countries/br/indicators/NY.GDP.MKTP.CD?date=2006>


### Response Format

By default, all requests will respond with valid XML. To receive the response in JSON format, provide "format=json" in any request.

### Sample valid request response:

```xml
<wb:sources xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="30">
<wb:source id="11">
	<wb:name>Africa Development Indicators</wb:name>
	<wb:description/>
	<wb:url/>
	<wb:dataavailability>Y</wb:dataavailability>
	<wb:metadataavailability>Y</wb:metadataavailability>
</wb:source>
```

### Sample invalid request response:

1.
```xml
<wb:error xmlns:wb="http://www.worldbank.org">
<wb:message id="150" key="Language is not yet supported in the API">Response requested in an unsupported language.</wb:message>
</wb:error>
```

2.

```xml
<wb:error xmlns:wb="http://www.worldbank.org">
<wb:message id="120" key="Invalid value">The provided parameter value is not valid</wb:message>
</wb:error>
```

_Note: See "Error Codes" for a full listing of possible errors._


## Limitations
You cannot currently sort any requests. Generally results are returned in a reasonable order (i.e. alpha), but that order cannot be controlled.
