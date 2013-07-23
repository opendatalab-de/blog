---
title: "Visualisierung der Regionalstatistikdaten"
description: "Vergleich von Gewerbesteuerzahlen, Hebesätzen, Verkehrsunfallzahlen, Tourismuszahlen, Trinkwasserkosten und mehr am Beispiel vom Landkreis Heilbronn"
tagline: "am Beispiel von Heilbronn"
layout: post
category : hack
tags : [heilbronn, regionalstatistik, genesis]
author: felix
snapshot: heilbronn-regionalstatistik-q.jpg
repository: https://github.com/opendatalab-de/gemeinde-api-mockup
---

Am Beispiel vom Landkreis Heilbronn haben wir zahlreiche Daten [visualisiert](http://opendatalab.de/heilbronn-regionalstatistik), die unter [regionalstatistik.de](https://www.regionalstatistik.de/genesis/online/logon) für alle Gemeinden in Deutschland als offene Datensätze zur Verfügung stehen.

So können unter anderem die Gewerbesteuerzahlen, die Hebesätze, Verkehrsunfallzahlen, Tourismuszahlen und Trinkwasserkosten im Landkreis Heilbronn kompakt verglichen werden.

Die Motivation für diese Visualisierung war die Bürgerbeteiligung [Stadtentwicklung Neckarsulm 2030](http://www.neckarsulm.de/main/unser-neckarsulm/stadtentwicklung-2030.html), bei der ich an zwei Planungswerkstätten teilgenommen habe.
Dort kamen immer wieder Fragen nach einem Vergleich mit anderen Gemeinden im Landkreis auf - zum Beispiel in Bezug auf Erholungsfläche (Parks), Pendlerzahlen und Einwohnerzahlen. Mit Hilfe einer Visualisierung wie dieser könnten zukünftig solche Fragen leichter beantwortet und Zusammenhänge einfacher erfasst werden.

<iframe src="http://opendatalab.de/heilbronn-regionalstatistik" width="100%" height="500"> </iframe>

### Wie wurde die Visualisierung erstellt?

#### Flächen-Polygone

Die Flächen-Polygone der Gemeinden im Landkreis Heilbronn stammen von der [Open Data Seite des Bundesamts für Kartographie und Geodäsie](http://www.geodatenzentrum.de/geodaten/gdz_rahmen.gdz_div?gdz_spr=deu&gdz_akt_zeile=5&gdz_anz_zeile=0&gdz_unt_zeile=0&gdz_user_id=0). Dort haben wir die Geodaten der Verwaltungsgebiete 1:250.000 mit Einwohnerzahlen (Georeferenzierung UTM32, Inhalt Ebenen) heruntergeladen.

Diese Geodaten haben wir mit folgendem Befehl in eine .geojson Datei umgewandelt:

	ogr2ogr -f GeoJSON -s_srs epsg:25832 -t_srs epsg:4326 -simplify 20 gemeinden.geojson vg250_gem.dbf

Anschließend haben wir diese GeoJSON Datei auf den Landkreis Heilbronn anhand des Gemeindeschlüssels [reduziert](https://github.com/opendatalab-de/gemeinde-api-mockup/blob/49fdc74bb39952c268894916d8215d0ede3d2453/gemeinde-api-mockup/src/main/java/de/opendatalab/utils/GemeindeFilter.java). 
Da die Stadt Heilbronn nicht im Shapefile aller Gemeinden enthalten ist, haben wir zusätzlich die Landkreis-Geodaten (vg250_krs) per ogr2ogr umgewandelt und die Stadt Heilbronn in die gefilterte GeoJSON-Datei der Gemeinden eingefügt.

Die resultierende GeoJSON-Datei kann anschließend mit der JavaScript-Bibliothek [Leaflet](http://leafletjs.com/examples/geojson.html) gerendert werden.

#### Regionalstatistikdaten

Wir haben für dieses Beispiel alle Daten auf regionalstatistik.de mit Bezug auf einzelne Gemeinden heruntergeladen.
Gerne hätten wir dabei gleich die Daten für ganz Deutschland heruntergeladen, leider ist das jedoch auf regionalstatistik.de aufgrund fragwürdiger Limitierungen nicht so einfach möglich.
Wollte man diese Visualisierung für ganz Deutschland erstellen, müsste man wohl leider erst einen Scraper für die GENESIS-Portale erstellen.

Für ein einfaches Beispiel haben wir uns daher vorerst auf den Landkreis Heilbronn beschränkt.
Zudem haben wir einzelne Datensätze wie zum Beispiel die Pendlerzahlen vorerst nicht in dieses Beispiel integriert, da diese verhältnismäßig umständlich maschinenlesbar zu erfassen waren.

Mit einem [Java-Converter](https://github.com/opendatalab-de/gemeinde-api-mockup/tree/master/gemeinde-api-mockup) haben wir die heruntergeladenen CSV-Dateien von regionalstatistik.de in die GeoJSON-Datei integriert, so dass die Zuordnung der Daten zum Polygon auf der Karte sehr einfach möglich ist.
Die [entstandene Datei](https://raw.github.com/opendatalab-de/gemeinde-api-mockup/master/viewer/src/data/heilbronn-rs.geojson) könnt ihr euch auf GitHub anschauen.

