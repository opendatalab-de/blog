---
title: Peer-to-peer communication using NFC in Android 4.4
description: Using the host-based card emulation mode for peer-to-peer communication.
tagline: 
layout: post
category: hack
tags: [english, android, nfc]
author: adrianenglish
repository: https://github.com/grundid/host-card-emulation-sample
snapshot: hce.jpg
---

With the new Host-based card emulation Android opened up a possibility for bidirectional peer-to-peer
communication using NFC. Since I now have access to a Nexus 5 and Nexus 7 both running Android 
Version 4.4 I gave it a try.

Based on my [previous example using the ACR122 as the card reader](/hack/2013/11/07/android-host-card-emulation-with-acr122) 
I was able to quickly modify it to adapt to this new functionality.

#### EnableReaderMode

There are basically two things you have to do to be able to establish an bidirectional NFC connection.
Firstly, configure the host-based card emulation mode like described in [one of my previous blog posts](/hack/2013/11/07/android-host-card-emulation-with-acr122).
Secondly, create an Activity that will [enable the new Reader-Mode in Android 4.4](http://developer.android.com/reference/android/nfc/NfcAdapter.html#enableReaderMode%28android.app.Activity,%20android.nfc.NfcAdapter.ReaderCallback,%20int,%20android.os.Bundle%29) 
and create a reader callback that will handle the discovered tag as an IsoDep tag.

The code is really simple. For a full example, please have a look at the [github project](https://github.com/grundid/host-card-emulation-sample).

	@Override
	public void onResume() {
		super.onResume();
		nfcAdapter.enableReaderMode(this, this, NfcAdapter.FLAG_READER_NFC_A | NfcAdapter.FLAG_READER_SKIP_NDEF_CHECK,
				null);
	}

	@Override
	public void onPause() {
		super.onPause();
		nfcAdapter.disableReaderMode(this);
	}

	@Override
	public void onTagDiscovered(Tag tag) {
		IsoDep isoDep = IsoDep.get(tag);
		IsoDepTranceiver transceiver = new IsoDepTransceiver(isoDep, this);
		Thread thread = new Thread(transceiver);
		thread.start();
	}


In your transceiver thread you first connect to the tag and then issue a SELECT AID APDU using your Application ID.
This looks like this:

	private static final byte[] CLA_INS_P1_P2 = { 0x00, (byte)0xA4, 0x04, 0x00 };
	private static final byte[] AID_ANDROID = { (byte)0xF0, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06 };
	
	private byte[] createSelectAidApdu(byte[] aid) {
		byte[] result = new byte[6 + aid.length];
		System.arraycopy(CLA_INS_P1_P2, 0, result, 0, CLA_INS_P1_P2.length);
		result[4] = (byte)aid.length;
		System.arraycopy(aid, 0, result, 5, aid.length);
		result[result.length - 1] = 0;
		return result;
	}

	@Override
	public void run() {
		int messageCounter = 0;
		try {
			isoDep.connect();
			byte[] response = isoDep.transceive(createSelectAidApdu(AID_ANDROID));
			while (isoDep.isConnected() && !Thread.interrupted()) {
				String message = "Message from IsoDep " + messageCounter++;
				response = isoDep.transceive(message.getBytes());
				onMessageReceived.onMessage(response);
			}
			isoDep.close();
		}
		catch (IOException e) {
			onMessageReceived.onError(e);
		}
	}

#### Conclusion

I hope this example will allow you to write some awesome NFC apps. Please check the full 
example at my [GitHub repo](https://github.com/grundid/host-card-emulation-sample) and 
comment if you have any questions.

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<!-- Unter Blog Content Responsive -->
<ins class="adsbygoogle"
     style="display:block"
     data-ad-client="ca-pub-4734442255165118"
     data-ad-slot="9649993785"
     data-ad-format="auto"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script>