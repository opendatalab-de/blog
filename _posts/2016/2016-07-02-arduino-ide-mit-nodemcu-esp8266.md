---
title: Einrichtung der Arduino IDE mit dem NodeMCU/ESP8266 Board 
description: Tipps und Tricks für die Einrichtung und die Konfiguration der Arduino IDE mit dem NodeMCU/ESP8266 Board
tagline:
layout: post
category: codeforbuga
tags: [arduino]
author: adrian
snapshot: nodemcu_small.jpg
---

Bei unseren [Workshops und Coding Abenden](https://meetup.com/codeforhn/) mit dem NodeMCU Board und der Arduino IDE haben wir in letzter Zeit viele Erfahrungen gesammelt,
die ich hier im Blogpost zusammenfassen möchte.

Uns sind bisher zwei verschiedene NodeMCU Boards begegnet, die auch deutlich unterschiedliche Größen haben. 
Das größere Board wird dabei mit einem CH340 Chip für die USB Schnitstelle ausgeliefert. Das kleinere Board kommt
mit einem Silicon Labs CP210x Chip. Je nachdem, welches Board man hat muss man natürlich den 
entsprechenden Treiber installieren.
  
![NodeMcu]({{ BASE_PATH }}/assets/hardware/nodemcu_compare1.jpg )
  
Den Treiber für den CP210x findet man ganz leicht auf der [Seite von Silicon Labs](https://www.silabs.com/products/mcu/Pages/USBtoUARTBridgeVCPDrivers.aspx).
Da die Seite des Herstellers vom CH340 Chip leider auf chinesisch ist, 
haben bereits [andere entsprechende Installationsanweisungen](http://kig.re/2014/12/31/how-to-use-arduino-nano-mini-pro-with-CH340G-on-mac-osx-yosemite.html) 
geschrieben, auf die hier nur verlinkt wird. 
Installiert man den richtigen Treiber, dann erscheint nach dem Anschließen des Boards per USB Kabel unter Windows 
im Geräte-Manager eine neue COM-Schnitstelle. Unter Mac OS und unter Linux ist dann ein entsprechendes Device ist der
Liste zu finden.

![NodeMcu]({{ BASE_PATH }}/assets/hardware/nodemcu_compare2.jpg )

Ist dieser Schritt bewältigt so kann man jetzt problemslos die [Arudino IDE downloaden](https://www.arduino.cc/en/Main/Software).
Die Arudino IDE ist leider nicht von Haus aus für das NodeMCU konfiguriert, so dass man einen zusätzlichen
Boardmanager installieren muss. Dies geschieht in drei Schritten. Zuerst muss man in den Einstellungen 
eine zusätzliche Boardverwalter-URL angeben. Für den NodeMCU lautet sie wie folgt (bitte in die Zwischenablage kopieren):

[http://arduino.esp8266.com/stable/package_esp8266com_index.json](http://arduino.esp8266.com/stable/package_esp8266com_index.json)

![NodeMcu]({{ BASE_PATH }}/assets/hardware/arduino_screenshot_config.png )

Danach muss man auch das entsprechende Board downloaden. Hierzu geht man auf "Werkzeuge" > "Board ..." und wählt in der
Liste die oberste Position "Boardverwalter..." aus. Dort kann man in das Suchfeld "nodemcu" eingeben und es sollte dann
ein "esp8266 by ESP8266 Community" Board auftauchen. Hier genügt ein Klick auf "Installieren" 
und die Boardinformationen werden downgeloadet. 

![NodeMcu]({{ BASE_PATH }}/assets/hardware/arduino_screenshot_boardverwalter.png )

Als letzter Schritt muss nur noch das entsprechende Board in der Auswahlliste ausgewählt werden und der entsprechende 
Port eingestellt werden. Beides geschieht wieder in dem Menü "Werkzeuge", dort dann den Punkt "Board ..." auswählen
und dort den Eintrag "NodeMCU 1.0 ..." auswählen. Danach nochmals im Menü "Werkzeuge" unter dem Punkt "Port ..." den 
richtigen COM-Port auswählen.

![NodeMcu]({{ BASE_PATH }}/assets/hardware/arduino_screenshot_werkzeuge.png )

Danach sollte dem ersten Sketch nichts mehr im Wege stehen, so dass man unter "Datei" > "Beispiele" schnell ein
Beispiel-Sketch z.B. für das Blinken einer LED öffnen kann und mit dem Klick auf den 
"Hochladen" Button (Pfeil nach rechts) das Programm auf den NodeMCU hochspielen kann. Bei dem kleinen Board ist bereits eine 
LED auf dem digital Pin D0 "on-board" gelötet, so das man diese für das Blinken verwenden kann. Bei dem größerem Board
muss man selber eine kleine LED-Schaltung zusammen stecken.
 
Hier noch zwei Tipps für die Konfiguration und Verwendung der Arduino IDE

**1. Schriftgröße erhöhen** 

Damit bei 2er oder 3er Teams alle gut am Monitor den Programcode mitverfolgen können lohnt es sich die
 Schriftgröße in den Einstellungen zu erhöhen. Man sollte hier einfach etwas rumexperimentieren. Für mich ist
 die Schriftgröße 16 optimal. Damit kann man den Programmcode noch aus einer Entfernung von 1m einwandfrei lesen.
    
**2. Maximale Uploadgeschwindigkeit**

Bei der Arbeit mit dem NodeMCU ist uns aufgefallen, dass bei dem Board der Programmcode deutlich langsamer im
Vergleich z.B. zu einem Arduino Nano hochgeladen wird. Ob der kompilierte Code dabei größer ist oder nicht, 
weiß ich nicht, aber nachdem wir etwas mit der Geschwindigkeit der seriellen Schnittstelle experimentiert haben
ging es mit dem Upload deutlich schneller vonstatten. Es lohnt sich also auch hier das Maximum
auszuloten statt jedes Mal einen Upload von 20-30 Sekunden über sich ergehen zu lassen.
      
**3. Vorkonfigurierte Konstanten für die Pins verwenden**

Ist der Boardmanager installiert, so sind die Bezeichnungen der digitalen und analogen Pins des NodeMCU als Konstanten verfügbar.
D.h. man kann direkt im Code D0 für den ersten digitalen Pin und A0 für den analogen Pin verwenden. Da die Pin-Bezeichungen
in den vielen Beispiel-Codes den direkten Wert wie 13 oder 10 verwenden und bei dem NodeMCU die Belegung anders ist, lohnt es 
sich kurz den Programmcode anzupassen und die Konstanten zu verwenden.
      

Hier ein Beispiel der Arduino IDE in Schriftgröße 16 und mit Verwendung von D0 als Konstante
 
![NodeMcu]({{ BASE_PATH }}/assets/hardware/arduino_screenshot.png )

Um das ganze Potenizal des NodeMCUs zu nutzen sollte man das Board mit einem WiFi-Netzwerk verbinden. Wie das geht erkläre ich
in einem separaten Blogpost.
