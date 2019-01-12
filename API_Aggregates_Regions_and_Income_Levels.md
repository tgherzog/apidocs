---
title: Aggregate API Queries
output:
  html_document:
    keep_md: true
---

Aggregates---by region, income level or lending group---are also available in the API.
You can retrieve data for aggregates by using the appropriate code where you would
otherwise specify a country.

The following two examples retrieve GDP data for Brazil (BRA)
and the Latin America and Caribbean region as a whole (LCN):

<http://api.worldbank.org/v2/country/BRA/indicator/NY.GDP.MKTP.CD>  
<http://api.worldbank.org/v2/country/LCN/indicator/NY.GDP.MKTP.CD>

## Aggregate Definitions in the API ##

To get the definition list for all Region codes:

**XML**

<http://api.worldbank.org/v2/region?format=xml>

```
<?xml version="1.0" encoding="utf-8"?>
<wb:regions page="1" pages="1" per_page="50" total="48" xmlns:wb="http://www.worldbank.org">
  <wb:region id="">
    <wb:code>AFR</wb:code>
    <wb:iso2code>A9</wb:iso2code>
    <wb:name>Africa</wb:name>
  </wb:region>
  ...
</wb:regions>
```

**JSON**

<http://api.worldbank.org/v2/region?format=json>

```
[
  {
    "page": "1",
    "pages": "1",
    "per_page": "50",
    "total": "48"
  },
  [
    {
      "id": "",
      "code": "AFR",
      "iso2code": "A9",
      "name": "Africa"
    },
    ...
  ]
]
```

To get the list of all Income Level code definitions:  
<http://api.worldbank.org/v2/incomelevel>

To get the list of all Lending Type code definitions:  
<http://api.worldbank.org/v2/lendingtypes>

Or you can retrieve a list of definitions for specific regions, income levels or lending types,
separating multiple codes with semicolons (`;`):

<http://api.worldbank.org/v2/region/LCN>  
<http://api.worldbank.org/v2/incomelevel/UMC>  
<http://api.worldbank.org/v2/lendingtype/IBD;IDB>

Querying a country shows you which aggregate groups it belongs to:

<http://api.worldbank.org/v2/country/BRA>

Conversely, you can apply a filter to see all countries in a specified aggregate:

<http://api.worldbank.org/v2/country?region=LCN>  
<http://api.worldbank.org/v2/country?incomelevel=UMC>  
<http://api.worldbank.org/v2/country?lendingtype=IBD>



