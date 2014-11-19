---
title: Kastanien App als Beispiel für die Nutzung des Baumkatasters
description: Ideensammlung und mögliche Ansätzung für die Nutzung des Baumkatasters als Open Data
tagline: 
layout: post
category: opendata
tags: [opendata]
author: adrian
repository: https://github.com/opendata-heilbronn/kastanien-app
snapshot: kastanien-app-s.png
---

Vor ein paar Monaten hat die Stadt Hamburg auf ihrem [Transparenzportal](http://transparenz.hamburg.de/) das [Baumkataster]( http://suche.transparenz.hamburg.de/dataset/strassenbaumkataster-hamburg)
als Open Data veröffentlicht. Passend zur Zeit der Herbstsparziergänge drängte sich uns die Idee einer Baum App auf,
um unterwegs leicht Kastanienbäume zu finden und deren Flüchte zu sammeln.

Nachdem wir die Daten in das GeoJson Format konvertiert und sie kurz analysiert haben, stellten wir fest, dass
die Daten viel umfangreicher waren als ursprünglich angenommen. Statt nur einer Baumbezeichnung und den GPS-Koordinaten
enthalten die Daten teilweise auch den Ort (Straße), den Stammumfang, den Kronendurchmesser und das Pflanzjahr.

Hier mal ein Beispieldatensatz:

    {
        "type": "Feature",
        "properties": {
        "BAUM_ID": 100061819,
        "BOTANISCHE": "Castanea sativa",
        "BAUMART": "Esskastanie, Marone",
        "PFLANZJAHR": 2005,
        "KRONE_DM": "3 m",
        "STAMMUMFAN": "18 cm",
        "STANDORT": "An der Alster g85"
    },
      "geometry": {
        "type": "MultiPoint",
        "coordinates": [
          [
            10.002291161830076,
            53.55674324547057
          ]
        ]
      }
    }

Diese Informationen können auch für den Laien sehr interessant sein. Beispielsweise lässt sich daraus leicht das
ungefähre Alter des Baums abschätzen und auch benachbarte Bäume gut vergleichen. Auch die mögliche Menge der Kastanienfrüchte
lässt sich mit diesen Informationen besser abschätzen.

Mit diesen Erkenntnissen haben wir dann angefangen erste Mockups und Prototypen zu bauen. Im Moment kann das Projekt
bereits die Kastanien auf einer Karte darstellen und auch Details zu den Kastanien anzeigen.

### Baumkataster in Heilbronn

Da wir aus der Region um Heilbronn kommen, bringt uns das Baumkataster aus Hamburg nicht so viel. Auch in
OpenStreetMap sind leider nicht sehr viele Bäume gepflegt. Daher haben wir das Katasteramt in Heilbronn mit der Bitte
angefragt, uns das lokale Baumkataster zur Verfügung zu stellen. Nach einiger Zeit haben wir dann auch die Zusage
bekommen und sind sehr gespannt auf die Daten. :)

Mit der Umsetzung der Ideen könnte sich daraus auch eine interessante Zusammenarbeit
entwickeln, wie wir im Folgendem darstellen wollen.


### Ideen für lebende Daten

![App Mockup]({{ BASE_PATH }}/assets/kastanien-app.png "App Mockup")

+ Mit einer mobilen App können von den Nutzern sehr schnell Bilder von den Bäumen erstellt werden. Da die Bilder über
 die Lebensdauer des Baums gespeichert bleiben, können damit sehr einfach Veränderungen am Baum festgestellt werden.

+ Die verschiedenen Baumsorten können mit Artikeln in Wikipedia verknüpft werden und so weiterführende Informationen
 den Benutzern liefern

+ Durch den Umfangreichen Datenbestand könnte die App den (Biologie-)Lehrern bei der
 Planung von Exkursionen behilflich sein.

+ Auch Baumpatenschaften wären einfach zu realisieren. Nutzer könnten sich als Paten für einen Baum registrieren und damit
 besondere Verantwortung für den Baum übernehmen.

+ Tipps und Tricks rund um den Baum. Man könnte virtuelle Post-Its an den Baum häften und den anderen Benutzern interessante
 Wander- oder Besichtigungstipps in der Nähe geben.

+ Mit einem entsprechenden Backend könnte auch das Katasteramt kleine Aufgaben an die Benutzer vergeben.
 So wäre es beispielsweise möglich, dass das Katasteramt die Benutzer auffordert einen Baum zu fotografieren oder
 auch direkt den Baumstamm zu messen. Diese Aufgaben könnten direkt bei den Details des Baums angezeigt werden (siehe Screenshot).
 Als Belohnung könnte man sich beispielsweise Kino-Gutscheine oder Ähnliches für die aktivsten Benutzer vorstellen.

Diese Ideen sind nur ein kleiner Anfang. Zuerst wird es wichtig sein bis zum nächsten Herbst eine läuffähige App zu
realisieren, die die Daten anzeigen und mit Bildern umgehen kann.

Unser kleines Team wird sowohl das Backend als auch die Android und iOS App entwickeln. Wir freuen uns jedoch über weitere
Mitstreiter und laden euch ein bei unserem Projekt via GitHub mitzumachen. Die Android App und das Backend in Java findet ihr unter
[https://github.com/opendata-heilbronn/kastanien-app](https://github.com/opendata-heilbronn/kastanien-app).
Die dazu passende iOS App wird unter
[https://github.com/opendata-heilbronn/kastanien-app-ios](https://github.com/opendata-heilbronn/kastanien-app-ios)
entwickelt.

Das [Kastanienbild](https://www.flickr.com/photos/anpena/3074426020/) für das Mockup wurde unter den
Bedinungen von CC BY-NC-SA verwendet.