---
title: 'GBFS'
permalink: '/gbfs/'
layout: single
author_profile: false
classes: wide
---

General Bikeshare Feed Specification, abbreviated as GBFS, provides a standardized data feed for bike share system. [GBFS](https://github.com/amohoste/gbfs-linked) makes real-time data feeds in a uniform format publicly available online, with an emphasis on findability. [GBFS](https://github.com/amohoste/gbfs-linked) is intended to make information publicly available online; therefore information that is personally identifiable is not currently and will not become part of the core specification. [GBFS](https://github.com/amohoste/gbfs-linked) is intended as a specification for real-time, read-only data - any data being written back into individual bikeshare systems are excluded from this spec

We provide a free and ready-to-use data processing system which transforms and publishes [GBFS](https://github.com/amohoste/gbfs-linked) archives into [Linked Data](https://github.com/amohoste/gbfs-linked) using Linked GBFS and [Linked Connections](https://linkedconnections.org/) vocabularies.

## GBFS Features

-   SPARQL service to query GBFS live data
-   Conversion of GBFS archives to Linked Data

## SPARQL API/Service Features

The presented offline novel solution is a micro-service, allows to send semantic queries against the legacy Web interfaces directly, and returns the result in RDF. The service API follows the SPARQL 1.1 Query API specification, and also supports federated queries over distributed endpoints, allowing an easy and accessible way for semantically enriched data integration over legacy endpoints.

-   Performs SPARQL queries against non-RDF datasets.
-   Is not dependent of a certain source format, as long as the source to be queried is structured.

## System Overview

![image-center](/assets/images/GBFS_call_sequence.png){: .align-center}

## SPARQL WRAPPER

![image-center](/assets/images/GBFS_sparql_wrapper.png){: .align-center}

## EXAMPLE QUERY

```
prefix rml: <http://semweb.mmlab.be/ns/rml#>
prefix carml: <http://carml.taxonic.com/carml/>
prefix rr: <http://www.w3.org/ns/r2rml#>
prefix ql: <http://semweb.mmlab.be/ns/ql#>
prefix wgs84_pos: <http://www.w3.org/2003/01/geo/wgs84_pos#>
prefix gbfs: <https://github.com/amohoste/gbfs-linked/blob/master/linked_data/ontology.ttl#>


CONSTRUCT
{
	?station a gbfs:Station , wgs84_pos:SpatialThing ;
			 gbfs:name ?station_name ;
			 wgs84_pos:lat_lon ?lat_lon_pos .

	?bike_id a gbfs:Bike ;
			 wgs84_pos:location ?station .
}
WHERE {
		?bike_id a gbfs:Bike ;
			wgs84_pos:lat ?bike_lat ;
			wgs84_pos:long ?bike_lon .
		SERVICE <http://[HOST]:[PORT]/query?mapping=http://[HOST]:[PORT]/mapping/station&source=https://gbfs.nextbike.net/maps/gbfs/v1/nextbike_bf/de/station_information.json>
		{
			?station a gbfs:Station ;
				gbfs:name ?station_name ;
				wgs84_pos:lat ?lat ;
				wgs84_pos:long ?lon .
		}
		FILTER( (abs(?bike_lat-?lat) < 0.001) && (abs(?bike_lon-?lon) < 0.001) )
		BIND (CONCAT(str(?lat), "," , str(?lon)) as ?lat_lon_pos)
}
```

## EXAMPLE CALL

```
http://[HOST]:[PORT]/query/?query=<examplequery>
	&source=https://gbfs.nextbike.net/maps/gbfs/v1/nextbike_bf/de/free_bike_status.json
	&mapping=http://[HOST]:[PORT]/gbfs
```
