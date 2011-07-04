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

Status Code 500 - Something went wrong on our end and we were not able to get the resource you requested.

##Brand Resources
**GET /api/v1/brand/**

*returns* - All the brands associated with your account. From here you will be able to get the necessary id's required to use the API calls listed below. Including brand id, event id, and pod id.

**GET /api/v1/brand/{brand_id}/**

*returns* - The brand associated with the brand id provided. 

**Fields**

account - The URI to the account that the brand belongs to.<br/>
name - The name of the brand<br/>
created_at - The date and time the band was created at, in the format of iso-8601 (2011-05-24T13:14:57)<br/>
id - The id of the brand.<br/>
logo - <br/>
CSS -  <br/>

##Event Resource
**GET /api/v1/brand/{brand_id}/event/**

*returns* - The events that are associated with the specified band id.

**GET /api/v1/brand/{brand_id}/event/{event_id}/**

*returns* - The specific event that is specified by the event id.

**Fields**

name - <br/>
deleted - <br/>
created_at - <br/>
id - <br/>
brand - <br/>
date - <br/>

##Pod Resource
**GET /api/v1/brand/{brand_id}/pod/**

*returns* - The pods which are associated with the specified brand id.

**GET /api/v1/brand/{brand_id}/pod/{pod_id}/**

*returns* - The specific pod specified by the pod id parameter. 

**Fields**

name - <br/>
created_at - <br/>
uri - <br/>
updated_at - <br/>
id - <br/>
active - <br/>
type - <br/>
brand - <br/>
seriesdata - <br/>

##Series Data Resource
**GET /api/v1/brand/{brand_id}/pod/{pod_id}/seriesdata/**

*returns* - The series data that we have collected for that pod. See the additional parameter below to see more options. 

**Fields**

*twitter*

followers - <br/>
listed - <br/>
friends - <br/>
id - <br/>
statuses - <br/>

###Additional Parameters

**graph**

**fields**

**startdate**

**enddate**
