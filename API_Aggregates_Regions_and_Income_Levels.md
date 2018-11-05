---
title: "API: Aggregates - Regions and Income Levels"
output:
  html_document:
    keep_md: true
---
# About Aggregates - Regions and Income Levels

In several instances in which you typically use a country ISO code it is possible to use regions and income level codes as well.

In the following call, "br" is the ISO2 code for Brazil, and "NY.GDP.MKTP.CD" is the indicator ID for GDP (current US$):
<http://api.worldbank.org/v2/countries/br/indicators/NY.GDP.MKTP.CD>

In this example, you can substitute "br" with list region codes/Incomelevels.

## Region codes
To get list of all region codes: <http://api.worldbank.org/v2/region>


## Income level codes
To get list of all income level codes:
<http://api.worldbank.org/v2/incomelevel>

## Requests by Income Level
To query the GDP (current US$) for all Lower Middle Income (LMC) countries: <http://api.worldbank.org/v2/countries/lmc/indicators/NY.GDP.MKTP.CD>


## Requests by Region
To query the GDP (current US$) for all countries in Latin America and the Caribbean (LAC): <http://api.worldbank.org/v2/countries/lac/indicators/NY.GDP.MKTP.CD>
