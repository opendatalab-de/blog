---
title: Creating QR-Codes with dynamic WiFi configuration for Point-Of-Sale (POS) systems
description: How to create QR-Codes for WiFi configuration, print them on an Epson POS printer and update the WiFi router settings.
tagline: 
layout: post
category: hack
tags: [english, pos, qrcode, opensource]
author: adrianenglish
repository: https://github.com/grundid/fritzbox-java-api
snapshot: qrcode1.jpg
---

The project I just finished was on my roadmap for months. In the end it took me about two 
days to stitch everything together.

The idea is to have a system that would regularly change the WiFi password
of an access point in a public cafe and allow the service staff to easily print out 
the new password on the POS printer and hand it out to the customer.
For the customer it should be as easy as possible to connect to the WiFi network. For 
this I'm using a QR-Code format that can be recognized by most QR-Code scanners. The QR scanner 
then sets up the network setting on the customers' phone and he or she is ready to go.

Since the [café in question](http://annablume-cafe.de) is run by my mom and I'm the system administrator of the POS 
system I have full control over all the software and hardware components. Our current setup involves a simple 
Windows PC with a touchscreen TFT and an Epson TM-T88IV POS printer connected over USB. As for software I'm
using [OpenbravoPOS](http://sourceforge.net/projects/openbravopos/), a Spanish open-source POS software 
written in Java that I [adopted and enhanced](https://code.google.com/p/openpos/) over the 
last couple of years with new reporting functions and a time reporting system for the employees.
The connection between the USB printer and Java is possible due to a virtual Com-port driver from Epson.

#### WiFi configuration

Our WiFi network is handled by a FirtzBox. To be able to configure the guest WiFi settings on the FritzBox one 
has to login into the router via a Web interface and set the appropriate settings in a web form. I haven't found any
FritzBox Java API for the box but was lucky enough to find a [python module](https://github.com/valpo/fritzbox/blob/master/fritzbox/fritzlogin.py)
that can login into the box and acquire the session ID which is nessecary for all requests. 
I've adapted the python code 
to a [Java version](https://github.com/grundid/fritzbox-java-api/blob/master/src/main/java/de/grundid/fritz/FritzTemplate.java)
 and added a function to activate and deactivate the guest WiFi settings.
I'm using here the RestTemplate pattern from the SpringFramework. This way the FritzBox module can 
also be used on [Android](http://projects.spring.io/spring-android/) if you decide to implement a simple one-button solution on your phone to activate and 
deactivate the guest WiFi network for your friends and visitors.

The code for all this is as simple as this (example from [WifiService](https://code.google.com/p/openpos/source/browse/trunk/openpos-commands/src/main/java/org/openpos/wifi/WifiService.java)):

	FritzTemplate fritzTemplate = new FritzTemplate(new RestTemplate(), "yourfritzpassword");
	fritzTemplate.activateGuestAccess("network-ssid", "wifi-wpa-key");

The call above activates the following features.

![FritzBox setup]({{ BASE_PATH }}/assets/fritzbox_guest.png "FritzBox setup")

#### QR-Code generation

One last thing remains and this is the QR-Code. The above POS printer has a build-in capability to 
generate and print QC-Codes so I directly went for this approach. It would be possible to generate the QR-Code 
in software and then print it as a bitmap but this would make the software unnecessary complicated.
After [some research](http://code.google.com/p/python-escpos/wiki/Usage) and after reading the ESC POS references the code cannot get easier than this:

	out.write(ESCPOS.CENTER);
	out.write(EscPosEncoder.qrCodeModule((byte)4));
	out.write(EscPosEncoder.qrCodeCorrection(CorrectionLevel.L));
	out.write(EscPosEncoder.qrCodeStore(code));
	out.write(EscPosEncoder.qrCodePrint());

Have a look at [EscPosEncoder](https://code.google.com/p/openpos/source/browse/trunk/openpos-print/src/main/java/com/openbravo/pos/printer/escpos/EscPosEncoder.java)
for more details on how to encode the ESC POS commands.

With this knowledge you can generate a nice printout with the name of your location, the QC-Code, the SSID and 
password for those who don't have a QR-Code scanner installed. Since the user wants to access the Internet
you can also add some valuable marketing information like your Facebook/Titter/G+ account.

![QR-Code printout]({{ BASE_PATH }}/assets/qrcode2.jpg "QR-Code printout")

To make the access for the customer as simple as possible I'm using the following pattern for the QR-Code:

	String code = "WIFI:S:<network-ssid>;T:WPA;P:<wifi-wpa-key>;;";

I haven't lookup any official documentation for this but the [ZXing QR-Code builder](http://zxing.appspot.com/generator) generates this pattern and the
barcode scanner is able to recognize it. With one click on the button below you are logged in:

![Barcode Scanner]({{ BASE_PATH }}/assets/qrcode3.jpg "Barcode Scanner")

#### Conclusion

I would say this is a perfect team play for open source software. It would be great to have an official API for
the FritzBox but I can live with the current approach.

With this solution as a foundation I'm thinking about a couponing system or even a QR-Code based game. One challenging 
thing would be to use the WiFi version of a POS printer. Not that I would put the printer into the guest WiFi network,
but I think that using a socket connection would be more interesting that using a Com-port.
Also this would allow to implement a tablet-based version of a POS system. This is a project that has been on 
my road-map for years. ;)

You can find all the components online. My version of OpenbravoPOS is still at [Google code](https://code.google.com/p/openpos/).
I might extract the QR-Code functions into an extra library one day but for the moment 
it is just one class, so it's not worth it.
The library for the FritzBox access is on [github](https://github.com/grundid/fritzbox-java-api).
