FORMAT: 1A
HOST: https://api.ents24.com

# Ents24 REST API (Beta 2)
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

# Group Location

### Search [/event/list?name={name}&postcode={postcode}&geo={geo}]
Search for unique location identifiers [postcode, lat,lonfor use as the value on Location request parameters.

#### Location Search [GET]
+ Parameters
  + name (optional, string, `Newcastle`) ... The name of the location your searching for.
  + postcode (optional, string, `NE82 6YY`) ... The postcode of the location your searching for.
  + geo (optional, string, `54.974384411995,-1.6015806376512`) ... Comma separated latitude and longitude of the location your searching for.

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
                  "postCodes": {
                    "description": "Valid postal codes for this location",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
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

### List [/event/list?location={location}&radius\_distance="{radius\_distance}"&distance\_unit="{distance\_unit}"&type={type}&genre={genre}&date={date}&date\_from={date\_from}&date\_to={date\_to}&venue\_name={venue\_name}&artist\_name={artist\_name}&results\_per\_page={results\_per\_page}&page={page}&incl\_image={incl\_image}&image\_size={image\_size}&incl\_artists={incl\_artists}&incl\_tickets={incl\_tickets}&full\_description={full\_description}&updated\_since={updated\_since}]
Multiple event objects with selected fields.  
***NB:*** *You must filter resources retrieved from this end-point with at least one of the following request parameters:*  
`location` `venue_name` `artist_name`

#### Event List [GET]
+ Parameters
  + location (optional, string, `postcode:SW1X 7LY`) ... The location of events you want a listing for. Values should be prefixed with the type of location data you are submitting. [name, postcode, geo].<br />***NB:*** *Values applied to this parameter with the `name` may be ambiguous E.G: Newcastle. Use `location/search` endpoint to find a unique location identifier (postcode or lat,lng) that matches the location you want.*
  + radius_distance (optional, integer, `10`) ... The furthest distance from the location you want events listed for.<br />***NB:*** *The `location` parameter is required when this parameter is set.*
  + distance_unit (optional, string, `mi`) ... The unit of measurment that should be applied to the radius\_distance value [mi, km].<br />***NB:*** *The `location` parameter is required when this parameter is set.*
  + genre (optional, string, `rock`) ... The genre of event type you want listed.
  + date (optional, date, `2014-09-03`) ... A specific date you want an events listing for.<br />***NB:*** *This parameter is disregarded if `date_from` and `date_to` parameters are set in the same request*.
  + date_from (optional, date, `2014-09-03`) ... The date you want an events listing from.<br />***NB:*** *This parameter is required when `date_to` parameter is set.*
  + date_to (optional, date, `2014-09-10`) ... The date you want an events listing to.<br />***NB:*** *This parameter is required when `date_from` parameter is set.*
  + venue_name (optional, string, `Hyde Park`) ... The venue you want an events listing for.<br />***NB:*** *Values applied to this parameter may match more than one venue!<br />You should use the `venue/read` end-point to get event listings for a particular venue.*
  + artist_name (optional, string, `Blondie`) ... The artist you want an events listing for.<br />***NB:*** *Values applied to this parameter may match more than one artist!<br />You should use the `artist/read` end-point to get an upcoming events list for a particular artist.*
  + results\_per\_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
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
                    "type": ["string","null"]
                  },
                  "headline": {
                    "description": "Headline of the event",
                    "type": ["string","null"]
                  },
                  "startDate": {
                    "description": "RFC-3339 formatted start date for the event",
                    "type": ["string","null"]
                  },
                  "endDate": {
                    "description": "RFC-3339 formatted end date for the event",
                    "type": ["string","null"]
                  },
                  "startTimeString": {
                    "description": "Start time string for the event",
                    "type": ["string","null"]
                  },
                  "endTimeString": {
                    "description": "End time string for the event",
                    "type": ["string","null"]
                  },
                  "isSoldOut": {
                    "description": "Flag to indicate whether the event is sold out.",
                    "type": "boolean"
                  },
                  "ticketsAvailable": {
                    "description": "Flag to indicate whether there are tickets available for the event.",
                    "type": "boolean"
                  },
                  "isFree": {
                    "description": "Flag to indicate whether the event is free entry.",
                    "type": "boolean"
                  },
                  "price": {
                    "description": "Price info for the event.",
                    "type": ["string","null"]
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
                        "type": ["string","null"]
                      },
                      "town": {
                        "description": "Town or city where the venue is located",
                        "type": ["string","null"]
                      },
                      "location": {
                        "description": "Lat/Lon coordinates of the venue",
                        "$ref": "http://json-schema.org/geo"
                      }
                    },
                    "required": ["id","name","town","location"]
                  },
                  "description": {
                    "description": "Description text for the event",
                    "type": ["string","null"]
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
                          "type": ["string","null"]
                        }
                      },
                      "required": ["name"]
                    }
                  },
                  "stages": {
                    "description": "Stages at the event",
                    "type": "array",
                    "items": {
                      "type": "object",
                      "properties": {
                        "name": {
                          "description": "Name of the stage",
                          "type": ["string","null"]
                        },
                        "days": {
                          "description": "Days or timespans performances are occuring on the stage",
                          "type": "array",
                          "items": {
                            "type": "object",
                            "properties": {
                              "id": {
                                "description": "Unique identifier for the stage day(s)",
                                "type": "string"
                              },
                              "startDate": {
                                "description": "The start date for this day or time-span",
                                "type": ["string","null"]
                              },
                              "endDate": {
                                "description": "The end date for this day or time-span",
                                "type": ["string","null"]
                              },
                              "artists": {
                                "description": "Performing artists",
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
                                      "type": ["string","null"]
                                    }
                                  },
                                  "required": ["name"]
                                }
                              }
                            },
                            "required": ["startDate","endDate"]
                          }
                        }
                      },
                      "required": ["name","days"]
                    }
                  },
                  "image": {
                    "description": "Multiple image assets for the event",
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
                            "type": ["string","null"]
                          },
                          "caption": {
                            "description": "Caption text for this image",
                            "type": ["string","null"]
                          }
                        },
                        "required": ["copyright","caption"]
                      }
                    },
                    "required": ["url","width","height","metadata"]
                  },
                  "tickets": {
                    "description": "Tickets for this event",
                    "type": "array",
                    "items": {
                      "type": "object",
                      "properties": {
                        "dateTime": {
                          "description": "RFC-3339 formatted date and time this ticket is valid for",
                          "type": ["string","null"]
                        },
                        "supplier": {
                          "description": "The supplier of this ticket",
                          "type": ["string","null"]
                        },
                        "price": {
                          "description": "The face-value price for this ticket",
                          "type": ["string","null"]
                        },
                        "totalPrice": {
                          "description": "The total price for this ticket",
                          "type": ["string","null"]
                        },
                        "inclBookingFee": {
                          "description": "Flag indicating whether a booking fee is included in the price of this ticket.",
                          "type": "boolean"
                        },
                        "onSaleFrom": {
                          "description": "RFC-3339 formatted date this ticket goes on sale",
                          "type": ["string","null"]
                        },
                        "onSaleUntil": {
                          "description": "RFC-3339 formatted date this ticket is / will be on sale until",
                          "type": ["string","null"]
                        },
                        "url": {
                          "description": "The purchase URL for this ticket",
                          "type": ["string","null"]
                        }
                      },
                      "required": ["dateTime","supplier","price","totalPrice","inclBookingFee","onSaleFrom","onSaleUntil","url"]
                    }
                  },
                  "genre": {
                    "description": "The genre(s) this event is found under",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  "webLink": {
                    "description": "URL for the web page for the event on ents24.com",
                    "type": "string"
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
                "required": ["id","title","headline","startDate","endDate","startTimeString","endTimeString","isSoldOut","ticketsAvailable","isFree","price","description","genre","webLink","fansOnEnts24","lastUpdate"]
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

### Read [/event/read?id={id}&incl\_artists={incl\_artists}&incl\_images={incl\_images}&incl\_tickets={incl\_tickets}&full\_description={full\_description}]
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
                  "type": ["string","null"]
                },
                "headline": {
                  "description": "Headline of the event",
                  "type": ["string","null"]
                },
                "startDate": {
                  "description": "RFC-3339 formatted start date for the event",
                  "type": ["string","null"]
                },
                "endDate": {
                  "description": "RFC-3339 formatted end date for the event",
                  "type": ["string","null"]
                },
                "startTimeString": {
                  "description": "Start time string for the event",
                  "type": ["string","null"]
                },
                "endTimeString": {
                  "description": "End time string for the event",
                  "type": ["string","null"]
                },
                "isSoldOut": {
                  "description": "Flag to indicate whether the event is sold out.",
                  "type": "boolean"
                },
                "ticketsAvailable": {
                  "description": "Flag to indicate whether there are tickets available for the event.",
                  "type": "boolean"
                },
                "isFree": {
                  "description": "Flag to indicate whether the event is free entry.",
                  "type": "boolean"
                },
                "price": {
                  "description": "Price info for the event.",
                  "type": ["string","null"]
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
                      "type": ["string","null"]
                    },
                    "town": {
                      "description": "Town or city where the venue is located",
                      "type": ["string","null"]
                    },
                    "location": {
                      "description": "Lat/Lon coordinates of the venue",
                      "$ref": "http://json-schema.org/geo"
                    }
                  },
                  "required": ["id","name","town","location"]
                },
                "description": {
                  "description": "Description text for the event",
                  "type": ["string","null"]
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
                        "type": ["string","null"]
                      }
                    },
                    "required": ["name"]
                  }
                },
                "stages": {
                  "description": "Stages at the event",
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "name": {
                        "description": "Name of the stage",
                        "type": ["string","null"]
                      },
                      "days": {
                        "description": "Days or timespans performances are occuring on the stage",
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "description": "Unique identifier for the stage day(s)",
                              "type": "string"
                            },
                            "startDate": {
                              "description": "The start date for this day or time-span",
                              "type": ["string","null"]
                            },
                            "endDate": {
                              "description": "The end date for this day or time-span",
                              "type": ["string","null"]
                            },
                            "artists": {
                              "description": "Performing artists",
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
                                    "type": ["string","null"]
                                  }
                                },
                                "required": ["name"]
                              }
                            }
                          },
                          "required": ["startDate","endDate"]
                        }
                      }
                    },
                    "required": ["name","days"]
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
                          "type": ["string","null"]
                        },
                        "caption": {
                          "description": "Caption text for this image",
                          "type": ["string","null"]
                        }
                      },
                      "required": ["copyright","caption"]
                    }
                  }
                },
                "tickets": {
                  "description": "Tickets for this event",
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "dateTime": {
                        "description": "RFC-3339 formatted date and time this ticket is valid for",
                        "type": ["string","null"]
                      },
                      "supplier": {
                        "description": "The supplier of this ticket",
                        "type": ["string","null"]
                      },
                      "price": {
                        "description": "The face-value price for this ticket",
                        "type": ["string","null"]
                      },
                      "totalPrice": {
                        "description": "The total price for this ticket",
                        "type": ["string","null"]
                      },
                      "inclBookingFee": {
                        "description": "Flag indicating whether a booking fee is included in the price of this ticket.",
                        "type": "boolean"
                      },
                      "isOnSale": {
                        "description": "Flag indicating whether the ticket is on sale.",
                        "type": "boolean"
                      },
                      "isAvailable": {
                        "description": "Flag indicating whether the ticket is available.",
                        "type": "boolean"
                      },
                      "isPresaleTicket": {
                        "description": "Flag indicating whether the ticket is a pre-sale ticket.",
                        "type": "boolean"
                      },
                      "isResaleTicket": {
                        "description": "Flag indicating whether the ticket is a re-sale ticket.",
                        "type": "boolean"
                      },
                      "onSaleFrom": {
                        "description": "RFC-3339 formatted date this ticket goes on sale",
                        "type": ["string","null"]
                      },
                      "onSaleUntil": {
                        "description": "RFC-3339 formatted date this ticket is / will be on sale until",
                        "type": ["string","null"]
                      },
                      "url": {
                        "description": "The purchase URL for this ticket",
                        "type": ["string","null"]
                      },
                      "email": {
                        "description": "The sales email address for this ticket.",
                        "type": ["string","null"]
                      },
                      "telephone": {
                        "description": "The sales phone line number for this ticket.",
                        "type": ["string","null"]
                      }
                    },
                    "required": ["dateTime","supplier","price","totalPrice","inclBookingFee","isOnSale","isAvailable","isPresaleTicket","isResaleTicket","onSaleFrom","onSaleUntil","url","email","telephone"]
                  }
                },
                "genre": {
                  "description": "The genre(s) this event is found under",
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                },
                "webLink": {
                  "description": "URL for the web page for the event on ents24.com",
                  "type": "string"
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
              "required": ["id","title","headline","startDate","endDate","startTimeString","endTimeString","isSoldOut","ticketsAvailable","isFree","price","description","genre","webLink","fansOnEnts24","lastUpdate"]
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

### List [/artist/list?name={name}&event\_name={event\_name}&genre={genre}&results\_per\_page={results\_per\_page}&page={page}&incl\_image={incl\_image}&image\_size={image\_size}&incl\_events={incl\_events}&full\_description={full\_description}&updated\_since={updated\_since}]
Multiple artist objects with selected fields.  
***NB:*** *You must filter resources retrieved from this end-point with at least one of the following request parameters:*  
`name` `event_name`

#### Artist List [GET]
+ Parameters
  + name (optional, string, `Blondie`) ... The string that matches artist names you want a list of.<br />***NB:*** *Values applied to this parameter may match more than one artist!<br />You should use the `artist/read` end-point to retrieve data for a particular artist.*
  + event_name (optional, string, `BBC Radio 2 Live In Hyde Park`) ... The name for an event you want an artists listing for.<br />***NB:*** *Values applied to this parameter may match more than one event!<br />You should use the `event/read` end-point to retrieve data for a particular event.*
  + genre (optional, string, `rock`) ... The genre you want an artists listing for.
  + results\_per\_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
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
                  "fansOnEnts24": {
                    "description": "The number of Ents24 users tracking updates and announcements for this artist",
                    "type": "integer"
                  },
                  "lastUpdate": {
                    "description": "RFC-3339 formatted added/updated timestamp for this object",
                    "type": "string"
                  }
                },
                "required": ["id","name","description","webLink","fansOnEnts24","lastUpdate"]
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

