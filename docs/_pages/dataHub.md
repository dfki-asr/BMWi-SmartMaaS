---
title: "Linked Data Hub"
permalink: "/datahub/"
layout: single
author_profile: false
classes: wide
---
The Linked Data Hub provides an HTTP endpoint that wraps remote SPARQL endpoints behind a classic HTTP API.
Each HTTP call injects the parameters submitted with the call into a parameterized SPARQL query. This query is then executed against a SPARQL query endpoint, as defined by the Linked Data Hub server.
The result set is returned as paginated Hydra Result set.

* [Hydra Core Vocabulary](https://www.hydra-cg.com/spec/latest/core/){:target="_blank"}

## Architecture

![Linked Data Hub Architecture](/assets/images/Datahub_simplified.png){: .align-center }


## Public Service Base URI:

A public Linked Data Hub service endpoint is provided under the following URL:

    https://smartmaas.dfki.de/service/gtfsld

## Public Service HTTP API:

### HTTP Method:
    GET

### Content-Type Headers:
    Following parameters triggers the text/data format accordingly.    
    application/ld+json
    application/n-quads
    application/n-triples
    application/rdf+json
    application/rdf+xml
    application/trix
    application/x-turtle
    text/n3;charset=utf-8
    text/trig text/turtle

### HTTP Endpoints
	
* ### / 
    List all available endpoints
* ### /api/v1/providers/
    Paginates all available gtfs:Providers as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId:.+}
    Requests a particular gtfs:Provider(FLIXBUS, RNV etc)
* ### /api/v1/providers/{providerId}/itinerary/
    Paginates itinerary information available gtfs:Connections as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId}/stations/{stationId}
    Requests a particular gbfs:Station
* ### /api/v1/providers/{providerId}/stations/
    Paginates all available gbfs:Stations as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId}/status/
    Paginates all available gbfs:Status as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId}/status/{statusId}
    Requests a particular gbfs:Status
* ### /api/v1/providers/{providerId}/hours/
    Paginates all available gbfs:Hours as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId}/hours/{hourId}
    Requests a particular gbfs:Hours
* ### /api/v1/providers/{providerId}/routes/{routeId:.+}
    Requests a particular gtfs:Route
* ### /api/v1/providers/{providerId}/routes/
    Paginates all available gtfs:Routes as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId}/stops/{stopId}
    Requests a particular gtfs:Stop
* ### /api/v1/providers/{providerId}/stops/nearBy
    Paginates all gtfs:Stops nearby a given geographical position
* ### /api/v1/providers/{providerId}/stops/search
    Paginates all gtfs:Stops found by a text query
* ### /api/v1/providers/{providerId}/stops/
    Paginates all available gtfs:Stops as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId}/trips/{tripId:.+}
    Requests a particular gtfs:Trip
* ### /api/v1/providers/{providerId}/trips/
    Paginates all available gtfs:Trips as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId}/connections/
    Paginates all available gtfs:Connections as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId}/connections/{connectionId:.+}
    Requests a particular gtfs:Connection
* ### /api/v1/providers/{providerId}/agencies/
    Paginates all available gtfs:Agencies as hydra:PartialCollectionViews
* ### /api/v1/providers/{providerId}/agencies/{agencyId:.+}
    Requests a particular gtfs:Agency   


