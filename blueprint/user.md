FORMAT: 1A
HOST: https://api.ents24.com

# Ents24 REST API (Beta 3.2)
The Ents24 REST API gives you easy access to the UK's most comprehensive live entertainment database:  
A horde of event-listing experts add over 10,000 new listings every week!  
Easily use our data for your website or application.  

Licensing terms and conditions apply.

# Group User
Available resources on the User API endpoints.<br />
***NB:*** *A user access token is required to make requests to these endpoints.<br />Please see the 'User Authentication' section for more details.*  

### Tracked Artists [/user/tracked-artists?updated\_since={updated\_since}]
A list of artists the user is tracking.

#### User Tracked Artists [GET]
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
              "title": "User Tracked Artists",
              "description": "A list of artists tracked by the user",
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
                  "upcomingEvents": {
                    "description": "The number of upcoming events on Ents24 for the artist",
                    "type": "integer"
                  },
                  "image": {
                    "description": "Image asset for the artist",
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
                  "fansAlsoLiked": {
                    "description": "A list of unique identifier strings for artsists similar to this artist",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  "lastUpdate": {
                    "description": "RFC-3339 formatted added/updated timestamp for this object",
                    "type": "string"
                  }
                },
                "required": ["id","name","description","upcomingEvents","webLink","fansOnEnts24","lastUpdate"]
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

### Tracked Venues [/user/tracked-venues?updated\_since={updated\_since}]
A list of venues the user is tracking.

#### User Tracked Venues [GET]
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
              "title": "User Tracked Venues",
              "description": "A list of venues tracked by the user",
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
                      },
                      "disabled": {
                        "description": "Phone number for disabled users",
                        "type": "string"
                      }
                    }
                  },
                  "upcomingEvents": {
                    "description": "The number of upcoming events on Ents24 for the venue",
                    "type": "integer"
                  },
                  "image": {
                    "description": "Image asset for the artist",
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
                  "webLink": {
                    "description": "URL for the web page for the venue on ents24.com",
                    "type": "string"
                  },
                  "fansOnEnts24": {
                    "description": "The number of Ents24 users tracking updates and announcements for this venue",
                    "type": "integer"
                  },
                  "fansAlsoLiked": {
                    "description": "A list of unique identifier strings for venues similar to this venue",
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  "lastUpdate": {
                    "description": "RFC-3339 formatted added/updated timestamp for this object",
                    "type": "string"
                  }
                },
                "required": ["id","name","location","description","webLink","fansOnEnts24","lastUpdate"] 
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

### Tracked Events [/user/tracked-events?updated\_since={updated\_since}]
A list of events the user is tracking.

#### User Tracked Events [GET]
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
              "title": "User Tracked Events",
              "description": "A list of events tracked by the user",
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
                  "image": {
                    "description": "Image asset for the event",
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

### Tracking Update [/user/tracking-update]
Make changes to the users tracked artists, venues and events.

#### User Tracking Update [POST]
+ Request

    + Headers

            Authorization: qnFqFAVw8pJMCF1z8tIMYoXwommArRmt9C08jIRA

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "User Tracking Updates Request",
              "description": "Entity tracking update requests for the user",
              "type": "object",
              "properties": {
                "lastSyncDate": {
                  "description": "RFC-3339 formatted timestamp for the last time the user client sent updates",
                  "type": "string"
                },
                "artists": {
                  "description": "Tracked artists",
                  "type": "array",
                  "items": { 
                    "type": "object",
                    "properties": {
                      "id": {
                        "description": "The unique identifier for the artist",
                        "type": "string"
                      },
                      "subscribed": {
                        "description": "RFC-3339 formatted timestamp for when this artist was tracked by the user",
                        "type": "string"
                      }
                    },
                    "required": ["id","subscribed"]
                  }
                },
                "venues": {
                  "description": "Tracked venues",
                  "type": "array",
                  "items": { 
                    "type": "object",
                    "properties": {
                      "id": {
                        "description": "The unique identifier for the venue",
                        "type": "string"
                      },
                      "subscribed": {
                        "description": "RFC-3339 formatted timestamp for when this venue was tracked by the user",
                        "type": "string"
                      }
                    },
                    "required": ["id","subscribed"]
                  }
                },
                "events": {
                  "description": "Tracked events",
                  "type": "array",
                  "items": { 
                    "type": "object",
                    "properties": {
                      "id": {
                        "description": "The unique identifier for the event",
                        "type": "string"
                      },
                      "subscribed": {
                        "description": "RFC-3339 formatted timestamp for when this event was tracked by the user",
                        "type": "string"
                      }
                    },
                    "required": ["id","subscribed"]
                  }
                }
              },
              "required": ["lastSyncDate","artists","venues","events"]
            }

+ Response 200 (application/json)

    + Headers

            Date: Tue, 26 Aug 2014 08:00:00 GMT
            Expires: Tue, 26 Aug 2014 09:00:00 GMT
            Last-Modified: Tue, 25 Aug 2014 22:10:00 GMT

    + Body

            {
              "$schema": "http://json-schema.org/draft-04/schema#",
              "title": "User Tracking Updates Response",
              "description": "Entity tracking updates for the user",
              "type": "object",
              "properties": {
                "lastSyncDate": {
                  "description": "RFC-3339 formatted timestamp for the last time the user client sent updates",
                  "type": "string"
                },
                "changes": {
                  "description": "Tracked artist updates",
                  "type": "array",
                  "items": { 
                    "type": "object",
                    "properties": {
                      "type": {
                        "description": "The type of tracked entity (E.G. `artist`)",
                        "type": "string"
                      },
                      "id": {
                        "description": "The unique identifier for the entity",
                        "type": "string"
                      },
                      "action": {
                        "description": "The action that should be taken for the entity (E.G. `track`)",
                        "type": "string"
                      },
                      "timestamp": {
                        "description": "RFC-3339 formatted timestamp showing when the action was scheduled for the entity",
                        "type": "string"
                      }
                    },
                    "required": ["type","id","action","timestamp"]
                  }
                }
              },
              "required": ["lastSyncDate","changes"]
            }
           