### Read [/artist/read?id={id}&incl\_events={incl\_events}&incl\_image={incl\_images}&full\_description={full\_description}]
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
                "fansOnEnts24": {
                  "description": "The number of Ents24 users tracking updates and announcements for this artist",
                  "type": "integer"
                },
                "lastUpdate": {
                  "description": "RFC-3339 formatted added/updated timestamp for this object",
                  "type": "string"
                }
              },
              "required": ["id","name","description","webLink","fansOnEnts24","lastUpdate"]
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

### List [/venue/list?name={name}&location={location}&radius\_distance="{radius\_distance}"&distance\_unit="{distance\_unit}"&event\_name={event\_name}&genre={genre}&results\_per\_page={results\_per\_page}&page={page}&incl\_image={incl\_image}&image\_size={image\_size}&incl\_events={incl\_events}&full\_description={full\_description}&updated\_since={updated\_since}]
Multiple venue objects with selected fields.  
***NB:*** *You must filter resources retrieved from this end-point with at least one of the following request parameters:*  
`name` `location` `event_name`

#### Venue List [GET]
+ Parameters
  + name (optional, string, `The Fleece`) ... The name of a venue.
  + location (optional, string, `postcode:SW1X 7LY`) ... The location of events you want a listing for. Values should be prefixed with the type of location data you are submitting. [name, postcode, geo].<br />***NB:*** *Values applied to this parameter with the `name` may be ambiguous E.G: Newcastle. Use `location/search` endpoint to find a unique location identifier (postcode or lat,lng) that matches the location you want.*
  + radius_distance (optional, integer, `10`) ... The furthest distance from the location you want events listed for.<br />***NB:*** *The `location` parameter is required when this parameter is set.*
  + distance_unit (optional, string, `mi`) ... The unit of measurment that should be applied to the radius\_distance value [mi, km].<br />***NB:*** *The `location` parameter is required when this parameter is set.*
  + event_name (optional, string, `BBC Radio 2 Live In Hyde Park`) ... The name for an event you want an venue list for.<br />***NB:*** *Values applied to this parameter may match more than one event!<br />You should use the `event/read` end-point to retrieve data for a particular event.*
  + genre (optional, string, `rock`) ... The genre of event you want a venues listing for.
  + results\_per\_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
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
                  "fansOnEnts24": {
                    "description": "The number of Ents24 users tracking updates and announcements for this venue",
                    "type": "integer"
                  },
                  "lastUpdate": {
                    "description": "RFC-3339 formatted added/updated timestamp for this object",
                    "type": "string"
                  }
                },
                "required": ["id","name","town","location","description","webLink","fansOnEnts24","lastUpdate"]
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

### Read [/venue/read?id={id}&incl\_events={incl\_events}&incl\_images={incl\_images}&full\_description={full\_description}]
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
                "fansOnEnts24": {
                  "description": "The number of Ents24 users tracking updates and announcements for this venue",
                  "type": "integer"
                },
                "lastUpdate": {
                  "description": "RFC-3339 formatted added/updated timestamp for this object",
                  "type": "string"
                }
              },
              "required": ["id","name","town","location","description","webLink","fansOnEnts24","lastUpdate"]
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
