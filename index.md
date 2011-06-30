---
title: SWIX Rest API
layout: default
---

#Introduction to SWIX's REST Api
SWIX's API allows you to access our system programmatically. Before you can acces the SWIX api you must first obtain an API key from us. 

##Query String
**Format**

You may use the *format* parameter in all of your calls to the API. 

For JSON formatting.

[http://swixapp.com/api/v1/brand/?format=json](http://swixapp.com/api/v1/brand/?format=json)

For XML formatting.

'''html
http://swixapp.com/api/v1/brand/?format=xml
'''

**API Key**

For the read only API we are using API Key authentication. API Key authentication requires you to provide your *API Key* and *User Name* in the query string. 

For example:

[http://swixapp.com/api/v1/brand/?format=json&username=fakeusername&api_key=fakeapikey](http://swixapp.com/api/v1/brand/?format=json&username=fakeusername&api_key=fakeapikey)

##Brand Resources
**GET /api/v1/brand/**

*returns* - All data pertaining to any brands associated with your account. From here you will be able to get the necessary id's required to use the API calls listed below. Including brand id, event id, and pod id.

**GET /api/v1/brand/{brand_id}/**

##Event Resource
**GET /api/v1/brand/{brand_id}/event/**

**GET /api/v1/brand/{brand_id}/event/{event_id}/**

##Pod Resource
**GET /api/v1/brand/{brand_id}/pod/**

**GET /api/v1/brand/{brand_id}/pod/{pod_id}/**

##Series Data Resource
**GET /api/v1/brand/{brand_id}/pod/{pod_id}/seriesdata/**
###Additional Parameters
**fields**

**startdate**

**enddate**
