---
title: Mein Bad Wimpfen - die Bad Wimpfen App 
description: Ein City Guide mit Open Data
tagline:
layout: post
category: opendata
tags: []
author: adrian
snapshot: mein-badwimpfen.png
---

Der Markt der CityApps ist sehr groß. Fast jede größere Stadt und vor allem Touristenorte bieten in den Apps Stores
eigene Apps an, die den Besucher über das Geschehene vor Ort informieren sollen. Einige Softwarehersteller bieten
mittlerweile diese Apps von der Stange an, die einen Mix aus einer Webseite und einiger nativer Funktionen darstellen.
Über die Herkunft und Aktualität der Inhalte wird selten ein Wort gesagt. Ob es die Location noch gibt und ob sie offen 
ist erfährt der Besucher erst, wenn er vor der Tür steht. Wenn es um aktuelle Termine geht, wird der Anwender 
dann doch lieber auf die Homepage der Stadt verwiesen statt ihm sinnvolle Funktionen zur Übernahme des Events in 
seinen Terminkalender anzubieten.

Wir von [Code For Heilbronn](http://codefor.de/heilbronn/) haben uns was anderes überlegt und in 
Zusammenarbeit mit der [Stadt Bad Wimpfen](http://www.badwimpfen.de) einen
einfachen aber auch gleichzeitig coolen City Guide für Bad Wimpfen entwickelt. Unser City Guide basiert auf 
drei Themen: Events, Locations und Sehenswürdigkeiten.

Den aktuellen Eventkalender haben wir von der Stadt Bad Wimpfen kostenlos und als Open Data zur Verfügung 
gestellt bekommen. Dies erlaubt uns alle Daten uneingeschränkt in die App einzubauen und zu verwenden. Wir 
aktualisieren die Daten alle 24h und bieten den Benutzen damit einen topaktuellen Eventkalender direkt in der App 
an. Wo das Event stattfindet kann sofort auf der Karte auf dem Smartphone nachgeschaut werden und bei 
Bedarf kann dahin navigiert werden. Mit nur einem Klick wird der Termin in den eigenen Terminkalender übernommen. 
Alle Details, wie Start- und Endzeit, der Ort und die Beschreibung werden direkt im Terminkalender angezeigt.
Aus dem Terminkalender kann der Termin natürlich mit Freunden geteilt werden und weitere Teilnehmer 
können eingeladen werden.
Um bei den über 400 Events in Bad Wimpfen die Übersicht nicht zur verliehren, bietet ein komfortabler Filter
die Möglichkeit bestimmte Events auszublenden.

![Termin in der App]({{ BASE_PATH }}/assets/bwapp/IMG_0082.PNG "Terminanzeige in der App")
![Terminübernahme]({{ BASE_PATH }}/assets/bwapp/IMG_0083.PNG "Terminübernahme")
![Eigener Terminkalender]({{ BASE_PATH }}/assets/bwapp/IMG_0084.PNG "Eigener Terminkalender")
  
Die Locations haben wir zum Teil aus dem offenen Locations-Portal [gonam.de](http://gonam.de) übernommen, aber auch selbst recherchiert.
Dadurch bietet der City Guide eine aktuelle Übersicht der Top-Locations in Bad Wimpfen an. Diese können sowohl als Liste,
aber auch auf einer Karte dargestellt werden. Natürlich kann auch hier leicht zu einer bestimmten Location navigiert werden.
Ein Klick auf das Höhrericon und man kann einen Tisch reservieren. Ein Klick auf das Home-Icon und die Homepage wird angezeigt.
Für verschiedene Locations haben wir auch die Bewertungen aus anderen Portalen recherchiert. Langfristig würden
wir jedoch gerne unsere User die Locations auch bewerten lassen.

![Liste der Locations]({{ BASE_PATH }}/assets/bwapp/IMG_0086.PNG "Liste der Locations")
![Karte mit Locations]({{ BASE_PATH }}/assets/bwapp/IMG_0087.PNG "Karte mit Locations")
![Locationdetails]({{ BASE_PATH }}/assets/bwapp/IMG_0088.PNG "Locationdetails")
 
Unser City Guide listet auch eine Auswahl an den bekanntesten Sehenswürdigkeiten der Stadt. Vom Blauen Turm 
bis hin zur Stadtkirche sind alle Attraktionen enthalten. Alle Sehenswürdigkeiten werden mit Bild gezeigt.
Eine Karte mit Satelitenansicht ist ebenfalls vorhanden und erlaubt die Orientierung innerhalb der Stadt.
Zu den meisten Gebäuden haben wir eine Beschreibung und das Baujahr hinzugefügt.
Als Quelle für die Inhalten haben wir auf die Wikipedia zurückgegriffen. Dort wird eine umfangreiche [Liste 
aller Sehenswürdigkeiten und Denkmale](http://de.wikipedia.org/wiki/Liste_der_Kulturdenkmale_in_Bad_Wimpfen) 
in Bad Wimpfen gepflegt.

![Liste der Sehenswürdigkeiten]({{ BASE_PATH }}/assets/bwapp/IMG_0090.PNG "Liste der Sehenswürdigkeiten")
![Details zu einer Sehenswürdigkeit]({{ BASE_PATH }}/assets/bwapp/IMG_0091.PNG "Details zu einer Sehenswürdigkeit")
![Karte mit den Sehenswürdigkeiten]({{ BASE_PATH }}/assets/bwapp/IMG_0092.PNG "Karte mit den Sehenswürdigkeiten")

Als letztes Feature haben wir in die App die Anzeige der Wetterverhersage implementiert. Auch hier greifen wir auf die 
Dienste von Open Data zurück und bedienen uns der [OpenWeatherMap](http://openweathermap.org). Dort werden die 
Daten unter einer CC BY-SA Lizenz zur Verfügung gestellt. Wir rufen die Wettervorhersage für die nächsten 
drei Tage ab und zeigen sie automatisch, wenn der Benutzer die App öffnet. Um alle drei Tage zu sehen, 
genügt es den Screen einfach nach unten zu ziehen. 

![App im Einsatz]({{ BASE_PATH }}/assets/bwapp/bwapp-wetter.jpg "Bad Wimpfen App")

### Fazit

Dieses Projekt hat mal wieder gezeigt, dass mit etwas Wille und den entsprechenden Partnern 
([Thomas Michl](https://twitter.com/thomas_michl)) bei der Stadt
es doch möglich ist Open Data Projekte umzusetzen. Wir hoffen auf weitere Kooperationen und möchten auch in Zukunft die 
App weiter entwickeln.
Für uns war die Arbeit an dem Projekt sehr lehrreich. Wir haben eine neue Sprache gelernt (Swift) und haben mit der 
App eine gute Basis für weitere Projekte geschaffen. 

Die hier gezeigte App ist für das iPhone entwickelt worden und hat den Namen "Mein Bad Wimpfen". Wir haben sie erst vor Kurzem im App Store 
eingereicht und erwarten, dass sie bis zur KW20 von Apple freigeschaltet wird. Eine Android Version ist bereits in Planung
und wird je nach verfügbaren Resourcen umgesetzt.

Die App wurde von [Christian](http://appproject.de/) und [Adrian](http://grundid.de) entwickelt. 