---
title: Metadata API Queries
---

Metadata is data about data. It provides users with more information about the data such as where the data comes from, the way in which the data is measured, and the frequency with which the data is collected, just to name a few. For example, for the indicator Population (total), SP.POP.TOTL, the metadata includes this indicator’s long definition, its sources, its periodicity, its methodology, etc.

## About Metadata Queries

Below is an example response to a Metadata query. Please refer to this example when reading the query definitions below.

```xml
<wb:metadata xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="5000" total="24">
<wb:source id="2" name="World Development Indicators">
<wb:concept id="Country">
<wb:variable id="JPN">
<wb:metatype id="2-alphacode">JP</wb:metatype>
<wb:metatype id="BalanceofPaymentsManualinuse">IMF Balance of Payments Manual, 6th edition.</wb:metatype>
<wb:metatype id="CurrencyUnit">Japanese yen</wb:metatype>
<wb:metatype id="GovernmentAccountingconcept">Consolidated central government</wb:metatype>
```

### Query Definitions

The following metadata queries can be made through the Metadata API. Detailed explanations and examples are provided for each query type. Please refer to the above response example when interpreting these explanations.

**Source:** Retrieves information about the source database.
  - *Examples: World Development Indicators, Doing Business, International Debt Statistics, etc.*

    ```xml
    <wb:source id="2" name="World Development Indicators">
    ```

**Concept:** Retrieves source Concepts (also known as "dimensions" or combinations of dimensions).  

Examples: Country, Series, Country-Time, Country-Series, Time, etc.

```xml
<wb:concept id="Country">
```

**Metatype:** Retrieves the types of Metadata available. Metatypes belong to Concepts; each concept may have one or more Metatypes.

Examples: Region, Income Group, Periodicity, Source, etc.

```xml
<wb:metatype id="2-alphacode">JP</wb:metatype>
```

**Metadata:** Retrieves Metadata for any combination of Source, Concept and Metatype.

Examples: High Income, East Asia & Pacific, United States of America, 2012, etc.

```xml
<wb:metatype id="2-alphacode">JP</wb:metatype>
```

**Search:** Retrieves Metadata by using keywords in the query string.

Examples: Solid Fuel, United, South, etc.  
<http://api.worldbank.org/v2/sources/2/search/solid%20fuel>

**Download:** Retrieves Metatype and their Metadata description in downloaded CSV and EXCEL files.

- Examples: CSV, EXCEL, etc.
- <http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata?downloadformat=excel>


## Source Queries

The following data source information will appear, when available, in the response.

* Date last updated
* Source ID
* Source Name
* WB Source Code
* Source description
* Source URL
* Data availability: `Y` means indicator data is available for that source; `N` means it is not available.
* Meta data availability: `Y` means metadata is available for that source; `N` means it is not available.
* Number of concepts

### Sample Request Format: Source Queries

To request information about all sources:
<http://api.worldbank.org/v2/sources>

### Sample Response Format: Source Queries

* XML Request: <http://api.worldbank.org/v2/sources>

  ```xml
  <wb:sources xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="42">
  <wb:source lastupdated="2013-02-22" id="11">
  	<wb:name>Africa Development Indicators</wb:name>
          <wb:code>ADI</wb:code>
  	<wb:description/>
  	<wb:url/>
  	<wb:dataavailability>Y</wb:dataavailability>
  	<wb:metadataavailability>Y</wb:metadataavailability>
    <wb:concepts>3</wb:concepts>
  </wb:source>
  ...
  </wb:sources>

  ```

* JSON Request: <http://api.worldbank.org/v2/sources?format=json>

  ```json
  [
    {
      "page":1,
      "pages":1,
      "per_page":50,
      "total":42
    },
    [
      {
        "id":"11",
        "name":"Africa Development Indicators ",
        "description": "",
        "url": "",
        "dataavailability": "Y",
        "metadataavailability": "Y"      
      },
    ...
    ]
  ]
  ```

* More examples
  - To request information about a particular source:  
    <http://api.worldbank.org/v2/sources/2>

## Concept Queries
This call will return the following information, when available, about concepts of a specific source.

* Source ID
* Source Name
* Concept ID
* Concept Name

### Sample Request Formats: Concept Queries
To retrieve a list of concepts for a source:
<http://api.worldbank.org/v2/sources/2/concepts>

To request a list of all available concepts:  
<http://api.worldbank.org/v2/sources/2/concepts/metadata>

