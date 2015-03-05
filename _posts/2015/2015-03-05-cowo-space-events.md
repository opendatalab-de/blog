---
title: Out of Space - Neue Event-Ideen aus dem Coworking Space Heilbronn
description: Regelmäßige Events im Coworkingspace Heilbronn
tagline:
layout: post
category: coworking
tags: [event]
author: adrian
snapshot: community.jpg
---

> “Wie wird man ein guter Musiker? Es hilft, die Theorie zu kennen, die Mechanik des Instruments zu verstehen und Talent zu haben. Der größte Faktor aber ist Übung, die Theorie wieder und immer wieder anzuwenden und durch Feedback jedes Mal etwas besser zu werden.”
*codekata.com*

Wir glauben, dass das auch auf Software-Entwickler zutrifft. Daher möchten wir im [Coworking Space Heilbronn](http://coworking-heilbronn.org/) den Donnerstag Abend als einen festen Zeitpunkt zum gemeinsamen Austausch, Lernen und Umsetzen von Projekten etablieren.

Folgende Events stehen bereits fest:

* 12.03.2015: Git + GitHub Workshop für Einsteiger
* 19.03.2015: Code for Heilbronn mit Special Guest [Drew](http://www.codeforamerica.org/people/drew-wilson/) von [Code for America](http://www.codeforamerica.org/)
* 22.04.2015: AngularJS Workshop für Einsteiger

Einen Abend im Monat treffen wir uns speziell für den Zweck, im Rahmen von [Code for Heilbronn](http://codefor.de/heilbronn) Open Data Projekte umzusetzen.

An den übrigen Donnerstagen wollen wir das Format “4 hour venture” ausprobieren, bei dem kurze Projekte zum Testen einer Idee oder zum Einarbeiten in eine neue Technologie umgesetzt werden - ganz nach dem Prinzip Learning by doing.

Für dieses Format haben wir uns bereits 3 machbare Projekte mit viel Lernpotenzial überlegt:

### Where is my Bus - Mobile App um Busse Live zu tracken
Echtzeitdaten im ÖPNV sind ein spannendes Thema: Wo bleibt der Bus? Wir wollen eine Mobile-App auf Android Basis (bei Interesse auch iPhone) entwickeln, die es erlaubt einen Bus während der Fahrt zu tracken und seine Position zu übermitteln. Die Idee ist, dass wir Fahrgäste und Busfahrer finden, die diese App nutzen wollen um anderen Gästen live Daten über die Position eines Busses zu übermitteln. Alle Daten werden anonymisiert erfasst und auch während der Fahrt wird es keine Möglichkeit geben, Bewegungsprofile zu erstellen. Nach jeder Haltestelle werden neue zufällige IDs für die Nutzer erstellt.

Vorgehen:
Wir vervollständigen die Busslinien in Heilbronn in OpenStreetMap und extrahieren sie in eine separate Datenbank. Danach erstellen wir eine einfache App, die die GPS Position des Nutzers erfasst und prüft, ob die Bewegung entlang einer Buslinie verläuft. Der Nutzer wird die Möglichkeit haben die Buslinie genau festzulegen, falls die Strecke von mehreren Bussen frequentiert wird.
Die aktuelle Position des Nutzers wird nur solange übertragen, wie er sich entlang der Buslinie bewegt. Sobald eine Abweichung festgestellt wird, beendet sich die App automatisch.
Gleichzeitig werden wir eine Kartenansicht in die App integrieren, in der man alle Busse als bewegliche Icons sehen kann.
Als ein schönes Add-On können wir auch eine Webseite erstellen, auf der die Busse ebenfalls verfolgt werden können.

Skills to learn:
Android, Java, Geo-Daten, Livestreaming, (optional iOS, und HTML mit AngularJS und Leaflet)


### AngularJS Plugin für Adressenerfassung

Projektbeschreibung:
Es gibt kaum ein Formular bei dem keine Adressdaten erfasst werden. Die Eingabe der Straße, PLZ und des Ortes ist jedoch mühsam und könnte dank bereits verfügbarer Datendanken stark erleichtert werden. So gibt es zum Beispiel die Open GeoDB, die alle PLZ und die dazugehörigen Orte enthält. Ähnlich sieht es bei OpenStreetMap und den Straßennamen aus. Eine Eingabemaske könnte also zuerst die PLZ erfragen und den passenden Ort automatisch ermitteln. Danach bei der Eingabe automatisch die Straßen vorschlagen, die es in diesem Ort gibt.

Vorgehen:
Wir wollen die PLZ und Orte aus Open GeoDB und die Straßen aus OpenStreetMap zu einer gemeinsamen Datenbank zusammenführen. Danach entwickeln wir ein Backendsystem welches via REST-API Suchanfragen zu einer PLZ, Ort oder Straße ausführen kann. Im letzten Schritt erstellen wir ein AngularJS Plugin, welches ganz einfach in vorhandene AngularJS Projekte eingebunden werden kann und mit Formularen verknüpft werden kann.

Skills to learn:
JavaScript, Java, Geo-Daten, OpenStreetMap, HTML, CSS, Open Data


### Point Of Sale für den Coworking Space

Projektbeschreibung:
Im Coworking Space gibt es die Möglichkeit kleine Snacks und Getränke zu kaufen. Diese wollen wir mit einem POS System erfassen. Wir haben bereits in der Vergangenheit ein POS für einen Blumenladen erstellt. Dieses POS wurde mit der Zeit ersetzt, doch wir haben immer noch die Hardware (Touchscreen, POS Drucker, Kassenladen, PC) und könnten daraus eine Kasse bauen.

Vorgehen:
Aus den bereits vorhandenen Hardwareteilen basteln wir einen WLAN-tauglichen POS Drucker. Ein Backend in der Cloud wird für die Speicherung der Coworkingkunden und der Belege erstellt. Ein AngularJS Frontend wird für die Erfassung der Kunden und die Durchführung der Transaktionen implementiert. Diese Lösung soll es möglich machen, von allen Geräten aus im Coworking Space (PC, Notebook, Handy, Tablet) die Kasse im Browser zu öffnen und einen Beleg zu erfassen und auszudrucken.

Skills to learn:
Hardware-Hacking, Java, MongoDB, Druckersteuerung, AngularJS Frontend

- - -

Natürlich kannst du auch deine eigenen Ideen vorschlagen und bei einem der nächsten Treffen vorstellen. Welche Themen und Events interessieren dich am meisten?
Schick uns deine Ideen oder Vorschläge via Twitter oder Besuche unsere Facebook Seite.

Wir freuen uns auf deinen Besuch.
