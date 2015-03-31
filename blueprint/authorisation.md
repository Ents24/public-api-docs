FORMAT: 1A
HOST: https://api.ents24.com

# Ents24 REST API (Beta 3)
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

        client_id=aho0bVpKdFURaZ37tkYT&client_secret=uQmfyQsqeKfIMJg4FKQ9gi8cSLFXATpGFyBx038nHy

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT

    + Body

            {
              "access_token": "qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA"
              "token_type": "Bearer"
              "expires": 1414317411
              "expires_in": 5184000
            }

# Group User Authentication
To obtain an access token you must authenticate your client user credentials with our authentication server.
User credentials should represent a valid Ents24 user account. 

### Request Access Token [/auth/login]
Request an access token to authenticate future client user requests.

#### Auth Login [POST]
+ Request (application/x-www-form-urlencoded)

        client_id=aho0bVpKdFURaZ37tkYT&client_secret=uQmfyQsqeKfIMJg4FKQ9gi8cSLFXATpGFyBx038nHy&username=auser&password=mypa55w0rd

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT

    + Body

            {
              "access_token": "qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA"
              "token_type": "Bearer"
              "expires": 1414317411
              "expires_in": 5184000
            }

# Group Request Authentication
Your access token must be included as an **Authorization header** in each request sent to the API.

    Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA
