FORMAT: 1A
HOST: https://api.ents24.com

# Ents24 REST API (Beta 1.2)
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

# Group Event
Available resources on the Event API endpoints.

### Genres [/event/genres]
A list of all valid event genres.

#### Event Genres [GET]
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
              "title": "Event Genres",
              "description": "A list of valid event genres",
              "type": "array",
              "items": {
                "type": "string"
              }
            }

### List [/event/list?location={location}&type={type}&genre={genre}&date={date}&date_from={date_from}&date_to={date_to}&venue_name={venue_name}&venue={venue}&venue_id={venue_id}&artist_name={artist_name}&artist={artist}&artist_id={artist_id}&results_per_page={results_per_page}&page={page}&incl_image={incl_image}&image_size={image_size}&incl_artists={incl_artists}&incl_tickets={incl_tickets}&full_description={full_description}&updated_since={updated_since}]
Multiple event objects with selected fields.  
***NB:*** *You must filter resources retrieved from this end-point with at least one of the following request parameters:*  
`location` `venue_name` `artist_name`

#### Event List [GET]
+ Parameters
  + location (optional, string, `London`) ... The location of events you want a listing for.
  + genre (optional, string, `rock`) ... The genre of event type you want listed.
  + date (optional, date, `2014-09-03`) ... A specific date you want an events listing for.<br />***NB:*** *This parameter is disregarded if `date_from` and `date_to` parameters are set in the same request*.
  + date_from (optional, date, `2014-09-03`) ... The date you want an events listing from.<br />***NB:*** *This parameter is required when `date_to` parameter is set.*
  + date_to (optional, date, `2014-09-10`) ... The date you want an events listing to.<br />***NB:*** *This parameter is required when `date_from` parameter is set.*
  + venue_name (optional, string, `Hyde Park`) ... The venue you want an events listing for.<br />***NB:*** *Values applied to this parameter may match more than one venue!<br />You should use the `venue/read` end-point to get event listings for a particular venue.*
  + venue (optional, string, `Hyde Park`) ... **DEPRECATED IN BETA 2! You should use the `venue_name` parameter instead**
  + venue_id (optional, string, `lRx9`) ... **DEPRECATED IN BETA 2!** The unique identifier for a venue you want an events listing for.
  + artist_name (optional, string, `Blondie`) ... The artist you want an events listing for.<br />***NB:*** *Values applied to this parameter may match more than one artist!<br />You should use the `artist/read` end-point to get an upcoming events list for a particular artist.*
  + artist (optional, string, `Blondie`) ... **DEPRECATED IN BETA 2! You should use the `artist_name` parameter instead**
  + artist_id (optional, string, `njyZ`) ... **DEPRECATED IN BETA 2!** The unique identifier for an artist you want an events listing for.
  + results_per_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
  + page (optional, string, `ZW0=`) ... The page/chunk of results to be requested.
  + incl_image (optional, boolean, `1`) ... Decides whether or not an event image is included in the response.
  + image_size (optional, string, `medium`) ... Chooses the size of image included with each image object if one is available.
  + incl_artists (optional, boolean, `1`) ... Decides whether or not a list of performing artists is included in the response. 
  + incl_tickets (optional, boolean, `1`) ... Decides whether or not a list of available tickets is included in the response.  
  + full_description (optional, boolean, `0`) ... Decides whether full or summarised description text is included in the response. 
  + updated_since (optional, date, `2014-08-31`) ... Only retrive events that have been added/updated since the given date.

