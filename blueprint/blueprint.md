FORMAT: 1A
HOST: http://api.ents24.com

# Ents24 REST API (Beta 1)
The Ents24 REST API gives you easy access to the the UK's most comprehensive live entertainment database:  
A horde of event-listing experts add over 10,000 new listings every week!  
Easily use our data for your website or application.  

Licensing terms and conditions apply.

# Group Client Authentication
In order to use the Ents24 public API you must first register as a developer, once you have your API client credentials you may use them to authenticate your requests to the API.

### Request Access Token [/auth/token]
To obtain an access token you must authenticate your client credentials with our authentication server.

#### Auth Token [POST]
+ Request (application/x-www-form-urlencoded)

    + Headers

            Cache-Control: no-cache

    + Body

            client_id=aho0bVpKdFURaZ37tkYT&client_secret=uQmfyQsqeKfIMJg4FKQ9gi8cSLFXATpGFyBx038nHy

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT

    + Body

            {
              access_token: "qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA"
              token_type: "Bearer"
              expires: 1414317411
              expires_in: 5184000
            }

# Group Event
Available actions on the event resource.

### Genres [/event/genres]
A list of all valid event genres.

#### Event Genres [GET]
+ Request

    + Headers

            Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA
            Cache-Control: no-cache

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

### List [/event/list?location={location}&type={type}&genre={genre}&date={date}&date_from={date_from}&date_to={date_to}&venue={venue}&venue_id={venue_id}&artist={artist}&artist_id={artist_id}&results_per_page={results_per_page}&page={page}&incl_image={incl_image}&full_description={full_description}&updated_since={updated_since}]
Multiple event objects with selected fields.

#### Event List [GET]
+ Parameters
  + location (optional, string, `London`) ... The location of events you want a listing for.
  + genre (optional, string, `rock`) ... The genre of event type you want listed.
  + date (optional, date, `2014-09-03`) ... A specific date you want an events listing for.<br />***NB:*** *This parameter is disregarded if `date_from` and `date_to` parameters are set in the same request*.
  + date_from (optional, date, `2014-09-03`) ... The date you want an events listing from.<br />***NB:*** *This parameter is required when `date_to` parameter is set.*
  + date_to (optional, date, `2014-09-10`) ... The date you want an events listing to.<br />***NB:*** *This parameter is required when `date_from` parameter is set.*
  + venue (optional, string, `Hyde Park`) ... The venue you want an events listing for.
  + venue_id (optional, string, `lRx9`) ... The unique identifier for a venue you want an events listing for.
  + artist (optional, string, `Blondie`) ... The artist you want an events listing for.
  + artist_id (optional, string, `njyZ`) ... The unique identifier for an artist you want an events listing for.
  + results_per_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
  + page (optional, integer, `1`) ... The page/chunk of results to be requested.
  + incl_image (optional, boolean, `1`) ... Decides whether or not an event image is included in the response.
  + full_description (optional, boolean, `0`) ... Decides whether full or summarised description text is included in the response. 
  + updated_since (optional, date, `2014-08-31`) ... Only retrive events that have been added/updated since the given date.

+ Request

    + Headers

            Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA
            Cache-Control: no-cache

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Current-Page: 2
            X-Next-Page: https://api.ents24.com/event/list?...&page=3
            X-Previous-Page: https://api.ents24.com/event/list?...&page=1
            X-Total-Items-Found: 75
            X-Total-Pages: 3

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "Event Collection",
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
                        "required": ["id", "name", "town"]
                    },
                    "startDateTime": {
                      "description": "RFC-3339 formatted start date and time the event",
                      "type": "string"
                    },
                    "endDateTime": {
                      "description": "RFC-3339 formatted end date and time the event",
                      "type": "string"
                    },
                    "description": {
                      "description": "Description text for the event",
                      "type": "string"
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
                                  "description": "Image width",
                                  "type": "integer"
                              },
                              "height": {
                                  "description": "Image height",
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
                                  "required": ["copyright", "caption"]
                              }
                          },
                          "required": ["metadata", "url", "width", "height"]
                  },
                      "webLink": {
                          "description": "URL for the web page for the event on ents24.com",
                          "type": "string"
                      }
                },
                "required": ["id", "title", "startDateTime", "endDateTime", "description", "webLink"]
              }
            }

