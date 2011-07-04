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
**GET /api/v1/brand/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format

*returns* - All the brands associated with your account. From here you will be able to get the necessary id's required to use the API calls listed below. Including brand id, event id, and pod id.

**GET /api/v1/brand/{brand_id}/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format

*returns* - The brand associated with the brand id provided. 

**Fields**

account - The URI to the account that the brand belongs to.<br/>
name - The name of the brand.<br/>
created_at - The date and time the band was created at, in the format of iso-8601 (2011-05-24T13:14:57)<br/>
id - The id of the brand.<br/>
logo - <br/>
CSS -  <br/>

##Event Resource
**GET /api/v1/brand/{brand_id}/event/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format

*returns* - The events that are associated with the specified band id.

**GET /api/v1/brand/{brand_id}/event/{event_id}/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format

*returns* - The specific event that is specified by the event id.

**Fields**

name - Name of the event.<br/>
deleted - Flag that indicates whether the event is deleted.<br/>
created_at - Date the event was created.<br/>
id - The id of the Event.<br/>
brand - The brand the event belongs to.<br/>
date - The date of the event.<br/>

##Pod Resource
**GET /api/v1/brand/{brand_id}/pod/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format

*returns* - The pods which are associated with the specified brand id.

**GET /api/v1/brand/{brand_id}/pod/{pod_id}/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format

*returns* - The specific pod specified by the pod id parameter. 

**Fields**

name - Pod name<br/>
created_at - Date pod was created.<br/>
uri - URI to the resource this pod uses.<br/>
updated_at - Date pod was updated<br/>
id - The id of the pod.<br/>
active - Flag that tells you if this pod is active.<br/>
type - This will indicate what type of pod this is. This will tell you which format seriesdata will be in.<br/>
brand - The brand this pod belongs to.<br/>
seriesdata - the URI to the series data for this pod<br/>

##Series Data Resource
**GET /api/v1/brand/{brand_id}/pod/{pod_id}/seriesdata/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format, graph, startdate, enddate

*returns* - The series data that we have collected for that pod. See the additional parameter below to see more options. 

**Fields**<br/>
*twitter*

id - <br/>
measured_at - <br/>
updated_at - <br/>
followers - <br/>
listed - <br/>
friends - <br/>
statuses - <br/>

*facebook*

id - <br/>
measured_at - <br/>
updated_at - <br/>
friends - <br/>
wallposts - <br/>

*Blog*

id - <br/>
measured_at - <br/>
updated_at - <br/>
subscribers - <br/>
reach - <br/>
hits - <br/>

*Google Analytics*

newvisits - <br/>
visits - <br/>
pageviews - <br/>
uniquepageviews - <br/>

*Youtube Channel*

subscribers - <br/>
views - <br/>

*Youtube Video*

views - <br/>
favorited - <br/>

*Facebook Group*

members - <br/>

*Facebook App*

monthly_active_users - <br/>
weekly_active_users - <br/>
daily_active_users - <br/>

*Facebook Page*

fans - <br/>

*Flickr User*

photos - <br/>
groups - <br/>
contacts - <br/>

*Flickr Group*

members - <br/>

*Flickr Set*

comments - <br/>

*Identica Profile*

followers - <br/>
friends - <br/>
statuses - <br/>

*Linkedin Profiles*

connections - <br/>
recommendations - <br/>

*Delicious Url*

bookmark - <br/>

*Stumbleupon Url*

reviews - <br/>
rating - <br/>

*Mybloglog Community*

members - <br/>

*Upcoming Event*

attending - <br/>
interested - <br/>

*Metacafe Channel*

views - <br/>
rank - <br/>
subscribers - <br/>
videos - <br/>

*Metacafe Video*

views - <br/>
rank - <br/>
comments - <br/>

*Meetup Group*

members - <br/>
events - <br/>
rating - <br/>

*Meetup Event*

rsvp - <br/>

*Myspace Profile*

friends - <br/>
comments - <br/>

*Vimeo Video*

plays - <br/>
comments - <br/>
rating - <br/>

*Vimeo Channel*

subscribers - <br/>
videos - <br/>

*Vimeo Group*

members - <br/>
videos - <br/>
topics - <br/>
events - <br/>

*Digg Url*

diggs - <br/>
storie - <br/>
comments - <br/>


###Additional Parameters

**graph**

**fields**

**startdate**

**enddate**