### Sample Response Formats: Concept Queries

**XML:** <http://api.worldbank.org/v2/sources/2/concepts/metadata>

```xml
<wb:metadata xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="5000" total="7">
<wb:source id="2" name="World Development Indicators">
    <wb:concept id="Country">Country</wb:concept>
    <wb:concept id="Country-Series">Country-Series</wb:concept>
    <wb:concept id="Country-Time">Country-Time</wb:concept>
    <wb:concept id="FootNote">FootNote</wb:concept>
    <wb:concept id="Series">Series</wb:concept>
    <wb:concept id="Series-Time">Series-Time</wb:concept>
    <wb:concept id="Time">Time</wb:concept>
</wb:source>
</wb:metadata>
```

**JSON:** <http://api.worldbank.org/v2/sources/2/concepts/metadata?format=json>

```json
  {
    "page": 1,
    "pages": 1,
    "per_page": "5000",
    "total": 7,
    "source": [{
      "id": "2",
      "name": "World Development Indicators",
      "concept": [
        {"id": "Country","value": "Country"},
        {"id": "Country-Series","value": "Country-Series"},
        {"id": "Country-Time","value": "Country-Time"},
        {"id": "FootNote","value": "FootNote"},
        {"id": "Series","value": "Series"},
        {"id": "Series-Time","value": "Series-Time"},
        {"id": "Time","value": "Time"}
      ]
    }]
  }
```

* More examples
  - To retrieve a specific concept detail for a source (in this example, concept ID is `country` and Source is `2` - World Development Indicators):  
    <http://api.worldbank.org/v2/sources/2/concepts/country/metadata>

## Metatype Queries

Metatype simply describes the type of metadata. Region, Income Group, Periodicity, and Source are all examples of Metatypes. Metatype calls retrieve lists of data types available for the given source. Metatype calls will return the following information in the response, when available.

* Source ID
* Concept ID
* Metatype ID
* Metatype Detail (name and description)

### Sample Request Format: Metatype Queries

To return a list of all available Metatypes for a specific source (in this case, `2` or World Development Indicators):  
<http://api.worldbank.org/v2/sources/2/metatypes>

### Sample Response Format: Metatype Queries

**XML:** <http://api.worldbank.org/v2/sources/2/metatypes>

```xml
  <wb:metadata xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="5000" total=" 52">
    <wb:source id="2">
      <wb:concept id="Country">
        <wb:metatype id="2-alphacode">
          <wb:value>2-alpha code</wb:value>
          <wb:description>2-alpha code</wb:description>
        </wb:metatype>
        <wb:metatype id="Alternativeconversionfactor">
          <wb:value>Alternative conversion factor</wb:value>
          <wb:description>Alternative conversion factor</wb:description>
        </wb:metatype>
        ...    
      </wb:concept>
      ...
    </wb:source>
  </wb:metadata>
```

**JSON:** <http://api.worldbank.org/v2/sources/2/metatypes?format=json>

```json
  {
    "page": 1,
    "pages": 1,
    "per_page": "5000",
    "total": 52,
    "source": [{
      "ETime": null,
      "STime": null,"id":
      "2",
      "concept": [
        {"id": "Country","metatype": [
          {"id": "2-alphacode","value": "2-alpha code"},
          {"id": "Alternativeconversionfactor","value": "Alternative conversion factor"},
          {"id": "BalanceofPaymentsManualinuse","value": "Balance of Payments Manual in use"}
        ]}
      ]
    }]
  }
```

* More examples:
  - The following call retrieves metatypes for a specific concept. In this example, `country` is a concept ID for the source `2`:  
    <http://api.worldbank.org/v2/sources/2/concepts/country/metatypes>

## Metadata Queries

Metadata can be retrieved for any combination of Source, Concept and Metatype.

### Sample Request Format: Metadata Queries

The following request provides metadata for Income Group in the United States and Japan. In this example, `sources`, `country`, `metatypes`, and `metadata` are all keywords. `usa;jpn` belongs to the concept `country` and `incomegroup` belongs to `metatypes`.

<http://api.worldbank.org/v2/sources/2/country/usa;jpn/metatypes/incomegroup/metadata>

### Sample Response Format: Metadata Queries

**XML:** <http://api.worldbank.org/v2/sources/2/country/usa;jpn/metatypes/incomegroup/metadata>

