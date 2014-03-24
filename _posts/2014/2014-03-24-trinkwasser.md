---
title: Was steckt in meinem Leitungswasser?
description: Visualisierung der Inhaltsstofe und Härtegrade des Trinkwassers in der Stadt Heilbronn und (fast) allen Gemeinden im Landkreis Heilbronn - Natrium, Kalium, Calcium, Sulfat, Natrium, Magnesium, Chlorid
tagline: Region Heilbronn
layout: post
category: opendata
tags: [opendata, trinkwasser, ddj]
author: felix
repository: https://github.com/opendata-heilbronn/trinkwasser
snapshot: trinkwasser-screenshot-small.png
---

Trinkwasser gilt als das am besten kontrollierte Lebensmittel in Deutschland.
Und trotzdem wissen wir sehr wenig über das Wasser, das bei uns aus dem Hahn kommt.

Einige Kommunen veröffentlichen die Untersuchungsergebnisse des Trinkwassers zumindest auf ihren Webseiten, bei manchen wird nur der Härtegrad genannt.
Doch selbst wenn die Zahlen veröffentlicht sind, sind sie auf den Webseiten der Gemeinden oft schlecht auffindbar und bleiben für den Bürger eine abstrakte Größe.
Was bedeutet ein Härtegrad von 9?
Sind 200 Milligramm Calcium pro Liter viel oder wenig?
Wie mineralreich unser Leitungswasser ist, zeigt sich erst, wenn wir es untereinander und mit Wasser aus dem Handel vergleichen können. 

[Das ist für die Region Heilbronn jetzt möglich.](http://opendatalab.de/projects/trinkwasser)

[![Screenshot aus dem Projekt]({{ BASE_PATH }}/assets/trinkwasser-screenshot.png "Screenshot aus dem Projekt")](http://opendatalab.de/projects/trinkwasser)

Der Aufwand dieser Visualisierung war jedoch beträchtlich, weil es keine vollständige Datenbank für die Trinkwasser-Werte der Landkreise gibt
(im Fall der Trinkwasser-Preise stellt das [Statistische Landesamt](http://www.statistik.baden-wuerttemberg.de/SRDB/home.asp?E=GE) die Daten gesammelt zur Verfügung).
Jede Kommune veröffentlicht die Analyseberichte ihres Trinkwassers in Mitteilungsblättern und auf den Webseiten - jedoch nicht in maschinenlesbarer Form. 

Teilweise konnten die Daten, wie im Fall von Heilbronn und Neckarsulm, immerhin gescraped werden.
Bei vielen kleinen Landkreis-Kommunen mussten die Trinkwasseranalyse-Daten aber manuell in eine Excel-Datei übertragen werden.
Eine große Anzahl der Kommunen mussten wir sogar erst kontaktieren, um noch unveröffentlichte Daten abzufragen. 
Die Mühe hat sich jedoch gelohnt: Wir haben wir von fast allen Kommunen im Landkreis Heilbronn die Daten erhalten - nur drei fehlen noch.

Überraschend war für uns, wie unterschiedlich das Trinkwasser in der Region zusammengesetzt ist.
Teilweise differiert der Mineraliengehalt innerhalb einer Ortschaft sehr stark - nämlich dann, wenn es verschiedene Versorgungsbereiche gibt.
Kommunen wie Bad Friedrichshall, Neckarsulm oder Zaberfeld sind in mehrere Gebiete eingeteilt, was auch bei der Umsetzung des Tools eine zusätzliche Herausforderung war.
Die Gebiete mussten teilweise noch den Straßen zugeordnet werden, damit der Benutzer auch die korrekten Werte für seine eigene Straße angezeigt bekommt.
Auch dies war nur teilweise durch Scrapen möglich.

Die Idee zum Projekt entstand Ende Februar beim [Open Data Day in Heilbronn](http://blog.opendatalab.de/opendata/2014/01/15/opendataday-heilbronn/).
Dort wurde auch bereits an einem Prototyp gearbeitet, der nun Stück für Stück gemeinsam ausgebaut wurde. 

Das Projekt kann problemlos auch für andere Landkreise und Regionen weiterverwendet werden - der Sourcecode steht auf [GitHub](https://github.com/opendata-heilbronn/trinkwasser) zur Verfügung.
Wenn du Interesse hast, melde dich einfach bei uns - wir helfen dir bei der Umsetzung.

Mitgewirkt haben:
* [Vanessa Wormer](https://www.torial.com/vanessa.wormer) [@remrow](https://twitter.com/Remrow)
* Isabelle Müller [@isa_mue](https://twitter.com/isa_mue)
* Heiko Nicht [@HeikoNicht](https://twitter.com/HeikoNicht)
* Felix Ebert [@femeb](https://twitter.com/femeb)
* Ulrich Stech
* Alexander Walther [@alexplus_de](https://twitter.com/alexplus_de)
* Tom Görner
* Gerd Hoffmann

In Heilbronn treffen wir uns regelmäßig im Rahmen von [Code for Germany](http://codefor.de), um gemeinsam Open Data Projekten umzusetzen - das nächste Treffen findet am [10. April](http://pad.opendatacloud.de/p/OK-Lab-HN) in den Räumen des [CC86 Heilbronn e.V.](http://neu.cc86.org/) statt. Wir würden uns über deinen Besuch freuen!
