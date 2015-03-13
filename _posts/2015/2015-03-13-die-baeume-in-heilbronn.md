---
title: Die Bäume in Heilbronn
description: Eine Auswertung des Baumkatasters der Stadt Heilbronn
tagline:
layout: post
category: opendata
tags: []
author: adrian
snapshot: baum_map.jpg
---

Vor einigen Wochen haben wir vom Grünflächenamt das Baumkataster Heilbronns als Shape-Datei erhalten. Daraus konnten
wir die einzelnen Baumdaten extrahieren und in eine GeoJson-Datei konvertieren. Die Idee ist eine
[Kastanien-App]({% post_url /2014/2014-11-19-kastanien-app-mit-baumkataster %}) daraus
zu machen, die ich bereits in einem früheren Post beschrieben habe.
Bevor wir jedoch mit der App richtig loslegen, wollte ich erstmal schauen, wie es mit den Heilbronner Bäumen aussieht
und habe einige Auswertungen durchgeführt.

Das Baumkataster enthält pro Baum mehrere Informationen, die man für Auswertungen nutzen kann. So findet man außer
dem Baumnamen auch die Art, den Stammumfang, den Kronendurchmesser und den Ort (Stadtteil und Straße) wo sich der
Baum befindet. Natürlich sind auch die genauen GPS Koordinaten enthalten.

Als Erstes kann man sagen, dass das Baumkataster insgesamt 43605 Bäume umfasst. Diese sind in 35817 Laubbäume,
1653 Nadelbäume und 5638  Obstbäume untergliedert. 497 Bäume werden unter der Kategorie "Baumgruppe" geführt.
Hier sind mehrere gleichartige Bäume zusammengefasst.

### Stadtteile

Als nächstes habe ich einen Blick auf die Aufteilung zwischen den Stadtteilen geworfen. Hier zeigt sich, dass in der
Innenstadt doch eine recht große Menge an Bäumen wächst.

<table class="table table-striped table-bordered">
<thead>
<tr><th>Stadtteil</th><th>Anzahl Bäume</th></tr>
</thead>
<tbody>
<tr><td>Biberach</td><td>1925</td></tr>
<tr><td>Böckingen</td><td>6955</td></tr>
<tr><td>Frankenbach</td><td>1230</td></tr>
<tr><td>HN Innenstadt</td><td>7914</td></tr>
<tr><td>HN Äussere Bezirke</td><td>10504</td></tr>
<tr><td>Horkheim</td><td>1516</td></tr>
<tr><td>Kirchhausen</td><td>1122</td></tr>
<tr><td>Klingenberg</td><td>944</td></tr>
<tr><td>Neckargartach</td><td>6082</td></tr>
<tr><td>Sontheim</td><td>5312</td></tr>
</tbody>
</table>

![Aufteilung als Grafik]({{ BASE_PATH }}/assets/baum_stadtteile.png "Aufteilung als Grafik")


### Straßen

Wertet man die Zahlen nach Straße aus, dann ergibt sich ein Bild, das die meisten Heilbronner nicht glauben werden.
Die Wollhausstraße mit über 1200 Bäumen im Baumkataster sieht nicht unbedigt als die grüne Meile Heilbronns aus.
Diese Zahlen kommen dadurch zustande, dass alle Bäumen auf dem Hauptfriedhof dieser Straße zugeordnet sind.

Entlang der Neckartalstraße, die als eine der längsten Straßen in Heilbronn gilt, wachsen über 1000 Bäume.
Auch der Wertwiesenpark ist mit knapp über 900 Bäumen gut bestückt. Die Staußenbergstraße punktet hauptsächlich
mit dem Südfriedhof in Sontheim.

<table class="table table-striped table-bordered">
<thead>
<tr><th>Straße</th><th>Anzahl Bäume</th></tr>
</thead>
<tbody>
<tr><td>Wollhausstraße</td><td>1264</td></tr>
<tr><td>Neckartalstraße</td><td>1059</td></tr>
<tr><td>Wertwiesen</td><td>919</td></tr>
<tr><td>Staufenbergstraße</td><td>832</td></tr>
<tr><td>Römerstraße</td><td>675</td></tr>
<tr><td>Neckar</td><td>653</td></tr>
<tr><td>Badstraße</td><td>612</td></tr>
<tr><td>Neipperger Straße</td><td>576</td></tr>
<tr><td>Neckar Schiffahrtskanal</td><td>563</td></tr>
<tr><td>Am Gesundbrunnen</td><td>548</td></tr>
</tbody>
</table>

### Baumarten