+ Request

    + Headers

            Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Next-Page: R2U=
            X-Previous-Page: bUw=
            X-Total-Items-Found: 75

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "Event List",
              "description": "A list of Event objects with selected fields",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "id": {
                    "description": "Unique identifier for the event",
                    "type": "string"
                  },
                  "title": {
                    "description": "Title of the event",
                    "type": "string"
                  },
                  "venue": {
                    "description": "Venue the event is being held at",
                    "type": "object",
                    "properties": {
                      "id": {
                        "description": "Unique identifier for the venue",
                        "type": "string"
                      },
                      "name": {
                        "description": "Name of the venue",
                        "type": "string"
                      },
                      "town": {
                        "description": "Town or city where the venue is located",
                        "type": "string"
                      },
                      "location": {
                        "description": "Lat/Lon coordinates of the venue",
                        "$ref": "http://json-schema.org/geo"
                      }
                    },
                    "required": ["id","name","town","location"]
                  },
                  "startDateTime": {
                    "description": "DEPRECATED IN BETA 2! RFC-3339 formatted start date and time for the event",
                    "type": "string"
                  },
                  "endDateTime": {
                    "description": "DEPRECATED IN BETA 2! RFC-3339 formatted end date and time for the event",
                    "type": "string"
                  },
                  "startDate": {
                    "description": "RFC-3339 formatted start date for the event",
                    "type": "string"
                  },
                  "endDate": {
                    "description": "RFC-3339 formatted end date for the event",
                    "type": "string"
                  },
                  "startTimeString": {
                    "description": "Start time string for the event",
                    "type": "string"
                  },
                  "endTimeString": {
                    "description": "End time string for the event",
                    "type": "string"
                  },
                  "description": {
                    "description": "Description text for the event",
                    "type": "string"
                  },
                  "artists": {
                    "description": "Featured artists",
                    "type": "array",
                    "items": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "description": "Unique identifier for a featured artist",
                          "type": "string"
                        },
                        "name": {
                          "description": "Name of a featured artist",
                          "type": "string"
                        }
                      },
                      "required": ["id","name"]
                    }
                  },
                  "tickets": {
                    "description": "Tickets for this event",
                    "type": "array",
                    "items": {
                      "type": "object",
                      "properties": {
                        "supplier": {
                          "description": "The supplier for this ticket",
                          "type": "string"
                        },
                        "price": {
                          "description": "The price for this ticket",
                          "type": "string"
                        },
                        "dateTime": {
                          "description": "RFC-3339 formatted date and time this ticket is valid for",
                          "type": "string"
                        },
                        "url": {
                          "description": "The purchase URL for this ticket",
                          "type": "string"
                        },
                        "onSaleFrom": {
                          "description": "RFC-3339 formatted date this ticket goes on sale",
                          "type": "string"
                        },
                        "onSaleUntil": {
                          "description": "RFC-3339 formatted date this ticket is / will be on sale until",
                          "type": "string"
                        }
                      },
                      "required": ["supplier","price","dateTime","onSaleUntil"]
                    }
                  },
                  "image": {
                    "description": "Single image asset for the event",
                    "type": "object",
                    "properties": {
                      "url": {
                        "description": "Image source URL",
                        "type": "string"
                      },
                      "width": {
                        "description": "Image width (px)",
                        "type": "integer"
                      },
                      "height": {
                        "description": "Image height (px)",
                        "type": "integer"
                      },
                      "metadata": {
                        "description": "Metadata related to this image",
                        "type": "object",
                        "properties": {
                          "copyright": {
                            "description": "The copyright holder for this image",
                            "type": "string"
                          },
                          "caption": {
                            "description": "Caption text for this image",
                            "type": "string"
                          }
                        },
                        "required": ["copyright","caption"]
                      }
                    },
                    "required": ["metadata","url","width","height"]
                  },
                  "webLink": {
                    "description": "URL for the web page for the event on ents24.com",
                    "type": "string"
                  },
                  "viewsOnEnts24": {
                    "description": "The number of unique vistors to this event's page on Ents24",
                    "type": "integer"
                  },
                  "fansOnEnts24": {
                    "description": "The number of Ents24 users tracking updates and announcements for this event",
                    "type": "integer"
                  },
                  "lastUpdate": {
                    "description": "RFC-3339 formatted added/updated timestamp for this object",
                    "type": "string"
                  }
                },
                "required": ["id","title","startDate","endDate","description","webLink","viewsOnEnts24","fansOnEnts24","lastUpdate"]
              }
            }

+ Response 204

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Next-Page: MDg=
            X-Previous-Page: ZW0=
            X-Total-Items-Found: 75

### Read [/event/read?id={id}&incl_artists={incl_artists}&incl_images={incl_images}&incl_tickets={incl_tickets}&full_description={full_description}]
An event object with all fields.

