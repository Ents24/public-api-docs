FORMAT: 1A
HOST: https://api.ents24.com

# Ents24 REST API (Beta 3)
The Ents24 REST API gives you easy access to the UK's most comprehensive live entertainment database:  
A horde of event-listing experts add over 10,000 new listings every week!  
Easily use our data for your website or application.  

Licensing terms and conditions apply.

# Group Event
Available resources on the Event API endpoints.

### Genres [/event/genres?parent\_key={parent\_key}&parent\_genres\_only={parent\_genres\_only}]
A list of all valid event genres.

#### Event Genres [GET]
+ Parameters
  + parent\_key (optional, string, `music`) ... The parent of genre you want a list of genres for. E.G: music, comedy or theatre-shows.
  + parent\_genres\_only (optional, boolean, `1`) ... Decides whether or not subgenres are included in the genre list. ***NB:*** *This parameter is disregarded if the `parent_key` parameter is set in the same request.*

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
                "type": "object",
                "properties": {
                  "key": {
                    "description": "The genre key. This is the value used in an Event object's `genre` property",
                    "type": "string"
                  },
                  "title": {
                    "description": "The genre title",
                    "type": ["string","null"]
                  },
                  "isChild": {
                    "description": "Flag showing if this genre object represents a subgenre of another genre",
                    "type": "boolean"
                  },
                  "parentKey": {
                    "description": "The key of the parent genre object. E.G: music, comedy or theatre-shows",
                    "type": "string"
                  }
                },
                "required": ["key","title","isChild"]
              }
            }

### List [/event/list?location={location}&radius\_distance={radius\_distance}&distance\_unit={distance\_unit}&type={type}&genre={genre}&date={date}&date\_from={date\_from}&date\_to={date\_to}&venue\_name={venue\_name}&artist\_name={artist\_name}&results\_per\_page={results\_per\_page}&page={page}&incl\_image={incl\_image}&image\_size={image\_size}&incl\_stages={incl\_stages}&incl\_artists={incl\_artists}&incl\_occurrences={incl\_occurrences}&incl\_tickets={incl\_tickets}&full\_description={full\_description}&updated\_since={updated\_since}&order\_by={order\_by}&order\_direction={order\_direction}]
Multiple event objects with selected fields.  
***NB:*** *You must filter resources retrieved from this end-point with at least one of the following request parameters:*  
`location` `venue_name` `artist_name`

