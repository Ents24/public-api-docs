FORMAT: 1A
HOST: https://api.ents24.com

# Ents24 REST API (Beta 3.2)
The Ents24 REST API gives you easy access to the UK's most comprehensive live entertainment database:  
A horde of event-listing experts add over 10,000 new listings every week!  
Easily use our data for your website or application.  

Licensing terms and conditions apply.

# Group Client Authentication
To obtain an access token you must authenticate your client credentials with our authentication server.

### Request Access Token [/auth/token]
Request an access token to authenticate future requests.

#### Auth Token [POST]
+ Request (application/x-www-form-urlencoded)
    
    + Body

            client\_id=aho0bVpKdFURaZ37tkYT&client\_secret=uQmfyQsqeKfIMJg4FKQ9gi8cSLFXATpGFyBx038nHy

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT

    + Body

            {
              "description": "An OAuth2 access token object",
              "type": "object",
              "properties": {
                "access_token": {
                  "description": "The requested access token",
                  "type": "string"
                },
                "token_type": {
                  "description": "The type of access token issued",
                  "type": "string"
                },
                "expires": {
                  "description": "The expiry date of the issued access token",
                  "type": "integer"
                },
                "expires_in": {
                  "description": "The validity timespan for the token from the time of issue",
                  "type": "integer"
                }
              },
              "required": ["access\_token", "token\_type", "expires", "expires\_in"]
            }

# Group User Authentication
To obtain an access token you must authenticate your client user credentials with our authentication server.
User credentials should represent a valid Ents24 user account. 

### Request Access Token [/auth/login]
Request an access token to authenticate future client user requests.

#### Auth Login [POST]
+ Request (application/x-www-form-urlencoded)
    
    + Body

            client\_id=aho0bVpKdFURaZ37tkYT&client\_secret=uQmfyQsqeKfIMJg4FKQ9gi8cSLFXATpGFyBx038nHy&username=auser&password=mypa55w0rd

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT

    + Body

            {
              "description": "An OAuth2 access token object",
              "type": "object",
              "properties": {
                "access_token": {
                  "description": "The requested access token",
                  "type": "string"
                },
                "token_type": {
                  "description": "The type of access token issued",
                  "type": "string"
                },
                "expires": {
                  "description": "The expiry date of the issued access token",
                  "type": "integer"
                },
                "expires_in": {
                  "description": "The validity timespan for the token from the time of issue",
                  "type": "integer"
                }
              },
              "required": ["access\_token", "token\_type", "expires", "expires\_in"]
            }

# Group Request Authentication
Your access token must be included as an **Authorization header** in each request sent to the API.

    Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA
