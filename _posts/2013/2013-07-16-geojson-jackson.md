---
title: GeoJson POJOs for Jackson
description: Java-Library for parsing and writing GeoJson using Jackson annotations. Easy mapping of GeoJson objects to Java objects.
tagline: Parse and write GeoJson from Java
layout: post
category : hack
tags : [opensource, geojson, english]
author: adrianenglish
repository: https://github.com/opendatalab-de/geojson-jackson
snapshot: geojson-jackson-q.jpg
---

As a result of our latest project I've extracted a small set of Java Objects that can easily be serialized 
and deserialized into [GeoJson](http://www.geojson.org) files using the [Jackson JSON parser](http://jackson.codehaus.org/) library.
The java objects are quite optimized and use the Jackson annotations to identify the different types of GeoJson objects. 
This way you can save the "type" property within every object. On export the Jackson parser will automatically 
insert the type property based on the Java class name.

Without the GeoJson POJOs you would have to let Jackson parse the contents of a geojson file 
into HashMaps which I previously did like this:

	Map<String, Object> map = new ObjectMapper().readValue(inputStream,
	MapType.construct(HashMap.class, SimpleType.construct(String.class),
	SimpleType.construct(Object.class)));

After this you have to typecast every property and dive from HashMap into HashMap. 

Using the above library the mapping is much easier. Here are two examples how you read GeoJson data.
If you know what kind of data you expect from a GeoJson file you can directly parse the data:

	FeatureCollection featureCollection = 
	new ObjectMapper().readValue(inputStream, FeatureCollection.class);

Otherwise you can read a GeoJsonObject and decide the type using instanceOf checks:

	GeoJsonObject object = new ObjectMapper().readValue(inputStream, GeoJsonObject.class);
	if (object instanceOf Polygon) {
		...
	} else if (object instanceOf Feature) {
		...
	}

For more examples, please have a look at 
the [tests](https://github.com/opendatalab-de/geojson-jackson/tree/master/src/test/java/org/geojson/jackson) 
in the project repository. 

This library is available for download at Maven Central:

	<dependency>
		<groupId>de.grundid.opendatalab</groupId>
		<artifactId>geojson-jackson</artifactId>
		<version>1.0</version>
	</dependency>


If you want to contribute to this library, please check our GitHub repository:
[github.com/opendatalab-de/geojson-jackson](https://github.com/opendatalab-de/geojson-jackson)