#### Event [GET]
+ Parameters
  + id (required, string, `mDDaoO`) ... Unique identifier string of the Event you want full details for.  
  + incl_artists (optional, boolean, `1`) ... Decides whether or not a list of performing artists is included in the response.  
  + incl_images (optional, boolean, `1`) ... Decides whether or not an event images are included in the response.  
  + incl_tickets (optional, boolean, `1`) ... Decides whether or not a list of available tickets is included in the response.  
  + full_description (optional, boolean, `1`) ... Decides whether full or summarised description text is included in the response. 

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
              "title": "Event",
              "description": "A single Event object with all fields",
              "type": "object",
              "properties": {
                "id": {
                  "description": "Unique identifier for the event",
                  "type": "string"
                },
                "title": {
                  "description": "Title of the event",
                  "type": "string"
                },
                "venue": {
                  "description": "Venue the event is being held at",
                  "type": "object",
                  "properties": {
                    "id": {
                      "description": "Unique identifier for the venue",
                      "type": "string"
                    },
                    "name": {
                      "description": "Name of the venue",
                      "type": "string"
                    },
                    "town": {
                      "description": "Town or city where the venue is located",
                      "type": "string"
                    },
                    "location": {
                      "description": "Lat/Lon coordinates of the venue",
                      "$ref": "http://json-schema.org/geo"
                    }
                  },
                  "required": ["id","name","town","location"]
                },
                "startDateTime": {
                  "description": "DEPRECATED IN BETA 2! RFC-3339 formatted start date and time for the event",
                  "type": "string"
                },
                "endDateTime": {
                  "description": "DEPRECATED IN BETA 2! RFC-3339 formatted end date and time for the event",
                  "type": "string"
                },
                "startDate": {
                  "description": "RFC-3339 formatted start date for the event",
                  "type": "string"
                },
                "endDate": {
                  "description": "RFC-3339 formatted end date for the event",
                  "type": "string"
                },
                "startTimeString": {
                  "description": "Start time string for the event",
                  "type": "string"
                },
                "endTimeString": {
                  "description": "End time string for the event",
                  "type": "string"
                },
                "description": {
                  "description": "Description text for the event",
                  "type": "string"
                },
                "artists": {
                  "description": "Featured artists",
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "description": "Unique identifier for a featured artist",
                        "type": "string"
                      },
                      "name": {
                        "description": "Name of a featured artist",
                        "type": "string"
                      }
                    },
                    "required": ["id","name"]
                  }
                },
               "image": {
                  "description": "Multiple image assets for the event",
                  "type": "object",
                  "properties": {
                    "small": {
                      "description": "Small sized image",
                      "type": "object",
                      "properties": {
                        "url": {
                          "description": "Image source URL",
                          "type": "string"
                        },
                        "width": {
                          "description": "Image width (px)",
                          "type": "integer"
                        },
                        "height": {
                          "description": "Image height (px)",
                          "type": "integer"
                        }
                      },
                      "required": ["url","width","height"]
                    },
                    "medium": {
                      "description": "Medium sized image",
                      "type": "object",
                      "properties": {
                        "url": {
                          "description": "Image source URL",
                          "type": "string"
                        },
                        "width": {
                          "description": "Image width (px)",
                          "type": "integer"
                        },
                        "height": {
                          "description": "Image height (px)",
                          "type": "integer"
                        }
                      },
                      "required": ["url","width","height"]
                    },
                    "large": {
                      "description": "Medium sized image",
                      "type": "object",
                      "properties": {
                        "url": {
                          "description": "Image source URL",
                          "type": "string"
                        },
                        "width": {
                          "description": "Image width (px)",
                          "type": "integer"
                        },
                        "height": {
                          "description": "Image height (px)",
                          "type": "integer"
                        }
                      },
                      "required": ["url","width","height"]
                    },
                    "metadata": {
                      "description": "Metadata related to this image",
                      "type": "object",
                      "properties": {
                        "copyright": {
                          "description": "The copyright holder for this image",
                          "type": "string"
                        },
                        "caption": {
                          "description": "Caption text for this image",
                          "type": "string"
                        }
                      },
                      "required": ["copyright","caption"]
                    }
                  }
                },
                "genre": {
                  "description": "The genre(s) this event is found under",
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                },
                "tickets": {
                  "description": "Tickets for this event",
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "supplier": {
                        "description": "The supplier for this ticket",
                        "type": "string"
                      },
                      "price": {
                        "description": "The price for this ticket",
                        "type": "string"
                      },
                      "dateTime": {
                        "description": "RFC-3339 formatted date and time this ticket is valid for",
                        "type": "string"
                      },
                      "url": {
                        "description": "The purchase URL for this ticket",
                        "type": "string"
                      },
                      "onSaleFrom": {
                        "description": "RFC-3339 formatted date this ticket goes on sale",
                        "type": "string"
                      },
                      "onSaleUntil": {
                        "description": "RFC-3339 formatted date this ticket is / will be on sale until",
                        "type": "string"
                      }
                    },
                    "required": ["supplier","price","dateTime","onSaleUntil"]
                  }
                },
                "webLink": {
                  "description": "URL for the web page for the event on ents24.com",
                  "type": "string"
                },
                "viewsOnEnts24": {
                  "description": "The number of unique vistors to this event's page on Ents24",
                  "type": "integer"
                },
                "fansOnEnts24": {
                  "description": "The number of Ents24 users tracking updates and announcements for this event",
                  "type": "integer"
                },
                "lastUpdate": {
                  "description": "RFC-3339 formatted added/updated timestamp for this object",
                  "type": "string"
                }
              },
              "required": ["id","title","startDate","endDate","description","webLink","viewsOnEnts24","fansOnEnts24","lastUpdate"]
            }

### Image [/event/image?id={id}&size={size}&format={format}]
An event image retrieved as either a JSON object or JPEG image.

