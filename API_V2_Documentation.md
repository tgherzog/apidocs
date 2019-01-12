---
title: About the Indicators API Documentation
output:
  html_document:
    keep_md: true
---

## About the Indicators API ##

The World Bank Indicators API provides access to nearly 16,000 time series indicators.
Most of these indicators are available online through tools such as [Databank](https://databank.worldbank.org) and
the [Open Data website](https://data.worldbank.org). The API provides programmatic access to this same data.
Many data series date back over 50 years, and can be used to create interesting applications.

The Indicators API provides access to over 45 databases, including:

* [World Development Indicators](http://datatopics.worldbank.org/world-development-indicators)
* [International Debt Statistcs](https://data.worldbank.org/products/ids)
* [Doing Business](http://www.doingbusiness.org/)
* [Human Capital Index](http://www.worldbank.org/en/publication/human-capital)
* [Subnational Poverty](http://databank.worldbank.org/data/reports.aspx?source=subnational-poverty)
* And [many more](https://api.worldbank.org/v2/sources)

The Indicators API documentation, the contents of which you can see to the right side of the page under "Developer Information", explains the different types of call that can be made to the V2 API.  It also explains each call's purpose, how to structure a specific call, what the response looks like, and provides example URL endpoints for API calls. 

Get started by reading about the [Basic Call Structure](https://datahelpdesk.worldbank.org/knowledgebase/articles/898581).


## How to use the V2 Indicators API
Version 2 (V2) of the Indicators API has been released and replaces V1 of the API. V1 API calls will no longer be supported. To use the V2 API, you must place **`v2`** in the call. For example: <http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL>.

The API supports both "http" and "https" protocols.

Besides making calls to the API using an application or custom program, you can also put any of the example API URL endpoints given in the documentation, or your own custom calls, into a web browser and view the results. If you choose to receive the result in JSON format you can use the [JSON View](https://addons.mozilla.org/en-US/firefox/addon/10869/) Firefox plugin for easily viewing JSON results directly in Firefox.

There are also third party applications and libraries that can make using the API easier depending on your objectives. See [Application Showcase](http://data.worldbank.org/developers/application-showcase) for more details.

## API Access / Authentication

API keys and other authentication methods are no longer necessary to access the API.
