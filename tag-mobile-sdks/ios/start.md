---
layout: page
title: Getting Started with iOS SDK
permalink: /tag-mobile-sdks/ios/start/
---

The PowaTag SDK for iOS is the easiest way to integrate your iOS app with PowaTag.

It enables:

* Triggers - Your app can react to PowaTag tags placed around the environment.
* Workflows - Respond to tags by providing appropriate and contextual user journeys.
* Baskets - Users can add products to a basket for purchase from PowaTag merchants to using your app.
* Payments - Users can easily pay for the products they selected using your app.

<br />

# Requirements

PowaTag SDK for iOS requires a minimum iOS version of 7.

<br />

# Install the SDK with CocoaPods

To use PowaTag SDK in a project, add it as a build dependency and import it.

1. Create a file called "Podfile" at the root of your project, if you don't already have one.

2. If the file is empty, you will need to include at least the version of iOS you are supporting. You may also need to include your workspace name. See the following link for more info on working with CocoaPods: http://guides.cocoapods.org/using/using-cocoapods.html.

    <img src="{{ '/images/powatag_mobile_sdks_ios_start_new_podfile.png' | prepend: site.baseurl }}" />

3. Add the PowaTag SDK dependency to the Podfile:

    <pre>pod 'PowaTagKit'</pre>

    <img src="{{ '/images/powatag_mobile_sdks_ios_start_podfile.png' | prepend: site.baseurl }}" />

4. Save your changes, and then open a terminal window. Enter the following command:

    <pre>pod install</pre>

5. Build your project. Now you can import `PowaTagKit.h` into your project.

<br />

# Initialize the SDK

You need to initialize PowaTag SDK before you can use it. Add a call to `[PowaTagSDK initializeSdkWithApiKey]` from application:didFinishLaunchingWithOptions: in UIApplicationDelegate or viewDidLoad in UIViewController:
	
	- (void)viewDidLoad {
		[PowaTagKit initializeSdkWithApiKey:@“apiKey”
		secret:@“secret”];
	}

	
During development you need to use a non-production endpoint and for this a second initialization method is available:
	
	- (BOOL)application:(UIApplication *)application 
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
	{
		[PowaTagKit initializeSdkWithEndpoint:[PowaTagEndpoint defaultEndpoint]
		apiKey:@“apiKey”
		secret:@“secret”];
    }
			 
<br />

# Importing The Sample App

The **HelloPowaTagSample** app is included with the SDK to provide you with examples of the main PowaTag SDK features. 

You can experiment with the SDK features by importing the app into Xcode.

1. Go to Xcode \| File \| Open

2. Navigate to the folder where you unpacked the SDK, open the Samples folder, and choose the HelloPowaTagSample project. Click OK to open it.

3. Build the sample project.

The samples have a project dependency rather than a central repository dependency via CocoaPods. This is so that when a local copy of the SDK gets updates, the samples reflect the changes.

<br />

# Next Steps

After you install PowaTag SDK for iOS, you can see:

* [Login]({{site.baseurl}}/tag-mobile-sdks/ios/login/)
* [Profile]({{site.baseurl}}/tag-mobile-sdks/ios/profile/)
* [Triggers]({{site.baseurl}}/tag-mobile-sdks/ios/triggers/)
* [Workflows]({{site.baseurl}}/tag-mobile-sdks/ios/workflows/)
* [Baskets]({{site.baseurl}}/tag-mobile-sdks/ios/baskets/)
* [Campaigns]({{site.baseurl}}/tag-mobile-sdks/ios/campaigns/)
* [Acts]({{site.baseurl}}/tag-mobile-sdks/ios/acts/)
* [Payments]({{site.baseurl}}/tag-mobile-sdks/ios/payments/)

<br />

# Install the SDK Manually

1. Extract the SDK Zip and copy the PowaTagKit.framework into your Xcode project.

2. Build your project. Now you can import `PowaTagKit.h` into your app.
