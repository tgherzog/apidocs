---
title: "Topic Queries"
output: 
  html_document:
    keep_md: true
---



### About Topic Queries

Topics are high level categories that all to which all indicators are mapped.  Some examples are: Agriculture & Rural Development, Education, and Trade.

### Sample Request Format: Topic Query

1. To list all indicators under a specific topic (in this example the topic is Energy, or ID 5):

    http://api.worldbank.org/v2/topic/5/indicator

2. To list all topics:

    http://api.worldbank.org/v2/topics

3. To get details of one indicator in that particular topic (in this example the topic is Energy, or ID 5. Indicator is Fuel imports (% of merchandise imports) or ID- TM.VAL.FUEL.ZS.UN ):

    http://api.worldbank.org/v2/topic/5/indicator/TM.VAL.FUEL.ZS.UN

### Sample Response Format: Topic Query

<b>XML</b> 
http://api.worldbank.org/v2/topics/

```
<wb:topics xmlns:wb="http://www.worldbank.org"  page="1"  pages="1"  per_page="50"  total="21" >
  <wb:topic id="1" >
    <wb:value>Agriculture &amp; Rural Development</wb:value>
    <wb:sourceNote>For the 70 percent of the world's poor...</wb:sourceNote>
</wb:topic>
  <wb:topic id="2" >
    <wb:value>Aid Effectiveness</wb:value>
```

<b>JSON</b> 
http://api.worldbank.org/v2/topics?format=json

```
[
   {
      "page":1,
      "pages":1,
      "per_page":50,
      "total":21
   },
   [
      {
         "id":"1",
         "value":"Agriculture & Rural Development",
         "sourceNote":"For the 70 percent of the world's poor..."
      },
      {
         "id":"2",

```