#### Event List [GET]
+ Parameters
  + location (optional, string, `postcode:SW1X 7LY`) ... The location of events you want a listing for. Values should be prefixed with the type of location data you are submitting. [name, postcode, geo].<br />***NB:*** *Values applied to this parameter with the `name` may be ambiguous E.G: Newcastle. Use `location/search` endpoint to find a unique location identifier (postcode or lat,lng) that matches the location you want.*
  + radius\_distance (optional, integer, `10`) ... The furthest distance from the location you want events listed for.<br />***NB:*** *The `location` parameter is required when this parameter is set.*
  + distance\_unit (optional, string, `mi`) ... The unit of measurment that should be applied to the radius\_distance value [mi, km].<br />***NB:*** *The `location` parameter is required when this parameter is set.*
  + genre (optional, string, `rock`) ... The genre of event type you want listed.
  + date (optional, date, `2014-09-03`) ... A specific date you want an events listing for.<br />***NB:*** *This parameter is disregarded if `date_from` and `date\_to` parameters are set in the same request*.
  + date\_from (optional, date, `2014-09-03`) ... The date you want an events listing from.<br />***NB:*** *This parameter is required when `date\_to` parameter is set.*
  + date\_to (optional, date, `2014-09-10`) ... The date you want an events listing to.<br />***NB:*** *This parameter is required when `date_from` parameter is set.*
  + venue_name (optional, string, `Hyde Park`) ... The venue you want an events listing for.<br />***NB:*** *Values applied to this parameter may match more than one venue!<br />You should use the `venue/read` end-point to get event listings for a particular venue.*
  + artist_name (optional, string, `Blondie`) ... The artist you want an events listing for.<br />***NB:*** *Values applied to this parameter may match more than one artist!<br />You should use the `artist/read` end-point to get an upcoming events list for a particular artist.*
  + incl\_image (optional, boolean, `1`) ... Decides whether or not an event image is included in the response.
  + image\_size (optional, string, `medium`) ... Chooses the size of image included with each image object if one is available.
  + incl\_stages (optional, boolean, `1`) ... Decides whether or not a list of stages is included for any festival events in the response. 
  + incl\_artists (optional, boolean, `1`) ... Decides whether or not a list of performing artists is included in the response. 
  + incl\_occurrences (optional, boolean, `1`) ... Decides whether or not a list of individual event occurrences is included for any repeat events in the response.
  + incl\_tickets (optional, boolean, `1`) ... Decides whether or not a list of available tickets is included in the response.  
  + full\_description (optional, boolean, `0`) ... Decides whether full or summarised description text is included in the response. 
  + updated\_since (optional, date, `2014-08-31`) ... Only retrive events that have been added/updated since the given date.
  + results\_per\_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
  + page (optional, string, `ZW0=`) ... The page/chunk of results to be requested.
  + order\_by (optional, string, `lastUpdate`) ... Order events by the named object property.
  + order\_direction (optional, string, `desc`) ... Ordering direction [asc, desc].

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
                    "type": "string"
                  },
                  "endDate": {
                    "description": "RFC-3339 formatted end date for the event",
                    "type": "string"
                  },
                  "startTimeString": {
                    "description": "Start time string for the event",
                    "type": ["string","null"]
                  },
                  "endTimeString": {
                    "description": "End time string for the event",
                    "type": ["string","null"]
                  },
                  "hasMoved": {
                    "description": "Flag to indicate if an event has been moved to another location",
                    "type": "boolean"
                  },
                  "isCancelled": {
                    "description": "Flag to indicate if an event has been cancelled",
                    "type": "boolean"
                  },
                  "isPostponed": {
                    "description": "Flag to indicate if an event has been postponed",
                    "type": "boolean"
                  },
                  "isRescheduled": {
                    "description": "Flag to indicate if an event has been re-scheduled",
                    "type": "boolean"
                  },
                  "isSoldOut": {
                    "description": "Flag to indicate whether the event is sold out",
                    "type": "boolean"
                  },
                  "ticketsAvailable": {
                    "description": "Flag to indicate whether there are tickets available for the event",
                    "type": "boolean"
                  },
                  "isFree": {
                    "description": "Flag to indicate whether the event is free entry",
                    "type": "boolean"
                  },
                  "price": {
                    "description": "Price info for the event",
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
                          "type": "string"
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
                          "type": "string"
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
                                "type": "string"
                              },
                              "endDate": {
                                "description": "The end date for this day or time-span",
                                "type": "string"
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
                                      "type": "string"
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
                  "occurrences": {
                    "description": "The individual occurences of a repeated event (E.G. A theatre show)",
                    "type": "array",
                    "items": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "description": "Unique identifier for the event",
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
                          "type": ["string","null"]
                        },
                        "endTimeString": {
                          "description": "End time string for the event",
                          "type": ["string","null"]
                        },
                        "hasMoved": {
                          "description": "Flag to indicate if an event has been moved to another location",
                          "type": "boolean"
                        },
                        "isCancelled": {
                          "description": "Flag to indicate if an event has been cancelled",
                          "type": "boolean"
                        },
                        "isPostponed": {
                          "description": "Flag to indicate if an event has been postponed",
                          "type": "boolean"
                        },
                        "isRescheduled": {
                          "description": "Flag to indicate if an event has been re-scheduled",
                          "type": "boolean"
                        },
                        "isSoldOut": {
                          "description": "Flag to indicate whether the event is sold out",
                          "type": "boolean"
                        },
                        "ticketsAvailable": {
                          "description": "Flag to indicate whether there are tickets available for the event",
                          "type": "boolean"
                        },
                        "isFree": {
                          "description": "Flag to indicate whether the event is free entry",
                          "type": "boolean"
                        },
                        "price": {
                          "description": "Price info for the event",
                          "type": ["string","null"]
                        },
                        "tickets": {
                          "description": "Tickets for this event",
                          "type": "array",
                          "items": {
                            "type": "object",
                            "properties": {
                              "dateTime": {
                                "description": "RFC-3339 formatted date and time this ticket is valid for",
                                "type": "string"
                              },
                              "supplier": {
                                "description": "The supplier of this ticket",
                                "type": "string"
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
                                "description": "Flag indicating whether a booking fee is included in the price of this ticket",
                                "type": "boolean"
                              },
                              "isOnSale": {
                                "description": "Flag indicating whether the ticket is on sale",
                                "type": "boolean"
                              },
                              "isAvailable": {
                                "description": "Flag indicating whether the ticket is available",
                                "type": "boolean"
                              },
                              "isPresaleTicket": {
                                "description": "Flag indicating whether the ticket is a pre-sale ticket",
                                "type": "boolean"
                              },
                              "isResaleTicket": {
                                "description": "Flag indicating whether the ticket is a re-sale ticket",
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
                                "description": "The sales email address for this ticket",
                                "type": ["string","null"]
                              },
                              "telephone": {
                                "description": "The sales phone line number for this ticket",
                                "type": ["string","null"]
                              }
                            },
                            "required": ["dateTime","supplier","price","totalPrice","inclBookingFee","isOnSale","isAvailable","isPresaleTicket","isResaleTicket","onSaleFrom","onSaleUntil","url","email","telephone"]
                          }
                        }
                      },
                      "required": ["id","startDate","endDate","startTimeString","endTimeString","hasMoved","isCancelled","isPostponed","isRescheduled","isSoldOut","ticketsAvailable","isFree","price"]
                    }
                  },
                  "images": {
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
                          "type": "string"
                        },
                        "supplier": {
                          "description": "The supplier of this ticket",
                          "type": "string"
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
                          "description": "Flag indicating whether a booking fee is included in the price of this ticket",
                          "type": "boolean"
                        },
                        "isOnSale": {
                          "description": "Flag indicating whether the ticket is on sale",
                          "type": "boolean"
                        },
                        "isAvailable": {
                          "description": "Flag indicating whether the ticket is available",
                          "type": "boolean"
                        },
                        "isPresaleTicket": {
                          "description": "Flag indicating whether the ticket is a pre-sale ticket",
                          "type": "boolean"
                        },
                        "isResaleTicket": {
                          "description": "Flag indicating whether the ticket is a re-sale ticket",
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
                          "description": "The sales email address for this ticket",
                          "type": ["string","null"]
                        },
                        "telephone": {
                          "description": "The sales phone line number for this ticket",
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
                "required": ["id","title","headline","startDate","endDate","startTimeString","endTimeString","isSoldOut","ticketsAvailable","isFree","description","genre","webLink","fansOnEnts24","lastUpdate"]
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

### Read [/event/read?id={id}&incl\_artists={incl\_artists}&incl\_images={incl\_images}&incl\_tickets={incl\_tickets}&incl\_occurrences={incl\_occurrences}&full\_description={full\_description}]
An event object with all fields.

#### Event [GET]
+ Parameters
  + id (required, string, `mDDaoO`) ... Unique identifier string of the Event you want full details for.  
  + incl\_artists (optional, boolean, `1`) ... Decides whether or not a list of performing artists is included in the response.  
  + incl\_images (optional, boolean, `1`) ... Decides whether or not an event images are included in the response.  
  + incl\_tickets (optional, boolean, `1`) ... Decides whether or not a list of available tickets is included in the response.  
  + incl\_occurrences (optional, boolean, `1`) ... Decides whether or not a list of individual event occurrences is included in the response.
  + full\_description (optional, boolean, `1`) ... Decides whether full or summarised description text is included in the response. 

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
                  "type": "string"
                },
                "endDate": {
                  "description": "RFC-3339 formatted end date for the event",
                  "type": "string"
                },
                "startTimeString": {
                  "description": "Start time string for the event",
                  "type": ["string","null"]
                },
                "endTimeString": {
                  "description": "End time string for the event",
                  "type": ["string","null"]
                },
                "hasMoved": {
                  "description": "Flag to indicate if an event has been moved to another location",
                  "type": "boolean"
                },
                "isCancelled": {
                  "description": "Flag to indicate if an event has been cancelled",
                  "type": "boolean"
                },
                "isPostponed": {
                  "description": "Flag to indicate if an event has been postponed",
                  "type": "boolean"
                },
                "isRescheduled": {
                  "description": "Flag to indicate if an event has been re-scheduled",
                  "type": "boolean"
                },
                "isSoldOut": {
                  "description": "Flag to indicate whether the event is sold out",
                  "type": "boolean"
                },
                "ticketsAvailable": {
                  "description": "Flag to indicate whether there are tickets available for the event",
                  "type": "boolean"
                },
                "isFree": {
                  "description": "Flag to indicate whether the event is free entry",
                  "type": "boolean"
                },
                "price": {
                  "description": "Price info for the event",
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
                        "type": "string"
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
                        "type": "string"
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
                              "type": "string"
                            },
                            "endDate": {
                              "description": "The end date for this day or time-span",
                              "type": "string"
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
                                    "type": "string"
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
                "occurrences": {
                  "description": "The individual occurences of a repeated event (E.G. A theatre show)",
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "description": "Unique identifier for the event",
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
                        "type": ["string","null"]
                      },
                      "endTimeString": {
                        "description": "End time string for the event",
                        "type": ["string","null"]
                      },
                      "hasMoved": {
                        "description": "Flag to indicate if an event has been moved to another location",
                        "type": "boolean"
                      },
                      "isCancelled": {
                        "description": "Flag to indicate if an event has been cancelled",
                        "type": "boolean"
                      },
                      "isPostponed": {
                        "description": "Flag to indicate if an event has been postponed",
                        "type": "boolean"
                      },
                      "isRescheduled": {
                        "description": "Flag to indicate if an event has been re-scheduled",
                        "type": "boolean"
                      },
                      "isSoldOut": {
                        "description": "Flag to indicate whether the event is sold out",
                        "type": "boolean"
                      },
                      "ticketsAvailable": {
                        "description": "Flag to indicate whether there are tickets available for the event",
                        "type": "boolean"
                      },
                      "isFree": {
                        "description": "Flag to indicate whether the event is free entry",
                        "type": "boolean"
                      },
                      "price": {
                        "description": "Price info for the event",
                        "type": ["string","null"]
                      },
                      "tickets": {
                        "description": "Tickets for this event",
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "dateTime": {
                              "description": "RFC-3339 formatted date and time this ticket is valid for",
                              "type": "string"
                            },
                            "supplier": {
                              "description": "The supplier of this ticket",
                              "type": "string"
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
                              "description": "Flag indicating whether a booking fee is included in the price of this ticket",
                              "type": "boolean"
                            },
                            "isOnSale": {
                              "description": "Flag indicating whether the ticket is on sale",
                              "type": "boolean"
                            },
                            "isAvailable": {
                              "description": "Flag indicating whether the ticket is available",
                              "type": "boolean"
                            },
                            "isPresaleTicket": {
                              "description": "Flag indicating whether the ticket is a pre-sale ticket",
                              "type": "boolean"
                            },
                            "isResaleTicket": {
                              "description": "Flag indicating whether the ticket is a re-sale ticket",
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
                              "description": "The sales email address for this ticket",
                              "type": ["string","null"]
                            },
                            "telephone": {
                              "description": "The sales phone line number for this ticket",
                              "type": ["string","null"]
                            }
                          },
                          "required": ["dateTime","supplier","price","totalPrice","inclBookingFee","isOnSale","isAvailable","isPresaleTicket","isResaleTicket","onSaleFrom","onSaleUntil","url","email","telephone"]
                        }
                      }
                    },
                    "required": ["id","startDate","endDate","startTimeString","endTimeString","hasMoved","isCancelled","isPostponed","isRescheduled","isSoldOut","ticketsAvailable","isFree","price"]
                  }
                },
                "images": {
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
                        "type": "string"
                      },
                      "supplier": {
                        "description": "The supplier of this ticket",
                        "type": "string"
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
                        "description": "Flag indicating whether a booking fee is included in the price of this ticket",
                        "type": "boolean"
                      },
                      "isOnSale": {
                        "description": "Flag indicating whether the ticket is on sale",
                        "type": "boolean"
                      },
                      "isAvailable": {
                        "description": "Flag indicating whether the ticket is available",
                        "type": "boolean"
                      },
                      "isPresaleTicket": {
                        "description": "Flag indicating whether the ticket is a pre-sale ticket",
                        "type": "boolean"
                      },
                      "isResaleTicket": {
                        "description": "Flag indicating whether the ticket is a re-sale ticket",
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
                        "description": "The sales email address for this ticket",
                        "type": ["string","null"]
                      },
                      "telephone": {
                        "description": "The sales phone line number for this ticket",
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
              "required": ["id","title","headline","startDate","endDate","startTimeString","endTimeString","isSoldOut","ticketsAvailable","isFree","description","genre","webLink","fansOnEnts24","lastUpdate"]
            }

### Image [/event/image?id={id}&size={size}&format={format}]
An event image retrieved as either a JSON object or JPEG image.

#### Event Image [GET]
+ Parameters
  + id (required, string, `mDDaoO`) ... Unique identifier string of the Event you want an image for.
  + size (optional, string, `medium`) ... Size of image you want [small, medium, large].
  + format (optional, string, `json`) ... The format of the response you want back from the resource [json, file].

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