Die Sortenaufteilung sieht wie folgt aus. In den TOP 10 taucht leider keine Kastanie auf. Erst auf dem 11. Platz
findet sich in Heilbronn die Gewöhnliche [Roßkastanie](http://de.wikipedia.org/wiki/Rosskastanien) mit genau 800 Bäumen.

Hier sind die Top 10 Arten jeweils mit einem Link zu WikiPedia.

<table class="table table-striped table-bordered">
<thead>
<tr><th>Baumart</th><th>Anzahl Bäume</th></tr>
</thead>
<tbody>
<tr><td><a href="http://de.wikipedia.org/wiki/Ahornbl%C3%A4ttrige_Platane">Ahornblättrige Platane</a></td><td>4497</td></tr>
<tr><td><a href="http://de.wikipedia.org/wiki/Spitzahorn">Spitz-Ahorn</a></td><td>2874</td></tr>
<tr><td><a href="http://de.wikipedia.org/wiki/Hainbuche">Gemeine Hainbuche</a></td><td>2261</td></tr>
<tr><td><a href="http://de.wikipedia.org/wiki/Feldahorn">Feld-Ahorn</a></td><td>1841</td></tr>
<tr><td><a href="http://de.wikipedia.org/wiki/Stieleiche">Stiel-Eiche</a></td><td>1723</td></tr>
<tr><td><a href="http://de.wikipedia.org/wiki/Berg-Ahorn">Berg-Ahorn</a></td><td>1657</td></tr>
<tr><td><a href="http://de.wikipedia.org/wiki/%C3%84pfel">Apfelbaumart</a></td><td>1619</td></tr>
<tr><td><a href="http://de.wikipedia.org/wiki/Gemeine_Esche">Gemeine Esche</a></td><td>1462</td></tr>
<tr><td><a href="http://de.wikipedia.org/wiki/Krim-Linde">Krim-Linde</a></td><td>1326</td></tr>
<tr><td><a href="http://de.wikipedia.org/wiki/H%C3%A4nge-Birke">Gemeine Weiß-Birke</a></td><td>871</td></tr>
</tbody>
</table>

Ein Blick auf das Ende der Liste verrät, dass Heilbronn ca. 100 Baumarten hat, die jeweils nur 1 Mal
in der Stadt vorkommen.
Vielleicht würde es sich lohnen, all diese Bäume zu besuchen und zu fotografieren? Das ist eine Idee für die Kastanien-App.

### Stammumfang

Eine Auswertung nach Stammumfang zeigt, dass die meisten Bäume in der Stadt einem Stammumfang bis zu 2 Metern haben.
Ab 5 Meter wird die Luft schnell dünn und ab 10 Meter findet man nur noch Einzelstücke. Leider enthält das
Baumkataster keine Informationen über das Alter der Bäume.

![Aufteilung als Grafik]({{ BASE_PATH }}/assets/baum_stammumfang.png "Aufteilung als Grafik")


### Top 3 Größe

Zu guter letzt habe ich noch einen Blick auf die größten Bäume in Heilbronn geworfen.
Der Baum mit dem größtem Stammumfang ist die [Flügelnuß](http://de.wikipedia.org/wiki/Kaukasische_Fl%C3%BCgelnuss)
am Süd-Eingang vom Frankenstadion. [Gleich auf der rechten Seite](https://www.google.de/maps/place/49%C2%B008'02.2%22N+9%C2%B012'17.6%22E/@49.1338697,9.204929,161m/data=!3m1!1e3!4m2!3m1!1s0x0:0x0) befindet sich der riesen Baum mit
einem Kronendurchmesser von 25m.

Die Nummer 2, was den Stammumfang anbetrifft ist ebenfalls eine Flügelnuß mit einem Umfang von 13,46m. Sie ist
wahrscheinlich allen Heilbronnern bekannt, denn sie befindet sich
[gleich neben der Harmonie](https://www.google.de/maps/place/49%C2%B008'30.6%22N+9%C2%B013'23.1%22E/@49.1418114,9.2228586,161m/data=!3m1!1e3!4m2!3m1!1s0x0:0x0),
an der Kreuzung zwischen Allee und Moltkestraße. Dieser Baum hat einen Kronendurchmesser von 24m.


Ein weiteres Highlight der riesen Bäume ist die [Winter-Linde](http://de.wikipedia.org/wiki/Winterlinde), die sich im [Stadtteil Kirchhausen](https://www.google.de/maps/place/49%C2%B010'18.7%22N+9%C2%B007'46.9%22E/@49.1685988,9.1297534,70a,20y,83.36t/data=!3m1!1e3!4m2!3m1!1s0x0:0x0) befindet. Sie
 ist mit 29m Kronendurchmesser die Nummer 1 in dieser Kategorie. Diese Krone wird von "nur" 7,6m Stammumfang getragen.


### Fazit

Das Baumkataster ist eine interessante Datenbank über die Umwelt, die uns umgibt. Ich möchte mir diesen Sommer auf
jeden Fall all die großen Bäume aus der Nähe anschauen. Auch einige Einzelstücke will ich mit dem Fahrrad anfahren und
fotografieren. Diese Bilder sollen in die
[Kastanien-App]({% post_url /2014/2014-11-19-kastanien-app-mit-baumkataster %}) einfliesen, die bereits in der Umsetzung ist.
Mit dieser App werden alle interessierten Bürger leicht Bäume in Heilbronn finden können.

Alle Daten Stand: 27.11.2014, Quelle: Stadt Heilbronn, Grünflächenamt, 12/2014