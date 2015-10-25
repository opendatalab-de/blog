---
title: Handle 3D Touch quick actions with UITabBarController and UINavigationController
description: Short description how to handle ShortcutItem quick actions and pass data to a UITabBarController and UINavigationController hierarchy
tagline:
layout: post
category: hack
tags: [english, ios]
author: adrian
snapshot: 3d-touch-weddian.png
---

In our Wedding Planer app we recently introduced 3D Touch quick actions from the home screen. 
On an iPhone with 3D Touch you can now quickly reach four of the most important sections of
the app directly from the home screen. 

![Home Screen]({{ BASE_PATH }}/assets/3d-touch-weddian.png "Home Screen")

In this blog post I want to show you, how we implemented this function in our controller hierarchy. As a root
view controller we use a UITabBarController and then on each tab we use a UINavigationController. With the
quick actions we want to give users the possibility to quickly access the second ViewController in each tab.
To accomplish this the app has to be able to switch the tab and then perform a segue to the second controller.
This way we can keep the hierarchy within the app and the user can easily move back and forth 
in the app after using the quick action.


![Weddian]({{ BASE_PATH }}/assets/weddian-home.jpg "Weddian")

First let's have a look at our definition in the Info.plist file. Here we use the UIApplicationShortcutItemType key to
encode the tab number and the first segue to perform. We decided not to use the UIApplicationShortcutItemUserInfo dictionary 
for this kind of data because this should contain user data for dynamic quick actions.

{% highlight xml %}

    <key>UIApplicationShortcutItems</key>
	<array>
		<dict>
			<key>UIApplicationShortcutItemTitle</key>
			<string>Action Title</string>
			<key>UIApplicationShortcutItemType</key>
			<string>tab1:segueName</string>
		</dict>
	</array>

{% endhighlight %}

In the second step we have to implement the performActionForShortcutItem method in the UIApplicationDelegate.
Since we have a fixed hierarchy in our app and use a schema for the ShortcutItemType we can create a nice
implementation that opens a specific tab and if a segue is part of the type string also performs the segue on the first
controller.

{% highlight objective-c %}

    - (void)application:(UIApplication *)application performActionForShortcutItem:(UIApplicationShortcutItem *)shortcutItem completionHandler:(void (^)(BOOL))completionHandler {
    
        UITabBarController *rootController = (UITabBarController *)self.window.rootViewController;
    
        NSString *type = shortcutItem.type;
        NSArray *types = [type componentsSeparatedByString:@":"];
    
        NSString *tabNo = [((NSString*)types[0]) substringFromIndex:3];    
        [rootController setSelectedIndex:tabNo.integerValue];
        UINavigationController *navController = rootController.selectedViewController;
        [navController popToRootViewControllerAnimated:false];
    
        if ([types count] > 1) {
            NSString *segue = (NSString*)types[1];
            if (segue != nil) {
                UIViewController *firstViewController = navController.viewControllers[0];
                [firstViewController performSegueWithIdentifier:segue sender:nil];
            }
        }
    }

{% endhighlight %}

With this implementation you can easily access all your second level view controller in a tab bar app from a home screen
quick action.
