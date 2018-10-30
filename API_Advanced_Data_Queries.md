---
title: "API: Advanced Data Queries"
output:
  html_document:
    keep_md: true

---
# About Advanced Data Queries (BETA)

Below is an example response to an Advanced Data Query.  Please refer to this example when reading the query definitions below:
```xml
<wb:data xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="1" lastupdated="2011-12-15">
  <wb:source id="2" name="World Development Indicators">
    <wb:data>
      <wb:variable name="Country" id="IND">India</wb:variable>
      <wb:variable name="Series" id="SP.POP.TOTL">Population, total</wb:variable>
      <wb:variable name="Time" id="YR2011">2011</wb:variable>
      <wb:value>1241491960</wb:value>
    </wb:data>
  </wb:source>
</wb:data>
```

## Query Definitions

Advanced Data Queries allow you to retrieve data for any combination of multidimensional data sources and multidimensional concepts.  The following Advanced Data Queries can be made through the Metadata API. Detailed explanations and examples are provided for each query type in the following pages. Please refer to the above response example when interpreting these explanations.

* **Source:** Retrieves information about the source database.
  - *Examples: World Development Indicators, Doing Business, International Debt Statistics, etc.*
  ```xml
  <wb:source id="2" name="World Development Indicators">
  ```

* **Concept:** Retrieves source Concepts (also known as "Dimensions" or combinations of dimensions).  
  - *Examples: Country, Series, Time, etc.*
  ```xml
    <wb:variable name="Country">
  ```

* **Concept Variables:** Retrieves source Concept Variables (also known as "Dimension Variables"). Concept Variables belong to Concepts.
  - *Examples: High Income, East Asia & Pacific, United States of America, 2012, etc.*
  ```xml
    <wb:variable name="Country" id="IND">India</wb:variable>
  ```


* **Data:** Retrieves data for any combination of Source and Concepts.
  - *Examples: 12341491960, etc.*
   ```xml
    <wb:value>1241491960</wb:value>
   ```


## Source Queries

The following data source information will appear, when available, in the response.
* Source ID
* Source Name
* WB Source Code
* Source description
* Source URL
* Data availability: "Y" means indicator data is available for that source; "N" means it is not available.
* Meta data availability: "Y" means Meta data is available for that source; "N" means it is not available.

### Sample Request Format: Source Queries

To request information about all sources:
<http://api.worldbank.org/v2/sources>

### Sample Response Format: Source Queries

* XML Request: <http://api.worldbank.org/v2/sources>
```xml
<wb:sources xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="42">
<wb:source id="11">
	<wb:name>Africa Development Indicators</wb:name>
       <wb:code>ADI</wb:code>
	<wb:description/>
	<wb:url/>
	<wb:dataavailability>Y</wb:dataavailability>
	<wb:metadataavailability>Y</wb:metadataavailability>
</wb:source>
```

* JSON Request: <http://api.worldbank.org/v2/sources?Format=json>
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
    }
  ]
]
```

* Examples
To request information about a particular source: <http://api.worldbank.org/v2/sources/57>

## Concept Queries
This call will return the following information, when available, about concepts of a specific source.
* Source ID
* Concept ID
* Concept Name

### Sample Request Formats: Concept Queries
To request a list of all available concepts:
<http://api.worldbank.org/v2/sources/57/concepts/data>

Sample Response Formats: Concept Queries

* XML Request: <http://api.worldbank.org/v2/sources/57/concepts/data?format=xml>
```xml
<wb:data xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="4">
  <wb:source id="57" name="WDI Database Archives">
    <wb:concept id="Country">Country</wb:concept>
    <wb:concept id="Series">Series</wb:concept>
    <wb:concept id="Time">Time</wb:concept>
    <wb:concept id="Version">Version</wb:concept>
  </wb:source>
