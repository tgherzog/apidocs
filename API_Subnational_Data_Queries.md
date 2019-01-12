---
title: Subnational Data API Queries
output:
  html_document:
    keep_md: true
---

*TGH: all of the download URLs I tried were broken. Needs review*

Selected indicators are available for "admin level 1" boundaries (the first subnational level) and can be called by the API.  "Admin level 1" boundaries are usually referred to as states, regions, or provinces within a country.   

For example, the indicator Sub-National Malnutrition prevalence, weight for age (% of children under 5), or SN.SH.STA.MALN.ZS, is available for thirteen "admin level1" boundaries in El Salvador.  

Web developers can use this API in real time to support their own applications, so long as they abide by the World Bank"s [Terms of Use](http://data.worldbank.org/summary-terms-of-use).

## Request Format: Subnational API
Requests support the following parameters.

**Date or Date-Range:**

* Users can request data for a desired year by using the query string "date=______".  For example, "date=2007" will pull 2007 data.
  - Example: <http://api.worldbank.org/v2/subnationals/AO.BO/indicators/SN.SH.STA.MALN.ZS?date=2007>
* Users can also request data than spans multiple years. A date-range is indicated using the colon separator ( : ).  For example, "date=2007:2010" will pull data from 2007 to 2010.
  - Example: <http://api.worldbank.org/v2/subnationals/AO.BO/indicators/SN.SH.STA.MALN.ZS?date=2007:2010>

**Response Formats:** The API supports four response formats.

* XML format: <http://api.worldbank.org/v2/subnationals/AO.BO/indicators/SN.SH.STA.MALN.ZS?format=xml>
* JSON format: <http://api.worldbank.org/v2/subnationals/AO.BO/indicators/SN.SH.STA.MALN.ZS?format=json>
* JSONP format: <http://api.worldbank.org/v2/subnationals/AO.BO/indicators/SN.SH.STA.MALN.ZS?format=jsonP&prefix=getdata>
  - _Note: For JSONP format, 'prefix' parameter needs to be specified._
* KML format: <http://api.worldbank.org/v2/subnational/ind/IN.TN?format=kml>

**Download formats:** API supports two download formats.

* CSV Download (Downloads to ZIP file): <https://api.worldbank.org/v2/subnational/ind/IN.TN?downloadformat=csv>
* EXCEL Download (Downloads to ZIP file): <https://api.worldbank.org/v2/subnational/ind/IN.TN?downloadformat=excel>

**Page:** For paging through large result-sets. This allows users to indicate the page number requested from the record-set.

* Example: <http://api.worldbank.org/v2/subnationals/AO.BO;AO.ZA;AO.UI/indicators/SN.SH.STA.MALN.ZS?page=2>

**Per_page:** For determining the number of results per page. The default setting is 50 results per page.

* Example: <http://api.worldbank.org/v2/subnationals/AO.BO;AO.ZA;AO.UI/indicators/SN.SH.STA.MALN.ZS?per_page=25>

**MRV:** For fetching most recent values based on the number specified.

* Example: <http://api.worldbank.org/v2/subnationals/AO.BO;AO.ZA;AO.UI/indicators/SN.SH.STA.MALN.ZS?mrv=2>

## About Subnational List Queries
The following information will appear, when available, in the response when using this Subnational List Query in the World Bank API:

* 3 letter country code of the Subnational
* Name of the country to which Subnational belongs
* Subnational ID
* Subnational Name
* Subnational Alternative Names
* GADM ID and Alternative Names
* GAUL ID
* UNSALB ID
* Longitude
* Latitude

_Note: The above Subnational List Queries are currently available for Admin Level 1 boundaries._

### Sample Request Format: Subnational List Query

To request all subnational level1 locations for all countries:
<http://api.worldbank.org/v2/subnational>

### Sample Response Format: Subnational List Query

**XML:** <http://api.worldbank.org/v2/subnational>