#### Event Image [GET]
+ Parameters
  + id (required, string, `mDDaoO`) ... Unique identifier string of the Event you want an image for.
  + size (optional, string, `medium`) ... Size of image you want [small, medium, large].
  + format (optional, string, `json`) ... The format of the response you want back from the resource [json, jpeg].

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
              "title": "Event Image",
              "description": "An image asset for an event",
              "type": "object",
              "properties": {
                "url": {
                  "description": "Image source URL",
                  "type": "string"
                },
                "width": {
                  "description": "Image width (px)",
                  "type": "integer"
                },
                "height": {
                  "description": "Image height (px)",
                  "type": "integer"
                },
                "metadata": {
                  "description": "Metadata related to this image",
                  "type": "object",
                  "properties": {
                    "copyright": {
                      "description": "The copyright holder for this image",
                      "type": "string"
                    },
                    "caption": {
                      "description": "Caption text for this image",
                      "type": "string"
                    }
                  },
                  "required": ["copyright","caption"]
                }
              },
              "required": ["url","width","height","metadata"]
            }

# Group Artist
Available resources on the Artist API endpoints.

### List [/artist/list?name={name}&event_name={event_name}&event={event}&genre={genre}&results_per_page={results_per_page}&page={page}&incl_image={incl_image}&image_size={image_size}&incl_events={incl_events}&full_description={full_description}&updated_since={updated_since}]
Multiple artist objects with selected fields.  
***NB:*** *You must filter resources retrieved from this end-point with at least one of the following request parameters:*  
`name` `event_name`

#### Artist List [GET]
+ Parameters
  + name (optional, string, `Blondie`) ... The string that matches artist names you want a list of.<br />***NB:*** *Values applied to this parameter may match more than one artist!<br />You should use the `artist/read` end-point to retrieve data for a particular artist.*
  + event_name (optional, string, `BBC Radio 2 Live In Hyde Park`) ... The name for an event you want an artists listing for.<br />***NB:*** *Values applied to this parameter may match more than one event!<br />You should use the `event/read` end-point to retrieve data for a particular event.*
  + event (optional, string, `BBC Radio 2 Live In Hyde Park`) ... **DEPRECATED IN BETA 2! You should use the `event_name` parameter instead**
  + genre (optional, string, `rock`) ... The genre you want an artists listing for.
  + results_per_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
  + page (optional, string, `ZW0=`) ... The page/chunk of results to be requested.
  + incl_image (optional, boolean, `1`) ... Decides whether or not an artist image is included in the response.
  + image_size (optional, string, `medium`) ... Chooses the size of image included with each artist object if one is available.
  + incl_events (optional, boolean, `1`) ... Decides whether or not a list of upcoming events is included with each artist object in the response.
  + full_description (optional, boolean, `0`) ... Decides whether full or summarised description text is included in the response. 
  + updated_since (optional, date, `YYYY-MM-DD`) ... Only retrive artists that have been added/updated since the given date.

+ Request

    + Headers

            Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Next-Page: R2U=
            X-Previous-Page: bUw=
            X-Total-Items-Found: 75

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "Artist List",
              "description": "A list of Artist objects with selected fields",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "id": {
                    "description": "Unique identifier for the artist",
                    "type": "string"
                  },
                  "name": {
                    "description": "Name of the artist",
                    "type": "string"
                  },
                  "description": {
                    "description": "Description text for the artist",
                    "type": "string"
                  },
                  "events": {
                    "description": "Artists upcoming events",
                    "type": "array",
                    "items": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "description": "Unique identifier for the event",
                          "type": "string"
                        },
                        "title": {
                          "description": "Title of the event",
                          "type": "string"
                        },
                        "venue": {
                          "description": "Venue the event is being held at",
                          "type": "object",
                          "properties": {
                            "id": {
                              "description": "Unique identifier for the venue",
                              "type": "string"
                            },
                            "name": {
                              "description": "Name of the venue",
                              "type": "string"
                            },
                            "town": {
                              "description": "Town or city where the venue is located",
                              "type": "string"
                            },
                            "location": {
                              "description": "Lat/Lon coordinates of the venue",
                              "$ref": "http://json-schema.org/geo"
                            }
                          },
                          "required": ["id","name","town","location"]
                        },
                        "startDateTime": {
                          "description": "DEPRECATED IN BETA 2! RFC-3339 formatted start date and time for the event",
                          "type": "string"
                        },
                        "endDateTime": {
                          "description": "DEPRECATED IN BETA 2! RFC-3339 formatted end date and time for the event",
                          "type": "string"
                        },
                        "startDate": {
                          "description": "RFC-3339 formatted start date for the event",
                          "type": "string"
                        },
                        "endDate": {
                          "description": "RFC-3339 formatted end date for the event",
                          "type": "string"
                        },
                        "startTimeString": {
                          "description": "Start time string for the event",
                          "type": "string"
                        },
                        "endTimeString": {
                          "description": "End time string for the event",
                          "type": "string"
                        }
                      },
                      "required": ["id","title","startDate","endDate"]
                    }
                  },
                  "image": {
                    "description": "Single image asset for the artist",
                    "type": "object",
                    "properties": {
                      "url": {
                        "description": "Image source URL",
                        "type": "string"
                      },
                      "width": {
                        "description": "Image width (px)",
                        "type": "integer"
                      },
                      "height": {
                        "description": "Image height (px)",
                        "type": "integer"
                      },
                      "metadata": {
                        "description": "Metadata related to this image",
                        "type": "object",
                        "properties": {
                          "copyright": {
                            "description": "The copyright holder for this image",
                            "type": "string"
                          },
                          "caption": {
                            "description": "Caption text for this image",
                            "type": "string"
                          }
                        },
                        "required": ["copyright","caption"]
                      }
                    }
                  },
                  "webLink": {
                    "description": "URL for the web page for the artist on ents24.com",
                    "type": "string"
                  },
                  "viewsOnEnts24": {
                    "description": "The number of unique vistors to this artist's page on Ents24",
                    "type": "integer"
                  },
                  "fansOnEnts24": {
                    "description": "The number of Ents24 users tracking updates and announcements for this artist",
                    "type": "integer"
                  },
                  "lastUpdate": {
                    "description": "RFC-3339 formatted added/updated timestamp for this object",
                    "type": "string"
                  }
                },
                "required": ["id","name","description","webLink","viewsOnEnts24","fansOnEnts24","lastUpdate"]
              }
            }