```xml
  <wb:metadata xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="5000" total="2">
    <wb:source id="2" name="World Development Indicators">
        <wb:concept id="Country">
            <wb:variable id="JPN">
                <wb:metatype id="IncomeGroup">High income</wb:metatype>
            </wb:variable>
            <wb:variable id="USA">
                <wb:metatype id="IncomeGroup">High income</wb:metatype>
            </wb:variable>
        </wb:concept>
    </wb:source>
  </wb:metadata>
```

**JSON:** <http://api.worldbank.org/v2/sources/2/country/usa;jpn/metatypes/incomegroup/metadata?format=json>

```json
    {
      "page": 1,
      "pages": 1,
      "per_page": "5000",
      "total": 2,
      "source": [{
        "id": "2",
        "name": "World Development Indicators",
        "concept": [{
          "id": "Country",
          "variable": [
            {
            "id": "JPN",
            "metatype": [{
            "id": "IncomeGroup",
          "value": "High income: OECD"
        }]
          },
            {
              "id": "USA","metatype": [{
              "id": "IncomeGroup",
              "value": "High income: OECD"}]
            }]
        }]
      }]
    }
    ...
```

* More examples:
  - To retrieve all the metadata for one concept (in this case, the concept is `country`, and the country is `jpn` (Japan)):  
     <http://api.worldbank.org/v2/sources/2/country/jpn/metadata>
  - To retrieve metadata for a combination of concepts (in this case,
    one of the concepts is `country` and the other is `series`. United
    States and Japan belong to the concept `country` and SP.POP.TOTL
    belongs to `series`.):  
    <http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata>

## Search Queries

The Metadata API can be used to search metadata. Search calls will return the following information, when available:

* Source ID
* Concept ID
* Variable ID
* Metatype ID and detail

### Request Format
To search metadata (in this example, for search term Solid Fuel):  
<http://api.worldbank.org/v2/sources/2/search/solid%20fuel>

_Note: To add spaces in search terms, use `%20` as in the example above._

### Response Format

**XML:** <http://api.worldbank.org/v2/sources/2/search/solid%20fuel>

```xml
  <wb:metadata page="1" pages="1" per_page="5000" total="17" xmlns:wb="http://www.worldbank.org">
    <wb:source id="2">
      <wb:concept id="Series">
          <wb:variable id="EG.CFT.ACCS.RU.ZS">
            <wb:metatype id=" Statisticalconceptandmethodology">
                Data for access to clean fuels and technologies for cooking are based on the the World Health Organization's (WHO) Global ...
            </wb:metatype>
          </wb:variable>
          ...
      </wb:concept>
    </wb:source>
  </wb:metadata>
```

**JSON:** <http://api.worldbank.org/v2/sources/2/search/solid%20fuel?format=json>

```json
    {
      "page": 1,
      "pages": 1,
      "per_page": "5000",
      "total": 17,
      "source": [
        {
          "ETime": null,
          "STime": null,
          "id": "2",
          "concept": [
            {
              "id": "Series",
              "variable": [
                {
                  "id": "EG.CFT.ACCS.RU.ZS ",
                  "name": null,
                  "metatype": [
                    {
                      "id": "Statisticalconceptandmethodology ",
                      "value": "Data for access to clean fuels and technologies for cooking are based on the the World Health Organization's (WHO) Global Household Energy Database..",
                    }
                  ]
                },
                ...
              ]
            }
          ]
        }
      ]
    }
```

* More examples
  - To perform a search within a specific concept, for example, to search within the concept "country" for values that contain "united" in its Metatypes:  
     <http://api.worldbank.org/v2/sources/2/concepts/country/search/united>
  - To perform search within a specific metatype, for example, to search within the Metatype "region" for values that contain "south":  
     <http://api.worldbank.org/v2/sources/2/metatypes/region/search/south>

## Download Queries

Metadata can be downloaded along with Metatype and their Metadata description.

### Sample Request Format: Download Queries

* CSV:
  <http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata?downloadformat=csv>
* EXCEL:
<http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata?downloadformat=excel>
* Examples:
  - To download the results of a search within a specific concept, for example, "Country-Series" is a concept and "AFG~1.1\_YOUTH.LITERACY.RATE" is a value:
    <http://api.worldbank.org/v2/Sources/34/Country-Series/AFG~1.1_YOUTH.LITERACY.RATE/metadata?downloadformat=csv>