```xml
<wb:subnational xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="100" total="53">
  <wb:country id="USA" name="United States">
    <wb:adminlevel1 id="USA_Wyoming_US.WY_3264_USA051" name="USA, Wyoming" alternativenames="">
      <wb:gadm id="US.WY" name="USA, Wyoming" alternativenames=""/>
      <wb:gaul id="3264" name="USA, Wyoming" alternativenames=""/>
      <wb:unsalb id="USA051" name="USA, Wyoming" alternativenames=""/>
      <wb:longitude/>
      <wb:latitude/>
    </wb:adminlevel1>
    ...
  </wb:country>
</wb:subnational>
```

**JSON:** <http://api.worldbank.org/v2/subnational?format=json>

```json
[
  {
    "page": 1,
    "pages": 1,
    "per_page": "100",
    "total": 53
  },
  [
    {
      "id": "USA",
      "Country Name": "United States",
      "AdminLevel2": null,
      "adminlevel1": [
        {
	  "id": "USA_Wyoming_US.WY_3264_USA051",
	  "SubnationalId": null,
	  "name": "USA, Wyoming",
	  "adminlevel2": [],
	  "alternativenames": "",
	  "gadm": {"GadmId": "US.WY","GadmName": "USA, Wyoming","GadmAlternativeName": ""},
	  "gaul": {"GaulId": "3264","GaulName": "USA, Wyoming","GaulAlternativeName": ""},
	  "unaslab": {"UnslabId": "USA051","UnslabName": "USA, Wyoming","UnslabAlternativeName": ""},
	  "longitude": "",
	  "latitude": ""
	},
	...
      ],
      ...
```

### Single-Country Subnational Requests

To request all available subnational locations for one specified country, simply add either the ISO or World Bank country code to the end of the query.  In this example, the United States is used, with the ISO code "usa".

Example: <http://api.worldbank.org/v2/subnational/usa>

### Multiple-Country Subnational Requests

To request all available subnational locations for multiple specified countries, again add the ISO or World Bank country codes to the end of the query, separated by semicolons (;).  In this example, Angola and India are used with the ISO codes "ago;ind".


Example: <http://api.worldbank.org/v2/subnational/ago;ind>

### Admin-Level-Specific Subnational Requests

1. To retrieve only "admin level 1" data for a specific country: <http://api.worldbank.org/v2/subnational/usa/adminlevel1>
2. To retrieve only "admin level 1" data for a specific countries: <http://api.worldbank.org/v2/subnational/usa;ind/adminlevel/1>
3. To retrieve only "admin level 2" data for a specific country: <http://api.worldbank.org/v2/subnational/usa/adminlevel2>
4. To retrieve only "admin level 2" data for specific countries: <http://api.worldbank.org/v2/subnational/usa;ind/adminlevel/2>

### Geocode Subnational Requests

To retrieve a list of all subnational geocodes: <http://api.worldbank.org/v2/subnational>

To retrieve a subnational detail based on Gadm Code, Gaul code, UnSalb code, and World Bank code:

* Gadm Code: <http://api.worldbank.org/v2/subnational/ind/IN.WB>
* Gaul Code: <http://api.worldbank.org/v2/subnational/ind/1511>
* UnSalb Code: <http://api.worldbank.org/v2/subnational/ind/IND032>
* World Bank Admin Level 1 Code: <http://api.worldbank.org/v2/subnational/ind/IND_West_Bengal_IN.WB_1511_IND032>

## Subnational Indicator Queries

This call will return following information, when available, about subnational indicators.

* Indicator Id
* Indicator Name
* Source ID to which Indicator belongs.
* Source Name to which Indicator belongs.

### Sample Request Format: Subnational Indicator Queries

*TGH: review this section for accuracy and clarity*