+ Response 204

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Next-Page: MDg=
            X-Previous-Page: ZW0=
            X-Total-Items-Found: 75

### Read [/artist/read?id={id}&incl_events={incl_events}&incl_image={incl_images}&full_description={full_description}]
An artist object with all fields.

#### Artist [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the Artist you want full details for.
  + incl_events (optional, boolean, `1`) ... Decides whether or not a list of events the artists is performing at is included in the response.  
  + incl_images (optional, boolean, `1`) ... Decides whether or not an artist images are included in the response.  
  + full_description (optional, boolean, `1`) ... Decides whether full or summarised description text is included in the response. 

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
              "title": "Artist",
              "description": "A single Artist object with all fields",
              "type": "object",
              "properties": {
                "id": {
                  "description": "Unique identifier for the artist",
                  "type": "string"
                },
                "name": {
                  "description": "Name of the artist",
                  "type": "string"
                },
                "description": {
                  "description": "Description text for the artist",
                  "type": "string"
                },
                "events": {
                  "description": "Artists upcoming events",
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "description": "Unique identifier for the event",
                        "type": "string"
                      },
                      "title": {
                        "description": "Title of the event",
                        "type": "string"
                      },
                      "venue": {
                        "description": "Venue the event is being held at",
                        "type": "object",
                        "properties": {
                          "id": {
                            "description": "Unique identifier for the venue",
                            "type": "string"
                          },
                          "name": {
                            "description": "Name of the venue",
                            "type": "string"
                          },
                          "town": {
                            "description": "Town or city where the venue is located",
                            "type": "string"
                          },
                          "location": {
                            "description": "Lat/Lon coordinates of the venue",
                            "$ref": "http://json-schema.org/geo"
                          }
                        },
                        "required": ["id","name","town","location"]
                      },
                      "startDateTime": {
                        "description": "DEPRECATED IN BETA 2! RFC-3339 formatted start date and time for the event",
                        "type": "string"
                      },
                      "endDateTime": {
                        "description": "DEPRECATED IN BETA 2! RFC-3339 formatted end date and time for the event",
                        "type": "string"
                      },
                      "startDate": {
                        "description": "RFC-3339 formatted start date for the event",
                        "type": "string"
                      },
                      "endDate": {
                        "description": "RFC-3339 formatted end date for the event",
                        "type": "string"
                      },
                      "startTimeString": {
                        "description": "Start time string for the event",
                        "type": "string"
                      },
                      "endTimeString": {
                        "description": "End time string for the event",
                        "type": "string"
                      }
                    },
                    "required": ["id","title","startDate","endDate"]
                  }
                },
                "image": {
                  "description": "Multiple image assets for the artist",
                  "type": "object",
                  "properties": {
                    "small": {
                      "description": "Small sized image",
                      "type": "object",
                      "properties": {
                        "url": {
                          "description": "Image source URL",
                          "type": "string"
                        },
                        "width": {
                          "description": "Image width (px)",
                          "type": "integer"
                        },
                        "height": {
                          "description": "Image height (px)",
                          "type": "integer"
                        }
                      },
                      "required": ["url","width","height"]
                    },
                    "medium": {
                      "description": "Medium sized image",
                      "type": "object",
                      "properties": {
                        "url": {
                          "description": "Image source URL",
                          "type": "string"
                        },
                        "width": {
                          "description": "Image width (px)",
                          "type": "integer"
                        },
                        "height": {
                          "description": "Image height (px)",
                          "type": "integer"
                        }
                      },
                      "required": ["url","width","height"]
                    },
                    "large": {
                      "description": "Medium sized image",
                      "type": "object",
                      "properties": {
                        "url": {
                          "description": "Image source URL",
                          "type": "string"
                        },
                        "width": {
                          "description": "Image width (px)",
                          "type": "integer"
                        },
                        "height": {
                          "description": "Image height (px)",
                          "type": "integer"
                        }
                      },
                      "required": ["url","width","height"]
                    },
                    "metadata": {
                      "description": "Metadata related to this image",
                      "type": "object",
                      "properties": {
                        "copyright": {
                          "description": "The copyright holder for this image",
                          "type": "string"
                        },
                        "caption": {
                          "description": "Caption text for this image",
                          "type": "string"
                        }
                      },
                      "required": ["copyright","caption"]
                    }
                  }
                },
                "genre": {
                  "description": "The genre(s) the artist is found under",
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                },
                "webLink": {
                  "description": "URL for the web page for the artist on ents24.com",
                  "type": "string"
                },
                "viewsOnEnts24": {
                  "description": "The number of unique vistors to this artist's page on Ents24",
                  "type": "integer"
                },
                "fansOnEnts24": {
                  "description": "The number of Ents24 users tracking updates and announcements for this artist",
                  "type": "integer"
                },
                "lastUpdate": {
                  "description": "RFC-3339 formatted added/updated timestamp for this object",
                  "type": "string"
                }
              },
              "required": ["id","name","description","webLink","viewsOnEnts24","fansOnEnts24","lastUpdate"]
            }

