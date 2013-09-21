---
title: Zulassungsantrag als Verbraucher-Informationsdienst
description: Zulassungsantrag als Verbraucher-Informationsdienst bei der Markttransparenzstelle für Kraftstoffe als OpenSource Projekt
tagline: 
layout: post
category: social
tags: [benzinpreise, opensource]
author: adrian
snapshot: tankstelle.jpg
---

Seit Anfang August bietet das Bundeskartellamt mit der 
[Markttransparenzstelle für Kraftstoffe MTS-K](http://www.bundeskartellamt.de/wDeutsch/MTS-K/MTS-KW3DnavidW26133.php) 
die Möglichkeit an, sich als Anbieter eines Verbraucher-Informationsdienstes zu registrieren. 
Der Verbraucher-Informationsdienst soll die Autofahrer und somit die meisten Menschen über die tagesaktuellen Preise 
an den Tankstellen informieren.

Als OpenData Enthusiasten sehen wir hier natürlich eine gigantische Chance eine interessante Anwendung 
für die Verbraucher zu entwickeln und so die Möglichkeiten von OpenData aufzuzeigen.

Um an die Daten zu kommen muss man jedoch einen recht umfangreichen Fragenkatalog beantworten. 
Damit auch andere Anbieter einen leichteren Einstieg und mögliche Argumente für die Erstellung eines 
Antrags haben, bieten wir hier einen Auszug aus unserem Antrag an.

##### Informationsdienst

Unser geplanter Informationsdienst soll „tankenhier.de“ heißen und als Location-Based-Service 
für alle Internetnutzer zur Verfügung gestellt werden. Der Zugriff soll sowohl über den 
Internet-Browser als auch über native Apps möglich sein. Am Anfang planen wir die Erstellung 
einer Android-App. Smartphone Nutzer werden alle Informationen auch über eine für Mobilgeräte 
optimierte Webseite erreichen können.

Der Informationsdienst stellt die Preisinformationen in Abhängigkeit der aktuellen Position 
des Benutzers dar. Der Benutzer kann gezielt nach Tankstellen suchen, z.B. über Eingabe einer 
Postleitzahl. Tankstellen, die entlang von häufig gefahrenen Strecken liegen, können für 
einen einfachen Zugriff als Favoriten markiert werden. Der Benutzer soll einen Wunschpreis 
für eine Kraftstoffsorte festlegen können und sobald der Preis erreicht oder unterschritten 
wird, darüber informiert werden können. Für einen barrierefreien Zugang können die 
Informationen mit Hilfe von Text-To-Speech dem Benutzer vorgelesen werden, was gerade 
bei mobilen Benutzern sehr hilfreich sein wird.

Grundsätzlich werden dem Benutzer immer die aktuellsten Preisdaten angezeigt. Die Anzeige 
erfolgt dabei in Form von detaillierten Tabellen oder auf einer Landkarte. Dies beinhaltet 
auch alle statischen Daten, wie Adresse und Öffnungszeiten. Darüber hinaus wird es auch 
Zugriff auf historische Daten geben. Mit der Zeit wollen wir auch Algorithmen entwickeln, 
die Prognosen für Preissenkungen und Preiserhöhungen berechnen.

Außer den unmittelbaren Verbrauchern wollen wir die Informationen auch weiteren Entwicklern 
zur Verfügung stellen. Vor allem im Rahmen von OpenData Days und Hackathons soll so ein 
schneller und unbürokratischer Zugang zu den Preisinformationen möglich sein.
Durch die dauerhafte Speicherung der Daten wollen wir auch Hochschulen und Statistikern 
die historischen Preisinformationen uneingeschränkt zur Verfügung stellen.

##### Verfügbarkeit und Aktualisierung des Informationssystems

Unser Informationssystem soll möglichst zeitnah mit der produktiven Verfügbarkeit der 
Preisinformationen seitens von MDM starten. Da wir ein auf Open Source bedachtes Unternehmen 
sind, werden wir den BETA-Betrieb sofort ab der Zulassung zum Abruf der Informationen starten.

Der Zugriff auf das Informationssystem soll über das Internet erfolgen, was für eine weltweite 
Erreichbarkeit sorgt. Es werden alle verfügbaren Tankstellen in dem Informationssystem 
verwaltet und dem Verbraucher zugängig gemacht werden.

Die Preisdaten werden automatisch mit den MDM-Servern abgeglichen und aktualisiert. Die 
Aktualisierung der Daten wird in dem spezifizierten Intervall erfolgen. Es wird dafür 
Sorge getragen, dass die MDM-Server nicht mit unnötigen Anfragen belastet werden.
Der Dienst wird auf Servern gehostet für die wir ein SLA mit 99,9% Verfügbarkeit haben. 
Der Server verfügt über 24GB RAM und eine 100Mbit Anbindung an das Internet. Bei Bedarf 
können kurzfristig weitere Server angemietet werden.

Die Finanzierung der Server ist durch unser Sponsoring Budget für mehrere Jahre gesichert. 
Darüber hinaus wollen wir das Projekt bei verschiedenen Wettbewerben vorstellen und so weiteres Kapital aufbringen.

Grundsätzlich sehen wir die Notwendigkeit, den Informationsdienst für den Verbraucher 
kostenlos, registrierungsfrei und werbefrei anzubieten um einen hohen Datenschutz zu gewährleisten.

Da wir bereits seit über 10 Jahren im Open Source und OpenData Umfeld Projekte 
hosten, sehen wir keine Probleme darin, das Informationssystem dauerhaft zur Verfügung zu stellen.
 
##### Fazit

Wir sind sehr gespannt, ob die MTS-K unseren Antrag akzeptieren wird. Grundsätzlich sehen wir solche 
Hürden als unnötig an. Es bleibt zu hoffen, dass zukünftig der Zugriff auf OpenData nicht auf diese Weise behindert wird.

Sobald wir eine Rückmeldung erhalten werden wir dies natürlich posten.
