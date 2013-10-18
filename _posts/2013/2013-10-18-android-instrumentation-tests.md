---
title: Android Instrumentation Tests
description: Multi module setup with Android instrumentation tests
tagline: 
layout: post
category: hack
tags: [english, android]
author: adrian
snapshot: android.png
---

We are currently working on an [Android App](https://play.google.com/store/apps/details?id=de.grundid.hp24) 
in collaboration with the guys from Hochzeitsportal24. 
Yes, it’s a wedding planner ;)

Anyway, since we use Maven for all our Java projects, we also went with it for this project. 
I had some experience with the [android-maven-plugin](http://code.google.com/p/maven-android-plugin/) because 
I used it with two of my [prior Android Apps](https://play.google.com/store/apps/developer?id=Adrian+Stabiszewski).

Our app setup consists of an android app module and an instrumentation test module. 
Besides these two modules, we have a third module that we call the core module. 
It contains only android independent code and unit tests for this code. This setup works 
great with maven on the command line and on the Jenkins build server, however there are some 
issues if you use it in Eclipse.

Here the m2e plugin handles the build path of your projects and this leads to a problem where 
the classes from the core module get included in the instrumentation test APK. As a result of 
this you cannot launch the instrumentation tests from Eclipse because the test runner fails 
with an exception like this:

	java.lang.IllegalAccessError: Class ref in pre-verified class resolved to unexpected implementation

Prior to this exception you can see several ClassNotFoundExceptions which make you believe 
that you are missing some jar libraries in your class path. However, this is a totally wrong direction. 

The true problem here is the last exception. It tells you that you have two instances of the 
same class in your test scenario. This happens when one version is in your app APK and a 
second version is in the test APK. To verify this you can use the [dex2jar](http://code.google.com/p/dex2jar/) tool
and convert the classes.dex file to a jar file and then check the contents of this file.

This happens in our setup due to the fact that we need the classes from the core module in 
our app and in the instrumentation tests. Since all modules are under a heavy development 
we use SNAPSHOT dependencies. And now m2e kicks in and resolves the SNAPSHOT dependencies 
into project dependencies. This way the classes from the core module appear in the test module 
and get added to the test APK.
I’ve tried several solutions and actually none of them really works in the long term. 
I’ll document them here so you might choose one that hurts you less.

1.	Declare the core module dependency with scope “provided” in the test module pom.xml. This works from the command line but not in Eclipse since m2e resolves the SNAPSHOT dependency anyway.
2.	Declare the core module as optional in the app module pom.xml. This actually works in Eclipse but it fails on the command line because here the compiler cannot find the classes.
3.	Uncheck the “Maven Dependencies” from the “Order and Export” tab in Java build path config. This solves the problem in Eclipse but only until the next time you hit Maven/Update Project…

Right now I’m using the third option since it is somehow predictable and we rely on a clean 
build on the Jenkins server. One possible long term solution might be to look into the Android 
Maven Plugin and change it in a way where it hides the “provided” dependencies from m2e.