### Image [/artist/image?id={id}&size={size}&format={format}]
An artist image retrieved as either a JSON object or JPEG image.

#### Artist Image [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the Event you want an image for.
  + size (optional, string, `medium`) ... Size of image you want [small, medium, large].
  + format (optional, string, `json`) ... The format of the response you want back from the resource [json, jpeg].

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
              "title": "Artist Image",
              "description": "An image asset for an artist",
              "type": "object",
              "properties": {
                "url": {
                  "description": "Image source URL",
                  "type": "string"
                },
                "width": {
                  "description": "Image width (px)",
                  "type": "integer"
                },
                "height": {
                  "description": "Image height (px)",
                  "type": "integer"
                },
                "metadata": {
                  "description": "Metadata related to this image",
                  "type": "object",
                  "properties": {
                    "copyright": {
                      "description": "The copyright holder for this image",
                      "type": "string"
                    },
                    "caption": {
                      "description": "Caption text for this image",
                      "type": "string"
                    }
                  },
                  "required": ["copyright","caption"]
                }
              },
              "required": ["url","width","height","metadata"]
            }

# Group Venue
Available resources on the Venue API endpoints.

### List [/venue/list?name={name}&location={location}&event_name={event_name}&event={event}&genre={genre}&results_per_page={results_per_page}&page={page}&incl_image={incl_image}&image_size={image_size}&incl_events={incl_events}&full_description={full_description}&updated_since={updated_since}]
Multiple venue objects with selected fields.  
***NB:*** *You must filter resources retrieved from this end-point with at least one of the following request parameters:*  
`name` `location` `event_name`

#### Venue List [GET]
+ Parameters
  + name (optional, string, `The Fleece`) ... The name of a venue.
  + location (optional, string, `bristol`) ... The location of venue(s) you want a listing for.
  + event_name (optional, string, `BBC Radio 2 Live In Hyde Park`) ... The name for an event you want an venue list for.<br />***NB:*** *Values applied to this parameter may match more than one event!<br />You should use the `event/read` end-point to retrieve data for a particular event.*
  + event (optional, string, `BBC Radio 2 Live In Hyde Park`) ... **DEPRECATED IN BETA 2! You should use the `event_name` parameter instead**
  + genre (optional, string, `rock`) ... The genre of event you want a venues listing for.
  + results_per_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
  + page (optional, integer, `1`) ... The page/chunk of results to be requested.
  + incl_image (optional, boolean, `1`) ... Decides whether or not an artist image is included in the response.
  + image_size (optional, string, `medium`) ... Chooses the size of image included with each venue object if one is available.
  + incl_events (optional, boolean, `1`) ... Decides whether or not a list of upcoming events is included with each venue object in the response.
  + full_description (optional, boolean, `0`) ... Decides whether full or summarised description text is included in the response. 
  + updated_since (optional, date, `YYYY-MM-DD`) ... Only retrive venues that have been added/updated since the given date.

