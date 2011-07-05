---
title: SWIX Rest API
layout: default
---

#Introduction to SWIX's REST Api
SWIX's API allows you to access our system programmatically. Before you can acces the SWIX api you must first obtain an API key from us. 

##Query String
**Format**<br/>
Available Values: XML, JSON

You may use the *format* parameter in all of your calls to the API. 

For JSON formatting:

[http://swixapp.com/api/v1/brand/?format=json](http://swixapp.com/api/v1/brand/?format=json)

For XML formatting:

[http://swixapp.com/api/v1/brand/?format=xml](http://swixapp.com/api/v1/brand/?format=xml)

**API Key**

For the read only API we are using API Key authentication. API Key authentication requires you to provide your *API Key* and *User Name* in the query string. 

For example:

[http://swixapp.com/api/v1/brand/?format=json&username=fakeusername&api_key=fakeapikey](http://swixapp.com/api/v1/brand/?format=json&username=fakeusername&api_key=fakeapikey)

##Status Codes

In all of the resource below we return status codes to indicate to you the outcome of your request. The general meaning of those status codes are as follows:

Status Code 200 - The resource you specified exists, we successfully retrieved the resource and have returned the results to you.

Status Code 401 - You do not have access or authorization to access the resource you are requesting.

Status Code 404 - The url does not exists. You would get this error if you mistyped 'api/v1/brand/' as 'api/v1/barnd/'

Status Code 410 - You have requested a resource that does not exist. For instance, you are trying to retrieve /api/v1/brand/5987487 and brand with the id of 5987487 does not exist.

Status Code 500 - Something went wrong on our end and we were not able to get the resource you requested.

##Brand Resources
**GET /api/v1/brand/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: List of Brands

*returns* - All the brands associated with your account. From here you will be able to get the necessary id's required to use the API calls listed below. Including brand id, event id, and pod id.

Example:<br/>
/api/v1/brand/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1065033.js"> </script>

**GET /api/v1/brand/{brand_id}/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: A Brand

*returns* - The brand associated with the brand id provided. 

**Fields**

account - The URI to the account that the brand belongs to.<br/>
name - The name of the brand.<br/>
created_at - The date and time the band was created at, in the format of iso-8601 (2011-05-24T13:14:57).<br/>
id - The id of the brand.<br/>
logo - path to your logo.<br/>
CSS -  path to your CSS.<br/>
event - List of events that belong to the brand<br/>
pod - List of pods that belong to the brand<br/>

Example:<br/>
/api/v1/brand/55/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1065046.js"> </script>

##Event Resource
**GET /api/v1/brand/{brand_id}/event/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: List of Events

*returns* - The events that are associated with the specified band id.

Example: <br/>
/api/v1/brand/55/event/?format=json&username=your_username&api_key=your_password<br/>

<script src="https://gist.github.com/1065059.js"> </script>

**GET /api/v1/brand/{brand_id}/event/{event_id}/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: An Event

*returns* - The specific event that is specified by the event id.

**Fields**

name - Name of the event.<br/>
deleted - Flag that indicates whether the event is deleted.<br/>
created_at - Date the event was created.<br/>
id - The id of the Event.<br/>
brand - The brand the event belongs to.<br/>
date - The date of the event.<br/>

Example:<br/>
/api/v1/brand/55/event/12/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1065072.js"> </script>

##Pod Resource
**GET /api/v1/brand/{brand_id}/pod/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: List of Pods

*returns* - The pods which are associated with the specified brand id.

Example: <br/>
/api/v1/brand/55/pod/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1065080.js"> </script>

**GET /api/v1/brand/{brand_id}/pod/{pod_id}/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: A Pod

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

Example:<br/>
/api/v1/brand/55/pod/1/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1065096.js"> </script>

##Series Data Resource
**GET /api/v1/brand/{brand_id}/pod/{pod_id}/seriesdata/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format, graph, startdate, enddate<br/>
Response: Series data for a given pod

*returns* - The series data that we have collected for that pod in the last 90 days. See the additional parameter below to see more options (like getting more than 90 days worth of data). 

The data in the series data is pretty much a count, for that metric, on the day of measured_at. If you wish to know the exact time the metric was taken, you can use updated_at.

**Fields**<br/>
*twitter*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
followers - Count of twitter followers.<br/>
listed - Count of places you are listed<br/>
friends - Count of friends.<br/>
statuses - Count of statuses.<br/>

Example: <br/>
This example gives you an idea of what to expect from twitter series data. However, all the others will be pretty much the same but with different field names.<br/>
Also, please note there are more examples below that demonstrate the use the optional query string parameters.
/api/v1/brand/55/pod/1/seriesdata/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1065305.js"> </script>

*facebook*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
friends - Count of facebook friends.<br/>
wallposts - Count of wallposts.<br/>

*Blog*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
subscribers - Count of subscribers to your blog.<br/>
reach - You total reach.<br/>
hits - Number of hits.<br/>

*Google Analytics*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
newvisits - Total number of new visits.<br/>
visits - Total number of visits<br/>
pageviews - Total number of page views.<br/>
uniquepageviews - Total number of unique page views.<br/>

*Youtube Channel*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
subscribers - Total number of subscribers.<br/>
views - Total number of views.<br/>

*Youtube Video*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
views - Total number of views on your youtube video.<br/>
favorited - Total number of times your video was favorited.<br/>

*Facebook Group*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
members - Number of members in your facebook group.<br/>

*Facebook App*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
monthly_active_users - Total number of active monthly users for your app.<br/>
weekly_active_users - Total number of active weekly users for your app.<br/>
daily_active_users - Total number of active daily users for your app.<br/>

*Facebook Page*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
fans - Total number of facebook fans.<br/>

*Flickr User*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
photos - Number of photos.<br/>
groups - Number of groups.<br/>
contacts - Number of contacts.<br/>

*Flickr Group*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
members - <br/>

*Flickr Set*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
comments - Number of comments.<br/>

*Identica Profile*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
followers - Number of followers.<br/>
friends - Number of friends.<br/>
statuses - Number of statuses.<br/>

*Linkedin Profiles*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
connections - Total number of connections.<br/>
recommendations - Total number of recommendations.<br/>

*Delicious Url*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
bookmark - Number of bookmarks<br/>

*Stumbleupon Url*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
reviews - Number of reviews<br/>
rating - Number of Ratings<br/>

*Mybloglog Community*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
members - Number of members.<br/>

*Upcoming Event*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
attending - <br/>
interested - <br/>

*Metacafe Channel*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
views - <br/>
rank - <br/>
subscribers - <br/>
videos - <br/>

*Metacafe Video*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
views - Number of views.<br/>
rank - Total rank.<br/>
comments - Number of comments.<br/>

*Meetup Group*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
members - Number of members.<br/>
events - Number of events.<br/>
rating - Total rating.<br/>

*Meetup Event*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
rsvp - Number of RSVP.<br/>

*Myspace Profile*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
friends - Number of friends.<br/>
comments - Number of comments.<br/>

*Vimeo Video*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
plays - Number of times a video is played.<br/>
comments - Number of comments.<br/>
rating - Total rating.<br/>

*Vimeo Channel*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
subscribers - Total number of subscribers.<br/>
videos - Total videos.<br/>

*Vimeo Group*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
members - Number of members.<br/>
videos - Number of videos.<br/>
topics - Number of topics.<br/>
events - Number of events.<br/>

*Digg Url*

id - Series Data ID.<br/>
measured_at - Date measured at.<br/>
updated_at - Date and Time the data was updated at.<br/>
diggs - Number of diggs.<br/>
stories - Number of stories.<br/>
comments - Number of comments.<br/>

###Additional Parameters

**graph**<br/>
Available Values: highcharts

This parameter allows you to specify a special format for graphing libraries. At this point in time we only support Highcharts. Highcharts is a javascript library that creates awesome graphs, and with our javascript library it's super easy.

For more information checkout Highchart's website http://www.highcharts.com/.

Notes about the format:
We return the JSON that you would assign to the "data" portion of the graph options. In the data field, we have a list of values, [Date, Count]. The date field is stored in epoch format, the second field is the metric specified in the "name" fields.

Example:<br/>
/api/v1/brand/55/pod/1/seriesdata/?format=json&username=your_username&api_key=your_apikey&graph=highcharts<br/>
<script src="https://gist.github.com/1065423.js"> </script>

**fields**

Use this query string parameter to specify the metrics you would like to retrieve. You specify the fields using a comma separated list. For instance, if you wanted only the number of followers on twitter you would do "fields=followers". Or perhaps you want followers and friends. To do so you would do "fields=followers,friends". If you specify fields that don't exist in the seriesdata you requested, you will receive an empty reply.

Examples:<br/>
Only followers:<br/>
/api/v1/brand/55/pod/1/seriesdata/?format=json&username=your_username&api_key=your_apikey&fields=followers<br/>
<script src="https://gist.github.com/1065544.js"> </script>

Only followers and friends:<br/>
/api/v1/brand/55/pod/1/seriesdata/?format=json&username=your_username&api_key=your_apikey&fields=followers,friends<br/>
<script src="https://gist.github.com/1065554.js"> </script>

**startdate**

This query string parameter allows you to specify the start date for the date range used to retrieve the seriesdata. The format of the date needs to be YYYY-MM-DD.

Example:<br/>
/api/v1/brand/55/pod/1/seriesdata/?format=json&username=your_username&api_key=your_apikey&startdate=2011-05-15<br/>
<script src="https://gist.github.com/1065659.js"> </script>

**enddate**

This query string parameter allows you to specify the end date for the date range used to retrieve the seriesdata. The format of the date needs to be YYYY-MM-DD.

Example:<br/>
api/v1/brand/55/pod/1/seriesdata/?format=json&username=your_username&api_key=your_apikey&enddate=2011-05-20<br/>
<script src="https://gist.github.com/1065683.js"> </script>

**Putting it together**



/api/v1/brand/55/pod/1/seriesdata/?format=json&username=your_username&api_key=your_apikey&enddate=2011-05-31&startdate=2011-05-01&graph=highcharts&fields=followers<br/>
<script src="https://gist.github.com/1065749.js"> </script>
