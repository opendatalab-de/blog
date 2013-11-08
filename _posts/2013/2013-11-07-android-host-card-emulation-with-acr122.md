---
title: Android Host-based Card Emulation connected to ACR122U
description: Using a ACR122U to connect to an Android device running host-based card emulation
tagline: 
layout: post
category: hack
tags: [english, android, nfc]
author: adrian
repository: https://github.com/grundid/nfctools-examples
snapshot: hce.jpg
---

Last week Google released the new Android 4.4 version and I was quite happy to see some 
updates to the NFC implementation. The biggest change is the new 
[Host-based Card Emulation](http://developer.android.com/guide/topics/connectivity/nfc/hce.html) mode. 
This opens up the possibility of Peer-to-Peer communication over NFC.

I immediately ordered the new Nexus 5 to be able to hack on this new feature. Yesterday the phone arrived 
and today I was able to invest a few hours with reading docs and writing some lines of code.
Good news everyone: it’s working quite nice.

First, I would like to give you some background info how this is all working. If you just want to 
see the code, scroll down please.

#### ISO/IEC 7816-4 card emulation

ISO/IEC 7816-4 tags are organized into applications that can be individually selected. Each 
application has a name or a file ID. You can connect to an application by issuing 
a SELECT command with the appropriate name. Android implements this system basically 
by saying that each Android application can act as one or more applications on a 
tag. Since the application name or file ID should be unique this is quite cool, 
because now your Android smartphone becomes one big tag.

This system can even [coexist with secure element based card emulations](http://developer.android.com/guide/topics/connectivity/nfc/hce.html#Coexistence) but I don’t want 
to dive into this because I haven’t done anything with it so far.

The steps to establish the connection are really quite easy. Using the ACR122U desktop 
reader (PN532 NFC chip) I first issued an InListPassiveTarget command and once the 
target appeared in range I directly send a SELECT APDU using the DataExchange command. 
From here on you simply continue to send DataExchange commands until you’re done with the 
whole communication process.

In hex this looks like this (InListPassiveTarget):

	D4 4A 01 00
	
Once the target is in range you will get the following target data:

	01 0004 60 04 089D64A2 0575807002
	
	01 = Target No
	0004 = SENS_RES
	60 = SEL_RES (please have a look at the HCE documentation how to compare the value)
	04 = length of the NFCID
	089D64A2 = random NFCID, it changes with every connection
	0575807002 = ATS

Now you can simply send a SELECT APDU to connect to your app on the phone:

	D44001 00A4040007F001020304050600
	
The data out part is as follows:

	00 = CLAss
	A4 = INStruction, SELECT
	04 = P1, select by name
	00 = P2
	07 = length of the application name
	F0010203040506 = application name as defined in the manifest by the AID-filter

Your [HostApduService](http://developer.android.com/guide/topics/connectivity/nfc/hce.html#ImplementingService) 
will receive the above message as the first APDU. From now on you can send 
any data you want. I noticed that this doesn’t even have to be encoded as APDU.

Here is some code I’ve compiled for this demo.

The IsoDepTamaCommunicator is the part on the desktop side what will use the NFCTools 
and establish the IsoDep connection to the Android device. For the complete example please have a look at the 
[org.nfctools.examples.hce package](https://github.com/grundid/nfctools-examples/tree/master/src/main/java/org/nfctools/examples/hce).

	public class IsoDepTamaCommunicator extends AbstractTamaCommunicator {
	
		private Logger log = LoggerFactory.getLogger(getClass());
		private int messageCounter = 0;
		private static final byte[] CLA_INS_P1_P2 = { 0x00, (byte)0xA4, 0x04, 0x00 };
		private static final byte[] AID_ANDROID = { (byte)0xF0, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06 };
	
		public IsoDepTamaCommunicator(ByteArrayReader reader, ByteArrayWriter writer) {
			super(reader, writer);
		}
	
		private byte[] createSelectAidApdu(byte[] aid) {
			byte[] result = new byte[6 + aid.length];
			System.arraycopy(CLA_INS_P1_P2, 0, result, 0, CLA_INS_P1_P2.length);
			result[4] = (byte)aid.length;
			System.arraycopy(aid, 0, result, 5, aid.length);
			result[result.length - 1] = 0;
			return result;
		}
	
		public void connectAsInitiator() throws IOException {
			while (true) {
				InListPassiveTargetResp inListPassiveTargetResp = 
					sendMessage(new InListPassiveTargetReq((byte)1, (byte)0, new byte[0]));
				if (inListPassiveTargetResp.getNumberOfTargets() > 0) {
					log.info("TargetData: " + 
						NfcUtils.convertBinToASCII(inListPassiveTargetResp.getTargetData()));
					if (inListPassiveTargetResp.isIsoDepSupported()) {
						log.info("IsoDep Supported");
						byte[] selectAidApdu = createSelectAidApdu(AID_ANDROID);
						DataExchangeResp resp = 
							sendMessage(
								new DataExchangeReq(inListPassiveTargetResp.getTargetId(),
								false, selectAidApdu, 0, selectAidApdu.length));
						String dataIn = new String(resp.getDataOut());
						log.info("Received: " + dataIn);
						if (dataIn.startsWith("Hello")) {
							exchangeData(inListPassiveTargetResp);
						}
					}
					else {
						log.info("IsoDep NOT Supported");
					}
					break;
				}
				else {
					try {
						Thread.sleep(100);
					}
					catch (InterruptedException e) {
						throw new RuntimeException(e);
					}
				}
			}
		}
	
		private void exchangeData(InListPassiveTargetResp inListPassiveTargetResp) throws IOException {
			DataExchangeResp resp;
			String dataIn;
			while (true) {
				byte[] dataOut = ("Message from desktop: " + messageCounter++).getBytes();
				resp = sendMessage(
					new DataExchangeReq(inListPassiveTargetResp.getTargetId(), false, dataOut, 0,
					dataOut.length));
				dataIn = new String(resp.getDataOut());
				log.info("Received: " + dataIn);
			}
		}
	}
	
On the Android side you have a simple HostApduService as defined in the HCE documentation. 
The complete source code is in the [host-card-emulation-sample repository](https://github.com/grundid/host-card-emulation-sample).

	public class MyHostApduService extends HostApduService {
	
		private int messageCounter = 0;
	
		@Override
		public byte[] processCommandApdu(byte[] apdu, Bundle extras) {
			if (selectAidApdu(apdu)) {
				Log.i("HCEDEMO", "Application selected");
				return getWelcomeMessage();
			}
			else {
				Log.i("HCEDEMO", "Received: " + new String(apdu));
				return getNextMessage();
			}
		}
	
		private byte[] getWelcomeMessage() {
			return "Hello Desktop!".getBytes();
		}
	
		private byte[] getNextMessage() {
			return ("Message from android: " + messageCounter++).getBytes();
		}
	
		private boolean selectAidApdu(byte[] apdu) {
			return apdu.length >= 2 && apdu[0] == (byte)0 && apdu[1] == (byte)0xa4;
		}
	
		@Override
		public void onDeactivated(int reason) {
			Log.i("HCEDEMO", "Deactivated: " + reason);
		}
	}
	

#### Pitfalls

During development I first assumed I would have to use a common CLA for 
the APDU so I stared with the 0x90 used in DesFire cards. But this led to the following error message:

	E/BrcmNfcNfa(1187): CET4T: Unsupported Class byte (0x90)
	
So I looked at the [Android source code](https://android.googlesource.com/platform/external/libnfc-nci/+/master/src/nfc/include/tags_defs.h)
and found out that the correct CLA is 0x00. Also the expected P1 parameter can be found in the source code.


#### NFCTools Examples 

If you want to try this out you can clone the 
[host-card-emulation-sample](https://github.com/grundid/host-card-emulation-sample) GitHub repository 
and compile the Android app for your device. Android 4.4 is required for this to work.
Then for the desktop side just download the latest version of the 
nfctools-examples.jar from [nfctools-examples releases](https://github.com/grundid/nfctools-examples/releases)

Launch the examples with the following command:

	java -cp nfctools-examples.jar org.nfctools.examples.hce.HceDemo
	
<iframe width="640" height="480" src="//www.youtube.com/embed/y_AYWqUtb_0?rel=0" frameborder="0" allowfullscreen="allowfullscreen">
</iframe>

	
#### Conclusion

The Host-based Card Emulation is really easy to use. Compared to the LLCP/SNEP implementation of Android Beam it is
way less error prone and gives you much faster responsiveness.
Using this HCE mode for P2P communication is of course just a hack. I can only hope that the Android team will
allow access to the SNEP stack in one the coming releases.

Please also note that the amount of data that can be transmitted with one DataExchange 
command is limited to around 200 bytes. If you want to transfer larger amounts of data you have to 
chunk it yourself into smaller pieces.

Another thing is the security of this implementation. Basically you cannot trust the other party as anyone can
create an Android app or a desktop app using your AID. Please also refer to 
the [HCE and Security](http://developer.android.com/guide/topics/connectivity/nfc/hce.html#HceSecurity) section 
of the documentation.

If you have any questions regarding nfctools please come by our 
[discussion group](https://groups.google.com/forum/?fromgroups#!forum/nfc-developers).

	