+ Request

    + Headers

            Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Next-Page: R2U=
            X-Previous-Page: bUw=
            X-Total-Items-Found: 75

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "Venue List",
              "description": "A list of Venue objects with selected fields",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "id": {
                    "description": "Unique identifier for the venue",
                    "type": "string"
                  },
                  "name": {
                    "description": "Name of the venue",
                    "type": "string"
                  },
                  "town": {
                    "description": "Town or city where the venue is located",
                    "type": "string"
                  },
                  "county": {
                    "description": "The county where the venue is located",
                    "type": "string"
                  },
                  "location": {
                    "description": "Lat/Lon coordinates of the venue",
                    "$ref": "http://json-schema.org/geo"
                  },
                  "description": {
                    "description": "Description text for the venue",
                    "type": "string"
                  },
                  "events": {
                    "description": "Upcoming events at the venue",
                    "type": "array",
                    "items": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "description": "Unique identifier for an event",
                          "type": "string"
                        },
                        "title": {
                          "description": "Title of an event",
                            "type": "string"
                        },
                        "startDateTime": {
                          "description": "DEPRECATED IN BETA 2! RFC-3339 formatted start date and time for the event",
                          "type": "string"
                        },
                        "endDateTime": {
                          "description": "DEPRECATED IN BETA 2! RFC-3339 formatted end date and time for the event",
                          "type": "string"
                        },
                        "startDate": {
                          "description": "RFC-3339 formatted start date for the event",
                          "type": "string"
                        },
                        "endDate": {
                          "description": "RFC-3339 formatted end date for the event",
                          "type": "string"
                        },
                        "startTimeString": {
                          "description": "Start time string for the event",
                          "type": "string"
                        },
                        "endTimeString": {
                          "description": "End time string for the event",
                          "type": "string"
                        }
                      },
                      "required": ["id","title","startDate","endDate"]
                    }
                  },
                  "image": {
                    "description": "Single image asset for the venue",
                    "type": "object",
                    "properties": {
                      "url": {
                        "description": "Image source URL",
                        "type": "string"
                      },
                      "width": {
                        "description": "Image width (px)",
                        "type": "integer"
                      },
                      "height": {
                        "description": "Image height (px)",
                        "type": "integer"
                      },
                      "metadata": {
                        "description": "Metadata related to this image",
                        "type": "object",
                        "properties": {
                          "copyright": {
                            "description": "The copyright holder for this image",
                            "type": "string"
                          },
                          "caption": {
                            "description": "Caption text for this image",
                            "type": "string"
                          }
                        },
                        "required": ["copyright","caption"]
                      }
                    }
                  },
                  "webLink": {
                    "description": "URL for the web page for the venue on ents24.com",
                    "type": "string"
                  },
                  "viewsOnEnts24": {
                    "description": "The number of unique vistors to this venue's page on Ents24",
                    "type": "integer"
                  },
                  "fansOnEnts24": {
                    "description": "The number of Ents24 users tracking updates and announcements for this venue",
                    "type": "integer"
                  },
                  "lastUpdate": {
                    "description": "RFC-3339 formatted added/updated timestamp for this object",
                    "type": "string"
                  }
                },
                "required": ["id","name","town","location","description","webLink","viewsOnEnts24","fansOnEnts24","lastUpdate"]
              }
            }

+ Response 204

  + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Next-Page: MDg=
            X-Previous-Page: ZW0=
            X-Total-Items-Found: 75

### Read [/venue/read?id={id}&incl_events={incl_events}&incl_images={incl_images}&full_description={full_description}]
A venue object with all fields.

