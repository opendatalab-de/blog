---
title: Java Tools für das ZUGFeRD Datenmodell
description: Sammlung von Java Tools zum Verarbeiten von Rechnungen im ZUGFerd Format
tagline: 
layout: post
category: hack
tags: [invoice, opensource]
author: adrian
repository: https://github.com/opendatalab-de/zugferd
snapshot: zugferd-invoice.jpg
---

Die elektronische Rechnung ist mit dem ZUGFeRD Format endlich in greifbare Nähe gerückt.
Das Format, welches von der Arbeitsgemeinschaft für wirtschaftliche Verwaltung e.V. (AWV) 
unter [www.ferd-net.de](http://www.ferd-net.de) veröffentlicht wurde, erlaubt es elektronische 
Rechnungen als XML-Datei im Anhang einer PDF Datei zu versenden.
Die XML Datei wird dabei an eine [PDF/A-3](http://de.wikipedia.org/wiki/PDF/A) angehängt und kann 
von [EDI Systemen](http://de.wikipedia.org/wiki/Elektronischer_Datenaustausch) 
verarbeitet und ausgewertet werden. Das PDF/A Format ist im Prinzip ein PDF Format, welches für 
Archivierungszwecke mit bestimmten Restriktionen belegt wurde. Damit soll sichergestellt werden, dass 
das Dokument auch in Zukunft dargestellt werden kann.

Der AWV stellt auf seiner FeRD-Net Seite ein [Infopaket](http://www.ferd-net.de/front_content.php?idcat=255&lang=3) 
mit der Spezifikation und einigen Beispielrechnungen im PDF- und XML-Format zur Verfügung. 
Dies sollte Grund genug sein um sich das Thema etwas anzuschauen und zu prüfen, 
ob die Dokumente mit Open-Source Mitteln verarbeitet werden können.

##### Java Tools

Hierzu habe ich ein Projekt mit den von mir hier beschriebenen Tools erstellt und in unserem Github Account 
online gestellt. In diesem Projekt habe ich als Erstes mit Hilfe von dem xjc Schema Compiler 
aus dem JAXB (Java Architecture for XML Binding) Paket Objekt-Dateien erstellt, die dazu verwendet 
werden können, einen Objektbaum aus der XML Datei einzulesen. 
Nachdem der Compile die Objekte erstellt hat,
kann die Beispiel-Rechnung einfach mit folgenden Zeilen eingelesen werden:

	JAXBContext jc = JAXBContext.newInstance(ObjectFactory.class);
	Unmarshaller u = jc.createUnmarshaller();
	JAXBElement<CBFBUYType> element = (JAXBElement<CBFBUYType>)u.unmarshal(in);
	CBFBUYType invoice = (CBFBUYType)element.getValue();

Als Nächstes habe ich mir die PDF Datei anschaut und sie mit Hilfe der iText Library geöffnet.
Damit konnte ich die Anhänge durchiterieren und die passende XML-Datei finden. Da der Code hierfür
etwas komplexter ist möchte ich hier auf die [PdfInvoiceReader](https://github.com/opendatalab-de/zugferd/blob/master/src/main/java/de/grundid/zugferd/PdfInvoiceReader.java)
Klasse verweisen, die sich in der Tools-Sammlung befindet und einem die Arbeit weitestgehend abnimmt.

Zwar sagt die Spezifikation aus, dass im Moment nur eine Rechnung pro PDF Dokument angehängt
werden darf, dies hindert jedoch niemanden daran auch andere Inhalte mit der PDF-Datei zu verschicken.
Deshalb ist es notwendig, den Namen der Datei im Anhang mit dem Eintrag in den 
Metadaten der PDF-Datei abzugleichen.

Um die Metadaten zu lesen gibt es von Adobe die 
[Extensible Metadata Platform (XMP) Library](http://www.adobe.com/devnet/xmp.html). Mit dieser Library
können die Metadaten in einer XML-Datei wieder in ein Objektbaum geparst und ausgewertet werden. Für
das ZUGFeRD Modell wurde eine entsprechende Schemaerweiterung spezifiziert. 
In dieser Schemaerweiterung sind vier Zusatzinformationen vorhanden und zwar:

- der Name des Rechnungsdokuments im Anhang der PDF Datei
- die Version des Spezifikation
- der Typ des Dokuments (im Moment nur INVOICE)
- Ausprägung der XMLRechnungsdaten (BASIC, COMFORT, EXTENDED)

Hierzu habe ich auch eine entsprechende Klasse [ZfMetaDataReader](https://github.com/opendatalab-de/zugferd/blob/master/src/main/java/de/grundid/zugferd/xmp/ZfMetaDataReader.java) 
vorbereitet, die in der Lage ist diese Daten aus den Metadaten zu extrahieren.
Mit dem Namen des Rechnungsdokuments kann man jetzt ganz sicher auf den entsprechenden Anhang zugreifen
und die Rechnungsdaten verarbeiten.

##### Fazit

Die aktuelle Version des ZUGFeRD Formats lässt sich sehr leicht mit Java Werkzeugen auslesen. 
In weiteren Tests wird man versuchen müssen auch entsprechende PDF Dokumente zu erzeugen. 
Dazu wäre es jedoch sinnvoll eine Art Referenzimplementierung seitens des AWV zu haben, um die 
erstellen Dokumenten verifizieren zu können.

Mittelfristig stellt sich die Frage, in wie fern die PDF Datei überhaupt notwendig ist. 
Sie wird vermutlich die Benutzer weiterhin dazu animieren das Dokument auszudrucken und abzuheften.
Daher plane ich einen weiteren Test indem die reine XML-Rechnungsdatei mit Hilfe 
von [XSLT](http://de.wikipedia.org/wiki/XSLT) in ein menschenlesbares Dokument umgewandelt wird.
Dies wird es erlauben, die Rechnungen nur als XML-Datei zu transportieren und nur bei 
Bedarf mit Hilfe von XSLT zu visualisieren.