+ Response 204

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            X-Total-Items-Found: 0
            X-Total-Pages: 0

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
            Cache-Control: no-cache

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Current-Page: 1
            X-Total-Items-Found: 1
            X-Total-Pages: 1

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
                      "required": ["id", "name", "town"]
                  },
                  "startDateTime": {
                    "description": "RFC-3339 formatted start date and time the event",
                    "type": "string"
                  },
                  "endDateTime": {
                    "description": "RFC-3339 formatted end date and time the event",
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
                          "required": ["id", "name"]
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
                                      "description": "Image width",
                                      "type": "integer"
                                  },
                                  "height": {
                                      "description": "Image height",
                                      "type": "integer"
                                  }
                              },
                              "required": ["url", "width", "height"]
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
                                      "description": "Image width",
                                      "type": "integer"
                                  },
                                  "height": {
                                      "description": "Image height",
                                      "type": "integer"
                                  }
                              },
                              "required": ["url", "width", "height"]
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
                                      "description": "Image width",
                                      "type": "integer"
                                  },
                                  "height": {
                                      "description": "Image height",
                                      "type": "integer"
                                  }
                              },
                              "required": ["url", "width", "height"]
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
                              "required": ["copyright", "caption"]
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
                      "description": "The genre(s) this event is found under",
                      "type": "array",
                      "items": {
                          "type": "object",
                          "properties": {
                              "supplier": {

                              },
                              "price": {

                              },
                              "dateTime": {

                              },
                              "url": {

                              },
                              "onSaleFrom": {

                              },
                              "onSaleUntil": {

                              }
                          },
                          "required": ["supplier", "price", "dateTime", "onSaleUntil"]
                      }
                  },
                  "webLink": {
                      "description": "URL for the web page for the event on ents24.com",
                      "type": "string"
                  }
              },
              "required": ["id", "title", "startDateTime", "endDateTime", "description", "webLink"]
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
            Cache-Control: no-cache

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Current-Page: 1
            X-Total-Items-Found: 1
            X-Total-Pages: 1

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
                      "description": "Image width",
                      "type": "integer"
                  },
                  "height": {
                      "description": "Image height",
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
                      "required": ["copyright", "caption"]
                  }
              },
              "required": ["url", "width", "height", "metadata"]
            }

# Group Artist
Available actions on the artist resource.

### List [/artist/list?genre={genre}&event={event}&event_id={event_id}&results_per_page={results_per_page}&page={page}&incl_image={incl_image}&full_description={full_description}&updated_since={updated_since}]
Multiple artist objects with selected fields.

#### Artist List [GET]
+ Parameters
  + genre (optional, string, `rock`) ... The genre of artist you want listed.
  + event (optional, string, `BBC Radio 2 Live In Hyde Park`) ... The name for an event you want an artists listing for.
  + event_id (optional, string, `mDDaoO`) ... The unique identifier for an event you want an artists listing for.
  + results_per_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
  + page (optional, integer, `1`) ... The page/chunk of results to be requested.
  + incl_image (optional, boolean, `1`) ... Decides whether or not an artist image is included in the response.
  + full_description (optional, boolean, `0`) ... Decides whether full or summarised description text is included in the response. 
  + updated_since (optional, date, `YYYY-MM-DD`) ... Only retrive artists that have been added/updated since the given date.

+ Request

    + Headers

            Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA
            Cache-Control: no-cache

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Current-Page: 2
            X-Next-Page: https://api.ents24.com/event/list?...&page=3
            X-Previous-Page: https://api.ents24.com/event/list?...&page=1
            X-Total-Items-Found: 75
            X-Total-Pages: 3

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "Artist Collection",
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
                    "image": {
                          "description": "Single image asset for the artist",
                          "type": "object",
                          "properties": {
                              "url": {
                                  "description": "Image source URL",
                                  "type": "string"
                              },
                              "width": {
                                  "description": "Image width",
                                  "type": "integer"
                              },
                              "height": {
                                  "description": "Image height",
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
                                  "required": ["copyright", "caption"]
                              }
                          }
                      },
                      "webLink": {
                          "description": "URL for the web page for the artist on ents24.com",
                          "type": "string"
                      }
                },
                "required": ["id", "name", "description", "webLink"]
              }
            }

