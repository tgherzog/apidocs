---
title: SDMX API Queries
output:
  html_document:
    keep_md: true

---

Use SDMX REST API to programmatically access databases that are available in Databank. At present the WDI (World Development Indicators) dataset is available through API, and we are planning to add more datasets soon. If you are interested in a specific dataset that are currently available in <a href="http://databank.worldbank.org/data/home.aspx">Databank</a>, please let us know by email at data@worldbank.org.

In SDMX API, users can give various dimensions as a parameter in the URL like series code, country code, or frequency and time range etc., and result data can be downloaded as XML or JSON.

## WDI (World development Indicators)

World Development Indicators (WDI) is the primary World Bank collection of development indicators, compiled from officially recognized international sources. It presents the most current and accurate global development data available, and includes national, regional and global estimates. WDI data can be downloaded by specifying values for the below dimensions 

### Series
Series code. Refer WDI DSD for list of series name and code 

### Country
ISO Country code

### Time
Specify a single or range of year

## Limitation on Data Request 

In order to avoid server overload, the request for entire database is not possible in one query so the data calls are restricted to 15000 data points per call which includes null values too. 

## Basic Call structure

There are two types of request: One request type is to retrieve the metadata and other is to retrieve data. The following SDMX response formats are supported in this API.

### SDMX-ML 2.1 generic schema: 
This is the default format. Please note that generic format output size will be more when compare to other formats.

### SDMX-ML 2.1 structure specific schema: 
The structure specific schema is more suited for processing of large data. To get the response in this format, modify the HTTP request header field  "Accept: application/vnd.sdmx.structurespecificdata+xml" on the SDMX data query request. 

### JSON Format: 
To get the data in JSON format, modify the HTTP request header field "Accept: application/vnd.sdmx.data+json;version=1.0.0-wd" on the SDMX data query request.

## Metadata request
This section explains the call to get DataFlow, Code List and DSD.

### Data Flow 
This end-point retrieves the unique dataset code for World bank dataset.  

* *URL:* 
  
  
    <http://api.worldbank.org/v2/sdmx/rest/dataflow>
    

* *Method:* 
    
    
    GET 
    

* *URL Parameter:* 
    
    
    None 
    
* *Response Format:*
    
    
    XML 
    
* *Success Response:*
    
    
    HTTP Response Status Code: 200
    
    Content: The response has the data flow code to access the World Bank datasets

* *Sample request and Output*

    + URL
    <http://api.worldbank.org/v2/sdmx/rest/dataflow>
    
    + Response
    ![Data Flow Sample Output](https://databank.worldbank.org/data/download/site-content/kb/api/Data_Flow_Sample_Output.png)
    
### Code List 

<b>This endpoint retrieves the code list for the WDI dataset. </b>

* URL: 
    
    
    <http://api.worldbank.org/v2/sdmx/rest/codelist/wb>
    
* *Method:* 

    
    GET 
     	
* *URL Parameter:*

    
    None 
    	
* *Response Format:*

    
    XML 
     	
* *Success Response:*

    
        HTTP Response Status Code: 200  
        Content: The response has the code list available for various dimension in WDI dataset.
        
* *Sample request and Output*
    
      + URL
      <http://api.worldbank.org/v2/sdmx/rest/codelist/wb>
    
      + Response:
      ![Code List Sample Output](https://databank.worldbank.org/data/download/site-content/kb/api/Code_List_Sample_Output.png)
    
     
### Data Structure Definition (DSD) 

This API retrieves the Data Structure Definition (DSD) for the WDI dataset  

* *URL:* 
  
  
    <http://api.worldbank.org/v2/sdmx/rest/datastructure/wb>
    
* *Method:* 
  
  
    GET 
     	
* *URL Parameter:*
  
  
    None 
    	
* *Response Format:* 
    
    
    XML 
     	
* *Success Response:*
    
    
        HTTP Response Status Code: 200  
        Content: The response has the Data Structure Definition (DSD) for WDI dataset

* *Sample request and Output*

    + URL
    <http://api.worldbank.org/v2/sdmx/rest/datastructure/wb>
    
    + Response
    ![DSD Sample Response](https://databank.worldbank.org/data/download/site-content/kb/api/DSD_Sample_Output.png)

    
* *Error Response:*

    The following error response is returned for invalid parameter value. 
    
        HTTP Response Status Code: 404 
        Content: Invalid structure code 
        
    ![DSD Sample Error Response](https://databank.worldbank.org/data/download/site-content/kb/api/DSD_Sample_Output_Error.png)
 

# Data Request

Data calls are used to download data in Generic, Compact and JSON format. Users can request data for a country, series over a period, however data points in a single query cannot exceed more than 15000 data points. 
In data calls, the dimensions are separated by "." dot as shown below

* *URL:*


    http://api.worldbank.org/v2/sdmx/rest/data/<dataset%20id>/<FREQ>.<SERIES>.<COUNTRY>/?startperiod=<YEAR>&endPeriod=<YEAR>

* *Method:* 

    
    GET

* *URL Parameter:*
    
    + Dataset id: Dataset id, "WDI"
    
    + Freq:  The possible value for frequency is "A". If no value is specified, it is considered as all frequencies.  
    
    + Series: Series code. Refer WDI DSD for list of series name and code
    
    + Country: ISO Country code 
    
    + StartPeriod: This is a year parameter and can have the value from 1960 onwards. If ignored, data for available years will be returned. 
    
    + EndPeriod: This is a year parameter and can have the value from 1960 onwards. If ignored, the data available from the start period to the latest available years will be returned. 

* *Response Format:*

    
    XML- SDMX-ML 2.1 generic schema, XML- SDMX-ML 2.1 structure specific schema or JSON 

* *Success Response:* 


        HTTP Response Status Code: 200  
        Content: The response has the following information. 
            - Series
            - Country
            - Time

### Sample Request: 

To request one country, one series  and a year

    <http://api.worldbank.org/v2/sdmx/rest/data/WDI/A.SP_POP_TOTL.AFG/?startperiod=2011&endPeriod=2011>

To request all countries, one series and a year

    <http://api.worldbank.org/v2/sdmx/rest/data/WDI/A.SP_POP_TOTL./?startperiod=2011&endPeriod=2011>

To request all series, one country and a year 

    <http://api.worldbank.org/v2/sdmx/rest/data/WDI/A..AFG/?startperiod=2011&endPeriod=2011>


To request one country, one series and a range of year

    <http://api.worldbank.org/v2/sdmx/rest/data/WDI/A.SP_POP_TOTL.AFG/?startperiod=2010&endPeriod=2015>



<b>Sample Response Format: </b>


SDMX-ML 2.1 generic schema

![](https://databank.worldbank.org/data/download/site-content/kb/api/generic_schema.png)


SDMX-ML 2.1 structure specific schema

![](https://databank.worldbank.org/data/download/site-content/kb/api/structure_specific_schema.png)


JSON Format

![](https://databank.worldbank.org/data/download/site-content/kb/api/json_format.png)


The response contains the result value of the Country, Series, Time and Frequency combination.
If we are not specifying any of the dimension in the request URL, all the data related to that dimension will be retrieved in relation with the other dimensions.


Error Response: 

![ ](https://databank.worldbank.org/data/download/site-content/kb/api/error_response.png)

