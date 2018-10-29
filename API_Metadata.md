---
---

### About Metadata

Metadata is data about data. It provides users with more information
about the data such as where the data comes from, the way in which the
data is measured, and the frequency with which the data is collected,
just to name a few. For example, for the indicator Population (total),
SP.POP.TOTL, the Metadata provides us with this indicator’s long
definition, its sources, its periodicity, its methodology, etc.

### About Metadata Queries

Below is an example response to a Metadata query. Please refer to this
example when reading the query definitions below.

    <wb:metadata xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="5000" total="24">
      <wb:source id="2" name="World Development Indicators">
        <wb:concept id="Country">
          <wb:variable id="JPN"> 
            <wb:metatype id="2-alphacode">JP</wb:metatype>
            <wb:metatype id="BalanceofPaymentsManualinuse">IMF Balance of Payments           
             Manual, 6th edition.</wb:metatype>
            <wb:metatype id="CurrencyUnit">Japanese yen</wb:metatype>
            <wb:metatype id="GovernmentAccountingconcept">Consolidated central                  
             government</wb:metatype>

Query Definitions

The following Metadata queries can be made through the Metadata API.
Detailed explanations and examples are provided for each query type in
the following pages. Please refer to the above response example when
interpreting these explanations.

-   Source: Retrieves information about the source database.

<!-- -->

    <wb:source id="2" name="World Development Indicators">

Examples: World Development Indicators, Doing Business, International
Debt Statistics, etc.

-   Concept: Retrieves source Concepts (also known as “dimensions” or
    combinations of dimensions).  

<!-- -->

    <wb:concept id="Country">

Examples: Country, Series, Country-Time, Country-Series, Time, etc.

-   Metatype: Retrieves the types of Metadata available. Meta types
    belong to Concept; each concept may have one or more Metatypes.

<!-- -->

    <wb:metatype id="2-alphacode">JP</wb:metatype>

Examples: Region, Income Group, Periodicity, Source, etc.

-   Metadata: Retrieves Metadata for any combination of Source, Concept
    and Metatype.

<!-- -->

    <wb:metatype id="2-alphacode">JP</wb:metatype>

Examples: High Income, East Asia & Pacific, United States of America,
2012, etc.

-   Search: Retrieves Metadata by using keywords in the query string.

    <a href="http://api.worldbank.org/v2/sources/2/search/solid%20fuel" class="uri">http://api.worldbank.org/v2/sources/2/search/solid%20fuel</a>

Examples: Solid Fuel, United, South, etc.

-   Download: Retrieves Metatype and their Metadata description in
    downloaded CSV and EXCEL files.

<a href="http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata?downloadformat=excel" class="uri">http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata?downloadformat=excel</a>

Examples: CSV, EXCEL, etc.

### Source Queries

The following Metadata source information will appear, when available,
in the response.

-   Source ID
-   Source Name
-   WB Source Code
-   Source description
-   Source URL
-   Data availability: “Y” means indicator data is available for that
    source; “N” means it is not available.
-   Meta data availability: “Y” means Meta data is available for that
    source; “N” means it is not available.

### Sample Request Format: Source Queries

To request information about all sources:

<a href="http://api.worldbank.org/v2/sources" class="uri">http://api.worldbank.org/v2/sources</a>

### Sample Response Format: Source Queries

XML Request:
<a href="http://api.worldbank.org/v2/sources" class="uri">http://api.worldbank.org/v2/sources</a>

    <wb:sources xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="30">
    <wb:source id="11">
        <wb:name>Africa Development Indicators</wb:name>
           <wb:code>ADI</wb:code>
        <wb:description/>
        <wb:url/>
        <wb:dataavailability>Y</wb:dataavailability>
        <wb:metadataavailability>Y</wb:metadataavailability>
    </wb:source>

