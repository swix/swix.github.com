---
title: SWIX Rest API
layout: default
---

#Introduction to SWIX's REST Api
SWIX's API allows you to access our system programmatically. Before you can acces the SWIX api you must first obtain an API key from us. 

#Query String
##Format
You may use the *format* parameter in all of your calls to the API. The valid values for the format parameter include:
    * json 
    * xml

##Brand Resources
**GET /api/v1/brand/**

**GET /api/v1/brand/{brand_id}/**

##Event Resource
**GET /api/v1/brand/{brand_id}/event/**

**GET /api/v1/brand/{brand_id}/event/{event_id}/**

##Pod Resource
**GET /api/v1/brand/{brand_id}/pod/**

**GET /api/v1/brand/{brand_id}/pod/{pod_id}/**

##Series Data Resource
**GET /api/v1/brand/{brand_id}/pod/{pod_id}/seriesdata/**
