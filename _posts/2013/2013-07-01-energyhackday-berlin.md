---
title: "Live-Visualisierung der Berliner Energiedaten"
description: "Interaktive Karte der Berliner Bezirke, auf der im Abstand von 15-Minuten der Energieverbrauch live eingesehen werden kann"
tagline: "Berlin, Energyhackday"
layout: post
category : hack
tags : [hackday, energy]
author: felix
snapshot: energyhackday-q.jpg
repository: https://github.com/felixebert/energyhack
---

Auf dem [Energyhackday in Berlin](http://energyhack.de/) habe ich zusammen mit [Michael Hörz](http://www.michael-hoerz.de/) eine [Visualisierung der Verbrauchsdaten der Berliner Bezirke](http://felixebert.de/energyhackday) entwickelt.
Mit dieser Visualisierung kann schnell der Verlauf des Stromverbrauchs (und der Stromerzeugung) der Berliner Bezirke über einen Tag hinweg eingesehen werden.

<iframe src="http://felixebert.de/energyhackday/" width="100%" height="600"> </iframe>

Die aktuellen Daten zum Energieverbrauch der Bezirke werden von Stromnetz Berlin in 15-Minuten Intervallen über eine [Web-API](http://www.netzdaten-berlin.de/web/guest/suchen/-/details/web-service-last-und-erzeugung-berlin) bereitgestellt. Leider ist der Datenabruf noch etwas mühsam, da momentan jeder Bezirk nur einzeln abgefragt werden kann, die API auf XML basiert und der Response der Web-API keine [CORS-Header](http://enable-cors.org/server.html) mitschickt.

Aus diesem Grund hat Stefan Wehrmeyer einen Wrapper auf node.js Basis entwickelt, die diese Hindernisse beseitigt. Der Wrapper ist unter http://pure-headland-2592.herokuapp.com/ erreichbar, der Quellcode befindet sich auf [GitHub](https://github.com/stefanw/smeterengine-json). 

Weiterführende Informationen:
* [Review des Energyhackdays](http://okfn.de/2013/06/review-energy-hack-kreative-hacks-fur-die-energie-der-zukunft/) im [Open Knowledge Foundation Blog](http://okfn.de/blog/) - unter anderem mit dem Gewinner-Projekt Yoda, der seine Schüler vor zu hohem Stromverbrauch warnt: „Consuming this much energy leads you to the dark side“.
* [Sammlung an Datenquellen rund um das Thema Energie](http://de.okfnpad.org/energyhackdata), die am Energyhackday zur Verfügung standen
* [Liste der Projekte des Energyhackdays](http://de.okfnpad.org/energyhack)
