---
title: "Visualisierung der Regionalstatistikdaten"
description: "Vergleich von Gewerbesteuerzahlen, Hebesätzen, Verkehrsunfallzahlen, Tourismuszahlen, Trinkwasserkosten und mehr am Beispiel vom Landkreis Heilbronn"
tagline: "am Beispiel von Heilbronn"
layout: post
category : hack
tags : [heilbronn, regionalstatistik, genesis]
author: felix
snapshot: heilbronn-regionalstatistik.png
repository: https://github.com/opendatalab-de/gemeinde-api-mockup
---

Am Beispiel vom Landkreis Heilbronn haben wir zahlreiche Daten [visualisiert](http://opendatalab.de/heilbronn-regionalstatistik), die unter [regionalstatistik.de](https://www.regionalstatistik.de/genesis/online/logon) für alle Gemeinden in Deutschland als offene Datensätze zur Verfügung stehen.

So können unter anderem die Gewerbesteuerzahlen, die Hebesätze, Verkehrsunfallzahlen, Tourismuszahlen und Trinkwasserkosten im Landkreis Heilbronn kompakt verglichen werden.

<iframe src="http://opendatalab.de/heilbronn-regionalstatistik" width="100%" height="500"> </iframe>

Wir haben für dieses Beispiel alle Daten auf regionalstatistik.de mit Bezug auf einzelne Gemeinden heruntergeladen.
Gerne hätten wir dabei gleich die Daten für ganz Deutschland heruntergeladen, leider ist das jedoch auf regionalstatistik.de aufgrund fragwürdiger Limitierungen nicht so einfach möglich.
Daher haben wir uns für ein einfaches Beispiel vorerst auf den Landkreis Heilbronn beschränkt.

Zudem haben wir einzelne Datensätze wie zum Beispiel die Pendlerzahlen nicht in dieses Beispiel integriert, da diese verhältnismäßig umständlich maschinenlesbar zu erfassen waren.

Die Flächen-Polygone der Gemeinden im Landkreis Heilbronn stammen von der [Open Data Seite des Bundesamts für Kartographie und Geodäsie](http://www.geodatenzentrum.de/geodaten/gdz_rahmen.gdz_div?gdz_spr=deu&gdz_akt_zeile=5&gdz_anz_zeile=0&gdz_unt_zeile=0&gdz_user_id=0). Dort haben wir die Geodaten der Verwaltungsgebiete 1:250.000 mit Einwohnerzahlen (Georeferenzierung UTM32, Inhalt Ebenen) heruntergeladen.

Diese Geodaten haben wir mit folgendem Befehl in eine .geojson Datei umgewandelt:

	ogr2ogr -f GeoJSON -s_srs epsg:25832 -t_srs epsg:4326 -simplify 20 gemeinden.geojson vg250_gem.dbf

Anschließend haben wir diese GeoJSON Datei auf den Landkreis Heilbronn anhand der Regionalschlüsselnummer reduziert.

Da die Stadt Heilbronn nicht im Shapefile aller Gemeinden enthalten ist, haben wir zusätzlich die Landkreis-Geodaten (vg250_krs) per ogr2ogr umgewandelt und die Stadt Heilbronn manuell in die GeoJSON-Datei der Gemeinden eingefügt. 

Die Daten der heruntergeladenen CSV-Dateien von regionalstatistik.de haben wir in die GeoJSON-Datei integriert, so dass die Zuordnung der Daten zum Polygon auf der Karte sehr einfach möglich ist. Die entstandene Datei könnt ihr euch auf [GitHub](https://github.com/opendatalab-de/gemeinde-api-mockup/tree/master/viewer/src/data) anschauen.
