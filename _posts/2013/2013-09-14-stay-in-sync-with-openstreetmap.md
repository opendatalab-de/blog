---
title: Stay in sync with OpenStreetMap
description: How to stay in sync with OpenStreetMap using the osm-tools library
tagline: 
layout: post
category: hack
tags: [english, opensource, openstreetmap]
author: adrian
repository: https://github.com/grundid/osm-tools
snapshot: osmsync.jpg
---

The [Relation Analyzer for OpenStreetMap](http://ra.osmsurround.org) keeps a copy of all relations to provide a simple search 
function. You can easily search for the relation name or the type. Also some special attributes 
like the route or operator are available. 

Since the early days of the Relation Analyzer I copied from time to time the planet file and 
then started a script that would parse the file and extract all the relations from it. This 
process would take several hours and create a heavy load on my server. I wasn’t happy with this 
solution and this was the main reason why I never added this script as a cronjob so it would 
run automatically. Instead I waited until a user would send me an e-mail that he cannot find 
his relation in my Relation Analyzer. This was usually the time to launch the update script by hand.

During the last few weeks I was moving all of my projects to a new, more powerful server and 
in the process of doing so I decided to create a sync function that would automatically update the 
relations database with the OSM server. I always knew that OSM provides minutely, hourly and daily 
updates to its database and I even looked at the OSM-Change format a few months back. The format 
is quite simple: for every object (node, way, relation) in the OSM database you get the info if it 
was created, modified or deleted. Every dump gets a unique nine-digit sequence number. 
This sequence number is split into three parts where every part becomes a part of the 
directory structure. The latest sequence number can be obtained from a static URL. The details 
of this process can be found [here](http://wiki.openstreetmap.org/wiki/Planet.osm/diffs#Minute.2C_Hour.2C_and_Day_Files_Organisation).

Now, the idea to get into sync with OSM is simple: get a planet file and start downloading 
and merging the diff files somewhere before the planet file was created. This makes sure that 
you get all the updates and that you have a complete database. The only thing you have to 
make sure is not to add the same object twice. Usually this is accomplished by setting a 
unique index on the id row of the object.

Since most of my OSM functions are now part of 
the [osm-tools library](https://github.com/grundid/osm-tools) I also added this sync framework 
to this library. It can be found in the [osm-tools-process module](https://github.com/grundid/osm-tools/tree/master/osm-tools-process) in the package org.osmtools.osmchange.
To use the framework you have to three things. First decide how and where you want to sore your 
current sequence number. For this I created the [SequenceHandler](https://github.com/grundid/osm-tools/blob/master/osm-tools-process/src/main/java/org/osmtools/osmchange/SequenceHandler.java) 
interface with a [SimpleFileSequenceHandler](https://github.com/grundid/osm-tools/blob/master/osm-tools-process/src/main/java/org/osmtools/osmchange/SimpleFileSequenceHandler.java) 
default implementation. This implementation stores your current sequence number in a file. 
By creating your own implementation you can also store it in the database if you want. 

The second thing is to create an implementation of the [OsmChangeService](https://github.com/grundid/osm-tools/blob/master/osm-tools-process/src/main/java/org/osmtools/osmchange/OsmChangeService.java) 
interface. This interface contains a method that is called with every OsmChange object 
that is fetched from the OSM server. Since this task is quite similar in all implementations 
I’ve already created a dummy implementation that you can extend and override the process methods 
you are interested in. For example if you only want to listen for new relations you would extend 
the [AbstractOsmChangeService](https://github.com/grundid/osm-tools/blob/master/osm-tools-process/src/main/java/org/osmtools/osmchange/AbstractOsmChangeService.java) 
and override the createRelation method. 

The third thing is to wire everything up. In my case this looks like this:

	SequenceHandler sequenceHandler = new SimpleFileSequenceHandler(new File(args[0]));
	OsmChangeService osmChangeService = new RelationOsmChangeService();
	RestOperations restOperations = new RestTemplate();
	OsmChangeSyncService osmChangeSyncService = new OsmChangeSyncService(Granularity.hour, restOperations, osmChangeService, sequenceHandler);
	osmChangeSyncService.run();

There is one more thing. Since the OSM-Change files (osc) are packed with GZip some extra wiring 
is needed. As you can see I’m using the RestTemplate from the Spring Framework. 
The RestTemplate can automatically handle lots of content types. Unfortunately it cannot 
handle gzipped XML files (application/x-gzip). For this I created the 
[ReadOnlyGzipJaxb2HttpMessageConverter](https://github.com/grundid/osm-tools/blob/master/osm-tools-process/src/main/java/org/osmtools/osmchange/ReadOnlyGzipJaxb2HttpMessageConverter.java). 
As the name says this converter is only able to read gzipped XML files. It will use the 
JAXB framework to parse the OSM-Change file and create an object model. To wire it up you 
have to create the RestTemplate like this:

	RestTemplate restTemplate = new RestTemplate();
	restTemplate.getMessageConverters().add(new ReadOnlyGzipJaxb2HttpMessageConverter());

With all this knowledge you can now package everything up and plan your cronjob to run at the 
defined intervals. In my case I decided to update the database once an hour. This process 
takes about 2-3 sec and is acceptable as server load.

I hope this simple overview will encourage you to take a look at the 
[osm-tools library](https://github.com/grundid/osm-tools) and help you implement 
your own sync functions for OSM. You can find the binary release on the osm-tools library in 
[maven central](http://search.maven.org/#search|ga|1|g%3A%22de.grundid.osmtools%22). 
Please use at least use version 1.0.M7.

