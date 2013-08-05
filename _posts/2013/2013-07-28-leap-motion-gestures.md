---
title: Leap Motion Controller Gestures
description: Short overview of the gestures in the JavaScript API for the Leap Montion Controller
tagline: First steps toward minority report
layout: post
category: learning
tags: [leapmotion, english]
author: adrian
repository: https://github.com/grundid/lm-experiments
snapshot: lm_hand.jpg
---

After a long wait the Leap Motion controller finally arrived last week. Based on the many videos online, 
my expectations were quite high: a Kinect like device especially designed to control the UI of your 
desktop computer. Finally I could eat pizza and control the video playback without having to touch 
the keyboard or the mouse. A perfect world so to speak ;) Well, not so fast.

After I installed the device drives and played with the visualization tool everything looked promising. 
The next step was to install the free Touchless app from the Airspace Store to be able to control 
your system UI. In the introduction tutorial you get an impression how to generate gestures like a 
click, swipe or the zoom gesture. Basically you create user inputs by interacting with an invisible 
surface. However what looks quite easy in the demo videos is much harder in real life. The device is 
quite sensitive so it is really hard at the beginning to hit the right icons on the desktop. 
Since there is no gesture for a double click you have to switch the Windows UI to single click deal 
with files. With that you are at least able to launch applications and open files. Since all 
my apps are unaware of the Leap Motion controller you have to rely on the Touchless app to 
simulate touch/mouse events.

Unfortunately this does not work very reliably. Since you are interacting with an invisible surface it is 
quite easy to generate events and gestures that are unintentional. It is especially frustrating to 
see a swipe gesture to end up as a drag and drop of some of your desktop files into the recycle bin.

<iframe width="640" height="480" src="//www.youtube.com/embed/vBrhL5WFOx8?rel=0" frameborder="0" allowfullscreen="allowfullscreen">
</iframe>

Anyway, I still think that this device has huge potential. Since it is a 3D controller maybe it is a 
wrong approach to use it to control a 2D surface. Also I think we should think of new gestures that suit 
the 3D environment and no try to simulate touch gestures on an invisible surface.

To know more I looked at the API for the Leap Motion controller at [js.leapmotion.com](http://js.leapmotion.com). 
It is a simple JavaScript API that you can use in your browser or from a node.js environment. 
It uses a nice approach where it connects via a WebSocket to the device driver and transfers all the 
relevant data in real time as JSON structures. The API web site shows [many examples](http://js.leapmotion.com/examples) 
that can be used as a starting point for your own experiments. 
I went with the [gesture example](https://github.com/grundid/lm-experiments) since I wanted to find 
out how reliable the gesture recognition is.

The [gesture API](http://js.leapmotion.com/api/v0.2.0-beta6/docs#leap-gesture) is able to recognize four gestures: 
-	a swipe, where you move your palm from left to right or from right to left
-	a circle, where you move your finger in a circle motion
-	a screen tap, where you move your finger as if you would want to punch a hole in a dust cloud
-	a key tap, where you move your finger down as if pressing a key on a keyboard.

Both tap gestures have to be a fluid motion, however you have to pause before you start the gesture. 
After some testing the swipe and screen tap gestures can be recognizes with the highest certainty. 
The circle gesture always interferes. I wouldn’t use it in a project right now. The key tap 
gesture can be recognized quite certain if the motion is a clean downward motion. If you move 
your finger too much into the empty space a screen tap gesture can be recognized as well or instead.

Let’s have a short look at the data structures that are delivered on each gesture.
	
	var circle = {
		"center" : [ -8.35835, 162.173, 52.877 ],
		"normal" : [ 0.549754, -0.034748, 0.834604 ],
		"progress" : 1.08131,
		"radius" : 57.2113,
		"id" : 831,
		"handIds" : [ 43 ],
		"pointableIds" : [ 47 ],
		"duration" : 1347543,
		"state" : "stop",
		"type" : "circle"
	};
	var keyTap = {
		"position" : [ -9.38897, 169.063, 55.731 ],
		"direction" : [ -0.141792, -0.988074, -0.0600328 ],
		"progress" : 1,
		"id" : 828,
		"handIds" : [ 43 ],
		"pointableIds" : [ 47 ],
		"duration" : 93555,
		"state" : "stop",
		"type" : "keyTap"
	};
	var screenTap = {
		"position" : [ -3.99414, 152.783, 33.5111 ],
		"direction" : [ 0.19501, -0.331286, -0.923158 ],
		"progress" : 1,
		"id" : 825,
		"handIds" : [ 43 ],
		"pointableIds" : [ 47 ],
		"duration" : 93556,
		"state" : "stop",
		"type" : "screenTap"
	};
	var swipe = {
		"startPosition" : [ -123.199, 111.351, 79.4682 ],
		"position" : [ -8.70678, 128.55, -2.90308 ],
		"direction" : [ 0.822251, 0.117758, -0.556809 ],
		"speed" : 1101.57,
		"id" : 821,
		"handIds" : [ 43 ],
		"pointableIds" : [ 95 ],
		"duration" : 9356,
		"state" : "update",
		"type" : "swipe"
	};

All gestures have a “type” and “state” property. The type property is basically the name of the 
gesture: swipe, circle, screenTap, keyTap. The state can be “start”, “update” or “stop”. 
Only the swipe and circle gestures generate all three states. The tap gestures only generate a single event 
with the state “stop”.

Within the swipe gesture you can use the “direction” property to decide in which direction 
the gesture was made. The property describes an X/Y/Z vector, so the first element is our X axis. 
If this value is positive the motion was from left to right, otherwise it was from right to left. 
With this knowledge you can already start building “cut the rope” games ;)

I hope the Leap Motion will introduce a similar gesture recognition system like on android 
where you can add your own gestures. The screen tap gesture does not feel right for me so 
I’ll try to implement a different approach. My idea is to keep the pointing finger in the 
air while closing the thumb into your palm. This gesture it known as shooting at something, 
but since the Leap Motion controller is not able to recognize fingers on top of each other you 
have to rotate your hand 90 degrees counter-clockwise. Hopefully I’ll be able to present 
you this idea with a data visualization demo soon.