JSON Request:
<a href="http://api.worldbank.org/v2/sources?Format=json" class="uri">http://api.worldbank.org/v2/sources?Format=json</a>

    [
       {
          "page":1,
          "pages":1,
          "per_page":50,
          "total":30
       },
       [
          {
             "id":"11",
             "name":"Africa Development Indicators ",
             "code":"ADI"",
             "description": "",
          "url": "",
          "dataavailability": "Y",
          "metadataavailability": "Y"      },

More Examples

To request information about a particular source:
<a href="http://api.worldbank.org/v2/sources/2" class="uri">http://api.worldbank.org/v2/sources/2</a>

### Concept Queries

This call will return the following information, when available, about
concepts of a specific source.

-   Source ID
-   Concept ID
-   Concept Name

Sample Request Formats: Concept Queries

To request a list of all available concepts:
<a href="http://api.worldbank.org/v2/sources/2/concepts/metadata" class="uri">http://api.worldbank.org/v2/sources/2/concepts/metadata</a>

Sample Response Formats: Concept Queries

XML Request:
<a href="http://api.worldbank.org/v2/sources/2/concepts/metadata" class="uri">http://api.worldbank.org/v2/sources/2/concepts/metadata</a>

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

JSON Request:
<a href="http://api.worldbank.org/v2/sources/2/concepts/metadata?format=json" class="uri">http://api.worldbank.org/v2/sources/2/concepts/metadata?format=json</a>

    {"page": 1,"pages": 1,"per_page": "5000","total": 7,"source": [{"id": "2","name": "World Development Indicators","concept": [{"id": "Country","value": "Country"},{"id": "Country-Series","value": "Country-Series"},{"id": "Country-Time","value": "Country-Time"},{"id": "FootNote","value": "FootNote"},{"id": "Series","value": "Series"},{"id": "Series-Time","value": "Series-Time"},{"id": "Time","value": "Time"}]}]} 
    Examples
    To retrieve a specific concept detail for a source (in this example, concept ID is Country and Source is World Development Indicators):
    http://api.worldbank.org/v2/sources/2/concepts/country/metadata

### Metatype Queries

Metatype simply describes the type of metadata. Region, Income Group,
Periodicity, and Source are all examples of Metatypes. Metatype calls
retrieve lists of data types available for the given source. Metatype
calls will return the following information in the response, when
available.

-   Source ID
-   Concept ID
-   Metatype ID
-   Metatype detail

### Sample Request Format: Metatype Queries

To return a list of all available Metatypes for a specific source (in
this case, 2 or World Development Indicators):

<a href="http://api.worldbank.org/v2/sources/2/metatypes" class="uri">http://api.worldbank.org/v2/sources/2/metatypes</a>

### Sample Response Format: Metatype Queries

XML Request:
<a href="http://api.worldbank.org/v2/sources/2/metatypes" class="uri">http://api.worldbank.org/v2/sources/2/metatypes</a>

    <wb:metadata xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="5000" total=" 52">
    <wb:source id="2">
    <wb:concept id="Country">
    <wb:metatype id="2-alphacode">2-alpha code</wb:metatype>
    <wb:metatype id="Alternativeconversionfactor">Alternative conversion factor</wb:metatype>
    <wb:metatype id="BalanceofPaymentsManualinuse">Balance of Payments Manual in use</wb:metatype>
    .
    .
    .
    <wb:metatype id="Topic">Topic</wb:metatype>
    </wb:concept>
    </wb:source>
    </wb:metadata>

JSON Request:
<a href="http://api.worldbank.org/v2/sources/2/metatypes?format=json" class="uri">http://api.worldbank.org/v2/sources/2/metatypes?format=json</a>

    {"page": 1,"pages": 1,"per_page": "5000","total": 52,"source": [{"ETime": null,"STime": null,"id": "2","concept": [{"id": "Country","metatype": [{"id": "2-alphacode","value": "2-alpha code"},{"id": "Alternativeconversionfactor","value": "Alternative conversion factor"},{"id": "BalanceofPaymentsManualinuse","value": "Balance of Payments Manual in use"},. . .

More Examples

The following call retrieves Meta types for a specific concept. In this
example, “Country” is a concept ID for the source “2”.

<a href="http://api.worldbank.org/v2/sources/2/concepts/country/metatypes" class="uri">http://api.worldbank.org/v2/sources/2/concepts/country/metatypes</a>

### Metadata Queries

Metadata can be retrieved for any combination of Source, Concept and
Metatype.

Sample Request Format: Metadata Queries

The following request provides Metadata for Income Group in the United
States and Japan. In this example, “Sources”, “Country”, “Metatypes”,
and “Metadata” are all keywords. “Usa;Jpn” belongs to the concept
“Country” and “incomegroup” belongs to Metatypes.

<a href="http://api.worldbank.org/v2/sources/2/country/usa;jpn/metatypes/IncomeGroup/metadata" class="uri">http://api.worldbank.org/v2/sources/2/country/usa;jpn/metatypes/IncomeGroup/metadata</a>

### Sample Response Format: Metadata Queries

XML Request:
<a href="http://api.worldbank.org/v2/sources/2/country/usa;jpn/metatypes/IncomeGroup/metadata" class="uri">http://api.worldbank.org/v2/sources/2/country/usa;jpn/metatypes/IncomeGroup/metadata</a>

    <wb:metadata xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="5000" total="2">
    <wb:source id="2">
        <wb:concept id="Country">
            <wb:variable id="JPN">
                <wb:metatype id="IncomeGroup">High income: OECD</wb:metatype>
            </wb:variable>
            <wb:variable id="USA">
                <wb:metatype id="IncomeGroup">High income: OECD</wb:metatype>
            </wb:variable>
        </wb:concept>
    </wb:source>
    </wb:metadata>

JSON Request:
<a href="http://api.worldbank.org/v2/sources/2/country/usa;jpn/metatypes/IncomeGroup/metadata?format=json" class="uri">http://api.worldbank.org/v2/sources/2/country/usa;jpn/metatypes/IncomeGroup/metadata?format=json</a>

    {"page": 1,"pages": 1,"per_page": "5000","total": 2,"source": [{"id": "2","name": "World Development Indicators","concept": [{"id": "Country","variable": [{"id": "JPN","metatype": [{"id": "IncomeGroup","value": "High income: OECD"}]},{"id": "USA","metatype": [{"id": "IncomeGroup","value": "High income: OECD"}]}]}]}]}. . . 

More Examples

1.  To retrieve all the Metadata for one Concept (in this case, the
    Concept is Country, and the Country is Japan):

    <a href="http://api.worldbank.org/v2/sources/2/country/jpn/metadata" class="uri">http://api.worldbank.org/v2/sources/2/country/jpn/metadata</a>

2.  To retrieve Metadata for a combination of concepts (In this case,
    one of the Concepts is Country and the other is Series. United
    States and Japan belong to the Concept Country and SP.POP.TOTL
    belongs to Series.):

    <a href="http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata" class="uri">http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata</a>

Search Queries

Metadata API can be used to search Metadata. Search call will return the
following information, when available:

-   Source ID
-   Concept ID and Name
-   Variable ID
-   Metatype ID and detail

Request Format

To search the Metadata (in this example, for search term Solid Fuel):

<a href="http://api.worldbank.org/v2/sources/2/search/solid%20fuel" class="uri">http://api.worldbank.org/v2/sources/2/search/solid%20fuel</a>

Response Format

XML Request:
<a href="http://api.worldbank.org/v2/sources/2/search/solid%20fuel" class="uri">http://api.worldbank.org/v2/sources/2/search/solid%20fuel</a>

    <wb:metadata xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="5000" total="17">
    <wb:source id="2">
        <wb:concept id="Series">
            <wb:variable id=" EG.CFT.ACCS.RU.ZS ">
            <wb:metatype id=" Statisticalconceptandmethodology ">
                Data for access to clean fuels and technologies for cooking are based on the the World Health Organization's (WHO) Global...
            </wb:metatype>
            .
            .
            </wb:variable>
        </wb:concept>
    </wb:source>
    </wb:metadata>

JSON Request:
<a href="http://api.worldbank.org/v2/sources/2/search/solid%20fuel?format=json" class="uri">http://api.worldbank.org/v2/sources/2/search/solid%20fuel?format=json</a>

    {"page": 1,"pages": 1,"per_page": "5000","total": 5,"source": [{"ETime": null,"STime": null,"id": "2","concept": [{"id": "Series","variable": [{"id": "EG.CFT.ACCS.RU.ZS ","name": null,"metatype": [{"id": "Statisticalconceptandmethodology ","value": "Data for access to clean fuels and technologies for cooking are based on the the World Health Organization's (WHO) Global Household Energy Database.."}]},. . . 

### Examples

1.  To perform a search in a specific Concept (In this example, the
    search is within the concept “country” for values that contain
    “united” in its Metatypes):

    <a href="http://api.worldbank.org/v2/sources/2/concepts/country/search/united" class="uri">http://api.worldbank.org/v2/sources/2/concepts/country/search/united</a>

2.  To perform search in specific a Metatype (In this example, the
    search is within the Metatype “region” for values that contain
    “south”):

    <a href="http://api.worldbank.org/v2/sources/2/metatypes/region/search/south" class="uri">http://api.worldbank.org/v2/sources/2/metatypes/region/search/south</a>

### Download Queries

Metadata can be downloaded along with Metatype and their Metadata
description.

Sample Request Format: Download Queries

CSV
<a href="http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata?downloadformat=csv" class="uri">http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata?downloadformat=csv</a>

EXCEL
<a href="http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata?downloadformat=excel" class="uri">http://api.worldbank.org/v2/sources/2/country/usa;jpn/series/SP.POP.TOTL/metadata?downloadformat=excel</a>

Examples

To download a search in specific concept (in this example,
“Country-Series” is a concept and “AFG~1.1\_YOUTH.LITERACY.RATE” is a
value):

<a href="http://api.worldbank.org/v2/Sources/34/Country-Series/AFG~1.1_YOUTH.LITERACY.RATE/metadata?downloadformat=csv" class="uri">http://api.worldbank.org/v2/Sources/34/Country-Series/AFG~1.1_YOUTH.LITERACY.RATE/metadata?downloadformat=csv</a>
