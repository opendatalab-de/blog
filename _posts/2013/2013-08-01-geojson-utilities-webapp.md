---
title: GeoJson Utilites für den Export von Verwaltungsgrenzen
description: Export von Gemeinde-, Landkreis- und Bundeslandgrenzen ins GeoJson Format inkl. Fläche und Einwohnerzahlen
tagline: 
layout: post
category: hack
tags: [geojson, opendata]
author: adrian
repository: https://github.com/opendatalab-de/simple-geodata-selector
snapshot: geojson-utilities-s.jpg
---

Bei der Umsetzung von dem [Finanzdatenvergleich für NRW](https://kfd.piratenfraktion-nrw.de/) 
haben wir recht viel Zeit mit der Zusammenstellung und Konvertierung der notwendigen GeoDaten verbracht. 
Die vom [Geodatenzentrum](http://www.geodatenzentrum.de/geodaten/gdz_rahmen.gdz_div?gdz_spr=deu&gdz_akt_zeile=5&gdz_anz_zeile=0&gdz_user_id=0) 
bereitgestellten Daten sind im sogenannten Shape-Format (SHP) und damit nicht im webtauglichen 
Format wie GeoJson vorhanden. Die reine Konvertierung der Daten von einer SHP-Datei zu einer 
GeoJson Datei ist recht leicht mit GDAL Tools möglich, jedoch enthalten die SHP Dateien alle 
Land- und Wasserflächen Deutschlands und das ist nicht immer das was man braucht.

In diesem Zusammenhang und für zukünftige Visualisierungen haben wir eine WebApp entwickelt, 
die es uns langfristig erlauben wird schnell und mit wenigen Clicks, die benötigten Daten 
zusammenzustellen. Auf der Webseite der GeoJson Utilities sieht man auf einen Blick alle 
Landkreise und kreisfreie Städte und kann sie je nach Wunsch auswählen. Danach kann mit 
einem Click eine GeoJson Datei mit den entsprechenden Gemeindegrenzen, Landkreisgrenzen 
oder Bundeslandgrenzen erstellt werden.

Für spezielle Auswertungen haben wir auch die neusten Einwohnerzahlen vom statistischen 
Bundesamt in die GeoJson Daten integriert. Da die Daten vom Geodatenzentrum die Flächen 
der Gemeinden und Landkreise bereits enthalten lassen sich somit sehr schnell Daten 
visualisieren und pro Einwohner bzw. pro Fläche umrechnen.

Um die Funktionalität für den Anfang abzurunden ist es auch möglich bereits vorhandene 
GeoJson Dateien in dem Tool zu visualisieren. Dazu genügt es einfach die GeoJson Datei 
in das Browserfenster zu ziehen und schon werden die Daten aus der Datei auf der Karte 
dargestellt. Da hierbei kein Upload der Daten erfolgt, können auf diese Weise sehr schnell 
auch recht große GeoJson Dateien visualisiert werden.

[![Screenshot aus dem Projekt]({{ BASE_PATH }}/assets/geojson-utilities.jpg "Screenshot aus dem Projekt")](http://opendatalab.de/projects/geojson-utilities/)

Wir hoffen, dass dieses Tool vielen Entwicklern bei Hackathons und OpenData Days den 
Zugriff auf die entsprechenden Grenzflächen vereinfacht und es ihnen erlaubt direkt 
mit der Umsetzung ihrer Ideen loszulegen statt erst mühsam Rohdaten zu konvertieren.

Als weitere Zielgruppe sehen wir auch die Datenjournalisten, die dieses Tool zur 
Datenaufbereitung für ihre Blog-Posts nutzen können.

Um die WebApp langfristig mit weiteren Features anzureichern würden wir gerne von 
euch hören, welche Funktionen für euch in der Aufbereitung von Geodaten nützlich wären. 
Habt ihr Ideen?

