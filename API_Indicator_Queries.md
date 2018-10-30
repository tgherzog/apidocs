---
title: "API: Indicator Queries"
output:
  html_document:
    keep_md: true
---
# About Indicator Queries

Indicators represent data like total population, gross national income, energy use, and many more. Indicator queries return the following information in the response:

* Code
* Name
* Unit
* Source ID
* Source Note
* Source Organization
* Topic ID
* Topic Name

## Sample Request Format: Indicator Query

To request all indicators: <http://api.worldbank.org/v2/indicators>

To request the indicator GDP (Current US$) using its indicator code, "NY.GDP.MKTP.CD": <http://api.worldbank.org/v2/indicators/NY.GDP.MKTP.CD>

## Sample Response Format: Indicator Query

* XML: <http://api.worldbank.org/v2/indicators/NY.GDP.MKTP.CD?format=xml>

```xml
<wb:indicators xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="1">
  <wb:indicator id="NY.GDP.MKTP.CD">
    <wb:name>GDP (current US$)</wb:name>
    <wb:unit></wb:unit>
    <wb:source id="2">World Development Indicators</wb:source>
    <wb:sourceNote>
    GDP at purchaser's prices ...
    </wb:sourceNote>
    <wb:sourceOrganization>
    World Bank national accounts data, and OECD National Accounts data files.
    </wb:sourceOrganization>
    <wb:topics>
      <wb:topic id="19">Climate Change</wb:topic>
      <wb:topic id="3">Economy & Growth</wb:topic>
    </wb:topics>
  </wb:indicator>
</wb:indicators>
```

* JSON: <http://api.worldbank.org/v2/indicators/NY.GDP.MKTP.CD?format=json>

```json
[{
  "page": 1,
  "pages": 1,
  "per_page": "50",
  "total": 1
  },
  [{
    "id": "NY.GDP.MKTP.CD","name":
    "GDP (current US$)",
    "unit": "",
    "source": {
      "id": "2",
      "value": "World Development Indicators"},
    "sourceNote": "GDP at purchaser's prices ... ",
    "sourceOrganization": "World Bank national accounts data, and OECD National Accounts data files.",
    "topics": [
      {"id": "19","value": "Climate Change"},
      {"id": "3","value": "Economy & Growth"}
    ]
  }]
]
```

## Indicators Belonging to Multiple Sources

Sometimes indicators belong to multiple sources. To find an indicator from a specific source, the indicator's source ID must be provided as query parameter.

For example:
* <http://api.worldbank.org/v2/indicators/NY.GDP.MKTP.CD?source=11>
* http://api.worldbank.org/v2/source/11/indicators/NY.GDP.MKTP.CD  
