FORMAT: 1A
HOST: https://api.ents24.com

# Ents24 REST API (Beta 3)
The Ents24 REST API gives you easy access to the UK's most comprehensive live entertainment database:  
A horde of event-listing experts add over 10,000 new listings every week!  
Easily use our data for your website or application.  

Licensing terms and conditions apply.

# Group Venue
Available resources on the Venue API endpoints.

### List [/venue/list?name={name}&like={like}&location={location}&radius\_distance={radius\_distance}&distance\_unit={distance\_unit}&results\_per\_page={results\_per\_page}&page={page}&incl\_image={incl\_image}&image\_size={image\_size}&full\_description={full\_description}&incl\_also\_liked={incl\_also\_liked}&updated\_since={updated\_since}&order\_by={order\_by}&order\_direction={order\_direction}]
Multiple venue objects with selected fields.  
***NB:*** *You must filter resources retrieved from this end-point with at least one of the following request parameters:*  
`name` `location` `event_name`

#### Venue List [GET]
+ Parameters
  + name (optional, string, `The Fleece`) ... The name of a venue.
  + like (optional, string, `oKkO`) ... Unique identifier string of the venue for which you want a list of similar venues.
  + location (optional, string, `postcode:SW1X 7LY`) ... The location of events you want a listing for. Values should be prefixed with the type of location data you are submitting. [name, postcode, geo].<br />***NB:*** *Values applied to this parameter with the `name` may be ambiguous E.G: Newcastle. Use `location/search` endpoint to find a unique location identifier (postcode or lat,lng) that matches the location you want.*
  + radius\_distance (optional, integer, `10`) ... The furthest distance from the location you want events listed for.<br />***NB:*** *The `location` parameter is required when this parameter is set.*
  + distance\_unit (optional, string, `mi`) ... The unit of measurment that should be applied to the radius\_distance value [mi, km].<br />***NB:*** *The `location` parameter is required when this parameter is set.*
  + incl\_image (optional, boolean, `1`) ... Decides whether or not an artist image is included in the response.
  + image\_size (optional, string, `medium`) ... Chooses the size of image included with each venue object if one is available.
  + full\_description (optional, boolean, `0`) ... Decides whether full or summarised description text is included in the response. 
  + incl\_also\_like (optional, boolean, `1`) ... Decides whether or not a list of IDs for similar venues is included in the response.
  + updated\_since (optional, date, `YYYY-MM-DD`) ... Only retrive venues that have been added/updated since the given date.
  + results\_per\_page (optional, integer, `25`) ... The number of results you want per page/chunk [25, 50, 100].
  + page (optional, integer, `1`) ... The page/chunk of results to be requested.
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
                    "type": ["string","null"]
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
                        }
                      },
                      "required": ["id","title","startDate","endDate"]
                    }
                  },
                  "images": {
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
                "required": ["id","name","location","description","webLink","viewsOnEnts24","fansOnEnts24","lastUpdate"] 
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

### Read [/venue/read?id={id}&incl\_events={incl\_events}&incl\_images={incl\_images}&incl\_also\_liked={incl\_also\_liked}&full\_description={full\_description}]
A venue object with all fields.

#### Venue [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the Artist you want full details for.
  + incl\_events (optional, boolean, `1`) ... Decides whether or not a list of events at this venue at is included in the response.  
  + incl\_images (optional, boolean, `1`) ... Decides whether or not an venue images are included in the response.  
  + incl\_also\_like (optional, boolean, `1`) ... Decides whether or not a list of IDs for similar venues is included in the response.
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
                  "type": ["string","null"]
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
                      }
                    },
                    "required": ["id","title","startDate","endDate"]
                  }
                },
                "images": {
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
                "webLink": {
                  "description": "URL for the web page for the venue on ents24.com",
                  "type": "string"
                },
                "viewsOnEnts24": {
                  "description": "The number of unique vistors to this venue's page on Ents24",
                  "type": "integer"
                },
                "fansAlsoLiked": {
                  "description": "A list of unique identifier strings for venues similar to this venue",
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
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
              "required": ["id","name","location","description","webLink","viewsOnEnts24","fansOnEnts24","lastUpdate"]
            }

### Events [/venue/events?id={id}&results\_per\_page={results\_per\_page}&page={page}&incl\_image={incl\_image}&image\_size={image\_size}&incl\_stages={incl\_stages}&incl\_artists={incl\_artists}&incl\_occurrences={incl\_occurrences}&incl\_tickets={incl\_tickets}&full\_description={full\_description}&updated\_since={updated\_since}&order\_by={order\_by}&order\_direction={order\_direction}]
A list of events for a venue.

#### Venue Events [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the Venue you want full details for.
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

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "Venue Events",
              "description": "A list of events for a venue",
              "type": "array",
              "items": { 
                "$ref": "https://raw.githubusercontent.com/Ents24/public-api-docs/beta3/response\_schemas/\_nested-event.schema.json" 
              }
            }

### Image [/venue/image?id={id}&size={size}&format={format}]
A venue image retrieved as either a JSON object or JPEG image.

#### Venue Image [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the venue you want an image for.
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