1. To request a list of all subnational indicators currently available:
<http://api.worldbank.org/v2/subnational/indicator>
2. To request a specific subnational indicator detail:
<http://api.worldbank.org/v2/subnational/indicator/SN.SH.STA.MALN.ZS> or <http://api.worldbank.org/v2/subnational/indicator[SN.SH.STA.MALN.ZS]>
3. To request all subnational indicators with metadata, you must specify the source:
<http://api.worldbank.org/v2/indicators?source=5>
4. To request a specific subnational indicator with metadata, you must also specify the source:
<http://api.worldbank.org/v2/indicators/SN.SH.STA.MALN.ZS?source=5>

_Note: Subnational indicators are currently only available for "source" 5._

*TGH: this is not true. 41, 45, 38 and 39 are also subnational databases*

### Sample Response Format: Subnational Indicator Queries

**XML:** <http://api.worldbank.org/v2/subnational/indicator>

*TGH: incomplete code snippets need ellipses as shown above*

```xml
</wb:metadata>
<wb:subnationalindicators xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="100" total="319">
<wb:indicator id="SN.SH.STA.MALN.ZS">
<wb:name>
Sub-National Malnutrition prevalence, weight for age (% of children under 5)
</wb:name>
<wb:source id="5">Subnational Malnutrition Database</wb:source>
</wb:indicator>
```

**JSON:** <http://api.worldbank.org/v2/subnational/indicator?format=json>

*TGH: json snippets should be pretty printed and include appropriate snippets, as per above*

```json
[
	{
		"page": 1,
		"pages": 1,
	"per_page": "100",
"total": 5
},
[
	{
		"id": "SN.SH.STA.MALN.ZS",
		"name": "Sub-National Malnutrition prevalence, weight for age (% of children under 5)",
		"source": {
					"id": "5",
					"value": "Subnational Malnutrition Database"
				},
		"sourceNote": null,
		"sourceOrganization": null,
		"topics": null
	}
]
```

## Subnational Indicator Data Queries

Subnational indicator data calls return the following information, when available.

* Indicator Id
* Indicator Name
* Subnational ID
* Subnational Name
* Date (in years)
* Value, i.e. indicator value for given year
* Decimal

### Sample Request Format: Subnational Indicator Data Queries

To request data for a specific indicator in a specific "admin level 1" location, you must provide both a geocode and an indicator code.  In this example, the geocode ARM_Aragatsotn_AM.AG_453_ARM001 requests data for the Armenian state, Aragatsotn, and the indicator code SN.SH.STA.MALN.ZS requests data for the indicator "Sub-National Malnutrition prevalence, weight for age (% of children under 5)".  

<http://api.worldbank.org/v2/subnationals/ARM_Aragatsotn_AM.AG_453_ARM001/indicators/SN.SH.STA.MALN.ZS>

### Sample Response Format: Subnational Indicator Data Queries

**XML**

```xml
<wb:subnationaldata xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="100" total="44" lastupdated="2013-11-26">
<wb:data>
<wb:indicator id="SN.SH.STA.MALN.ZS">
Sub-National Malnutrition prevalence, weight for age (% of children under 5)
</wb:indicator>
<wb:subnational id="453">Armenia, Aragatsotn</wb:subnational>
<wb:date>2012</wb:date>
<wb:value/>
<wb:decimal>0</wb:decimal>
</wb:data>
```

**JSON**

```json
[
	{
		"page": 1,
		"pages": 1,
		"per_page": "100",
		"lastupdated": "2013-11-26",
		"total": 44
	},
	[
		{
			"indicator": 
						{
							"id": "SN.SH.STA.MALN.ZS",
							"value": "Sub-National Malnutrition prevalence, weight for age (% of children under 5)"
						},
			"subnational": 
						{
							"id": "453",
							"value": "Armenia, Aragatsotn"
						},
			"value": "",
			"decimal": "0",
			"date": "2012"
		}
```

### Examples

