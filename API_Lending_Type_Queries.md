---
title: "API: Lending Type Queries"
output:
  html_document:
    keep_md: true
---
# About Lending Type Queries
The World Bank classifies countries according to the type of lending for which they are eligible through the World Bank. For a description of these categories and how they are set, please visit the [country classification page](http://web.worldbank.org/WBSITE/EXTERNAL/DATASTATISTICS/0,,contentMDK:20420458~menuPK:64133156~pagePK:64133150~piPK:64133175~theSitePK:239419,00.html).

### Sample Request Format: Lending Type Query

Lending type can be used to narrow country or indicator queries.

For example:
1.	To see a list of IDA only countries, use the following call:

    <http://api.worldbank.org/v2/countries?lendingType=IDX>

2.	To list all Lending Types:

    <http://api.worldbank.org/v2/lendingTypes>

### Sample Response Format: Lending Type Query

* XML: <http://api.worldbank.org/v2/lendingTypes?format=xml>

```xml
<wb:lendingTypes xmlns:wb="http://www.worldbank.org" page="1" pages="1" per_page="50" total="4">
  <wb:lendingType id="IBD" iso2code="XF">IBRD</wb:lendingType>
  <wb:lendingType id="IDB" iso2code="XH">Blend</wb:lendingType>
  <wb:lendingType id="IDX" iso2code="XI">IDA</wb:lendingType>
  <wb:lendingType id="LNX" iso2code="XX">Not classified</wb:lendingType>
</wb:lendingTypes>
```

* JSON: <http://api.worldbank.org/v2/lendingTypes?format=json>

```json
 [
   {
     "page": "1",
     "pages": "1",
     "per_page": "50",
     "total": "4"
   },
   [
     {"id": "IBD","iso2code": "XF","value": "IBRD"},
     {"id": "IDB","iso2code": "XH","value": "Blend"},
     {"id": "IDX","iso2code": "XI","value": "IDA"},
     {"id": "LNX","iso2code": "XX","value": "Not classified"}
   ]
 ]
```