+ Response 204

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            X-Total-Items-Found: 0
            X-Total-Pages: 0

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
            Cache-Control: no-cache

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Current-Page: 1
            X-Total-Items-Found: 1
            X-Total-Pages: 1

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
                                  "required": ["id","name","location"]
                              },
                              "startDateTime": {
                                  "description": "RFC-3339 formatted start date and time the event",
                                  "type": "string"
                              },
                              "endDateTime": {
                                  "description": "RFC-3339 formatted end date and time the event",
                                  "type": "string"
                              }

                          },
                          "required": ["id", "title", "startDateTime", "endDateTime"]
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
                                      "description": "Image width",
                                      "type": "integer"
                                  },
                                  "height": {
                                      "description": "Image height",
                                      "type": "integer"
                                  }
                              },
                              "required": ["url", "width", "height"]
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
                                      "description": "Image width",
                                      "type": "integer"
                                  },
                                  "height": {
                                      "description": "Image height",
                                      "type": "integer"
                                  }
                              },
                              "required": ["url", "width", "height"]
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
                                      "description": "Image width",
                                      "type": "integer"
                                  },
                                  "height": {
                                      "description": "Image height",
                                      "type": "integer"
                                  }
                              },
                              "required": ["url", "width", "height"]
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
                              "required": ["copyright", "caption"]
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
                  }
              },
              "required": ["id", "name", "description", "webLink"]
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
            Cache-Control: no-cache

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Current-Page: 1
            X-Total-Items-Found: 1
            X-Total-Pages: 1

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
                      "description": "Image width",
                      "type": "integer"
                  },
                  "height": {
                      "description": "Image height",
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
                      "required": ["copyright", "caption"]
                  }
              },
              "required": ["url", "width", "height", "metadata"]
            }

# Group Venue
Available actions on the venue resource.

### List [/venue/list?name={name}&location={location}&results_per_page={results_per_page}&page={page}&incl_image={incl_image}&full_description={full_description}&updated_since={updated_since}]
Multiple venue objects with selected fields.

#### Venue List [GET]
+ Parameters
  + name (optional, string, `The Fleece`) ... The name of a venue.
  + location (optional, string, `bristol`) ... The location of venue(s) you want a listing for.
  + results_per_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
  + page (optional, integer, `1`) ... The page/chunk of results to be requested.
  + incl_image (optional, boolean, `1`) ... Decides whether or not an artist image is included in the response.
  + full_description (optional, boolean, `0`) ... Decides whether full or summarised description text is included in the response. 
  + updated_since (optional, date, `YYYY-MM-DD`) ... Only retrive venues that have been added/updated since the given date.

+ Request

    + Headers

            Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA
            Cache-Control: no-cache

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Current-Page: 2
            X-Next-Page: https://api.ents24.com/event/list?...&page=3
            X-Previous-Page: https://api.ents24.com/event/list?...&page=1
            X-Total-Items-Found: 75
            X-Total-Pages: 3

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "Venue Collection",
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
                    "image": {
                          "description": "Single image asset for the venue",
                          "type": "object",
                          "properties": {
                              "url": {
                                  "description": "Image source URL",
                                  "type": "string"
                              },
                              "width": {
                                  "description": "Image width",
                                  "type": "integer"
                              },
                              "height": {
                                  "description": "Image height",
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
                                  "required": ["copyright", "caption"]
                              }
                          }
                      },
                      "webLink": {
                          "description": "URL for the web page for the venue on ents24.com",
                          "type": "string"
                      }
                },
                "required": ["id", "name", "location", "description", "webLink"]
              }
            }

+ Response 204

  + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            X-Total-Items-Found: 0
            X-Total-Pages: 0

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
            Cache-Control: no-cache

+ Response 200 (application/json)

  + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Current-Page: 1
            X-Total-Items-Found: 1
            X-Total-Pages: 1

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
                      "required": ["town", "country"]
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
                                  "description": "RFC-3339 formatted start date and time the event",
                                  "type": "string"
                              },
                              "endDateTime": {
                                  "description": "RFC-3339 formatted end date and time the event",
                                  "type": "string"
                              }
                          },
                          "required": ["id","title","startDateTime","endDateTime"]
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
                                      "description": "Image width",
                                      "type": "integer"
                                  },
                                  "height": {
                                      "description": "Image height",
                                      "type": "integer"
                                  }
                              },
                              "required": ["url", "width", "height"]
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
                                      "description": "Image width",
                                      "type": "integer"
                                  },
                                  "height": {
                                      "description": "Image height",
                                      "type": "integer"
                                  }
                              },
                              "required": ["url", "width", "height"]
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
                                      "description": "Image width",
                                      "type": "integer"
                                  },
                                  "height": {
                                      "description": "Image height",
                                      "type": "integer"
                                  }
                              },
                              "required": ["url", "width", "height"]
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
                              "required": ["copyright", "caption"]
                          }
                      }
                  },
                  "webLink": {
                      "description": "URL for the web page for the venue on ents24.com",
                      "type": "string"
                  }
              },
              "required": ["id", "name", "location", "description", "webLink"]
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
            Cache-Control: no-cache

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT
            X-Current-Page: 1
            X-Total-Items-Found: 1
            X-Total-Pages: 1

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
                      "description": "Image width",
                      "type": "integer"
                  },
                  "height": {
                      "description": "Image height",
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
                      "required": ["copyright", "caption"]
                  }
              },
              "required": ["url", "width", "height", "metadata"]
            }