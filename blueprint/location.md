FORMAT: 1A
HOST: https://api.ents24.com

# Ents24 REST API (Beta 3.2)
The Ents24 REST API gives you easy access to the UK's most comprehensive live entertainment database:  
A horde of event-listing experts add over 10,000 new listings every week!  
Easily use our data for your website or application.  

Licensing terms and conditions apply.

# Group Location

### Search [/location/search?name={name}&postcode={postcode}&geo={geo}&radius\_distance={radius\_distance}&distance\_unit={distance\_unit}]
Check location parameter values for use in event or venue list by location requests.

#### Location Search [GET]
+ Parameters
  + name (optional, string, `Newcastle`) ... The name of the location your searching for.
  + postcode (optional, string, `NE82 6YY`) ... The postcode of the location your searching for.
  + geo (optional, string, `54.974384411995,-1.6015806376512`) ... Comma separated latitude and longitude of the location your searching for.
  + radius\_distance (optional, integer, `10`) ... The furthest distance from the given location that should be searched.<br />***NB:*** *This parameter is disregarded unless either the `postcode` or `geo` parameter is set.*
  + distance\_unit (optional, string, `mi`) ... The unit of measurment that should be applied to the radius\_distance value [mi, km].<br />***NB:*** *This parameter is disregarded unless either the `postcode` or `geo` parameter is set.*

+ Request

    + Headers

            Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "Location Search",
              "description": "List of location objects matching the request parameters",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "name": {
                    "description": "Name of the location",
                    "type": "string"
                  },
                  "county": {
                    "description": "County where the location is found",
                    "type": "string"
                  },
                  "latitude": {
                    "description": "Latitude of the location",
                    "type": "number"
                  },
                  "longitude": {
                    "description": "Longitude of the location",
                    "type": "number"
                  }
                },
                "required": ["name","latitude","longitude"]
              }
            }