#### Venue [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the Artist you want full details for.
  + incl_events (optional, boolean, `1`) ... Decides whether or not a list of events at this venue at is included in the response.  
  + incl_images (optional, boolean, `1`) ... Decides whether or not an venue images are included in the response.  
  + full_description (optional, boolean, `1`) ... Decides whether full or summarised description text is included in the response. 

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
              "title": "Venue",
              "description": "A single Venue object with all fields",
              "type": "object",
              "properties": {
                "id": {
                  "description": "Unique identifier for the venue",
                  "type": "string"
                },
                "name": {
                  "description": "Name of the venue",
                  "type": "string"
                },
                "address": {
                  "description": "The location details for a venue",
                  "type": "object",
                  "properties": {
                    "streetAddress": {
                      "description": "The building name/number, street name and district",
                      "type": "array",
                      "items": {
                        "type": "string"
                      },
                      "minItems": 1
                    },
                    "town": {
                      "description": "Town or city where the venue is located",
                      "type": "string"
                    },
                    "county": {
                      "description": "The county where the venue is located",
                      "type": "string"
                    },
                    "postcode": {
                      "description": "Postal code for the venue address",
                      "type": "string"
                    },
                    "country": {
                      "description": "The country where the venue is located",
                      "type": "string"
                    }
                  },
                  "required": ["town","country"]
                },
                "location": {
                  "description": "Lat/Lon coordinates of the venue",
                  "$ref": "http://json-schema.org/geo"
                },
                "description": {
                  "description": "Description text for the venue",
                  "type": "string"
                },
                "website": {
                  "description": "URL for the venues website",
                  "type": "string"
                },
                "email": {
                  "description": "Email address for general enquires",
                  "type": "string"
                },
                "phone": {
                  "description": "Phone numbers for the venue",
                  "type": "object",
                  "properties": {
                    "enquires": {
                      "description": "Phone number for general enquires",
                      "type": "string"
                    },
                    "booking": {
                      "description": "Phone number for bookings",
                      "type": "string"
                    }
                  }
                },
                "events": {
                  "description": "Upcoming events at the venue",
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "description": "Unique identifier for an event",
                        "type": "string"
                      },
                      "title": {
                        "description": "Title of an event",
                          "type": "string"
                      },
                      "startDateTime": {
                        "description": "DEPRECATED IN BETA 2! RFC-3339 formatted start date and time for the event",
                        "type": "string"
                      },
                      "endDateTime": {
                        "description": "DEPRECATED IN BETA 2! RFC-3339 formatted end date and time for the event",
                        "type": "string"
                      },
                      "startDate": {
                        "description": "RFC-3339 formatted start date for the event",
                        "type": "string"
                      },
                      "endDate": {
                        "description": "RFC-3339 formatted end date for the event",
                        "type": "string"
                      },
                      "startTimeString": {
                        "description": "Start time string for the event",
                        "type": "string"
                      },
                      "endTimeString": {
                        "description": "End time string for the event",
                        "type": "string"
                      }
                    },
                    "required": ["id","title","startDate","endDate"]
                  }
                },
                "image": {
                  "description": "Multiple image assets for the venue",
                  "type": "object",
                  "properties": {
                    "small": {
                      "description": "Small sized image",
                      "type": "object",
                      "properties": {
                        "url": {
                          "description": "Image source URL",
                          "type": "string"
                        },
                        "width": {
                          "description": "Image width (px)",
                          "type": "integer"
                        },
                        "height": {
                          "description": "Image height (px)",
                          "type": "integer"
                        }
                      },
                      "required": ["url","width","height"]
                    },
                    "medium": {
                      "description": "Medium sized image",
                      "type": "object",
                      "properties": {
                        "url": {
                          "description": "Image source URL",
                          "type": "string"
                        },
                        "width": {
                          "description": "Image width (px)",
                          "type": "integer"
                        },
                        "height": {
                          "description": "Image height (px)",
                          "type": "integer"
                        }
                      },
                      "required": ["url","width","height"]
                    },
                    "large": {
                      "description": "Medium sized image",
                      "type": "object",
                      "properties": {
                        "url": {
                          "description": "Image source URL",
                          "type": "string"
                        },
                        "width": {
                          "description": "Image width (px)",
                          "type": "integer"
                        },
                        "height": {
                          "description": "Image height (px)",
                          "type": "integer"
                        }
                      },
                      "required": ["url","width","height"]
                    },
                    "metadata": {
                      "description": "Metadata related to this image",
                      "type": "object",
                      "properties": {
                        "copyright": {
                          "description": "The copyright holder for this image",
                          "type": "string"
                        },
                        "caption": {
                          "description": "Caption text for this image",
                          "type": "string"
                        }
                      },
                      "required": ["copyright","caption"]
                    }
                  }
                },
                "webLink": {
                  "description": "URL for the web page for the venue on ents24.com",
                  "type": "string"
                },
                "viewsOnEnts24": {
                  "description": "The number of unique vistors to this venue's page on Ents24",
                  "type": "integer"
                },
                "fansOnEnts24": {
                  "description": "The number of Ents24 users tracking updates and announcements for this venue",
                  "type": "integer"
                },
                "lastUpdate": {
                  "description": "RFC-3339 formatted added/updated timestamp for this object",
                  "type": "string"
                }
              },
              "required": ["id","name","town","location","description","webLink","viewsOnEnts24","fansOnEnts24","lastUpdate"]
            }

### Image [/venue/image?id={id}&size={size}&format={format}]
A venue image retrieved as either a JSON object or JPEG image.

#### Venue Image [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the venue you want an image for.
  + size (optional, string, `medium`) ... Size of image you want [small, medium, large].
  + format (optional, string, `json`) ... The format of the response you want back from the resource [json, jpeg].

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
              "title": "Venue Image",
              "description": "An image asset for an venue",
              "type": "object",
              "properties": {
                "url": {
                  "description": "Image source URL",
                  "type": "string"
                },
                "width": {
                  "description": "Image width (px)",
                  "type": "integer"
                },
                "height": {
                  "description": "Image height (px)",
                  "type": "integer"
                },
                "metadata": {
                  "description": "Metadata related to this image",
                  "type": "object",
                  "properties": {
                    "copyright": {
                      "description": "The copyright holder for this image",
                      "type": "string"
                    },
                    "caption": {
                      "description": "Caption text for this image",
                      "type": "string"
                    }
                  },
                  "required": ["copyright","caption"]
                }
              },
              "required": ["url","width","height","metadata"]
            }
