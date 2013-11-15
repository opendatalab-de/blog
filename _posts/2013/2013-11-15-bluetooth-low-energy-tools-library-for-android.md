---
title: Bluetooth Low Energy Tools and Library for Android
description: Collection of tools to parse bluetooth characteristics and to communicate with sensors.
tagline: 
layout: post
category: hack
tags: [english, android, ble, opensource]
author: adrianenglish
repository: https://github.com/grundid/bletools
snapshot: ble-parser.jpg
---

The last few days I’ve spent exploring some of the possibilities of [Bluetooth Low Energy on Android](http://developer.android.com/guide/topics/connectivity/bluetooth-le.html). 
For that I used a Nexus 5 phone, a FitBit Flex and some [Tokencube sensors](http://www.starnberger.at/tokencube/).

What came out is a simple Android app that can scan for sensors and interact with then. 
For example, the Tokencubes have temperature and orientation sensors and you can use the 
app to read out this data.

Besides the app I also started working on a [Bluetooth Low Energy Tools](https://github.com/grundid/bletools) 
library. Since BLE is a quite new technology there aren’t many libraries to use and since there are lots of 
[GATT Services](https://developer.bluetooth.org/gatt/services/Pages/ServicesHome.aspx) 
and [Characteristics](https://developer.bluetooth.org/gatt/characteristics/Pages/CharacteristicsHome.aspx) 
it would be nice to have some reusable code.

The goals of the library are as follows:
*	design and implement patterns for the communication with BLE sensors
*	implement parsers for all the known characteristics
*	collect and implement parsers for proprietary sensors and characteristics
*	implement classes to read all values of a sensor
*	implement a fingerprint DB for sensors

For now I’ve implemented some characteristics parsers for the Tokencube sensors and of course 
I’ve created fingerprints for the FitBit Flex and the Tokencubes. The fingerprints allow you to identify a sensor
by looking at its services and characteristics. I plan to create an open database where everybody can 
store and access fingerprints for sensors.

At the moment these are just ideas, but it’s a start and I’ll add more characteristics parsers 
as soon as I have some reliable data to test them.
All official characteristics and services by the Bluetooth SID are defined in XML files. 
Unfortunately the XML specifications are too complicated to create a generic generator that would 
generate the source code for the characteristics parsers. I think the XML specifications 
have been designed with the intention to generate the documentation and not the parser code.

There are currently some [80 characteristics](https://developer.bluetooth.org/gatt/characteristics/Pages/CharacteristicsHome.aspx) 
defined and having a generator for them would 
be nice, but at the moment I’m going for the crowd sourced approach and I’m launching 
this [BLE Tools](https://github.com/grundid/bletools) project.

So this blog post is a first call for action. If you are working on BLE sensors and already 
have some characteristics parsers please try to contribute to the project.