</wb:data>
```

* JSON Request: <http://api.worldbank.org/v2/sources/57/concepts/data?format=json>
```json
{
  "page":1,
  "pages":1,
  "per_page":50,
  "total":4,
  "source":[{
    "id":"57",
    "name":"WDI Database Archives",
    "concept":[
      {"id":"Country","value":"Country"},
      {"id":"Series","value":"Series"},
      {"id":"Time","value":"Time"},
      {"id":"Version","value":"Version"}
    ]
  }]
}
```

* Examples
To retrieve a specific concept detail for a source (in this example, Concept ID is "Country" and Source is "WDI Database Archives" or source  57): <http://api.worldbank.org/v2/sources/57/concepts/Country/data>

## Concept Variables Queries
This call will return the following information, when available, about concept variables of a specific source.
* Source ID
* Concept ID
* Concept Name
* Variable ID
* Variable Name

### Sample Request Formats: Concept Variables Queries
To request a list of all available variables in a concept:
<http://api.worldbank.org/v2/sources/57/Country/data>

### Sample Response Formats: Concept Queries
* XML Request: <http://databankapiqa.worldbank.org/v2/sources/57/Country/data?format=xml>
```xml
<wb:data xmlns:wb="http://www.worldbank.org" page="1" pages="6" per_page="50" total="290">
<wb:source id="57" name="WDI Database Archives">
<wb:concept id="country" name="country">
<wb:variable id="ABW">Aruba</wb:variable>
<wb:variable id="AFG">Afghanistan</wb:variable>
<wb:variable id="AGO">Angola</wb:variable>
<wb:variable id="ALB">Albania</wb:variable>
```

* JSON Request: <http://api.worldbank.org/v2/sources/57/country/data?format=json>
```json
 {
   "page":1,
   "pages":6,
   "per_page":50,
   "total":290,
   "source":[{
     "id":"57",
     "name":"WDI Database Archives",
     "concept":[{
       "id":"country",
       "name":"country",
       "variable":[
         {"id":"ABW","value":"Aruba"},
         {"id":"AFG","value":"Afghanistan"},
         {"id":"AGO","value":"Angola"},
         {"id":"ALB","value":"Albania"}]
     }]
   }]
 }
```

* Examples
To retrieve a specific concept variable detail for a source (in this example, concept ID is "Country", Country variable id is "ALB" and Source is WDI Database Archivesor source 57): <http://api.worldbank.org/v2/sources/57/Country/ALB/data>


## Advanced Data Queries
Data can be retrieved for any combination of Source and Concepts
Sample Request Format: Advanced Data Queries
The following request provides data for Country ALB (Albania), Series AG.AGR.TRAC.NO ( Agricultural machinery, tractors), Time 1975, Version 1997 Apr.

In this example, "Sources", "Country", "Series", "Time", and "Version" are all keywords: 	
<http://api.worldbank.org/v2/sources/57/Country/ALB/Series/AG.AGR.TRAC.NO/Time/yr1975/Version/199704>

### Response Format: Advanced Data Queries

* XML Request:   <http://api.worldbank.org/v2/sources/57/Country/ALB/Series/AG.AGR.TRAC.NO/Time/yr1975/Version/199704/data?format=xml>
```XML
<wb:data xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="1" lastupdated="2017-07-13">
  <wb:source id="57" name="WDI Database Archives">
    <wb:data>
      <wb:variable concept="Country" id="ALB">Albania</wb:variable>
      <wb:variable concept="Version" id="199704">1997 Apr</wb:variable>
      <wb:variable concept="Series" id="AG.AGR.TRAC.NO">Agricultural machinery, tractors</wb:variable>
      <wb:variable concept="Time" id="YR1975">1975</wb:variable>
      <wb:value>9620</wb:value>
    </wb:data>
  </wb:source>
</wb:data>
```

* JSON
Request:   <http://api.worldbank.org/v2/sources/57/Country/ALB/Series/AG.AGR.TRAC.NO/Time/all/Version/199704/data?format=json>
```json
{
  "page":1,
  "pages":2,
  "per_page":50,
  "total":67,
  "lastupdated":"2017-07-13",
  "source":{
    "id":"57",
    "name":"WDI Database Archives",
    "data":[
      {"variable":[
        {"concept":"Country","id":"ALB","value":"Albania"},
        {"concept":"Version","id":"199704","value":"1997 Apr"},
        {"concept":"Series","id":"AG.AGR.TRAC.NO","value":"Agricultural machinery, tractors"},
        {"concept":"Time","id":"YR2016","value":"2016"}],
        "value":null},
      {"variable":[
        {"concept":"Country","id":"ALB","value":"Albania"},
        {"concept":"Version","id":"199704","value":"1997 Apr"},
        {"concept":"Series","id":"AG.AGR.TRAC.NO","value":"Agricultural machinery, tractors"}]}
      ]
    }
  }
```

* Examples
To retrieve all the data for one or more Concepts (in this case, the Concept is "time" and the value is "all"): <http://api.worldbank.org/v2/sources/57/Country/ALB/Series/AG.AGR.TRAC.NO/Time/all/Version/199704/data>

## Jsonstat Queries (BETA)
Data can be retrieved in Jsonstat format.

### Sample Request Format: Jsonstat Queries
<http://api.worldbank.org/v2/sources/57/Country/ALB/Series/AG.AGR.TRAC.NO/Time/all/Version/199704/data?format=jsonstat>
