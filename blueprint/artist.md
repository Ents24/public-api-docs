FORMAT: 1A
HOST: https://api.ents24.com

# Ents24 REST API (Beta 3)
The Ents24 REST API gives you easy access to the UK's most comprehensive live entertainment database:  
A horde of event-listing experts add over 10,000 new listings every week!  
Easily use our data for your website or application.  

Licensing terms and conditions apply.

# Group Artist
Available resources on the Artist API endpoints.

### List [/artist/list?name={name}&like={like}&genre={genre}&results\_per\_page={results\_per\_page}&page={page}&incl\_image={incl\_image}&image\_size={image\_size}&full\_description={full\_description}&incl\_also\_liked={incl\_also\_liked}&updated\_since={updated\_since}&order\_by={order\_by}&order\_direction={order\_direction}]
Multiple artist objects with selected fields.  
***NB:*** *You must filter resources retrieved from this end-point with at least one of the following request parameters:*  
`name` `event_name`

#### Artist List [GET]
+ Parameters
  + name (optional, string, `Blondie`) ... The string that matches artist names you want a list of.<br />***NB:*** *Values applied to this parameter may match more than one artist!<br />You should use the `artist/read` end-point to retrieve data for a particular artist.*
  + like (optional, string, `oKkO`) ... Unique identifier string of the artist for which you want a list of similar artists.
  + genre (optional, string, `rock`) ... The genre you want an artists listing for.
  + incl\_image (optional, boolean, `1`) ... Decides whether or not an artist image is included in the response.
  + image\_size (optional, string, `medium`) ... Chooses the size of image included with each artist object if one is available.
  + full\_description (optional, boolean, `0`) ... Decides whether full or summarised description text is included in the response. 
  + incl\_also\_like (optional, boolean, `1`) ... Decides whether or not a list of IDs for similar artists is included in the response.
  + updated\_since (optional, date, `YYYY-MM-DD`) ... Only retrive artists that have been added/updated since the given date.
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
                    "type": ["string","null"]
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
                        "headline": {
                          "description": "Headline of the event",
                          "type": ["string","null"]
                        },
                        "title": {
                          "description": "Title of the event",
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
                  "fansAlsoLiked": {
                    "description": "Artists also liked by users who like the artist",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
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

### Read [/artist/read?id={id}&incl\_events={incl\_events}&incl\_image={incl\_images}&incl\_also\_liked={incl\_also\_liked}&full\_description={full\_description}]
An artist object with all fields.

#### Artist [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the Artist you want full details for.
  + incl\_events (optional, boolean, `1`) ... Decides whether or not a list of events the artists is performing at is included in the response.  
  + incl\_images (optional, boolean, `1`) ... Decides whether or not an artist images are included in the response.  
  + incl\_also\_like (optional, boolean, `1`) ... Decides whether or not a list of IDs for similar artists is included in the response.
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
                  "type": ["string","null"]
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
                      "headline": {
                        "description": "Headline of the event",
                        "type": ["string","null"]
                      },
                      "title": {
                        "description": "Title of the event",
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
                "fansAlsoLiked": {
                  "description": "A list of unique identifier strings for artists similar to this artist",
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
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

### Events [/artist/events?id={id}&results\_per\_page={results\_per\_page}&page={page}&incl\_image={incl\_image}&image\_size={image\_size}&incl\_stages={incl\_stages}&incl\_artists={incl\_artists}&incl\_occurrences={incl\_occurrences}&incl\_tickets={incl\_tickets}&full\_description={full\_description}&updated\_since={updated\_since}&order\_by={order\_by}&order\_direction={order\_direction}]
A list of events for an artist.

#### Artist Events [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the Artist you want full details for.
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
              "title": "Artist Events",
              "description": "A list of events for an artist",
              "type": "array",
              "items": { 
                "$ref": "https://raw.githubusercontent.com/Ents24/public-api-docs/beta3/response\_schemas/\_nested-event.schema.json" 
              }
            }

### Image [/artist/image?id={id}&size={size}&format={format}]
An artist image retrieved as either a JSON object or JPEG image.

#### Artist Image [GET]
+ Parameters
  + id (required, string, `oKkO`) ... Unique identifier string of the Event you want an image for.
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
