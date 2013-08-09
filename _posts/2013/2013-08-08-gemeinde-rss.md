---
title: Gemeinde RSS Feed Aggregator
description: Alle Nachrichten aus deiner Gemeinde und Umgebung
tagline: 
layout: post
category: hack
tags: [gemeinde, opendata]
author: adrian
repository: https://github.com/opendatalab-de/gemeinde-rss
snapshot: gemeinde-rss-s.jpg
---

Die beste Art Nachrichten zu lesen ist für mich ein RSS Feed. Vor allem wenn er nach Keywords 
gefiltert und örtlich eingegrenzt werden kann. Die Gemeindenachrichten haben hier noch einen 
riesigen Nachholbedarf. Bei einer kurzen Analyse aller 46 Gemeinden im Landkreis Heilbronn 
stellt nur eine Gemeinde einen RSS Feed zur Verfügung. Da ich mich schon seit längerer Zeit 
mit dem Gedanken auseinander setze, einem RSS Feed Aggregator zu schreiben, habe ich kurzerhand 
beschlossen die Nachrichten/Aktuelles Seiten aller Gemeinden im LK HN zu erfassen und zu schauen, 
welche dieser Seiten mit einem verträglichen Aufwand analysiert werden können um die aktuellen 
Beiträge zu extrahieren.

Da ich in [Untergruppenbach](http://www.untergruppenbach.de) wohne, 
hatte diese Homepage natürlich die höchste Priorität. 
Sie ist mit TYPO3 umgesetzt und die [Aktuelles-Seite](http://www.untergruppenbach.de/index.php?id=7&publish[p]=7&publish[start]=1) hat eine überschaubare Struktur aus 
ListItem (LI) Elementen, die einen Titel, einen Link und das Datum des Beitrags enthalten. 
Diese Daten zu extrahieren war recht einfach. Als Weiteres habe ich gesehen, dass mehrere 
andere Gemeinde-Homepages von derselben Agentur eingerichtet wurden, so dass 
deren interner Aufbau mit den Seiten aus Untergruppenbach identisch war. Im Detail sind das 
die Gemeinden [Wüstenrot](http://www.gemeinde-wuestenrot.de), 
[Massenbachhausen](http://www.massenbachhausen.de), [Neudenau](http://www.neudenau.de), 
[Hardthausen](http://www.hardthausen.de), [Erlenbach](http://www.erlenbach-hn.de) 
und [Neckarwestheim](http://www.neckarwestheim.de).

Damit konnte ich mit recht einfachen Mitteln die Nachrichten aus sieben Gemeinden abrufen. 
Die gesammelten Daten werden ab jetzt einmal täglich in eine Datendank geschrieben. 
Duplikate werden rausgefiltert. Falls die Gemeinde kein Datum beim Beitrag hinterlegt hat, dann wird das
Datum an dem die Seite gescraped wurde als Beitrag-Datum erfasst. 
Somit wird man zumindest ab jetzt das Veröffentlichungsdatum auf einen Tag genau kennen, 
was durchaus einen Mehrwert schafft.

Auf der [Gemeinde-RSS](http://gemeinde-rss.grundid.de) Seite werden im Moment einfach 
alle Nachrichten in einer Liste nach Datum sortiert und mit einem Link zum ursprünglichen 
Artikel angezeigt. Diese Seite soll erstmal nur eine kleine Demo darstellen. Demnächst 
wird auch ein richtiger RSS Feed eingerichtet, der dann weiter mit einem entsprechenden 
Reader verarbeitet werden kann.

[![Screenshot aus dem Projekt]({{ BASE_PATH }}/assets/gemeinde-rss.png "Screenshot aus dem Projekt")](http://gemeinde-rss.grundid.de)

Als nächstes muss der [Scraper](https://github.com/opendatalab-de/gemeinde-scraper-tools) noch verbessert werden, damit er mehrere Seiten mit 
Nachrichten pro Gemeinde verarbeiten kann. Im Moment wird nur die erste Seite abgearbeitet. 
Viele Gemeinden zeigen hier jedoch nur 5 Beiträge an. Obwohl der Scraper die Seite täglich 
besucht, kann es vorkommen, dass eine Gemeinde mehr als 5 Beiträge an einem Tag 
veröffentlicht. In diesem Fall würden die Beiträge auf der zweiten Seite verloren gehen. 
Dies kann recht leicht korrigiert werden.

Darüber hinaus muss der Scraper noch auf andere Homepages ausgeweitet werden. Es gibt einige 
weitere Gemeinden, die zwar ältere Systeme verwenden, aber deren Aufbau wiederum für 
mehrere Gemeinden gleich ist. Diese zu identifizieren und den Scraper zu schreiben wird 
die nächste Aufgabe sein.

Bei all dieser Arbeit stellt sich natürlich die Frage, wieso betreibt jede Gemeinde 
eine eigene CMS Instanz? Jede Instanz muss auf die Dauer gesehen mit Updates und 
Patches versorgt werden. Keine der Gemeinden im LK verwendet die neuste TYPO3 Version. 
Viele haben die Version 4.5, die als LTS definiert ist, aber ich konnte nicht auf die 
Schnelle ermitteln, ob sie auch auf dem neusten Patchstand sind. Langfristig muss ein 
einheitliches System für die Gemeinden erstellt werden, der den administrativen Aufwand 
deutlich reduziert und den Zugang zu OpenData vereinfacht. 
Mal sehen, ob wir im LK HN was bewegen können.
