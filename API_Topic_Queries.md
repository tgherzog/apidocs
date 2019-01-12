---
title: Topic API Queries
output:
  html_document:
    keep_md: true
---

Topics are high level categories to which all indicators are mapped. Agriculture & Rural Development, Education, and Trade are examples of topics.

### Sample Topic API Requests ###

To list all topics:

<http://api.worldbank.org/v2/topic>

To list specific topics, separating multiple codes with semicolons (`;`):

<http://api.worldbank.org/v2/topic/5>  
<http://api.worldbank.org/v2/topic/5;11>

To list all indicators under a specified topic:

<http://api.worldbank.org/v2/topic/5/indicator> or:  
<http://api.worldbank.org/v2/indicator?topic=5>

### Sample Response Format: Topic Query

**XML:** <http://api.worldbank.org/v2/topic/>

```xml
<wb:topics xmlns:wb="http://www.worldbank.org"  page="1"  pages="1"  per_page="50"  total="21" >
  <wb:topic id="1" >
    <wb:value>Agriculture &amp; Rural Development</wb:value>
    <wb:sourceNote>For the 70 percent of the world's poor...</wb:sourceNote>
</wb:topic>
  <wb:topic id="2" >
    <wb:value>Aid Effectiveness</wb:value>
```

**JSON:** <http://api.worldbank.org/v2/topic?format=json>

```json
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
       "id":"2"
    }
  ]
]
```
