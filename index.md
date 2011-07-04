---
title: SWIX Rest API
layout: default
---

#Introduction to SWIX's REST Api
SWIX's API allows you to access our system programmatically. Before you can acces the SWIX api you must first obtain an API key from us. 

##Query String
**Format**

You may use the *format* parameter in all of your calls to the API. 

For JSON formatting:

[http://swixapp.com/api/v1/brand/?format=json](http://swixapp.com/api/v1/brand/?format=json)

For XML formatting:

[http://swixapp.com/api/v1/brand/?format=xml](http://swixapp.com/api/v1/brand/?format=xml)

**API Key**

For the read only API we are using API Key authentication. API Key authentication requires you to provide your *API Key* and *User Name* in the query string. 

For example:

[http://swixapp.com/api/v1/brand/?format=json&username=fakeusername&api_key=fakeapikey](http://swixapp.com/api/v1/brand/?format=json&username=fakeusername&api_key=fakeapikey)

**Status Codes**

In all of the resource below we return status codes to indicate to you the outcome of your request. The general meaning of those status codes are as follows:

Status Code 200 - The resource you specified exists, we successfully retrieved the resource and have returned the results to you.

Status Code 401 - You do not have access or authorization to access the resource you are requesting.

Status Code 404 - The url does not exists. You would get this error if you mistyped 'api/v1/brand/' as 'api/v1/barnd/'

Status Code 410 - You have requested a resource that does not exist. For instance, you are trying to retrieve /api/v1/brand/5987487 and brand with the id of 5987487 does not exist.

Status Code 500 - Something went wrong on our end, and we were not able to get the resource you requested.

##Brand Resources
**GET /api/v1/brand/**

*returns*

All the brands associated with your account. From here you will be able to get the necessary id's required to use the API calls listed below. Including brand id, event id, and pod id.

**GET /api/v1/brand/{brand_id}/**

*returns*

##Event Resource
**GET /api/v1/brand/{brand_id}/event/**

*returns*

**GET /api/v1/brand/{brand_id}/event/{event_id}/**

*returns*

##Pod Resource
**GET /api/v1/brand/{brand_id}/pod/**

*returns*

**GET /api/v1/brand/{brand_id}/pod/{pod_id}/**

*returns*

##Series Data Resource
**GET /api/v1/brand/{brand_id}/pod/{pod_id}/seriesdata/**

*returns*

###Additional Parameters
**fields**

**startdate**

**enddate**
