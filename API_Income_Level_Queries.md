---
title: "API: Income Level Queries"
output:
  html_document:
    keep_md: true
---
# About Income Level Queries
Income levels show the income category of a particular country as identified by the World Bank. Income level queries return a name and an id code. For more information on income level, including the methodology used by the World Bank, please visit [Country Classification](http://data.worldbank.org/about/country-classifications).

## Sample Request Format: Income Level Query

To list all income levels:
<http://api.worldbank.org/v2/incomeLevels>

### Sample Response Format: Income Level Query

* XML: <http://api.worldbank.org/v2/incomeLevels?format=xml>

```xml
<wb:IncomeLevels xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="7">
  <wb:incomeLevel id="HIC" iso2code="XD">High income</wb:incomeLevel>
  ..
  <wb:incomeLevel id="UMC" iso2code="XT">Upper middle income</wb:incomeLevel>
</wb:IncomeLevels>

```

* JSON: <http://api.worldbank.org/v2/incomeLevels?format=json>

```json
[
  {"page": "1",
    "pages": "1",
    "per_page": "50",
    "total": "7"
  },
  [
    {"id": "HIC","iso2code": "XD","value": "High income"},
    {"id": "INX","iso2code": "XY","value": "Not classified"},
    {"id": "LIC","iso2code": "XM","value": "Low income"},
    {"id": "LMC","iso2code": "XN","value": "Lower middle income"},
    {"id": "LMY","iso2code": "XO","value": "Low & middle income"},
    {"id": "MIC","iso2code": "XP","value": "Middle income"},
    {"id": "UMC","iso2code": "XT","value": "Upper middle income"}
  ]
]
```

## Filtering by Income Level
It is not common to query income level directly. It is more common to use income level as a way to delimit other calls. For example:

1. To show a list of countries of the "Lower middle income" level, use the following call: <http://api.worldbank.org/v2/countries?incomeLevel=LMC>

2. To request a list of countries of the "Low income" level, use the following call: <http://api.worldbank.org/v2/countries?incomeLevel=LIC>
