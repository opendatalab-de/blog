---
title: Digitaler Abfallkalender für den Landkreis Heilbronn 
description: Mit Mob-Programming zum digitalen Abfallkalender in Heilbronn
tagline:
layout: post
category: opendata
tags: [mobprogramming, opendata, event]
author: adrian
repository: https://github.com/opendata-heilbronn/garbage-collection
snapshot: abfallkalender.png
---

Vor zwei Jahren haben wir beim ersten [Open Data Day 2014 in Heilbronn]({% post_url /2014/2014-01-15-opendataday-heilbronn %} ) 
alle Müllabfuhrtermine aus den über 50 Abfallkalender
im Landkreis abgetippt und in [maschinenlesbare Formate](http://recycling.gonam.de/kalender/) überführt. Dadurch war es dann möglich die Abfuhrtermine ganz einfach
in seinen digitalen Kalender auf dem PC oder Smartphone zu importieren um rechtzeitig an die Mülltonne erinnert zu werden.
Das Landratsamt war leider nicht bereit uns die Daten in tabellarischer Form zu geben, so dass nur die händische Erfassung 
der Termine aus den PDF-Dateien in Frage kam.

Für 2015 haben wir den Aufwand gescheut, denn beim Erfassen der Daten im Jahr 2014 hat ein Team aus drei Personen den ganzen Tag 
gebraucht um die Termine abzutippen. Doch wir lieben Daten und noch viel mehr lieben wir das Programmieren. Der nächste 
digitale Terminkalender sollte unbedingt voll automatisch konvertiert werden.

Als wir uns gestern Gedanken über den Coding-Abend im [Coworking Space Heilbronn](http://coworking-heilbronn.org) gemacht haben, kam uns die Idee für eine
ganz einfache Programmieraufgabe, die wir gut als [Mob-Programming](https://en.wikipedia.org/wiki/Mob_programming) umsetzen können: Wir machen aus einer PDF-Datei
eine Pixel-Grafik und suchen dann in dem Raster der Monate und Tage nach entsprechenden Farben (grau für Mülltonne, blau
für Papiertonne usw.). Aus der Position der Farbe in der Grafik können wir ganz leicht den Tag des Monats errechnen, da alle Tage
dieselbe Zeilenhöhe haben. So haben wir z.B. herausgefunden, dass der Tag eine Höhe von 22 Pixel hat und der Monat eine
Breite von 145 Pixel (die Angaben hängen davon ab, wie die PDF skaliert wird).

![Beispiel]({{ BASE_PATH }}/assets/abfallkalender-beispiel.png "Beispiel")

Danach konnten wir mit einfachen Schleifen eine Zeile nach der anderen abscannen und die gewünschten Farben identifizieren.
Dasselbe haben wir dann für die zweite Seite gemacht (pro Seite gibt es sechs Monate) und dann natürlich auch für die über 50 Abfallkalender aus 
dem Landkreis.
Am Ende kommen strukturierte Daten für alle Müllabfuhrbezirke, die man in beliebige andere Datenformate wie z.B. ical/ics konvertieren kann.

Hier ein Beispiel für einen Datensatz in Untergruppenbach: 

{% highlight json  %}
{
    "Untergruppenbach": {
        "Biomüll": ["8.1.2015", "22.1.2015", "5.2.2015", "19.2.2015", "5.3.2015", "19.3.2015", "2.4.2015", "17.4.2015", "30.4.2015", "15.5.2015", "29.5.2015", "11.6.2015", "18.6.2015", "25.6.2015", "2.7.2015", "9.7.2015", "16.7.2015", "23.7.2015", "30.7.2015", "6.8.2015", "13.8.2015", "20.8.2015", "3.9.2015", "17.9.2015", "1.10.2015", "15.10.2015", "29.10.2015", "12.11.2015", "26.11.2015", "10.12.2015", "28.12.2015"],
        "Papier": ["21.1.2015", "4.3.2015", "15.4.2015", "28.5.2015", "8.7.2015", "19.8.2015", "30.9.2015", "11.11.2015", "23.12.2015"],
        "Restmüll": ["15.1.2015", "29.1.2015", "12.2.2015", "26.2.2015", "12.3.2015", "26.3.2015", "11.4.2015", "23.4.2015", "7.5.2015", "21.5.2015", "5.6.2015", "18.6.2015", "2.7.2015", "16.7.2015", "30.7.2015", "13.8.2015", "27.8.2015", "10.9.2015", "24.9.2015", "8.10.2015", "22.10.2015", "5.11.2015", "19.11.2015", "3.12.2015", "17.12.2015"],
        "Schadstoffsammlung": ["28.2.2015", "7.3.2015", "16.5.2015", "23.5.2015", "20.6.2015", "11.7.2015", "18.7.2015", "19.9.2015", "31.10.2015", "3.12.2015"]
    }
}
{% endhighlight %}

Die Programmieraufgabe hat ca. 2h gedauert und der Scanprozess läuft in wenigen Sekunden durch. Immer wieder abwechselnd am PC 
haben [Anna, Ketoma, Felix und ich](http://codefor.de/heilbronn/#members) viel Spass und konnten auch einiges dabei lernen.
Wir planen in Zukunft weitere [Open Data Mob-Programming](http://www.meetup.com/de/OK-Lab-Heilbronn) Sessions, 
schaut einfach mal bei uns vorbei.
