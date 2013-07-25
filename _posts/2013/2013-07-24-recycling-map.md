---
title: Recyclinghöfe und Müllabfuhrtermine visualisiert
description: 
tagline: Landkreis Heilbronn
layout: post
category : hack
tags : [opensource, gemeinde, recycling]
author: adrian
repository: https://github.com/opendatalab-de/recycling-map
snapshot: muellabfuhr.jpg
---

Die Themen Recycling und Müllabfuhrtermine beschäftigen mich schon seit längerer Zeit. 
Wäre es nicht schön, wenn man wie bei Google Now immer automatisch wüsste, wann welcher 
Mülleimer rausgestellt werden soll und wann der nächste gelegene Recyclinghof offen hat?

Mit offenen Daten seitens der Müllabfuhrunternehmen und des Landratsamtes wären solche 
Apps kein Problem. Nun sind die Daten eigentlich verfügbar. Auf den Seiten vom 
[Landratsamt](http://www.landkreis-heilbronn.de/sixcms/detail.php?id=10804&_nav=19947,19945) 
findet man in einer kleinen Auswahlliste rechts unten alle Recyclinghöfe im Landkreis. 
Möchte man auch die Daten wie Öffnungszeiten und Adresse erfahren muss man sich mühsam durch alle Optionen durchklicken. Das ist ziemlich umständlich.

Dasselbe gilt für die Müllabfuhrtermine. Auch hierzu bietet das Landratsamt eine entsprechende 
[Web-Seite](http://www.landkreis-heilbronn.de/sixcms/detail.php?id=10808&_nav=19947,19945) an. Die passende Auswahlliste ist diesmal rechts oben untergebracht und erlaubt den Zugriff auf eine PDF Datei mit dem Namen der entsprechenden Gemeinde. In dieser Abfuhrplan-PDF findet man einen bunten Kalender mit allen Abfuhrterminen für die Restmüll-, Biomüll- und Papiertonne.

Das Landratsamt geht noch einen Schritt weiter und offeriert seit einigen Monaten eine 
[App](http://www.landkreis-heilbronn.de/sixcms/detail.php?id=10926&_nav=10926&artikel=37893&template=presseartikel_detail_lra). 
In Zusammenarbeit mit der Firma idContor GmbH wird im 
[Google Play](https://play.google.com/store/apps/details?id=abfallH.ucom.de) und im Appstore eine 
App angeboten, die die aktuellen Abfuhrtermine und Recyclinghöfe darstellt. 
Die Daten sind akkurat und man kann sich eine Erinnerungsfunktion für das 
Rausstellen der entsprechenden Mülltonnen einrichten. Leider scheint gerade diese 
interessante Funktion etwas störanfällig zu sein, so dass nach einem Neustart des 
Smartphones keine weiteren Erinnerungen angezeigt werden.

Im Prinzip sind also die Daten vorhanden, nur leider nicht für jedermann 
in maschinenlesbarer Form verfügbar. Mit ein wenig Aufwand haben wir uns vorgenommen 
diese Informationen aufzubereiten und in einer einfachen Kartendarstellung zu präsentieren. 
Entstanden ist daraus die [Recycling-Map für den Landkreis Heilbronn](http://opendatalab.de/recycling-map/).

[![Screenshot aus dem Projekt]({{ BASE_PATH }}/assets/recycling-map-voll.jpg "Screenshot aus dem Projekt")](http://opendatalab.de/recycling-map/)

Auf einen Blick kann man hier alle Recyclinghöfe in seiner Umgebung sehen und anhand der Farbgebung der Gemeinden erkennen, 
an welchen Tagen der Müll rausgefahren wird.
Über einen Klick auf eine Gemeinde kann direkt die entsprechende PDF-Datei mit den genauen Müllabfuhrterminen geöffnet werden.

Die Anzeige der Recyclinghöfe auf der rechten Seite zeigt alle Öffnungszeiten im Wochenverlauf an 
und bietet somit einen einfachen Weg um seine Zeit in Bezug auf das Recycling zu organisieren.

Interessant an der farblichen Darstellung der Restmüllabfuhr ist, dass man leicht 
Gemeinde-Cluster erkennen kann, in denen die Leerung am selben Tag erfolgt.
Aufgrund diverser Feiertagsverschiebungen und unterschiedlicher Zyklen bei der Restmüll- und Biomüllabfuhr 
und der Tatsache, dass die Daten in ca. 46 PDF Dateien in einem bunten Kalender zerstreut sind, 
haben wir die Darstellung nur auf den Wochentag der regelmäßigen Restmüllleerung begrenzt. 
Das heißt, die farbliche Kennzeichnung der Gemeinde sagt aus, an welchem Wochentag 
normalerweise die Leerung erfolgt.

Dieses simple [Projekt](https://github.com/opendatalab-de/recycling-map) soll zeigen, wie man auf einfache Art und Weise den Zugang 
zu Informationen im Bereich Recycling und Müllabfuhr verbessern kann. In Zukunft hoffen wir, 
dass der Landkreis alle Daten über diesen Bereich offen und maschinenlesbar zur Verfügung stellen 
wird und wir eines Tages eine ähnliche Recycling-Map wie in der 
[Schweiz](http://recycling-map.ch/) anbieten können.
