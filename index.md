---
title: SWIX Rest API
layout: default
---
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js">
</script>
#Introduction to SWIX's REST Api
SWIX's API allows you to access our system programmatically. Before you can acces the SWIX api you must first obtain an API key from us. 

**Upcoming Changes**<br/>
Before we outline our upcoming changes we want to thank you for your support while we develop our API. Version 1 is almost complete and 
we have made a few changes with you in mind.

Throughout the document we have now put a note underneath any field that is going to change. That being said the most significant change
we have made is in regard to 'related resources'. A related resource is just a field in a resource which points to a different resource.
For example, in the Brand Resource there is a field called 'pod' which points to a Pod Resouse.

Currently when you request a resource, we gather and return all the related resource's data with it. This approach seemed appropriate at first
but this has added significant over head and increased the time it takes for us to respond to a request. Once we deploy our changes later
this month this behavior will change. Going forward when you request a resource instead of getting all the related resource's data, you will 
get the url to the related resource.

##Query String
**Format**<br/>
Purpose: Allows you to specify the format the data is returned in.<br/>
Available Values: XML, JSON

You may use the *format* parameter in all of your calls to the API. 

For JSON formatting:

[http://swixapp.com/api/v1/brand/?format=json](http://swixapp.com/api/v1/brand/?format=json)

For XML formatting:

[http://swixapp.com/api/v1/brand/?format=xml](http://swixapp.com/api/v1/brand/?format=xml)

**API Key**<br/>
Purpose: Allows you to authenticate.

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
**Upcoming Change** events - URL to the Event Resource which lists the events that belong to the brand<br/>
pod - List of pods that belong to the brand<br/>
**Upcoming Change** pods - URL to the Pod Resource which lists the pods that belong to the brand<br/>
**Upcoming Chane** offers - URL to the Offer Resource which lists the offers that belong to the brand<br/>

<div class='gist_data'>
<div id='gist_head' style="padding: .5em;background-color: #EAEAEA;border: 1px solid #DEDEDE;">
<p style="margin: 0px;"><strong>Example: </strong>/api/v1/brand/55/?format=json&username=your_username&api_key=your_apikey <a href="#" class="hide-button" style="float: right">Hide</a></p>
</div>
<script src="https://gist.github.com/1065046.js"> </script>
</div>

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
**Upcoming Change** brand - URL to the brand which owns the event.<br/>
date - The date of the event.<br/>

Example:<br/>
/api/v1/brand/55/event/12/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1065072.js"> </script>

##Offer Resource
**GET /api/v1/brand/{brand_id}/offer/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: List of Offers

*returns* - The offers which are assocaited with the specified offer id.

Example:<br/>
/api/v1/brand/55/offer/17/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1229878.js"> </script>

**GET /api/v1/brand/{brand_id}/offer/{offer_id}/**<br/>
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: An Offer

*returns* - The offer which is specified by the offer_id parameter.

**Fields**

landing_page - The page the offer is on. The short url will point to this URL.<br/>
conversion - URL to the Conversion Resource which lists the conversions by date.<br/>
name - Name of the Offer.<br/>
end_date - The date the offer is scheduled to end.<br/>
roi - The calculated return on investment. 'N/A' if this field does not apply.<br/>
short_url - The short URL which will redirect a user to the landing page.<br/>
brand - The URL to the Brand Resource which this offer belongs to.<br/>
updated_at - When the resource was last updated.<br/>
start_date - The start date of the offer.<br/>
total_revenue - Total revenue this campaign has given you.<br/>
conversions - The total number of conversions this offer has given you.<br/>
default_value_in_cents - The default value of each sale, in cents.<br/>
activity_name - The name of the activity.<br/>
initial_cost_in_cents - The upfront consts of the offer.<br/>
click_data - URL to the Click Data Resource.<br/>
created_at - Date the offer was created.<br/>
offer_transactions - URL to the Offer Transaction Resource.<br/>
type - Type of offer, Either 'Sales' or 'Activity'.<br/>
id - ID of the offer.<br/>
revenue_by_day - URL to the Revenue By Day Resource.<br/>

Example:<br/>
/api/v1/brand/55/offer/17/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1229870.js"> </script>

##Offer Transaction Resource
**GET /api/v1/brand/{brand_id}/offer/{offer_id}/offertransaction/**
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: List of Offer Transactions

**returns** - A list of Offer Transactions that belong to the given offer id.

Example:<br/>
/api/v1/brand/55/offer/17/offertransaction/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1229944.js"> </script>

**GET /api/v1/brand/{brand_id}/offer/{offer_id}/offertransaction/{offertransaction_id}/**
Required Parameters: api_key, username<br/>
Optional Parameters: format<br/>
Response: An Offer Transaction

**returns** - The Offer Transaction specified by the offertransaction_id parameter.

**Fields**

referrer - Where the sale came from. (i.e Twitter, Facebook, ect.)<br/>
created_at - When the transaction took place.<br/>
offer - URL to the offer the transaction belongs to.<br/>
id - ID of the transaction.<br/>
amount_in_cents - Transaction amount in cents.<br/>

Example:<br/>
/api/v1/brand/55/offer/17/offertransaction/20/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1229948.js"> </script>

##Click Data Resource
**GET /api/v1/brand/{brand_id}/offer/{offer_id}/clickdata/**
Required Parameters: api_key, username<br/>
Optional Parameters: format, graph, startdate, enddate<br/>
Response: Click data.

**returns** - A compiled list of the click data, from various reffers.

**Fields**

clicks - Number of clicks.
measured_at - The date the clicks happened on.

Example:<br/>
/api/v1/brand/55/offer/17/clickdata/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1230281.js"> </script>

##Revenue By Day Resource
**GET /api/v1/brand/{brand_id}/offer/{offer_id}/revenuebyday/**
Required Parameters: api_key, username<br/>
Optional Parameters: format, graph, startdate, enddate<br/>
Response: A compiled list of the total revenue by day.

**returns** - A compiled list of revenue earned, by day for the given offer.

**Fields**

sales - Amount of sales in dollars.
measured_at - The date for the sales.

Example:<br/>
/api/v1/brand/55/offer/17/revenuebyday/?format=json&username=your_username&api_key=your_apikey<br/>

<script src="https://gist.github.com/1230026.js"> </script>

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
uri - URL to the resource this pod uses.<br/>
updated_at - Date pod was updated<br/>
id - The id of the pod.<br/>
active - Flag that tells you if this pod is active.<br/>
type - This will indicate what type of pod this is. This will tell you which format seriesdata will be in.<br/>
brand - The brand this pod belongs to.<br/>
**Upcoming Change** brand - URL to the brand which owns the event.<br/>
seriesdata - the URL to the series data for this pod<br/>

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
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
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
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
friends - Count of facebook friends.<br/>
wallposts - Count of wallposts.<br/>

*Blog*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
subscribers - Count of subscribers to your blog.<br/>
reach - You total reach.<br/>
hits - Number of hits.<br/>

*Google Analytics*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
newvisits - Total number of new visits.<br/>
visits - Total number of visits<br/>
pageviews - Total number of page views.<br/>
uniquepageviews - Total number of unique page views.<br/>

*Youtube Channel*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
subscribers - Total number of subscribers.<br/>
views - Total number of views.<br/>

*Youtube Video*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
views - Total number of views on your youtube video.<br/>
favorited - Total number of times your video was favorited.<br/>

*Facebook Group*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
members - Number of members in your facebook group.<br/>

*Facebook App*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
monthly_active_users - Total number of active monthly users for your app.<br/>
weekly_active_users - Total number of active weekly users for your app.<br/>
daily_active_users - Total number of active daily users for your app.<br/>

*Facebook Page*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
fans - Total number of facebook fans.<br/>

*Flickr User*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
photos - Number of photos.<br/>
groups - Number of groups.<br/>
contacts - Number of contacts.<br/>

*Flickr Group*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
members - <br/>

*Flickr Set*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
comments - Number of comments.<br/>

*Identica Profile*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
followers - Number of followers.<br/>
friends - Number of friends.<br/>
statuses - Number of statuses.<br/>

*Linkedin Profiles*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
connections - Total number of connections.<br/>
recommendations - Total number of recommendations.<br/>

*Delicious Url*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
bookmark - Number of bookmarks<br/>

*Stumbleupon Url*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
reviews - Number of reviews<br/>
rating - Number of Ratings<br/>

*Mybloglog Community*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
members - Number of members.<br/>

*Upcoming Event*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
attending - <br/>
interested - <br/>

*Metacafe Channel*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
views - <br/>
rank - <br/>
subscribers - <br/>
videos - <br/>

*Metacafe Video*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
views - Number of views.<br/>
rank - Total rank.<br/>
comments - Number of comments.<br/>

*Meetup Group*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
members - Number of members.<br/>
events - Number of events.<br/>
rating - Total rating.<br/>

*Meetup Event*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
rsvp - Number of RSVP.<br/>

*Myspace Profile*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
friends - Number of friends.<br/>
comments - Number of comments.<br/>

*Vimeo Video*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
plays - Number of times a video is played.<br/>
comments - Number of comments.<br/>
rating - Total rating.<br/>

*Vimeo Channel*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
subscribers - Total number of subscribers.<br/>
videos - Total videos.<br/>

*Vimeo Group*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
members - Number of members.<br/>
videos - Number of videos.<br/>
topics - Number of topics.<br/>
events - Number of events.<br/>

*Digg Url*

id - Series Data ID.<br/>
measured_at - Date measured at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-08T13:50:28<br/>
updated_at - Date and Time the data was updated at. Appears in the format YYYY-MM-DD"T"HH:MM:SS. Example: 2011-04-12T13:50:28<br/>
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

Lets say we want to graph the number of followers we have, from the seriesdata that belongs to pod 1 for the month of May. We would use the following url:

/api/v1/brand/55/pod/1/seriesdata/?format=json&username=your_username&api_key=your_apikey&enddate=2011-05-31&startdate=2011-05-01&graph=highcharts&fields=followers<br/>
<script src="https://gist.github.com/1065749.js"> </script>
<script type="text/javascript">
jQuery(document).ready(function() {
  jQuery(".hide-button").click(function(event)
  {
    var src = event.srcElement;
    if( src.text == 'Hide' )
    {
      var obj = jQuery(this).closest('.gist_data').find(".gist");
      obj.hide();
      src.text = 'Show';
    }
    else
    {
      var obj = jQuery(this).closest('.gist_data').find(".gist");
      obj.show();
      src.text = 'Hide';
    }
    return false;
  });
});
</script>