#### 1. Sample Request Format using Geocodes: Subnational Indicator Data
To retrieve subnational indicator data based on Gadm code, Gaul code, UnSalb code and World Bank code you must provide both the desired location's geocode, as well as the desired indicator code.

  * Gadm Code: <http://api.worldbank.org/v2/subnationals/AO.BO/indicators/SN.SH.STA.MALN.ZS>
  * Gaul Code: <http://api.worldbank.org/v2/subnationals/398/indicators/SN.SH.STA.MALN.ZS>
  * UnSalb: <http://api.worldbank.org/v2/subnationals/AGO001/indicators/SN.SH.STA.MALN.ZS>
  * World Bank Indicator Code: <http://api.worldbank.org/v2/subnational/in.mp;in.up/indicator/SN.SH.STA.MALN.ZS>

#### 2. Sample Request Format: Multiple Subnational Indicators
To retrieve multiple subnational indicator data you must indicate both the indicator codes, separated by semi-colons ( ; ) and the source code.  

Example: <http://api.worldbank.org/v2/subnational/ARM_Ararat_AM.AR_454_ARM002/indicator/SN.SH.STA.MALN.ZS;SN.SH.STA.WAST.ZS?source=5>

#### 3. Sample Request Format: All Subnational Data for a Specified Country and Indicator

To retrieve subnational indicator data for all subnational locations belonging to a single country you must indicate the desired country, year, indicator, and admin level (with "admin level 1" equivalent to states and "admin level 2" equivalent to counties).  This example shows indicator data for indicator SN.SH.STA.MALN.ZS, Sub-National Malnutrition Prevalence, Weight for Age (% of Children under 5), in all admin 1 locations in Argentina in 2005.  

Example: <http://api.worldbank.org/v2/country/arg/subnational/adminlevel/1/indicator/SN.SH.STA.MALN.ZS?date=2005>

#### 4. Sample Request Format: Subnational Data for Multiple Countries

To retrieve subnational data for multiple countries, you must place a semi-colon (;) between the two country codes.  In this example, data is retrieved for SN.SH.STA.MALN.ZS, Sub-National Malnutrition Prevalence, Weight for Age (% of Children under 5), in the subnational locations in the United States and China, for the year 2005, from source 5.  

Example: <http://api.worldbank.org/v2/country/usa;chn/indicator/SN.SH.STA.MALN.ZS?date=2005&source=5>

#### 5. Sample Request Format: Subnational Data for Specific Subnational Location

To retrieve subnational indicator data for one subnational location, you must use an SNCODE (i.e. GAUL, GADM, or UNSALB).  

In this example, GAUL code is called: <http://api.worldbank.org/v2/subnational/IN.WB/indicator/SN.SH.STA.MALN.ZS/?sncode=gaul>

## Subnational KML Download Queries

The Subnational API produces KML definition downloads for subnationals, which can be used in any map-based application that recognizes the KML format.

### Sample Request Format: KML Queries

1. To request subnational KML definitions based on UnSalb code (in this example, for Tamil Nadu, India):
<http://api.worldbank.org/v2/subnationals/ind/IND029?format=kml>
2. To request subnational KML definitions based on Gadm code (in this example, for Tamil Nadu, India):
<http://api.worldbank.org/v2/subnational/ind/IN.TN?format=kml>
3. To request subnational KML definitions based on Gaul code (in this example, for Tamil Nadu, India):
<http://api.worldbank.org/v2/subnational/ind/1508?format=kml>
4. To request KML definitions for all subnational locations in a country (in this example, for India):
<http://api.worldbank.org/v2/subnational/IND/all?format=kml>
5. To request KML definitions for a country (in this example, for India):
<http://api.worldbank.org/v2/country/IND?format=kml>

## Subnational Indicator Data Download Queries

Subnational indicator data can be downloaded in excel and csv formats by typing either "downloadformat=csv" or "downloadformat=excel" into the query string.

**Sample Request Format: Subnational Indicator Data Download Queries**

*TGH: neither of these urls work for me*

* CSV Download: <http://api.worldbank.org/v2/subnationals/398/indicators/SN.SH.STA.MALN.ZS?downloadformat=csv>
* EXCEL Download: <http://api.worldbank.org/v2/subnationals/398/indicators/SN.SH.STA.MALN.ZS?downloadformat=excel>

